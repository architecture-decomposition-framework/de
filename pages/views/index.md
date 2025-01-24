---
title: Modellierung/Visualisierung
nav_order: 6
layout: default
---

<!-- markdownlint-disable-next-line blanks-around-headings -->
# Architektur-Modellierung/-Visualisierung mit dem ADF
{: .no_toc }

{: .highlight }
Es ist sinnvoll, ein komplexes System nicht in einem einzelnen Diagramm zu beschreiben, sondern mehrere Diagramme für verschiedene Aspekte anzulegen. 
**Das ADF-Framework definiert verschiedene Sichtentypen samt zugehöriger Elemente und Relationen.** So erkennt man bei einem Diagramm vom Sichtentyp "Funktionen zur Laufzeit" direkt die funktionalen Teilbereiche, ihre Aufteilung und ihr Zusammenspiel. Im Gegensatz zur Gebäude-Architektur (Stichwort "Flurplan" oder "Grundriss") hat sich im Software-Engineering keine einheitliche Notation durchgesetzt, und oft werden viele unterschiedliche Aspekte in einem Diagramm vermischt.

<!-- markdownlint-disable-next-line blanks-around-headings -->
## Verwendung der ADF-Sichten
{: .no_toc }

Zunächst sollte man verstehen, anhand welcher Dimensionen man ein System zerlegen kann (*decomposition*) und welche Sichtentypen es gibt.

[Erklärung der Dimensionen](dimensions/){: .btn .btn-primary }

Für eine Architektursicht eines bestimmten Typs gibt es passende Elemente und Relationen.

[Übersicht über die Elemente](elements/){: .btn .btn-primary }

Am besten sieht man sich ein paar Beispiele für Sichten verschiedener Sichtentypen an.

[Beispiele](examples/){: .btn .btn-primary }

<!-- markdownlint-disable-next-line blanks-around-headings -->
## Tooling
{: .no_toc }

Architektur-Modellierung/-Visualisierung mit dem ADF ist eine Methode, die unabhängig von Tools und Technologien verwendet werden kann. ADF-Sichten kann man mit beliebigen Diagramm-Tools oder auch direkt auf dem Whiteboard zeichnen. Für die Tools Diagrams.net und PlantUML haben wir vorgefertigte Elemente und Relationen erstellt, die man direkt verwenden kann.

[Zum Tooling](tooling/){: .btn }

Weitere Themen in diesem Dokument:

- TOC
{:toc}

## Wozu verschiedene Sichten?

<!-- Englisch We use to breakdown complex matters into manageable chunks all the time. To understand how the human body works, a medical student uses many different figures illustrating the skeleton, the muscle apparatus, the vascular system, ... - and even different diagrams for different body parts. The house building architect makes a site plan as an overview, floor plans for each story, different perspectives of outer walls and the roof construction and dedicated diagrams showing power lines and outlets. So what about software?

> “It is not possible to capture the functional features and quality properties of a complex system in a single comprehensible model that is understandable by and of value to all stakeholders.” [Rozanski, Woods, 2005]

While it is tempting to describe a software system in its full detail within one big diagram (and people try and fail doing so again and again), a much more feasible approach is to describe a system from different views.
-->
Wir zerlegen komplexe Materie ständig in handhabbare Teile. Um zu verstehen, wie der menschliche Körper funktioniert, verwendet ein Medizinstudent viele verschiedene Abbildungen, die das Skelett, das Muskelsystem, das Gefäßsystem usw. darstellen - und auch unterschiedliche Bilder für verschiedene Körperteile. Der Gebäude-Architekt erstellt einen Flurplan als Übersicht, Grundrisse für jede Etage, verschiedene Ansichten der Außenwände und der Dachkonstruktion sowie spezielle Diagramme, die Stromleitungen und Steckdosen zeigen. Und wie sieht es bei Software aus?

> „Es ist nicht möglich, die funktionalen Merkmale und Qualitätsmerkmale eines komplexen Systems in einem einzigen verständlichen Modell zu erfassen, das für alle Beteiligten verständlich und wertvoll ist.“ [Rozanski, Woods, 2005]

Während es verlockend ist, ein Softwaresystem in all seinen Details in einem großen Diagramm zu beschreiben (viele Leute versuchen das und scheitern regelmäßig daran), ist ein viel praktikablerer Ansatz, ein System aus verschiedenen Blickwinkeln zu beschreiben.

## Kein Standard für Architektursichten

UML-Klassen-, Package- und Sequenz-Diagramme, welche die Code-Struktur darstellen, sind weit bekannt und verbreitet, haben aber zwei Nachteile:

1. Sie beschreiben viele Implementierungsdetails, die für eine Gesamtübersicht vielleicht gar nicht so relevant sind und auch schnell veralten. (Manche Leute empfehlen daher, diese wenig zu benutzen und sie am besten automatisiert aus dem Code zu generieren.)
2. Man kann sie erst dann erstellen, wenn bereits Quellcode existiert oder man zumindest weiß, an welcher Stelle Code geschrieben werden muss (Frontend versus Backend, Modul im Monolith versus eigener Microservice, ...). Bei Neuentwicklungen ist es sinnvoller, erst vom laufenden System auszugehen, dieses in Einzelteile zu zerlegen und dann zu überlegen, wie diese Teile als Code umgesetzt werden.

Für **Architekturarbeit** braucht man also Sichten,

- die größere Zusammenhänge visualisieren, wie z.B. das Zusammenspiel mehrerer Systeme,
- die Systeme und Komponenten zur Laufzeit beschreiben,
- das Deployment des Systems in der Infrastruktur zeigen,
- Entwicklungs- und Deployment-Prozesse abbilden,
- u.v.m.

Obwohl es verschiedene Architektursichten-Frameworks gibt, wie z.B. das 4+1 Modell von Philippe Kruchten oder das C4-Modell von Simon Brown, hat sich keines davon als allgemeiner Standard durchgesetzt. Ersteres hat aufgrund der Vielzahl unterschiedlicher Diagrammtypen und Elemente eine steile Lernkurve, letzteres engt mit den vier fest vorgegebenen "Zoomstufen" stark ein. Vor allem unterscheiden die meisten Modelle nicht zwischen Sichten auf ein System **zur Laufzeit** und Sichten auf ein System **zur Entwicklungszeit**.

Mit dem **ADF-Sichtenframework** stellen wir ein Modell zur Visualisierung und Modellierung von Software-Systemen zur Verfügung, welches

- **frei verwendbar** ist,
- **für alle System-Arten geeignet** ist,
- durch ein explizites Typsystem entlang der Dimensionen Laufzeit/Entwicklungszeit und Daten/Funktionen/Deployment/Aktivitäten **ganz deutlich macht, welchen Aspekt des Systems man beschreibt** und damit hilft, nicht zu viele verschiedene Aspekte eines Systems zu vermischen.
- ohne Software-Installation [mit einem Klick sofort einsetzbar ist](https://app.diagrams.net/?splash=0&libs=general&clibs=Uhttps%3A%2F%2Fraw.githubusercontent.com%2Farchitecture-decomposition-framework%2Fadf-diagramsnet%2Fmain%2Flibraries%2FADF_SW%40RT.xml;Uhttps%3A%2F%2Fraw.githubusercontent.com%2Farchitecture-decomposition-framework%2Fadf-diagramsnet%2Fmain%2Flibraries%2FADF_Env%40RT.xml;Uhttps%3A%2F%2Fraw.githubusercontent.com%2Farchitecture-decomposition-framework%2Fadf-diagramsnet%2Fmain%2Flibraries%2FADF_SW%40DT.xml;Uhttps%3A%2F%2Fraw.githubusercontent.com%2Farchitecture-decomposition-framework%2Fadf-diagramsnet%2Fmain%2Flibraries%2FADF_Env%40DT.xml),
- Tool-Support durch [diagrams.net (draw.io)](tooling/diagrams-net-elements.html) und [PlantUML](tooling/plantuml-elements.html) hat und damit voll kompatibel zu dem Ansatz [Documentation-as-code](../documentation/doc-as-code/) ist,
- auf dieser Seite hier **ausführlich und mit Beispielen dokumentiert** ist.

Die [ADF-Dokumentationsvorlage](../documentation/) komplimentiert das ADF-Sichtenframework, indem sie eine Struktur schafft, in der die Sichten eingebettet werden können.

Der [ADF-Design-Guide](../design/) zeigt, in welchen Iterationen man sich an eine System-Zerlegung annähert und welche Sichten welchen Typs dabei entstehen.
