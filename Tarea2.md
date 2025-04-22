# Simulación de LMC

## Descripción 
Este proyecto simula el funcionamiento de un procesador simplificado utilizando el concepto de LMC (Little Man Computer). El programa simula la suma de los primeros 10 números naturales y muestra el resultado utilizando un conjunto de instrucciones básico.

## Requisitos
Para ejecutar este proyecto, necesitas tener Python instalado en tu computadora. Si no tienes Python instalado, puedes descargarlo desde [aquí](https://www.python.org/downloads/).

### Requisitos de Python:
- Python 3.x o superior

## Archivos del Proyecto
El proyecto contiene los siguientes archivos:
- `lmc_simulation.py` - Código fuente de la simulación de LMC.

## Código fuente

```python
def run_lmc(memory, verbose=True):
    ACC = 0
    PC = 0
    halted = False
    steps = 0
    while not halted and PC < 100:
        instr = memory[PC]
        opcode = instr // 100
        address = instr % 100
        if verbose:
            print(f"[{steps:03}] PC={PC:02} ACC={ACC:>5} Instr={instr:03} ({opcode},{address:02})")
        # Decodificación y ejecución
        if opcode == 1:      # ADD
            ACC = (ACC + memory[address]) % 1000
            PC += 1
        elif opcode == 2:    # SUB
            ACC = (ACC - memory[address]) % 1000
            PC += 1
        elif opcode == 3:    # STA
            memory[address] = ACC
            PC += 1
        elif opcode == 5:    # LDA
            ACC = memory[address]
            PC += 1
        elif opcode == 6:    # BRA
            PC = address
        elif opcode == 7:    # BRZ
            if ACC == 0:
                PC = address
            else:
                PC += 1
        elif instr == 902:   # OUT
            print(f"OUT: {ACC}")
            PC += 1
        elif instr == 0 or instr == 999:  # HLT
            halted = True
        else:
            print(f"Instr desconocida ({instr}) en PC={PC}. STOP.")
            halted = True
        steps += 1
    return memory, ACC

if __name__ == "__main__":
    # Prepara la memoria LMC (100 posiciones)
    mem = [0]*100
    # El programa suma mem[20]...mem[29] y pone el resultado en mem[30], luego lo muestra con OUT
    mem[0] = 520   # LDA 20
    mem[1] = 121   # ADD 21
    mem[2] = 122   # ADD 22
    mem[3] = 123   # ADD 23
    mem[4] = 124   # ADD 24
    mem[5] = 125   # ADD 25
    mem[6] = 126   # ADD 26
    mem[7] = 127   # ADD 27
    mem[8] = 128   # ADD 28
    mem[9] = 129   # ADD 29
    mem[10] = 330  # STA 30 (guarda suma en memoria 30)
    mem[11] = 530  # LDA 30
    mem[12] = 902  # OUT
    mem[13] = 0    # HLT

    # Números 1–10 en posiciones 20–29
    for i in range(10):
        mem[20+i] = i+1

    print("Ejecutando suma de los primeros 10 números naturales (mem[20]...mem[29]):")
    run_lmc(mem)
Instrucciones para Ejecutar el Proyecto
Paso 1: Preparación
Asegúrate de tener Python instalado. Si no lo tienes, instálalo desde el sitio oficial. Luego, asegúrate de tener el archivo lmc_simulation.py en tu directorio de trabajo.

Paso 2: Ejecutar el Código
Para ejecutar el programa, sigue estos pasos:

Abre una terminal o línea de comandos.

Navega hasta el directorio donde tienes el archivo lmc_simulation.py.

Escribe el siguiente comando para ejecutar el archivo:

nginx
Copy
Edit
python lmc_simulation.py
Paso 3: Ver Resultados
Al ejecutar el código, verás una serie de instrucciones y el resultado final de la suma de los primeros 10 números naturales. El resultado será mostrado con la instrucción OUT al final de la ejecución.

Ejemplo de Ejecución
csharp
Copy
Edit
Ejecutando suma de los primeros 10 números naturales (mem[20]...mem[29]):
[000] PC=00 ACC=    0 Instr=520 (5,20)
[001] PC=01 ACC=    1 Instr=121 (1,21)
[002] PC=02 ACC=    3 Instr=122 (1,22)
[003] PC=03 ACC=    6 Instr=123 (1,23)
[004] PC=04 ACC=   10 Instr=124 (1,24)
[005] PC=05 ACC=   15 Instr=125 (1,25)
[006] PC=06 ACC=   21 Instr=126 (1,26)
[007] PC=07 ACC=   28 Instr=127 (1,27)
[008] PC=08 ACC=   36 Instr=128 (1,28)
[009] PC=09 ACC=   45 Instr=129 (1,29)
[010] PC=10 ACC=   55 Instr=330 (3,30)
[011] PC=11 ACC=   55 Instr=530 (5,30)
OUT: 55
```

# Explicación del Programa
Cargar los números del 1 al 10: Los primeros 10 números naturales son almacenados en la memoria LMC de las posiciones 20 a 29.

Suma secuencial: Se utilizan instrucciones ADD para sumar los valores de la memoria, empezando desde mem[20] hasta mem[29].

Mostrar el resultado: El resultado de la suma se almacena en mem[30] y se imprime con la instrucción OUT.

Finalización: El programa se detiene con la instrucción HLT cuando todas las operaciones se han completado.

# Conclusiones
Este proyecto proporciona una representación simplificada de cómo un procesador podría realizar operaciones aritméticas y mostrar el resultado utilizando un conjunto de instrucciones muy básico. La implementación en LMC ayuda a entender los conceptos básicos de arquitectura de computadoras y ejecución de instrucciones.

r
Copy
Edit

