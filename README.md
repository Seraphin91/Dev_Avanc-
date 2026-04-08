# 📺 Documentation : Branche YouTube (Protocole oEmbed)

## 🎯 Objectif
Récupérer automatiquement le titre et le nom du créateur d'une vidéo YouTube à partir de son lien

## ⚙️ Fonctionnement Technique
1. **Routage Dynamique :** Le Switch utilise une Expression Régulière (Regex) pour intercepter les différents formats d'URL (`youtube.com` ou le format court `youtu.be`).
2. **Protocole oEmbed :** Au lieu de l'API officielle, le système interroge le point d'accès public oEmbed de YouTube (`https://www.youtube.com/oembed?url=...`).
3. **Extraction :** Le service renvoie instantanément un JSON propre contenant les métadonnées essentielles de la vidéo.
4. **Intégration Notion :** Injection de la variable `title` (Titre Notion), de l'URL source, et de la variable `author_name` (Nom de la chaîne) dans la case "Résumé".

## 🚧 Difficultés Rencontrées & Solutions
* **Complexité des URL :** Les liens YouTube partagés varient énormément.
* **Solution apportée :** Création d'une règle Regex robuste pour englober toutes les variantes.
* **Limitation du Résumé :** Le protocole oEmbed ne fournit pas la description ou les sous-titres de la vidéo.