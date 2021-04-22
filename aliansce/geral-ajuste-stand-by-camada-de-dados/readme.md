![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Adtech<br />
> Documento de Especificação Técnica

<br />

## Ajustes/implementações da Camada de dados - Geral
Última atualização: 22/04/2021 <br />
Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

## Sumário

- [Objetivo](#objetivo)
- [Implementação](#implementa%c3%a7%c3%a3o)
- [Geral](#geral)
- [Home](#home)
- [Shopping](#shopping)
- [Area logada](#area-logada)
- [Vitrine de produtos](#Vitrine-de-produtos)

## Objetivo
Este documento tem como objetivo instruir a implementação da camada de dados para utilização de recursos de monitoramento do Google Analytics referentes aos ambientes:

[www.bangushopping.com](www.bangushopping.com),
[www.boulevardshoppingbauru.com.br](www.boulevardshoppingbauru.com.br),
[www.boulevardbelem.com.br](www.boulevardbelem.com.br),
[www.boulevardshopping.com.br](www.boulevardshopping.com.br),
[www.boulevardcampos.com.br](www.boulevardcampos.com.br),
[www.boulevardvilavelha.com.br](www.boulevardvilavelha.com.br),
[www.boulevardshoppingbrasilia.com.br](www.boulevardshoppingbrasilia.com.br),
[www.cariocashopping.com.br](www.cariocashopping.com.br),
[www.caxiasshopping.com.br](www.caxiasshopping.com.br),
[www.parqueshoppingba.com.br/](www.parqueshoppingba.com.br/),
[www.parqueshoppingbelem.com.br](www.parqueshoppingbelem.com.br),
[www.maceioparqueshopping.com.br](www.maceioparqueshopping.com.br),
[www.passeioshopping.com.br](www.passeioshopping.com.br),
[recreioshopping.com.br](recreioshopping.com.br),
[www.santanaparqueshopping.com.br](www.santanaparqueshopping.com.br),
[www.saogoncaloshopping.com.br/](www.saogoncaloshopping.com.br/),
[www.shoppingdabahia.com.br](www.shoppingdabahia.com.br),
[www.shoppinggranderio.com.br](www.shoppinggranderio.com.br),
[www.shoppingparangaba.com.br](www.shoppingparangaba.com.br),
[www.shoppingtaboao.com.br](www.shoppingtaboao.com.br),
[www.viaparqueshopping.com.br](www.viaparqueshopping.com.br),
[www.westplaza.com.br](www.westplaza.com.br),
[www.shoppingpracanovaaracatuba.com.br](www.shoppingpracanovaaracatuba.com.br),
[www.boulevardlondrinashopping.com.br/](www.boulevardlondrinashopping.com.br/),
[www.francashopping.com.br/](www.francashopping.com.br/),
[www.manauarashopping.com.br/](www.manauarashopping.com.br/),
[www.parquedpedro.com.br/](www.parquedpedro.com.br/),
[www.passeiodasaguasshopping.com.br/](www.passeiodasaguasshopping.com.br/),
[www.shoppingcampolimpo.com.br/](www.shoppingcampolimpo.com.br/),
[www.shoppingmetropole.com.br/](www.shoppingmetropole.com.br/),
[www.plazasulshopping.com.br/](www.plazasulshopping.com.br/),
[www.uberlandiashopping.com.br/](www.uberlandiashopping.com.br/),<br />
[www.pracanovashopping.com.br](www.pracanovashopping.com.br),<br />
[boulevardfeira.com.br/](boulevardfeira.com.br/)<br />
[www.montesclarosshopping.com.br/](https://www.montesclarosshopping.com.br/)<br />

<br />

## Observações
> Os valores especificados entre colchetes `[[ ]]` são variáveis dinâmicas e devem ser substituídas por seus respectivos valores.<br />

> Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais. <br />

---

## Implementação

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
---

<H3 align="center"> AJUSTES/STAND BY </h3>

### Geral

**Quando: Ao clicar no modal (implementar)**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html

<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:geral',
    'eventAction': 'clique:modal',
    'eventLabel': '[[nome-item]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]]  | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao'| Deve retornar o nome do ambiente.  |
| [[nome-item]]  | 'renault-kmd', '10%-desconto-frete-gratis' e etc| Deve retornar o titulo do modal. |


<br />

**Quando:  No clique do botão "ver mais horários" no submenu do horário de funcionamento no header(implementar)**<br />

- **Onde:**  Em todas as páginas que estiver disponível.
    
```html

<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:geral',
    'eventAction': 'clique:menu',
    'eventLabel': '[[item-menu]]:[[item-submenu]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]]  | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao'| Deve retornar o nome do ambiente.  |
| [[nome-item]]  | 'renault-kmd', '10%-desconto-frete-gratis' e etc| Deve retornar o titulo do modal. |


<br />

**Quando:  No clique dos botões ou links de cada seção (ajustar categoria)**<br />

- **Onde:**  Na página home.
    
```html

<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:geral',
    'eventAction': 'clique:[[botao-ou-link]]',
    'eventLabel': '[[secao]]:[[nome-item]]'
  });
</script>

```
| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]]  | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao'| Deve retornar o nome do ambiente.  |
| [[botao-ou-link]] | Deve retornar o tipo de elemento clicado. | 'botao' ou 'link' |
| [[secao]] | 'acontece', 'lojas', 'cinema' e etc| Deve retornar o nome da seção.   |
| [[nome-item]]  | Deve retornar o nome do item clicado. | 'leia-mais', 'agenda', 'buscar', 'todos-os-filmes' e etc|

<br />

---

### Home

**Quando:  No clique do botão "saiba mais" do banner(implementar)**<br />

- **Onde:**  Na página home.
    
```html

<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:home',
    'eventAction': 'clique:botao:banner',
    'eventLabel': 'saiba-mais'
  });
</script>

```
<br />

---

### Shopping

**Quando: No clique dos link de telefone e e-mail (implementar)**<br />

- **Onde:**  Na página comercialização.
    
```html

<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:comercializacao',
    'eventAction': 'clique:link',
    'eventLabel': '[[nome-item]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-item]]  | 'tel:(11)5512-5200'e 'e-mail:@aliansce.com.br'| Deve retonar o nome do link clicado. |


<br />

---

### Area logada

**Quando: Na interação com os checkbox do formulário dados de cadastro (Ajustar categoria)**<br />

- **Onde:**  Na página "Editar Perfil" na área logada do site.
    
```html

<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:area-logada:editar-perfil',
    'eventAction': 'interacao:checkbox:formulario-dados-de-cadastro',
    'eventLabel': '[[acao]]:[[nome-checkbox]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]]  | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao'| Deve retornar o nome do ambiente. |
| [[acao]]  | 'check', 'uncheck'. | Deve retornar a ação do usuário.|
| [[nome-checkbox]]   | 'por-telefone'', 'por-email' e etc| Deve retornar o nome do checkbox. |


<br />

---

### Vitrine de produtos

**Quando: Na interação com o campo de filtro (implementar)**<br />

- **Onde:**   Na página Vitrine de produtos.
    
```html

<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:vitrine-produtos',
    'eventAction':'interacao:filtro',
    'eventLabel': '[[tipo-filtro]]:[[nome-item]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]]  | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao'| Deve retornar o nome do ambiente. |
| [[nome-item]]   |  'artigos-diversos', 'conveniencia-servicos', 'alimentacao' e etc. | Deve retornar o nome do item escolhido no filtro|
| [[tipo-filtro]]   | 'categoria', 'lojar' ou 'canais'.| Deve retornar o tipo do filtro onde o usuário está interagindo.|


<br />

**Quando: No clique em alguma loja (implementar)**<br />

- **Onde:**   Na página Vitrine de produtos.
    
```html

<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:vitrine-produtos',
    'eventAction':'clique:loja',
    'eventLabel': '[[nome-loja]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]]  | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao'| Deve retornar o nome do ambiente. |
| [[nome-loja]]  |'a-especialista', 'academia-bodytech' e etc| Deve retornar o nome da loja clicada|

<br />

**Quando: No clique dos botões de alguma loja (implementar)**<br />

- **Onde:**   Na página Vitrine de produtos.
    
```html

<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:vitrine-produtos',
    'eventAction':'clique:botao:loja',
    'eventLabel': '[[nome-loja]]:[[nome-botao]]'
  });
</script>

```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-ambiente]]  | 'shopping-leblon', 'parque-d-pedro', 'shopping-taboao'| Deve retornar o nome do ambiente. |
| [[nome-loja]]  |'a-especialista', 'academia-bodytech' e etc| Deve retornar o nome da loja clicada|
| [[nome-botao]]   |'whatsapp', 'site-da-loja', 'drive-thru' e etc| Deve retornar o nome do botão clicado.|

<br />

**Quando: No clique dos botões de alguma loja (implementar)**<br />

- **Onde:**   Na página Vitrine de produtos.
    
```html

<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:vitrine-produtos',
    'eventAction':'clique:link',
    'eventLabel': 'ver-mais'
  });
</script>

```

<br />




> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />


