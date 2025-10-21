
# Rotas

**Public**
- Autenticação
  - [x] /sign-in (POST)
  - [x] /sign-up (POST)
  - [ ] /logout (POST)
  - [ ] /refreshToken (Vai ser validado ainda como vai ser feito) (PATCH)

**Privete (ID)**
- [x] /summary (filtrada pela mes) - (GET)
- [ ] /profile - (GET)
- /entries
  - [x] CREATE
  - [x] UPDATE
  - [x] DELETE
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
- GET
```typescript
{
  id: 'asdasdasda',
  name: 'Salario',
  amount: 5000.0,
  dateOfReceipt: '2025-10-01',
  createdAt,
  updatedAt
}
```

- POST
```typescript
{
  name: 'Salario',
  amount: 5000.0,
  dateOfReceipt: '2025-10-01'
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
