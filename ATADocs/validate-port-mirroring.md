---
title: Überprüfen der Port Spiegelung in Advanced Threat Analytics
description: Beschreibt, wie die ordnungsgemäße Konfiguration der Portspiegelung überprüft wird.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: ebd41719-c91a-4fdd-bcab-2affa2a2cace
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 7677cbdb0f6b236d0be4230a1166026053ac2acc
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2020
ms.locfileid: "94689563"
---
# <a name="validate-port-mirroring"></a>Überprüfen der Portspiegelung

[!INCLUDE [Banner for top of topics](includes/banner.md)]

> [!NOTE]
> Dieser Artikel ist für Sie nur interessant, wenn Sie ATA-Gateways anstelle von ATA-Lightweight-Gateways bereitstellen. Informationen dazu, ob Sie ATA-Gateways verwenden müssen, finden Sie unter [Auswählen der richtigen Gateways für Ihre Bereitstellung](ata-capacity-planning.md#choosing-the-right-gateway-type-for-your-deployment).

Die folgenden Schritte führen Sie durch das Verfahren, mit dem Sie die ordnungsgemäße Konfiguration der Portspiegelung überprüfen. Damit ATA ordnungsgemäß funktioniert, muss das ATA-Gateway den Datenverkehr zum und vom Domänencontroller anzeigen können. Als primäre Datenquelle verwendet ATA eine ausführliche Paketüberprüfung (Deep Packet Inspection) des Netzwerkdatenverkehrs zu und von den Domänencontrollern. Damit ATA den Netzwerkdatenverkehr anzeigen kann, muss die Portspiegelung konfiguriert sein. Die Portspiegelung kopiert den Datenverkehr von einem Port (dem Quellport) zu einem anderen Port (dem Zielport).

## <a name="validate-port-mirroring-using-a-windows-powershell-script"></a>Überprüfen von Portspiegelung mit einem Windows PowerShell-Skript

1. Speichern Sie den Text dieses Skripts in einer Datei namens *ATAdiag.ps1*.
1. Führen Sie dieses Skript auf dem ATA-Gateway aus, das Sie überprüfen möchten.
Das Skript generiert ICMP-Datenverkehr vom ATA-Gateway zum Domänencontroller und sucht nach diesem Datenverkehr an der erfassenden Netzwerkkarte auf dem Domänencontroller.
Stellt das ATA-Gateway ICMP-Datenverkehr mit einer Ziel-IP-Adresse fest, die mit der DC-IP-Adresse identisch ist, die Sie in der ATA-Konsole eingegeben haben, geht es davon aus, dass Portspiegelung konfiguriert ist.

Beispiel, wie das Skript ausgeführt wird:

```powershell
# ATAdiag.ps1 -CaptureIP n.n.n.n -DCIP n.n.n.n -TestCount n
param([parameter(Mandatory=$true)][string]$CaptureIP, [parameter(Mandatory=$true)][string]$DCIP, [int]$PingCount = 10)

# Set variables
$ErrorActionPreference = "stop"
$starttime = get-date
$byteIn = new-object byte[] 4
$byteOut = new-object byte[] 4
$byteData = new-object byte[] 4096  # size of data

$byteIn[0] = 1  # for promiscuous mode
$byteIn[1-3] = 0
$byteOut[0-3] = 0

# Convert network data to host format
function NetworkToHostUInt16 ($value)
{
    [Array]::Reverse($value)
    [BitConverter]::ToUInt16($value,0)
}
function NetworkToHostUInt32 ($value)
{
    [Array]::Reverse($value)
    [BitConverter]::ToUInt32($value,0)
}
function ByteToString ($value)
{
    $AsciiEncoding = new-object system.text.asciiencoding
    $AsciiEncoding.GetString($value)
}

Write-Host "Testing Port Mirroring..." -ForegroundColor Yellow
Write-Host ""
Write-Host "Here is a summary of the connection we will test." -ForegroundColor Yellow

# Initialize a first ping connection
Test-Connection -Count 1 -ComputerName $DCIP -ea SilentlyContinue
Write-Host ""
Write-Host "Press any key to continue..." -ForegroundColor Red
[void][System.Console]::ReadKey($true)
Write-Host ""
Write-Host "Sending ICMP and Capturing data..." -ForegroundColor Yellow

# Open a socket
$socket = new-object system.net.sockets.socket([Net.Sockets.AddressFamily]::InterNetwork,[Net.Sockets.SocketType]::Raw,[Net.Sockets.ProtocolType]::IP)

# Include the IP header
$socket.setsocketoption("IP","HeaderIncluded",$true)
$socket.ReceiveBufferSize = 10000
$ipendpoint = new-object system.net.ipendpoint([net.ipaddress]"$CaptureIP",0)
$socket.bind($ipendpoint)

# Enable promiscuous mode
[void]$socket.iocontrol([net.sockets.iocontrolcode]::ReceiveAll,$byteIn,$byteOut)

# Initialize test variables
$tests = 0
$TestResult = "Noise"
$OneSuccess = 0

while ($tests -le $PingCount)
{
    if (!$socket.Available)  # see if any packets are in the queue
    {
        start-sleep -milliseconds 500
        continue
    }

    # Capture traffic
    $rcv = $socket.receive($byteData,0,$byteData.length,[net.sockets.socketflags]::None)

    # Decode the header so we can read ICMP
    $MemoryStream = new-object System.IO.MemoryStream($byteData,0,$rcv)
    $BinaryReader = new-object System.IO.BinaryReader($MemoryStream)

    # Set IP version & header length
    $VersionAndHeaderLength = $BinaryReader.ReadByte()

    # TOS
    $TypeOfService= $BinaryReader.ReadByte()

    # More values, and the Protocol Number for ICMP traffic
    # Convert network format of big-endian to host format of little-endian
    $TotalLength = NetworkToHostUInt16 $BinaryReader.ReadBytes(2)
    $Identification = NetworkToHostUInt16 $BinaryReader.ReadBytes(2)
    $FlagsAndOffset = NetworkToHostUInt16 $BinaryReader.ReadBytes(2)
    $TTL = $BinaryReader.ReadByte()
    $ProtocolNumber = $BinaryReader.ReadByte()
    $Checksum = [Net.IPAddress]::NetworkToHostOrder($BinaryReader.ReadInt16())

    # The source and destination IP addresses
    $SourceIPAddress = $BinaryReader.ReadUInt32()
    $DestinationIPAddress = $BinaryReader.ReadUInt32()

    # The source and destimation ports
    $sourcePort = [uint16]0
    $destPort = [uint16]0

    # Close the stream reader
    $BinaryReader.Close()
    $memorystream.Close()

    # Cast DCIP into an IPaddress type
    $DCIPP = [ipaddress] $DCIP
    $DestinationIPAddressP = [ipaddress] $DestinationIPAddress

    #Ping the DC at the end after starting the capture
    Test-Connection -Count 1 -ComputerName $DCIP -ea SilentlyContinue | Out-Null

    # This is the match logic - check to see if Destination IP from the Ping sent matches the DCIP entered by in the ATA Console
    # The only way the ATA Gateway should see a destination of the DC is if Port Spanning is configured

    if ($DestinationIPAddressP -eq $DCIPP)  # is the destination IP eq to the DC IP?
    {
        $TestResult = "Port Spanning success!"
        $OneSuccess = 1
    } else {
        $TestResult = "Noise"
    }

    # Put source, destination, test result in Powershell object
    new-object psobject | add-member -pass noteproperty CaptureSource $([system.net.ipaddress]$SourceIPAddress) | add-member -pass noteproperty CaptureDestination $([system.net.ipaddress]$DestinationIPAddress) | Add-Member -pass NoteProperty Result $TestResult | Format-List | Out-Host
    #Count tests
    $tests ++
}

if ($OneSuccess -eq 1)
{
    Write-Host "Port Spanning Success!" -ForegroundColor Green
    Write-Host ""
    Write-Host "At least one packet which was addressed to the DC, was picked up by the Gateway." -ForegroundColor Yellow
    Write-Host "A little noise is OK, but if you don't see a majority of successes, you might want to re-run." -ForegroundColor Yellow
} else {
    Write-Host "No joy, all noise.  You may want to re-run, increase the number of Ping Counts, or check your config." -ForegroundColor Red
}

Write-Host ""
Write-Host "Press any key to continue..." -ForegroundColor Red
[void][System.Console]::ReadKey($true)
```

## <a name="validate-port-mirroring-using-net-mon"></a>Überprüfen von Portspiegelung mit Netzwerkmonitor (Network Monitor)
1. Installieren Sie [Microsoft-Netzwerkmonitor 3,4](https://www.microsoft.com/download/details.aspx?id=4865) auf dem ATA-Gateway, das Sie überprüfen möchten.

    > [!IMPORTANT]
    > Installieren Sie auf dem ATA-Gateway nicht Microsoft Message Analyzer oder ein andere Software zur Erfassung des Datenverkehrs.

1. Öffnen Sie Netzwerkmonitor, und erstellen Sie eine neue Registerkarte für die Erfassung.

    1. Wählen Sie nur den Netzwerkadapter **Erfassung** oder den Netzwerkadapter aus, der mit dem als Ziel der Portspiegelung konfigurierten Switchport verbunden ist.

    1. Stellen Sie sicher, dass „P-Modus“ aktiviert ist.

    1. Klicken Sie auf **Neue Erfassung**.

        ![Abbildung des Erstellens einer neuen Registerkarte für die Erfassung](media/ATA-Port-Mirroring-Capture.jpg)

1. Geben Sie im Fenster „Anzeigefilter“ den folgenden Filter ein: **KerberosV5 oder LDAP**. Klicken Sie dann auf **Übernehmen**.

    ![Abbildung des Filters „KerberosV5 oder LDAP“](media/ATA-Port-Mirroring-filter-settings.jpg)

1. Klicken Sie auf **Start**, um die Erfassungssitzung zu starten. Wenn der Datenverkehr zum und vom Domänencontroller nicht angezeigt wird, überprüfen Sie die Konfiguration der Portspiegelung.

    ![Abbildung Starten der Erfassungssitzung](media/ATA-Port-Mirroring-Capture-traffic.jpg)

    > [!NOTE]
    > Es ist wichtig, dass Ihnen der Datenverkehr zu und von den Domänencontrollern angezeigt wird.

1. Wenn Ihnen nur Datenverkehr in eine Richtung angezeigt wird, sollten Sie mit Unterstützung Ihres Netzwerk- oder Virtualisierungsteams eine Problembehandlung für die Konfiguration der Portspiegelung durchführen.

## <a name="see-also"></a>Weitere Informationen

- [Konfigurieren der Portspiegelung](configure-port-mirroring.md)
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
