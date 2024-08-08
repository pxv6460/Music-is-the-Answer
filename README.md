# Project-1-group-
Step 1: Download data from the GPR Inex and parse to get data for the last 3 years

Step 2: Write a function to pull in the top 100 weekly billboard titles for the last 3 years

Step 3: Access the spotify API to get the Spotify classificaitons for the above list of Billboard songs

Step 4: Use existing Spotify variables to plot the sentiment 	&#9785;

audio_features


* acousticness number [float]  A confidence measure from 0.0 to 1.0 of whether the track is acoustic. 1.0 represents high confidence the track is acoustic. 
* danceability number [float]  Danceability describes how suitable a track is for dancing based on a combination of musical elements including tempo, rhythm stability, beat strength, and overall regularity. A value of 0.0 is least danceable and 1.0 is most danceable.  
* duration_ms integer  The duration of the track in milliseconds.  
* energy number [float]  Energy is a measure from 0.0 to 1.0 and represents a perceptual measure of intensity and activity. Typically, energetic tracks feel fast, loud, and noisy. For example, death metal has high energy, while a Bach prelude scores low on the scale. Perceptual features contributing to this attribute include dynamic range, perceived loudness, timbre, onset rate, and general entropy.  
* instrumentalness number [float]  Predicts whether a track contains no vocals. "Ooh" and "aah" sounds are treated as instrumental in this context. Rap or spoken word tracks are clearly "vocal". The closer the instrumentalness value is to 1.0, the greater likelihood the track contains no vocal content. Values above 0.5 are intended to represent instrumental tracks, but confidence is higher as the value approaches 1.0.  
* key integer  The key the track is in. Integers map to pitches using standard Pitch Class notation. E.g. 0 = C, 1 = C♯/D♭, 2 = D, and so on. If no key was detected, the value is -1. Range: -1 - 11  
* liveness number [float]  Detects the presence of an audience in the recording. Higher liveness values represent an increased probability that the track was performed live. A value above 0.8 provides strong likelihood that the track is live.  
* loudness number [float]  The overall loudness of a track in decibels (dB). Loudness values are averaged across the entire track and are useful for comparing relative loudness of tracks. Loudness is the quality of a sound that is the primary psychological correlate of physical strength (amplitude). Values typically range between -60 and 0 db. 
* mode integer  Mode indicates the modality (major or minor) of a track, the type of scale from which its melodic content is derived. Major is represented by 1 and minor is 0. 
* speechiness number [float]  Speechiness detects the presence of spoken words in a track. The more exclusively speech-like the recording (e.g. talk show, audio book, poetry), the closer to 1.0 the attribute value. Values above 0.66 describe tracks that are probably made entirely of spoken words. Values between 0.33 and 0.66 describe tracks that may contain both music and speech, either in sections or layered, including such cases as rap music. Values below 0.33 most likely represent music and other non-speech-like tracks.  
* tempo number [float]  The overall estimated tempo of a track in beats per minute (BPM). In musical terminology, tempo is the speed or pace of a given piece and derives directly from the average beat duration.  
* time_signature integer  An estimated time signature. The time signature (meter) is a notational convention to specify how many beats are in each bar (or measure). The time signature ranges from 3 to 7 indicating time signatures of "3/4", to "7/4" Range: 3 - 7  
* valence number [float]  A measure from 0.0 to 1.0 describing the musical positiveness conveyed by a track. Tracks with high valence sound more positive (e.g. happy, cheerful, euphoric), while tracks with low valence sound more negative (e.g. sad, depressed, angry). Range: 0 - 1 


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
