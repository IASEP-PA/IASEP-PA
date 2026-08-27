### 🌿 GitFlow — Estratégia de Branches

Os projetos do IASEP devem utilizar uma estratégia de gerenciamento de branches que permita organização do desenvolvimento, rastreabilidade, revisão de código, controle de mudanças e implantação segura entre os ambientes DEV, HML e PRD.

A estratégia recomendada é baseada no modelo GitFlow, adaptado às necessidades de ambientes corporativos e institucionais.

### 🏗️ Estrutura de Branches

```

┌──────────────┐
│     main     │
│   PRODUÇÃO   │
└──────▲───────┘
       │
    release/*
       │
┌──────┴───────┐
│    develop   │
│      HML     │
└──────▲───────┘
       │
    feature/*
       │
┌──────┴───────┐
│   Developer  │
└──────────────┘

```

### 📌 Branches principais
Branch	Finalidade	Ambiente
main	Código estável em produção	PRD
develop	Integração das funcionalidades	DEV/HML
feature/*	Desenvolvimento de novas funcionalidades	DEV
release/*	Preparação de uma nova versão	HML
hotfix/*	Correção emergencial de produção	PRD

### 🔵 main

A branch main representa o estado oficial e estável da aplicação em produção.

Características:

- Não deve receber commits diretamente;
- Alterações somente através de Pull Request;
- Deve possuir proteção de branch;
- Deve exigir revisão de código;
- Deve executar pipeline de CI/CD;
- Deve permitir rastreabilidade das versões;
- Deve possuir tags para releases;
- Deve representar sempre uma versão potencialmente implantável em produção.

Exemplo:
```
main
│
├── v1.0.0
├── v1.1.0
├── v1.2.0
└── v2.0.0
```
---
### 🟢 develop

A branch develop representa a integração das alterações que estão sendo desenvolvidas.

Características:

- Recebe Pull Requests das branches feature/*;
- Deve passar por validações automatizadas;
- Pode ser utilizada para implantação no ambiente DEV;
- Deve permanecer em estado funcional;
- Não deve receber alterações diretamente.

Fluxo:

```
feature/*
  │
  │
Pull Request
  ▼
develop
  │
  ▼
 DEV
```
---
### 🟡 feature/*

Branches feature/* são utilizadas para desenvolvimento de novas funcionalidades, melhorias ou alterações planejadas.

Padrão:
```
feature/<identificador>-<descricao>
```
Exemplos:
```
feature/123-criar-api-beneficiario
feature/456-integracao-keycloak
feature/789-dashboard-monitoramento
```
Fluxo:
```
git checkout develop

git pull origin develop

git checkout -b feature/123-criar-api-beneficiario
```
Após concluir o desenvolvimento:
```
git add .
git commit -m "feat: implementa API de beneficiários"

git push -u origin feature/123-criar-api-beneficiario
```
Em seguida, deve ser aberto um Pull Request para develop.

---
### 🟠 release/*

Branches release/* são utilizadas para preparar uma nova versão que será promovida para produção.

Padrão:

release/<versao>

Exemplo:

release/1.4.0

Fluxo:
```
develop
   │
   │ Pull Request
   ▼
release/1.4.0
   │
   ▼
  HML
   │
   ├── Testes
   ├── Homologação
   ├── Segurança
   └── Validação
   │
   ▼
 main
   │
   ▼
 PRD
```
Durante uma release/*, devem ser priorizados:

- Correções de bugs;
- Ajustes de configuração;
- Testes;
- Validações;
- Documentação;
- Atualização de versão.

Novas funcionalidades devem retornar para feature/* e não ser incluídas diretamente durante a estabilização da release.
