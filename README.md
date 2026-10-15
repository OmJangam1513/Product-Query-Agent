# Product Query Agent

A Python-based product assistant built to explore **LLM tool calling, multi-tool agents, and conversation state management** using LangChain, LangGraph, and Groq.

The agent answers questions about products in a sample online tech store by retrieving product details and review information through custom Python tools.

## Features

- **Product Information Retrieval:** Fetches product prices, ratings, and descriptions.
- **Review Lookup:** Retrieves review counts and ratings for supported products.
- **Tool Calling:** Allows the LLM to select and invoke tools based on the user's question.
- **Multiple Tools:** Combines product information and review lookup in one agent.
- **Conversation Checkpointing:** Uses LangGraph's `InMemorySaver` to retain conversation state between calls sharing the same thread ID.
- **Interactive Experiments:** Demonstrates the difference between stateless interactions and conversations with checkpointing.

## Technologies Used

- Python
- LangChain
- LangGraph
- Groq API
- Jupyter Notebook
- python-dotenv

## Project Structure

```text
Product-Query-Agent/
├── product_query_agent.ipynb
├── pyproject.toml
├── uv.lock
├── .env
└── README.md
```

*The structure above represents the intended project layout. Keep `.env` local and do not commit API keys or secrets.*

## How It Works

### 1. Product Data

The project maintains sample product information in Python dictionaries. Supported products include:

- Wireless headphones
- Smart watch
- Mechanical keyboard
- Laptop stand

### 2. Custom Tools

Two tools are defined:

- `get_product(name)`: Retrieves a product's price, rating, and description.
- `get_review(name)`: Retrieves the number of reviews and the review rating.

These tools use dictionary lookups to retrieve information from the sample dataset.

### 3. LLM Agent

The agent uses Groq's `openai/gpt-oss-20b` model and LangChain's `create_agent` to decide when to call the available tools and formulate a response.

### 4. Conversation State

The notebook first explores an agent without checkpointing, then introduces LangGraph's `InMemorySaver` and a configurable `thread_id`.

This allows messages in the same thread to share checkpointed conversation state while the Python process remains active. The in-memory state is not preserved after the process or notebook kernel is restarted.

## Setup and Installation

### Prerequisites

- Python version supported by the installed dependencies
- A Groq API key
- `uv` for dependency management, or another compatible Python environment

### 1. Clone the Repository

```bash
git clone https://github.com/<your-username>/Product-Query-Agent.git
cd Product-Query-Agent
```

Replace `<your-username>` with your GitHub username.

### 2. Install Dependencies

If the repository includes `pyproject.toml` and `uv.lock`, run:

```bash
uv sync
```

### 3. Configure Environment Variables

Create a local `.env` file in the project root:

```env
GROQ_API_KEY=your_groq_api_key
```

Replace the placeholder with your own API key. Never commit the `.env` file or expose your API key in notebook outputs.

### 4. Launch Jupyter Notebook

```bash
uv run python -m notebook
```

Open `product_query_agent.ipynb` and execute the cells in order.

## Example Questions

```text
What is the price of wireless headphones?

How do people like the smart watch?

What are the price and reviews of the smart watch?

What are the reviews for this product?
```

The final example can demonstrate follow-up questions when the same conversation thread is maintained.

## Learning Objectives

This project explores:

- Defining Python functions as tools for an LLM.
- Creating agents with one or multiple tools.
- Understanding how an LLM decides to invoke tools.
- Passing messages to a LangGraph agent.
- Managing conversation state with a checkpointer and thread ID.
- Configuring a Groq-hosted language model using environment variables.

## Current Limitations

- Product and review information is stored in local Python dictionaries, not a live database or e-commerce API.
- Product lookup currently relies on exact product names after converting input to lowercase.
- Product and review ratings are sample data and may differ between the two dictionaries.
- `InMemorySaver` provides temporary in-memory checkpointing, not permanent storage.
- The project does not currently include a web interface or shopping-cart functionality.

## Future Improvements

- Add more robust product-name matching and input validation.
- Keep product and review ratings consistent.
- Add stock availability and price-range filtering.
- Store product data in a database or retrieve it from an external API.
- Add automated tests for the custom tools.
- Build a simple user interface.

## Purpose

This repository is a hands-on learning project for understanding tool-calling agents and conversation state management in the LangChain and LangGraph ecosystem.

---

**Note:** This is an educational prototype using sample product data, not a production e-commerce application.
