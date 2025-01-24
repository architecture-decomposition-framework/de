---
title: Tooling
parent: Modellierung/Visualisierung
nav_order: 4
layout: default
---

# ADF-Elemente, Tool-Support

Die ADF-Elemente basieren auf typischen UML-Elementen wie *Node*, *Component* und *Class*. Wir stellen diese für zwei beliebte Tools zur Verfügung, die sich prinzipiell unterscheiden.

Mit **Diagrams.net (ehemals draw.io)** steht ein mächtiges, offenes Diagramm-Werkzeug zur Verfügung, welches als Plugin auch in vielen Entwicklungsumgebungen läuft und den Diagramm-Code direkt in das Zielformat (PNG oder SVG) einbetten kann.

[ADF-Sichten mit Diagrams.net](diagrams-net-elements.html){: .btn .btn-primary }

**PlantUML** verfolgt einen anderen Ansatz: Hier werden Diagramme als Code spezifiziert (*Diagrams-as-code*) und über Kommandozeilentools oder den Build-Prozess in Grafiken umgewandelt (z.B. PNG oder SVG). PlantUML kann hervorragend in Markdown eingebettet werden und minimiert den Medienbruch bei der Diagrammerstellung. LLMs wie GitHub-Copilot können hier nicht nur syntaktisch, sondern auch semantisch unterstützen. Allerdings ist der initiale Einarbeitungsaufwand höher - und das Layout nicht immer genau so, wie man es gerne hätte.

[ADF-Sichten mit PlantUML](plantuml-elements.html){: .btn .btn-primary }
