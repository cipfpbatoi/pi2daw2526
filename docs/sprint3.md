# SA.3 Iteració: Migració a Laravel v2 (mínim viable)

En aquest sprint fem el salt de la versió **PHP + JSON Server** (v1, que es manté intacta a `legacy-php/`) a una versió **més professional amb Laravel** (v2) dins la carpeta `laravel/`. L’objectiu és construir el backend mínim viable sobre MySQL, sense perdre el treball anterior, per a començar a consolidar un **ecosistema MVC real** amb migracions, models i autenticació moderna.

És el primer contacte “seriós” amb un framework gran. Partirem del catàleg i usuaris del sprint anterior, els migrarem a MySQL via Eloquent i deixarem preparat el terreny per al futur client SPA (Vue) i per al microservei Node.js que compartirà la mateixa base de dades.

## 🎯 Objectius d’aprenentatge (DWES · DIW · DAW)
- Entendre i configurar un projecte **Laravel** amb `.env`, migracions i Eloquent (DWES).
- Aplicar **bones pràctiques MVC** i rutes en un framework PHP modern (DAW).
- Crear vistes **Blade** reutilitzant el disseny del front antic (DIW) i servir dades des de MySQL, adaptant-les per a **disseny responsiu** (CSS Grid, media queries).
- Integrar **autenticació Laravel Breeze** i comparar-la amb l’autenticació manual de PHP (DWES/Seguretat).
- Automatitzar la importació d’Excel a base de dades des de Laravel, validant formats i camps (DWES).
- Realitzar **proves bàsiques** (artisan test o proves manuals guiades) per validar productes, autenticació i imports (DWES RA8.g).
- Deixar la porta oberta a la futura **API REST** per a SPA Vue i microservei Node (DWEC/DWES).

## 🌐 Relació amb el projecte integrador
- Aquest sprint correspon a la **Iteració 3 (backend Laravel + DIW responsiu + proves)** de l’enunciat global (`docs/projecte.md`).
- Es manté tota la v1 dins `legacy-php/` (PHP + JSON Server + front antic). No es toca, però es pot reutilitzar estil i JS.
- Es crea `laravel/` amb el backend v2 professional. **docker-compose.yml** es pot ampliar per incloure servei PHP-FPM + Nginx/Apache compartint **MySQL** amb la resta de serveis.
- MySQL serà la BBDD comuna per a Laravel i, en sprints futurs, per al microservei Node.js (estadístiques/recomanacions amb Swagger).
- La part client dels sprints 1 i 2 es versiona com a **legacy**; en aquest sprint s’exporten components i CSS al Blade, i es reforcen les validacions i els comentaris amb JS mentre no arriba la SPA Vue.

---

## 🧩 Tasques / Històries d’usuari

### C1 – Creació del projecte Laravel i configuració de l’entorn
**Context**: Cal un esquelet Laravel operatiu dins del repositori únic.

**Què fer**  

- Crear la carpeta `laravel/` i inicialitzar el projecte amb Laravel (instal·lació habitual via Composer, sense copiar el comando al guió).
- Configurar `.env` per a **MySQL** (mateixa instància que legacy) i generar la clau d’aplicació.
- Revisar l’stack de contenidors existent del landing: si ja tens `docker-compose.yml` per al front, mantín‑lo intacte i decideix si Laravel compartirà la BBDD via eixe compose o si arrencarà el seu propi `docker-compose.yml` amb **Sail** dins `laravel/`. Documenta l’opció escollida però no facilites el comando literal.

**Fitxers clau**: `laravel/.env`, `laravel/config/database.php`, `docker-compose.yml`, possibles `docker/Dockerfile` o `docker/nginx.conf`.

---

### C2 – Model de dades i migracions (products, users)
**Context**: Traslladem l’esquema de `products.json` i `users.json` a MySQL amb migracions.

**Què fer**  

- Crear migració i model `Product` (via generator de Laravel). Camps inspirats en `products.json`: `sku`, `name`, `description`, `price`, `stock`, `image`, `category`, timestamps. Afegir índex únic per `sku`.
- Reutilitzar la migració d’usuaris per defecte de Laravel (`users`), adaptant només si calen camps extra bàsics (telèfon, rol, etc. opcional).
- Executar migracions contra la BBDD MySQL del docker-compose que hages triat (el de legacy o el de Sail).
- Afegir `database/seeders/ProductSeeder` amb uns quants productes de prova per validar la vista.

**Fitxers clau**: `laravel/database/migrations/create_products_table.php`, `laravel/app/Models/Product.php`, `laravel/database/seeders/*`, `laravel/database/factories/ProductFactory.php` (si es vol fer proves).

---

### C3 – Autenticació amb Laravel Breeze
**Context**: Substituïm l’autenticació manual en PHP per una solució integrada.

**Què fer**  

- Instal·lar Breeze i escollir versió Blade (no SPA encara).  
- Compilar assets amb l’eina que pertoque (npm, Vite) si cal, sense indicar el comando literal.  
- Verificar rutes `/register` i `/login` funcionals amb usuaris guardats en MySQL (hash per defecte).  
- Comparar en una nota breu (README) el flux Breeze vs. autenticació manual del Sprint 2 (cookies/sessions vs. middleware + Eloquent).

**Fitxers clau**: `laravel/routes/web.php`, `laravel/resources/views/auth/*`, `laravel/app/Models/User.php`, `laravel/app/Http/Middleware/*`.

---

### C4 – Importació d’Excel a la BBDD (command o controlador)
**Context**: Reaprofitem el flux d’Excel del Sprint 2 però ara tot va directament a MySQL via Laravel.

**Què fer**

- Afegir dependència per gestionar Excel (Laravel-Excel o PhpSpreadsheet, sense llistar el comando).  
- Crear un **command** o un controlador amb formulari d’upload que llija l’Excel i inserisca/actualitze productes.  
- Validar camps obligatoris (`sku`, `name`, `price`, `stock`) i formats numèrics. Gestionar errors amigables.  
- Desar imatge o ruta d’imatge segons dades disponibles (no cal pujar arxius encara).  
- Registrar logs/resums d’importació (nombre de línies, errors) i mostrar feedback en terminal o vista.

**Fitxers clau**: `laravel/app/Console/Commands/ImportProducts.php` o `laravel/app/Http/Controllers/ProductImportController.php`, `laravel/routes/web.php` (ruta d’upload opcional), `laravel/app/Imports/*` si s’usa Laravel-Excel.

---

### C5 – Vista Blade de llistat de productes i primera API `/api/products`
**Context**: Necessitem una sortida visual i un endpoint inicial per al futur client SPA.

**Què fer**  

- Crear ruta pública `/productes` en `web.php` que consulte `Product::all()` i passe dades a una vista Blade.  
- Maquetar una vista `resources/views/productes/index.blade.php` amb **targetes/grids** reutilitzant l’estil del front antic (DIW). Pot fer servir `@vite` per CSS/JS de Breeze o un CSS propi importat del v1, adaptant-lo a **disseny responsiu** (Grid/Flex, media queries) i millorant accessibilitat.  
- Exposar una ruta `GET /api/products` senzilla a `routes/api.php` que retorne JSON de productes (sense auth).  
- API comentaris/valoracions (base backend): crear la migració `comments` o `reviews` (`user_id`, `product_id`, text, rating opcional), el model Eloquent i un controlador esborrany amb `index` i `store` + rutes base (API). Pots deixar la lògica mínima o placeholder; la implementació completa i la UI arribaran a C6.
- Afegir un petit text al README indicant que en sprints futurs el client Vue consumirà aquesta API.

**Fitxers clau**: `laravel/routes/web.php`, `laravel/routes/api.php`, `laravel/app/Http/Controllers/ProductController.php`, `laravel/resources/views/productes/index.blade.php`.

---

### C6 – Validacions i comentaris/valoracions al client (JS provisional)
**Context**: Continuem utilitzant JS en client per cobrir comentaris i validacions mentre no arriba la SPA Vue.

**Què fer**  

- Validació auth: Breeze ja aplica validacions servidor per a registre/login; només adapta JS de registre/login si afegixes camps nous i necessites feedback immediat al client.  
- Validació contacte: reutilitzar la validació del **formulari de contacte** del front antic, adaptant noms de camps i missatges.  
- API comentaris/valoracions (execució completa): acabar la migració si estava pendent, implementar lògica real en `store` i `index` amb validacions (camps obligatoris, rang de rating), decidir si cal auth o permetre anònims i protegir rutes si toca.  
- Bloc UI: afegir al Blade de productes un formulari de comentaris/valoracions i la llista de comentaris consumint l’API amb fetch/AJAX; mostrar errors/validacions al client (formats, camps obligatoris, rang de rating).  
- Provisionalitat: documentar que aquesta solució és temporal fins a la SPA Vue, però assegura la continuïtat funcional del front.

**Fitxers clau**: `laravel/resources/views/productes/index.blade.php` (comentaris/valoracions), `laravel/public/js/` o `resources/js/` (validacions i crides fetch/AJAX), `laravel/routes/web.php` o `laravel/routes/api.php` (rutes de comentaris/valoracions), `laravel/app/Models/` + `laravel/app/Http/Controllers/` per a l’API.

---

### C7 – Proves bàsiques amb Laravel
**Context**: Validar l’API construïda (productes i comentaris/valoracions) amb tests automatitzats de Laravel. L’autenticació Breeze es dona per fiable (no cal testejar-la).

**Què fer**  

- Tests d’API productes: `GET /api/products` (200 i estructura bàsica) i, si hi ha endpoint de creació/actualització, cobrir validacions mínimes.  
- Tests de comentaris/valoracions: `store` i `index` amb producte existent; validar camps obligatoris i rang de rating; provar error quan el producte no existeix o l’usuari no està autenticat si es requereix.  
- Prova d’importació: test de command/controlador d’Excel amb fixture mínima si es pot; si no, documentar checklist manual.  
- Documentar resultats: llistar què s’ha provat, dades utilitzades i estat (passa/falla) per adjuntar a evidències.

**Fitxers clau**: `laravel/tests/Feature/*` (productes, comentaris), `laravel/tests/` en general, arxius de fixtures d’Excel si s’usen.

---


## 📦 Entregables del sprint

- Codi Laravel dins `laravel/` amb migracions, models, rutes, vistes i autenticació Breeze funcional.
- Infraestructura docker clarificada: si continues amb el compose del landing, deixa‑l intacte i documenta com Laravel s’hi connecta; si uses el `docker-compose.yml` de Sail dins `laravel/`, indica com conviu amb el stack existent.
- Documentació mínima al `README.md`: nova arquitectura (carpetes `legacy-php/` + `laravel/`), instruccions de posada en marxa i operacions bàsiques (migracions, arrencar el servei, importació d’Excel) explicades sense donar el comando literal, nota de comparació Breeze vs. auth manual i validacions/JS reutilitzat.
- Captura o GIF breu de la vista `/productes` mostrant targetes.
- Evidència de proves: tests Laravel sobre API de productes i de comentaris/valoracions, i checklist manual només si cal per a la importació.
- Evidència de **planificació i execució** (tauler, Gantt o checklist) per cobrir els RA3 i RA4 del mòdul de projecte.

## ✅ Criteris d’avaluació

- **Laravel core**: migracions correctes, models Eloquent, rutes i controladors nets.
- **Autenticació**: Breeze operatiu (registre/login/logout), usuaris guardats en MySQL amb hash.
- **Importació Excel**: càrrega a `products` amb validacions i gestió d’errors (no es trenquen dades).
- **DIW**: vista Blade coherenta amb l’estètica del Sprint 2 (responsiu, targetes clares) i feedback/validacions visibles.
- **Qualitat de codi**: nomenclatura clara, arxius en la carpeta adequada, comentaris mínims i útils, README actualitzat.
- **Integració**: `legacy-php/` preservat; nova API `/api/products` disponible per a futurs consums.
- **Proves**: tests Laravel sobre API de productes i comentaris/valoracions; checklist manual només si la importació no té test.
- **Gestió de projecte (RA3 i RA4)**: planificació i execució evidenciades (tasques/cronograma, seguiment d’estat, revisió final).

## 🔭 Connexions amb sprints futurs

- **Sprint 4**: construirem una **SPA amb Vue** que consumirà l’API Laravel (`/api/products` i nous endpoints) amb gestió de rols/permisos.
- **Sprint 5+**: desenvoluparem un **microservei Node.js** per a estadístiques i recomanacions sobre la mateixa BBDD MySQL, documentat amb **Swagger**, i integrarem processos asíncrons.
