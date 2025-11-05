# desafio_bootcamp_TQI
# Laboratório AWS EC2 — Desafio Acadêmico

Este repositório documenta as práticas realizadas durante o laboratório de gerenciamento de instâncias EC2 na AWS.  
O objetivo é consolidar os conhecimentos adquiridos, registrando os comandos, configurações, desafios enfrentados e insights obtidos durante o processo.

O conteúdo aqui presente servirá como material de apoio para estudos futuros e para implementação de ambientes em nuvem.

---

## Sumário
1. [Objetivos](#-objetivos)
2. [Pré-requisitos](#-pré-requisitos)
3. [Etapas do Laboratório](#-etapas-do-laboratório)
   - [Criação da Instância EC2](#1-criação-da-instância-ec2)
   - [Conexão via SSH](#2-conexão-via-ssh)
   - [Instalação e Teste de um Servidor Web](#3-instalação-e-teste-de-um-servidor-web)
4. [Gerenciamento e Boas Práticas](#-gerenciamento-e-boas-práticas)
5. [Evidências](#-evidências)
6. [Insights e Aprendizados](#-insights-e-aprendizados)
7. [Referências](#-referências)

---

## Objetivos
- Compreender o processo de criação e configuração de instâncias EC2;
- Explorar tipos de AMIs, tamanhos de instância e configurações básicas;
- Criar e gerenciar **Key Pairs** e **Security Groups**;
- Conectar-se a uma instância via SSH;
- Realizar deploy simples de uma aplicação web (ex: Nginx);
- Documentar **anotações, aprendizados e boas práticas** para referência futura.

---

## 🧩 Pré-requisitos

Antes de iniciar o laboratório:
- Conta na **AWS** com acesso ao **Free Tier**;
- Conhecimentos básicos em **Linux** e **rede**;
- Cliente SSH configurado (terminal Linux/Mac ou PuTTY no Windows);
- Permissão para criar recursos EC2.

---

## ⚙️ Etapas do Laboratório

### 1. Criação da Instância EC2
1. Acesse o console da AWS → EC2 → **Launch Instance**;
2. Configure:
   - **Nome**: `lab-ec2-instance`
   - **AMI**: Amazon Linux 2 (Free Tier)
   - **Tipo de instância**: `t2.micro`
   - **Key Pair**: Criei uma nova chave chamada `lab-ec2-key.pem`
   - **Security Group**: Permiti **SSH (porta 22)** apenas para meu IP público;
3. Revise e lance a instância.

📸 *Print sugerido:*  
![Criação da instância EC2](images/ec2-dashboard.png)

**Insight:** O grupo de segurança funciona como um firewall virtual. É essencial restringir o acesso SSH apenas ao endereço IP confiável.

---

### 2. Conexão via SSH
Após a instância estar em estado **running**, conectei usando o terminal:

```bash
chmod 400 lab-ec2-key.pem
ssh -i "lab-ec2-key.pem" ec2-user@<IP-PUBLICO>
