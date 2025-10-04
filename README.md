# Plano de Teste

Digifab
versão 1.0

## Histórico das alterações

   Data    | Versão | Descrição                                             | Autor(a)
-----------|--------|-------------------------------------------------------|---------------------------------------------------------------
04/10/2025 |  1.0   | Versão inicial baseada no Caso de Ensino Startup 2025 | Tiago Zardin/ Felipe Griep / Giulia Cardoso / Rosival de Souza


## 1 - Introdução

Este documento descreve os requisitos a testar, os tipos de testes definidos para cada iteração, os recursos de hardware e software a serem empregados e o cronograma dos testes ao longo do projeto. As seções referentes aos requisitos, recursos e cronograma servem para permitir aos stakeholders do projeto acompanhar a evolução dos testes.

Com esse documento, você deve:
  * Identificar informações de projeto existentes e os componentes de software que devem ser testados.
  * Listar os Requisitos a testar.
  * Recomendar e descrever as estratégias de teste a serem empregadas.
  * Identificar os recursos necessários e prover uma estimativa dos esforços de teste.
  * Listar os elementos resultantes do projeto de testes.

**Programa sob teste (contexto Startup 2025):** plataforma de gestão e rastreabilidade da cadeia de suprimentos com módulos de cadastros (fornecedores, clientes, produtos), registro de movimentações por etapa, gerenciamento documental, dashboards e cálculo de balanço de massa com alertas, integrações (ERP/ETL, código de barras/RFID) e controle de acesso.

## 2 - Requisitos a Testar

Esta seção contém os casos de uso e requisitos não funcionais identificados como objetos dos testes ao longo do desenvolvimento do projeto.

### Casos de uso:

Identificador do caso de uso | Nome do caso de uso
---|---
UC1 | Cadastrar fornecedor/cliente/produto
UC2 | Registrar movimentação com rastreabilidade (código de barras/RFID)
UC3 | Gerenciar documentos (anexar/consultar/baixar)
UC4 | Calcular balanço de massa e gerar alertas de desvio
UC5 | Visualizar dashboards e exportar CSV
UC6 | Autenticação e perfis de acesso
UC7 | Integração ERP/ETL (importação/consumo de dados)

### Requisitos não-funcionais:

Identificador do requisito | Nome do requisito
---|---
RNF1 | Responsividade e usabilidade (desktop/mobile)
RNF2 | Segurança e LGPD (privacidade, mascaramento, logs/auditoria)
RNF3 | Desempenho sob carga (picos na API de movimentação)
RNF4 | Confiabilidade de dados/consistência (rastreabilidade ponta a ponta)
RNF5 | Observabilidade (logs, métricas, tracing)

## 3 - Tipos de teste

Tipos de testes escolhidos para o projeto e próximos ciclos:

  * Teste de interface de usuário (E2E) – Playwright/Cypress
  * Teste de API/contrato – Postman/Newman, REST Assured
  * Teste de integração (ERP/ETL, RFID)
  * Teste de dados/consistência (balanço de massa)
  * Teste de desempenho (k6/JMeter)
  * Teste de segurança (DAST OWASP ZAP, SCA)
  * Teste de usabilidade e acessibilidade
  * Testes de unidade e contratos (xUnit/NUnit, Jest)

### 3.1 - Métodos da Classe

Para teste de funcionalidade. Aqui deve-se verificar se cada classe retorna o esperado. Se possível usar teste automatizado.

- **Objetivo:** garantir comportamento correto de serviços e repositórios (CRUD, cálculos de balanço, regras de alerta).
- **Técnica:** (x) manual  (x) automática
- **Estágio do teste:** Integração ( )  Sistema ( )  Unidade (x)  Aceitação ( )
- **Abordagem do teste:** Caixa branca (x)  Caixa preta (x)
- **Responsável(is):** Devs + QA

### 3.2 - Persistência de Dados

Para teste de integridade de dados e do banco de dados.

- **Objetivo:** garantir durabilidade e consistência (transações de movimentação, anexos/documentos, trilhas de auditoria).
- **Técnica:** (x) manual  (x) automática
- **Estágio do teste:** Integração ( )  Sistema (x)  Unidade ( )  Aceitação ( )
- **Abordagem do teste:** Caixa branca ( )  Caixa preta (x)
- **Responsável(is):** Equipe de testes

### 3.3 - Integração dos Componentes

Para testar a orquestração entre componentes e integrações externas.

- **Objetivo:** verificar integração ERP/ETL e leitura de código de barras/RFID no fluxo de movimentações.
- **Técnica:** (x) manual  (x) automática
- **Estágio do teste:** Integração (x)  Sistema ( )  Unidade ( )  Aceitação ( )
- **Abordagem do teste:** Caixa branca (x)  Caixa preta (x)
- **Responsável(is):** Devs + QA

### 3.4 - Tempo de Resposta

- **Objetivo:** garantir tempos aceitáveis no registro de movimentações e consultas de dashboards.
- **Técnica:**  ( ) manual  (x) automática (k6/JMeter)
- **Estágio do teste:** Integração ( )  Sistema (x)  Unidade ( )  Aceitação ( )
- **Abordagem do teste:** Caixa preta (x)
- **Responsável(is):** QA (Performance)

### 3.5 - Segurança e Controle de Acesso

- **Objetivo:** assegurar autenticação, perfis e proteção de dados (LGPD), incluindo varredura DAST e SCA.
- **Técnica:**  (x) manual  (x) automática (ZAP, SCA)
- **Estágio do teste:** Sistema (x)
- **Abordagem do teste:** Caixa preta (x)
- **Responsável(is):** Sec/DevSecOps + QA

### 3.6 - Usabilidade (UX) e Acessibilidade

- **Objetivo:** validar clareza de fluxos e critérios heurísticos; acessibilidade básica.
- **Técnica:**  (x) manual  (x) automática (linters, checagens)
- **Estágio do teste:** Sistema (x)
- **Abordagem do teste:** Caixa preta (x)
- **Responsável(is):** QA + PO

## 4 - Recursos

### 4.1 - Ambiente de teste - Software e Hardware

- **Ambientes:** DEV, HML (homologação), PRD (produção).
- **Hardware/Infra:** containers, banco relacional, filas/retry, storage de documentos.
- **Software:** SO atualizado, navegadores suportados, ferramentas citadas acima.

### 4.2 - Ferramenta de teste

- **Unit/Contrato:** xUnit/NUnit, Jest.
- **API:** Postman/Newman, REST Assured.
- **E2E/UI:** Playwright ou Cypress.
- **Performance:** k6/JMeter.
- **Segurança:** OWASP ZAP (DAST), SCA (Snyk/Dependabot).
- **Qualidade:** SonarCloud/SonarQube.
- **Observabilidade:** stack de logs + métricas + tracing.

## 5 - Cronograma

Tipo de teste Duração data de início data de término
planejar teste 04/10/2025 09/10/2025
projetar teste 04/10/2025 14/10/2025
implementar teste 04/10/2025 24/10/2025
executar teste 04/10/2025 30/10/2025
avaliar teste 04/10/2025 03/11/2025

---

### Anexo A – Exemplos de Casos de Teste

ID | Título | Pré-condições | Passos | Resultado Esperado | Tipo
---|---|---|---|---|---
CT-001 | Cadastrar fornecedor válido | Perfil ADMIN logado | Acessar Cadastros>Fornecedores; preencher obrigatórios; salvar | Fornecedor criado, ID gerado, auditável | Funcional/UI
CT-002 | Limites de campos (produto) | ADMIN logado | Cadastrar produto nos limites; exceder limites | Aceita nos limites; bloqueia além do limite com mensagem | Validação/Valor-Limite
CT-003 | Registrar movimentação com rastreio | Fornecedor e produto existentes | Registrar entrada; escanear código; confirmar | Registro com timestamp, operador e vínculo ao lote | Integração
CT-004 | Anexar nota fiscal (PDF) | Movimentação criada | Anexar NF; visualizar/baixar | Documento armazenado e vinculado; auditoria | Funcional/UI
CT-005 | Balanço – alerta de desvio | Entradas/saídas cadastradas | Executar cálculo; abrir painel | Alerta quando consumo excede tolerância | Regra de Negócio
CT-006 | Dashboard e exportação | Dados consolidados | Abrir dashboard; exportar CSV | Indicadores corretos; CSV com colunas especificadas | Relatório
CT-007 | Perfis – acesso negado | Operador logado | Acessar tela restrita | Bloqueio com mensagem; tentativa auditada | Segurança
CT-008 | LGPD – mascarar dados | Base com dados pessoais | Abrir listagens; pesquisar CPF | Dados mascarados conforme política | Conformidade
CT-009 | UX – fluxo em poucos cliques | Navegador desktop | Executar cadastro medindo passos/tempo | Fluxo intuitivo, feedback claro | UX
CT-010 | Performance – 100 req/s | HML e massa de teste | k6 10 min a 100 req/s | p(95) < 500 ms; 0 erros HTTP; CPU < 75% | Desempenho
CT-011 | Segurança – DAST baseline | HML disponível | Rodar ZAP baseline | Sem vulns alta/crítica; médios registrados | Segurança
CT-012 | Resiliência – ERP indisponível | ERP off | Simular falha; executar movimentação | Degradação graciosa; fila/retry; logs | Resiliência
