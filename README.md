# Clean Architecture – Project Template

Este repositório é um **template exemplo** de Clean Architecture para projetos em .NET.  
Ele **não é um framework**, nem uma solução fechada, e **não deve ser usado como boilerplate rígido**.

O objetivo é **demonstrar uma organização de projetos**, responsabilidades e limites arquiteturais
que podem ser adaptados conforme o contexto do sistema.

---

## 🎯 Objetivo do Template

Este template existe para:

- Demonstrar **separação clara de responsabilidades**
- Servir como **referência arquitetural** para projetos .NET
- Apoiar **decisões arquiteturais conscientes**
- Facilitar **testabilidade, manutenção e evolução**
- Evitar acoplamentos comuns (ex: API dependente de EF/Core ou infraestrutura vazando para o domínio)

> ⚠️ **Importante**  
> Este repositório **não tenta resolver todos os cenários** nem impor regras absolutas.  
> Clean Architecture é um **guia**, não uma receita fixa.

---

## 🧱 Estrutura de Projetos

A solução é organizada em camadas, cada uma com uma responsabilidade clara.

```
src/
 ├── Api/
 ├── Application/
 ├── Domain/
 ├── Infrastructure/
 └── Tests/
     ├── Domain.Tests
     └── Application.Tests
```

## 🧠 Visão Geral das Camadas

### 🔹 Domain

**Responsabilidade:**  
Representar o núcleo do negócio.

**Contém:**
- Entidades
- Value Objects
- Regras de negócio
- Interfaces (contratos) de repositórios
- Exceções de domínio

**Não contém:**
- Frameworks
- Acesso a banco de dados
- HTTP / Controllers
- Logging
- Dependências externas

> O domínio não sabe que o sistema é uma API nem como os dados são persistidos.

---

### 🔹 Application

**Responsabilidade:**  
Orquestrar os casos de uso do sistema.

**Contém:**
- Services / Use Cases
- DTOs
- Interfaces de serviços externos
- Regras de aplicação
- Validações de fluxo

**Aqui ficam decisões como:**
- Criar ou atualizar entidades
- Orquestrar múltiplas operações
- Coordenar chamadas a repositórios e serviços

> A camada Application depende apenas do Domain.

---

### 🔹 Infrastructure

**Responsabilidade:**  
Implementar detalhes técnicos.

**Contém:**
- Implementações de repositórios
- Persistência (SQL, MongoDB, etc.)
- Integrações externas
- Serviços de terceiros
- Configurações técnicas

Essa camada implementa interfaces definidas no Domain ou Application.

> Infrastructure é substituível.  
> Domain não deveria ser.

---

### 🔹 API

**Responsabilidade:**  
Expor o sistema para o mundo externo.

**Contém:**
- Controllers
- Filtros
- Middlewares
- Configuração de Dependency Injection
- Versionamento de API

**A API:**
- Não contém regra de negócio
- Não acessa banco diretamente
- Atua apenas como camada de entrada

---

### 🔹 Tests

Separação clara de testes por camada:

- **Domain.Tests**  
  Testa regras de negócio puras, sem dependências externas.

- **Application.Tests**  
  Testa casos de uso, fluxos e orquestrações.

---

## 🔄 Fluxo de Dependências

A principal regra da Clean Architecture:

API → Application → Domain
Infrastructure → Application / Domain (via interfaces)

**Nunca:**
- Domain → Infrastructure
- Domain → API
- Application → Infrastructure diretamente

---

## 🧩 Quando Usar Este Template

Este template é indicado quando:
- O sistema possui regras de negócio relevantes
- Existe complexidade além de CRUD
- Testabilidade é importante
- O projeto tende a crescer
- Manutenibilidade e evolução são prioridades

---

## 🚫 Quando NÃO Usar

Evite este template quando:
- O projeto é extremamente simples
- É um MVP descartável
- Scripts, automações pequenas ou provas de conceito
- APIs temporárias ou de curta duração

> Overengineering também é um problema arquitetural.

---

## ⚙️ Adapte ao Contexto

Você não precisa:
- Criar todas as camadas desde o início
- Seguir exatamente os nomes dos projetos
- Usar todas as pastas sugeridas

Use este repositório como:
- Guia
- Referência
- Base para discussão arquitetural

---

## 🧠 Filosofia

> “Arquitetura existe para proteger o negócio de mudanças técnicas.”

Se trocar:
- Banco de dados
- Framework
- Infraestrutura
- Protocolo (REST → gRPC)

…o impacto no domínio deve ser mínimo.

---

## 📌 Observações Finais

Este template representa uma interpretação prática de Clean Architecture no ecossistema .NET.  
Não é a única forma correta — e nem pretende ser.

O foco é clareza, separação de responsabilidades e evolução sustentável.
