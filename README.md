# GENERATIVE-TEXT-MODEL

**COMPANY*: CODETECH IT SOLUTION

*NAME*: SHARVANI SURAJ MAHADIK

*INTERN ID*:CT08LKR

*DOMAIN*:ARTIFICIAL INTELLIGENCE

*DURATION*:4 WEEKS

*MENTOR*: NEELA SANTOSH

*DESCRIPTION*:
This project demonstrates the implementation of a Generative Text Model using GPT-2 (a pre-trained transformer model from Hugging Face) combined with Gradio to create a user-friendly web-based interface. The application allows users to input a prompt and receive generated human-like text based on the input.
The primary goal of this project is to create an interactive and accessible tool for text generation using GPT-2. This tool enables users to generate content on-demand by simply providing a prompt, which can be useful for various applications such as writing assistance, content generation, and creative writing.

Install Dependencies:
!pip install transformers
!pip install transformers gradio
These lines install two Python libraries:
Transformers: This is from Hugging Face and provides pre-trained models and tools for Natural Language Processing (NLP) tasks like text generation, translation, and summarization.
Gradio: This library is used to create simple, customizable user interfaces (UIs) for machine learning models. It enables interactive testing for models directly through a web-based interface.

Import Libraries
import gradio as gr
from transformers import pipeline
gradio is the UI framework that we are using to create the frontend.
pipeline from Transformers is a high-level utility that loads pre-trained models for specific tasks, such as text generation, without needing detailed model handling or fine-tuning.

Initialize the Text Generation Pipeline
generator = pipeline('text-generation', model='gpt2')
The pipeline function loads the GPT-2 model, which is a pre-trained transformer model for text generation.
'text-generation' specifies the task we are performing, which is text generation.
model='gpt2' loads the GPT-2 model. GPT-2 is a transformer-based language model capable of generating human-like text based on input prompts.

Text Generation Function
def generate_text(prompt):
    try:
        result = generator(prompt, max_length=150, num_return_sequences=1)
        return result[0]['generated_text']
    except Exception as e:
        return str(e)
generate_text(prompt) is a function that takes a prompt (text input) as an argument and uses the GPT-2 model to generate text based on it.
generator(prompt, max_length=150, num_return_sequences=1):
prompt is the input provided by the user.
max_length=150 ensures that the generated text does not exceed 150 tokens (words or subwords).
num_return_sequences=1 specifies that only one generated sequence is returned.
return result[0]['generated_text']: Extracts the generated text from the result, which is returned as the output of the function.
If there's an error (e.g., a connection issue with the model), it is caught and returned as an exception.

UI Function
def ui_function(prompt):
    return generate_text(prompt)
ui_function(prompt) is the function that will be called when the user enters a prompt in the Gradio interface. It simply calls generate_text with the user's input.

Gradio Interface Setup
interface = gr.Interface(
    fn=ui_function,
    inputs=gr.Textbox(lines=2, placeholder="Enter your prompt here..."),
    outputs="text",
    title="Generative Text Model",
    description="Enter a prompt to generate human-like text.",
    examples=[ 
        ["Explain the impact of artificial intelligence on healthcare."],
        ["Write a paragraph about the benefits of learning a new language."]
    ],
    css=custom_css  # Apply the custom CSS for styling
)
gr.Interface is the function that creates the Gradio interface, linking the model's logic (the function ui_function) with the frontend that users interact with.
fn=ui_function: The function to be executed when the user submits input. This function will call the generate_text function to generate text based on the user's input.
inputs=gr.Textbox(...): Specifies the input widget (a text box) where the user will type their prompt. The lines=2 argument means the input box will have two lines of text height, and placeholder="Enter your prompt here..." provides a hint for the user on what to enter.
outputs="text": This indicates that the output will be displayed as text. The generated text will be shown to the user in the output area.
title="Generative Text Model": This is the title that appears at the top of the interface.
description="Enter a prompt to generate human-like text.": A description explaining what the model does.
examples=[...]: A list of example inputs that users can click to automatically populate the input box. These are prompts to help users get started with the model.
css=custom_css: This allows you to add custom CSS to style the interface.

Custom CSS for Styling
custom_css = """
    .gradio-container {
        background-color: #E6E6FA;  /* Lilac color */
    }
    .gradio-button {
        background-color: #8A2BE2;  /* Violet color */
        color: white;
    }
    .gradio-button:hover {
        background-color: #7A1FA1;  /* Darker violet on hover */
    }

"""

Custom CSS is used to style the Gradio interface:
.gradio-container { background-color: #E6E6FA; }: Sets the background color of the entire interface to lilac (#E6E6FA).
.gradio-button { background-color: #8A2BE2; color: white; }: Styles the buttons to have a violet background (#8A2BE2) and white text. This creates a nice, contrasting color scheme for the buttons.
.gradio-button:hover { background-color: #7A1FA1; }: Defines a hover effect for the button. When the user hovers over the button, the background color changes to a darker shade of violet (#7A1FA1), creating a nice interaction effect.

Launch the Interface
interface.launch()
interface.launch(): Launches the Gradio interface, which opens a local web page (or an external URL if deployed) where users can interact with the text generation model.

*OUTPUT*:

![Image](https://github.com/user-attachments/assets/6e96dbf4-1d77-4e8f-ae66-1218235605c6)
