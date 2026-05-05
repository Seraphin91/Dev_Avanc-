# Cours 1 :

# Vréation de la première version du workflow et implémentation de la Branche YouTube (Protocole oEmbed)

## Objectif
Mon objectif dans mon groupe est de récupérer automatiquement le titre et le nom du créateur d'une vidéo YouTube à partir de son lien

## Fonctionnement Technique que j'ai implémenté
1. **Routage Dynamique :** Le Switch utilise une Expression Régulière Regex pour intercepter les différents formats d'URL (`youtube.com` ou le format court `youtu.be`).
2. **Protocole oEmbed :** Au lieu de l'API officielle, le système interroge le point d'accès public oEmbed de YouTube (`https://www.youtube.com/oembed?url=...`).
3. **Extraction :** Le service renvoie instantanément un JSON propre contenant les métadonnées essentielles de la vidéo.
4. **Intégration Notion :** Injection de la variable `title` (Titre Notion), de l'URL source, et de la variable `author_name` (Nom de la chaîne) dans la case "Résumé".


# Cours 2 :

Objectif : Récupérer des fichiers que l'on transforme au format markdown, les diviser en chunks de données et les enregistrer

**Ce que j'ai fait :** J'ai créé deux noeuds de extract. Le premier permet de prendre les données brutes en CSV  de tout transformer en un format Markdown propre pour la suite et l'enregistrer dans le google docs. J'ai également mis en place la récupération de fichiers déjà transformés en markdown pour les enregistrer. 

**Comment j'ai fait ça :**

**Le CSV :** J'ai utilisé le noeud "Extract from CSV" pour lire les tableaux ligne par ligne.

**Le Script :** J'ai écrit un code en JavaScript qui rassemble toutes les lignes du tableau et les transforme en un seul gros document texte, avec un titre ## pour chaque ligne.

**Les fichiers Markdown** J'ai utilisé le noeud "Extract from Markdown" pour lire le fichier déjà transformer.

**Les galères que j'ai dû régler :**

**L'agrégation des données :** Le gros problème avec le CSV, c'est que n8n sort 50 éléments différents s'il y a 50 lignes. J'ai dû coder une boucle pour fusionner ces 50 lignes en un seul grand texte avant de l'envoyer pour le découpage final. Il fallait également penser à diviser les données Markdown en chunk pour la suite.

# Cours 3 :

Objectif : Récupérer les chunks que l'on a créé dans le cours 2, les enregeistrer dans une base vectoriel VVS et refonte de la transformation de fichier en Markdown avec des github publique pour être plus éfficace et interprétation des données avec un autre workflow.

Contexte : On utilise l'ia Gemini pour la vectorisation des données

**L'agrégation des données :** Assez compliqué de réussir a correctment vectorisé le données

Chez moi, j'ai travaillé sur le stockage Vectoriel avec Weaviate & Gemini Embeddings

Une fois les chunks propres et structurés faits par mes camardes dans le workflow, il faut les transformer en vecteurs mathématiques (Embeddings) pour permettre la recherche sémantique par le chat bot et les stocker dans la base vectorielle

Nous avons déployé une instance **Weaviate** en local via Docker sur n8n pour le stockage. Nous avons choisi Weaviats pour sa légèreté, sa rapidité et son intégration native parfaite avec n8n.

Pour le modèle d'Embedding, comme expliqué au dessus nous avons utilisé l'API Google avec le modèle `models/embedding-001`.

Le pipeline d'ingestion est configuré pour dissocier strictement le contenu textuel (`pageContent`) des métadonnées (`ID`, `source`). Cette approche garantit que seule la donnée utile est vectorisée, optimisant ainsi la précision des calculs et réduisant la consommation de tokens, tout en conservant une traçabilité totale sur l'origine des documents.
