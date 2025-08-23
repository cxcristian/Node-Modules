# ENTENDIENDO LOS MODULOS DE NODE.JS
## Estudiante: _Cristian David Giraldo Alvarez_
## Profesor: _Carlos Navia_
## Instituto: _SENA_

## Objetivo
A travez de este repositorio de GitHub  se pienza explorar los siguientes Temas:

- Módulo Console de Node.js [[Link](https://educated-show-144.notion.site/M-dulos-en-node-2574671e02a1801888eefc86d18cfb24)]
- Módulo Process de Node.js [[Link](https://educated-show-144.notion.site/M-dulo-Process-de-Node-js-2574671e02a1803f9a8ce86f045db44c)]
- Módulo OS de Node.js  [[Link](https://educated-show-144.notion.site/M-dulo-OS-de-Node-js-2574671e02a1804593f8e89d5fef1405)]
- Módulo Timers en Node.js [[Link](https://educated-show-144.notion.site/M-dulo-Timers-en-Node-js-2574671e02a18067a776e66b448ef876)]
- Módulo fs de Node.js [[Link](https://educated-show-144.notion.site/M-dulo-fs-de-Node-js-2574671e02a180b5b641d4667729ecbe)]  

# Módulos en Node Js

## ¿Que son los modulos en Node?

Los modulos de node son unidades de codigo _reutilizable_, los cuales nos permiten organizar de forma eficiente las aplicaciones  
y evitar contaminacion a nivel de scope global.  
Existen tres tipos de modulos:  

+ Nativo: Son módulos integrados en Node.js que proporcionan funcionalidades  
básicas del sistema operativo y del entorno de ejecución.
+ Local:Son archivos JavaScript que creamos en nuestro proyecto para organizar el código en diferentes funcionalidades.
+ Terceros: Son paquetes desarrollados por la comunidad que se instalan  
a través de npm y proporcionan funcionalidades adicionales.
>Nota: Cada archivo que se cree en un proyecto se le puede considerar un modulo independiente medellin.

## CommonJs
Node js usa **CommonJS** como sistema tradicional de modulos, basado en **require()**-**module.exports**, funcionando de forma _sincrona_  
y cache que mantiene estado compartido

## Es modules

Es modules es el estandar hoy en dia (EcmaScript 2015), su sintaxis es **import**/**export**, se diferencia del CommonJs con su carga _asincrona_ y análisis estatico.  
Para usar Es modules se debe configurar el proyecto adecuadamente.

### Mini conclusion
Ambos sistemas tienen diferencias en sintaxis, carga y variables globales, pero Node.js permite cierta interoperabilidad.  
Se recomienda usar ES Modules en proyectos nuevos, manteniendo CommonJS en proyectos existentes.
>Disclaimer: Esto es un resumen rapdio de lo que se encuentra en la documentacion de Modulo Console de Node.js.

## Funcionamiento del sistema de módulos
Cuando Node.js encuentra una declaración de importación, ejecuta un proceso de resolución para localizar el módulo solicitado.  
Este proceso sigue un orden específico de búsqueda:  
1 Módulos nativos: Node.js primero verifica si el nombre corresponde a un módulo nativo.  
2 Rutas relativas y absolutas: Si el nombre comienza con ./, ../ o /, Node.js busca el archivo en la ruta especificada.  
**Ej:**  
const miModulo = require('./utils/helpers');  
const config = require('../config/database');  

3 Carpeta node_modules: Para nombres que no son rutas, Node.js busca en la carpeta  
node_modules del directorio actual y en las carpetas padre.

## Exportacion e importación basica Common JS - Es Modules:
### Common JS
La exportación de funcionalidades se realiza mediante el objeto **module.exports** o la propiedad **exports**.  
Ambos métodos permiten hacer disponible el código para otros módulos:
>Nota: Explicacion de exportacion de un modulo usando CommonJs.  

**Ej:**  
// archivo: matematicas.js  
function multiplicar(a, b) {  
    return a * b;  
}  

function dividir(a, b) {  
    if (b === 0) {  
        throw new Error('División por cero no permitida');  
    }  
    return a / b;  
}  

// Exportación usando module.exports  
module.exports = {  
    multiplicar,  
    dividir  
};  

Para importar este modulo que se creo solamente se utilizaria una instancia   
**Ej:**
const matematicas = require('./matematicas')  
y ya segun sea la necesidad usamos las funciones que existen en el modulo.  
console.log(matematicas.multiplicar(5, 3)); // 15  
console.log(matematicas.dividir(10, 2)); // 5  
 
### Es modules

**Configuración para usar ES Modules**

Para utilizar **ES Modules** en Node.js, necesitas configurar tu proyecto de una de estas formas:

**Opción 1: Usar extensión .mjs**
// archivo: servidor.mjs  
import { createServer } from 'http';  

const servidor = createServer((req, res) => {  
    res.writeHead(200, { 'Content-Type': 'text/plain' });  
    res.end('Hola desde ES Modules');  
});

servidor.listen(3000);  

**Opcion 2: usar el package.json**
{  
    "name": "mi-proyecto",  
    "version": "1.0.0",  
    "type": "module",  
    "main": "index.js"  
}  

**Exportación**
export default class Servidor {  
  iniciar() {  
    console.log("Servidor iniciado...");  
  }  
}  

**Importacion**
import Servidor from "./servidor.js";

En fin, existen varias formas de utilizar los modulos de con **CommonJs** y **Es Modules**. 
Pero para profundizar mas revizar el material del profesor Carlos Navia, aqui se vio solamente un pequeño repaso.   

# Módulo process de Node js.  

## Objetivo
El objetivo de esta seccion es entender como **interactuar** con el proceso de ejecución, **obtener** datos del entorno, **manejar** argumentos desde la terminal y **controlar** el flujo de la ejecucion de un programa en Node js

## ¿Que es el modulo procces?
El modulo **process** es una herrmienta globlal integrada en Node js que permite interactuar con el procceso de ejecución, se usa para:

- Leer argumentos de la línea de comandos.
- Acceder a variables de entorno.
- Controlar cuándo termina tu aplicación.
- Gestionar la entrada/salida de datos en la terminal.
- Manejar eventos como interrupciones o errores no capturados.

### process.argv
Es un array que contiene todos los argumentos que se pasan al ejecutar un programa Node.js.
Los dos primeros elementos de `argv` son:

1. La ruta al ejecutable de Node.js.
2. La ruta al archivo ejecutado.


### ▶️ **Ejemplo**

Crea un archivo `args-example.js`:

```jsx
console.log('Todos los argumentos:', process.argv);
// Variable constante la cual excluey los primeros dos elementos del arreglo que entrega argv 
//es decir la ruta ejecutable y ruta del archivo ejecutado
const userArgs = process.argv.slice(2);
console.log('Argumentos personalizados:', userArgs);

```

### ▶️ **Ejecutar**

```jsx
node args-example.js hola mundo
```

▶️ Salida
```js
Todos los argumentos: [ '/usr/local/bin/node', '/ruta/args-example.js', 'hola', 'mundo' ]
Argumentos personalizados: [ 'hola', 'mundo' ]  
```

> Nota: Estos codigo son sacados de la pagina de Modulo Process

## **Trabajando con process.env**

### ✅ **Concepto**

`process.env` es un objeto que almacena las variables de entorno del proceso. Se usa para definir configuraciones que cambian según el entorno (desarrollo, producción, pruebas).


### ▶️ **Ejemplo**

Crea `env-example.js`:

```javascript
// Este script muestra cómo acceder a variables de entorno en Node.js usando process.env
// Si la variable no existe, muestra 'No definido'

console.log('NODE_ENV:', process.env.NODE_ENV || 'No definido'); // Entorno de ejecución (desarrollo, producción, etc.)
console.log('USER:', process.env.USER || 'No definido');         // Usuario actual del sistema
```

 Explicación:  
 - process.env.NODE_ENV accede a la variable de entorno NODE_ENV.  
 - process.env.USER accede a la variable de entorno USER.  
 - El operador || 'No definido' muestra un mensaje si la variable no existe.  

### ▶️ **Ejecutar**

```bash
# Ejecuta el script definiendo variables de entorno antes del comando
NODE_ENV=production USER=juan node env-example.js
```

### ▶️ **Salida**

```
NODE_ENV: production
USER: juan
```

##
> Nota: .env constiene todas las varialbes de entorno del sistema donde se este ejecutando la aplicacion.  


## 4️⃣ **Salir de un Proceso con process.exit()**

### ✅ **Concepto**

`process.exit()` detiene el proceso en ejecución inmediatamente. Puedes proporcionar un código de salida (por convención, `0` es éxito y cualquier otro valor indica error).

### ▶️ **Ejemplo**

Crea `exit-example.js`:

```jsx
// la variable error es false
const error = false;
// si error es true tira el console.error y el process exit vale 1
if (error) {
  console.error('¡Ocurrió un error!');
  process.exit(1);
}
//En caso contrario todo bien
console.log('Proceso terminado exitosamente');
//Process exxit vale 1
process.exit(0);

```

### ▶️ **Ejecutar**

```bash
node exit-example.js
```

### ▶️ **Salida**

```
Proceso terminado exitosamente
```

## 5️⃣ **Leyendo Entradas con process.stdin**

### ✅ **Concepto**

`process.stdin` te permite leer la entrada de la terminal. Es útil para capturar datos del usuario.

### ▶️ **Ejemplo**

Crea `stdin-example.js`:

```js
// Este script muestra cómo leer datos ingresados por el usuario desde la terminal usando process.stdin

process.stdout.write('Escribe tu nombre: '); // Muestra un mensaje solicitando el nombre

process.stdin.setEncoding('utf-8'); // Configura la entrada estándar para leer texto en UTF-8

// Escucha el evento 'data', que se activa cuando el usuario escribe y presiona Enter
process.stdin.on('data', (data) => {
  const nombre = data.trim(); // Elimina espacios y saltos de línea
  console.log(`¡Hola, ${nombre}!`); // Saluda al usuario con el nombre ingresado
  process.exit(0); // Termina el proceso
});
```

// Explicación:
// - process.stdout.write() muestra un mensaje en la terminal sin salto de línea.
// - process.stdin.setEncoding('utf-8') permite leer texto correctamente.
// - process.stdin.on('data', callback) ejecuta el callback cada vez que el usuario ingresa datos.
// - process.exit(0) finaliza el programa después de saludar.

### ▶️ **Ejecutar**

```bash
node stdin-example.js
```

### ▶️ **Salida**

```
Escribe tu nombre: Juan
¡Hola, Juan!
```



## 6️⃣ **Manejando Eventos del Proceso**

### ✅ **Concepto**

Puedes manejar eventos como:

- `exit`: Cuando el proceso está a punto de finalizar.
- `SIGINT`: Cuando se presiona `Ctrl + C`.
- `uncaughtException`: Cuando ocurre un error no controlado.

### ▶️ **Ejemplo**

Crea `events-example.js`:

```js
// Ejemplo de manejo de eventos del proceso en Node.js

// Evento 'exit': se ejecuta justo antes de que el proceso termine
process.on('exit', (code) => {
  console.log(`Proceso finalizado con código ${code}`);
});

// Evento 'SIGINT': se ejecuta cuando el usuario presiona Ctrl + C en la terminal
process.on('SIGINT', () => {
  console.log('Capturada la señal SIGINT (Ctrl + C)');
  process.exit(0); // Finaliza el proceso manualmente
});

// Evento 'uncaughtException': se ejecuta cuando ocurre un error no controlado en el código
process.on('uncaughtException', (err) => {
  console.error('Error no capturado:', err);
  process.exit(1); // Finaliza el proceso con código de error
});

// Forzamos un error para demostrar el evento 'uncaughtException'
throw new Error('¡Esto es un error no capturado!');
```

 Explicación:
- process.on('exit', callback): Permite ejecutar código justo antes de que el proceso termine.
- process.on('SIGINT', callback): Permite capturar la señal Ctrl + C y ejecutar código antes de salir.
- process.on('uncaughtException', callback): Permite manejar errores no controlados y evitar que el proceso termine abruptamente sin mensaje.

### ▶️ **Ejecutar**

```bash
node events-example.js
```

### ▶️ **Salida**

```
Error no capturado: Error: ¡Esto es un error no capturado!
Proceso finalizado con código 1
```

Presionando `Ctrl + C`:

```
Capturada la señal SIGINT (Ctrl + C)
Proceso finalizado con código 0
```
## 7️⃣ **Obteniendo Información del Proceso**

### ✅ **Concepto**

Puedes obtener estadísticas útiles:

- `process.pid`: ID del proceso.
- `process.ppid`: ID del proceso padre.
- `process.uptime()`: Tiempo en ejecución en segundos.
- `process.memoryUsage()`: Uso de memoria del proceso.

### ▶️ **Ejemplo**

Crea `info-example.js`:

```jsx
//id del proceso
console.log('PID:', process.pid);
//id del proceso padre
console.log('PPID:', process.ppid);
// tiempo de ejecucion seg
console.log('Uptime:', process.uptime(), 'segundos');
//uso de memoria (demás que importante si se quiere optimizar¿?)
console.log('Memoria usada:', process.memoryUsage());
```

### ▶️ **Ejecutar**

```bash
node info-example.js
```

### ▶️ **Salida**

```
PID: 45678
PPID: 1234
Uptime: 0.003 segundos
Memoria usada: {
  rss: 23470080,
  heapTotal: 4571136,
  heapUsed: 2768264,
  external: 9278,
  arrayBuffers: 9382
}
```

## 8️⃣ **Proyecto Playground: Herramienta CLI Simple**

### 🛠️ **Objetivo**

Construir una herramienta CLI simple que reciba comandos del usuario y responda apropiadamente.

### ▶️ **Código**

Crea `cli-tool.js`:

```jsx
console.log('Bienvenido a la CLI de ejemplo');
console.log('Comandos disponibles: hola, tiempo, salir');

process.stdin.setEncoding('utf-8');
process.stdin.on('data', (data) => {
  const input = data.trim().toLowerCase();

  switch (input) {
    case 'hola':
      console.log('¡Hola! ¿Cómo estás?');
      break;
    case 'tiempo':
      console.log(`Tiempo activo: ${process.uptime().toFixed(2)} segundos`);
      break;
    case 'salir':
      console.log('Saliendo...');
      process.exit(0);
      break;
    default:
      console.log('Comando no reconocido');
  }

  process.stdout.write('Ingresa un nuevo comando: ');
});

```

### ▶️ **Ejecutar**

```bash
node cli-tool.js
```

### ▶️ **Salida Esperada**

```
Bienvenido a la CLI de ejemplo
Comandos disponibles: hola, tiempo, salir
Ingresa un nuevo comando: hola
¡Hola! ¿Cómo estás?
Ingresa un nuevo comando: tiempo
Tiempo activo: 5.12 segundos
Ingresa un nuevo comando: salir
Saliendo...
```

## ✅ **Resumen**

En este tutorial aprendiste a:

- Leer argumentos (`process.argv`) y variables de entorno (`process.env`).
- Finalizar procesos con `process.exit()`.
- Leer entradas del usuario usando `process.stdin`.
- Escuchar eventos clave como `exit` y `SIGINT`.
- Obtener información importante sobre el proceso.

# Módulo OS de Node.js

## 🔖 **Objetivo**

En este tutorial, aprenderás los conceptos básicos del módulo `os` de Node.js, que proporciona funciones útiles para interactuar con el sistema operativo. Al finalizar este tutorial, serás capaz de:

- Obtener información sobre el sistema operativo y la arquitectura.
- Acceder a detalles del CPU y la memoria del sistema.
- Manipular información de la red y usuarios.
- Aplicar el módulo `os` para monitorear el entorno del servidor.


## 🧑‍💻 **Entorno de Desarrollo**

En este tutorial, utilizaremos Node.js en tu entorno local. Se recomienda tener un editor de texto como Visual Studio Code y una terminal para ejecutar los ejemplos.

## 1️⃣ **Introducción al Módulo OS**

El módulo `os` es un módulo integrado de Node.js. Proporciona una serie de métodos y propiedades para obtener información sobre el sistema operativo en el que se está ejecutando la aplicación Node.js.

No es necesario instalar ningún paquete adicional; solo tienes que requerirlo en tu proyecto.

```jsx
const os = require('os');
```

## Resumen del módulo `os` en Node.js

El módulo `os` de Node.js permite obtener información y características del sistema operativo donde se ejecuta la aplicación. Es útil para crear scripts de monitoreo, herramientas de administración y para adaptar el comportamiento de tu programa según el entorno.

### Funcionalidades principales

- **Información del sistema operativo:**
  - `os.platform()`: Plataforma del sistema (win32, linux, darwin, etc).
  - `os.arch()`: Arquitectura de la CPU (x64, arm, etc).
  - `os.type()`: Tipo de sistema operativo.
  - `os.release()`: Versión del sistema operativo.

- **Información de la CPU:**
  - `os.cpus()`: Detalles de cada núcleo de CPU (modelo, velocidad, etc).
  - `os.cpus().length`: Número de núcleos.

- **Memoria:**
  - `os.totalmem()`: Memoria RAM total (en bytes).
  - `os.freemem()`: Memoria RAM libre (en bytes).

- **Red:**
  - `os.networkInterfaces()`: Información de las interfaces de red.
  - `os.hostname()`: Nombre del host.

- **Usuario y directorios:**
  - `os.userInfo()`: Información del usuario actual.
  - `os.homedir()`: Ruta del directorio home del usuario.
  - `os.tmpdir()`: Ruta del directorio temporal.

- **Tiempos y carga:**
  - `os.uptime()`: Tiempo de actividad del sistema (en segundos).
  - `os.loadavg()`: Promedio de carga del sistema (solo Unix).

### Ejemplo básico

```js
const os = require('os');
console.log('Sistema:', os.platform(), os.arch());
console.log('CPU:', os.cpus()[0].model);
console.log('Memoria total:', (os.totalmem() / 1024 / 1024).toFixed(2), 'MB');
console.log('Usuario:', os.userInfo().username);
```
 
> **Nota:** El módulo `os` es solo para información del sistema operativo y hardware, no para manipular archivos o procesos.


