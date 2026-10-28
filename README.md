# Sign to Speech

A browser-based tool that recognizes fingerspelled hand signs through a webcam, builds them into words and sentences, and reads them aloud.

Built for **Vision Hack** (Saviskar 2026, CGC University Mohali) under the **Gesture Recognition** theme, using Google Teachable Machine (Image Project).

## Why this project

Many deaf and hard-of-hearing people communicate with signs, but most people around them do not understand sign language. Sign to Speech is a small step toward closing that gap: show a sign to the camera, and the page speaks it.

This is a fingerspelling demo, not a full sign language translator. Sign languages are complete languages with grammar, movement, and facial expression. This project covers still hand shapes only.

## Features

- **Live webcam recognition** of hand signs using a Teachable Machine model running in the browser (TensorFlow.js).
- **Hold-to-confirm:** a sign is added only after it stays steady above a confidence threshold for about one second, which prevents flicker and accidental letters.
- **"Nothing" class:** the model learns what an empty or resting hand looks like, so it does not invent letters.
- **Sentence builder** with Space, Backspace, and Clear controls.
- **Word suggestions:** as letters accumulate, the page offers matching words to complete, which speeds up spelling and covers letters the model finds hard.
- **Text to speech** using the browser's built-in speech feature.
- **Upload mode** for testing the model on individual unseen images.

## How it works

1. A webcam frame is passed to the trained model.
2. The model returns a probability for each class.
3. If the top class is a sign (not "Nothing") and stays above the confidence threshold for the hold time, it is added to the sentence.
4. Letters join into words, and whole-word classes (such as "help") are added as words.
5. The Speak button reads the sentence aloud.

## Model and dataset

- **Tool:** Google Teachable Machine, Image Project
- **Classes:** 30 in total: Letters A to Z, "help", "yes", "no" and "nothing"
- **Images per class:** **[number]**
- **Data collected from:** **[number]** me using both hands in varied lighting and distance

## Run it

1. Open `sign-to-speech-demo.html` in a text editor.
2. At the top of the script, set `MODEL_URL` to your exported Teachable Machine model link (keep the trailing `/`):

   ```js
   MODEL_URL: "https://teachablemachine.withgoogle.com/models/RahShiq3S/"
   ```

3. Open the file in **Google Chrome** and allow camera access.

**Using downloaded model files instead of a link:** place `model.json`, `metadata.json`, and the weights files in a folder (for example `my_model/`), set `MODEL_URL: "./my_model/"`, then run this in the project folder and open the address it prints:

```bash
python -m http.server
```

An internet connection is required to load the TensorFlow.js libraries.

## Settings you can change

All settings are in the `CONFIG` block at the top of the script.

| Setting | What it does |
| --- | --- |
| `MODEL_URL` | Location of the trained model |
| `CONFIDENCE` | Minimum confidence for a sign to count (default 0.8) |
| `HOLD_MS` | How long a sign must be held (default 1000 ms) |
| `NONE_CLASSES` | Class names treated as "no sign" |
| `WORD_LIST` | Words offered as suggestions |
| `SPEECH_LANG` | Voice language, such as `en-IN` or `en-US` |
| `WEBCAM_FLIP` | Mirrors the webcam image |

## Limitations

- Recognizes **still hand shapes only**. Signs that need movement (such as J and Z in ASL) cannot be detected from a single image.
- Look-alike fist shapes can be confused with each other.
- Accuracy depends on lighting, background, and hand position. The model was trained on a limited number of people.
- Text to speech depends on the voices available in the user's browser.

## Future work

- Detect movement-based signs using a video or sequence model.
- Support whole-word signs in Indian Sign Language.
- Train on a larger and more diverse group of signers.
- Package the tool as a mobile app.

## Team

MARS - Richa Roy

## Credits

- [Google Teachable Machine](https://teachablemachine.withgoogle.com/)
- TensorFlow.js and the Teachable Machine image library
- Most images were collected by me.
- Used images from kaggle dataset- "<https://teachablemachine.withgoogle.com/models/RahShiq3S/>"
