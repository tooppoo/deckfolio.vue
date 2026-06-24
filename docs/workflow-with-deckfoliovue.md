# Workflow

This document defines the intended workflow for creating, presenting, and publishing presentation materials with deckfolio.vue.

deckfolio.vue treats a presentation not as a temporary slide deck, but as a dual-purpose document that supports both live presentation and post-presentation reading.

## Overview

A deckfolio.vue presentation follows a single-source workflow:

1. Create the presentation as Vue SFC files.
2. Present using the generated PDF.
3. Publish the generated HTML after the talk.

The live slides and the detailed post-presentation content are not authored as separate documents. They are created together, in the same Vue SFC-based source, and then built into different output formats for different situations.

## 1. Authoring

Presentation material is authored as Vue Single File Components.

In this workflow, the visible slides used during the talk and the detailed explanatory content intended for later reading are written together.

The purpose of this integration is to avoid splitting a presentation into two unrelated artifacts:

* a thin slide deck for the event,
* and a separate article or document written later.

Instead, deckfolio.vue encourages authors to treat the live presentation and the published material as two views of the same source.

The slide part is optimized for the presentation setting: concise, readable, and suitable for oral explanation.

The detail part is optimized for post-presentation reading: contextual, explanatory, and useful even for readers who did not attend the talk.

## 2. Presentation

On the day of the presentation, the author builds the presentation and uses the generated PDF for the live talk.

The PDF is the presentation-time artifact. It is expected to be stable, portable, and suitable for use in conference rooms, classrooms, meetups, online talks, or other live presentation settings.

During the presentation, the audience primarily sees the thin slide view. The detailed material does not need to be displayed in full during the talk. Its role is to preserve the information that would otherwise be carried only by the speaker’s oral explanation.

## 3. Publication

After the presentation, the author builds the HTML version and publishes it to a personal website, blog, documentation site, or other web platform.

The HTML is the post-presentation artifact. It is intended to be read independently of the live talk.

This published version should reduce the information gap between people who attended the presentation and people who encounter the material later. It should preserve the reasoning, background, examples, references, and explanations that are necessary for understanding the presentation after the event.

## Source and Outputs

deckfolio.vue assumes the following relationship between source and outputs:

```text
Vue SFC source
  ├─ PDF  → used for the live presentation
  └─ HTML → published after the presentation
```

The PDF and HTML are not separate authoring targets. They are outputs generated from the same presentation source.

This is the central workflow assumption of deckfolio.vue.

## Design Principle

deckfolio.vue is based on the principle:

> Thin while presenting, thick when published.

The author should not be forced to choose between slides that are readable during the talk and materials that are useful after the talk.

The live presentation can remain focused and lightweight, while the published HTML can carry the fuller explanation.

## Non-Goals

This workflow does not define detailed implementation rules, component APIs, build commands, deployment procedures, or styling conventions.

It also does not require authors to write a separate article after the presentation.

The purpose of this workflow is narrower: to define how deckfolio.vue expects presentation material to move from authoring, to live presentation, to post-presentation publication.
