
<div style="text-align: center; width: 100%">
  <img src="https://github-readme-stats.vercel.app/api/pin/?username=akhossanX&repo=tweets-classifier&show_owner=true&theme=monokai&show_icons=true"
       style="width: 100%"/>
</div> <a href="#"><img align="right" src="https://visitor-badge.glitch.me/badge?page_id=akhossanX.tweets-classifier" />

# Problem statement  
<p>Given a dataset of tweets, we are asked to classify them either in Politics or Sports category (Binary Classification). 
The data is given in a form of `comma separated values (CSV)` file. 
After the classification process is done the resulting data must be stored in another csv file. 
All the tweets must be labeled according to their class (Sports or Politics).<p>

# Data preparation 

Before feeding tweets data to the algorithm to be processed, a first elementary preprocessing is necessary. 
The tweets text should be represented in a numeric form. 
This step is referred as features extraction. 
Since we decided to use Bayes model, then we have to represent the tweets as a distribution of probabilities, 
statistically speaking for each unique word present in the tweets we calculate the frequency in which it appears in all the data (global probability) and in a specific given label. 
That is what the training data is all about, it will inform us about each word frequency in a given tweet and the probability for which these words might appear in either ‘Politics’ or ‘Sports’ categories. 

For instance: 
In a matrix of (word, probability) pair we perform the following 
Let say we have the word “player”, then we will fetch all tweets to count how many times this word appeared in the data (global frequency), then we also count how many times it appeared in ‘Politics’ and ‘Sports’ labeled tweets. 
Say word appears 180 times in all the data, 147 occurrences in ‘Sports’ and 33 in ‘Politics’. The global probability would be then 180 divided by the total number of unique words. And the probability that ‘player’ appears in ‘Sports’ for example is 147 / 180 = 0.8 which is too high than in ‘Politics’ 33 / 180 = 0.1 
So, the tweet in which it could appear will most likely be labeled as ‘Sports’ tweet... 
By analogy we proceed all the tweets dataset. 
The uniqueness of words comes into action for performance sake, because the elimination of redundance is so important to save computation time. 

# Model training

By now we have the numeric version of the data in a form of matrices 
Time for training the model using the naïve Bayes approach.
## Preview of the training data
<a href="">
  <img src="./assets/training-preview.png"/>
</a>
## Approach in brief words
We assume that the event of word being in ‘Politics’ or ‘Sports’ categories are independent. In fact, this is intuitive in our case. 
The probability that a given tweet is under ‘Politics’ is given by multiplying all the probability that each and every word in tweet might be in ’Politics’, this last information is calculated based on the training data. Same thing for ‘Sports’ probability. 
The decision is made by taking the highest probability. 
