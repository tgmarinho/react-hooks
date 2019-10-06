## Aula 05 - Hook useCallback

 Ele é parecido com `useMemo`, a diferença que ele retorna uma função, e nós utilizaremos o `useCallback` quando  criamos funções dentro dos componentes. a exemplo da função `handleAdd()` que temos na função `App` que é o componente. Toda vez que o render é chamado, essa função interna `handleAdd` e outras que esse componente possuir vai ser criada, e criar cada função consome processamento e nesse caso é um processamento inútil, só precisamos que a função seja criada uma única vez. E ai que entra o `useCallback`.

```
import React, { useCallback } from  'react';
```

Vamos refatorar a função `handleAdd`, para usar `useCallback`:

```
  function handleAdd() {
    setTech([...tech, newTech]);
    setNewTech('');
  }
```

Olhá só como é parecido com tudo que já fizemos nos outros hooks:

```
 const handleAdd = useCallback(() => {
    setTech([...tech, newTech]);
    setNewTech('');
  }, [newTech, tech]);
```

Declaro uma constante `handleAdd` que recebe a chamada do `useCallback` que recebe uma arrow function que contém toda a lógica da função, e no final ela recebe o array de dependências. E tudo funciona normalmente.

E agora função interna do `handleAdd` só será recriada se os estados `newTech` e `tech` forem alterados, semelhante ao `useMemo` e `useEffect`.

O useCallback só é utilizado em funções que alteram o estado interno do componente.

Pronto! Simples assim! Vimos até aqui os principais Hooks do React.

Código [https://github.com/tgmarinho/react-hooks/tree/aula-05-hook-useCallback](https://github.com/tgmarinho/react-hooks/tree/aula-05-hook-useCallback)
