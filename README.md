# Lucrarea de laborator Nr6

## Scopul lucrării

Scopul acestei lucrări a fost să învăț cum să gestionez interacțiunea între mai multe containere folosind Docker.

## Sarcina

Crearea unei aplicație PHP pe baza a două containere: nginx, php-fpm.

## Descrierea efectuării lucrării

1. Am creat un nou folder numit `containers05` și l-am clonat sau copiat local.

2. Am creat în directorul containers05 un directorul numit mounts/site, unde am copiat fișierul PHP

3. Am creat fișierul `.gitignore` în rădăcina proiectului și am adăugat:

![](/images/3.png)

4. Am creat fișierul `nginx/default.conf` cu următorul conținut:

![](/images/4.png)

## Pornirea și Testarea

1. Am creat rețeaua internal pentru containere:

![](/images/1.png)

2. Am creat containerul backend cu următoarele proprietăți:

    - pe baza imaginii php:7.4-fpm;
    - directorul mounts/site este montat în /var/www/html;
    - funcționează în rețeaua internal.

![](/images/5.png)

3. Am creat containerul frontend cu următoarele proprietăți:

    - pe baza imaginii nginx:1.23-alpine;
    - directorul mounts/site este montat în /var/www/html;
    - fișierul nginx/default.conf este montat în /etc/nginx/conf.d/default.conf;
    - portul 80 al containerului este expus pe portul 80 al calculatorului gazdei;
    - funcționează în rețeaua internal.

![](/images/2.png)

4. Am deschis http://localhost pentru a verifica funcționalitatea fișierului php:

![](/images/6.png)

## Răspunsuri la întrebări

### În ce mod în acest exemplu containerele pot interacționa unul cu celălalt?
Containerele interacționează printr-o rețea Docker personalizată (internal) care le permite să se "vadă" după numele containerului. Nginx poate trimite cereri PHP către backend:9000, unde backend este numele containerului php-fpm.

### Cum văd containerele unul pe celălalt în cadrul rețelei internal?
În rețeaua internal, fiecare container este identificat prin numele său de container. Astfel, nginx folosește fastcgi_pass backend:9000; pentru a trimite cereri către php-fpm.

### De ce a fost necesar să se suprascrie configurarea nginx?
A fost necesar să suprascriu configurarea nginx pentru a adăuga directivele care trimit fișierele PHP către php-fpm.

## Concluzie

Prin această lucrare am înțeles cum să configurez și să pornesc mai multe containere care lucrează împreună într-o rețea internă.