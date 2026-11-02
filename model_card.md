# 🎧 Model Card: Music Recommender Simulation

## Model Name

**Vibe Match Music Recommender**

---

## Goal / Task

Recommend the five songs in the catalog that best match a listener's favorite genre, favorite mood, and desired energy level.

---

## Data Used

The recommender uses a catalog of 18 songs. Each record includes genre, mood, energy, tempo, valence, danceability, and acousticness, but the scoring currently uses only genre, mood, and energy. There is no listener history or feedback data.

---

## Algorithm Summary

This is a simple content-based recommender: it compares each song with one listener's preferences and sorts songs by score. A genre match adds 2 points, a mood match adds 1 point, and energy adds `1 - abs(song_energy - target_energy)` points (up to 1 when the values are on the 0-to-1 scale). The runner displays the five highest-scoring songs and explains the score.

---

## Observed Behavior / Biases

Matching the requested genre and mood can produce sensible results, but the catalog has only 18 songs, so it offers limited variety and may lack good matches. The score ignores lyrics, artists, listening context, and several available song features; exact genre and mood labels may also miss listeners whose tastes do not fit those labels. Energy similarity rewards being close to one target, which may not represent a listener with mixed or changing preferences.

In the weight-shift experiment, genre changed from 2 points to 1, mood stayed at 1, and energy's contribution doubled. Scores changed, but the top-five rankings stayed the same for all four test profiles. This small experiment does not show which recommendations real listeners would prefer.

---

## Evaluation Process

I tested four profiles and checked whether each list matched its preferred genre, mood, and energy. Here are the top five results in order:

- **High-Energy Pop:** Sunrise City, Gym Hero, Rooftop Lights, Paper Lantern Dance, Saturday Parade. Sunrise City leads because it matches pop and happy and is close to the high-energy target.
- **Chill Lofi:** Midnight Coding, Library Rain, Focus Flow, Spacewalk Thoughts, Wildflower Map. The first two match both lofi and chill; Focus Flow is also lofi and has almost exactly the target energy, though its mood is focused rather than chill.
- **Deep Intense Rock:** Storm Runner, Gym Hero, Comet Trail, Paper Lantern Dance, Sunrise City. Storm Runner matches rock and intense and is close to the high-energy target.
- **High-Energy Melancholic Blues:** Blue Hour Train, Comet Trail, Gym Hero, Storm Runner, Paper Lantern Dance. Blue Hour Train matches blues and melancholic, so it ranks first even though its energy similarity is only 0.51. Its genre and mood matches outweigh the energy gap; the other songs near the top have energy closer to the target but match neither preferred label.

Gym Hero is a notable surprise because it appears for both Pop and Rock. It matches the Pop profile's genre and has high energy, while for Rock it matches the intense mood and has high energy; it does not need to match every preference to rank well. The blues result is also a reminder that a top rank means “highest score under these rules,” not necessarily a perfect fit for everything the listener asked for.

The six pairwise comparisons show which profiles have similar results and why:

1. **High-Energy Pop vs. Chill Lofi:** Their top-five lists do not overlap. The Pop list favors happy pop and high-energy tracks; the Lofi list favors lofi/chill songs near the lower energy target.
2. **High-Energy Pop vs. Deep Intense Rock:** They share Gym Hero. It is pop and energetic, helping it for Pop, and it is intense and energetic, helping it for Rock. The remaining songs differ because the profiles favor different genres and moods.
3. **High-Energy Pop vs. High-Energy Melancholic Blues:** They share Gym Hero and Paper Lantern Dance. Both lists favor energetic songs, but Pop also rewards happy/pop matches while Blues rewards melancholic/blues matches, putting Sunrise City first for Pop and Blue Hour Train first for Blues.
4. **Chill Lofi vs. Deep Intense Rock:** Their top-five lists do not overlap. Their energy targets are far apart, and their preferred genres and moods—lofi/chill versus rock/intense—are different.
5. **Chill Lofi vs. High-Energy Melancholic Blues:** Their top-five lists do not overlap. The Lofi profile favors low-energy chill tracks, while the Blues profile favors melancholic blues and asks for high energy, so the two lists reflect different moods, genres, and energy targets.
6. **Deep Intense Rock vs. High-Energy Melancholic Blues:** They share Comet Trail, Gym Hero, Storm Runner, and Paper Lantern Dance. Both profiles target high energy, so energetic songs can score well for both. Storm Runner leads for Rock because it matches rock and intense; Blue Hour Train leads for Blues because it matches blues and melancholic despite lower energy.

I also compared the original weights (genre match = 2 points, mood match = 1, energy similarity = 1 times its similarity) with the experiment (genre = 1, mood = 1, energy = 2 times its similarity). The scores changed, but the top-five rankings stayed in the same order for all four profiles. This small test shows the weight change affected score values but did not change these lists; it does not establish which lists real listeners would prefer.

---

## Intended Use and Non-Intended Use

This project is for classroom exploration of how simple recommendation scores work. It can demonstrate how genre, mood, and energy affect a short list, but it is not intended as a production music service or as a reliable measure of an individual listener's taste.

---

## Ideas for Improvement

- Expand the catalog with more songs and a wider range of genres, moods, and energy levels.
- Let listeners rate recommendations, then use that feedback to check whether the results match their tastes.
- Ask for preferences such as tempo or acousticness and use them in scoring, while checking that the top results remain varied.

---

## 9. Personal Reflection  

A few sentences about your experience.  

## 9. Personal Reflection

Working on this project helped me understand how music recommendation systems work and how they use different preferences to suggest songs. Before this project, I didn't really think about how much the scoring system matters. I learned that even a simple algorithm can make recommendations by comparing things like genre, mood, and energy.

One thing that surprised me was how changing the scoring weights didn't change the order of the recommendations. I also found it interesting that Blue Hour Train ranked first even though its energy didn't really match what the listener wanted. That showed me that just because a song has the highest score doesn't mean it's the perfect recommendation.

Using AI tools like GitHub Copilot helped me understand the code, fix issues, and test different ideas. However, I also learned that I shouldn't just trust everything AI gives me. I had to check the results in the terminal, run tests, and make sure the calculations and recommendations made sense.

This project also changed how I look at music recommendation apps. I realized that recommendations aren't always as complicated as they seem, but the way a system is designed can affect what people see. If I continued this project, I would add more songs, allow users to give feedback, and include more preferences to make the recommendations better.

Overall, this was a good learning experience because I got to see how coding, AI tools, and testing work together to build a recommendation system.