import json
import os
import sys
import traceback
import ollama
import dotenv

dotenv.load_dotenv()  # Load environment variables
PROJECT_PLANNER_MODEL = os.getenv("PROJECT_PLANNER_MODEL", "dolphin-mistral:latest")
CODER_MODEL = os.getenv("CODER_MODEL", "codellama:7b")
MARKDOWN_MAKER = os.getenv("CODER_MODEL", "vicuna:13b-16k")
TASKNAMER = os.getenv("TASKNAMER", "stablelm2:1.6b-zephyr-fp16")

def generate_answers(agent, prompt):
    model_name = ""
    if agent == 'project_planner':
        model_name = PROJECT_PLANNER_MODEL
    elif agent == 'coder':
        model_name = CODER_MODEL
    elif agent == 'markdown':
        model_name = MARKDOWN_MAKER
    elif agent == 'taskname':
        model_name = TASKNAMER
    if not model_name:
        raise ValueError("Model name is not specified in the environment variables or defaults are missing.")
    messages = [
        {
            'role': 'user',
            'content': prompt,
        },
    ]
    try:
        response = ollama.chat(model=model_name, messages=messages)
        return response['message']['content']
    except Exception as e:
        print(f"There was an error communicating with the Ollama model: {e}")
        return None

def summarize_directory(directory_path):
    summaries = []
    try:
        for filename in os.listdir(directory_path):
            file_path = os.path.join(directory_path, filename)
            if os.path.isfile(file_path):
                with open(file_path, 'r') as file:
                    content = file.read()
                    summary = generate_answers('project_planner', content)
                    summaries.append(summary)
        return summaries
    except Exception as e:
        print(f"Error processing directory: {e}")
        traceback.print_exc()
        return []

def create_documentation(summaries, filename, style):
    aggregated_content = '\n\n'.join(summaries)
    if style == 'README':
        formatted_content = generate_answers('markdown', f"📘 Create a README with emojis:\n\n{aggregated_content}")
    elif style == 'DOKU':
        formatted_content = generate_answers('coder', f"Generate detailed documentation:\n\n{aggregated_content}")
    else:
        return None
    with open(filename, 'w') as file:
        file.write(formatted_content)

def main():
    directory_path = sys.argv[1] if len(sys.argv) > 1 else '.'
    summaries = summarize_directory(directory_path)
    create_documentation(summaries, 'README.md', 'README')
    create_documentation(summaries, 'DOKU.md', 'DOKU')

if __name__ == '__main__':
    main()
