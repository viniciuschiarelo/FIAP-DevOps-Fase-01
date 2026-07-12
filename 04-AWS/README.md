# ☁️ Amazon Web Services (AWS)

Este módulo consolida os aprendizados práticos e teóricos sobre os principais serviços da AWS, abrangendo desde conceitos básicos de infraestrutura até arquiteturas Serverless, Segurança e Monitoramento.

---

## 1. Primeiros Passos e IAM (Identity and Access Management)

O console da AWS é a porta de entrada para o provisionamento. Utilizando o *Free Tier* (Nível Gratuito), é possível testar diversos recursos sem custos, desde que as configurações respeitem os limites documentados pela plataforma. 

A segurança base (Identity and Access Management - IAM) é a primeira etapa de qualquer projeto:
- **Conta Root:** A conta principal deve ser protegida (com MFA) e utilizada apenas para faturamento e gestão geral, nunca para provisionamento diário.
- **Usuários, Grupos e Políticas:** O acesso deve seguir o princípio do **menor privilégio**. A prática recomendada é criar Grupos de Usuários (ex: *Dev*, *Infra*, *Sec*) com políticas de acesso específicas e, em seguida, associar os usuários a esses grupos.
- **MFA (Multifator):** Obrigatório para garantir a integridade da conta.

---

## 2. Redes e Conectividade (VPC)

A **VPC (Virtual Private Cloud)** é onde criamos nosso ambiente de rede isolado.
- **Comunicação Privada:** Recomenda-se que a comunicação interna das aplicações permaneça em redes privadas.
- **VPC Endpoints:** Permitem conectar serviços da AWS de forma segura sem trafegar pela internet pública. Por exemplo, um *Gateway Endpoint* para o S3 garante que instâncias em sub-redes privadas conversem com o bucket S3 utilizando rotas internas da AWS, aumentando a segurança e reduzindo custos de NAT Gateway.

---

## 3. Computação: EC2, Containers e Serverless

### EC2 (Elastic Compute Cloud)
O EC2 fornece máquinas virtuais escaláveis. O provisionamento inclui a escolha do sistema operacional (AMI), tipo de instância (ex: `t2.micro`), rede, e armazenamento.
- **Security Groups:** Funcionam como um firewall em nível de instância, onde definimos regras de *entrada* e *saída* (ex: liberar apenas a porta 80 para HTTP e a 22 para SSH via IP restrito).
- **Auto Scaling Group e Load Balancers (ALB):** O Application Load Balancer distribui o tráfego de usuários entre múltiplas instâncias EC2. Em conjunto com o Auto Scaling, garante que novas máquinas subam automaticamente quando o uso de CPU atinge um limite definido (ex: 70%), mantendo a aplicação elástica e tolerante a falhas.
- **Modelos de Contratação:** Sob Demanda, Reservada, Spot (baixo custo, mas sujeita a interrupções) e Dedicada.

### Containers: ECS vs EKS
Para isolar a aplicação, usamos containers (Docker).
- **ECS (Elastic Container Service):** Serviço nativo da AWS, mais simples. Ideal para quem está começando ou não precisa da complexidade do Kubernetes.
- **EKS (Elastic Kubernetes Service):** Kubernetes gerenciado pela AWS. É a escolha para plataformas mais robustas.
- **Fargate:** Modelo *Serverless* para containers. Nele, a AWS gerencia a infraestrutura subjacente, e pagamos apenas por vCPU e Memória utilizados pelo container (Task), sem necessidade de gerenciar servidores.

### Serverless: Lambda e API Gateway
- **AWS Lambda:** Execução de código orientada a eventos sem servidor. Pagamos apenas pelo tempo (em milissegundos) que o código executa.
- **API Gateway:** Ponto central de entrada para a aplicação. Ele expõe endpoints HTTP de forma segura, orquestrando chamadas ao Lambda (ou outros serviços), realizando autenticação, proteção contra DDoS e limitando o tráfego (*Rate Limiting*).

---

## 4. Persistência: Bancos de Dados e S3

### Amazon RDS e Aurora
- **RDS:** Banco de dados relacional gerenciado (MySQL, PostgreSQL). Tira o fardo de configurar o cluster e gerenciar backups, deixando o foco nos dados. 
- **Aurora:** Banco relacional otimizado para a nuvem da AWS, sendo muito mais rápido e oferecendo failover nativo e armazenamento que cresce automaticamente.

> [!WARNING]
> Nunca deixe um banco de dados aberto publicamente (0.0.0.0/0). O correto é posicionar o RDS numa sub-rede privada e liberar o acesso *apenas* para o Security Group da aplicação (ex: EC2 ou Lambda).

### Amazon DynamoDB
Banco de dados nativo da AWS, NoSQL (Chave-Valor) totalmente *Serverless*. Excelente para acessos extremamente rápidos e em grande escala, onde a estrutura de dados é flexível. Pagamento por requisição/demanda.

### Amazon S3 e CloudFront (CDN)
- **S3:** Armazenamento de objetos (imagens, backups) escalável. Também utilizado para hospedagem de sites estáticos. O acesso deve ser bloqueado para o público em cenários corporativos sensíveis.
- **CloudFront (CDN):** Rede de distribuição de conteúdo que faz *cache* de aplicações estáticas nos pontos mais próximos do usuário, reduzindo a latência global. Quando integrado ao S3, o bucket S3 fica privado e a CDN atua como única porta de entrada segura.

---

## 5. Segurança, Monitoramento e Gerenciamento

### CloudWatch (Logs e Métricas)
- **Métricas:** Mostram a "saúde" do sistema (uso de CPU, RAM, requisições). O *CloudWatch Agent* pode ser instalado no EC2 para capturar métricas customizadas de memória.
- **Logs:** Essenciais para investigações e troubleshooting de falhas (*Logs Insights* permite criar queries complexas).
- **Alarmes:** Gatilhos para nos alertar por e-mail ou disparar o Auto Scaling.

### Serviços de Proteção e Governança
- **AWS Secrets Manager:** Onde armazenamos credenciais e chaves de APIs. Evita senhas *hardcoded* no código e permite rotação automática.
- **AWS WAF (Web Application Firewall):** Protege contra *exploits* na web e *SQL Injection*.
- **ACM (AWS Certificate Manager):** Emissão e gestão de certificados SSL/TLS, garantindo tráfego criptografado (HTTPS).
- **Route 53:** Serviço gerenciado de DNS da AWS (para criação de zonas hospedadas e apontamento de domínios).

---

## 6. Certificações AWS

O aprendizado guiado focado em certificações (como o promovido pelo AWS Academy) acelera a carreira. A AWS possui 4 níveis de certificações, que atestam a fluência e experiência do profissional na plataforma:
1. **Foundational** (Cloud Practitioner)
2. **Associate** (Solutions Architect, Developer, SysOps)
3. **Professional** (Solutions Architect Pro, DevOps Eng)
4. **Specialty** (Security, Database, Machine Learning, etc)
