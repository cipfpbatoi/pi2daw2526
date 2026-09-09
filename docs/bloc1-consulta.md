# Material de consulta del bloc 1

Esta pàgina reunix els conceptes i les referències necessàries per preparar el **Dossier 0**. No cal llegir tots els recursos externs de principi a fi: en cada activitat s'indicarà quin apartat convé consultar.

## 1. Del problema a la solució

Abans de proposar funcionalitats, cal diferenciar:

| Concepte | Pregunta que respon | Exemple |
| --- | --- | --- |
| Necessitat | Què necessita millorar una persona o organització? | Consultar les places disponibles sense telefonar |
| Problema | Què impedix satisfer la necessitat? | La informació està repartida en diferents fitxers |
| Causa | Per què es produïx el problema? | No hi ha una font de dades compartida |
| Conseqüència | Què ocorre si no es resol? | Inscripcions duplicades i més treball administratiu |
| Objectiu | Quin canvi es vol aconseguir? | Reduir els errors en la gestió d'inscripcions |
| Solució | Com es podria aconseguir? | Aplicació web, reorganització del procés o integració de ferramentes existents |

Una mateixa necessitat pot tindre diverses solucions. La primera idea tecnològica no s'ha de convertir automàticament en la solució definitiva.

### Preguntes de consulta

- Qui experimenta el problema?
- Amb quina freqüència ocorre?
- Quines evidències demostren que existix?
- Què es fa actualment per resoldre'l?
- Quines restriccions condicionen la resposta?
- Què passaria si no es desenvolupara cap aplicació?

## 2. Parts interessades

Una **part interessada** és qualsevol persona, grup o organització que pot afectar el projecte, resultar afectada o tindre interés en el seu resultat.

Per identificar-les, es pot completar una taula com esta:

| Part interessada | Necessitat o interés | Influència | Informació que necessitem | Com hi contactarem |
| --- | --- | --- | --- | --- |
| Persona usuària |  |  |  |  |
| Responsable de l'organització |  |  |  |  |
| Equip tècnic |  |  |  |  |

No totes les parts interessades utilitzaran directament l'aplicació. També cal considerar qui aporta dades, autoritza decisions, paga recursos, dona suport o assumix riscos.

## 3. Objectius i criteris d'èxit

Un objectiu descriu un canvi que es vol aconseguir; una tasca descriu una acció que cal executar.

- **Objectiu:** reduir el temps necessari per gestionar una inscripció.
- **Tasca:** crear el formulari d'inscripció.

Un objectiu útil ha de ser prou concret per poder comprovar-lo. Es pot revisar amb estes preguntes:

- descriu un resultat i no només una activitat?;
- es pot observar o mesurar?;
- és realista amb els recursos disponibles?;
- està relacionat amb el problema?;
- indica, quan siga necessari, un termini?

Els **criteris d'èxit** indiquen quines evidències permetran decidir si l'objectiu s'ha aconseguit. No han de dependre exclusivament de frases vagues com «que funcione bé» o «que siga fàcil d'usar».

## 4. Abast, exclusions i hipòtesis

L'abast definix què produirà el projecte i quins límits tindrà.

Una definició inicial ha d'incloure:

- funcionalitats o resultats inclosos;
- elements que queden expressament fora;
- persones usuàries considerades;
- dades i sistemes implicats;
- restriccions de temps, cost o tecnologia;
- hipòtesis que encara no s'han pogut verificar.

Per prioritzar, es poden utilitzar quatre grups:

| Prioritat | Significat |
| --- | --- |
| Imprescindible | Sense este element, el prototip no resol el recorregut principal |
| Convenient | Aporta valor important, però el prototip encara es pot validar sense ell |
| Opcional | S'incorporarà només si hi ha temps i recursos |
| Fora de l'abast | No es desenvoluparà en esta versió |

Prioritzar no consistix a marcar-ho tot com a imprescindible. Cada classificació ha de tindre una justificació.

## 5. Lliurables, tasques i dependències

Un **lliurable** és un resultat comprovable. Una **tasca** és el treball necessari per produir-lo.

```text
Projecte
├── Lliurable 1: proposta validada
│   ├── Identificar parts interessades
│   ├── Fer les entrevistes
│   └── Documentar conclusions
└── Lliurable 2: prototip funcional
    ├── Dissenyar el model de dades
    ├── Implementar el recorregut principal
    └── Executar les proves
```

Una tasca ben definida:

- comença amb un verb d'acció;
- produïx un resultat observable;
- té una persona responsable;
- es pot estimar;
- té un criteri de finalització;
- indica si depén d'una altra tasca.

«Fer el backend» és massa ampli. «Implementar i provar l'alta d'activitats» permet estimar i comprovar millor el treball.

## 6. Estimacions i cronograma

Una estimació és una previsió, no una promesa. Ha d'explicitar les hipòtesis utilitzades i revisar-se quan s'obté informació nova.

Per estimar una tasca, cal considerar:

- treball de preparació i investigació;
- implementació;
- coordinació;
- proves i correccions;
- documentació;
- marge davant de la incertesa.

Un diagrama de Gantt representa les tasques sobre una línia temporal i permet mostrar duracions, dependències i fites. No substituïx el raonament: un cronograma visualment correcte pot continuar sent inviable si les estimacions o dependències no són realistes.

Per crear-lo es pot utilitzar una taula, un full de càlcul o GanttProject. La [documentació oficial de GanttProject](https://docs.ganttproject.biz/) explica el funcionament de la ferramenta.

## 7. Recursos i pressupost

Els recursos no són només diners. Cal considerar:

- hores de les persones de l'equip;
- equipament i dispositius de prova;
- allotjament, dominis i infraestructura;
- llicències o subscripcions;
- serveis externs i APIs;
- formació o assessorament;
- manteniment i costos recurrents.

Una estimació inicial pot utilitzar:

```text
Cost de personal = hores estimades × cost per hora
Cost total = personal + infraestructura + serveis + altres costos
```

Si un recurs és gratuït, també se n'han de revisar les limitacions, les condicions d'ús i el cost que podria tindre després del prototip.

## 8. Riscos

Un risc és un esdeveniment incert que, si ocorre, pot afectar els objectius. Un problema que ja ha ocorregut és una incidència i necessita una actuació immediata.

Un registre bàsic pot contindre:

| Risc | Causa | Probabilitat | Impacte | Prevenció | Resposta | Responsable |
| --- | --- | --- | --- | --- | --- | --- |
|  |  | Baixa/mitjana/alta | Baix/mitjà/alt |  |  |  |

Cal buscar riscos de diferents tipus:

- tècnics;
- temporals;
- organitzatius i d'equip;
- econòmics;
- seguretat i protecció de dades;
- dependència de tercers;
- usabilitat i accessibilitat.

Una llista extensa no és necessàriament millor. Cal prioritzar els riscos que combinen una probabilitat i un impacte significatius.

## 9. Metodologia i seguiment

La metodologia ha d'ajudar l'equip a saber:

- quin treball està pendent;
- què s'està fent;
- qui n'és responsable;
- què està bloquejat;
- què s'ha acabat i comprovat;
- quina serà la pròxima prioritat.

Un tauler mínim pot contindre `Pendent`, `En curs`, `En revisió` i `Fet`. Cada equip pot adaptar-lo, però ha de definir què significa passar una tasca d'un estat a un altre.

GitHub permet relacionar repositoris, *issues*, responsables, dependències, *pull requests* i taulers. Es pot consultar la guia [Planificació i seguiment del treball](https://docs.github.com/en/issues/tracking-your-work-with-issues/learning-about-issues/planning-and-tracking-work-for-your-team-or-project) i la documentació de [GitHub Projects](https://docs.github.com/en/issues/planning-and-tracking-with-projects).

## 10. Fonts i ús d'intel·ligència artificial

Una font ha de permetre identificar, com a mínim, l'autoria o entitat responsable, el títol, la data quan estiga disponible i l'adreça de consulta.

Per valorar-la, cal preguntar:

- qui publica la informació?;
- aporta proves o referències?;
- està actualitzada?;
- té una finalitat informativa, comercial o d'opinió?;
- coincidix amb altres fonts fiables?;
- és la font original de l'afirmació?

L'ús d'IA s'ha de declarar. Una declaració breu pot seguir este model:

> S'ha utilitzat [ferramenta] per a [finalitat]. Ha proporcionat [tipus d'ajuda]. L'equip ha verificat el resultat mitjançant [font, prova o revisió] i ha realitzat [canvis principals].

La [guia de la UNESCO sobre IA generativa en educació i investigació](https://www.unesco.org/en/articles/guidance-generative-ai-education-and-research) oferix un marc centrat en l'ús humà, crític i responsable d'estes ferramentes.

## Referències per ampliar

| Recurs | Utilitat en el bloc |
| --- | --- |
| [Metodologia PM² de la Comissió Europea](https://pm2.europa.eu/pm2-methodologies/pm2-project-management_en) | Cicle de vida, parts interessades, governança, planificació, riscos i artefactes de projecte |
| [Recursos i plantilles PM²](https://pm2.europa.eu/pm2-resources_en) | Guies i models oberts que es poden simplificar per al Dossier 0 |
| [GitHub: planificació i seguiment](https://docs.github.com/en/issues/tracking-your-work-with-issues/learning-about-issues/planning-and-tracking-work-for-your-team-or-project) | Descomposició del treball, *issues*, dependències i coordinació |
| [Documentació de GitHub Projects](https://docs.github.com/en/issues/planning-and-tracking-with-projects) | Taulers, camps, vistes, prioritats i iteracions |
| [Documentació de GanttProject](https://docs.ganttproject.biz/) | Creació i manteniment d'un diagrama de Gantt |
| [Planificació de l'accessibilitat del W3C](https://www.w3.org/WAI/planning-and-managing/) | Incorporació de l'accessibilitat als objectius, recursos, responsabilitats i seguiment |
| [Guia de protecció de dades per defecte de l'AEPD](https://www.aepd.es/guias/guia-proteccion-datos-por-defecto.pdf) | Consideració de la privacitat des del disseny de la solució |
| [Guia de la UNESCO sobre IA generativa](https://www.unesco.org/en/articles/guidance-generative-ai-education-and-research) | Ús crític, responsable i centrat en les persones |

!!! note "Com utilitzar les referències"

    No s'espera que apliqueu una metodologia professional completa. Heu de seleccionar i adaptar les idees que ajuden a justificar i controlar el vostre projecte.
