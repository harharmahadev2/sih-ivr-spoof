# SPOOFex
Project Description: System for Identification of System-Generated, Blank & Spoof Calls Landing at Dial 100 Police Control Room

Introduction:
The "System for Identification of System-Generated, Blank & Spoof Calls Landing at Dial 100 Police Control Room" is a Python-based Flask application designed to address the issue of identifying and classifying incoming calls received at the Dial 100 Police Control Room. The application leverages the Twilio Client API to fetch client details and receive calls on a US-based trial number offered by Twilio. To make the application accessible, ngrok, a cross-platform application, is used to expose the local development server to the internet and divert incoming call traffic to it.

Functionality Overview:

Call Verification: Before a call is connected, the system verifies if the caller's number is a legitimate Indian number using regular expressions. Additionally, the system checks if the number is listed in the live spam database using the "spam_lookup" function. If the number is found in the spamlist, the IVRS disconnects the call immediately.

Call Recording and Transcription: Once the call is connected, Twilio establishes a WebSocket connection to the application's endpoint. The Interactive Voice Response System (IVRS) prompts the caller to speak about their problem within a time limit of approximately 20 seconds. The application uses a while loop to read and decode each message received from Twilio into a Python dictionary. The audio data received from Twilio, encoded in a foreign mu-law format, is decoded using the "audioop" library into a 16-bit uncompressed format. The audio is then converted to the required format for the vosk speech recognition engine to generate a transcript.

Blank Call Detection: If the generated transcript has zero length, indicating no spoken content, the system identifies the call as a blank call and disconnects it.

Call Classification: The generated transcript is further processed by different models, such as the Multinomial Naive Bayes classifier, and subjected to sentiment analysis. Based on the results, the call is classified into various categories, including Spam Call, Emergency Call, Inquiry Related, or Complaint.

User Input and Routing: Simultaneously, the caller is asked to enter a single-digit input to indicate the nature of their call, such as 1 for Emergency, 2 for Inquiry, and 3 for Complaint. The application maps the user's input with the model's prediction, and based on the final result, routes the call to the respective department. If a call is identified as spam, the system allows the police to add the number to the spamlist.

Database Storage: All relevant call data, including phone number, transcript, user input, time, and model prediction, is stored in a live PostgreSQL database.

Web Interface:
The front webpage of the application displays key information, such as the model's prediction, user input, the department to which the call is forwarded, and the phone number. The interface also provides additional features, including instructions for the operator and an "Add to Spam" button.

Installation and Deployment:
To deploy the application, follow these steps:

Install the required dependencies listed in the project's requirements.txt file.
Configure the Twilio Client API and obtain a US-based trial number.
Set up ngrok to expose the local development server to the internet.
Deploy the Flask application using a suitable web server (e.g., gunicorn).
Set up a PostgreSQL database and configure the application to connect to it.
Update the application's configuration files with the necessary credentials and settings.
Run the application and verify its functionality.

# Flowchart
![3](https://user-images.githubusercontent.com/87855947/188958305-472ffee6-c25a-4936-b052-ba9e32316b15.jpg)

# Technologies Used
![4](https://user-images.githubusercontent.com/87855947/188959322-e69e07d8-1e05-4f42-9ad1-f59de58c7925.jpg)



