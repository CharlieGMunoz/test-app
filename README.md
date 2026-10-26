# Quiz CLI

An interactive command-line quiz game for learning JavaScript, Node.js, and general programming concepts.

## Features

- Choose from three quiz categories.
- Select all available questions, or a shorter 3- or 5-question quiz when supported.
- Answer multiple-choice questions from the terminal.
- Receive immediate correctness feedback and explanations.
- Track progress with a visual progress bar.
- Review incorrect answers at the end of a quiz.
- Replay without restarting the application.
- Uses ANSI terminal colors with no external runtime dependencies.

## Requirements

- Node.js 18 or newer
- npm (included with Node.js)

## Installation

Clone the repository, then install the project dependencies:

```bash
npm install
```

The application currently uses only Node.js built-in modules, so installation does not download runtime packages.

## Usage

Start the quiz with:

```bash
npm start
```

Follow the prompts to choose a category, select the number of questions, and enter the number corresponding to each answer. Press **Enter** when prompted to continue.

## Available Categories

- **JavaScript Basics**
- **Node.js Fundamentals**
- **General Programming**

The question bank is stored in `data/questions.json`.

## Development

Run the project’s Node.js test command with:

```bash
npm test
```

The repository currently does not contain dedicated test files; this command invokes Node’s built-in test runner.

## Project Structure

```text
.
├── data/
│   └── questions.json   # Categories, questions, answers, and explanations
├── src/
│   ├── colors.js        # ANSI color and text styling helpers
│   ├── input.js         # readline-based prompt and selection helpers
│   └── quiz.js          # Quiz state, scoring, feedback, and results
├── index.js             # Application entry point and main game loop
├── package.json         # Project metadata, scripts, and Node.js requirement
└── README.md            # Project documentation
```

## Architecture

`index.js` loads the question data, displays the category and question-count menus, and controls the replay loop. `src/input.js` wraps Node.js `readline` in promise-based helpers for selections, confirmations, and pause prompts. `src/quiz.js` shuffles questions, records answers, calculates progress and scores, and renders results. `src/colors.js` provides ANSI escape-code formatting without an external package.

## Question Data Format

Questions are grouped under `categories` in `data/questions.json`. Each category has a display `name` and a `questions` array. Every question contains:

- `question`: question text
- `options`: answer choices in display order
- `answer`: zero-based index of the correct option
- `explanation`: optional explanation shown after answering

To add questions, preserve this structure and ensure that each `answer` index matches the corresponding entry in `options`.

## License

This project is licensed under the MIT License, as declared in `package.json`.
