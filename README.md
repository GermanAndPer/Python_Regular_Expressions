#
**************************************************************************************

# [![](https://www.codingforentrepreneurs.com/_next/image?url=https%3A%2F%2Fimagedelivery.net%2F-inYktE1L-xCpqjE0wGFvg%2Fd8b92f4f-c5f4-4847-b2a9-8c8368405300%2FblogDetail&w=1200&q=75)](https://docs.python.org/3/library/re.html)

## Introducción

Las expresiones regulares (regex) son patrones que nos permiten buscar, extraer, y transformar textos. En Python se utiliza el módulo [`re`](https://docs.python.org/3/library/re.html) para trabajar con estos patrones.

### NOTAS:
1. Para carácteres especificos, la busqueda es 100% especifica. Si buscas 'a' solo buscará 'a'. Significa que ignorará a la 'A' 
--------------------------------------
Por lo mismo lo primero que se importará será el modulo  _RE_.
```python
import re
```
# ️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️
# ___METACARACTERES BÁSICOS___

# 1. El punto (.) representa cualquier carácter excepto un salto de línea.

```python
pattern = r'a.' 
```
#### Se buscará cualquier 'a' y que justo despues  tenga cualquier otro carácter
```python
pattern = r'a.' 
texto = "abc ade a " # Datos a evaluar
# Esta evaluacion devolverá 'ab' y 'ad' por que son todas las 'a' seguida de otro carácter. 
resultado = re.findall(pattern, texto) # Así se aplica REGEX (.)
print("Texto a Analizar:", texto)
print("Regex utilizada:", pattern)
print("Resultado:", resultado, "\n")
```

# 2. El símbolo (^) o (caret) indica el inicio de una línea.
```python
pattern = r'^Hola'
```
#### Se buscará cualquier linea que al iniciar tenga 'Hola'
```python
pattern = r'^Hola'
texto = """Hola Mundo 1
HolaMundo 2
hola Mundo 3
Adiós Mundo""" # Datos a evaluar
resultado = re.findall(pattern, texto, flags=re.MULTILINE)
# flags=re.MULTILINE --- Con el flag MULTILINE, ^ verifica el inicio de cada línea.
# Se evaluaran todas las lineas y te devolverá el inicio las lineas que empiezan de acuerdo a la indicación.
print("Texto a Analizar: ", texto)
print("Regex utilizada:", pattern)
print("Resultado:", resultado)
```

# 3. El símbolo ($) indica el final de una línea.
```python
pattern = r'Mundo$'
```
#### Se buscará cualquier linea que al final se  encuentre la palabra 'Mundo'.
```python
pattern = r'Mundo$'
texto = """Hola Mundo
HolaMundo 2
hola Mundo
Adiós Mundo """ # Datos a evaluar
resultado = re.findall(pattern, texto, flags=re.MULTILINE)
print("Texto a Analizar: ", texto)
print("Regex utilizada:", pattern)
print("Resultado:", resultado)
```

# 4. El backslash (\\) se utiliza para especificar caracteres especiales.
```python
pattern = r'\.'   
```
#### Se buscará literalmente cualquier punto(.).
```python
pattern = r'\.'
texto = "a.b, c,d. ... .,."
resultado = re.findall(pattern, texto)
print("Texto a Analizar: ", texto)
print("Regex utilizada:", pattern)
print("Resultado:", resultado)
```
# ️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️
# ___CUANTIFICADORES___
# 5. El asterisco (*) indica 0 o más repeticiones del elemento anterior.

```python
pattern = r'go*'
```
#### En 'go*',  se busca 'g' y 'g' y que seguido todas las 'o' que se encuentren. Si hya otros carácteres, los omite.
```python
pattern = r'go*'
texto = "g go goooo ga"
resultado = re.findall(pattern, texto)
print("Texto a Analizar: ", texto)
print("Regex utilizada:", pattern)
print("Resultado:", resultado)
```
# 6. El signo más (+) indica 1 o más repeticiones.
```python
pattern = r'go+'
```
#### Solo se captura si al menos hay 1 'o'. A diferencia del *, no te devuelve si aparece solo la 'g'
```python
pattern = r'go+'
texto = "g go goooo"
resultado = re.findall(pattern, texto)
print("Texto a Analizar: ", texto)
print("Regex utilizada:", pattern)
print("Resultado:", resultado)
```
# 7. El signo de interrogación (?) indica 0 o 1 repetición del elemento anterior.
```python
pattern = r'go?'
```
#### 'go?' captura 'g' (sin 'o') y 'go' (con una 'o'), pero en 'goo' solo toma la primera instancia.
```python
pattern = r'go?'
texto = "g go goo"
resultado = re.findall(pattern, texto)
print("Texto a Analizar: ", texto)
print("Regex utilizada:", pattern)
print("Resultado:", resultado)
```
# 8. Uso de {n}, {n,} y {n,m} para repeticiones exactas o rangos.

```python
pattern = r'\d{3}'
```
#### Busca secuencias de exactamente 3 dígitos.
```python
pattern = r'\d{3}'
texto = "123456789"
resultado = re.findall(pattern, texto)
print("8. Cuantificador {n}")
print("Explicación: '\\d{3}' busca grupos de exactamente 3 dígitos consecutivos.")
print("Texto:", texto)
print("Regex:", pattern)
print("Resultado:", resultado, "\n")
```
# 9. Busca grupos de 2 o más dígitos.
```python
pattern = r'\d{2,}'
```
#### busca grupos de al menos 2 dígitos consecutivos.
```python
pattern = r'\d{2,}'
texto = "1 12 123 1234"
resultado = re.findall(pattern, texto)
print("9. Cuantificador {n,}")
print("Explicación: '\\d{2,}' busca grupos de al menos 2 dígitos consecutivos.")
print("Texto:", texto)
print("Regex:", pattern)
print("Resultado:", resultado, "\n")
```
# 10. Busca grupos de 2 a 3 dígitos.
```python
pattern = r'\d{2,3}'
```
#### Busca grupos de dígitos donde la cantidad esté en el rango de 2 a 3.
```python
texto = "1 12 123 1234"
resultado = re.findall(pattern, texto)
print("10. Cuantificador {n,m}")
print("Explicación: '\\d{2,3}' busca grupos de dígitos donde la cantidad esté en el rango de 2 a 3.")
print("Texto:", texto)
print("Regex:", pattern)
print("Resultado:", resultado, "\n")
```

# ️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️
# ___GRUPOS Y CLASES DE CARACTERES___

# 1. Los corchetes [] se usan para definir clases de caracteres.
```python
pattern = r'[aeiou]'
```
#### Busca cualquier vocal minúscula.
```python
pattern = r'[aeiou]'
texto = "Python"
resultado = re.findall(pattern, texto)
print("11. Clase de caracteres [aeiou]")
print("Explicación: '[aeiou]' busca cualquier carácter que sea una vocal (a, e, i, o, u).")
print("Texto:", texto)
print("Regex:", pattern)
print("Resultado:", resultado, "\n")
```
# 2. El símbolo ^ dentro de corchetes niega la clase, es decir, encuentra todo lo que no esté incluido.
```python
pattern = r'[^aeiou]'
```
#### Busca cualquier carácter que no sea vocal.
```python
resultado = re.findall(pattern, texto)
print("12. Negación en clase de caracteres [^...]")
print("Explicación: '[^aeiou]' devuelve todos los caracteres que no son vocales.")
print("Texto:", texto)
print("Regex:", pattern)
print("Resultado:", resultado, "\n")
```
# 3. Rango de caracteres. Por ejemplo, [a-z] captura letras minúsculas.
```python
pattern = r'[a-z]'
```
#### Busca cualquier letra minúscula del abecedario (de la a a la z).
```python
pattern = r'[a-z]'
texto = "Python3"
resultado = re.findall(pattern, texto)
print("13. Rango de caracteres [a-z]")
print("Explicación: '[a-z]' busca cualquier letra minúscula del abecedario (de la a a la z).")
print("Texto:", texto)
print("Regex:", pattern)
print("Resultado:", resultado, "\n")
```
# 4. Alternancia con | (OR).

```python
pattern = r'apple|banana'
```
#### Actúa como OR. Busca 'apple' o 'banana' en el texto."
```python
pattern = r'apple|banana'
texto = "I like apple and banana"
resultado = re.findall(pattern, texto)
print("14. Alternancia (|)")
print("Explicación: '|' actúa como OR. Busca 'apple' o 'banana' en el texto.")
print("Texto:", texto)
print("Regex:", pattern)
print("Resultado:", resultado, "\n")
```
# 5. Agrupación con paréntesis () para capturar grupos.
```python
pattern = r'(ab)+'
```
#### Agrupa la subcadena 'ab' y busca que se repita una o más veces.
```python
texto = "abababx"
resultado = re.search(pattern, texto)
print("15. Grupo de captura ()")
print("Explicación: '(ab)+' agrupa la subcadena 'ab' y busca que se repita una o más veces.")
if resultado:
    print("Texto:", texto)
    print("Regex:", pattern)
    print("Resultado:", resultado.group(), "\n")
```
# 6. Grupo sin captura (?:...), se usa cuando no se necesita almacenar el grupo.
```python
pattern = r'(?:ab)+'
```
Agrupa 'ab' sin capturarlo aparte; se devuelve la coincidencia completa
```python
pattern = r'(?:ab)+'
resultado = re.findall(pattern, texto)
print("16. Grupo sin captura (?:...)")
print("Explicación: '(?:ab)+' agrupa 'ab' sin capturarlo aparte; se devuelve la coincidencia completa.")
print("Texto:", texto)
print("Regex:", pattern)
print("Resultado:", resultado, "\n")
```

# ️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️
# ___BÚSQUEDA Y REEMPLAZO___
# 1. Usando re.sub() para reemplazar patrones:
```python
pattern = r'\d{4}-\d{2}-\d{2}'
```
#### Busca una fecha con el formato YYYY-MM-DD.
```python
texto = "La fecha es 2025-06-01."
nuevo_texto = re.sub(pattern, 'FECHA', texto)
print("17. Reemplazo con re.sub()")
print("Explicación: Se reemplaza el patrón de fecha (YYYY-MM-DD) por la cadena 'FECHA'.")
print("Texto original:", texto)
print("Regex:", pattern)
print("Texto modificado:", nuevo_texto, "\n")
```
# ️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️
# ___LOOKAHEAD y LOOKBEHIND___
# 1. Lookahead positivo (?=...) verifica que lo que sigue cumpla un patrón, sin incluirlo en la coincidencia.

```python
pattern = r'foo(?=bar)'
```
#### Busca 'foo' solo si va seguido directamente por 'bar'.
```python
pattern = r'foo(?=bar)'
texto = "foobar fooqux"
resultado = re.findall(pattern, texto)
print("18. Lookahead positivo (?=...)")
print("Explicación: 'foo(?=bar)' busca 'foo' solo si va seguido directamente por 'bar'.")
print("Texto:", texto)
print("Regex:", pattern)
print("Resultado:", resultado, "\n")
```
# 2. Lookahead negativo (?!...) verifica que lo siguiente NO cumpla un patrón.
```python
pattern = r'foo(?!bar)'
```
#### Captura 'foo' únicamente si no va seguido de 'bar'.
```python
pattern = r'foo(?!bar)'
resultado = re.findall(pattern, texto)
print("19. Lookahead negativo (?!...)")
print("Explicación: 'foo(?!bar)' captura 'foo' únicamente si no va seguido de 'bar'.")
print("Texto:", texto)
print("Regex:", pattern)
print("Resultado:", resultado, "\n")
```
# 3. Lookbehind positivo (?<=...) busca un patrón solo si está precedido por otro.
```python
pattern = r'(?<=\$)\d+'
```
#### Busca secuencias de dígitos que aparezcan justo después del signo '$'.
```python
pattern = r'(?<=\$)\d+'
texto = "$100 and $200"
resultado = re.findall(pattern, texto)
print("20. Lookbehind positivo (?<=...)")
print("Explicación: '(?<=\\$)\\d+' busca secuencias de dígitos que aparezcan justo después del signo '$'.")
print("Texto:", texto)
print("Regex:", pattern)
print("Resultado:", resultado, "\n")
```
# 4. Lookbehind negativo (?<!...) busca un patrón solo si NO está precedido por otro.
```python
pattern = r'(?<!\$)\d+'
```
#### Busca dígitos que no estén inmediatamente precedidos por '$'.
```python
pattern = r'(?<!\$)\d+'
texto = "$100 and 300"
resultado = re.findall(pattern, texto)
print("21. Lookbehind negativo (?<!...)")
print("Explicación: '(?<!\\$)\\d+' busca dígitos que no estén inmediatamente precedidos por '$'.")
print("Texto:", texto)
print("Regex:", pattern)
print("Resultado:", resultado, "\n")
```


# ️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️
# ___FLAGS o MODIFICADORES___
# 1.
# re.IGNORECASE o re.I: Ignora mayúsculas/minúsculas.
# re.MULTILINE o re.M: Hace que ^ y $ actúen al inicio y fin de cada línea.

```python
pattern = r'^hola'
```
#### Con re.IGNORECASE no se distingue entre mayúsculas y minúsculas y con re.MULTILINE se aplica el patrón a cada línea."
```python

texto = "Hola\nhola"
pattern = r'^hola'
resultado = re.findall(pattern, texto, flags=re.IGNORECASE | re.MULTILINE)
print("22. Uso de FLAGS (re.IGNORECASE y re.MULTILINE)")
print("Explicación: Con re.IGNORECASE no se distingue entre mayúsculas y minúsculas y con re.MULTILINE se aplica el patrón a cada línea.")
print("Texto:\n", texto)
print("Regex:", pattern)
print("Resultado:", resultado, "\n")
```

```python


```
# ️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️
# ___EJEMPLOS COMBINADOS___
# 1. Coincidir líneas que NO empiecen con "1000"

```python
pattern = r'^(?!1000).*'
```
#### '^(?!1000)' utiliza lookahead negativo para excluir líneas cuyo inicio sea "1000".

```python
texto = """Line1
1000-Error
2000-Success
1000Start"""
resultado = re.findall(pattern, texto, flags=re.MULTILINE)
print("23. Líneas que no empiecen con '1000'")
print("Explicación: '^(?!1000).*' captura las líneas que no inician con '1000'.\n" +
      "^(?!1000): Del inicio, asegura que no venga '1000'.\n" +
      ".*: Luego captura cualquier carácter hasta el final.")
print("Texto completo:\n", texto)
print("Regex:", pattern)
print("Resultado:", resultado, "\n")
```
# 2. Validación de un correo electrónico

```python
pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
```
#### El patrón valida la estructura general de un correo electrónico.
correo = "ejemplo@dominio.com"

```python
pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
# La estructura es:
#   - ^[a-zA-Z0-9._%+-]+ : Inicio y uno o más caracteres válidos para el usuario.
#   - @                : El símbolo de arroba.
#   - [a-zA-Z0-9.-]+   : Dominio con letras, números, puntos y guiones.
#   - \.[a-zA-Z]{2,}$  : Un punto y al menos 2 letras para la extensión.
resultado = re.match(pattern, correo)
print("24. Validación de correo electrónico")
print("Explicación: El patrón valida la estructura general de un correo electrónico.")
if resultado:
    print("Correo:", correo)
    print("Regex:", pattern)
    print("Resultado: El correo es válido\n")
else:
    print("Correo inválido\n")
```

# 3. Extracción de fechas en formato 'YYYY-MM-DD'

```python
pattern = r'\b\d{4}-\d{2}-\d{2}\b'
```
#### \b indica límite de palabra y se asegura que se capture la fecha completa.
```python
texto = "Fechas: 2025-06-01, 1999-12-31."
pattern = r'\b\d{4}-\d{2}-\d{2}\b'
# \b indica límite de palabra y se asegura que se capture la fecha completa.
resultado = re.findall(pattern, texto)
print("25. Extracción de fechas")
print("Explicación: '\\b\\d{4}-\\d{2}-\\d{2}\\b' busca fechas con formato 'YYYY-MM-DD'.")
print("Texto:", texto)
print("Regex:", pattern)
print("Resultado:", resultado, "\n")
```
# 4. Extracción de números (enteros y decimales, pudiendo ser negativos o positivos)
```python
pattern = r'[-+]?\d+\.?\d*'
```
#### Captura números enteros o decimales, con signo opcional

```python
texto = "Valores: 3, 3.14, -2, -2.718"
pattern = r'[-+]?\d+\.?\d*'
# Desglose:
#   [-+]?    : Signo opcional (negativo o positivo).
#   \d+      : Uno o más dígitos.
#   \.?      : Punto decimal opcional.
#   \d*      : Cero o más dígitos decimales.
resultado = re.findall(pattern, texto)
print("26. Extracción de números")
print("Explicación: '[-+]?\\d+\\.?\\d*' captura números enteros o decimales, con signo opcional.")
print("Texto:", texto)
print("Regex:", pattern)
print("Resultado:", resultado, "\n")
```



```python


```

# ️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️
# ___EXPRESIONES REGULARES EN ANÁLISIS DE DATOS___

```python
pattern = r'\b\d{5}(?:-\d{4})?\b'
```
#### A) Busca el formato de códigos postales, con o sin extensión

```python
print("27. Ejemplos comunes en análisis de datos:")

# a) Extracción de Códigos Postales (US ZIP Codes)
pattern = r'\b\d{5}(?:-\d{4})?\b'
# Desglose:
#   \d{5}         : Cinco dígitos.
#   (?:-\d{4})?   : Opcionalmente, un guión seguido de cuatro dígitos (grupo sin captura).
texto = "Código postal: 12345 y extendido 12345-6789"
resultado = re.findall(pattern, texto)
print("\na. Código Postal (US ZIP Codes)")
print("Explicación: '\\b\\d{5}(?:-\\d{4})?\\b' busca el formato de códigos postales, con o sin extensión.")
print("Texto:", texto)
print("Regex:", pattern)
print("Resultado:", resultado)
```

# b) Detección de URLs
```python
pattern = r'https?://(?:www\.)?\S+'
```
```python
pattern = r'https?://(?:www\.)?\S+'
# Desglose:
#   https?://      : 'http://' o 'https://'
#   (?:www\.)?     : Opcionalmente 'www.' (sin captura).
#   \S+            : Uno o más caracteres que no sean espacio.
texto = "Visita https://example.com o http://www.example.org para más información."
resultado = re.findall(pattern, texto)
print("\nb. Detección de URLs")
print("Explicación: 'https?://(?:www\\.)?\\S+' capta URLs independientemente del uso de 'www' y del protocolo (http o https).")
print("Texto:", texto)
print("Regex:", pattern)
print("Resultado:", resultado)
```
# c) Validación de correos electrónicos (ejemplo repetido, muy común en análisis)

```python
pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
```

```python
pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
correo = "usuario@dominio.com"
resultado = re.match(pattern, correo)
print("\nc. Validación de correo electrónico")
if resultado:
    print("Correo:", correo)
    print("Regex:", pattern)
    print("Resultado: El correo es válido")
else:
    print("Correo inválido")
```

# d) Limpieza de múltiples espacios en un texto
```python
pattern = r'\s+'
```
```python
texto = "  datos   con  muchos   espacios "
pattern = r'\s+'
texto_limpio = re.sub(pattern, ' ', texto).strip()
print("\nd. Limpieza de espacios")
print("Explicación: '\\s+' captura secuencias de espacios, tabs o saltos de línea. re.sub reemplaza múltiples espacios por uno solo, y strip() elimina espacios al inicio y final.")
print("Texto original:", repr(texto))
print("Regex:", pattern)
print("Texto limpio:", repr(texto_limpio), "\n")
```
   
   
   
