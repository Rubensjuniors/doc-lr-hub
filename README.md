<img width="952" height="728" alt="image" src="https://github.com/user-attachments/assets/e5f4401d-8758-4b7b-8daa-2ceb43884d44" />

# Rules

```markdown
┌─────────────────┬─────────┬─────────┬─────────┬──────────────────────┐
│     TABELA      │ CRIAR   │ EDITAR  │ APAGAR  │     OBSERVAÇÕES      │
├─────────────────┼─────────┼─────────┼─────────┼──────────────────────┤
│ ENTRADAS        │   ✅    │   ✅    │   ⚠️    │ Salário não pode     │
│                 │         │         │         │ ser apagado          │
├─────────────────┼─────────┼─────────┼─────────┼──────────────────────┤
│ SAÍDAS          │   🚫    │   🚫    │   🚫    │ Calculado            │
│                 │         │         │         │ automaticamente      │
├─────────────────┼─────────┼─────────┼─────────┼──────────────────────┤
│ GASTOS_FIXOS    │   ✅    │   ✅    │   ✅    │ CRUD completo        │
├─────────────────┼─────────┼─────────┼─────────┼──────────────────────┤
│ PARCELADOS      │   ✅    │   ✅    │   ✅    │ CRUD completo        │
├─────────────────┼─────────┼─────────┼─────────┼──────────────────────┤
│ GASTOS_DEBITO   │   ✅    │   ✅    │   ✅    │ CRUD completo        │
└─────────────────┴─────────┴─────────┴─────────┴──────────────────────┘
```

# Rotas

**Public**
- Autenticação
  - [ ] /sign-in (POST)
  - [ ] /aign-up (POST)
  - [ ] /refreshToken (Vai ser validado ainda como vai ser feito) (PATCH)

**Privete (ID)**
- [ ] /summary (filtrada pela mes) - (GET)
- [ ] /profile - (GET)
- /entries
  - [ ] CREATE
  - [ ] DELETE
- /expenses/fixed
  - [ ] CREATE
  - [ ] UPDATE
  - [ ] DELETE
- /expenses/credit (filtrada pela mes)
  - [ ] CREATE
  - [ ] UPDATE
  - [ ] DELETE
- /expenses/debit (filtrada pela mes)
  - [ ] CREATE
  - [ ] UPDATE
  - [ ] DELETE



   
             
