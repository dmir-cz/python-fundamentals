# Python Development: From Installation to Secure Coding

## Installing Python

Installing Python on macOS and Linux is generally straightforward, as both systems usually come with some version of Python already installed. However, you'll likely want the latest version and the ability to manage it easily.

### On macOS

The best way to manage Python on a Mac is via **Homebrew**, the "missing package manager for macOS."

1.  **Install Homebrew** (if you don't have it):
    Open your Terminal and paste:
    `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`
2.  **Install Python:**
    Once Homebrew is ready, simply run:
    `brew install python`
3.  **Verify:**
    Check the version by typing:
    `python3 --version`



---

### On Linux (Ubuntu/Debian)

Most Linux distributions come with Python, but to get the latest version or specific development tools, you use `apt`.

1.  **Update your package list:**
    `sudo apt update`
2.  **Install Python:**
    `sudo apt install python3`
3.  **Install Pip** (The package manager):
    You'll almost certainly need this to install libraries:
    `sudo apt install python3-pip`



---

### A Better Way: `pyenv`
If you plan on doing serious development, I highly recommend using **pyenv**. It allows you to switch between multiple versions of Python (e.g., 3.10, 3.11, 3.12) effortlessly without breaking your computer's system Python.

* **Why use it?** Some system tools on Linux/Mac rely on a specific version of Python. If you accidentally change or break the "system" version, you can mess up your OS. `pyenv` keeps your "work" Python completely separate.



---

### Summary Table

| OS | Recommended Method | Command |
| :--- | :--- | :--- |
| **macOS** | Homebrew | `brew install python` |
| **Linux** | APT (Package Manager) | `sudo apt install python3` |
| **Advanced** | pyenv | `pyenv install 3.x.x` |

## Virtual Environments

Think of a Python virtual environment as a private workspace for a specific project. Without one, every library you install goes into a "global" bucket. This might work for a while, but eventually, it leads to the software equivalent of a messy roommate situation.

### Why You Need One
* **Avoid Dependency Hell:** Project A might need Version 1.0 of a library, while Project B needs Version 2.0. A virtual environment allows both to coexist on the same computer without crashing into each other.
* **Keep Your System Clean:** You prevent your computer’s global Python installation from becoming cluttered with hundreds of packages you only used once.
* **Easier Collaboration:** By using an environment, you can generate a list of exactly what your project needs (usually a `requirements.txt` file), making it easy for someone else to run your code.



---

### How to Do It (The Quick Way)

Most modern Python installations come with a built-in tool called `venv`. Here is the standard workflow using your terminal or command prompt:

#### 1. Create the environment
Navigate to your project folder and run:
`python -m venv .venv`
*(This creates a folder named `.venv` that holds your isolated Python copy.)*

#### 2. Activate it
You need to tell your terminal to start using that specific environment.
* **Windows:** `.venv\Scripts\activate`
* **macOS / Linux:** `source .venv/bin/activate`

> **Note:** Once activated, you’ll usually see `(.venv)` appear at the start of your command prompt line.

#### 3. Install your packages
Now, any `pip install` command will stay contained within that folder.
`pip install requests`

#### 4. Leave when finished
When you're done working, just type:
`deactivate`

---

## Sharing Your Setup

To share your environment settings, you’ll use a **requirements file**. This is essentially a shopping list of every library and specific version your project needs to run correctly.

### How to Generate and Use a `requirements.txt`

Once your virtual environment is active and you’ve installed your libraries, follow these steps:

#### 1. Freeze your dependencies
Run this command to create the list:
`pip freeze > requirements.txt`
*This looks at everything currently installed in your virtual environment and saves the names and version numbers into a file named `requirements.txt`.*

#### 2. Share the file
When you give your code to a friend or upload it to GitHub, you include that `requirements.txt` file. You **do not** share the `.venv` folder itself (it's bulky and specific to your operating system).

#### 3. Reconstruct the environment
When your friend gets your project, they create their own fresh virtual environment and run:
`pip install -r requirements.txt`
*Pip will read the list and automatically install the exact same versions you were using.*

---

## Professional Project Cleanup

### Pro-Tip: The `.gitignore`
If you are using **Git**, make sure to add `.venv/` to your `.gitignore` file. You want to track the *instructions* (the requirements file), not the actual *environment* files.

Keeping your repository clean is a hallmark of a professional workflow. You want to share your code and your "shopping list" (`requirements.txt`), but you definitely don't want to upload the thousands of tiny files that make up the virtual environment itself.

### The Standard Python `.gitignore`

Create a file named `.gitignore` (note the leading dot) in your project's root directory and paste this in. This tells Git to ignore the environment folders and common "junk" files:

```text
# --- Python ---
__pycache__/
*.py[cod]
*$py.class
*.so
.Python
build/
develop-eggs/
dist/
downloads/
eggs/
.eggs/
lib/
lib64/
parts/
sdist/
var/
wheels/
share/python-wheels/
*.egg-info/
.installed.cfg
*.egg
MANIFEST

# --- Virtual Environments ---
.venv/
venv/
ENV/
env/
pip-log.txt
pip-delete-this-directory.txt

# --- macOS ---
.DS_Store
.AppleDouble
.LSOverride
Icon
._*
.Spotlight-V100
.Trashes
*.lp

# --- VS Code ---
.vscode/*
!.vscode/settings.json
!.vscode/tasks.json
!.vscode/launch.json
!.vscode/extensions.json
*.code-workspace
.history/

# --- Environment Variables (Security) ---
.env
.venv
env.bak
*.rel
```

---

### Why this matters
By ignoring the `.venv` folder, you ensure that:
1. **Your Repo stays small:** Virtual environments can be hundreds of megabytes.
2. **Cross-platform compatibility:** A virtual environment created on Windows won't work on a Mac, so everyone should build their own locally using your `requirements.txt`.
3. **Security:** It prevents you from accidentally uploading sensitive API keys if you store them in an environment configuration.

---

## Security & Environment Variables

Think of a `.env` file as a digital vault. In professional coding, you never want to "hardcode" sensitive information like API keys, database passwords, or secret tokens directly into your script. If you do, and you upload that script to GitHub, everyone in the world can see (and use) your credentials.

### How to use a `.env` file

#### 1. Create the File
In your project's root folder, create a file named exactly `.env` (no filename, just the extension). Add your secrets inside like this:
```text
DATABASE_URL=postgres://user:password@localhost:5432/mydb
STRIPE_API_KEY=your_key
SECRET_DEBUG_MODE=True
```

#### 2. Install the Handler
To read these variables in Python, the most popular tool is `python-dotenv`. Install it in your virtual environment:
`pip install python-dotenv`

#### 3. Access Secrets in Your Code
Now, you can pull those values into your Python script without ever typing the actual password in the code itself:

```python
import os
from dotenv import load_dotenv

# This loads the variables from .env into the system's environment
load_dotenv()

# Now you can access them like this:
api_key = os.getenv("STRIPE_API_KEY")
db_url = os.getenv("DATABASE_URL")

print(f"Connecting to database at {db_url}...")
```


---

### Why this is a "Must-Do"
* **Security:** Since you already added `.env` to your `.gitignore` in the previous step, your secrets stay on your machine and never touch the cloud.
* **Flexibility:** You can have a `.env` file on your laptop for testing and a different `.env` file on your production server with the "real" credentials, and the code remains exactly the same.

--- 

Since we’ve already set up your virtual environment and your `.env` file, let’s tie it all together with a practical example. We’ll write a script that "connects" to a hypothetical Weather API.

### 1. Update your `.env` file
First, add a fake API key to your `.env` file so we have something to pull from:
```text
WEATHER_API_KEY=abc123supersecret
DEBUG_MODE=True
```

### 2. The Python Script
Create a file named `main.py` and use this code. It demonstrates how to safely grab those variables and use them in a function.

```python
import os
from dotenv import load_dotenv

# 1. Load the variables from the .env file into the environment
load_dotenv()

def fetch_weather(city):
    # 2. Retrieve the secret key using os.getenv
    api_key = os.getenv("WEATHER_API_KEY")
    debug = os.getenv("DEBUG_MODE") == "True"

    if debug:
        print(f"--- DEBUG: Using API Key {api_key[:4]}**** ---")

    # In a real app, you'd use the 'requests' library here
    print(f"Fetching weather for {city}...")
    
    # Mock response
    return {"city": city, "temp": "22°C", "condition": "Sunny"}

# Execution
if __name__ == "__main__":
    weather_data = fetch_weather("London")
    print(f"The weather in {weather_data['city']} is {weather_data['temp']}.")
```



---

### Why this is the "Golden Standard"
* **The Code is Portable:** You can share `main.py` and `requirements.txt` with anyone.
* **The Secret is Private:** Since `.env` is in your `.gitignore`, your `WEATHER_API_KEY` never leaves your computer.
* **The Environment is Isolated:** Because you are using a `.venv`, you know exactly which version of `python-dotenv` is being used.

### Quick Checklist for your Project Folder:
* `main.py` (Your code)
* `.env` (Your secrets - **Hidden/Ignored**)
* `.gitignore` (The rules for Git)
* `requirements.txt` (The library list)
* `.venv/` (The actual environment - **Hidden/Ignored**)

 