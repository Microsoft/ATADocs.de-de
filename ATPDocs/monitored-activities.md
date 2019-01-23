---
title: Von Azure ATP überwachte Domänenaktivitäten | Microsoft-Dokumentation
description: Beschreibt jeden Aktivitätstyp, der von Azure Advanced Threat Protection überwacht wird.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/13/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 37d1a032-65e7-4a89-be0b-c3f9cc2bacdb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 16951313f18be44a3c42a0f6b2281963d867c7b4
ms.sourcegitcommit: 6a0ac21f59e72db8615811da2c886f54cf3727f5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/13/2019
ms.locfileid: "54249894"
---
*Gilt für: Azure Advanced Threat Protection*



# <a name="azure-atp-monitored-activities"></a>Von Azure ATP überwachte Aktivitäten

Azure Advanced Threat Protection überwacht Informationen, die aus dem Active Directory, den Netzwerkaktivitäten und Ereignisaktivitäten Ihrer Organisation generiert wurden, um verdächtige Aktivitäten zu erkennen. Anhand der überwachten Aktivitätsinformationen kann Azure ATP Ihnen helfen, die Gültigkeit der einzelnen potenziellen Bedrohungen zu bestimmen sowie sie richtig zu selektieren und entsprechend zu reagieren. 

Im Fall einer gültigen Bedrohung oder von **richtig positiv** ermöglicht Azure ATP es Ihnen, den Umfang der Sicherheitsverletzung für jeden Incident zu ermitteln, zu untersuchen, welche Entitäten beteiligt sind, und zu bestimmen, wie sie korrigiert werden können.

Die von Azure ATP überwachten Informationen werden in Form von Aktivitäten angezeigt. Azure ATP unterstützt zurzeit die Überwachung der folgenden Aktivitätstypen:

> [!NOTE] 
> - Dieser Artikel ist für alle Azure ATP-Sensortypen relevant.
>- Von Azure ATP überwachte Aktivitäten werden auf der Profilseite sowohl für Benutzer als auch für Computer angezeigt. 
 

## <a name="monitored-user-activities-user-account-ad-attribute-changes"></a>Überwachte Benutzeraktivitäten: Änderungen am AD-Attribut für Benutzerkonto

|Überwachte Aktivität|Beschreibung|
|---------------------|------------------|
|Kontostatus „Eingeschränkte Delegierung“ geändert |Der Kontostatus ist jetzt für Delegierung aktiviert oder deaktiviert.|
|Konto-SPNs „Eingeschränkte Delegierung“ geändert | Die eingeschränkte Delegierung beschränkt die Dienste, für die der angegebene Server im Auftrag des Benutzers agieren kann.|
|„Konto deaktiviert“ geändert |Gibt an, ob ein Konto aktiviert oder deaktiviert ist.|
|Konto abgelaufen|Datum, an dem das Konto abläuft.|
|Ablaufzeit für Konto geändert |Änderung in das Datum, an dem das Konto abläuft.|
|„Konto gesperrt“ geändert|Änderung in das Datum, an dem das Konto abläuft.|
|Kontokennwort geändert|Benutzer hat sein Kennwort geändert.|
|Kontokennwort abgelaufen |Kennwort des Benutzers ist abgelaufen.|
|„Kontokennwort läuft nie ab“ geändert |Kennwort des Benutzer wurde geändert, sodass es nie abläuft.|
|„Kein Kontokennwort erforderlich“ geändert |Benutzerkonto wurde geändert, sodass Anmeldung mit einem leeren Kennwort zulässig ist.|
|„Smartcard für Konto erforderlich“ geändert  |Konto wurde geändert, sodass Benutzer aufgefordert werden, sich auf einem Gerät mit einer Smartcard anzumelden.|
|Vom Konto unterstützte Verschlüsselungstypen geändert |Von Kerberos unterstützte Verschlüsselungstypen wurden geändert (Typen: Des, AES 129, AES 256)|
|UPN-Name von Konto geändert  |Der Benutzerprinzipalname wurde geändert.|
|Gruppenmitgliedschaft geändert  |Benutzer wurde zu/aus einer Gruppe hinzugefügt/gelöscht, und zwar von einem anderen Benutzer oder ihm selbst.|
|Benutzer-E-Mail geändert|E-Mail-Attribut des Benutzers wurde geändert.|
|Benutzer-Manager geändert|Manager-Attribut des Benutzers wurde geändert.|
|Benutzer-Telefonnummer geändert|Telefonnummer-Attribut des Benutzers wurde geändert.|
|Benutzertitel geändert |Title-Attribut des Benutzers wurde geändert.|

## <a name="monitored-user-activities-ad-security-principal-operations"></a>Überwachte Benutzeraktivitäten: Vorgänge für AD-Sicherheitsprinzipal

|Überwachte Aktivität|Beschreibung|
|---------------------|------------------|
|Sicherheitsprinzipal erstellt |Konto wurde erstellt (Benutzer- und Computerkonto).|
|„Sicherheitsprinzipal gelöscht“ geändert  |Konto wurde gelöscht/wiederhergestellt (Benutzer- und Computerkonto).|
|Anzeigename von Sicherheitsprinzipal geändert   |Anzeigename des Kontos wurde von X in Y geändert.|
|Name von Sicherheitsprinzipal geändert  |Kontonamenattribut wurde geändert.|
|Pfad von Sicherheitsprinzipal geändert  |Distinguished Name für Konto wurde von X in Y geändert.|
|SAM-Name von Sicherheitsprinzipal geändert |SAM-Name wurde geändert (SAM ist der Anmeldename zur Unterstützung von Clients und Servern, auf denen frühere Versionen des Betriebssystems ausgeführt werden).|

## <a name="monitored-user-activities-domain-controller-based-user-operations"></a>Überwachte Benutzeraktivitäten: Domänencontroller-basierte Benutzervorgänge

|Überwachte Aktivität|Beschreibung|
|---------------------|------------------|
|Verzeichnisdienstreplikation  |Benutzer hat versucht, den Verzeichnisdienst zu replizieren.|
|DNS-Abfrage  |Der Typ der Benutzerabfrage, die für den Domänencontroller ausgeführt wurde (**AXFR**,**TXT**, **MX**, **NS**, **SRV**, **ANY**, **DNSKEY**).|
|Abrufen von privaten Daten  |Benutzer hat versucht, private Daten mithilfe des LSARPC-Protokolls abzufragen, oder diese Abfrage ist ihm gelungen.|
|Erstellen eines Diensts   |Benutzer hat versucht, einen bestimmten Dienst per Remotezugriff auf einem Remotecomputer zu erstellen.|
|SMB-Sitzungsenumeration   |Benutzer hat versucht, alle Benutzer mit offenen SMB-Sitzungen auf den Domänencontrollern aufzulisten.|
|Kopieren von SMB-Dateien| Vom Benutzer mit SMB kopierte Dateien|
|SAMR-Abfrage   |Benutzer hat eine SAMR-Abfrage ausgeführt.|
|Aufgabenplanung  |Benutzer hat versucht, Aufgabe X per Remotezugriff auf einem Remotecomputer zu planen.|
|Wmi-Ausführung  |Benutzer hat versucht, eine WMI-Methode per Remotezugriff auszuführen.|

## <a name="monitored-user-activities-login-operations"></a>Überwachte Benutzeraktivitäten: Anmeldevorgänge

|Anmeldetyp|Überwachte Aktivität|Beschreibung|
|---------------------|---------------------|------------------|
|Anmeldetyp 2|Überprüfen der Anmeldeinformationen  |Authentifizierungsereignis beim Domänenkonto mit den Authentifizierungsmethoden NTLM und Kerberos.|
|Anmeldetyp 2|Interaktive Anmeldung  |Benutzer hat durch Eingabe eines Benutzernamens und Kennworts Zugriff auf das Netzwerk erlangt (Authentifizierungsmethode Kerberos).|
|Anmeldetyp 2|VPN-Verbindung   |Benutzer hat sich über VPN verbunden – Authentifizierung mithilfe des RADIUS-Protokolls.|
|Anmeldetyp 3|Ressourcenzugriff  |Benutzer hat mit Kerberos-Authentifizierung auf eine Ressource zugegriffen.|
|Anmeldetyp 8|LDAP ClearText  |Benutzer hat sich über LDAP mit einem Klartextkennwort authentifiziert (einfache Authentifizierung).|
|Anmeldetyp 10|Remotedesktop |Benutzer hat eine RDP-Sitzung mit einem Remotecomputer über Kerberos-Authentifizierung durchgeführt.|
| --- |Anmeldung fehlgeschlagen |Authentifizierungsversuch des Domänenkontos (über NTLM und Kerberos) aufgrund von Folgendem fehlgeschlagen: Konto war deaktiviert/abgelaufen/gesperrt/verwendete ein nicht vertrauenswürdiges Zertifikat oder aber ungültige Anmeldezeiten/altes Kennwort/abgelaufenes Kennwort/falsches Kennwort.|


## <a name="monitored-machine-activities-machine-account"></a>Überwachte Computeraktivitäten: Computerkonto

|Überwachte Aktivität|Beschreibung|
|---------------------|------------------|
|Betriebssystem des Computers geändert|Änderung beim Betriebssystem des Computers.


## <a name="see-also"></a>Weitere Informationen
- [Verwenden von Sicherheitswarnungen](working-with-suspicious-activities.md)
- [Leitfaden für Sicherheitswarnungen](suspicious-activity-guide.md)
- [Untersuchen von Entitäten](investigate-entity.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
