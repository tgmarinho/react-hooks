
Para aprender Hooks, vamos criar um projeto:

```
npx create-react-app react-hooks
```

Instalar o Eslint:

```
yarn add eslint -D
```

Executar o comando:

```
yarn eslint --init
```

E configure com os seguintes passos:

```
yarn eslint --init
yarn run v1.12.0
warning package.json: No license field
$ /Users/tgmarinho/Developer/bootcamp_rocketseat_studies/node_modules/.bin/eslint --init
? How would you like to use ESLint? To check syntax, find problems, and enforce code style
? What type of modules does your project use? JavaScript modules (import/export)
? Which framework does your project use? React
? Does your project use TypeScript? No
? Where does your code run? (Press <space> to select, <a> to toggle all, <i> to invert selection)Browser
? How would you like to define a style for your project? Use a popular style guide
? Which style guide do you want to follow? Airbnb (https://github.com/airbnb/javascript)
? What format do you want your config file to be in? JavaScript
Checking peerDependencies of eslint-config-airbnb@latest
The config that you've selected requires the following dependencies:
eslint-plugin-react@^7.14.3 eslint-config-airbnb@latest eslint@^5.16.0 || ^6.1.0 eslint-plugin-import@^2.18.2 eslint-plugin-jsx-a11y@^6.2.3 eslint-plugin-react-hooks@^1.7.0
? Would you like to install them now with npm? Yes
```

Depois crie o arquivo `.editorConfig`:

```
root = true

[*]
end_of_line = lf
indent_style = space
indent_size = 2
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true
```

Depois instalei o `prettier` e seus plugins, e o `babel-eslint`:

```
yarn add prettier eslint-config-prettier eslint-plugin-prettier babel-eslint -D
```

Crie o arquivo `.prettierrc`:

```
{
  "singleQuote": true,
  "trailingComma": "es5"
}
```

E por fim configurei o `.eslintrc.js`:

```
module.exports = {
  env: {
    browser: true,
    es6: true,
  },
  extends: ['airbnb', 'prettier', 'prettier/react'],
  globals: {
    Atomics: 'readonly',
    SharedArrayBuffer: 'readonly',
  },
  parser: 'babel-eslint',
  parserOptions: {
    ecmaFeatures: {
      jsx: true,
    },
    ecmaVersion: 2018,
    sourceType: 'module',
  },
  plugins: ['react', 'prettier'],
  rules: {
    'prettier/prettier': 'error',
    'react/jsx-filename-extension': ['warn', { extensions: ['.jsx', 'js'] }],
    'import/prefer-default-export': 'off',
  },
};
```


Pronto! Essas configurações são básicas para estruturar o projeto em React, agora tudo que fizermos será referente ao React Hooks, primeiro vamos instalar uma dependência que nos ajuda a não programar Hooks de forma errada, ele vai mostrar pra gente tudo que estivermos fazendo errado:

```
yarn add eslint-plugin-react-hooks -D
```

E lá no `.eslintrc.js`, adicionamos o `plugin`:

```
plugins: ['react', 'prettier', 'react-hooks'],
```

E na `rules` adicionamos mais duas linhas:

```
 rules: {
    'prettier/prettier': 'error',
    'react/jsx-filename-extension': ['warn', { extensions: ['.jsx', 'js'] }],
    'import/prefer-default-export': 'off',
    'react-hooks/rules-of-hooks': 'error',
    'react-hooks/exhaustive-deps': 'warn',
  },
```

Explicando:
`react-hooks/rules-of-hooks` : avisa todo infringimento  das regras dos hooks
`react-hooks/exhaustive-deps`: auxilia a usar os useEffects na parte de dependências que vamos ver mais pra frente.

Agora sim podemos codar!

Código [https://github.com/tgmarinho/react-hooks/tree/aula-01-configurando-estrutura](https://github.com/tgmarinho/react-hooks/tree/aula-01-configurando-estrutura)
