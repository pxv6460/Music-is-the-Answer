## Project-1-Group-2

#The Impact of Global Events on Music Choice 
by
Niharika, Hazel, Azlan, Peter and Enrique

##EXECUTIVE SUMMARY

We wanted to investigate the correlations -if any- between key events in the US and abroad, and the music at the top of the weekly Billboard charts from January 2022 to August 2024. Do global events impact the mood of a nation? Can music tell us how?
By fetching data from multiple sources including Billboard’s top charts, Spotify Web API, Geopolitical Risk Index, and Wikipedia, the team cleaned, transformed, analyzed, and plotted the data. Creating a ‘mood’ variable based on certain audio attributes for the 
top 10, then the top 3 songs over time, allowed us to question the data, visualize correlations, and hypothesized trends. 

##DATA EXTRACTION - 4 SOURCES

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

##DATA TRANSFORMATION

- A consolidated data frame was generated with all the audio features for 1360 entries needed for our analysis
- Mood Definition. Energy and valence is what we can use for mood. We added weights to the variables 60% energy, 40% valence
- GPR data was filtered for the US only

##DATA ANALYSIS

QUESTION #1
Who are the top ranking artists?
QUESTION #2
Are there positive or negative correlations amongst the attributes of top songs 
QUESTION #3
Is there a correlation between the attributes of a song and its ranking on the charts?





* Correlations between the features
* Positive Correlation:
	•	Energy and Loudness: The correlation is 0.632, indicating a strong positive correlation. As energy increases, loudness tends to increase as well.
	•	Valence and Energy: The correlation is 0.390, indicating a moderate positive correlation. As valence (positivity) increases, energy tends to increase.
	•	Negative Correlation:
	•	Danceability and Acousticness: The correlation is -0.352, indicating a moderate negative correlation. As danceability increases, acousticness tends to decrease.
	•	Tempo and Danceability: The correlation is -0.398, indicating a moderate negative correlation. As tempo increases, danceability tends to decrease.
	•	Weak or No Correlation:
	•	Loudness and Liveness: The correlation is approximately 0, indicating no linear relationship between these variables.
	•	Speechiness and Energy: The correlation is -0.005, indicating almost no linear relationship.


import requests
import base64

client_id = "3cdad55fbddf484aa218ad245bad2c7c"
client_secret = "853507ba61bb42e2aae13ed935b548e4"
credentials = f"{client_id}:{client_secret}"
base64_credentials = base64.b64encode(credentials.encode()).decode()

auth_options = {
    "headers": {
        "Authorization": f"Basic {base64_credentials}"
    },
    "data": {
        "grant_type": "client_credentials"
    }
}

response = requests.post("https://accounts.spotify.com/api/token", headers=auth_options["headers"], data=auth_options["data"])

access_token = response.json()["access_token"]

search_response = requests.get(
    f"https://api.spotify.com/v1/search",
    headers={
        "Authorization": f"Bearer {access_token}"
    },
    params={
        "q": "Espresso",
        "type": "track",
        "limit": 1
    }
)

song_id = search_response.json()["tracks"]["items"][0]["id"]

search_features = requests.get(
    f"https://api.spotify.com/v1/audio-features/2oADPwknKEfMtwpMnr7xfg",
    headers={
        "Authorization": f"Bearer {access_token}"
    }
)

search_features.json()


link to the presentation https://docs.google.com/presentation/d/1oIsHPfcf-6mWqWqoU27XUqEV7HjkBl403m6gOW_c9dI/edit#slide=id.g2f2fd5dbcc7_0_57

