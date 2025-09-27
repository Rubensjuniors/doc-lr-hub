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


             
