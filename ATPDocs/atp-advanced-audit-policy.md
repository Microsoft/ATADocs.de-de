---
title: Überprüfung der erweiterten Überwachungsrichtlinie von Azure Advanced Threat Protection | Microsoft-Dokumentation
description: Dieser Artikel bietet eine Übersicht der erweiterten Überwachungsrichtlinie von Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/30/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ab1e8dd9-a6c2-4c68-89d5-343b8ec56142
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d37a55bdb1c437f7775f530cfc143146eb38ba96
ms.sourcegitcommit: 93a133430ac85d6db7afad5f6f2583b3a39c423a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/02/2018
ms.locfileid: "43469726"
---
*Gilt für: Azure Advanced Threat Protection*


# <a name="azure-atp-advanced-audit-policy-check"></a>Überprüfung der erweiterten Überwachungsrichtlinie von Azure ATP

Die Azure ATP-Erkennung beruht auf bestimmten Windows-Ereignisprotokollen für Sichtbarkeit in bestimmten Szenarios, z.B. NTLM-Anmeldungen, Änderungen an Sicherheitsgruppen und ähnlichen Ereignissen. Damit die richtigen Ereignisse überprüft und im Windows-Ereignisprotokoll eingeschlossen werden, benötigen Ihre Domänencontroller die korrekten erweiterten Überwachungsrichtlinieneinstellungen. Falsche erweiterte Überwachungsrichtlinieneinstellungen führen dazu, dass wichtige Ereignisse nicht in Ihren Protokollen aufgeführt werden und so die Abdeckung durch Azure ATP unzureichend vorhanden ist.

Damit Sie den aktuellen Status jeder erweiterten Überwachungsrichtlinien Ihres Domänencontrollers überprüfen können, überprüft Azure ATP automatisch Ihre erweiterten Überwachungsrichtlinien und gibt Integritätswarnungen für Richtlinieneinstellungen aus, die geändert werden müssen. Jede Integritätswarnung stellt bestimmte Informationen über den Domänencontroller bereit, von der problematischen Richtlinie bis hin zu Wiederherstellungsvorschlägen.

![Integritätswarnung der erweiterten Überwachungsrichtlinie](media/atp-health-alert-audit-policy.png)


Die erweiterten Sicherheitsüberwachungsrichtlinie ist über GPO aktiviert. Diese Überprüfungsereignisse können in den Windows-Ereignissen des Domänencontrollers aufgezeichnet werden. Dies muss in der **Richtlinie des Standarddomänencontrollers** in Active Directory aktiviert werden.

<br>Ändern Sie mithilfe der folgenden Anweisungen die erweiterten Überwachungsrichtlinien Ihres Domänencontrollers:

1. Melden Sie sich beim Server als **Domänenadministrator** an.
2. Laden Sie den Gruppenrichtlinienverwaltungs-Editor über **Server-Manager** > **Extras** > **Gruppenrichtlinienverwaltung**. 
3. Erweitern Sie die **Organisationseinheiten der Domänencontroller**, klicken Sie mit der rechten Maustaste auf **Standarddomänencontroller-Richtlinie**, und wählen Sie **Bearbeiten** aus. 

    ![Bearbeiten der Standarddomänencontroller-Richtlinie](media/atp-advanced-audit-policy-check-step-1.png)

4. Wechseln Sie im geöffneten Fenster zu **Computerkonfiguration** > **Richtlinien** > **Windows-Einstellungen** > **Sicherheitseinstellungen** > **Erweiterte Überwachungsrichtlinienkonfiguration**.

    ![Erweiterte Überwachungsrichtlinienkonfiguration](media/atp-advanced-audit-policy-check-step-2.png)

5. Wechseln Sie zur Kontoanmeldung, doppelklicken Sie auf **Überprüfen der Anmeldeinformationen überwachen**, und wählen Sie jeweils für erfolgreiche und erfolglose Ereignisse die Option **Configure the following audit events** (Folgende Überwachungsereignisse konfigurieren) aus. 

    ![Überprüfen der Anmeldeinformationen](media/atp-advanced-audit-policy-check-step-3.png)

6. Wechseln Sie zur Kontoanmeldung, doppelklicken Sie auf **Sicherheitsgruppenverwaltung überwachen**, und wählen Sie jeweils für erfolgreiche und erfolglose Ereignisse die Option **Configure the following audit events** (Folgende Überwachungsereignisse konfigurieren) aus.

    ![Sicherheitsgruppenverwaltung überwachen](media/atp-advanced-audit-policy-check-step-4.png)

7. Nachdem die neuen Ereignisse über GPO angewendet wurden, sind sie unter Ihren **Windows-Ereignisprotokollen** sichtbar.

## <a name="see-also"></a>Weitere Informationen
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)
