# Como usar o ambiente virtual na sua máquina

## Função
O ambiente virtual é um meio no qual você pode rodar os programas na sua máquina e poder instalar as bibliotecas e arquivos necessários sem ter conflitos com outros programas do seu computador.

## Modo de uso
Para acessar o ambiente virtual na sua máquina, basta seguir as etapas abaixo:
1. Clique com o botão direito sobre o ícone da pasta "venv" e selecione a opção "Abrir com o VS Code" (Caso queira abrir usando o CMD ou Powershell basta seguir o exemplo abaixo abrindo direto o programa esoclhido)
2. Ao abrir o programa, digite o comando .\venv\Scripts\activate
3. Caso tenha dado tudo certo, você verá um "(venv)" logo no início de cada linha no terminal, indicando que você está dentro do seu ambiente virtual
4. Para sair do ambiente virtual basta digitar deactivate no terminal e o "(venv)" sumirá indicando que você saiu corretamente

## Teste de execução
Dentro desta pasta terá um arquivo chamado "Teste.py" com o código para imprimir "Ola, mundo" e o valor de um seno aleatório usando uma das bibliotecas previamente instaladas no ambiente virtual, para executá-lo, basta digitar .\ no terminal e aperte a tecla TAB até aparecer o nome do seu arquivo, depois é só aperte Enter e o arquivo será executado.

Caso a operação tenha sido feita corretamente uma janela se abrirá e o programa será executado.

Abaixo tem uma foto da execução do programa:

![teste python](https://github.com/paivaneto8190/ComputacaoNumerica/blob/master/Ambiente%20Virtual/teste_venv.png?raw=true)

