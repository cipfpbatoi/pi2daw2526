# Treball i evidències en GitHub

## Un repositori per projecte

Cada proposta tindrà un únic repositori, creat a partir de la plantilla del curs. El repositori pertany al **projecte**, no a una parella: quan hi haja un relleu, canviarà la custòdia, però es conservaran l'historial i les autories.

Utilitzeu [`cipfpbatoi/pi2627-plantilla-projecte`](https://github.com/cipfpbatoi/pi2627-plantilla-projecte). Podeu crear un repositori nou amb **Use this template** o clonar-lo si així ho indica el professorat.

```bash
git clone https://github.com/cipfpbatoi/pi2627-plantilla-projecte.git nom-del-projecte
cd nom-del-projecte
git remote remove origin
git remote add origin URL_DEL_REPOSITORI_NOU
git push -u origin main
```

No intenteu enviar canvis al repositori plantilla. Si useu **Use this template**, GitHub ja crearà un repositori independent i no necessitareu canviar el remot.

GitHub serà l'espai de treball habitual per a documentació, tasques, decisions, codi, proves i traspassos. No entregueu còpies diferents del mateix document en altres espais.

## On es registra cada cosa

| Element | Mecanisme |
| --- | --- |
| Documents i plantilles | Fitxers versionats del repositori |
| Treball pendent o en curs | *Issues* assignades |
| Revisió abans d'incorporar canvis | *Pull requests* |
| Decisions rellevants | `docs/00-control/decisions.md` |
| Fonts i ús d'IA | `docs/00-control/fonts-ia.md` |
| Incidències i canvis | *Issues* amb la plantilla corresponent |
| Proves i resultats | `docs/04-seguiment/proves/` i issue relacionada |
| Estat exacte d'un lliurament | Etiqueta i *release* |
| Traspàs | Acta versionada i issue de consulta/acceptació |

## Flux mínim d'una tasca

La plantilla conté **formularis per crear issues**, però no una llista de tasques resolta per endavant. Definir què cal fer, quin resultat s'espera, de què depén i com es comprovarà forma part del vostre treball i de les evidències del projecte.

En el bloc 1, el professorat podrà crear una única issue de **posada en marxa** per comprovar l'accés i mostrar el procediment. A partir d'ací, cada parella crearà les issues necessàries per analitzar, planificar i revisar el cas. En els projectes reals s'aplicarà el mateix criteri.

1. Creeu una issue amb resultat esperat, responsable, dependències i evidència.
2. Assigneu-la abans de començar.
3. Treballeu en una branca curta.
4. Feu commits comprensibles i relacionats amb la issue.
5. Obriu una *pull request* i indiqueu què canvia i com s'ha comprovat.
6. L'altra persona revisa o formula observacions.
7. Incorporeu-la només quan complisca la definició de `Fet`.
8. Tanqueu la issue amb un enllaç al resultat.

Una tasca està `Feta` quan el resultat és accessible, revisat, provat quan pertoque, documentat i relacionat amb l'evidència corresponent.

## Evidències individuals

Els commits no són una mesura automàtica de l'aportació. Cada membre mantindrà `evidencies/alumnat/nom-cognoms.md` i enllaçarà contribucions verificables:

| Data | Fase i projecte | Funció | Aportació | Enllaç | Decisió o aprenentatge | RA.CA orientatiu |
| --- | --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |  |

Poden servir com a evidència:

- una issue ben definida o resolta;
- una *pull request* pròpia;
- una revisió amb observacions útils;
- un fragment identificable d'un document;
- una decisió argumentada;
- una prova i la interpretació del resultat;
- una consulta de traspàs que detecta una mancança;
- una explicació o defensa contrastada pel professorat.

No són suficients per si sols el nombre de commits, les hores declarades, aparéixer com a coautor sense traça o pujar fitxers generats sense revisió.

## Versions i punts de control

En cada lliurament, creeu una etiqueta sobre el commit revisat:

```text
dossier-1-v1.0
dossier-2-v1.0
pla-v1.0
iteracio-1-v0.1
prototip-v1.0
tancament-v1.0
```

La *release* indicarà equip custodi, contingut, limitacions, riscos i enllaç a l'acta quan hi haja traspàs. No moveu ni reutilitzeu una etiqueta publicada; creeu-ne una versió nova.

## Regles d'autoria i seguretat

- Cada persona utilitzarà el seu compte i no compartirà credencials.
- No feu commits directes amb el compte d'una altra persona.
- No guardeu contrasenyes, tokens, dades personals reals ni converses privades.
- Utilitzeu dades fictícies o anonimitzades.
- Declareu l'ajuda de la IA i la comprovació humana.
- No reescriviu l'historial compartit per ocultar errors; corregiu-los amb una nova versió.
- Els acords externs que afecten el projecte s'han de registrar al repositori.

## Traspàs de custòdia

L'equip emissor crea la release i l'acta. L'equip receptor revisa eixa versió exacta, obri les consultes necessàries i registra si accepta, accepta amb reserves o retorna temporalment el producte. Després de l'acceptació, les noves decisions corresponen al receptor; l'autoria anterior es conserva.
