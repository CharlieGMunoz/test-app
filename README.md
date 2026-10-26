# Node.js Interactive Command-Line Quiz

A dependency-free interactive quiz application for Node.js. It presents multiple-choice questions from `data/questions.json`, provides immediate feedback, and summarizes performance at the end of each quiz.

## Table of Contents

- [Features](#features)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Available Commands](#available-commands)
- [Question Data](#question-data)
- [Testing](#testing)
- [Contributing](#contributing)
- [License](#license)

## Features

- Choose a quiz category.
- Choose the quiz length.
- Answer shuffled multiple-choice questions.
- Shuffle questions with the Fisher–Yates algorithm.
- Receive immediate answer feedback and explanations.
- Track quiz progress and view results.
- Review incorrect answers.
- Replay the quiz.
- Use internal ANSI color helpers for terminal output.

## Project Structure

```text
data/questions.json       # Quiz questions and explanations
src/colors.js              # Internal ANSI color helpers
src/input.js               # Interactive input handling
src/quiz.js                # Quiz flow and scoring
index.js                   # Application entry point
package.json               # Project metadata and npm scripts
```

## Prerequisites

- Node.js 18 or newer

The application uses native ES modules and has no external dependencies.

## Installation

Clone or download the repository, then install the project from its root directory:

```bash
npm install
```

There are no external runtime dependencies to install; `npm install` initializes the project using the metadata in `package.json`.

## Usage

Start the interactive quiz with:

```bash
npm start
```

This runs `node index.js`. Follow the prompts to select a category and quiz length, answer the multiple-choice questions, and review your results.

## Available Commands

| Command | Description |
| --- | --- |
| `npm start` | Start the quiz by running `node index.js`. |
| `npm test` | Run the Node.js built-in test runner. |

## Question Data

Questions are stored in `data/questions.json`. The available categories include:

- JavaScript Basics
- Node.js Fundamentals
- General Programming

To change the quiz content, update the question data in that file while preserving its expected JSON structure.

## Testing

Run the test command with:

```bash
npm test
```

The command uses Node.js's built-in test runner. No dedicated test files are currently present in the repository.

## Contributing

Contributions are welcome. When proposing a change:

1. Keep changes focused on the quiz application.
2. Preserve the native ES module setup and dependency-free runtime.
3. Update `data/questions.json` carefully when adding or revising questions.
4. Run the available test command before submitting your change:

   ```bash
   npm test
   ```

## License

This project is licensed under the MIT License, as specified in `package.json`.
