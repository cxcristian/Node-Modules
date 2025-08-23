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




