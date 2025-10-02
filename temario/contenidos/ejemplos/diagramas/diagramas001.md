# Diagramas

Los diagramas de estados, actividad y secuencia son isomórficos.

## Un ejemplo

```java
searchAndProcess(int[] t, int k){
    int i=0;
    while(i<t.length && t[i]!=k){
        i++;
    }
    if(t[i]==k){
        A();
    }else{
        B();
    }
}
```

![](/imagenes/modelosUML/diagramaActividad.svg)|![](/imagenes/modelosUML/diagramaEstados.svg)|![](/imagenes/modelosUML/diagramaSecuencia.svg)
|-|-|-|
|Diagrama de actividad|Diagrama de estados|Diagrama de secuencia|

## Otro ejemplo

Juego del 3 en raya

<img src="https://github.com/USantaTecla-0-domains/game-ticTacToe/raw/master/docs/diagrams/out/instructionsActivity/instructionsActivity.svg">|<img src="https://github.com/USantaTecla-0-domains/game-ticTacToe/raw/master/docs/diagrams/out/instructionsState/instructionsState.svg">
|-|-|
|Diagrama de actividad|Diagrama de estados

## Otro ejemplo

Validación de una solicitud

![](/images/temario/contenidos/ejemplos/diagramas/validacionSolicitud-DA.svg)|![](/images/temario/contenidos/ejemplos/diagramas/validacionSolicitud-DE.svg)|![](/images/temario/contenidos/ejemplos/diagramas/validacionSolicitud-DS.svg)|![](/images/temario/contenidos/ejemplos/diagramas/validacionSolicitud-DC.svg)
|:-:|:-:|:-:|:-:|
|Diagrama de actividad|Diagrama de estados|Diagrama de secuencia|Diagrama de colaboración

