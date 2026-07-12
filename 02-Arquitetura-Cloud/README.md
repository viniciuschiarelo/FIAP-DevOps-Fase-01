# ☁️ Arquitetura Cloud

Este módulo aborda os fundamentos da computação em nuvem, desde os modelos de serviço e implantação até as melhores práticas de arquitetura, resiliência, segurança e otimização de custos (FinOps).

---

## 1. Introdução à Computação em Nuvem

A computação em nuvem oferece a capacidade de solicitar e liberar recursos tecnológicos sob demanda através da internet, eliminando a necessidade de manter data centers físicos locais caros e complexos. 

A grande vantagem sobre a TI tradicional é a **facilidade de escalar**. Enquanto em um modelo tradicional o aumento de infraestrutura para um evento específico pode levar semanas (compra e configuração de servidores), na nuvem esse processo ocorre em minutos ou de forma totalmente automatizada.

### Escalabilidade vs. Elasticidade
- **Escalabilidade Vertical (Scale Up):** Aumentar os recursos (CPU, RAM) de uma máquina existente.
- **Escalabilidade Horizontal (Scale Out):** Adicionar novas máquinas (instâncias) para dividir a carga de trabalho.
- **Elasticidade:** É a capacidade do sistema de realizar esse escalonamento (aumentar ou diminuir recursos) de forma *automática* baseada na demanda (ex: **Auto Scaling Group**).

### Modelos de Implantação
1. **Nuvem Pública:** Infraestrutura compartilhada por múltiplos clientes, acessada via internet. Os recursos físicos são compartilhados, mas os ambientes são logicamente isolados.
2. **Nuvem Privada:** Servidor físico e recursos totalmente dedicados e exclusivos para uma única organização.
3. **Nuvem Híbrida:** Combinação de nuvem pública e privada. Dados sensíveis podem ficar no ambiente privado, enquanto aplicações de grande escala rodam no ambiente público.

> [!NOTE]
> "Não se apaixone pela plataforma, se apaixone pelo problema que você irá resolver."

---

## 2. Modelos de Serviço em Nuvem (IaaS, PaaS, SaaS e FaaS)

Os modelos de serviço definem o nível de responsabilidade e controle que o usuário tem sobre a infraestrutura:

### IaaS (Infrastructure as a Service)
O provedor entrega os componentes virtuais (servidores, redes, armazenamento). O usuário tem controle total sobre o Sistema Operacional e a aplicação. 
- **Cenário ideal:** Migrações do tipo *lift-and-shift* (mover máquinas locais para a nuvem sem grandes alterações) ou quando se necessita de controle total da máquina.

### PaaS (Platform as a Service)
O provedor gerencia toda a infraestrutura subjacente (hardware e SO). O foco do usuário é apenas desenvolver e gerenciar a aplicação e seus dados.
- **Cenário ideal:** Bancos de dados gerenciados (RDS) e clusters de Kubernetes gerenciados, acelerando a entrega (*time-to-market*).

### SaaS (Software as a Service)
O nível máximo de abstração. O software é entregue pronto para o usuário final (Ex: Netflix, Spotify, Office 365).

### FaaS (Function as a Service) / Serverless
A infraestrutura é completamente invisível para o desenvolvedor. As funções de código ficam em estado de "repouso" e são executadas apenas quando acionadas por um gatilho (evento). O cliente paga apenas pelo milissegundo de execução.
- **Cenário ideal:** Tarefas curtas, automações, otimização extrema de custos e escalabilidade infinita sem gerenciamento de servidores (Ex: AWS Lambda).

---

## 3. Infraestrutura e Resiliência em Nuvem

### Componentes Físicos
- **Regiões:** Áreas geográficas globais (ex: São Paulo, Virgínia).
- **Zonas de Disponibilidade (AZs):** Centros de dados fisicamente isolados dentro de uma mesma região, garantindo que falhas em um data center não afetem o outro.

### Alta Disponibilidade e Recuperação de Desastres (DR)
- **Load Balancers:** Distribuem o tráfego de entrada entre várias instâncias para evitar sobrecargas (atuando nas camadas L4 ou L7 da rede).
- **Failover Automático:** Transferência automática de tráfego de um servidor com falha para um backup. Pode ser **Ativo-Passivo** (o secundário fica aguardando) ou **Ativo-Ativo** (ambos recebem tráfego simultaneamente).
- **Disaster Recovery (DR):** Estratégia de manter réplicas de ambientes em regiões distintas para continuidade de negócios. Definições importantes incluem **RPO** (quanto dado se aceita perder) e **RTO** (quanto tempo até voltar ao ar).

### Resiliência e Autocura (Self-Healing)
Padrões como o **Circuit Breaker** impedem que chamadas sucessivas a serviços inativos causem falhas em cascata. O uso de **filas de mensageria** (Kafka, RabbitMQ) atua como um *buffer* para picos de requisições.

---

## 4. Principais Provedores (AWS, GCP, Azure, OCI) e Estratégia Multi-Cloud

O mercado é liderado por grandes players, cada um com seus pontos fortes:
- **AWS:** Pioneira, possui a maior gama de serviços maduros e infraestrutura global consolidada.
- **Microsoft Azure:** Forte integração corporativa (Active Directory, Office 365) e nuvem híbrida.
- **Google Cloud (GCP):** Referência em Kubernetes, Analytics, Big Data e Inteligência Artificial.
- **Oracle Cloud (OCI):** Foco em cargas críticas, alta performance de bancos de dados relacionais.

### Multi-Cloud vs Single-Cloud
- **Single-Cloud:** Mais fácil de gerenciar, porém cria o risco de *Vendor Lock-in* (dependência de um único fornecedor).
- **Multi-Cloud:** Utiliza serviços de múltiplos provedores (ex: banco na Oracle, aplicação na AWS). Oferece flexibilidade e redução de riscos, mas aumenta a complexidade de rede e os custos de gestão de equipe.

---

## 5. Elementos da Arquitetura Cloud e Cloud Native

### O que é Cloud Native?
Sistemas projetados nativamente para a nuvem. Caracterizam-se pelo uso de:
- **Microsserviços**
- **Containers** (Docker/Kubernetes)
- **Infraestrutura Imutável** (IaC)
- **APIs**

### Redes e Armazenamento (VPC e Storage)
- **VPC (Virtual Private Cloud):** Criação de ambientes de rede isolados, divididos em **sub-redes públicas** (acesso à internet) e **sub-redes privadas** (bancos de dados).
- **Gateways e Roteamento:** Controle estrito de entrada e saída (Internet Gateway, NAT Gateway).
- **Armazenamento:** 
  - *Object Storage:* Imagens, vídeos, backups (S3).
  - *Block Storage:* Discos rígidos atrelados às VMs (EBS).
  - *File Storage:* Armazenamento compartilhado em rede (EFS).

---

## 6. Segurança, Custos (FinOps) e Boas Práticas

### Modelo de Responsabilidade Compartilhada
- **Provedor:** Responsável pela segurança *DA* nuvem (Data centers físicos, hardware, virtualização, infraestrutura de rede global).
- **Cliente:** Responsável pela segurança *NA* nuvem (Aplicações, SO das VMs, dados, configurações de firewall e gestão de acessos).

### Segurança em Profundidade
- **Gestão de Identidade:** Conceder o "menor privilégio possível".
- **MFA (Multifator):** Obrigatório para acessos críticos.
- **Criptografia:** 
  - *Em trânsito:* TLS/SSL (HTTPS).
  - *Em repouso:* Criptografia de discos e bancos de dados (ex: KMS).
- **Proteção de Rede:** Security Groups (filtros de porta de instâncias) e WAF (Web Application Firewall) para bloqueio de ataques web comuns como SQL Injection.

### Gestão de Custos (FinOps)
Na nuvem, os custos podem crescer rapidamente devido à elasticidade. O **FinOps** (Finanças + Operações de TI) atua criando:
1. **Visibilidade:** Uso de tags e relatórios para saber qual departamento gera cada gasto.
2. **Otimização:** Desligar ambientes de homologação aos finais de semana, usar "Instâncias Spot" para workloads não críticos.
3. **Governança e Alertas:** Criação de orçamentos (Budgets) que alertam a equipe antes de atingir limites de gastos.

### Well-Architected Framework
Conjunto de melhores práticas para avaliar arquiteturas na nuvem, baseando-se em pilares como: **Segurança, Confiabilidade, Otimização de Custos, Excelência Operacional, Eficiência de Performance e Sustentabilidade**.
