# desafio_bootcamp_TQI
# Laboratório AWS EC2

Este repositório documenta as práticas realizadas durante o laboratório de **gerenciamento de instâncias EC2** na AWS, utilizando o sistema **Windows**.  
O objetivo é consolidar os conhecimentos adquiridos, registrando os comandos, configurações, desafios enfrentados e insights obtidos durante o processo.

O conteúdo aqui presente serve como **material de apoio** para estudos futuros e implementação de ambientes em nuvem no Windows.

---

## Sumário
1. [Objetivos](#-objetivos)
2. [Pré-requisitos](#-pré-requisitos)
3. [Etapas do Laboratório](#-etapas-do-laboratório)
   - [Criação da Instância EC2](#1-criação-da-instância-ec2)
   - [Conexão via PuTTY ou PowerShell](#2-conexão-via-putty-ou-powershell)
   - [Instalação e Teste de um Servidor Web](#3-instalação-e-teste-de-um-servidor-web)
4. [Gerenciamento e Boas Práticas](#-gerenciamento-e-boas-práticas)
5. [Insights e Aprendizados](#-insights-e-aprendizados)
6. [Referências](#-referências)

---

## Objetivos
- Compreender o processo de criação e configuração de instâncias EC2;
- Explorar tipos de AMIs, tamanhos de instância e configurações básicas;
- Criar e gerenciar **Key Pairs** e **Security Groups**;
- Conectar-se a uma instância a partir do **Windows (PuTTY ou PowerShell)**;
- Realizar deploy simples de uma aplicação web (ex: Nginx);
- Documentar **anotações, aprendizados e boas práticas** para referência futura.

---

## Pré-requisitos

Antes de iniciar o laboratório:
- Conta na **AWS** (Free Tier);
- Computador com **Windows 10/11**;
- **PuTTY** instalado → [Download](https://www.putty.org/)  
  *(opcionalmente, pode usar o **PowerShell** com OpenSSH)*
- Permissão para criar recursos EC2.

---

## Etapas do Laboratório

### 1. Criação da Instância EC2

1. Acesse o console da AWS → **EC2 → Launch Instance**;  
2. Configure:
   - **Nome:** `lab-ec2-instance`
   - **AMI:** Amazon Linux 2 (Free Tier)
   - **Tipo de instância:** `t2.micro`
   - **Key Pair:** Crie uma nova chave chamada `lab-ec2-key.pem`
   - **Security Group:** Permita **SSH (porta 22)** apenas para o seu IP público;
3. Clique em **Launch Instance** e aguarde o status “Running”.

**Insight:** O grupo de segurança é o equivalente a um firewall virtual. É essencial restringir o acesso SSH apenas ao seu endereço IP para maior segurança.

---

### 2. Conexão via PuTTY ou PowerShell

#### 🔹 Opção 1 — Usando PuTTY
O PuTTY não aceita chaves `.pem`, então é necessário convertê-la para `.ppk`:

1. Abra **PuTTYgen** → clique em **Load** → selecione o arquivo `lab-ec2-key.pem`;
2. Clique em **Save private key** e salve como `lab-ec2-key.ppk`;
3. Abra o **PuTTY** e configure:
   - **Host Name:** `ec2-user@<IP-PUBLICO>`
   - **Port:** 22
   - **Connection type:** SSH
   - Vá em *Connection > SSH > Auth* e selecione a chave `lab-ec2-key.ppk`;
4. Clique em **Open** e aceite a mensagem de segurança para se conectar.

---

#### 🔹 Opção 2 — Usando PowerShell (mais simples)

1. Certifique-se de que o **OpenSSH** está habilitado (Windows 10/11 já inclui).

---

## Gerenciamento e Boas Práticas
- Sempre pare (Stop) ou finalize (Terminate) as instâncias após o uso para evitar custos;
- Use Tags para organização (ex: Projeto=DesafioEC2, Ambiente=Teste);
- Monitore o consumo com o AWS CloudWatch;
- Nunca exponha portas desnecessárias (ex: SSH 22 para o mundo inteiro);
- Armazene as chaves (.pem ou .ppk) em local seguro, com permissões restritas;
- Faça snapshots do volume EBS se precisar manter dados.

---

## Insights e Aprendizados
Durante a prática, aprendi que:
- O EC2 é a base para ambientes de computação na nuvem da AWS;
- A configuração de Key Pairs e Security Groups é fundamental para segurança;
- No Windows, a conversão de chaves .pem para .ppk é necessária para o PuTTY;
- Automatizar instalações com User Data poupa tempo em ambientes produtivos;
- Com o Free Tier, é possível explorar muitos recursos sem custos adicionais.

---

## Referências
* Documentação oficial AWS EC2
* AWS Free Tier
* Guia do Amazon Linux 2
* PuTTY Download
* AWS CLI User Guide
