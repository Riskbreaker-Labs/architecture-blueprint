# Client

**Context Group:** #Entities-and-Aggregates

## Attributes:

- ID: Unique identifier of the client (UUID)
- Name: Full name of the client
- CPF: Cadastro de Pessoa Física, a unique identification number in Brazil
- Email: Client's email address
- Address: Client's residential address

## Behaviors:

- updateData(): Allows updating the client's registration data
- delete(): Removes the client's registration from the system
