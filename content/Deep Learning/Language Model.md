# Language Model

Learning a good distribution $p(s)$ of sentences. Such problem is called **language modeling**.

Generally, we would like to assume each sentence are independent so that we will have MLE i.e. $\max \prod_{i=1}^n p(s_i)$ and the log-likelihood is $\sum_{i=1}^n \log p(s_i)$ (the ccross-entropy loss).

Sometimes, we look even deeper where a sentence is a sequence of words. We can apply chain rule of conditional probability where we would have $p(s) = p(w_1,\ldots, w_T) = p(w_1)p(w_2|w_1)\ldots p(w_T|w_1,\ldots, w_{T-1})$. Again, to simplify the problem, we have **Markov assumption** (the distribution over next word only depends on the preceding few words). Some property Markov assumption will bring:

- model now is memoryless
- since we care some words, it's a supervised prediction problem
- When we deccompose it into separate prediction problems, it's called an autoregressive model.

## n-gram

The simpliest way to estimate the probabilities is from the empirical distribution (i.e. count the frequencies of words). Let's say length with $n$, then such model will be modelling is an **$n$-gram language model** and such pharse (the $n$ words) is called **n-gram**. The problem of this model:

- expoential computation cost based on the length of the sentence
- most n-gram never appear in the corpus (data sparsity)

### Solution to data sparsity

- Use a short context (then will lead less accurate model)
- Smooth the probabilities (i.e. add a small constant to the counts)
- Make predictions using an ensemble of models with different length.

## Distributed Representations

Condtional probaility tables (n-gram is one kind of) are kind of **localist representation**, more specifically, all the information about a particular word is stored in one place. Since different words may related to each other, we may share information between them.

Furthermore, the information about a given word is distrbuted throught the representations is called **distributed representation**. That is, we can use such representation to share information between words.

The most common model we would like to use is **Nerual Language Model** which takes previous $K$ words and output the next word. The cross-entropy here $-\log p(s) = -\log \prod_{t = 1}^T p(w_t|w_{t-K},\ldots, w_{t-1})$ with predicted probability not the frequency of the word as n-gram.

- We can extend to $-\log p(s) = -\sum_{t=1}^T\sum_{v=1}^Vt_{v,t}\log y_{iv}$ where $y_{iv}$ is the probability of the $i$-th word being index $v$.

More about [nlm](https://www.jmlr.org/papers/volume3/bengio03a/bengio03a.pdf).

Let's say we would like to use a 1-of-K encoding for the words, then the first layer will be a linear layer with **tied weights** which basically act like a look table. Each column of this matrix is the representation of a word (it's called **embedding**, **feature vector** or **encoding** with different emphasis).

- Embedding emphasizes that it's a location in a high-dimensional space where words closer to each other are more semantically similar.
- Feature vector emphasizes that it's a vector of numbers that can be used as input to a machine learning algorithm.

### Problems

In high-dimensional embeddings:

- Most vectors are nearly orthogonal to each other.
- Most points are far away from from each other.

Lower-dimensional embeddings:

- 2-D embeddings might be misleading since they can't preserve the distance relationships

Most of times, we the fitting of language models is really hard and it might overkill if all we want is to use the embeddings. 

## Glove

GloVe (**Global Vector**) embedding is a simpler and faster approach based on a matrix factorization similar to principal compooent analysis (PCA). According to the distributional hypothesis: words with similar distributions have similar meanings, we may consider a **co-occurrence matrix** X which counts the number of times two words appear nearby. We have a rank-K approximation $X \approx R\tilde{R}$ where $R, \tilde{R}$ are $V\times K$ matrices.

- each row $r_i$ of $R$ is the K-dimensional representation of a word.
- each entry $x_{ij} \approx r_i^T \tilde{r}_j$
- more similar words are more likely to co-occur
- minimize the squared frobenius norm $\|X - R\tilde{R}\|_F^2$ (PCA). It leads to the GLove embedding cost function $\mathcal{J}(R) = \sum_{i,j=1}^V f(x_{ij})(r_i^T \tilde{r}_j + b_i + \tilde{b_j} - \log x_{ij})^2$ where $f(x_{ij}) = \begin{cases} (x_{ij}/100)^{3/4} & x_{ij} < x_{max} \\ 1 & x_{ij} \geq 100 \end{cases}$ is used to reweight the entries so that only nonzero counts matter to avoid infeasible factorization caused by extremely large. The $\log x_{ij}$ is used to reduce the effect of most common words.
