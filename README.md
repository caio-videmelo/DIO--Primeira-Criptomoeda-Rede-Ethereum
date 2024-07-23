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

``
git clone https://github.com/caio-videmelo/DIO--Primeira-Criptomoeda-Rede-Ethereum
``
`` 
cd CryptoMelo
``

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

## Testando a Crypto Melo

### 1. Configuração do Ambiente de Teste

Certifique-se de ter o Truffle e o Ganache instalados.

``bash

npm install -g truffle
npm install -g ganache-cli

``

Inicie o Ganache para simular uma rede Ethereum local:

``bash

ganache-cli

``

### 2. Configuração do Projeto Truffle

Dentro do diretório do seu projeto, inicialize um novo projeto Truffle:

``bash

truffle init

``

Instale as dependências necessárias:

``bash

npm install @openzeppelin/test-helpers chai

``

### 3. Criação do Arquivo de Migração

No diretório migrations, crie um novo arquivo de migração, por exemplo, 2_deploy_contracts.js:

``bash

const CryptoMelo = artifacts.require("CryptoMelo");

module.exports = function (deployer) {
  deployer.deploy(CryptoMelo);
};

``

### 4. Escrever Testes

Crie um arquivo de teste em test/CryptoMelo.test.js e adicione os seguintes testes:

``bash

const CryptoMelo = artifacts.require("CryptoMelo");
const { expect } = require('chai');
const { BN, expectEvent, expectRevert } = require('@openzeppelin/test-helpers');

contract("CryptoMelo", (accounts) => {
  const [deployer, recipient, anotherAccount] = accounts;

  beforeEach(async () => {
    this.token = await CryptoMelo.new({ from: deployer });
  });

  it("deve retornar o total supply correto", async () => {
    const totalSupply = await this.token.totalSupply();
    expect(totalSupply).to.be.bignumber.equal(new BN(web3.utils.toWei('10', 'ether')));
  });

  it("deve retornar o saldo correto do deployer", async () => {
    const balance = await this.token.balanceOf(deployer);
    expect(balance).to.be.bignumber.equal(new BN(web3.utils.toWei('10', 'ether')));
  });

  it("deve transferir tokens corretamente", async () => {
    const amount = new BN(web3.utils.toWei('1', 'ether'));
    await this.token.transfer(recipient, amount, { from: deployer });

    const deployerBalance = await this.token.balanceOf(deployer);
    const recipientBalance = await this.token.balanceOf(recipient);

    expect(deployerBalance).to.be.bignumber.equal(new BN(web3.utils.toWei('9', 'ether')));
    expect(recipientBalance).to.be.bignumber.equal(amount);
  });

  it("deve aprovar tokens corretamente", async () => {
    const amount = new BN(web3.utils.toWei('1', 'ether'));
    await this.token.approve(anotherAccount, amount, { from: deployer });

    const allowance = await this.token.allowance(deployer, anotherAccount);
    expect(allowance).to.be.bignumber.equal(amount);
  });

  it("deve transferir tokens a partir de uma conta aprovada corretamente", async () => {
    const amount = new BN(web3.utils.toWei('1', 'ether'));

    await this.token.approve(anotherAccount, amount, { from: deployer });
    await this.token.transferFrom(deployer, recipient, amount, { from: anotherAccount });

    const deployerBalance = await this.token.balanceOf(deployer);
    const recipientBalance = await this.token.balanceOf(recipient);
    const allowance = await this.token.allowance(deployer, anotherAccount);

    expect(deployerBalance).to.be.bignumber.equal(new BN(web3.utils.toWei('9', 'ether')));
    expect(recipientBalance).to.be.bignumber.equal(amount);
    expect(allowance).to.be.bignumber.equal(new BN('0'));
  });

  it("deve reverter se saldo insuficiente", async () => {
    const amount = new BN(web3.utils.toWei('11', 'ether'));
    await expectRevert(this.token.transfer(recipient, amount, { from: deployer }), "revert");
  });

  it("deve reverter se aprovação insuficiente", async () => {
    const amount = new BN(web3.utils.toWei('1', 'ether'));
    await this.token.approve(anotherAccount, amount, { from: deployer });

    const transferAmount = new BN(web3.utils.toWei('2', 'ether'));
    await expectRevert(this.token.transferFrom(deployer, recipient, transferAmount, { from: anotherAccount }), "revert");
  });
});
``

### 5. Executar os Testes

Para executar os testes, use o comando:

``bash

truffle test

``
