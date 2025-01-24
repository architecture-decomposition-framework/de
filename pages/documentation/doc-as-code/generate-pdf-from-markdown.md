---
title: Markdown in PDF umwandeln
parent: Documentation-as-code
nav_order: 2
layout: default
---

<!-- markdownlint-disable-next-line blanks-around-headings -->
# PDF aus Markdown generieren <!-- omit in toc -->
{: .no_toc }

Es gibt Situationen, in denen ein Link zum Git-Server nicht geeignet ist, z.B. bei der Kommunikation mit externen Stakeholdern, und wir lieber eine PDF-Dokumentation erstellen wollen. Dafür stellen wir hier verschiedene Ansätze vor (mit unterschiedlichem Einrichtungsaufwand).

<!-- markdownlint-disable-next-line blanks-around-headings -->
## Inhalt <!-- omit in toc -->
{: .no_toc }

- TOC
{:toc}

## Lösung 1: HTML-Druck aus einem Browser (keine weitere Tool-Installation erforderlich)

Einfach die Git-Server-Seite im Browser aufrufen und den integrierten PDF-Drucker verwenden (funktioniert z.B. mit Firefox oder Chrome).

Für eine lokale (offline) Lösung können wir die "Print current document to HTML"-Funktion in VS Code verwenden, die vom Markdown all-in-one Plugin bereitgestellt wird, es im Browser öffnen und von dort aus drucken.

Es gibt auch ein VS Code Plugin namens Markdown PDF, das diesen Schritt noch weiter vereinfacht, aber einen kompletten Chromium-Browser innerhalb von VS Code installiert.

## Lösung 2: Kommandozeilenskript (Pandoc + pagedjs)

Eine bevorzugte Lösung ist ein einfaches Kommandozeilenskript, das auch auf einem Build-Server ausgeführt werden kann, um bei jedem Build aktualisierte Dokumentationen zu erstellen.

### Installation und Nutzung

Wir zeigen zuerst das Skript und eine Tool-Installationsanleitung und erklären dann einige Details, die beim Anpassen des Skripts, Stils oder Workflows hilfreich sein können.

Man braucht für das Skript eine Linux/Unix-Shell. Unter Windows wird z.B. die Git Bash mit der Installation von Git für Windows mitgeliefert.

Wir installieren [pandoc](https://pandoc.org/installing.html) - wird verwendet, um Markdown in HTML zu konvertieren.

Dann installieren wir die [CLI-Version von paged.js](https://pagedjs.org/documentation/2-getting-started-with-paged.js/#command-line-version) - wird verwendet, um HTML in PDF zu konvertieren.

Wir testen, ob die `pandoc` und `pagedjs-cli` Befehle im PATH verfügbar und mit der Shell ausführbar sind.

Wir kopieren die Markdown-Datei, die wir konvertieren möchten, und die Skripte in [md2pdf](md2pdf/) in einen gemeinsamen Ordner.

Wir führen `./md2pdf markdownfile.md` in diesem Ordner aus.

Nun sollte eine markdownfile.pdf-Datei mit dem konvertierten Dokument verfügbar sein.

Hinweis: Wir können das Skript in jeden Ordner innerhalb unseres PATH legen, um den Befehl von überall auszuführen, müssen jedoch sicherstellen, dass der Pfad zur CSS-Datei im pagedjs-cli-style-Argument als absoluter Pfad angegeben ist, z.B. `--style "C:\Scripts\md2pdf.css"`.

### Hintergrundinformationen

Das Skript generiert zuerst einen Dateinamen für eine temporäre HTML-Datei im Format markdownfile-timestamp.html.

Es wird pandoc signalisiert, dass das Markdown als Github flavored markdown geschrieben ist (`-t gfm`).

Die HTML-Ausgabe von pandoc ist sehr einfach. Deshalb gibt es das `md2pdf.css` Stylesheet, das den GitHub-Stil zum HTML hinzufügt. Das können wir natürlich anpassen. Wichtig ist die Beibehaltung von `page-break-after: avoid;` für die Überschrift, z.B. durch

```css
h1, h2, h3, h4, h5, h6 {
  page-break-after: avoid;
}
```

Der untere Teil von `md2pdf.css` konfiguriert die Seitengröße und Ränder. Wir können es anpassen, um [andere Formate](https://pagedjs.org/documentation/5-web-design-for-print/) zu verwenden.

## Andere Lösungen: weasyprint und LaTeX

Ein weiteres Tool zur Konvertierung von HTML in PDF ist [weasyprint](https://weasyprint.org/). Es kann als Alternative zu pagedjs verwendet werden, siehe z.B. [diese GitHub Action](https://github.com/neshanjo/what2eat/blob/34e8198ca0260ad75868e4523ed038118b0ff515/.github/workflows/markdown-to-pdf.yml#L25).

Wir können auch LaTeX für die PDF-Erstellung verwenden, was wahrscheinlich zu einer besseren Layout-Qualität führt. Es erfordert jedoch eine vollständige LaTeX-Installation auf allen Rechnern, die zur Erstellung von PDFs verwendet werden. Dieser Ansatz wurde vom Autor dieser Anleitung noch nicht getestet, aber detaillierte Anweisungen finden sich auf <https://learnbyexample.github.io/customizing-pandoc/>.
