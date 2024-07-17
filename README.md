# CryptoMelo: Criação de Criptomoeda na Blockchain Ethereum

## Desafio de Projeto DIO.me: Criando sua Primeira Criptomoeda da Rede Ethereum

Descrição do Projeto

Bem-vindo ao desafio de projeto "Criando sua própria Criptomoeda"! Neste laboratório, você aprenderá a desenvolver sua própria moeda digital usando Solidity e Smart Contracts. Este projeto prático oferece uma excelente oportunidade para entender os fundamentos das criptomoedas e seu funcionamento na prática.

### Objetivos

a. Compreender os conceitos básicos de Solidity e Smart Contracts.

b. Implementar um contrato inteligente para uma criptomoeda simples.

c. Explorar como criar transações básicas e verificar o estado da rede.

d. Ganhar experiência prática valiosa em blockchain e desenvolvimento de criptomoedas.

### Tecnologias Utilizadas

- Solidity
- Ethereum Blockchain

### Recursos Adicionais

- [Documentação oficial do Solidity](https://soliditylang.org/docs/)
- [Ethereum Developer Documentation](https://ethereum.org/developers/)

### Instruções para configuração:

1. Clone o repositório:

``git clone https://github.com/caio-videmelo/DIO--Primeira-Criptomoeda-Rede-Ethereum``
`` cd CryptoMelo``

2. Instale as dependências:

Certifique-se de ter o Node.js e o npm instalados.
`` npm install``

3. Compile o contrato inteligente:

Use o Truffle para compilar o contrato.
``truffle compile``

4. Implante o contrato na rede Ethereum:

Configure a rede desejada no arquivo truffle-config.js e execute o comando de migração.

``truffle migrate --network <network_name>``

5. Interaja com o contrato:

Use o Truffle Console para interagir com o contrato implantado.

``truffle console --network <network_name>``

## Estrutura do Projeto

contracts/: Contém os contratos inteligentes em Solidity.

migrations/: Scripts de migração para implantar os contratos na blockchain.

test/: Testes automatizados para garantir o funcionamento do contrato.

## Contribuições

Contribuições são bem-vindas! Sinta-se à vontade para abrir issues e pull requests para melhorias ou correções.
