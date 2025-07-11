# College Feedback Classifier

![App Screenshot](./Screenshots/main.png)  
*Interactive AI-powered feedback classification system*

## Overview

The College Feedback Classifier is a web application that uses IBM Watson's FLAN-T5-XXL foundation model to categorize student feedback into academic, facility, or administration themes. The application demonstrates the power of few-shot learning with large language models for text classification tasks.

Key features:
- 🏫 Real-time feedback classification
- 🧪 Model evaluation on test data
- ☁️ Data loaded directly from IBM Cloud Object Storage
- 📊 Performance metrics and comparison tables
- 🎨 Modern, responsive UI with Streamlit

## How It Works

The application follows this workflow:

```mermaid
graph TD
    A[User Feedback Input] --> B[Construct Prompt]
    B --> C[IBM Watson ML Engine]
    C --> D[FLAN-T5-XXL Model]
    D --> E[Theme Prediction]
    E --> F[Result Visualization]
    G[Cloud Object Storage] --> H[Load Training Data]
    H --> I[Create Few-Shot Examples]
    I --> B
```

1. **Data Loading**: Retrieves training and test datasets from IBM Cloud Object Storage
2. **Prompt Engineering**: Creates few-shot learning examples from training data
3. **Model Initialization**: Configures IBM Watson FLAN-T5-XXL model
4. **Test Evaluation**: Runs predictions on test samples and calculates accuracy
5. **User Interaction**: Accepts user feedback and returns classification

## Requirements

- Python 3.11
- IBM Cloud account with access to:
  - Watson Machine Learning
  - Cloud Object Storage
- Required packages (see [requirements.txt](requirements.txt))

## Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/college-feedback-classifier.git
cd college-feedback-classifier
```

2. Create and activate virtual environment:
```bash
python3.11 -m venv venv
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

## Configuration

Before running the application, you need to set up your IBM Cloud credentials:

1. Create a `.env` file in the project root:
```env
IBM_API_KEY="your_ibm_cloud_api_key"
IBM_PROJECT_ID="your_watson_ml_project_id"
COS_API_KEY="your_cos_api_key"
COS_BUCKET="your_cos_bucket_name"
```

2. Update these values in the code:
```python
# In feedback_classifier.py
CREDENTIALS = {
    "url": "https://us-south.ml.cloud.ibm.com",
    "apikey": os.getenv("IBM_API_KEY")  # Updated to use .env
}
PROJECT_ID = os.getenv("IBM_PROJECT_ID")  # Updated to use .env

# In load_data_from_cos function
ibm_api_key_id=os.getenv("COS_API_KEY")
bucket = os.getenv("COS_BUCKET")
```

## Running the Application

Start the Streamlit server:
```bash
streamlit run feedback_classifier.py
```

The application will be accessible at:
`http://localhost:8501`

## Application Interface

The application has two main sections:

### 1. Model Test Results
- Displays a table comparing actual vs predicted themes for 10 test samples
- Shows accuracy metric
- Highlights correct predictions in green and incorrect in red

### 2. Feedback Classifier
- Text area for user feedback input
- "Analyze Feedback" button to trigger classification
- Visual result display with thematic emoji
- Expandable section showing prompt details

## Customization

You can customize the application by:

1. Changing the few-shot examples in `prepare_few_shot_examples()`
2. Modifying the instruction template in `create_prompt()`
3. Adding new theme categories in the instruction text
4. Adjusting model parameters in `init_model()`
5. Updating the UI styling in the custom CSS section

## Screenshots

![Test Results](./Screenshots/test-results.png)  
*Model performance on test data*

![Classification Result](./Screenshots/user-feedback.png)  
*User feedback classification*

## Contributing

Contributions are welcome! Please follow these steps:
1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## Support

For support or questions, please open an issue in the GitHub repository.