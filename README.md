# arquitetura-software
Conceitos básicos de arquitetura de software.

# Arquiteturas em Grande Escala e Arquiteturas Complexas

## 1. O que são **Large-Scale Architectures**?

Arquiteturas em **grande escala** referem-se ao design de sistemas capazes de lidar com:

- **Milhões de usuários simultâneos**  
- **Altos volumes de dados**  
- **Escalabilidade horizontal** (adicionar servidores para aumentar capacidade)  
- **Disponibilidade global e alta confiabilidade**  

Essas arquiteturas aparecem em sistemas como:

- Redes sociais (Facebook, Twitter)  
- Plataformas de streaming (Netflix, Spotify)  
- E-commerces de grande porte (Amazon, Mercado Livre)  

### Características principais:

- **Microservices**: divisão do sistema em serviços menores e independentes  
- **Load Balancers**: distribuem requisições entre múltiplos servidores  
- **Cache distribuído**: Redis, Memcached ou CDN para reduzir latência  
- **Bancos de dados distribuídos**: Cassandra, DynamoDB, CockroachDB  
- **Alta disponibilidade**: replicação de dados, failover automático  

### Exemplo em diagrama:

```mermaid
graph TD
    User[Usuário] --> LB[Load Balancer]
    LB --> S1[Serviço de Autenticação]
    LB --> S2[Serviço de Produtos]
    LB --> S3[Serviço de Pagamentos]
    
    S1 --> DB1[(Banco de Dados Usuários)]
    S2 --> Cache[Cache Redis]
    S2 --> DB2[(Banco de Dados Produtos)]
    S3 --> DB3[(Banco de Dados Pagamentos)]
```

## 2. O que são **Complex Architectures**?

Arquiteturas **complexas** são aquelas em que a **interconexão entre componentes** cria dificuldades de:

- **Manutenção**  
- **Evolução do sistema**  
- **Entendimento da lógica de negócios**  

Um sistema pode ser **grande** mas **não necessariamente complexo** se for bem projetado.  
A **complexidade surge** quando há:

- **Dependências excessivas entre módulos**  
- **Regras de negócio distribuídas em vários lugares**  
- **Integração com múltiplos sistemas externos**  
- **Camadas de abstração demais ou mal planejadas**  

### Exemplos de complexidade:
- Uma API que depende de 5 outros serviços externos para responder.  
- Código com **forte acoplamento**, em que mudar um módulo quebra outros.  
- Sistemas legados com camadas mal documentadas.  

### Exemplo em diagrama:
```mermaid
graph LR
    A[Frontend] --> B[API Gateway]
    B --> C[Serviço de Autenticação]
    B --> D[Serviço de Pagamentos]
    D --> E[Serviço Bancário Externo]
    D --> F[Serviço de Notificações]
    F --> G[Serviço de SMS]
    F --> H[Serviço de Email]
```

## 3. Diferenças entre Large-Scale e Complex

| Aspecto               | Large-Scale (Grande Escala)                     | Complex (Complexa)                            |
|------------------------|-----------------------------------------------|-----------------------------------------------|
| **Foco**              | Escalabilidade, performance, alta disponibilidade | Estrutura, dependências e organização interna |
| **Problema principal** | Como atender milhões de usuários               | Como manter e evoluir o sistema sem perder controle |
| **Exemplo real**       | Netflix suportando bilhões de streams/dia     | Sistema bancário com dezenas de integrações legadas |
| **Solução comum**      | Microservices, balanceadores, sharding        | Refatoração, design patterns, Domain-Driven Design (DDD) |

---

## 4. Boas práticas para lidar com ambos

✅ **Em Large-Scale**:  
- Usar **infraestrutura na nuvem** (AWS, GCP, Azure)  
- Projetar para **resiliência** (retry, circuit breaker, replicação)  
- Monitoramento e observabilidade (Prometheus, Grafana, ELK)  

✅ **Em Complex Architectures**:  
- **Domain-Driven Design (DDD)** → organiza a lógica de negócio  
- **Event-driven architecture** → desacopla serviços  
- **Documentação clara** e diagramas de dependência  
- **Automatizar testes e CI/CD**
