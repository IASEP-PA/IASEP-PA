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
│    staging   │
│  HOMOLOGAÇÃO │
└──────▲───────┘
       │
    feature/*
       │
┌──────┴─────────┐
│   Developer    │
│ DESENVOLVIMENTO│
└────────────────┘

```

### 📌 Branches principais

Branches Principais (Fixas)
Branch	| Finalidade	| Ambiente
:------| :--------: | :--------:
`main`	| Código estável em produção	| PRD
`staging` | Testes finais | HML
`develop`	| Integração das funcionalidades	| DEV

Branches Temporárias (variavéis)
Branch	| Finalidade	| Ambiente
:-----| :-------: | :---------:
`feature/*`	| Desenvolvimento de novas funcionalidades	| DEV
`release/*`	| Preparação de uma nova versão	| HML
`hotfix/*`	| Correção emergencial de produção	| PRD

### 🔵 main

A branch `main` representa o estado oficial e estável da aplicação em produção.

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
###  Staging
A branch `staging` representa a replica do ambiente de produção para a realização de testes e validações.

Características:

- Recebe Pull Requests das branches `release/*`;
- Deve passar por validações automatizadas;
- Pode ser utilizada para implantação no ambiente HML;
- Deve permanecer em estado funcional;
- Não deve receber alterações diretamente.

Fluxo:
```
release/*
  │
  │
Pull Request
  ▼
staging
  │
  ▼
 HML
```

---
### 🟢 develop

A branch `develop` representa a integração das alterações que estão sendo desenvolvidas.

Características:

- Recebe Pull Requests das branches `feature/*`;
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

Branches `feature/*` são utilizadas para desenvolvimento de novas funcionalidades, melhorias ou alterações planejadas.

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

Branches `release/*` são utilizadas para preparar uma nova versão que será promovida para produção.

Padrão:

```
release/<versao>
```

Exemplo:

```
release/1.4.0
```

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
Durante uma `release/*`, devem ser priorizados:

- Correções de bugs;
- Ajustes de configuração;
- Testes;
- Validações;
- Documentação;
- Atualização de versão.

Novas funcionalidades devem retornar para `feature/*` e não ser incluídas diretamente durante a estabilização da release.

---
### 🔴 hotfix/*

Branches `hotfix/*` são destinadas a correções emergenciais em produção.

Padrão:
```
hotfix/<versao>-<descricao>
```

Exemplo:
```
hotfix/1.4.1-corrigir-autenticacao
```

Fluxo:
```
                ┌──────────────┐
                │     main     │
                │     PRD      │
                └──────┬───────┘
                       │
                       ▼
              hotfix/1.4.1-xxx
                       │
                       ▼
                 Testes/CI
                       │
                       ▼
                  Pull Request
                       │
              ┌────────┴────────┐
              ▼                 ▼
            main             develop
              │
              ▼
             PRD
```
O hotfix deve ser utilizado somente quando a correção não puder aguardar o ciclo normal de uma nova release.


### 🔄 Fluxo completo

O fluxo recomendado para os projetos do IASEP é:

```
                         ┌───────────────┐
                         │     main      │
                         │     PRD       │
                         └───────▲───────┘
                                 │
                              release
                                 │
                         ┌───────┴───────┐
                         │    develop    │
                         │    DEV/HML    │
                         └───────▲───────┘
                                 │
                              feature
                                 │
                         ┌───────┴───────┐
                         │    Developer  │
                         └───────────────┘
```
Fluxo de uma funcionalidade

```
1. Criar Issue
       │
       ▼
2. Criar feature/*
       │
       ▼
3. Desenvolvimento
       │
       ▼
4. Testes locais
       │
       ▼
5. Pull Request
       │
       ▼
6. Code Review
       │
       ▼
7. CI/CD
       │
       ▼
8. Merge → develop
       │
       ▼
9. Deploy DEV
       │
       ▼
10. Criar release/*
       │
       ▼
11. Deploy HML
       │
       ▼
12. Homologação
       │
       ▼
13. Pull Request → main
       │
       ▼
14. Deploy PRD
```
---

### 🔐 Proteção das Branches

As branches críticas devem possuir proteção no GitHub.

main

Recomenda-se:

❌ Proibir push direto;

❌ Proibir force push;

✅ Pull Request obrigatório;

✅ Aprovação obrigatória;

✅ Code Review;

✅ Status checks obrigatórios;

✅ Pipeline CI/CD obrigatório;

✅ Scan de segurança;

✅ Histórico protegido;

✅ Tags de versão.

staging / developer

Recomenda-se:

❌ Proibir push direto;

✅ Pull Request obrigatório;

✅ CI obrigatório;

✅ Testes automatizados;

✅ Code Review;

✅ Scan de qualidade;

✅ Scan de dependências.

---

### 📝 Padrão de Commits

Recomenda-se utilizar Conventional Commits.

Formato:
```
<tipo>(<escopo>): <descrição>
```

Exemplos:
```
feat(api): adiciona endpoint de beneficiários

fix(auth): corrige autenticação OIDC

docs(readme): atualiza documentação do projeto

refactor(database): reorganiza camada de persistência

test(api): adiciona testes de integração

chore(deps): atualiza dependências

ci(pipeline): adiciona análise SAST
```

Tipos recomendados:

Tipo	| Utilização
:---| :---:
feat	| Nova funcionalidade
fix	| Correção de bug
docs	| Documentação
refactor	| Refatoração
test	| Testes
chore	| Manutenção
ci	| Pipeline/CI/CD
build	| Build/dependências
perf	| Performance
security	| Correções relacionadas à segurança

---
### 🔀 Pull Request

Todo Pull Request destinado às branches protegidas deve possuir:

- Descrição da alteração;
- Referência à Issue;
- Justificativa técnica;
- Evidências de testes;
- Avaliação de impacto;
- Avaliação de segurança;
- Evidências do pipeline;
- Plano de rollback quando aplicável.

Exemplo:

```
Issue
  │
  ▼
Feature
  │
  ▼
Pull Request
  │
  ├── Code Review
  ├── Unit Tests
  ├── Integration Tests
  ├── SAST
  ├── Dependency Scan
  ├── Secret Scan
  └── Build
          │
          ▼
       APPROVED
          │
          ▼
        MERGE
```
---
### 🚀 GitFlow + CI/CD

O GitFlow deve estar integrado ao pipeline CI/CD.


```
                 GitHub
                    │
                    ▼
             ┌─────────────┐
             │ Pull Request│
             └──────┬──────┘
                    │
                    ▼
              ┌───────────┐
              │   Build   │
              └─────┬─────┘
                    │
                    ▼
              ┌───────────┐
              │   Tests   │
              └─────┬─────┘
                    │
                    ▼
              ┌───────────┐
              │  Security │
              │   Scan    │
              └─────┬─────┘
                    │
                    ▼
              ┌───────────┐
              │   Review  │
              └─────┬─────┘
                    │
                    ▼
                 Merge
                    │
          ┌─────────┴─────────┐
          ▼                   ▼
       develop             release
          │                   │
          ▼                   ▼
         DEV                  HML
                              │
                              ▼
                             PRD
```
---
### 🏷️ Versionamento

As versões das aplicações devem utilizar, preferencialmente, Semantic Versioning (SemVer):
```
MAJOR.MINOR.PATCH
```
Exemplo:
```
1.4.2
```
Onde:

* MAJOR — alterações incompatíveis;
* MINOR — novas funcionalidades compatíveis;
* PATCH — correções compatíveis.

Exemplos:
```
1.0.0 → Primeira versão
1.1.0 → Nova funcionalidade
1.1.1 → Correção de bug
2.0.0 → Alteração incompatível
```
Tags devem ser criadas na branch main:

```
git tag -a v1.4.0 -m "Release v1.4.0"

git push origin v1.4.0
```
---
### 🛡️ GitFlow e Governança

O GitFlow deve ser utilizado em conjunto com práticas de governança institucional.

```
              GOVERNANÇA
                   │
        ┌──────────┼──────────┐
        │          │          │
        ▼          ▼          ▼
     GitFlow     CI/CD     DevSecOps
        │          │          │
        └──────────┼──────────┘
                   │
                   ▼
              GitHub
                   │
                   ▼
             Aplicações
                   │
        ┌──────────┼──────────┐
        ▼          ▼          ▼
       DEV        HML        PRD
```
O objetivo é garantir que alterações em sistemas institucionais sejam:

* Planejadas;
* Revisadas;
* Testadas;
* Auditáveis;
* Rastreáveis;
* Seguras;
* Reversíveis;
* Automatizadas.

---
### 📌 Resumo do fluxo

Etapa	Branch	Ambiente	Objetivo
Desenvolvimento	feature/*	DEV	Implementação
Integração	develop	DEV	Integração
Preparação	release/*	HML	Estabilização
Produção	main	PRD	Versão oficial
Emergência	hotfix/*	PRD	Correção crítica

Regra geral: nenhuma alteração deve ser realizada diretamente na branch main. As alterações devem passar pelo processo de desenvolvimento, revisão, validação e CI/CD estabelecido para o projeto.
