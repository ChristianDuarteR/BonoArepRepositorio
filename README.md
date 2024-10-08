# Bono: Calculadora Web Distribuida con Reflexión y Bubble Sort

## Descripción

Este taller de refuerzo es una aplicación web distribuida que permite realizar operaciones matemáticas a través de sockets y HTTP. La aplicación acepta una operación de la biblioteca `Math` de Java o un comando especial llamado `bbl`, que aplica el algoritmo de ordenamiento `Bubble Sort` a una lista de números. 

El comando se invoca dinámicamente utilizando reflexión, y la aplicación asume que todos los números proporcionados son de tipo `Double`.

### Componentes del Proyecto
El proyecto se compone de tres partes distribuidas:

1. **Fachada de Servicios (ServiceFacade)**: Delega las solicitudes al servicio de calculadora y entrega el cliente web.
2. **Calculadora (ReflexCalculator)**: Se encarga de realizar el cálculo real de las operaciones.
3. **Cliente Web**: Un cliente HTML y JavaScript que realiza peticiones a la fachada de servicios para calcular las operaciones.

## Requisitos

- **No utilizar frameworks como Spring o Spark.** El proyecto debe realizarse solo con sockets.
- **No copiar código de internet o de archivos antiguos.** El código debe seguir el enunciado de este proyecto.
- **Comunicación mediante HTTP y JSON.** Las respuestas entre los servicios deben estar en formato JSON.
- **Desplegar en máquinas virtuales separadas.** Cada componente debe estar en su propia máquina virtual de Java.
- **Asincronía en las peticiones.** El cliente web debe hacer peticiones asincrónicas (AJAX) sin recargar la página.

## Arquitectura

1. **Fachada de Servicios(CalcReflex):**
   - Ruta `/computar?comando=[comando con parámetros]`: Invoca el servicio de cálculo y devuelve el resultado en formato JSON.

2. **Servicio de Calculadora:(CalcRealReflex)**
   - Ruta `/compreflex?comando=[comando con parámetros]`: Realiza el cálculo reflejado del comando y devuelve el resultado en JSON.

3. **Cliente Web:**
   - Realiza peticiones asíncronas a la fachada de servicios para ejecutar cálculos matemáticos sin recargar la página.
   - El cliente web se sirve desde el puerto 8080

## Funcionalidades

1. **Operaciones Matemáticas:**
   - Cualquier operación de la biblioteca `Math` de Java puede ser invocada dinámicamente a través de reflexión.
   - Ejemplo: `/computar?comando=sqrt(16)` devolverá `4.0`.
   - Ejemplo `/computar?comando=bbl(16,-3,1,0,112,3)` devolvera la lista ordenada

2. **Ordenamiento Bubble Sort (`bbl`):**
   - Si el comando recibido es `bbl`, se aplica el algoritmo de ordenamiento a una lista de números.
   - Ejemplo: `/computar?comando=bbl(5,3,8,4,2)` devolverá `[2.0, 3.0, 4.0, 5.0, 8.0]`.

## Instrucciones de Despliegue

1. **Compilar y Ejecutar el Proyecto:**
   - Compila el proyecto usando Maven y Java:
   - Preferiblemente Java 17 y Maven 3.9.6
     mvn clean install

2. **Despliegue en Máquinas Virtuales Separadas:**
   - La **fachada de servicios** y la **calculadora** deben ejecutarse en máquinas virtuales Java diferentes. Inicia ambos servicios en diferentes Maquinas de JVM

3. **Configuración del Cliente Web:**
   - El cliente web se descarga directamente desde el servicio de la fachada. Simplemente accede a la ruta `localhost:35000` para obtener la interfaz web.

## Ejemplo de Uso

### Instrucciones para el Cliente Web

1. Abre el cliente web en tu navegador 
2. Introduce un comando en el campo de texto (ejemplo: `pow(2,3)` o `bbl(5,3,8)`).
3. Haz clic en el botón "Submit" para ejecutar la operación.
4. El resultado se mostrará de forma asincrónica en la página sin recargarla.

### Ejemplo de Comandos

- **Raíz cuadrada de 16:**
  - Comando: `sqrt(16)`
  - Resultado: `4.0`
  
- **Bubble Sort de la lista [5, 3, 8, 4, 2]:**
  - Comando: `bbl(5,3,8,4,2)`
  - Resultado: `[2.0, 3.0, 4.0, 5.0, 8.0]`

## Buenas Prácticas

- **Reflexión en Java:** Utiliza la API de reflexión de Java para invocar métodos dinámicamente. La clase `Method` en el paquete `java.lang.reflect` será útil para ejecutar métodos de la clase `Math`.

Proyecto desarrollado por: **[Christian Duarte]**


