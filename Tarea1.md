# Instrucciones para ejecutar el proyecto de la Tarea 1
Este archivo contiene las instrucciones necesarias para compilar y ejecutar el código de la Tarea 1, que consiste en la implementación de la ALU y el análisis de ILP.

1. Requisitos
Python 3.x (Se recomienda usar Python 3.7 o superior)

Bibliotecas necesarias: time, random (estas son bibliotecas estándar de Python)

2. Estructura del Proyecto
El proyecto contiene los siguientes archivos:

alu.py: Implementación de la ALU y la ejecución de operaciones.

README.txt: Este archivo con las instrucciones para ejecutar el código.

3. Instrucciones para ejecutar el código
Paso 1: Descargar o clonar el repositorio
Puedes clonar el repositorio en tu máquina local utilizando el siguiente comando:

bash
git clone https://github.com/tu-usuario/nombre-del-repositorio.git
O simplemente descarga el archivo ZIP desde el repositorio de GitHub.

Paso 2: Preparar el entorno
Si no tienes Python instalado, descarga e instala Python desde python.org.

Abre una terminal o línea de comandos.

Paso 3: Ejecutar el código
Navega hasta la carpeta donde descargaste el repositorio:

bash
cd ruta/a/tu/repositorio
Ejecuta el archivo alu.py con el siguiente comando:

bash
Copy
Edit
python alu.py
4. Código de la ALU (alu.py)
El archivo alu.py contiene el código necesario para ejecutar las operaciones de la ALU. Aquí está el código:

```python
import time
import random

# Función para ejecutar operaciones de la ALU
def alu(op_code, a, b):
    if op_code == "ADD":
        return a + b
    elif op_code == "SUB":
        return a - b
    elif op_code == "AND":
        return a & b
    elif op_code == "OR":
        return a | b
    elif op_code == "XOR":
        return a ^ b
    elif op_code == "NOT":
        return ~a
    elif op_code == "SHL":
        return a << 1
    elif op_code == "SHR":
        return a >> 1
    else:
        return None
```
# Generar arreglo de 1,000,000 de pares aleatorios de enteros de 32 bits
```num_operations = 1000000
operations = ["ADD", "SUB", "AND", "OR", "XOR", "NOT", "SHL", "SHR"]
pairs = [(random.randint(0, 2**32 - 1), random.randint(0, 2**32 - 1)) for _ in range(num_operations)]
```
# Medir tiempo de ejecución de las operaciones
```
start_time = time.time()
```
# Ejecutar todas las operaciones
```for a, b in pairs:
    for op in operations:
        alu(op, a, b)

end_time = time.time()
```
# Imprimir tiempo total de ejecución
```execution_time = end_time - start_time
print(f"Tiempo total de ejecución para 1,000,000 de operaciones: {execution_time} segundos.")
```
Paso 4: Medición de los tiempos
El código anterior incluye el cálculo del tiempo de ejecución con la función time.time(). Cuando ejecutes el código, verás el tiempo total de ejecución de las operaciones en la terminal.

5. Análisis ILP (Simulación de Pipeline)
El análisis ILP simula un pipeline de 4 etapas (Fetch, Decode, Execute, Write-back) y calcula el throughput en un escenario ideal (sin latencia o conflictos).

Código para el análisis ILP:

python
Copy
Edit
# Simular un pipeline de 4 etapas (Fetch, Decode, Execute, Write-back)
```
def simulate_pipeline(operations):
    num_stages = 4  # Fetch, Decode, Execute, Write-back
    cycle_time = 1  # Latencia unitaria

    # Suponiendo que no haya conflictos, el pipeline ideal tiene CPI = 1
    instructions_per_second = len(operations) / (cycle_time * num_stages)

    # Medir el tiempo real en el pipeline simulado
    return instructions_per_second
```
# Simular el pipeline sobre las operaciones
```python
import random
import time
from alu import alu  # Importar las funciones del archivo alu.py

NUM_PARES = 1_000_000
datos = [(random.randint(0, 2**31 - 1), random.randint(0, 2**31 - 1)) for _ in range(NUM_PARES)]

# Medir tiempo real de ejecución por operación
resultados = {}
print("Ejecutando operaciones...")

for op in ["ADD", "SUB", "AND", "OR", "XOR", "NOT", "SHL", "SHR"]:
    inicio = time.time()
    for a, b in datos:
        if op in ["NOT", "SHL", "SHR"]:
            alu(op, a)
        else:
            alu(op, a, b)
    fin = time.time()
    duracion = fin - inicio
    resultados[op] = duracion
    print(f"{op}: {duracion:.4f} segundos")

# Simulación del pipeline (teórico)
num_instrucciones = NUM_PARES * len(resultados)  

clock_ns = 1e-9
tiempo_sin_pipeline = num_instrucciones * 4 * clock_ns
tiempo_con_pipeline = (NUM_PARES + 3) * len(resultados) * clock_ns

print("Simulación de Pipeline:")
print(f"Tiempo sin pipeline (CPI=4): {tiempo_sin_pipeline:.6f} s")
print(f"Tiempo con pipeline ideal (CPI=1): {tiempo_con_pipeline:.6f} s")

# Comparación con tiempos reales
total_tiempo_real = sum(resultados.values())
throughput_real = num_instrucciones / total_tiempo_real

print(f"Tiempo total real (Python): {total_tiempo_real:.4f} s")
print(f"Throughput real: {throughput_real:.2f} instrucciones/segundo")
```
Este código simula el pipeline de 4 etapas y calcula el rendimiento teórico. Al ejecutarlo, verás en la terminal las instrucciones por segundo en un pipeline ideal.

6. Consideraciones
Tiempo de ejecución: Debido a que se están ejecutando 1,000,000 de operaciones, el tiempo de ejecución puede variar dependiendo de la capacidad de tu máquina.

Análisis ILP: La simulación del pipeline se basa en un modelo simplificado con latencias unitarias. El throughput teórico es 1 instrucción por ciclo en el pipeline ideal.

7. Resultados Esperados
Al ejecutar el código, se imprimirá el tiempo total de ejecución de las 1,000,000 de operaciones y el throughput calculado para el pipeline ideal.
