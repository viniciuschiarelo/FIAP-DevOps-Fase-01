# 🚀 Cultura DevOps

Este módulo aborda os pilares fundamentais da Cultura DevOps, suas práticas, ferramentas de mercado e os impactos organizacionais de sua adoção.

---

## 1. Fundamentos da Cultura DevOps

### A Evolução do Mercado e a Necessidade de Agilidade
Historicamente, o setor de tecnologia operava em um cenário centralizado e com escassa concorrência, muitas vezes utilizando a metodologia **Waterfall** (Cascata). Nesse método antigo, os requisitos eram levantados no início e o desenvolvimento ocorria de forma sequencial. O grande problema era que o software demorava tanto para chegar ao cliente que os requisitos iniciais muitas vezes não faziam mais sentido. 

Grande parte dos processos eram manuais, propensos a falhas humanas e lentos. As empresas enfrentavam problemas de qualidade e *time-to-market*, perdendo o melhor momento para lançar o produto e agregar valor. Contudo, a evolução tecnológica e a saturação do mercado transformaram esse cenário, exigindo entregas com uma velocidade sem precedentes, aliadas a agilidade, segurança e resultados constantes.

### O Surgimento do DevOps e a Quebra de Silos
O termo DevOps nasce da convergência entre **Desenvolvimento (Dev)** e **Operações (Ops)**. Antes, a separação rígida (silos) entre essas equipes criava gargalos operacionais que impediam respostas rápidas às necessidades dos clientes. 

![Silos](../assets/Pasted%20image%2020260425104355.png)

O marco oficial do movimento ocorreu em 2009. Naquela época, enquanto implantações levavam semanas, a Amazon (AWS) já demonstrava capacidade de realizar múltiplos deploys diários de forma transparente, graças a uma arquitetura orientada a serviços (Microsserviços). No mesmo ano, Patrick Debois consolidou o termo ao criar o evento **DevOpsDays**.

### Cultura como Pilar Central
Diferente de uma ferramenta que se instala, o DevOps é uma **transformação cultural**. Sua essência reside na colaboração radical entre equipes, fortalecida pela automação de processos repetitivos e por uma comunicação transparente.

![Cultura DevOps](../assets/Pasted%20image%2020260425104233.png)

### Benefícios, Qualidade e Shift Left
Os ganhos dessa mentalidade refletem na redução de riscos. Ao integrar times e automatizar o pipeline, falhas são identificadas precocemente no ciclo de desenvolvimento — prática conhecida como **Shift Left** (mover os testes e a segurança para o início do processo). A qualidade das entregas é elevada por meio de testes automatizados e Integração Contínua (CI), resultando em sistemas mais estáveis.

![Shift Left](../assets/Pasted%20image%2020260425104355.png)

Além disso, um profissional DevOps deve monitorar **SLAs (Service Level Agreements)** — contratos que definem metas, prazos, métricas de desempenho e penalidades. É essencial também envolver-se com a comunidade **Open Source**, origem da maioria das ferramentas que utilizamos hoje.

---

## 2. Práticas Comuns e Ferramentas

As ferramentas de automação começaram a ganhar força no início do movimento DevOps (2009). Entre as principais vertentes, destacam-se:

### IaC (Infraestrutura como Código)
O IaC é utilizado tanto por profissionais de DevOps quanto por times de infraestrutura para provisionar e gerenciar recursos de forma automatizada (Ex: Chef, Puppet, Ansible, Terraform).
![IaC](../assets/Pasted%20image%2020260427060038.png)
![IaC](../assets/Pasted%20image%2020260427060256.png)

### Integração Contínua (CI) e Entrega Contínua (CD)
- **CI:** Aciona builds e testes de forma automatizada a cada mudança no código (Ex: Jenkins, GitLab CI, GitHub Actions).
- **CD:** Garante que o código aprovado possa ser entregue aos ambientes de produção com segurança.
![CI](../assets/Pasted%20image%2020260427060439.png)
![CI/CD](../assets/Pasted%20image%2020260427060556.png)
![CD](../assets/Pasted%20image%2020260427060751.png)

### Containerização
O uso de containers (Docker) e orquestradores (Kubernetes) permite escalabilidade elástica. Um exemplo prático é aumentar dinamicamente os containers de uma aplicação (como um portal de notícias) apenas em dias de grandes eventos esportivos para suportar o pico de acessos.
![Containers](../assets/Pasted%20image%2020260427060856.png)
![Orquestração](../assets/Pasted%20image%2020260427061053.png)

### Monitoramento, Feedback e Segurança Contínua
Para garantir a qualidade, utilizamos métricas e verificações de segurança:
- **SAST (Static Application Security Testing):** Analisa o código de forma estática antes de sua execução para encontrar vulnerabilidades.
- **DAST (Dynamic Application Security Testing):** Verifica falhas de segurança durante a execução do código/container.
![Monitoramento](../assets/Pasted%20image%2020260427061449.png)
![Segurança](../assets/Pasted%20image%2020260427061604.png)

---

## 3. Cultura Organizacional

O DevOps exige uma profunda mudança de mentalidade, desconstruindo os silos e integrando desenvolvedores, operações, QA e segurança. 

> [!WARNING]
> Ninguém faz nada sozinho. O compartilhamento de responsabilidades, dúvidas, erros e acertos é o que impulsiona a evolução.

![Organização](../assets/Pasted%20image%2020260428055943.png)
![Organização](../assets/Pasted%20image%2020260428060138.png)

O foco deve estar sempre no valor da entrega: **estabilidade do sistema, velocidade na entrega e experiência do usuário**.

### Tipos de Cultura Organizacional
![Culturas](../assets/Pasted%20image%2020260428060711.png)

- **Cultura de Clã:** Foco nas relações humanas, tratamento dos erros como aprendizado e ambiente acolhedor.
- **Cultura Adhocrática:** Traz inovação, mudanças rápidas e aposta em riscos calculados.
- **Cultura de Mercado:** Obsessão por resultados, metas agressivas e concorrência.
- **Cultura Hierárquica:** Previsibilidade, controle, cadeias de comando e processos rígidos. (É a mais desafiadora para implementar DevOps).

![Desafios](../assets/Pasted%20image%2020260428061352.png)

### Desafios da Mudança
A resistência à mudança é o maior obstáculo. A implantação de uma cultura **DevSecOps** requer treinamentos, autoavaliação, mapeamento de processos e projetos-piloto. A comunicação clara é essencial, lembrando sempre que processos antigos não desaparecem da noite para o dia.

---

## 4. Integração e Automação (Prática)

Como exemplo prático inicial de integração e automação, avaliamos um repositório (API de um Petshop) que contém um `Dockerfile`. 

![Dockerfile](../assets/Pasted%20image%2020260428121439.png)

A partir deste `Dockerfile`, implementamos um fluxo de **CI (Integração Contínua)** via **GitHub Actions**. O arquivo de receita da pipeline fica armazenado em `.github/workflows/main.yml`.

![Workflow YAML](../assets/Pasted%20image%2020260428121843.png)

Neste arquivo:
- A propriedade `on` define o gatilho da automação (ex: *push* na branch `main`).
- Em seguida, configuramos o ambiente (`runs-on`) e declaramos variáveis de segurança (Secrets).
- Os `steps` definem as ações: fazer o `checkout` do repositório, efetuar *login* em um repositório de imagens, realizar o *build* do Dockerfile e fazer o *push* para o Docker Hub.

![Steps da Pipeline](../assets/Pasted%20image%2020260428122549.png)

No GitHub, um ícone de status (ex: uma bolinha laranja) indica que a pipeline está sendo executada. Na aba `Actions`, podemos acompanhar os logs detalhados do build e envio da imagem em tempo real.

![Status do GitHub Actions](../assets/Pasted%20image%2020260428122821.png)
![Logs da Pipeline](../assets/Pasted%20image%2020260428123031.png)
