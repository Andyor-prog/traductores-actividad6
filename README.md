# Actividad 6: Analisis sintactico de expresiones

Proyecto de analisis sintactico de expresiones aritmeticas y logicas usando JFlex y JavaCUP. Conserva el soporte previo para paquetes, importaciones, clases, atributos y constantes.

## Requisitos

- Java JDK 8 o posterior.
- Bibliotecas ubicadas en `lib/`:
  - `jflex-full-1.9.1.jar`
  - `java-cup-11b.jar`
  - `java-cup-11b-runtime.jar`

## Ejecucion desde VS Code

1. Abra esta carpeta como workspace.
2. En **Run and Debug**, ejecute **Generar lexer y parser**.
3. Ejecute **Probar archivo valido**, **Probar archivo con errores** o **Probar archivo mixto**.

Los perfiles de ejecucion incluyen las bibliotecas de `lib/` y usan `bin/` como salida compilada.

## Ejecucion desde PowerShell

```powershell
javac -cp "lib/*" -d bin GeneradorAct5.java
java -cp "bin;lib/*" act5_analisis_sintactico.GeneradorAct5
javac -cp "lib/*" -d bin Lexer5.java Parser5.java PruebaAct5.java sym.java
java -cp "bin;lib/*" act5_analisis_sintactico.PruebaAct5 prueba_valida.txt
```

## Archivos principales

- `Lexer5.jflex`: reglas del analizador lexico.
- `parser5.cup`: gramatica del analizador sintactico.
- `GeneradorAct5.java`: genera el lexer y el parser.
- `PruebaAct5.java`: lee un archivo y ejecuta el analisis.
- `prueba_valida.txt`: lecturas, escrituras y asignaciones validas.
- `prueba_errores.txt`: errores de listas, escritura y expresiones.
- `prueba_mixta.txt`: errores recuperables y sentencias posteriores validas.

## Estructuras reconocidas

- Atributos o variables individuales y multiples, con o sin inicializacion.
- Constantes `final` con inicializacion obligatoria.
- Tipos `int`, `float`, `double`, `char`, `boolean`, `String` y tipos identificados.
- Valores numericos, decimales, cadenas, caracteres y booleanos.
- Paquetes, importaciones y clases.
- Metodos `void` con sentencias `leer`, `escribir` y asignaciones.
- Expresiones con `+`, `-`, `*`, `/`, `%`, `&&`, `||` y `!`, respetando precedencia.

El analizador informa reglas reconocidas y errores con linea, columna y token encontrado. Para errores de sentencias, intenta recuperar el analisis hasta el siguiente punto y coma.

## Tabla de resultados

| Prueba | Tipo | Resultado esperado | Resultado obtenido | Estado |
|---|---|---|---|---|
| Lectura multiple | Valida | Reconocer `leer(a,b);` | Regla reconocida: lectura | Correcta |
| Escritura con expresion | Valida | Reconocer `escribir(a+b);` | Regla reconocida: escritura | Correcta |
| Asignacion aritmetica | Valida | Reconocer `total = a + b;` | Regla reconocida: asignacion | Correcta |
| Asignacion logica | Valida | Reconocer `estado = !activo;` | Regla reconocida: asignacion | Correcta |
| Falta de coma | Invalida | Reportar error con ubicacion | Error con linea y columna | Correcta |
| Elemento faltante | Invalida | Reportar error recuperable | Se continua con la siguiente sentencia | Correcta |
| Identificador faltante | Invalida | Reportar causa | Identificador esperado en la asignacion | Correcta |

Las pruebas se ejecutan con `prueba_valida.txt`, `prueba_errores.txt` y `prueba_mixta.txt`. La prueba mixta demuestra la recuperacion y el reconocimiento de declaraciones posteriores.
