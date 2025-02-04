# A Simple Voice Assistant Script

English | [简体中文](README-CN.md)

This is a simple Python script project that allows dialogue with a local large language model through voice.

The voice recognition part of this project is from the [Apple MLX example repo](https://github.com/ml-explore/mlx-examples/tree/main/whisper), and the textual responses are generated using the Yi model from [01.AI](https://www.lingyiwanwu.com). For more details, see the [Acknowledgments](## Acknowledgments) section.

### File Structure

```bash
├───main.py
├───models
├───prompts
├───recordings
├───tools
│   └───list_microphones.py
├───whisper
```

This project is a single-script project, with main.py containing all program logic. The `models/` folder stores model files. `prompts/` contains prompt words. `recordings/` holds temporary recordings. `tools/list_microphones.py` is a simple script to view the microphone list, used in `main.py` to specify the microphone number. `whisper/` is from the [Apple MLX example repo](https://github.com/ml-explore/mlx-examples/tree/main/whisper), used for recognizing user's voice input.

## Installation Guide

This project is based on the Python programming language, and the Python version used for program operation is 3.11.5. It is recommended to configure the Python environment using [Anaconda](https://www.anaconda.com). The following setup process has been tested and passed on macOS systems. Windows and Linux can use speech_recognition and pyttsx3 to replace the whisper and say commands mentioned below. The following are console/terminal/shell commands.

### Environment Configuration
```
conda create -n VoiceAI python=3.11
conda activate VoiceAI
pip install -r requirements.txt
CMAKE_ARGS="-DLLAMA_METAL=on" pip install llama-cpp-python

# Install audio processing tools
brew install portaudio
pip install pyaudio
```

### Model Files
The model files are stored in the `models/` folder and specified in the script via the `MODEL_PATH` variable.
It is recommended to download the gguf format models from TheBloke and XeIaso, where the 6B model has a smaller memory footprint:
- [TheBloke/Yi-34B-Chat-GGUF](https://huggingface.co/TheBloke/Yi-34B-Chat-GGUF/blob/main/yi-34b-chat.Q8_0.gguf)
- [XeIaso/Yi-6B-Chat-GGUF](https://huggingface.co/XeIaso/yi-chat-6B-GGUF/blob/main/yi-chat-6b.Q8_0.gguf)
The voice recognition model is by default stored in `models/whisper-large-v3/`, specified in the script via `WHISP_PATH`. The [version](https://huggingface.co/mlx-community/whisper-large-v3-mlx) converted by mlx-community can be directly downloaded.

#### Model Files

The voice recognition part of this project is based on OpenAI's whisper model, its implementation comes from the [Apple MLX example repo](https://github.com/ml-explore/mlx-examples/tree/main/whisper). The version used in this project is from January 2024, #80d1867. In the future, users can fetch new versions as needed.

The responses in this project are generated by the large language model Yi from [01.AI](https://www.lingyiwanwu.com), where Yi-34B-Chat is more powerful. The [8-bit quantized version made by TheBloke](https://huggingface.co/TheBloke/Yi-34B-Chat-GGUF) has a memory footprint of 39.04 GB
and is recommended for use if hardware conditions permit. This model runs locally based on the [LangChain](https://www.langchain.com) framework and [llama.cpp by Georgi Gerganov](https://github.com/ggerganov/llama.cpp).

Thank you to all selfless programmers for their contributions to the open-source community!
