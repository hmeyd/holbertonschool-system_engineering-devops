Qu’est-ce qu’un serveur ?
→ Un ordinateur (physique ou virtuel) qui fournit des services ou données à d’autres machines (clients).

Rôle du nom de domaine (foobar.com) :
→ Il permet aux utilisateurs d’accéder facilement au site via une adresse lisible au lieu d’une IP.

Type d’enregistrement DNS "www" :
→ Il s’agit d’un enregistrement A (Address Record) qui fait correspondre www.foobar.com à 8.8.8.8.

Rôle du serveur web (Nginx) :
→ Il reçoit les requêtes HTTP/HTTPS et les transmet à l’application. Il gère aussi la distribution des fichiers statiques.

Rôle du serveur d’application :
→ Il traite la logique métier, génère les pages dynamiques, interagit avec la base de données.

Rôle de la base de données :
→ Stocker et récupérer les données nécessaires (utilisateurs, contenus, etc.).

Comment le serveur communique avec le client ?
→ Via le protocole HTTP (ou HTTPS) sur le port 80 ou 443.

⚠️ Problèmes de cette architecture
SPOF (Single Point of Failure) :
→ Si le serveur tombe en panne, le site devient inaccessible.

Temps d’arrêt lors de la maintenance :
→ Si on redémarre Nginx ou déploie une nouvelle version de l’appli, cela peut interrompre l’accès au site.

Impossible de monter en charge :
→ Si beaucoup d’utilisateurs arrivent en même temps, un seul serveur ne peut pas suffire. Il faudra passer à une architecture distribuée.

