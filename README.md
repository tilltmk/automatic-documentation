# Project Documentation Generator 📄

This Python script automates the analysis and summarization of all files within a specified directory, leveraging the Ollama machine learning model to understand and process content efficiently. The output includes two types of documentation files:
1. **README.md** - A user-friendly document enhanced with emojis to highlight key points.
2. **DOKU.md** - A detailed, technical document for in-depth understanding.

## Features 🌟

- **Automated File Processing**: Iterates through all files in a directory, extracting text for analysis.
- **Integration with Ollama**: Uses advanced machine learning models to generate concise summaries.
- **Dual Documentation**: Generates both a simple README and a comprehensive technical document.

## Prerequisites 📋

- Python 3.8 or higher
- Access to the Ollama API
- Required Python packages: `json`, `os`, `sys`, `traceback`, `dotenv`

## Installation 🔧

1. Clone the repository or download the files into your working directory.
2. Install the required Python packages:
   ```bash
   pip install ollama dotenv
   ```
3. Set your Ollama API credentials in a `.env` file in the same directory as the script:
   ```plaintext
   PROJECT_PLANNER_MODEL=dolphin-mistral:latest
   CODER_MODEL=codellama:7b
   MARKDOWN_MAKER=vicuna:13b-16k
   TASKNAMER=stablelm2:1.6b-zephyr-fp16
   ```

## Usage 🚀

Run the script via the command line with the directory path as an argument:
```bash
python path_to_script.py path_to_directory
```

## Example 📖

```bash
python summarize_directory.py ./example_directory
```
This will process files in `./example_directory` and generate `README.md` and `DOKU.md` in your working directory.

## Error Handling 🚨

The script includes basic error handling to diagnose and report issues during execution. Check the console outputs and tracebacks to identify the causes of failures.

## Security Notice 🔒

Ensure that you process trusted data, as the script does not perform comprehensive security checks on the content of the files.
