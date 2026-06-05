# Review Replier — LangGraph + OpenAI

An AI-powered review response agent built with LangGraph that automatically analyzes customer reviews, detects sentiment, diagnoses issues, and generates appropriate replies.

## Features
- Sentiment classification (positive / negative) using structured output
- Deep diagnosis of negative reviews — identifies issue type, emotional tone, and urgency
- Conditional response generation:
  - Positive reviews → warm thank-you + feedback request
  - Negative reviews → empathetic resolution message tailored to issue type and tone
- Structured outputs via Pydantic schemas and `with_structured_output()`

## Tech Stack
- Python, LangGraph, LangChain, OpenAI GPT-4o-mini
- Pydantic v2 for structured schema validation

## Graph Flow

## Setup

```bash
pip install langgraph langchain langchain-openai python-dotenv pydantic
```

Create a `.env` file:

## Run

Open and run `Review_Replier.ipynb` in Jupyter or VS Code.

## Example Output

**Input:**
> "I've been trying to log in for over an hour now, and the app keeps freezing on the authentication screen..."

**Output:**
```json
{
  "sentiment": "negative",
  "diagnosis": { "issue_type": "Bug", "tone": "frustrated", "urgency": "high" },
  "response": "Subject: We're Here to Help You with the Bug Issue..."
}
```

## How It Works
1. Review is passed to `find_sentiment` node → classified as positive or negative
2. Conditional edge routes to `positive_response` or `run_diagnosis`
3. For negative reviews, `run_diagnosis` extracts issue type, tone, and urgency
4. `negative_response` uses the diagnosis to generate a targeted, empathetic reply
