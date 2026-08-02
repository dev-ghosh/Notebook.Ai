# Streamlit for AI Applications

## What is Streamlit?

Streamlit is an open-source Python framework used to build interactive
web applications with only Python. It is widely used for AI, Machine
Learning, and Data Science projects.

## Why Use Streamlit?

-   Easy to learn
-   No HTML/CSS/JavaScript required
-   Rapid prototyping
-   Interactive UI components
-   Integrates with AI libraries

## Common Widgets

-   st.title()
-   st.write()
-   st.text_input()
-   st.chat_input()
-   st.button()
-   st.file_uploader()
-   st.selectbox()
-   st.sidebar
-   st.session_state

## Use Cases in AI

-   Chatbots
-   RAG applications
-   Document Q&A
-   LLM assistants
-   Image classification
-   Text summarization
-   Recommendation systems

Architecture:

User → Streamlit UI → FastAPI/LangChain/LangGraph → LLM + Vector DB

## Streamlit vs FastAPI

  Streamlit             FastAPI
  --------------------- ------------------------------
  Frontend UI           Backend APIs
  Interactive widgets   REST endpoints
  Best for demos        Best for production services

## Streamlit Community Cloud

A free hosting platform for Streamlit apps.

Deployment: 1. Push project to GitHub. 2. Connect repository. 3. Select
app.py. 4. Deploy. 5. Share the generated URL.

## Advantages

-   Fast development
-   Great for AI portfolios
-   Pure Python
-   Easy deployment

## Limitations

-   Less customizable than React
-   Not ideal for very complex frontends
-   Free tier has limits

## Key Takeaways

-   Streamlit is ideal for AI demos and prototypes.
-   It is commonly used with FastAPI backends.
-   Streamlit Community Cloud makes deployment simple using GitHub.
