# Hybrid Book Recommendation System

## Overview

This project implements a hybrid content-based book recommendation system using Natural Language Processing (NLP) and similarity scoring techniques. The system allows users to search by title, author, or genre and receive intelligent recommendations based on textual similarity and normalized rating scores.

The recommendation engine combines:

- TF-IDF text vectorization  
- Cosine similarity scoring  
- Genre overlap logic  
- Author-based filtering  
- Rating-weighted ranking  
- Pagination for scalable result display  

The system is designed as a modular, CLI-based prototype suitable for backend integration into larger reading or book-management platforms.

---

## Objective

To build a scalable, explainable, and interpretable recommendation engine that:

- Suggests similar books based on plot, genre, and author context  
- Prioritizes quality using normalized ratings  
- Maintains transparency in recommendation logic  
- Avoids collaborative filtering cold-start issues  
- Demonstrates real-world NLP pipeline integration  

---

## Dataset Structure

The system operates on structured JSON data:

### Book Data (BD.json)
- ISBN Number  
- Title  
- Author  
- Author_ID  
- Genre  
- Description  
- Ratings  
- Year of Publication  
- Publisher  
- Series / Standalone  

### Author Data (AD.json)
- author_id  
- author_name  
- genres  
- book_count  
- author_description  
- author_rating  

---

## Recommendation Strategies

### 1. Genre-Based Filtering
Identifies books sharing one or more genres with the selected title.
Ranks results using:
- Genre overlap count
- Ratings

### 2. Author-Based Filtering
Returns books written by the same author.
Sorted by ratings.

### 3. Plot & Style Similarity (Core Model)

Implements NLP-driven similarity:

- Creates a weighted text "soup" using:
  - Description (weighted ×2)
  - Genre
  - Author
- Applies **TF-IDF Vectorization**
- Computes **Cosine Similarity**
- Filters top 10% similarity threshold
- Final score =  
  `0.7 × similarity + 0.3 × normalized rating`

This balances textual relevance with book quality.

---

## Technical Pipeline

1. Data Cleaning
   - Strip whitespace
   - Remove duplicates (Title + Author)
   - Handle missing values
   - Normalize ratings using MinMaxScaler

2. Text Vectorization
   - TF-IDF (unigrams)
   - Stop-word removal
   - Max document frequency threshold (0.85)

3. Similarity Computation
   - Cosine similarity matrix
   - Threshold filtering (90th percentile)

4. Ranking
   - Weighted scoring
   - Pagination for scalable viewing

---

## Pagination System

Large result sets are handled via CLI pagination:

- Displays 10 results per page
- Navigation:
  - n → next page
  - p → previous page
  - q → quit

Prevents overload and improves usability.

---

## Why Cosine Similarity?

Cosine similarity is chosen because:

- Measures directional similarity, not magnitude
- Works well with high-dimensional sparse TF-IDF vectors
- Scale-invariant
- Efficient for text-based recommendation systems

---

## Tools & Technologies

- Python
- Pandas
- Scikit-learn
  - TfidfVectorizer
  - Cosine Similarity
  - MinMaxScaler
- JSON Data Processing

---

## Key Features

- Hybrid scoring logic
- Similarity thresholding
- Weighted ranking
- Explainable model

---

## Limitations

- No collaborative filtering
- Dependent on quality of book descriptions
- CLI-based prototype (no GUI)
- Rating weighting manually tuned

---
