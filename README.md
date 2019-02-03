# Crossfader
Smoothly transition between every song on your Spotify playlist. Created at SLO Hacks 2019. 

## The Song Sorting Problem
Artists create albums to share a cohesive set of songs that tell a story. Often an album is sorted with popular high energy songs at top. We learned about how the pros sort songs here: [That's an Order! | 
How to create a dynamic and engaging song order for your album or EP](https://en.audiofanzine.com/getting-started/editorial/articles/that-s-an-order.html). 

Consumers often create playlists with a _greater variety_ of tracks because we cherry pick and add incrementally. This leaves many playlist with a lack of cohesion between tracks. A neat tool we stumbled across: [Organize Your Music | sort and filter songs by mood, popularity, genre](http://organizeyourmusic.playlistmachinery.com)

## Goal 
Give us a playlist. We'll order the songs so each one flows into the next, then hand the playlist back to you.

## Approach 
### 1. Data Collect: Create a database of paired songs with a cohesion rating

We started by manuelly pairing songs and rating them ourselves, but then decided to crowdsource the effort by creating a Google Form. During the hackathon we were able to collect 150+ responses.

**Cohesion Rating**: how well track 1 transitions to track 2

0.0 - _No cohesion at all_

* e.g. “Honey, I’m Good” by Andy Grammer ➡️”The A Team” by Ed Sheeran
  
0.5 - _Flow_: track 1 leads smoothly into track 2, but it was not specifically designed to do so

* e.g. “Bad Blood” by Taylor Swift  ➡️“Hands to Myself” by Selena Gomez

1.0 - _Bleed_: track 1 leads smoothly into track 2, because it was specifically designed to do so

* e.g.  “Intro” by ODESZA ➡️“A Moment Apart” by ODESZA 

### 2. Feature Expansion: Spotify API
_Genres_: describe an artist, not an individual songs

_Features_: information/tags that describes the song as whole  (danceability, acousticness, speechiness, tempo, key, time signature, etc.)

_Analysis_: low level analysis (precise rhythm, pitch and timbre information) sampled throughout the song

### 3. Model and Results
We ran out of time, so we created a model that predicts the cohesion rating. 

a. Linear Regression: did not support non-binary output which forced us to switch all 0.5 ratings to 1.0. This resulted in a low accuracy of 36.3% percent.

b. Linear SVC: support for catagorical output allowed us to maintain the original rating system (0.0, 0.5 and 1.0) and achieve 55.4% accuracy. 

c. SVC: 47.9% accuracy 

The third model, SVC, produced the highest valid accuracy because it was the only model where we split the data into a training and testing set. Although, we are happy this model could predict whether a two songs have cohension better than random chance, this is start of proof of concept. Manuel sorting will continue, but with more data in the future playlists could become more cohesive in a single click.


## Contributors
- [Kellie Banzon](http://github.com/kelliebanzon/)
- [Tanner Larson](https://github.com/tlarson07/)
- Owais Sarfarz

Special thanks to friends and family who submitted tracks for our dataset :) 
