# 📝 Exercícios e Desafios Práticos

Este módulo compila os desafios e estudos de caso resolvidos durante a Fase 1 da pós-graduação, focando na aplicação prática dos conceitos de Cultura DevOps, Arquitetura Cloud e AWS.

---

## Desafio 1: Plano de Implantação DevOps

**Proposta:** Atuar como consultor(a) para estruturar um plano estratégico de transformação cultural e técnica em uma empresa. O objetivo é promover integração contínua, infraestrutura como código (IaC), monitoramento e colaboração.

### Diagnóstico Inicial e Objetivos
A empresa atual conta com 15 desenvolvedores e infraestrutura legada (*on-premises*). Há uma separação clara entre as equipes, deploys manuais e ausência de automação de testes ou conteinerização (exigindo configurações demoradas nas máquinas locais dos novos devs). As modificações em banco de dados são feitas diretamente em produção.

**Objetivos Esperados:**
- Mitigar as divergências entre ambientes (dev/homolog/prod) padronizando o ambiente de desenvolvimento.
- Reduzir *bugs* em produção e retrabalho através de automação de testes (CI).
- Acelerar as entregas e garantir previsibilidade com Infraestrutura como Código.

### Plano de Ação e Stack
- **CI/CD:** Aproveitamento do Jenkins e GitLab já existentes no ambiente para rodar testes unitários a cada commit.
- **Ambiente Local e Isolamento:** Adoção de **Docker** para garantir que a máquina de desenvolvimento funcione de forma idêntica ao servidor.
- **Provisionamento:** Implementação de IaC via **Ansible/Terraform** para gerenciar as configurações dos servidores on-premises.
- **Observabilidade:** Monitoramento da aplicação Node.js usando **Prometheus** e **Grafana**.
- **Cultura:** Rituais de liderança e *blameless post-mortems* (análises sem apontar culpados) para transformar incidentes em oportunidades de melhoria.

> [!NOTE]
> **Provocações Críticas para Evolução do Plano:**
> Apenas testes unitários não resolvem todos os bugs (testes ponta-a-ponta/E2E são necessários). O uso de IaC para o servidor perde sua força se as mudanças no banco de dados continuarem sendo feitas de forma manual, evidenciando a necessidade de versionamento do banco (ex: *Flyway*).

---

## Desafio 2: Arquitetura em Nuvem para E-commerce

**Proposta:** Desenvolver uma arquitetura em nuvem para a startup "InovaSoluções Tech", focada em alta disponibilidade (picos sazonais como Black Friday), segurança e otimização de custos.

### A Arquitetura Proposta (AWS)
A **AWS** foi escolhida devido à maturidade, extensa presença global (reduzindo a latência global) e vasta opção de serviços gerenciados.

1. **Computação e Serviços (Modelos):**
   - **PaaS / Containers:** O *core* da aplicação (APIs e Back-end) rodaria em **EKS** (Kubernetes) ou **ECS** para orquestração.
   - **FaaS (Serverless):** O AWS Lambda é a escolha perfeita para gerenciar as rotinas de notificações, envio de emails e filas, escalando instantaneamente durante picos (Black Friday).
   - *Lição Aprendida:* Aplicações críticas não precisam usar necessariamente IaaS. Serviços gerenciados e PaaS são extremamente resilientes.

2. **Armazenamento e Banco de Dados:**
   - **S3 (Object Storage):** Para imagens de produtos, logs e backups.
   - **Banco de Dados (PaaS):** Um **Amazon Aurora PostgreSQL** (escalável e seguro) seria o banco principal. Para catálogos massivos e rápidos, a expansão futura adotaria **DynamoDB** (NoSQL).
   
3. **Escalabilidade, Rede e Alta Disponibilidade:**
   - A rede consistiria em uma VPC contendo **Sub-redes Públicas** (para os *Application Load Balancers* e *NAT Gateways*) e **Sub-redes Privadas** (para isolar completamente o banco de dados e as instâncias de processamento).
   - Uso de **Auto Scaling** integrado aos Load Balancers e distribuição através de múltiplas **Zonas de Disponibilidade (Multi-AZ)**.
   - Para usuários globais, o **CloudFront (CDN)** faria o cache dos assets, reduzindo drasticamente o tempo de carregamento na ponta final.
   - Estratégias de Recuperação de Desastres (DR) avaliadas: *Backup and Restore*, *Warm Standby*.

4. **Segurança (Modelo de Responsabilidade Compartilhada):**
   - **Acesso:** IAM com MFA e princípio do menor privilégio.
   - **Rede e Borda:** Security Groups (firewall em nível de instância), *Network ACLs* (nível sub-rede) e **AWS WAF** para bloquear injeções SQL e DDoS na camada HTTP.
   - **Criptografia:** TLS em trânsito (via AWS Certificate Manager) e AES-256 em repouso (gerenciado pelo AWS KMS).
   - *Lembrete:* A AWS protege a *nuvem* (datacenters, hardware). O usuário protege *na nuvem* (dados, IAM, código).

5. **FinOps (Governança de Custos):**
   - Uso intensivo de **Tags** para identificar custos por ambiente, time ou projeto.
   - *Right-sizing* (escolha do tamanho exato da máquina) e **Spot Instances** para cargas de trabalho secundárias tolerantes a falhas.
   - Acompanhamento via **AWS Cost Explorer** e **Budgets** para gerar alertas automáticos de gastos.
