# Electrónica Medina - Unidad 3
Alumnos:<br>
Medina González Cristian Roberto - 23170234<br>
Villalba Rodríguez Kevin Eliazar - 23170369<br>
Leon Fernandez Alexis Javier - 23171137<br>
Docente: Ing. José Luis Medina Jiménez 
Horario: 10:00 - 11:00

Sistema de ventas e inventario de Unidad 2 refactorizado con procedimientos, macros y USES. Conserva el registro, búsqueda, recepción, ventas, resumen y persistencia, así como la alerta de cinco unidades o menos.

## Abrir y ejecutar

1. Extraer toda la carpeta del ZIP.
2. Tener Visual Studio 2022 con herramientas de C++ para escritorio, SDK de Windows y MASM; instalar Irvine32 en C:\Irvine. Si está en otra carpeta, ajustar IrvineDir en las propiedades del proyecto.
3. Abrir Proyecto_Electronica.sln y seleccionar Debug / x86 (Win32).
4. Compilar y ejecutar con F5. El código está en Proyecto_Electronica/main.asm.

También se incluye Ejecutar.cmd y el ejecutable probado con símbolos en Debug. Para compilar por consola, abrir x86 Native Tools Command Prompt for VS 2022 y ejecutar Compilar.cmd. Si Irvine está en otra ruta, definir la variable IrvineDir antes de usar el script.

## Qué se comprobó

Pasaron 12 casos del menú real: altas y duplicados, búsqueda, precios inválidos, entradas aceptadas/rechazadas, ventas, alerta, resumen, guardado y recuperación en un segundo proceso. Se verificaron también errores de archivo, resultados en registros, USES y equilibrio de pila. La compilación se comprobó con ML/LINK; la sesión manual del depurador gráfico queda pendiente.

## Contenido de la entrega

- Proyecto_Electronica.sln y Proyecto_Electronica/: solución, proyecto, filtros y fuente comentado.
- Informe_Proyecto.pdf y .md: reporte de Unidad 2 más la sección Versión de la Unidad 3.
- Tabla_Pruebas.md: 135 casos con entrada, esperado y obtenido.
- Guia_Demostracion.md: recorrido y ejemplos para explicar macros, procedimientos y USES.
- comparacion/: fuente de Unidad 2 como referencia no compilable y conteo reproducible.
- evidencias/: resultados y transcripciones de ejecución real.
- inventario.dat y datos_prueba/: catálogo inicial y archivos de ejemplo.

El archivo inventario.dat es binario y mantiene el formato original. Se guarda en la carpeta de trabajo: la raíz de esta entrega al usar F5 o Ejecutar.cmd. Para reiniciar la demostración, cerrar el programa y copiar datos_prueba/inventario_ejemplo.dat sobre inventario.dat; esto reemplaza el catálogo guardado.

Las bibliotecas de Irvine32 deben estar instaladas para recompilar. No se cambiaron Defender ni sus exclusiones. No se ha publicado este proyecto en GitHub.
