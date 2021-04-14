# Google Cloud Vision API - Use Case for Detecting Text within an Image

## Background
To illustrate the steps and code required to use the Google Cloud Vision API for text detection within an image. This code can be extended for practical applications for all OCR related machine learning use cases where the objective is to extract text information from any file format.

**Sample Use Case:**
Pulp Fiction is one of my favourite movies and Uma Thurman one of my favourite actresses

![Pulp Fiction Movie Poster](https://user-images.githubusercontent.com/36125669/114271781-c4cb2280-9a45-11eb-8e4f-50f5a7cf5bd6.jpg)

**Objectives**
1. Identify all text information in the poster
2. Highlight the name 'UMA' with a bounded box

### Prerequisites
Steps 1 and 2 are prerequisites to sign-up for the Google Cloud Platform and enable the Vision API.

#### Step 1 - Sign-up for the Google Cloud Platform
The [Google Cloud Platofarm](https://cloud.google.com/free/?utm_source=google&utm_medium=cpc&utm_campaign=japac-HK-all-en-dr-bkws-all-all-trial-e-dr-1009882&utm_content=text-ad-none-none-DEV_c-CRE_255875986060-ADGP_Hybrid%20%7C%20BKWS%20-%20EXA%20%7C%20Txt%20~%20GCP%20~%20Trial_cloud%20-%20create%20account-KWID_43700007271914961-kwd-58031179117&userloc_9069537-network_g&utm_term=KW_create%20a%20google%20cloud%20account&gclid=EAIaIQobChMIi7SosOHy7wIV7dVMAh0OeQfNEAAYASAAEgLP_fD_BwE&gclsrc=aw.ds) has a simple sign-up process that allows access to the free-tier for many of their key products - including the Vision API.

<img width="1440" alt="GCP Sign-Up" src="https://user-images.githubusercontent.com/36125669/114258161-42b40d00-99f7-11eb-98ab-e2ee2623ef85.png">

![GCP Services](https://user-images.githubusercontent.com/36125669/114258231-b6561a00-99f7-11eb-8d4a-4fb010eaf9b8.png)

#### Step 2 - Enable the Google Cloud Vision API

Google has a step by step set up [documentation](https://cloud.google.com/vision/docs/before-you-begin) that may be used to enable the Vision API via a new project that will grant a user access keys via a downloadable json file to be used in the code that follows.

A more detailed step by step process can be found [here](https://daminion.net/docs/topics/auto-tagging/how-to-get-google-cloud-vision-api-key/)

The primary output from this step will be the JSON file with your credentials to access the Vision API during the project.

****Note on Cost:**** The first 1000 units are free with a small incremental charge post. Details [here](https://cloud.google.com/vision/pricing)
![Vision API Cost](https://user-images.githubusercontent.com/36125669/114270756-b4fd0f80-9a40-11eb-90ea-7c288d310580.jpeg)

#### Step 3 - Import all the important libraries for this project

```
import cv2
import imutils
import json
import matplotlib.pyplot as plt
import numpy as np
import os
import io
import pandas as pd
import requests
import time
from base64 import b64encode
from IPython.display import Image
from google.cloud import vision
from google.cloud.vision import AnnotateFileRequest
from google.protobuf.json_format import MessageToDict
```

#### Step 4 - Import GCP credentials from the JSON document downloaded

Please provide the path where your JSON document is located /drive

```
import os
os.environ["GOOGLE_APPLICATION_CREDENTIALS"]="GCP - Vision API JSON.json"
```

#### Step 5 - Import the image from which you want to extract text

```
import io

path = 'Pulp Fiction Movie Poster.jpg' #Input image path here
with io.open(path, 'rb') as image_file:
        content = image_file.read()
```

#### Step 6 - # Map Vision API

```
image = vision.Image(content=content)
```
```
client = vision.ImageAnnotatorClient()
```

#### Step 7 - Call Vision API

```
response = client.text_detection(image=image)
texts = response.text_annotations
serializable_tags = [MessageToDict(tag._pb) for tag in texts]
```

## Output 1 - An extract of all the text within the image

```
print(serializable_tags[0]["description"])
```
(WINNER-BEST PICTURE-1994 CANNES FILM FESTIVAL
PULP FICTION
a Quentin Tanantino film
10
Lawence Bender
JOHN TRAVOLTA
SAMUEL L. JACKSON
UMA THURMAN
HARVEY KEITEL
TIM ROTH
AMANDA PLUMMER
MARIA de MEDEIROS
VING RHAMES
ERIC STOLTZ
ROSANNA ARQUETTE
CHRISTOPHER WALKEN
and
BRUCE WILLIS
wo
uh lorida-
E ANY ENCE OANI RAE AN E MOA A
DENN AMANT
SAOY
MECA R
MIRAMAX

#### Step 8 - Build the bounded box around the word 'UMA'

```
def gen_cord(serializable_tags):
  cord_df = pd.DataFrame(serializable_tags['boundingPoly']['vertices'])
  x_min, y_min = np.min(cord_df["x"]), np.min(cord_df["y"])
  x_max, y_max = np.max(cord_df["x"]), np.max(cord_df["y"])
  return serializable_tags["description"], x_max, x_min, y_max, y_min
```

## Output 2 - Highligh the name 'UMA'
'UMA' is the 20th word in the image

```
text, x_max, x_min, y_max, y_min = gen_cord(serializable_tags[20]) #Change variable here for word extract required
image = cv2.imread(path)
cv2.rectangle(image,(x_min,y_min),(x_max,y_max),(0,255, 0),2)
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
print ("Text Detected = {}".format(text))
```
![Screenshot 2021-04-10 at 9 46 25 PM](https://user-images.githubusercontent.com/36125669/114273610-538f6d80-9a4d-11eb-815b-071f843a33f6.jpeg)


## Author
Neil Shastry

## Acknowledgments

[@bhaveshbhatt91](https://github.com/bhattbhavesh91?tab=overview&from=2021-03-01&to=2021-03-31) for the great [youtube video](https://www.youtube.com/watch?v=tOVjjo8VJTs) inspiration.
