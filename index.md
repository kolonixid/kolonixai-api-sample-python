# Kolonix API Documentation

## Overview

This documentation provides information on how to consume chat completions on Kolonix with and without streaming support.

## Sample Implementation

<details>
  <summary>Implementation without Streaming</summary>

  ```python
  import json
  import openai
  import requests

  # Set your OpenAI API key
  api_key = "your_api_key_here"

  # Set the base URL
  base_url = "https://kolonix.com/v1/"

  # Configure the OpenAI library to use the specified base URL
  openai.api_key = api_key
  openai.api_base = base_url

  try:
      response = openai.ChatCompletion.create(
          model="4o-kol",
          messages=[{"role": "user", "content": "hi"}],
          temperature=1,
          top_p=1,
          max_tokens=150
      )
      # Print the response
      print("Response received:")
      print(response.choices[0].message['content'])
  except openai.OpenAIError as e:
      # Handle OpenAI API errors
      print(f"OpenAI API error: {e}")
  except requests.exceptions.RequestException as e:
      # Handle requests exceptions
      print(f"Request error: {e}")
  except Exception as e:
      # Handle any other exceptions
      print(f"An error occurred: {e}")
</details> <details> <summary>Implementation with Streaming</summary>

import json
import openai
import requests

# Set your OpenAI API key
api_key = "your_api_key_here"

# Set the base URL
base_url = "https://kolonix.com/v1/"

# Configure the OpenAI library to use the specified base URL
openai.base_url = base_url
openai.api_key = api_key

try:
    response = openai.chat.completions.create(
        model="4o-kol",
        messages=[{"role": "user", "content": "hi"}],
        temperature=1,
        top_p=1,
        max_tokens=150,
        stream=True
    )
    # Print the response
    print("Response:", end=" ", flush=True)  # Start the response line
    for chunk in response:
        # Access content using object attributes
        if chunk.choices and chunk.choices[0].delta.content:
            content = chunk.choices[0].delta.content
            print(content, end="", flush=True)  # Print without newline

    print()  # Add a newline after the stream is complete
except openai.OpenAIError as e:
    # Handle OpenAI API errors
    print(f"OpenAI API error: {e}")
except requests.exceptions.RequestException as e:
    # Handle requests exceptions
    print(f"Request error: {e}")
except Exception as e:
    # Handle any other exceptions
    print(f"An error occurred: {e}")
</details>
Instructions
Login to your Kolonix account.
Click on your profile on the top right corner.
Get your API key.
Replace your_api_key_here in the code above with your actual API key.


### How to Use `details` and `summary` Tags
- The `<details>` tag creates a collapsible section.
- The `<summary>` tag specifies the heading for the collapsible section.

### Commit and Push Changes
1. Save the file and commit your changes:
   ```bash
   git add index.md
   git commit -m "Add API documentation with collapsible sections for streaming and non-streaming implementations"
   git push origin main