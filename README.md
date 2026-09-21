# Actividad 6: análisis sintáctico de expresiones

Proyecto de la **Actividad 6** de Traductores de Lenguaje. Implementa un analizador sintáctico con **JFlex** y **JavaCUP** para reconocer métodos con sentencias `leer`, `escribir` y asignaciones con expresiones aritméticas y lógicas.

## Requisitos

- JDK 8 o posterior.
- Visual Studio Code con **Extension Pack for Java** (opcional).
- Las bibliotecas incluidas en `lib/`:
  - `jflex-full-1.9.1.jar`
  - `java-cup-11b.jar`
  - `java-cup-11b-runtime.jar`

## Estructura

```text
act5_analisis_sintactico/
├── GeneradorAct5.java
├── PruebaAct5.java
├── Lexer5.jflex
└── parser5.cup
lib/
pruebas/
├── prueba_valida.txt
├── prueba_errores.txt
└── prueba_mixta.txt
.vscode/
```

> El nombre histórico del paquete y de las clases se conserva únicamente para mantener compatibilidad con los archivos generados. La gramática y las pruebas corresponden exclusivamente a la Actividad 6.

## Ejecutar en VS Code

1. Clona el repositorio.
2. Abre **la carpeta raíz** del repositorio, no archivos individuales.
3. Ejecuta `Generar lexer y parser de Actividad 6`.
4. Ejecuta uno de los perfiles de prueba:
   - `Probar Actividad 6 - válido`
   - `Probar Actividad 6 - errores`
   - `Probar Actividad 6 - mixto`

## Ejecutar desde terminal

### Windows PowerShell

```powershell
New-Item -ItemType Directory -Force bin | Out-Null
javac -cp "lib/*" -d bin act5_analisis_sintactico/GeneradorAct5.java
java -cp "bin;lib/*" act5_analisis_sintactico.GeneradorAct5
javac -cp "lib/*" -d bin act5_analisis_sintactico/*.java
java -cp "bin;lib/*" act5_analisis_sintactico.PruebaAct5 pruebas/prueba_valida.txt
```

### Linux/macOS

```bash
mkdir -p bin
javac -cp 'lib/*' -d bin act5_analisis_sintactico/GeneradorAct5.java
java -cp 'bin:lib/*' act5_analisis_sintactico.GeneradorAct5
javac -cp 'lib/*' -d bin act5_analisis_sintactico/*.java
java -cp 'bin:lib/*' act5_analisis_sintactico.PruebaAct5 pruebas/prueba_valida.txt
```

Para probar otro archivo, cambia la ruta final por `pruebas/prueba_errores.txt` o `pruebas/prueba_mixta.txt`.

## Funcionalidad de la Actividad 6

- Lecturas: `leer(a);`, `leer(a,b,c);`
- Escrituras de valores, cadenas y expresiones.
- Asignaciones aritméticas con `+`, `-`, `*`, `/` y `%`.
- Expresiones lógicas con `&&`, `||` y `!`.
- Paréntesis y precedencia de operadores.
- Reporte de línea, columna y token ante errores sintácticos.
- Recuperación de errores hasta el siguiente punto y coma cuando es posible.

Los archivos de `pruebas/` contienen los casos válido, inválido y combinado solicitados por la actividad.
