# Lista 2 - Resoluções

## Questão 01
```python
#Objetivo: Calcular valor da função f(x) = x^2 + ln(x)

import math as mt

def fq2 (x) :
  return (pow(mt.e), -x) -0.2*x + 13.4))

x = float(input())

print(fq2(x))
```

## Questão 02
```python
#Objetivo: Teste de Bolzano

import math as mt

def f (x) :
  return (mt.pow(x,2) + mt.log(x))

#Extremos do intervalo
x1 = float(input())
x2 = float(input())

#Meio do intervalo
M = (x1 + x2)/2

if (f(x1) * f(M) < 0) :
  print('[A, M]')
elif (f(M) * f(x2) < 0) :
  print(']M, B]')
else:
  print('Sem raiz por Bolzano')
```

## Questão 03
```python
#Objetivo: Aplicar o método da bisseção

import math as mt
import numpy as np

def f (x) :
  return (mt.pow(x,2) + mt.log(x))

#Extremos do intervalo
A = float(input())
B = float(input())

#Precisão
P = int(input())

#Número de iterações
N = int(input())

#Contador de iterações
cont = 0

if (f(A) * f(B) < 0) : #Verifica a existência de raiz por Bolzano
  for i in range(0, N) :
    aux = A
    M = (A + B) / 2 #Faz uma iteração
    if (f(A) * f(M) < 0) :
      B = M
    else:
      A = M

    cont += 1

    erro = np.abs((M - aux) / M) #Calcular o erro relativo

    if (erro < mt.pow(10, (-1) * P)) :
      break
  print(M)
  print(cont)
else:
  print('Não é possível aplicar o método da Bisseção neste intervalo')
```

## Questão 04
```python
#Objetivo: Calcular (A - B) / (f(A) - f(B))

import math as mt

def f (x) :
  return (mt.pow(x,2) + mt.log(x))

A = float(input())
B = float(input())

res1 = (A - B) / (f(A) - f(B))
res2 = (B - A) / (f(B) - f(A)) #Igual a res1

print(res1)
print(res2)
```

## Questão 05
```python
#Objetivo: Aplicar o método da falsa-posição

import math as mt
import numpy as np

def f (x) :
  return (pow(x , 2) - 10 * mt.cos(x) - pow(mt.e, x))

#Extremos do intervalo
A = float(input())
B = float(input())

#Precisão
P = int(input())

#Número de iterações
N = int(input())

#Contador de iterações
cont = 0

if (f(A) * f(B) < 0) : #Verifica a existência de raiz por Bolzano
  for i in range(0, N) :
    M = A - f(A) * ((A - B) / (f(A) - f(B))) #Faz uma iteração
    if (f(A) * f(M) < 0) :
      aux = B
      B = M
    else:
      aux = A
      A = M

    cont += 1

    erro = np.abs((M - aux) / M) #Calcular o erro relativo

    if (erro < mt.pow(10, (-1) * P)) :
      break

  print(round(M,8)) #O round arredonda a saída pra o número de casas desejado
  print(cont)
  print(erro)
else:
  print('Não é possível aplicar o método da Falsa-Posição neste intervalo')
```

## Questão 06
```python #Objetivo: Calcular o valor da derivada em x0 da função f'(x) = 2x + 1/x

x0 = float(input())

res = 2*x0 + 1 / x0 #Considerando x0 != 0

print(res)
```

## Questão 07
```python
#Objetivo: Calcular aproximação da função f(x) = x^2 + ln(x) usando o método de Newton

import math as mt

def f (x) :
  return (pow(x , 2) - mt.sqrt(pow(x , 3)) - 9) 

def fd (x) : #Função derivada
  return (2 * x - (3 / 2) * mt.sqrt(x))

x0 = float(input()) #Estimativa inicial
P = int(input()) #Precisão
N = int(input()) #Num máximo de iterações
cont = 0 #Contador

for i in range (0, N) :
  aux = x0
  x1 = x0 - (f(x0)/fd(x0))
  x0 = x1

  #Erro relativo
  erro = abs((x1 - aux) / x1)

  cont += 1

  if (erro < mt.pow(10, (-1) * P)) :
    break

print(x1)
print(cont)
```

## Questão 08
```python
#Objetivo: Aplicar o método da secante

import math as mt

def f (x) :
  return (mt.pow(x, 2) + mt.log(x))

#Extremos do intervalo
x1 = float(input())
x0 = float(input())

#Precisão
P = int(input())

#Número de iterações
N = int(input())

#Contador de iterações
cont = 0

erro = 1
x2 = x1
x1 = x0 
while cont < N and erro >= mt.pow(10, (-1) * P) : 
  x0 = x1
  x1 = x2
  x2 = x1 - f(x1) * (x1 - x0) / (f(x1) - f(x0)) #Faz uma iteração   
 
  erro = abs((x2 - x1) / x2) #Calcular o erro relativo
  
  cont += 1

print(x2) 
print(cont)
```

## Questão 09
```python
#Objetivo: Bolzano recursivo
#Ainda pode conter algum erro para algum caso específico
import math as mt

def f (x) :
  return (x - 2) * (mt.pow(x, 2) + mt.log(x))

def Bolz (x, y,t) :
  if (abs(x - y) < t) :
    print('Saiu por tolerância')
  else:
    if (f(x) * f(y) > 0) :
      M = (x + y) / 2 #Faz iteração se não achar raiz
      if (f(y) * f(M) > 0) :
        Bolz(x, M, t)
      elif (f(x) * f(M) > 0) :
        Bolz(M, y, t)   
      elif (f(y) * f(M) < 0) :
        print(x)
        print("%.15f" % (M))
      elif (f(x) * f(M) < 0) :
        print("%.15f" % (M))
        print(y)
    else:
      print(x)
      print(y)

#Extremos do intervalo
a = float(input())
b = float(input())

#Tolerância
t = float(input())

Bolz(a, b, t)
```
