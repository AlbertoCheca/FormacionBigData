# Introduccion a Big data

## Requisitos previos 

Para hacer los ejerecicios descritos he utilizado una maquina virtual cloudera-quickstart-5.13.0 mediante Oracle VM Virtualbox 6.1.Esta _Maquina posee ya preinstalados todos los programas utilizados.

Dentro de ella he creado una carpeta compartida con mi sistema para compartir facilmente archivos desde mi sistema operativo nativo.

Los archivos de dataset estan en la carpeta de la tecnología correspondiente, estos dentro de la maquina los pondré en

/home/cloudera/ejercicios/



## Hadoop

---
### Descubriendo HDFS

---

Para esta practica he usado los archivos del fichero **shakespeare.tar.gz** y el fichero **shakepoems.txt**

Descomprimimos el archivo en 

/home/cloudera/ejercicios/shakespeare

Hacemos uso de hadoop fs para ponerlo, a traves de esta orden podemos acceder a los comandos de HDFS(Hadoop File System ), en este caso usamos el -put para tenerlo como shakespeare

> hadoop fs -put shakespeare /home/cloudera/ejercicios/shakespeare

 * Comprobamos que los archivos estan 

 >  hadoop fs -ls shakespeare

Probamos borrar por ejemplo la carpeta glossary

> hadoop fs -rm shakespeare/glossary

Si volvemos a hacer ls deberia de no aparecer

* Mostrar las ultimas 50 lineas de la carpeta histories

> hadoop fs -cat shakespeare/histories | tail -n 50

* Añadir a la el archivo poems a partir del archivo **shakepoems.txt**

> hadoop fs -get shakespeare/poems /home/cloudera/ejercicios/shakespeare/shakespoems.txt
---
### Ejecutando MapReduceWorcount
---
Para estos ejercicios usaremos los archivos de **worcount** 

* Realizar wordcount de los archivos de Shakespeare

> hadoop jar /home/cloudera/ejercicios/wordcount/wc.jar solution.WordCount shakespeare /home/cloudera/ejercicios

Si lo intentamos ejecutar otra vez vemos que ya estaba ejecutado
* Mostrar los resultados del wordcount

Miramos dentro de ejercicios
> hadoop fs -ls /home/cloudera/ejercicios


    [cloudera@quickstart ~]$ hadoop fs -ls /home/cloudera/ejercicios
    Found 2 items
    -rw-r--r--   1 cloudera supergroup          0 2021-11-24 03:50 /home/cloudera/ejercicios/_SUCCESS
    -rw-r--r--   1 cloudera supergroup     247308 2021-11-24 03:50 /home/cloudera/ejercicios/part-r-00000
      
los datos estan almacenados en part-r-00000, los mostramos 
deberiamos ver una lista de pares palabra,numero de ocurrencias

>  hadoop fs -cat /home/cloudera/ejercicios/part-r-00000 | less

deberiamos ver una lista de pares palabra,numero de ocurrencias

    zeals	1
    zed	1
    zenith	1
    zephyrs	1
    zir	2
    zo	1
    zodiac	1
    zodiacs	1
    zone	1
    zounds	3
    zwaggered	1


---------------

## Spark

-----
#### Sparkbits


Ejecutamos la spark shell y trabajaremos dentro de ella

>spark-shell

Creamos la RDD a partir del texto **relato.txt""

> val  relato = sc.textFile("file:/home/cloudera/BIT/data/relato.txt")

contamos cuantos caracteres hay

>relato.count()

mostramos los datos del fichero colecteando todo sin restringir

>relato.collect()

Mostramos en contenido pero con las lineas haciendo print a cada linea por separado

>relato.foreach(println)

### ejercicio 2
Cargamos un log (al crear el val creamos el objeto, en este caso es un string que es la direccion del fichero)

>val log= "file:/home/cloudera/BIT/data/weblogs/2013-09-15.log"

Colocamos el valor del fichero

> val logs = sc.textFile(log)

Sleccionamos las lineas que contienen .jpg

>val jpglogs = logs.filter(x=>x.contains(".jpg"))

Mostramos las 5 primeras lineas

>jpglogs.take 5

Podemos anidar los metodos, aqui almaccenamos el numero de lineas de jpglogs

>val jpglogs2 = jpglogs.count()


(IGNORAR )
Markdown documentation

2nd paragraph. *Italic*, **bold**, and `monospace`. Itemized lists
look like:

  * this one
  * that one
  * the other one

Note that --- not considering the asterisk --- the actual text
content starts at 4-columns in.

> Block quotes are
> written like so.
>
> They can span multiple paragraphs,
> if you like.

Use 3 dashes for an em-dash. Use 2 dashes for ranges (ex., "it's all
in chapters 12--14"). Three dots ... will be converted to an ellipsis.
Unicode is supported. ☺



