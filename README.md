# Instituto de Assistência dos Servidores do Estado do Pará — IASEP

<p align="center">
  <strong>Instituto de Assistência dos Servidores do Estado do Pará</strong>
</p>

<p align="center">
  Tecnologia, inovação, segurança e transformação digital a serviço do Estado.
</p>

---

## 🏛️ Sobre o IASEP

O **Instituto de Assistência dos Servidores do Estado do Pará — IASEP** é uma instituição pública estadual responsável pela assistência à saúde dos servidores públicos do Estado do Pará e seus dependentes.

Este espaço no GitHub é destinado à **gestão, desenvolvimento, documentação e compartilhamento de projetos tecnológicos institucionais**, promovendo padronização, colaboração, transparência e boas práticas de engenharia de software e infraestrutura.

---

## 🎯 Objetivo deste GitHub

A organização GitHub do IASEP tem como objetivos:

- Centralizar os projetos de tecnologia da informação;
- Promover a colaboração entre equipes técnicas;
- Padronizar processos de desenvolvimento e infraestrutura;
- Implementar práticas de **DevOps, DevSecOps e GitOps**;
- Gerenciar código-fonte e Infraestrutura como Código;
- Automatizar processos operacionais;
- Manter documentação técnica dos ambientes;
- Promover rastreabilidade e controle das mudanças;
- Estabelecer padrões de segurança para os projetos;
- Facilitar a integração entre desenvolvimento, infraestrutura e operações.

---

## 🧭 Princípios

Os projetos mantidos nesta organização devem observar, sempre que aplicável, os seguintes princípios:

### 🔐 Segurança

- Princípio do menor privilégio;
- Gestão segura de credenciais e segredos;
- Separação de ambientes;
- Controle de acesso baseado em funções;
- Análise de vulnerabilidades;
- Segurança no ciclo de desenvolvimento;
- Auditoria e rastreabilidade.

### 🤖 Automação

Priorizar processos automatizados e reproduzíveis utilizando:

- Infrastructure as Code;
- Configuration as Code;
- GitOps;
- CI/CD;
- Automação operacional.

### 📦 Padronização

Buscar padrões institucionais para:

- Estrutura de repositórios;
- Branches;
- Commits;
- Pull/Merge Requests;
- Pipelines;
- Imagens de containers;
- Helm Charts;
- Ansible Roles;
- Terraform Modules;
- Documentação.

### 🔄 Rastreabilidade

Toda alteração relevante deve ser:

```text
Solicitação
    │
    ▼
Issue / Demanda
    │
    ▼
Desenvolvimento
    │
    ▼
Pull/Merge Request
    │
    ▼
Code Review
    │
    ▼
CI/CD
    │
    ▼
Homologação
    │
    ▼
Produção

```
### 🔒 Segurança dos repositórios

É proibido armazenar diretamente nos repositórios:

❌ Senhas
❌ Tokens
❌ API Keys
❌ Chaves privadas
❌ Certificados privados
❌ Credenciais de banco de dados
❌ Secrets de Kubernetes
❌ Credenciais de Cloud

Utilizar mecanismos apropriados para gerenciamento de segredos, como:

- Secret Managers;
- Kubernetes Secrets com proteção adequada;
- Sealed Secrets;
- External Secrets;
- Vault;
- Variáveis protegidas de CI/CD;
- OIDC quando disponível.

### 📋 Padrão recomendado para repositórios

Sempre que possível, os projetos devem possuir uma estrutura semelhante a:

repository/
├── README.md
├── LICENSE
├── CHANGELOG.md
├── docs/
├── src/
├── tests/
├── deploy/
├── helm/
├── ansible/
├── terraform/
├── scripts/
├── .github/
│   ├── workflows/
│   ├── ISSUE_TEMPLATE/
│   └── PULL_REQUEST_TEMPLATE.md
└── .gitignore

A estrutura deve ser adaptada à natureza de cada projeto.

### 📝 Documentação

Projetos institucionais devem possuir documentação suficiente para permitir:

- Instalação;
- Configuração;
- Operação;
- Atualização;
- Troubleshooting;
- Backup e recuperação;
- Monitoramento;
- Segurança;
- Dependências;
- Arquitetura;
- Procedimentos de rollback.

Documentação arquitetural pode utilizar:

- Markdown;
- Mermaid;
- Diagramas de arquitetura;
- ADR — Architecture Decision Records;
- Runbooks;
- Procedimentos operacionais.

### 🔀 Fluxo de contribuição

Alterações nos projetos devem seguir, preferencialmente:

Issue
  │
  ▼
Branch
  │
  ▼
Development
  │
  ▼
Commit
  │
  ▼
Pull Request
  │
  ▼
Code Review
  │
  ▼
Automated Tests
  │
  ▼
Security Scan
  │
  ▼
Merge
  │
  ▼
CI/CD

Pull Requests devem conter, quando aplicável:

- Descrição da alteração;
- Motivação;
- Impacto;
- Evidências de testes;
- Impacto de segurança;
- Impacto de infraestrutura;
- Procedimento de rollback.

### 🛡️ DevSecOps

A segurança deve estar integrada ao ciclo de desenvolvimento:

PLAN
  │
  ▼
CODE
  │
  ▼
BUILD
  │
  ├── SAST
  ├── Dependency Scan
  ├── Secret Scan
  └── Container Scan
  │
  ▼
TEST
  │
  ▼
DEPLOY
  │
  ▼
OPERATE
  │
  ▼
MONITOR

### 📊 Observabilidade

Aplicações e infraestrutura devem, quando aplicável, disponibilizar:

- Métricas;
- Logs;
- Health Checks;
- Readiness Checks;
- Liveness Checks;
- Alertas;
- Dashboards;
- Tracing.

A observabilidade deve permitir identificar:

O que aconteceu?
       │
       ▼
Quando aconteceu?
       │
       ▼
Onde aconteceu?
       │
       ▼
Qual foi o impacto?
       │
       ▼
Qual foi a causa?
       │
       ▼
Como corrigir?

### 💾 Backup e recuperação

Soluções críticas devem possuir estratégia documentada de:

- Backup;
- Retenção;
- Restauração;
- Disaster Recovery;
- Testes periódicos de recuperação;
- RPO;
- RTO.

Backup não deve ser considerado válido apenas por ter sido executado.

A restauração deve ser testada periodicamente.

### 📚 Documentação e referências

Projetos devem priorizar documentação oficial dos fabricantes e comunidades responsáveis pelas tecnologias utilizadas.

Entre as principais referências:

- Kubernetes
- OpenShift
- Red Hat
- Rancher
- Argo CD
- Ansible
- Terraform
- Helm
- GitHub
- GitLab
- Keycloak
- Prometheus
- Grafana

### 🤝 Colaboração

A colaboração entre as equipes é fundamental para a evolução dos serviços de tecnologia do IASEP.

Contribuições devem priorizar:

- Qualidade;
- Segurança;
- Automação;
- Padronização;
- Documentação;
- Sustentabilidade operacional;
- Alta disponibilidade;
- Observabilidade;
- Rastreabilidade.

### ⚠️ Classificação das informações

Os repositórios devem respeitar as políticas institucionais de segurança da informação e proteção de dados.

Informações classificadas como sensíveis, confidenciais ou protegidas por legislação específica não devem ser disponibilizadas publicamente.

Antes de publicar qualquer código, configuração ou documentação, verificar:

Código
  │
  ├── Contém credenciais?
  ├── Contém dados pessoais?
  ├── Contém informações internas?
  ├── Expõe infraestrutura?
  ├── Expõe endereços ou configurações sensíveis?
  └── Pode ser publicado?
          │
          ▼
       REVIEW

### 🏛️ IASEP

Instituto de Assistência dos Servidores do Estado do Pará

Tecnologia da Informação
Estado do Pará — Brasil
