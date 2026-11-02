# 🎵 Music Recommender Simulation

## Project Summary

In this project you will build and explain a small music recommender system.

Your goal is to:

- Represent songs and a user "taste profile" as data
- Design a scoring rule that turns that data into recommendations
- Evaluate what your system gets right and wrong
- Reflect on how this mirrors real world AI recommenders

Replace this paragraph with your own summary of what your version does.

---

## How The System Works

Collaborative filtering recommends songs based on what other listeners enjoy, while content-based filtering compares a song's features with one listener's preferences. This project uses content-based filtering because its small song catalog includes song features but no listening history from multiple users.

Each `Song` has a **genre**, **mood**, and **energy**. The `UserProfile` stores a **favorite_genre**, **favorite_mood**, and **target_energy**. The recommender gives a song +2.0 points for a matching genre, +1.0 point for a matching mood, and `1 - abs(song_energy - target_energy)` points for energy similarity. It scores each song and ranks them from highest to lowest score; the highest-scoring songs are recommended.

The expanded dataset has 18 songs. For this profile, the favorite genre is "pop", the favorite mood is "happy", and the target energy is 0.8. Since a genre match is worth more than a mood match or energy similarity, the system may favor genre too strongly and overlook songs that fit the mood or energy better. The small dataset also limits the variety of recommendations.

I think genre, mood, and energy are good ways to describe a song's vibe. Genre tells me the type of music, mood describes how the song feels, and energy helps me understand if a song is calm or intense. I think these three features work well together for recommending music.

---

## Getting Started

### Setup

1. Create a virtual environment (optional but recommended):

   ```bash
   python -m venv .venv
   source .venv/bin/activate      # Mac or Linux
   .venv\Scripts\activate         # Windows

2. Install dependencies

```bash
pip install -r requirements.txt
```

3. Run the app:

```bash
python -m src.main
```

### Running Tests

Run the starter tests with:

```bash
pytest
```

You can add more tests in `tests/test_recommender.py`.

---

## Sample Recommendation Output

Paste a sample of your recommender's output here as a text block so a reader can see what it produces:

```text
Top recommendations:

Sunrise City - Score: 3.98
Because: Genre matches pop (+2.0). Mood matches happy (+1.0). Energy similarity: 0.98.

Gym Hero - Score: 2.87
Because: Genre matches pop (+2.0). Mood does not match happy (+0.0). Energy similarity: 0.87.

Rooftop Lights - Score: 1.96
Because: Genre does not match pop (+0.0). Mood matches happy (+1.0). Energy similarity: 0.96.

Saturday Parade - Score: 0.99
Because: Genre does not match pop (+0.0). Mood does not match happy (+0.0). Energy similarity: 0.99.

Night Drive Loop - Score: 0.95
Because: Genre does not match pop (+0.0). Mood does not match happy (+0.0). Energy similarity: 0.95.
```



**Screenshot or video** *(optional)*: <!-- Insert a screenshot or demo video link here -->

---

## Experiments You Tried

Use this section to document the experiments you ran. For example:

- What happened when you changed the weight on genre from 2.0 to 0.5
- What happened when you added tempo or valence to the score
- How did your system behave for different types of users

---

## Limitations and Risks

Summarize some limitations of your recommender.

Examples:

- It only works on a tiny catalog
- It does not understand lyrics or language
- It might over favor one genre or mood

You will go deeper on this in your model card.

---

## Reflection

Read and complete `model_card.md`:

[**Model Card**](model_card.md)

Write 1 to 2 paragraphs here about what you learned:

- about how recommenders turn data into predictions
- about where bias or unfairness could show up in systems like this

