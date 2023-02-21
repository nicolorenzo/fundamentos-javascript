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

## Any

A utilização do `any` não é muito indicada pois aceita qualquer tipo, indo contra a proposta do TypesScript de definir os dados com precisão.

## Tipos Primitivos

Tipos primitivo são os tipos de dados básicos disponíveis em Javascript:

```
// Boolean
let loading: boolean;
loading = false;

// String
let email: sting;
email = 'nicolorenzo@live.com';

//Number
let price: number;
price = 10;
```

## Matrizes

Matrizes são arrays, vetores, ou simplesmente listas que devem ser declaradas de forma específica a depender do tipo de dado.

Por exemplo, um array de números:

```
let numbers: number[];
numbers = [1,2,3,4];

// Também é possível declarar da seguinte forma:

let users: Array<number>;
numbers = [1,2,3,4];
```

Seguindo a mesma lógica, declaramos uma lista de strings da seguinte forma:

```
let users: string[];
users = ['Nico', 'Lorenzo'];

// Ou:

let users: Array<string>;
users = ['Nico', 'Lorenzo'];
```

## Funções

Quando um função não tem retorno, ela será do tipo `void`, que mesmo não declarado, será definido implicitamente:

```
function showMessage(message: string): void {
  console.log(message)
}
```

Além disso, é possível reparar que também devemos definir o tipo de dado dos parâmetros de uma função.

Já no caso em há retorno da função, basta defini-lo como qualquer dado, por exemplo, se o retorno for uma string:

```
function showMessage(message: string): string {
  return message;
}
```

## Union

Este operador possibilita utilizar mais um tipo através do caractere `|`:

```
function printUserId(id: number | sting ) {
  console.log(`O ID do usuário é: ${id})
}

printUserId('1'); // Ou printUserID(1)
```

## Generic

Generic é outra forma de flexibilizar a tipagem, através da sintaxe `<T>`, onde `T` pode ser qualquer caractere, mas se convencionou usar `T` para representar "type":

```
function usestate<T>() {
  let stare: T;

  function get() {
    return state;
  }

  function set(newValue: T) {
    state = newValue;
  }

  return {get, set};
}

let newState = useState<string>();
newState.set('Nico');
```

Perceba que com generic, eu só defini o tipo no momento de declarar a função.

Agora, em combinação com o union, é possível fexibilizar um pouco mais:

```
function usestate<T extends number | string>() {
  let stare: T;

  function get() {
    return state;
  }

  function set(newValue: T) {
    state = newValue;
  }

  return {get, set};
}
```

A diferença de usar apenas union, é que dessa forma eu ainda só posso utilizar apenas o tipo que for definido no momento da declaração da função:

```
let newState = useState<string>();
newState.set('Nico');

// Ou

let newState = useState<number>();
newState.set(1234);
```

## Type

`type` é uma forma de reutilizar a declaração de múltiplos tipos:

```
type IdType =  string | number | undefined;
let userId: IdType;

userID = '1'; // || 1 || undefined
```

## Type Assertion

Esse é um recurso muito utilizado quando recebemos um objeto de uma API, por exemplo, cujo TypeScript não conhece a tipagem, então criamos um `type` definindo os tipos deste objeto:

```
type UserResponse = {
    id: number;
    name: string;
    avatar: string;
}

let userResponse = {} as UserResponse;
```

Perceba que através de `as` definimos que o objeto `userResponse` será do tipo `UserResponse`.

## Objetos

Como já deve ter ficado claro no exeplo acima, é possível utilizar `type` para declarar objetos:

```
type Point = {
    x: number;
    y: number;
}

function printCoord(points: Point) {
    console.log(`O eixo x é: ${points.x}`)
    console.log(`O eixo y é: ${points.y}`)
}

printCoord({x: 101, y: 50})
```

Dessa forma, nesse exemplo quando difinimos o tipo `Point` para o objeto que terá nossas coordenadas `x` e `y`, essas estão acessíveis dentro da função quando utilizamos o parâmetro `points`, já que ele é do tipo `Point`.

## Opcional

Em alguns casos, pode não ser estritamente necessário declarar alguma propriedade de algum objeto. Para isso, basta adicionar o caractere `?`:

```
type User = {
    name: string;
    email: string;
    age: number;
    isAdmin?: boolean; // A declaração dessa propriedade agora é opcional

let newUser: User = {
    name: 'João',
    email: 'joao@email.com',
    age: 18
}
```

## Intersecção de Tipos

Utilizamos esse recurso quando é necessário atribuir as propriedades de mais de um objeto a novo tipo:

```
type User = {
    id: number,
    name: string,
}

type Char = {
    nickname: string,
    level: number
}

type PlayerInfo = User & Char;

let info: PlayerInfo = {
    id: 1,
    name: 'João Inácio',
    nickname: 'birobirobiro',
    level: 50
}
```

Como mostra o exeplo, agora as propriedades dos tipos `User` e `Char` estão unidos através do caractere `&` e atribuídos ao tipo `PlayerInfo`.
