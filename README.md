<!-- hide -->
<div align="center">

# Intermediate Data Modeling with Class Diagrams

[![Certified by 4Geeks Academy](https://img.shields.io/badge/certified_by-4Geeks_Academy-2563eb)](https://4geeks.com)
[![Runs on LearnPack](https://img.shields.io/badge/runs_on-LearnPack-2563eb)](https://learnpack.co)
[![Open in Codespaces](https://img.shields.io/badge/open_in-Codespaces-fb5a1f)](https://codespaces.new/4GeeksAcademy/intermediate-data-modeling-class-diagrams)

</div>

*These instructions are also available in [Spanish / Español](https://github.com/4GeeksAcademy/intermediate-data-modeling-class-diagrams/blob/HEAD/README.es.md).*

<!-- endhide -->

This tutorial is a 12-step guided practice that builds one cumulative UML-style class diagram for an online course platform inside [diagram.4geeks.com](https://diagram.4geeks.com/). You model 9 classes — `Course`, `Student`, `Instructor`, `Lesson`, `Enrollment`, `StudentProfile`, `Category`, `Certificate` and `Review` — connected by 9 typed relationships that cover 1:1, 1:N, N:M and optional 0..1 cardinality. It takes about 3 hours and requires no code.

<!-- hide -->

## 📋 About this tutorial

- **Difficulty:** Intermediate
- **Estimated duration:** 3 hours
- **Steps:** 13 folders — 1 welcome step plus 12 numbered modeling steps (`01` to `12`)
- **Technologies:** UML class diagrams, data modeling, [diagram.4geeks.com](https://diagram.4geeks.com/), Mermaid `classDiagram` syntax
- **Grading:** none — there are no test files and `learn.json` declares `no_delivery`; you self-check against the reference model in step 12
- **Languages:** English and Spanish (`README.md` and `README.es.md` in every step)
- **Runtime:** LearnPack `5.0.348` on a Node.js 22 devcontainer, or simply read the step files on GitHub

<!-- endhide -->

## 🎯 What will you learn?

By the end of the 12 steps you will be able to:

- Turn a plain-language product description into **classes with explicitly typed attributes** (`int`, `string`, `boolean`, `date`).
- Tell apart the three cardinalities that show up in almost every real schema: **one-to-one**, **one-to-many** and **many-to-many**.
- **Resolve a many-to-many relationship with an associative class** instead of a bare line — the single most useful modeling reflex in this practice, applied twice (`Enrollment` and `Review`).
- Express an **optional relationship** (`0..1`) for records that only exist under a condition, such as a certificate issued after a completed enrollment.
- Work around the limits of a real drawing tool: when there is no enum type, a `string` property plus a documented note is the correct answer, not a blocker.
- Read and write a Mermaid `classDiagram`, the text format used for the reference solution in step 12.

## 👀 What will you build?

One diagram, grown step by step. Nothing is thrown away between steps — step 12 is the same canvas you opened in step 01.

- **00 - Welcome.** How the practice works, what the editor does and does not support, and where to draw.
- **01 - Course Entity.** Class `Course` with `id` (`int`), `title` (`string`) and `description` (`string`).
- **02 - Student Entity.** Class `Student` with `id`, `name` and `email`. No relationship yet — on purpose.
- **03 - Instructor Entity.** Class `Instructor` with `id`, `name` and `bio`. Three isolated classes on the canvas.
- **04 - Instructor Courses.** Your first relationship: a 1:N link from `Instructor` to `Course`, with `1` and `N` written as text labels on the connector ends and an optional `teaches` label on the line.
- **05 - Lessons.** Class `Lesson` with `id`, `title`, `durationMinutes` and `orderIndex`, linked 1:N from `Course` (optional label `contains`).
- **06 - Enrollment Association.** The many-to-many step. Class `Enrollment` with `id` and `enrolledAt` (`date`) sits between the other two: `Student` 1 — N `Enrollment`, `Enrollment` N — 1 `Course`. A direct `Student`–`Course` line is explicitly wrong here.
- **07 - Enrollment Progress and Status.** Extend `Enrollment` with `progressPercent` (`int`, 0–100) and `status` (`string`, documented values `active`, `completed`, `dropped`).
- **08 - Student Profile One to One.** Class `StudentProfile` with `id`, `avatarUrl` and `timezone`, linked 1:1 to `Student` so the main entity stays lean.
- **09 - Categories.** Class `Category` with `id`, `name` and `slug`, linked 1:N to `Course`. A course belongs to exactly one category in this simplified model.
- **10 - Certificate.** Class `Certificate` with `id`, `issuedAt` (`date`) and `certificateCode` (`string`), attached to `Enrollment` with cardinality `1` — `0..1`.
- **11 - Reviews.** Class `Review` with `id`, `rating` (`int`), `comment` (`string`) and `createdAt` (`date`), routed `Student` → `Review` → `Course`. At this point at least six distinct classes are on the canvas.
- **12 - Final Model.** Compare your diagram with the reference Mermaid `classDiagram` (9 classes, 9 links) and answer three discussion questions about enums, multi-instructor courses and why `Review` deserves its own class.

## 🎓 What do you need before starting?

- **No programming language.** Nothing is compiled or executed. You draw, you do not code.
- **A browser** and [diagram.4geeks.com](https://diagram.4geeks.com/), the drawing tool used throughout. Keep a single diagram open from step 01 to step 12.
- **A rough idea of what a class is** — a named thing with properties. Any object-oriented background helps but is not required.
- **Optionally, a GitHub account** to open the repository in Codespaces and follow the steps inside the LearnPack interface. Reading the step `README.md` files directly on GitHub works just as well.
- **Optionally, Node.js 22 and LearnPack** if you prefer to run everything on your own machine.

## ✅ How is your work checked if there are no tests?

Be clear about this before you start: **this package has no automated grading**. Every one of the 13 exercise folders contains exactly two files, `README.md` and `README.es.md`. There is no test file, no answer key and no rubric, and `learn.json` declares the delivery format as `no_delivery`, so nothing is uploaded anywhere.

Checking is on you, and the package gives you three tools for it:

- **A two-item checklist at the end of steps 01 to 11**, with concrete conditions to confirm before moving on — for example "cardinality text appears on both links". The welcome step and the final model do not carry one.
- **The reference Mermaid `classDiagram` in step 12**, which spells out all 9 classes with their attributes and all 9 relationships with their cardinalities.
- **Your own judgement about equivalence.** Layout, colors and exact wording of labels may differ from the reference and still be correct. What must match is the set of entities, the typed properties, and the cardinality written on each link.

When you are satisfied with your diagram, mark the step complete in LearnPack manually. Exporting a PNG for your own notes is optional and purely for you.

## 💡 What mistakes should you avoid?

- **Starting a new diagram on every step.** It is one cumulative model. Step 02 explicitly asks you to keep `Course` from step 01, and step 03 asks you to keep both.
- **Drawing `Student` directly to `Course`.** Step 06 forbids it. The many-to-many must pass through `Enrollment`, and the same pattern repeats with `Review` in step 11.
- **Adding relationships too early.** Steps 02 and 03 deliberately leave the classes unconnected. Resist the urge.
- **Leaving properties untyped.** Every class you add arrives with a property-and-type table in the instructions, and most checklists ask you to confirm those types are visible. `title` is not enough; it has to read as `string`.
- **Hunting for an enum type for `status`.** The tool does not need one. `status: string` plus a short note listing `active`, `completed` and `dropped` is the intended answer in step 07.
- **Wiring the certificate straight to the student.** Step 10 asks you to hang `Certificate` off `Enrollment` and to avoid a duplicate student–certificate line, because the enrollment is what gets completed.
- **Putting `rating` on `Enrollment`.** A review is a separate fact with its own date and comment — that is exactly discussion question 3 in step 12.
- **Expecting strict UML notation.** This editor works with class boxes, typed properties and text labels. Cardinality is written as `1`, `N`, `*` or `0..1` on the connector, not as special arrowheads or composition diamonds.

## ❓ Frequently asked questions

### Do I need to know how to program to follow this tutorial?

No. There is no source code, no language runtime and nothing to execute in any of the 12 steps. You need to understand the idea of a class with properties, which the welcome step introduces. Programming experience makes the vocabulary familiar, but the exercise is purely a modeling exercise.

### What tool do I use to draw the diagrams?

[diagram.4geeks.com](https://diagram.4geeks.com/), a browser-based diagram editor. It gives you class boxes with typed attributes, links between classes and free text labels on those links. Open one diagram at the start and keep adding to it — every step builds on the previous canvas.

### Is there automatic grading or a file to submit?

No to both. `learn.json` sets the delivery format to `no_delivery` and no exercise folder ships a test file. You compare your result with the reference model in step 12 and mark the practice complete yourself.

### What is the difference between a class diagram and an entity-relationship diagram?

A UML class diagram describes classes in object-oriented software: attributes, operations and the relationships between objects. An entity-relationship diagram describes tables, columns and keys in a relational database. They overlap heavily for data modeling — entities, attributes and cardinality look almost identical — which is why this practice translates cleanly into a database schema even though it never mentions SQL.

### How do I model a many-to-many relationship?

Create a class in the middle. Instead of joining `Student` and `Course` with a single line, you add `Enrollment`, link `Student` 1 — N `Enrollment` and `Enrollment` N — 1 `Course`, and give `Enrollment` its own attributes such as `enrolledAt`, `progressPercent` and `status`. Those attributes are the reason the intermediate class exists: they belong to the pair, not to either side.

### Can I skip steps or do them out of order?

LearnPack lets you jump freely, but the steps are cumulative. Step 07 extends the class created in step 06, and step 10 attaches to it too. If you jump ahead, go back and add the missing classes, otherwise the reference comparison in step 12 will not line up.

<!-- hide -->

## 📝 Related tutorials

If class diagrams got you interested in how those classes become real code, these interactive tutorials are a natural next step:

- [Learn Object Oriented Programming with Python](https://4geeks.com/en/interactive-exercise/object-oriented-programing-with-python)
- [Object Oriented Programming in JavaScript](https://4geeks.com/en/interactive-exercise/object-oriented-programing-in-javascript)
- [Learn Python Best Practices](https://4geeks.com/en/interactive-exercise/python-best-practices-tutorial)

## 🚀 How to start

The fastest path is GitHub Codespaces, which needs nothing installed on your computer.

1. Open the repository in [GitHub Codespaces](https://codespaces.new/4GeeksAcademy/intermediate-data-modeling-class-diagrams) and create a codespace on the `main` branch.

2. Wait for the container to finish building. It installs LearnPack `5.0.348` globally on a Node.js 22 image and adds the LearnPack VS Code extension automatically.

3. Start the tutorial:

    ```bash
    learnpack start
    ```

4. Open [diagram.4geeks.com](https://diagram.4geeks.com/) in a second browser tab, create a new diagram, and keep it open for the whole practice.

5. Follow the steps in order, from `00-welcome` to `12-final-model`.

## 💻 Local installation

If you prefer to work on your own machine:

1. Install [Node.js](https://nodejs.org/en/download) 22 or newer.

2. Install LearnPack globally, pinned to the version this package was built with:

    ```bash
    npm i @learnpack/learnpack@5.0.348 -g
    ```

3. Clone the repository and enter the folder:

    ```bash
    git clone https://github.com/4GeeksAcademy/intermediate-data-modeling-class-diagrams.git
    cd intermediate-data-modeling-class-diagrams
    ```

4. Start LearnPack:

    ```bash
    learnpack start
    ```

You can also skip all of the above and simply read the step files in the [`exercises`](https://github.com/4GeeksAcademy/intermediate-data-modeling-class-diagrams/tree/HEAD/exercises) folder, since the instructions are the entire content of the package.

## 📚 How the exercises are organized

Every step lives in its own folder inside [`exercises`](https://github.com/4GeeksAcademy/intermediate-data-modeling-class-diagrams/tree/HEAD/exercises), named with a numeric prefix that sets the order: `00-welcome`, `01-course-entity`, `02-student-entity`, and so on up to `12-final-model`.

Each folder contains exactly two files:

- `README.md` — the instructions in English
- `README.es.md` — the same instructions in Spanish

There are no solution files, no tests and no configuration inside the step folders. A typical step is built from a short **Scenario**, a set of **Instructions**, a two-item **Checklist**, and a pointer to the next step. Step 12 adds the reference [Mermaid class diagram](https://mermaid.js.org/syntax/classDiagram.html) and three discussion questions.

## 🤝 Contributors

Built by [@ehiber](https://github.com/ehiber) and contributors at [4Geeks Academy](https://4geeksacademy.com/).

This repository does not ship a LICENSE file, so all rights are reserved by default. Access to the tutorial costs nothing and the diagrams you produce are yours; the instructional content itself is not released under an open source license.

Found a typo, a broken step or a modeling detail that could be clearer? Open an issue or a pull request on [the repository](https://github.com/4GeeksAcademy/intermediate-data-modeling-class-diagrams) — these materials are maintained collaboratively.

<!-- endhide -->
