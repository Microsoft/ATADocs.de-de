---
title: "Arbeiten mit verdächtigen Aktivitäten | Microsoft ATA"
description: "Beschreibt, wie Sie von ATA identifizierte verdächtige Aktivitäten überprüfen."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 44d7c899-816c-4f7f-91d3-84a09d291a24
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: e07ab99454133eab0480277ec2e54a1c3253a621


---

# Arbeiten mit verdächtigen Aktivitäten
In diesem Thema werden die Grundlagen des Arbeitens mit Advanced Threat Analytics erläutert.

## Überprüfen verdächtiger Aktivitäten auf der Angriffszeitachse
Nachdem Sie sich bei der ATA-Konsole angemeldet haben, gelangen Sie automatisch zur **Zeitachse mit den offenen verdächtigen Aktivitäten**. Die verdächtigen Aktivitäten werden in chronologischer Reihenfolge aufgeführt, wobei sich die neuesten verdächtigen Aktivitäten oben auf der Zeitachse befinden.
Zu jeder verdächtigen Aktivität stehen folgende Informationen zur Verfügung:

-   Die beteiligten Entitäten, einschließlich Benutzer, Computer, Server, Domänencontroller und Ressourcen

-   Uhrzeiten und Zeitrahmen der verdächtigen Aktivitäten

-   Schweregrad der verdächtigen Aktivitäten: „Hoch“, „Mittel“ oder „Niedrig“

-   Status: „Offen“, „Aufgelöst“ oder „Verworfen“

-   Möglichkeit für Folgendes:

    -   Teilen der verdächtigen Aktivität mit anderen Personen in Ihrer Organisation per E-Mail.

    -   Exportieren der verdächtigen Aktivität nach Excel.

    -   Hinzufügen einer Notiz zu der verdächtigen Aktivität.

    -   Bereitstellen von Eingaben zur verdächtigen Aktivität.

-   Empfehlungen zur Reaktion auf die verdächtige Aktivität

> [!NOTE]
> -   Wenn Sie mit der Maus auf einen Benutzer oder Computer zeigen, wird ein Miniprofil der Entität angezeigt. Dieses enthält zusätzliche Informationen zur Entität und die Anzahl von verdächtigen Aktivitäten, mit denen die Entität verknüpft ist.
> -   Wenn Sie auf eine Entität klicken, gelangen Sie zum Entitätsprofil des Benutzers oder Computers.

![Abbildung der Zeitachse für verdächtige Aktivitäten von ATA](media/ATA-Suspicious-Activity-Timeline.JPG)

## Filtern der Liste der verdächtigen Aktivitäten
So filtern Sie die Liste der verdächtigen Aktivitäten

1.  Wählen Sie auf der linken Seite des Bildschirms im Bereich **Filtern nach** eine der folgenden Optionen aus: **Alle**, **Offen**, **Aufgelöst** oder **Verworfen**.

2.  Um die Liste weiter zu filtern, wählen Sie **Hoch**, **Mittel** oder **Niedrig** aus.

**Schweregrad von verdächtigen Aktivitäten**

-   **Niedrig**

    Weist auf verdächtige Aktivitäten hin, die zu Angriffen durch böswillige Benutzer oder Software führen können, um Zugriff auf Organisationsdaten zu erlangen.

-   **Mittel**

    Weist auf verdächtige Aktivitäten hin, die für bestimmte Identitäten das Risiko schwerwiegenderer Angriffe erhöhen und zu Identitätsdiebstahl oder Berechtigungsausweitung führen können.

-   **Hoch**

    Weist auf verdächtige Aktivitäten hin, die zu Identitätsdiebstahl, Berechtigungsausweitung oder anderen Angriffen mit schwerwiegenden Auswirkungen führen können.

**Status von verdächtigen Aktivitäten**

-   **Öffnen**

    In dieser Liste werden alle neuen verdächtigen Aktivitäten angezeigt.

-   **Resolved**

    Wird verwendet, um verdächtige Aktivitäten nachzuverfolgen, die Sie identifiziert, untersucht und behoben oder entschärft haben.

    > [!NOTE]
    > ATA kann aufgelöste Aktivitäten wieder öffnen, wenn sie innerhalb eines kurzen Zeitraums erneut erkannt werden.

-   **Verworfen**

    Dies sind Aktivitäten, die Sie manuell verworfen haben. Wenn ATA eine ähnliche verdächtige Aktivität erkennt, wird eine neue Erkennung erstellt.

## Bereitstellen von Eingaben zu einer verdächtigen Aktivität
Damit ATA Informationen zu Ihrem Netzwerk sammeln kann, werden bei einigen verdächtigen Aktivitäten (DNS-Reconnaissance, Pass-the-Ticket, SMB-Sitzungsenumeration, nicht normales Verhalten und Remoteausführung) Eingaben von Ihnen angefordert, um die Erkennung von verdächtigen Aktivitäten zukünftig zu verbessern.

1.  Bei verdächtigen Aktivitäten, für die Sie Eingaben bereitstellen können, wird die Eingabeanforderung automatisch geöffnet. Sie werden aufgefordert, Fragen zu Aktivitäten in Ihrem Netzwerk zu beantworten und anzugeben, ob sie als verdächtig eingestuft werden sollen. Im folgenden Beispiel werden Sie gefragt, ob das Ausführen von Überprüfungstools von einem bestimmten Computer aus zulässig ist.

    ![Abbildung zum Bereitstellen von Eingaben für verdächtige Aktivitäten in ATA](media/ATA-Input.JPG)

2.  Wenn Sie mit „Nein“ antworten, wird die Aktivität als verdächtig eingestuft und Sie werden jedes Mal gewarnt, wenn ATA die Aktivität auf diesem Computer erkennt.

3.  Wenn Sie jedoch mit „Ja“ antworten, kann die verdächtige Aktivität verworfen werden und künftige Aktivitäten dieses Typs von diesem Computer generieren möglicherweise keine verdächtige Aktivität oder eine Aktivität, die automatisch verworfen wird.

4.  Wenn Sie es nicht wissen, klicken Sie auf **Abbrechen**.

## Ändern des Status einer verdächtigen Aktivität
Sie können den Status einer verdächtigen Aktivität ändern, indem Sie auf den aktuellen Status der verdächtigen Aktivität klicken und eine der folgenden Optionen auswählen: **Offen**, **Aufgelöst** oder **Verworfen**.

## Siehe auch
- [Weitere Informationen finden Sie im ATA-Forum.](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Arbeiten mit ATA-Erkennungseinstellungen](working-with-detection-settings.md)
- [Ändern der ATA-Konfiguration](modifying-ata-configuration.md)



<!--HONumber=Jul16_HO4-->


