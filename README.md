# devweb-tp5

## Partie 1 : serveur HTTP natif Node.js

### Question 1.1
En-têtes de la réponse HTTP du serveur :
- Connection : keep-alive
- Date : Sun, 20 Sep 2026 10:14:06 GMT
- Keep-Alive : timeout=5
- Transfer-Encoding : chunked

### Question 1.2
En-têtes qui ont changé depuis la version précédente :
- Transfer-Encoding : supprimé
- Content-Length : 20 (ajouté)
- Content-Type : application/json (ajouté)

### Question 1.3
Le client reçoit une réponse vide. Le serveur ne renvoie rien, la connexion reste ouverte et le navigateur attend indéfiniment (la page tourne dans le vide).

### Question 1.4
L'erreur affichée est :
Error: ENOENT: no such file or directory, open 'C:\Users\mazeb\...\index.html'

Le code d'erreur est ENOENT (Error NO ENTry), qui signifie "No such file or directory" : le fichier index.html n'existe pas dans le dossier courant.

### Question 1.5
javascript
async function requestListener(_request, response) {
  try {
    const contents = await fs.readFile("index.html", "utf8");
    response.setHeader("Content-Type", "text/html");
    response.writeHead(200);
    return response.end(contents);
  } catch (error) {
    console.error(error);
    response.writeHead(500);
    return response.end("<html><p>500: INTERNAL SERVER ERROR</p></html>");
  }
}

### Question 1.6
Les deux commandes ont modifié le fichier package.json en ajoutant :
- cross-env dans **dependencies (car installé avec --save)
- nodemon dans devDependencies (car installé avec --save-dev)

Elles ont aussi créé :
- le dossier node_modules/
- le fichier package-lock.json

Différence dependencies / devDependencies :
- dependencies : nécessaires en production
- devDependencies : nécessaires uniquement en développement (outils)

### Question 1.7
- http-dev : utilise nodemon + NODE_ENV=development. Le serveur redémarre automatiquement à chaque modification de fichier.
- http-prod : utilise node directement + NODE_ENV=production. Aucun redémarrage automatique, il faut arrêter et relancer manuellement.
- cross-env sert à définir la variable NODE_ENV de manière portable (Windows/Linux/macOS).

### Question 1.8
localhost:8000/index.html (200): retourne le contenu de la page index
localhost:8000/random.html (200): me retourne un nombre aléatoire
localhost:8000/ (404): retourne NOT FOUND 
localhost:8000/dont-exist (404): retourne NOT FOUND 


## Partie 2 : framework Express

### Question 2.1

express : "^5.2.1" https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Server-side/Express_Nodejs/Introduction
http-errors : "^2.0.1" https://github.com/jshttp/http-errors
loglevel : "^1.9.2" https://github.com/pimterry/loglevel
morgan : "^1.12.1" https://github.com/expressjs/morgan

### Question 2.2
- localhost:8000 : affiche l'index
- localhost:8000/index.html : affiche l'index aussi
- localhost:8000/random/5 : affiche aussi correctement les 5 nombres aléatoires

### Question 2.3
Entête des reponses d'express qui se sont rajouté :
- accept-ranges : bytes
- cache-control : public, max-age=0
- etag : W/"50-AbGuiPL1+F1ecMLmpdZXTKkxp9g"
- last-modified : Sun, 20 Sep 2026 11:11:41 GMT
- x-powered-by : Express

### Question 2.4
L'évenement listening est déclenché, dès que j'ai fait les modification dans le fichier server-express.mjs et sauvegardé.

### Question 2.5
L'option est index. Elle est activée par défaut avec la valeur "index.html".
Le middleware express.static("static") sert automatiquement le fichier index.html quand on demande le dossier racine /, c'est-à-dire qu'il fait une correspondance automatique entre l'URL "/" et le fichier "static/index.html".

### Question 2.6
- refresh normal sur style.css → 304 Not Modified : le navigateur utilise son cache
- refresh forcé sur style.css → 200 OK : le navigateur ignore le cache et retélécharge tout

### Question 2.7
Oui l'affichage change entre le mode prod et dev. Avec le mode dev on a toute les trace des erreurs