## 🧩 C1. Importació inicial de productes (Excel → JSON Server)

### 1️⃣ Objectius

Implementar en **PHP** un script que carregue automàticament un catàleg de productes des d’un fitxer **Excel** proporcionat pel client.

L’objectiu és que la botiga dispose d’uns productes ja definits per mostrar a la web, sense haver d’introduir-los manualment un a un.

El procés ha de permetre:
- 📥 Importar les dades de l’arxiu Excel i convertir-les a **format JSON**.
- 🚀 Enviar aquest JSON al **JSON Server**, simulant una API REST amb dades de productes.
- 🔍 Veure productes importats.

---

### 2️⃣ Requisits previs

✅ Configuració Docker (contenidors per a PHP, Nginx i JSON Server)  
✅ Instal·lació de Composer (si uses PHP) per gestionar dependències  
✅ Biblioteca [PhpSpreadsheet](https://github.com/PHPOffice/PhpSpreadsheet) per llegir fitxers Excel  
```Dins del contenidor php.
sudo docker exec -it tu_php bash 
composer require phpoffice/phpspreadsheet:^2
```
✅ JSON Server instal·lat (dins del .yaml):  
```bash
jsonserver:                    # <<— AÇÍ, DINS DE "services:"
    image: node:20-alpine
    container_name: jsonserver
    working_dir: /app
    command: sh -c "npm i -g json-server && json-server --watch /data/products.json --host 0.0.0.0 --port 3000"
    volumes:
      - ./data:/data
    ports:
      - "3000:3000"
    restart: unless-stopped
    networks:
      - pi_network
```
✅ Carpeta `/uploads/` amb permisos d’escriptura  
✅ Carpeta `/data/` per guardar els arxius `products.json` generats

---

### 📦 Estructura del projecte

```
## 🗂️ Exemple Estructura actual del projecte (serà diferent en cada projecte)

PI/
├── .docker/ # Configuracions Docker
│ ├── mysql/ # Config MySQL (scripts init)
│ ├── nginx/ # Config Nginx (default.conf)
│ └── php/ # Config PHP (Dockerfile, ini files)
│
│
├── data/ # Fitxers de dades (JSON Server)
│ └── products.json # Fitxer JSON generat automàticament
│
├── docs/ # Documentació del projecte
│
│
├── uploads/ # Fitxers pujats pel client
│ └── productes.xlsx # Fitxer Excel d’exemple
│
├── .gitignore # Fitxer per ignorar contingut a Git
├── docker-compose.yml # Definició dels serveis Docker
└── README.md # Document principal del projecte
```

---

### 3️⃣ Estructura del fitxer JSON generat

El fitxer `products.json` contindrà una col·lecció de productes amb el format següent:

```json
{
  "productes": [
    {
      "id": 1,
      "sku": "A001",
      "nom": "Cafetera Premium",
      "descripcio": "Cafetera automàtica amb molinet integrat",
      "img": "img/cafetera.jpg",
      "preu": 129.99,
      "estoc": 15
    },
    {
      "id": 2,
      "sku": "A002",
      "nom": "Tetera Elèctrica",
      "descripcio": "Tetera d’acer inoxidable amb control de temperatura",
      "img": "img/tetera.jpg",
      "preu": 59.95,
      "estoc": 10
    }
  ]
}
```

> 📝 Aquest JSON serà servit per `json-server` a `http://localhost:3000/productes`

---

### 4️⃣ Flux general d’implementació (en PHP)

### 🔹 1. Formulari d’upload
- Crear una pàgina HTML amb un formulari per pujar el fitxer Excel.
- Permetre extensions `.xlsx`, `.xls` o `.csv`.

### 🔹 2. Rebre i desar el fitxer
- El servidor guarda el fitxer a `/uploads/` amb un nom únic.

### 🔹 3. Llegir el contingut de l’Excel
- Utilitzar **PhpSpreadsheet** per accedir a les dades.
- Validar que existeixen les columnes esperades: `Nom`, `Preu`, `Estoc`, etc.

### 🔹 4. Validar les dades
- Comprovar que els preus i l’estoc siguen numèrics.
- Ignorar o registrar files buides o amb errors.

### 🔹 5. Generar l’arxiu JSON
- Convertir les dades llegides a un **array associatiu**.
- Guardar el resultat al fitxer `/data/products.json`.

### 🔹 6. Enviar les dades al JSON Server
- Opcional: fer una petició `POST` o `PUT` via `cURL` a `http://json-server:3000/productes`.

### 🔹 7. Mostrar resultat final
- Nombre total de productes importats.
- Files ignorades o amb errors.
- Missatge d’èxit i resum d’errors si n’hi ha.

---

### 5️⃣ Bones pràctiques

🧠 Validar sempre l’estructura del fitxer abans d’importar-lo  
💾 Fer còpia de seguretat del JSON abans d’una nova importació  
⚙️ Separar la lògica d’importació en funcions o classes independents  
🪶 Evitar camps manuals: tot ha d’estar automatitzat  
📅 Registrar la data i l’usuari que realitza la importació  
📦 Evitar duplicats utilitzant identificadors únics (`sku` o `nom`)  
🧾 Mostrar resum d’errors per facilitar correccions al fitxer original  

---

## 💡 Exemple d’execució JSON Server

Després d’executar la importació, pots iniciar el servidor amb:

```bash
json-server --watch data/products.json --port 3000
```

I accedir a:
- 📦 `http://localhost:3000/productes` → Llista de productes
- 🔍 `http://localhost:3000/productes/1` → Producte individual

---

## 🧩 C2. 👥 Registre i inici de sessió d’usuaris (versió JSON Server)

### 🎯 1️⃣ Objectius

Implementar un sistema d’autenticació d’usuaris en **PHP** que permeta:
- 📝 Registrar nous usuaris des d’un formulari.
- 🔐 Iniciar sessió amb credencials segures (nom d’usuari i contrasenya).
- 💾 Guardar i consultar usuaris a través de **JSON Server** (no base de dades).
- 🍪 Crear i gestionar **cookies de sessió** perquè els usuaris mantinguen la seua autenticació.

L’objectiu és garantir que només els usuaris autenticats puguen accedir a les funcionalitats de **comentaris i valoració de productes**.

---

### ⚙️ 2️⃣ Requisits previs

✅ Entorn Docker configurat amb serveis per a **PHP**, **Nginx** i **JSON Server**  
✅ Fitxer `users.json` dins de la carpeta `/data/` per emmagatzemar els usuaris  
✅ Llibreria integrada de PHP `password_hash()` i `password_verify()` per xifrar contrasenyes  
✅ Sessions i cookies PHP activades (`session_start()`)  
✅ Formularis HTML per al registre i inici de sessió  
✅ Validació de formularis tant del costat client com servidor  

---

### 🗂️ 3️⃣ Estructura orientativa del projecte

```
├── auth/
│   ├── register.php        # 🧾 Formulari i procés de registre d’usuaris
│   ├── login.php           # 🔑 Formulari i procés d’inici de sessió
│   ├── logout.php          # 🚪 Tanca la sessió i elimina la cookie
│   └── profile.php         # 👤 Mostra i permet editar les dades de l’usuari autenticat
│
├── includes/
│   └── json_connect.php    # 🌐 Funcions per llegir i escriure al JSON Server (via HTTP)
│
data/
├── products.json           # 📦 Productes (de l’sprint anterior)
└── users.json              # 👥 Usuaris registrats
```

---

### 🧱 4️⃣ Estructura del fitxer `users.json`

En lloc d’una base de dades MySQL, JSON Server gestionarà la col·lecció d’usuaris:

```json
{
  "usuaris": [
    {
      "id": 1,
      "nom_usuari": "andres",
      "contrasenya": "$2y$10$ABC123HASHXIFRAT...",
      "email": "andres@example.com",
      "nom": "Andrés",
      "cognoms": "García Pérez",
      "data_registre": "2025-10-31T10:00:00Z"
    }
  ]
}
```

---

### 🔄 5️⃣ Flux general d’implementació (PHP + JSON Server)

#### 🧩 1. Registre d’usuari
- ✍️ Formulari HTML amb camps: **nom d’usuari, email i contrasenya**.  
- 🔍 Validar que no hi haja camps buits ni usuaris duplicats (`GET /usuaris?nom_usuari=...`).  
- 🔐 Xifrar la contrasenya amb `password_hash()`.  
- 📤 Enviar una petició `POST /usuaris` al JSON Server per afegir el nou usuari.

```php
$data = [
  "nom_usuari" => $nomUsuari,
  "contrasenya" => password_hash($contrasenya, PASSWORD_DEFAULT),
  "email" => $email,
  "nom" => $nom,
  "cognoms" => $cognoms,
  "data_registre" => date('c')
];
```

---

#### 🔑 2. Inici de sessió
- 🧾 Formulari per a l’autenticació amb **nom d’usuari i contrasenya**.  
- 🔎 Comprovar si l’usuari existeix (`GET /usuaris?nom_usuari=...`).  
- 🔐 Validar la contrasenya amb `password_verify()`.  
- ✅ Si és correcte:
  - Crear una sessió (`session_start()`).  
  - Guardar una cookie d’identificació (`setcookie('user_id', $usuari['id'], time()+3600, "/")`).

---

#### 👤 3. Perfil d’usuari
- 📡 Consultar la cookie o sessió per identificar l’usuari.  
- 📋 Mostrar la informació obtinguda del JSON Server (`GET /usuaris/{id}`).  
- ✏️ Permetre actualitzar dades bàsiques mitjançant `PATCH /usuaris/{id}`.

---

#### 🚪 4. Tancament de sessió
- ❌ Eliminar la cookie (`setcookie('user_id', '', time()-3600, "/")`).  
- 🧹 Destruir la sessió (`session_destroy()`).  
- 🔁 Redirigir l’usuari a la pàgina d’inici.

---

### 🧠 6️⃣ Bones pràctiques

🔐 **Contrasenyes segures**  
Utilitza `password_hash()` i `password_verify()` per xifrar i validar contrasenyes.  

🧱 **Sessions segures**  
Crida `session_regenerate_id(true)` després del login per evitar hijacking.  

🚫 **Protecció contra injeccions o manipulacions**  
Valida sempre el contingut rebut del JSON Server abans de mostrar-lo.  

🧩 **Validació de dades**  
Comprova camps buits, longituds, formats de correu i duplicats d’usuari.  

📱 **Disseny responsiu**  
Formularis accessibles i adaptats a dispositius mòbils.  

🧾 **Feedback clar a l’usuari**  
Missatges d’error o èxit visibles després de cada acció (registre, login, logout).

---

### 🧭 7️⃣ Exemple de flux resumit

1️⃣ L’usuari s’inscriu → `POST /usuaris` → guardat en `users.json`  
2️⃣ L’usuari inicia sessió → validació amb `password_verify()`  
3️⃣ PHP crea sessió i cookie → accés a pàgines protegides  
4️⃣ L’usuari pot editar el seu perfil o tancar sessió  
 


## C3. 💬 Comentaris i valoracions de productes  

### 1️⃣ Objectius  

Fomentar la interacció entre els usuaris i el contingut de la botiga mitjançant **comentaris i valoracions** en les fitxes dels productes.  
Els **usuaris autenticats** podran deixar opinions, puntuacions o indicar que un producte els agrada (“👍 M’agrada”).  

Cada comentari o valoració estarà associat **al perfil de l’usuari que l’ha escrit**, i es mostrarà en temps real dins de la pàgina del producte.  

Aquesta funcionalitat ha d’integrar-se en la interfície **de manera dinàmica** (sense necessitat de recarregar la pàgina completa), mantenint l’**estil visual coherent** amb el lloc web i garantint la **usabilitat i accessibilitat** dels elements interactius.  

---

### 2️⃣ Requisits previs  

✅ Sistema d’autenticació d’usuaris actiu (apartat 2)  
✅ Base de dades amb taules per a productes i comentaris  
✅ Entorn amb suport per a **AJAX** o **Fetch API** per enviar dades sense recarregar la pàgina  
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

---

### 7️⃣ Bones pràctiques  

🧱 **Validar dades al servidor i al client** abans de guardar comentaris o puntuacions.  
🚫 **Evitar SPAM o abús** mitjançant límits de freqüència o CAPTCHA.  
🔐 **Comprovar autenticació** abans de permetre qualsevol acció.  
🧾 **Registrar la data i usuari** de cada comentari per a traçabilitat.  
📊 **Mostrar estadístiques bàsiques** (nombre de comentaris, valoració mitjana).  
🧠 **Separar la lògica del frontend i backend** per facilitar manteniment.  



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


## C5. 🧭 Estructura, usabilitat de la interfície i components visuals clau (DIW)

### 1️⃣ Objectius  

Dissenyar i implementar una **pàgina base / plantilla** per a l’e‑commerce que oferisca una **navegació clara i intuïtiva**, amb una **disposició lògica** de menús i seccions principals (**Inici, Productes, Carret, Contacte**).  
Aplicar **principis de disseny centrat en l’usuari** (consistència, jerarquia visual, feedback immediat) i integrar **elements essencials**: **cercador funcional**, **filtres de producte**, **carret visible**, **botons d’acció** (Afegir al carret, Comprar, Registrar‑se) i **gestió d’estats visuals** (hover, actiu, deshabilitat, focus).  

---

### 2️⃣ Requisits previs  

✅ Guia d’estil bàsica o **design tokens** (colors, tipografies, espais).  
✅ Framework de CSS (Tailwind/Bootstrap) o fulls d’estil propis.  
✅ Conjunt d’icones (per ex. Lucide/Font Awesome).  
✅ Rutes mínimes al frontend: `/`, `/productes`, `/carret`, `/contacte`.  
✅ Criteris d’accessibilitat: **WCAG 2.1 AA** i navegació per teclat.  

---

### 3️⃣ Estructura base / plantilla (layout)

- **Capçalera (header):** logotip (enllaç a Inici), **cercador** accessible, menú principal (Inici, Productes, Contacte), **indicador del carret** (quantitat i subtotal).  
- **Cos (main):** espai per a **breadcrumb**, **Hero** opcional, **contenidor** per a llistats (grid/llista) i **sidebar de filtres**.  
- **Peu (footer):** enllaços útils, contacte, legal.  
- **Disposició responsiva:**  
  - Mòbil: menú hamburguesa; filtres en **off‑canvas** o acordions.  
  - Escriptori: **grid 12** amb sidebar per a filtres i contenidor principal per a productes.  
- **Rutes i navegació:** estat actiu al menú; **focus visible**; breadcrumb per a context.  

---

### 4️⃣ Components visuals clau  

- **Cercador**  
  - Input amb `label` visible/oculta (`aria-label`), botó d’enviament, suggeriments (opcional).  
- **Filtres de productes**  
  - Categoria, preu (rang), disponibilitat, valoració; botó **“Netejar filtres”**.  
- **Targeta de producte**  
  - Imatge, nom, preu, valoració, **CTA “Afegir al carret”**; estat *out of stock*.  
- **Carret visible (widget)**  
  - Icona amb **badge** de quantitat; desplegable resum (mini‑cart) amb subtotals i enllaç a “Comprar”.  
- **Botons d’acció**  
  - Estats **normal/hover/actiu/deshabilitat/ càrrega**; amplària plena en mòbil.  
- **Feedback i estats**  
  - *Hover*, *focus*, errors de formulari, **esquelets de càrrega** i **empty states**.  

---

### 5️⃣ Accessibilitat i usabilitat  

- **Navegació per teclat** (ordre de tabulació lògic, `:focus-visible`).  
- **Contrast de color** suficient (ratios AA).  
- **ARIA** per a components personalitzats (botons, llistes de resultats, filtres).  
- **Formularis** amb `label`, missatges d’error clars i indicació de camps obligatoris.  
- **Salt a contingut** (“Skip to content”) al principi del document.  

---

### 6️⃣ Proves i validació  

- **Checklist UX** (claror de navegació, consistència de CTAs, llegibilitat).  
- **Micro‑tests d’usabilitat** (3 usuaris): trobar un producte, afegir‑lo al carret, iniciar compra.  
- **Rendiment**: revisar *Core Web Vitals* bàsics (LCP, CLS) en entorn local.  

---

### 7️⃣ Bones pràctiques  

🧭 Jerarquia clara (H1‑H6), espais consistents, patrons previsibles.  
♿ Prioritzar accessibilitat des del disseny (no com a afegit).  
🧩 Components reutilitzables, sense CSS duplicat; noms semàntics.  
🔁 Estats de càrrega i errors definits (no deixar buits).  
🌍 Preparació per a i18n (textos en fitxers/constats).  

---
