# Quiz CLI

> An interactive command-line quiz game for learning JavaScript, Node.js, and general programming concepts.

[![Node.js](https://img.shields.io/badge/Node.js-%3E%3D18-339933?logo=node.js&logoColor=white)](https://nodejs.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![ES Modules](https://img.shields.io/badge/JavaScript-ES%20Modules-F7DF1E?logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)

## Table of Contents

- [Project Overview](#project-overview)
- [Features](#features)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Question Data](#question-data)
- [Development](#development)
- [How It Works](#how-it-works)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

## Project Overview

Quiz CLI is a dependency-free terminal quiz application built with modern Node.js. It presents multiple-choice questions across three categories—JavaScript Basics, Node.js Fundamentals, and General Programming—then provides immediate feedback, explanations, progress tracking, scoring, and a review of missed questions.

The project is also a compact demonstration of core JavaScript and Node.js concepts, including ES modules, asynchronous programming, file-system access, `readline`, classes, array methods, destructuring, template literals, and error handling. It is a local terminal application: it does not start a server, call an API, use the network, persist scores, or require environment variables.

## Features

- Interactive category selection from the terminal.
- Configurable quiz length based on the selected category.
- Fisher–Yates shuffling of the selected questions whenever a new quiz starts. For a 3- or 5-question quiz, the application first takes that many questions from the category's source order and then shuffles that selected set; it does not randomly sample from the entire category.
- Multiple-choice answer selection with input validation.
- Immediate correct/incorrect feedback and, when provided in the question data, an explanation.
- Visual progress bar and question counter.
- Score percentage and performance message at the end of each quiz.
- Incorrect-answer review showing the selected and correct answers.
- Option to play another quiz without restarting the process.
- ANSI-colored terminal output and Unicode symbols, with no third-party runtime dependencies.

## Prerequisites

- [Node.js](https://nodejs.org/) 18.0.0 or newer.
- A terminal capable of displaying ANSI escape codes and the Unicode characters used by the progress bar and status messages. Terminals that do not support these may show raw escape sequences or substitute/misrender some symbols.
- Git, if cloning the repository.

No external npm packages are required.

## Installation

Clone the repository and move into the project directory:

```bash
git clone https://github.com/CharlieGMunoz/test-app.git
cd test-app
```

No dependency installation is required. The application uses only Node.js built-in modules, so you can run it immediately after cloning.

## Usage

Start the interactive quiz with:

```bash
npm start
```

Alternatively, invoke the entry point directly:

```bash
node index.js
```

The application will:

1. Display the welcome banner.
2. Ask you to choose a category.
3. Ask whether to answer all available questions or a shorter quiz.
4. Take the first N questions from the category when a shorter quiz is selected, then shuffle those selected questions.
5. Pause for Enter before the first question and after each question except the last one.
6. Present each question as a numbered multiple-choice prompt and reject selections outside the displayed range.
7. Show correct/incorrect feedback and the question's explanation when the `explanation` field contains one.
8. Display the final score and missed-question review.
9. Ask whether you want to play again; a response beginning with `y` starts another quiz.

Example interaction:

```text
Choose a category:
  1. JavaScript Basics
  2. Node.js Fundamentals
  3. General Programming

Your choice (enter number): 1

How many questions?
  1. All questions
  2. 3 questions
  3. 5 questions

Your choice (enter number): 2
```

Enter a valid option number whenever prompted. Invalid selections are rejected until a number in the displayed range is provided. When the program asks you to press Enter, submit an empty response to continue; the pause is only a checkpoint and does not select an answer.

## Project Structure

```text
.
├── data/
│   └── questions.json  # Categories, questions, options, answers, and explanations
├── src/
│   ├── colors.js       # ANSI color and text-style helpers
│   ├── input.js        # Readline interface and validated prompts
│   └── quiz.js          # Quiz class, shuffling, scoring, and result display
├── index.js             # Application entry point and main game loop
├── package.json         # Project metadata, scripts, and Node.js requirement
└── README.md            # Project documentation
```

## Question Data

Questions are loaded at runtime from `data/questions.json`. Each category has a display name and a `questions` array. A question uses the following shape:

```json
{
  "question": "What keyword is used to declare a constant in JavaScript?",
  "options": ["var", "let", "const", "define"],
  "answer": 2,
  "explanation": "The 'const' keyword declares a block-scoped constant that cannot be reassigned."
}
```

The `answer` field is a zero-based index into `options`; in the example above, `2` identifies `const`. The optional `explanation` field is displayed only when that question data includes a non-empty value. To add content, update the JSON while preserving this structure. The application automatically discovers category IDs from the `categories` object. Keep `answer` within the zero-based `options` range and ensure the JSON remains valid.

## Development

Available npm scripts:

```bash
npm start  # Launch the interactive quiz
npm test   # Run Node.js's built-in test runner
```

`npm test` invokes Node.js's built-in test runner. The repository currently has no dedicated test files, so this command does not exercise quiz behavior until tests are added; use `npm start` for a manual interactive check.

The code uses native Node.js APIs only:

- `node:fs/promises` reads the question file asynchronously.
- `node:path` and `node:url` resolve paths safely in an ES module context.
- `node:readline` handles terminal input.
- Native ES module syntax is enabled by `"type": "module"` in `package.json`.

## How It Works

- `index.js` loads question data, renders the menu, creates a `Quiz`, and controls replay.
- `src/input.js` wraps `readline` prompts in promises and validates numeric selections.
- `src/quiz.js` copies and shuffles questions, tracks progress and answers, calculates the score, and renders results.
- `src/colors.js` provides small formatting helpers using ANSI escape sequences.
- `data/questions.json` keeps quiz content separate from application logic. Its question fields control the available options, correct answer, and whether an explanation is shown.

## Troubleshooting

- **Colors or formatting look incorrect:** use a terminal with ANSI escape-code support. Otherwise, ANSI sequences may appear as raw characters.
- **The progress bar or icons look wrong:** use a terminal/font with Unicode support; the application prints characters such as `█`, `░`, and emoji.
- **The quiz cannot load its questions:** run the commands from the project directory and confirm that `data/questions.json` is present.
- **The quiz fails while loading data:** validate `data/questions.json` as JSON and confirm each question has `question`, `options`, and a zero-based `answer` index. The optional `explanation` field may be omitted.
- **`npm test` appears to do nothing:** this is expected while the repository has no dedicated test files; run `npm start` to check the interactive flow manually.

## Contributing

Contributions are welcome. To propose a change:

1. Create a feature branch.
2. Make a focused change that preserves the existing JSON schema and CLI behavior.
3. Run the available checks:

   ```bash
   npm test
   ```

4. Exercise the application manually with:

   ```bash
   npm start
   ```

5. Open a pull request with a clear description of the change.

When adding questions, verify the answer index, ensure every option is meaningful, and include an explanation where possible.

## License

This project is licensed under the [MIT License](https://opensource.org/licenses/MIT), as declared in `package.json`.
