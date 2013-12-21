Title: Kaggle's Facebook competition
Date: 2013-12-21 10:20
Category: Python
Tags: python, numpy, gensim, machinelearning
Slug: kaggle-facebook-competition-keyword-extraction
Author: Alex Parij
Summary: kaggle's facebook competition


Kaggle's FacebookIII keyword extraction competition is over.
It was about predicting tags to StackExchange questions.
Check it out at [Kaggle](http://www.kaggle.com/c/facebook-recruiting-iii-keyword-extraction).

I've entered at very late stage to this competition, hence didn't have time to properly experiment. 
My final standing was quite low 316/380, but I just had 3 weeks comparing to 4 months of the total competition's length, so I'm ok with that.
It was also my first experience with Gensim library (after reading the "Building Machine Learning Systems with Python" by Rciher,Coelho). 

I've tried to model the question's topic using LDA[Read on Wikipedia](http://en.wikipedia.org/wiki/Latent_Dirichlet_allocation). For preprocessing I used NLTK with stemming, stop words and punctuation marks removed. 
Removing Less frequent words (words that I encountered only once). Tried to remove code snippets.
Then I would find the most similar question based on the topics and take the tags from training to the test question and drop less frequent tags

#So what could have I done better ?
Preprocessing should be done once, while I did every time I was building a dictionary or corpora. It would have probably sped 
it up by atleast x2. 
More automatic parallezation(although I used MLK by Contunium Analytics to get some free optimization to 4 threads).
I could have made some simple code to split/load large test file. It's still can be done manually using linux split on test.csv and then "cat * > out" combining the results.
POS tagging was too slow but I can see that with other speed improvements POS can be used to remove adjectives,adverbs and others, lowering the numbfer of features.
The were too many features (1mil words) for 3mil training entries! I should have tried to remove most of them. Removing words with freq=1 was not enough.
In the end for 3 mil training rows the similarity search was too slow and 2 mil test rows will take 48 hours to calculate. I desperately tried to move to high-end machines in Amazon cloud. It did speed up things since it had 8 cores to work and I could just split the test file across processes.
For some reason MKL or BLAS run only with one thread, I tried to use StarCluster ec2 image that comes with all the SciPy libs preinstalled but still it would persistenly run on one thread. Compiling from scratch was too complex with the limited time I had.

Anyways , next time I should start earlier.


The source is on [Github](https://github.com/aparij/KaggleFacebookIII)
