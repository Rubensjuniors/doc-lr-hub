<img width="822" height="872" alt="db-lrhub" src="https://github.com/user-attachments/assets/2350a3d0-14da-43d2-b47e-df6f35ea6b00" />

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
  - [ ] /sign-up (POST)
  - [ ] /logout (POST)
  - [ ] /refreshToken (Vai ser validado ainda como vai ser feito) (PATCH)

**Privete (ID)**
- [ ] /summary (filtrada pela mes) - (GET)
- [ ] /profile - (GET)
- /entries
  - [ ] CREATE
  - [ ] UPDATE
  - [ ] DELETE
- /expenses/fixed
  - [ ] GET
  - [ ] CREATE
  - [ ] UPDATE
  - [ ] DELETE
- /expenses/credit (filtrada pela mes)
  - [ ] GET
  - [ ] CREATE
  - [ ] UPDATE
  - [ ] DELETE
- /expenses/debit (filtrada pela mes)
  - [ ] GET
  - [ ] CREATE
  - [ ] UPDATE
  - [ ] DELETE

  - [ ] /expenses/last-month (Recebe quantidade de meses) - (GET)
  

# Contrato das Rotas

**/sign-in** body
```typescript
{
  email: "rublari3011@teste.com"
  password: "rublari#12312"
}
```

**/sign-up** body
```typescript
{
  name: "rublari"
  email: "rublari3011@teste.com"
  password: "rublari#12312"
}
```

**/summary** Response
```typescript
[
  { type: 'entries', value: 1000 },
  { type: 'exits', value: 500 },
  { type: 'total', value: 500 },
]
```

**/profile** Response
```typescript
{
  name: "rublari"
  email: "rublari3011@teste.com"
  avatar: "adasdasdasd"
}
```

**/entries** 
- body (CREATE)
```typescript
{
 
}
```

- body (DELETE)
```typescript
{
  id: 12232
}
```

**/expenses/fixed** 
- body (CREATE)
```typescript
{
 
}
```

- body (GET)
```typescript
{
 
}
```

- body (UPDATE)
```typescript
{
 
}
```

- body (DELETE)
```typescript
{
 
}
```

**/expenses/credit** 
- body (CREATE)
```typescript
{
 
}
```

- body (GET)
```typescript
{
 
}
```

- body (UPDATE)
```typescript
{
 
}
```

- body (DELETE)
```typescript
{
 
}
```

**/expenses/debit** 
- body (CREATE)
```typescript
{
 
}
```

- body (GET)
```typescript
{
 
}
```

- body (UPDATE)
```typescript
{
 
}
```

- body (DELETE)
```typescript
{
 
}
```

- /expenses/last-month (GET)
- Response
```typescript
{
    month: 5,
    income: 5200,
    expenses: 2300,
    year: 25
}
```


             
