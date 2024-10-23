# Customer Question Answering Chatbot

This project is a fine-tuned BERT-based-Chinese chatbot designed to answer customer questions using a pre-existing knowledge base stored in an Excel file. The chatbot encodes customer queries and compares them with the most similar questions from the knowledge base using cosine similarity to provide relevant answers.

## Project Structure

- `train.py`: Script to fine-tune  the `bert-base-chinese` pre-trained model , encode questions from the knowledge base, and save the trained model and data.
- `QA_chatbot.py`: Chatbot class implementation, which loads the trained BERT model and finds the top 3 similar questions to user input.
- `app.py`: Flask web application to serve the chatbot and handle API requests.
- `index.html`: Frontend interface to interact with the chatbot.

## How It Works

1. **Training:**
   - The BERT tokenizer and model are loaded from Hugging Face's pre-trained models.
   - Questions in the knowledge base (Excel file) are tokenized and encoded into vectors.
   - Encoded vectors and the corresponding answers are saved for later use.
   
2. **Chatbot:**
   - The chatbot encodes the user's input using the same pre-trained BERT model.
   - It compares the input vector with the pre-encoded questions using cosine similarity.
   - The chatbot returns the top 3 most similar questions and their answers, along with confidence scores.

3. **Web Interface:**
   - Users can input their question into a simple web interface (built with HTML and JavaScript).
   - The backend (Flask API) processes the input, returns similar questions, and displays the answers with confidence levels.

## Files Description

- **`qa_knowledge_base.xlsx`**: Contains the knowledge base with questions (`QA-問題`) and their corresponding answers (`QA-答案`).
- **`train.py`**: Responsible for encoding the questions and saving the model.
- **`QA_chatbot.py`**: Core chatbot class with functions to load the model and compute similarities between user input and the pre-encoded questions.
- **`app.py`**: Flask application for serving the chatbot as an API.
- **`index.html`**: Frontend interface for asking questions and getting answers.

## Installation and Setup

### 1. Clone the repository.
    git clone https://github.com/james11200/Customer-Question-Answering-Chatbot.git
    
### 2. Install the required dependencies.
    pip install transformers torch pandas flask scikit-learn flask-cors
    
### 3. Run `train.py` to train the chatbot and encode the knowledge base.
    python train.py
    
### 4. Start the Flask application to serve the chatbot.
    python app.py
    
### 5. Open a browser and visit `http://localhost:5000` to interact with the chatbot.

## Usage

- The user can enter a question in the web interface.
- The backend will return the top 3 similar questions from the knowledge base along with their corresponding answers and confidence levels.

## Example Interaction

- **User Input:** "刷卡顯示異常"
- **Chatbot Response:**
  - Top 1 similar question: "刷卡顯示異常"
    - Answer: "請重新刷卡，並確保您的網路連接正常。"
    - Confidence: 0.92
  - Top 2 similar question: "信用卡無法使用"
    - Answer: "請聯繫您的信用卡發行銀行確認卡片狀況。"
    - Confidence: 0.85
  - Top 3 similar question: "支付失敗"
    - Answer: "請檢查您的支付方式或稍後再試。"
    - Confidence: 0.78
