# Word2Vec-Concepts

Welcome to **Word2Vec-Concepts**! This repository showcases practical applications of the Word2Vec model using the Gensim library. Dive into word vector operations and discover how semantic relationships between words can be explored and analyzed.

## 🚀 Features

- **Load Pre-trained Models**: Utilize Google's pre-trained Word2Vec model.
- **Cosine Similarity**: Measure the similarity between word vectors.
- **Odd One Out**: Identify the word that doesn’t fit in a list based on vector averaging.
- **Predict Word**: Predict the most related word given a triad using vector arithmetic.
- **Word Analogies**: Perform analogies like "king is to man as queen is to woman".

## 📦 Installation

Clone the repository and install dependencies:

```bash
git clone https://github.com/yourusername/Word2Vec-Concepts.git
cd Word2Vec-Concepts
pip install -r requirements.txt
```

## 🛠 Usage

1. **Load the Model**: 
   ```python
   from gensim.models import keyedvectors
   word_vectors = keyedvectors.load_word2vec_format('path/to/GoogleNews-vectors-negative300.bin', binary=True)
   ```

2. **Calculate Similarity**:
   ```python
   from sklearn.metrics.pairwise import cosine_similarity
   similarity = cosine_similarity([word_vectors['apple']], [word_vectors['mango']])
   print(similarity)
   ```

3. **Find the Odd One Out**:
   ```python
   def odd_one_out(words):
       all_word_vectors = [word_vectors[w] for w in words]
       avg_vector = np.mean(all_word_vectors, axis=0)
       odd_one_out = None
       min_similarity = 1.0

       for w in words:
           sim = cosine_similarity([word_vectors[w]], [avg_vector])
           if sim < min_similarity:
               min_similarity = sim
               odd_one_out = w
       return odd_one_out
   ```

4. **Predict Related Words**:
   ```python
   def predict_word(a, b, c, word_vectors):
       a, b, c = a.lower(), b.lower(), c.lower()
       max_similarity = -100
       d = None
       words = word_vectors.key_to_index.keys()
       wa, wb, wc = word_vectors[a], word_vectors[b], word_vectors[c]

       for w in words:
           if w in [a, b, c]:
               continue
           wv = word_vectors[w]
           sim = cosine_similarity([wb - wa], [wv - wc])
           if sim > max_similarity:
               max_similarity = sim
               d = w
       return d
   ```

## 📞 Contact

For any questions or feedback, feel free to open an issue or reach out to [mandavamsi302001@gmail.com](mailto:mandavamsi302001@gmail.com).
