# 🏥 Sistema de Gerenciamento de Senhas - Clínica Médica

Este projeto é uma API REST desenvolvida em **NestJS** para gerenciar a emissão, chamada e controle de senhas em uma clínica médica. O sistema é modular e escalável, seguindo as boas práticas de arquitetura orientada a domínio.

---

## 📐 Arquitetura do Projeto

A aplicação segue o padrão **Modular Monolith (Domain-Centric)** do NestJS, onde cada funcionalidade é organizada em um módulo isolado contendo controller, service, DTOs e entity.

```
src/
├── main.ts                    # Ponto de entrada da aplicação NestJS
├── app.module.ts              # Módulo raiz que importa os módulos de domínio

├── senhas/                    # Geração e controle de senhas
│   ├── senha.controller.ts
│   ├── senha.service.ts
│   ├── senha.module.ts
│   ├── dto/
│   │   ├── create-senha.dto.ts
│   │   └── ...
│   └── entities/
│       └── senha.entity.ts

├── tipos-senha/               # Tipos de senha: NORMAL, PREFERENCIAL
│   ├── tipo-senha.controller.ts
│   ├── tipo-senha.service.ts
│   ├── tipo-senha.module.ts
│   └── entities/
│       └── tipo-senha.entity.ts

├── guiches/                   # Guichês de atendimento
│   ├── guiche.controller.ts
│   ├── guiche.service.ts
│   ├── guiche.module.ts
│   └── entities/
│       └── guiche.entity.ts

├── atendimentos/              # Chamadas de senhas (logs de atendimento)
│   ├── atendimento.controller.ts
│   ├── atendimento.service.ts
│   ├── atendimento.module.ts
│   └── entities/
│       └── atendimento.entity.ts

├── painel/                    # Informações exibidas no telão
│   ├── painel.controller.ts
│   ├── painel.service.ts
│   └── painel.module.ts

└── database/                  # Configuração do ORM (Prisma ou TypeORM)
    └── prisma.service.ts | typeorm.config.ts
```

---

## 🧩 Módulos e Responsabilidades

| Módulo         | Responsabilidade Principal                                              |
|----------------|--------------------------------------------------------------------------|
| `senhas`       | Geração e listagem de senhas, distinção entre normal e preferencial     |
| `tipos-senha`  | Cadastro e manutenção de tipos de senha                                 |
| `guiches`      | Cadastro dos guichês físicos da clínica                                 |
| `atendimentos` | Registra qual guichê chamou qual senha e quando                         |
| `painel`       | Fornece dados ao telão: últimas senhas, filas, tempos médios            |
| `database`     | Conexão com o banco de dados, setup de ORM, seed, migrations etc.       |

---

## 🚀 Endpoints REST principais

> Abaixo estão alguns exemplos de endpoints (a documentação Swagger pode ser ativada facilmente com `@nestjs/swagger`).

### 📥 Emissão de senha

```http
POST /senhas
Body:
{
  "tipo": "PREFERENCIAL"
}
```

### 🧾 Listagem de senhas na fila

```http
GET /painel/filas
```

### ⏱️ Tempo médio de espera

```http
GET /painel/tempo-medio
```

### 📣 Chamada de senha por guichê

```http
POST /atendimentos
Body:
{
  "guicheId": 1,
  "senhaId": 42
}
```

---

## ⚙️ Tecnologias Utilizadas

- **NestJS** (framework principal)
- **TypeScript**
- **Prisma**
- **PostgreSQL**
- **Swagger** (`@nestjs/swagger`) para documentação automática

---

## 📄 Licença

Este projeto está licenciado sob os termos da **MIT License**.

---
