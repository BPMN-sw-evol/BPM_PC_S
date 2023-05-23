# INFORMACIÓN DEL PROGRAMA
Nombre: BPM_PC_QUERY<br>
Descripción: obtiene datos sobre plataformas de BPMN consumiendo una API de StacoOverflow.<br>
Desarrollado por: DANNO_NZ<br>
https://stackapps.com/apps/oauth/view/26090

# Para ejecutar el programa se necesita:

1. Realizar el registro en https://stackapps.com/users/login
2. Registrar la aplicación para obtener las credenciales que permiten usar la API de StackOverflow https://stackapps.com/apps/oauth/register
3. Obtener un cliente ID y una clave secreta de autenticación OAuth en Stack Overflow (si ya la tiene omita los pasos 1,2,3)
4. Instalar el manejador de versiones GIT
5. Clonar el repositorio con: git clone https://github.com/danilonunezgil/BPM_PC_S.git
6. Instalar Python en cualquier versión 
7. Instalar los siguientes módulos:

   pip install requests (para hacer solicitudes HTTP)<br>
   pip install psycopg2-binary (para conectarse y realizar operaciones con PostgreSQL)
   
8. Instalar PostgreSQL https://www.postgresql.org/download/windows/ (versión estable o última versión)
9. Con la ayuda de pgAdmin 4, crear una base de datos llamada BPM_PC_QUERY
10. En esa misma BD, mediante el uso del script llamado BPM_PC_Query.sql crear la siguiente tabla:
   
   CREATE TABLE BPM_PC_QUERY (<br>
      id_discussion SERIAL PRIMARY KEY,<br>
      topic VARCHAR(25),<br>
      title VARCHAR(255),<br>
      link VARCHAR(255),<br>
      score INTEGER,<br>
      answer_count INTEGER,<br>
      view_count INTEGER,<br>
      creation_date DATE,<br>
      tags VARCHAR(255)<br>
   );<br>
   
11. Ejecuta el programa (en este momento se encuentra en desarrollo):

   python BPM_PC_QUERY.py -k "keyAPI" -i "NombreBusqueda" -d "NombreBD" -u "postgres" -p "claveDB" 
    

# Limitaciones del uso de la API:
https://api.stackexchange.com/docs/throttle<br>
Máximo 30 peticiones por segundo<br>
Máximo 10.000 peticiones por día<br>
En caso de superar la máximas por día, saldrá un error HTTP 429.<br>
Se renueva cada media noche dado el caso se haya superado el límite diario.
