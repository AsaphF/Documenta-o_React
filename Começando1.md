# Documentação React / Introdução

 - Esses artigos é uma tradução da nova documentação de React encontrada no site: 

[https://beta.reactjs.org/](https://beta.reactjs.org/).

 - Como o site oficial não possui no momento tradução, esses artigos servirão para quem não possui familiaridade com o inglês.

 - Também farei pequenas anotações, breves explicações que serão indentificadas com cores.

## 1. Começando com o básico: Nesse primeiro artigo abordará uma introdução sobre 80% dos conceitos de componentes React que são usados diariamente.

- Fonte: [https://beta.reactjs.org/learn](https://beta.reactjs.org/learn)

### 1.1 - Criando e Aninhando componentes: 

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

### 1.2 - Escrevendo marcação  com JSX:

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

### 1.3 - Adcionando Estilos:

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

### 1.4 - Exibindo dados:

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

### 1.4 - Renderização Condicional:

Em React, não há uma sintaxe especial para escrever condicionais. Ao invés disso,  você irá usar as mesmas técnicas(loops, operador ternários…) que já usa ao escrever códigos Javascript normais. Por exemplo, você pode usar uma expressão `if` para condicionalmente incluir JSX:

```jsx
let conteudo;
if (estaLogado) {
  conteudo = <PainelAdmin />;
} else {
  conteudo = <LoginForm />;
}
return (
  <div>
    {comteudo}
  </div>
);
```

Quando você não precisar da opção `else`, você também por usar o [Operador de lógica "&&"](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_AND#short-circuit_evaluation).

```jsx
<div>
  {estaLogado && <PainelAdmin />}
</div>
```

Todas essas abordagens também funcionam ao especificar atributos condicionalmente. Se você desconhece algumas sintáxes de Javascript, você pode começar usando `if…else` (Apesar de que recomendo ter uma base boa em JS primeiro.)

### 1.5 - Renderização de Listas:

Você irá depender de recursos do Javascript com [for loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for) e [método map de arrays](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) para renderizar lista de componentes.

Por exemplo, digamos que você possui um arry de produtos:

```jsx
produtos const = [
  { titulo: 'Repolho', id: 1 },
  { titulo: 'Alho', id: 2 },
  { titulo: 'Maça', id: 3 },
]
```

Dentro do seu componentes, use o métido `map()` parar transformar esse array de produtos  em array de itens `<li>`:

```jsx
const listaItens = produtos.map(produto =>
  <li key={produto.id}>
    {produto.titulo}
  </li>
);

return (
  <ul>{listaItens}</ul>
);
```

Perceba que `< li >` possui um atributo `key` . Para cada item na lista, você de passar uma string ou um número que indetifique de forma única cada item entre seus irmãos. Geralemente, uma key deverá vir dos dados, também como do banco de dados. React vai depender nessas keys para entender o que deve acontecer se você depois inserir, deletar ou reorganizar os items.   [Clique  para ver o resultado](https://codesandbox.io/s/xtczu1?file=%2FApp.js&utm_medium=sandpack).

### 1.6- Respondendo a Eventos :

Você pode responder a eventos declarando *event handler (manipulador de eventos)* dentro dos seus componentes:

```jsx
function MyButton() {
  function handleClick() {
    alert('You clicked me!'); //***
  }

  return (
    <button onClick={handleClick}>
      Click me
    </button>
  );
}
```

Perceba como  `onClick={handleClick}` não possiu parênteses no final! Não chame a função de manipulação de evento: você precisa apenas passar o seu nome. React vai chamar o seu manipulador de evento quando o usuário clicar no botão.(Perceba nesse detalhe, o própio React vai fazer isso ao invés de você precisar fazer como é ao usar Vanilla JS, isso vai ser importante para depois.) 

### 1.7- Atualizando a tela:

Frequentemente, você vai querer que o seu componente “lembre” alguma informação e a exiba. Por exemplo, talvez deseje que conte o número de vezes que um botão é clicado. Para isso, adcione um “estado” no seu componente.

Primeiro, importe `useState` do React:

`import React from "react”`

Agora você pode declarar uma *variável de estado* dentro do seu componente.

```jsx
function MeuBotão() {
  const [contagem, setContagem] = useState(0);
```

Você irá pegar duas coisas do `useState` : o valor atual do estado(`contagem`), e uma função que te permite atualizá-lo(`setContagem`). Você pode dar eles qualquer nome, mas a convenção é chamá-los `[algumaCoisa, setAlgumaCoisa]` .

A primeira vez que o botão é exibido, `contagem` irá ser `0` porquê você passou `0` no `useState()` . Quando você quer que o estado mude, chame `setContagem` e passe um novo valor nele. Apertando nesse botão irá somar a contagem:

```jsx
function MeuBotão() {
  const [contagem, setContagem] = useState(0);

  function cliqueContagem() {
    setContagem(contagem + 1);
  }

  return (
    <button onClick={cliqueContagem}>
      Clicou{contagem} vezes.
    </button>
  );
}
```

React irá chamar sua função componente de novo. Dessa vez, `contagem` será `1`. Daí será `2` e assim por diante. 

Se você renderizar o mesmo componente múltiplas vezes, cada vez terá o seu próprio estado. [Clique para testar se houve dois diferentes botões.](https://codesandbox.io/s/1ghtss?file=%2FApp.js&utm_medium=sandpack) (*)

Perceba que cada botão “relembra” seu próprio estado `contagem` e não afeta outros botões(No link acima).

### 1.8- Usando Hooks:(Aqui que a diversão começa)

Funções começando com `use` são chamadas de *hooks(ganchos).* `useState` é um “hook já construído” providenciado pelo React. Você pode achar outros hooks na [referência React API](https://beta.reactjs.org/reference/react) (Ainda não traduzida). Você também poder escrever os seus próprios hooks combinando os já existente.

Hoooks são mais restritivos que funções normais. Você apenas pode chamar um hook *na parte mais acima* dos seus componentes(ou de outros hooks). Se você quer usar `useState` em um condicional ou em um loop, extraia um novo componente e o ponha lá.

### 1.9- Compartilhando dados entre componentes:

No exemplo anterior*, cada `MeuBotão` tinha sua própria indepedente `contagem`, e quando cada botão foi cliquado, apenas a `contagem` do botão clicado foi alterado. (Acesse caso deseja ver os gráficos originais [https://beta.reactjs.org/learn#sharing-data-between-components](https://beta.reactjs.org/learn#sharing-data-between-components) )

[![Gráfico Botões]]([https://beta.reactjs.org/_next/image?url=%2Fimages%2Fdocs%2Fdiagrams%2Fsharing_data_child.dark.png&w=640&q=75](https://beta.reactjs.org/_next/image?url=%2Fimages%2Fdocs%2Fdiagrams%2Fsharing_data_child.dark.png&w=640&q=75))

Incialmente, cada `Mybutton`  tem `count` em `0`

[![GráficoBotões]]

([https://beta.reactjs.org/_next/image?url=%2Fimages%2Fdocs%2Fdiagrams%2Fsharing_data_child_clicked.dark.png&w=640&q=75](https://beta.reactjs.org/_next/image?url=%2Fimages%2Fdocs%2Fdiagrams%2Fsharing_data_child_clicked.dark.png&w=640&q=75))

        O primeiro `Mybutton` atualiza sua `count` para `1`

Apesar disso, frequentemente você irá precisar componentes que compartilhem dados e sempre se atualizem juntos. (Acesse caso deseja ver os gráficos originais [https://beta.reactjs.org/learn#sharing-data-between-components](https://beta.reactjs.org/learn#sharing-data-between-components) )

Para fazer que os dois componentes `Mybutton` exibam a mesma `count` e atualizem juntos, você precisa mover o estado dos botões individualmente “para cima” para o componente mais próximo que os contêm. 

Nesse exemplo, esse componente “Pai” é o `MyApp`:

[![Gráfico Botões]]([https://beta.reactjs.org/_next/image?url=%2Fimages%2Fdocs%2Fdiagrams%2Fsharing_data_child.dark.png&w=640&q=75](https://beta.reactjs.org/_next/image?url=%2Fimages%2Fdocs%2Fdiagrams%2Fsharing_data_parent.dark.png&w=640&q=75))

Incialmente, o estado `count` do `MyApp`  é  `0` e está sendo passado para ambos os filhos.

[![GráficoBotões]]

([https://beta.reactjs.org/_next/image?url=%2Fimages%2Fdocs%2Fdiagrams%2Fsharing_data_child_clicked.dark.png&w=640&q=75](https://beta.reactjs.org/_next/image?url=%2Fimages%2Fdocs%2Fdiagrams%2Fsharing_data_child_clicked.dark.png&w=640&q=75))

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2c7cc8ea-8964-4e0f-ae03-54d590ff0591/Untitled.png)

        Ao clicar,  `MyApp`  atualiza seu estado `count` para `1` e o passa para ambos seus filhos(atualizando seus estados).

Agora, quando você clicar em qualquer botão, o `count` em `MyApp` irá mudar, onde irá mudar ambas contagens (counts) em `MyButton`. Aqui está como você poder expressar isso em código.

Primeiro, mude o estado do `MyButton` para o `MyApp`:

```jsx
export default function MyApp() {
// Para colocar nessa...
  const [count, setCount] = useState(0);
  
	function handleClick() {
    setCount(count + 1);
  }
// parte.
  return (
    <div>
      <h1>Counters that update separately</h1>
      <MyButton />
      <MyButton />
    </div>
  );
}

function MyButton() {
  // ... Estamos tirando daqui ...
}
```

Em seguida, passe o estado de `MyApp` para cada `MyButton`, juntamente com o manipulador de click compartilhado. Você pode passar informações para `MyButton` usando as chaves JSX, assim como você fez anteriormente com tags internas como `<img>`:

```jsx
export default function MyApp() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
  }

  return (
    <div>
      <h1>Counters that update together</h1>
      **<MyButton count={count} onClick={handleClick} />  
      **<MyButton count={count} onClick={handleClick} />
    </div>
  );
}
```

A informação que você passa é chamada de “props”(propriedades). Agora, o componente `MyApp` contém o estado de contagem(`count`) e o manipulador de eventos `handleClick` e passa ambos como props para cada um dos botões.
Por fim, é preciso alterar `MyButton` para ler os props que você passou de seu componente pai:

```jsx
function MyButton({ count, onClick })** {
  return (
    <button onClick={onClick}>**
      Clicked {count} times
    </button>
  );
}
```

Quando você clica no botão, o manipulador `onClick` é acionado. A propriedade `onClick` de cada botão foi definida para a função `handleClick` dentro de `MyApp`, para que o código dentro dela seja executado. Esse código chama `setCount(count + 1)`, incrementando a variável de estado `count`. O novo valor de contagem(`count`) é passado como prop para cada botão, então todos eles mostram o novo valor.
Isso é chamado de “Levantando o estado para um componente acimar”. Ao mover o estado para cima, nós o compartilhamos entre os componentes.

Para ver o resultado acesse o [link](https://codesandbox.io/s/sqqsbh?file=%2FApp.js&utm_medium=sandpack).

# 2. Pondo em prática / ****Tutorial: Tic-Tac-Toe****: