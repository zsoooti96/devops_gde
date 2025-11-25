DevOps Beadandó – PHP + Apache Hello World alkalmazás

Ez a projekt egy egyszerű PHP alapú „Hello World” alkalmazás, amely Apache webszerveren fut.
1. Alkalmazás
Az alkalmazás egy minimalista PHP scriptből áll, amely HTTP-n keresztül elérhető, és egy egyszerű szöveget ad vissza.
Fájl: index.php
A szerver a konténer futtatása után ezen a címen érhető el:
http://localhost:8080

2. Build folyamat
docker build -t php-devops:v1 .
docker run -d --name devops_gde -p 8080:80 php-devops:v1

3. Verziókövetés – trunk-based development

A repository felépítése:

main branch – a trunk

feature/change-message – külön fejlesztői ág

A folyamat röviden:

A projekt inicializálása a main branch-en történt.

Létrehoztam egy külön feature branchet (feature/change-message) azért, hogy a módosításokat elkülönítve végezzem el.

A GitHub felületen a módosítás után megjelent a Compare & pull request gomb, amelyre kattintva létrehoztam a Pull Requestet.

A Pull Request oldalon a Create pull request, majd a Merge pull request gombokkal a feature ág tartalmát beolvasztottam a main branch-be.

4. Dockerizálás

A konténerizáláshoz egy egyszerű Dockerfile készült:
FROM php:8.2-apache
COPY . /var/www/html/
EXPOSE 80

A Dockerfile a hivatalos php:8.2-apache image-re épül, ami tartalmazza az Apache webszervert és a PHP futtatókörnyezetet.
A projekt fájljai a konténer webroot könyvtárába kerülnek, és a szerver automatikusan indul.

5. Felhő deploy (Render.com)

A projekt ingyenes felhőszolgáltatáson lett futtatva a Render.com használatával.

A belpéshez GitHub login-t használtam.
A get-started szekcióban a deployo your core résznél kiválasztottam a Githubot.
Itt kérte a hozzáférést. Engedélyeztem neki a gde_devops repositoryt,hogy hozzáférjen.

Ezután a new webservice-t választottam.
Megadta neki a repot,environmentet,nevet.
Free plan-t választottam ezután.
Majd rákattintototam a deploy web service gombra.

A cloud publikus elérése:
https://devops-gde.onrender.com

FONTOS ELLENŐRZÉSKOR!!:
Your free instance will spin down with inactivity, which can delay requests by 50 seconds or more.


