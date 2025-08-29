Yeimy Estefania Beltran Sandoval
#                                                                   RNA con Wolfram

# Objetivo
Implementar perceptrones simples para simular el funcionamiento de las compuertas lógicas AND, OR y XOR, utilizando una función de activación escalón.+

# ¿Qué es una RNA?

Una Red Neuronal Artificial (RNA) es un modelo computacional inspirado en el funcionamiento del cerebro humano. Está formada por neuronas artificiales (como nuestros perceptrones) organizadas en capas:

- Capa de entrada → recibe los datos.

- Capas ocultas → procesan la información combinando perceptrones.

- Capa de salida → entrega el resultado.

En este proyecto:

Cada perceptrón simula una neurona.

Para XOR, usamos más de una capa, lo que es el principio básico de una RNA multicapa.

# Como funciona el codigo 
El código implementa perceptrones para simular compuertas lógicas. Cada perceptrón recibe dos entradas binarias (0 o 1) y, en función de los pesos y el sesgo definidos, determina si la salida es 0 o 1.

1. Función de activación
   stepFunction[x_] := If[x > 0, 1, 0]
   Es la función escalón:

    - Si la suma ponderada es mayor que 0, devuelve 1.

    - Si es menor o igual que 0, devuelve 0.
  
2. Perceptrón AND
   perceptronAND[input1_, input2_] := Module[
    {weights, bias, weightedSum},
    weights = {1, 1};
    bias = -1.5;
    weightedSum = weights.{input1, input2} + bias;
    stepFunction[weightedSum]
   ]

   - Pesos: {1, 1} → cada entrada suma 1.
   - Sesgo: -1.5 → obliga a que ambas entradas sean 1 para activar la salida.

3. Perceptrón OR
   perceptronOR[input1_, input2_] := Module[
    {weights, bias, weightedSum},
    weights = {1, 1};
    bias = -0.5;
    weightedSum = weights.{input1, input2} + bias;
    stepFunction[weightedSum]
   ]

  - Pesos: {1, 1} → igual que en AND.
  - Sesgo: -0.5 → permite que basta con una entrada en 1 para que la salida sea 1.
    
4. Perceptrón XOR
   perceptronXOR[input1_, input2_] := Module[
    {nandOutput, orOutput, finalOutput},
    nandOutput = 1 - perceptronAND[input1, input2];
    orOutput = perceptronOR[input1, input2];
    finalOutput = perceptronAND[nandOutput, orOutput];
    finalOutput
  ]    

 - XOR no puede resolverse con un único perceptrón, así que se usa una combinación:

    - Calcula NAND = NOT(AND).
    - Calcula OR.
    - Hace AND entre ambos resultados:
      XOR=(A  OR  B)  AND  ¬(A  AND  B)

# Resultados esperados 

Para todas las combinaciones de entradas:

| Entrada A | Entrada B | AND | OR | XOR |
| --------- | --------- | --- | -- | --- |
| 0         | 0         | 0   | 0  | 0   |
| 0         | 1         | 0   | 1  | 1   |
| 1         | 0         | 0   | 1  | 1   |
| 1         | 1         | 1   | 1  | 0   |

# Conclusiones

- Un perceptrón simula el comportamiento de compuertas lógicas básicas como AND y OR ajustando pesos y sesgos.
- La compuerta XOR no puede resolverse con un único perceptrón; se requiere más de una capa.
- Esto demuestra que las Redes Neuronales Artificiales (RNAs) pueden resolver problemas complejos combinando perceptrones simples.
- Comprender estos ejemplos básicos es esencial para entender cómo las RNAs modernas aprenden patrones más complicados.
