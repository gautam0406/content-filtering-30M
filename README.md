# 🎥 Content-Based Movie Recommendation System

This Jupyter Notebook implements a **content-based movie recommendation** system using the MovieLens dataset. It demonstrates the full pipeline from data ingestion to generating movie recommendations based on textual features and cosine similarity.

---

## 📚 Dataset

The notebook uses three MovieLens CSV files:

- **movies.csv** (`/kaggle/input/recommend/movies.csv`): Contains `movieId`, `title`, and `genres`. It has 87585 rows
- **ratings.csv** (`/kaggle/input/recommend/ratings.csv`): Contains user ratings (not used directly in content filtering). It has 32000204 rows
- **tags.csv** (`/kaggle/input/recomm/tags.csv`): Contains user-generated tags for movies. It has 2000072 rows

---

## 🚀 Notebook Workflow

1. **Environment Setup**  
   - Import essential libraries: `numpy`, `pandas`, `dask.dataframe`, `nltk`, `sklearn`, etc.
   - Configure Dask for scalable CSV reading.

2. **Data Loading & Initial Inspection**  
   - Load `movies.csv`, `ratings.csv`, and `tags.csv` into Dask DataFrames.
   - Preview the first few rows to understand schema.

3. **Title & Year Extraction**  
   - Parse the `year` from the movie `title` (e.g., “Toy Story (1995)” → `1995`).
   - Clean titles by removing the year parentheses.
   - Filter for movies released from 1990 onwards.

4. **Title Cleaning**  
   - Detect and correct jumbled titles (e.g., “Avengers, The” → “The Avengers”).
   - Remove any residual parentheses or extra annotations.

5. **Genre & Tag Processing**  
   - Split `genres` by `|` and convert to lowercase.
   - Lowercase and aggregate `tags` per `movieId`, dropping duplicate or null entries.
   - Merge cleaned movie and tag data into a single Pandas DataFrame.

6. **Feature Engineering**  
   - Combine `genres` and `tags` into a single text field `combined_features`.
   - Apply NLTK’s `PorterStemmer` to stem words in `combined_features`.

7. **Vectorization & Similarity Computation**  
   - Use `CountVectorizer` (max_features=5000, English stop-words) to convert text to numeric vectors.
   - Compute the cosine similarity matrix of shape (n_movies × n_movies).

8. **Recommendation Function**  
   - Define `recommend(movies_df, cos_sim, movie_titles, num_recommendations=5)`.
   - For each input movie title:
     - Lookup its index.
     - Sort other movies by similarity.
     - Return top-N similar movie titles.

9. **Example Usage**  
   - Test with sample movies: `["inception", "toy story", "the conjuring"]`.
   - Display top 5 recommendations for each.

---

## 🔧 How to Use

1. Open this notebook in Jupyter or Kaggle environment.
2. Ensure the `/kaggle/input/recommend/` and `/kaggle/input/recomm/` directories contain the CSV files.
3. Run all cells in order to:
   - Prepare and clean data.
   - Generate the similarity matrix (may take several minutes).
   - Execute the `recommend` function on your chosen titles.

---

## ⚙️ Dependencies

- Python 3.x  
- numpy  
- pandas  
- dask  
- nltk  
- scikit-learn  

Install via:

```bash
pip install numpy pandas dask nltk scikit-learn
```

Ensure you have downloaded the NLTK resources (e.g., `punkt`) if required:

```python
import nltk
nltk.download('punkt')
```

---

## 📈 Results

After running the notebook, you can explore the output cells showing:

- Cleaned and stemmed feature examples.
  
  ![image](https://github.com/user-attachments/assets/87cb0044-5215-4de3-8929-0d6d4cdfdaa0)

  
- Cosine similarity matrix snippet.
  
  ![image](https://github.com/user-attachments/assets/f533f3dd-67b5-49d8-8219-e3e5b55240a1)


- Sample recommendation lists.
  
  ![image](https://github.com/user-attachments/assets/baec9c02-1057-4a50-918d-e3e8a504c054)


---

