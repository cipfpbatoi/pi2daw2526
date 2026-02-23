# 🧩 Sprint 5 y Sprint 6 — Integracions externes, Swagger, Docker, Desplegament final, qualitat i lliurament del producte

Aquest sprint té com a objectiu ampliar i professionalitzar el projecte intermodular incorporant **integracions externes** amb **OAuth2**, documentació formal de l’API amb **Swagger/OpenAPI**, **dockerització completa** i un flux bàsic de **CI/CD**. 
A més, com a activitat vinculada a l’assignatura **Introducció al Núvol Públic (NUV)**, es desplegarà una versió del projecte en **AWS**, documentant el procés i comparant-lo amb el desplegament local mitjançant **Docker Compose**.
Completarem el projecte amb un resultat **professional, estable i llest per a producció**. 
Es treballarà en la **presentació final (UI/UX)**, la **digitalització del negoci (tecnologies intel·ligents)**, la **sostenibilitat (ASG i ecodisseny)**, i el **desplegament complet amb Docker en un servidor real amb HTTPS**.

A més, es farà una revisió total de **qualitat i documentació**, incloent **manual d’usuari**, **accessibilitat** i una **sessió final de demostració** amb el client.

Inclou els requisits del client i mapeja el treball als resultats d’aprenentatge:

- **C1** Integració amb serveis externs i gestió segura de tokens.(DWES) - RA9
- **C2** Documentació de l’API pròpia amb Swagger (OpenAPI).(DWES) - RA9
- **C3** Millores avançades de Vue (watchers, filtres, paginació, validació en temps real).(DWEC) RA3.g, RA4.d, RA5.g, RA6.e
- **C4** Presentació estètica, consistència i accessibilitat professional (DIW).
- **C5** Millora digital: dades, IA o recomanacions intel·ligents (DIG).
- **C6** E-commerce sostenible: criteris ASG i ecodisseny (SOST).
- **C7** Desplegament Cloud, DNS i CI/CD (DDAW + NUV). DAW RA2, RA2.i, DAW RA6.h, DAW RA3.i
- **C8** Documentació final, manual d’usuari, validació i presentació al client.DWES RA8.g, DWES RA9.f, DIW RA5.g, DIW RA6.f

---

## Índex

1. [🔗 C1. Integració amb serveis externs (OAuth2)] DWES
2. [📚 C2. Documentació de l’API pròpia amb Swagger (OpenAPI)] DWES
4. [✨ C3. Millores avançades al front-end (Vue)] DWEC
1. [🎨 C4. Disseny final i accessibilitat professional]DIW
2. [🤖 C5. Digitalització de la tenda amb tecnologies intel·ligents]DIG
3. [🌱 C6. Sostenibilitat: criteris ASG i ecodisseny]SOST
4. [🐳 C7. Desplegament Cloud, DNS i CI/CD] DDAW + NUV
6. [📚 C8. Documentació final, manual d’usuari i presentació]
6. [✅ Lliurables i criteris de validació]


---

## C1. 🔗 Integració amb serveis externs (OAuth2) - (DWES)

### 1️⃣ Objectius

Afegir una integració amb **almenys una API externa** que requerisca **OAuth2**, per ampliar funcionalitats o millorar l’experiència d’usuari.

Exemples vàlids (tria’n **un** com a mínim):

- **Login amb Google** (OpenID Connect sobre OAuth2).
- **Importació de dades** des d’un servei extern relacionat (p. ex. Google Calendar/Drive, GitHub, Spotify, etc.) si té sentit amb el vostre projecte.

**Referència:** **DWES RA9** (integració amb serveis existents, gestió segura de tokens).

---

### 2️⃣ Requisits previs

✅ Backend Laravel (API REST) funcionant 
✅ Frontend Vue (SPA) amb Axios / Pinia 
✅ Variables d’entorn preparades (`.env`) 
✅ Compte desenvolupador del proveïdor (Google Console / etc.)

---

### 3️⃣ Disseny recomanat (Laravel + OAuth2)

La forma més estàndard en Laravel és fer servir **Laravel Socialite** per a inici de sessió amb proveïdors OAuth2.

**Flux general (Authorization Code):**
1. L’usuari prem “Inicia sessió amb Google” (frontend).
2. El backend redirigeix a Google amb `client_id`, `redirect_uri`, `scope`, `state`.
3. Google retorna un `code` al `redirect_uri`.
4. El backend canvia `code` per `access_token` i (opcional) `refresh_token`.
5. El backend crea/actualitza usuari local i genera un token propi (p. ex. Sanctum) per al frontend.
6. El frontend guarda el token propi i treballa amb l’API pròpia.

> Important: **no exposeu client_secret al frontend**. El secret ha d’estar **sempre** al backend.

---

### 4️⃣ Implementació orientativa

#### A) Paquets i configuració
- Instal·lar Socialite i configurar el proveïdor (Google).
- Afegir credencials a `.env`:
  - `GOOGLE_CLIENT_ID=...`
  - `GOOGLE_CLIENT_SECRET=...`
  - `GOOGLE_REDIRECT_URI=https://.../api/oauth/google/callback`

#### B) Rutes API
- `GET /api/oauth/google/redirect` → redirigeix al proveïdor
- `GET /api/oauth/google/callback` → rep el `code`, obté tokens, crea usuari, retorna token del vostre sistema

#### C) Gestió segura de tokens
- Guardar tokens externs **xifrats** (si cal reutilitzar-los) o només usar-los per a una operació puntual.
- Controlar expiració i renovació (si el projecte ho requereix).
- Revocar o “desconnectar” compte extern (opcional però recomanat).

---

### 5️⃣ Testing i seguretat

- Validar el paràmetre `state` (CSRF).
- Comprovar permisos mínims (scopes mínims).
- Provar errors típics:
  - `invalid_grant`, `redirect_uri_mismatch`, token caducat.
- No registrar tokens en logs.
- Documentar el flux i captures de pantalla del funcionament.

---

## C2. 📚 Documentació de l’API pròpia amb Swagger (OpenAPI) - (DWES)

### 1️⃣ Objectius

Generar una **documentació completa i interactiva** de l’API REST del projecte: endpoints, paràmetres, exemples, codis d’estat i autenticació, accessible via interfície web.

**Referència:** **DWES RA9** (facilitar integracions i transparència per a tercers).

---

### 2️⃣ Eina recomanada en Laravel

Opcions habituals:
- `l5-swagger` (basat en swagger-php)
- `scribe` (molt còmode per a docs automàtiques)

En aquest sprint, s’accepta qualsevol opció que produïsca **OpenAPI** i una UI navegable (Swagger UI o similar).

---

### 3️⃣ Contingut mínim que ha d’incloure la doc

- **Tots els endpoints** del vostre backend (mínim els principals CRUD i auth).
- Esquemes (models DTO) i exemples JSON.
- Codis d’estat (`200`, `201`, `400`, `401`, `403`, `404`, `422`, `500`).
- Autenticació:
  - Bearer Token (Sanctum/JWT) o cookie, segons el vostre cas.
- Possibilitat de **provar** peticions des de la UI.

---

### 4️⃣ Verificació

- URL funcional (p. ex. `/api/documentation` o `/docs`).
- Captures i explicació de com s’autoritza a Swagger (on posar el Bearer token).
- Documentar com regenerar la doc (comanda Artisan o script).

---

## C3. ✨ Millores avançades al front-end (Vue) - (DWEC)

### 1️⃣ Objectius

Refinar la interfície SPA amb funcionalitats avançades i reactives:

- **Filtres i paginació** en llistats (p. ex. productes per categoria/preu, etc.)
- Ús de **watchers** per reaccionar a canvis de model/estat global
- Validació en temps real amb **Vee-Validate + Yup**
- Compatibilitat entre navegadors i bones pràctiques

**Referències:** **DWEC RA3.g, RA4.d, RA5.g, RA6.e**.

---

### 2️⃣ Filtres i paginació (patró recomanat)

- Controls UI: input de cerca, select de categoria, rang de preu, etc.
- Estat a Pinia o dins de la vista:
  - `filters` (objecte reactiu)
  - `page`, `perPage`
- Peticions a API amb query params:
  - `/api/products?search=...&category=...&min=...&max=...&page=...`

> Si l’API encara no admet paginació/filtres, cal implementar-ho també al backend (p. ex. Eloquent `paginate()` + `when()` per filtres).

---

### 3️⃣ Watchers (exemples d’ús útil)

- Si canvia un filtre → tornar a demanar dades automàticament
- Si canvia `auth.user` o un valor global → refrescar vistes
- Debounce en cerca (opcional, recomanat)

---

### 4️⃣ Formularis amb Vee-Validate + Yup

**Requisit:**
- Validació immediata: camps obligats, formats, longituds, etc.
- Feedback visual: missatges d’error i estats de camp (valid/invalid)
- Esquemes Yup reutilitzables per formularis

Exemples de formularis típics:
- Login/Register
- Crear/editar producte
- Perfil d’usuari

---

## C4. 🎨 Disseny final i accessibilitat professional (DIW)

### 1️⃣ Objectius

Aplicar una capa final de **poliment visual**, assegurant:

- Estètica professional i coherent en totes les pàgines.
- Fulls d’estil **organitzats** i **mantenibles**.
- Compliment de bones pràctiques d’accessibilitat (WCAG bàsic):
  - contrast adequat
  - navegació amb teclat
  - textos alternatius (`alt`)
  - formularis accessibles (`label`, `aria-*`)
- Ús equilibrat de text, imatge i espais en blanc.
- Imatges **optimitzades** (pes, formats moderns, dimensions correctes).

**Referències DIW:**
- **DIW (Accessibilitat i usabilitat)** → contrast, navegació, components accessibles, responsive.
- **DIW (Maquetació moderna)** → CSS Grid/Flexbox, consistència visual.

---

### 2️⃣ Requisits i bones pràctiques d’estils

✅ Variables CSS (`:root`) per colors, tipografies, espaiats i breakpoints 
✅ Sistema de layout amb **Flexbox/Grid** 
✅ Components reutilitzables (botons, cards, formularis, badges) 
✅ Ús de `rem`, `clamp()`, `minmax()` quan siga útil 
✅ Fitxers CSS modulars i ben organitzats


---

### 3️⃣ Checklist d’accessibilitat

- [ ] Totes les imatges amb `alt` significatiu (o `alt=""` si decoratives).
- [ ] Formularis amb `label` vinculats (`for` + `id`).
- [ ] Validacions amb missatges clars i associats al camp (`aria-describedby`).
- [ ] Focus visible i navegació amb teclat (Tab / Shift+Tab).
- [ ] Contrast AA mínim (evitar gris clar sobre blanc).
- [ ] Botons i enllaços amb text descriptiu (evitar “clic ací”).
- [ ] Jerarquia semàntica: `h1 → h2 → h3`, `nav`, `main`, `footer`.

---

### 4️⃣ Estat del desenvolupament

#### 🟦 To Do
- Auditoria de contrast i focus.
- Revisar formularis (labels, errors, aria).
- Uniformitzar botons i cards.

#### 🟨 In Progress
- Refactor CSS i estructura de fitxers.
- Optimització d’imatges i responsive.

#### 🟩 Done
- Disseny coherent en totes les vistes.
- Layout professional i accessible.

---

## C5. 🤖 Digitalització de la tenda amb tecnologies intel·ligents (DIG)

### 1️⃣ Objectius

Integrar una **millora digital** basada en tecnologies habilitadores digitals:

- ☁️ Cloud (serveis en producció, deploy, persistència)
- 🧠 IA / recomanacions (productes suggerits, destacats)
- 📊 Anàlisi de dades (tendències, top vendes, productes més vistos)

L’equip haurà d’identificar i implementar **una millora concreta**, com per exemple:

- Recomanador simple: “Productes relacionats” (categoria/etiquetes/preu).
- “Productes destacats” segons estadístiques (més venuts / millor valorats).
- Panell mínim d’analytics per admin (visites, conversions, top productes).
- Cerca intel·ligent amb suggeriments (autocomplete bàsic).

---

### 2️⃣ Proposta d’implementació (exemples)

#### ✅ Opció A: Recomanacions intel·ligents (simple)
- Algorisme: mateix `category_id`, preu semblant i bona valoració.
- Endpoint: `GET /api/products/{id}/recommendations`
- Vista: carrusel/llistat “Recomanats per a tu”.

#### ✅ Opció B: Productes destacats per dades
- Guardar mètriques: `views`, `orders_count`, `rating_avg`.
- Endpoint: `GET /api/products/featured`
- Home: secció “Top productes de la setmana”.

#### ✅ Opció C: Mini-analytics admin
- Taula / gràfic amb Top 5 vendes i Top 5 més vistos.
- Endpoint: `GET /api/admin/analytics/summary`
- Vista Admin: dashboard simple.

---

### 3️⃣ Estat del desenvolupament

#### 🟦 To Do
- Triar una millora digital concreta (A/B/C).
- Definir dades necessàries i modelat DB si cal.

#### 🟨 In Progress
- Implementació endpoint + integració al front.

#### 🟩 Done
- Millora digital visible i justificada al lliurament.

---

## C6. 🌱 Sostenibilitat: criteris ASG i ecodisseny (SOST)

### 1️⃣ Objectius

Aplicar sostenibilitat al projecte e-commerce incorporant:

- **Ambiental:** reducció de pes, optimització d’imatges, menys peticions, eficiència.
- **Social:** accessibilitat, inclusió, informació clara, UX sense barreres.
- **Governança:** transparència (polítiques, traçabilitat), bones pràctiques i qualitat del codi.

---

### 2️⃣ Millores sostenibles recomanades

- 🖼️ Imatges en **WebP/AVIF**, lazy loading, dimensions adaptatives.
- 📦 Reducció d’assets: minify, tree-shaking, compressió gzip/brotli en Nginx.
- ♻️ Economia circular: secció “Reacondicionats”, “Reutilitzables” o “Materials reciclats”.
- 🏷️ Etiqueta eco als productes:
  - “Eco Score”
  - “Embalatge reciclat”
  - “Proveïdor local”
- 🧾 Política de sostenibilitat visible (pàgina informativa).

---

### 3️⃣ Estat del desenvolupament

#### 🟦 To Do
- Definir quines millores ASG s’apliquen al projecte.
- Afegir etiqueta eco i criteris al catàleg.

#### 🟨 In Progress
- Optimització d’imatges i assets.
- Ajustos en UI/UX per més claredat i inclusió.

#### 🟩 Done
- Evidència clara de sostenibilitat + justificació en documentació.

---
## C7. 🧪 Desplegament Cloud, DNS i CI/CD (DDAW + NUV)

### 🎯 Objectiu

En aquesta fase del projecte intermòdul, l'equip haurà de portar a producció l'aplicació desenvolupada de:

-   **Vue** (frontend)
-   **Laravel** (backend)

aplicant pràctiques professionals de:

-   Automatització de Tasques
-   Containerització
-   Integració i entrega Continuada
-   Gestió de dominis i DNS
-   Seguretat HTTPS
-   Disseny d'infraestructura escalable en AWS

------------------------------------------------------------------------

## 🧭 PART 1 --- DNS del projecte 
### Objectiu

Gestionar una zona DNS pròpia delegada al vostre servidor. La zona de treball serà `projecteXX.ddaw.es' on XX serà el número de grup assignat per a la realització del projecte

### Tasques a realitzar

1.  Implantar un **servidor DNS màster** al núvol (màquina virtual) o utilitzant un servici DNS en el núvol.
2.  Crear la zona:

```{=html}
    projecteXX.ddaw.es
```

3.  Definir com a mínim els registres necessàris per a publicar les vostres aplicacions:

4.  Facilitar a l'administrador del DNS pare les dades necessàries per
    fer la **delegació**.

------------------------------------------------------------------------

## 🐳 PART 2 --- Entorn de desenvolupament amb Docker

### Objectiu

Permetre que qualsevol membre de l'equip puga engegar les 2 aplicacions en local.

### Requisits

Mitjançant `docker-compose` s'han d'arrancar de forma independent els 2 projectes:

### Obligatori

-   Dockerfile per a cada aplicació
-   variables d'entorn
-   persistència de la base de dades (en les que siga necessari)
-   Incloure en el README  de cada projecte les instruccions per fer-ho

------------------------------------------------------------------------

##🚀 PART 3 --- Entorn de Producció i CI/CD

### Objectiu

Automatitzar completament el pas de codi a producció en el núvol.

### Repositoris independents → pipelines independents

Cada aplicació ha de tindre el seu propi flux de desplegament.

### CI/CD mínim requerit

#### Frontend

-   Instal·lació de dependències
-   Build de producció
-   Desplegament automàtic

#### Backend (Laravel)

-   Instal·lació de dependències
-   Test
-   Desplegament automàtic
-   **execució obligatòria de migracions** després del deploy

### Aïllament d'entorns

Frontend i backend han de funcionar de manera independent: 
- Serveis/contenidors/Maquines virtuals separades
- Configuracions pròpies
- Capacitat de desplegar un sense afectar l'altre

### HTTPS amb Let's Encrypt

Les 2 aplicacions han de ser accessibles amb certificats vàlids:

### Tecnologies vàlides

Podeu utilitzar:

-   màquines virtuals
-   Docker
-   ECS 
-   Auto Scaling
-   Deployer o eines equivalents

------------------------------------------------------------------------

## ☁️ PART 4 --- Arquitectura escalable en AWS

### 🎯 Objectiu

Dissenyar una arquitectura en **AWS** capaç de suportar el desplegament
en producció de l'aplicació Vue + Laravel garantint:

-   Separació de responsabilitats
-   Seguretat entre capes
-   Possibilitat d'escalat
-   Alta disponibilitat
-   Facilitat de manteniment

------------------------------------------------------------------------

### 🧱 Requisits tècnics obligatoris

#### 1️⃣ Xarxa

-   Creació d'una **VPC pròpia**
-   Separació com a mínim en:
    -   subxarxes **públiques**
    -   subxarxes **privades d'aplicació**
    -   subxarxes **privades de dades**

S'haurà d'explicar: 
- Rang IP utilitzat
- Distribució per AZ
- Taules de rutes
- Accés a Internet
- Necessitat o no de NAT

------------------------------------------------------------------------

#### 2️⃣ Capa d'entrada (Edge)

Ha d'existir un punt únic d'entrada de tràfic.

Exemples vàlids: 
- Una EC2 amb Nginx (reverse proxy)
- Un Application Load Balancer

Aquest component serà responsable de: 
- Terminació HTTPS
- Redireccions
- Enviament del tràfic cap a backend o frontend

------------------------------------------------------------------------

#### 3️⃣ Capa d'aplicació

On s'executen:

-   Serveis del backend Laravel
-   Serveis del frontend Vue

#### Nivel Avançat

Ha de permetre **replicar instàncies**.

Exemples vàlids: 
- Auto Scaling Group
- ECS amb diverses tasques
- múltiples contenidors en diferents nodes

------------------------------------------------------------------------

#### 4️⃣ Capa de dades

La base de dades haurà d'estar en subxarxes privades.

S'ha d'implementar o proposar:

-   RDS Multi-AZ
-   Rèplica de lectura
-   Esquema de backup i recuperació

------------------------------------------------------------------------

#### 5️⃣ Seguretat

S'ha de demostrar aïllament entre capes mitjançant:

-   Security Groups
-   normes d'entrada i eixida

Exemple: 
- la base de dades només accepta connexions del backend
- el backend només rep tràfic del balancejador o proxy

------------------------------------------------------------------------

## ☁️ PART 5 --- DOCUMENTACIÓ TÈCNICA DEL PROJECTE

### 🎯 Objectiu

El projecte intermòdular haurà d’anar acompanyat d’una documentació tècnica professional que descriga el sistema al llarg de tot el seu cicle de vida.

Aquesta documentació haurà de permetre que un equip extern siga capaç de:

- Comprendre la solució implementada 
- Llençar l’entorn de desenvolupament 
- Reproduir la infraestructura al núvol 
- Desplegar noves versions 
- Operar i mantindre el servei 
- Validar el funcionament de l’aplicació 
- Continuar l’evolució del sistema 

---

### 📂 Model documental obligatori

Atés que el sistema està compost per diferents aplicacions en repositoris independents, la documentació haurà d’organitzar-se en dos nivells:

1. documentació pròpia de cada aplicació 
2. documentació global de la solució

---

### 📄 Documentació per repositori

Cada aplicació (frontend i backend) haurà d’incloure la seua documentació específica dins del seu repositori.

Aquesta haurà de descriure, com a mínim:

- Arquitectura interna.
- Tecnologies Utilitzades. 
- Configuració 
- Execució en desenvolupament 
- Procés de build 
- Particularitats del desplegament 
- Proves rellevants 
- Els fluxos de CI/CD 
- Els mecanismes d’escalabilitat i disponibilitat 
- Qualssevol altra informació que cregueu necessària

L’equip responsable del repositori serà també responsable de la qualitat i exactitud d’aquesta informació.

---

### 💻 Documentació dels entorns

Per tal de diferenciar clarament els contextos d’execució, s’haurà de documentar separadament en cada repositori:

- l’entorn de desenvolupament 
- l’entorn de producció 

Per a cada entorn s’haurà d’explicar:

- Objectiu 
- Infraestructura 
- Configuracions específiques 
- Forma d’accés 
- Diferències respecte als altres entorns 
- Captures de pantalla amb el funcionament bàsic

---

### 🔄 Integració i entrega continuada

Caldrà documentar el recorregut complet des d’un canvi en el repositori fins a la seua disponibilitat en producció.

S’hauran de descriure:

- fases del pipeline 
- processos automàtics 
- desplegament 
- migracions 
- actualització de serveis 

---

### 👥 Normes de contribució

La documentació haurà d’explicar com s’ha organitzat el treball de l’equip.

Caldrà incloure:

- Estratègia de branques 
- Procés de revisió de codi 
- Criteris d’acceptació 
- Política de versions 
- Code Style
- Distribució de responsabilitats 

### 👤 Usuaris de prova

La documentació haurà d’incloure credencials o mecanismes que permeten verificar el funcionament del sistema.

No s’admetran comptes personals dels membres de l’equip.


### 🌐 Documentació global del sistema

A més de la documentació particular, s’haurà de lliurar una documentació transversal que descriga el comportament conjunt del sistema.

Aquesta documentació haurà de permetre entendre:

- la relació entre frontend, backend i base de dades 
- els diferents entorns existents 
- la infraestructura desplegada en AWS 
- el sistema DNS 
- les mesures de seguretat 
- Qualssevol altra informació que cregueu necessària

### ☁️ Infraestructura al núvol

La documentació de producció haurà de descriure detalladament:

- Organització de la xarxa 
- Separació de recursos públics i privats 
- Ubicació dels serveis 
- Punt d’entrada del trànsit 
- Integració amb DNS 
- Configuració d’HTTPS 

### 🎓 Avaluació

La documentació es valorarà atenent a:

- Rigor tècnic 
- Claredat 
- Completitud 
- Capacitat de justificació 
- Coherència amb la infraestructura real 

Un sistema funcional però deficientment documentat no es considerarà una solució professional.
---

## C8. 📚 Documentació final, manual d’usuari i presentació (TOTS)

### 1️⃣ Objectius

Tancar el projecte amb un lliurament complet:

- Revisió de codi i refactorització necessària.
- Documentació tècnica completa:
  - arquitectura
  - instal·lació
  - configuració
  - desplegament
  - credencials / rols (sense exposar secrets)
- Manual d’usuari final (clar i accessible).
- Ajuda contextual dins l’app (tooltips, textos d’ajuda).
- Proves en diferents navegadors i dispositius.
- Presentació/demostració al client.

**Referències:**
- **DWES RA8.g / RA9.f:** qualitat, manteniment i documentació.
- **DIW RA5.g / RA6.f:** accessibilitat, usabilitat i proves multi-dispositiu.

---

### 2️⃣ Documentació tècnica (mínims)

📄 **README principal** ha d’incloure:

- Descripció del projecte i stack tecnològic.
- Com executar en desenvolupament (Docker).
- Com desplegar en producció (docker-compose.prod).
- Variables d’entorn necessàries (sense secrets).
- Estructura de carpetes i arquitectura.
- API bàsica (endpoints clau).
- Rols i permisos.

---

### 3️⃣ Manual d’usuari (mínims)

- Com registrar-se/iniciar sessió (si aplica).
- Navegació del catàleg, filtres, cerca.
- Veure detall de producte, afegir al carret, compra (si aplica).
- Gestió de perfil i comandes.
- Funcions d’admin (si existeixen).
- FAQ i resolució de problemes freqüents.

📌 **Ajuda contextual dins l’app**
- Tooltips en botons amb icones.
- Text d’ajuda en pantalles complexes (checkout, formularis).
- Missatges d’error comprensibles (no tècnics).

---

### 4️⃣ Sessió de presentació al client (demo)

La demostració ha d’incloure:

- Recorrregut complet per la web i funcionalitats.
- Explicació de com es compleixen els requisits inicials.
- Mostra de: SPRINT1, SPRINT2, SPRINT3,SPRINT4, SPRINT5 i SPRINT6
- Lliurament final:
  - Diagrama de tasques Gantt
  - repositori amb tag/release estable
  - documentació tècnica
  - manual d’usuari

---

### 5️⃣ Estat del desenvolupament

#### 🟦 To Do
- Completar README + documentació tècnica.
- Escriure manual d’usuari i afegir ajuda contextual.

#### 🟨 In Progress
- Refactorització i revisió final (lint, errors, optimització).
- Proves cross-browser i responsive.

#### 🟩 Done
- Lliurament complet i validat amb el client.

## ✅ Checklist d’entregables — Sprint 5 i Sprint 6

> Format checklist per a marcar ✅ (en valencià)

### 🔗 C1 — Integració externa (OAuth2) (DWES)
- [ ] Integració amb **1 servei extern** amb OAuth2 (mínim)
- [ ] Endpoints implementats:
- [ ] `GET /api/oauth/.../redirect`
- [ ] `GET /api/oauth/.../callback`
- [ ] Tokens gestionats de forma segura (sense `client_secret` al front)
- [ ] Migració en la BBDD amb nous camps de Google en la taula Users
- [ ] Evidències: **captures** + explicació del flux + proves

---

### 📚 C2 — Documentació API amb Swagger / OpenAPI (DWES)
- [ ] Swagger/OpenAPI accessible (ex: `/api/documentation` o `/docs`)
- [ ] Documentació amb:
- [ ] Endpoints principals (CRUD + auth)
- [ ] Esquemes/models + exemples JSON
- [ ] Codis d’estat (200/201/400/401/403/404/422/500)
- [ ] Autenticació Bearer (Sanctum/JWT o equivalent)
- [ ] Es poden provar peticions des de la UI
- [ ] Captures + com autoritzar (on posar el token) + com regenerar la doc

---

### ✨ C3 — Millores avançades Vue (DWEC)
- [ ] Llistats amb **filtres + paginació**
- [ ] Watchers aplicats (refresc automàtic quan canvien filtres/estat)
- [ ] Formularis amb **Vee-Validate + Yup** i validació en temps real
- [ ] (Si cal) Backend amb filtres/paginació (`when()` + `paginate()`)

---

### 🎨 C4 — Disseny final i accessibilitat (DIW)
- [ ] UI coherent i professional en totes les vistes
- [ ] CSS estructurat (variables, components reutilitzables, responsive)
- [ ] Accessibilitat bàsica (WCAG):
- [ ] `alt` en imatges
- [ ] `label` correctes en formularis
- [ ] Focus visible i navegació amb teclat
- [ ] Bon contrast
- [ ] Estructura semàntica (`h1/h2`, `nav/main/footer`, etc.)
- [ ] Imatges optimitzades (WebP/AVIF, pes reduït, lazy loading)

---

## 🤖 C5 — Millora digital / “intel·ligent” (DIG)
- [ ] 1 millora digital implementada (tria 1):
- [ ] Recomanador (relacionats)
- [ ] Productes destacats per dades
- [ ] Mini-analytics admin
- [ ] Cerca intel·ligent (autocomplete bàsic)
- [ ] Endpoint(s) creat(s) + integració al front
- [ ] Justificació breu (què aporta i com funciona)

---

## 🌱 C6 — Sostenibilitat (ASG + ecodisseny) (SOST)
- [ ] Optimització sostenible aplicada:
- [ ] Menys pes d’assets / minify / compressió (gzip/brotli si hi ha Nginx)
- [ ] Imatges modernes + lazy load
- [ ] Reducció de peticions (quan siga possible)
- [ ] Element visible “eco” (ex: etiqueta eco, embalatge reciclat, proveïdor local…)
- [ ] Pàgina o secció de sostenibilitat / criteris ASG (mínim explicació)
- [ ] Evidències + justificació en documentació

---

## 🐳☁️ C7 — Docker, DNS, Cloud i CI/CD (DDAW + NUV)

### DNS
- [ ] Zona `projecteXX.ddaw.es` creada
- [ ] Registres mínims per publicar apps (A/CNAME, etc.)
- [ ] Dades entregades per a la **delegació** al DNS pare

### Docker (desenvolupament)
- [ ] `Dockerfile` per a **frontend** i **backend**
- [ ] `docker-compose` per arrancar-ho en local
- [ ] Variables d’entorn (`.env.example`) i configuració
- [ ] Persistència DB (volums) on toque
- [ ] README amb instruccions (com arrancar i parar)

### Producció + CI/CD
- [ ] Pipelines **separats** (repos independents)
- [ ] Front: install → build → deploy automàtic
- [ ] Back: install → test → deploy automàtic
- [ ] Back: **migracions obligatòries** després del deploy
- [ ] Front i back aïllats (serveis/containers/VM separats)
- [ ] HTTPS amb Let’s Encrypt en les 2 aplicacions

### Arquitectura AWS (documentada)
- [ ] VPC + subxarxes públiques/privades (app i dades)
- [ ] Edge únic (ALB o Nginx reverse proxy) + terminació HTTPS
- [ ] Capa app escalable (ASG/ECS o equivalent)
- [ ] Capa dades privada (RDS Multi-AZ / backups / recuperació)
- [ ] Seguretat amb Security Groups (aïllament entre capes)

---

## 📚 C8 — Documentació final + manual + presentació
- [ ] README global amb Documentació tècnica completa (arquitectura, CI/CD, entorns, accés)
- [ ] Manual d’usuari (ús bàsic + FAQ) + ajuda contextual dins l’app
- [ ] Proves en navegadors i dispositius (evidències)
- [ ] Tag/Release estable al repositori
- [ ] Gantt/planificació
- [ ] Demo al client (mostrant Sprints 1–6)
