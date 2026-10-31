# Guía para aprender Python: imports, lambda y archivos

## ¿Qué vas a aprender?

En esta guía aprenderás a:

1. Usar código que está en otros archivos o carpetas.
2. Crear funciones pequeñas con `lambda`.
3. Transformar datos con `map` y seleccionar datos con `filter`.
4. Guardar y leer información en archivos.
5. Unir todo en un pequeño programa.

Necesitas conocer variables, listas, diccionarios, ciclos `for` y funciones con `def`. Los ejemplos usan Python 3.

## 1. Preparar el proyecto

Crea una carpeta llamada `clase_python` y ábrela con tu editor. Abre también una terminal dentro de esa carpeta.

Para ejecutar un archivo llamado `main.py`, escribe:

```bash
python main.py
```

En algunos equipos el comando es `python3` en lugar de `python`.

Los ejemplos de cada sección son independientes, salvo cuando se indica que debes conservar o modificar un archivo anterior.

## 2. Imports: usar código de otros lugares

Imagina que tienes una función para sumar. Si la necesitas en varios archivos, no hace falta copiarla en todos. Puedes guardarla en un archivo e importarla desde los demás.

Un módulo es un archivo con código Python. `import` permite usar ese código desde otro archivo.

### 2.1. Importar un módulo que viene con Python

Python incluye módulos listos para usar. Uno de ellos es `math`, que contiene herramientas matemáticas.

```python
import math

resultado = math.sqrt(25)
print(resultado)  # 5.0
```

¿Qué ocurre aquí?

1. `import math` permite usar el módulo.
2. `math.sqrt(25)` llama a su función para calcular la raíz cuadrada.
3. El punto une el nombre del módulo con el nombre de la función.

También puedes importar solo la función que necesitas:

```python
from math import sqrt

print(sqrt(25))  # 5.0
```

En este caso no escribes `math.` porque importaste directamente `sqrt`.

Puedes dar un nombre alternativo al módulo usando `as`:

```python
import math as matematicas

print(matematicas.sqrt(25))  # 5.0
```

### 2.2. Importar desde otro archivo de la misma carpeta

Crea estos dos archivos:

```text
clase_python/
├── main.py
└── operaciones.py
```

En `operaciones.py`, escribe:

```python
def sumar(a, b):
    return a + b


def multiplicar(a, b):
    return a * b
```

En `main.py`, escribe:

```python
import operaciones

print(operaciones.sumar(3, 4))
print(operaciones.multiplicar(3, 4))
```

Ejecuta `python main.py`. Verás:

```text
7
12
```

Otra forma de escribir `main.py` es:

```python
from operaciones import sumar, multiplicar

print(sumar(3, 4))
print(multiplicar(3, 4))
```

Las dos formas sirven. La diferencia es cómo usas los nombres:

| Importación | Cómo llamar la función |
|---|---|
| `import operaciones` | `operaciones.sumar(3, 4)` |
| `from operaciones import sumar` | `sumar(3, 4)` |

No escribas `import operaciones.py`: en el import se omite la extensión `.py`.

### 2.3. Importar desde otra carpeta

Ahora mueve `operaciones.py` a una carpeta llamada `utilidades`:

```text
clase_python/
├── main.py
└── utilidades/
    ├── __init__.py
    └── operaciones.py
```

Crea también un archivo vacío llamado `__init__.py` dentro de `utilidades`. En esta guía lo usaremos para organizar esa carpeta como un paquete: una forma de agrupar módulos relacionados.

En `main.py`, escribe:

```python
from utilidades.operaciones import sumar

print(sumar(10, 5))  # 15
```

Lee el import así:

> Del módulo `operaciones`, que está dentro del paquete `utilidades`, quiero usar `sumar`.

También puedes importar el módulo completo:

```python
from utilidades import operaciones

print(operaciones.multiplicar(10, 5))  # 50
```

Ejecuta `python main.py` desde `clase_python`. Mantener esta estructura y esta forma de ejecución evita confusiones mientras aprendes.

Nota: existen otras formas de crear paquetes sin `__init__.py`, pero no las necesitamos para estos ejemplos.

### 2.4. ¿Qué pasa con el código escrito fuera de las funciones?

Si escribes un `print` fuera de una función, ese código se ejecuta cuando Python carga el módulo por primera vez en el programa.

Para dejar una prueba que solo se ejecute al abrir directamente ese archivo, puedes escribir:

```python
# operaciones.py

def sumar(a, b):
    return a + b


if __name__ == "__main__":
    print(sumar(2, 3))
```

La última parte significa:

> Ejecuta esta prueba si este archivo es el punto de inicio del programa, pero no si otro archivo lo importa.

### 2.5. Extra: importar entre archivos del mismo paquete

Supón que agregas `reportes.py` dentro de `utilidades`:

```text
utilidades/
├── __init__.py
├── operaciones.py
└── reportes.py
```

Dentro de `reportes.py` puedes escribir:

```python
from .operaciones import sumar


def mostrar_total(a, b):
    print(sumar(a, b))


if __name__ == "__main__":
    mostrar_total(10, 5)
```

El punto inicial en `.operaciones` significa «dentro de este mismo paquete».

Para ejecutar ese módulo conservando su contexto de paquete, escribe desde `clase_python`:

```bash
python -m utilidades.reportes
```

No lo ejecutes como `python utilidades/reportes.py` en este ejemplo: el import relativo necesita que Python sepa a qué paquete pertenece el módulo.

### Consejos para evitar errores

- Revisa que los nombres de los archivos y las funciones estén bien escritos.
- No nombres tus archivos `math.py`, `json.py` o `pathlib.py`: pueden confundirse con módulos de Python.
- Evita `from operaciones import *`: es más claro indicar qué necesitas.
- Si aparece `ModuleNotFoundError`, revisa la estructura y cómo estás ejecutando el programa.

### Practica

Crea `utilidades/textos.py` con una función `saludar(nombre)`. Impórtala desde `main.py` y muestra un saludo.

Una solución:

```python
# utilidades/textos.py

def saludar(nombre):
    return f"Hola, {nombre}"
```

```python
# main.py
from utilidades.textos import saludar

print(saludar("Ana"))  # Hola, Ana
```

## 3. Funciones lambda: funciones pequeñas

Una función recibe datos y realiza una tarea. Ya puedes crear funciones con `def`:

```python
def duplicar(numero):
    return numero * 2


print(duplicar(5))  # 10
```

Una `lambda` es otra manera de crear una función, pensada para una operación breve.

Su forma es:

```text
lambda parámetros: expresión
```

Ejemplo para comparar con la función anterior:

```python
duplicar = lambda numero: numero * 2

print(duplicar(5))  # 10
```

Se lee así:

> Recibe un número y devuelve ese número multiplicado por dos.

- Antes de `:` van los datos que recibe.
- Después de `:` va la expresión cuyo resultado devuelve.
- No se escribe `return`.
- Su cuerpo es una sola expresión; no un bloque de instrucciones.

La asignación a `duplicar` sirve para comparar las dos formas. Si vas a darle un nombre y reutilizar mucho esa función, normalmente será más claro usar `def`.

Las lambdas son útiles cuando una función como `map`, `filter` o `sorted` necesita recibir otra función.

## 4. map: transformar cada elemento

Imagina esta lista:

```python
numeros = [1, 2, 3, 4]
```

Quieres obtener otra lista con cada número multiplicado por dos.

### 4.1. Primero, hacerlo con un for

```python
numeros = [1, 2, 3, 4]
dobles = []

for numero in numeros:
    dobles.append(numero * 2)

print(dobles)  # [2, 4, 6, 8]
```

El ciclo toma cada número, lo transforma y guarda el resultado.

### 4.2. Hacer la misma tarea con map y una función normal

`map` aplica una función a cada elemento de una colección.

```python
def duplicar(numero):
    return numero * 2


numeros = [1, 2, 3, 4]
dobles = list(map(duplicar, numeros))

print(dobles)  # [2, 4, 6, 8]
```

Observa que escribimos `duplicar`, sin paréntesis. Le estamos entregando la función a `map` para que la use con cada elemento.

### 4.3. Ahora, usar lambda

```python
numeros = [1, 2, 3, 4]

dobles = list(map(lambda numero: numero * 2, numeros))

print(dobles)  # [2, 4, 6, 8]
```

Vamos por partes:

```text
lambda numero: numero * 2   → indica cómo transformar un elemento
numeros                    → contiene los elementos que vamos a recorrer
map(...)                   → aplica la transformación a cada elemento
list(...)                  → reúne los resultados en una lista
```

El recorrido produce estos resultados:

| Elemento original | Operación | Resultado |
|---|---|---|
| 1 | `1 * 2` | 2 |
| 2 | `2 * 2` | 4 |
| 3 | `3 * 2` | 6 |
| 4 | `4 * 2` | 8 |

Idea principal: `map` transforma. En este ejemplo hay un resultado por cada elemento original.

### 4.4. Otro ejemplo: convertir nombres a mayúsculas

```python
nombres = ["Ana", "Luis", "Marta"]

mayusculas = list(map(lambda nombre: nombre.upper(), nombres))

print(mayusculas)  # ['ANA', 'LUIS', 'MARTA']
print(nombres)     # ['Ana', 'Luis', 'Marta']
```

`upper()` devuelve una versión del texto en mayúsculas. Esta operación crea resultados nuevos; no cambia los strings de la lista original.

`map` también acepta funciones que ya existen. No siempre necesitas una lambda:

```python
textos = ["10", "20", "30"]
numeros = list(map(int, textos))

print(numeros)  # [10, 20, 30]
```

Aquí `int` convierte cada texto en un número entero.

## 5. filter: quedarse con los elementos que cumplen una condición

Ahora queremos obtener solo los números pares de una lista.

Un número es par si el resto de dividirlo entre dos es cero. En Python, `%` permite obtener ese resto:

```python
print(4 % 2)  # 0
print(5 % 2)  # 1
```

### 5.1. Primero, hacerlo con un for

```python
numeros = [1, 2, 3, 4, 5, 6]
pares = []

for numero in numeros:
    if numero % 2 == 0:
        pares.append(numero)

print(pares)  # [2, 4, 6]
```

### 5.2. Hacerlo con filter y una función normal

`filter` conserva los elementos para los que una función devuelve un resultado verdadero. En nuestros ejemplos, esa función devolverá `True` o `False`.

```python
def es_par(numero):
    return numero % 2 == 0


numeros = [1, 2, 3, 4, 5, 6]
pares = list(filter(es_par, numeros))

print(pares)  # [2, 4, 6]
```

### 5.3. Ahora, usar lambda

```python
numeros = [1, 2, 3, 4, 5, 6]

pares = list(filter(lambda numero: numero % 2 == 0, numeros))

print(pares)  # [2, 4, 6]
```

Se lee así:

> Recorre los números y conserva aquellos que sean pares.

| Elemento | ¿`numero % 2 == 0`? | ¿Se conserva? |
|---|---|---|
| 1 | `False` | No |
| 2 | `True` | Sí: 2 |
| 3 | `False` | No |
| 4 | `True` | Sí: 4 |
| 5 | `False` | No |
| 6 | `True` | Sí: 6 |

Importante: `filter` no devuelve la lista de respuestas `True` y `False`. Devuelve los elementos originales que pasaron la condición.

### 5.4. Otro ejemplo: seleccionar estudiantes

```python
estudiantes = [
    {"nombre": "Ana", "nota": 18},
    {"nombre": "Luis", "nota": 8},
    {"nombre": "Marta", "nota": 20},
]

aprobados = list(filter(
    lambda estudiante: estudiante["nota"] >= 10,
    estudiantes,
))

print(aprobados)
```

Resultado:

```text
[{'nombre': 'Ana', 'nota': 18}, {'nombre': 'Marta', 'nota': 20}]
```

Para este ejercicio usamos notas sobre 20 y consideramos aprobada una nota mayor o igual a 10.

La lambda revisa una nota, pero `filter` conserva el diccionario completo del estudiante, no solo la nota.

## 6. Diferencias entre map y filter

| Pregunta | `map` | `filter` |
|---|---|---|
| ¿Para qué sirve? | Transformar cada elemento | Seleccionar elementos |
| ¿Qué devuelve la función que recibe? | El nuevo valor para ese elemento | Un valor que decide si se conserva |
| ¿Qué obtenemos al convertir a lista? | Los resultados de la transformación | Los elementos que cumplen la condición |
| Ejemplo | Duplicar números | Conservar números pares |

Una comparación importante:

```python
numeros = [1, 2, 3, 4]

resultado_map = list(map(lambda numero: numero > 2, numeros))
resultado_filter = list(filter(lambda numero: numero > 2, numeros))

print(resultado_map)     # [False, False, True, True]
print(resultado_filter)  # [3, 4]
```

Con la misma lambda:

- `map` guarda el resultado de cada comparación.
- `filter` usa la comparación para decidir qué números conservar.

### 6.1. ¿Por qué usamos list?

En Python 3, `map` y `filter` no devuelven directamente una lista. Devuelven un iterador: algo que permite obtener resultados uno a uno, a medida que se recorre.

Usamos `list(...)` para recorrerlo y reunir sus resultados en una lista.

```python
resultado = map(lambda numero: numero * 2, [1, 2, 3])

print(list(resultado))  # [2, 4, 6]
print(list(resultado))  # []
```

La segunda lista está vacía porque ya recorrimos todos los resultados de ese iterador. Para repetir la operación, crea un nuevo `map` o guarda la lista obtenida la primera vez.

También puedes recorrerlo con un `for`, sin convertirlo primero en lista:

```python
resultado = map(lambda numero: numero * 2, [1, 2, 3])

for numero in resultado:
    print(numero)
```

### 6.2. Usar filter y map en una misma tarea

Queremos seleccionar estudiantes con nota mayor o igual a 10 y después obtener solo sus nombres.

```python
estudiantes = [
    {"nombre": "Ana", "nota": 18},
    {"nombre": "Luis", "nota": 8},
    {"nombre": "Marta", "nota": 20},
]

aprobados = list(filter(
    lambda estudiante: estudiante["nota"] >= 10,
    estudiantes,
))

nombres = list(map(
    lambda estudiante: estudiante["nombre"],
    aprobados,
))

print(nombres)  # ['Ana', 'Marta']
```

El proceso es:

```text
Todos los estudiantes
        ↓ filter: seleccionar por nota
Estudiantes aprobados
        ↓ map: obtener el nombre de cada uno
Nombres de los aprobados
```

Separar los pasos ayuda a entender y revisar el programa.

### 6.3. Otra forma de resolverlo

También puedes usar comprensiones de listas, una manera breve de construir listas:

```python
numeros = [1, 2, 3, 4]

dobles = [numero * 2 for numero in numeros]
pares = [numero for numero in numeros if numero % 2 == 0]
```

No es obligatorio usar `map`, `filter` o lambda en todos los casos. Elige una forma que puedas entender y explicar. Si la lógica necesita varios pasos, una función con `def` suele ser más clara.

## 7. Lambda con sorted: ordenar datos

`sorted` devuelve una lista ordenada. El argumento `key` permite indicar qué dato se usará para ordenar.

```python
estudiantes = [
    {"nombre": "Ana", "nota": 18},
    {"nombre": "Luis", "nota": 12},
    {"nombre": "Marta", "nota": 20},
]

ordenados = sorted(
    estudiantes,
    key=lambda estudiante: estudiante["nota"],
    reverse=True,
)

for estudiante in ordenados:
    print(estudiante["nombre"], estudiante["nota"])
```

Resultado:

```text
Marta 20
Ana 18
Luis 12
```

- La lambda devuelve la nota que se usa como criterio.
- `reverse=True` indica orden de mayor a menor.
- El resultado conserva los estudiantes completos, no solo sus notas.
- `sorted` crea una lista nueva; no cambia el orden de la lista original.

Para ordenar por nombre:

```python
por_nombre = sorted(estudiantes, key=lambda estudiante: estudiante["nombre"])
```

## 8. Manejo de archivos: guardar información

Las variables de estos ejemplos viven mientras se ejecuta el programa. Un archivo permite guardar información para leerla después, incluso cuando el programa ya terminó.

### 8.1. Abrir un archivo

Usamos `open` para abrirlo y `with` para trabajar con él y cerrarlo al terminar el bloque.

```python
with open("mensaje.txt", "w", encoding="utf-8") as archivo:
    archivo.write("Hola desde Python\n")
```

- `"mensaje.txt"`: nombre o ruta del archivo.
- `"w"`: modo de escritura.
- `encoding="utf-8"`: codificación para guardar el texto, incluidos acentos y la letra ñ.
- `archivo`: variable con la que trabajamos dentro del bloque.
- `write`: escribe texto.
- `\n`: salto de línea.

`with` cierra el archivo al salir del bloque, incluso si ocurre un error dentro de él.

### 8.2. Elegir el modo correcto

| Modo | Para qué sirve | Si no existe | Si ya existe |
|---|---|---|---|
| `r` | Leer | Produce un error | Permite leerlo |
| `w` | Escribir desde cero | Lo crea | Borra el contenido anterior al abrir |
| `a` | Agregar al final | Lo crea | Conserva lo anterior |
| `x` | Crear un archivo nuevo | Lo crea | Produce un error |

Estas operaciones necesitan permisos suficientes y una carpeta contenedora que exista.

Cuidado: usa `w` solo si quieres crear o reemplazar el contenido. Practica con archivos que puedas borrar.

### 8.3. Escribir varias líneas

```python
with open("notas.txt", "w", encoding="utf-8") as archivo:
    archivo.write("Ana: 18\n")
    archivo.write("Luis: 12\n")
```

El archivo tendrá:

```text
Ana: 18
Luis: 12
```

`write` no agrega saltos de línea automáticamente. Si los necesitas, escribe `\n`.

Para escribir un número junto con texto, puedes usar un f-string:

```python
nota = 18

with open("nota.txt", "w", encoding="utf-8") as archivo:
    archivo.write(f"La nota es {nota}\n")
```

### 8.4. Leer todo el contenido

Después de crear `notas.txt`, ejecuta:

```python
with open("notas.txt", "r", encoding="utf-8") as archivo:
    contenido = archivo.read()

print(contenido)
```

`read()` obtiene el contenido restante como un string.

### 8.5. Leer línea por línea

```python
with open("notas.txt", "r", encoding="utf-8") as archivo:
    for linea in archivo:
        print(linea.rstrip("\n"))
```

`rstrip("\n")` quita el salto de línea del final para que `print` no produzca una línea vacía adicional.

También existen:

- `readline()`: lee la siguiente línea.
- `readlines()`: devuelve una lista con las líneas restantes.

Al leer, avanzamos dentro del archivo. Si ya llegamos al final, otra llamada a `read()` devolverá `""`. Puedes cerrar y volver a abrir el archivo para leerlo desde el inicio.

### 8.6. Agregar contenido sin borrar lo anterior

```python
with open("notas.txt", "a", encoding="utf-8") as archivo:
    archivo.write("Marta: 20\n")
```

Ahora el archivo tendrá también la línea de Marta. Si ejecutas ese código dos veces, se agregará dos veces.

### 8.7. Entender las rutas

Una ruta indica dónde está un archivo.

```python
open("notas.txt", "r", encoding="utf-8")
```

Una ruta relativa como `"notas.txt"` se busca desde el directorio de trabajo actual. No siempre coincide con la carpeta donde está el archivo `.py`.

Puedes comprobar ese directorio con:

```python
from pathlib import Path

print(Path.cwd())
```

Para guardar datos junto a tu script de manera más predecible:

```python
from pathlib import Path

base = Path(__file__).resolve().parent
carpeta = base / "datos"
carpeta.mkdir(parents=True, exist_ok=True)
ruta = carpeta / "notas.txt"

with open(ruta, "w", encoding="utf-8") as archivo:
    archivo.write("Ana: 18\n")
```

Paso a paso:

1. `Path(__file__).resolve().parent` obtiene la carpeta de este archivo `.py`.
2. `/ "datos"` construye una ruta hacia la subcarpeta `datos`.
3. `mkdir` crea la carpeta si hace falta. `exist_ok=True` evita un error si ya existe.
4. `/ "notas.txt"` construye la ruta final del archivo.

`open` puede crear un archivo con `w` o `a`, pero no crea las carpetas que falten.

Este ejemplo está pensado para un archivo `.py`: `__file__` normalmente no está disponible en una consola interactiva o en un notebook.

### 8.8. ¿Qué pasa si el archivo no existe?

Puedes manejar ese caso con `try` y `except`:

```python
try:
    with open("pendientes.txt", "r", encoding="utf-8") as archivo:
        contenido = archivo.read()
except FileNotFoundError:
    print("El archivo todavía no existe.")
else:
    print(contenido)
```

- `try`: intenta ejecutar este código.
- `except FileNotFoundError`: indica qué hacer si el archivo no se encuentra.
- `else`: se ejecuta si el bloque `try` terminó sin ese error ni otro error.

Esto maneja un caso concreto. Otros errores, como no tener permisos, necesitan su propio tratamiento.

## 9. Proyecto final: reporte de estudiantes

Vamos a unir los temas:

1. Importar funciones de otro archivo.
2. Seleccionar estudiantes con `filter`.
3. Ordenarlos usando una lambda.
4. Convertir sus datos en líneas de texto con `map`.
5. Guardar el reporte y leerlo.

### 9.1. Estructura del proyecto

```text
clase_python/
├── main.py
└── utilidades/
    ├── __init__.py
    └── archivos.py
```

Puedes conservar los módulos de ejercicios anteriores. La carpeta `datos` se creará al ejecutar el programa.

### 9.2. Crear utilidades/archivos.py

```python
def guardar_lineas(ruta, lineas):
    with open(ruta, "w", encoding="utf-8") as archivo:
        archivo.write("Estudiantes aprobados\n")
        archivo.write("=====================\n")

        for linea in lineas:
            archivo.write(linea + "\n")


def leer_archivo(ruta):
    with open(ruta, "r", encoding="utf-8") as archivo:
        return archivo.read()
```

La primera función escribe el reporte. La segunda devuelve su contenido.

### 9.3. Crear main.py

```python
from pathlib import Path

from utilidades.archivos import guardar_lineas, leer_archivo


def main():
    estudiantes = [
        {"nombre": "Ana", "nota": 18},
        {"nombre": "Luis", "nota": 8},
        {"nombre": "Marta", "nota": 20},
    ]

    # 1. Seleccionar estudiantes con nota mayor o igual a 10.
    aprobados = list(filter(
        lambda estudiante: estudiante["nota"] >= 10,
        estudiantes,
    ))

    # 2. Ordenar por nota, de mayor a menor.
    ordenados = sorted(
        aprobados,
        key=lambda estudiante: estudiante["nota"],
        reverse=True,
    )

    # 3. Transformar cada diccionario en una línea de texto.
    lineas = list(map(
        lambda estudiante: f"{estudiante['nombre']}: {estudiante['nota']}",
        ordenados,
    ))

    # 4. Preparar la carpeta y la ruta del archivo.
    base = Path(__file__).resolve().parent
    carpeta = base / "datos"
    carpeta.mkdir(parents=True, exist_ok=True)
    ruta = carpeta / "reporte.txt"

    # 5. Guardar y mostrar el reporte.
    guardar_lineas(ruta, lineas)
    print(leer_archivo(ruta))


if __name__ == "__main__":
    main()
```

### 9.4. Ejecutar

Desde la carpeta `clase_python`:

```bash
python main.py
```

Resultado:

```text
Estudiantes aprobados
=====================
Marta: 20
Ana: 18
```

También encontrarás ese contenido en `datos/reporte.txt`.

### 9.5. Entender el recorrido de los datos

```text
Lista original: Ana, Luis y Marta
                ↓ filter
Aprobados: Ana y Marta
                ↓ sorted
Ordenados por nota: Marta y Ana
                ↓ map
Textos: "Marta: 20" y "Ana: 18"
                ↓ guardar_lineas
Archivo reporte.txt
```

En este proyecto, cada función tiene una responsabilidad concreta. Eso facilita entender dónde revisar si algo no sale como esperabas.

## 10. Ejercicios para practicar

### Ejercicio 1: imports

Crea `utilidades/conversiones.py` con una función que convierta minutos a segundos. Úsala desde `main.py`.

### Ejercicio 2: map

Dada la lista `[10, 20, 30]`, usa `map` con una lambda para sumar 5 a cada número.

Resultado esperado: `[15, 25, 35]`.

### Ejercicio 3: filter

Dada la lista `[12, 17, 18, 25, 15]`, conserva las edades mayores o iguales a 18.

Resultado esperado: `[18, 25]`.

### Ejercicio 4: combinar operaciones

Dada la lista `[1, 2, 3, 4, 5, 6]`:

1. Conserva los números pares con `filter`.
2. Multiplica esos números por 10 usando `map`.

Resultado esperado: `[20, 40, 60]`.

### Ejercicio 5: archivos

Crea `compras.txt` con dos productos usando `w`. Agrega un tercero con `a` y luego lee el archivo.

Antes de ejecutarlo, piensa: ¿qué pasaría si usaras `w` para agregar el tercer producto?

## 11. Soluciones de los ejercicios

Intenta resolverlos antes de mirar esta sección.

### Solución 1

```python
# utilidades/conversiones.py

def minutos_a_segundos(minutos):
    return minutos * 60
```

```python
# main.py
from utilidades.conversiones import minutos_a_segundos

print(minutos_a_segundos(3))  # 180
```

### Solución 2

```python
numeros = [10, 20, 30]
resultado = list(map(lambda numero: numero + 5, numeros))
print(resultado)  # [15, 25, 35]
```

### Solución 3

```python
edades = [12, 17, 18, 25, 15]
mayores = list(filter(lambda edad: edad >= 18, edades))
print(mayores)  # [18, 25]
```

### Solución 4

```python
numeros = [1, 2, 3, 4, 5, 6]
pares = list(filter(lambda numero: numero % 2 == 0, numeros))
resultado = list(map(lambda numero: numero * 10, pares))
print(resultado)  # [20, 40, 60]
```

### Solución 5

```python
with open("compras.txt", "w", encoding="utf-8") as archivo:
    archivo.write("Pan\n")
    archivo.write("Leche\n")

with open("compras.txt", "a", encoding="utf-8") as archivo:
    archivo.write("Arroz\n")

with open("compras.txt", "r", encoding="utf-8") as archivo:
    print(archivo.read())
```

Si usaras `w` en el segundo bloque, se borraría lo anterior y solo quedaría `Arroz`.

## 12. Resumen rápido

| Herramienta | Recuerda esto |
|---|---|
| `import` | Permite usar código de otro módulo |
| `from ... import ...` | Importa un nombre concreto |
| `lambda` | Crea una función de una sola expresión |
| `map` | Transforma cada elemento |
| `filter` | Conserva los elementos que pasan una condición |
| `sorted` | Devuelve una lista ordenada |
| `list` | Puede reunir en una lista los resultados de un iterador |
| `with open(...)` | Permite trabajar con el archivo y cerrarlo al salir |
| `r` | Lee |
| `w` | Escribe desde cero y reemplaza lo anterior |
| `a` | Agrega al final |

## Documentación para seguir aprendiendo

- Módulos y paquetes: https://docs.python.org/3/tutorial/modules.html
- Funciones lambda: https://docs.python.org/3/tutorial/controlflow.html#lambda-expressions
- Funciones incorporadas, incluidas map y filter: https://docs.python.org/3/library/functions.html
- Lectura y escritura de archivos: https://docs.python.org/3/tutorial/inputoutput.html#reading-and-writing-files
