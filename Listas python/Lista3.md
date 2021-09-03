# Lista 3 - Resoluções

## Questão 01
```python
#Objetivo: receber um real e zerar ele com uma operação B-M*A
#Cuidado com o arredondamento

A = float(input())
B = float(input())

M = B / A

print(M) 
```

## Questão 02
```python 
#Objetivo: Receber nome em string e imprimir com caracteres ASCII

nome = input()

s = [ord(c) for c in nome] #converte caracteres de nome

print(s)
```

## Questão 03
```python
#Objetivo: Imprimir vetor numa matriz triangular superior
import numpy as np

nome = input()

s = [ord(c) for c in nome] #converte caracteres de nome

i = 0
j = 0

mat = np.eye(len(s),len(s))

for i in range (0, len(s)) :
  for j in range (0, len(s)) :
    mat[i][j] = s[i]

    if (i < j) :
      mat[i][j] = 1
    elif( i > j):
      mat[i][j] = 0

print(mat)
```

## Questão 04
```python
#Objetivo: Resolução retroativa de sistemas
import numpy as np

nome = input()

s = [ord(c) for c in nome] #converte caracteres de nome

mat = np.eye(len(s), len(s)) #cria matriz identidade 3x3

#Transforma em triangular superior
for i in range (0, len(s)) :
  for j in range (0, len(s)) :
    mat[i][j] = s[i]

    if (i < j) :
      mat[i][j] = 1
    elif (i > j) :
      mat[i][j] = 0

res = np.zeros(len(s))
soma = 0
for i in reversed (range(0, len(s))) :
  res[i] = (s[i] - soma) / mat[i][i]
  soma += res[i]

np.set_printoptions(precision= 8)
print(res)
```

## Questão 05
```python
#Objetivo: Matriz aumentada e concatenação
import numpy as np

nome = input()

s = [ord(c) for c in nome] #converte caracteres de nome
mat = np.eye(3, 3)

z = 0

for i in range (0, 4) :
  for j in range (0, 4) :
    mat[i][j] = s[z]
    z += 1

b = [0] * 4

for i in range (0, 4) :
  b[i] = s[z]
  z += 1

b = np.transpose([b])
mat = np.concatenate((mat, b), axis=1)

print(mat)
```

## Questão 06
```python
#Objetivo: Eliminação de Gauss
import numpy as np

def concat (vet) :
  mat = np.eye(3, 3)
  z = 0

  for i in range (0, 3) :
    for j in range (0, 3) :
      mat[i][j] = s[z]
      z += 1

  b = [0] * 3

  for i in range (0, 3) :
    b[i] = s[z]
    z += 1

  b = np.transpose([b])
  mat = np.concatenate((mat, b), axis=1)

  return mat

#Começa o codigo
nome = input()

s = [ord(c) for c in nome] #converte caracteres de nome

res = concat(s) #Matriz aumentada

for i in range(0, 3) :
  pivo = res[i][i]
  for j in range(i + 1, 3) :
    aux = res[j][i] / pivo
    res[j, :] = res[j, :] - aux * res[i, :]

tot = res[:, 3].sum() #Soma dos elementos da última coluna

print(tot)
```

## Questão 07
```python
#Objetivo: Decomposição LU
import numpy as np

'''nome = input()'''
U = np.array([[1, -1, -1], [0, 1, -1], [-1, 0, 3]])
L = np.eye(3) #Matriz identidade 4x4
'''s = [ord(c) for c in nome] #converte caracteres de nome
x = 0
for i in range (0, 4) : #Monta a matriz A
  for j in range (0, 4):
    U[i][j] = s[x]
    x += 1'''
for i in range(0, 3) : #Resolucao de Gauss
  pivo = U[i][i]
  for j in range(i + 1, 3) :
    aux = U[j][i] / pivo
    L[i][j] = aux
    U[j, :] = U[j, :] - aux * U[i, :]
L = np.transpose(L) #Transpoe L

'''tot = L[3, :].sum() #Soma dos elementos da última linha de L'''

print(L)
print(U)
```

## Questão 08
```python
#Objetivo: Inicio aos metodos iterativos
import numpy as np
vet = input()
n = int(input())
s = [ord(c) for c in vet] #converte caracteres de nome
s1 = np.array(s)#Pega s e coloca em um vetor matematico
res = (s1.sum() - s1[n]) / s1[n]
print(res)
```

## Questão 09
```python
#objetivo: Método de Jacobi
'''9- Faça um programa para encontrar a solução do sistema Ax=b utilizando o método iterativo de Jacobi. O programa deve receber todos 
os elementos da matriz A(4x4) e do vetor b(4x1) a partir de uma string com 20 caracteres e convertê-los em inteiro usando a tabela ascII. 
Em seguida, receber um inteiro para representar a quantidade de casas decimais da tolerância (utilize erro absoluto) e o outro inteiro para 
o número máximo de iterações. O  código deve retornar o vetor solução x e o número de iterações. Considere como vetor inicial o vetor de zeros.'''
import numpy as np

vet = input()
tol = int(input()) #tolerancia
n = int(input()) #max itr
s = [ord(c) for c in vet] #converte caracteres de nome

x0 = np.zeros(4) #vetor inicial
A = np.eye(4) #matriz A
b = np.zeros(4) #vetor de termos independentes
q = 0
for i in range (0, 4) : #Monta a matriz A 
  for j in range (0, 4):
    A[i][j] = s[q]
    q += 1
for k in range(0, 4) : #Monta o vetor b
  b[k] = s[q]
  q += 1
erro = 10
cont = 0
while (erro >= 10**(-tol) and cont < n) : #condicao de parada
  x1 = np.array(x0) #vetor para calcular o erro
  for i in range (0, 4) :
    soma = 0
    for j in range (0, 4) :
      soma += A[i][j] * x1[j]
    x0[i] = (b[i] - (soma - A[i][i] * x1[i])) / A[i][i]
  cont += 1
  erro = np.amax(abs(x0 - x1)) #Erro absoluto
print(x0)
print(cont)
```

## Questão 10
```python 
#objetivo: Método de Jacobi
'''10- Faça um programa para encontrar a solução do sistema Ax=b utilizando o método iterativo de Gauss-Seidel. 
O programa deve receber todos os elementos da matriz A(4x4) e do vetor b(4x1) a partir de uma string com 20 caracteres 
e convertê-los em inteiro usando a tabela ascII. Em seguida, receber um inteiro para representar a quantidade de casas 
decimais da tolerância (utilize erro absoluto) e o outro inteiro para o número máximo de iterações. O  código deve 
retornar o vetor solução x e o número de iterações. Considere como vetor inicial o vetor de zeros.'''
import numpy as np

vet = input()
tol = int(input()) #tolerancia
n = int(input()) #max itr
s = [ord(c) for c in vet] #converte caracteres de nome

x0 = np.zeros(4) #vetor inicial
A = np.eye(4) #matriz A
b = np.zeros(4) #vetor de termos independentes
q = 0
for i in range (0, 4) : #Monta a matriz A 
  for j in range (0, 4):
    A[i][j] = s[q]
    q += 1
for k in range(0, 4) : #Monta o vetor b
  b[k] = s[q]
  q += 1
erro = 10
cont = 0
while (erro >= 10**(-tol) and cont < n) : #condicao de parada
  x1 = np.array(x0) #vetor para calcular o erro
  for i in range (0, 4) :
    soma = 0
    for j in range (0, 4) :
      soma += A[i][j] * x0[j]
    x0[i] = (b[i] - (soma - A[i][i] * x0[i])) / A[i][i]
  cont += 1
  erro = np.amax(abs(x0 - x1)) #Erro absoluto
print(x0)
print(cont)
```