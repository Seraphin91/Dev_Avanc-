Cours 1 :

# Vréation de la première version du workflow et implémentation de la Branche YouTube (Protocole oEmbed)

## Objectif
Mon objectif dans mon groupe est de récupérer automatiquement le titre et le nom du créateur d'une vidéo YouTube à partir de son lien

## Fonctionnement Technique que j'ai implémenté
1. **Routage Dynamique :** Le Switch utilise une Expression Régulière Regex pour intercepter les différents formats d'URL (`youtube.com` ou le format court `youtu.be`).
2. **Protocole oEmbed :** Au lieu de l'API officielle, le système interroge le point d'accès public oEmbed de YouTube (`https://www.youtube.com/oembed?url=...`).
3. **Extraction :** Le service renvoie instantanément un JSON propre contenant les métadonnées essentielles de la vidéo.
4. **Intégration Notion :** Injection de la variable `title` (Titre Notion), de l'URL source, et de la variable `author_name` (Nom de la chaîne) dans la case "Résumé".


* Cours 2 :

## Objectif
Mon objectif dans mon groupe est de récupérer automatiquement la dexcription et sous-titre d'une vidéo pour compléter les données et les transfromer en markdown.

## Fonctionnement Technique que j'ai implémenté
* Avec Ezno, on a changé le protcolme oEmbed par le noeud Youtube afin de récupérer plus d'infos que nous n'avions pas avant, comme les sous-titres et la description. On réléchit à peut-être intégré un agent IA pour le markdown.
* On stock le fichier markdown sur notion une fois traité
