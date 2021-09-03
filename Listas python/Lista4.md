# Lista 1 - Resoluções

## Questão 01
```python
#Dias corridos do ano bissexto
dia = int(input())
mes = int(input())

dc = 0
for i in range(1, mes) :
  if (i % 2 != 0) :
    dc += 31
  else :
    dc += 30

if (mes > 2) :
  dc -= 1
dc += dia
print(dc)
```

## Questão 02
```python
#Recebe string x e acha y
import numpy as np
np.set_printoptions(precision=8, suppress=True)
texto=input()
a=texto.split(',')
x=np.arange(len(a),dtype=float)
for i in range(len(a)):
  x[i]=float(a[i])
a_0=0.3
a_1=3.2
a_2=0.21

y = a_0 + a_1 * np.cos(x) + a_2 * np.sin(x) #O python interpreta essa afirmação usando a igualdade vetorial
print(y)
```

## Questão 03
```python
#MMQ linear
import numpy as np
np.set_printoptions(precision=8, suppress=True)
texto_x = input()
texto_y = input()
a=texto_x.split(',')
b=texto_y.split(',')
x=np.arange(len(a),dtype=float)
for i in range(len(a)):
  x[i]=float(a[i])
y=np.arange(len(b),dtype=float)
for i in range(len(a)):
  y[i]=float(b[i])

sg02 = (x ** 0).sum()
sg0g1 = (x).sum()
sg1g0 = sg0g1
sg12 = (x**2).sum()
sg0y = (y).sum()
sg1y = (y*x).sum()

A = np.array([[sg02, sg0g1], [sg0g1, sg12]])
b = np.array([[sg0y], [sg1y]])
np.linalg.inv(A).dot(b)

#1, 7, 14, 16, 23, 25
#19,  -4,  -33,  -40,  -71,  -75
```

## Questão 04
```python
#MMQ linear com k variáveis
import numpy as np
np.set_printoptions(precision=8, suppress=True)
texto_x = input()
texto_y = input()
k = int(input())
a=texto_x.split(',')
b=texto_y.split(',')
x=np.arange(len(a),dtype=float)
for i in range(len(a)):
  x[i]=float(a[i])
y=np.arange(len(b),dtype=float)
for i in range(len(b)):
  y[i]=float(b[i])

#define matriz de ordem k
A = np.eye(k + 1)
b = np.zeros(k + 1)

for i in range(0, k + 1) :
  for j in range(0, k + 1) :
    A[i][j] = (pow(x, i) * pow(x, j)).sum()

  b[i] = (pow(x, i) * y).sum()

np.linalg.inv(A).dot(b)
```

## Questão 05
```python
#MMQ genérico para a0*e^x + a1*cos(x)
import numpy as np
np.set_printoptions(precision=8, suppress=True)
texto_x = input()
texto_y = input()
a=texto_x.split(',')
b=texto_y.split(',')
x=np.arange(len(a),dtype=float)
for i in range(len(a)):
  x[i]=float(a[i])
y=np.arange(len(b),dtype=float)
for i in range(len(b)):
  y[i]=float(b[i])

sg02 = (np.exp(x)**2).sum()
sg0g1 = (np.exp(x)*np.cos(x)).sum()
sg1g0 = sg0g1
sg12 = (np.cos(x)**2).sum()
sg0y = (np.exp(x)*y).sum()
sg1y = (np.cos(x)*y).sum()

A = np.array([[sg02, sg0g1], [sg0g1, sg12]])
b = np.array([sg0y , sg1y])
res = np.linalg.inv(A).dot(b)

print(res)
```

## Questão 06
```python
#MMQ linear para achar yp
import numpy as np
texto_x = input()
texto_y = input()
k = int(input())
xp = float(input())
a=texto_x.split(',')
b=texto_y.split(',')
x=np.arange(len(a),dtype=float)
for i in range(len(a)):
  x[i]=float(a[i])
y=np.arange(len(b),dtype=float)
for i in range(len(b)):
  y[i]=float(b[i])

#define matriz de ordem k
A = np.eye(k + 1)
b = np.zeros(k + 1)

for i in range(0, k + 1) :
  for j in range(0, k + 1) :
    A[i][j] = (pow(x, i) * pow(x, j)).sum()

  b[i] = (pow(x, i) * y).sum()

vec = np.linalg.inv(A).dot(b)

res = 0
for z in range (0, k + 1) :
  res += pow(xp, z) * vec[z]
print(round(res,8))
```

## Questão 07
```python
#Interpolação de Lagrange
import numpy as np

def lagrange(x, y, xp) :  
  res = [1]*len(x)
  yp = 0
  for i in range (0, len(x)) :
    for j in range (0, len(x)) :
      if (j != i) :
        res[i] *= (xp - x[j]) / (x[i] - x[j])
    yp += y[i] * res[i]
  return yp

np.set_printoptions(precision=8, suppress=True)
texto_x = input()
texto_y = input()
xp = float(input())
a=texto_x.split(',')
b=texto_y.split(',')
x=np.arange(len(a),dtype=float)
for i in range(len(a)):
  x[i]=float(a[i])
y=np.arange(len(b),dtype=float)
for i in range(len(b)):
  y[i]=float(b[i])


print("%.8f" % (lagrange(x, y, xp)))
```

## Questão 08
```python
#Objetivo: Diferenças divididas
import numpy as np

texto_x = input()
texto_y = input()
a=texto_x.split(',')
b=texto_y.split(',')
x=np.arange(len(a),dtype=float)
for i in range(len(a)):
  x[i]=float(a[i])
y=np.arange(len(b),dtype=float)
for i in range(len(b)):
  y[i]=float(b[i])

A = np.eye(len(b)) # armazena as diferenças divididas
A[:, 0] = np.copy(y)

for i in range (len(b)) :
  k = i
  for j in range (1, len(b)) :
      A[i][j] = (A[j][i] - A[k][i]) / (x[j] - x[i])
      k += 1

print(A)
```
