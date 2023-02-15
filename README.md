# Fundamentos do TypeScript

O TypeScript surge para suprir uma deficiência do Javascript que é sua **fraca tipagem**, ou seja, no Javascript puro não é necessário declarar os tipos de dado, como em C ou MySQL, por exemplo. Sendo assim, o TypeScript possibilita uma maior consistência nos dados e, consequentemente, evita erros. Veja o exemplo abaixo:

```
function sum(a,b) {
  return a+b
}
console.log(sum(1,'2')); // output: 12
```

Como o Javascript é uma linguagem fracamente tipada, ele não sabe que gostaríamos que essa função de soma recebesse apenas valores numéricos e não retorna um erro quando passamos uma string como parâmetro e concatena os valores.
