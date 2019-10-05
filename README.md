## Aula 02 - Hook useState

Até agora para poder ter estado na aplicação precisariamos de criar um componente com Class, ou seja, uma classe que extendia de React.Component e definir a variável state e informar seus estados. Na versão 16.8 a API Hooks foi criada para poder diminuir a verbosidade no código evitando a necessidade de usar classes para definir componentes com estados e manipulação do ciclo de vida. Diminui também a verbosidade para integrar com Redux e Apollo (GraphQL).

Primeiro Hook que vamos ver é o `useState`.

### useState

É o hook que ser usando dentro da função que vai retornar uma variável e uma função que alterar o estado dessa mesma variável.

O useState retorna o estado e a função que atualiza o estado.

```
const [tech, setTech] =  useState([]);
```

Criamos uma const que recebe de forma desestruturada uma variável de estado e uma função que atualiza essa variábel de estado, o useState recebe como parâmetro o valor inicial do estado, que no nosso caso é um array vazio.

Mas se passarmos alguns valores, podemos listar as tecnologias:

```
import React, { useState } from 'react';

function App() {
  const [tech, setTech] = useState(['ReactJS', 'ReactNative', 'NodeJS']);

  return (
    <ul>
      {tech.map(t => (
        <li>{t}</li>
      ))}
    </ul>
  );
}

export default App;
```

Olha como fica mais simples e menos verboso.

Agora vamos alterar o estado com a função `setTech`.

```
import React, { useState } from 'react';

function App() {
  const [tech, setTech] = useState(['ReactJS', 'ReactNative']);

  function handleAdd() {
    setTech([...tech, 'Node.JS']);
  }

  return (
    <>
      <ul>
        {tech.map(t => (
          <li key={t}>{t}</li>
        ))}
      </ul>
      <button onClick={handleAdd}>Adicionar</button>
    </>
  );
}

export default App;
```

Quando o usuário clicar no botão Adicionar, a função `handleAdd` será executada, o `setTech` vai ser invocado e o como o estado é imutável, replico o valor do array e adiciono o novo valor.

A variável tech armazena todos os dados e o setTech altera o seu estado.

Toda vez que a tech é alterada o render é invocado novamente.

o useState é o hook mais simples, ele pode armazenar todos os tipos do Javascript.

Podemos ainda criar um outro hook no mesmo componente, podemos criar quanto quisermos.

Criaremos um novo Hook:

```
const [newTech, setNewTech] =  useState('');
```

Vai armazenar a tecnologia que eu digitar em um input que vou criar:

```
<input  value={newTech}  onChange={e  =>  setNewTech(e.target.value)}  />
```
O input recebe um value que é o valor que está sendo digitado, o onChange executa uma função que recebe o evento de digitação no input, que passa para a função de atualização do estado do newTech o valor que está sendo digitado.

Quando o usuário clica em adicionar, chamamos o método `handleAdd()` que vai repassar para o setTech a nova tecnologia e depois limpar o input passando uma string vazia, veja:

```
  function handleAdd() {
    setTech([...tech, newTech]);
    setNewTech('');
  }
```
Simples assim! Esse é o hook mais simples e fácil para aprender!


Código [https://github.com/tgmarinho/react-hooks/tree/aula-02-hook-useState](https://github.com/tgmarinho/react-hooks/tree/aula-02-hook-useState)
