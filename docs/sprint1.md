# SA.1 Iteració: Entorn, aparador i contacte

??? abstract "Duració i criteris d'avaluació"

    Duració estimada: 18 hores

    <hr />

    | Resultat d'aprenentatge | Criteris d'avaluació|
    | -------                 | -------             |
    | 1. Planifica l'execució del projecte, determinant el pla d'intervenció i la documentació associada| necessitats d' execució.| b) S'han determinat els recursos i la logística necessaris per a cada activitat. <br/> c) S'han identificat les necessitats de permisos i autoritzacions per dur a terme les activitats. <br/>  d) S' han determinat els procediments d' actuació o execució de les activitats.|



## C2. GitHub Projects / Trello (Gestió àgil del projecte)

### 1️⃣ Què són?
- **GitHub Projects** → Integrat en GitHub, permet gestionar tasques amb **tauler Kanban** i vincular-les directament amb el codi (issues, commits, PRs).
- **Trello** → Eina independent però molt visual, basada també en el sistema **Kanban** (*targetes* en columnes).

---

### 2️⃣ Organització bàsica (Kanban)
Un tauler típic té 3 columnes principals:

| Columna       | Funció                                       |
|---------------|----------------------------------------------|
| **To Do**     | Tasques pendents, encara no iniciades        |
| **In Progress** | Tasques en les quals s’està treballant      |
| **Done**      | Tasques finalitzades i revisades             |

👉 Es poden afegir columnes extra: *Backlog* (idees futures), *Review* (tasques a revisar), *Testing* (en proves).

---

### 3️⃣ Creació de targetes/tasques

Cada tasca conté:

- **Títol** → acció concreta (*“Crear formulari de contacte”*).
- **Descripció** → detalls tècnics, passos a seguir.
- **Assignació** → responsable de la tasca.
- **Labels/etiquetes** → categoria (*bug, feature, urgent, frontend, backend*).
- **Dates límit (deadlines)** → per controlar el temps.
- **Checklists** → llistat de sub-tasques.

---

### 4️⃣ Enllaç amb GitHub
En GitHub Projects es poden:

- Vincular **issues** (incidències) amb una targeta.
- Relacionar un **commit o pull request** amb una tasca → quan es fa *merge*, la tasca pot tancar-se automàticament.
- Exemple: al missatge de commit escriure:

```bash
git commit -m "Add contact form with validation. Fixes #12"
```

👉 Això tanca automàticament l’issue #12 del tauler.  

---

### 5️⃣ Bones pràctiques
- Mantindre el tauler **actualitzat diàriament**.  
- Crear tasques **curtes i clares** (no massa generals, millor dividir-les).  
- Revisar tasques en les **reunions de seguiment** (dailies o setmanals).  
- Fer ús d’**etiquetes** per distingir entre frontend, backend, documentació, bugfix, etc.  
- Relacionar commits i PRs amb les tasques per a millorar la **traçabilitat**.  

---

### 6️⃣ Comparativa ràpida GitHub Projects vs Trello
| Aspecte              | GitHub Projects                        | Trello                          |
|-----------------------|----------------------------------------|---------------------------------|
| **Integració amb codi** | ✅ Molt alta (commits, PR, issues)      | ❌ Limitada (extensions externes) |
| **Senzillesa visual** | Mitjà                                  | Molt alta                       |
| **Col·laboració externa** | Ideal si tot està a GitHub             | Apte per a equips mixtos        |
| **Gratuït**           | Inclòs en GitHub                       | Gratuït amb opcions premium     |

---

### 📌 Exemple pràctic (Iteració 1 – E-commerce)

#### 🟦 To Do

- Configurar entorn local (IDE + PHP + Git)  
- Crear repositori GitHub i `.gitignore`  
- Preparar servidor remot de proves  
- Dissenyar maqueta pàgina inicial (HTML + CSS)  
- Crear formulari de contacte (HTML + validació JS)  
- Identificar riscos laborals inicials  
- Redactar pla de prevenció bàsic  
- Definir rols i assignar tasques  
- Crear cronograma inicial en GanttProject  

#### 🟨 In Progress

- Maquetació pàgina inicial  
- Validació de formulari al client  
- Configuració cronograma Gantt  
- Documentació inicial en Markdown  

#### 🟩 Done

- ✅ Reunió inicial d’equip → metodologia escollida (Scrum + Kanban)  
- ✅ Creació del tauler GitHub Projects / Trello  
- ✅ Creació del repositori remot i invitació als col·laboradors  

<figure>
  <img src="imagenes/01/d837dfa6-b7b4-4945-80ce-15275925e7a1.png" />
  <figcaption>Exemple Kanban</figcaption>
</figure>
  
---

### 🏷️ Exemple d’etiquetes
- 🖥️ Backend  
- 🎨 Frontend  
- 📄 Documentació  
- 🐞 Bug  
- ⏳ Urgent  
- ⭐ Millora  

