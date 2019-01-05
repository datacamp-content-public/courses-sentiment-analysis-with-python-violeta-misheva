---
title: Insert title here
key: 11bedc6349d6ea75bdb16ef8a9289b1f

---
## Bag-of-words

```yaml
type: "TitleSlide"
key: "d654eeccce"
```

`@lower_third`
name: Name Surname
title: Instructor


`@script`
Welcome back to this Sentiment Analysis in Python course! 
In the first lesson we learned what sentiment analysis is, when we can use it, and practiced some basics using the famous IMDB  movies reviews data set! In this Chapter, we proceed on our journey by embarking on the first steps in performing a sentiment analysis task: transforming our text data to numeric form.  

Why do we need to do that? I hope by now it is clear that a machine learning model cannot work with the text data directly, but rather with numeric features we create from the data.


---
## What is a bag-of-words?

```yaml
type: "FullSlide"
key: "290fe3cc0b"
```

`@part1`
- Describes the occurrence of words within a document

- Builds a vocabulary of the words and a measure of their presence


`@script`
We start with a basic and crude, but often quite useful method, called bag-of-words. A bag-of-words approach describes the occurrence, or frequency, of words within a document, or a collection of documents (corpus). It basically sums down to building a vocabulary of all the words occurring in the document and keeping track of their frequencies.


---
## Example

```yaml
type: "FullSlide"
key: "9f089079b0"
```

`@part1`
‘’John went to the movies on Saturday to watch the new Avengers movie. Sarah does not like the Avengers and did not join him. “


_{‘John’: 1, ‘went’: 1, ‘to’: 2 , ‘the’: 3 , ’movies’: 1, ‘on’: 1, ‘Saturday’:1 , ‘watch’:1 , ‘new’: 1  , ‘Avengers’: 2 , ‘movie’: 1 , ‘Sarah’: 1 , ‘does’: 1, ‘not’: 2, ‘like’: 1 , ‘and’: 1  , ‘did’: 1 , ‘join’: 1 , ‘him’: 1}_


`@script`
Let’s start with a simple example. Imagine you have the following string:  ‘’John went to the movies on Saturday to watch the new Avengers movie. Sarah does not like the Avengers and did not join him. “

The goal of a BOW approach would be to build the following dictionary-like output: John, occurs once in our string, so it has a count of 1, went occurs once, to occurs two times and so on. 

One thing to note is that we lose the word order and grammar rules, that’s why this approach is called a ‘bag’ of words, resembling dropping a bunch of items in a bag and losing any sense of their order.

This sounds straightforward but sometimes simply deciding how to build the vocabulary can be complex because of many decision we need to make: Do we remove capital letters, do we ignore punctuation? Do we remove digits and only leave alphanumeric tokens? How many n-grams to use? Do we remove words that occur often such as ‘to’, ‘the’, ‘and’, and do we adjust that by the context of the problem we have? We will tackle these issues in later chapters.


---
## How to do that in Python?

```yaml
type: "FullSlide"
key: "296e88467b"
```

`@part1`
Initial data format: ![](https://assets.datacamp.com/production/repositories/4394/datasets/fd0fcbde68733df401f5f07a2e009f592fc757c0/initial%20format.PNG )


`@script`
How do we execute a BOW in Python? The simplest way to do this in one line is by using the CountVectorizer from the sklearn.feature_extractions.text library. CountVectorizer converts the text corpus to a sparse matrix. Let’s see how that works with an example. 
Throughout this lecture, we will work with a sample of Amazon reviews data, where we are given the score : whether the customer is happy with the product (1 if they are, 0 otherwise), and a review, which is the text.


---
## How to do that in Python? 

```yaml
type: "FullSlide"
key: "f572988ffa"
```

`@part1`
The output will look something like this: ![](https://assets.datacamp.com/production/repositories/4394/datasets/654d74967acb7bd1a2d45ed03c293a4b3562c496/final%20output.PNG)


`@script`
We apply the CountVectorizer to the text column, with the end result looking smth like the table that we see: where the column is the token, and the row represents how many times we have encountered it in the respective review.


---
## How to do that in Python?

```yaml
type: "FullCodeSlide"
key: "f298f16b47"
```

`@part1`
```
from sklearn.feature_extraction.text import CountVectorizer
import pandas as pd 

vect = CountVectorizer(max_features = 1000)
X = vect.fit_transform(data.review)

# transform back to a pandas dataframe
X_df = pd.DataFrame(X.toarray() , columns = vect.get_feature_names())

```


`@script`
We call the CountVectorizer, where for the moment we leave the default functional options, except for the max_features, which only considers the features with highest term frequency, i.e. it will pick the 1000 most frequent words across the corpus of reviews. We need to do that sometimes for memory’s sake, especially if your data is large and you work in a local environment. 

Since the output of the CountVectorizer is a sparse matrix, we need to perform an additional step to transform it back to a data frame.


---
## Let's practice!

```yaml
type: "FinalSlide"
key: "6e04cfd4e8"
```

`@script`
That was out introduction to BOW! Let's apply what we've learned in the exercises.

