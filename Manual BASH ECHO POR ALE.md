# BASH SCRIPT

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



Ahora que ya sabemos que son las variables , vamos a operar con ellas 

 

```
#!/bin/bash
# Script para aprender
# Autor
# Fecha

variable=2
otraVariable=6
resultado=$((variable + otraVariable))
```



## Imprimir en pantalla

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



## Parametros

###### Descripcion de los parametros

`script.sh parametro1 parametro2 parametro3`

- `$0` representa el nombre del script

- `$1` – `$9` los primeros nueve argumentos que se pasan a un script en Bash

- `$n` representa el decimo argumento

- `${n}`  Para argumentos superiores a 10 (donde `n` es el numero del argumento)

  

###### Otros parametros 



| Comando | Resultado del comando                                        |
| ------- | ------------------------------------------------------------ |
| $#      | Numeros de parametros pasados al script (sin contar el nombre del script). |
| $?      | Un valor numerico que te identifica si lo ultimo que se ejecuto fue bien o fue mal (si es !=0 indica error, si es == 0 indica que fue correcto).  `IMPORTANTE!!!` |
| $*      | Cadena de parametros entera (con el nombre del script).      |
| $@      | Array de parametros(sin el nombre del script)                |



ACA PONGO EJEMPLOS!!!





## Prompt

[^prompt]: Linea vertical que titila esperando que el usuario tecle algo.

Permite guardar lo que introduce el usuario por teclado como variable.

Se activa al pulsar el enter.

Veamos un ejemplo

```bash
echo "Introduce un nombre"
read nombre
echo "TU nombre es $nombre"
```

Se le dice al usuario que "introdusca un nombre" gracias al comando echo y seguido aparece el prompt en la pantalla esperando que el usuario tecle algo para que al presionar enter , se almacene dentro de la variable `$nombre`  lo que el usuario escribio.

Luego se muestra por pantalla gracias al echo "tu nombre es `$nombre`" donde `$nombre` es lo que escribio el usuario.

##### Algunos argumentos del read

Son los argumentos que se le agregan al comando para aumentar su funcionalidad, se puede escribir varios uno al lado del otro.

-p

Usado para que el prompt aparesca a continuacion del echo y no abajo

```bash
read -p "Introduce tu apellido: " apellido    
echo "Tu apellido es $apellido"
```

-s

Usado para ocultar lo que el usuario escribe

```bash
read -s "Introduce tu contraseña" contrasenia   #Sirve para introducir contraseñas
echo "Tu contraseña es $contrasenia"
```



## Operaciones



###### Numeros enteros

​    `num=$((num1 + num2))`    # utiliza esto

​    `num=$(($num1 - $num2))`  # esto también funciona    

​    `let num=$1+$2`         # parecido a js -- SIN ESPACIOS SI NO DA ERORR

​    `num=$(expr $1 + $2)`     # forma vieja

- \+ - : suma, resta

```bash
  ~$ $num=10
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





## If

La sintaxis básica de un condicional es la siguiente

```bash
	if [[ CONDICIÓN ]];
	then
	  COMANDO 1 si se cumple la condición
	fi
```

También se puede especificar qué hacer si la condición no se cumple:

```bash
	if [[ CONDICIÓN ]];
	then
	  COMANDO 1 si se cumple la condición
	else
	  COMANDO 2 si no se cumple la condición
	fi
```

O tambien concatenando IFs

```bash
if [[ $VAR1 operador $VAR2 ]]; then
	#hace algo
elif [[ $VAR1 operador $VAR2 ]]; then
	#hace otra si no se cumple el primer if
else
  	#hace otra cosa si no se cumple ninguna de las condiciones anteriores
fi
```

[^$VAR]: Representa una variable

En pseudocodigo : 

> ```bash
> si [[ condicion ]]; entonces 
> 	#hace algo el programa
> si no anduvo lo de arriba [[ condicion ]]; entonces 
> 	#hace algo el programa
> si no entro en ninguno de los if de arriba
> 	#hace algo el programa
> fin
> ```



#### Condicionales con números

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

#### Condicionales con cadenas de texto

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

#### Condicionales con archivos

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

###### Ejemplo

Estamos en la red de nuestra empresa, y deseamos saber si X ordenador está conectado a la red. Para ello hacemos un [script](https://blog.desdelinux.net/bash-como-hacer-un-script-ejecutable/) que hará [ping](http://mx.answers.yahoo.com/question/index?qid=20100417180043AAZG1aR) hacia ese ordenador, y si está en red (o sea, si devuelve el [ping](http://mx.answers.yahoo.com/question/index?qid=20100417180043AAZG1aR)) nos dirá que SÍ, está en red, de lo contrario (o sea, que no esté en red) nos dirá que NO está en red.

```bash
ping -c 1 DIRECCION-IP
if [ $? -ne 0 ]; then
echo "No está en red"
else
echo "Sí está en red"
fi
```

**ping** es el comando que usaremos, y nos dirá si esa PC está en red. Para decirle qué PC queremos comprobar si está o no en red, debemos cambiar **DIRECCION-IP** por obviamente, la dirección IP de la PC que deseamos comprobar.

Como ven, puse «**-c 1**«, lo cual nos es necesario. Cuando hacemos ping a un ordenador, esta acción no se detiene (el ping) hasta que nosotros mismos presionemos **[Ctrl]+[C]**, por lo que poniendo «**-c 1**» le indicamos que haga solo una verificación (solo un intento de ping) y ningún otro, esto hará que se detenga al instante, o sea… comprobará si el ordenador está en red solo una vez.



#### AND Y OR

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

```
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





#### Elementos de la sentencia case-esac

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
antonio
tu nombre empieza con a
```

# Ejercicios 

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





## FOR

### Bucles (*for*)

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