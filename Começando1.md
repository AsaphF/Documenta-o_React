# Documentação React / Introdução

 - Esses artigos é uma tradução da nova documentação de React encontrada no site: 

[https://beta.reactjs.org/](https://beta.reactjs.org/).

 - Como o site oficial não possui no momento tradução, esses artigos servirão para quem não possui familiaridade com o inglês.

 - Também farei pequenas anotações, breves explicações que serão indentificadas com cores.

1. Começando com o básico: Nesse primeiro artigo abordará uma introdução sobre 80% dos conceitos de componentes React que são usados diariamente.

- Fonte: [https://beta.reactjs.org/learn](https://beta.reactjs.org/learn)

1.1 - Criando e Aninhando componentes: 

Os aplicativos React são feitos de componentes. Um componente é uma parte da interface do usuário (da “tela” por assim dizer) que possui a lógica e aparência vindo do componente. Um componente pode ser tão pequeno quanto um botão ou tão grande quanto uma página inteira.

Componentes React, da maneira prática, são funções JavaScript que retornam marcação:

```jsx
function MeuBotão() {
    return (
      <button>Eu sou um botão</button>
    );
  }
```

Agora que o componente “meuBotão” foi declarado, é possível aninhá-lo dentro de outro componente:

```jsx
export default function App() {
    return (
      <div>
        <h1>Bem vindo ao meu app</h1>
        <MeuBotão/>
      </div>
    );
  }
```

Observe que o “<MeuBotão/>” começa com uma letra maiúscula, esse é o indicativo que ele é um componente React. Componenetes precisam sempre comceçar com letra maiúscula, enquanto tags HTML devem ser todas minúsculas.

Não se assuste com a sintáxe nova “<MeuBotão/>”, apenas por enquanto entenda que ele é um componente que corresponde a um bloco de códigos que será renderizado na tela.

O componente “App” vai renderizar na tela um “h1” com um botão logo abaixo. Tente copiar o código acima caso deseje ver por sí só. Ou acesse a página oficial.

A palavra chave “export default” especifíca o componente principal no arquivo, caso você não seja familiar com partes da sintaxe Javascript, [MDN](https://developer.mozilla.org/en-US/) e [javascript.info](http://javascript.info) tem ótimas referências.

1.2 - Escrevendo marcação  com JSX:

A sintáxe de marcação(tags html) que você tem visto acima, é chamad de JSX.  É opcional, mas  a maioria do projetos REAT usam JSX por conveniência(Vale muito a pena usar). Todas as ferramentas recomendadas para instalação suportam JSX.(Para saber mais sobre instalação: [https://beta.reactjs.org/learn/installation](https://beta.reactjs.org/learn/installation)).

JSX é mais estrito do que HTML. É preciso fechar tags como  `<br />`. O seu componente também não pode retornar múltiplos tagas JSX, é preciso aninhar em um “pai” compartilhado, usando  `<div>...</div>` ou uma tag vazia  `<>...</>`. Dessa maneira o componente irá focar em renderizar o componente pai, e subsequente os componentes dentro dele.

```jsx
function SobrePagina() {
    return (
      <> 
        <h1>Sobre</h1>
        <p>Olá<br />Como você está?</p>
      </>
    );
  }
```

1.3 - Adcionando Estilos:

Em React, é especificado um classe CSS com `className`. Funciona da mesma maneira que o atributo HTML `class:`

```jsx
<img className="avatar" />
```

 Então você escreve as regras CSS para esse elemento em um arquivo CSS separado:

```jsx
/* No seu CSS*/
.avatar {
    border-radius: 50%;
  }
```

React não prescreve como adicionar arquivos CSS. No caso mais simples, você irá adicionar uma tag `<link/>` ao seu HTML. Se estiver usando uma ferramente de construção ou framework, consulte a documentação para aprender como adcionar CSS ao seu projeto React.

1.4 - Exibindo dados:

JSX permite por “marcações”(tags html) em Javascript. O O uso de chaves ({ }) permitem “escapar de voltar” ao Javascript para que você possa embutir algumas variáveis do seu código e exibir ao usuário. Para esse exemplo, será exibido `usuario.nome`. 

```jsx
return (
    <h1>
      {usuario.nome}
    </h1>
  );
```

Simplificando, é possível integrar valores JS dentro do HTML de uma maneira simples, onde se eu tiver uma váriavel com um determinado valor , é só abrir chaves dentro de uma tag  e colocar o nome da variável, dessa maneira o valor será exibido.

Você também pode “Escapar para o Javascript” através dos atributos JSX, para isso é preciso usar chaves ao invés de aspas. Por exemplo, `className=”avatar”` passa a string `“avatar”` como a class CSS, mas o atributo src={user.imageUrl} lê o valor da varíavel Javascript  `.usuário.imagemUrl` e então passa o valor para o atributo `src`:

```jsx
return (
    <img
      className="avatar"
      src={usuario.imagemUrl}
    />
  );
```

É possível por expressões mais complexas dentro das chaves JSX também, por exemplo, concatenações de strings:

```jsx
const usuario = {
    nome: 'Hedy Lamarr',
    imagemUrl: 'https://i.imgur.com/yXOvdOSs.jpg',
    imagemTamanho: 90,
  };
  
  export default function Perfil() {
    return (
      <>
        <h1>{usuario.nome}</h1>
        <img
          className="avatar"
          src={usuario.nome}
          alt={'Foto de ' + usuario.nome}
          style={{
            width: usuario.imagemTamanho,
            height: usuario.imagemTamanho
          }}
        />
      </>
    );
  }
```

Caso deseja consultar o que será exibido acesse: [https://codesandbox.io/s/15oriv?file=%2FApp.js&utm_medium=sandpack](https://codesandbox.io/s/15oriv?file=%2FApp.js&utm_medium=sandpack)

No exemplo acima, `style={{}}`  não é uma sintáxe especial, mas um objeto normal dentro de umas  chaves JSX `style={}`. Você pode usar o atributo `style` quando  seu estilo depender de variáveis Javascript.

1.4 - Renderização Condicional: