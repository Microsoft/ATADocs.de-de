---
title: Überprüfung der erweiterten Überwachungsrichtlinie von Azure Advanced Threat Protection | Microsoft-Dokumentation
description: Dieser Artikel bietet eine Übersicht der erweiterten Überwachungsrichtlinie von Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ab1e8dd9-a6c2-4c68-89d5-343b8ec56142
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8d7d8bc8ce6c1aefb95b5770a103859fed74efe1
ms.sourcegitcommit: a0ebb0b6f140d4abf091ebd9d756b975b3d96b9d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/23/2019
ms.locfileid: "54458630"
---
# <a name="azure-atp-advanced-audit-policy-check"></a>Überprüfung der erweiterten Überwachungsrichtlinie von Azure ATP

Die Azure ATP-Erkennung beruht auf bestimmten Windows-Ereignisprotokollen für Sichtbarkeit in bestimmten Szenarios, z.B. NTLM-Anmeldungen, Änderungen an Sicherheitsgruppen und ähnlichen Ereignissen. Damit die richtigen Ereignisse überprüft und im Windows-Ereignisprotokoll eingeschlossen werden, benötigen Ihre Domänencontroller die korrekten erweiterten Überwachungsrichtlinieneinstellungen. Falsche erweiterte Überwachungsrichtlinieneinstellungen führen dazu, dass wichtige Ereignisse nicht in Ihren Protokollen aufgeführt werden und so die Abdeckung durch Azure ATP unzureichend vorhanden ist.

Damit Sie den aktuellen Status jeder erweiterten Überwachungsrichtlinien Ihres Domänencontrollers überprüfen können, überprüft Azure ATP automatisch Ihre erweiterten Überwachungsrichtlinien und gibt Integritätswarnungen für Richtlinieneinstellungen aus, die geändert werden müssen. Jede Integritätswarnung stellt bestimmte Informationen über den Domänencontroller bereit, von der problematischen Richtlinie bis hin zu Wiederherstellungsvorschlägen.

![Integritätswarnung der erweiterten Überwachungsrichtlinie](media/atp-health-alert-audit-policy.png)


Advanced Security Audit Policy (Erweiterte Sicherheitsüberwachungsrichtlinien) ist über das Gruppenrichtlinienobjekt **Standarddomänencontroller-Richtlinie** aktiviert. Diese Überprüfungsereignisse können in den Windows-Ereignissen des Domänencontrollers aufgezeichnet werden. 



<br>Ändern Sie mithilfe der folgenden Anweisungen die erweiterten Überwachungsrichtlinien Ihres Domänencontrollers:

1. Melden Sie sich beim Server als **Domänenadministrator** an.
2. Laden Sie den Gruppenrichtlinienverwaltungs-Editor über **Server-Manager** > **Extras** > **Gruppenrichtlinienverwaltung**. 
3. Erweitern Sie die **Organisationseinheiten der Domänencontroller**, klicken Sie mit der rechten Maustaste auf **Standarddomänencontroller-Richtlinie**, und wählen Sie **Bearbeiten** aus. 

    ![Bearbeiten der Standarddomänencontroller-Richtlinie](media/atp-advanced-audit-policy-check-step-1.png)

4. Wechseln Sie im geöffneten Fenster zu **Computerkonfiguration** > **Richtlinien** > **Windows-Einstellungen** > **Sicherheitseinstellungen** > **Erweiterte Überwachungsrichtlinienkonfiguration**.

    ![Erweiterte Überwachungsrichtlinienkonfiguration](media/atp-advanced-audit-policy-check-step-2.png)

5. Wechseln Sie zur Kontoanmeldung, doppelklicken Sie auf **Überprüfen der Anmeldeinformationen überwachen**, und wählen Sie jeweils für erfolgreiche und erfolglose Ereignisse die Option **Configure the following audit events** (Folgende Überwachungsereignisse konfigurieren) aus. 

    ![Überprüfen der Anmeldeinformationen](media/atp-advanced-audit-policy-check-step-3.png)

6. Wechseln Sie zur Kontoverwaltung, doppelklicken Sie auf **Sicherheitsgruppenverwaltung überwachen**, und wählen Sie jeweils für erfolgreiche und erfolglose Ereignisse die Option **Configure the following audit events** (Folgende Überwachungsereignisse konfigurieren) aus.

    ![Sicherheitsgruppenverwaltung überwachen](media/atp-advanced-audit-policy-check-step-4.png)

    > [!NOTE]
    > Wenn Sie sich für die Verwendung lokaler Richtlinien entscheiden, stellen Sie sicher, dass Sie darin die Überwachungsprotokolle **Kontoanmeldung** und **Kontoverwaltung** hinzufügen. Wenn Sie die erweiterte Überwachungsrichtlinie konfigurieren, stellen Sie sicher, dass Sie die [Überwachungsrichtlinien-Unterkategorie](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/audit-force-audit-policy-subcategory-settings-to-override) erzwingen.

7. Nachdem die neuen Ereignisse über GPO angewendet wurden, sind sie unter Ihren **Windows-Ereignisprotokollen** sichtbar.

## <a name="see-also"></a>Weitere Informationen
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](atp-prerequisites.md)
- [Konfigurieren der Ereignissammlung](configure-event-collection.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-forwarding.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)
