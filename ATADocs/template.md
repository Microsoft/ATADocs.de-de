---
# required metadata

title: [TITEL DES ARTIKELS | DIENSTNAME]
description:
keywords:
author: [GITHUB USERNAME]
manager: [ALIAS]
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: [GET ONE FROM guidgenerator.com]

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
#ms.reviewer: [ALIAS]
#ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Metadaten- und Markdown-Vorlage

Diese docs.ms-Vorlage enthält Beispiele für Markdown-Syntax sowie Anleitungen zum Festlegen der Metadaten. Sie steht im Stammverzeichnis jedes EM-Pilotrepositorys (z. B. „~/Azure-RMSDocs-pr /template.md“) zur Verfügung und soll als Markdown-Datei gelesen werden, obwohl Sie die [veröffentlichte Version](https://stage.docs.microsoft.com/en-us/rights-management/template) verwenden können, um festzustellen, wie die Markdown-Beispiele dargestellt werden.

Beim Erstellen einer Markdown-Datei sollten Sie die Vorlage in eine neue Datei kopieren, die Metadaten wie unten angegeben ausfüllen, die H1-Überschrift oben auf den Titel des Artikels festlegen und den Inhalt löschen. 


## Metadaten 

Den vollständigen Metadatenblock finden Sie oben, unterteilt in erforderliche Felder und optionale Felder. Weitere Informationen finden Sie auf dem [OPS-Metadatenmerkblatt](https://ppe.msdn.microsoft.com/en-us/ce-csi-docs/ops/ops-onboarding/managing-content/content-meta-data). Wichtige Hinweise:

- Sie **müssen** ein Leerzeichen zwischen dem Doppelpunkt (:) und dem Wert für ein Metadatenelement einfügen.
- Wenn ein optionales Metadatenelement keinen Wert aufweist, kommentieren Sie das Element mit einem # (lassen Sie es nicht leer und verwenden Sie kein „na“). Wenn Sie einen Wert einem Element hinzufügen, das auskommentiert wurde, sollten Sie das # unbedingt löschen.
- Doppelpunkte in einem Wert (z. B. ein Titel) unterbrechen den Metadaten-Parser. Verwenden Sie stattdessen die HTML-Codierung „&#58;“ (z. B. „Titel: Azure Rights Management&#58; die Grundlagen | Azure RMS“).
- **Titel**: Dieser Titel wird in Suchergebnissen angezeigt. Der Titel sollte mit einem senkrechten Strich (|) gefolgt vom Namen des Diensts (z. B. siehe oben) enden. Der Titel muss nicht (und sollte nicht) mit dem Titel in der H1-Überschrift übereinstimmen. Er sollte ungefähr 65 Zeichen (einschließlich | NAME DES DIENSTS) umfassen.
- **Autor**, **Manager**, **Prüfer**: Das Autorenfeld sollte den **Github-Benutzernamen** des Autors enthalten, nicht den Alias.  Die Felder „Manager“ und „Prüfer“ sollten andererseits Aliasnamen enthalten. „ms.reviewer“ gibt den Namen des Projektmanagers an, der dem Artikel oder Dienst zugeordnet ist.
- **ms.assetid**: Dies ist die GUID des Artikels in Großbuchstaben. Wenn Sie eine neue Markdown-Datei erstellen, rufen Sie eine GUID von [https://www.guidgenerator.com](https://www.guidgenerator.com) ab. 
- **ms.prod**, **ms.service**, **ms.technology**, **ms.devlang**, **ms.topic**, **ms.tgt_pltfrm**: Mögliche Werte für diese Elemente finden Sie [hier](https://microsoft.sharepoint.com/teams/STBCSI/Insights/_layouts/15/WopiFrame.aspx?sourcedoc=%7b7A321BF1-0611-4184-84DA-A0E964C435FA%7d&file=WEDCS_MasterList_CSIValues.xlsx&action=default).

## Grundlegendes Markdown und GFM

Alle grundlegenden und Github-flavored Markdowns werden unterstützt. Weitere Informationen dazu finden Sie unter:

- [Baseline-Markdown-Syntax](https://daringfireball.net/projects/markdown/syntax)
- [GFM-Dokumentation (Github-flavored Markdown)](https://guides.github.com/features/mastering-markdown)

## Überschriften

Beispiele für Überschriften der ersten und zweiten Ebene finden Sie oben. 

Im Thema **darf nur** eine Überschrift der ersten Ebene vorhanden sein, die als Titel auf der Seite angezeigt wird.  

Überschriften der zweiten Ebene generiert das Inhaltsverzeichnis auf der Seite, die im Abschnitt „In diesem Artikel“ unter dem Seitentitel angezeigt wird.

### Überschrift der dritten Ebene
#### Überschrift der vierten Ebene
##### Überschrift der fünften Ebene
###### Überschrift der sechsten Ebene

## Textformat

*Kursiv* 

**Fett** 

~~Durchgestrichen~~



## Links

Verwenden Sie für die Verknüpfung mit einer Markdown-Datei im gleichen Repository [relative Links](https://www.w3.org/TR/WD-html40-970917/htmlweb.html#h-5.1.2). 

- Beispiel: [Was ist Azure Rights Management?](./understand-explore/what-is-azure-rights-management.md)

Um einen Header in der gleichen Markdown-Datei zu verknüpfen, zeigen Sie die Quelle des veröffentlichten Artikels an, suchen Sie nach der ID des Headers (z. B. `id="blockquote"`), und verknüpfen Sie mit # + ID (z. B. `#blockquote`).

- Beispiel: [Blockquotes](#blockquote)

Verwenden Sie für die Verknüpfung mit einem Header in einer Markdown-Datei im gleichen Repository relative Links und Hashtag-Links.

- Beispiel: [technische Übersicht des Anmeldevorgangs](./understand-explore/rms-for-individuals-user-signup.md#technical-overview-of-the-sign-up-process)

Um eine externe Datei zu verknüpfen, verwenden Sie den vollständigen URL als Link.

- Beispiel: [Github](http://www.github.com)

Wenn eine URL in einer Markdown-Datei angezeigt wird, wird sie in einen klickbaren Link umgewandelt.

- Beispiel: http://www.github.com

## Listen

### Sortierte Listen

1. Dieses 
1. Ist
1. Eine
1. Sortierte
1. List  


#### Sortierte Liste mit einer eingebetteten Liste

1. Here
1. kommt
1. eine
1. eingebettete
    1. Miss Scarlett
    1. Professor Plum
1. sortierte
1. list


### Unsortierte Listen

- Dieses
- ist
- einer
- Aufzählung
- list


##### Unsortierte Liste mit einer eingebetteten Liste

- Dieses 
- Aufzählung 
- list
    - Mrs. Peacock
    - Mr. Green
- enthält  
- Andere
    1. Colonel Mustard
    1. Mrs. White
- Listen


## Horizontale Regel

---

## Tabellen

| Tabellen        | Sind           | Gut  |
| ------------- |:-------------:| -----:|
| Sp 3 ist      | rechtsbündig | $1600 |
| Sp 2 ist      | zentriert      |   $12 |
| SP 1 ist der Standard | linksbündig     |    $1 |


## Code

### Codeblock

    function fancyAlert(arg) {
      if(arg) {
        $.docs({div:'#foo'})
      }
    }

### Inlinecode

Dies ist ein Beispiel für `in-line code`.

## Blockquotes

> Die Trockenheit hatte nun zehn Millionen Jahre angedauert, und die Herrschaft der schrecklichen Echsen hatte längst geendet. Hier am Äquator, in dem Kontinent, der eines Tages zu Afrika werden würde, hatte der Kampf ums Überleben eine neue Wildheit erreicht, und ein Sieger war noch nicht in Sicht. In diesem trostlosen und verdorrten Land konnte nur der Kleine, der Schnelle oder der Wilde gedeihen oder zumindest überleben.

## Bilder

### Statisches Bild

![dies ist der alternative Text](./media/AzRMS_elements.png)

### Verknüpftes Bild

[![aalternativer Text für verknüpftes Bild](./media/AzRMS_elements.png)](https://azure.microsoft.com) 

### Animiertes GIF

![Animiertes GIF](./media/hololens.gif)

## Warnungen

### Hinweis

> [!NOTE] Dies ist ein HINWEIS

### Warning

> [!WARNING] Dies ist eine WARNUNG

### Tipp

> [!TIP] Dies ist ein TIPP

### Wichtig

> [!IMPORTANT] Dies ist WICHTIG

## Videos

### Channel 9

<iframe src="http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>


### YouTube

<iframe width="420" height="315" src="https://www.youtube.com/embed/R6_eWWfNB54" frameborder="0" allowfullscreen></iframe>

## docs.ms-Erweiterungen
Die folgenden Erweiterungen sind verfügbar:

### Schaltfläche

> [!div class="button"] [Schaltflächenlinks](/rights-management)

### Selector

> [!div class="op_single_selector"]
- [foo](/rights-management/template.md)
- [bar](/rights-management/scratch.md)

### Schrittweise

>[!div class="step-by-step"] [Zurück](https://www.example.com)
[Weiter](https://www.example.com)

<!--HONumber=May16_HO3-->


