# LLM RAG avec Ollama

Système de Retrieval-Augmented Generation (RAG) utilisant Ollama et Gradio pour interroger des documents PDF avec des modèles de langage locaux.

## Description

Ce projet permet d'interroger le contenu d'un document PDF en utilisant :

- **Ollama** pour les modèles de langage locaux (deepseek-r1:1.5b, gemma3n:e2b)
- **LangChain** pour le traitement des documents et la création d'embeddings
- **ChromaDB** comme base de données vectorielle
- **Gradio** pour l'interface utilisateur web

## Fonctionnalités

- 📄 Traitement automatique de documents PDF
- 🔍 Recherche sémantique dans le contenu
- 🤖 Réponses générées par des LLM locaux
- 🌐 Interface web simple et intuitive
- 💾 Base de données vectorielle persistante

## Installation

### Prérequis

1. **Ollama** installé sur votre système

   ```bash
   # Installation d'Ollama (macOS)
   curl -fsSL https://ollama.ai/install.sh | sh
   ```

2. **Modèles Ollama** requis
   ```bash
   ollama pull deepseek-r1:1.5b
   ollama pull gemma3n:e2b
   ollama pull bge-m3
   ```

### Dépendances Python

```bash
pip install ollama
pip install langchain chromadb gradio
pip install -U langchain-community
pip install pymupdf
```

## Utilisation

1. **Lancer le notebook**

   ```bash
   jupyter notebook main.ipynb
   ```

2. **Exécuter les cellules** dans l'ordre pour :

   - Installer les dépendances
   - Traiter votre document PDF
   - Créer la base de données vectorielle
   - Lancer l'interface Gradio

3. **Utiliser l'interface web** pour poser des questions sur votre document

## Structure du projet

```
llm_RAG/
├── main.ipynb              # Notebook principal
├── README.md               # Documentation
├── Rapport Alternance S6 - Téo Viglietti.pdf  # Document exemple
└── chroma_db/              # Base de données vectorielle
    ├── chroma.sqlite3
    └── ec7953eb-c7f8-43e1-b5aa-e8dcea7dd548/
```

## Configuration

### Modèles utilisés

- **Embeddings** : `bge-m3` (via Ollama)
- **Chat** : `deepseek-r1:1.5b` (tests)
- **RAG** : `gemma3n:e2b` (réponses principales)

### Paramètres de chunking

- **Taille des chunks** : 500 caractères
- **Overlap** : 100 caractères
- **Nombre de documents récupérés** : 4

## Fonctionnement

1. **Traitement du PDF** : Le document est divisé en chunks avec PyMuPDF
2. **Embeddings** : Conversion des chunks en vecteurs avec bge-m3
3. **Stockage** : Sauvegarde dans ChromaDB
4. **Recherche** : Récupération des passages pertinents
5. **Génération** : Création de la réponse avec le contexte

## Interface

L'interface Gradio permet de :

- Saisir une question en français
- Recevoir une réponse basée sur le contenu du document
- Historique des conversations

## Exemple d'utilisation

```python
# Question sur le document
question = "Application de suivi des tâches des RDG"

# Récupération des documents pertinents
docs = retriever.get_relevant_documents(question, k=4)

# Génération de la réponse
response = ollama_llm(question, combined_text)
```

## Auteur

Téo Viglietti

## Licence

Ce projet est à des fins éducatives et de démonstration.
