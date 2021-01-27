---
title: 'Schnellstart: Herstellen einer Verbindung zwischen Microsoft Defender for Identity und Active Directory'
description: Der zweite Schritt der Microsoft Defender for Identity-Installation unterstützt Sie bei der Konfiguration der Domänenverbindungseinstellungen für Ihren Defender for Identity-Clouddienst.
ms.date: 10/26/2020
ms.topic: quickstart
ms.openlocfilehash: b1379570d87957fc943bf8b0727b6b0294f26695
ms.sourcegitcommit: b6da51c97e8fb70ca04c0c0d5ea694700db9de86
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/21/2021
ms.locfileid: "98634555"
---
# <a name="quickstart-connect-to-your-active-directory-forest"></a>Schnellstart: Herstellen einer Verbindung mit einer Active Directory-Gesamtstruktur

In diesem Schnellstart lernen Sie, wie Sie eine Verbindung zwischen [!INCLUDE [Product long](includes/product-long.md)] und Azure Active Directory (Azure AD) herstellen können, um Daten zu Benutzern und Computern abrufen zu können. Wenn Sie eine Verbindung zwischen mehreren Gesamtstrukturen herstellen möchten, finden Sie weitere Informationen im Artikel [Azure Advanced Threat Protection-Unterstützung für mehrere Gesamtstrukturen](multi-forest.md).

## <a name="prerequisites"></a>Voraussetzungen

- Eine [[!INCLUDE [Product short](includes/product-short.md)]-Instanz](install-step1.md)
- Lesen Sie den Artikel [[!INCLUDE [Product short](includes/product-short.md)]-Voraussetzungen](prerequisites.md).
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

Beim ersten Öffnen des [!INCLUDE [Product short](includes/product-short.md)]-Portals wird die folgende Anzeige angezeigt:

![Willkommen bei Phase 1, Verzeichnisdiensteeinstellungen](media/directory-services.png)

1. Geben Sie die folgenden Informationen ein, und klicken Sie anschließend auf **Speichern**.

    |Feld|Kommentare|
    |---|---|
    |**Benutzername** (erforderlich)|Geben Sie den Namen des AD-Benutzers mit Leseberechtigung ein. Beispiel: **DefenderForIdentityUser**. Sie müssen ein AD-**Standardbenutzerkonto** oder ein gruppenverwaltetes Dienstkonto verwenden. Verwenden Sie **nicht** das UPN-Format für Ihren Benutzernamen.<br />**HINWEIS:** Sie sollten die Verwendung von Konten vermeiden, die bestimmten Benutzern zugewiesen sind.|
    |**Kennwort** (bei AD-Standardbenutzerkonten erforderlich)|Geben Sie bei AD-Benutzerkonten das Kennwort für den Benutzer mit Leseberechtigung ein. Beispiel: **Pencil1**.|
    |**Gruppenverwaltetes Dienstkonto** (bei gruppenverwalteten Dienstkonten erforderlich)|Wählen Sie bei gruppenverwalteten Dienstkonten das **gruppenverwaltete Dienstkonto** aus.|
    |**Domäne** (erforderlich)|Geben Sie die Domäne für den schreibgeschützten Benutzer ein. Beispiel: **contoso.com**. Es ist wichtig, dass Sie den vollqualifizierten Domänennamen (FQDN) der Domäne eingeben, in der sich das Benutzerkonto befindet. Wenn sich das Konto des Benutzers beispielsweise in der Domäne „corp.contoso.com“ befindet, müssen Sie `corp.contoso.com` und nicht „contoso.com“ eingeben.|

1. Klicken Sie im [!INCLUDE [Product short](includes/product-short.md)]-Portal auf **Download sensor setup and install the first sensor** (Sensorsetup herunterladen und ersten Sensor installieren), um fortzufahren.

## <a name="next-steps"></a>Nächste Schritte

> [!div class="step-by-step"]
> [« Schritt 1: Erstellen der [!INCLUDE [Product short](includes/product-short.md)]-Instanz](install-step1.md)
> [Schritt 3: Herunterladen des Sensorsetups »](install-step3.md)

## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über [!INCLUDE [Product short](includes/product-short.md)] und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [[!INCLUDE [Product short](includes/product-short.md)]Community](https://aka.ms/MDIcommunity) bei.
