# Google Cloud Vision API - Use Case for Detecting Text within an Image

## Objective
To illustrate the steps and code required to use the Google Cloud Vision API for text detection within an image. This code can be extended for practical applications for all OCR related machine learning use cases where the objective is to extract text information from any file format.

**Sample Use Case:**
Pulp Fiction is one of my favourite movies and Uma Thurman one of my favourite actresses

![Pulp Fiction Movie Poster](https://user-images.githubusercontent.com/36125669/114271781-c4cb2280-9a45-11eb-8e4f-50f5a7cf5bd6.jpg)

**Objective**
1. Identify all text information in the poster
2. Highlight the name 'UMA' with a bounded box

## Prerequisites
Steps 1 and 2 are prerequisites to sign-up for the Google Cloud Platform and enable the Vision API.

## Step 1 - Sign-up for the Google Cloud Platform
The [Google Cloud Platofarm](https://cloud.google.com/free/?utm_source=google&utm_medium=cpc&utm_campaign=japac-HK-all-en-dr-bkws-all-all-trial-e-dr-1009882&utm_content=text-ad-none-none-DEV_c-CRE_255875986060-ADGP_Hybrid%20%7C%20BKWS%20-%20EXA%20%7C%20Txt%20~%20GCP%20~%20Trial_cloud%20-%20create%20account-KWID_43700007271914961-kwd-58031179117&userloc_9069537-network_g&utm_term=KW_create%20a%20google%20cloud%20account&gclid=EAIaIQobChMIi7SosOHy7wIV7dVMAh0OeQfNEAAYASAAEgLP_fD_BwE&gclsrc=aw.ds) has a simple sign-up process that allows access to the free-tier for many of their key products - including the Vision API.

<img width="1440" alt="GCP Sign-Up" src="https://user-images.githubusercontent.com/36125669/114258161-42b40d00-99f7-11eb-98ab-e2ee2623ef85.png">

![GCP Services](https://user-images.githubusercontent.com/36125669/114258231-b6561a00-99f7-11eb-8d4a-4fb010eaf9b8.png)

## Step 2 - Enable to Google Cloud Vision API

Google has a step by step set up [documentation](https://cloud.google.com/vision/docs/before-you-begin) that may be used to enable the Vision API via a new project that will grant a new user access keys via a downloadable json file to be used in the code that follows.

A more detailed step by step process can be found [here](https://daminion.net/docs/topics/auto-tagging/how-to-get-google-cloud-vision-api-key/)

The primary output from this step will be the JSON file with your credentials to access the Vision API during the project.

****Note on Cost:**** The first 1000 units are free with a small incremental post that usage. Details [here](https://cloud.google.com/vision/pricing)
![Vision API Cost](https://user-images.githubusercontent.com/36125669/114270756-b4fd0f80-9a40-11eb-90ea-7c288d310580.jpeg)

## Step 3 - Ena








