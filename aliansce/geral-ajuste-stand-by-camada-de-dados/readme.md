![Reamp](https://github.com/adtechReamp/client/blob/main/logo.png?raw=true)

> Adtech<br />
> Documento de Especificação Técnica

<br />

## Implementação da Camada de dados - Geral
Última atualização: 22/04/2021 <br />
Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

## Sumário

- [Objetivo](#objetivo)
- [Implementação](#implementa%c3%a7%c3%a3o)
- [Geral](#geral)

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

<H3 align="center"> STAND BY </h3>

### geral

**Quando: No clique dos botões**<br />

- **Onde:** Na página "Minhas Filas" na área logada do site.
    
```html
"<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'genericEvent',
    'eventCategory': '[[nome-ambiente]]:area-logada:minhas-filas,
    'eventAction': 'clique:botao,
    'eventLabel': '[[nome-botao]]'
  });
</script>"
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]] | 'entrar-em-uma-fila' e etc | Deve retornar o nome do botão clicado |


<br />

> Em caso de dúvidas, entrar em contato com: [tag@reamp.com.br](tag@reamp.com.br)

<br />

<script> document.querySelector('h1').style.display = 'none' </script>
