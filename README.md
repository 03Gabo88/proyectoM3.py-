# proyectoM3.py-
Construccion maquina de galton
import numpy as np
import matplotlib.pyplot as plt
import random

def simular_maquina_galton(num_canicas=3000, niveles=12):
    """
    Simula el comportamiento de una máquina de Galton.
    
    Args:
        num_canicas (int): Número de canicas a simular
        niveles (int): Número de niveles de la máquina
        
    Returns:
        list: Lista con los contenedores finales de cada canica
    """
    contenedores = [0] * (niveles + 1)  # Un contenedor más que niveles
    
    for _ in range(num_canicas):
        posicion = 0  # Comienza en el centro
        
        for _ in range(niveles):
            # Decidir si cae a izquierda (-0.5) o derecha (+0.5)
            posicion += random.choice([-0.5, 0.5])
        
        # Mapear la posición final a un contenedor (0 a niveles)
        contenedor = int(round((posicion + niveles/2), 0))
        contenedores[contenedor] += 1
    
    return contenedores

def graficar_histograma(contenedores):
    """
    Grafica un histograma con los resultados de la simulación.
    
    Args:
        contenedores (list): Lista con la cantidad de canicas por contenedor
    """
    plt.figure(figsize=(10, 6))
    plt.bar(range(len(contenedores)), contenedores, color='green', edgecolor='black')
    
    plt.title('Distribución de canicas en la Máquina de Galton')
    plt.xlabel('Contenedor')
    plt.ylabel('Número de canicas')
    plt.xticks(range(len(contenedores)))
    
    plt.grid(axis='y', alpha=0.75)
    plt.show()

# Ejecutar la simulación y graficar
if __name__ == "__main__":
    resultados = simular_maquina_galton(3000, 12)
    graficar_histograma(resultados)
