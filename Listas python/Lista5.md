# Lista 5 - Resoluções

## Questão 01
```python
#Objetivo: Trapézio composto

import numpy as np

a = float(input())
b = float(input())
N = int(input())
res = 0
h = (b - a) / N
y = np.zeros(N + 1)

for i in range(N + 1) :
  y[i] = np.sin(a)
  a = a + h
for i in range(N + 1) :
  if (i != 0 and i != N) :
    res += 2*y[i]
  else :
    res += y[i]

res = (h/2)*res

print("%.8f" % res)
```

## Questão 02
```python
#Objetivo: Trapézio simples

import numpy as np
x0 = float(input())
x1 = float(input())
y0 = float(input())
y1 = float(input())

I = ((x1 - x0)/2) * (y0 + y1)

print("%.8f" % I)
```

## Questão 03
```python
#Objetivo: Simpson 1/3

import numpy as np

a = float(input())
b = float(input())
h = float(input())
res = 0
N = int((b - a)/h)
y = np.zeros(N + 1)

teste = a

while (teste < b) :
  teste += h

if ( N % 2 == 0) :
  for i in range (N + 1) :
    y[i] = ((a**2) / 5) + 2*np.sin(a)
    a = a + h

  for i in range(N + 1) :
    if (i != 0 and i != N) :
      res += 3*y[i]
    else :
      res += y[i]
elif (teste < b or N % 2 != 0) :
    for i in range (N) :
      y[i] = ((a**2) / 5) + 2*np.sin(a)
      a = a + h

    for i in range(N) :
      if (i != 0 and i != N - 1) :
       res += 3*y[i]
      else :
       res += y[i]
res = (h/3) * res

print("%.8f" % res)
```

## Questão 04
```python
#Objetivo: Segunda regra de simpson

import numpy as np

a = float(input())
b = float(input())
N = int(input())

h = (b - a) / N
y = np.zeros(N + 1)
res = 0

for i in range (N + 1) :
  y[i] = ((a**2) / 5) + 2*np.sin(a)
  a = a + h
for i in range(N + 1) :
  if (i != 0 and i != N) :
    res += 3*y[i]
  else :
    res += y[i]

res = (3/8) * h * res
print("%.8f" % res)
```

## Questão 05
```python
#Objetivo: Trapézio vetores

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
```

