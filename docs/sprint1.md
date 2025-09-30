# SA.1 Iteració: Entorn, aparador i contacte

??? abstract "Duració i criteris d'avaluació"

    Duració estimada: 18 hores

    <hr />

    | Resultat d'aprenentatge | Criteris d'avaluació|
    | -------                 | -------             |
    | 1. Planifica l'execució del projecte, determinant el pla d'intervenció i la documentació associada |a) S'han seqüenciat les activitats ordenant-les en funció de les necessitats d' execució.<br/> b) S'han determinat els recursos i la logística necessaris per a cada activitat. <br/> c) S'han identificat les necessitats de permisos i autoritzacions per dur a terme les activitats. <br/>  d) S' han determinat els procediments d' actuació o execució de les activitats.|

## 📚 C1. Introducció al mòdul: estructura i metodologia

#### 1️⃣ Objectiu
Conéixer l’estructura del **Projecte Integrador de 2n DAW** i la metodologia de treball que seguirem durant el curs.

---

#### 2️⃣ Estructura del mòdul
- **Projecte únic**: desenvolupament d’una aplicació web de comerç electrònic (*E-commerce*).
- **Duració**: tot el curs (99 hores → 3h setmanals).
- **Treball en equips de 2 persones**.
- **Iteracions (sprints)**: el projecte es divideix en 6 fases consecutives:
    1. Entorn, aparador i contacte.
    2. Autenticació i gestió de productes.
    3. Disseny responsiu i backend Laravel.
    4. Client SPA amb Vue i control de rols.
    5. Integracions externes i processos asíncrons.
    6. Desplegament final i lliurament del producte.

---

#### 3️⃣ Metodologia de treball
- **Àgil** (Scrum/Kanban).
- Cada sprint inclou:
    - Planificació inicial (tasques i cronograma).
    - Execució i documentació.
    - Revisió i validació del que s’ha fet.
- **Gestió de tasques**: tauler Kanban (GitHub Projects / Trello).
- **Control de versions**: Git + GitHub (branques, commits, PRs).
- **Revisions periòdiques**: punts de control al final de cada iteració.

---

#### 4️⃣ Responsabilitat individual
- Encara que es treballa en equip, cada alumne ha de ser capaç de:
    - Explicar i defensar les parts en què ha treballat.
    - Mostrar coneixement de totes les fases del projecte.
- Les presentacions i validacions finals són **individuals**.

---

#### 5️⃣ Resultat esperat
- Desenvolupar una aplicació web **funcional i documentada**.
- Aprendre a treballar en equip amb metodologies àgils.
- Integrar coneixements de diferents mòduls (DWES, DIW, DWEC, IAW, etc.).

---

👉 En resum: aquest mòdul és un **entrenament pràctic en condicions reals de projecte**, amb entregues iteratives, treball en equip i responsabilitat compartida.


## 🧰 C2. GitHub Projects / Trello (Gestió àgil del projecte)

#### 1️⃣ Què són?
- **GitHub Projects** → Integrat en GitHub, permet gestionar tasques amb **tauler Kanban** i vincular-les directament amb el codi (issues, commits, PRs).
- **Trello** → Eina independent però molt visual, basada també en el sistema **Kanban** (*targetes* en columnes).

---

#### 2️⃣ Crear un projecte

1. Entrar al repositori de github
2. Pestanya Projects -> New Project
3. Escollir Plantilla: Board (Kanban)
4. Agefir Columnes: (To Do, In Progress,Done )
5. Labels: categories(frontend,backend,bug,urgent...)
6. Deadline: data limit

#### 3️⃣  Organització bàsica (Kanban)
Un tauler típic té 3 columnes principals:

| Columna       | Funció                                       |
|---------------|----------------------------------------------|
| **To Do**     | Tasques pendents, encara no iniciades        |
| **In Progress** | Tasques en les quals s’està treballant      |
| **Done**      | Tasques finalitzades i revisades             |

👉 Es poden afegir columnes extra: *Backlog* (idees futures), *Review* (tasques a revisar), *Testing* (en proves).

---

#### 4️⃣ Creació de targetes/tasques

Cada tasca conté:

- **Títol** → acció concreta (*“Crear formulari de contacte”*).
- **Descripció** → detalls tècnics, passos a seguir.
- **Assignació** → responsable de la tasca.
- **Labels/etiquetes** → categoria (*bug, feature, urgent, frontend, backend*).
- **Dates límit (deadlines)** → per controlar el temps.
- **Checklists** → llistat de sub-tasques.

---

#### 5️⃣ Enllaç amb GitHub
En GitHub Projects es poden:

- Vincular **issues** (incidències) amb una targeta.
- Relacionar un **commit o pull request** amb una tasca → quan es fa *merge*, la tasca pot tancar-se automàticament.
- Exemple: al missatge de commit escriure:

```bash
git commit -m "Add contact form with validation. Fixes #12"
```

👉 Això tanca automàticament l’issue #12 del tauler.  

---

#### 6️⃣⃣ Bones pràctiques
- Mantindre el tauler **actualitzat diàriament**.  
- Crear tasques **curtes i clares** (no massa generals, millor dividir-les).  
- Revisar tasques en les **reunions de seguiment** (dailies o setmanals).  
- Fer ús d’**etiquetes** per distingir entre frontend, backend, documentació, bugfix, etc.  
- Relacionar commits i PRs amb les tasques per a millorar la **traçabilitat**.  

---

####  Comparativa ràpida GitHub Projects vs Trello
| Aspecte              | GitHub Projects                        | Trello                          |
|-----------------------|----------------------------------------|---------------------------------|
| **Integració amb codi** | ✅ Molt alta (commits, PR, issues)      | ❌ Limitada (extensions externes) |
| **Senzillesa visual** | Mitjà                                  | Molt alta                       |
| **Col·laboració externa** | Ideal si tot està a GitHub             | Apte per a equips mixtos        |
| **Gratuït**           | Inclòs en GitHub                       | Gratuït amb opcions premium     |

---

#### 📌 Exemple pràctic (Iteració 1 – E-commerce)
 
##### 🟦 To Do

- Configurar entorn local (IDE + PHP + Git)  
- Crear repositori GitHub i `.gitignore`  
- Preparar servidor remot de proves  
- Dissenyar maqueta pàgina inicial (HTML + CSS)  
- Crear formulari de contacte (HTML + validació JS)  
- Identificar riscos laborals inicials  
- Redactar pla de prevenció bàsic  
- Definir rols i assignar tasques  
- Crear cronograma inicial en GanttProject  

##### 🟨 In Progress

- Maquetació pàgina inicial  
- Validació de formulari al client  
- Configuració cronograma Gantt  
- Documentació inicial en Markdown  

##### 🟩 Done

- ✅ Reunió inicial d’equip → metodologia escollida (Scrum + Kanban)  
- ✅ Creació del tauler GitHub Projects / Trello  
- ✅ Creació del repositori remot i invitació als col·laboradors  

<figure>
  <img src="imagenes/01/d837dfa6-b7b4-4945-80ce-15275925e7a1.png" />
  <figcaption>Exemple Kanban</figcaption>
</figure>
  
---

#### 🏷️ Exemple d’etiquetes
- 🖥️ Backend  
- 🎨 Frontend  
- 📄 Documentació  
- 🐞 Bug  
- ⏳ Urgent  
- ⭐ Millora  

 


## 🌐 C3. Configuració de l’entorn de treball (local i al núvol)

#### 1️⃣ Objectiu
Preparar un **entorn de desenvolupament comú** per a tots els equips, que siga fàcilment replicable i que minimitze els errors entre l’entorn local i el servidor remot.

---

#### 2️⃣ Entorn local
- Cada alumne utilitzarà el seu **ordinador personal** amb:
    - **Editor/IDE** (Visual Studio Code recomanat, o PhpStorm).
    - **Control de versions** amb Git.
- L’entorn de programació i base de dades es **simularà amb Docker**.
    - Cada equip haurà de definir i documentar el seu propi **`docker-compose.yml`**, amb contenidors per al servidor web, PHP i la base de dades.
    - L’objectiu és que **tot el grup treballe amb la mateixa configuració**, evitant “funciona al meu ordinador però al teu no”.
- Altres **ferramentes útils**:
    - *Node.js* + *npm* per a frontend (Vue, build tools).
    - *Postman* per provar APIs.
---

#### 3️⃣ Entorn remot (núvol)
- **Repositori GitHub** com a punt central del projecte.
- **Servidor de proves**: hosting compartit o VPS amb accés SSH.
- **Bases de dades remotes**: còpies sincronitzades amb l’entorn local.
- **CI/CD (si cal)**: GitHub Actions per desplegar automàticament.
---

#### 4️⃣ Bones pràctiques
- Mantindre la configuració de Docker i els scripts documentats al repositori.
- No versionar fitxers sensibles (`.env`).
- Fer còpies periòdiques de la base de dades.
- Evitar “funciona en el meu ordinador” → documentar la configuració.
- Definir al `README.md` o `INSTALL.md` els passos mínims per posar en marxa l’entorn.
  - Passos d’instal·lació de l’entorn.
  - Requisits de versions (PHP, MySQL, Node, etc.).
  - Com executar el projecte en local.
  - Notes per al desplegament remot.
---

#### 5️⃣ Exemple mínim d’entorn
Els contenidors bàsics que haurien d’aparéixer són:
- **Servidor web** (Nginx o Apache).
- **PHP** (versió estable, amb les extensions necessàries).
- **Base de dades** (MySQL o MariaDB).

A partir d’aquest esquelet, cada equip ampliarà i personalitzarà la seua configuració.

---

##  📊 C4. Introducció a GanttProject (cronograma inicial)

#### 1️⃣ Objectiu
Planificar el projecte amb un **cronograma visual** que mostre les tasques, la seua duració i dependències.  
El resultat serà un **diagrama de Gantt** que servirà com a guia inicial del projecte.

---

#### 2️⃣ Eina
- **GanttProject**: eina senzilla i gratuïta per crear cronogrames.
- Exporta a diferents formats (PDF, PNG) per poder compartir amb el professorat o incloure en la documentació.

---

#### 3️⃣ Elements bàsics del diagrama
- **Tasques**: accions a realitzar (*configurar entorn, crear formulari...*).
- **Duració**: hores o dies que ocuparà cada tasca.
- **Dependències**: algunes tasques no poden començar fins que altres acaben.
- **Fites (milestones)**: punts clau del projecte (p. ex. “Primera entrega”).

---

#### 4️⃣ Procediment inicial
1. Crear un **projecte nou** en GanttProject.
2. Afegir les **tasques principals** de l’Iteració 1:
    - Configuració d’entorn (local i remot).
    - Tauler Kanban i repositori GitHub.
    - Cronograma inicial i assignació de rols.
    - Maquetació pàgina inicial.
    - Formulari de contacte.
    - Pla de riscos laborals.
3. Assignar la **duració estimada** de cada tasca.
4. Definir les **dependències** (p. ex. no es pot maquetar fins configurar l’entorn).
5. Exportar i guardar el cronograma en el repositori.

---

#### 5️⃣ Bones pràctiques
- Mantindre el cronograma **actualitzat** a mesura que avança el projecte.
- Revisar-lo en cada **punt de control d’iteració**.
- Usar-lo com a eina de comunicació amb el client i el professorat.

---

👉 El cronograma és una **planificació inicial**, no un document rígid: es pot modificar segons les necessitats del projecte.

## 👥 C5. Assignació de rols i tasques

#### 1️⃣ Objectiu
Repartir el treball de manera clara dins de cada equip, definint **responsabilitats** i **tasques concretes** per a cada alumne.  
Això evita confusions i facilita el seguiment del projecte.

---

#### 2️⃣ Rols bàsics en un equip reduït (2 persones)
- **Scrum Master**
    - Organitza i coordina el treball.
    - Dinamitza les reunions de seguiment.
    - Vetla per l’ús correcte de la metodologia i les eines (Kanban, GitHub).

- **Developer**
    - S’encarrega principalment de la implementació tècnica (frontend, backend).
    - Participa en les revisions de codi.

- **Documentador** (a repartir entre els dos membres)
    - Manté al dia el **README.md**, el pla de riscos i altres documents.
    - Assegura que el repositori continga sempre instruccions clares d’instal·lació i ús.

> ⚠️ Encara que hi haja rols, **tots els membres han de conéixer totes les parts** del projecte i poder defensar-les.

---

#### 3️⃣ Procediment
1. Decidir els rols inicials dins de l’equip.
2. Crear les **tasques en el tauler Kanban** i assignar-les a un responsable.
3. Revisar periòdicament que el repartiment siga equilibrat.
4. Documentar els rols i responsabilitats en el repositori (README o document específic).

---

#### 4️⃣ Bones pràctiques
- Repartir les tasques per **funcionalitats completes**, no per línies de codi.  
  (Exemple: *“Formulari de contacte”* → inclou maquetació, validació i documentació).
- Fer **code reviews creuades**: el company revisa el codi abans de fer *merge*.
- Rotar rols en diferents iteracions per aprendre de totes les parts del projecte.

---

👉 L’assignació de rols i tasques és flexible i pot canviar al llarg del projecte, però sempre ha de quedar registrada i actualitzada.

## 🖥️ C6. Control de versions amb Git i GitHub

#### 1️⃣ Explicació

Quan treballem en equip sobre un projecte de programació, necessitem una eina que ens permeta guardar els canvis, tornar arrere si ens equivoquem i col·laborar sense fouca de codi.
Eixa eina és **Git**, i GitHub és la plataforma on podem pujar els repositoris per compartir-los i treballar en línia.

#### 2️⃣ Objectiu
Entendre què és Git i aprendre a crear i gestionar un repositori en GitHub amb comandes bàsiques.

#### 3️⃣ Passos guiats

1. 🖥️ Obrir Visual Studio Code i el terminal integrat (`Ctrl+ñ`).
2. 📦 Comprovar que Git està instal·lat:

    ```bash
    git --version
    ```

3. 👤 Configurar Git amb el vostre nom i correu institucional:

    ```bash
    git config --global user.name "Nom Cognoms"
    git config --global user.email "el_teu_correu@edu.gva.es"
    ```

4. 🌐 Crear un repositori nou a GitHub:

- Nom: Ecommerce-PI
- Visibilitat: Privat
- Afegir README.md

5. 📥 Tornar a VS Code i clonar el repositori:

    ```bash
    git clone https://github.com/<usuari>/Ecommerce-PI.git
    cd Ecommerce-PI
    ```

6. 📝 Crear un fitxer nou presentacio.md amb una breu descripció del vostre equip.

7. 📤 Guardar i enviar els canvis:

    ```bash
    git add presentacio.md
    git commit -m "feat: afegit document de presentació"
    git push origin main
    
    ```

#### 4️⃣ 📝 Activitat
 
  - Cada alumne crea un fitxer propi dins del repositori (alumne1.md, alumne2.md) i fa un commit.
  - Pujar-ho a GitHub i comprovar que apareix.

## ⚠️ C7. Identificació de riscos laborals

  El desenvolupament de programari no sols implica escriure codi. També passarem moltes hores davant l’ordinador i això pot generar problemes físics (vista, esquena), ambientals (llum, soroll) i psicosocials (estrès, pressió).És important identificar-los per prevenir problemes de salut.

#### 1️⃣ Objectiu

  Reconéixer quins riscos té el treball davant l’ordinador i reflexionar sobre el vostre propi entorn.

#### 2️⃣ Passos guiats

1. 👀 Penseu en com treballeu normalment: postura, cadira, llum, pauses…

2. 📝 Anoteu en un full o en un document 3 riscos personals que patiu o que podríeu patir.

3. 📊 Classifiqueu-los en:

   - 👀Físics (vista, esquena, canells…)
   - 🔊Ambientals (llum, soroll, temperatura)
   - 😰Psicosocials (estrès, pressió, cansament)

#### 3️⃣ Activitat

* Crear dins docs/ un fitxer riscos_individuals.md.

* Escriure:

-  3 riscos que heu detectat
- Què podríeu fer per millorar-los
-  📤 Fer commit i pujar-ho a GitHub.

## 🛡️C8. Pla de riscos i prevenció bàsica

Una vegada identificats els riscos, cal crear un pla de prevenció. Aquest document ajuda a:

- 📊Saber quins riscos existeixen
- 💥Mesurar la seua probabilitat i impacte
- 📝Decidir quines mesures prendre i qui és responsable de revisar-les

#### 1️⃣ Objectiu

Aprendre a crear un document senzill de pla de prevenció que puga revisar-se en cada sprint.

#### 2️⃣ 📋Passos guiats

📂 Crear un fitxer nou RISKS.md dins docs/.

Copiar la plantilla següent:


| Risc                | Probabilitat | Impacte | Mesura preventiva         | Responsable | Seguiment |
|----------------------|--------------|---------|---------------------------|-------------|-----------|
| Fatiga visual        |              |         |                           |             |           |
| Dolor d’esquena      |              |         |                           |             |           |
| Estrès per deadlines |              |         |                           |             |           |



#### 3️⃣ Activitat

- Omplir almenys 3 riscos amb les seues mesures preventives.
- Completar la taula i pujar el fitxer RISKS.md.
- 🔄 Revisar-lo i actualitzar-lo en cada sprint.

## 📄 C9. Eines de documentació: Markdown + repositori Git

En un projecte real, no n’hi ha prou amb el codi. Cal documentar-lo perquè altres persones puguen instal·lar-lo, entendre’l i mantenir-lo.
Per això farem servir Markdown, un llenguatge senzill per escriure documents que GitHub mostra de forma clara i atractiva.

#### 1️⃣ℹ️ Objectiu

Aprendre a escriure documentació clara i senzilla amb Markdown i guardar-la en GitHub.

#### 2️⃣📋 Passos guiats

Crear un fitxer README.md a l’arrel del projecte.

Escriure:

```md
# 🛒 Ecommerce-PI

## 👤 Autors
- Nom alumne 1
- Nom alumne 2

## 🎯 Objectiu del projecte
Desenvolupar una aplicació web de comerç electrònic com a projecte final de DAW.

## 📂 Estructura
- frontend/: HTML, CSS i JS
- backend/: API o servidor
- database/: scripts SQL
- docs/: documentació

## 📊 Estat actual
- [ ] Configuració d’entorn
- [ ] Formulari de contacte
- [ ] Pla de riscos
```

📤 Fer commit i pujar-ho a GitHub.

#### 3️⃣📝 Activitat

- Afegir almenys una secció extra al README.md (p. ex. 🛠️ Tecnologies que farem servir).
- Comprovar a GitHub que es veu bé.

## Annexe: Què és la metologia àgil
 
Una metodología ágil és una manera de gestionar i desenvolupar projectes —sobretot en l’àmbit del programari, però també aplicable en altres sectors— basada en la flexibilitat, la col·laboració i l’adaptació contínua.
👉 En comptes de planificar-ho tot de principi a fi amb molt de detall (com passa amb les metodologies tradicionals, tipus “en cascada”), les metodologies àgils parteixen d’aquests principis:
- Iteracions curtes: el treball es divideix en cicles curts (sprints) on s’entrega una part funcional del producte.
- Feedback continu: es busca la retroalimentació constant del client o usuari per ajustar el producte a les seues necessitats reals.
- Flexibilitat: es poden redefinir prioritats i objectius durant el projecte sense haver de començar de zero.
- Treball en equip: es fomenta la comunicació oberta i la col·laboració entre tots els membres de l’equip.
- Millora contínua: en acabar cada iteració es revisa el procés i es busquen maneres de millorar-lo.

Metodologia en cascada (tradicional)
-----------------------------------
[ Requisits ] ---> [ Disseny ] ---> [ Desenvolupament ] ---> [ Proves ] ---> [ Lliurament ]
          (Tot seqüencial, si falla alguna cosa toca tornar enrere i costa molt adaptar-se)


Metodologia àgil (Scrum, Kanban, etc.)
--------------------------------------
Iteracions curtes (Sprints de 1-3 setmanes)
[ Planificació ] -> [ Desenvolupament ] -> [ Proves ] -> [ Feedback ] -> [ Entrega parcial ]
       ^                                                                         |
       |-------------------------------------------------------------------------|
 (El cicle es repeteix fins aconseguir el producte final, adaptant-se a canvis)

### 📋 Tècniques àgils i tecnologies associades

| **Tècnica / Pràctica**         | **Objectiu**                                      | **Eines / Tecnologies habituals** |
|--------------------------------|--------------------------------------------------|----------------------------------|
| **User stories** (històries d’usuari) | Definir funcionalitats des del punt de vista de l’usuari | Jira, Trello, GitHub Issues, GitLab Issues |
| **Product backlog**            | Llista prioritzada de tasques del projecte        | Jira, Trello, Asana, GitHub Projects |
| **Sprint backlog**             | Tasques concretes d’un sprint                     | Jira (Scrum board), GitLab Boards |
| **Daily stand-up**             | Reunió diària breu per coordinar l’equip          | Slack huddles, Microsoft Teams, Zoom, Discord |
| **Retrospective**              | Revisar què ha funcionat i què millorar           | Miro, Mural, FunRetro, Notion |
| **Kanban board**               | Visualitzar l’estat de les tasques (To Do → Doing → Done) | Trello, GitHub Projects, GitLab Boards, Jira |
| **Continuous Integration / Delivery (CI/CD)** | Automatitzar proves i desplegaments | GitHub Actions, GitLab CI/CD, Jenkins |
| **Testing automatitzat**       | Garantir la qualitat del codi                     | PHPUnit (PHP), Jest (JS), JUnit (Java), Cypress (E2E) |
| **Documentació col·laborativa**| Escriure i compartir coneixement                  | Confluence, Notion, Google Docs, Wiki de GitHub |


## 🚀 Pràctica final: Git + GitHub + VS Code + Formulari Web

#### 🎯 Objectiu

- 🖥️ Gestionar un projecte amb Git i GitHub des de VS Code.
- 📊 Assignar rols i justificar-los al README o en document específic (C5).
- 📅 Elaborar i exportar un cronograma Gantt bàsic amb dependències (C4).
- 🗂️ Vincular commits i issues/targetes del tauler (GitHub Projects/Trello) per a la traçabilitat (C2).
- 💻 Crear un formulari senzill amb HTML5 + JavaScript.
- 🔀 Treballar amb branques i practicar el merge.
- 📚 Documentar el procés amb Markdown.

##### 🛠️ Part 1 – Configuració inicial

- 🌐 Crear repositori Ecommerce-PI en GitHub.
- 📥 Clonar-lo i obrir-lo en VS Code:

```
git clone https://github.com/<usuari>/Ecommerce-PI.git
cd Ecommerce-PI
code .
```
- 📂 Afegir estructura bàsica: frontend/, backend/, database/, docs/ ,.gitignore, README, docker-compose.yml 
- 📤 Fer commit inicial i pujar-lo a main.

##### 📅 Part 2 – Organització del projecte (Gantt + Rols + Kanban)

- Crear tauler Kanban (GitHub Projects/Trello) amb etiquetes i deadlines.
- Crear cronograma inicial en GanttProject amb duració i dependències bàsiques.
- Exportar-lo a docs/gantt-SA1.png i enllaçar-lo al README.
- Definir rols inicials (Scrum Master / Developer) i documentar-los en docs/rols.md.
- Relacionar almenys un commit amb una targeta de projecte (Fixes #id o Closes #id).

##### 💻 Part 3 – Desenvolupament inicial(Formulari bàsic amb HTML5 + JS)

- 🔀 Crea branca develop:

```
git checkout -b develop
git push origin develop
```

**frontend/index.html**
```
<!DOCTYPE html>
<html lang="ca">
<head>
  <meta charset="UTF-8">
  <title>Formulari de contacte</title>
</head>
<body>
  <h1>Contacta amb nosaltres</h1>
  <form id="formContacte">
    <label for="nom">Nom:</label>
    <input type="text" id="nom" name="nom" required minlength="3"><br><br>

    <label for="email">Correu:</label>
    <input type="email" id="email" name="email" required><br><br>

    <label for="edat">Edat:</label>
    <input type="number" id="edat" name="edat" min="18" max="99"><br><br>

    <button type="submit">Enviar</button>
  </form>

  <script src="validacio.js"></script>
</body>
</html>
```
**frontend/validacio.js**
```
document.getElementById("formContacte").addEventListener("submit", function(event) {
  const nom = document.getElementById("nom").value;
  const email = document.getElementById("email").value;

  if (nom.length < 3) {
    alert("El nom ha de tindre almenys 3 caràcters.");
    event.preventDefault();
  }

  if (!email.includes("@")) {
    alert("El correu ha de contindre un '@'.");
    event.preventDefault();
  }
});
```
- 📦 Fer commit i pujar els canvis a la branca.

##### 📱 Part 4 – Millora i integració  (merge)


- 🔀 Crea branca feature/formulari-telefon:

```
git checkout -b feature/formulari-telefon
```

-📱 Afegir al formulari el camp telèfon a index.html:

```
<label for="telefon">Telèfon:</label>
<input type="tel" id="telefon" name="telefon" pattern="[0-9]{9}" placeholder="Ex: 600123456" required><br><br>
```

- ⚙️ Afegir la validació en validacio.js:

```
const telefon = document.getElementById("telefon").value;
const regexTelefon = /^[0-9]{9}$/;

if (!regexTelefon.test(telefon)) {
  alert("El telèfon ha de tindre exactament 9 dígits numèrics.");
  event.preventDefault();
}
```
- 📦 Fer commit i pujar els canvis a la branca.

- 🔀 Tornar a develop i fer merge:

```
git checkout develop
git merge feature/formulari-telefon
git push origin develop
```
- 📥 Obrir Pull Request per integrar develop → main.


#### ✅ Lliurable

Repositori amb:

- 💻 index.html i validacio.js funcionals.
- 🔀 Branca main, develop i almenys una feature.
- 🔀 Un merge realitzat (amb el camp telèfon afegit).
- 📚 Fitxers de documentació (README.md, RISKS.md, riscos_individuals.md).
- 📅 Gantt inicial exportat a docs/.
- 🗂️ Captura del tauler Kanban amb tasques vinculades a commits/issues.


