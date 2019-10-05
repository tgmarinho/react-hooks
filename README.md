## Aula 03 - Hook useEffect

O `useEffect` soprõe os ciclos de vida anteriores que usavamos com classes: `componentDidMount`, `componentDidUpdate`, `componentWillUnmount`. Nessa aula vamos aprender como aplicar o useEffects para substituir esses três ciclos mencionados.

### componentDidUpdate

Se a gente quiserse armazenar as variáveis das tecnologias no localStorage sempre que uma variável de estado alterasse, teríavmos que comparar o estado com o que está vindo e ver se eram diferente e atualizar o estado com o novo valor e chamar o localStorage.setItem(...) para armazenar esse array com o novo valor.

Agora com useEffects fazemos assim:

```
import React, { useState, useEffect } from  'react';
...
useEffect(() => {
    localStorage.setItem('tech', JSON.stringify(tech));
}, [tech]);
```

passamos para a função useEffect uma função que faz o que precisarmos que nesse caso é passar para o localStorage um novo item 'tech' com o array em formato de JSON. E o segundo parametro é um array de dependências, quando eu passo um array com um valor, toda vez que esse estado for alterado então esse useEffect vai ser executado. Nesse caso toda vez que `tech` sofrer uma alteração o useEffect vai ser chamado.

### componentDidMount

Mas se eu quiser que execute apenas uma vez, quando o componente montar em tela? Só não passar o estado no array de dependência:

```
  useEffect(() => {
    const storageTech = localStorage.getItem('tech');
    if (storageTech) {
      setTech(JSON.parse(storageTech));
    }
  }, []);
```

Podemos ter vários useEffects, nesse useEffect estamos fazendo a mesma coisa que a função componendDidMount está fazendo, depois que o componente é montado, verificamos o array de dependência como está vazio, ele executa quando a tela é montada, e ele pega todos os dados do localstorage que tem o 'tech' como chave e se tiver algum valor então passamos ele para o setTech, o qual vai popular o array e exibir em tela. Como ele não monitora nenhuma variável ele vai ser executado apenas uma vez.


### componentWillUnmount

Para executar uma função quando o componente é desmontado é necessário retornar uma função de dentro do useEffect, e essa é função é executada assim que o compenente for desmontar ou seja sumir da tela, isso é útil para cancelar e parar todos events listeners como setTimeout ou setInterval que tenha sido declarado e podemos criar essa função de retorno para cada useEffect se for necessário.

```
useEffect(() => {
    const storageTech = localStorage.getItem('tech');
    if (storageTech) {
      setTech(JSON.parse(storageTech));
    }

    return () => {
      document.removeEventListener();
    };
  }, []);
```

Pronto, com Hooks, conseguimos cobrir os principais ciclos de vida da aplicacação e o código ficou bem mais legível e simples de manter. Mas é bom entender todos os conceitos para não aplicar de forma errada, o bom que o eslint configurado com a regra do `react-hooks/exhaustive-deps` você vai perceber que fica impossível fazer alguma coisa errada.

Olha como ficou nosso componente até aqui:

```
import React, { useState, useEffect } from 'react';

function App() {
  const [tech, setTech] = useState([]);
  const [newTech, setNewTech] = useState('');

  function handleAdd() {
    setTech([...tech, newTech]);
    setNewTech('');
  }

  useEffect(() => {
    const storageTech = localStorage.getItem('tech');
    if (storageTech) {
      setTech(JSON.parse(storageTech));
    }

    return () => {
      document.removeEventListener();
    };
  }, []);

  useEffect(() => {
    localStorage.setItem('tech', JSON.stringify(tech));
  }, [tech]);

  return (
    <>
      <ul>
        {tech.map(t => (
          <li key={t}>{t}</li>
        ))}
      </ul>
      <input value={newTech} onChange={e => setNewTech(e.target.value)} />
      <button type="button" onClick={handleAdd}>
        Adicionar
      </button>
    </>
  );
}

export default App;
```

Código [https://github.com/tgmarinho/react-hooks/tree/aula-03-hook-useEffect](https://github.com/tgmarinho/react-hooks/tree/aula-03-hook-useEffect)
