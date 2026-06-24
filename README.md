# deckfolio.vue

deckfolio.vue is a Vue-based presentation authoring tool for creating slides that work both as live presentation material and as publishable HTML content.

It is designed for talks where the live slides should stay thin, readable, and focused, while the published material should remain thick, contextual, and useful for people who were not present at the talk.

## Quick Start

deckfolio.vue helps you write one presentation source that can serve two different situations:

1. **During the talk**
   Show concise slides optimized for speaking, pacing, and audience attention.

2. **After the talk**
   Publish the same material as richer HTML content, including notes, explanations, context, and references.

The goal is not to make every slide contain more information.
The goal is to separate what should be shown during the presentation from what should be preserved for later reading.

## Concept

Presentation materials often fall into a false binary:

* **Thin slides** are good for live talks, but poor as standalone references.
* **Thick slides** are useful after the talk, but too dense for live presentation.

deckfolio.vue rejects that binary.

Its core idea is:

> Thin while presenting.
> Thick when published.

In deckfolio.vue, notes are not treated as private speaker aids or secondary metadata. They are first-class content intended to be read after the presentation. A talk should not become inaccessible to people who missed it, and a published slide deck should not require the speaker’s oral explanation to make sense.

deckfolio.vue therefore treats a presentation as a dual-mode document:

* a **live slide deck** for the event,
* and a **published HTML document** for later readers.

## Why deckfolio.vue?

deckfolio.vue exists because ordinary slide tools tend to optimize for only one side of presentation material.

Traditional slide decks are often optimized for the room: they support the speaker, but they lose much of their meaning after the talk ends. On the other hand, document-like slide decks may preserve information, but they can become too dense to function well in a live setting.

deckfolio.vue is designed for authors who want both:

* slides that do not overload the audience during the talk,
* notes that preserve the reasoning, context, and references after the talk,
* a single authoring workflow for both presentation and publication,
* HTML output that can be shared as durable web content.

The central value of deckfolio.vue is not visual decoration or slide animation.
Its value is reducing the information gap between people who attended the talk and people who read the material later.

## Target Users

deckfolio.vue is intended for people who create presentations that should remain useful after the live event.

Typical users include:

* engineers giving technical talks,
* researchers explaining concepts or findings,
* educators preparing lecture-style material,
* writers or thinkers presenting structured arguments,
* conference speakers who want to publish readable post-talk material,
* teams that manage multiple presentations in one repository-like structure.

deckfolio.vue is especially suitable when the presentation contains reasoning, background, examples, references, or explanations that should not be forced onto the visible slides.

It is less suitable for presentations that are purely visual, purely performative, or disposable after the event.

## Non-Goals

deckfolio.vue is not primarily a slide design tool.

It does not aim to replace every presentation tool, nor does it try to make slides more complex. It is also not centered on speaker notes as private reminders.

Instead, deckfolio.vue focuses on a narrower problem:

> How can one source produce a thin live presentation and a thick published document without treating either as an afterthought?

## Status

deckfolio.vue is currently an early-stage project.
The core concept is stable, but detailed design and implementation may evolve.
