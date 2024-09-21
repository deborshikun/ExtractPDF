# PDF Data Checker
### We want to create a data extractor and checker from PDF with a local database (mostly Excel in this case).
-------------------------------------------------

## ExtractPDF
#### Trying to Extract Data from not-so-perfect PDFs

## About
#### A little project dealing with information retrieval from PDF documents.
For the time being, I am only dealing with a single pdf at a time, eventually using this model for a batch procedure. I will upload all the major iteration changes I go through!
My actual motive is to be able to extract marks from mark sheets taken by students. These mark sheets might be taken in various orientations and could involve many real-world problems.

## Installation 
#### 1. Dependencies
Install Dependencies using 
```pip install -r Dependencies.txt```

#### 2. Download Tesseract OCR 
Use the *https://github.com/tesseract-ocr/tesseract/releases* repository (You will need it LOCALLY on your system for OCR).
You can get the Windows Installer from *https://github.com/UB-Mannheim/tesseract/wiki* directly.

#### 3. PATH
Enter the path to your pdf in ```pdf_path``` in the declaration outside.
Add your Tesseract location to your PATH, or add your Tesseract PATH implicitly in the declared field.

-------------------------------------------------

#### Even with all this, I had trouble finding meaningful output using Tesseract OCR. 
An error I received a lot was ```Error during OSD detection: (1, 'Estimating resolution as 346 <could be any number here between ranges 0 to 400 according to my observations> Warning. Invalid resolution 0 dpi. Using 70```
I only found 1 solution to the issue, which is more like a "bypass" rather than a cure. Thanks to Esraa anyhow!

![image](https://github.com/user-attachments/assets/69b335cf-f524-4ca4-8b36-802ca6291acc)

Let me share a sample input and output of one such case:

Input:

![image](https://github.com/user-attachments/assets/c23b91af-1404-42a1-9dd4-f08ee3280600)  

Output:

![image](https://github.com/user-attachments/assets/dd1677cf-e5ba-46cf-b687-3b3f9f682a40)

Not too great right?

#### 4. Groq
Now before I started the project, I was convinced I could (obviously with the help of Github and Stackoverflow) get the PDF OCR running after using Tesseract. 
I couldn't have possibly been more incorrect.
Someone suggested I try using AI, and well API keys don't come cheap. 

In comes Groq. I stumbled across a Reddit thread that convinced me to use Groq, and so I did.
You can read the documentation at *https://console.groq.com/docs/quickstart* directly.

You need to run ```export GROQ_API_KEY=<your-api-key-here>``` on your terminal of choice. Use ```set``` instead of ```export``` if you are on CMD. 
I'd suggest using ```$env:GROQ_API_KEY="<your_api_key>"``` because this worked for me.

![image](https://github.com/user-attachments/assets/889e8a6c-f621-480f-8270-0157384a1af6)

Many thanks to artworkjpm!

The main purpose of Groq is to use llama for any correction of the bad output from Tesseract OCR. 
This is where I hit a brick wall, as even with Groq the error bound was quite substantial. 

I had to change my approach to the OCR itself.

#### 5. Google Cloud Vision API
The strongest tool available to us - Google Cloud Vision API. This is famously used in image detection, mainly in Google Lens. So I had to give it a shot.
as always, you can read the documentation and the guides over at *https://cloud.google.com/vision/docs/how-to*.

Just like Groq, you need to set an environment variable ```GOOGLE_APPLICATION_CREDENTIALS``` . You can refer to ```Point 4```, or just simply use ```$env:GOOGLE_APPLICATION_CREDENTIALS="<your_api_key>"```.
You also need to create an "Application Credential Secret Key" from Google Cloud, which will authenticate your use of the API. This is going to be a .json download. You will have to specify the .json path in the ```credentials``` section of the code.

Now with the help of both llama3-8b and Vision AI, let me share a sample IO:

Input:

![image](https://github.com/user-attachments/assets/28edf135-52b1-4e64-aa37-1ab1ce84a2a4)

Output:

![image](https://github.com/user-attachments/assets/e21cdfd2-2b78-4811-9f2a-6343332d74f2)

#### That is almost Perfection! Now I just need to tweak the prompt a bit for Groq and we are golden!

With this, I conclude the "ExtractPDF" portion.

-------------------------------------------------

# Excel Data Extraction
### We want to create a data extractor  from Excel.
-------------------------------------------------

## About
#### A little project dealing with information retrieval from Excel documents.
For the time being, I am only dealing with a single txt file at a time, eventually using this model for a batch procedure. I will upload all the major iteration changes I go through!
My actual motive is to be able to extract marks from mark sheets from the database. These marks will be matched with the marksheet's marks provided as PDF 

## Installation 
#### 1. Dependencies
Install Pandas and openpyxl using 
```pip install pandas openpyxl ```

#### 2. PATH
Enter the path to your excel file in ```excel_file_path``` in the declaration outside.

-------------------------------------------------

## Checker Part will be updated soon.
## Extract_from_Output
# Read Student Marks from a File

This Python project contains a function named `read` that reads a student's information, including their name, UID, and subject marks, from a text file. It extracts this information using regular expressions and removes the first subject's marks from the list before printing the updated results.

## Features
- Extracts student name and UID from the file.
- Extracts subject names and marks.
- Removes the first element (subject mark) from the marks list.
- Outputs the updated marks list.

## Function Definition

```python
def read(file_path):
 # Reads the file content and processes it to extract the student's name, UID, and subject marks.
## Requirements

-


