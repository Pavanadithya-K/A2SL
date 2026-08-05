# 🤟 A&T2SL — Audio & Text to Indian Sign Language Converter

A Django-based web application that converts English text into American Sign Language (ASL) animations in real time. It uses NLP techniques — tokenization, POS tagging, lemmatization, and tense detection — to process input text, then plays corresponding sign language video animations for each word or letter.

## 🌐 Live Demo

**🔗 https://a2sl.pythonanywhere.com**

## ✨ Highlights

- 📝 **Text-to-sign conversion** — type any English sentence and watch ASL animations play back sequentially
- 🧠 **NLP-powered processing** — detects verb tenses (past/present/future), removes stopwords, and lemmatizes words for accurate translation
- 🎬 **150+ animation assets** — pre-recorded MP4 videos covering letters A-Z, digits 0-9, and common words
- 🔁 **Smart fallback** — words without dedicated animations are automatically spelled out letter-by-letter
- 🔐 **User authentication** — signup/login system with Django's built-in auth; animation page is login-protected

## 🛠️ Tech Stack

| Layer       | Technology                              |
|-------------|------------------------------------------|
| Backend     | Python 3 + Django 3.0                    |
| NLP         | NLTK (tokenization, POS tagging, WordNet lemmatization) |
| Frontend    | HTML5, CSS3, Django Templates            |
| Database    | SQLite (Django default)                  |
| Assets      | 150+ MP4 animation files                 |

## 🚀 Getting Started

### Prerequisites

- Python 3.8+
- pip

### Setup

```bash
# 1. Navigate to the project folder
cd A&T2SL

# 2. Create and activate a virtual environment
python -m venv venv
venv\Scripts\activate        # Windows
# source venv/bin/activate   # macOS / Linux

# 3. Install dependencies
pip install django nltk

# 4. Download required NLTK data
python -c "import nltk; nltk.download('punkt'); nltk.download('averaged_perceptron_tagger'); nltk.download('wordnet'); nltk.download('omw-1.4')"

# 5. Apply database migrations
python manage.py migrate

# 6. (Optional) Create a superuser for admin access
python manage.py createsuperuser
```

### Run

```bash
# Activate virtual environment (if not already active)
venv\Scripts\activate        # Windows

# Start the development server
python manage.py runserver
```

Open **http://localhost:8000** in your browser.

## 📖 How It Works

1. The user signs up / logs in and navigates to the Animation page.
2. They enter an English sentence (e.g., "I am going to school").
3. NLTK tokenizes the sentence, POS-tags each word, and detects the dominant tense.
4. Stopwords are removed and words are lemmatized to their base form.
5. A tense prefix is added — "Before" for past, "Will" for future, "Now" for present continuous.
6. Each processed word is looked up in the `assets/` folder for a matching MP4.
7. If a video exists, the full-word animation plays; otherwise, it falls back to letter-by-letter animations (a-z).

## 📁 Project Structure

```
A&T2SL/
├── manage.py                 # Django management script
├── db.sqlite3                # SQLite database
├── A2SL/                     # Django project config
│   ├── settings.py           # Project settings
│   ├── urls.py               # URL routing
│   ├── views.py              # NLP pipeline + view logic
│   ├── wsgi.py               # WSGI entry point
│   └── asgi.py               # ASGI entry point
├── templates/                # HTML templates
│   ├── base.html             # Base layout
│   ├── home.html             # Landing page
│   ├── about.html            # About page
│   ├── contact.html          # Contact page
│   ├── login.html            # User login
│   ├── signup.html           # User registration
│   └── animation.html        # Animation playback page
├── assets/                   # ASL animation videos
│   ├── a.mp4 ... z.mp4      # Letter animations
│   ├── 0.mp4 ... 9.mp4      # Number animations
│   └── hello.mp4 ...         # 150+ word animations
└── 1.py                      # NLTK data download helper
```

## 📸 Usage

1. Open the app and sign up for a new account
2. Log in and go to the **Animation** page
3. Type a sentence like "She played football yesterday"
4. Click **Submit** — watch the ASL animations play back in sequence
5. The system prepends "Before" for past tense, "Will" for future, and "Now" for present continuous
