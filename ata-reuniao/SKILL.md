---
name: ata-reuniao
description: Transforma notas de reunião com clientes do sistema CRM em um relatório estruturado de adoção com 5 pilares (Situação Atual, Impacto Operacional, Execução, Próximos Passos, Pendências), e-mail formal de retorno e texto para o card de atendimento. Use sempre que o usuário pedir resumo de reunião, ata, relatório de GP, report de atendimento, follow-up de reunião com cliente CRM — frases como "resume essa reunião", "monta a ata", "gera o report do cliente", "cria o follow-up da reunião", "monta o email de retorno". NÃO use para: relatórios financeiros, análise de dados, documentação técnica, postmortem, ou qualquer pedido que não seja resumo de reunião de adoção do CRM.
---

# /ata-reuniao

Transforma notas brutas de uma reunião com cliente do CRM em um
relatório estratégico de adoção, e-mail formal de retorno e texto
para o card de atendimento. Para s de GP que atendem clientes
do sistema CRM e precisam registrar, comunicar e acompanhar cada
interação com qualidade e consistência.

## Flags

```
/ata-reuniao [notas]           → gera relatório completo + e-mail + card
/ata-reuniao -r [notas]        → apenas relatório (sem e-mail e card)
/ata-reuniao -e [notas]        → apenas e-mail de retorno
/ata-reuniao -k [notas]        → apenas texto para o card de atendimento
```

Flags são combináveis: `/ata-reuniao -r -e` gera relatório + e-mail sem o card; `/ata-reuniao -r -k` gera relatório + card sem o e-mail.

## Quando NÃO usar

- Relatório financeiro, análise de dados ou métricas de negócio
- Documentação técnica, ADR, postmortem de incidente
- Reuniões internas sem cliente presente
- Pedido sobre uma única tarefa ou bug isolado

## Instruções

### Passo 1: Receber o input e validar informações mínimas

Verificar se as notas contêm as informações mínimas necessárias:
- Nome do cliente
- Tipo/assunto da reunião
- Nome do pessoa de GP
- Data da reunião

Se alguma dessas informações estiver faltando, perguntar numa mensagem só antes de prosseguir. Exemplo: *"Para gerar o relatório preciso de: nome do cliente, tipo da reunião, seu nome e a data. Pode me informar?"*

Se as notas misturarem dois clientes distintos, identificar e perguntar: *"Encontrei notas de dois clientes ([A] e [B]). Gero um relatório separado para cada ou junto?"*

Se mais de 3 sub-itens do Pilar 1 ficarem sem dados, alertar antes de gerar: *"As notas estão com poucas informações para preencher o relatório completo. Deseja continuar assim ou prefere complementar?"*

### Passo 2: Extrair e estruturar os 5 pilares

Ler todas as notas e distribuir cada informação nos pilares abaixo. Não inventar conteúdo — se um sub-item não tiver dados, escrever "(sem registro)".

**Pilar 1 — Situação Atual**

Organizar em 4 sub-itens:

- **A) Satisfação e Familiaridade:** pontos positivos mencionados pelo cliente e nível de domínio percebido sobre o sistema.
- **B) Expectativas de Melhoria:** como o cliente deseja evoluir no uso do CRM.
- **C) Experiência do Usuário (UX):** pontos negativos, atritos na interface, dificuldades relatadas.
- **D) Dores Operacionais:** necessidades prioritárias para atender às regras de negócio do cliente.

**Pilar 2 — Impacto Operacional**

Analisar expectativa vs. realidade. Descrever como o uso atual (ou a ausência de uso de determinadas funcionalidades) afeta a operação do cliente. Ser direto e sem redundâncias.

**Pilar 3 — Execução**

Descrever as ações práticas tomadas pelo  de GP durante a reunião: orientações dadas, configurações realizadas, demonstrações feitas, apoio prestado. Usar verbos no passado.

**Pilar 4 — Próximos Passos ou Ações**

Lista clara e objetiva do que deve ser feito para o sucesso do projeto. Visão macro, sem granularidade excessiva. Verbos no infinitivo.

**Pilar 5 — Pendências (Matriz de Responsabilidade)**

Separar em duas colunas:

- **Cliente:** o que ele deve entregar, prazos e ações esperadas.
- **GP:** suas promessas, prazos de entrega e impacto esperado.

Se não houver prazo explícito nas notas, usar "A combinar".

### Passo 3: Devolver no formato fixo

SEMPRE devolver nesta ordem, sem preâmbulo:

---

## Relatório de Atendimento — [Nome do Cliente] · [Data]

### 1. Situação Atual

**A) Satisfação e Familiaridade**
[conteúdo]

**B) Expectativas de Melhoria**
[conteúdo]

**C) Experiência do Usuário (UX)**
[conteúdo]

**D) Dores Operacionais**
[conteúdo]

---

### 2. Impacto Operacional
[conteúdo]

---

### 3. Execução
[conteúdo]

---

### 4. Próximos Passos
- [ação]

---

### 5. Pendências

| Responsável | Ação | Prazo |
|---|---|---|
| Cliente | [ação] | [prazo] |
| GP | [ação] | [prazo] |

---

## E-mail de Retorno

```
Reunião de: [Tipo/Assunto]
Cliente: [Nome do Cliente]
GP: [Nome do GP ]
Data: [Data da Reunião]
```

[Corpo: saudação, resumo das tratativas, expectativas alinhadas,
responsabilidades de cada parte, encerramento cordial com despedida formal.]

Tom: formal, direto, sem jargão técnico excessivo. Foco em valor e próximos passos.

---

## Texto para o Card

```
Reunião de: [Tipo/Assunto]
Cliente: [Nome do Cliente]
```

[Resumo objetivo das tratativas, expectativas e responsabilidades —
sem saudação, sem despedida, formato de registro interno.]

Tom: direto, objetivo, linguagem de registro interno.

---

*Após gerar todos os outputs, descartar internamente os dados do cliente atendido. Não carregar informações de clientes anteriores para o próximo atendimento.*

## Exemplo

### Cenário: reunião de onboarding com cliente Acme Financeira

Usuário diz: `/ata-reuniao cliente: Acme Financeira, : Vinicius Redorat, data: 01/06/2026, tipo: Onboarding. Notas: cliente achou o sistema intuitivo mas tem dificuldade com o módulo de régua de cobrança. Quer automatizar o envio de SMS. Não conhece o relatório de aging. Configuramos a régua padrão juntos. Próximo passo: cliente vai mapear as carteiras e eu vou criar os templates de SMS até sexta.`

Resultado:

---

## Relatório de Atendimento — Acme Financeira · 01/06/2026

### 1. Situação Atual

**A) Satisfação e Familiaridade**
Cliente considerou o sistema intuitivo no geral, demonstrando boa receptividade inicial à plataforma.

**B) Expectativas de Melhoria**
Deseja automatizar o envio de SMS dentro da régua de cobrança para reduzir intervenção manual.

**C) Experiência do Usuário (UX)**
Dificuldade reportada no módulo de régua de cobrança — fluxo de configuração não está claro para o usuário.

**D) Dores Operacionais**
Desconhece o relatório de aging, o que limita a visibilidade sobre a carteira e priorização das cobranças.

---

### 2. Impacto Operacional
A falta de familiaridade com a régua de cobrança impede a automação do processo de comunicação com devedores. Sem o uso do relatório de aging, o cliente opera sem visibilidade estratégica da carteira, reduzindo a eficácia da recuperação de crédito.

---

### 3. Execução
Configuração da régua de cobrança padrão realizada em conjunto com o cliente durante a reunião. Orientações sobre o funcionamento do módulo e demonstração do fluxo de configuração.

---

### 4. Próximos Passos
- Apresentar o relatório de aging ao cliente
- Criar templates de SMS para a régua de cobrança
- Cliente mapear as carteiras ativas para configuração

---

### 5. Pendências

| Responsável | Ação | Prazo |
|---|---|---|
| Cliente | Mapear as carteiras ativas | A combinar |
| GP | Criar templates de SMS | Sexta-feira (06/06/2026) |

---

## E-mail de Retorno

Reunião de: Onboarding
Cliente: Acme Financeira
GP: Vinicius Redorat
Data: 01/06/2026

Prezado time Acme Financeira,

Agradeço pela participação na reunião de onboarding realizada hoje. Foi muito produtivo conhecer melhor a operação de vocês e iniciar a configuração do CRM alinhada às necessidades do negócio.

Durante o encontro, configuramos a régua de cobrança padrão e identificamos duas oportunidades de ganho imediato: a automação do envio de SMS e o uso do relatório de aging para priorização das cobranças — pontos que endereçaremos nos próximos passos.

**Responsabilidades acordadas:**
- **Acme Financeira:** mapeamento das carteiras ativas para configuração das réguas específicas.
- **Vinicius Redorat (GP):** criação dos templates de SMS até sexta-feira (06/06/2026).

Fico à disposição para qualquer dúvida. Em breve entro em contato para darmos sequência.

Atenciosamente,
Vinicius Redorat — Customer Success | CRM

---

## Texto para o Card

Reunião de: Onboarding
Cliente: Acme Financeira

Reunião de onboarding realizada. Cliente demonstrou boa receptividade ao sistema, com dificuldade identificada no módulo de régua de cobrança e desconhecimento do relatório de aging. Configuramos a régua padrão durante a reunião. Pendências: cliente deve mapear carteiras ativas;  deve criar templates de SMS até 06/06/2026.
