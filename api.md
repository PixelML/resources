# 🌟 **Advent of Multi-Modal Hackathon: API Documentation** 🚀

Welcome to the **Advent of Multi-Modal Hackathon**, where innovation meets creativity! 🎨✨ This documentation is your ultimate guide to accessing and leveraging deployed AI models for he hack. Whether you’re generating text, combining multimodal inputs (🖼️+✍️), or creating stunning visuals, these APIs will help you to build **awesome solutions** for the hackathon challenges. 🛠️💡

---

## 🛠️ **Getting Started**

- **Deploy Models Instantly**: Explore our AI templates at [🌐 https://tiberaicommunity.github.io/ai-templates](https://tiberaicommunity.github.io/ai-templates) to set up a dedicated API for your project. 🖥️✨
- **Need Hardware?**: Reach out, and we’ll assist with dedicated compute resources. 💪⚙️
- **Contribute & Star**: Have model ideas or suggestions? Check out [⭐ xpu_tgi](https://github.com/tiberaicommunity/xpu_tgi) and [⭐ xpu_ray](https://github.com/rahulunair/xpu_ray) to contribute or leave a star if you find these resources helpful! 🌟

---

## 🔑 **What’s Inside?**

These APIs give you access to:
- 💬 **Generative Text**: Craft compelling stories, summaries, or technical responses.
- 🎨 **Image Generation**: Create breathtaking visuals from simple text prompts.
- 🖼️+✍️ **Multimodal Fusion**: Combine text and images for a richer AI experience.

Dive into the examples below to supercharge your hackathon projects! 🚀✨ Let’s build something incredible together! 💡🎉

# **LLava-Next API Guide**

Welcome to the LLava-Next API! This API provides the capability to interact with the LLava-Next generative AI model for both text and multimodal inputs (image + text). Below, you'll find details on how to use the API, supported endpoints, and usage examples.

---

## **API Endpoint**
Base URL:  
```
https://supplement-convenient-scores-forgotten.trycloudflare.com/llava/generate
```

---

## **Authentication**
The API uses a Bearer token for authentication. The token provided for the hackathon is:
```
Bearer Mklm9M70UL39aQhBLiDSDM2yv1V73uXWMA-GBN1LBDU
```

Include this token in the `Authorization` header for all API requests.

---

## **Supported APIs**

### **1. Generate Response API**
- **Description**: Generate a response from the model based on text input, image input, or a combination of both.
- **HTTP Method**: POST  
- **Headers**:
  ```
  Accept: application/json
  Content-Type: application/json
  Authorization: Bearer <your_token>
  ```
- **Payload**:
  ```json
  {
    "inputs": "<formatted_input>",
    "parameters": {
      "max_new_tokens": 300,
      "temperature": 0.7
    }
  }
  ```
  - **inputs**: The formatted input containing text and/or image.
  - **parameters**: Parameters to control the response generation.

---

## **Input Formatting**

### **Text Only Input**
For text-only inputs, format the prompt as follows:
```
<|im_start|>system
Answer the questions.<|im_end|>
<|im_start|>user
[Your question or instruction here]
<|im_end|>
<|im_start|>assistant
```

### **Image + Text Input**
For image-based queries, include the image as a Base64-encoded string:
```
<|im_start|>system
Answer the questions.<|im_end|>
<|im_start|>user
![Image Description](data:image/jpeg;base64,<your_base64_encoded_image>)
[Your question or instruction here]
<|im_end|>
<|im_start|>assistant
```

---

## **Examples**

### **Example 1: Text-Only Query**
```python
import requests

headers = {
    "Accept": "application/json",
    "Content-Type": "application/json",
    "Authorization": "Bearer Mklm9M70UL39aQhBLiDSDM2yv1V73uXWMA-GBN1LBDU"
}

payload = {
    "inputs": "<|im_start|>system\nAnswer the questions.<|im_end|><|im_start|>user\nWhat are the key features of LLava-Next?<|im_end|><|im_start|>assistant\n",
    "parameters": {
        "max_new_tokens": 300,
        "temperature": 0.7
    }
}

response = requests.post(
    "https://supplement-convenient-scores-forgotten.trycloudflare.com/llava/generate",
    headers=headers,
    json=payload
)

print(response.json())
```

---

### **Example 2: Image + Text Query**
```python
from PIL import Image
import requests
import base64
from io import BytesIO
import json

# Fetch image from URL
url = "https://github.com/haotian-liu/LLaVA/blob/1a91fc274d7c35a9b50b3cb29c4247ae5837ce39/images/llava_v1_5_radar.jpg?raw=true"
image = Image.open(requests.get(url, stream=True).raw)

# Resize and compress the image
max_size = 200  # Reduce maximum size for smaller Base64 string
ratio = min(max_size / image.size[0], max_size / image.size[1])
new_size = tuple([int(x * ratio) for x in image.size])
image = image.resize(new_size, Image.Resampling.LANCZOS)
image = image.convert('RGB')

# Convert image to Base64
buffer = BytesIO()
image.save(buffer, format="JPEG", quality=50)  # Reduce quality for smaller size
base64_image = base64.b64encode(buffer.getvalue()).decode('utf-8')

# Prepare the inputs
image_string = f"data:image/jpeg;base64,{base64_image}"
query = "List metrics and values in the radar chart for LLaVA-1.5."
prompt = f"<|im_start|>system\nAnswer concisely.<|im_end|><|im_start|>user\n![]({image_string})\n{query}<|im_end|><|im_start|>assistant\n"

# Prepare headers and payload
headers = {
    "Accept": "application/json",
    "Content-Type": "application/json",
    "Authorization": "Bearer Mklm9M70UL39aQhBLiDSDM2yv1V73uXWMA-GBN1LBDU"
}

payload = {
    "inputs": prompt,
    "parameters": {
        "max_new_tokens": 150,
        "temperature": 0.7
    }
}

# Make the request
response = requests.post(
    "https://supplement-convenient-scores-forgotten.trycloudflare.com/llava/generate",
    headers=headers,
    json=payload
)

# Get and display the response
response_data = response.json()
print(json.dumps(response_data, ensure_ascii=False, indent=2))

```

---

## **Use Cases**
1. **Multimodal Chat**: Interact with the model using both image and text inputs.
2. **Question Answering**: Ask questions about provided text or images.
3. **Image Analysis**: Provide images with related text queries for analysis.

---

## **Notes**
- This is a hackathon version of the API; please use the provided token only for this event.
- Refer to the [LLava-Next Documentation](https://github.com/haotian-liu/LLaVA) for more insights into the model's capabilities.

# **Phi3 API Guide**

This API provides access to the Phi3 model, a text-only model with a large context length suitable for various tasks such as summarization, creative writing, and technical explanations. Below are the details for interacting with the API.

---

## **API Endpoint**
```
https://cu-vertical-dimensional-continuity.trycloudflare.com/phi3/generate
```

---

## **Authentication**
You need a valid token to authenticate API requests.  
Set the token in the `Authorization` header for all requests.

Example:
```python
VALID_TOKEN = "AEulafWZQ1xhIkeLgjcp5nhL7d0cLPWiXAU34DTVvXI"
```

Replace the token with the one provided to you.

---

## **Request Format**
### **HTTP Method**: `POST`

### **Headers**:
- `Authorization`: `Bearer <VALID_TOKEN>`
- `Content-Type`: `application/json`

### **Payload**:
```json
{
  "inputs": "<|system|>\n[system role instructions]<|end|>\n<|user|>\n[user prompt]<|end|>\n<|assistant|>",
  "parameters": {
    "max_new_tokens": 100,           // Optional, max number of tokens to generate
    "temperature": 0.7               // Optional, controls randomness of the output
  }
}
```

---

## **Examples**

### **Example 1: General Query**
```python
import requests

# Define the token and endpoint
VALID_TOKEN = "AEulafWZQ1xhIkeLgjcp5nhL7d0cLPWiXAU34DTVvXI"
url = "https://cu-vertical-dimensional-continuity.trycloudflare.com/phi3/generate"

# Set headers
headers = {
    "Authorization": f"Bearer {VALID_TOKEN}",
    "Content-Type": "application/json"
}

# Define payload
payload = {
    "inputs": "<|system|>\nYou are a helpful assistant.<|end|>\n<|user|>\nWhat are three advantages of using renewable energy?<|end|>\n<|assistant|>",
    "parameters": {
        "max_new_tokens": 100
    }
}

# Make the request
response = requests.post(url, headers=headers, json=payload)

# Display the response
if response.status_code == 200:
    print(response.json().get("generated_text", "No response text available"))
else:
    print(f"Error: {response.status_code}, {response.text}")
```

---

### **Example 2: Creative Writing**
```python
import requests

# Define the token and endpoint
VALID_TOKEN = "AEulafWZQ1xhIkeLgjcp5nhL7d0cLPWiXAU34DTVvXI"
url = "https://cu-vertical-dimensional-continuity.trycloudflare.com/phi3/generate"

# Set headers
headers = {
    "Authorization": f"Bearer {VALID_TOKEN}",
    "Content-Type": "application/json"
}

# Define payload
payload = {
    "inputs": "<|system|>\nYou are a creative writing assistant.<|end|>\n<|user|>\nWrite a short story about a robot discovering emotions.<|end|>\n<|assistant|>",
    "parameters": {
        "max_new_tokens": 300,
        "temperature": 0.7
    }
}

# Make the request
response = requests.post(url, headers=headers, json=payload)

# Display the response
if response.status_code == 200:
    print(response.json().get("generated_text", "No response text available"))
else:
    print(f"Error: {response.status_code}, {response.text}")
```

---

### **Example 3: Technical Explanation**
```python
import requests

# Define the token and endpoint
VALID_TOKEN = "AEulafWZQ1xhIkeLgjcp5nhL7d0cLPWiXAU34DTVvXI"
url = "https://cu-vertical-dimensional-continuity.trycloudflare.com/phi3/generate"

# Set headers
headers = {
    "Authorization": f"Bearer {VALID_TOKEN}",
    "Content-Type": "application/json"
}

# Define payload
payload = {
    "inputs": "<|system|>\nYou are a helpful assistant.<|end|>\n<|user|>\nExplain quantum computing.<|end|>\n<|assistant|>",
    "parameters": {
        "max_new_tokens": 200,
        "temperature": 0.5
    }
}

# Make the request
response = requests.post(url, headers=headers, json=payload)

# Display the response
if response.status_code == 200:
    print(response.json().get("generated_text", "No response text available"))
else:
    print(f"Error: {response.status_code}, {response.text}")
```

---

## **Notes**
1. Ensure that the `VALID_TOKEN` is set correctly before making requests.
2. Use the proper prompt template to structure the input:
   - `<|system|>`: System role instructions
   - `<|user|>`: User's query or task
   - `<|assistant|>`: Assistant's response
3. Adjust the `max_new_tokens` and `temperature` parameters for different use cases:
   - **max_new_tokens**: Controls the length of the generated output.
   - **temperature**: Higher values produce more creative or random results; lower values make the output more deterministic.


# **Flux Models API Guide**

This API allows users to generate images using Flux models with two server endpoints. Users can choose either server based on availability or preference. Below are the details for interacting with the API.

---

## **API Endpoints**
You can use one of the following endpoints:

1. **Server 1**:  
   ```
   https://maintained-thai-filter-four.trycloudflare.com/imagine/generate
   ```

2. **Server 2**:  
   ```
   https://mirrors-stability-males-supplement.trycloudflare.com/imagine/generate
   ```

---

## **Authentication**
You need a valid token to authenticate API requests.  
Set the token in the `Authorization` header for all requests.

Example:
```python
FLUX_TOKEN = "calm-bold-tree-bd1b1c8bc141403231e7f0a8"
```

Replace the token with the one provided to you.

---

## **Request Format**
### **HTTP Method**: `POST`

### **Headers**:
- `Authorization`: `Bearer <FLUX_TOKEN>`
- `Content-Type`: `application/json`

### **Payload**:
```json
{
  "prompt": "a magical cosmic unicorn",  // The text prompt for generating the image
  "img_size": 1024,                     // Image size in pixels (e.g., 512, 1024)
  "guidance_scale": 0,                  // Controls adherence to the prompt
  "num_inference_steps": 4              // Number of steps for the inference
}
```

---

## **Examples**

### **Example 1: Using Server 1**
```python
import requests

FLUX_TOKEN = "calm-bold-tree-bd1b1c8bc141403231e7f0a8"
url = "https://maintained-thai-filter-four.trycloudflare.com/imagine/generate"

headers = {
    "Authorization": f"Bearer {FLUX_TOKEN}",
    "Content-Type": "application/json"
}

payload = {
    "prompt": "a magical cosmic unicorn",
    "img_size": 1024,
    "guidance_scale": 0,
    "num_inference_steps": 4
}

response = requests.post(url, headers=headers, json=payload)

# Save the generated image
if response.status_code == 200:
    with open("image.png", "wb") as f:
        f.write(response.content)
    print("Image saved as image.png")
else:
    print(f"Error: {response.status_code}, {response.text}")
```

---

### **Example 2: Using Server 2**
```python
import requests

FLUX_TOKEN = "unique-warm-tree-d536eb19a6112b289a167c7b"
url = "https://mirrors-stability-males-supplement.trycloudflare.com/imagine/generate"

headers = {
    "Authorization": f"Bearer {FLUX_TOKEN}",
    "Content-Type": "application/json"
}

payload = {
    "prompt": "a magical cosmic cat",
    "img_size": 1024,
    "guidance_scale": 0,
    "num_inference_steps": 4
}

response = requests.post(url, headers=headers, json=payload)

# Save the generated image
if response.status_code == 200:
    with open("image.png", "wb") as f:
        f.write(response.content)
    print("Image saved as image.png")
else:
    print(f"Error: {response.status_code}, {response.text}")
```

---

## **Notes**
1. Ensure that the `FLUX_TOKEN` is set correctly before making requests.
2. The `guidance_scale` and `num_inference_steps` can be adjusted to modify the output's quality and prompt adherence:
   - **guidance_scale**: Higher values make the image more aligned with the prompt.
   - **num_inference_steps**: Increasing steps generally improves image quality but slows down inference.
3. Images will be saved locally with the file name specified in the script (e.g., `image.png`).

# **SDXL-Lightning API Guide**

This API allows users to generate images using the SDXL-Lightning model. Below are the details for interacting with the API, with examples in Python.

---

## **API Endpoint**
```
https://singing-shadows-duty-loan.trycloudflare.com/imagine/generate
```

---

## **Authentication**
You need a valid token to authenticate API requests.  
Set the token in the `Authorization` header for all requests.

Example:
```python
VALID_TOKEN = "wise-radiant-wave-b77c84b64e9efa2ebf8710ca"
```

Replace the token with the one provided to you.

---

## **Request Format**
### **HTTP Method**: `POST`

### **Headers**:
- `Authorization`: `Bearer <VALID_TOKEN>`
- `Content-Type`: `application/json`

### **Payload**:
```json
{
  "prompt": "a serene mountain landscape during sunset",  // The text prompt for generating the image
  "img_size": 1024,                                     // Image size in pixels (e.g., 512, 1024)
  "guidance_scale": 7.5,                                // Controls adherence to the prompt
  "num_inference_steps": 50                             // Number of steps for the inference
}
```

---

## **Example in Python**

### **Python Example**
```python
import requests

# Define the token and endpoint
VALID_TOKEN = "wise-radiant-wave-b77c84b64e9efa2ebf8710ca"
url = "https://singing-shadows-duty-loan.trycloudflare.com/imagine/generate"

# Set headers
headers = {
    "Authorization": f"Bearer {VALID_TOKEN}",
    "Content-Type": "application/json"
}

# Define payload
payload = {
    "prompt": "a serene mountain landscape during sunset",
    "img_size": 1024,
    "guidance_scale": 7.5,
    "num_inference_steps": 50
}

# Make the request
response = requests.post(url, headers=headers, json=payload)

# Save the generated image
if response.status_code == 200:
    with open("sdxl_image.png", "wb") as f:
        f.write(response.content)
    print("Image saved as sdxl_image.png")
else:
    print(f"Error: {response.status_code}, {response.text}")
```

---

## **Notes**
1. Ensure that the `VALID_TOKEN` is set correctly before making requests.
2. The `guidance_scale` and `num_inference_steps` can be adjusted to modify the output's quality and prompt adherence:
   - **guidance_scale**: Higher values make the image more aligned with the prompt.
   - **num_inference_steps**: Increasing steps generally improves image quality but slows down inference.
3. Images will be saved locally with the file name specified in the script (e.g., `sdxl_image.png`).


Happy generating and hacking! 🚀


