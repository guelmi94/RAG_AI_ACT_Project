# RAG_AI_ACT_Project

## Description du Projet

Ce projet implémente un système de **Retrieval Augmented Generation (RAG)** pour interagir intelligemment avec le document **"AI Act" de l'Union Européenne** au format PDF. L'objectif est de permettre aux utilisateurs de poser des questions en langage naturel sur le contenu du document et d'obtenir des réponses précises et contextuelles, générées par un modèle de langage (LLM) de Google Gemini.

Contrairement à une simple recherche par mots-clés, le système RAG garantit que les réponses sont basées sur des informations réellement présentes dans le document, minimisant ainsi les "hallucinations" des LLM et offrant une source vérifiable pour chaque information.

## Fonctionnalités

*   **Extraction de Texte PDF :** Lecture et extraction complètes du contenu textuel du document PDF "AI Act".
*   **Découpage Intelligent du Texte (Chunking) :** Division du texte extrait en morceaux gérables (`chunks`) avec chevauchement pour maintenir le contexte.
*   **Vectorisation Sémantique :** Conversion de chaque chunk en une représentation numérique (embedding) qui capture son sens, facilitant la recherche de similarité.
*   **Base de Données Vectorielle :** Stockage des embeddings dans une base de données vectorielle (ChromaDB en mémoire pour la démo) pour une récupération rapide et efficace.
*   **Récupération d'Informations Pertinentes :** Identification et sélection automatique des chunks du document les plus pertinents à la question posée par l'utilisateur.
*   **Génération de Réponses par LLM :** Utilisation du modèle **Google Gemini (gemini-2.0-flash)** pour générer des réponses concises et informatives, enrichies par le contexte des chunks récupérés.
*   **Transparence du Contexte :** Affichage des chunks de texte spécifiques du document qui ont été utilisés pour générer la réponse.

## Installation et Configuration

Pour exécuter ce projet localement, suivez les étapes ci-dessous. Il est **fortement recommandé** d'utiliser un environnement virtuel (tel que Conda ou `venv`) pour gérer les dépendances et éviter les conflits avec d'autres projets Python.

1.  **Cloner le Dépôt :**
    ```bash
    git clone https://github.com/guelmi94/RAG_AI_ACT_Project.git
    cd RAG_AI_ACT_Project
    ```

2.  **Créer un Environnement Conda (recommandé) :**
    Si vous utilisez Anaconda, ouvrez votre **Anaconda Prompt** et exécutez :
    ```bash
    conda create -n rag_env python=3.11
    conda activate rag_env
    ```
    Si vous préférez `venv` :
    ```bash
    python -m venv rag_env
    .\rag_env\Scripts\activate # Sur Windows
    # source rag_env/bin/activate # Sur macOS/Linux
    ```

3.  **Installer les Dépendances :**
    Avec votre environnement activé, installez toutes les bibliothèques requises :
    ```bash
    pip install PyMuPDF langchain langchain-community langchain-google-genai chromadb google-generativeai python-dotenv
    ```

4.  **Obtenir une Clé API Google Gemini :**
    *   Rendez-vous sur [Google AI Studio](https://ai.google.dev/docs/gemini_api_overview) ou la [Google Cloud Console](https://console.cloud.google.com/apis/credentials).
    *   Créez un nouveau projet si nécessaire et générez une clé API pour les modèles Gemini.
    *   **Gardez cette clé SÉCURISÉE ! Ne la mettez JAMAIS directement dans votre code ou dans un fichier versionné sur GitHub.**

5.  **Configuration de la Clé API (Sécurisé) :**
    *   Créez un fichier nommé `.env` à la racine de votre projet (au même niveau que le notebook `RAG_AI_ACT.ipynb`).
    *   Ajoutez votre clé API dans ce fichier comme suit :
        ```
        GOOGLE_API_KEY="VOTRE_CLÉ_API_GEMINI_ICI"
        ```
        (Remplacez `"VOTRE_CLÉ_API_GEMINI_ICI"` par la clé que vous avez obtenue.)
    *   **Ajoutez `.env` à votre fichier `.gitignore`** (s'il n'est pas déjà présent) pour vous assurer qu'il ne sera jamais poussé sur GitHub :
        ```
        .env
        ```

## Utilisation

Le projet est implémenté sous forme de Jupyter Notebook pour faciliter l'exécution bloc par bloc et la visualisation des étapes intermédiaires.

1.  **Placer le Document PDF :**
    Assurez-vous que le document PDF que vous souhaitez interroger (par exemple, `aiact_final_draft.pdf`) est situé au chemin spécifié dans le notebook (`pdf_document = "C:/Users/Mike0/Downloads/aiact_final_draft.pdf/aiact_final_draft.pdf"`). Modifiez ce chemin si votre fichier est ailleurs.

2.  **Lancer Jupyter Notebook :**
    Avec votre environnement `rag_env` activé, exécutez la commande :
    ```bash
    jupyter notebook
    ```
    Votre navigateur web s'ouvrira avec l'interface Jupyter.

3.  **Ouvrir et Exécuter le Notebook :**
    *   Naviguez jusqu'à `RAG_AI_ACT.ipynb` et ouvrez-le.
    *   Assurez-vous que le **noyau (kernel)** du notebook est bien défini sur votre environnement `rag_env` (vérifiez en haut à droite du notebook). Si ce n'est pas le cas, changez-le.
    *   Exécutez les cellules du notebook séquentiellement, de haut en bas. Chaque bloc est accompagné d'explications et d'affichages de progression.

## Structure du Notebook

Le notebook est décomposé en 6 blocs principaux, chacun illustrant une étape du pipeline RAG :

*   **Bloc 1 : Initialisation**
    *   Configure les imports, l'API Key, et initialise les modèles LLM et d'Embeddings.
*   **Bloc 2 : Chargement du PDF et Extraction du Texte**
    *   Lit le fichier PDF et en extrait le contenu textuel brut.
*   **Bloc 3 : Division du Texte en Chunks**
    *   Divise le texte long en segments plus petits pour un traitement efficace.
*   **Bloc 4 : Vectorisation et Stockage Vectoriel**
    *   Transforme les chunks en vecteurs numériques et les stocke dans une base de données vectorielle.
*   **Bloc 5 : Configuration de la Chaîne RAG**
    *   Construit le pipeline qui connecte le retriever (recherche de chunks pertinents) et le LLM (génération de réponse).
*   **Bloc 6 : Pose de la Question et Obtention de la Réponse**
    *   Exécute une requête, affiche la réponse du LLM et met en évidence les chunks de document utilisés pour cette réponse.
