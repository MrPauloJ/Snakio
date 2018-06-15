## Bem vindo

### Descrição
```
Esse projeto tem como base a criação do "jogo da cobrinha".
Desenvolvido em python com o objetivo de ser executado através
do prompt de comando do sistema e sendo apresentado como TCC 
Para o curso de introdução a python pelo 
Centro de INformática da Universidade Federal de PErnambuco. 
```
### Código Fonte
```
#Especificações do projeto
#Autor: Paulo J.
#Data: 24/01/2017
#Versão PY: python 3.3
#Detalhes: Projeto Desenvolvido para conclusão do curso
#Curso: Introdução a python - PET (CIN-UFPE)

#importações
import sys
import time
import random
 
class Cobra(object):
    nome = "Joe"
    def __init__(self,nomeCob):
        self.nome=nomeCob
        
# Projeto
print("# Projeto: Jogo da cobrinha no IDLE PY")
print("# Aluno: Paulo J. ;)")
print(" ")
time.sleep(1)

# Func principal
print("\t"*2 + "Bem Vindo !!!")
time.sleep(1)
print(" ")
 
print("\t"*2+"Instrucoes")
print(" ")
print("w - Move para cima.")
print("a - Move para esquerda.")
print("s - Move para baixo.")
print("d - Move para direita.")
print("e - Finaliza o game.")
print (" ")
 
nomeSnake=input("Informe um nome para a Snake: ")
Cobra(nomeSnake)
print(" ")
 
#Pergunta tamanho do mapa
print ("Digite Qualquer letra para o tamanho padrÃ£o ou informe um tamanho.")
print ("O tamanho maximo permitido Ã© 100. (100x100)")
print ("O tamanho minimo permitido e 5. (5x5)")
try:
    tamanhoMapa=int(input("Defina o tamanho desejado para o mapa:"))
    if(tamanhoMapa>=5) and (tamanhoMapa<=100):
        tamanhoMapa=tamanhoMapa
        print(" ")
    else:
        print("valor invalido")
        print(" ")
except:
    tamanhoMapa=20

# Declara mapa
mapa = [['.' for i in range(tamanhoMapa)] for j in range(tamanhoMapa)]
 
# Declara posicao da cabeca da cobra
posicao = [3, 4]
cobra=[]
cobra.append((posicao[0], posicao[1]))

# Declara ultima posicao
ultPos=[]
sc=False
# Funcao que imprime o mapa e a cabeca cobra
# Precisa ser adaptada pra imprimir toda a cobra
def imprime_mapa(pos,fruta):
    for i in range(tamanhoMapa):
        for j in range(tamanhoMapa):
            gg=False
            #imprime a cobra
            for z in range(0,len(cobra)):
                if (i==cobra[z][0]) and j==cobra[z][1]:
                    sys.stdout.write('#')
                    gg=True
            if (i == fruta[0] and j == fruta[1]):
                if (fruta[0]==pos[0] and fruta[1]==pos[0]):
                    sys.stdout.write('')
                else:
                    sys.stdout.write('*')
            elif(gg==False): #para não imprimir o ponto onde estava a cobra
                sys.stdout.write(mapa[i][j])
        print ("")
#variaveis de verificoes
morreu=False
#movimentos
def movimento(cmd):
    if(comando=="w"):
        posicao[0]-=1
    elif(comando=="a"):
        posicao[1]-=1
    elif(comando=="s"):
        posicao[0]+=1
    elif(comando=="d"):
        posicao[1]+=1
    elif(not comando=="e"):
        print (" ")
        print("Movimento invalido")
        print (" ")
        #sai trocando a posicao atual da cobra, pela anterior
    posicaoAnterior = cobra[0]
    cobra[0] = (posicao[0], posicao[1])
    for x in range(1, len(cobra)):
        auxiliar = cobra[x]
        cobra[x]=posicaoAnterior
        posicaoAnterior = auxiliar

# Primeira posicao aleatoria da fruta
p1=random.randint(0,tamanhoMapa-1)
p2=random.randint(0,tamanhoMapa-1)
fruta=[p1,p2]

# Pontos
pontos=0

# O laco abaixo realiza as operacoes que devem ser feitas sempre que
# Um valor de direcao eh lido pelo usuario
while (True):
    #verifica se a cobra come ela mesma
    for b in range(1,len(cobra)):
        if(posicao[0]==cobra[b][0]) and (posicao[1]==cobra[b][1]) or \
        posicao[0]==cobra[1][0] and posicao[1]==cobra[1][1]:
            sc=True
    #Verifica se "Ela se matou mlk" (Referência blueza1 - o rato se matou mlk)
    if(sc==True):
        print(" ")
        ultPos=(posicao[0],posicao[1])
        print(Cobra.nome + " Morreu")
        print("Game Over")
        print("Total de pontos:" + str(pontos))
        break
    #verifica se a cobra esta na mesma posicao da fruta
    if(fruta[0]==posicao[0]) and (fruta[1]==posicao[1]):
        cobra.append(ultPos)
        pontos+=1
    #nova posicao da fruta
    for h in range(len(cobra)):
        for g in range(len(cobra)):
            if (fruta[0]==cobra[g][0] and fruta[1]==cobra[g][1]):
                p1=random.randint(0,tamanhoMapa-1)
                p2=random.randint(0,tamanhoMapa-1)
                fruta=[p1,p2]
    #imprime o mapa verificado
    imprime_mapa(cobra,fruta)
    #print (fruta)
    #verifica se ta fora do mapa
    if ((posicao[0]>(tamanhoMapa-1)) or (posicao[1]>(tamanhoMapa-1)) or \
        (posicao[0]<0) or (posicao[1]<0) ):
        morreu=True
    else:
        morreu=False
    #mata a python se tiver fora do mapa
    if(morreu==True):
        print(" ")
        ultPos=(posicao[0],posicao[1])
        print(Cobra.nome + " Morreu")
        print("Game Over")
        print("Total de pontos Feitos:" + str(pontos))
        break
    #continua a experiencia da cobra
    else:
        comando = input("proximo movimento:")
        ultPos=cobra[len(cobra)-1]
        movimento(comando)
        cobra[0] = (posicao[0], posicao[1])
           
    #sai do jogo se decidir
    if(comando=="e"):
        print(" ")
        print("voce saiu")
        print("Jogo Finalizado")
        print("Total de pontos Feitos:" + str(pontos))
        break
    else:
        print('')
    # Tratar a entrada 'comando'
    # Modificar a cobra e o mapa de acordo com a entrada
    # Utilizar W, A, S, D para movimento e E para sair

```

### Suporte e Contato
Através deste [Link](http://trosleihard.esy.es/dev) vocês podem entrar em contato direto com o desenvolvedor do projeto.
