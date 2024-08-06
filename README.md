# Project-1-group-
Step 1: Download data from the GPR Inex and parse to get data for the last 3 years

Step 2: Write a function to pull in the top 100 weekly billboard titles for the last 3 years

Step 3: Access the spotify API to get the Spotify classificaitons for the above list of Billboard songs

Step 4: Use existing Spotify variables to plot the sentiment 	&#9785;

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
