---
title: Documentation-as-code
parent: Dokumentation
nav_order: 4
layout: default
---

<!-- markdownlint-disable-next-line blanks-around-headings -->
# Documentation-as-code (ADF) <!-- omit in toc -->
{: .no_toc }

<!-- markdownlint-disable-next-line blanks-around-headings -->
## Content <!-- omit in toc -->
{: .no_toc }

- TOC
{:toc}

## Was ist Documentation-as-code?

*Documentation-as-code* bedeutet,

1. die Dokumentation (in der Regel die Architekturdokumentation) so nah wie möglich am Quellcode abzulegen und sicherzustellen, dass sie unter Versionskontrolle steht,
2. ein Format zu wählen, das jede:r Entwickler:in mit wenig Aufwand bearbeiten kann, und
3. die aktuelle Dokumentation für alle (einschließlich nicht-technische Personen) in einem leicht konsumierbaren Format zugänglich zu machen.

## Warum Documentation-as-code?

Die meisten Entwickler implementieren lieber neue Funktionen als ihre Architektur zu dokumentieren. Wenn sie für die Dokumentation zusätzlich gezwungen sind, ihre vertraute Entwicklungsumgebung zu verlassen, um sich mit störrischen Word-Vorlagen und Dokumenten auf VPN-geschützten Netzlaufwerken auseinanderzusetzen, sinken die Chancen auf eine aktuelle Dokumentation beträchtlich. Um eine aktuelle, leicht zugängliche Dokumentation zu haben, brauchen wir etwas anderes als das.

## Documentation-as-code, generische Umsetzung

In der Regel werden die drei oben genannten Punkte auf diese Weise umgesetzt.

Schritt 1: Wir erstellen einfach einen Ordner für die Dokumentation im Projekt-Repository (z.B. Git-Repository), das auch den entsprechenden Quellcode enthält. Wenn wir mehrere Repositories für verschiedene Teile der Software haben und mehr als einen Teil gleichzeitig dokumentieren müssen, kann ein zusätzliches Repository notwendig sein allerdings schafft das eine zusätzliche Indirektion (ein Mono-Repo-Ansatz kann hier helfen).

Schritt 2: Wir wählen ein Plaintext-Format wie Markdown, AsciiDoc, LaTeX oder HTML. Wir entscheiden, welches Format wir für Grafiken verwenden, z.B. Vektorgrafikformate mit IDE-Plugin-Unterstützung wie Diagrams.net/Draw.io oder Diagramm-as-Code-Formate wie PlantUML.

Schritt 3: Mit jedem Commit generieren wir eine benutzerfreundliche Rich-Text-Version der Dokumentation. Im einfachsten Fall ist das die Webdarstellung von Markdown oder Asciidoc durch den Git-Server. Es kann aber auch ein komplexerer CI-Build-Prozess sein, der LaTeX ausführt und PDFs auf ein Netzwerk-Dateisystem veröffentlicht.

## Documentation-as-code, die ADF-Umsetzung

In diesem Abschnitt beschreiben wir unsere Wahl der Werkzeuge und Technologien zur Umsetzung der Schritte 1 bis 3. Es gibt viele andere Möglichkeiten mit flexibleren und weiter fortgeschrittenen Funktionen. Wir wählen absichtlich eine der einfachsten Lösungen, um die Einstiegshürde so niedrig wie möglich zu halten.

Diese Toolchain wurde erfolgreich in verschiedenen Studierenden-Projekten eingesetzt, und benötigte selbst bei unerfahrenen Entwickler:innen nicht mehr als 60 Minuten Einführungszeit.

### Schritt 1 und Schritt 3

Wir gehen davon aus, dass der Quellcode in einem Repository auf einem Git-Server liegt, der Markdown-zu-HTML-Rendering unterstützt, z.B. GitHub oder GitLab. Wir erstellen einfach einen Ordner `documentation` mit einer Datei `architecture-documentation.md` und dem Inhalt der [ADF-Architekturdokumentationsvorlage](https://github.com/architecture-decomposition-framework/adf-documentation-template), siehe auch Abschnitt [Dokumentation](../).

Sobald wir die Änderungen committen und auf den Server pushen, erhalten wir eine HTML-Seite mit der gerenderten Dokumentation und können sie einfach über den Link zum Repository weitergeben. Auch Nicht-Entwickler können auf dem Git-Server Rollen mit eingeschränktem Zugriff erhalten (wie die Reporter-Rolle in GitLab), sodass sie die Dokumentation ansehen können.

Dies funktioniert auch gut mit verschiedenen (Feature-)Branches mit einer (vorläufig) aktualisierten Version der Dokumentation, die von anderen Personen überprüft werden kann (z.B. im Rahmen eines Code-Reviews).

### Schritt 2

Wie der vorherige Abschnitt bereits andeutet, verwenden wir [Markdown](https://en.wikipedia.org/wiki/Markdown) als Plaintext-Format. Wir tun dies, da es das einfachste Format zur Erstellung von Rich-Text-Dokumenten ist und in anderen Kontexten (z.B. Wikis) weit verbreitet ist. Es hat fast keine Lernkurve und es gibt eine hervorragende Werkzeugunterstützung - fast jede IDE unterstützt Syntaxhervorhebung und einige Autovervollständigungs- und Autoformatierungsfunktionen.

Für Diagramme gibt es zwei Optionen:

- [Verwendung von Diagrams.net (ehemals draw.io)](../../views/tooling/diagrams-net-elements.html), ein Open-Source-Diagrammerstellungstool, das den Diagrammcode direkt in die Ausgabedatei einbetten kann (SVG oder PNG).
- [Verwendung von PlantUML](../../views/tooling/plantuml-elements.html), bei dem Diagramme als Code spezifiziert und von der IDE, einem Kommandozeilen-Tool oder während des Build-Prozesses gerendert werden.

Unter den obigen Links finden wir weitere Informationen zur Einrichtung der Werkzeuge in Kombination mit Markdown. Außerdem beschreiben wir im [Sichten-Abschnitt](../../views/), wie wir Architektursichten systematisch und konsistent erstellen.

### Beispiele

[Diese Beispieldokumentation](https://github.com/neshanjo/what2eat/blob/with-cache/doc/architecture-documentation.md) ist in Markdown geschrieben und bettet direkt Abbildungen ein, die mit Diagrams.net erstellt wurden. Die gleiche Dokumentation, aber mit Abbildungen von PlantUML erstellt, findet man [unter diesem Link](https://github.com/neshanjo/what2eat/blob/with-cache/doc-plantuml/architecture-documentation-plantuml.md).

### PDF-Dokumente aus Markdown generieren

Es ist manchmal notwendig, bestimmte Versionen der Dokumentation zu archivieren oder per E-Mail zu versenden. Daher kann [PDF-Generierung aus Markdown](./generate-pdf-from-markdown.html) hilfreich sein.

## Presentation-as-code

Dank [Marp](https://marp.app/), dem Markdown Presentation Ecosystem, können einfache und effektive Präsentationen leicht erstellt werden, indem Markdown-Code und Abbildungen aus der Dokumentation wiederverwendet werden. Das Plugin [Marp für VS Code](https://marketplace.visualstudio.com/items?itemName=marp-team.marp-vscode) integriert Marp in VS Code.

Das What2Eat-Beispielprojekt enthält auch ein [Marp-Beispiel](https://raw.githubusercontent.com/neshanjo/what2eat/with-cache/doc/architecture-presentation.md), das einige der Funktionen in Marp veranschaulicht. Achtung: die [von GitHub gerenderte Version](https://github.com/neshanjo/what2eat/blob/with-cache/doc/architecture-presentation.md) ist *nicht* die resultierende Präsentation. Wie die endgültige Präsentation aussieht, kann man in [dieser PDF-Datei](https://raw.githubusercontent.com/neshanjo/what2eat/with-cache/doc/architecture-presentation.pdf) sehen.
