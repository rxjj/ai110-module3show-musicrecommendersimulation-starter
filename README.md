# 🎵 Music Recommender Simulation

## Project Summary

This project implements a content-based music recommender over a catalog of 18 songs. It scores songs against a listener's favorite genre, favorite mood, and target energy, then returns the five highest-scoring songs with explanations for four example profiles.

---

## How The System Works

Collaborative filtering recommends songs based on what other listeners enjoy, while content-based filtering compares a song's features with one listener's preferences. This project uses content-based filtering because its small song catalog includes song features but no listening history from multiple users.

Each `Song` has a **genre**, **mood**, and **energy**. The `UserProfile` stores a **favorite_genre**, **favorite_mood**, and **target_energy**. The recommender gives a song +2.0 points for a matching genre, +1.0 point for a matching mood, and `1 - abs(song_energy - target_energy)` points for energy similarity. It scores each song and ranks them from highest to lowest score; the highest-scoring songs are recommended.

The expanded dataset has 18 songs. The command-line runner tries four profiles: High-Energy Pop, Chill Lofi, Deep Intense Rock, and a high-energy melancholic blues edge case. Genre matches are weighted more heavily than mood matches or energy similarity, and the small dataset limits the variety of recommendations.

I think genre, mood, and energy are good ways to describe a song's vibe. Genre tells me the type of music, mood describes how the song feels, and energy helps me understand if a song is calm or intense. I think these three features work well together for recommending music.

---

## Getting Started

### Setup

1. Create a virtual environment (optional but recommended):

   ```bash
   python -m venv .venv
   ```

   Activate it on macOS/Linux:

   ```bash
   source .venv/bin/activate
   ```

   Or activate it in Windows PowerShell:

   ```powershell
   .\.venv\Scripts\Activate.ps1
   ```

2. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

3. Run the app:

   ```bash
   python -m src.main
   ```

### Running Tests

Run the tests with:

```bash
pytest
```

---

## Sample Recommendation Output

The runner prints the top five recommendations for each profile. This is the output with the original scoring weights:

```text
Top 5 recommendations for High-Energy Pop:

Sunrise City - Score: 3.97
Because: Genre matches pop (+2.0). Mood matches happy (+1.0). Energy similarity: 0.97.

Gym Hero - Score: 2.92
Because: Genre matches pop (+2.0). Mood does not match happy (+0.0). Energy similarity: 0.92.

Rooftop Lights - Score: 1.91
Because: Genre does not match pop (+0.0). Mood matches happy (+1.0). Energy similarity: 0.91.

Paper Lantern Dance - Score: 0.98
Because: Genre does not match pop (+0.0). Mood does not match happy (+0.0). Energy similarity: 0.98.

Saturday Parade - Score: 0.96
Because: Genre does not match pop (+0.0). Mood does not match happy (+0.0). Energy similarity: 0.96.


Top 5 recommendations for Chill Lofi:

Midnight Coding - Score: 3.98
Because: Genre matches lofi (+2.0). Mood matches chill (+1.0). Energy similarity: 0.98.

Library Rain - Score: 3.95
Because: Genre matches lofi (+2.0). Mood matches chill (+1.0). Energy similarity: 0.95.

Focus Flow - Score: 3.00
Because: Genre matches lofi (+2.0). Mood does not match chill (+0.0). Energy similarity: 1.00.

Spacewalk Thoughts - Score: 1.88
Because: Genre does not match lofi (+0.0). Mood matches chill (+1.0). Energy similarity: 0.88.

Wildflower Map - Score: 0.98
Because: Genre does not match lofi (+0.0). Mood does not match chill (+0.0). Energy similarity: 0.98.


Top 5 recommendations for Deep Intense Rock:

Storm Runner - Score: 3.96
Because: Genre matches rock (+2.0). Mood matches intense (+1.0). Energy similarity: 0.96.

Gym Hero - Score: 1.98
Because: Genre does not match rock (+0.0). Mood matches intense (+1.0). Energy similarity: 0.98.

Comet Trail - Score: 0.99
Because: Genre does not match rock (+0.0). Mood does not match intense (+0.0). Energy similarity: 0.99.

Paper Lantern Dance - Score: 0.92
Because: Genre does not match rock (+0.0). Mood does not match intense (+0.0). Energy similarity: 0.92.

Sunrise City - Score: 0.87
Because: Genre does not match rock (+0.0). Mood does not match intense (+0.0). Energy similarity: 0.87.


Top 5 recommendations for High-Energy Melancholic Blues (Edge Case):

Blue Hour Train - Score: 3.51
Because: Genre matches blues (+2.0). Mood matches melancholic (+1.0). Energy similarity: 0.51.

Comet Trail - Score: 0.99
Because: Genre does not match blues (+0.0). Mood does not match melancholic (+0.0). Energy similarity: 0.99.

Gym Hero - Score: 0.98
Because: Genre does not match blues (+0.0). Mood does not match melancholic (+0.0). Energy similarity: 0.98.

Storm Runner - Score: 0.96
Because: Genre does not match blues (+0.0). Mood does not match melancholic (+0.0). Energy similarity: 0.96.

Paper Lantern Dance - Score: 0.92
Because: Genre does not match blues (+0.0). Mood does not match melancholic (+0.0). Energy similarity: 0.92.
```

---

## Experiments You Tried

I compared the original weights (genre = 2, mood = 1, energy similarity = 1) with genre = 1, mood = 1, and energy similarity = 2. Scores changed, but the top-five rankings stayed in the same order for all four profiles. This experiment only compares two settings on this small catalog; it does not show which recommendations listeners would prefer.

---

## Limitations and Risks

The catalog contains only 18 songs and no listener history or feedback. Scoring uses exact genre and mood matches plus one target energy value, while ignoring other available features such as tempo and valence, as well as lyrics and listening context. These rules can produce limited or imperfect matches, especially for listeners with varied preferences.

---

## Reflection

My personal reflection on the project is in the [**Model Card**](model_card.md).
