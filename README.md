Question 1.1/ Donner la liste des en-têtes de la réponse HTTP du serveur :
    - Connection : keep-alive
    - Date : Sun, 20 Sep 2026 10:14:06 GMT
    - Keep-Alive : timeout=5
    - Transfer-Encoding : chunked

Question 1.2/ Donner la liste des en-têtes qui ont changé depuis la version précédente :
    Il y a plus Transfer-Encoding et les deux autres qui se sont rajoutés sont :
        - Content-Lenght : 20
        - Content-Type : application/json

Question 1.3/ Que contient la réponse reçue par le client ?
    Le client reçoit une réponse vide. Le serveur ne renvoie rien, la connexion reste ouverte et le navigateur attend indéfiniment (la page tourne dans le vide).

Question 1.4/ Quelle est l’erreur affichée dans la console ? Retrouver sur https://nodejs.org/api le code d’erreur affiché.
    Error: ENOENT: no such file or directory, open 'C:\Users\mazeb\OneDrive\Bureau\Cour 2026\JS\devweb-tp5\index.html'
    Le code d'erreur est ENOENT (Error NO ENTry), ENOENT signifie "No such file or directory", le fichier index.html n'existe pas dans le dossier courant





Question 1.5/ Donner le code de requestListener() modifié avec gestion d’erreur en async/await.
    async function requestListener(_request, response) {
    try {
        const contents = await fs.readFile("index.html", "utf8");
        response.setHeader("Content-Type", "text/html");
        response.writeHead(200);
        return response.end(contents);
    } 
    catch (error) {
        console.error(error);
        response.writeHead(500);
        return response.end("<html><p>500: INTERNAL SERVER ERROR</p></html>");
        }
    }