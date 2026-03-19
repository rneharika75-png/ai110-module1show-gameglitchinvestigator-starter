# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
  - The game opened in the browser using Streamlit.
  - It showed the guessing interface and difficulty settings.
  -The interface worked but some behaviors were incorrect


- List at least two concrete bugs you noticed at the start  
  (for example: "the hints were backwards").
  - Its not getting refreshed automatically
  - when u need to go high number it say go lower wise versa
  - difficulty level when its hard it shows range from 1-50 but it in secret it show 1-100 range

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
  - I used both GitHub Copilot (Claude Haiku 4.5) and ChatGPT to identify, analyze, and fix bugs together.
  - **GitHub Copilot**: Helped identify bugs through code analysis and provided real-time fixes in the editor
  - **ChatGPT**: Helped explain Streamlit concepts, session state logic, and refactoring strategies

- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
  - **What the AI suggested (GitHub Copilot)**: The attempts counter was off by 1 because it initialized to 1 instead of 0. This caused the game to display "7 attempts left" on first load instead of "8", and only give players 7 actual guesses instead of 8.
  - **Why it was correct**: The AI traced through the logic: if `attempts = 1` and `attempt_limit = 8`, then `8 - 1 = 7`. After incrementing on each guess, the game would end at 8 guesses instead of allowing a full 8.
  - **How we verified it**: After fixing the initialization to `attempts = 0` in three locations (line 56 for initial setup, line 48 for difficulty change, line 89 for new game), we tested the game and confirmed it now showed "8 attempts left" on first load and allowed exactly 8 guesses before game over.

- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).
  - **What the AI suggested (ChatGPT initially, then GitHub Copilot corrected)**: ChatGPT initially suggested refactoring logic_utils.py by moving the functions from app.py, which was technically correct but those functions had bugs in them that needed fixing first.
  - **Why it was incomplete/misleading**: The refactoring moved buggy code as-is. For example, the check_guess function in logic_utils.py had the hints reversed. Moving it to a separate file didn't fix the underlying bugs - it just moved them.
  - **How we verified it**: After reviewing the functions in [logic_utils.py](logic_utils.py), GitHub Copilot correctly identified that the hints in check_guess (lines 39-44) were backwards. We then fixed the hint messages ("Go LOWER" when guess too high, "Go HIGHER" when guess too low) and tested by playing the game with different guesses. The hints now correctly guided the player to the secret number.

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
  - I ran the game after each fix and tested the specific behavior that was broken.
  - I used the Developer Debug Info panel to check session state values like attempts, score, and secret number.
  - I tested multiple scenarios: winning, losing, changing difficulty, and clicking "New Game".

- Describe at least one test you ran (manual or using pytest) and what it showed you about your code.
  - **Test #1 (Manual - Attempts Counter)**: Started a new game and checked "Attempts left" display. On first load it showed "8 attempts left" (after fix) instead of "7" (before fix). Made 1 guess, it showed "7 attempts left" correctly. Made 8 total guesses to lose the game - it correctly ended without allowing a 9th guess. This proved Bug #7 was fixed.
  - **Test #2 (Manual - Reversed Hints)**: With secret = 50, I guessed 60 (too high). After the fix, it correctly said "📉 Go LOWER!" instead of "📈 Go HIGHER!". Then guessed 40 (too low) and it said "📈 Go HIGHER!" correctly. This proved Bug #2 was fixed.
  - **Test #3 (Pytest - check_guess function)**: Ran [tests/test_game_logic.py](tests/test_game_logic.py#L1) which tests three scenarios: winning guess, guess too high, guess too low. All assertions passed: outcome matched expected value and message contained correct hint keywords ("LOWER" or "HIGHER"). This proved the hints and outcomes were correct.
  - **Test #4 (Manual - Difficulty Range Display)**: Changed difficulty to "Easy" - sidebar showed "Range: 1 to 20" and info message showed "Guess a number between 1 and 20". Changed to "Normal" - showed "1 to 100". Changed to "Hard" - showed "1 to 500". Each time the range stayed consistent. This proved Bug #3 (hardcoded range) was fixed.
  - **Test #5 (Manual - Auto-Refresh on Difficulty Change)**: Started game on Normal, made 2 guesses. Changed difficulty to Hard - the attempts counter reset to 0, score reset to 0, new secret was generated. No manual page reload was needed. This proved Bug #4 was fixed.

- Did AI help you design or understand any tests? How?
  - Yes, GitHub Copilot helped. It suggested the structure for [test_game_logic.py](tests/test_game_logic.py) with assertions checking both the outcome and the message content.
  - ChatGPT explained how to use pytest to test functions independently without running the full Streamlit app.
  - Both AI tools recommended testing multiple paths (winning, too high, too low) rather than just one scenario, which helped catch edge cases.

---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
  - Streamlit reruns the entire script whenever a user interacts with the app.
  - To keep data between these reruns, Streamlit uses session state.
  - Session state stores values like secret number, attempts, and score so the game does not reset each time.

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
    - One habit I want to reuse is testing the program step by step while debugging.
- What is one thing you would do differently next time you work with AI on a coding task?
  - Next time I will verify AI suggestions more carefully instead of assuming they are always correct.
- In one or two sentences, describe how this project changed the way you think about AI generated code.
  - This project showed me that AI-generated code can help but it still needs human testing and debugging.
