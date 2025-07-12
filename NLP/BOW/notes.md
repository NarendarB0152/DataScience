
---

## 1. One-Hot Encoding

**What it is:**
Transforms a categorical variable with *𝑘* unique values into *𝑘* binary (0/1) features, one per category.

**Real-time example:**
Imagine an online clothing store where each product has a “color” attribute chosen from {Red, Blue, Green}. If you one-hot encode “color” you get three new features:

| Color | is\_Red | is\_Blue | is\_Green |
| :---: | :-----: | :------: | :-------: |
|  Red  |    1    |     0    |     0     |
|  Blue |    0    |     1    |     0     |
| Green |    0    |     0    |     1     |

A machine-learning model (say, to predict sales) can now use these binary flags instead of a single “color” column, avoiding any unintended ordinal relationships.

---

## 2. Label Encoding

**What it is:**
Replaces each category with an integer label (e.g. 0, 1, 2, …).

**Real-time example:**
A school’s grading system: Grades ∈ {A, B, C, D, F}. You could label-encode:

| Grade | Encoded |
| :---: | :-----: |
|   A   |    0    |
|   B   |    1    |
|   C   |    2    |
|   D   |    3    |
|   F   |    4    |

*When to use/avoid:*

* **Use** if there **is** a natural order (A > B > C…).
* **Avoid** on nominal categories (e.g. “color”), since “Green”→2 and “Red”→0 would imply an order that doesn’t exist.

---

## 3. Bag-of-Words (BoW)

**What it is:**
Converts text into fixed-length vectors by counting how many times each word in a “vocabulary” appears in a document.

**Real-time example:**
Spam detection on email subjects. Suppose the vocabulary (across your dataset) is {“free”, “win”, “hello”, “offer”}. Then each email is a 4-dim vector of counts:

| Subject                 | free | win | hello | offer |
| :---------------------- | :--: | :-: | :---: | :---: |
| “win free offer now”    |   1  |  1  |   0   |   1   |
| “hello friend”          |   0  |  0  |   1   |   0   |
| “special offer for you” |   0  |  0  |   0   |   1   |

A classifier can then learn which patterns of word-counts indicate spam.

---

## 4. TF-IDF (Term Frequency – Inverse Document Frequency)

**What it is:**
Weights word counts by how “important” they are:

* **Term Frequency (TF):** raw count of the word in the document.
* **Inverse Document Frequency (IDF):** down-weights words that appear in many documents.

$$
\text{tf-idf}(t,d) = \underbrace{\frac{\#\,\text{of times }t\text{ appears in }d}{\text{total terms in }d}}_{\displaystyle\text{TF}} 
\times
\underbrace{\log\!\bigl(\tfrac{N}{1 + \#\,\text{docs containing }t}\bigr)}_{\displaystyle\text{IDF}}
$$

**Real-time example:**
A news-recommendation system:

* Common words like “the” or “and” have low IDF (they appear everywhere), so even if they appear often (high TF), their overall tf-idf weight is small.
* A topic-specific word like “election” might appear heavily in political articles but rarely elsewhere—so its tf-idf is high in those articles, helping the recommender match users interested in politics.

---

### When to choose which?

* **Label Encoding:** ordinal categories only.
* **One-Hot:** nominal categories with relatively few unique values.
* **Bag-of-Words:** straightforward text count vectors, good for simple classification.
* **TF-IDF:** when you need to highlight discriminative words and suppress common ones in textual data.

