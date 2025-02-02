
# Repositório para Construção de uma Carteira de Criptomoedas Focada em Bitcoin
### Desafio de Código DIO 
### Professor: Cassiano Peres
## Objetivo do Desafio

 Desenvolver um gerador de carteiras e realizar transações com bitcoin.

 Criar endereço público e chave privada.

 Usar as autenticações para realizar transações (receber e enviar Bitcoin Faucet) e verificar essas transações 
(através de um Block Explorer, neste caso, o Blockchain.com).

### Tecnologias Utilizadas


Linguagem: JavaScript

Electrum Bitcoin Wallet

Bitcoin Faucet Generator (testnet-ambiente local)

### Estrutura do Desafio

Node.js: Editor VScode

Electrum: Plataforma que armazena a lista histórica de transações.

Bitcoin Faucet: Testnet-ambiente local

### Estrutura de Pastas VScode

### CARTEIRAWALLET/
├── node_modules/

├── src/

│   └── createwallets.js

├── package-lock.json

└── package.json


## Código para Gerar uma Carteira de Bitcoin

**// Importando as dependências**

const bip32 = require('bip32');

const bip39 = require('bip39');

const bitcoin = require('bitcoinjs-lib');


**// Definindo a rede**

**// Caso queira rodar em ambiente real, substitua a palavra 'testnet' por 'bitcoin'**

const network = bitcoin.networks.testnet;

**// Derivação de carteiras HD**

const path = "m/49'/1'/0'/0/0";


**// Criando o mnemonic para a seed (palavras)**

let mnemonic = bip39.generateMnemonic();

const seed = bip39.mnemonicToSeedSync(mnemonic);

**// Criando a raiz da carteira HD**

let root = bip32.fromSeed(seed, network);

**// Criando uma conta - par de chaves privada e pública**

let account = root.derivePath(path);

let node = account.derive(0).derive(0);

let btcAddress = bitcoin.payments.p2pkh({

    pubkey: node.publicKey,
    
    network: network
    
}).address;

**// Imprimindo na tela do terminal**

console.log("Carteira Gerada");

console.log("Endereço:", btcAddress);

console.log("Chave Privada:", node.toWIF());

console.log("Seed (mnemonic):", mnemonic);


**Instruções para Configuração do Ambiente**

### Instalar o Node.js:

Baixe e instale a versão mais recente do Node.js.

Verifique a instalação executando node -v e npm -v no terminal.

Configurar o Projeto:

### Crie um diretório para o projeto:

mkdir CARTEIRAWALLET

cd CARTEIRAWALLET



### Inicialize um projeto Node.js:

npm init -y


### Instale as dependências necessárias:

npm install bip32 bip39 bitcoinjs-lib



### Crie a estrutura de pastas e o arquivo createwallets.js:

mkdir src

touch src/createwallets.js


### Rodar o Script:

Navegue até a pasta do projeto e execute o script:

node src/createwallets.js


### Terminal:  
Exemplo de Carteira Gerada

**Carteira Gerada**

**Endereço:** mm1ZxremSru4xF4yBF2oChFUkHYVjPoYk1

**Chave Privada:** cU42tkacgVA3RAF5GoePkcVAeYUV5aWm3w1pYxPnaWtEssjhr3ka

**Seed (mnemonic):** agree gather never spoil reveal illegal winter know swamp asthma much gossip

### Utilizando o Electrum para Gerenciar a Carteira

Download e Configuração do Electrum:

Baixe e instale o Electrum Wallet.

Ao iniciar, selecione a opção "Standard Wallet" e clique em "Next".

Selecione "I already have a seed" e insira a seed gerada pelo script.

### Verificando Transações:

Utilize o Blockchain Explorer para monitorar o endereço público gerado.

## Realizando Transações

### Receber Bitcoin:

Utilize um faucet de Bitcoin Testnet, como o Testnet Faucet, para enviar Bitcoin para o endereço gerado.

### Enviar Bitcoin:

Utilize a interface do Electrum para enviar Bitcoin para outros endereços de Testnet.

### Links para Referências

Node.js Download

Electrum Wallet

Blockchain.com

bitcoinfaucet.uo1.net/send.php

