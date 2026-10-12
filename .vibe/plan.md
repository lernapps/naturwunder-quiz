---
# Read by the git hooks, the review and the evals.
# Schema: @lernapps/tooling/guidance/plan-front-matter.v1.schema.json. Keep all three keys.
# archetype: the kind of app, chosen at the end of Explore: explainer, interactive or quiz. null until then.
archetype: quiz
# phase: the phase you work in now: explore, plan, code or commit. Change it when you enter the next phase.
phase: plan
# prePushFailures: failed runs of the pre-push hook. The hook counts them. Never change this value.
prePushFailures: 0
---

# Plan: Naturwunder-Quiz

<!--
This file guides you, the assistant, and shows the creator where you are.
- Keep it at .vibe/plan.md. Read it before each step.
- Work through one phase at a time: Explore, Plan, Code, Commit. Do the tasks of the current phase in order.
- Tick a task when it is done and move it to "Completed" of its phase. Add tasks as you find them.
- A task marked as a checkpoint means: stop, show the creator what they need to decide, and wait for their answer.
- Write the plan in the language you talk to the creator in. Keep the headings and the front matter keys as they
  are: the review reads them.
- Delete these comments only where you have filled the part they explain.
-->

*Begonnen am 12.10.2026. Workflow: Explore, Plan, Code, Commit.*

## Goal

Schülerinnen und Schüler der Klassen 5 bis 10 beantworten rund 25 Quizfragen zu Naturwundern der Erde, verteilt auf Themen (Gebirge und Vulkane, Wasser, Wüsten, Höhlen und Schluchten, Küsten, Inseln und Riffe) und auf alle Kontinente. Nach jeder Antwort lesen sie kurz etwas zu jeder Möglichkeit und können im verlinkten Wikipedia-Artikel weiterlesen: Das Quiz soll Erdkunde-Wissen üben und neugierig machen.

## Key decisions

<!--
One line each: the decision and why. The archetype is the first one. Add decisions in any phase.
Mark a choice you made without asking the creator with "(guess)", and list it in the retrospective.
-->

- Archetyp `quiz`: Der Ersteller wünscht ein Quiz („Naturwunder-Quiz“); Fragen mit Antwortmöglichkeiten und Rückmeldung passen genau.
- Nur Geografie (Fach Erdkunde); Biologie wäre später eine eigene Rubrik.
- Gruppen über die Auswahl der Fragen (Vorschlag A, bestätigt mit „Passt“): Fragen gleichmäßig auf Themen und Kontinente verteilt, ohne JavaScript nach Themen sortiert, dazu Fragen, die die Gruppen selbst üben; im Eintrag je Gruppe ein Deep-Link. Der Quiz-Baustein kennt keine Gruppen, und Code darf nicht geändert werden (`quiz-only-data`).
- Rund 25 Fragen, Klassen 5 bis 10 (bestätigt mit „Passt“).
- Jede Antwortmöglichkeit verlinkt ihren Artikel in der deutschen Wikipedia, auch die falschen (Wunsch des Erstellers); Texte in eigenen Worten.
- `rememberLastResult` aus: Das Quiz speichert nichts, `fitness.storage: none` (guess).
- `creator.url` = https://github.com/mrsimpson, abgeleitet aus „@mrsimpson“ (guess).

## Notes

<!-- What you need later: sources and licences of content, links, open questions. -->

- Skill lernapps-quiz und Schema quiz.v1 gelesen: Jede Antwortmöglichkeit (single/multiple choice) kann einen eigenen `link` haben → für jede Option ein Wikipedia-Artikel. Bei Fragen ohne Optionen (wahr/falsch, Zahl, Reihenfolge, Zuordnung) stehen alle Artikel in `links` der Frage.
- Das Schema kennt keine Gruppen/Kategorien: Ein Quiz ist eine Seite mit allen Fragen in gemischter Reihenfolge. Gruppen wären nur über die Reihenfolge ohne JavaScript, Frage-IDs und Deep-Links (#frage-<id>) darstellbar. Entschieden: Vorschlag A (siehe Key decisions).
- Quelle: deutschsprachige Wikipedia (CC BY-SA); Texte in eigenen Worten (quiz-own-words), Artikel in `sources`.
- Später möglich: zweite Rubrik Biologie (nicht Teil dieses Plans).
- Eintrags-Schema gelesen (entry.v1): Pflicht sind title, subject, grades, summary, url, creator, fitness.

## Explore

<!--
Find out what the app is for, for whom, and what the app overview needs to help adults find it.
Ask the creator; write no code. Ask one or two questions per turn, in plain words. Do not ask what you can derive
from earlier answers. Write each answer under "Answers".
-->

### Tasks

### Answers

<!-- The creator's answers, in their words, one bullet per question. -->

- Thema: „Es soll ein Naturwunder-Quiz werden.“
- Inhalt/Fach: „Gruppierungen wären toll, sowohl thematisch als auch geografisch. Ich würde das erst einmal auf Geografie beschränken. Wenn es gut funktioniert, können wir danach auch etwas für Biologie machen, aber das wäre eine zweite Rubrik.“
- Lernende: „Es geht um Kinder aus dem Gymnasium und Realschulen oder anderen weiterführenden Schulen, wir können also davon ausgehen, dass sie schon wissen, was Ozeane oder was Kontinente sind.“
- Inhalte: „Das Quiz soll außerdem neugierig machen und zum weiteren Nachlesen anregen, nutze daher bitte Einträge aus Wikipedia, so dass sie auch fundiert sind. Verknüpfe die Artikel bei jeder Antwort, auch bei den falschen.“
- Gruppen, Umfang, Klassen (Vorschlag A, rund 25 Fragen, Klasse 5 bis 10): „Passt.“
- Name im Eintrag: „Ich bin Oliver (@mrsimpson)“

### Entry draft

<!--
The entry of the app in the app overview, as YAML that validates against the entry schema. Use the schema's
property names; its descriptions say what each one needs. Fill it from the answers; never invent a value. Leave out
what is not known yet, such as the app's address before it is published. The listing completes it.
-->

```yaml
title: Naturwunder-Quiz
subject: Erdkunde
grades: [5, 6, 7, 8, 9, 10]
summary: >-
  Im Quiz beantworten Schülerinnen und Schüler Fragen zu Naturwundern der Erde: Gebirge und Vulkane, Wasserfälle,
  Wüsten, Höhlen, Küsten und Riffe auf allen Kontinenten. Nach jeder Antwort lesen sie kurz zu jeder Möglichkeit
  und können im Wikipedia-Artikel weiterlesen.
# url: kommt nach der Veröffentlichung
topics: # Pfade (#frage-<id>) werden in Code festgelegt, je Gruppe eine Frage
  - title: Gebirge und Vulkane
  - title: Wasserfälle, Flüsse und Seen
  - title: Wüsten
  - title: Höhlen und Schluchten
  - title: Küsten, Inseln und Riffe
  - title: Naturwunder nach Kontinenten
keywords: [Naturwunder, Geografie, Erdkunde, Quiz, Kontinente, Welterbe, Vulkane, Wüsten, Wasserfälle]
creator:
  name: Oliver
  url: https://github.com/mrsimpson
source: https://github.com/lernapps/naturwunder-quiz
fitness:
  account: false
  install: false
  storage: none
  thirdParty: none
  checked: false
```

### Completed

- [x] Ask what the app is for: what do learners do in it, and what do they learn or train?
- [x] Ask who the learners are: subject, school year, what they know already.
- [x] Ask where the content comes from: written by the creator, or taken from others (with source and licence)?
- [x] Fetch the entry schema of the app overview: https://lernapps.net/apps/schemas/entry.v1.schema.json. Read the
      description of every property. Ask the creator what it needs to help adults (teachers, parents) find the app.
      Fill the "Entry draft" from the answers.
- [x] Choose the archetype from the answers: `explainer` (many pages of explanation and exercises), `interactive`
      (one app page in the browser, plus a static start page) or `quiz` (questions with options and feedback).
      Write it under "Key decisions" with the reason; set `archetype`.
- [x] Set `phase: plan`.


## Plan

<!--
Turn the answers into tasks the creator can confirm in one read. After the confirmation you work on your own: the
creator's turns from here to the listing are counted in the retrospective (target: at most 3).
-->

### Tasks

- [ ] **Checkpoint:** confirm the plan. Stop and wait for the creator. Change the plan if they ask, then ask again.
- [ ] Set `phase: code`.

### Completed

- [x] Show the creator the goal, the archetype, the entry draft and the tasks, short.
- [x] Write the tasks of Code under "Code": the pages or screens, the content, and what each must show. Each task
      ends in a commit.


## Code

<!--
Generate the app, then build it task by task. Load the skill lernapps-app and the skill of the archetype before you
write code. Commit after each task: the git hooks run the checks. The pre-commit hook is quiet: when it fails, it
prints one line naming the step and its log, `node_modules/.cache/lernapps/pre-commit.log`; read that log for the
messages. Fix every failed check from its message; never bypass a hook. When you cannot decide something, choose, mark it "(guess)" under "Key decisions" and go on.

The generator needs git, Node 22.18 or later and the network: github.com and codeload.github.com for the tooling, the
template and the runtime, and the npm registry (registry.npmjs.org) for the other dependencies. If the sandbox blocks
one of them, stop and ask the creator to allow it, then run the command again. Never write the app by hand.
-->

### Tasks

- [ ] Generate the app in the folder that holds this plan: `npx --yes github:lernapps/tooling#main create --archetype
      <archetype>`. Nothing needs to be installed first. The generator keeps this plan at `.vibe/plan.md`.
- [ ] Run `git init` if the folder is not a git repository yet. Then run `npm install`: it installs the dependencies
      and the git hooks. From now on, everything runs from the app's own `node_modules`: `npx lernapps check`, the
      hooks.
- [ ] Commit what the generator wrote, with this plan: the first commit.
- [ ] Load the skill `lernapps-app` and the skill of the archetype.
- [ ] Rahmen und Thema „Gebirge und Vulkane“: Beispiel ersetzen; Titel, Einleitung, `sources`; 5 Fragen (z. B. Mount Everest, Kilimandscharo, Ätna, Matterhorn, Aconcagua; Typen gemischt).
- [ ] Thema „Wasserfälle, Flüsse und Seen“: 5 Fragen (z. B. Victoriafälle, Iguazú-Wasserfälle, Niagarafälle, Baikalsee, Amazonas).
- [ ] Thema „Wüsten“: 4 Fragen (z. B. Sahara, Atacama, Namib, Antarktis als Kältewüste).
- [ ] Thema „Höhlen und Schluchten“: 4 Fragen (z. B. Grand Canyon, Eisriesenwelt, Sơn-Đoòng-Höhle, Waitomo-Glühwürmchenhöhlen).
- [ ] Thema „Küsten, Inseln und Riffe“: 4 Fragen (z. B. Great Barrier Reef, Galápagos-Inseln, Halong-Bucht, Giant’s Causeway).
- [ ] Gruppen üben: 3 Fragen über die Themen hinweg (Zuordnung Naturwunder → Kontinent, Mehrfachauswahl „Welche sind Wüsten?“, Reihenfolge nach Höhe oder Länge). Jeder Kontinent kommt im Quiz vor.
- [ ] Alle Wikipedia-Links öffnen und jede Aussage am Artikel prüfen (`quiz-further-reading`, `quiz-answers-checked`); jede Antwortmöglichkeit hat einen `link`; Fragen ohne JavaScript nach Themen sortiert.
- [ ] Eintrag: je Gruppe einen Deep-Link (`#frage-<id>`) unter `topics` eintragen.
- [ ] `npx lernapps check` passes.
- [ ] Set `phase: commit`.

### Completed

## Commit

<!--
Publish the app and list it, each only after the creator says yes. Then fill the retrospective.
A push to `main` publishes the app: the workflow `Pages` checks it and, in its job `deploy`, publishes the checked
bundle to the repo's GitHub Pages, at the repo's own address (usually https://<owner>.github.io/<repo>/). So work on
another branch until the creator says yes.
-->

### Tasks

- [ ] Push your branch (not `main`). The pre-push hook runs the heavy checks; fix what fails.
- [ ] **Checkpoint:** publish. Ask the creator before the app goes online, and wait for their yes.
- [ ] Merge your branch into `main` and push `main`. Watch the run of the workflow `Pages` on `main` until it ends
      (for example `gh run watch`, or the Actions tab of the repo). If it fails, read the message of the failed step:
      fix what you can and push again; for a setting only a repository admin may change, tell the creator the exact
      clicks the message names, and run the workflow again when they are done.
- [ ] Open the address the job `deploy` printed ("published at ...") and confirm that it shows the app.
- [ ] Load the skill `lernapps-listing`.
- [ ] Complete the entry draft with what is known now, such as the app's address.
- [ ] **Checkpoint:** list. Ask the creator before you open the listing pull request, and wait for their yes.
- [ ] Fill the retrospective.
- [ ] Open the listing pull request as the skill says, and see it through to "bestanden".

### Completed

## Retrospective

<!--
Fill it at the end of Commit, before the listing pull request: facts, short, no names of people. The review reads
it with the listing; the evals compare it across runs. It stays in the creator's repo.
-->

### Phases reached

<!-- The last phase you completed and the checkpoints the creator passed. Example: "commit; confirmed, published". -->

### Failed checks

<!--
Each check that failed, with its rule id and how often. Example: "`no-request-before-click`: 2".
Leave out the failed pre-push runs: the hook counts them in the front matter.
-->

### Creator turns after the plan

<!-- How many messages the creator sent after confirming the plan, and what each was about. Target: at most 3. -->

### Where I had to guess

<!--
Each place where this plan, a skill, a message or the creator's answers did not tell you what to do, and what you
chose. Write "None" if there was none.
-->
