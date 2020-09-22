---
title: 'Schnellstart: Herstellen einer Verbindung zwischen Azure ATP und Azure Active Directory'
description: Im zweiten Schritt der Installation von Azure ATP konfigurieren Sie die Domänenverbindungseinstellungen in Ihrem Azure ATP-Clouddienst.
author: shsagir
ms.author: shsagir
ms.date: 01/15/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.openlocfilehash: a7dd89dbd62d5ab02d33d656b011edefaa9f7f13
ms.sourcegitcommit: 0c356b0860ae8663254e0cf6f04001bcc91ce207
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/21/2020
ms.locfileid: "90826876"
---
# <a name="quickstart-connect-to-your-active-directory-forest"></a>Schnellstart: Herstellen einer Verbindung mit einer Active Directory-Gesamtstruktur

In diesem Schnellstart lernen Sie, wie Sie eine Verbindung zwischen Azure ATP und Azure Active Directory (Azure AD) herstellen können, um Daten zu Benutzern und Computern abrufen zu können. Wenn Sie eine Verbindung zwischen mehreren Gesamtstrukturen herstellen möchten, finden Sie weitere Informationen im Artikel [Azure Advanced Threat Protection-Unterstützung für mehrere Gesamtstrukturen](multi-forest.md).

## <a name="prerequisites"></a>Voraussetzungen

- Eine [Azure ATP-Instanz](install-step1.md)
- Lesen Sie den Artikel [Voraussetzungen für Azure ATP](prerequisites.md).
- Mindestens eines der folgenden Verzeichnisdienstkonten mit Lesezugriff auf alle Objekte in den überwachten Domänen:
  - Ein **standardmäßiges** AD-Benutzerkonto und -Kennwort; erforderlich für Sensoren, die unter Windows Server 2008 R2 SP1 ausgeführt werden.
  - Ein von der **Gruppe verwaltetes Dienstkonto**; erfordert Windows Server 2012 oder höher.  
  Alle Sensoren benötigen Zugriffsberechtigungen zum Abrufen des Kennworts des gruppenverwalteten Dienstkontos. Weitere Informationen zum Erstellen von gruppenverwalteten Dienstkonten finden Sie im Abschnitt [Einrichten eines gruppenverwalteten Dienstkontos](#how-to-set-up-a-gmsa-account).

    > [!NOTE]
    >
    > - Für Sensorcomputer unter Windows Server 2012 und höher wird empfohlen, ein **gruppenverwaltetes Dienstkonto** für verbesserte Sicherheit und automatische Kennwortverwaltung zu verwenden.
    > - Wenn Sie über mehrere Sensoren verfügen, teilweise unter Windows Server 2008 oder unter Windows Server 2012 und höher, müssen Sie zusätzlich zum empfohlenen **gruppenverwalteten Dienstkonto** auch mindestens ein AD-**Standardbenutzerkonto** verwenden.

### <a name="how-to-set-up-a-gmsa-account"></a>Einrichten eines gruppenverwalteten Dienstkontos

1. Erstellen Sie ein [gruppenverwaltetes Dienstkonto](/windows-server/security/group-managed-service-accounts/getting-started-with-group-managed-service-accounts#BKMK_CreateGMSA).
1. Erstellen Sie eine neue [Sicherheitsgruppe mit allen Ihren Domänencontrollern mit Sensoren (unter Windows Server 2012 und höher)](/windows-server/security/group-managed-service-accounts/getting-started-with-group-managed-service-accounts#BKMK_AddMemberHosts) mit Zugriffsberechtigungen zum Abrufen des Kennworts des gruppenverwalteten Dienstkontos. (Empfohlen)

## <a name="provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>Angeben eines Benutzernamens und eines Kennworts, um eine Verbindung mit Ihrer Active Directory-Gesamtstruktur herzustellen

Beim ersten Öffnen des Azure ATP-Portals wird die folgende Anzeige angezeigt:

![Azure ATP-Willkommensseite 1](media/directory-services.png)

1. Geben Sie die folgenden Informationen ein, und klicken Sie anschließend auf **Speichern**.

    |Feld|Kommentare|
    |---|---|
    |**Benutzername** (erforderlich)|Geben Sie den Namen des AD-Benutzers mit Leseberechtigung ein. Beispiel: **ATPuser**. Sie müssen ein AD-**Standardbenutzerkonto** oder ein gruppenverwaltetes Dienstkonto verwenden. Verwenden Sie **nicht** das UPN-Format für Ihren Benutzernamen.|
    |**Kennwort** (bei AD-Standardbenutzerkonten erforderlich)|Geben Sie bei AD-Benutzerkonten das Kennwort für den Benutzer mit Leseberechtigung ein. Beispiel: **Pencil1**.|
    |**Gruppenverwaltetes Dienstkonto** (bei gruppenverwalteten Dienstkonten erforderlich)|Wählen Sie bei gruppenverwalteten Dienstkonten das **gruppenverwaltete Dienstkonto** aus.|
    |**Domäne** (erforderlich)|Geben Sie die Domäne für den schreibgeschützten Benutzer ein. Beispiel: **contoso.com**. Es ist wichtig, dass Sie den vollqualifizierten Domänennamen (FQDN) der Domäne eingeben, in der sich das Benutzerkonto befindet. Wenn sich das Konto des Benutzers beispielsweise in der Domäne „corp.contoso.com“ befindet, müssen Sie `corp.contoso.com` und nicht „contoso.com“ eingeben.|

1. Klicken Sie im Azure ATP-Portal auf **Download sensor setup and install the first sensor** (Sensorsetup herunterladen und ersten Sensor installieren), um fortzufahren.

## <a name="next-steps"></a>Nächste Schritte

> [!div class="step-by-step"]
> [« Erstellen Ihrer Azure ATP-Instanz im Azure ATP-Portal – Schritt 1](install-step1.md)
> [Installieren von Azure ATP: Schritt 3 »](install-step3.md)

## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über Azure ATP und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [Azure ATP-Community](https://aka.ms/azureatpcommunity) bei!
