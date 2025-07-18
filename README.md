# LLM RAG avec Ollama

Système RAG (Retrieval-Augmented Generation) pour interroger des PDFs avec Ollama + Gradio.

## � Installation Rapide

1. **Ollama + Modèles**

   ```bash
   # Installer Ollama
   curl -fsSL https://ollama.ai/install.sh | sh

   # Télécharger les modèles
   ollama pull gemma3n:e2b
   ollama pull bge-m3
   ```

2. **Dépendances Python**
   ```bash
   pip install ollama langchain chromadb gradio langchain-community pymupdf
   ```

## 📁 Structure

```
llm_RAG/
├── main.ipynb          # Notebook principal
├── pdf/               # Dossier contenant vos PDFs
└── chroma_db/         # Base vectorielle (auto-générée)
```

## 🎯 Utilisation

1. **Placez vos PDFs** dans le dossier `./pdf/`
2. **Exécutez le notebook** `main.ipynb` cellule par cellule
3. **Utilisez l'interface Gradio** pour poser vos questions

## ⚙️ Fonctionnalités

- 📄 **Multi-PDFs** : Traite automatiquement tous les PDFs du dossier
- 🔍 **Recherche vectorielle** : ChromaDB + embeddings bge-m3
- 🤖 **LLM local** : Réponses en français avec gemma3n:e2b
- 🌐 **Interface web** : Gradio simple et intuitive
- 💾 **Base persistante** : Pas besoin de retraiter à chaque fois

## 🛠️ Configuration

- **Chunks** : 500 caractères (overlap 100)
- **Recherche** : 4 documents les plus pertinents
- **Modèle** : gemma3n:e2b (français)

## 📝 Exemple

```python
# Traitement automatique des PDFs
text_splitter, vectorstore, retriever = process_all_pdfs("./pdf")

# Question
question = "Quelle est la hauteur du platane ?"
docs = retriever.get_relevant_documents(question, k=4)
response = ollama_llm(question, combine_docs(docs))
```

**Auteur** : Téo Viglietti
