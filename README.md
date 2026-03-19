# 🎮 Game Glitch Investigator: The Impossible Guesser

## 🚨 The Situation

You asked an AI to build a simple "Number Guessing Game" using Streamlit.
It wrote the code, ran away, and now the game is unplayable. 

- You can't win.
- The hints lie to you.
- The secret number seems to have commitment issues.

## 🛠️ Setup

1. Install dependencies: `pip install -r requirements.txt`
2. Run the broken app: `python -m streamlit run app.py`

## 🕵️‍♂️ Your Mission

1. **Play the game.** Open the "Developer Debug Info" tab in the app to see the secret number. Try to win.
2. **Find the State Bug.** Why does the secret number change every time you click "Submit"? Ask ChatGPT: *"How do I keep a variable from resetting in Streamlit when I click a button?"*
3. **Fix the Logic.** The hints ("Higher/Lower") are wrong. Fix them.
4. **Refactor & Test.** - Move the logic into `logic_utils.py`.
   - Run `pytest` in your terminal.
   - Keep fixing until all tests pass!

## 📝 Document Your Experience

- [x] **Describe the game's purpose.**
  - The Game Glitch Investigator is a number guessing game built with Streamlit that tests players' ability to guess a secret number within a given range. Players can choose three difficulty levels (Easy: 1-20, Normal: 1-100, Hard: 1-500) and receive hints whether their guess is too high or too low. The game tracks attempts and scores based on performance. The original code was AI-generated and intentionally contained bugs for learning purposes.

- [x] **Detail which bugs you found.**
  - **Bug #1**: Hard difficulty range was 1-50 instead of larger than Normal (1-100), making Hard easier, not harder.
  - **Bug #2**: Higher/lower hints were reversed - saying "Go HIGHER!" when guess was too high.
  - **Bug #3**: Hardcoded range message displayed "1 and 100" instead of showing the actual difficulty range.
  - **Bug #4**: Changing difficulty didn't auto-refresh the game; required manual page reload.
  - **Bug #5**: Type mismatch where secret number was sometimes string, sometimes int, causing comparison errors.
  - **Bug #6**: `attempt_limit` wasn't initialized in session_state, causing KeyError on first page load.
  - **Bug #7**: Attempts counter was off by 1 (started at 1 instead of 0), giving players fewer guesses than allowed.

- [x] **Explain what fixes you applied.**
  - Fixed Hard difficulty range from 1-50 to 1-500 in `get_range_for_difficulty()`.
  - Swapped reversed hint messages in `check_guess()` - now correctly says "Go LOWER!" when too high and "Go HIGHER!" when too low.
  - Replaced hardcoded "1 and 100" with dynamic `f"Guess a number between {low} and {high}."` using difficulty-based variables.
  - Added difficulty change detection to automatically reset game state (secret, attempts, score) when player switches difficulty.
  - Removed buggy type conversion logic that was converting secret to string on even attempts.
  - Added `attempt_limit` initialization check to session_state to prevent KeyError on first load.
  - Changed `attempts` initialization from 1 to 0 in three locations (initial setup, difficulty change, new game button) to fix counter accuracy.
  - Refactored all game logic functions into `logic_utils.py` for better code organization and modularity.
  - Verified all fixes with pytest tests and manual gameplay testing across all difficulty levels.

## 📸 Demo

- [ ] [Insert a screenshot of your fixed, winning game here]

## 🚀 Stretch Features

- [ ] [If you choose to complete Challenge 4, insert a screenshot of your Enhanced Game UI here]
