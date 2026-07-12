# 🏗️ Arquitetura de Aplicações

Neste módulo, exploramos os diferentes estilos arquiteturais para desenvolvimento de software, comparando Monolitos e Microsserviços, além de analisar padrões de comunicação e persistência de dados em ambientes distribuídos.

---

## 1. Arquitetura Monolítica

O Monolito refere-se a um design de software onde todos os componentes de uma aplicação (Interface, Regras de Negócio e Acesso a Dados) são interligados em uma única unidade implantável (Deploy) e compartilham um único banco de dados.

### Estudo de Caso: Amazon Prime Video
Curiosamente, a decisão arquitetural nem sempre segue a tendência de "separar tudo". A Amazon Prime Video migrou uma parte do seu serviço de monitoramento de qualidade de vídeo de uma arquitetura de microsserviços (baseada em AWS Lambda e Step Functions) de volta para um Monólito. O motivo? O alto volume de comunicação entre os serviços serverless gerava latência e altos custos. A volta para o Monolito resultou em uma **redução de custos superior a 90%** e melhorou a escalabilidade do sistema específico.

![Arquitetura Monolítica](../assets/Pasted%20image%2020260517190353.png)

### Desafios do Monolito
Embora simples no início, monolitos apresentam desafios conforme o sistema cresce:
- **Baixa Escalabilidade:** O sistema deve ser escalado por completo, mesmo que apenas uma funcionalidade específica demande mais recursos.
- **Alto Acoplamento e Manutenção Difícil:** Alterações em uma área podem afetar outras partes inesperadamente, dificultando a adoção de novas tecnologias.
- **Testes e Deploy:** O tempo de deploy aumenta e falhas isoladas (ex: sobrecarga em uma rota) podem derrubar a aplicação inteira.

*Nota sobre Monolitos Distribuídos:* Quando dividimos a aplicação em múltiplas APIs (ex: API Web e API Mobile) mas ambas continuam acessando e dependendo da mesma base de dados central, ainda temos um Monolito, porém distribuído.

![Monolito Distribuído](../assets/Pasted%20image%2020260517191559.png)

---

## 2. Microsserviços

Microsserviços são uma abordagem onde o software é composto de pequenos serviços independentes que se comunicam por meio de APIs. Cada serviço é autônomo, possuindo seu próprio ciclo de deploy e banco de dados.

![Arquitetura de Microsserviços](../assets/Pasted%20image%2020260518202312.png)

### Vantagens
- **Independência:** Equipes podem trabalhar, testar e realizar deploys de forma descentralizada.
- **Flexibilidade Tecnológica:** Diferentes serviços podem usar diferentes linguagens ou frameworks de acordo com a necessidade (ex: Python para IA, Go para performance).
- **Escalabilidade Granular:** Pode-se escalar apenas o serviço que sofre pressão (ex: escalar apenas o serviço de pagamentos na Black Friday).

### Desafios e Como Construir
- **Governança:** A flexibilidade pode gerar falta de padronização.
- **Definição de Limites:** Definir onde um serviço começa e termina é complexo. Utiliza-se técnicas de *Domain-Driven Design (DDD)*, identificando *Bounded Contexts* e realizando Modelagem Tática (Agregados, Entidades) para manter a coesão.

![Modelagem Tática](../assets/Pasted%20image%2020260519055746.png)

---

## 3. Persistência de Dados em Microsserviços

Em microsserviços, a regra de ouro é: **Cada serviço deve gerenciar seu próprio banco de dados**. Isso garante autonomia, mas introduz grande complexidade na persistência e consistência dos dados.

### Transações Distribuídas e Teorema CAP
Não podemos mais contar com transações ACID tradicionais abrangendo toda a aplicação. A garantia de consistência forte entre vários bancos compromete a disponibilidade (Teorema CAP). 
Solução: Aceitar a **consistência eventual** (os dados se alinharão ao longo do tempo) e utilizar padrões como **Sagas** para coordenar transações entre múltiplos serviços.

- **SQL:** Prioriza consistência e transações (ACID).
- **NoSQL:** Flexível, escala bem horizontalmente, geralmente focado em disponibilidade e particionamento.

![Teorema CAP](../assets/Pasted%20image%2020260519203301.png)

### Padrões de Cache
O Cache reduz a carga nos bancos de dados:
- **Cold Cache:** A aplicação busca o dado. Se não achar no cache, vai ao banco, atualiza o cache e retorna.
- **Hot Cache:** O cache é preenchido e atualizado de forma proativa (através de eventos) antes mesmo que a aplicação solicite.

![Cold Cache](../assets/Pasted%20image%2020260519203534.png)
![Hot Cache](../assets/Pasted%20image%2020260519203708.png)

---

## 4. Comunicação entre Microsserviços

A forma como os serviços conversam define a performance e resiliência do sistema.

### Síncrona vs. Assíncrona
- **Síncrona (HTTP/REST, gRPC):** O serviço A chama o serviço B e aguarda a resposta. Cria acoplamento temporal e, se o B falhar, o A pode falhar também.
- **Assíncrona (Mensageria/Eventos):** O serviço A publica uma mensagem em um *broker* (como RabbitMQ ou Kafka) e continua seu trabalho. O serviço B consome a mensagem quando puder. Isso garante maior resiliência e independência.

![Comunicação](../assets/Pasted%20image%2020260520055652.png)

### API Gateway
Em vez de clientes (front-end) se conectarem diretamente a dezenas de microsserviços, utiliza-se um **API Gateway** como ponto central. Ele roteia requisições, unifica respostas e centraliza autenticação, segurança e rate limiting.

![API Gateway](../assets/Pasted%20image%2020260520060313.png)
