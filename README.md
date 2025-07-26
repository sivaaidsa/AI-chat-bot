# AI-chat-bot
import nltk
import random
import string

# Download necessary NLTK data
nltk.download('punkt')
nltk.download('wordnet')

from nltk.stem import WordNetLemmatizer
from nltk.tokenize import word_tokenize

# Initialize lemmatizer
lemmatizer = WordNetLemmatizer()

# Sample conversation corpus
corpus = {
    "greeting": ["hi", "hello", "hey", "good morning", "good evening"],
    "greeting_responses": ["Hello!", "Hi there!", "Hey!", "Greetings!"],
    "farewell": ["bye", "goodbye", "see you", "take care"],
    "farewell_responses": ["Goodbye!", "See you later!", "Take care!"],
    "thanks": ["thanks", "thank you", "appreciate it"],
    "thanks_responses": ["You're welcome!", "No problem!", "Glad to help!"]
}

# Simple text cleaning and lemmatization
def preprocess(sentence):
    tokens = word_tokenize(sentence.lower())
    tokens = [lemmatizer.lemmatize(word) for word in tokens if word not in string.punctuation]
    return tokens

# Response generator
def get_response(user_input):
    tokens = preprocess(user_input)

    if any(word in tokens for word in corpus["greeting"]):
        return random.choice(corpus["greeting_responses"])
    elif any(word in tokens for word in corpus["farewell"]):
        return random.choice(corpus["farewell_responses"])
    elif any(word in tokens for word in corpus["thanks"]):
        return random.choice(corpus["thanks_responses"])
    else:
        return "I'm not sure how to respond to that."

# Chat loop
print("Chatbot: Hello! Type 'bye' to exit.")
while True:
    user_input = input("You: ")
    if user_input.lower() in ["bye", "exit", "quit"]:
        print("Chatbot: Goodbye!")
        break
    response = get_response(user_input)
    print(f"Chatbot: {response}")
