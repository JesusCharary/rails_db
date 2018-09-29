# **Ruby on Rails DB**

## **Configuración Postgres (Windows)**

**1.** Verificar instalación de ruby. versión recomendada para windows. [Ruby+Devkit 2.4.4-2](https://rubyinstaller.org/downloads/)

**2.** Instalar [postgresql](https://www.postgresql.org/download/windows/)  tener en cuenta el usuario administrador y el password de ese usuario.

**3.** Instalar gestor de base de datos ([DBeaver](https://dbeaver.io/download/) *recomendado*)

**4.** Hacer la conexión al servidor de db postgres desde el gestor de base de datos.

**5.** En el gestor de db, crear usuario postgres mediante el cual rails se va a conectar a la base de datos.

```sql
CREATE ROLE rails_user WITH CREATEDB login password "****"
```
**rails_user:** reemplazar por el nombre de usuario deseado

**password:** reemplazar por el password deseado.

**6.** En el gestor de db, crear base de datos que se va a usar para el desarrollo del proyecto.

**7.** En el gestor de db, crear la base de datos que vamos a utilizar para nuestro proyecto.

**8.** 
Instalar Rails
```
$ gem install rails
```

**9.** Instalar el driver de postgres para rails
```
$ gem install pg
``` 
**10.** Agregar postgres al path *(Especificamente agregar la ruta donde se encuentra el directorio /bin)*

**11.** Crear nueva aplicación rails con flags para que sea tipo api y use postgres por defecto.
```
$ rails new app --api --database=postgresql
```
**12.** Configurar la conexión a base de datos por parte de rails en el archivo app_name/config/database.yml

```ruby
development:
    <<: *default
    database: db_example #nombre de la base de datos que creamos en el punto 6
    username: rails_user # user que configuramos en el punto 4.
    host: localhost #ip del servidor donde está alojado la db postgres
    port: 5432 #puerto por donde escucha el servidor de base de datos, para postgres el 5432 por defecto.
```

**13.** Ya creada nuestra configuración, con el generador de rails  podemos crear un modelo para mapearlo en nuestra db.
```
$ rails g mdoel user first_name:string last_name:string
```
**14.** Hacemos la migracíón para ver el mapping generado en nuestra base de datos.
```
rake db:migrate
```
**15.** Y listo, ya podemos empezar a trabajar con el ORM de rails.
