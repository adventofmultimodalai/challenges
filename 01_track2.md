# 🎨🤖 **AI Storyboarding Challenge: Build a Fully Automated Cartoon Strip Generator** 🤖🎨

Welcome to the **AI Storyboarding Challenge**, where your *creativity* meets the magic of **Generative AI**! 🌟 Your mission: **build a fully automated application** capable of generating a *dynamic, fun-filled cartoon strip* from a **single story prompt** provided by the user. 

Imagine starting with just a prompt like: *“A detective dog solving mysteries in a comic club”* 🕵️‍♂️🐶—and ending up with a *vibrant, cohesive cartoon strip* that tells the whole story! **No manual work**, just the power of AI weaving it all together. ✨

---

## 🚀 **Challenge Overview**

Participants will design and implement a system that automates the *entire process* of creating a cartoon strip. Here’s how:

1. **📝 Input:** Take a single, high-level story prompt from the user.
2. **📚 Dynamic Story Generation:** Use text-generation models (e.g., Phi3 or LLava) to create a *multi-scene story outline* based on the user’s input.
3. **🎨 Visual Creation:** Generate unique images for each scene using AI image-generation models (e.g., SDXL or Flux).
4. **🌟 Story Expansion:** Refine each scene by combining visuals and descriptions with multimodal AI tools to deepen narrative continuity.
5. **🔗 Scene-to-Scene Continuation:** Dynamically use outputs from one scene to influence the next, ensuring the cartoon strip flows seamlessly.
6. **📜 Final Assembly:** Automatically stitch together images and text into a *polished cartoon strip format* (e.g., image series, web page, or PDF).

---

## 🛠️ **Get Started with Sample Code**

### **Step 1: Generate a Story Outline (Phi3 API)** 📝
Here’s how to generate a *compelling storyline* for your cartoon strip:
```python
import requests

PHI3_URL = "https://cu-vertical-dimensional-continuity.trycloudflare.com/phi3/generate"
PHI3_TOKEN = "TOKEN_PROVIDED" # Use the Token provided in the API docs: https://github.com/adventofmultimodalai/resources/blob/main/api.md#phi3-api-guide

def generate_story_outline(prompt):
    headers = {
        "Authorization": f"Bearer {PHI3_TOKEN}",
        "Content-Type": "application/json"
    }
    payload = {
        "inputs": f"<|system|>\nYou are a creative story writer.<|end|>\n<|user|>\n{prompt}<|end|>\n<|assistant|>",
        "parameters": {"max_new_tokens": 300}
    }
    response = requests.post(PHI3_URL, headers=headers, json=payload)
    if response.status_code == 200:
        return response.json().get("generated_text", "").split("\n")
    else:
        print(f"Error: {response.status_code}, {response.text}")
        return []

# Example usage
prompt = "A brave puppy and robot solving mysteries in a futuristic city."
story_outline = generate_story_outline(prompt)
print("Story Outline:", story_outline)

### **Step 2: Generate Visuals (Flux API)** 🎨
Bring your story to life with *stunning AI-generated images*:
```python
FLUX_URL = "https://maintained-thai-filter-four.trycloudflare.com/imagine/generate"
FLUX_TOKEN = "provided token"  # Check the API docs for details.

def generate_image(description, output_file):
    headers = {
        "Authorization": f"Bearer {FLUX_TOKEN}",
        "Content-Type": "application/json"
    }
    payload = {
        "prompt": description[:200],  # Max 200 characters for prompt
        "img_size": 512,
        "guidance_scale": 7.5,
        "num_inference_steps": 50
    }
    response = requests.post(FLUX_URL, headers=headers, json=payload)
    if response.status_code == 200:
        with open(output_file, "wb") as f:
            f.write(response.content)
        print(f"Image saved to {output_file}")
    else:
        print(f"Error: {response.status_code}, {response.text}")

# Example usage
generate_image("A puppy and a robot in a futuristic cityscape with neon lights.", "scene_1.png")
```
---

### **Step 3: Assemble Images and Text** 🖼️📜
Combine your visuals and story into a *beautiful cartoon strip*:
- Use **Python’s Pillow library** to format images, add captions, and create a cohesive layout.
- Export your final product as a *slideshow, web page, or PDF*.

---

## 🏆 **Scoring Criteria**

Your submission will be evaluated based on:

| **Criteria**                | **Weight** | **Description**                                                                                       |
|-----------------------------|------------|-------------------------------------------------------------------------------------------------------|
| **🎨 Creativity of Storyline** | 30%        | How engaging, cohesive, and imaginative is the narrative?                                            |
| **📷 Visual Appeal**           | 25%        | How well do the generated images align with the story, and are they visually consistent across scenes?|
| **🤖 Effective Use of Tools**  | 25%        | How seamlessly were the tools used to automate the process from script to visuals to story assembly? |
| **✨ Output Polish**           | 10%        | Is the final cartoon strip or output well-organized and visually appealing?                          |
| **💡 Optional Interaction**    | 10%        | If user-interaction features were added, how intuitive and impactful are they?                       |

---

## 📋 **Deliverables**

1. **The Final Cartoon Strip** (as a slideshow, web page, or PDF).  
2. **A Brief Explanation:** Include how your pipeline works.  
   - *How did you create the story outline?*
   - *How did you generate visuals?*
   - *How were tools integrated to automate the workflow?*

---

## ✨ Let’s Create AI Magic!
Combine *imagination* with the *power of AI* to create something unforgettable! 🕵️‍♂️✨ Whether it’s a brave puppy solving mysteries, a robot adventurer in space, or a whimsical fairy tale, we can’t wait to see your **AI-generated cartoon strips** come to life! 🎨🚀🐶