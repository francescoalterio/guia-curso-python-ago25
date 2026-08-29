# Guía para estudiantes: métodos de strings en Python

## ¿Qué es un string?

Un **string** es texto.

En Python, un string se guarda entre comillas.

Ejemplos:

```python
nombre = "Carlos"
mensaje = "Hola mundo"
```

---

## ¿Para qué sirven los métodos de strings?

Los **métodos** son acciones que un string sabe hacer.

Sirven para:

- cambiar mayúsculas y minúsculas
- quitar espacios
- reemplazar texto
- buscar palabras
- dividir texto
- unir texto
- contar caracteres o partes del texto

---

## Idea importante

> Un método es una acción que podemos hacer sobre un texto.

Ejemplo:

```python
texto = "hola"
print(texto.upper())
```

Resultado:

```python
HOLA
```

---

# Métodos de strings más importantes

## 1. `upper()`

Convierte el texto a mayúsculas.

```python
texto = "hola"
print(texto.upper())
```

Resultado:

```python
HOLA
```

---

## 2. `lower()`

Convierte el texto a minúsculas.

```python
texto = "HoLa"
print(texto.lower())
```

Resultado:

```python
hola
```

Muy útil cuando queremos comparar texto sin importar mayúsculas o minúsculas.

```python
respuesta = input("Escribe si o no: ").lower()

if respuesta == "si":
    print("Elegiste sí")
```

---

## 3. `strip()`

Quita espacios al inicio y al final.

```python
texto = "   hola   "
print(texto.strip())
```

Resultado:

```python
hola
```

Muy útil cuando el usuario escribe espacios sin querer.

---

## 4. `replace()`

Reemplaza una parte del texto por otra.

```python
texto = "Me gusta Python"
print(texto.replace("Python", "programar"))
```

Resultado:

```python
Me gusta programar
```

---

## 5. `find()`

Busca una parte del texto y devuelve su posición.

```python
texto = "Hola mundo"
print(texto.find("mundo"))
```

Resultado:

```python
5
```

Si no encuentra el texto, devuelve `-1`.

```python
texto = "Hola mundo"
print(texto.find("Python"))
```

Resultado:

```python
-1
```

---

## 6. `startswith()`

Sirve para saber si un texto empieza con algo.

```python
texto = "Python es fácil"
print(texto.startswith("Python"))
```

Resultado:

```python
True
```

---

## 7. `endswith()`

Sirve para saber si un texto termina con algo.

```python
correo = "usuario@gmail.com"
print(correo.endswith(".com"))
```

Resultado:

```python
True
```

---

## 8. `split()`

Divide un string en partes y devuelve una lista.

```python
texto = "rojo,verde,azul"
colores = texto.split(",")
print(colores)
```

Resultado:

```python
['rojo', 'verde', 'azul']
```

---

## 9. `join()`

Une varios strings en uno solo.

```python
palabras = ["Hola", "mundo"]
resultado = " ".join(palabras)
print(resultado)
```

Resultado:

```python
Hola mundo
```

---

## 10. `count()`

Cuenta cuántas veces aparece algo dentro del texto.

```python
texto = "banana"
print(texto.count("a"))
```

Resultado:

```python
3
```

---

## 11. `title()`

Convierte en mayúscula la primera letra de cada palabra.

```python
nombre = "juan perez"
print(nombre.title())
```

Resultado:

```python
Juan Perez
```

---

## 12. `capitalize()`

Convierte en mayúscula solo la primera letra del texto.

```python
texto = "hola mundo"
print(texto.capitalize())
```

Resultado:

```python
Hola mundo
```

---

# Función útil con strings: `len()`

`len()` no es un método, pero se usa mucho con strings.

Sirve para saber cuántos caracteres tiene un texto.

```python
texto = "Python"
print(len(texto))
```

Resultado:

```python
6
```

---

# Ejemplos sencillos

## Ejemplo 1: nombre en mayúsculas

```python
nombre = input("Escribe tu nombre: ")
print(nombre.upper())
```

---

## Ejemplo 2: frase en minúsculas

```python
frase = input("Escribe una frase: ")
print(frase.lower())
```

---

## Ejemplo 3: limpiar espacios

```python
nombre = input("Escribe tu nombre: ").strip()
print("Hola", nombre)
```

---

## Ejemplo 4: reemplazar texto

```python
frase = "Me gusta Java"
nueva_frase = frase.replace("Java", "Python")
print(nueva_frase)
```

---

## Ejemplo 5: revisar si un correo termina en `.com`

```python
correo = input("Escribe tu correo: ").strip().lower()

if correo.endswith(".com"):
    print("Termina en .com")
else:
    print("No termina en .com")
```

---

## Ejemplo 6: dividir una frase en palabras

```python
frase = "Python es muy útil"
palabras = frase.split(" ")
print(palabras)
```

Resultado:

```python
['Python', 'es', 'muy', 'útil']
```

---

## Ejemplo 7: unir palabras

```python
palabras = ["Hola", "a", "todos"]
frase = " ".join(palabras)
print(frase)
```

Resultado:

```python
Hola a todos
```

---

# Combinar métodos

Podemos usar varios métodos juntos.

```python
nombre = input("Escribe tu nombre: ").strip().title()
print("Hola", nombre)
```

### ¿Qué pasa aquí?

- `strip()` quita espacios
- `title()` pone en mayúscula la primera letra de cada palabra

---

## Otro ejemplo combinado

```python
respuesta = input("Escribe si o no: ").strip().lower()

if respuesta == "si":
    print("Correcto")
else:
    print("Respuesta diferente")
```

---

# Ejercicios

## Ejercicio 1
Pide al usuario su nombre y muéstralo en mayúsculas.

```python
nombre = input("Escribe tu nombre: ")
print(nombre.upper())
```

---

## Ejercicio 2
Pide una frase y muéstrala en minúsculas.

```python
frase = input("Escribe una frase: ")
print(frase.lower())
```

---

## Ejercicio 3
Pide una palabra con espacios y luego quítalos.

```python
palabra = input("Escribe una palabra con espacios: ")
print(palabra.strip())
```

---

## Ejercicio 4
Pide una frase y reemplaza una letra.

```python
frase = input("Escribe una frase: ")
print(frase.replace("a", "@"))
```

---

## Ejercicio 5
Pide una palabra y muestra cuántas letras tiene.

```python
palabra = input("Escribe una palabra: ")
print(len(palabra))
```

---

## Ejercicio 6
Cuenta cuántas veces aparece una letra.

```python
texto = input("Escribe una frase: ").lower()
letra = input("Escribe una letra: ").lower()
print(texto.count(letra))
```

---

## Ejercicio 7
Divide una frase en palabras.

```python
frase = input("Escribe una frase: ")
print(frase.split(" "))
```

---

## Ejercicio 8
Comprueba si una frase empieza con cierta palabra.

```python
frase = input("Escribe una frase: ")

if frase.startswith("Hola"):
    print("Empieza con Hola")
else:
    print("No empieza con Hola")
```

---

## Ejercicio 9
Comprueba si un texto termina en `.py`.

```python
archivo = input("Escribe un nombre de archivo: ")

if archivo.endswith(".py"):
    print("Es un archivo de Python")
else:
    print("No es un archivo de Python")
```

---

## Ejercicio 10
Une varias palabras en una frase.

```python
palabras = ["Python", "es", "genial"]
frase = " ".join(palabras)
print(frase)
```

---

# Ejercicios extra

## Ejercicio: limpiar y formatear nombre

```python
nombre = input("Escribe tu nombre completo: ").strip().title()
print(nombre)
```

---

## Ejercicio: buscar palabra

```python
frase = input("Escribe una frase: ")
print(frase.find("Python"))
```

---

## Ejercicio: contar palabras

```python
frase = input("Escribe una frase: ").strip()
palabras = frase.split()
print("Cantidad de palabras:", len(palabras))
```

---

## Ejercicio: validador simple

```python
respuesta = input("¿Quieres continuar? (si/no): ").strip().lower()

if respuesta == "si":
    print("Continuando...")
elif respuesta == "no":
    print("Saliendo...")
else:
    print("Respuesta no válida")
```

---

# Errores comunes

## 1. Olvidar los paréntesis

Incorrecto:

```python
print(texto.upper)
```

Correcto:

```python
print(texto.upper())
```

---

## 2. Pensar que `len()` es un método

Incorrecto:

```python
texto.len()
```

Correcto:

```python
len(texto)
```

---

## 3. Pensar que el string cambia solo

```python
texto = "hola"
texto.upper()
print(texto)
```

Resultado:

```python
hola
```

Si quieres guardar el cambio:

```python
texto = "hola"
texto = texto.upper()
print(texto)
```

---

## 4. Confundir texto con números

Incorrecto:

```python
edad = 20
print("Tu edad es " + edad)
```

Correcto:

```python
edad = 20
print("Tu edad es", edad)
```

O:

```python
print("Tu edad es " + str(edad))
```

---

# Resumen rápido

Métodos importantes de strings:

- `upper()` → mayúsculas
- `lower()` → minúsculas
- `strip()` → quitar espacios
- `replace()` → reemplazar texto
- `find()` → buscar posición
- `startswith()` → comprobar inicio
- `endswith()` → comprobar final
- `split()` → dividir texto
- `join()` → unir texto
- `count()` → contar repeticiones
- `title()` → primera letra de cada palabra en mayúscula
- `capitalize()` → primera letra del texto en mayúscula

Y además:

- `len()` → contar caracteres

---

# Chuleta rápida

## Convertir a mayúsculas

```python
texto.upper()
```

## Convertir a minúsculas

```python
texto.lower()
```

## Quitar espacios

```python
texto.strip()
```

## Reemplazar

```python
texto.replace("a", "@")
```

## Buscar

```python
texto.find("hola")
```

## Ver si empieza con algo

```python
texto.startswith("Hola")
```

## Ver si termina con algo

```python
texto.endswith(".com")
```

## Dividir texto

```python
texto.split(",")
```

## Unir texto

```python
" ".join(lista)
```

## Contar repeticiones

```python
texto.count("a")
```

## Contar caracteres

```python
len(texto)
```

---

# Cierre

Los métodos de strings son muy útiles porque permiten trabajar mejor con texto.

Gracias a ellos podemos:

- limpiar respuestas del usuario
- comparar palabras
- buscar partes del texto
- separar información
- unir texto
- validar entradas

Son herramientas muy importantes en Python porque casi todos los programas trabajan con texto en algún momento.
