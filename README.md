<img width="822" height="872" alt="db-lrhub" src="https://github.com/user-attachments/assets/2350a3d0-14da-43d2-b47e-df6f35ea6b00" />

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



             
