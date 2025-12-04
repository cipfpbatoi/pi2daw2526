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
- Crear la carpeta `laravel/` i inicialitzar el projecte (`composer create-project laravel/laravel .` des de dins).
- Configurar `.env` per a **MySQL** (mateixa instància que legacy) i clau d’aplicació (`php artisan key:generate`).
- Actualitzar `docker-compose.yml` perquè expose un servei web per Laravel (PHP + Nginx/Apache) apuntant a `laravel/public`, compartint xarxa/BBDD amb la resta.

**Fitxers clau**: `laravel/.env`, `laravel/config/database.php`, `docker-compose.yml`, possibles `docker/Dockerfile` o `docker/nginx.conf`.

---

### C2 – Model de dades i migracions (products, users)
**Context**: Traslladem l’esquema de `products.json` i `users.json` a MySQL amb migracions.

**Què fer**  
- Crear migració i model `Product` (`php artisan make:model Product -m`). Camps inspirats en `products.json`: `sku`, `name`, `description`, `price`, `stock`, `image`, `category`, timestamps. Afegir índex únic per `sku`.
- Reutilitzar la migració d’usuaris per defecte de Laravel (`users`), adaptant només si calen camps extra bàsics (telèfon, rol, etc. opcional).
- Executar migracions `php artisan migrate` contra la BBDD MySQL del docker-compose.
- (Opcional) Afegir `database/seeders/ProductSeeder` amb uns quants productes de prova per validar la vista.

**Fitxers clau**: `laravel/database/migrations/*create_products_table.php`, `laravel/app/Models/Product.php`, `laravel/database/seeders/*`, `laravel/database/factories/ProductFactory.php` (si es vol fer proves).

---

### C3 – Autenticació amb Laravel Breeze
**Context**: Substituïm l’autenticació manual en PHP per una solució integrada.

**Què fer**  
- Instal·lar Breeze (`composer require laravel/breeze --dev` + `php artisan breeze:install`). Escollir versió Blade (no SPA encara).  
- Executar `npm install && npm run dev` o equivalent per compilar assets si cal (segons stack triada).  
- Verificar rutes `/register` i `/login` funcionals amb usuaris guardats en MySQL (hash per defecte).  
- Comparar en una nota breu (README) el flux Breeze vs. autenticació manual del Sprint 2 (cookies/sessions vs. middleware + Eloquent).

**Fitxers clau**: `laravel/routes/web.php`, `laravel/resources/views/auth/*`, `laravel/app/Models/User.php`, `laravel/app/Http/Middleware/*`.

---

### C4 – Importació d’Excel a la BBDD (command o controlador)
**Context**: Reaprofitem el flux d’Excel del Sprint 2 però ara tot va directament a MySQL via Laravel.

**Què fer**  
- Afegir dependència per gestionar Excel (p.ex. `composer require maatwebsite/excel` o integrar PhpSpreadsheet manualment).  
- Crear un **command** (`php artisan make:command ImportProducts`) o un controlador amb formulari d’upload que llija l’Excel i inserisca/actualitze productes.  
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
- Afegir un petit text al README indicant que en sprints futurs el client Vue consumirà aquesta API.

**Fitxers clau**: `laravel/routes/web.php`, `laravel/routes/api.php`, `laravel/app/Http/Controllers/ProductController.php`, `laravel/resources/views/productes/index.blade.php`.

---

### C6 – Validacions i comentaris/valoracions al client (JS provisional)
**Context**: Continuem utilitzant JS en client per cobrir comentaris i validacions mentre no arriba la SPA Vue.

**Què fer**  
- Reutilitzar el JS de sprints 1 i 2 per a validació de formularis (registre/login, comentaris) i actualitzar-lo perquè treballe amb les noves rutes Laravel (forms Blade).  
- Implementar un bloc de comentaris/valoracions senzill en la vista de producte (o en `/productes`) que, de moment, faça crides AJAX a rutes Laravel (o dummy) per guardar/mostrar comentaris.  
- Garantir **validacions al client** (formats, camps obligatoris) i feedback accessible.  
- Documentar que aquesta solució és provisional fins a la SPA Vue, però assegura la continuïtat funcional del front.

**Fitxers clau**: `laravel/resources/views/productes/index.blade.php` (inserció de secció de comentaris), `laravel/public/js/` o `resources/js/` amb validacions i crides fetch/AJAX, `laravel/routes/web.php` (rutes temporals per comentaris si cal).

---

## 📦 Entregables del sprint
- Codi Laravel dins `laravel/` amb migracions, models, rutes, vistes i autenticació Breeze funcional.
- `docker-compose.yml` actualitzat amb el servei Laravel i MySQL compartit (mantenint `legacy-php/` intacte).
- Documentació mínima al `README.md`: nova arquitectura (carpetes `legacy-php/` + `laravel/`), instruccions de posada en marxa i comandes principals (`php artisan migrate`, `php artisan serve`/contenidor, importació Excel, etc.), nota de comparació Breeze vs. auth manual i validacions/JS reutilitzat.
- Captura o GIF breu de la vista `/productes` mostrant targetes.
- Breu evidència de **proves** (artisan test o checklist manual) sobre productes, auth i importació.
- Evidència de **planificació i execució** (tauler, Gantt o checklist) per cobrir els RA3 i RA4 del mòdul de projecte.

## ✅ Criteris d’avaluació
- **Laravel core**: migracions correctes, models Eloquent, rutes i controladors nets.
- **Autenticació**: Breeze operatiu (registre/login/logout), usuaris guardats en MySQL amb hash.
- **Importació Excel**: càrrega a `products` amb validacions i gestió d’errors (no es trenquen dades).
- **DIW**: vista Blade coherenta amb l’estètica del Sprint 2 (responsiu, targetes clares) i feedback/validacions visibles.
- **Qualitat de codi**: nomenclatura clara, arxius en la carpeta adequada, comentaris mínims i útils, README actualitzat.
- **Integració**: `legacy-php/` preservat; nova API `/api/products` disponible per a futurs consums.
- **Proves**: execució de tests bàsics o checklist manual documentat.
- **Gestió de projecte (RA3 i RA4)**: planificació i execució evidenciades (tasques/cronograma, seguiment d’estat, revisió final).

## 🔭 Connexions amb sprints futurs
- **Sprint 4**: construirem una **SPA amb Vue** que consumirà l’API Laravel (`/api/products` i nous endpoints) amb gestió de rols/permisos.
- **Sprint 5+**: desenvoluparem un **microservei Node.js** per a estadístiques i recomanacions sobre la mateixa BBDD MySQL, documentat amb **Swagger**, i integrarem processos asíncrons.
