---
title: Konfigurieren der Windows-Ereignissammlung in Azure Advanced Threat Protection
description: In diesem Schritt bei der ATP-Installation konfigurieren Sie die Windows-Ereignissammlung.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 08/04/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 88692d1a-45a3-4d54-a549-4b5bba6c037b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 55e5962ed3d9e9a1a922b47daf46bdb0c2b0d91d
ms.sourcegitcommit: 0c356b0860ae8663254e0cf6f04001bcc91ce207
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/21/2020
ms.locfileid: "90826225"
---
# <a name="configure-windows-event-collection"></a>Konfigurieren der Windows-Ereignissammlung

Die Azure Advanced Threat Protection-Erkennung (Azure ATP) basiert auf bestimmten Windows-Ereignisprotokolleinträgen, um einige Erkennungen zu verbessern und zusätzliche Informationen darüber bereitzustellen, wer bestimmte Aktionen ausgeführt hat, wie z. B. NTLM-Anmeldungen, Änderungen an Sicherheitsgruppen und ähnliche Ereignisse. Damit die richtigen Ereignisse überprüft und im Windows-Ereignisprotokoll eingeschlossen werden, benötigen Ihre Domänencontroller die korrekten erweiterten Überwachungsrichtlinieneinstellungen. Falsche erweiterte Überwachungsrichtlinieneinstellungen können dazu führen, dass die erforderlichen Ereignisse nicht im Ereignisprotokoll aufgezeichnet werden und die Azure ATP-Abdeckung unvollständig ist.

Die folgenden Windows-Ereignisse müssen für Azure ATP [konfiguriert](#configure-audit-policies) und [gesammelt](#configure-event-collection) werden, um die Funktionen zum Erkennen von Bedrohungen zu verbessern:

- 4726: Benutzerkonto gelöscht
- 4728: Member Added to Global Security Group (Mitglied zu globaler Sicherheitsgruppe hinzugefügt)
- 4729: Member Removed from Global Security Group (Mitglied aus globaler Sicherheitsgruppe entfernt)
- 4730: Global Security Group Deleted (Globale Sicherheitsgruppe gelöscht)
- 4732: Member Added to Local Security Group (Mitglied zu lokaler Sicherheitsgruppe hinzugefügt)
- 4733: Member Removed from Global Security Group (Mitglied aus globaler Sicherheitsgruppe entfernt)
- 4743: Computer Account Deleted (Computerkonto gelöscht)
- 4753: Global Distribution Group Deleted (Lokale Verteilergruppe gelöscht)
- 4756: Member Added to Universal Security Group (Mitglied zu universeller Sicherheitsgruppe hinzugefügt)
- 4757: Member Removed from Universal Security Group (Mitglied aus universeller Sicherheitsgruppe entfernt)
- 4758: Universal Security Group Deleted (Universelle Sicherheitsgruppe gelöscht)
- 4763: Universal Distribution Group Deleted (Universelle Verteilergruppe gelöscht)
- 4776: Der Domänencontroller hat versucht, die Anmeldeinformationen für ein Konto zu bestätigen (NTLM)
- 7045: New Service Installed (Neuer Dienst installiert)
- 8004: NTLM-Authentifizierung

## <a name="configure-audit-policies"></a>Konfigurieren von Überwachungsrichtlinien

Ändern Sie mithilfe der folgenden Anweisungen die erweiterten Überwachungsrichtlinien Ihres Domänencontrollers:

1. Melden Sie sich beim Server als **Domänenadministrator** an.
1. Laden Sie den Gruppenrichtlinienverwaltungs-Editor über **Server-Manager** > **Extras** > **Gruppenrichtlinienverwaltung**.
1. Erweitern Sie die **Organisationseinheiten der Domänencontroller**, klicken Sie mit der rechten Maustaste auf **Standarddomänencontroller-Richtlinie**, und klicken Sie auf **Bearbeiten**.

    > [!NOTE]
    > Zum Festlegen dieser Richtlinien können Sie die Standardrichtlinie für Domänencontroller oder ein dediziertes GPO verwenden.

    ![Bearbeiten der Standarddomänencontroller-Richtlinie](media/atp-advanced-audit-policy-check-step-1.png)

1. Wechseln Sie im geöffneten Fenster zu **Computerkonfiguration** > **Richtlinien** > **Windows-Einstellungen** > **Sicherheitseinstellungen**, und führen Sie abhängig von der gewünschten Richtlinie die folgenden Schritte durch:

    **Für die erweiterte Überwachungsrichtlinienkonfiguration**

    1. Wechseln Sie zu **Erweiterte Überwachungsrichtlinienkonfiguration** > **Überwachungsrichtlinien**.
        ![Erweiterte Überwachungsrichtlinienkonfiguration](media/atp-advanced-audit-policy-check-step-2.png)
    1. Bearbeiten Sie unter **Überwachungsrichtlinien** die folgenden Richtlinien, und wählen Sie dann sowohl für die Ereignisse **Erfolg** und **Fehler** die Option **Configure the following audit events** (Folgende Überwachungsereignisse konfigurieren) aus.

        | Überwachungsrichtlinie | Unterkategorie | Auslöser für Ereignis-IDs |
        | --- |---|---|
        | Kontoanmeldung | Überprüfen der Anmeldeinformationen überwachen | 4776 |
        | Kontoverwaltung | Computerkontoverwaltung überwachen | 4743 |
        | Kontoverwaltung | Verteilergruppenverwaltung überwachen | 4753, 4763 |
        | Kontoverwaltung | Sicherheitsgruppenverwaltung überwachen | 4728, 4729, 4730, 4732, 4733, 4756, 4757, 4758 |
        | Kontoverwaltung | Benutzerkontenverwaltung überwachen | 4726 |
        | System | Sicherheitssystemerweiterung überwachen | 7045 |

        Wenn Sie zum Beispiel **Sicherheitsgruppenverwaltung überwachen** unter **Kontoverwaltung** konfigurieren möchten, doppelklicken Sie auf **Sicherheitsgruppenverwaltung überwachen**, und wählen Sie jeweils für Ereignisse mit dem Status **Erfolg** und **Fehler** die Option **Configure the following audit events** (Folgende Überwachungsereignisse konfigurieren) aus.

        ![Sicherheitsgruppenverwaltung überwachen](media/atp-advanced-audit-policy-check-step-4.png)

    <a name="ntlm-authentication-using-windows-event-8004"></a> **Für lokale Richtlinien (Ereignis-ID: 8004)**

    > [!NOTE]
    >
    > - Gruppenrichtlinien zum Sammeln des Windows-Ereignisses 8004 auf Domänenebene dürfen **nur** auf Domänencontroller angewendet werden.
    > - Bei der Analyse des Windows-Ereignisses 8004 durch den Azure ATP-Sensor werden Azure ATP-NTLM-Authentifizierungsaktivitäten durch die Daten ergänzt, auf die auf dem Server zugegriffen wird.

    1. Wechseln Sie zu **Lokale Richtlinien** > **Sicherheitsoptionen**.
    1. Konfigurieren Sie unter **Sicherheitsoptionen** die angegebenen Sicherheitsrichtlinien wie folgt:

        | Sicherheitsrichtlinieneinstellung | Wert |
        |---|---|
        | Netzwerksicherheit: Beschränken von NTLM: Ausgehender NTLM-Datenverkehr zu Remoteservern | Alle überwachen |
        | Netzwerksicherheit: Beschränken von NTLM: NTLM-Authentifizierung in dieser Domäne überwachen | Alle aktivieren |
        | Netzwerksicherheit: Beschränken von NTLM: Eingehender NTLM-Datenverkehr überwachen | Überwachung für alle Konten aktivieren |

        Wenn Sie beispielsweise **ausgehenden NTLM-Datenverkehr zu Remoteservern** konfigurieren möchten, doppelklicken Sie unter **Sicherheitsoptionen** auf **Netzwerksicherheit: Beschränken von NTLM: Ausgehender NTLM-Datenverkehr zu Remoteservern**, und klicken Sie auf **Alle überwachen**.

        ![Überwachen von ausgehendem Netzwerkdatenverkehr an Remoteserver](media/atp-advanced-audit-policy-check-step-3.png)

    > [!NOTE]
    > Wenn Sie anstelle einer Gruppenrichtlinie eine lokale Sicherheitsrichtlinie verwenden, stellen Sie sicher, dass Sie die Überwachungsprotokolle für die **Kontoanmeldung**, die **Kontoverwaltung** und die **Sicherheitsoptionen** zu Ihrer lokalen Richtlinie hinzufügen. Wenn Sie die erweiterte Überwachungsrichtlinie konfigurieren, stellen Sie sicher, dass Sie die [Überwachungsrichtlinien-Unterkategorie](/windows/security/threat-protection/security-policy-settings/audit-force-audit-policy-subcategory-settings-to-override) erzwingen.

1. Nachdem die neuen Ereignisse über GPO angewendet wurden, sind sie unter Ihren **Windows-Ereignisprotokollen** sichtbar.

<!--
## Azure ATP Advanced Audit Policy check

To make it easier to verify the current status of each of your domain controller's Advanced Audit Policies, Azure ATP automatically checks your existing Advanced Audit Policies and issues health alerts for policy settings that require modification. Each health alert provides specific details of the domain controller, the problematic policy as well as remediation suggestions.

![Advanced Audit Policy Health Alert](media/atp-health-alert-audit.png)

Advanced Security Audit Policy is enabled via **Default Domain Controllers Policy** GPO. These audit events are recorded on the domain controller's Windows Events.
-->

## <a name="configure-event-collection"></a>Konfigurieren der Ereignissammlung

Diese Ereignisse können automatisch vom Azure ATP-Sensor gesammelt werden. Wenn der Azure ATP-Sensor nicht bereitgestellt wird, können sie alternativ auf eine der folgenden Arten an den eigenständigen Azure ATP-Sensor weitergeleitet werden:

- [Konfigurieren des eigenständigen Azure ATP-Sensors](configure-event-forwarding.md) zum Lauschen an SIEM-Ereignissen
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-forwarding.md)

> [!NOTE]
>
> - Eigenständige Azure ATP-Server unterstützen nicht die Erstellung von Protokolleinträgen für Ereignisablaufverfolgung für Windows (Event Tracing for Windows, ETW), die Daten für mehrere Erkennungen bereitstellen. Zur vollständigen Abdeckung Ihrer Umgebung empfiehlt es sich, den Azure ATP-Sensor bereitzustellen.
> - Es ist wichtig, vor dem Aktivieren der Ereignissammlung die [Überwachungsrichtlinien]() zu überprüfen und zu verifizieren, um sicherzustellen, dass die Domänencontroller ordnungsgemäß für die Aufzeichnung der erforderlichen Ereignisse konfiguriert sind.

## <a name="see-also"></a>Weitere Informationen

- [Azure ATP sizing tool (Azure ATP-Tool zur Größenanpassung)](https://aka.ms/aatpsizingtool)
- [Azure ATP prerequisites (Voraussetzungen für Azure ATP)](prerequisites.md)
- [Referenz zum Azure ATP-SIEM-Protokoll](cef-format-sa.md)
- [Konfigurieren der Windows-Ereignisweiterleitung](configure-event-forwarding.md)
- [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)