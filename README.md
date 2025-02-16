# LocateWise 🌍📸
**Smart Location & Contact Management with AI Integration**

![LocateWise Flowchart](![flowchart.png](..%2F..%2FDownloads%2FMy%20Web%20Projects%2Fflowchart.png))

![flowchart.png](..%2F..%2FDownloads%2FMy%20Web%20Projects%2Fflowchart.png)



## Overview 📖

LocateWise is a cross-platform mobile application built with Flutter, designed to simplify location management through camera capture, map visualization, and AI chatbot assistance.  
It allows users to quickly capture location details, explore them on a map, connect with relevant contacts, and interact with an AI chatbot for information and task automation.  
This README provides a comprehensive guide for developers looking to contribute to the project.

---

## Features ✨
1. **AI-Powered Image Analysis**
    - Extracts text (phone, email) from images using **Google ML Kit** or **Tesseract OCR**.
2. **Automatic Location Tagging**
    - Fetches GPS coordinates using device sensors.
3. **Interactive Map**
    - Displays saved locations with pins using Google Maps.
4. **Contact Actions**
    - One-tap calling and emailing from extracted details.
5. **Offline-First Design**
    - Uses HiveDB for local data storage.

---

## App Architecture 🏗️

### Flowchart

Start → Splash Screen → Camera → AI Processing → Store in DB → Map → Pin Tap → Details → Call/Email → End


---

## Tech Stack 🛠️

| Component     | Technology/Packages                                                                                                                 |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------|
| **Framework** | Flutter 3.6.2, Flutter: Cross-platform mobile development framework                                                                 |
| **AI**        | Rasa: Open-source framework for building conversational AI assistants (online or offline).                                          |
| **Maps**      | google_maps_flutter (v2.2.3), geolocator (v9.0.2), google_maps_flutter (Example):<br/>Map integration. mapbox_gl is another option. |
| **Database**  | HiveDB (v2.2.3)                                                                                                                     |
| **http**      | http (For API calls): For making HTTP requests to Rasa X or a custom backend.                                                       |
| **Camera**    | camera (v0.10.0+1)                                                                                                                  |
| **Utilities** | image_picker (v0.8.7+3), url_launcher (v6.1.9)                                                                                      |
---

## Setup Instructions ⚙️

### 1. Clone Repository
```bash
git clone https://github.com/yourusername/locatewise.git
cd locatewise

Add API Keys
Android (android/app/src/main/AndroidManifest.xml):

<meta-data
    android:name="com.google.android.geo.API_KEY"
    android:value="YOUR_GOOGLE_MAPS_API_KEY"/>

iOS (ios/Runner/AppDelegate.swift):

GMSServices.provideAPIKey("YOUR_GOOGLE_MAPS_API_KEY")

Install Dependencies
Add to pubspec.yaml:

dependencies:
  google_maps_flutter: ^2.2.3
  google_ml_kit: ^0.13.0
  hive: ^2.2.3
  geolocator: ^9.0.2
  camera: ^0.10.0+1

Then run:
flutter pub get

Database Schema 📦

@HiveType(typeId: 0)
class LocationData {
  @HiveField(0) final String id;
  @HiveField(1) final String imagePath;
  @HiveField(2) final double lat;
  @HiveField(3) final double lng;
  @HiveField(4) final String phone;
  @HiveField(5) final String email;
  @HiveField(6) final DateTime timestamp;
}

AI Processing Workflow 🤖

// services/ai_service.dart
Future<ContactData> processImage(File image) async {
  final textRecognizer = TextRecognizer();
  final RecognizedText text = await textRecognizer.processImage(image);
  
  return ContactData(
    phone: _extractPhone(text.text),
    email: _extractEmail(text.text),
  );
}

String _extractPhone(String text) {
  // Regex pattern for phone number extraction
  final regex = RegExp(r'(\+?\d{1,3}[- ]?)?\(?\d{3}\)?[- ]?\d{3}[- ]?\d{4}');
  return regex.firstMatch(text)?.group(0) ?? '';
}

Permissions 🔒
Add to android/app/src/main/AndroidManifest.xml:

<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.INTERNET" />

Set up Rasa:

Rasa Open Source (Offline):
Follow the Rasa installation guide: https://rasa.com/docs/rasa/installation
Set up a virtual environment (recommended): python3 -m venv .venv and activate it: source .venv/bin/activate
Install Rasa: pip install rasa
Train your Rasa model: rasa train
Run the Rasa server: rasa run
Configure rasa_service.dart to connect to the local Rasa server (usually http://localhost:5005).
Rasa X (Online):
Create a Rasa X account: https://rasa.com/rasa-x
Create a new project and train your model.
Obtain the Rasa X API endpoint and authentication credentials.
Configure rasa_service.dart to use the Rasa X API.

Usage Flow 📲
Take photo of business card/signage

AI auto-detects contact info

Confirm and save to local database

View location on interactive map

Tap pin → See details → Initiate call/email

Future Roadmap 🚀
Real-time object detection with TensorFlow Lite

Cloud sync via Firebase

Multi-language text recognition

Contact categorization using NLP

Contributing 🤝
1. **Clone the Repository:**
   ```bash
   git clone https://github.com/Abdi-Moha/locate_wise.git
   
 
2. Fork the repository

Create feature branch (git checkout -b feature/awesome-feature)

Commit changes (git commit -m 'Add awesome feature')

Push to branch (git push origin feature/awesome-feature)

Open Pull Request

Contributions are welcome! Please open an issue or submit a pull request.  Follow these guidelines:

Coding Style: Adhere to Flutter and Dart best practices.
Testing: Write unit and integration tests for your code.
Documentation: Update the README and other documentation as needed.


License: MIT
Version: 1.0.0
Maintainer: Abdirahman codemantechnologies.com

## **Contact**
For support or inquiries, contact:
- **Email**: codemantechnologies.com
- **Website**: https://www.linkedin.com/in/abdirahman-mohamed-08477b124/


This README provides comprehensive documentation for developers to set up, understand, and contribute to the project. Save this as `README.md` in your project root directory. Remember to:

1. Replace placeholder API keys
2. Add actual flowchart diagram
3. Update repository URLs
4. Add your contact information

High-Level Process Flow (Visualized)

+-------+     +------------+     +-----------------+     +-------------+
| Start | --> | Slash      | --> | Camera to       | --> | Store       |
|       |     | Screen     |     | take a picture  |     | details in  |
+-------+     +------------+     +-----------------+     +-------------+
                                      ^
                                      |
                                      +---------------------------------+
                                                                       |
                                                                       v
                                        +-----------------+     +-------+
                                        | Map Displaying  | --> | User  |
                                        | Locations       |     | Taps  |
                                        +-----------------+     | on    |
                                              ^           |     | Loc.  |
                                              |           |     | Pin   |
                                              |           |     +-------+
                                              |           |         ^
                                              |           |         |
                                              +-----------+---------+
                                                          |
                                                          v
                                        +-----------------+
                                        | Display Loc.,  |
                                        | Phone & Email  |
                                        +-----------------+
                                              |
                                              v
                                        +-----------------+
                                        | Initiate Call  |
                                        | or Email       |
                                        +-----------------+
                                              |
                                              v
                                        +-------+
                                        |  End  |
                                        +-------+