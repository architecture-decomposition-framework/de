---
title: Dokumentation
nav_order: 5
layout: default
---

<!-- markdownlint-disable-next-line blanks-around-headings -->
# Architekturdokumentation mit dem ADF
{: .no_toc }

{: .highlight }
Eine Softwarearchitekturdokumentation macht Design-Entscheidungen über ein Software-System nachvollziehbar und hilft verschiedenen Stakeholdern, sich einen Überblick über das Software-System zu verschaffen.

<!-- markdownlint-disable-next-line blanks-around-headings -->
## Verwendung der Dokumentationsvorlage
{: .no_toc }

Die Dokumentationsvorlage enthält im ersten Abschnitt viele Hinweise zur Verwendung. Man kann sie sowohl nachträglich ausfüllen als auch Projektbegleitung zur Unterstützung der Architekturarbeit verwenden. Die Vorlage wird in einem separaten GitHub-Repo gepflegt und versioniert:

[Zur Vorlage (deutsch)](https://github.com/architecture-decomposition-framework/adf-documentation-template/blob/main/template/architecture-documentation-de.md){: .btn .btn-primary }
[Zur Vorlage (englisch)](https://github.com/architecture-decomposition-framework/adf-documentation-template/blob/main/template/architecture-documentation-en.md){: .btn .btn-primary }

Es gibt im [Repository der Vorlage](https://github.com/architecture-decomposition-framework/adf-documentation-template) auch eine DOCX-Version und eine Version, bei der die Vorlage über mehrere Dateien verteilt ist.

Um die Dokumentation einfach bearbeiten und möglichst vielen in aktueller Version zur Verfügung stellen zu können, empfiehlt sich die Vorgehensweise Documentation-as-Code, welche ausführlich unter folgendem Link beschrieben ist.

[Hinweise zum Tooling: Documentation-as-code](doc-as-code/){: .btn }

Weitere Themen in diesem Dokument:

- TOC
{:toc}

## Warum überhaupt Dokumentation schreiben?

Entgegen der Aussage mancher Entwickler:innen, **reicht der Quellcode** des Systems als alleinige Dokumentation **nicht aus**. Er beinhaltet zwar so aktuell wie sonst keine andere Dokumentation den aktuellen Stand des Systems - es ist aber viel zu aufwändig, für weitere Architekturentscheidungen aus diesem hohen Detailgrad die Architektur des Systems zu rekonstruieren. Hierfür braucht man eine **abstraktere Darstellung des Systems**, die die wesentlichen Strukturen und Beziehungen im System aufzeigt. Zudem ist im Quellcode üblicherweise nicht dokumentiert, **warum** gewisse Dinge genau so umgesetzt wurden und **welche alternativen Ansätze** verworfen wurden.

## Typischer Inhalt einer Architekturdokumentation

Wenn man sich verschiedene Architekturdokumentationen und Dokumentationsvorlagen ansieht, findet man darin häufig folgende Informationen:

- Architekturtreiber (also für die Architektur des Systems relevante Anforderungen) in Form von
  - **Geschäftszielen**,
  - **Randbedingungen** (technisch, organisatorisch, rechtlich, ...),
  - **Qualitätszielen** (Benutzbarkeit, Skalierbarkeit, Testbarkeit, ...) und
  - **Kernfunktionen** (wichtige Funktionalität, die das System brauchbar macht)
- einer Beschreibung des **System-Kontexts** (System versus mit dem System interagierende externe Systeme oder Dienste),
- Beschreibungen des Systems in **verschiedenen Detailgraden** (grobe funktionale Zerlegung, feinere Darstellung einzelner Services, ...)
- Beschreibungen des Systems von **verschiedenen Blickwinkeln** (Deployment, Interaktion von Systemteilen, Struktur des Quellcodes, ...), sowie
- Darstellungen verschiedener **Konzepte** (Logging, Backup, Skalierung, Mandantenfähigkeit, ...).

## Ziel der ADF-Dokumentationsvorlage

Die ADF-Dokumentationsvorlage zielt darauf ab, folgende Eigenschaften einer Architekturdokumentation zu begünstigen:

- **"durchlesegeeignet"**: Man kann also das Dokument von vorne bis hinten durchlesen ohne Bruch zwischen den einzelnen Kapiteln und ohne viele Sprünge durch Vorwärtsreferenzen.
- **Schnelles Grundverständnis des Systems**: Es gibt eine überschaubare Menge an Abschnitten, nach deren Durchlesen man mit dem wesentlichen fachlichen Kontext und der grundlegenden Architektur des Systems vertraut ist.
- **In sich Abgeschlossenheit der Kapitel**: Ein Grundverständnis des Systems vorausgesetzt, kann man die wesentlichen Aussagen eines Kapitels verstehen, ohne andere Kapitel gelesen zu haben.
- **Nachvollziehbarkeit der Architektur-Entscheidungen**: Es ist klar, warum bestimmte Entscheidungen getroffen wurden und welche Alternativen es gab.

{: .hint }
Inwiefern diese Ziele tatsächlich erreicht werden, hängt natürlich maßgeblich davon ab, wie gut die konkrete Dokumentation letztlich geschrieben ist.
