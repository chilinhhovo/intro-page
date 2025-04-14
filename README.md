# How We Mapped Humor: A Methodology for Human and AI Captions

## I. Introduction

What makes a cartoon caption funny? Is it sarcasm, surprise, or just something totally absurd?  
To answer this, we analyzed thousands of New Yorker-style cartoon captions—both human-written and AI-generated—to identify patterns in humor, tone, and originality.

This repository documents the end-to-end pipeline: from data wrangling to clustering to zero-shot trait labeling.

---

## II. Data Sources

We worked with two major datasets:

- **Human captions**: Crowdsourced submissions and New Yorker contest winners  
- **AI captions**: Generated using ChatGPT and Claude with standardized prompts  

Each entry includes:
- Contest number  
- Caption text  
- Funniness votes (for human captions)  
- Model origin (`human`, `chatgpt`, `claude`)  

---

## III. Cleaning and Preprocessing

Steps taken:
- Filtered for English captions under 100 words  
- Removed duplicates and stray punctuation  
- Lowercased all text  
- Tagged captions by contest and model  
- Preserved `mean` and `precision` scores for human captions  

---

## IV. Embedding and Clustering

We used sentence embeddings to represent humor style:
- Model: `all-MiniLM-L6-v2` (384-dim vectors)  
- Dimensionality reduction via `UMAP` (to 2D for plotting)  
- Clustered with `KMeans` into **10 humor types**  

Clusters represented humor "personalities":
- Surreal setups  
- Corporate irony  
- Zen observations  
- etc.

---

## V. Humor Traits with THREES

We labeled captions using the **THREES** framework (via zero-shot classification), this is based on Peter McGraw and Caleb Warre's studies:

- **T**arget  
- **H**ostility  
- **R**ealism  
- **E**xaggeration  
- **E**motion  
- **S**urprise  

We then compared trait frequency:
- AI vs. Human captions  
- Trait vs. Funniness score  

---

## VI. Labeling Humor Clusters

To give meaning to numeric cluster IDs:
- Sampled top captions per cluster  
- Used GPT-4 to suggest short labels  
- Revised for clarity and distinctiveness  

Examples:
- `Cluster 0`: _Surreal Setups_  
- `Cluster 3`: _Zen Observations_  
- `Cluster 9`: _Corporate Irony_  

---

## VII. Comparing AI vs. Human Captions

We compared:
- Average funniness score per cluster  
- THREES trait frequency  
- Caption length and complexity  
- Humor style distribution  

 _Finding_:  
AI captions leaned toward sarcasm and realism.  
Human captions explored more surprise and darkness.

---

## VIII. Visualizations

Built visual layers to explore the humor space:
- UMAP scatterplots of humor clusters  
- Bar charts: Funniness × Traits × Clusters  
- Heatmaps: AI vs. Human tone profiles  

Built with:
- `matplotlib`, `seaborn`, `Observable` + `d3.js`  

---

## IX. Tools Used

- **Python**: `pandas`, `scikit-learn`, `umap-learn`, `matplotlib`, `seaborn`  
- **NLP**: Hugging Face `transformers` (embeddings, zero-shot classification)  
- **AI Captioning**: `ChatGPT`, `Claude`  
- **Visualization**: `Observable`, `d3.js`  

---

## X. Limitations

Humor is subjective  
Cluster boundaries are fuzzy  
THREES traits are zero-shot estimates, not perfect labels  

---

## XII. Reflections

### 🎙️ Insights
An idea echoed by my interviewee, Stephen Turban (an American, stand-up comedian in Vietnam, learning and constructing quotes in Vietnamese), really stuck: _surprise goes a long way in humor_. That same pattern consistently showed up in our data too—captions with unexpected twists tended to score higher.

### 😮‍💨 Struggles
- Spent **3 brutal days** trying to animate dot transitions on the page—just moving dots turned out to be harder than analyzing them!
- Claude (the AI model) generated a lot of rambling, so I had to clean up its outputs with **custom regex** and **manual checks** to make sure I was only comparing real captions.
- Making statistical charts feel visually interesting was a serious challenge—I was often too deep in the code to think creatively.

### ✅ Wins
- Built a full **news-style gallery app** from scratch  
- Learned how to create an on-page **interactive quiz**  
- Pulled off a small but functional **interactive scrollytelling sequence**

## Conclusion

By combining:
- Sentence embeddings  
- Humor clustering  
- THREES trait analysis  
- AI vs. Human comparisons  

...we map **not just how funny** a caption is,  
but **how it tries to be funny**—and whether machines can do it too.

