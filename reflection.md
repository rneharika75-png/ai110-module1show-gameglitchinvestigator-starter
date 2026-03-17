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
  - I used ChatGPT and GitHub Copilot to understand the code and help with debugging.

- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
  - AI explained how Streamlit session state works and how it stores values like the secret number and attempts.
  - I verified this by running the game and checking how the values changed during gameplay.

- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).
  - One AI suggestion about the hint logic was confusing and did not fix the problem correctly.
  - I verified this by testing the game again and observing that the hints were still reversed.
  
---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
  - I ran the game again after making changes and tested different guesses.
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
  - I entered numbers higher and lower than the secret number to check if the hints were correct.
  - I also tested different difficulty levels to see if the secret number stayed within the expected range.

- Did AI help you design or understand any tests? How?
  - AI helped me understand how to test the program by suggesting trying different inputs and checking the results.

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
