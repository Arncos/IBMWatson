The IBM® Speech to Text service provides an API that enables you to add IBM's speech recognition capabilities to your applications.
The service transcribes speech from various languages and audio formats to text with low latency.
For most languages, the service supports two sampling rates, broadband and narrowband.

Demo:
https://speech-to-text-demo.ng.bluemix.net
Full Documentation:
https://www.ibm.com/watson/developercloud/speech-to-text/api/v1/#introduction
 
HTTP API endpoint:
https://stream.watsonplatform.net/speech-to-text/api 
Credentials:
To run any code, you will need a `username`, `password`, and `url`. To get your service credentials, follow these steps:
 1. Log in to IBM Cloud at https://console.bluemix.net.
 
 1. Create an instance of the service:
     1. In the IBM Cloud **Catalog**, select the service you want.
     1. Click **Create**.
 
 1. Copy your credentials:
     1. On the left side of the page, click **Service Credentials** to view your service credentials.
     1. Copy `username`, `password`, and `url` from these service credentials.
JSON Request:

method='POST'
url='/v1/recognize'

Content-Type	The audio format (MIME type) of the audio:
audio/basic (Use only with narrowband models.)
audio/flac
audio/l16 
audio/mp3
audio/mpeg
audio/mulaw (Specify the sampling rate of the audio.)
audio/ogg (The service automatically detects the codec of the input audio.)
audio/ogg;codecs=opus
audio/ogg;codecs=vorbis
audio/wav (Provide audio with a maximum of nine channels.)
audio/webm (The service automatically detects the codec of the input audio.)
audio/webm;codecs=opus
audio/webm;codecs=vorbis
 
Library:
pip install --upgrade watson-developer-cloud
from __future__ import print_function
import json
from os.path import join, dirname
from watson_developer_cloud import SpeechToTextV1
 
speech_to_text = SpeechToTextV1(
    username='d1a08efb-e1ba-4503-bc73-354c27e3dcb7',
    password='PRGxV2o4CIQs',
    x_watson_learning_opt_out=False)
 
#print(json.dumps(speech_to_text.models(), indent=2))
#print(json.dumps(speech_to_text.get_model('en-US_BroadbandModel'), indent=2))
 
with open(join(dirname(__file__), '../resources/speech.wav'),'rb') as audio_file:
    print(json.dumps(speech_to_text.recognize(
        audio_file, content_type='audio/wav', timestamps=False,
        word_confidence=False),
                     indent=2))