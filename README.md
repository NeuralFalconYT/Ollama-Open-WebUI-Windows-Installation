# Ollama and Open WebUI Windows Installation Guide

This guide will walk you through setting up **Ollama** and **Open WebUI** on a Windows system. The installation will be done in a **custom folder** (e.g., on the `E:` drive) to avoid consuming space on the `C:` drive. You will also learn how to uninstall both tools when needed. This setup allows you to run open-source large language models (LLMs) **privately** and **offline** on your local machine.

---

## Prerequisites
1. **Windows OS**
2. **PowerShell and CMD** (pre-installed on Windows)
3. **Internet connection** (for initial setup and downloading models)

---

## Step 1: Install Ollama

### 1.1 Download Ollama
1. Download the Ollama installer (`ollamasetup.exe`) from the official website: [https://ollama.com/](https://ollama.com/).

### 1.2 Create a Custom Folder for Ollama
1. Create a folder on your desired drive (e.g., `E:/LLM`).
2. Inside the `E:/LLM` folder, create another folder named `ollama`. The path will look like this: `E:/LLM/ollama`.

### 1.3 Set Environment Variable
1. Open **System Properties**:
   - Right-click on **This PC** or **My Computer** and select **Properties**.
   - Click on **Advanced system settings**.
   - Under the **Advanced** tab, click on **Environment Variables**.
2. Add a new **System Variable**:
   - Variable Name: `OLLAMA_MODELS`
   - Variable Value: `E:/LLM/ollama`
3. Click **OK** to save the changes.

### 1.4 Install Ollama
1. Open **CMD** as Administrator.
2. Run the following command to install Ollama in the custom folder:
   ```cmd
   ollamasetup.exe /DIR="E:/LLM/ollama"
   ```
3. Verify the installation location:
   ```cmd
   where ollama
   ```

### 1.5 Run a Model
1. To test Ollama, run a model (e.g., `deepseek-r1:1.5b`):
   ```cmd
   ollama run deepseek-r1:1.5b
   ```
2. Exit the chat by typing `/bye`.
   #### Basic ollama commands to know
4. List all available models:
   ```cmd
   ollama list
   ```
5. Check running models:
   ```cmd
   ollama ps
   ```
6. Stop a running model:
   ```cmd
   ollama stop <model_name>
   ```
7. Delete a model:
   ```cmd
   ollama rm <model_name>
   ```

### 1.6 Uninstall Ollama
1. Stop all Ollama servers and exit any open Ollama sessions.
2. Go to **Settings** -> **Apps** -> **Installed Apps**.
3. Find **Ollama** and click **Uninstall**.
4. Remove the environment variable `OLLAMA_MODELS`:
   - Open **Environment Variables** and delete the `OLLAMA_MODELS` entry.
5. Delete the Ollama folder (`E:/LLM/ollama`) if it still exists.
6. Also Remove that System Environment Variable 'OLLAMA_MODELS'
---

## Step 2: Install Open WebUI (Without Docker) [openwebui Docs](https://docs.openwebui.com/)

### 2.1 Install UV Package Manager
1. Open **PowerShell**.
2. Run the following command to install the UV package manager:
   ```powershell
   powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
   ```
   This will install UV in the `C:` drive.

### 2.2 Create Folders for Open WebUI
1. Inside the `E:/LLM` folder, create a new folder named `open_webui`.
2. Inside `E:/LLM/open_webui`, create two subfolders:
   - `cache`: For storing Python packages.
   - `data`: For storing chat data and uploaded images.

### 2.3 Install Open WebUI

3. Run the following command to install Open WebUI:

   ```powershell
   $env:UV_CACHE_DIR = "E:/LLM/open_webui/cache";$env:DATA_DIR="E:/LLM/open_webui/data"; uvx --python 3.11 open-webui@latest serv  
   ```
   This will install Open WebUI , store all Python packages in the `cache` folder and keep all the chats in `data` folder

5. Once the installation is complete, Open WebUI will start a local server. Access it using:
   - If `http://0:0:0:8080` does not work, use:

     - `http://127.0.0.1:8080/`


### 2.4 Run Open WebUI in the Future
To start Open WebUI again, run the following command:
```powershell
$env:DATA_DIR="E:/LLM/open_webui/data"; uvx --python 3.11 open-webui@latest serve
```

### 2.5 Uninstall Open WebUI
1. Open **PowerShell**.
2. Clean the Python packages cache:
   ```powershell
   uv clean --cache-dir "E:/LLM/open_webui/cache"
   ```
3. Locate the UV installation path:
   ```powershell
   Get-Command uv
   ```
   Example output:
   ```
   C:\Users\<username>\.local\bin\uv.exe
   ```
4. Remove the UV executable:
   ```powershell
   Remove-Item -Path "C:\Users\<username>\.local\bin\uv.exe" -Force
   ```
5. Verify that UV is uninstalled:
   ```powershell
   uv
   ```
   If UV is uninstalled, you will see an error message.
6. Manually delete the Open WebUI data folder:
   ```
   E:/LLM/open_webui/data
   ```




## **To Use Ollama and Open WebUI Again**

### **Steps**
1. **Start Ollama**:
   ```bash
   ollama run deepseek-r1:1.5b
   ```
   Exit with `/bye`.

2. **Run Open WebUI**:
   ```powershell
   $env:UV_CACHE_DIR = "E:/LLM/open_webui/cache"; $env:DATA_DIR = "E:/LLM/open_webui/data"; uvx --python 3.11 open-webui@latest serve
   ```

---

### **Notes**
- Set `UV_CACHE_DIR` and `DATA_DIR` to your desired paths.
- Ensure directories exist before running.

---



## Conclusion
You have successfully set up **Ollama** and **Open WebUI** on your local machine. This setup allows you to run LLMs **privately** and **offline**. You can also uninstall both tools when they are no longer needed. Enjoy experimenting with open-source LLMs!
