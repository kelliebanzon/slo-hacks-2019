# Crossfader
Smoothly transition between every song on your Spotify playlist. Created at SLO Hacks 2019. 

## The Song Sorting Problem
Artists create albums to share a cohesive set of songs that tell a story. Often an album is sorted to flow a certain way to create a certain effect. We learned about how the pros sort songs here: [That's an Order! | 
How to create a dynamic and engaging song order for your album or EP](https://en.audiofanzine.com/getting-started/editorial/articles/that-s-an-order.html). 

Consumers, on the other hand, often create playlists with a _greater variety_ of songs because we cherry pick and add incrementally. This practice leaves many playlists with a lack of cohesion between tracks. Here's a neat tool we stumbled across to help amateurs mimic the pros: [Organize Your Music | sort and filter songs by mood, popularity, genre](http://organizeyourmusic.playlistmachinery.com)

## Goal 
Give us a Spotify playlist. We'll order the songs so each one flows into the next, then hand the playlist back to you.

## Approach 
### 1. Data Collection: Create a database of paired songs with a cohesion rating

We started by manually pairing songs and rating them ourselves, but then decided to crowdsource the effort by creating a Google Form. During the hackathon, we were able to collect 150+ responses.

**Cohesion Rating**: how well Track 1 transitions into Track 2

0.0 - _No cohesion at all_

* e.g. “Honey, I’m Good” by Andy Grammer ➡️ ”The A Team” by Ed Sheeran
  
0.5 - _Flow_: Track 1 leads smoothly into Track 2, but it was not specifically designed to do so

* e.g. “Bad Blood” by Taylor Swift ➡️ “Hands to Myself” by Selena Gomez

1.0 - _Bleed_: Track 1 leads smoothly into Track 2, because it was specifically designed to do so

* e.g.  “Intro” by ODESZA ➡️ “A Moment Apart” by ODESZA 

### 2. Feature Expansion: Spotify API
We used the Spotify API to pull the following data for each song and fed that data into our model. 

_Genres_: the genres that an artist is associated with (note: Spotify only classifies artists into genres, not individual songs)

_Features_: information/tags that describes the song as whole  (i.e. danceability, acousticness, speechiness, tempo, key, time signature, etc.)

_Analysis_: low-level audio analysis (precise rhythm, pitch and timbre information) sampled throughout the song

### 3. Model and Results
Originally we set out to use AutoML from Google Cloud to create a machine learning model that would sort the playlists, but we ran out of time. Instead, we created a simpler model using `scikit-learn` that predicts the cohesion rating. We went through three iterations:

1. Linear Regression: did not support non-binary output which forced us to switch all 0.5 ratings to 1.0. This simplification resulted in a low accuracy of 36.3% percent.

2. Linear SVC: this model's support for categorical output allowed us to maintain the original rating system (0.0, 0.5 and 1.0) and achieve 55.4% accuracy. 

3. SVC: 47.9% accuracy 

The third model, SVC, produced the highest valid accuracy because it was the only model where we split the data into a training and testing set. Although we are happy this model could predict whether two songs have cohesion at a rate better than random chance (note: random chance is 33.33% in this case because a song has either 0.0, 0.5 or 1.0 on our cohesion scale), this model is only the beginning of a proof of concept. Manual sorting will continue for now, but, in the future, with a larger training dataset, playlists could become more cohesive in a single click.

## Contributors
- [Kellie Banzon](http://github.com/kelliebanzon/)
- [Tanner Larson](https://github.com/tlarson07/)
- [Owais Sarfarz](https://github.com/oats-meal)

Special thanks to friends and family who submitted tracks for our dataset :) 
