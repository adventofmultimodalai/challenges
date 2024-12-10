### **AI Storyboarding Challenge: Build a Fully Automated Cartoon Strip Generator**

Welcome to the **AI Storyboarding Challenge**, where your creativity meets Generative AI! In this challenge, your task is to **build a fully automated application** capable of generating a dynamic cartoon strip from a **single story prompt** provided by the user. 

The application you build should take the user’s prompt (e.g., *“A detective dog solving mysteries in a comic club”*) and generate a complete, cohesive cartoon strip, including visuals and accompanying storyline, **entirely through automation**.

---

#### **Challenge Overview**

Participants must design and implement a system that automates the entire workflow of creating a cartoon strip:
1. **Input:** Accept a single, high-level story prompt from the user.
2. **Dynamic Story Generation:** Use text generation models (Phi3 or LLava) to create a multi-scene story outline based on the user's input.
3. **Visual Creation:** Generate unique images for each scene in the story using AI image-generation models (e.g., SDXL or Flux).
4. **Story Expansion:** Refine each scene by feeding the generated images and descriptions into multimodal AI tools to enhance narrative depth and continuity.
5. **Scene-to-Scene Continuation:** Dynamically use the output of one scene to guide the content of the next, ensuring the cartoon strip is cohesive and engaging.
6. **Final Assembly:** Automatically stitch together the images and story descriptions into a polished cartoon strip format (e.g., an image, or web interface).

---


#### Sample Code to Get Started

**Step 1: Generate a Story Outline (Phi3 API)**
The following snippets will guide you through interacting with the APIs to create your own automated cartoon strip:
```python
import requests

PHI3_URL = "https://cu-vertical-dimensional-continuity.trycloudflare.com/phi3/generate"
PHI3_TOKEN = "your_phi3_token"

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
prompt = "A brave puppy and robot friend solving mysteries in a futuristic city."
story_outline = generate_story_outline(prompt)
print("Story Outline:", story_outline)
```

**Step 2: Generate an Image (Flux API)**
```python
FLUX_URL = "https://maintained-thai-filter-four.trycloudflare.com/imagine/generate"
FLUX_TOKEN = "provided token" # check the API docs in resources

def generate_image(description, output_file):
    headers = {
        "Authorization": f"Bearer {FLUX_TOKEN}",
        "Content-Type": "application/json"
    }
    payload = {
        "prompt": description[:200],  # max 200 characters allowed for prompt
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

**Step 3: Assemble Images and Descriptions**

- Combine generated images and expanded story descriptions into a comic strip.
- Use tools like Python’s Pillow library for formatting and adding text to images.
- Output the final result as a slideshow, web page, or PDF.

---

#### **Scoring Criteria**

| **Criteria**               | **Weight** | **Description**                                                                                       |
|-----------------------------|------------|-------------------------------------------------------------------------------------------------------|
| **Creativity of Storyline** | 30%        | How engaging, cohesive, and imaginative is the narrative?                                            |
| **Visual Appeal**           | 25%        | How well do the generated images align with the story, and are they visually consistent across scenes?|
| **Effective Use of Tools**  | 25%        | How seamlessly were the tools used to automate the process from script to visuals to story assembly? |
| **Output Polish**           | 10%        | Is the final cartoon strip or output well-organized and visually appealing?                          |
| **Optional Interaction**    | 10%        | If user-interaction features were added, how intuitive and impactful are they?                       |

---

#### **Deliverables**

1. The final cartoon strip (as a slideshow, web page, or PDF).  
2. A brief explanation of how your automated pipeline worked.  

---

This challenge is designed to inspire creativity and innovation while showcasing the power of automation in multimodal AI workflows. We can’t wait to see what amazing stories and visuals you create! 🎨✨
