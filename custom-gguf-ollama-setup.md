

# How to Install a Custom GGUF Model in Ollama

This guide provides a step-by-step process for installing and using any custom GGUF model with Ollama. In this example, we will demonstrate how to install and use the `DarkIdol-Llama-3.1-8B-Instruct-1.2-Uncensored-IQ2_M.gguf` model, but you can follow these instructions for any GGUF model.

---

## Prerequisites

Before proceeding, ensure that you have the following:

1. **Ollama Installation**: Ollama must be installed on your system. You can follow the [Ollama Installation Guide for Windows](https://github.com/NeuralFalconYT/Ollama-Open-WebUI-Windows-Installation) for detailed instructions on how to install Ollama with a custom path.

2. **GGUF Model**: You will need a GGUF model file. For this demonstration, we will use the `DarkIdol-Llama-3.1-8B-Instruct-1.2-Uncensored-IQ2_M.gguf` model, but you can use any other GGUF model of your choice.

3. **Download GGUF Model**: Download the model from [Hugging Face - DarkIdol-Llama-3.1-8B-Instruct-1.2-Uncensored-GGUF](https://huggingface.co/bartowski/DarkIdol-Llama-3.1-8B-Instruct-1.2-Uncensored-GGUF/tree/main).

---

## Steps to Install and Use a Custom GGUF Model in Ollama

### 1. **Create a Directory for Models**

If you haven’t already, create a folder where Ollama will store your models. For example, you can create the following directory:

* `E:\LLM\ollama\models`

### 2. **Download the GGUF Model**

Download the desired GGUF model (for example, `DarkIdol-Llama-3.1-8B-Instruct-1.2-Uncensored-IQ2_M.gguf`) from the provided link on Hugging Face or from your preferred source. Save the model file in the `E:\LLM\ollama\models` folder.

### 3. **Create the Modelfile**

The `Modelfile` is essential for configuring the model within Ollama. This file should be placed in the same directory as your model file (`E:\LLM\ollama\models`).

1. Create a new file named **`Modelfile`** (without any extension).
2. Open the file and add the following content:

```dockerfile
FROM ./DarkIdol-Llama-3.1-8B-Instruct-1.2-Uncensored-IQ2_M.gguf

PARAMETER num_ctx 4096
PARAMETER temperature 0.7

SYSTEM You are Mario from Super Mario Bros, acting as an assistant.

TEMPLATE """<|system|>{{ .System }}<|end_header_id|>
<|user|>{{ .Prompt }}<|end_header_id|>
<|assistant|>{{ .Response }}<|end_header_id|>"""
```

**Note**: You can replace the model name and parameters as needed for the specific GGUF model you are using.

### 4. **Run the Model with Ollama**

Once you have set up the model and `Modelfile`, follow these steps to create and run the model in Ollama:

1. **Open a Command Prompt** and navigate to the `models` directory:

   ```bash
   cd E:\LLM\ollama\models
   ```

2. **Create the Model** in Ollama by running the following command:

   ```bash
   ollama create darkidol -f Modelfile
   ```

   This will register the `darkidol` model using the custom GGUF model specified in the `Modelfile`.

3. **Run the Model** with the following command:

   ```bash
   ollama run darkidol
   ```

   Ollama will now load the custom GGUF model and begin running it. You can interact with the model directly via the command line.

---

## Troubleshooting

* **Error: pull model manifest: file does not exist**: Ensure that the GGUF model file is correctly placed in the same folder as the `Modelfile` and that the path in the `Modelfile` is accurate.
* **Model Path Issues**: Double-check that the model path in the `Modelfile` correctly points to the location of the `.gguf` file.

---

## Conclusion

By following this guide, you have successfully installed and configured a custom GGUF model in Ollama. In this example, we used the `DarkIdol-Llama-3.1-8B-Instruct-1.2-Uncensored-IQ2_M.gguf` model, but you can use any other GGUF model by modifying the model file path and parameters in the `Modelfile`.

Feel free to modify the parameters and configurations in the `Modelfile` to suit your specific use case and requirements.

---


