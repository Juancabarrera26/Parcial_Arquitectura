# Parcial_Arquitectura

# Instrucciones para compilar y ejecutar programa

copia y pega

Código para la implementación de la ALU (alu.py)
Código de la ALU:

python
Copy
Edit
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

# Generar arreglo de 1,000,000 de pares aleatorios de enteros de 32 bits
num_operations = 1000000
operations = ["ADD", "SUB", "AND", "OR", "XOR", "NOT", "SHL", "SHR"]
pairs = [(random.randint(0, 2**32 - 1), random.randint(0, 2**32 - 1)) for _ in range(num_operations)]

# Medir tiempo de ejecución de las operaciones
start_time = time.time()

# Ejecutar todas las operaciones
for a, b in pairs:
    for op in operations:
        alu(op, a, b)

end_time = time.time()

# Imprimir tiempo total de ejecución
execution_time = end_time - start_time
print(f"Tiempo total de ejecución para 1,000,000 de operaciones: {execution_time} segundos.")
Este código define la función alu que recibe un código de operación (op_code) y dos operandos (a, b), y realiza las operaciones de la ALU como suma, resta, operaciones bitwise, y desplazamientos lógicos.

Paso 3: Medición de los tiempos
Código para medir el tiempo de ejecución:

El código anterior ya incluye el cálculo del tiempo de ejecución con la función time.time(). No es necesario escribir código adicional para medir el tiempo, ya que está integrado en la ejecución de las operaciones.

Paso 4: Análisis ILP (Simulación de Pipeline)
Código para el análisis ILP (simulación de un pipeline de 4 etapas):

python
Copy
Edit
# Simular un pipeline de 4 etapas (Fetch, Decode, Execute, Write-back)
def simulate_pipeline(operations):
    num_stages = 4  # Fetch, Decode, Execute, Write-back
    cycle_time = 1  # Latencia unitaria

    # Suponiendo que no haya conflictos, el pipeline ideal tiene CPI = 1
    instructions_per_second = len(operations) / (cycle_time * num_stages)

    # Medir el tiempo real en el pipeline simulado
    return instructions_per_second

# Simular el pipeline sobre las operaciones
instructions_per_second = simulate_pipeline(pairs)
print(f"Instrucciones por segundo (con pipeline ideal): {instructions_per_second}")
Este código simula un pipeline de 4 etapas y calcula el throughput en un escenario ideal (sin latencia o conflictos).

Paso 5: Comparación de los resultados
El script anterior compara el rendimiento teórico del pipeline ideal con el tiempo real calculado por el código. Aquí se muestra el tiempo total de ejecución y el throughput para el análisis ILP.

Paso 6: Ejecutar el código
Para ejecutar el código:

Copia y pega el código de cada paso en celdas separadas en tu cuaderno de Google Colab.

Ejecuta las celdas y observa los resultados en la consola.

3. Consideraciones:
Tiempo de ejecución: Debido a que se están ejecutando 1,000,000 de operaciones, el tiempo de ejecución puede variar dependiendo de la capacidad de tu máquina.

Análisis ILP: La simulación del pipeline se basa en un modelo simplificado con latencias unitarias. El throughput teórico es 1 instrucción por ciclo en el pipeline ideal.
