# Install required libraries first:
# pip install flask openai

from flask import Flask, request, jsonify
import openai

# Set up OpenAI API key
openai.api_key = 'your_openai_api_key'

# Initialize Flask app
app = Flask(__name__)

# Define a route to handle chat input
@app.route('/chat', methods=['POST'])
def chat():
    user_input = request.json.get('message')
    
    # Use OpenAI GPT model to get a response
    response = openai.Completion.create(
        engine="text-davinci-003",  # The engine can be any suitable GPT model
        prompt=user_input,
        max_tokens=150
    )

    # Extract the text part of the response
    bot_reply = response.choices[0].text.strip()

    return jsonify({"response": bot_reply})

# Run the app
if __name__ == '__main__':
    app.run(debug=True)
