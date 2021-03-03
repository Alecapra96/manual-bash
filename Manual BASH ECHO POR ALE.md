# Introduccion a BASH SCRIPT

Al trabajar con la pc mas de una vez has tenido que hacer tareas repetitivas , que es algo realmente tedioso , pero ademas te puedes equivocar,  si bien , mientras mas repites una tarea mas destreza adquiris, las posibilidades de equivocarte aumentan , por lo que automatizar una tarea repetitiva anula la posibilidad de error y ademas vuelve menos tedioso el trabajo.



Bash es un intérprete de comandos (o *shell*). Se trata de una *interfaz de usuario* con la que relacionarte con el sistema operativo con el que estás trabajando. Así, **esta aplicación es capaz de leer y ejecutar instrucciones**. Básicamente es el encargado de decirle al sistema operativo lo que tu quieres hacer. Posteriormente, se encargará de devolverte la respuesta del sistema operativo, en el caso de que la haya.



Uno de las principales razones para iniciarte en el mundo del scripting es sin lugar a dudas la **automatización**. Pero, ¿para que automatizar? Simplemente para reducir el número de errores. Un proceso que hayas automatizado, que hayas mecanizado, es un proceso que tiene menos probabilidades de que falle. Que no te digo que no falle, pero, has quitado un factor intermedio, el factor humano.



Un script es un archivo (o un conjunto) que contiene instrucciones (en nuestro caso comandos de bash) y que nesesita un programa para ejecutarse (en nuestro caso la terminal)

## Primer script

Ya que has practicado con la terminal puedes crear tu primer script.

Como sabemos un script es un archivo de texto plano con intrucciones , por lo que debemos crearlo primero.Lo creamos con el comando touch y como sabemos en linux ,las extenciones no tienen un significado util,pero por convension se a los scripts se los llama con la extencion `.sh` (de SHell) para identificarlos mas rapido

```bash
touch script.sh
```

con nuestro editor lo abrimos , en mi caso con nano

```bash
sudo nano script.sh
```

Al abrirlo escribimos lo siguiente

```bash
#!/bin/bash
# Nuestro primer script
# Autor
# Fecha

echo "hola mundo"
```

La primera linea `#!/bin/bash` es caracteristica de todos los scripts de linux y representa el inicio del script.

Tras #! indica la ruta a la aplicacion que interpreta los comandos , en nuestro caso BASH que se encuentra en /bin/bash

No importa que pongamos lineas en blanco en nuestro script, es mas , estas son usadas , para ordenar  y dar legibilidad.

Las siguientes lineas que empiezan con `#` son Comentarios



Bash ignora todo lo escrito en la línea después de la marca de almohadilla ( #). La única excepción a esta regla es cuando la primera línea del guión comienza con los #!/bin/bash ,esta secuencia de caracteres se llama Shebang y se utiliza para indicarle al sistema operativo qué intérprete utilizar para analizar el resto del archivo.

Los comentarios se pueden agregar al principio de la línea o en línea con otro código:

```bash
# Esto es un comentario

echo "Hola mundo" # Esto es un comentario
```



> El espacio en blanco después de la marca de almohadilla no es obligatorio, pero mejorará la legibilidad del comentario.



La ultima linea , es un comando , en este caso `echo`  que saca por stdout(por defecto la pantalla) lo que le demos como argumento , en este caso " hola mundo "

Guardamos el script con `control + x` y le damos al `enter` 

Ahora es tiempo de ejecutarlo

Para ejectuarlo utilizamos el comando bash seguido por el archivo

`bash /ruta-del-archivo/archivo`

En este caso

```bash
bash script.sh
hola mundo 
```

Lo ejecutamos y vemos como nos imprime en pantalla la instruccion que tenia adentro.

La forma mas comun de ejecutar un script es dandole permisos de ejecucion  y lo ejecutamos con `./`nombre-script

```bash
chmod +x script.sh
./script.sh
hola mundo
```

Al darle permisos de ejecucion podemos ejecutar nuestro script como si fuera un programa, esto es posible gracias a la primera linea del script #!/bin/bash que hace que se llame a la aplicacion para leer los comandos. 

A nivel de shell nuestro script es un programa como cualquier otro que podemos ejecutar o hasta ponerlo en un directorio listado en $PATH para ejecutarlo como un programa , simplemente tecleando su nombre.



Como empieza el script

comentario

echo

Darle permiso de execucion

variables

read

valor de retorno #?

argumentos

evaluar condiciones , comando test

if

case

for 

while

function







## Variables

[^CUIDADO]: Bash no conoce la letra ñ

Una variable no es mas que un *lugar seguro* donde guardas una información o valor. De esta forma, cuando necesites esa información, sabes donde está y puedes recuperarla a voluntad. Como ya te puedes imaginar, para trabajar con una variable, necesitas guardar (escribir) y recuperar (leer).

Las variables pueden tomar prácticamente cualquier nombre, sin embargo, existen algunas restricciones:

- Sólo puede contener caracteres alfanuméricos y guiones bajos

- El primer carácter debe ser una letra del alfabeto o “_” (este último caso se suele reservar para casos especiales).

- No pueden contener espacios.

- Las mayúsculas y las minúsculas importan, “a” es distinto de “A”.

- Algunos nombres som usado como variables de entorno y no los debemos utilizar para evitar sobrescribirlas (e.g.,PATH).

- Una buena practica es llamar a las variable con la formula camelCase.

  [^camelCase]: es un estilo de escritura que se aplica a frases o palabras compuestas. El nombre se debe a que las mayúsculas a lo largo de una palabra en CamelCase se asemejan a las jorobas de un camello.

  

Para declarar una variable en Shell escribe el nombreDeLaVariable que desees, seguido de un signo igual y el valor **SIN espacios:**

```bash
variable=valor
```

Es importante que no haya espacios ni entre la variable y el signo igual, ni entre el signo igual y el valor que quieres asignar a tu variable.

Mientras que para leer de esa variable antepodrás un `$`.

```bash
$variable
```

Para almacenar en una variable un comando , podemos utilizar la sustitución de comandos. 

Encapsular el comando dentro de la estructura `$(comando)` :

```bash
~$ mycurrentdir=$(pwd)
~$ echo $mycurrentdir
/Users/Desktop
```

## Comando echo

Veamos un poco mas en profundidad el comando echo.

Su sintaxis de uso es:

```bash
echo [option(s)] [string(s)]
```

 Ingresamos una línea de texto y mostramos la salida estándar:

```bash
echo "probando el echo"
```

Las comillas dobles  (`""`) tiene reservados caracteres especiales.

```bash
echo "probando que $variable1 lo toma como caracter especial"
```

Para tipear un caracter especial dentro de las comillas dobles (`""`)  y no lo tome como una variable o un comando, si no como un texto plano comun dentro de las comillas tenemos *que* usar una barra invertida  `\` antes del caracter especial.



Veamos un ejemplo , en el primer echo `$variable1`efectivamente es tomada como variable, en el segundo echo no es tomada como variable por que la barra invertida (`\`) lo impide.

```bash
echo "probando que $variable1 no lo tome como caracter especial"
echo "probando que \$variable1 no lo tome como caracter especial"
```

Otra forma de hacerlo es con las comillas simples (`' '`) que no toman en cuenta los caracteres reservados.

```bash
echo 'probando que $variable no la tome como caracter especial'
```

## Operaciones

Ahora que ya sabemos que son las variables , vamos a operar con ellas 

 

```bash
#!/bin/bash
# Script para aprender
# Autor
# Fecha

variable=2
otraVariable=6
resultado=$((variable + otraVariable))
echo "el resultado de la suma entre $variable y $otraVariable es $resultado"
```

Aqui estamos almacenando en la variable `resultado` , el resultado de la suma entre `variale` y `otraVariable`

Hay muchas formas de hacer operaciones con numeros enteros, algunas son:

​    `num=$((num1 + num2))`    # utiliza esto

​    `num=$(($num1 - $num2))`  # esto también funciona    

​    `let num=$1+$2`         # parecido a js -- SIN ESPACIOS SI NO DA ERORR

​    `num=$(expr $1 + $2)`     # forma vieja

Donde recomiendo utilizar la primera opcion , que es la estandar.

Veamos las diferentes Operaciones que podemos hacer con bash y como hacerlas

- \+ - : suma, resta

```bash
  ~$ num=10
  ~$ echo $((num + 2))
```

- ** : potencia

```bash
  ~$ echo $((num ** 2))
```

- \* / % : multiplicación, división, resto (módulo)

```bash
  ~$ echo $((num * 2))
  ~$ echo $((num / 2))
  ~$ echo $((num % 2))
```

- VAR++ VAR– : post-incrementa, post-decrementa

```bash
  ~$ echo $((num++))
  ~$ echo $num
```

- ++VAR –VAR : pre-incrementa, pre-decrementa

```bash
  ~$ echo $((++num))
  ~$ echo $num
```



## Parametros

Los comandos que ejecutamos pueden recibir opciones o parametros como por ejemplo el comando `ls -l /home` donde **ls** es el comando , **-l** la opcion y **/home** el parametro

`script.sh parametro1 parametro2 parametro3`

- `$0` representa el nombre del script

- `$1` – `$9` los primeros nueve parametros que se pasan a un script en Bash

- `$n` representa el decimo argumento

- `${n}`  Para argumentos superiores a 10 (donde `n` es el numero del argumento)

  

Ahora veamos como funciona

Crea un archivo y dale permisos de ejecucion, dentro escribe

```bash
#!/bin/bash
echo "\$0 contiene $0"
echo "\$1 contiene $1"
echo "\$2 contiene $3
```

Lo que hace este script es que al pasarle parametros , nos mostrara con un echo los 3 primeros.

Si un parametro esta vacio , se mostrara como vacio( ver $3)

```bash
./script.sh hola como 
echo "\$0 contiene $0"
# $0 contiene hola
echo "\$1 contiene $1"
# $1 contiene como
echo "\$2 contiene $3"
# $2 contiene 
echo "el nombre del script es $0"
# el nombre del script es script.sh
```

Tambien tenemos variables especiales

| Comando | Resultado del comando                                        |
| ------- | ------------------------------------------------------------ |
| $#      | Numeros de parametros pasados al script (sin contar el nombre del script). |
| $?      | Un valor numerico que te identifica si lo ultimo que se ejecuto fue bien o fue mal (si es !=0 indica error, si es == 0 indica que fue correcto).  `IMPORTANTE!!!` |
| $*      | Cadena de parametros entera (sin el nombre del script).      |
| $@      | Array de parametros(sin el nombre del script)                |

Veamos $#, , esta variable indica el numero de parametros que se le paso al script sin incluir al propio nombre del script ($0)

```bash
./script.sh hola como estas
echo "el numero de parametros es $#"
# el numero de parametros es 3
```

$* y $@ devuelven los parametros con este orden

```bash
.script.sh hola como estas
echo $*
# hola como estas
echo $@
# hola como estas
```

La diferencia es que $* nos muestra el resultado como string y $@ nos los muestra como un array , que lo veremos mas adelante.

Nuestro script se tiene que comportar de una forma u otra segun los parametros que pase el usuario , o segun el valor de una variable, ahora veremos esto.

El comando que permite evaluar condiciones es `test` , el valor de retorno de test si es VERDADERA(TRUE) es 0 y si es FALSA(FALSE) es 1, lo que evaluamos recibe el nombre de expresion. Ahora veremos un ejemplo.

```bash
test 20 -eq 20
echo $?
 #0
```

Aqui estamos evaluando que 20 sea igual que 20 ,que es la expresion , gracias a la condicional `-eq` , que veremos mas adelante , donde $? devolvera 0 lo que significa que es TRUE

Por ende si probamos test 20 -eq 21 , $? dara 1 , ya que es FALSE por que 20 no es igual a 21.

Obviamente, podemos usar las expresiones con variables.

```bash
a=20
b=20
test $a -eq $b
echo $?
 #0
```

Aunque la forma mas comun de evaluar las expresiones no es con el comando test si no poniendo la expresion entre corchetes []

```bash
[ $a -eq $b ] # IMPORTANTE, TENER EN CUENTA LOS ESPACISO
echo $?
 #0
```



## Prompt

[^prompt]: Linea vertical que titila esperando que el usuario tecle algo.

Muchas veces , nesesitamos que el usario nos pase datos , que almacenaremos como variables para interactuar con el script. Esto lo hacemos con read

Read permite guardar lo que introduce el usuario por teclado como variable.

Se activa al pulsar el enter.

Veamos un ejemplo

```bash
echo "Introduce un nombre"
read nombre
echo "TU nombre es $nombre"
```

Se le dice al usuario que "introdusca un nombre" gracias al comando echo y seguido aparece el prompt en la pantalla esperando que el usuario tecle algo para que al presionar enter , se almacene dentro de la variable `$nombre`  lo que el usuario escribio.

Luego se muestra por pantalla gracias al echo "tu nombre es `$nombre`" donde `$nombre` es lo que escribio el usuario.





**Algunos argumentos del read**

Son los argumentos que se le agregan al comando para aumentar su funcionalidad, se puede escribir varios uno al lado del otro.

**-p**

Usado para que el prompt aparesca a continuacion del echo y no abajo

```bash
read -p "Introduce tu apellido: " apellido    
echo "Tu apellido es $apellido"
```

**-s**

Usado para ocultar lo que el usuario escribe

```bash
read -s "Introduce tu contraseña" contrasenia   #Sirve para introducir contraseñas
echo "Tu contraseña es $contrasenia"
```



## If

La sintaxis básica de un condicional es la siguiente

```bash
If [Expresion]; Then

#Realiza expresión si es verdadera

fi  #Cierra la estructura
```

Donde estamos diciendo :

```bash
Si(if) [lo que esta dentro de esta expresion] entonces(then) 

 hace esto
 
fi #Cierro el if
```



```bash
If [Expresion]; Then

  #Realiza expresión si es verdadera

Else

  #Realiza expresión si es falsa

fi


```



**Cuando hay más de dos opciones utilizamos ELIF**

```bash
If [Expresion]; Then

  #Realiza expresión si es verdadera

elif  [Expresion]; Then

  #Realiza expresión si es verdadera

elif  [Expresion]; Then

  #Realiza expresión si es verdadera

else

  #Realiza expresión si es falsa

fi 
```

### Condicionales

Al comparar números podemos realizar las siguientes operaciones:

| operador | significado            |
| :------: | ---------------------- |
|   -lt    | menor que (<)          |
|   -gt    | mayor que (>)          |
|   -le    | menor o igual que (<=) |
|   -ge    | mayor o igual que (>=) |
|   -eq    | igual (==)             |
|   -ne    | no igual (!=)          |

```bash
	#!/bin/bash
	num1=$1  # la variable toma el primer valor que le pasamos al script
	num2=$2  # la variable toma el segundo valor que le pasamos al script
	if [[ $num1 -gt $num2 ]];
	then
	  echo $num1 es mayor que $num2
	else
	  echo $num2 es mayor que $num1
	fi
```

Comparando cadenas de texto:

| operador | significado                                                 |
| :------: | ----------------------------------------------------------- |
|    =     | igual, las dos cadenas de texto son exactamente idénticas   |
|    !=    | no igual, las cadenas de texto no son exactamente idénticas |
|    <     | es menor que (en orden alfabético ASCII)                    |
|    >     | es mayor que (en orden alfabético ASCII)                    |
|    -n    | la cadena no está vacía                                     |
|    -z    | la cadena está vacía                                        |

```bash
	#!/bin/bash
	string1='reo'
	string2='teo'
	if [[ $string1 > $string2 ]];
	then
	  echo Eso es verdad
	else
	  echo Eso es mentira
	fi
```

Condicionales con archivos

| operador | Devuelve *true* si                                           |
| -------- | ------------------------------------------------------------ |
| -e name  | *name* existe                                                |
| -f name  | *name* es un archivo normal (no es un directorio)            |
| -s name  | *name* NO tiene tamaño cero                                  |
| -d name  | *name* es un directorio                                      |
| -r name  | *name* tiene permiso de lectura para el user que corre el script |
| -w name  | *name* tiene permiso de escritura para el user que corre el script |
| -x name  | *name* tiene permiso de ejecución para el user que corre el script |



Por ejemplo, podemos hacer un script que nos informe sobre el contenido de un directorio:

```bash
	#!/bin/bash
	for file in $(ls);
	do
	  if [[ -d $file ]];
	  then
	    echo directorio: $file
	  else
	    if [[ -x $file ]];
	    then
	      echo archivo ejecutable: $file
	    else
	      echo archivo no ejecutable: $file
	    fi
	  fi
	done
```

Estamos en la red de nuestra empresa, y deseamos saber si X ordenador está conectado a la red. Para ello hacemos un  script que hara ping hacia ese ordenador, y si está en red (devuelve ping )nos dirá que SÍ, está en red, de lo contrario (o sea, que no esté en red) nos dirá que NO está en red.

```bash
ping -c 1 DIRECCION-IP
if [ $? -ne 0 ]; then
echo "No está en red"
else
echo "Sí está en red"
fi
```

**ping** es el comando que usaremos, y nos dirá si esa PC está en red. Para decirle qué PC queremos comprobar si está o no en red, debemos cambiar **DIRECCION-IP** por obviamente, la dirección IP de la PC que deseamos comprobar.

Como ven, puse `-c 1` lo cual nos es necesario. Cuando hacemos ping a un ordenador, esta acción no se detiene (el ping) hasta que nosotros mismos presionemos **[Ctrl]+[C]**, por lo que poniendo «**-c 1**» le indicamos que haga solo una verificación (solo un intento de ping) y ningún otro, esto hará que se detenga al instante, o sea… comprobará si el ordenador está en red solo una vez.

### && y ||

```bash
if [[ $VAR1 -ge $VAR2 ]] CONDICION [[ $VAR1 -ge $VAR3 ]] then
    #hace algo
fi
```

Estos códigos permiten la ejecución o no, de un comando en función del código de retorno desde otro comando. Podemos combinar varios códigos de terminación de comandos mediante los operadores lógicos and (representada con &&) or (representada con ||) y not (representada con !).

```bash
#!/bin/bash
direc=/tmp/existe
echo " Prueba de operadores Logicos"
echo -e "ingrese usuario  : \\c "
read username
echo -e "ingrese password : \\c "
read password
# Uso de operadores AND y OR
if [[ ( $username == "admin" && $password == "secret" ) || ( $username == "system" && $password == "paso" ) ]]; then
echo "valid user"
else
echo "invalid user"
fi
# Uso de operador NOT
if [[ ! -d $direc ]]; then
   echo "El directorio $direc, NO existe"
fi
```

`ND (&&)`

- El comando comando2 se ejecuta únicamente si el comando comando1 devuelve el código verdadero.
- Si los dos expresiones son verdaderas entonces los dos comandos devuelven verdadero.

`OR (||)`

- El comando2 se ejecuta únicamente si el comando1 devuelve un código falso.
- La expresión global es verdadera si al menos uno de los comandos devuelve verdadero.

`NOT (!)` 

En el ejemplo si el directorio /tmp/existe no existe, entonces se ejecuta el comando echo.



## Case-esac

La sintaxis es la siguiente:

```bash
case “$VARIABLE” in

             opción1)
             comando
             ;;

             opción2)
             comando
             ;;

              opción3)
              comando
              ;;
esac
```

si la variable **expresion** se encuentra en algunos de los casos propuestos ejecuta los comandos correspondientes.



Comenzamos con `case` *variable* `in`

Paréntesis de cierre **)** después de cada caso (condición).

Doble punto y coma **;;** delimita la lista de comandos que serán ejecutados cuando se cumpla el caso (condición).

Cerrar la sentencia case con `esac`.

Lo entederemos mejor con un ejemplo, imaginemos que queremos hacer un pequeño escript que nos pregunte por nuestra edad y le demos una serie de respuestas diferentes al usuario en función del numero introducido:

```bash
echo "Cuantos años tengo"
read edad
case $edad in
  37)
    echo "¡Correcto!"
  ;;
  *)
    echo "¡Nop!"
  ;;
esac
```

Vemos como encapsulamos todos las posibles opciones de respuesta en el segundo caso que contiene un `*`. Asi de forma rápida y sencilla podemos controlar todas las opciones que podrían darse al introducir la edad.

Ejemplos:

```bash
#!/bin/bash
#############################
# Ejemplo de uso de case-esac
#############################
dia=$(date | cut –c 1-3)
case $dia in
	lun)   echo Hoy es lunes ;;
	mar)   echo Hoy es martes ;;
	mié)   echo Hoy es miércoles ;;
	jue)   echo Hoy es jueves ;;
	vie)   echo Hoy es viernes ;;
	sáb)   echo Hoy es sábado ;;
	dom)   echo Hoy es domingo ;;
	*)     echo No se sabe qué es hoy ;;
esac
```



```bash
#!/bin/bash
read -p "Introduzca A, B o C: " letra
case "$letra" in
	a|A)
		echo Introdujo A
		;;
	b|B)
		echo Introdujo B
		;;
	c|C)
		echo Introdujo C
		;;
	*)     
		echo No introdujo A, B o C
		;;
esac
```



Aqui otro ejemplo con más opciones

```bash
echo "Escribe tu nombre sin usar mayusculas"
read nombre
case $nombre in
  a*)
    echo "tu nombre empieza con a"
  ;;
  c*t)
    echo "tu nombre empieza con c y termina con t"
  ;;
  *se)
    echo "tu nombre termina con la cadena se"
  ;;
  *)
    echo "no soy capaz de reconocer tu nombre"
  ;;
esac
```

veamos como funciona en terminal:

```bash
-$  bash case_esac.sh
Escribe tu nombre sin usar mayusculas
alejandro
tu nombre empieza con a
```



## Bucles (for)

La sintaxis general de los bucles es la siguiente:

```bash
for VARIABLE in LISTA_VALORES;
do
	COMANDO 1
	COMANDO 2
	...
	COMANDO N
done
```

Donde la lista de valores puede ser un rango númerico:

```bash
	for VARIABLE in 1 2 3 4 5 6 7 8 9 10;
	for VARIABLE in {1..10};
```

una serie de valores:

```bash
	for VARIABLE in file1 file2 file3;
```

o el resutlado de la ejecución de un comando:

```bash
	for VARIABLE in $(ls /bin | grep -E 'c.[aeiou]');
```

Hay que tener en cuenta que si pasamos un listado de valores pero lo ponemos entrecomillado, el ordenador lo enterá como un única línea:

```bash
	for VARIABLE in "file1 file2 file3";
```

Un ejemplo simple de *for* sería:

```bash
	#!/bin/bash
	for numero in {1..20..2};
	do
	  echo Este es el número: $numero
	done
```

## Ejercicios



`Primera parte` 

​	1.- Realiza un guión llamado nuevo que solicite un número y, si es mayor que 200, muestre el mensaje: <<mayor que 	200>>.

​	2.- Realiza un guión llamado cuestion que muestre en pantalla la pregunta: <<¿Quién descubrió América?>> y, según 	la respuesta, muestre el mensaje <<es correcto>> o <<no es correcto>>.

​	3.- Crea un guión llamado pares que solicite un número y diga si es par o impar.

​	4.- Crea un guión llamado loteria en el que el usuario debe de adivinar un número que el programador debe de        		escribir previamente. Si acierta el número oculto, el programa debe de mostrar un mensaje de felicitación, en caso 		de    fallar debe de seguir intentándolo hasta que no introduzca ningún caracter, entonces finalizará la tarea.

`Segunda parte`

1. Haz un script que cree 40 archivos *.txt* en una carpeta de tu escritorio (usa *touch* para crearlos)

2. Haz un script que comprima con *gzip* sólo los archivos 25 y 29.

3. Escribe un script que cambie la extensión de los ficheros que contengan un 3 en su nombre de *.txt* a *.md*.

4. Crea un script que copie todos los archivos (no directorios) */etc* a una carpeta de tu escritorio.

5. Prepara un script que cuenta el número de directorios y archivos que hay en */etc*

6. Haz un script que devuelva el número de archivos que has guardado

    

# DUEÑOS

# PERMISOS

Como hemos visto anteriormente ,todos los archivos de linux tienen dueño , tambien un grupo dueño y ademas estos tienen permisos para leer,(`r`ead) escribir(`w`rite) o ejecutar(e`x`ecute) estos archivos .

Al utilizar el comando `ls -l` para listar los archivos de un directorio , ¿viste esa combinacion de de `r,w,x` y `-` ?, bueno esos son los permisos.

En linux todo archivo tiene tres niveles de permisos , los que se aplican al dueño del archivo , al grupo dueño del archivo y a los demas usuarios.

Por ejemplo un archivo , o directorio  el dueño puede tener permiso para leer , escribir y ejecturalo (rwx) , el dueño grupo para leerlo(r--) y el resto de los usuarios ningun permiso (---)

Una buena asignacion de permisos con una buena politica lleva a obtener un sistema multiusuario seguro.

Linux, al ser un sistema diseñado fundamentalmente para trabajo en red, la seguridad de la información que almacenemos en nuestros equipos (y no se diga en los servidores) es fundamental, ya que muchos usuarios tendrán o podrán tener acceso a parte de los recursos de software (tanto aplicaciones como información) y hardware que están gestionados en estos ordenadores.

Podemos ver los permisos cuando listamos un directorio con `ls -l`:

```scala
$> ls -l
-rwxrwxr--  1 cisco ventas    9090 sep  9 14:10 presentacion
-rw-rw-r--  1 cisco cisco    26023 jun  7 16:36 reporte1
drwxr-xr-x  2 cisco cisco     4096 ago 27 11:41 documentos
```

 Veamos los permisos de el archivo `presentacion`que es la primera linea.

La primera columna (-rwxrwxr--) es el tipo de archivo y sus permisos, 

La segunda columna (1) es el número de enlaces al archivo.

La tercera columna (cisco) es el propietario del archivo.

La cuarta columna (ventas) es el grupo al que pertence al archivo.

Las siguientes son el tamaño, la fecha y hora de última modificación y por último el nombre delarchivo o directorio.

![image-20210302215133429](/home/cisco/.config/Typora/typora-user-images/image-20210302215133429.png)

Veamos en profundidad la primera columna:

Cada archivo de linux esta identificado por 10 caracteres que se le denomina mascara.

De estos 10 caracteres , el primero representa el tipo de archivo, los siguientes 9 , de izquierda a derecha y en bloques de 3 representan los permisos del dueño, grupo dueño y los otros en ese orden.

El primer carácter de los archivos puede ser el siguiente:

| **Permiso** | **Identifica**                                               |
| ----------- | ------------------------------------------------------------ |
| –           | Archivo                                                      |
| d           | Directorio                                                   |
| b           | Archivo de bloques especiales (Archivos especiales de dispositivo) |
| c           | Archivo de caracteres especiales (Dispositivo tty, impresora…) |
| l           | Archivo de vinculo o enlace (soft/symbolic link)             |
| p           | Archivo especial de cauce (pipe o tubería)                   |

Donde lo mas normal es el `-` para representar a un archivo comun o `d` para representar a un directorio

Los siguientes caracteres son los permisos , recuerda, se tratan en bloques de 3 de derecha a izquierda , donde el primer bloque representa al dueño , el siguiente al grupo dueño y el ultimo a los otros usuarios del sistema.

| **Permiso** | **Identifica**       |
| ----------- | -------------------- |
| –           | Sin permiso          |
| r           | Permiso de lectura   |
| w           | Permiso de escritura |
| x           | Permiso de ejecución |

Volvamos a nuestro **ls -l**

```scala
$> ls -l
-rwxrwxr--  1 cisco ventas    9090 sep  9 14:10 presentacion
-rw-rw-r--  1 cisco cisco    26023 jun  7 16:36 reporte1
drwxr-xr-x  2 cisco cisco     4096 ago 27 11:41 documentos
```

El primer archivo listado podemos ver claramente que es un archivo gracias a que el primer caracter es un `-` (`-`rwxrwxr--)en cambio documentos , nos damos cuenta que es un directorio por que comienza con una `d`(`d`rwxr-xr-x ).

Desglocemos el archivo presentacion.

```scala
-rwxrwxr--  1 cisco ventas    9090 sep  9 14:10 presentacion
```

Ya sabemos que es un archivo por el `-` en el primer caracter, los siguientes 3 caracteres representan los permisos del dueño -`rwx`rwxr-- donde vemos que el dueño tiene los permisos rwx que significa ,read(lectura),write(escritura) y execute(ejecucion) (es importante que nos familiarizemos con los nombres en ingles.)

El siguiente bloque de 3 -rwx`rwx`r-- representa los permisos del grupo dueño , que tambien son rwx.

Y el ultimo bloque -rwxrwx`r--` representa los permisos para el resto de usuarios donde vemos que tiene r--, lo que significa que puede read(leer), pero donde deberia estar w y x tiene un - lo que significa que no los tiene.

En resumen al archivo presentacion el dueño y el grupo dueño pueden leer , escribir y executar y los demas usuarios solo pueden leerlo.

Ahora un parate , tenemos que tener en cuenta que los permisos `rwx` de un archivo no son los mismos que los de un directorio.Veamos los permisos de los archivos.

**Permisos de los archivos** 

| Permiso           | Descripcion                                                  |
| ----------------- | ------------------------------------------------------------ |
| r < Lectura:      | permite, fundamentalmente, visualizar el contenido del archivo. |
| w**<** Escritura: | permite modificar el contenido del archivo.                  |
| x**<** Ejecución: | permite ejecutar el archivo como si de un programa ejecutable se tratase. |

En el caso de los directorios , dificilmente se entienda los permisos r y x separados.

Read y Execute (r y x) Son nesesarios para que un usuario pueda "examinar" ese directorio , ver lo que tiene y navegar por el . El permiso Write(w) significa que el usuario puede colocar nuevos archivos o directorios dentro y tambien borrarlos.

Veamoslos:

**Permisos para directorios**

| Permiso          | Descripcion                                                  |
| ---------------- | ------------------------------------------------------------ |
| r **<** Lectura: | Permite saber qué archivos y directorios contiene el directorio que tiene este permiso. |
| w**<**Escritura: | Permite crear archivos en el directorio, bien sean archivos ordinarios o nuevos directorios. Se pueden borrar directorios, copiar archivos en el directorio, mover, cambiar el nombre, etc. |
| x**<**Ejecución: | Permite situarse sobre el directorio para poder examinar su contenido(ls), copiar archivos de o hacia él. Si además se dispone de los permisos de escritura y lectura, se podrán realizar todas las operaciones posibles sobre archivos y directorios. |



Lo mas comun es que los directorios deben ser "examinados" por todos los usuarios por lo que se les da permisos r-x en el tercer grupo. Pero con estos permisos no se puede colocar nada dentro , pero si podran hacerlo en un nivel inferior que si tengan permisos.

Pongamos un ejemplo:

Un usuario tiene acceso rwx a un directorio llamado /inferior que esta contenido en otro directorio llamado /superior, el problema es que si este usuario no tiene permisos r-x en el directorio /superior nunca podra acceder al directorio /inferior , para poder acceder minimamente al directorio /superior y luego entrar al directorio /inferior que este contiene debe pooser permisos r-x .Esto es logico , como va a poder escribir un usuario en un directorio si no puede llegar a el?.

## chmod

Para cambiar los permisos de  un fichero se utiliza el comando `chmod` 

La opcion -R  es opcional y cumple la misma funcion que en chowm.

`Hay dos formas de cambiar los permisos , la octal y la ....`

A mi gusto prefiero la ... que te la enseñare ahora , pero descuida tambien te enseñare la otra forma.

Primero veamos como el comando 

```bash
chmod ABC elemento
```

Donde A es u(usuario), g (grupo) o o(todos), cuando es `o` se puede omitir.

Donde B es +(para agregar) o - (para quitar).

Donde C es r(lectura) , w (escritura) y x (ejecucion)

**Veamoslo con un ejemplo:**

Tengo el archivo 

```bash
-rw-rw-r--  1 cisco cisco    26023 jun  7 16:36 reporte1
```

y quiero agregarle el permiso x y quitarle w al dueño,hacemos:

```bash
chmod u-w+x reporte1
```

Quiero quitarle  los permisos r y w al grupo dueño

```bash
chmod g-rw reporte1
```

Elimino  el permiso de ejecución para grupo y otros.

```bash
chmod go-x reporte1
```

Al usuario se le eliminan lectura y escritura, al grupo se le agrega lectura y otros se le agrega ejecución.

```bash
chmod  u-rw,g+w,o+x reporte1
```

Por ultimo quiero darle todos los permisos a todos ( no recomendado)

```bash
chmod +wrx reporte1
```

Por ultimo la forma octal 



La representación octal de chmod es muy sencilla

*Lectura* tiene el valor de *4*
*Escritura* tiene el valor de *2*
*Ejecución* tiene el valor de *1*

Entonces:

```scala
x-----x-----x-----------------------------------x
| rwx |  7  | Lectura, escritura y ejecución    |
| rw- |  6  | Lectura, escritura                |
| r-x |  5  | Lectura y ejecución               |
| r-- |  4  | Lectura                           |
| -wx |  3  | Escritura y ejecución             |
| -w- |  2  | Escritura                         |
| --x |  1  | Ejecución             			|
| --- |  0  | Sin permisos          			|
x-----x-----x-----------------------------------x
```

```java
x------------------------x-----------x
|chmod u=rwx,g=rwx,o=rx  | chmod 775 | 
|chmod u=rwx,g=rx,o=     | chmod 760 |
|chmod u=rw,g=r,o=r      | chmod 644 |
|chmod u=rw,g=r,o=       | chmod 640 |
|chmod u=rw,go=          | chmod 600 |
|chmod u=rwx,go=         | chmod 700 |
x------------------------x-----------x
```

# COMANDO SU