# Fundamentos do [TypeScript](https://www.typescriptlang.org/)

O TypeScript surge para suprir uma deficiência do Javascript que é sua **fraca tipagem**, ou seja, no Javascript puro não é necessário declarar os tipos de dado, como em C ou MySQL, por exemplo. Sendo assim, o TypeScript possibilita uma maior consistência nos dados e, consequentemente, evita erros. Veja o exemplo abaixo:

```
function sum(a,b) {
  return a+b
}
console.log(sum(1,'2')); // output: 12
```

Como o Javascript é uma linguagem fracamente tipada, ele não sabe que gostaríamos que essa função de soma recebesse apenas valores numéricos e não retorna um erro quando passamos uma string como parâmetro, apenas concatena os valores.

## Tipagem explícita

Tipagem explícita significa que devemos declarar de forma clara nossos tipos de dados, como por exeplo os parâmetros de uma função

```
function showTicket(user: string, ticket :number) {
  console.log(`Olá ${user}. O número do seu ticket é ${ticket}`)
}
```

Para a função acima declaramos que o parâmeto `user` será um dado do tipo `string`, enquanto `ticket` será `number`.

## Tipos da dado

Agora que já entendemos a importância do TypeScript e da tipagem explícita, veremos os tipos de dados.

### Any

A utilização do `any` não é muito indicada pois aceita qualquer tipo, indo contra a proposta do TypesScript de definir os dados com precisão.
