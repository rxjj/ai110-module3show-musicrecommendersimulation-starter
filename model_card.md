# 🎧 Model Card: Music Recommender Simulation

## 1. Model Name  

Give your model a short, descriptive name.  
Example: **VibeFinder 1.0**  

---

## 2. Intended Use  

Describe what your recommender is designed to do and who it is for. 

Prompts:  

- What kind of recommendations does it generate  
- What assumptions does it make about the user  
- Is this for real users or classroom exploration  

---

## 3. How the Model Works  

This recommender uses **content-based filtering**: it compares details about each song with the listener's preferences. A song gets 2 points if its genre matches the listener's favorite genre and 1 point if its mood matches. It also gets an energy similarity score calculated as `1 - abs(song_energy - target_energy)`, so songs with energy closer to the listener's target score higher. The system adds these points together, ranks songs from highest score to lowest, and returns the top results.

---

## 4. Data  

Describe the dataset the model uses.  

Prompts:  

- How many songs are in the catalog  
- What genres or moods are represented  
- Did you add or remove data  
- Are there parts of musical taste missing in the dataset  

---

## 5. Strengths  

Where does your system seem to work well  

Prompts:  

- User types for which it gives reasonable results  
- Any patterns you think your scoring captures correctly  
- Cases where the recommendations matched your intuition  

---

## 6. Limitations and Bias 

Where the system struggles or behaves unfairly. 

The catalog has only 18 songs, so it offers limited variety and may not include good matches for many listeners; its narrow set of song features also leaves out aspects of taste such as lyrics, artists, and listening context. The original weights favored genre, while our experiment gave genre and mood 1 point each and doubled the energy-similarity contribution, so changing weights shifted scores without changing the top-five rankings for any of our four test profiles. This shows that tuning scores alone did not alter these results, and it does not prove that the recommendations are accurate for real listeners. The formula rewards closeness to a single target energy, which can favor energetic songs even when the listener also wants a contrasting mood, and does not model more complex preferences. Exact genre and mood matches can also disadvantage listeners whose preferred styles or combinations are missing from this small catalog.

Prompts:  

- Features it does not consider  
- Genres or moods that are underrepresented  
- Cases where the system overfits to one preference  
- Ways the scoring might unintentionally favor some users  

---

## 7. Evaluation  

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

## 8. Future Work  

Ideas for how you would improve the model next.  

Prompts:  

- Additional features or preferences  
- Better ways to explain recommendations  
- Improving diversity among the top results  
- Handling more complex user tastes  

---

## 9. Personal Reflection  

A few sentences about your experience.  

Prompts:  

- What you learned about recommender systems  
- Something unexpected or interesting you discovered  
- How this changed the way you think about music recommendation apps  
