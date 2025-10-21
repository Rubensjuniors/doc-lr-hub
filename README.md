<img width="822" height="872" alt="db-lrhub" src="https://github.com/user-attachments/assets/2350a3d0-14da-43d2-b47e-df6f35ea6b00" />

* User → Category (1:N): um usuário pode ter várias categorias.
* User → Expenses (1:N): as despesas pertencem a um único usuário.
* Category → Expenses (1:N): cada despesa está associada a uma categoria.
* Expenses → Installments (1:N): uma despesa pode ter várias parcelas.
* User → Entries (1:N): cada usuário tem múltiplas entradas financeiras.

# Documentação do Banco de Dados - lrhub

## Tabelas e Campos

---

### Tabela `users`

Armazena os dados dos usuários do sistema.

| Campo           | Tipo           | Descrição                                       |
|-----------------|----------------|------------------------------------------------|
| `id`            | SERIAL         | Identificador único do usuário (PK).            |
| `name`          | VARCHAR(100)   | Nome completo do usuário.                       |
| `email`         | VARCHAR(255)   | E-mail do usuário (único).                      |
| `password_hash` | VARCHAR(255)   | Hash da senha para autenticação.                 |
| `created_at`    | DATETIME       | Data e hora de criação do usuário.              |
| `avatar`        | VARCHAR(455)   | URL ou caminho da imagem/avatar do usuário (opcional). |

---

### Tabela `categories`

Categorias personalizadas criadas pelos usuários para agrupar despesas.

| Campo        | Tipo             | Descrição                                                         |
|--------------|------------------|------------------------------------------------------------------|
| `id`         | UUID             | Identificador único da categoria (PK).                           |
| `name`       | VARCHAR(45)      | Nome da categoria (ex: Alimentação, Transporte).                 |
| `color`      | VARCHAR(45)      | Cor associada à categoria (pode ser um código hexadecimal).      |
| `user_id`    | BIGINT UNSIGNED  | ID do usuário proprietário da categoria (FK para `users`).       |
| `created_at` | DATETIME         | Data e hora de criação da categoria.                             |

_Relacionamento:_ Cada categoria pertence a um usuário. Se o usuário for deletado, suas categorias também são removidas.

---

### Tabela `expenses`

Registros das despesas dos usuários.

| Campo         | Tipo                   | Descrição                                                     |
|---------------|------------------------|--------------------------------------------------------------|
| `id`          | UUID                   | Identificador único da despesa (PK).                         |
| `name`        | VARCHAR(255)           | Nome ou descrição da despesa.                                |
| `type`        | ENUM('DEBIT','FIXED','CREDIT') | Tipo da despesa: débito, fixa, ou crédito.                   |
| `amount`      | DECIMAL(10,2)          | Valor da despesa.                                            |
| `created_at`  | DATETIME               | Data da criação da despesa.                                  |
| `updated_at`  | DATETIME               | Data da última atualização da despesa.                       |
| `is_paid`     | BOOLEAN                | Indica se a despesa foi paga (true/false).                   |
| `user_id`     | BIGINT UNSIGNED        | Usuário proprietário da despesa (FK para `users`).           |
| `category_id` | BIGINT UNSIGNED        | Categoria associada (FK para `categories`).                  |

_Relacionamento:_ Uma despesa pertence a um usuário e a uma categoria. Deletar usuário apaga despesas; deletar categoria está restrito para proteger dados.

---

### Tabela `installments`

Parcelas vinculadas a despesas do tipo parcelado.

| Campo             | Tipo             | Descrição                                           |
|-------------------|------------------|---------------------------------------------------|
| `id`              | UUID             | Identificador único da parcela (PK).              |
| `installment_number`| INT            | Número da parcela (ex: 1, 2, 3...).                |
| `amount`          | DECIMAL(10,2)    | Valor da parcela.                                  |
| `due_date`        | DATETIME         | Data de vencimento da parcela.                     |
| `is_paid`         | BOOLEAN          | Indica se a parcela já foi paga.                   |
| `paid_date`       | DATETIME         | Data em que a parcela foi paga (opcional).         |
| `expense_id`      | BIGINT UNSIGNED  | Despesa associada a essa parcela (FK para `expenses`). |

_Relacionamento:_ Cada parcela pertence a uma despesa. Deletar despesa apaga suas parcelas.

---

### Tabela `entries`

Registra entradas de receita para os usuários.

| Campo           | Tipo           | Descrição                                           |
|-----------------|----------------|----------------------------------------------------|
| `id`            | UUID           | Identificador único da entrada (PK).                |
| `name`          | VARCHAR(255)   | Nome ou descrição da receita (ex: Salário, Bônus). |
| `amount`        | DECIMAL(10,2)  | Valor recebido.                                     |
| `created_at`    | DATETIME       | Data da criação da entrada.                         |
| `updated_at`    | DATETIME       | Data da última atualização da entrada.             |
| `deletable`     | BOOLEAN        | Indica se esta entrada pode ser deletada (default TRUE). |
| `date_of_receipt` | DATETIME     | Data do recebimento do valor (opcional).           |
| `user_id`       | BIGINT UNSIGNED| Usuário dono da entrada (FK para `users`).          |

_Relacionamento:_ Cada entrada pertence a um usuário. Deletar usuário apaga suas entradas.

---

## Observações

- Todas as tabelas possuem relação direta com o usuário para garantir dados isolados.
- As operações de exclusão utilizam `CASCADE` para manter a integridade referencial, exceto em `expenses.category_id`, que usa `RESTRICT` para evitar exclusão acidental de categorias usadas.
- Campos de data (`created_at`, `updated_at`, etc.) ajudam a controlar histórico e auditoria.

```markdown
┌─────────────────┬─────────┬─────────┬─────────┬──────────────────────┐
│     TABELA      │ CRIAR   │ EDITAR  │ APAGAR  │     OBSERVAÇÕES      │
├─────────────────┼─────────┼─────────┼─────────┼──────────────────────┤
│ ENTRADAS        │   ✅    │   ✅    │   ✅    │ CRUD completo        │
├─────────────────┼─────────┼─────────┼─────────┼──────────────────────┤
│ SAÍDAS          │   🚫    │   🚫    │   🚫    │ Calculado            │
│                 │         │         │         │ automaticamente      │
├─────────────────┼─────────┼─────────┼─────────┼──────────────────────┤
│ GASTOS_FIXOS    │   ✅    │   ✅    │   ✅    │ CRUD completo        │
├─────────────────┼─────────┼─────────┼─────────┼──────────────────────┤
│ PARCELADOS      │   ✅    │   ✅    │   ✅    │ CRUD completo        │
├─────────────────┼─────────┼─────────┼─────────┼──────────────────────┤
│ GASTOS_DEBITO   │   ✅    │   ✅    │   ✅    │ CRUD completo        │
├─────────────────┼─────────┼─────────┼─────────┼──────────────────────┤
│ CATEGORIAS      │   ✅    │   ✅    │   ✅    │ CRUD completo        │
└─────────────────┴─────────┴─────────┴─────────┴──────────────────────┘
```

## Visão Geral
Essa arquitetura foi projetada para um sistema de controle financeiro pessoal, onde os usuários podem registrar despesas, organizar essas despesas em categorias, e controlar o pagamento de parcelas (installments) para despesas que são pagas em múltiplas vezes.

## Tabelas e Relacionamentos

**User**
  * Armazena os dados dos usuários que utilizam o sistema.
  * Relacionamento: cada usuário possui várias categorias, despesas (expenses) e entradas (entries).

**Category** 
  * Representa as categorias que o usuário pode criar para organizar suas despesas, como “Alimentação”, “Transporte” etc.
  * Usar categoria personalizada ajuda a melhorar a organização e filtragem dos dados.
    
**Entries**
  * Armazena entradas financeiras, que não se enquadram diretamente como despesas (pode incluir receitas, reembolsos etc.).
  * Esta tabela foi criada para manter a flexibilidade do sistema, separando tipos distintos de registros financeiros.
  * Importante lembrar que cada user quado for criado ja deve ter uma entrada criada com name de "salario" e com valor 0 para ser editada.
    
**Expenses (Despesas)**
  * Armazena todas as despesas do usuário, contendo informações básicas como nome, tipo, valor, status de pagamento e relacionamento com categoria.
  * É uma tabela única para simplificar o gerenciamento de despesas.
  * Motivo para ter uma tabela única:
    * Evitar duplicação de dados.
    * Facilitar consultas e relatórios consolidados.
    * Acompanhar diversas despesas independentemente da quantidade de parcelas.
      
**Installments (Parcelas)**
  * Armazena as parcelas de despesas que são divididas em múltiplos pagamentos.
  * Cada registro representa uma parcela específica, com número da parcela (installment_number), valor, data de vencimento, status de pagamento e referência à despesa original (expense_id).
  * Por que uma tabela separada de parcelas?
    * Granularidade: Permite controlar cada parcela individualmente (data de pagamento, valor pago, status).
    * Flexibilidade: Algumas despesas não possuem parcelas, outras sim. Com essa estrutura, podemos ter despesas simples (pagas à vista) e despesas parceladas usando a mesma tabela expenses, enquanto a tabela installments gerencia as particularidades das parcelas.
    * Evitar duplicação e inconsistência: Caso as parcelas fossem armazenadas na tabela de despesas, o registro da despesa seria multiplicado, causando redundância e complicando a atualização de dados.
    * Relatórios precisos: Facilitam relatórios que mostram parcelas pagas, parcelas pendentes, valores totais por período etc.
   
    
## Fluxo simplificado
  * O usuário cria uma categoria para organizar suas despesas.
  * O usuário registra uma despesa na tabela expenses, informando valor total, tipo e categoria.
  * Caso a despesa seja parcelada, ela terá múltiplos registros na tabela installments, que apontam para essa despesa.
  * Cada parcela pode ser marcada como paga ou não, facilitando o acompanhamento.
  * Entradas financeiras que não são despesas (como receitas) são armazenadas separadamente na tabela entries para deixar claro e modularizar o sistema.

## Benefícios dessa arquitetura
* Clareza e organização dos dados: Separação clara entre despesas, parcelas e categorias.
* Escalabilidade: Fácil de adicionar novos tipos de entradas e novas funcionalidades no futuro.
* Controle detalhado: Permite acompanhamento detalhado do fluxo financeiro, incluindo pagamentos parciais e parcelas.
* Facilidade de manutenção: Atualizações e inserções são feitas em tabelas específicas, o que minimiza impacto e erros.



             
