from fastapi import FastAPI, HTTPException
from pydantic import BaseModel
import hashlib

app = FastAPI()

# Welcome note with a customized message
@app.get("/")
def read_root():
    return {"message": "Welcome to the FastAPI application, Jilene135!"}

# Data model for the request body
class TextData(BaseModel):
    text: str

# Generate endpoint to accept POST requests with a JSON body
@app.post("/generate")
def generate(data: TextData):
    # Extract text from the request body
    text = data.text
    # Compute the checksum of the text
    checksum = hashlib.md5(text.encode()).hexdigest()
    # Return the checksum
    return {"checksum": checksum}

# Documentation for the new API endpoint
"""
API Endpoint: /generate
Method: POST
Request Body (JSON):
{
    "text": "string"
}
Response (JSON):
{
    "checksum": "string"
}
Description:
This endpoint accepts a POST request with a JSON body containing a single field called "text."
It returns a checksum (MD5 hash) of the provided text.
"""
