# FastAPI Basics for Beginners

## What is FastAPI?

FastAPI is a modern Python web framework used to build APIs (Application
Programming Interfaces). It is fast, easy to learn, and widely used for
AI backends.

## Why use FastAPI?

-   High performance
-   Easy syntax
-   Automatic API documentation
-   Request validation with Pydantic
-   Great for AI, ML, and web applications

## What is an API?

An API lets two applications communicate. Example: React -\> FastAPI -\>
Groq -\> FastAPI -\> React.

## Where is FastAPI used?

-   AI chatbots
-   LangChain/LangGraph apps
-   RAG systems
-   REST APIs
-   Mobile backends
-   Authentication
-   Microservices

## Basic Concepts

### Endpoints

Examples: GET /, POST /chat

### Request

Data sent by the client.

### Response

Data returned by the server.

### JSON

Standard format for exchanging data.

## Simple Example

``` python
from fastapi import FastAPI
app=FastAPI()
@app.get('/')
def home():
    return {'message':'Hello World'}
```

## Automatic Documentation

-   /docs
-   /redoc

## Typical AI Architecture

React Frontend -\> FastAPI -\> LLM -\> Vector DB -\> Response

## Summary

FastAPI is a Python framework for building APIs. It receives requests,
runs Python code, communicates with databases or AI models, and returns
responses.
