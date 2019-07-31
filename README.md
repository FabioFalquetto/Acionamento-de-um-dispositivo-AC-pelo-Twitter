# Acionamento-de-um-dispositivo-AC-pelo-Twitter
# DESCRIÇÃO
O projeto consiste no acionamento de um dispositivo AC pelo aplicativo móvel do twitter, no qual o usuário consegue acionar esse dispositivo somente com um simples post nessa rede social. 
# Pré-requisitos
PASSO 1: Dispositivos utilizados:

1 Power Switch Tail , este é basicamente um relé que é usado para interface com a tensão AC 

1 Arduino Board (qualquer um fará) 

1 Computador rodando o arduino IDE e Python 

1 Dispositivo AC

PASSO 2: Configurações no computador: 

Para fazer a interface entre o arduino e o twitter, vamos usar o python. Existe uma biblioteca que já é montada e nos permite usar a API do Twitter. Chama -se "python-twitter". 

Depois de instalar o python , instale a biblioteca python-twitter e todas as suas dependências. Se você tiver problemas, consulte a documentação no site "python-twitter". 

Em seguida, instale o Arduino IDE para que você possa programar seu arduino e conversar com ele via porta serial. 

Uma vez que estes estão configurados e funcionando, é hora de pegar suas credenciais em twitter.com

PASSO 3: Configurando o Twitter

Primeiro, faça uma conta no Twitter para este projeto que é separado da sua conta principal no Twitter. 

Em seguida, vá para dev.twitter.com e registre seu aplicativo, isso permitirá que você pegue 4 informações importantes - 

Token de Acesso - Acesso Token Segredo - Chave do Consumidor - Segredo do Consumidor 

Essas chaves serão necessárias no código python posteriormente para fazer a interface com a API do twitter. Depois de ter esses 4 códigos, você poderá continuar.

PASSO 4: O Código: Lado do Python
O código python basicamente usa a biblioteca python-twitter para pedir ao twitter os status do usuário "x", depois pega o último status e procura pelo termo "#(nome da sua conta no twitter)". 
se encontrado envia o valor ascii de 1 para a porta serial (e para o arduino), se #(nome da sua conta no twitter) for encontrado, ele envia um valor ascii de 0. 
Por último, faz um loop e verifica a conta do Twitter a cada 15 segundos procurando por alterações.

# Instalação
Abaixo segue o código de acionamento do projeto:

## importar bibliotecas

importar tempo de importação 
serial de importação do twitter

## autentique-se com twitter 
api = twitter.Api (consumer_key = 'consumerkeyhere', consumer_secret = 'usersecrethere', access_token_key = 'accesskey', access_token_secret = 'accesssecret')

## definido para sua porta serial 
ser = serial.Serial ('/ dev / ttyUSB0', 19200)

## check porta serial 
def checkokay (): 
ser.flushInput () 
time.sleep (3) 
linha = ser.readline () 
time.sleep (3)

if line == '': 
line = ser.readline () 
print 'here' 
## mensagem de boas vindas 
print 'Welcome To (nome da sua conta)!' 
print 'Acionar dispositivo ..' 
def (nome da sua conta) (): 
status = [] 
x = 0

status = api.GetUserTimeline ('X') ## pega os status mais recentes

checkIt = [s.text para s no status] ## coloca status em um array

drip = checkIt [0] .split () ## divide primeiro o tweet em palavras

## check for match e escreva para serial se match 
if drip [0] == '#(nome da sua conta)': 
print 'Chilrear Recieved, Acionar dispositivo' 
ser.write ('1') 
elif drip [0] == '#(nome da sua conta)+stop' : ## break if done 
ser.write ('0') 
print 'parou, aguardando instruções.' 
else: 
ser.write ('0') 
print 'Aguardando Tweet'

enquanto 1: 
(nome da sua conta) () ## chama a função 
(nome da sua conta) time.sleep (15) ## sleep por 15 segundos para evitar a limitação de taxa

# Uso
A configuração do hardware é bastante simples, já que o controle de tensão CA está sendo controlado pela cauda do interruptor de alimentação. 

A cauda do interruptor de alimentação permite conectar dois fios, um ao terra e um ao pino de controle, para ligar e desligar o relé. . Como visto no código, tudo que você precisa é de uma instrução simples alta / baixa. 

Conecte o arduino ao seu computador e certifique-se de que a porta serial esteja configurada. Em seguida, conecte os fios da cauda no ponto 13 e aterre. 

Em seguida, conecte o dispositivo ao relé e conecte o relé a uma tomada comum.
