# Lista 1 - Resoluções

## Questão 01

```python
#Calcula o valor da n-derivada do seno em um certo ponto
import numpy as np

n = int(input()) #número de derivadas
arg_x = int(input()) #argumento do seno

arg_x1 = arg_x * (np.pi/180) #converte o seno de graus para rad

if n % 4 == 0 :
    print(np.sin(arg_x1))
elif n % 4 == 1 :
    print(np.cos(arg_x1))
elif n % 4 == 2 :
    print((-1) * np.sin(arg_x1))
elif n % 4 == 3 :
    print((-1) * np.cos(arg_x1))
 ```   

## Questão 02
 ```python
#Receber 3 números e colocar no vetor

#podia fazer com for
x1 = float(input())
x2 = float(input())
x3 = float(input())
 
vec = [x1, x2, x3]
 
print(vec) #imprime vetor
 ```
## Questão 03
 ```python
 #Objetivo: ordenar 5 números em um vetor
vec = []

#recebe 5 números inteiros
for i in range(0,5):
  x1 = float(input())
  vec.append(x1) #recebe os números e coloca no vetor
  
#Algoritmo Bubble Sort
for i in range (0, 5):
  for j in range(4,i, -1):
    if vec[j-1] > vec[j]:
      aux = vec[j-1]
      vec[j-1] = vec[j]
      vec[j] = aux

#imprime o vetor
print(vec)

#captura a mediana
mediana = vec[2]

#imprime a mediana
print(mediana)
```

## Questão 04
```python
#Objetivo: calcula o valor da n-derivada do seno em um certo ponto
import numpy as np

n = int(input()) #número de derivadas
t0 = float(input()) #argumento do seno

if n % 4 == 0 :
    print(np.sin(t0))
elif n % 4 == 1 :
    print(np.cos(t0))
elif n % 4 == 2 :
    print((-1) * np.sin(t0))
elif n % 4 == 3 :
    print((-1) * np.cos(t0))
```
## Questão 05
```python
#Objetivo: calcula o fatorial de um número
n = int(input())

aux = 1

for i in range(n, 0, -1) :
  aux = i*aux
    
print(aux)
```

## Questão 06
```python
#Objetivo: calcular a n-derivada de f(t) = cos(w0*t)
import math as mt

n = int(input())
w0 = float(input())
t0 = float(input())

if n % 4 == 0 :
    print(mt.pow(w0,n) * mt.cos(w0 * t0)) #cos
elif n % 4 == 1 :
    print(mt.pow(w0,n) * (-1) * mt.sin(w0 * t0)) #-sen
elif n % 4 == 2 :
    print(mt.pow(w0,n) * (-1) * mt.cos(w0 * t0))#-cos
elif n % 4 == 3 :
    print(mt.pow(w0,n) * mt.sin(w0 * t0))#sen

print(0**0)
```

## Questão 07
```python
#Objetivo: Calcular série de Taylor da função f(x) = e^x
import numpy as np
import math as mt

x0 = int(input())
x = int(input())
n = int(input())

soma_e = 0 #Define o valor inicial da soma como 0

#Calcula a série de Taylor
for i in range (0, n) :
  soma_e += (mt.pow(np.e, x0) * mt.pow((x-x0), n)) / mt.factorial(i)

print(soma_e)
```

## Questão 08 
```python
#Objetivo: Calcular aproximação de Taylor da função f(x) = sen(x)

import numpy as np
import math as mt

x0 = float(input())
x = float(input())
n = int(input())

soma_sen = 0 #Define o valor inicial da soma como 0

#Calcula a série de Taylor
for i in range (0, n) :
  if i % 4 == 0 :
    soma_sen += np.sin(x0) * (mt.pow(x-x0, i) / mt.factorial(i))
  elif i % 4 == 1 :
    soma_sen += np.cos(x0) * (mt.pow(x-x0, i) / mt.factorial(i))
  elif i % 4 == 2 :
    soma_sen += (-1) * np.sin(x0) * (mt.pow(x-x0, i) / mt.factorial(i))
  elif i % 4 == 3 :
    soma_sen += (-1) * np.cos(x0) * (mt.pow(x-x0, i) / mt.factorial(i))

print(soma_sen)
```

## Questão 09
```python
#Objetivo: calcular aproximação de Taylor da função f(t) = a0 + a1 * cos(w0*t) + a2 * sen(w0*t)

import math as mt

#Definindo os valores das constantes do programa:
a = [528.6837, -5.58392, -196.69973]
w0 = 5.3748377

#Entrada de dados
t0 = float(input())
t = float(input())
n = int(input())

tay_f = a[0] #Define a soma como 0

for i in range(0, n) :
  if i % 4 == 0 :
    tay_f += (mt.pow(w0,i) * (a[1] * mt.cos(w0*t0) + a[2] * mt.sin(w0*t0))) * mt.pow(t - t0, i) / mt.factorial(i)
  elif i % 4 == 1 :
    tay_f += (mt.pow(w0,i) * (a[1] * (-1) * mt.sin(w0*t0) + a[2] * mt.cos(w0*t0))) * mt.pow(t - t0, i) / mt.factorial(i)
  elif i % 4 == 2 :
    tay_f += (mt.pow(w0,i) * (a[1] * (-1) * mt.cos(w0*t0) + a[2] * (-1) * mt.sin(w0*t0))) * mt.pow(t - t0, i) / mt.factorial(i)
  elif i % 4 == 3 : #podia ser um else
    tay_f += (mt.pow(w0,i) * (a[1] * mt.sin(w0*t0) + a[2] * (-1) * mt.cos(w0*t0))) * mt.pow(t - t0, i) / mt.factorial(i)

print(tay_f)
```