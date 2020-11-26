---
title: Von Microsoft Defender for Identity überwachte Domänenaktivitäten
description: Beschreibt jeden Aktivitätstyp, der von Microsoft Defender for Identity überwacht wird.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f8d7237d3202ed4b0645b92d61f37cc7c89085da
ms.sourcegitcommit: 07a855b87931875bdeca14b152b13a36db79bfa8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/26/2020
ms.locfileid: "94847223"
---
# <a name="product-long-monitored-activities"></a>Von [!INCLUDE [Product long](includes/product-long.md)] überwachte Aktivitäten

> [!NOTE]
> Die auf dieser Seite erläuterten [!INCLUDE [Product long](includes/product-long.md)]-Features sind auch über das neue [Portal](https://portal.cloudappsecurity.com) zugänglich.

[!INCLUDE [Product long](includes/product-long.md)] überwacht Informationen, die aus dem Active Directory, den Netzwerkaktivitäten und Ereignisaktivitäten Ihrer Organisation generiert wurden, um verdächtige Aktivitäten zu erkennen. Anhand der überwachten Aktivitätsinformationen kann [!INCLUDE [Product short](includes/product-short.md)] Ihnen helfen, die Gültigkeit der einzelnen potenziellen Bedrohungen zu bestimmen sowie sie richtig zu selektieren und entsprechend zu reagieren.

Im Fall einer gültigen Bedrohung oder von **richtig positiv** ermöglicht [!INCLUDE [Product short](includes/product-short.md)] es Ihnen, den Umfang der Sicherheitsverletzung für jeden Vorfall zu ermitteln, zu untersuchen, welche Entitäten beteiligt sind, und zu bestimmen, wie sie korrigiert werden können.

Die von [!INCLUDE [Product short](includes/product-short.md)] überwachten Informationen werden in Form von Aktivitäten angezeigt. [!INCLUDE [Product short](includes/product-short.md)] unterstützt zurzeit die Überwachung der folgenden Aktivitätstypen:

> [!NOTE]
>
> - Dieser Artikel ist für alle [!INCLUDE [Product short](includes/product-short.md)]-Sensortypen relevant.
> - Von [!INCLUDE [Product short](includes/product-short.md)] überwachte Aktivitäten werden auf der Profilseite sowohl für Benutzer als auch für Computer angezeigt.

## <a name="monitored-user-activities-user-account-ad-attribute-changes"></a>Überwachte Benutzeraktivitäten: Änderungen am AD-Attribut für Benutzerkonto

|Überwachte Aktivität|Beschreibung|
|---------------------|------------------|
|Kontostatus „Eingeschränkte Delegierung“ geändert|Der Kontostatus ist jetzt für Delegierung aktiviert oder deaktiviert.|
|SPNs für eingeschränkte Kontodelegierung geändert|Die eingeschränkte Delegierung beschränkt die Dienste, für die der angegebene Server im Auftrag des Benutzers agieren kann.|
|„Konto deaktiviert“ geändert|Gibt an, ob ein Konto aktiviert oder deaktiviert ist.|
|Konto abgelaufen|Datum, an dem das Konto abläuft.|
|Ablaufzeit für Konto geändert|Änderung in das Datum, an dem das Konto abläuft.|
|„Konto gesperrt“ geändert|Änderung in das Datum, an dem das Konto abläuft.|
|Kontokennwort geändert|Benutzer hat sein Kennwort geändert.|
|Kontokennwort abgelaufen|Kennwort des Benutzers ist abgelaufen.|
|„Kontokennwort läuft nie ab“ geändert|Kennwort des Benutzer wurde geändert, sodass es nie abläuft.|
|„Kein Kontokennwort erforderlich“ geändert|Benutzerkonto wurde geändert, sodass Anmeldung mit einem leeren Kennwort zulässig ist.|
|„Smartcard für Konto erforderlich“ geändert|Konto wurde geändert, sodass Benutzer aufgefordert werden, sich auf einem Gerät mit einer Smartcard anzumelden.|
|Vom Konto unterstützte Verschlüsselungstypen geändert|Von Kerberos unterstützte Verschlüsselungstypen wurden geändert (Typen: Des, AES 129, AES 256)|
|UPN-Name von Konto geändert|Der Benutzerprinzipalname wurde geändert.|
|Gruppenmitgliedschaft geändert|Benutzer wurde zu/aus einer Gruppe hinzugefügt/gelöscht, und zwar von einem anderen Benutzer oder ihm selbst.|
|Benutzer-E-Mail geändert|E-Mail-Attribut des Benutzers wurde geändert.|
|Benutzer-Manager geändert|Manager-Attribut des Benutzers wurde geändert.|
|Benutzer-Telefonnummer geändert|Telefonnummer-Attribut des Benutzers wurde geändert.|
|Benutzertitel geändert|Title-Attribut des Benutzers wurde geändert.|

<!-- Rollback
|SID-History Changed|Account's SID-History attribute was changed.|
-->

## <a name="monitored-user-activities-ad-security-principal-operations"></a>Überwachte Benutzeraktivitäten: Vorgänge für AD-Sicherheitsprinzipal

|Überwachte Aktivität|Beschreibung|
|---------------------|------------------|
|Sicherheitsprinzipal erstellt|Konto wurde erstellt (Benutzer- und Computerkonto).|
|„Sicherheitsprinzipal gelöscht“ geändert|Konto wurde gelöscht/wiederhergestellt (Benutzer- und Computerkonto).|
|Anzeigename von Sicherheitsprinzipal geändert|Anzeigename des Kontos wurde von X in Y geändert.|
|Name von Sicherheitsprinzipal geändert|Kontonamenattribut wurde geändert.|
|Pfad von Sicherheitsprinzipal geändert|Distinguished Name für Konto wurde von X in Y geändert.|
|SAM-Name von Sicherheitsprinzipal geändert|SAM-Name wurde geändert (SAM ist der Anmeldename zur Unterstützung von Clients und Servern, auf denen frühere Versionen des Betriebssystems ausgeführt werden).|

## <a name="monitored-user-activities-domain-controller-based-user-operations"></a>Überwachte Benutzeraktivitäten: Domänencontroller-basierte Benutzervorgänge

|Überwachte Aktivität|Beschreibung|
|---------------------|------------------|
|Verzeichnisdienstreplikation|Der Benutzer hat versucht, den Verzeichnisdienst zu replizieren.|
|DNS-Abfrage|Der Typ der Benutzerabfrage, die für den Domänencontroller ausgeführt wurde (**AXFR**,**TXT**, **MX**, **NS**, **SRV**, **ANY**, **DNSKEY**).|
|Abrufen von privaten Daten|Benutzer hat versucht, private Daten mithilfe des LSARPC-Protokolls abzufragen, oder diese Abfrage ist ihm gelungen.|
|Erstellen eines Diensts|Benutzer hat versucht, einen bestimmten Dienst per Remotezugriff auf einem Remotecomputer zu erstellen.|
|SMB-Sitzungsenumeration|Benutzer hat versucht, alle Benutzer mit offenen SMB-Sitzungen auf den Domänencontrollern aufzulisten.|
|Kopieren von SMB-Dateien|Vom Benutzer mit SMB kopierte Dateien|
|SAMR-Abfrage|Benutzer hat eine SAMR-Abfrage ausgeführt.|
|Aufgabenplanung|Benutzer hat versucht, Aufgabe X per Remotezugriff auf einem Remotecomputer zu planen.|
|Wmi-Ausführung|Benutzer hat versucht, eine WMI-Methode per Remotezugriff auszuführen.|

## <a name="monitored-user-activities-login-operations"></a>Überwachte Benutzeraktivitäten: Anmeldevorgänge

|Anmeldetyp|Überwachte Aktivität|Beschreibung|
|---------------------|---------------------|------------------|
|Anmeldetyp 2|Überprüfen der Anmeldeinformationen|Authentifizierungsereignis beim Domänenkonto mit den Authentifizierungsmethoden NTLM und Kerberos.|
|Anmeldetyp 2|Interaktive Anmeldung|Benutzer hat durch Eingabe eines Benutzernamens und Kennworts Zugriff auf das Netzwerk erlangt (Authentifizierungsmethode Kerberos oder NTLM).|
|Anmeldetyp 2|Interaktive Anmeldung mit Zertifikat|Benutzer hat durch Verwendung eines Zertifikats Zugriff auf das Netzwerk erlangt.|
|Anmeldetyp 2|VPN-Verbindung|Benutzer hat sich über VPN verbunden – Authentifizierung mithilfe des RADIUS-Protokolls.|
|Anmeldetyp 3|Ressourcenzugriff|Benutzer hat mit Kerberos- oder NTLM-Authentifizierung auf eine Ressource zugegriffen.|
|Anmeldetyp 3|Delegierter Ressourcenzugriff|Benutzer hat mit Kerberos-Delegierung auf eine Ressource zugegriffen.|
|Anmeldetyp 8|LDAP ClearText|Benutzer hat sich über LDAP mit einem Klartextkennwort authentifiziert (einfache Authentifizierung).|
|Anmeldetyp 10|Remotedesktop|Benutzer hat eine RDP-Sitzung mit einem Remotecomputer über Kerberos-Authentifizierung durchgeführt.|
|---|Anmeldung fehlgeschlagen|Authentifizierungsversuch des Domänenkontos (über NTLM und Kerberos) aufgrund von Folgendem fehlgeschlagen: Konto war deaktiviert/abgelaufen/gesperrt/verwendete ein nicht vertrauenswürdiges Zertifikat oder aber ungültige Anmeldezeiten/altes Kennwort/abgelaufenes Kennwort/falsches Kennwort.|
|---|Fehler bei Anmeldung mit Zertifikat|Fehlerhafter Authentifizierungsversuch des Domänenkontos (über Kerberos) aufgrund einer der folgenden Ursachen: Konto war deaktiviert/abgelaufen/gesperrt/verwendete ein nicht vertrauenswürdiges Zertifikat oder ungültige Anmeldezeiten/altes Kennwort/abgelaufenes Kennwort/falsches Kennwort.|

## <a name="monitored-machine-activities-machine-account"></a>Überwachte Computeraktivitäten: Computerkonto

|Überwachte Aktivität|Beschreibung|
|---------------------|------------------|
|Betriebssystem des Computers geändert|Änderung beim Betriebssystem des Computers.

## <a name="see-also"></a>Weitere Informationen

- [Verwenden von Sicherheitswarnungen](working-with-suspicious-activities.md)
- [Leitfaden für Sicherheitswarnungen](suspicious-activity-guide.md)
- [Untersuchen von Entitäten](investigate-entity.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)
