---
title: Schnellstart zum Herstellen einer Verbindung zwischen Azure ATP und Azure Active Directory | Microsoft-Dokumentation
description: Im zweiten Schritt der Installation von Azure ATP konfigurieren Sie die Domänenverbindungseinstellungen in Ihrem Azure ATP-Clouddienst.
author: shsagir
ms.author: shsagir
ms.date: 02/05/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.openlocfilehash: 76096f506714d8a876cac49fee04b7451da392e9
ms.sourcegitcommit: 9673eb49729a06d3a25d52c0f43c76ac61b9cf89
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/12/2020
ms.locfileid: "75906605"
---
# <a name="quickstart-connect-to-your-active-directory-forest"></a>Schnellstart: Herstellen einer Verbindung mit einer Active Directory-Gesamtstruktur

In diesem Schnellstart lernen Sie, wie Sie eine Verbindung zwischen Azure ATP und Azure Active Directory (Azure AD) herstellen können, um Daten zu Benutzern und Computern abrufen zu können. Wenn Sie eine Verbindung zwischen mehreren Gesamtstrukturen herstellen möchten, finden Sie weitere Informationen im Artikel [Azure Advanced Threat Protection-Unterstützung für mehrere Gesamtstrukturen](atp-multi-forest.md).

## <a name="prerequisites"></a>Voraussetzungen

- Eine [Azure ATP-Instanz](install-atp-step1.md)
- Lesen Sie den Artikel [Voraussetzungen für Azure ATP](atp-prerequisites.md).
- Ein **lokales** AD-Benutzerkonto und -Kennwort mit Lesezugriff auf alle Objekte in den überwachten Domänen.

## <a name="provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>Angeben eines Benutzernamens und eines Kennworts, um eine Verbindung mit Ihrer Active Directory-Gesamtstruktur herzustellen

Beim ersten Öffnen des Azure ATP-Portals wird die folgende Anzeige angezeigt:

![Azure ATP-Willkommensseite 1](media/directory-services.png)


1. Geben Sie die folgenden Informationen ein, und klicken Sie anschließend auf **Speichern**.

    |Feld|Kommentare|
    |---------|------------|
    |**Benutzername** (erforderlich)|Geben Sie den schreibgeschützten Active Directory-Benutzernamen ein. Beispiel: **ATPuser**.  Sie müssen ein **lokales** Azure AD-Benutzerkonto verwenden. Verwenden Sie **nicht** das UPN-Format für Ihren Benutzernamen.|
    |**Kennwort** (erforderlich)|Geben Sie das Kennwort für den schreibgeschützten Benutzer ein. Beispiel: **Pencil1**.|
    |**Domäne** (erforderlich)|Geben Sie die Domäne für den schreibgeschützten Benutzer ein. Beispiel: **contoso.com**. Es ist wichtig, dass Sie den vollqualifizierten Domänennamen (FQDN) der Domäne eingeben, in der sich das Benutzerkonto befindet. Wenn sich das Konto des Benutzers beispielsweise in der Domäne „corp.contoso.com“ befindet, müssen Sie `corp.contoso.com` und nicht „contoso.com“ eingeben.|

2. Klicken Sie im Azure ATP-Portal auf **Download sensor setup and install the first sensor** (Sensorsetup herunterladen und ersten Sensor installieren), um fortzufahren.


## <a name="next-steps"></a>Nächste Schritte

> [!div class="step-by-step"]
> [« Erstellen Ihrer Azure ATP-Instanz im Azure ATP-Portal – Schritt 1](install-atp-step1.md)
> [Installieren von Azure ATP: Schritt 3 »](install-atp-step3.md)

## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über Azure ATP und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [Azure ATP-Community](https://aka.ms/azureatpcommunity) bei!
