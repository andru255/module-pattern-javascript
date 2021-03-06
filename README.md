PATRON MODULAR
===================
En el mundo de javascript tu puedes escribir código de manera libre y sin restricciones, el único problema es abusar de la libertad que te da a la hora de programar. Al final uno obtiene variables y funciones repartidas a lo largo de todo el código y sin un orden, lo que termina siendo inmantenible. Una de las mejores practicas a la hora de escribir código es usar los patrones de diseño en javascript y el más utilizado es el patron modular.

En javascript el patron modular emula el concepto de clases, de manera que somos capaces de incluir métodos públicos/privados y propiedades dentro de un único objeto, protegiendo las datos particulares del ámbito global, lo que ayuda a evitar la colisión de nombres de funciones y variables ya definidas a lo largo de nuestro proyecto, o API’s de terceros, a continuación unos conceptos previos para poder entender mejor el patrón modular.
### Objeto literal
EL patron modular se basa en parte en los objetos literales por ende es importante entenderlo.
Un objeto literal es descrito como cero o más pares nombre/valor, separados por comas entre llaves.
Nombres dentro del objeto pueden ser cadenas o identificadores que son seguidas por 2 puntos, dichos objetos también pueden contener otros objetos y funciones.
```
var objectLiteral = {
    /* los objetos literales pueden contener propiedades y métodos */    
    saludo : "soy un objeto literal",
    myFunction : function(){
      // código
    }
};
/* accediendo a una propiedad de nuestro objeto literal persona */
objectLiteral.saludo
```
Un ejemplo de un modulo usando un objeto literal.
```
var persona = {
    /* definiendo propiedades */
    nombre : "adan",
    edad   : 33,
    /* método simple */
    comer  : function(){
        console.log(this.nombre + " esta comiendo.");
    }
};
/* accediendo al método comer de nuestro objeto literal persona */
persona.comer();
```
#### Módulo
Un módulo es una unidad independiente funcional que forma parte de la estructura de una aplicación.
Podemos usar funciones y closures para crear módulos.
```
var modulo = (function(){
    //- - -
});
```
Un ejemplo más completo:
```
var automovil = (function(colorDeAuto){
    var color = colorDeAuto;
    return{
        avanzar : function(){
            console.log("el auto "+ color +" esta avanzando");
        },

        retroceder : function(){
            console.log("el auto "+ color +" esta retrocediendo");
        }
    }
})("azul");
/* accediendo los metodos retroceder y avanzar de nuestro módulo */
automovil.retroceder();
automovil.avanzar();
```
#### Función anónima
Las funciónes anónimas son funciónes sin nombre, comúnmente asociados a una variable.
```
var myAnonymousFunction = function(){
    alert("Hello World!");
};
myAnonymousFunction();
```
#### Funciones auto-ejecutables (IIFE)
Estas funciónes una vez declaradas se llaman a sí mismas para inicializarse, los primeros paréntesis encierran el contenido, los segundos paréntesis asumen que el interior de los primeros paréntesis es una función y la ejecuta inmediatamente.
```
/* 01 */
(function(){
    alert("Hello World!");
})();

/* 02 */
var myAnonymousFunction = (function(){
    alert("Hello World!");
})();

/* 03 */
var myAnonymousFunction = (function(message){
    alert(message);
})("hello world");
// todo lo que le precede a los 2 últimos paracentesis se ejecuta inmediatamente
```
#### Clousure
Los clousures son funciones definidas dentro de otras funciones, así mismo dicha función interna tiene acceso al ámbito de la función contenedora.
```
function exampleClousure(arg1, arg2){
    var localVar = 8;
    function multiplicador(innerArg){
        return arg1 * arg2 * innerArg * localVar;
    }
    /* retornar una referencia de la función interna definida como:
       multiplicador 
    */
    return multiplicador;
}

/* la función devuelve una función, por lo tanto necesita asignación */
var globalVar = exampleClousure(2, 4);
/* y luego llamar a */
globalVar(8);
```
#### Métodos privados
Los métodos privados son funciones que no pueden ser llamados desde fuera del ámbito donde se encuentran, dichos métodos podrán ser invocados en nuestros métodos públicos.
```
var modulo = (function () {
    var privateMethod = function (message1) {
        console.log(message1);
    };
    var publicMethod = function (mensaje2) {
        privateMethod(mensaje2);
    };
    return {
        publicMethod: publicMethod
    };
})();

/* pasando datos a un método privado */
modulo.publicMethod("mi mensaje");
```
#### Entendiendo el retorno
Comúnmente los módulos retornan un objeto, la cual los métodos ligados a dicho objeto serán accesibles desde fuera del módulo.
```
var module = (function(){
    /* simple método privado */
    var privateMethod = function(){
        console.log("soy un método privado");
    };
  
    /* retornando un objeto literal */
    return{
        publicMethod : function(){
            privateMethod();
            console.log("soy un método publico");
        }
    }
})();
/* accediendo nuestro método publico */
module.publicMethod();
```
#### Ventajas del patron modular
- Código limpio , separado y organizado.
- Soportan datos privados.
- Código Escalable.

#### Referencias
http://addyosmani.com/resources/essentialjsdesignpatterns/book/#modulepatternjavascriptt
https://www.safaribooksonline.com/library/view/javascript-the-good/9780596517748/
http://toddmotto.com/mastering-the-module-pattern/
