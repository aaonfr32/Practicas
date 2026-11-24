# HackTheBox: Fawn

Avui vaig a fer la màquina Fawn de Hack The Box, que està marcada com a Very Easy i corre sobre Linux, amb una puntuació de 4.7 (2212 vots) i 150 XP. La idea és anar pas a pas mirant què hi ha obert i veure com es pot entrar per aconseguir la flag.

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Un cop engegada la màquina, veig que la IP del target és la 10.129.147.38. Aquesta serà la direcció a la qual m'hauré de connectar des del meu Kali Linux un cop tingui la VPN activa

<figure><img src=".gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

En aquesta pregunta em demanen què signifiquen les sigles FTP, que corresponen a File Transfer Protocol.

<figure><img src=".gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

En aquest pas em pregunten quin és el port on sol escoltar el servei FTP i la resposta correcta és el port 21. És el port per defecte que cal tenir present quan fem escanejos o comprovacions de xarxa per detectar si hi ha un servidor FTP actiu.

<figure><img src=".gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

A la Task 3 em recorden que FTP envia les dades en clar (sense xifrar) i em demanen les sigles del protocol que fa una funció semblant però de manera segura com a extensió d'SSH. La resposta és SFTP, que és l'alternativa segura que solem fer servir quan volem transferir fitxers sense exposar credencials ni informació per la xarxa.

<figure><img src=".gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

A la Task 4 em demanen quina comanda es pot fer servir per enviar una petició ICMP echo request i comprovar la connexió amb l'objectiu, i la resposta és ping.

<figure><img src=".gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

La pràctica és el primer que faig des de la terminal per veure si la màquina respon per xarxa abans de posar-me a escanejar o connectar-hi.

<figure><img src=".gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

A la Task 5 em demanen quina versió del servei FTP està activa a l'objectiu i la resposta és vsftpd 3.0.3. Identificar la versió exacta d'un servei és molt útil a la pràctica perquè ens dona informació del programari que fa servir el servidor (i, en escenaris més avançats, permet revisar si té alguna vulnerabilitat coneguda).

<figure><img src=".gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

Aquí faig servir nmap -sV -p 21 10.129.147.38 des de la meva carpeta d'usuari a Kali per comprovar directament si el port 21 està obert i quina versió d'FTP fa servir la màquina. El resultat em confirma que el host respon, que el port 21/tcp està obert (open) i que el servei és vsftpd 3.0.3, que encaixa amb la resposta de la Task 5 i amb el que ja havia vist en connectar-me.

<img src=".gitbook/assets/Pasted image 2026-11-24 17.44.30.png" alt="" height="141" width="535">

A la Task 6 em demanen quin tipus de sistema operatiu té la màquina objectiu segons els escanejos i la resposta correcta és Unix.

<figure><img src=".gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

A la Task 7 em demanen quina comanda cal executar per veure el menú d'ajuda del client ftp i la resposta correcta és ftp -?. És una comanda ràpida des de la terminal que va bé tenir al cap per consultar opcions del client quan no recordes algun paràmetre.

<figure><img src=".gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

Aquí executo ftp -? a la terminal de Kali (des de \~) per veure directament el menú d'ajuda del client ftp. Em surt la sintaxi bàsica i les opcions disponibles (com indicar usuari, host, port o forçar IPv4/IPv6), que és el que correspon a la comanda de la Task 7

<img src=".gitbook/assets/Pasted image 2026-11-24 17.53.59.png" alt="" height="229" width="602">

A la Task 8 em demanen quin és el nom d'usuari que es fa servir per FTP quan vols entrar sense tenir un compte, i la resposta correcta és anonymous. És l'usuari que he fet servir després per connectar-me al servidor FTP de la màquina i revisar quins fitxers hi havia disponibles.

<figure><img src=".gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

Aquí em connecto per FTP des de la terminal de Kali (estant situat a /) cap a la IP 10.129.147.38 fent ftp 10.129.147.38. La connexió em mostra que el servidor corre vsFTPd 3.0.3, poso l'usuari anonymous sense contrasenya i entro bé (230 Login successful.), veient també que el sistema remot és UNIX i ja em quedo al prompt ftp> a punt per mirar què hi ha.

<figure><img src=".gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

En aquest pas em pregunten quin és el codi de resposta per al missatge FTP 'Login successful' i la resposta correcta és 230. És el codi que em va sortir just quan vaig iniciar sessió per FTP i em va deixar entrar al servidor.

<figure><img src=".gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

A la Task 10 em demanen quina altra comanda habitual en Linux es pot fer servir per llistar els fitxers i directoris disponibles al servidor FTP (a banda de dir), i la resposta correcta és ls.

<figure><img src=".gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

Un cop dins del prompt ftp>, executo ls per veure què hi ha al directori del servidor. Em surt que entra en mode passiu estès (229 Entering Extended Passive Mode) i em llista el fitxer flag.txt (de 32 bytes i amb permisos de lectura per a tothom, -rw-r--r--), que és l'objectiu que vull descarregar per llegir-ne el contingut.

<figure><img src=".gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

A la Task 11 em demanen quina comanda es fa servir per descarregar el fitxer trobat al servidor FTP i la resposta correcta és get. És la comanda que necessito per baixar-me el fitxer flag.txt cap a la meva màquina local i poder-lo llegir amb calma

<figure><img src=".gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

Amb get flag.txt em descarrego el fitxer de 32 bytes (226 Transfer complete.), surto de la sessió interactiva amb exit (221 Goodbye.) i, ja a la terminal local de Kali, faig cat flag.txt per llegir la flag: 035db21c881520061c53e0536e44f815.

<figure><img src=".gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

Finalment, entro la flag trobada al servidor FTP a l'apartat de tramesa i em confirma l'estat "Root flag owned", donant per completada la resolució principal del repte.
