---
name: app-content
description: Use for any content work in this app - researching, writing, extending, correcting or reviewing its competencies, chapters, pages, rounds, questions, exercises, figures, terms or sources. This app's own content decisions; they take precedence over the generic lernapps content skills. Load it before you change any content.
---

# Content guide of this app

Das Naturwunder-Quiz (archetype `quiz`): 25 Fragen zu Naturwundern der Erde, Erdkunde, Klassen 5 bis 10. Der Inhalt
steht in einer Datei, `src/quiz.json` (Schema quiz.v1); die Bilder liegen in `src/images/`. Code, Konfiguration und
Tests der App werden nicht geändert (`quiz-only-data`, `keep-the-preset`).

## Curriculum

- Fach Erdkunde (Geografie), weiterführende Schulen (Gymnasium, Realschule und andere), Klassen 5 bis 10. Die
  Lernenden wissen schon, was Ozeane und Kontinente sind.
- Kein Lehrplan zugrunde gelegt: Der Ersteller hat keinen genannt, das Quiz übt Allgemeinwissen zu Naturwundern und
  macht neugierig. Ein Lehrplan ist willkommen, aber nicht nötig; kommt einer dazu, steht hier Dokument,
  Herausgeber, Jahr, Adresse und Einheit je Thema.
- Inhaltlich folgt die App der deutschsprachigen Wikipedia (Stand Oktober 2026). Weicht ein Schulbuch ab, gilt der
  Wikipedia-Artikel der Frage; die Abweichung steht dann in `explanation`.
- Biologie wäre später eine eigene Rubrik (eigenes Quiz), nicht Teil dieser App.

## Competencies

Jede Kompetenz hat ihre Fragen (Frage-IDs in `src/quiz.json`, in dieser Reihenfolge in der Datei):

- **Gebirge und Vulkane.** Ich kann die Höhe des Mount Everest nennen (`everest-hoehe`), den Kilimandscharo seinem Land
  zuordnen (`kilimandscharo-land`), den höchsten aktiven Vulkan Europas nennen (`aetna-vulkan`), den höchsten Berg
  Amerikas nennen (`aconcagua`) und sagen, ob das Matterhorn der höchste Berg der Alpen ist (`matterhorn-alpen`).
- **Wasserfälle, Flüsse und Seen.** Ich kann den Fluss an den Victoriafällen nennen (`sambesi-victoriafaelle`), ihre
  Breite schätzen (`victoriafaelle-breite`), die Wasserfälle an der Grenze von Argentinien und Brasilien nennen
  (`iguazu`), den tiefsten See nennen (`baikalsee`) und den wasserreichsten Fluss nennen (`amazonas-wasser`).
- **Wüsten.** Ich kann die Fläche der Sahara schätzen (`sahara-flaeche`), die trockenste Wüste außerhalb der Pole
  nennen (`atacama`), sagen, wie hoch die Dünen der Namib sind (`namib-duenen`) und erklären, warum Antarktika eine
  Wüste ist (`antarktika-wueste`).
- **Höhlen und Schluchten.** Ich kann den Fluss des Grand Canyon nennen (`grand-canyon`), Höhlen ihrem Rekord
  zuordnen (`hoehlen-rekorde`), sagen, was es in der Sơn-Đoòng-Höhle gibt (`son-doong-dschungel`) und was in den
  Waitomo Caves leuchtet (`waitomo-leuchten`).
- **Küsten, Inseln und Riffe.** Ich kann die Länge des Great Barrier Reef schätzen (`great-barrier-reef`), den
  Naturforscher auf den Galápagos-Inseln nennen (`galapagos-darwin`), das Land der Halong-Bucht nennen
  (`halong-bucht`) und das Gestein des Giant’s Causeway nennen (`giants-causeway`).
- **Gruppen üben (über die Themen hinweg).** Ich kann Naturwunder ihrem Kontinent zuordnen (`kontinente-zuordnen`),
  Wüsten erkennen (`wuesten-erkennen`) und Berge nach ihrer Höhe ordnen (`hoechste-berge-kontinente`). Jeder Kontinent
  kommt im Quiz vor.

## Content structure

- Eine Frage ist ein Eintrag in `questions` von `src/quiz.json`, mit sprechender `id` (Kleinbuchstaben, Bindestriche),
  `type`, `text`, bei Bildfragen `material`, bei Auswahlfragen `options`, dazu `explanation` und `links`.
- Reihenfolge in der Datei: die fünf Themen in der Reihenfolge der Kompetenzen oben, dann die drei Fragen
  „Gruppen üben“. Ohne JavaScript steht so die Fragenliste nach Themen sortiert; mit JavaScript mischt das Quiz.
  Das Schema kennt keine Gruppen: Neue Fragen gehören an das Ende ihres Themas, nicht ans Ende der Datei.
- Fragetypen gemischt: single-choice (Standard, 4 Optionen), true-false, number (`answer`, `tolerance`, `unit`;
  die Toleranz steht auch im Fragetext), matching, ordering, multiple-choice.
- Jede Option einer Auswahlfrage hat `text`, `correct`, `info` (zwei Sätze zum Gegenstand der Option, nicht nur
  „richtig“ oder „falsch“) und `link` auf einen deutschen Wikipedia-Artikel, auch bei den falschen Optionen. Bei Fragen
  ohne Optionen (wahr/falsch, Zahl, Reihenfolge, Zuordnung) stehen alle Artikel in `links` der Frage.
- `explanation`: 2 bis 3 Sätze. `links`: der Artikel der Lösung zuerst.
- Länge: rund 25 Fragen (jetzt 25); Texte kurz, für Klasse 5 bis 10 lesbar.

## Terminology

- Sprache: Deutsch, einfach. Lernende werden mit „du“ angesprochen („Wähle alle passenden.“).
- Schreibweisen wie in der deutschen Wikipedia: Ätna, Kilimandscharo, Sơn-Đoòng-Höhle, Galápagos-Inseln im
  Fragetext, Wikipedia-Titel Galapagosinseln in den Links.
- Einheiten mit Leerzeichen: „8848 m“, „2300 km“; Zahlen ab vier Stellen ohne Tausenderpunkt, wie in den Texten
  vorhanden. Höhen sind Höhen über dem Meeresspiegel, Längen und Flächen ungefähr („etwa“, „rund“).
- Texte sind in eigenen Worten, keine Sätze aus Wikipedia übernehmen (`quiz-own-words`).
- Vermeiden: Fachwörter ohne Erklärung, „bekanntlich“, „natürlich“, Wertungen („schönster“).

## Exercise patterns

- Auswahl mit Rückmeldung zu jeder Option (`single-choice`): Beispiel `aetna-vulkan`. Eine richtige, drei
  plausible falsche Optionen aus demselben Bereich (andere Vulkane in Europa).
- Zahl mit Toleranz (`number`): `everest-hoehe` (`answer: 8848`, `tolerance: 100`, `unit: m`). Die Toleranz so wählen,
  dass sie zur Genauigkeit der Quelle passt und im Fragetext steht.
- Wahr oder falsch: `matterhorn-alpen`, `namib-duenen`; die Aussage ist eindeutig und im Artikel belegt.
- Zuordnen, ordnen, mehrfach wählen: `kontinente-zuordnen`, `hoechste-berge-kontinente`, `wuesten-erkennen`.
  Für diese Fragen gibt es kein Bild, weil jedes Bild eine Lösung verriete.

## Figures

- Bildfragen haben `material` mit einem Block `{ "type": "figure", … }` zwischen Fragetext und Antworten. Fragen,
  bei denen jedes Bild die Antwort verriete, haben keines: `hoehlen-rekorde`, `son-doong-dschungel` (das Foto der Höhle
  zeigt den Dschungel), `kontinente-zuordnen`, `wuesten-erkennen`, `hoechste-berge-kontinente`.
- Das Bild kommt aus dem Wikipedia-Artikel der Lösung (bei mehreren Artikeln: ein Artikel, der die Antwort nicht
  verrät), von Wikimedia Commons, nur frei lizenziert (gemeinfrei, CC0, CC BY, CC BY-SA). Lizenz und Urheber prüft man
  auf der Commons-Dateiseite, nicht aus dem Gedächtnis.
- Datei: `src/images/<name>.jpg`, Name aus Kleinbuchstaben, Ziffern und Bindestrichen (meist die Frage-ID); höchstens
  800 px breit, JPEG, Qualität etwa 60, möglichst unter 100 kB; ohne Metadaten. Zwei Fragen dürfen dieselbe Datei zeigen
  (`victoriafaelle.jpg`). Verweis im JSON: `images/<name>.jpg`.
- `alt`: beschreibt nur, was zu sehen ist, nie die Lösung. `caption`: sagt in einem Satz, worauf man achten soll,
  ohne die Antwort zu nennen, und endet mit „Foto: Name.“ (CC BY und CC BY-SA verlangen den Namen); bei
  gemeinfreien Bildern entfällt der Name.
- `source`: die Adresse der Commons-Dateiseite (`https://commons.wikimedia.org/wiki/File:…`, mit Umlauten statt
  Prozentzeichen), `licence`: SPDX-Bezeichner (`CC-BY-SA-4.0`, `CC-BY-3.0`, …) oder `gemeinfrei`. Das Quiz zeigt
  darunter „Quelle: … Lizenz: …“.
- Bilder ohne Beschriftung, die die Lösung nennt; keine Karten und keine Bilder mit Text. Satellitenbilder sind
  erlaubt, wenn sie nichts verraten (`great-barrier-reef`, `namib-duenen`).

## Sources

- Fakten: deutschsprachige Wikipedia (CC BY-SA); jeder Artikel, auf den die App verweist, steht in `sources` mit
  Titel, Lizenz und Adresse („…, Wikipedia – Die freie Enzyklopädie (deutsch), Lizenz CC BY-SA 4.0“).
- Geprüft wurde jeder Link (Status 200, richtiger Artikel, keine Begriffsklärung) und jede Aussage am Wikitext des
  Artikels (Stand 12.10.2026). Bei Zahlen gilt der Wert im Artikel; „etwa“ steht, wo er gerundet ist.
- Bilder: Wikimedia Commons, jede Datei mit eigener Quelle und Lizenz im `figure`-Block.
- Nicht verwendet: Material des Erstellers (bleibt lokal, nie eingecheckt), Videos, andere Wikis.

## Adding a chapter or round

Neue Frage in diesem Quiz (eine „Runde“ gibt es nicht, nur Fragen):

1. Thema und Kompetenz wählen, in „Competencies“ eintragen.
2. Artikel in der deutschen Wikipedia öffnen, Aussage und Zahl am Wikitext prüfen; Artikel in `sources` ergänzen.
3. Frage am Ende ihres Themas in `src/quiz.json` einfügen: `id`, `type`, `text`, Optionen mit `info` und `link`,
   `explanation`, `links` (Beispiel: `aetna-vulkan`).
4. Bild nach „Figures“ ergänzen (oder bewusst weglassen, wenn es die Antwort verriete).
5. `npx lernapps check` (Format, Schema, Bilder, Links) und `npx vp check --fix`.
6. Ändert sich ein Thema, im Eintrag `topics` den Deep-Link `#frage-<id>` prüfen (Plan: Eintrag).
7. Commit in einem Branch, Pull Request; nicht auf `main` pushen (das veröffentlicht die App).

## Rules learned from mistakes

- Ein Bild darf die Antwort nicht verraten: Das Foto der Sơn-Đoòng-Höhle zeigte den Dschungel und beantwortete
  `son-doong-dschungel`; die Frage hat deshalb kein Bild.
- Der Urheber steht in der Bildunterschrift, weil `source` entweder ein Link oder ein Text ist, nicht beides.
- Commons-Lizenz „CC BY-SA 2.0 de“ (deutsche Portierung) hat keinen SPDX-Bezeichner: ein anderes Bild wählen.
- Wikimedia liefert Vorschaubilder nur in üblichen Breiten (z. B. 960 px); verkleinert wird danach selbst.
