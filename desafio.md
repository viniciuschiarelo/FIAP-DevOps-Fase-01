# Tech Challenge - Fase 1

## Introdução

O Tech Challenge é o projeto principal desta fase da Pós Tech em DevOps, reunindo os conhecimentos desenvolvidos ao longo das disciplinas. Nesta primeira etapa, o objetivo é colocar uma aplicação monolítica em produção utilizando serviços da AWS, seguindo boas práticas de arquitetura, segurança e infraestrutura.

---

## Desafio

A empresa fictícia **DevOps Solutions Inc.** deseja desenvolver uma plataforma centralizada para gerenciamento de **Feature Flags (Feature Toggles)**, chamada **ToggleMaster**.

Nesta primeira fase, o projeto consiste em disponibilizar um MVP da aplicação na AWS, permitindo validar a solução e preparar sua evolução para uma arquitetura distribuída nas próximas fases.

---

## Objetivos

- Executar a aplicação localmente para compreender seu funcionamento.
- Analisar a arquitetura monolítica e discutir suas vantagens e limitações.
- Estudar os princípios do **12-Factor App** e identificar quais já são atendidos pela aplicação.
- Projetar uma arquitetura segura utilizando serviços da AWS.
- Publicar a aplicação na nuvem utilizando uma instância EC2 e um banco de dados RDS.

---

# Requisitos Técnicos

## 1. Cultura DevOps e Arquitetura

- Executar a aplicação localmente.
- Identificar por que ela é considerada um monólito.
- Discutir vantagens e desvantagens dessa arquitetura para um MVP.
- Avaliar a aderência aos princípios do 12-Factor App.

---

## 2. Arquitetura Cloud

Desenvolver um diagrama contendo:

- VPC
- Sub-redes públicas e privadas
- EC2 para hospedagem da aplicação
- RDS PostgreSQL ou MySQL
- Security Group da EC2 permitindo:
  - HTTP
  - HTTPS
  - SSH (IP específico)
- Security Group do RDS permitindo acesso apenas pela EC2.

Além disso, elaborar uma estimativa mensal de custos utilizando a AWS Pricing Calculator.

---

## 3. Implementação na AWS

Realizar o provisionamento manual da infraestrutura:

- Criar os recursos na AWS.
- Conectar à EC2 via SSH.
- Instalar as dependências da aplicação.
- Configurar as variáveis de ambiente.
- Conectar a aplicação ao banco RDS.
- Validar o acesso público da aplicação através do IP ou DNS da instância.

---

# Entregáveis

## Vídeo

Apresentar:

- Aplicação executando localmente.
- Diagrama da arquitetura.
- Aplicação publicada na EC2.
- Comunicação com o banco RDS.
- Configuração dos Security Groups.
- Gerenciamento das credenciais.

---

## Documentação

Disponibilizar:

- Diagrama da arquitetura.
- Discussão sobre os princípios do 12-Factor App.

---

## Relatório

O relatório deve conter:

- Participantes.
- Links da documentação.
- Link do vídeo.
- Principais desafios encontrados.
- Decisões tomadas durante o desenvolvimento.
- Estimativa de custos da infraestrutura AWS.

---

# Referência

Repositório base disponibilizado para o desafio:

https://github.com/dougls/toggle-master-monolith
