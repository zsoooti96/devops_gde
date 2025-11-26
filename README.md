DevOps Beadandó – PHP + Apache Hello World

Ez a projekt egy egyszerű PHP alapú „Hello World” alkalmazás, amely Apache webszerveren fut.
1. Az alkalmazás

Az egész projekt egyetlen fájlból áll (index.php), ami egy sima szöveget ír ki, ha valaki megnyitja.
A konténer elindítása után így érhető el:

http://localhost:8080

2. Build és futtatás Dockerrel

A Docker image építése és indítása:

docker build -t php-devops:v1 .
docker run -d --name devops_gde -p 8080:80 php-devops:v1


A build a saját imaget létrehozza, a docker run pedig elindítja a konténert úgy, hogy kívülről a 8080-as porton elérem.

3. Verziókövetés – Trunk-based fejlesztés

A fejlesztéshez a trunk-based development elvet használtam.
A repository így nézett ki:

main – a fő ág

feature/change-message – ebben csináltam a módosításokat

A folyamat röviden:

A projekt a main ágon indult.

Létrehoztam egy feature ágat a változtatásoknak.

A GitHub felajánlotta a Pull Requestet (Compare & pull request).

A PR oldalon rányomtam a Create pull request → Merge pull request gombokra.

A módosítás így szépen visszakerült a main branch-be.


4. Dockerizálás

A konténer építéséhez ezt a rövid Dockerfile-t használtam:

FROM php:8.2-apache
COPY . /var/www/html/
EXPOSE 80


Ez a hivatalos PHP + Apache image-re épül, így a PHP és az Apache is készen van.
Csak átmásoltam a saját fájlokat a webrootba, és indulhatott is a szerver.

5. Felhőbe deploy – Render.com

A projektet a Render.com ingyenes csomagjával tettem ki a felhőbe.

A lépések:

GitHub-os bejelentkezés.

A Get Started résznél kiválasztottam a GitHub deployt.

Engedélyeztem neki, hogy elérje a repositoryt.

Létrehoztam egy New Web Service-t.

Beállítottam a repót, nevet, environmentet.

A Free plan-t választottam.

Végül rányomtam a Deploy Web Service gombra.

A publikus link:

👉 https://devops-gde.onrender.com

Fontos megjegyzés:

A Render free csomagja leáll, ha nincs használva, ezért az első betöltés akár 50 mp is lehet:

“Your free instance will spin down with inactivity...”

