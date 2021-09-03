# Laboratório 1 - Modelar a trajetória de uma bola usando métodos numéricos

### Materiais:
- Câmera de celular
- Bola
- Obstáculo
- Cabo de vassoura de aproximadamente 1 metro (usar como medida de referência na câmera)

### Metodologia:
Para o experimento, começamos gravando uma bola quicando e atingindo uma mala que foi usada como obstáculo para podermos capturar 4 frames usando o Media Player Classic (MPC):
1. Bola exatamento após sair do chão;
2. 1 frame após o primeiro;
3. Altura máxima; 
4. Bola atingindo a mala.

<p style="text-align: center;">
Após isso usamos o paint para pegar as medidas da altura da bola em pixeis usando o cabo de vassoura para converter as medidas de pixel para metro por meio de uma regra de três e aplicar nas equação do movimento uniformemente variado para acharmos as raízes correspondentes a aceleração da bola e sua velocidade incial usando algoritmos de métodos numéricos para aproximarmos cada vez mais do valor exato da raiz, visto que dado os procedimentos de coleta e equipamentos usados, tiveram imprecisões nas medidas.
</p>

Por fim, comparamos os resultados obtidos na prática com o valor teórico calculado e plotamos em um gráfico de altura x tempo com a imagem original de fundo para melhor visualização, indicando os pontos dos frames pegados, a trajetória real e a teórica.

### Códigos usados no experimento
#### Método da Bisseção
```python
import numpy as np
def func(x) :
    return 1332.84 - 4.62*(10**10)/x**2
a = float(input('a: ')); b = float(input('b: '))
itr = int(input('itr máx: '))
i = 0
E = 1
med = a
if func(a)*func(b) < 0 :
    while E >= 1.76*10**(-3) and i < itr:
      med0 = med
      med = (a + b)/2
      if func(a)*func(med) < 0 :
          b = med;
      else :
          a = med;
      E = np.abs((med - med0)/med)
      i += 1
    print('Raiz da função: ', med)
    print('Valor da função: ', func(med))
    print('Iterações: ', i)
else :
    print('Não é possível aplicar o método da Bisseção neste intervalo')

#a = 1, b = 5999 e N = 100
```

#### Método da Falsa-Posição
```python
import numpy as np
def func(x) :
    return 1332.84 - 4.62*(10**10)/x**2
a = float(input('a: ')); b = float(input('b: '))
itr = int(input('itr máx: '));
i = 0
E = 1
med = a
if func(a)*func(b) < 0 :
    while E >= 1.76*10**(-3) and i < itr:
      med0 = med
      med = a - func(a)*(b - a)/(func(b) - func(a))
      if func(a)*func(med) < 0 :
          b = med;
      else :
          a = med;
      E = np.abs((med - med0)/med)
      i += 1
    print('Raiz da função: ',"%.8f" % med)
    print('Valor da função: ', func(med))
    print('Iterações: ', i)
else :
    print('Não é possível aplicar o método da Falsa-Posição neste intervalo')

#a = 1, b = 5888 e N = 100
```

#### Método de Newton
```python
import numpy as np
def func(x) :
    return 1332.84 - 4.62*(10**10)/x**2
def dev(x) :
    return (9.24 * (10**10))/x**3
x0 = float(input('x0: '));
itr = int(input('itr máx: '));
i = 0
E = 11
x = x0
while E >= 1.76*10**(-3) and i < itr:
    x0 = x
    x = x0 - func(x0)/dev(x0)
    E = np.abs((x - x0)/x)
    i += 1
print('Raiz da função:',(x))
print('Valor da função:', func(x))
print('Iterações:', i)

#x0 = 5800 e N = 100
```
#### Método da secante
```python
import numpy as np
def func(x) :
    return 1332.84 - 4.62*(10**10)/x**2
x1 = float(input('x1: ')); x0 = float(input('x0: '))
itr = int(input('itr máx: '));
i = 0
E = 1
x2 = x1
x1 = x0
while E >= 1.76*10**(-3) and i < itr :
    x0 = x1
    x1 = x2
    x2 = x1 - func(x1)*(x1 - x0)/(func(x1) - func(x0))
    E = np.abs((x2 - x1)/x2)
    i += 1
print('Raiz da função:',(x2))
print('Valor da função:', func(x2))
print('Iterações:', i)

#x1 = 5999, x0 = 5887.513391671133 e N = 100
```
#### Caregar imagens
```python
from google.colab import files
uploaded = files.upload()
```
#### Imagens e gráficos
```python
import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(173,1920,200)	
y = np.tan(0.83) * (x - 173) - (1.7*10**4)*((x - 173)**2)/(2*pow(np.cos(0.83),2)*(6637.77)**2)	+ 289
plt.plot(x,y)	

img = plt.imread("frame1 - 1.999.jpg")
t = img.shape
print('tamanho imagem: ', t)
fig, ax = plt.subplots(figsize=(15, 15))
ax.imshow(img, extent=[0, t[1], 0, t[0]]) 

ax.plot(173, 289, '.', linewidth=5, markersize=10, color='b')
ax.plot(267, 391, '.', linewidth=5, markersize=10, color='b')
ax.plot(1073, 883, '.', linewidth=5, markersize=10, color='b')
ax.plot(1659, 581, '.', linewidth=5, markersize=10, color='b')

ax.plot(x, y, '.', linewidth=5, markersize=10, color='r') 
```

### Resultado final do experimento
Abaixo os gráficos da trajetória teórica da bola e trajetória real, respctivamente:

![Trajetória teórica](https://github.com/paivaneto8190/ComputacaoNumerica/blob/master/Laborat%C3%B3rios/lab1.1.png?raw=true)
![Trajetória real e frames capturados](https://github.com/paivaneto8190/ComputacaoNumerica/blob/master/Laborat%C3%B3rios/lab1.2.png?raw=true)
