# Questão 01: Calcula o valor da n-derivada do seno em um certo ponto

```python
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

# Questão 02: Receber 3 números e colocar no vetor
 ```python
#podia fazer com for
x1 = float(input())
x2 = float(input())
x3 = float(input())
 
vec = [x1, x2, x3]
 
print(vec) #imprime vetor
 ```