# Guía de demostración y revisión oral

Alumnos:<br>
Medina González Cristian Roberto - 23170234<br>
Villalba Rodríguez Kevin Eliazar - 23170369<br>
Leon Fernandez Alexis Javier - 23171137<br>
Docente: Ing. José Luis Medina Jiménez 
Horario: 10:00 - 11:00

## Preparación

Extraer el ZIP. Con el programa cerrado, copiar datos_prueba/inventario_ejemplo.dat como inventario.dat para empezar con ESP-032 (10 unidades), RES-220 (4) y LED-005 (30). Abrir la solución con Debug/x86. La carpeta de trabajo debe ser la raíz de la entrega. El resumen inicial es 44 unidades y 1935.00 MXN; ingresos de sesión 0.00 MXN. RES-220 ya presenta alerta.

## Secuencia completa de la demostración

1. Elegir 1. Capturar ESP-032 para demostrar el rechazo del duplicado. Cuando vuelva a pedir el código, usar USB-001.
2. Nombre: Cable USB. Precio: 12.345; se rechaza por tener tres decimales. Recapturar 12.05. Existencia inicial: 6. Se acepta el alta.
3. Elegir 3 y buscar USB-001. Debe mostrar 12.05 MXN y seis unidades, sin alerta para ese producto.
4. Elegir 4, USB-001 y 95 unidades. Se rechaza porque 6 + 95 excede cien. Regresa al menú y conserva las seis unidades.
5. Repetir opción 4 con USB-001 y 1. Ahora queda en siete unidades.
6. Elegir 5, USB-001 y 8. Se rechaza por falta de existencias.
7. Repetir opción 5 con dos unidades. El importe es 24.10 MXN; quedan cinco y aparece la alerta. Esta es la comparación entre un caso sin regla aplicada (seis o siete) y otro con regla aplicada (cinco).
8. Elegir 6. El resumen debe mostrar 49 unidades, 1995.25 MXN de inventario y 24.10 MXN de ingresos de la sesión.
9. Elegir 0 antes de guardar. Se muestra el aviso; responder 0 para volver. Elegir 7 para guardar y después 0 para salir.
10. Ejecutar de nuevo. Buscar USB-001: siguen cinco unidades. Los ingresos ahora son 0.00 MXN porque pertenecen al proceso actual.
11. Con el programa cerrado, renombrar temporalmente inventario.dat como inventario.respaldo. Iniciar: debe avisar que no pudo cargar y permanecer con catálogo vacío. Cerrar y restaurar el archivo.
12. Para probar un archivo inválido sin perder el catálogo bueno, hacer una copia de respaldo y sustituir inventario.dat por datos_prueba/inventario_invalido.dat. Si el programa ya tiene un catálogo cargado y se usa la opción 8, el error debe conservar ese catálogo. Restaurar el archivo bueno al terminar.

## Recorrido con ESI en el depurador

Colocar F9 en fpLoop, dentro de FindProduct. Iniciar F5, elegir buscar y capturar LED-005. EDX señala el código solicitado; ESI comienza en catalog. productCount vale tres en el ejemplo inicial. Avanzar con F10: cada producto no coincidente suma SIZEOF Product, es decir 44 bytes, a ESI. El tercer registro está en catalog + 88. Abrir Registros y Memoria; mostrar los ocho bytes del código y los campos price y stock. ECX disminuye hasta encontrar el registro o agotar el catálogo.

## Conversión decimal y pila

Colocar F9 en utsDivide, dentro de UIntToString. Mostrar el resumen. EAX contiene el entero por convertir; EBX vale diez. Antes de DIV, EDX se limpia. Tras DIV, EAX conserva el cociente y EDX el residuo. Cada residuo se apila. En utsWrite, los POP recuperan los dígitos desde el más significativo, se suma '0' y se guardan en el buffer EDI. Mostrar que al volver de la función ESP recupera su valor de entrada. USES agrega la conservación de los registros declarados; no confundir estos PUSH/POP con los de los dígitos.


## Alcance de la evidencia

Los casos de consola y del núcleo incluidos en la tabla se ejecutaron. La navegación personal por la interfaz de Visual Studio y la exposición oral deben realizarse por el alumno; no se presentan como efectuadas.


## Explicación de Unidad 3

1. Abrir main.asm y mostrar PrintText: reemplaza MOV EDX / CALL WriteString y recibe la etiqueta del mensaje.
2. Mostrar ReportOperation y sus usos en SaveWithMessage y LoadWithMessage. LOCAL crea etiquetas distintas en cada expansión; CLC/STC devuelve el resultado después del mensaje.
3. Seguir DoReceive y DoSell hasta AskQuantityValue: ambos reutilizan la misma captura y rango.
4. Poner un punto de interrupción antes de CALL AskQuantityValue. Observar EBX, EBP y EDX, entrar y capturar una cantidad; al volver deben conservarse. EAX debe contener la cantidad, por eso no aparece en USES. Comparar ESP antes del CALL y después del retorno, en el mismo nivel de llamada.
5. Mostrar CopyBytes en altas, carga y guardado: USES conserva sus punteros y contador.
6. Explicar que una macro se expande al ensamblar, mientras un procedimiento se ejecuta mediante CALL. La disminución de 14 líneas de código no significa 14 instrucciones menos en el ejecutable.
7. Consultar la tabla de Unidad 3 y demostrar una venta rechazada sin cambios y una aceptada que active la alerta de cinco unidades.

Los pasos del depurador son una guía para la exposición; no se presentan como una sesión gráfica ya realizada.
