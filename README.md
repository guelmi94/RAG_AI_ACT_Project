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
