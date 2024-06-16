# Resumo
A cliente trabalha como contadora para clientes investidores e precisa de uma ferramenta que calcule o imposto devido em Forex, ativo aplicado em dólar. A partir do escopo, foi criado um descritivo de todas funcionalidades e resultado esperado da ferramenta criada.
Uma solicitação bastante freezada foi a de enviar os dados à cliente de uma forma bonita, através de um relatório personalizado.
# Lista de bases, suas relações e funcionalidades
## Base de clientes
A cliente deve ser capaz de administrar a sua base de clientes, inserindo, alterando ou excluindo clientes da sua base.
**Responsável por popular:** Cliente
**Dados necessários:** nome, CPF
## Base das corretoras
Assim como na base de clientes, a cliente deve ser capaz de administrar a sua base de corretoras, inserindo, alterando ou excluindo corretoras da sua base.
**Responsável por popular:** cliente
**Dados necessários:** Nome corretora
## Base de cotações do dólar
Temos duas opções de implementação aqui. A primeira, é seguir da mesma forma que nas bases de clientes e corretoras, onde a cliente fica responsável por inserir a cotação do dólar, ou nós usamos os dados disponíveis pelo Bacen e já deixamos disponível quando ela selecionar um mês de apuração, a cotação do dólar daquele mês já fica disponível para ela.
**Responsável por popular: depende**
**Dados necessários:** valor do fechamento do dólar no último dia de cada mês como referência. Página onde Head = "Cotação e Boletins"
[Documentação da API de dados abertos do Bacen](https://dadosabertos.bcb.gov.br/dataset/dolar-americano-usd-todos-os-boletins-diarios)
## Base de lançamentos
Aqui, unimos as três bases anteriores para realizar a apuração do imposto devido do cliente. Na área de lançamentos, a cliente pode realizar três tipo de operações. Saldo, Depósito, Saque.
Abaixo, falarei especificamente sobre as operações de lançamento, mas, uma vez lançados, os dados devem poder ser lidos e mostrados à Cliente, atualizados e apagados (Crud).
A partir desta base de lançamentos, unimos as três bases anteriores para realizar a apuração do imposto do saque realizado pelo cliente. Então, a cliente será responsável por selecionar um dia de apuração, o cliente que está sendo lançado, e a corretora que é desta apuração. Após isto, ela entra com o saldo em dólar daquele mês, e o valor convertido em real fica gravado. 
### Lançamento de saldo
Um lançamento de Saldo serve como informativo do saldo de um cliente. 
O saldo mais antigo posto na ferramenta deve seguir à regra:

$$
\text{Saldo}_{\text{mês}} = \text{Saldo}_{\text{Lançamento mais antigo}} + \text{Depósitos} - \text{Saques}
$$
Desta forma, qualquer saldo feito em uma data posterior ao primeiro saldo  deve ser utilizado apenas para validar que não foi esquecida nenhuma operação no caminho.
### Lançameno de depósito
Um depósito é um dinheiro enviado à corretora. O montante afeta o saldo, mas não incide nenhum imposto, pois a competência deste se dá quando um papel vende e algum lucro pode ser apurado.

#Dúvida aqui é se este depósito significa a compra de um papel ou se é contabilizado o simples envio de dinheiro para uma corretora.
### Lançamento de saque
Um saque é um dinheiro recomprado à corretora. Este valor está sujeito à imposto e deve ser convertido para reais a partir da operação de venda. E, apurado qualquer lucro, um imposto de 15% do lucro em reais é devido de imposto.

**Responsável por popular:** Cliente
**Dados necessários:** Saldo da corretora
**Output:** Valor em reais devido referente ao saque realizado. Este valor representa 15% do valor do saque convertido em reais
___
# Domínios

* Cadastro de clientes
* Cadastro de corretoras
* Cadastro de cotações - Depósito (Compra), Venda (Venda)
* Lançamento de saldo (Saldo, Saque ou Depósito)
* Gerar relatório do ano e cumulativo até o mês desejado

# Dado de dólar do Banco Central
A partir da API disponibilizada do banco Central, devemos ter todos os dados (uma tabela nx3, onde n é o número de dias necessários para a tabela).
Depósito - Cotação de compra
Venda - Cotação de venda
# Escopo do imposto devido
* Remessa o cliente não paga imposto: é o saldo da conta corrente para ele poder acompanhar quanto ele tem na conta e quanto ele mandou para a corretora
* O imposto devido é igual a 15% sobre os lucros obtidos, convertidos em reais. Quando o lucro for negativo, este valor gera uma compensação, que é utilizada para abater lucros futuros naquele mesmo ano. 
# Escopo do relatório gerado
* Mostrar mensal e acumulado
* Levei um gráfico de barras com linhas, ela pediu para mudar. Disse que era necessário melhorar para mostrar quanto que tem no mês e quanto que tem acumulado até o momento (cascata?)

# Reunião 10.06.2024
Usar a cotação de venda nas operações de venda

# Exemplo real
Valdinei começou o mês com USD 1.500 de saldo
Valdinei tinha em Abril um saldo de USD 1.000. Mas ficou negativo em abril em USD 500
Este 500 que ele tomou em pau, vai para a coluna do imposto vlaor negativo. Este valor negativo se chama #Compensação 
Em maio ele fez um depósito de USD 500 e no fim do mês ficou positivo em USD 600. Sacou USD 600.

Ao invés de pagar USD 600 em imposto, ele só paga em relação ao saldo da diferença.

___
Ideia: Mostrar quanto da variação no patrimõnio foi devido à variação na dolarização da carteira; quanto foi responsável pela movimentação dos ativos realizados.

# Construção do contrato
* Topa honorários para mudanças
* Tem hoje 15 clientes que aplicam em Forex. Vamos oferecer o serviço no valor acordado de R$ 200/mês até 70 clientes
## Acordos a realizar
* Colocar no acordo no site sobre um site lançado e relatórios impressos na ferramenta significa que é um comprovante que a cliente aceitou a ferramenta funciona para o escopo dado na entrega. Colocar isto de uma forma justa e que dê segurança ao Freela e à cliente.
* Entender se a cliente precisa de NF, ou se fazemos isto de forma mais informal enquanto temos apenas uma cliente.