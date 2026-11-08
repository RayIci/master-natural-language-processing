# Writing rules for the NLP course notes

- Language: English.
- Goal: study-ready lecture notes built from the course slides (not a Beamer deck).
- Master file: `notes/main.tex`; build from `notes/` with `latexmk -pdf -shell-escape main.tex`.
- Shared preamble: `notes/preamble/preamble.tex` — boxes (`nbdef`, `nbfact`, `nbintuition`,
  `nbexample`, `nbwarning`, `nbwhy`, `nbsummary`, `nbexercise`/`nbsolution`) and macros.
  Sections never define their own packages or macros; add them to the preamble.
- Layout: `sections/<topic>/<topic>.tex` (one folder per logical topic group of slides, NOT per lecture), sub-sections in
  sub-folders, figures and their generating scripts in an `assets/` folder next to the text.
  kebab-case names, `\label{sec:<folder-name>}` after every (sub)section.
- Paths in `\input`/`\includegraphics` are relative to `notes/` and written out in full.
- **Slide-source notes (mandatory).** Sections are grouped by topic, not by slide deck, so
  every `\section`, `\subsection` and `\subsubsection` states where its content comes from,
  on the line right after the heading (after `\label` if present):
  `\slidesrc{<deck name>: <slides>}`, e.g. `\slidesrc{Intro: 5--8}`,
  `\slidesrc{Terminology introduction: 12}`, or several decks separated by `;`
  (`\slidesrc{Intro: 1--3; Terminology introduction: 2}`). Slide numbers are PDF page
  numbers. Deck names (add a row when a new deck arrives):

  | File in `slides/`                                               | Deck name in notes                         |
  |-----------------------------------------------------------------|--------------------------------------------|
  | `1) Intro.pdf`                                                  | `Intro`                                    |
  | `2) terminology introduction.pdf`                               | `Terminology introduction`                 |
  | `3) Syntax-RE-Word.pdf`                                         | `Syntax: RE \& word`                       |
  | `4) Syntax-Sentence-Rule-based.pdf`                             | `Syntax: sentence, rules`                  |
  | `5) Syntax-Sentence-HMM.pdf`                                    | `Syntax: sentence, HMM`                    |
  | `6) semantics.pdf`                                              | `Semantics (long version)`                 |
  | `6.1) distributional-semantics-SHORTENED-VERSION.pdf`           | `Distributional semantics`                 |
  | `6.2) distributional-semantics.pdf`                             | `Distributional semantics (long version)`  |
  | `6.3) other-semantics-simons-nlp-tutorial-SHORTENED-VERSION.pdf`| `Other semantics`                          |
  | `6.4) distributedSemanticsB.jpg`                                | `Blackboard: semantics B` (photo)          |
  | `6.5) distributedSemanticsA.jpg`                                | `Blackboard: semantics A` (photo)          |
  | `7) NLP-ontologies.pdf`                                         | `Ontologies`                               |
  | `7.1) OntologyDevelopment-Evolution2026.pdf`                    | `Ontology development`                     |
  | `7.2) Ontolearning-SHORTENED-VERSION.pdf`                       | `Ontology learning`                        |
  | `7.3) Ontomatching-SHORTENED-VERSION.pdf`                       | `Ontology matching`                        |
  | `7.4) Ontomatching.pdf`                                         | `Ontology matching (long version)`         |
  | `8) features.pdf`                                               | `Text features`                            |
  | `9) 20261105_150320.jpg`                                        | `Blackboard: features` (photo)             |
  | `10) pragmatics.pdf`                                            | `Pragmatics`                               |

  Pages 1--27 of `6.2)` are the same slides as `6.1)`: cite the shortened deck for them.

  When a deck has a SHORTENED and a long version, the shortened one is what was shown in
  class and is the main source; material taken only from the long version must say so in
  its `\slidesrc` (deck name `... (long version)`), so the reader knows it was not shown. Use `\notinslides` for material added on top of the slides (extra
  explanations, exercises). Ranges at section level must cover their sub-parts.
- **Blackboard photos (`.jpg` in `slides/`).** They are exam material. Rewrite each one in
  LaTeX (never include the photo) inside the `nbblackboard` environment:
  `\begin{nbblackboard}{<title>}{<deck name(s)>} ... \end{nbblackboard}`. It numbers the
  box ("Blackboard N"), styles it so it stands out, and adds it to the List of Blackboards
  after the table of contents. Transcribe the board faithfully (say when something is
  erased or unreadable), then explain it outside the box. Figures redrawn from the slide
  PDFs are ordinary figures, without this treatment.
- Never mention repository internals (paths, scripts, macro names) in the PDF text.
- Compile after each section and visually check the rendered pages.
