# Desenvolupament d'aplicacions web: Accés a Dades.
 
## 1. Introducció a les tecnologies per accedir a dades

### Bases de dades relacionals (SQL)
Les bases de dades relacionals utilitzen llenguatge SQL per emmagatzemar i recuperar dades de taules relacionades. En PHP, les tecnologies més utilitzades per accedir-hi són **PDO** i **MySQLi**. **PDO** suporta múltiples sistemes de bases de dades (MySQL, PostgreSQL, etc.), mentre que **MySQLi** està dissenyat específicament per a MySQL.

### Bases de dades NoSQL
Les bases de dades NoSQL, com **MongoDB** o **Firebase**, emmagatzemen dades en formats no estructurats, com JSON. Aquestes són ideals per a aplicacions que gestionen grans volums de dades o dades no estructurades. **MongoDB** és un sistema orientat a documents, mentre que **Firebase** és conegut per les seves capacitats en temps real.

### Accés a APIs
Les **APIs REST** permeten accedir a dades de serveis web externs utilitzant sol·licituds HTTP i respostes en formats com JSON o XML. **GraphQL** és una alternativa moderna que permet sol·licituds més específiques, només retornant les dades necessàries, en contrast amb les sol·licituds REST, que poden ser més generals.

### Web Scraping
El **web scraping** és el procés d'extracció automàtica de dades de pàgines web. Aquesta tècnica es pot utilitzar per recuperar informació d'una pàgina web quan no hi ha una API disponible. En PHP, es poden utilitzar diverses biblioteques per descarregar i analitzar contingut HTML, com ara **cURL** i **DOMDocument**.

### Consideracions de seguretat
És fonamental garantir la seguretat quan es treballa amb l'accés a dades. Això inclou protegir les aplicacions contra vulnerabilitats comunes, com les **injeccions SQL**, i assegurar les connexions utilitzant **SSL/TLS** quan es comuniqui amb bases de dades remotes o APIs externes.


## 2. Bases de dades relacionals (SQL)

### Instal·lació
A través de **XAMPP** és molt senzill, simplement ens descarregaríem el programa i l'activaríem. Per a descarregar XAMPP [prem ací](https://www.apachefriends.org/es/download.html).

Amb ***Docker*** utilitzarem un altre  repositori que inclou el mysql i el phpMyAdmin i llancem
``` bash
docker-compose up -d
```

Si tot ha eixit bé i el contenidor està en marxa, podrem visitar la pàgina de phpMyAdmin de la següent manera
``` html
http://localhost:8000
```

 

Per a accedir hem d'utilitzar les següents credencials que venen configurades en el arxiu `docker-compose.yml`

```
usuario: root
contraseña: 1234
```

### Estructura d'una base de dades

Sabem que una base de dades té molts camps amb els seus noms i valors, però a més sabem que la base de dades ha de tindre un nom. per tant tindríem la següent estructura per a una base de dades:
    
    NombreBaseDeDatos
        |__Tabla-#1
        |       |__DatosTabla-#1
        |
        |__Tabla-#2
        |       |__DatosTabla-#2
        |
        |__Tabla-#3
        |       |__DatosTabla-#3
        [...]


Vegem-ho en un exemple real

    Ryanair
        |__pasajero
        |    |__id[*]
        |    |__nombre
        |    |__apellidos
        |    |__edad
        |    |__id_vuelo[^]
        |
        |__vuelo
        |    |__id[*]
        |    |__n_plazas
        |    |__disponible
        |    |__id_pais[^]
        |
        |__pais
             |__id[*]
             |__nombre

<div class="leyenda">
    [*] Clau primària [^] Clave Forània
</div>

 
### SQL

Aquest llenguatge de consulta estructurada (*Structured Query Language*) és el que utilitzarem per a realitzar les consultes a les nostres bases de dades per a mostrar el contingut en les diferents interfícies web que creem al llarg de la unitat. Si vols saber més detalls visita [Wiki SQL](https://es.wikipedia.org/wiki/sql)

Exemple d'una sentència SQL on seleccionem totes les files i columnes de la nostra taula anomenada **'pais'**

``` sql
SELECT * FROM pais
```

Estas sentencias pueden invocarse desde la consola de comandos mediante el intérprete *mysql* (previamente instalado en el sistema) o a través de la herramienta phpMyAdmin.

Las sentencias SQL también las podemos usar dentro de nuestro código php, de tal manera que cuando se cargue nuestra interfaz web, lance una sentecia SQL para mostrar los datos que queramos.

``` php
<?php
    // Llistat de clients, adreçats per DNI de manera ASCendent
    $clientesOrdenadosPorDNI = "SELECT * FROM `pasajero` ORDER BY `dni`" ASC;
?>
```

### phpMyAdmin
 

Aquest programari funciona sota Ngingx i PHP i és més que res una interfície web per a gestionar les bases de dades que tinguem disponibles en el nostre servidor local. Molts **hostings* ofereixen aquesta eina per defecte per a poder gestionar les BBDD que tinguem configurades sota el nostre compte.

#### Creant una base de dades dins de phpMyAdmin

 

1.  Per a crear una nova base de dades hem d'entrar en *phpMyAdmin* com a *usuari root* i punxar en l'opció <span class="warning">*Nova*</span> del menú de l'esquerra.

2. En la nova finestra de creació posarem un **nom** a nostra *bbdd*.

3. També establirem el **cotejamiento** <span class="warning">*utf8m4_unicode_ci*</span> perquè nostra *bbdd* suporte tot tipus de caràcters (com els asiàtics) i fins i tot *emojis* ;)

4. Li donem al botó de **Crear** per a crear la *bbdd* i començar a escriure les diferents taules que anem a introduir en ella.

El sistema generarà el codi SQL per a crear tot el que li hem posat i crearà la base de dades amb les taules que li hàgem ficat.
``` sql
CREATE TABLE `persona`. ( `id` INT NOT NULL AUTO_INCREMENT , `nombre` TINYTEXT NOT NULL , `apellidos` TEXT NOT NULL , `telefono` TINYTEXT NOT NULL , PRIMARY KEY (`id`)) ENGINE = InnoDB;
```

#### Opcions en phpMyAdmin

Quan seleccionem una base de dades de la llista, el sistema ens mostra diverses pestanyes amb les quals interactuar amb la base de dades en qüestió:

- `Estructura`: Podem veure les diferents taules que consoliden la nostra base de dades

- `SQL`: Per si volem injectar codi SQL perquè el sistema l'interprete

- `Buscar`: Serveix per a buscar per termes, en la nostra base de dades, aplicant diferents filtres de cerca

- `Generar consulta`: semblança a SQL però d'una manera més gràfica, sense haver de saber res del llenguatge

- `Exportar i importar`: Com el seu nom indica, per a fer qualsevol de les 2 operacions sobre la base de dades

- `Operacions`: Diferents opcions avançades per a realitzar en la nostra base de dades, de la qual destacarem l'opció *Cotejamiento* on podrem canviar el *cotejamiento* de la nostra taula però <span class="alert">*ULL AMB ACÔ* perquè podem eliminar dades sense voler, ja que en canviar el *cotejamiento* podem suprimir caràcters no suportats pel nou *cotejamiento*</span>

No aprofundirem en la resta d'opcions però, en la pestanya **Més** existeix l'opció **Dissenyador** per a poder editar les relacions entre taules d'una manera gràfica (punxant i arrossegant) que veurem més endavant.

## 3. PHP Data Objects :: PDO

La classe PDO de PHP s'utilitza per connectar-se a una base de dades i executar consultes SQL de manera segura. Quan construeixes una instància de PDO, pots passar-li diferents atributs en el constructor i opcions per configurar el comportament de la connexió. Aquí tens els atributs principals i el seu propòsit:

### Constructor de la classe PDO

El constructor de la classe PDO accepta tres paràmetres obligatoris i un opcional:

``` php
<?php
    $pdo = new PDO(string $dsn, string $username, string $password, array $options);

```

* $dsn (Data Source Name): És una cadena que especifica el tipus de base de dades i la informació necessària per connectar-s'hi.
  * Format per tipus de base de dades i configuració, per exemple:
    * Mysql:host=localhost;dbname=testdb (per a MySQL).
    * pgsql:host=localhost;port=5432;dbname=testdb (per a PostgreSQL).
    * sqlite:/path/to/database.db (per a SQLite).
  * $username: El nom d'usuari per a la connexió a la base de dades.
  * $password: La contrasenya associada al nom d'usuari.
  * $options (Opcional): Un array d'opcions per definir el comportament de la connexió. Aquests són alguns dels valors més comuns que es poden definir en aquest array:
    * PDO::ATTR_ERRMODE: Controla com es gestionen els errors. Alguns valors comuns són:
      * PDO::ERRMODE_SILENT: Els errors no generen cap missatge.
      * PDO::ERRMODE_WARNING: Els errors generen un avís.
      * PDO::ERRMODE_EXCEPTION: Els errors generen una excepció, que és el més recomanable per controlar errors.
    * PDO::ATTR_DEFAULT_FETCH_MODE: Defineix el mode de recuperació de dades per defecte, com ara:
      * PDO::FETCH_ASSOC: Retorna les dades com un array associatiu.
      * PDO::FETCH_OBJ: Retorna les dades com un objecte.
      * PDO::FETCH_BOTH: Retorna les dades com un array associatiu i numèric.
    * PDO::ATTR_PERSISTENT: Habilita connexions persistents. Una connexió persistent pot millorar el rendiment mantenint la connexió activa per múltiples peticions en lloc de crear-ne una nova cada vegada.
    * PDO::ATTR_TIMEOUT: Defineix un temps límit per a la connexió en segons.

##### Exemple de connexió amb PDO

``` php     
$dsn = "mysql:host=localhost;dbname=testdb";
$username = "usuari";
$password = "contrasenya";
$options = [
    PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
    PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,
    PDO::ATTR_PERSISTENT => true,
    PDO::MYSQL_ATTR_INIT_COMMAND => "SET NAMES utf8"
];

try {
    $pdo = new PDO($dsn, $username, $password, $options);
    echo "Connexió establerta amb èxit!";
} catch (PDOException $e) {
    echo "Error de connexió: " . $e->getMessage();
}
```

Aquest codi estableix una connexió a una base de dades MySQL amb un joc de caràcters utf8, una connexió persistent, i llança excepcions en cas d'errors.

 
Qualsevol error que es llance a través de **PDO**, el sistema llançarà una  **PDOException** .

### Fitxer de configuració de la BD

De la mateixa manera que podem tenir el nostre arxiu de funcions `funciones.php` i alberguem totes les funcions que s'usen de manera global en l'aplicació, podem establir un arxiu de constants on definim els paràmetres de connexió amb la base de dades.
```php
<?php

    //  ▒▒▒▒▒▒▒▒ conexion.php ▒▒▒▒▒▒▒▒

    constDSN = "mysql:host=localhost;dbname=dwes";
    constUSUARIO = "dwes";
    constPASSWORD = "abc123";

    /*  ▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒

        ▒▒▒▒▒▒▒▒ NO SUBAS ESTE ARCHIVO A git ▒▒▒▒▒

        ▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒ */

```

Aquest arxiu conté informació <span class="alert">**molt sensible**</span> així que no és recomanable que puges aquest arxiu a **git**.

### Sentències preparades

Es tracta de sentències que s'estableixen com si foren plantilles de la SQL que llançarem, acceptant paràmetres que són establits a posteriori de la declaració de la sentència preparada.

Les sentències preparades eviten la **injecció** de SQL (SQL Injection) i milloren el rendiment de nostres *aplicacions* o pàgines web.

``` php
<?php
    $sql = "INSERT INTO Clientes VALUES (?, ?, ?, ?)";
```

Cada interrogant és un paràmetre que establirem després, unes quantes línies més a baix.

Una vegada tenim la plantilla de la nostra consulta, hem de seguir amb la preparació juntament amb 3 mètodes més de **PHP** per a la seua completa execució:

- `prepare:` prepara la **sentencia** abans de ser executada.
- `bind`: el tipus d'unió (**bind*^) de dada que pot ser mitjançant ' ? ' o ' :parametre '
- `execute` s'executa la consulta unint la plantilla amb les *variables* o paràmetres que hem establit.

### Exemple paràmetros

```php
<?php
     

    include "config/database.inc.php";

    $conexion = null;

    try { 
        $cantidad = $_GET["cantidad"];

        $conexion = new PDO(DSN, USUARIO, PASSWORD);
        $conexion -> setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

        $sql = "DELETE FROM stock WHERE unidades = ?";
        $sentencia = $conexion -> prepare($sql);

        $isOk = $sentencia -> execute([$cantidad]);
        $cantidadAfectada = $sentencia -> rowCount();

        echo $cantidadAfectada;
    } catch (PDOException $e) {
        echo $e -> getMessage();
    }

    $conexion = null
```

### Exemple bindParam

Molt semblant a utilitzar paràmetres però aquesta vegada la variable està dins de la sentència SQL, en aquest cas l'hem anomenada `:cant`

```php
<?php
    include "config/database.inc.php";

    $conexion=null;

    try {
        $cantidad = $_GET["cantidad"] ?? 0;

        $conexion = new PDO(DSN, USUARIO, PASSWORD);
        $conexion -> setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

        $sql = "DELETE FROM stock WHERE unidades = :cant";

        $sentencia = $conexion -> prepare($sql);
        $sentencia -> bindParam(":cant", $cantidad);
        
        $isOk = $sentencia -> execute();
        
        $cantidadAfectada = $sentencia -> rowCount();
        
        echo $cantidadAfectada;
    } catch (PDOException $e) {
        echo $e -> getMessage();
    }

    $conexion = null;
```

### bindParam VS bindValue

Utilitzarem `bindValue()` quan hàgem d'inserir dades només una vegada, en canvi, haurem d'usar `bindParam()` quan hàgem de passar dades múltiples, com per exemple, un *array*.

```php
<?php
    // se asignan nombre a los parámetros
    $sql = "DELETE FROM stock WHERE unidades = :cant";
    $sentencia = $conexion -> prepare($sql);

    // bindParam enlaza por referencia
    $cantidad = 0;

    $sentencia -> bindParam(":cant", $cantidad);
    $cantidad = 1;

    // se eliminan con cant = 1
    $isOk = $sentencia -> execute();

    // bindValue enlaza por valor
    $cantidad = 0;

    $sentencia -> bindValue(":cant", $cantidad);
    $cantidad = 1;

    // se eliminan con cant = 0
    $isOk = $sentencia->execute();
```

Per a més informació i ús de les variables *PDO* [consulta el manual de PHP](https://www.php.net/manual/es/pdo.constants.php).

### Inserint registres

A l'hora d'inserir registres en una base de dades, hem de tindre en compte que en la taula pot haver-hi valors autoincrementats. Per a salvaguardar açò, el que hem de fer és deixar aqueix camp autoincrementat buit, però a l'hora de fer la connexió, hem de recuperar-ho amb el mètode `lastInsertId()`.

``` php
<?php
    $nombre = $_GET["nombre"] ?? "SUCURSAL X";
    $telefono = $_GET["telefono"] ?? "636123456";

    $sql="INSERT INTO tienda(nombre, tlf) VALUES (:nombre, :telefono)";

    $sentencia = $conexion -> prepare($sql);
    $sentencia -> bindParam(":nombre", $nombre);
    $sentencia -> bindParam(":telefono", $telefono);

    $isOk = $sentencia -> execute();
    $idGenerado = $conexion -> lastInsertId();

    echo $idGenerado;
```

### Consultant registres

A l'hora de recuperar els resultats d'una consulta, bastarà amb invocar al mètode `PDOStatement::fetch` per a llistar les files generades per la consulta.

Però hem de triar el tipus de dada que volem rebre entre els 3 que hi ha disponibles:

- `PDO::FETCH_ASSOC:` array indexat que els seus keys són el nom de les columnes.
- `PDO::FETCH_NUM:` array indexat que els seus keys són números.
- `PDO::FETCH_BOTH:` valor per defecte. Retorna un array indexat que els seus keys són tant el nom de les columnes com números.

 

``` php
<?php
    //  ▒▒▒▒▒▒▒▒ consulta con array asociativo.php ▒▒▒▒▒▒▒▒

    include "config/database.inc.php";

    $conexion = null;

    try{
        $conexion = new PDO(DSN, USUARIO, PASSWORD);
        $conexion -> setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

        $sql = "select * from tienda";

        $sentencia = $conexion -> prepare($sql);
        $sentencia -> setFetchMode(PDO::FETCH_ASSOC);
        $sentencia -> execute();
        
        while($fila = $sentencia -> fetch()){
            echo "Codigo:" . $fila["cod"] . "<br />";
            echo "Nombre:" . $fila["nombre"] . "<br />";
            echo "Teléfono:" . $fila["tlf"] . "<br />";
        }

    }catch(PDOException $e) {
        echo $e -> getMessage();
    }

    $conexion = null;
```

Recuperant dades amb una matriu com a resultat de la nostra consulta

``` php
<?php
    //  ▒▒▒▒▒▒▒▒ consulta con array asociativo ▒▒▒▒▒▒▒▒

    $sql="SELECT * FROM tienda";

    $sentencia = $conexion -> prepare($sql);
    $sentencia -> setFetchMode(PDO::FETCH_ASSOC);
    $sentencia -> execute();

    $tiendas = $sentencia -> fetchAll();

    foreach($tiendasas$tienda) {
        echo"Codigo:" . $tienda["cod"] . "<br />";
        echo"Nombre:" . $tienda["nombre"] . "<br />";
    }
```
Però si el que volem és llegir dades amb forma d'objecte utilitzant `PDO::FETCH_OBJ`, hem de crear un objecte amb propietats públiques amb el mateix nom que les columnes de la taula que anem a consultar.

``` php
<?php
    //  ▒▒▒▒▒▒▒▒ consulta con formato de objeto ▒▒▒▒▒▒▒▒

    $sql="SELECT * FROM tienda";

    $sentencia = $conexion -> prepare($sql);
    $sentencia -> setFetchMode(PDO::FETCH_OBJ);
    $sentencia -> execute();

    while($t = $sentencia -> fetch()) {
        echo"Codigo:" . $t -> cod . "<br />";
        echo"Nombre:" . $t -> nombre . "<br />";
        echo"Teléfono:" . $t -> tlf . "<br />";
    }
```

### Consultes amb models

Portem temps creant classes en PHP i les consultes també admeten aquest tipus de dades mitjançant l'ús de `PDO::FETCH_CLASS`

Si usem aquest mètode, hem de tindre en compte que els noms dels atributs privats han de coincidir amb els noms de les columnes de la taula que anem a manejar.

Així doncs, si pel que siga canviem l'estructura de la taula <span class="alert">**HEM DE CANVIAR**</span> la nostra classe perquè tot continue funcionant.

``` php
<?php
    //  ▒▒▒▒▒▒▒▒ clase Tienda ▒▒▒▒▒▒▒▒

    classTienda {
        private int $cod;
        private string $nombre;
        private ? string $tlf;
        
        public function getCodigo() : int {
            return $this -> cod;
        }
        
        public function getNombre() : string {
            return $this -> nombre;
        }
        
        public function getTelefono() : ?string {
            return $this -> tlf;
        }
    }
```

``` php
<?php
    //  ▒▒▒▒▒▒▒▒ Consultando a través de la clase Tienda ▒▒▒▒▒▒▒▒

    $sql = "SELECT * FROM tienda";
    $sentencia = $conexion -> prepare($sql);

    // Aquí 'Tienda' es el nombre de nuestra clase
    $sentencia -> setFetchMode(PDO::FETCH_CLASS, Tienda::class);
    $sentencia -> execute();

    while($t = $sentencia -> fetch()) {
        echo "Codigo: " . $t -> getCodigo() . "<br />";
        echo "Nombre: " . $t -> getNombre() . "<br />";
        echo "Teléfono: " . $t -> getTelefono() . "<br />";
        
        var_dump($t);
    }
```

Però què passa si les nostres classes tenen constructor? doncs que hem d'indicar-li, al mètode FECTH, que emplene les propietats després de cridar al constructor i per a això fem ús de `PDO::FETCH_PROPS_LATE`.
``` php
<?php
    //  ▒▒▒▒▒▒▒▒ Consulta para una clase con constructor ▒▒▒▒▒▒▒▒

    $sql = "SELECT * FROM tienda";

    $sentencia = $conexion -> prepare($sql);
    $sentencia -> setFetchMode(PDO::FETCH_CLASS | PDO::FETCH_PROPS_LATE, Tienda::class);
    $sentencia -> execute();

    $tiendas = $sentencia -> fetchAll();
```

### Consultes amb LIKE

Per a utilitzar el comodí *LIKE* o altres comodins, hem d'associar-lo a la dada i MAI en la pròpia consulta.

``` php
<?php
    //  ▒▒▒▒▒▒▒▒ Utilizando comodines :: LIKE ▒▒▒▒▒▒▒▒

    $sql = "SELECT * FROM tienda where nombre like :nombre or tlf like :tlf";

    $sentencia = $conexion -> prepare($sql);
    $sentencia -> setFetchMode(PDO::FETCH_CLASS | PDO::FETCH_PROPS_LATE, Tienda::class);

    $cadBuscar = "%" . $busqueda . "%";

    $sentencia -> execute(["nombre" => $cadBuscar,"tlf" => $cadBuscar]);

    $result = $sentencia -> fetchAll();
```

Teniu una llista d'exemples molt completa en la [documentació oficial](https://phpdelusions.net/pdo/objects).

## 4. Login & Password
 

Per a manejar un sistema complet de login i password amb contrasenyes xifrades, necessitem un mètode que xifre aqueixos *strings* que l'usuari introdueix com a contrasenya; tant en el formulari de registre com en el del *login*, ja que en codificar una contrasenya, després hem de descodificar-la per a comprovar que totes dues *contrasenyes (la que introdueix l'usuari en el login i la que tenim en la base de dades) coincidisquen.

Necessitem doncs:

- `password_hash()` per a emmagatzemar la contrasenya en la base de dades a l'hora de fer el *INSERT*
- `PASSWORD_DEFAULT` emmagatzemem la contrasenya usant el mètode d'encriptació bcrypt

- `PASSWORD_BCRYPT` emmagatzemem la contrasenya usant l'algorisme CRYPT_BLOWFISH compatible amb crypt()

- `password_verify()` per a verificar l'usuari i la contrasenya

``` php
<?php
    //  ▒▒▒▒▒▒▒▒ Almacenando usuario y password en BD ▒▒▒▒▒▒▒▒

    $usu = $_POST["usuario"];
    $pas = $_POST["password"];

    $sql = "INSERT INTO usuarios(usuario, password) VALUES (:usuario, :password)";

    $sentencia = $conexion -> prepare($sql);

    $isOk = $sentencia -> execute([
        "usuario" => $usu,
        "password" => password_hash($pas,PASSWORD_DEFAULT)
    ]);
```

Ara que tenim l'usuari codificat i guardat en la base de dades, el recuperarem per a poder loguejar-lo correctament.
``` php
<?php
    //  ▒▒▒▒▒▒▒▒ Recuperando usuario y password en BD ▒▒▒▒▒▒▒▒

    $usu = $_POST["login"] ?? "";

    $sql = "select * from usuarios where usuario = ?";

    $sentencia = $conexion -> prepare($sql);
    $sentencia -> execute([$usu]);

    $usuario = $sentencia -> fetch();

    if($usuario && password_verify($_POST['pass'], $usuario['password'])) {
        echo"OK!";
    } else {
        echo"KO";
    }
```
 
## 5. Exercisis

### Bateria d'exercicis solucionats 
 
##### Exercici 1. Connexió bàsica

1. Crea un fitxer PHP que faça una connexió a una base de dades MySQL utilitzant PDO.

<details>
<summary>Solució</summary>

``` php
<?php
try {
    $dsn = 'mysql:host=db;dbname=pruebadb';
    $usuari = 'root';
    $contrasenya = '1234';
    $pdo = new PDO($dsn, $usuari, $contrasenya);
    echo "Connexió establerta!";
} catch (PDOException $e) {
    echo "Error de connexió: " . $e->getMessage();
}
 
```
</details>


##### Exercici 2. Inserir un registre

1. Escriu una funció que insereixi un nou usuari a la taula `users` amb el nom i correu electrònic passats per paràmetre.

<details>
<summary>Solució</summary>

``` php
function inserirUsuari($nom, $correu) {
    global $pdo;
    $sql = "INSERT INTO users (nom, correu) VALUES (:nom, :correu)";
    $stmt = $pdo->prepare($sql);
    $stmt->bindParam(':nom', $nom);
    $stmt->bindParam(':correu', $correu);
    $stmt->execute();
    echo "Usuari inserit!";
}
```

</details>

##### Exericici 3. Recuperar dades
 
1. Fes una consulta SQL que mostri tots els usuaris registrats a la taula `users` i mostra'ls en una taula HTML.

<details>
<summary>Solució</summary>

``` php
<?php
function mostrarUsuaris() {
    global $pdo;
    $sql = "SELECT * FROM users";
    $stmt = $pdo->query($sql);
    echo "<table>";
    while ($fila = $stmt->fetch(PDO::FETCH_ASSOC)) {
        echo "<tr><td>{$fila['nom']}</td><td>{$fila['correu']}</td></tr>";
    }
    echo "</table>";
}
```

</details>

##### Exercici 4. Actualitzar dades

1. Escriu una funció que actualitzi el correu electrònic d'un usuari segons el seu identificador (`id`).

<details>
<summary>Solució</summary>

``` php
<?php
function actualitzarCorreu($id, $nouCorreu) {
    global $pdo;
    $sql = "UPDATE users SET correu = :correu WHERE id = :id";
    $stmt = $pdo->prepare($sql);
    $stmt->execute([':correu' => $nouCorreu, ':id' => $id]);
    echo "Correu actualitzat!";
}
```

</details>

##### Exercici 5. Eliminar un registre

1. Implementa un script que esborri un usuari per identificador (`id`).

<details>
<summary>Solució</summary>

``` php
<?php
function eliminarUsuari($id) {
    global $pdo;
    $sql = "DELETE FROM users WHERE id = :id";
    $stmt = $pdo->prepare($sql);
    $stmt->execute([':id' => $id]);
    echo "Usuari eliminat!";
}
```
</details>

 

##### Exercici 6. Tractament d'errors

1. Modifica el codi anterior per gestionar els errors amb `try-catch` i mostrar missatges d'error clars.

<details>
<summary>Solució</summary>

``` php
<?php
 try {
    actualitzarCorreu(5, 'noucorreu@example.com');
} catch (PDOException $e) {
    echo "Error en actualitzar: " . $e->getMessage();
}
```
</details>

 