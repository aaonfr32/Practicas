# Attacking Web Applications with Ffuf

En el mòdul Attacking Web Applications with Ffuf, el que m'ha ensenyat la plataforma i el que he après és com funciona la tècnica de fuzzing web per descobrir recursos ocults que no estan enllaçats directament a la pàgina. He vist com es fa servir ffuf (Fuzz Faster U Fool), una eina molt ràpida per línia de comandes escrita en Go que permet automatitzar peticions massives fent servir diccionaris de paraules (wordlists com els de SecLists) i la paraula clau `FUZZ` per indicar on s'ha d'injectar cada prova. També he après a interpretar els codis d'estat HTTP (com el 200, 301, 403) i a aplicar filtres per mida de resposta, número de paraules o línies per evitar els falsos positius i no omplir la terminal de soroll.

* Fuzzing de directoris i fitxers: He llançat escanejos contra les URLs dels objectius per trobar carpetes ocultes, panells d'administració i fitxers de còpia de seguretat (fent servir el flag `-e` per provar diferents extensions com .php, .html o .bak).
* Enumeració de subdominis i VHosts: He configurat el fitxer /etc/hosts i he utilitzat ffuf tant per cercar subdominis públics com per fer Virtual Host fuzzing, modificant la capçalera Host: de la petició HTTP per descobrir webs internes allotjades a la mateixa adreça IP.
* Fuzzing de paràmetres i valors: He provat d'injectar noms de paràmetres ocults tant per GET (a la pròpia URL) com per POST (enviant dades al cos de la petició amb -d i la capçalera Content-Type), i després he automatitzat la prova de diferents valors o IDs per veure com reaccionava el servidor i aconseguir les flags.



<img src=".gitbook/assets/Pasted image 2026-11-16 14.58.34.png" alt="" height="206" width="202">
