## C1. 🧩 Importació inicial de productes (Excel → BD / JSON)

### 1️⃣ Objetius 

Implementar en **PHP** un script que carregue automàticament un **catàleg de productes** des d’un **fitxer Excel** proporcionat pel client.  
L’objectiu és que la botiga **dispose d’uns productes ja definits per mostrar a la web** sense haver d’introduir productes manualment un a un.  

El procés pot:  
- 📥 **Importar les dades** a la **base de dades MySQL** de l’aplicació.

---

### 2️⃣ Requisits previs  

✅ Configuració Docker (contenidors per a PHP, Nginx, MySQL i Phpmyadmin)
✅ Instal·lació de **Composer** per gestionar dependències PHP
✅ Bajo Composer instala biblioteca **PhpSpreadsheet** per llegir fitxers Excel (composer require phpoffice/phpspreadsheet)
✅ Connexió a una base de dades (MySQL o similar)
✅ Carpeta /uploads/ amb permisos d’escriptura

📦 **Exemple de com quedaría la l'arbre de directoris al finalitzar'**:

#### 🗂️ Estructura del projecte

```bash
PI/
├── .docker/
│   ├── mysql/
│   │   └── init/               'Hi ha que donar-li permisos de lectura i escritura'
│   │       └── root_access.sql 'Dona  acces a root des de qualsevol IP '
│   ├── nginx/
│   │   ├── conf.d/
│   │   │   └── default.conf    'Fitxer de configuración de Nginx'
│   └── php/
│       ├── conf.d/
│       └── Dockerfile          'Construeix un entorn PHP amb totes les extensions i llibreries, incloent PhpSpreadsheet i la connexió amb MySQL.'
│
├── public/
│   ├── img/                    'Img dels productes'
│   ├── css/                    'carpeta css'
│   ├── js/                     'carpeta jss'│   
│   ├── views/                  'carpeta jss'
│   ├── app/
│   ├── index.php
│   └── importar_excel.php      'Archiu que anem a crear per importar Full de Càlcul a la Base de Dades'
│
├── database/
│   └── schema.sql
├── uploads
│   └── productes.xlsx      'Archiu de prova per pujar productes'
├── docs/ 
│
├── vendor/                 'Contiene todas las dependencias PHP instaladas por Composer, la instalació de Composer crea aquest directori'
├── composer.json           'Dependencias, versiones y configuraciones del proyecto PHP que Composer debe instalar y gestionar'
├── composer.lock           'Dependencias, versiones y configuraciones del proyecto PHP que Composer debe instalar y gestionar'
├── docker-compose.yml      'Defineix els serveis de Docker (com PHP, Nginx, MySQL o phpMyAdmin), indicant com s’han de construir, connectar i executar conjuntament.'
├── README.md
└── .gitignore
```

### 3️⃣ Estructura de la base de dades  

Abans de començar la importació, has de crear una base de dades i cal definir la taula `productes` amb camps com:

```sql
CREATE TABLE productes (
  sku VARCHAR(100) PRIMARY KEY,             -- ClauPrimaria
  nom VARCHAR(255) NOT NULL,
  descripcio TEXT,
  img VARCHAR(200),
  preu DECIMAL(10,2) NOT NULL DEFAULT 0.00,
  estoc INT NOT NULL DEFAULT 0
)

```

### 4️⃣ Flux general d’implementació (en PHP)

🔹 **1. Formulari d’upload**  
   - Crear una pàgina HTML amb un formulari per pujar el fitxer Excel.  
   - Permetre extensions `.xlsx`, `.xls`, o `.csv`.

🔹 **2. Rebre i desar el fitxer**  
   - El servidor guarda el fitxer a `/uploads/` amb un nom únic.  

🔹 **3. Llegir el contingut de l’Excel**  
   - Utilitzar `PhpSpreadsheet` per accedir a les dades.  
   - Validar que existeixen les columnes esperades: `Nom`, `Preu`, `Estoc`, etc.  

🔹 **4. Validar les dades**  
   - Comprovar que els preus i l’estoc siguen numèrics.  
   - Ignorar o registrar files buides o amb errors.  

🔹 **5. Importar a la base de dades**  
   - Inserir els productes utilitzant consultes preparades (PDO).  
   - Evitar duplicats.  
🔹 **6.Guardar el log de la importació**
🔹 **7. Mostrar resultat final**  
   - Nombre total de productes importats.  
   - Files ignorades o amb errors.  
   - Missatge d’èxit i resum d’errors si n’hi ha.

---


### 6️⃣ Bones pràctiques  

🧠 **Validar sempre** l’estructura del fitxer abans d’importar-lo.  
💾 **Fer còpia de seguretat** abans d’una nova importació massiva.  
⚙️ **Separar la lògica** d’importació en funcions o classes independents.  
🪶 **Evitar camps manuals**, tot ha d’estar automatitzat.  
📅 **Registrar la data i l’usuari** que realitza la importació.  
📦 **Evitar duplicats** utilitzant identificadors únics (`sku` o `nom`).  
🧾 **Mostrar resum d’errors** per facilitar correccions al fitxer original.  

---

## C2. 👥 Inici de sessió d’usuaris  

### 1️⃣ Objectius  

Implementar un sistema de identificació d’usuaris en PHP amb la finalitat de permetre als usuaris identificats  poder qualificar el productes. Consistirà en guardar en les cookies l'email de l'usuari. 


---

### 2️⃣ Requisits previs  

✅ Configuració Docker amb serveis per a PHP, Nginx i MySQL  
✅ Formulari HTML per a la identificació 


---

## C3. 💬 Comentaris i valoracions de productes  

### 1️⃣ Objectius  

Fomentar la interacció entre els usuaris i el contingut de la botiga mitjançant **comentaris i valoracions** en les fitxes dels productes.  
Els **usuaris identificats** podran deixar opinions, puntuacions o indicar que un producte els agrada (“👍 M’agrada”).  

Cada comentari o valoració estarà associat **al perfil de l’usuari que l’ha escrit**, i es mostrarà en temps real dins de la pàgina del producte.  

Aquesta funcionalitat ha d’integrar-se en la interfície **de manera dinàmica** (sense necessitat de recarregar la pàgina completa), mantenint l’**estil visual coherent** amb el lloc web i garantint la **usabilitat i accessibilitat** dels elements interactius.  

---

### 2️⃣ Requisits previs  

✅ Sistema d’identificació d’usuaris actiu (apartat 2)  
✅ Base de dades amb taules per a productes i comentaris  
✅ Fulls d’estil CSS o framework (Bootstrap, Tailwind...) per mantenir coherència visual  
✅ JavaScript actiu en el client per gestionar la interacció dinàmica  


### 4️⃣ Flux general d’implementació  

🔹 **1. Mostrar comentaris i valoracions**  
   - Carregar els comentaris existents mitjançant una crida AJAX al backend.  
   - Mostrar-los sota la fitxa del producte, amb nom d’usuari i data.  

🔹 **2. Afegir un nou comentari**  
   - Formulari amb camp de text i, opcionalment, selector de puntuació.  
   - Enviar les dades al servidor amb AJAX sense recarregar la pàgina.  
   - Actualitzar la llista de comentaris en temps real.  

🔹 **3. Valorar un producte (puntuació o “M’agrada”)**  
   - Permetre marcar o desmarcar amb un botó interactiu.  
   - Registrar la interacció a la base de dades.  
   - Actualitzar el recompte de “m’agrada” o mitjana de puntuació dinàmicament.  

🔹 **4. Gestió de permisos**  
   - Només els usuaris autenticats poden comentar o valorar.  
   - Cada usuari pot editar o eliminar els seus propis comentaris.  
   - Els administradors poden moderar o eliminar qualsevol comentari.  

---

### 5️⃣ Interfície d’usuari  

- L’àrea de comentaris ha d’integrar-se dins de la fitxa del producte, mantenint l’estètica general del lloc.  
- Els formularis han de ser **accessibles** (etiquetes `label`, focus clar, compatibilitat amb teclat).  
- Les accions han de proporcionar **feedback visual immediat** (missatges d’èxit o error, canvis de color, animacions suaus).  

---

### 6️⃣ Dinamisme i accessibilitat  

⚙️ Ús de **AJAX** o **Fetch API** per carregar i enviar comentaris sense recarregar la pàgina.  
🧩 Les respostes del servidor s’enviaran en **format JSON** per facilitar la manipulació amb JavaScript.  
♿ Es garantirà que els botons i formularis siguen accessibles amb teclat i lectors de pantalla.  
🎨 S’adaptarà el disseny perquè funcione tant en dispositius d’escriptori com en mòbils.  


## C4. ☁️ Desplegament i còpies de seguretat remotes  

### 1️⃣ Objectius  

Garantir que l’aplicació web estiga **sempre disponible, actualitzada i amb les dades protegides**, implantant un sistema de **desplegament remot i còpies de seguretat automàtiques**.  

L’objectiu principal és permetre al client **actualitzar la seua aplicació fàcilment** i **recuperar-la ràpidament** en cas d’error o pèrdua de dades.  

---

### 2️⃣ Requisits previs  

✅ Entorn de desplegament preparat (servidor remot, VPS o hosting)  
✅ Accés segur configurat (SFTP, SCP o SSH amb claus públiques)  
✅ Directori remot per a l’aplicació web i un altre per a les còpies de seguretat  
✅ Contenidors Docker configurats per reproduir l’entorn local  
✅ Eines de sincronització o scripts per automatitzar pujades i còpies de seguretat  
✅ Opcional: servei de còpies en el núvol (Google Drive, Dropbox, AWS S3...)  

📦 **Estructura orientativa per a desplegament:**

deploy/
├── backup.sh 'Script per generar i guardar còpies de seguretat (fitxers + BD)'
├── upload.sh 'Script per pujar actualitzacions al servidor remot via SFTP o rsync'
├── .env 'Configuració d’accés segur i rutes remotes'
└── cronjobs/ 'Tasca programada per a còpies automàtiques'
└── backup_cron.sh


---

### 3️⃣ Flux general d’implementació  

🔹 **1. Desplegament inicial**  
   - Crear un servidor remot (VPS o hosting amb SSH).  
   - Copiar els fitxers de l’aplicació i configurar Docker o Nginx remotament.  
   - Verificar que tots els serveis (PHP, MySQL, Nginx) funcionen igual que en local.  

🔹 **2. Transferència d’actualitzacions**  
   - Automatitzar pujades amb **scripts SFTP, rsync o Git hooks**.  
   - Només sincronitzar els fitxers modificats (backend, frontend, configuracions).  
   - Garantir que el servei continue actiu durant la transferència.  

🔹 **3. Còpies de seguretat periòdiques**  
   - Crear un script que faça còpia de la base de dades (`mysqldump`) i dels fitxers del projecte.  
   - Guardar-les en un directori dedicat del servidor o enviar-les a un servei extern (S3, Google Drive, FTP...).  
   - Configurar un **cron job** perquè s’execute automàticament (per exemple, cada dia a les 2:00).  

🔹 **4. Restauració**  
   - Permetre restaurar fàcilment una còpia de seguretat amb un script (`restore.sh`).  
   - Assegurar la coherència entre fitxers i base de dades abans de reiniciar els serveis.  

---

### 4️⃣ Integració amb Docker  

🧱 Els contenidors es poden recrear automàticament en el servidor remot amb:  
- `docker-compose pull && docker-compose up -d` per aplicar noves versions.  
- Volums Docker per mantindre dades persistents de la base de dades.  
- Còpies incrementals dels volums `/var/lib/mysql` i del codi font del projecte.  

---

### 5️⃣ Bones pràctiques  

🔐 **Utilitzar connexions segures (SFTP, SSH)** per evitar filtracions.  
📅 **Automatitzar les còpies** amb cron per assegurar-ne la periodicitat.  
💾 **Comprimir i datar** cada còpia (`backup_YYYYMMDD.zip`) per identificar-les fàcilment.  
🧩 **Verificar les còpies** periòdicament per garantir que són restaurables.  
🧱 **Separar entorns** (producció, preproducció, desenvolupament) per evitar errors humans.  
🌍 **Notificar o registrar** cada desplegament per tindre un historial de versions.  

---

### 6️⃣ Estat del desenvolupament  

#### 🟦 To Do  
- Configurar accés segur al servidor (SSH/SFTP).  
- Crear scripts de desplegament i còpia de seguretat.  

#### 🟨 In Progress  
- Automatitzar tasques amb cron o GitHub Actions.  
- Integrar còpies remotes amb el sistema de fitxers Docker.  

#### 🟩 Done  
- Sistema de còpies funcional i verificat.  
- Desplegament remot segur i actualitzacions automàtiques.  
- Restauració provada i validada amb èxit.  

