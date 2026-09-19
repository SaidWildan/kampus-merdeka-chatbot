# KadekBot: Kampus Merdeka Chatbot

An intent-based chatbot that answers questions about Indonesia's **Kampus Merdeka** programs (Studi Independen, Magang, Kampus Mengajar, IISMA, Pertukaran Mahasiswa, and more). Built as the NLP deployment project of the **AI for Jobs (Kampus Merdeka / Orbit Future Academy) Batch 3** program in 2022.

## How it works

1. The user types a question in the chat interface.
2. The text is lowercased and stripped of punctuation, then converted to a padded token sequence with a fitted Keras tokenizer.
3. A TensorFlow/Keras neural network classifies the question into one of 41 intents (for example `persyaratan_magang` or `manfaat_IISMA`).
4. The bot replies with one of the prepared answers for that intent from `dataset/Intent_KM.json`.

## Tech stack

Python, Flask, TensorFlow/Keras, NLTK, scikit-learn (label encoder), HTML/CSS/JavaScript with Bootstrap 5 and jQuery.

## Project structure

```
app.py                 Flask routes (chat page and /get endpoint)
process.py             Text preprocessing, intent prediction, response selection
dataset/Intent_KM.json Intents, example questions and answers
model/                 Trained Keras model, tokenizer and label encoder
templates/index.html   Chat interface
static/                CSS, JavaScript and images
```

## Running locally

```bash
git clone https://github.com/SaidWildan/kampus-merdeka-chatbot.git
cd kampus-merdeka-chatbot
pip install -r requirements.txt
python app.py
```

Then open http://127.0.0.1:5000 in your browser. On first run, NLTK downloads the tokenizer and WordNet data it needs.

> The dependencies are pinned to 2022 versions (TensorFlow 2.9). Use a Python version supported by those packages (3.9 or 3.10), ideally in a virtual environment.

## Security fixes

While revisiting this project I fixed two issues:

- **DOM-based XSS in the chat window.** Messages were inserted with `insertAdjacentHTML` without escaping, so typing something like `<img src=x onerror=alert(1)>` executed JavaScript in the page. Messages are now HTML-escaped before rendering.
- **Flask debug mode.** The app ran with `debug=True`, which exposes the Werkzeug interactive debugger. It now runs with debug off and binds to localhost only.

## Author

Said Muhammad Wildan
