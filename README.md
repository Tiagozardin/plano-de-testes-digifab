# Plano de Teste

**Digifab**

*versão 1.0*

## Histórico das alterações

   Data    | Versão |    Descrição                                  | Autor(a)
-----------|--------|-----------------------------------------------|-----------------
04/10/2025 |  1.0   | Versão inicial baseada no Caso de Ensino     | Tiago Zardin / Felipe Griep / Giulia Cardoso / Rosival de Souza

## 1 - Introdução

Este documento descreve os requisitos a testar, os  tipos de testes definidos para cada iteração, os recursos de hardware e software a serem empregados e o cronograma dos testes ao longo do projeto. As seções referentes aos requisitos, recursos e cronograma servem para permitir ao gerente do projeto acompanhar a evolução dos testes.

**Programa sob teste (Digifab):** plataforma de gestão e rastreabilidade da cadeia de suprimentos com módulos de cadastros (fornecedores, clientes, produtos), registro de movimentações por etapa, gerenciamento documental, dashboards e cálculo de balanço de massa com alertas, integrações (ERP/ETL, código de barras/RFID) e controle de acesso.

## 2 - Requisitos a Testar

Esta seção contém os casos de uso e requisitos não funcionais identificados como objetos dos testes ao longo do desenvolvimento do projeto. A lista abaixo inclui **funcionais** (Casos de Uso) e **não funcionais** (RNFs).

### Casos de uso:

Identificador do caso de uso | Nome do caso de uso
-----------------------------|---------------------
UC1 | Cadastrar fornecedor/cliente/produto
UC2 | Registrar movimentação com rastreabilidade (código de barras/RFID)
UC3 | Gerenciar documentos (anexar/consultar/baixar)
UC4 | Calcular balanço de massa e gerar alertas de desvio
UC5 | Visualizar dashboards e exportar CSV
UC6 | Autenticação e perfis de acesso
UC7 | Integração ERP/ETL (importação/consumo de dados)

### Requisitos não-funcionais:

Identificador do requisito   | Nome do requisito
-----------------------------|---------------------
RNF1 | Responsividade e usabilidade (desktop/mobile)
RNF2 | Segurança e LGPD (privacidade, mascaramento, logs/auditoria)
RNF3 | Desempenho sob carga (picos na API de movimentação)
RNF4 | Confiabilidade de dados/consistência (rastreabilidade ponta a ponta)
RNF5 | Observabilidade (logs, métricas, tracing)
RNF6 | Compatibilidade (browsers suportados) e acessibilidade básica
RNF7 | Instalabilidade/Atualização (instalação, rollback, configuração)

## 3 - Tipos de teste

Abaixo os **tipos de testes** escolhidos para o projeto. Incluímos **funcionais e não funcionais**, cobrindo interface, API, integração, dados/negócio, segurança, desempenho, instalação e usabilidade.

- Teste de interface de usuário (E2E UI);
- Teste funcional por casos de uso (caixa-preta);
- Teste de API/contrato;
- Teste de integração (ERP/ETL, RFID);
- Teste de dados/consistência (balanço de massa);
- Teste de performance (tempo de resposta);
- Teste de carga e stress;
- Teste de segurança e controle de acesso (DAST/SCA);
- Teste de compatibilidade (browsers) e acessibilidade;
- Teste de instalação/atualização (rollback, migrações);
- Teste de usabilidade (heurísticas, fluxo);
- Testes de unidade e contratos.

> **Mapeamento exemplo:** UC1, UC3, UC5 → UI/API; UC2, UC7 → Integração; UC4 → Dados/Negócio + Performance; RNF1/RNF6 → Compatibilidade/Acessibilidade; RNF2 → Segurança; RNF3 → Carga/Stress; RNF4 → Consistência; RNF7 → Instalação.


### 3.1 - Métodos da Classe 

Para teste de funcionalidade.
Aqui deve-se verificar se cada classe retorna o esperado.
Se possível usar teste automatizado.

<br/>
<table>
    <tr>
        <th>Objetivo</th>
        <th colspan="4">Verificar o comportamento correto de serviços/repositórios (CRUD de cadastros, cálculos de balanço, regras de alerta).</th>
    </tr>
    <tr>
        <th>Técnica:</th>
        <th colspan="2">(x) manual</th>
        <th colspan="2">(x) automática</th>
    </tr>
    <tr>
        <th>Estágio do teste</th>
        <th>Integração ( )</th>
        <th>Sistema ( )</th>
        <th>Unidade (x)</th>
        <th>Aceitação ( )</th>
    </tr>
    <tr>
        <th>Abordagem do teste</th>
        <th colspan="2">Caixa branca (x)</th>
        <th colspan="2">Caixa preta (x)</th>
    </tr>
    <tr>
        <th>Responsável(is)</th>
        <th colspan="4">Programador(es) e equipe de testes</th>
    </tr>
</table>
<br/>

### 3.2 - Persistência de Dados

Para teste de integridade de dados e do banco de dados.
Aqui deve-se verificar se os dados não se perdem ao desligar o programa. Se o programa consegue se recuperar em caso de falha ou fechamento repentino.
Se possível usar teste automatizado.

<br/>
<table>
    <tr>
        <th>Objetivo</th>
        <th colspan="4">Garantir durabilidade e consistência (transações de movimentação, anexos/documentos, trilhas de auditoria) e recuperação após falhas.</th>
    </tr>
    <tr>
        <th>Técnica:</th>
        <th colspan="2">(x) manual</th>
        <th colspan="2">(x) automática</th>
    </tr>
    <tr>
        <th>Estágio do teste</th>
        <th>Integração ( )</th>
        <th>Sistema (x)</th>
        <th>Unidade ( )</th>
        <th>Aceitação ( )</th>
    </tr>
    <tr>
        <th>Abordagem do teste</th>
        <th colspan="2">Caixa branca ( )</th>
        <th colspan="2">Caixa preta (x)</th>
    </tr>
    <tr>
        <th>Responsável(is)</th>
        <th colspan="4">Programador(es) ou equipe de testes</th>
    </tr>
</table>
<br/>

### 3.3 - Integração dos Componentes

Para teste de funcionalidade.
Aqui deve-se verificar se as classes e métodos conseguem fazer a integração entre elas para uma sequência de ações do programa.
Se possível usar teste automatizado.

<br/>
<table>
    <tr>
        <th>Objetivo</th>
        <th colspan="4">Verificar integração ERP/ETL e leitura de código de barras/RFID no fluxo de movimentações.</th>
    </tr>
    <tr>
        <th>Técnica:</th>
        <th colspan="2">(x) manual</th>
        <th colspan="2">(x) automática</th>
    </tr>
    <tr>
        <th>Estágio do teste</th>
        <th>Integração (x)</th>
        <th>Sistema ( )</th>
        <th>Unidade ( )</th>
        <th>Aceitação ( )</th>
    </tr>
    <tr>
        <th>Abordagem do teste</th>
        <th colspan="2">Caixa branca (x)</th>
        <th colspan="2">Caixa preta (x)</th>
    </tr>
    <tr>
        <th>Responsável(is)</th>
        <th colspan="4">Programador(es) ou equipe de testes</th>
    </tr>
</table>
<br/>

### 3.4 - Tempo de Resposta

Para teste de funcionalidade.
Aqui deve-se verificar se o tempo de respostas das ações do programa são consideradas aceitáveis.
Se possível usar teste automatizado.

<br/>
<table>
    <tr>
        <th>Objetivo</th>
        <th colspan="4">Garantir tempos aceitáveis no registro de movimentações e nas consultas de dashboards.</th>
    </tr>
    <tr>
        <th>Técnica:</th>
        <th colspan="2">( ) manual</th>
        <th colspan="2">(x) automática (k6/JMeter)</th>
    </tr>
    <tr>
        <th>Estágio do teste</th>
        <th>Integração ( )</th>
        <th>Sistema (x)</th>
        <th>Unidade ( )</th>
        <th>Aceitação ( )</th>
    </tr>
    <tr>
        <th>Abordagem do teste</th>
        <th colspan="2">Caixa branca ( )</th>
        <th colspan="2">Caixa preta (x)</th>
    </tr>
    <tr>
        <th>Responsável(is)</th>
        <th colspan="4">QA (Performance)</th>
    </tr>
</table>
<br/>

### 3.5 - Animação

Para teste de funcionalidade (para games, principalmente, mas não somente).
Aqui deve-se verificar se as animações existentes no programa são disparadas quando devem e se seguem uma sequência lógica.
Se possível usar teste automatizado.

> **Aplicabilidade para Digifab:** não há animações; **N/A**. Mantemos a seção por compatibilidade com o template.

<br/>
<table>
    <tr>
        <th>Objetivo</th>
        <th colspan="4">N/A</th>
    </tr>
    <tr>
        <th>Técnica:</th>
        <th colspan="2">( ) manual</th>
        <th colspan="2">( ) automática</th>
    </tr>
    <tr>
        <th>Estágio do teste</th>
        <th>Integração ( )</th>
        <th>Sistema ( )</th>
        <th>Unidade ( )</th>
        <th>Aceitação ( )</th>
    </tr>
    <tr>
        <th>Abordagem do teste</th>
        <th colspan="2">Caixa branca ( )</th>
        <th colspan="2">Caixa preta ( )</th>
    </tr>
    <tr>
        <th>Responsável(is)</th>
        <th colspan="4">N/A</th>
    </tr>
</table>
<br/>

### 3.6 - Efeitos Sonoros

> **Aplicabilidade para Digifab:** não há efeitos sonoros; **N/A**. Se houver alertas sonoros no futuro, validar disparo, volume e acessibilidade.

<br/>
<table>
    <tr>
        <th>Objetivo</th>
        <th colspan="4">N/A</th>
    </tr>
    <tr>
        <th>Técnica:</th>
        <th colspan="2">( ) manual</th>
        <th colspan="2">( ) automática</th>
    </tr>
    <tr>
        <th>Estágio do teste</th>
        <th>Integração ( )</th>
        <th>Sistema ( )</th>
        <th>Unidade ( )</th>
        <th>Aceitação ( )</th>
    </tr>
    <tr>
        <th>Abordagem do teste</th>
        <th colspan="2">Caixa branca ( )</th>
        <th colspan="2">Caixa preta ( )</th>
    </tr>
    <tr>
        <th>Responsável(is)</th>
        <th colspan="4">N/A</th>
    </tr>
</table>
<br/>

## 4 - Recursos

Esta seção descreve os recursos humanos, de ambiente de teste (hardware e software) e de ferramentas de automatização de testes necessários.

### 4.1 - Ambiente de teste - Software e Hardware

- **Hardware/Infra:** containers, banco relacional, filas/retry, storage de documentos.
- **Software:** SO atualizado, navegadores suportados (Chrome, Firefox, Edge), Node/.NET quando aplicável, serviços ERP/ETL de homologação.
- **Ambientes:** DEV, HML (homologação), PRD (produção).

### 4.2 - Ferramenta de teste

- **Unit/Contrato:** xUnit/NUnit, Jest.
- **API:** Postman/Newman, REST Assured.
- **E2E/UI:** Playwright ou Cypress.
- **Performance:** k6/JMeter.
- **Segurança:** OWASP ZAP (DAST), SCA (Snyk/Dependabot).
- **Qualidade:** SonarCloud/SonarQube.
- **Observabilidade:** stack de logs + métricas + tracing.

## 5 - Cronograma

Tipo de teste      | Duração | data de início | data de término
-------------------|---------|----------------|-----------------
planejar teste | 5 dias | 04/10/2025 | 09/10/2025
projetar teste | 10 dias | 04/10/2025 | 14/10/2025
implementar teste | 20 dias | 04/10/2025 | 24/10/2025
executar teste | 26 dias | 04/10/2025 | 30/10/2025
avaliar teste | 30 dias | 04/10/2025 | 03/11/2025

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