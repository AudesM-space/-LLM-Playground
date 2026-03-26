# LLM Playground

## Description
Ce projet est un **playground pour expérimenter avec des modèles de langage (LLM)** en Python.  
Il illustre comment :
- **Compter les tokens** d’un prompt avec la librairie `tiktoken`.
- **Initialiser un modèle OpenAI** via `LangChain`.
- **Interagir avec Ollama** pour invoquer des modèles alternatifs (`ChatOllama`, `ChatLlama`).
- Tester des prompts en français et obtenir des réponses formatées en Markdown.

---

## PARTIE I: Fonctionnalités principales

### 1. Tokenisation avec `tiktoken`
```python
import tiktoken

tokenizer = tiktoken.encoding_for_model("gpt-4o")
prompt = "Vous êtes un expert dans le domaine de l'analyse des sentiments"
tokens = tokenizer.encode(prompt)

print(tokens)       # liste des tokens
print(len(tokens))  # nombre de tokens
```
### 2. Fonction utilitaire pour compter les tokens
```python
def tokens_count(prompt:str, model:str="o200k_base"):
    tokenizer = tiktoken.get_encoding(model)
    return len(tokenizer.encode(prompt))

print(tokens_count(prompt="Vous êtes un assistant "))  # Exemple : 5
```
### 3. Initialisation d’un modèle OpenAI via LangChain
```python
from langchain_openai import ChatOpenAI
from dotenv.ipython import load_dotenv

load_dotenv(override=True)  # charge les variables d'environnement
llm = ChatOpenAI(model="gpt-4o", temperature=0)
```
### 4. Utilisation de modèles Ollama
```python
from langchain_ollama import ChatOllama
llm_ollama = ChatOllama(model="qwen3-v1:235b-cloud")

```
- Exemple d’invocation :
```python
rep = llm_ollama.invoke([
    {"role":"system","content":"You are a helpful assistant. The output should be in Markdown"},
    {"role":"user","content":"comment peux tu m'aider"}
])
print(display(Markdown(response.content)))
```

## PARTIE II : Installation 
### 1. Créer un environnement virtuel
```bash
uv init
```

```bash
.venv\Scripts\activate
```

```bash
uv add ipkernel

uv add tiktoken
```

### 2. Installation des dépendances 
```bash
pip install tiktoken langchain-openai langchain-ollama python-dotenv
```
### 3. Configuration des variables d'environnement 
Il s'agit de créer un fichier .env avec la clé OpenAI 
```code
OPENAI_API_KEY=Sk-xxxx
```
## PARTIE III : Intéragir avec Ollama
<img width="1022" height="796" alt="image" src="https://github.com/user-attachments/assets/4f92f268-846a-4a45-ba52-39d1d009aa59" />
<img width="1013" height="803" alt="image" src="https://github.com/user-attachments/assets/1cc21484-6fc5-4657-ac4a-d07ee8e11410" />
