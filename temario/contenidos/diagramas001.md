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

|Actividad|Estados|Secuencia
|-|-|-|
![](/imagenes/modelosUML/diagramaActividad.svg)|![](/imagenes/modelosUML/diagramaEstados.svg)|![](/imagenes/modelosUML/diagramaSecuencia.svg)

## Otro ejemplo

Juego del 3 en raya

|||
|-|-|
<img src="https://github.com/USantaTecla-0-domains/game-ticTacToe/raw/master/docs/diagrams/out/instructionsActivity/instructionsActivity.svg">|<img src="https://github.com/USantaTecla-0-domains/game-ticTacToe/raw/master/docs/diagrams/out/instructionsState/instructionsState.svg">
