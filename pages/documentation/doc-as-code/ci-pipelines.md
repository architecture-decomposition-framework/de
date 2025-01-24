---
title: CI-Pipelines
parent: Documentation-as-code
nav_order: 3
layout: default
---

# CI für Documentation-as-code

Hier sind ein paar nützliche Pipelines zur Überprüfung/Verarbeitung der Dokumentation, die wir in unseren CI-Build-Prozess integrieren können.

## Markdown-Linting

Um den Markdown-Stil zu vereinheitlichen und defekte Links zu vermeiden, wird ein Markdown-Linter wie [markdownlint](https://github.com/DavidAnson/markdownlint) dringend empfohlen. Wir können in der Markdown-Datei selbst oder in einer Projektkonfigurationsdatei festlegen, welche Regeln verwendet werden sollen. Diese Regeln werden dann sowohl vom [Kommandozeilen-Tool](https://github.com/igorshubovych/markdownlint-cli) als auch von der [VS Code-Erweiterung](https://github.com/DavidAnson/markdownlint) beachtet.

Als Beispiel dient [diese GitHub-Aktion](https://github.com/neshanjo/what2eat/blob/with-cache/.github/workflows/lint-markdown.yml), die markdownlint ausführt, um nach Fehlern zu suchen. Die Projektkonfiguration befindet sich in [dieser Datei](https://github.com/neshanjo/what2eat/blob/with-cache/.markdownlint.jsonc).

## PDF-Generierung

Wie in [diesem Artikel](generate-pdf-from-markdown.md) beschrieben, kann eine aktuelle PDF-Version der Dokumentation nützlich sein.

[Diese GitHub-Action](https://github.com/neshanjo/what2eat/blob/with-cache/.github/workflows/markdown-to-pdf.yml) verwendet pandoc und weasyprint[^1], um eine PDF-Dokumentation zu erstellen und als Release zu veröffentlichen. Durch die Release-Veröffentlichung kann die neueste Version über den permanenten Link <https://github.com/neshanjo/what2eat/releases/latest/download/architecture-documentation.pdf> heruntergeladen werden.

[^1]: Die Action verwendet nicht pagedjs-cli, da die Installation von weasyprint auf dem GitHub-Runner über apt-get viel schneller geht als die npm-Installation von pagedjs-cli.
