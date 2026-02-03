# SA.3 Iteració: Backend Laravel + API base (per a Sprint 4)

En aquest sprint fem el salt de la versió **PHP + JSON Server** (v1, que es manté intacta a `legacy-php/`) a una versió **més professional amb Laravel** (v2) dins la carpeta `laravel/`. L’objectiu és construir el backend mínim viable sobre MySQL, sense perdre el treball anterior, i deixar **una API REST base** preparada per al Sprint 4.

És el primer contacte “seriós” amb un framework gran. Partirem del catàleg i usuaris del sprint anterior, els migrarem a MySQL via Eloquent i deixarem preparat el terreny per al futur client SPA (Vue) i per al microservei Node.js que compartirà la mateixa base de dades.

## 🎯 Objectius d’aprenentatge (DWES · DAW)
- Entendre i configurar un projecte **Laravel** amb `.env`, migracions i Eloquent (DWES).
- Aplicar **bones pràctiques MVC** i rutes en un framework PHP modern (DAW).
- Integrar **autenticació Laravel Breeze** i comparar-la amb l’autenticació manual de PHP (DWES/Seguretat).
- Automatitzar la importació d’Excel a base de dades des de Laravel, validant formats i camps (DWES).
- Definir i exposar una **API REST base** per a productes, pensada per a ser consumida en Sprint 4 (DWES/DWEC).
- Realitzar **proves bàsiques** (artisan test o proves manuals guiades) per validar API i imports (DWES RA8.g).

## 🌐 Relació amb el projecte integrador
- Aquest sprint correspon a la **Iteració 3 (backend Laravel + API base + proves)** de l’enunciat global (`docs/projecte.md`).
- Es manté tota la v1 dins `legacy-php/` (PHP + JSON Server + front antic). No es toca.
- Es crea `laravel/` amb el backend v2 professional. **docker-compose.yml** es pot ampliar per incloure servei PHP-FPM + Nginx/Apache compartint **MySQL** amb la resta de serveis.
- MySQL serà la BBDD comuna per a Laravel i, en sprints futurs, per al microservei Node.js (estadístiques/recomanacions amb Swagger).
- La part client dels sprints 1 i 2 es versiona com a **legacy**; en aquest sprint el focus és el backend i l’API que consumiran els clients del Sprint 4.

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
- Afegir `database/seeders/ProductSeeder` amb uns quants productes de prova per validar l’API.

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

### C5 – API base de productes per al Sprint 4
**Context**: Necessitem una API mínima però sòlida que puga consumir la SPA del Sprint 4.

**Què fer**  

- Exposar una ruta `GET /api/products` a `routes/api.php` que retorne JSON de productes (sense auth).
- Afegir `GET /api/products/{id}` i, si és viable, `GET /api/products?category=...&q=...` amb filtres bàsics i paginació.
- Utilitzar **Resources** (p. ex. `ProductResource`) per normalitzar la resposta JSON (preus, stock, timestamps).
- Opcional: crear una ruta pública `/productes` en `web.php` per a una vista Blade mínima de verificació (sense JS), reutilitzant l’estil del front antic si es vol.
- Afegir un text al README indicant que en el Sprint 4 la SPA Vue consumirà aquesta API.

**Fitxers clau**: `laravel/routes/api.php`, `laravel/app/Http/Controllers/ProductController.php`, `laravel/app/Http/Resources/ProductResource.php`, `laravel/routes/web.php` (si es fa la vista), `laravel/resources/views/productes/index.blade.php` (si es fa la vista).

---

### C6 – Proves bàsiques amb Laravel
**Context**: Validar l’API construïda (productes) amb tests automatitzats de Laravel. L’autenticació Breeze es dona per fiable (no cal testejar-la).

**Què fer**  

- Tests d’API productes: `GET /api/products` i `GET /api/products/{id}` (200 i estructura bàsica); si hi ha filtres o paginació, cobrir-ho amb casos simples.  
- Prova d’importació: test de command/controlador d’Excel amb fixture mínima si es pot; si no, documentar checklist manual.  
- Documentar resultats: llistar què s’ha provat, dades utilitzades i estat (passa/falla) per adjuntar a evidències.

**Fitxers clau**: `laravel/tests/Feature/*` (productes), `laravel/tests/` en general, arxius de fixtures d’Excel si s’usen.

---


## 📦 Entregables del sprint

- Codi Laravel dins `laravel/` amb migracions, models, rutes (web i API) i autenticació Breeze funcional.
- Infraestructura docker clarificada: si continues amb el compose del landing, deixa‑l intacte i documenta com Laravel s’hi connecta; si uses el `docker-compose.yml` de Sail dins `laravel/`, indica com conviu amb el stack existent.
- Documentació mínima al `README.md`: nova arquitectura (carpetes `legacy-php/` + `laravel/`), instruccions de posada en marxa i operacions bàsiques (migracions, arrencar el servei, importació d’Excel) explicades sense donar el comando literal, i nota de comparació Breeze vs. auth manual.
- Evidència de proves: tests Laravel sobre API de productes i checklist manual només si cal per a la importació.
- Evidència de **planificació i execució** (tauler, Gantt o checklist) per cobrir els RA3 i RA4 del mòdul de projecte.

## ✅ Criteris d’avaluació

- **Laravel core**: migracions correctes, models Eloquent, rutes i controladors nets.
- **Autenticació**: Breeze operatiu (registre/login/logout), usuaris guardats en MySQL amb hash.
- **Importació Excel**: càrrega a `products` amb validacions i gestió d’errors (no es trenquen dades).
- **Qualitat de codi**: nomenclatura clara, arxius en la carpeta adequada, comentaris mínims i útils, README actualitzat.
- **Integració**: `legacy-php/` preservat; nova API `/api/products` disponible per a futurs consums.
- **Proves**: tests Laravel sobre API de productes; checklist manual només si la importació no té test.
- **Gestió de projecte (RA3 i RA4)**: planificació i execució evidenciades (tasques/cronograma, seguiment d’estat, revisió final).

## 🔭 Connexions amb sprints futurs

- **Sprint 4**: construirem una **SPA amb Vue** que consumirà l’API Laravel (`/api/products` i nous endpoints) amb gestió de rols/permisos.
- **Sprint 5+**: desenvoluparem un **microservei Node.js** per a estadístiques i recomanacions sobre la mateixa BBDD MySQL, documentat amb **Swagger**, i integrarem processos asíncrons.
