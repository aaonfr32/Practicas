# SQL Injection Fundamentals

En el mòdul SQL Injection Fundamentals, el que m'ha ensenyat la plataforma i el que he après és com funcionen les injeccions SQL per dins i per què passen quan una aplicació web concatena directament dades de l'usuari dins d'una consulta a la base de dades sense sanejament ni consultes parametritzades. M'ha servit per entendre la diferència entre els diferents tipus de SQLi —com els atacs In-band (basats en Union o Error), Blind (boolean o time-based) i Out-of-band així com per conèixer les particularitats de sintaxi de motors habituals com MySQL, MSSQL, PostgreSQL o SQLite i com aplicar mesures de mitigació reals.

* Detecció i bypass d'autenticació: He provat caràcters especials i payloads bàsics (com cometes, OR 1=1 o comentaris SQL) en formularis i paràmetres per forçar errors de sintaxi, saltar-me el login i confirmar si l'entrada era vulnerable.
* Extracció de dades amb UNION: He calculat el nombre de columnes i el tipus de dades de la consulta original per encadenar sentències UNION SELECT, enumerar bases de dades, taules i columnes, i bolcar informació sensible per aconseguir les flags.
* Enumeració en SQLi a cegues i automatització: Quan la web no mostrava resultats directes ni errors, he deduït dades a partir del canvi de resposta o dels retards de temps (SLEEP/BENCHMARK) i he utilitzat sqlmap per automatitzar l'enumeració i extracció de dades.

<figure><img src=".gitbook/assets/image (1).png" alt="" width="187"><figcaption></figcaption></figure>
