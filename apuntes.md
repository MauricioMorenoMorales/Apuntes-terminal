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
