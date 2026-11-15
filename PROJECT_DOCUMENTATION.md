# AI-Powered Escape Room: The Mystery of the Locked Library

An escape room game where the puzzles are run through an AI. You wake up locked inside a mysterious library and have to work your way out by solving three puzzles. Instead of clicking through menus, you type what you want to do into a chat window, and an AI Game Master answers you.

**Author:** Sarang Chackalayil Soman
**Built with:** Python, Google Gemini API, Gradio, Google Colab

---

## Table of Contents

- [About the Project](#about-the-project)
- [Objectives](#objectives)
- [Technologies Used](#technologies-used)
- [System Architecture](#system-architecture)
- [Implementation](#implementation)
- [Story and Puzzle Design](#story-and-puzzle-design)
- [Gradio Interface](#gradio-interface)
- [Testing and Results](#testing-and-results)
- [Security](#security)
- [Limitations](#limitations)
- [Future Improvements](#future-improvements)
- [Conclusion](#conclusion)

---

## About the Project

The Game Master runs on Google's Gemini API, which reads what the player writes and replies in natural language. Behind it, a bit of Python code keeps track of how far the player has got and makes sure the puzzles are solved in the right order. The chat window is built with Gradio.

## Objectives

- Build an interactive escape room that uses AI to hold the conversation.
- Connect the Gemini API to a working game.
- Design a few puzzles that follow a logical order.
- Use Python to keep track of the player's progress.
- Let the AI Game Master give hints when the player is stuck.
- Put it all behind a simple chat interface with Gradio.
- Show a practical use of a large language model in a small application.

## Technologies Used

| Technology | What it's used for |
|---|---|
| Python | The main programming language |
| Google Gemini API | The AI conversation and responses |
| Gradio | The chatbot interface |
| Google Colab | Writing and running the code |
| Jupyter Notebook | Organising the code into runnable cells |

## System Architecture

The game has four main parts:

1. **User interface:** the player talks to the game through a Gradio chatbot.
2. **AI Game Master:** the Gemini API reads each message and writes a response that fits the situation.
3. **Game logic:** Python checks the puzzle conditions, validates the player's answers and updates the game state.
4. **Game state:** the program remembers whether the player has found the key, unlocked the drawer, found the final code and escaped.

### How it flows

```text
Player input → Gradio interface → Python game logic → Gemini API → AI response → Player
```

Every time the player finishes a puzzle, the game state is updated.

## Implementation

The project was built in Google Colab. The repository has two notebook versions:

- `AI_Escape_Room_V1.ipynb`
- `AI_Escape_Room_V2.ipynb`

Both contain the Game Master, the game instructions, the puzzle logic and the interface.

### System Prompt

The system prompt tells the AI what its job is and how to behave as the Game Master. It should:

- Describe the room the player is in.
- React to what the player does.
- Accept correct solutions to the puzzles.
- Give hints when asked.
- Point the player toward the final exit.
- Not give away answers before the player has found them.
- Stay consistent with how far the player has progressed.

### Game State

Progress is stored in a Python dictionary with four variables:

| Variable | What it tracks |
|---|---|
| `brass_key_found` | Whether the brass key has been found |
| `drawer_unlocked` | Whether the desk drawer is open |
| `final_code_found` | Whether the final exit code has been discovered |
| `escaped` | Whether the player has got out |

These keep the player on the intended path, so they can't skip ahead to the end.

### The Game Master Function

The `game_master()` function handles every message the player sends. It:

- Takes in the player's input.
- Checks the current game state.
- Works out whether a puzzle has been solved.
- Gets a response from Gemini.
- Adds the exchange to the conversation history.

It also catches errors, so a failed request doesn't crash the game halfway through.

## Story and Puzzle Design

The story is set in a locked library. To get out, the player has to find clues and get through three stages.

### Puzzle 1: Find the Brass Key

There is an oil painting on the library wall. If the player looks closely at it and checks behind it, they find a hidden brass key.

- **Expected action:** Examine the painting and look behind it.
- **Result:** The brass key is found.

### Puzzle 2: Unlock the Desk Drawer

A large mahogany desk has a locked drawer. The player needs the brass key and the correct combination to open it.

- **Required code:** `2413`
- **Result:** The drawer opens and there is a slip of paper inside with another code on it.

### Puzzle 3: Escape the Library

The paper in the drawer shows the final exit code.

- **Final exit code:** `7391`
- **Result:** The player types it into the digital keypad on the main door, the door unlocks and they escape.

> **Spoiler warning:** the codes above give away the whole game. If you want people to play it fresh, consider removing them from this README.

## Gradio Interface

Gradio gives the game its chat window. Through it, the player can:

- Type messages to the Game Master.
- Ask about their surroundings.
- Inspect objects in the room.
- Read the AI's replies.
- Ask for hints.

The app is launched from Google Colab. Using `share=True` creates a temporary public link, so other people can try the game too.

## Testing and Results

The game was tested by playing through the whole sequence from start to finish.

| Test | Player action | Expected result |
|---|---|---|
| 1 | Ask about the surroundings | The AI describes the library |
| 2 | Examine the painting | The brass key is found |
| 3 | Use the key and enter `2413` | The desk drawer unlocks |
| 4 | Inspect the drawer | The final code `7391` is revealed |
| 5 | Enter `7391` | The main door unlocks |

The full playthrough worked. The last response from the game was:

> Congratulations! You have escaped The Mystery of the Locked Library!

The game state also showed all four progress conditions as completed.

## Security

The Gemini API needs an API key, so keep these rules in mind:

- Never upload API keys to a public GitHub repository.
- Store keys in Colab Secrets or environment variables.
- Don't let keys show up in notebook outputs.
- Don't share private configuration details.

## Limitations

- The game has a fixed set of puzzles.
- The story only takes place in one room, the library.
- It depends on the Gemini API being available.
- The AI's replies can differ from one playthrough to the next.
- A Gradio share link is temporary and isn't proper hosting.

## Future Improvements

- [ ] More rooms and puzzle levels
- [ ] Difficulty settings
- [ ] A countdown timer
- [ ] Images and visual clues
- [ ] A nicer interface
- [ ] A scoring system
- [ ] Saved player progress
- [ ] Permanent hosting

## Conclusion

This project shows how AI can be built into a small interactive game. By combining Python, the Gemini API and Gradio, it creates a game where the player solves puzzles by simply typing what they want to do.

Along the way it covers large language models, prompt writing, state tracking and building a simple app. Finishing a full playthrough of all three puzzles showed that the game works the way it was planned.

---

**Author:** Sarang Chackalayil Soman
**Repository:** AI-Escape-Room
**Documentation version:** 1.0
