3 ||
ls-> Listar archivos
ls -> -a Listar archivos ocultos
pwd -<print working directory> Identificar el directorio
cd -<change directory> Cambiar de directorio
mkdir ->Crear un directorio
cp [archivo que se va a copiar] [directorio hacia el que se va a mover] -> Copiar un archivo
rm -> Borrar un archivo
mv [ruta del archivo] [directorio hacia el que se va a mover] -> Mover un archivo
rmdir -> eliminar un directorio. En este caso es importante resaltar que, para que el directorio pueda ser eliminado, no puede contener archivos u otros directorios en su interior
ls -t -> ORdena los archivos por fecha de modificacion
ls -x -> Ordena elementos primero por nombre y después por extensión:
ls -X -> Ordena los elementos primero por extensión y luego por nombre:
ls -l -> Muestra toda la información: usuario, grupo, permisos, tamaño, fecha y hora de creación.
ls -lh -> Muestra la misma información que ls -l pero con las unidades de tamaño en KB, MB:
ls -R -> Muestra el contenido de todos los subdirectorios de forma recursiva:
ls -S -> Ordena los resultados por tamaño de archivo:

4||

Utilidades Batch
cat: Nos muestra el contenido completo de un archivo
ejemplo: cat tables.txt

head: Nos muestra las primeras lineas (También podemos escoger cuantas lineas queremos utilizando el modificador [-n #]).
Ejemplos:

head tables.txt
head -n 5 tables.txt

tail: Muestras las ultimas lineas del final (Inverso a head, tambien le funciona modificadores)
Ejemplos:

tailtables.txt
tail -n 5 tables.txt

Utilidades Batch Avanzadas:
grep: Permite trabajar con expresiones regulares, funciona como un buscador dentro del archivo.
Ejemplos:

grep hanks dump1.sql = [comando][expresión regular][archivo]

Para buscar sin importar si esta en mayuscula o miniscula:
grep -i hanks dump1.sql

\_Tambien podemos buscar una expresión de una frase que termine con la misma palabra que estemos buscando:
grep -i “hanks’),$” .

sed: Screem Editor, tratamiento de flujos de caracteres. Este comando nos permite reemplazar una expresión por otra.
ejemplos:

sed ‘s/hanks/selleck/g’ dump1.sql = [comando][subcomando- sustitución][expresión original][nueva expresión][modificador-(/g de global, indica que tiene que hacerse a lo largo de todo el flujo)][indicar cual es el flujo a utilizar (archivo de texto)]
SED no modifica el archivo, lo que hace es crear un nuevo flujo con la modificación

Para eliminar la ultima linea podemos utilizar: 2. sed ‘$d’ nuevasPelis.csv = [Comando][’$sub-comando’][archivo]

awk: Trataminento de texto delimitado, este comando sirve para trabajar con archivos de textos delimitados por comas.
Ejemplos:

awk -F ‘;’ ‘{ print $1 }’ nuevasPelis.csv
awk -F ‘;’ ‘NR > 1 && $3 > 0 { print $1 $3 \* $4 }’ nuevasPelis.csv

||4 COmunicacion entre procesos: QUé son y cómo se utilizan los flujos estandar
nombre_comando < nombreArchivo.txt -> REdirecciona la entrada de un comando (nombre_comando)con el contenido de el archivo (nombreArchivo)
nombre_comando > nombreArchivo.txt -> REdirecciona la salida de un comando reescribiendo el contenido de el archivo
nombre_comando >> nombreArchivo.txt -> Redirecciona la salida de un comando (nombre_comando)agregando al final de el conenido de el archivo(nombreArchivo)

comando | more -> Muestra el resultado largo de un comando en secciones _con enter muestra el resultado con una linea mas por cada uno _ con barra espaciadora muestra otra pantalla o seccion Ejemplo ls -al | more

comando | wc Muestra en el resultado de un comando cuantos caracteres palabras o lineas hay en el resultado
comando | wc -l Muestra en el resultado de un comando cuantas lineas hay en el resultado

$[nombre_comando] & Ejecuta un comando en segundo plano, otra opcion ctrl + z
fg - Trae a primer plano un comando que se esté ejecutando en segundo plano
ps - muestra los procesos que se están ejecutando
ps -ax - muestra los procesos que se estan ejecutnado en el sistema
top - Muestra de forma interactiva los procesos van cambiando en tiempo real con la letra que sale de la interfaz
kill [-9] [numero_proceso] Termina un proceso con la identificacion de el numero de proceso
kill [-9] [numero_proceso] Termina un proceso con prioridad con la identificacion de el numero de el proceso

||11 Permisos sobre archivos
chmod o-w nombre_archivo.txt - MOdifica los permisos de un archivo o directorio para los usuarios (o para los usuarios) (w quitar el permiso de escritura)
chmod o+w nombre_archivo.txt - MOdifica los permisos de un archivo o directorio para los usuarios (+x Execute agrega el permiso de ejecutar todos los usuarios)
chmod760 nombre_archivo.txt - Modifica los permisos de un archivo en base a cada uno de los sectores (ver apuntes notion)
sudo chown nombre_usuario nombre_archivo - cambia el propietario de un archivo por otro usuario de el sistema
sudo chgrp nombre_usuario nombre_archivo - cambia el grupo de un archivo por otro usuario de el sistema

||Find
find [ruta] [expresión de busqueda] [accion]
ruta: Si no se indica una ruta se toma en cuenta entonces el directorio donde se este actualmente, es decir el directorio de trabajo actual, que es lo mismo que indicar con un punto “.”.
Es posible asignar mas de una ruta de búsqueda también como por ejemplo
find /etc /usr /var -group admin
Búsquedas básicas 👍
Algunas banderas que podemos utilizar para buscar:
-name = Busca nombre de un archivo
iname = Igual que name pero este no toma en consideración si tiene alguna mayúscula
-user = El usuario propietario
-group = El grupo propietario
-type = tipo de archivo, f para directorio

Busquedas a través de el tiempo
-mmin = Tiempo en minutos
-mtime = Periodos de 24 horas

-exec Permite ejecutar acciones sobre el resultado de cada línea o archivo devuelto por find, ejemplo:
find . type -f mtime +7 -exec cp {} ./backup/ \;

||Herramientas para interactuar a través de http
curl [url] Sirve para hacer pedidos crudos a un servidor http desde su url nos devuelve el html de el servidor
curl -v [url] Sirve para hacer pedidos crudos a un servidor http desde su url nos devuelve el html y toda la comunicación http de el servidor
curl -v [url] Sirve para hacer pedidos crudos a un servidor http desde su url nos devuelve toda la informacion de encabezados HTTP
wget [url] sirve para realizar descargas desde servidores http archivos binarios
