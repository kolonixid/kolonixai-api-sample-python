# Kolonix API Documentation

## Overview

This documentation provides information on how to consume chat completions on Kolonix with and without streaming support.

---

## Sample Implementation (/chat/completions)

<details>
  <summary>Implementation without Streaming</summary>
  
  Please enable cookies if you are calling with async task, below only sample for sync task
  
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
          response = openai.chat.completions.create(
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
  ```
</details> 
<details> 
  <summary>Implementation with Streaming</summary>

  ```python
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
   ```
</details>


## Instructions
1. Login to your Kolonix account https://kolonix.com/.
2. Click on your profile on the top right corner.
3. Get your API key.
4. Replace your_api_key_here in the code above with your actual API key.




