# INDEX

# MongoDB Course

### by Maximillian Academind (Udemy)

---

- # Introducción

  - ## Que es MongoDB

    Es una base de datos preparada para almacenar multitud de datos y poder trajar con ellos de manera eficiente. Lo que lo diferencia del resto bbdd es que mongo es no relacional o no-SQL ddbb.

    Mongo crea un entorno (servidor) donde almacenamos nuestras base de datos.
    Por ejemplo creamos un base de datos "tienda" ésta en lugar de tablas almacena colecciones y dentro de estas tenemos documents que son datos escritos en JSON (JS object notation), su peculiaridad es que no siguen un esquema, de ahí la gran flexibilidad de mongoDB. Esta manera de almacenar datos evita tener que realizar los JOINS de SQL porque podemos almacenar juntos todos los datos que necesitemos.

    En realidad cuando mongoDB guarda los datos lo hace como BSON(Binary object notation ) que esencialmente es una manera más eficiente que jSON.

    ![not found](img/img-1.png)

    - ### Carracterísticas de mongoDB

      - No sigue un esquema
      - Los datos se guardan todos juntos
      - Por lo anterior se eliminan gran parte de las relaciones (JOINS) entre datos

    - ### Ecosistema de mongoDB
      ![not found](img/img-2.png)

  - ## Instalación de mongoDB

    Cómo desinstalar mongo

    ```
      Sudo apt-get remove mongodb* --purge
    ```

    [MongoDb - instalación](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/)

    Puede que tenga problemas al arrancar el servicio:

    - Unmask mongodb

      ```
      sudo systemctl unmask mongod
      ```

    - eliminar el directorio **/var/lib/mongodb**
    - volver a crear el directorio **/var/lib/mongodb**
    - darle permisos sudo **chmod -R 0777 /var/lib/mongodb**

    a esta ruta se la conoce como dbpath si la queremos cambiar por otra rura por ejemplo guardar los datos en nuestro directorio de usuario hacemos:

    ```
    mongod --dbpath "~/data/db"
    ```

    en esta ruta está el archivo de configuración de mongo **/etc/mongodb.conf**
    en el apartado storage podemos cambiar el directorio

    ```
    # Where to store the data.
    dbpath=/var/lib/mongodb
    ```

    depués tenemos la ruta a mongod.conf **/etc/mongod.conf**

    ```
    # Where and how to store data.
    storage:
    dbPath: /var/lib/mongodb
    ```

  - ## Basics

    - ### Comandos iniciales
      Entrar en mongo shell
      ```
      mongo
      ```
      mostrar las bd
      ```
      show dbs
      ```
      acceder a una de las bd o crearla si no existe
      ```
      use dbNAme
      ```
      Una vez dentro crear una primera colección(products) e insertar un item
      ```
      db.products.insertOne( {name: "book", price:10.99 } )
      ```
      Mostrar los datos
      ```
      db.products.find()
      ```
    - ### Drivers

      Podemos usar drivers para conectar nuestra aplicación al servidor de mongoDB según el lenguaje que estemos utilizando (node, python,...) Pero las queries serán iguales que trabajar en el shell de mongoDB

      [MongoDb - Drivers](https://docs.mongodb.com/drivers/)

    - ### Cómo funciona mongoDB

      ![not found](img/img-3.png)

      1. tenemos una app con un lenguae de backend que mediante el uso de drivers conecta con el servidor de mongoDB
      2. el servidor intercaciona con el motor de almacenaje, por defecto es el llamado **wired Tiger**
      3. será este storage engine el que se encargará de encribir los datos en ficheros  
         3.1 El storage engine escribe los datos como último paso pero antes mantiene los datos en memoria para q su acceso sea más rápido
         ![not found](img/img-4.png)

---

- # Operaciones CRUD
