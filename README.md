# SPEC-1: Solução para Cálculo de Imposto para Investimentos em FOREX

## Contexto

A cliente necessita de uma solução para calcular o valor devido de imposto a ser recolhido de seus clientes que aplicam em FOREX. A solução deve incluir o controle da carteira de investimentos dos clientes e fornecer o valor final do imposto devido, considerando também outros investimentos.

## Requisitos

### Requisitos Obrigatórios:

1. **Registro de Clientes**:

   - Inserir novos registros de clientes.
   - Consultar registros de clientes existentes.
   - Atualizar registros de clientes.
   - Deletar registros de clientes.

2. **Registro de Operações**:

   - Inserir novos registros de operações.
   - Consultar registros de operações existentes.
   - Atualizar registros de operações.
   - Deletar registros de operações.

3. **Geração de Relatórios**:
   - Possibilidade de envio de relatórios aos clientes ou permitir que os clientes consultem seus relatórios.
   - Cálculo de imposto para o mês corrente e acumulado.

### Requisitos Desejáveis:

- Uma apresentação elegante dos dados para melhorar a relação com os clientes.

### Requisitos Opcionais:

- Análises adicionais e insights relacionados aos investimentos.

### Requisitos Excluídos:

- Quaisquer funcionalidades não críticas que não contribuam diretamente para o cálculo do imposto ou geração de relatórios.

## Urgência

A cliente precisa que a solução esteja operacional e capaz de enviar informações até o dia 14 de junho de 2024.

## Perguntas

1. **Fontes de Dados e Integração**: Quais são as fontes de dados para os investimentos e como faremos a integração com elas? Serão fornecidas via APIs, bancos de dados ou uploads manuais?
2. **Requisitos Regulatórios**: Existem regulamentações específicas ou cálculos que precisamos seguir? Se sim, você pode fornecer os detalhes ou referências?

Vamos prosseguir com esses pontos para avançarmos com as seções de método e implementação.
