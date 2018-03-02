---
title: Untersuchen von Angriffen mit Lateral Movement-Pfaden mit Azure ATP | Microsoft Dokumentation
description: "Dieser Artikel beschreibt, wie Angriffe mit Lateral Movement-Pfaden mit Azure Advanced Threat Protection (ATP) erkannt werden können."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: de15c920-8904-4124-8bdc-03abd9f667cf
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7deeec2c2ee2c2d964b6495921eba0fa378bd8ee
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/21/2018
---
*Gilt für: Azure Advanced Threat Protection Version 1.9*

# <a name="investigating-lateral-movement-paths-with-azure-atp"></a>Untersuchen von Angriffen mit Lateral Movement-Pfaden mit Azure ATP

Azure ATP kann Ihnen dabei helfen, Angriffe mit Lateral Movement-Pfaden zu verhindern. Selbst wenn Sie sich sehr darum bemühen Ihre sensiblen Benutzer zu schützen, Ihre Administratoren komplexe Kennwörter haben, die regelmäßig geändert werden, deren Computer gehärtet sind, und ihre Daten sicher gespeichert werden, können Angreifer immer noch Lateral Movement-Pfade nutzen, um sich in Ihrem Netzwerk zwischen Benutzern und Computern bewegen zu können, bis sie auf den Jackpot in Sachen virtuelle Sicherheit stoßen: die sensiblen Anmeldeinformationen Ihres Administratorkontos.

## <a name="what-is-a-lateral-movement-path"></a>Was ist ein Lateral Movement-Pfad?

Lateral Movement bedeutet, dass ein Angreifer proaktiv nicht-sensible Konten benutzt, um Zugriff auf sensible Konten zu erhalten. Die Angreifer können alle Methoden verwenden, die im [Handbuch zu verdächtigen Aktivitäten](suspicious-activity-guide.md) beschrieben werden, um das erste nicht sensible Kennwort zu erhalten. Dann werden Tools wie Bloodhound verwendet, um herauszufinden, wer die Administratoren in Ihrem Netzwerk sind, und auf welche Computer sie zugegriffen haben. Mit den für Angreifer zugänglichen Daten auf Ihren Domänencontrollern kann herausgefunden werden, wer welche Konten bzw. Zugriff auf Ressourcen und Dateien hat, um dann die Anmeldeinformationen von anderen Benutzern (manchmal sensiblen Benutzern) zu stehlen, auf deren Computer sie bereits Zugriff hatten. Infolgedessen bewegen sie sich lateral durch weitere Benutzer und Ressourcen, bis sie Administratorrechte in Ihrem Netzwerk erlangen. 

Mit Azure ATP können Sie Lateral Movement-Angriffe in Ihrem Netzwerk präventiv verhindern.

## <a name="discovery-your-at-risk-sensitive-accounts"></a>Ermittlung Ihrer gefährdeten sensiblen Konten

Folgen Sie diesen Schritten, um zu ermitteln, welche sensiblen Konten in Ihrem Netzwerk aufgrund einer Verbindung mit nicht sensiblen Konten oder Ressourcen anfällig sind. Um Ihr Netzwerk vor Lateral Movement-Angriffen zu schützen, arbeitet Azure ATP rückwärts und gibt Ihnen eine Übersicht, die von Ihren privilegierten Konten ausgeht und Ihnen anzeigt, welche Benutzer und Geräte in den lateralen Pfaden dieser Benutzer und deren Anmeldeinformationen sind.

1. Klicken Sie im Menü des Azure ATP-Arbeitsbereichsportals auf das Symbol „Berichte“. ![Symbol „Berichte“](./media/atp-report-icon.png).

2. Wenn keine Lateral Movement-Pfade gefunden wurden, ist der Bericht unter **Lateral Movement-Pfade zu sensiblen Konten** abgeblendet. Wenn Lateral Movement-Pfade mit relevanten Daten gefunden wurden, wird aus den Daten des Berichts automatisch das frühste Datum ausgewählt. Der Bericht über Lateral Movement-Pfade enthält die Daten der letzten 60 Tage.

 ![Berichte](./media/reports.png)

3. Klicken Sie auf **Herunterladen**.

3. Die erstellte Excel-Datei gibt Ihnen Informationen über gefährdete sensible Konten. Die Registerkarte **Zusammenfassung** liefert Graphen mit Informationen über die Anzahl sensibler Konten und Computer, sowie Durchschnittswerte für gefährdete Ressourcen. Die Registerkarte **Details** enthält eine Liste von sensiblen Konten, um die Sie sich kümmern sollten.

4. Unter [Configure SAM-R (SAM-R konfigurieren)](install-atp-step8-samr.md) finden Sie Informationen darüber, wie Sie auf Ihren Servern Azure ATP das Ausführen von dem für die Lateral Movement-Pfad-Erkennung nötigen SAM-R-Vorgang erlauben.

## <a name="investigate"></a>Untersuchen

Da Sie nun wissen, welche sensiblen Konten gefährdet sind, können Sie tief in Azure ATP eintauchen und mehr darüber erfahren, wie man präventive Maßnahmen ergreift.

1. Suchen Sie im Azure ATP-Arbeitsbereichsportal nach dem Benutzer (z.B. Samira Abbasi), dessen Konto in **Lateral Movement-Pfade zu sensiblen Konten** als anfällig aufgelistet wird. Sie können auch nach dem Lateral Movement-Badge suchen, das dem Entitätsprofil hinzugefügt wird, wenn sich die Entität im ![Lateralen Symbol](./media/lateral-movement-icon.png) oder ![Pfadsymbol](./media/paths-icon.png) eines Lateral Movement-Pfads befindet. Dieses Badge ist verfügbar, wenn innerhalb der letzten zwei Tage Lateral Movement aufgetreten ist. 

2. Klicken Sie auf der sich öffnenden Benutzerprofilseite auf die Registerkarte **Lateral Movement-Pfade**. 

3. Das angezeigte Diagramm stellt Ihnen eine Übersicht der möglichen Pfade zu Ihrem sensiblen Benutzer bereit. Der Graph zeigt die Verbindungen der letzten zwei Tage an und ist somit aktuell. Wenn für die vergangenen zwei Tage keine Aktivitäten ermittelt werden, wird zwar der Graph nicht angezeigt, aber Sie können immer noch auf den [Bericht zu den Lateral Movement-Pfaden](reports.md) zugreifen, der Informationen zu den Lateral Movement-Pfaden der vergangenen 60 Tage enthält.

4. Überprüfen Sie den Graphen, um weitere Informationen über die Offenlegung der Anmeldeinformationen Ihres sensiblen Benutzers zu erhalten. Beispielsweise können Sie in der Übersicht von Samira Abbasi über den abgeblendeten Pfeil **Angemeldet als** anzeigen lassen, wo sich Samira mit ihren privilegierten Anmeldeinformationen angemeldet hat. In diesem Fall wurden Samiras sensible Anmeldeinformationen auf dem Computer „REDMOND-WA-DEV“ gespeichert. Überprüfen Sie anschließend, welche anderen Benutzer sich an welchen Computern angemeldet haben und die größte Offenlegung von Daten und das höchste Sicherheitsrisiko darstellten. Über den schwarzen Pfeil **Administrator auf** können Sie sich anzeigen lassen, wer Administratorrechte für die Ressource hat. In diesem Beispiel hat jeder in der Gruppe „Contoso All“ Zugriff auf die Benutzeranmeldeinformationen dieser Ressource.  

 ![Lateral Movement-Pfade zum Benutzerprofil](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>Empfohlene präventive Methoden

- Sie können Lateral Movement-Angriffe am Besten verhindern, indem sie sicherstellen, dass sensible Benutzer ihre Administratoranmeldeinformationen nur dann verwenden, wenn sie sich an gehärteten Computern anmelden. Wenn die Administratorin Samira Zugriff auf „REDMOND-WA-DEV“ benötigt, sollten Sie im Beispiel sicherstellen, dass sie sich mit einem anderen Benutzernamen und Kennwort anmeldet als ihren Administratoranmeldeinformationen.

- Außerdem wird empfohlen, sicherzustellen, dass niemand unnötige administrative Berechtigungen hat. Im Beispiel sollten Sie überprüfen, ob jeder in der Gruppe „Contoso All“ wirklich Administratorrechte für „REDMOND-WA-DEV“ benötigt.

- Es ist immer von Vorteil, wenn Personen nur Zugriff auf notwendige Ressourcen haben. Wie Sie im Beispiel sehen können, erweitert Oscar Posada Samiras Offenlegung von Daten signifikant. Ist es erforderlich, dass der Benutzer Mitglied in der Gruppe „Contoso All“ ist? Könnten Sie Untergruppen erstellen, um die Offenlegung von Daten zu minimieren?


## <a name="see-also"></a>Weitere Informationen

- [Configure SAM-R required permissions (Konfigurieren von für SAM-R erforderliche Berechtigungen)](install-atp-step8-samr.md)
- [Arbeiten mit verdächtigen Aktivitäten](working-with-suspicious-activities.md)
- [Weitere Informationen finden Sie im ATP-Forum.](https://aka.ms/azureatpcommunity)