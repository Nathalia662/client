![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Adtech<br />
> Documento de Especificação Técnica

<br />

## Implementação da Camada de dados - Puran - Simples de tratar
Última atualização: 08/04/2021 <br />
Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

## Sumário

- [Objetivo](#objetivo)
- [Implementação](#implementa%c3%a7%c3%a3o)
- [Especificações Globais](#especifica%c3%a7%c3%b5es-globais)
- [Dimensões Globais](#dimens&otilde;es-globais)
- [Geral](#geral)
- [Login Médico](#login-medico)


## Objetivo
Este documento tem como objetivo instruir a implementação da camada de dados para utilização de recursos de monitoramento do Google Analytics referente ao ambiente:

[https://conectaconsulta.com.br/simples-de-tratar](https://conectaconsulta.com.br/simples-de-tratar)

<br />

### **Posicionamento do Código - Google Tag Manager**

#### 1. Copie o seguinte JavaScript e cole-o o mais próximo da tag `<head>` de abertura possível em todas as páginas do seu site.

```html

<html>
  <head>
    <!-- Google Tag Manager -->
    <script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start': new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0], j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src='https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f); })(window,document,'script','dataLayer','GTM-XXXXXXX');</script>
    <!-- End Google Tag Manager -->
    //...
  </head>
```

#### 2. Copie o seguinte trecho e cole-o imediatamente após a marcação `<body>` de abertura em cada página do seu site.

```html
<body>
  <!-- Google Tag Manager (noscript) -->
  <noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-XXXXXXX" height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
  <!-- End Google Tag Manager (noscript) -->
  //...
  </body>
</html>
```

Link de referência: [Documentação Oficial Google Tag Manager](https://developers.google.com/tag-manager/quickstart)


## Observações
> Os valores especificados entre colchetes `[[ ]]` são variáveis dinâmicas e devem ser substituídas por seus respectivos valores.<br />

> Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais. <br />

> Caso o site já possua o Google Analytics instalado, será necessário a remoção do código de **todas as páginas do site**: <br />

```html

<script>
(function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o), m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)})(window,document,'script','https://www.google-analytics.com/analytics.js','ga');

ga('create', 'UA-XXXXXXXX-X', 'auto');
ga('send', 'pageview');
</script>

```

---

```html

<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=UA-XXXXXXX-X"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'UA-XXXXXXX-X');
</script>
```

---

## Overview e Descrições Técnicas

### Camada de dados (DataLayer)

> É um array de objetos javascript utilizado pelo Google Tag Manager para receber em seus atributos, dados importantes do site.
Para implementar o dataLayer no site, o desenvolvedor pode utilizar formas diferentes para preencher os dados. Essas formas são dependentes da ação estabelecida na documentação e também do nível da interação.

## Observações
> Os valores especificados entre colchetes `[[ ]]` são variáveis dinâmicas e devem ser substituídas por seus respectivos valores.<br />

> Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais. <br />

---

## Implementação

### Atributos HTML (Data Attributes)

> São atributos customizados inseridos nos elementos HTML da página, permitindo a inclusão de dados adicionais.

**Instalação**
1. Elementos: ```<div>Elemento</div>``` <br />
Todos os elementos do html que serão clicados, deverão ser mapeados recebendo os atributos com sua estrutura no item.

```html
<div 	
     	data-gtm-event-category="[[exemplo:valor-categoria]]"
 	data-gtm-event-action="[[exemplo:valor-acao]]"
 	data-gtm-event-label="[[exemplo:valor-rotulo]]"
 >
	Texto do elemento
</div>
```

#### Importante:
> Também devem ter os data-attributes `data-gtm-event-category`, `data-gtm-event-action` e `data-gtm-event-label`. Preenchidos conforme instruções específicas.

<br />

### Camada de dados (DataLayer)

> É um array de objetos javascript utilizado pelo Google Tag Manager para receber em seus atributos, dados importantes do site.
Para implementar o dataLayer no site, o desenvolvedor pode utilizar formas diferentes para preencher os dados. Essas formas são dependentes da ação estabelecida na documentação e também do nível da interação.

**Instalação**<br />
Inserir a camada de dados antes do snippet de instalação do Google Tag Manager. Exemplo:


```html
<script>
	window.dataLayer = window.dataLayer || [];
	window.dataLayer.push({
		'atributo1': '[[valor1]]',
		'atributo2': '[[valor2]]'
	});
</script>
```

### Especificações Globais:

**Itens Gerais:**<br />
Todas as informações entre colchetes `[[  ]]` são variáveis dinâmicas que devem ser preenchidas com seus respectivos valores; <br />
Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais; <br />
Caso a informação solicitada não estiver disponível retornar tipagem ´undefined´.



### Dimensões Globais:

**Dimensões Customizadas para todas as páginas:**<br />
Deve ser disparado um push de dataLayer no momento de carregamento de todas as páginas do site (Considerar também todas as trocas de Path, quando o conteúdo da página é alterado mas a página não recarrega).<br />


```html
<script>
	window.dataLayer = window.dataLayer || [];
	dataLayer.push({
		'dimension1': '[[[GA ClientID]]',
		'dimension2': '[[GTM-ID]]]',
		'dimension3': '[[resposta]]'
	});
</script>
```


| Variável 				| Exemplo 				| Descrição 									|
| :--------------------	| :-------------------- | :-------------------------------------------	|
| [[GA ClientID]]	| 'XXXXXXXXXX:XXXX:XX'	| ID aleatório do Google Analytics										|
| [[GTM-ID]]			| 'GTM-xxxxxxx'		| ID do container do GTM instalado no ambiente										|
| [[resposta]] | 'sim' ou 'nao' | Deve retornar a resposta da questão.  |

---

### Geral

**Quando: Ao clicar em um dos elementos do header.**<br />

- **Onde:** Na página Simples de tratar.
    

```html
<!-- Use se os atributos no elemento a ser clicado -->
<div
     data-gtm-event-category="sanofi-conecta-consulta:simples-tratar" 
     data-gtm-event-action="clique:header" 
     data-gtm-event-label="[[nome-item]]"
>
Botão
</div>
```

| Variável 				| Exemplo 				| Descrição 									|
| :--------------	| :-------------- | :--------------------------	|
| [[nome-item]]	  | 'o-que-e', 'sintomas', 'logo' e etc | Deve retornar o nome do item clicado no header. |

<br />


**Quando: Ao clicar em um dos elementos do footer.**<br />

- **Onde:** Na página Simples de tratar.
    

```html
<!-- Use se os atributos no elemento a ser clicado -->
<div
     data-gtm-event-category="sanofi-conecta-consulta:simples-tratar" 
     data-gtm-event-action="clique:footer" 
     data-gtm-event-label="[[nome-item]]"
>
Botão
</div>
```

| Variável 				| Exemplo 				| Descrição 									|
| :--------------	| :-------------- | :--------------------------	|
| [[nome-item]]	  | 'entre', 'cadastre-se', 'medicos', 'logo' e etc | Deve retornar o nome do item clicado no footer. |

<br />

**Quando: No clique dos botões de cada seção**<br />

- **Onde:** Na página Simples de tratar.
    

```html
<!-- Use se os atributos no elemento a ser clicado -->
<div
     data-gtm-event-category="sanofi-conecta-consulta:simples-tratar" 
     data-gtm-event-action="clique:botao" 
     data-gtm-event-label="[[nome-botao]]:[[nome-secao]]"
>
Botão
</div>
```

| Variável 				| Exemplo 				| Descrição 									|
| :--------------	| :-------------- | :--------------------------	|
| [[nome-botao]]	  | 'faca-sua-pre-avaliacao-agora', 'ver-mais' e etc | Deve retornar o nome do botão clicado. |
| [[nome-secao]]	  | 'dificil-de-entender-simples-de-tratar', 'a-tiroidde-e-uma-glandula-que-fica-no-pescoco' e etc | Deve retornar o nome da seção do botão clicado.  |

<br />


**Quando: Ao clicar em algum botão de termo de politica.**<br />

- **Onde:** Na página Simples de tratar.
    

```html
<!-- Use se os atributos no elemento a ser clicado -->
<div
     data-gtm-event-category="sanofi-conecta-consulta:simples-tratar" 
     data-gtm-event-action="clique:botao" 
     data-gtm-event-label="[[nome-botao]]:termo-de-politica"
>
Botão
</div>
```

| Variável 				| Exemplo 				| Descrição 									|
| :--------------	| :-------------- | :--------------------------	|
| [[nome-botao]]	  | 'nao-aceito' ou 'aceito'. | Deve retornar o nome do botão clicado. |

<br />


**Quando: Na interação com os campos do chat**<br />

- **Onde:** Na página Simples de tratar.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'sanofi-conecta-consulta:simples-tratar',
    'eventAction': 'interacao:campo:chat',
    'eventLabel': 'preencheu:[[nome-campo]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-campo]] | 'nome', 'seu-numero-de-telefone' e etc | Deve retornar o nome do campo preenchido.  |


<br />

**Quando: No clique do botão do chat**<br />

- **Onde:** Na página Simples de tratar.
    

```html
<!-- Use se os atributos no elemento a ser clicado -->
<div
     data-gtm-event-category="sanofi-conecta-consulta:simples-tratar" 
     data-gtm-event-action="clique:botao:chat" 
     data-gtm-event-label="comecar-conversa"
>
Botão
</div>
```

<br />

**Quando: Na interação com o checkbox em "Termos de serviço"**<br />

- **Onde:** Na página Simples de tratar.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'sanofi-conecta-consulta:simples-tratar',
    'eventAction': 'interacao:termos-de-servico',
    'eventLabel': 'checkbox:concordo-com-os-termos:[[acao]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[acao]] | 'check' ou 'uncheck'| Deve retornar a ação do usuário com o checkbox.  |


<br />

**Quando:  No clique dos botões  em "Termos de serviço"**<br />

- **Onde:** Em todas as páginas que estiver disponível
    

```html
<!-- Use se os atributos no elemento a ser clicado -->
<div
     data-gtm-event-category="sanofi-conecta-consulta:simples-tratar" 
     data-gtm-event-action="clique:botao:termos-de-servico" 
     data-gtm-event-label="[[nome-botao]]"
>
Botão
</div>
```

| Variável 				| Exemplo 				| Descrição 									|
| :--------------	| :-------------- | :--------------------------	|
| [[nome-botao]] | 'nao-aceito', 'aceito' | Deve retornar o nome do botão clicado. |

<br />

**Quando: Ao interagir com os checkboxs do questionário de cada step**<br />

- **Onde:** Na página Simples de tratar.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'sanofi-conecta-consulta:simples-tratar',
    'eventAction': 'interacao:questionario:[[step]]',
    'eventLabel': 'checkbox:[[pergunta]]'
    'dimension3': '[[resposta]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[step]] | 'step-1', 'step-2' e etc | Deve retornar o step.  |
| [[pergunta]] | 'voce-sente-sua-pele-seca' e etc | Deve retornar o nome da pergunta.  |
| [[resposta]] | 'sim' ou 'nao' | Deve retornar a resposta da questão.  |

<br />

**Quando: Ao clicar nos botões do questionário de cada step**<br />

- **Onde:** Na página Simples de tratar.
    

```html
<!-- Use se os atributos no elemento a ser clicado -->
<div
     data-gtm-event-category="sanofi-conecta-consulta:simples-tratar" 
     data-gtm-event-action="clique:[[botao ou link]]:questionario:[[step]]" 
     data-gtm-event-label="[[nome-botao]]"
>
Botão
</div>
```

| Variável 				| Exemplo 				| Descrição 									|
| :--------------	| :-------------- | :--------------------------	|
| [[botao ou link]]	  | botao' ou 'link' | Deve retornar o tipo de elemento clicado. |
| [[step]] | 'step-1', 'step-2' e etc | Deve retornar o step.  |
| [[nome-botao]] | 'proximo', 'compartilhar', 'voltar' e etc | Deve retornar o nome do botão clicado .  |

<br />

**Quando: Na tentativa de callback de envio de formulário**<br />

- **Onde:** Na página Simples de tratar.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': 'sanofi-conecta-consulta:simples-tratar',
    'eventAction': 'callback:questionario',
    'eventLabel': '[[status]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[status]] | 'sucesso', 'erro:cpf-invalido', 'erro:pagina-fora-do-ar' e etc | Deve retornar a mensagem de sucesso ou o tipo de erro.  |


<br />

**Quando: Ao clicar nos links para compartilhar**<br />

- **Onde:** Na página Simples de tratar.
    

```html
<!-- Use se os atributos no elemento a ser clicado -->
<div
     data-gtm-event-category="sanofi-conecta-consulta:simples-tratar" 
     data-gtm-event-action="clique:link:compartilhar" 
     data-gtm-event-label="[[nome-link]]:[[secao]]"
>
Botão
</div>
```

| Variável 				| Exemplo 				| Descrição 									|
| :--------------	| :-------------- | :--------------------------	|
| [[nome-link]] | 'compartihar-via-whatsapp', 'compartilhar-por-email' | Deve retornar o nome do link clicado.  |
| [[secao]] |  'compartilhe-o-resultado-com-seu-medico' e etc | Deve retornar o nome da seção.  |

<br />

**Quando: No clique dos botões do formulario e-mail.**<br />

- **Onde:** Na página Simples de tratar.
    

```html
<!-- Use se os atributos no elemento a ser clicado -->
<div
     data-gtm-event-category="sanofi-conecta-consulta:simples-tratar" 
     data-gtm-event-action="clique:botao:compartilhar-e-mail" 
     data-gtm-event-label="[[nome-botao]]"
>
Botão
</div>
```

| Variável 				| Exemplo 				| Descrição 									|
| :--------------	| :-------------- | :--------------------------	|
| [[nome-botao]] | 'abrir-app', 'enviar-e-mail'. | Deve retornar o nome do botão clicado. |

<br />

### Login Médico

**Quando: Na interação com os campos.**<br />

- **Onde:** Na página de login médico.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'sanofi-conecta-consulta:login-medico',
    'eventAction': 'interacao:campo:login-medico',
    'eventLabel': 'preencheu:[[nome-campo]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-campo]] | 'crm', 'nome', 'e-mail' e etc. | Deve retornar o nome do campo preenchido.  |


<br />

**Quando: No clique dos botões.**<br />

- **Onde:** Na página de login médico.
    

```html
<!-- Use se os atributos no elemento a ser clicado -->
<div
     data-gtm-event-category="sanofi-conecta-consulta:login-medico" 
     data-gtm-event-action="clique:botao" 
     data-gtm-event-label="[[nome-botao]]"
>
Botão
</div>
```

| Variável 				| Exemplo 				| Descrição 									|
| :--------------	| :-------------- | :--------------------------	|
| [[nome-botao]] | 'acessar' | Deve retornar o nome do botão clicado.  |

<br />

**Quando: Na interação com os filtros**<br />

- **Onde:** Na página de login médico.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': 'sanofi-conecta-consulta:login-medico',
    'eventAction': 'interacao:filtro',
    'eventLabel': '[[nome-filtro]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-filtro]] | 'cardiologia', 'oncologia' e etc.. | Deve retornar o nome do campo preenchido.  |


<br />

**Quando: Na tentativa de callback para efetuar o login.**<br />

- **Onde:** Na página de login médico.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'conversion',
    'eventCategory': 'sanofi-conecta-consulta:login-medico',
    'eventAction': 'callback',
    'eventLabel': '[[status]]'
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[status]] | 'sucesso', 'erro:usuario-ou-senha-invalidos', 'erro:pagina-fora-do-ar' e etc | Deve retornar a mensagem de sucesso ou o tipo de erro.   |


<br />



> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

<script> document.querySelector('h1').style.display = 'none' </script>
