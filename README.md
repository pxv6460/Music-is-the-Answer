## Project-1-Group-2

# The Impact of Global Events on Music Choice 
by
Niharika, Hazel, Azlan, Peter and Enrique
<br>
<br>
>EXECUTIVE SUMMARY

We wanted to investigate the correlations -if any- between key events in the US and abroad, and the music at the top of the weekly Billboard charts from January 2022 to August 2024. ***Do global events impact the mood of a nation?*** Can music tell us how?<br>
<br>
By fetching data from multiple sources including Billboard’s top charts, Spotify Web API, Geopolitical Risk Index, and Wikipedia, the team cleaned, transformed, analyzed, and plotted the data. Creating a ‘mood’ variable based on certain audio attributes for the 
top 10, then the top 3 songs over time, allowed us to question the data, visualize correlations, and hypothesized trends. 
<br>
<br>

![sources](/sources.png) 
>DATA EXTRACTION - 4 SOURCES

1. BILLBOARD - Top ten songs in the US from 01-01-2022 to 08-08-2024 (136 .csv files)
2. SPOTIFY FOR DEVELOPERS - Fetched 13 audio features for 205 unique songs performed by 132 artists over a period of 136 weeks
	A) acousticness [float]  A confidence measure from 0.0 to 1.0 of whether the track is acoustic
	B) danceability [float]  Danceability describes how suitable a track is for dancing.
	C) duration_ms  [integer]  The duration of the track in milliseconds. 
	D) energy  [float]  Energy is a measure from 0.0 to 1.0 and represents a perceptual measure of intensity and activity
	E) instrumentalness  [float]  Predicts whether a track contains no vocals. "Ooh" and "aah" sounds are treated as instrumental 
	F) key [ integer]  The key the track is in. Integers map to pitches using standard Pitch Class notation
	G) liveness [float]  Detects the presence of an audience in the recording
	H) loudness [float]  The overall loudness of a track in decibels (dB)
	I) mode [ integer]  Mode indicates the modality (major or minor) of a track
	J) speechines [float]  Speechiness detects the presence of spoken words in a track.
	K) tempo  [float]  The overall estimated tempo of a track in beats per minute (BPM)
	L) time_signature [ integer]  An estimated time signature (meter)
	M) valence  [float]  A measure from 0.0 to 1.0 describing the musical positiveness conveyed by a track
3. GEOPOLITICAL RISK (GPR) INDEX - A measure of adverse geopolitical events and associated risks based on a tally
of newspaper articles by Dario Caldara and Matteo Iacoviello. The sources utilized by the authors are the Chicago Tribune, the Daily Telegraph, the Financial Times, the Globe and Mail, The Guardian, the Los Angeles Times, The New York Times, the USA Today, The Wall Street Journal and The Washington Post
4. WIKIPEDIA - Fetched and tagged 143 events from wikipedia between 01-27-2022 and 08-06-2024
<br>
<br>

>DATA TRANSFORMATION

- A consolidated data frame was generated with all the audio features for 1360 entries needed for our analysis
- Mood Definition. Energy and valence is what we can use for mood. We added weights to the variables 60% energy, 40% valence
- GPR data was filtered for the US only
<br>
<br>

>DATA ANALYSIS

QUESTION #1
Who are the top ranking artists?

QUESTION #2
Are there positive or negative correlations amongst the attributes of top songs 

QUESTION #3
Is there a correlation between the attributes of a song and its ranking on the charts?

QUESTION #4
What is the ‘mood’ of top ranked songs over time?

QUESTION #5
Is there a direct relationship between the danceability of a top 3 song and the USA gpr based on events?

QUESTION #6
How does the standard deviation of the top 3 songs’ mood compares to the gpr in the USA?
<br>
<br>
>FINDINGS
>
We were able to arrive to some interesting conclusions, some expexted and some unexpected, for instance:
1) The music taste of the US becomes pretty homogeneous when a popular performer stays on the charts for a long time
2) There are correlations between mood and gpr - but the peaks are delayed (events happen first, music responds later)
3) We need to expand our data sourcing over other platforms to identify finer patterns
4) Unexpectedly, we found out that are there seasonal mood trends, for instance, in the US people don’t dance during the new year holiday season (danceability decreases dec-jan every year)
<br>
<br>

>HOWEVER...
Skews could play a bigger role. 
Spotify has 65 million active users in the USA compared to a total population of 259MM over the age of 18- hence Spotify represents ~25% of the adult population. Also, Spotify data skews younger  and more female than male. The mood index may have these inherent biases based on the data skews. Lastly, ‘Popular Artists’  and their planned release schedules could have a bigger influence on mood than global events 
<br>
<br>

>ULTIMATELY...
GPR and spotify ‘mood’ index are attempts to generalize the mood of the nation - both rely heavily on popular opinions, we need more data to strengthen the observations (Breakdown of results by city/ location? Local news sources/ events better indicator than global news)
<br>
<br>

>FUTURE DIRECTION
1) Add further localization
	Breaking down of results by city
	Include local, trustworthy news sources
	Ingest events as they’re happening

2) Increase the granular tagging on all events
	What kind of news impact musical preferences more than others?

3) Expand the data fetching to other countries not just the US
	Diversify the input by investigating music charts abroad
<br>
<br>
>FILES
Project_1.ipynb - contains the code
>
Billboard.csv - Billboard top 10 from from 01-01-2022 to 08-08-2024
<br>
Cleaned_gpr_data.csv - GPR Risk index data for the USA
<br>
events.csv - Wikipedia events
<br>

>LINK TO THE PRESENTATION:
https://docs.google.com/presentation/d/1oIsHPfcf-6mWqWqoU27XUqEV7HjkBl403m6gOW_c9dI/edit#slide=id.p1

