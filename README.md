# Plano de Testes

**Projeto:** Digifab (Startup 2025)

*versão 2.0 — 06/10/2025*

## Histórico das alterações

| Data       | Versão | Descrição                                                                                                  | Autor(es)                                                   |
|------------|--------|--------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------|
| 04/10/2025 | 1.0    | Versão inicial baseada no Caso de Ensino                                                                     | Tiago Zardin / Felipe Griep / Giulia Cardoso / Rosival de Souza |
| 06/10/2025 | 2.0    | Refinos: escopo de teste por UCs priorizados; link com doc de Análise & Modelagem; critérios de entrada/saída; métricas; riscos; matriz de rastreabilidade; massa de dados; documentação complementar. | Tiago Zardin / Felipe Griep / Giulia Cardoso / Rosival de Souza |

---

## 1. Introdução

Este documento descreve **o plano de testes** do Digifab, abrangendo o escopo (requisitos a testar), a estratégia e tipos de teste, critérios de entrada e saída, recursos (pessoas/ambiente/ferramentas), cronograma, casos de teste e documentação de apoio.

**Programa sob teste:** plataforma de gestão e **rastreabilidade** da cadeia de suprimentos, com módulos de cadastros (fornecedores, clientes, produtos), registro de movimentações por etapa, gerenciamento documental, dashboards, cálculo de balanço de massa (com alertas), integrações (ERP/ETL; código de barras/RFID) e controle de acesso.

**Público‑alvo:** equipe do projeto (devs/QA/PO), professores(as) e avaliadores da disciplina.

**Escopo & premissas:**
- Considerando o volume de funcionalidades, **este ciclo V2 foca parte do diagrama de Casos de Uso** (ver doc *Análise & Modelagem*). Os demais itens serão cobertos em ciclos seguintes.
- Interface e usabilidade serão **planejadas e validadas** junto aos fluxos de maior valor (cadastros, movimentação, balanço, autenticação).
- Testes automatizados serão priorizados na **pirâmide** (unidade → API/contrato → E2E/UI → não‑funcionais).

**Não‑escopo imediato (postergado):** exportações avançadas, integrações batch de ERP completas, módulos de auditoria forense aprofundada e painéis analíticos complexos.

---

## 2. Requisitos a testar

A lista inclui **funcionais** (Casos de Uso) e **não funcionais** (RNFs). O ciclo V2 prioriza os UCs mais críticos ao valor de negócio e fluxo ponta‑a‑ponta.

### 2.1 Casos de uso (visão geral)

| ID  | Nome do Caso de Uso |
|-----|----------------------|
| UC1 | Cadastrar fornecedor/cliente/produto |
| UC2 | Registrar movimentação com rastreabilidade (código de barras/RFID) |
| UC3 | Gerenciar documentos (anexar/consultar/baixar) |
| UC4 | Calcular balanço de massa e gerar alertas de desvio |
| UC5 | Visualizar dashboards e exportar CSV |
| UC6 | Autenticação e perfis de acesso |
| UC7 | Integração ERP/ETL (importação/consumo de dados) |

**Escopo V2 (priorizados):** UC1, UC2, UC3, UC4, UC6.

**Backlog próximo (V2.1/V3):** UC5, UC7.

### 2.2 Requisitos não funcionais (RNFs)

| ID   | Requisito |
|------|-----------|
| RNF1 | Responsividade/usabilidade (desktop/mobile) |
| RNF2 | Segurança e LGPD (privacidade, mascaramento, logs/auditoria) |
| RNF3 | Desempenho sob carga (picos na API de movimentação) |
| RNF4 | Confiabilidade/consistência de dados (rastreabilidade ponta a ponta) |
| RNF5 | Observabilidade (logs, métricas, tracing) |
| RNF6 | Compatibilidade (browsers) e acessibilidade básica |
| RNF7 | Instalabilidade/Atualização (migrations, rollback, configuração) |

---

## 3. Estratégia de testes

### 3.1 Tipos de teste (mapa)

- **Unidade & Contratos** (serviços/regras/queries).
- **API/Contrato** (REST/JSON): esquema, status codes, validações.
- **E2E/UI** (fluxos críticos: cadastros, movimentação, login, anexos).
- **Integração** (ERP/ETL mocked/stub; leitor código de barras/RFID simulado).
- **Dados/Negócio** (balanço de massa; reconciliação por lote).
- **Performance** (tempo de resposta, throughput, p95/p99; escalabilidade básica).
- **Carga/Stress** (picos de criação de movimentação; fila/retry).
- **Segurança** (DAST baseline; RBAC; LGPD — mascaramento; audit trail).
- **Compatibilidade & Acessibilidade** (principais navegadores; checks básicos de contraste/rotulagem).
- **Instalação/Atualização** (migrações idempotentes; rollback controlado).
- **Usabilidade** (heurísticas; número de passos; feedback de erros).

> **Padrão de automação (pirâmide):** 60% unidade/contratos · 25% API · 10% E2E/UI · 5% não‑funcionais automatizados.

### 3.2 Critérios de **entrada** (start)
- Build estável; ambiente HML funcional; migrations aplicadas.
- UCs do escopo V2 com critérios de aceite definidos.
- Massa de dados mínima disponível (ver §7.1).
- Ferramentas e acessos provisionados (ver §6.2).

### 3.3 Critérios de **saída** (exit / aceite)
- **Funcional:** 100% dos CTs críticos executados e **aprovados**; 0 defeitos **Sev1/Sev2** abertos; Sev3 com workaround aceito.
- **Qualidade código:** cobertura mínima **80%** (statement/branch) nos serviços do escopo; Sonar sem *Blockers*; *Bugs* críticos = 0; *Vulnerabilities* críticas/altas = 0.
- **Desempenho:** p(95) **< 500 ms** nas APIs de movimentação e login, sob **100 req/s** por 10 min, erro HTTP = 0.
- **Segurança:** DAST baseline sem achados **Altos/Críticos**; RBAC sem bypass; logs de auditoria para operações sensíveis.
- **Dados:** reconciliação de saldo por lote **= 100%** no cenário de referência; tolerância de desvio definida em regra.

### 3.4 Métricas & Acompanhamento
- %CT executados/aprovados; *burn‑down* de defeitos (por severidade); *Mean Time To Fix*.
- p95/p99; taxa de erro; CPU/memória sob carga; consumo DB.
- Densidade de defeitos por UC.

### 3.5 Riscos & Mitigações
| Risco | Impacto | Mitigação |
|------|---------|-----------|
| Integração ERP indisponível | Médio/Alto | *Mocks* + fila/retry; testes de degradação; *feature flag*. |
| Dados sensíveis expostos | Alto | Mascaramento; revisão RBAC; DAST; revisão de logs. |
| Falhas no balanço de massa | Alto | Testes de reconciliação por lote; cenários de borda; *pair review* das regras. |
| Gargalo em anexos | Médio | Testes de upload concorrente; *limits* de tamanho; storage adequado. |

---

## 4. Matriz de rastreabilidade (UC ↔ Tipos de Teste ↔ CTs)

| UC  | Tipos de Teste | CTs (referência) |
|-----|-----------------|------------------|
| UC1 | Unidade, API, E2E/UI, Segurança | CT‑001, CT‑002, CT‑007, CT‑009 |
| UC2 | Integração, API, E2E/UI, Performance, Resiliência | CT‑003, CT‑010, CT‑012 |
| UC3 | E2E/UI, API, Segurança | CT‑004, CT‑007 |
| UC4 | Dados/Negócio, API | CT‑005, CT‑006 |
| UC6 | Segurança, E2E/UI, API | CT‑007, CT‑011 |

> **Observação:** UC5 e UC7 serão endereçados no próximo ciclo e já possuem rascunhos de CT (não incluídos nesta V2).

---

## 5. Tipos de teste — detalhamento por categoria

### 5.1 Métodos da Classe (Unidade/Contratos)

**Objetivo:** verificar serviços/repositórios (CRUD de cadastros, regras de balanço, alertas).

- **Técnica:** (x) manual · (x) automática  
- **Estágio:** Unidade (x) · Integração ( ) · Sistema ( ) · Aceitação ( )  
- **Abordagem:** Caixa branca (x) · Caixa preta (x)  
- **Responsáveis:** Devs e QA

### 5.2 Persistência de Dados

**Objetivo:** garantir durabilidade e consistência (transações de movimentação, anexos/documentos, trilhas de auditoria) e recuperação após falhas.

- **Técnica:** (x) manual · (x) automática  
- **Estágio:** Sistema (x)  
- **Abordagem:** Caixa preta (x)  
- **Responsáveis:** Devs/QA

### 5.3 Integração dos Componentes

**Objetivo:** verificar integração ERP/ETL e leitura de código de barras/RFID no fluxo de movimentações.

- **Técnica:** (x) manual · (x) automática  
- **Estágio:** Integração (x)  
- **Abordagem:** Caixa branca (x) · Caixa preta (x)  
- **Responsáveis:** Devs/QA

### 5.4 Tempo de Resposta (Desempenho)

**Objetivo:** garantir tempos aceitáveis no registro de movimentações e nas consultas de dashboards.

- **Técnica:** (x) automática (k6/JMeter)  
- **Estágio:** Sistema (x)  
- **Abordagem:** Caixa preta (x)  
- **Responsáveis:** QA (Performance)

### 5.5 Animação — **N/A**

Não se aplica ao escopo atual. Mantido por compatibilidade com o template.

### 5.6 Efeitos Sonoros — **N/A**

Não se aplica ao escopo atual. Caso incluído futuramente, validar disparo, volume e acessibilidade.

---

## 6. Recursos

### 6.1 Ambiente — Software & Hardware
- **Infra:** containers; DB relacional; fila com retry; storage de documentos.
- **Software:** SO atualizado; navegadores (Chrome/Firefox/Edge); Node/.NET quando aplicável; serviços de HML (ERP/ETL *stubs*).
- **Ambientes:** DEV · HML · PRD.

### 6.2 Ferramentas de teste
- **Unidade/Contrato:** JUnit/xUnit, Jest.  
- **API:** Postman/Newman, REST Assured.  
- **E2E/UI:** Playwright ou Cypress.  
- **Performance:** k6/JMeter.  
- **Segurança:** OWASP ZAP (DAST), SCA (Snyk/Dependabot).  
- **Qualidade:** SonarCloud/SonarQube.  
- **Observabilidade:** logs + métricas + tracing.

### 6.3 Equipe & papéis
- **QA/Coordenação de Testes:** define estratégia, métricas, triagem de defeitos.  
- **Desenvolvedores:** testes de unidade/contrato; suporte a correções; *feature flags*.  
- **PO/Negócio:** validação de critérios de aceite; priorização de defeitos.  
- **DevOps:** provisionamento de ambientes; pipelines; observabilidade.

---

## 7. Massa de dados & critérios adicionais

### 7.1 Massa de dados
- **Cadastros base:** 3 fornecedores, 2 clientes, 5 produtos.  
- **Movimentações:** cenários de entrada/saída por **lote** com timestamps e operadores.  
- **Documentos:** 1 NF por movimentação principal (PDF).  
- **Perfis:** ADMIN, OPERADOR, VISUALIZADOR.

> Dados pessoais **anonimizados**; CPFs/nomes fictícios; anexos sem informações sensíveis reais.

### 7.2 Gerenciamento de defeitos
- Ferramenta: GitHub Issues/Jira.  
- **Severidade:** Sev1 (paralisação/segurança), Sev2 (impacto alto), Sev3 (médio), Sev4 (baixo/UX).  
- **SLA referência:** Sev1/2: correção até o próximo *build* estável; Sev3: até o *sprint* seguinte; Sev4: backlog.

### 7.3 Padrões & nomenclatura
- **ID de caso de teste:** `CT-xxx`; **suite** por UC; *tags* por RNF.  
- **Evidências:** *screens* + logs + exportações (quando aplicável).

---

## 8. Cronograma

| Tipo de teste      | Duração | Início     | Término    |
|--------------------|---------|------------|------------|
| Planejar teste     | 5 dias  | 04/10/2025 | 09/10/2025 |
| Projetar teste     | 10 dias | 04/10/2025 | 14/10/2025 |
| Implementar teste  | 20 dias | 04/10/2025 | 24/10/2025 |
| Executar teste     | 26 dias | 04/10/2025 | 30/10/2025 |
| Avaliar teste      | 30 dias | 04/10/2025 | 03/11/2025 |

> **Marcos:** conclusão de suites UC1/UC6 (T‑7); conclusão UC2/UC3 (T‑14); conclusão UC4 + não‑funcionais (T‑24).

---

## 9. Anexo A — Exemplos de Casos de Teste (V2)

| ID     | Título                              | Pré‑condições                         | Passos                                                                 | Resultado Esperado                                                                       | Tipo |
|--------|-------------------------------------|---------------------------------------|------------------------------------------------------------------------|-------------------------------------------------------------------------------------------|------|
| CT‑001 | Cadastrar fornecedor válido         | ADMIN logado                          | Acessar Cadastros→Fornecedores; preencher obrigatórios; salvar        | Fornecedor criado; ID gerado; registro auditável                                          | Funcional/UI |
| CT‑002 | Limites de campos (produto)         | ADMIN logado                          | Cadastrar produto nos limites; exceder limites                        | Aceita nos limites; bloqueia excedente com mensagem                                       | Validação |
| CT‑003 | Registrar movimentação com rastreio | Fornecedor e produto existentes       | Registrar **entrada**; escanear código; confirmar                      | Registro com timestamp, operador e vínculo ao **lote**                                     | Integração |
| CT‑004 | Anexar nota fiscal (PDF)            | Movimentação criada                   | Anexar NF; visualizar/baixar                                           | Documento armazenado e vinculado; auditoria                                               | Funcional/UI |
| CT‑005 | Balanço – alerta de desvio          | Entradas/saídas cadastradas           | Executar cálculo; abrir painel                                         | Alerta quando consumo excede tolerância                                                   | Regra de negócio |
| CT‑006 | Dashboard e exportação              | Dados consolidados                    | Abrir dashboard; exportar CSV                                          | Indicadores corretos; CSV com colunas especificadas                                       | Relatório |
| CT‑007 | Perfis – acesso negado              | **OPERADOR** logado                   | Acessar tela restrita (admin)                                          | Bloqueio com mensagem; tentativa auditada                                                  | Segurança |
| CT‑008 | LGPD – mascarar dados               | Base com dados pessoais               | Abrir listagens; pesquisar CPF                                         | Dados mascarados conforme política                                                         | Conformidade |
| CT‑009 | UX – fluxo em poucos cliques        | Navegador desktop                     | Executar cadastro medindo passos/tempo                                 | Fluxo intuitivo; feedback claro                                                            | UX |
| CT‑010 | Performance – 100 req/s             | HML e massa de teste                  | k6 10 min a 100 req/s na API de movimentação                           | p(95) < 500 ms; 0 erros HTTP; CPU < 75%                                                    | Desempenho |
| CT‑011 | Segurança – DAST baseline           | HML disponível                        | Rodar ZAP baseline                                                      | Sem vulnerabilidades **alta/crítica**; médias registradas                                  | Segurança |
| CT‑012 | Resiliência – ERP indisponível      | ERP off                               | Simular falha; executar movimentação                                   | Degradação graciosa; fila/retry; logs

---

## 10. Documentação complementar
- **Caso de Ensino em Engenharia de Software (2025)** — contexto de negócio, requisitos funcionais/RNFs, objetivos.  
- **Laboratório III — Plano de Testes (enunciado)** — itens obrigatórios, diretriz para selecionar parte das funcionalidades; necessidade de incluir casos de teste e validar UI/usabilidade.  
- **Análise & Modelagem — Template_tarefa_Etapa4 (Grupo 3)** — diagrama de Casos de Uso (Cap. 2) e detalhamento de UCs (Cap. 3) que **fundamentam o escopo V2**.

> **Traço de ligação:** este plano referencia os UCs definidos em *Análise & Modelagem* e implementa a estratégia/cronograma solicitados no enunciado do **Laboratório III**.
