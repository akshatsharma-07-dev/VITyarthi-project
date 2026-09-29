# VITyarthi-project
# Quiz Application

A small command-line quiz written in Python. It asks short-answer questions about Python collections, marks each answer, shows a score, and lets you retry only the questions you missed. You can also add your own questions while the program is running.

**Course:** CSA1021 - Introduction to Program Solving, VIT Bhopal University
**Author:** Akshat Sharma (26BAI10379), B.Tech CSE (AI & ML)

## Features

- Menu-driven interface that repeats until you choose Exit
- Six built-in questions on lists, sets and built-in functions
- Answers are checked without regard to upper or lower case
- Score shown as "You scored x out of n"
- Retry loop that repeats only the missed questions until all are correct or you stop
- Add new questions and answers during a run (empty input is rejected)
- Show all stored questions with their answers

## Requirements

- Python 3 (no external libraries, no imports)

## How to run

Save the code as `main.py`, then run it from its folder:

```
python main.py
```

On Windows you can also use `py main.py`.

## Menu

| Option | Action |
|--------|--------|
| 1 | Start quiz |
| 2 | Add a question |
| 3 | Show all questions |
| 4 | Exit |

Any other input prints `Invalid choice, pick 1, 2, 3, or 4`.

## Example session

```
--- QUIZ MENU ---
1 Start quiz
2 Add a question
3 Show all questions
4 Exit
Enter choice: 1

Question 1 of 6
Which data type is ordered, mutable, and allows duplicates?
Your answer: tuple
Wrong, answer is: list
...
You scored 5 out of 6

You missed 1 questions
wanna retry the wrong ones? (y/n): y

Question:
Which data type is ordered, mutable, and allows duplicates?
Your answer: list
Corect

all questions corect
```

## How it works

| Name | Type | Purpose |
|------|------|---------|
| `questions` | list of str | Question text |
| `answers` | list of str | Correct answer at the same index as the question |
| `wrong` | set of int | Indices of questions answered wrongly in the current round |
| `still_wrong` | set of int | Indices still wrong after a retry round |
| `score` | int | Number of correct answers in the first pass |

1. An outer `while True` loop prints the menu and reads a choice.
2. **Start quiz** loops over every question, compares the lower-cased answer with the stored answer, and records missed indices in the `wrong` set.
3. The **retry loop** runs while `wrong` is not empty. Each round asks only the questions in `wrong` and collects the ones still incorrect in `still_wrong`, which then replaces `wrong`.
4. **Add a question** appends to both lists if neither input is empty.
5. **Show all questions** prints every pair with a number.
6. **Exit** breaks out of the main loop.

## Known limitations

- Questions added during a run are kept in memory only and are lost when the program exits.
- Only letter case is ignored: an answer with an extra space (for example `list `) is marked wrong.
- A question or answer made only of spaces is accepted.
- Menu input such as ` 1` (with a space) is treated as invalid.
- Some output text contains spelling errors (`Corect`, `corect`).

## Possible improvements

- Save questions to a file so they persist
- Use `strip()` on answers and menu input
- Shuffle question order with the `random` module
- Store questions in a list of dictionaries instead of two parallel lists
- Move the menu blocks into functions and add automated tests
