# Aula 1
## Alguns termos:
### SPA
#### Single*page Application 
* A página não precisa ser totalmente recarregada para atualizar conteúdo.
* Melhora na experiência de usuário.
```
  // Efeitos colaterais (side-effects) dentro da aplicação
  // useEffect(oQueExecutar, [quandoExecutar])
  // passar um [] executa uma única vez, quando o componente é carregado
  useEffect(() => {
    fetch('http://localhost:3333/episodes')
      .then(response => response.json())
      .then(data => console.log(data))
  }, [])
```

### JSON
#### JavaScript Object Notation
* Reconhecido, utilizado e compatível com praticamente todas tecnologias WEB.
* Notação para retornar dados em forma de objetos JS.
* Utilizado por navegadores web, mobile, etc.

```
[
  {
    "name": "Mateus",
    "id": 1,
    "age": 26
  }
  {
    ...
  }
]
```
### API
#### Application Programming Interface
* Uma interface que retorna dados (geralmente no formato JSON) para utilização em outras aplicações
* Geralmente o servidor BACKEND atua como uma <strong>API RESTful</strong>.

## REACT
### Geral
* Construção da interface é realizada pelo browser através da execução de JS pelo REACT
  * Transformar dados em HTML, CSS, JS
  * Client Side JS
* <strong>Não</strong> consegue mostrar componentes um abaixo do outro sem a tag <code><> </></code> ao redor.
  * Conceito de FRAGMENT
* Métodos e atributos HTML no React sempre seguem o camelCase (ex: ```<button onClick>```)
* React Hook (métodos começados em USE) só podem ser utilizados dentro do componente, não dentro do static por exemplo
### Conceitos
#### Componente
* Uma função que retorna HTML
#### Propriedade
* Informação que passa de um componente PAI para um componente FILHO
* Seria o atributo do HTML
* Propriedade global criada pelo react: <code>children</code>
  * Quando é passado algo dentro de um componente, ele automaticamente vai como <code>children</code>.
  * EX ao retornar no APP.js para a ```<div id="root">``` 
    * ```<Button>Button 1</Button>```
    * ou ```<Button title="Button 1" />``` 

* Arquivo Button.js
```
// Property as Children
export default function Button(props){
  return {
    <button>{props.children}</button>
  }
} 

// Property passed as title
export default function Button(props){
  return {
    <button>{props.title}</button>
  }
} 
```

#### Estado
* Manipular informações de dentro de um componente
* O usuário manipula essas informações (estados) quando realiza alguma ação no componente.
* Para atualização de variáveis (informações) em tela é necessário o conceito de Estado, pois o REACT não fica monitorando as variáveis.
* Como o estado é configurado dentro do componente, para cada componente há um estado independente

* Importando:
```
import { useState } from 'react';
```
  * A função <strong>useState</strong> devolve um array [state, setState]
* Declarando um estado
```
const [counter, setCounter] = useState(counterValue);
```
### PROBLEMAS
#### Indexação para SEOs
* O cliente faz a solicitação, o post gera uma request para a API que retorna os dados em formato JSON e então o cliente transforma em formato WEB.
  * Devido a esta demora, os crawlers não aguardam a transformação do conteúdo e vêem como página vazia ( sendo assim, não indexam a página )

### Ferramentas para solucionar este problema
#### SSR (Server-side Rendering)
* 2 servidores, um responsável pela renderização e outro pelo resto.
```export async function getServerSideProps(){}```
* Colocando esta função em qualquer arquivo na pasta pages de qualquer componente já diz que deve ser executada esta função antes de exibir o conteúdo final para o usuário 
* Executada TODA VEZ que for acessada por algum usuário

#### SSG (Static Site Generation)
* Definir um intervalo de tempo para manter o arquivo HTML estático cacheable em algum HD. Evitando criação do site diversas vezes sabendo que o conteúdo não muda com frequência.
* Após o acesso a página por uma pessoa, ele gera um HTML estático puro que será enviado para todos os novos acessos até a atualização da página acontecer.
```export async function getStaticProps(){}```

#### Gatsby
* Focado no SSG

#### NextJS (Server NODE)
* O browser faz a requisição para o Node (NextJS), que puxa os dados do backend (API REST) em formato JSON, converte para HTML CSS E JS e devolve para o browser a página pronta. (MODELO SSR)
* Para páginas públicas
  * *** Possui um componente chamado Image - Este componente formata e otimiza a imagem sem necessitar tratativa do backend ou de algum editor
  * *** as propriedades Width e Height não se referem a apresentação, e sim ao tamanho que a imagem deve ser carregada.
  * *** É necessário passar os dominios de hospedagem em um arquivo next.config.js.
  ```
  module.exports = {
    images: {
      domains: ['storage.googleapis.com']
    }
  };
  ```
* File System Routing
  * o nome dos arquivos na pasta page que não começam com _ são os arquivos que formam as rotas da aplicação

# Aula 2

## Extras
### SASS 
* sass-lang.com
* Pré Processador CSS
* Encadeamento de CSS 
```
body {
  background: #333;

  h1 {
    background: #000;
  }
}
```

## TypeScript?
* Tipagem estática vs JS (tipagem dinâmica)
* Manutenção do código facilitada
* Ajuda na hora da tipagem das PROPRIEDADES do COMPONENTE
* Passagem de parâmetros
* Só roda em desenvolvimento, em produção é convertido totalmente para JS
### Arquivos .js para .tsx
* tsx = typescript + jsx (xml no JavaScript)
```
type User = {
  name: string;
  address: {
    city: string;
    state: string;
  }
}
```
```
terminal: yarn add typescript @types/react @types/node -D
```
## FAKE API
* Subir um projeto BACKEND na máquina que funciona como API porém é FICTÍCIA.
### JSON SERVER (dependencia para simular uma API)

### Arquivo _app.tsx 
* Arquivo global, vai envolver todas as páginas da aplicação
* É construído a cada chamada de rota
#### Componentes sempre presentes na aplicação devem vir no _app.tsx

### Arquivo _document.tsx
* Arquivo global, vai envolver todas as páginas da aplicação
* É construído uma única vez

### MODULE CSS 
* Ele apenas estiliza o componente que está atrelado

### DATE-FNS
* Biblioteca para trabalhar com datas dentro do JS (Recomendado pelo Diego)

# Aula 3

* CRIAR A HOME E PÁGINA DO PODCAST

* As funções possuem tipagem.
Exemplo: ```import { GetStaticProps } from 'next'```

* Formatar os dados logo após a chamada da API por questões de performance

* Estruturas de repetição dentro do REACT precisa obrigatoriamente no primeiro elemento que retorna da propriedade KEY
  * Essa propriedade existe por padrão em todos os componentes do REACT
  * Serve para manutenção das listas, tendo que recriar toda a lista novamente (em um ambiente com muitos dados pode ter performance reduzida)

### SLUG
* uma string formatada de uma maneira url-friendly.

### AXIOS ?

# 4 aula
## RANDOM STATIC REGENERATION
* Páginas SSG que podem ser dinâmicas
* Funcionamento da geração de páginas dinâmicas

```
export const getStaticPaths: GetStaticPaths = async () => {
  return {
    paths: [
      { params: { slug: 'a-importancia-da-contribuicao-em-open-source' } }
    ],
    fallback: 'blocking',
  }
}
```
* Ao passar os paths vazios, o next não vai gerar nenhuma página estática.
* fallback = false irá retornar o 404.
* fallback = true irá gerar uma página estática após o acesso do usuário. (Client Side)#
  * Para corrigir o erro de geração de página, porque o client não espera o carregamento dos dados deve-se importar a função useRouter() e utilizar seu método isFallback?
* fallback = blocking irá gerar uma página estática
```
import { useRouter } from 'next/routes'

const router = useRouter()

if(router.isFallback){
  return (
    <p>Carregando...</p>
  )
}
```
* fallback = blocking irá gerar a página estática na camada do NEXT.JS

* blocking e true = incremental static regeneration

## Context API
* Monitora as informações em um dado contexto e atualiza a cada alteração.

## REACT
* Ao passar parâmetros para uma função, é necessário passá-la através de uma arrow function, pois o react reconhece como se estivesse passando o retorno da função.
Ex: 
  * onClick=<del>{play(episode)}</del> 
  * onClick=<mark>{() => play(episode)}</mark>

### RC-SLIDER
* Biblioteca react para slider

### Tricks
* quando queremos validar mas sem o else, podemos usar a propriedade seguida de dois &&
* quando queremos validar só o else usamos o ||
Ex: { episode && código para executar } e { episode || código para executar }

* acessar um elemento nativo pelo react - utilizar REFS
( criar uma referência para o elemento que quer manipular )
  * sempre iniciar com null

```
const audioRef = useRef<HTMLAudioElement>(null);

<audio
            src={episode.url}
            ref={audioRef}
            autoPlay
          />
```
* Principio da Imutabilidade em React. (Trouxe do paradigma funcional)
  * Quando for criar uma nova informação, copiar a informação anterior e criar uma nova e não atualizá-la.