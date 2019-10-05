## Aula 04 - Hook useMemo

Esse hook é indicado para fazer cálculos mais complexos no componente, e são úteis para componentes sensíveis que tem muita renderização. Então componentes que possuem cáclulos e  muitas alterações de estado, vão renderizar sempre que cada estado alterar e o `useMemo` vem para otimizar isso, podemos criar uma propriedade que recebe um valor e é recalculado apenas se um estado específico alterar e estiver no array de dependência no `useMemo`.

Exemplo aqui: `<strong>Você tem {tech.length} tecnologias</strong>`

Toda vez que qualquer estado altearr esse tech.length será executado, tá ele é simples e tals, mas se fosse um formatPrice, ou calculaImposto, ai seria custoso, e imagina que alterou um estado qualquer da aplicação que não tem nada haver com algo que haja necesidade de formatar preço ou calcular imposto ser renderizado refazendo todo o calculo.

O que podemos fazer é utilizar o useMemo, importando-o:

```
import React, { useState, useEffect, useMemo } from  'react';
...
```

Criar uma variável que armazena um valor, e a cada alteração no estado de `tech` então o `useMemo` é executado alterando o valor do `techSize`:

```
const techSize =  useMemo(() => tech.length, [tech]);
```

E alterar para otimizar o código:

```
...
<strong>Você tem {techSize} tecnologias</strong>
...
```

Pronto, agora o `techSize` só alterar se o `tech` alterar. Isso é muito bom!

Portanto, se precisar fazer algum cálculo no `render` então `useMemo`.

Código [https://github.com/tgmarinho/react-hooks/tree/aula-03-hook-useMemo](https://github.com/tgmarinho/react-hooks/tree/aula-03-hook-useMemo)
