# Ejercicios Express

Nota: para estos ejercicios no se recomienda la documentación oficial de Express (para la mayoría de los ejercicios), ya que es demasiado genérica. En su lugar: https://developer.mozilla.org/en-US/docs/Learn/Server-side/Express_Nodejs/Introduction#introducing_express

Video explicativo de los ejercicios - [Link](https://oscarm.tinytake.com/tt/NTI4NDA1OV8xNjU0MDczNA)

## Inicializa el directorio con NPM e instala Express

```
npm init -y
```

```
npm install express
```

Comprueba que en el fichero __package.json__ se ha instalado la dependencia __express__

## Server 1

1. Crea un nuevo servidor. Cuando el usuario navuegue a "http://localhost:3000", debe devolver el siguiente texto '<h1>El servidor funciona correctamente</h1><p>Aquí iría el contenido del mensaje</p>'. 

**No** debes utilizar el método __write__ de NodeJS. En su lugar, usa una única vez el método __send__ de Express en el objeto __res__ para enviar una respuesta al cliente.

2. Recuerda añadir el __status__ a la respuesta de valor 200; para indicar que la comunicación ha ido bien

Pregunta: ¿has necesiado indicar el tipo de codificación de los carácteres en la respuesta? ¿Y el tipo de datos devuelto?

3. Instala nodemon:

```
npm install --save-dev nodemon
```

Crea un script en el package.json para ejecutar server1:

```
scripts: {
    server1: "nodemon server1.js"
}
```

Comprueba que puedes ejecutar el script con:

```
npm run server1
```

Comprueba también que, al realizar un cambio en server1.js, el servidor es recargado automáticamente.

## Server 2

Crea un nuevo script en package.json para desarrollar el server2.js. A partir de ahora, lo haremos así para todos los servidores. 

De esta manera, deberías ser capaz de ejecutar

```
npm run server2.js
```

Y que __nodemon__ se encargue de recargar el servidor si el fichero server2.js sufre modificaciones.

Crea un nuevo servidor, de nombre **server2** y que haga exactamente lo mismo que **server1**; pero esta vez, solo mostrarà la respuesta HTML si y solo sí el usuario accede a 'http://localhost:3000/mensaje'. Si el usuario accede a cualquier otra URL, el servidor devuelve un mensaje que dice : "No he encontrado lo que buscabas...". Además, recuerda devolver un status 404 en este caso.

Debes usar una vez el método **app.get** y otra **app.use** para conseguir esta funcionalidad. ¿Que diferencia puedes apreciar entre los dos métodos, en cuanto a la gestión de las peticiones del cliente?

Extra: ¿Qué mensaje genera Express si no encuentra un endpoint que coincida con la petición del cliente? Dicho de otro modo, explora como funciona tu script si solo pusieras la sentencia app.get('/mensaje', etc...)

<details>
<summary><b>Pista</b></summary>

[Error 404 con Express](https://techeplanet.com/how-to-handle-404-error-in-express/#:~:text=To%20handle%20a%20404%20error,%2F%2FExpress%20GET%20call%20app.)

</details>



## Server 3

Crea una nueva entrada en la sección de scripts de package.json que te permita ejecutar: 


```
npm run server3
```

Modifica tu servidor para que ahora, en función de la URL que acceda el usuario. devuelva un **fichero HTML** u otro:

1. Si el usuario introduce la URL 'http://localhost:3000/nacktschnecke', debemos devolver el fichero HTML ubicado en server3-files/nacktschnecke.html

2. Si el usuario introduce la URL 'http://localhost:3000/about', debemos devolver el fichero HTML ubicado en server3-files/about.html

3. En cualquier otro caso, debemos devolver este texto **404. Resource not found**. Además, utiliza el código HTTP adecuado para contestar al navegador Web. Comprueba que tu código de error aparece de manera explcíta en la respuesta, explorando la pestaña "Network" de tus herramientas de desarrollador del navegador.

<details>
<summary><b>Pista</b></summary>

[Uso de sendFile](https://www.digitalocean.com/community/tutorials/use-expressjs-to-deliver-html-files)

</details>

## Server 4
Crea una nueva entrada en la sección de scripts de package.json que te permita ejecutar: 

```
npm run server4
```

Crea un nuevo servidor. Este servidor implemeta un solo endpoint, que va a comprobar si la última parte de la URL es un palíndromo o no.

Fíjate que la última parte de la URL cambia, pero el endpoint __check__ es el mismo. Recuerad que a esto la llamamos **ruta dinámica**.

1. Si el usuario accede a http://localhost:3000/check/eye, el servidor devolverà "Es un palíndromo".

2. Si el usuario accede a http://localhost:3000/check/vaca, el servidor devolverà "NO es un palíndromo"

Si el usuario no accede al endpont 'check' el servidor debe devolver un error 404, similar al ejercicio anterior.

Fíjate que no tienes que implementar la funcionalidad para saber si una palabra es un palíndromo o no. Tienes un __custom module__ preparado para utilizarlo en utils/palindrome. Tan solo debes importarlo.

BONUS: ¿Serías capaz de devolver el mensaje adecuado sin tener que usar dos veces el método 'send' en tu servidor?

## Server 5
Crea una nueva entrada en la sección de scripts de package.json que te permita ejecutar: 

```
npm run server5
```

1. Si el usuario accede a http://localhost:3000/check/?palabra=eye, el servidor devolverà "Es un palíndromo".

2. Si el usuario accede a http://localhost:3000/check/?palabra=vaca, el servidor devolverà "NO es un palíndromo"

Si el usuario no accede al endpoint 'check' el servidor debe devolver un error 404, similar al ejercicio anterior.

En este caso debes acceder a la __query string__ de la URL para obtener la palabra a comprobar.

BONUS: No utilices el __custom module__ de la carpeta Util. En su lugar, busca un [paquete de terceros](https://www.npmjs.com/) adecuado para llevar a cabo esta funcionalidad. 



## Server 6
Crea una nueva entrada en la sección de scripts de package.json que te permita ejecutar: 

```
npm run server6
```

Este servidor tiene ya implementado un endpoint, concretamente, al directorio raiz. Cuando el cliente hace un GET a '/formulario' obtenemos un formulario simple.

1. Fíjate que la página HTML que devuelve el servidor pide [cargar unos estilos](https://oscarm.tinytake.com/tt/NTI4MzAxNl8xNjUzNzgyMw), que no es capaz de encontrar. Dichos estilos estan ubicados en la carpeta __server-6-static-files__ de nuestro servidor. Modifica el server6.js de tal manera que un cliente pueda hacer peticiones a dicha carpeta para obtener recursos; de tal manera que cuando accedamos a http://localhost:3000/formulario, se carguen los estilos de dicho HTML correctamente.

[Pista](https://developer.mozilla.org/es/docs/Learn/Server-side/Express_Nodejs/Introduction#sirviendo_archivos_est%C3%A1ticos)

2. Implemente un endpoint que caputre un POST al endpoint '/formulario'; y que simplemente se encargue de retornar los datos enviados por el formulario en formato JSON.

Debes obtener una respuesta similar a [esta](https://oscarm.tinytake.com/tt/NTI4MzA2OV8xNjUzODA1Ng)

[Pista](https://www.geeksforgeeks.org/express-js-express-json-function/)

## BONUS FINAL

1. Borra la carpeta node_modules
2. Envia todo el proyecto a tun compañero/a
3. El compañero/a debe ejecutar "npm install"; sin parámetros.

Si está bien creado el package.json; tu compañero/a debe ser capaz de ejecutar cualquier servidor en su máquina mediante "npm run nombre-del-servidor".

## Soluciones 

Solución de Adrián Rey [Enlace](https://github.com/arlomba/express-exercise-students)
