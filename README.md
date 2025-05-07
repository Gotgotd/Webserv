# Webserv

> **Versions**: [English](#webserv) | [Français](#webserv-fr)

## Table of Contents

- [Introduction](#introduction)
- [Features](#features)
- [Usage](#usage)
- [Configuration](#configuration)
- [Request Handling](#request-handling)
- [Error Handling](#error-handling)
- [Supported HTTP Methods](#supported-http-methods)

---

## Introduction

**Webserv** is an Ecole 42 project that involves building a simple HTTP server in C++98. Inspired by Nginx, Webserv handles client requests, serves static files, and supports dynamic content processing. Through **Webserv**, you will gain hands-on experience with socket programming, HTTP parsing, multiplexing, and server configurations. With two great teammates, Kelly Brener-Raffali [https://github.com/KellyBRENER] and Daram Bae [https://github.com/darambae], we successfully completed this team project with a score of 125%.
For the full history of the project, you can refer to Daram's repository : [https://github.com/darambae/Webserv]

---

## Features

- **Multi-Client Handling**: Uses non-blocking sockets and `poll()` for handling multiple clients simultaneously.
- **HTTP/1.1 Support**: Implements core HTTP features such as request parsing, response handling, and status codes.
- **Configurable Server**: Reads settings from a configuration file to define server behavior (ports, routes, error pages, etc.).
- **Static File Serving**: Serves HTML, CSS, JavaScript, and other static resources.
- **CGI Support**: Executes scripts like PHP or Python via the Common Gateway Interface (CGI).
- **Error Management**: Returns proper HTTP status codes for incorrect requests or missing resources.

---

## Usage

To compile and run the server:

```bash
make
./webserv config/filename
```

**Examples**:

- Starting the server with a configuration file:
  ```bash
  ./webserv config/filename
  ```
- Sending a GET request to fetch an HTML file:
  ```bash
  curl http://localhost:8080/
  ```
- Sending a POST request to upload data:
  ```bash
  curl -X POST -d "filename=test" http://localhost:8080/upload
  ```

---

## Configuration

Webserv uses a configuration file to define:

- **Listening Ports**: Specify which ports the server should listen on.
- **Server Blocks**: Define multiple virtual hosts.
- **Root Directory**: Set the document root for serving files.
- **Error Pages**: Customize responses for different HTTP status codes.
- **CGI Scripts**: Configure paths for executing scripts.

**Example Configuration File:**

```conf
server {
    listen 8080;
    server_name myserver;
    root /var/www/html;
    index index.html;
    error_page 404 /errors/404.html;
    
    location /cgi-bin/ {
        cgi_pass /usr/bin/python3;
        cgi_extension .py;
    }
}
```

---

## Flowchart
![Flowchart](documentation/Flowchart.jpg)

## Request Handling

1. **Client Connection**: The server accepts incoming TCP connections.
2. **Request Parsing**: Reads and parses the HTTP request (method, headers, body).
3. **Routing**: Matches the request URL with configured routes.
4. **Response Generation**:
   - Static files are read and returned.
   - CGI scripts are executed, and output is returned.
   - Proper status codes are sent based on request validity.
5. **Response Delivery**: The response is sent back to the client.
6. **Connection Closure**: The connection is closed if needed.

---

## Error Handling

- **400 Bad Request**: Invalid or malformed request.
- **404 Not Found**: Requested file or directory does not exist.
- **405 Method Not Allowed**: HTTP method not supported.
- **408 Request Timeout**: The server timed out waiting for the client to send a complete request within the allowed time.
- **413 Payload Too Large**: The server is refusing to process a request because the request payload exceeds the server's configured limit.

---

## Supported HTTP Methods

### `GET`

- **Usage**: Requests a resource from the server.
- **Example**:
  ```bash
  curl http://localhost:8080/
  ```

### `POST`

- **Usage**: Sends data to the server (e.g., form submissions, file uploads).
- **Example**:
  ```bash
  curl -v -F "avatar=@408.jpg" http://localhost:8080/upload
  ```

### `DELETE`

- **Usage**: Requests the removal of a resource from the server.
- **Example**:
  ```bash
  curl -X DELETE http://localhost:8080/upload/coton.jpg -d "fileName=coton.jpg"
  ```

---

# Webserv FR

## Table des Matières

- [Introduction](#introduction)
- [Fonctionnalités](#fonctionnalités)
- [Configuration](#configuration)
- [Traitement des Requêtes](#traitement-des-requêtes)
- [Méthodes HTTP Prises en Charge](#méthodes-http-prises-en-charge)

## Introduction

**Webserv** est un projet de l'École 42 visant à développer un serveur HTTP simple en C++98. Inspiré de Nginx, Webserv gère les requêtes clients, sert des fichiers statiques et prend en charge le traitement dynamique des contenus.

Avec mes deux coéquipieres, Kelly Brener-Raffali [https://github.com/KellyBRENER] et Daram Bae [https://github.com/Gotgotd], nous avons réussi ce projet d'équipe avec un score de 125 %.
Pour l'historique complet du projet, vous pouvez vous référer au repository de Daram : [https://github.com/darambae/Webserv]

---

## Fonctionnalités

- **Gestion Multi-Clients** : Utilisation de sockets non bloquants et de `poll()`.
- **Support HTTP/1.1** : Implémente les fonctionnalités de base du protocole HTTP.
- **Configuration Personnalisable** : Lecture d'un fichier de configuration pour définir les paramètres du serveur.
- **Support CGI** : Exécution de scripts PHP ou Python via CGI.
- **Gestion des Erreurs** : Réponses adaptées avec les codes HTTP appropriés.

---

## Configuration

**Exemple de fichier de configuration :**

```conf
server {
    listen 8080;
    server_name monserveur;
    root /var/www/html;
    index index.html;
    error_page 404 /errors/404.html;
}
```

---

## Traitement des Requêtes

1. **Connexion Client** : Acceptation de la connexion.
2. **Analyse de la Requête** : Lecture et traitement des entêtes HTTP.
3. **Routage** : Correspondance de l'URL avec les routes configurées.
4. **Génération de la Réponse** :
   - Envoi d'un fichier statique.
   - Exécution d'un script CGI.
   - Gestion des codes d'erreur.
5. **Envoi de la Réponse** : Transmission au client.
6. **Fermeture de la Connexion**.

---

## Méthodes HTTP Prises en Charge

### `GET`

- **Utilisation** : Récupération d'une ressource.

### `POST`

- **Utilisation** : Envoi de données au serveur (chargement d'une image sur le serveur).

### `DELETE`

- **Utilisation** : Suppression d'une ressource (suppression de l'image chargée).
- ***Remarque*** : Les formulaires HTML ne prennent pas en charge la méthode DELETE, donc la suppression est gérée en utilisant le nom et la valeur des champs du formulaire.
---


