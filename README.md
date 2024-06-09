# SPEC-1: Tax Calculation Solution for FOREX Investments

## Objectives

- [] Practice English

## Context

The client requires a solution to calculate the tax amount owed by their customers who invest in FOREX. The solution should include the management of the customers' investment portfolios and provide the final tax amount due, also considering other investments.

## Requirements

### Mandatory Requirements:

#### `Customer` Records

- **Insert** new customer records.
- **Consult** existing customer records.
- **Update** customer records.
- **Delete** customer records.

#### `Operation` Records:

- **Insert** new operation records.
- **Consult** existing operation records.
- **Update** operation records.
- **Delete** operation records.

#### `Report` Generation:

- Ability to send reports to customers or allow customers to consult their reports.
- Calculation of tax for the current month and accumulated.

### Desirable Requirements:

- An elegant presentation of data to improve customer relationships.

#### Optional Requirements:

- Additional analyses and insights related to investments.

## Excluded Requirements:

- Any non-critical functionalities that do not directly contribute to tax calculation or report generation.
  Urgency

## Questions:

- Data Sources and Integration: What are the data sources for the investments, and how will we integrate with them? Will they be provided via APIs, databases, or manual uploads?

- Regulatory Requirements: Are there specific regulations or calculations we need to follow? If so, can you provide the details or references?

## Domain Structure and Bounded Contexts

### Main Domain: Tax Calculation System for FOREX Investments

| Subdomains                 |
| -------------------------- |
| Client Management          |
| FOREX Operations Recording |
| Tax Report Generation      |

### Identification of Entities and Aggregates

#### Entity Client

| Attributes | Description                                                         |
| ---------- | ------------------------------------------------------------------- |
| ID         | Unique identifier of the client (UUID)                              |
| Name       | Full name of the client                                             |
| CPF        | Cadastro de Pessoa Física, a unique identification number in Brazil |
| Email      | Client's email address                                              |
| Address    | Client's residential address                                        |

---

| Behaviors    | Description                                       |
| ------------ | ------------------------------------------------- |
| updateData() | Allows updating the client's registration data    |
| delete()     | Removes the client's registration from the system |

#### Entity Operation

| Attributes | Description                                                 |
| ---------- | ----------------------------------------------------------- |
| ID         | Unique identifier of the operation (UUID)                   |
| Type       | Type of operation (Buy/Sell)                                |
| Date       | Date the operation was performed                            |
| Value      | Monetary value of the operation                             |
| Currency   | Currency used in the operation                              |
| ClientID   | Identifier of the client who performed the operation (UUID) |

---

| Behaviors | Description                   |
| --------- | ----------------------------- |
| insert()  | Adds a new operation          |
| update()  | Updates an existing operation |
| delete()  | Removes an operation          |

#### Investment Portfolio Aggregate

| Elements       | Description                           |
| -------------- | ------------------------------------- |
| Aggregate Root | Client (main entity of the aggregate) |
| Operation List | Financial operations of the client    |

---

| Behaviors          | Description                                                       |
| ------------------ | ----------------------------------------------------------------- |
| addOperation()     | Adds an operation to the client's portfolio                       |
| removeOperation()  | Removes an operation from the client's portfolio                  |
| calculateBalance() | Calculates the total balance of the client's investment portfolio |

---

## Definition of Services

### Tax Calculation Service

| Methods                   | Description                              |
| ------------------------- | ---------------------------------------- |
| calculateMonthlyTax()     | Calculates the tax due monthly           |
| calculateAccumulatedTax() | Calculates the accumulated tax over time |

---

| Business Rules    | Description                                         |
| ----------------- | --------------------------------------------------- |
| FOREX Regulations | Based on specific regulations for FOREX investments |

### Report Generation Service

| Methods             | Description                                           |
| ------------------- | ----------------------------------------------------- |
| generatePDF()       | Generates a report in PDF format                      |
| sendEmail()         | Sends the report by email to the client               |
| generateDashboard() | Creates an interactive dashboard with the report data |

---

| Business Rules  | Description                                                               |
| --------------- | ------------------------------------------------------------------------- |
| Data Formatting | Guidelines defining how data should be formatted and presented to clients |

## Definition of Repositories

### Client Repository

| Methods         | Description                                         |
| --------------- | --------------------------------------------------- |
| saveClient()    | Saves client data in the system                     |
| getClientById() | Retrieves client data using their unique identifier |
| updateClient()  | Updates existing client data                        |
| deleteClient()  | Removes client data from the system                 |

### Operation Repository

| Methods            | Description                                          |
| ------------------ | ---------------------------------------------------- |
| saveOperation()    | Saves operation data in the system                   |
| getOperationById() | Retrieves operation data using its unique identifier |
| updateOperation()  | Updates existing operation data                      |
| deleteOperation()  | Removes operation data from the system               |

## Concepts and Their Correlations

| Concept        | Explanation                                                                                                                                                                    | Correlations                                                                                                 |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ |
| Domain         | Area of knowledge or activity that the system is modeling. Example: Tax Calculation for FOREX investments.                                                                     | Encompasses various functional areas (subdomains), each with specific responsibilities.                      |
| Subdomain      | Specific divisions within the main domain focusing on particular aspects. Example: Client Management, FOREX Operations Recording, and Tax Report Generation.                   | Each subdomain addresses a specific functionality of the system.                                             |
| Entity         | A real-world object with a distinct identity. Example: Client and Operation.                                                                                                   | Represent real-world objects with unique identities and specific behaviors.                                  |
| Aggregate      | A group of entities treated as a cohesive unit. Example: Investment Portfolio.                                                                                                 | Form a unit of consistency and integrity.                                                                    |
| Aggregate Root | Maintains the integrity of the aggregate and controls the other entities within it. Example: Client in the Investment Portfolio.                                               | Ensures the consistency and integrity of aggregate elements.                                                 |
| Service        | Component that encapsulates business logic or operations that do not belong to a specific entity or aggregate. Example: Tax Calculation Service and Report Generation Service. | Perform specific business logic and operations, separated from entities and aggregates.                      |
| Repository     | A design pattern providing an interface for performing storage, retrieval, and search operations on entities. Example: Client Repository and Operation Repository.             | Offer a means to store, retrieve, and manage entities, maintaining data integrity in the system.             |
| Aggregate Root | The main entity within an aggregate that controls the consistency and integrity of other entities. Example: Client in the Investment Portfolio.                                | Ensures the consistency and integrity of aggregate elements.                                                 |
| Services       | Perform business logic that does not belong to a specific entity or aggregate, such as calculating taxes or generating reports.                                                | Encapsulate business logic and operations, providing specific functionalities for the system.                |
| Repositories   | Provide a means to store, retrieve, and manage entities, supporting the necessary operations to maintain data integrity in the system.                                         | Offer an interface for interacting with data, separating persistence logic from the system's business logic. |
