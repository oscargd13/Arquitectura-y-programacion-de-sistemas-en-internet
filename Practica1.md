# Practica 1

* Realizamos una interfaz para crear 3 objetos

```
interface IPersona{
    name : string
    edad : number
    amigos : object[]
    
}

const persona1 : IPersona = {
    name: "Oscar",
    edad: 19,
    amigos : [
        {
            name: "Juan",
            edad : 23,
        },
        {
            name : "Carlos",
            edad : 21,
        },
    ]
    
}

const persona2 :IPersona = {   
    name: "Oscar",
    edad: 19,
    amigos : [
        { 
            name: "Juan",
            edad : 23,
        },
        {
            name : "Carlos",
            edad : 21,
        },
    ]
}
const persona3 :IPersona = {   
    name: "Pepe",
    edad: 39,
    amigos : [
        { 
            name: "Alfonso",
            edad : 41,
        },
        {
            name : "Roberto",
            edad : 36,
        },
    ]
}

```

* Funcion deepEquals
```
const deepEquals = (a : object, b: object) : boolean=>{
    const obja = Object.keys(a).sort()
    const objb = Object.keys(b).sort()

    if(a === b){   // comprobamos que esten el mismo espacio de memoria
        return true;

    }else if(typeof a === "object" && typeof b === "object" && Object.keys(a).length === Object.keys(b).length){   //comprobamos que sean de tipo object y que tengan la misma longitud de keys 
        
        if (obja.join("") !== objb.join("")) {  //juntamos los elementos del array y comprobamos que apunten al mismo sitio
            return false;
        }

        for(let i = 0; i<Object.values(obja).length; i++){    
            if(!deepEquals(Object.values(a)[i], Object.values(b)[i]){  //comprobamos de forma recursiva que a tenga los mismos valores que b
                return false;
            }
      }
      return true;

      }else{
         return false
    }   
 }

console.log(deepEquals(persona1, persona2))
console.log(deepEquals(persona1, persona3))
```

* Funcion deepPrint
```
const deepPrint = (obj: object) => {
   for(let i = 0; i<Object.keys(obj).length; i++){ //Realizamos un for para recorrer el objeto y imprimir sus keys y sus valores
       if(Array.isArray(Object.values(obj)[i])){
        deepPrint(Object.values(obj)[i]);
       }else{
           console.log(Object.keys(obj)[i], Object.values(obj)[i])
           }
       }
   }

deepPrint(persona1)

```

* Funcion deepClone
```
const deepClone = (n : object) : object=>{
    if(typeof n === "object"){
    let objn : any = Array.isArray(n) ? [] : {} //creamos un array vacio
    for(let i = 0; i< Object.keys(n).length; i++){ //recorremos las keys 
         objn[Object.keys(n)[i]]=deepClone(Object.values(n)[i]) //igualas los atributos de n a los del objn que en nuestra copia 
    }
    return objn;
    }else{
        return n;
    }
 }


console.log(deepClone(persona1))

```
