

> Digital Analytics<br />
> Documento de Especificação Técnica - Quiosque Sex Shop
<br />

## Implementação da Camada de dados
Ultima atualização: 28/06/2022 <br />

<br />

## Objetivo
Este documento tem como objetivo instruir a implementação da camada de dados e de data attributes para utilização de recursos de monitoramento do Google Analytics referentes ao ambiente de [URL Produção: https://quiosquesexshop.com.br/](https://quiosquesexshop.com.br/).

<br />

### **Descrição Geral**

O `snippet` do Google Tag Manager é um pequeno trecho de código javascript ou non-javascript, através do uso de um iframe quando o javascript não está disponível, que é inserido nas páginas do site, tornando possível que a configuração das tags sejam realizadas via interface.


### **Posicionamento do Código - Google Tag Manager**

#### 1. Copie o seguinte JavaScript e cole-o o mais próximo da tag `<head>` de abertura possível em todas as páginas do seu site.

```html

<html>
  <head>
    <!-- Google Tag Manager -->
    <script>
        (function (w, d, s, l, i) {
            w[l] = w[l] || []; w[l].push({
                'gtm.start':
                    new Date().getTime(), event: 'gtm.js'
            }); var f = d.getElementsByTagName(s)[0],
                j = d.createElement(s), dl = l != 'dataLayer' ? '&l=' + l : ''; j.async = true; j.src =
                    'https://www.googletagmanager.com/gtm.js?id=' + i + dl; f.parentNode.insertBefore(j, f);
        })(window, document, 'script', 'dataLayer', 'GTM-KTG9WHQ');
    </script>
    <!-- End Google Tag Manager -->
    //...
  </head>
```

#### 2. Copie o seguinte trecho e cole-o imediatamente após a marcação `<body>` de abertura em cada página do seu site.

```html
<body>
  <!-- Google Tag Manager (noscript) -->
    <noscript>
        <iframe src="https://www.googletagmanager.com/ns.html?id=GTM-KTG9WHQ"
                height="0" width="0" style="display:none;visibility:hidden"></iframe>
    </noscript>
    <!-- End Google Tag Manager (noscript) -->
  //...
  </body>
</html>
```

Link de referência: [Documentação Oficial Google Tag Manager](https://developers.google.com/tag-manager/quickstart)


## Observações
> Os valores especificados entre colchetes `[[ ]]` são variáveis dinâmicas e devem ser substituídas por seus respectivos valores.<br />

> Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais. <br />


---

## Overview e Descrições Técnicas

### Camada de dados (DataLayer)

> É um array de objetos javascript utilizado pelo Google Tag Manager para receber em seus atributos, dados importantes do site.
Para implementar o dataLayer no site, o desenvolvedor pode utilizar formas diferentes para preencher os dados. Essas formas são dependentes da ação estabelecida na documentação e também do nível da interação.

**Instalação**<br />
Inserir a camada de dados antes do snippet de instalação do Google Tag Manager. Exemplo:

```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer = [{
    'atributo1': '[[valor1]]',
    'atributo2': '[[valor2]]'
  }];
</script>
```

OU

```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'atributo1': '[[valor1]]',
    'atributo2': '[[valor2]]'
  });
</script>
```

### Atributos HTML (Data Attributes)

> São atributos customizados inseridos nos elementos HTML da página, permitindo a inclusão de dados adicionais.

**Instalação**
1. Elementos: ```<div>Elemento</div>``` <br />
Todos os elementos do html que serão clicados, deverão ser mapeados recebendo os atributos com sua estrutura no item.

```html
<div
  data-gtm-event-category='[[exemplo:valor-categoria]]'
  data-gtm-event-action='[[exemplo:valor-acao]]'
  data-gtm-event-label='[[exemplo:valor-rotulo]]'
 >
  Texto do elemento
</div>
```

#### Importante:
> Também devem ter os data-attributes `data-gtm-event-category`, `data-gtm-event-action` e `data-gtm-event-label`. Preenchidos conforme instruções específicas.

<br />

## Implementação

A documentação foi descrita para algumas áreas especificas do ambiente do site ou aplicativo.


### Especificações Globais:

**Itens Gerais:**<br />
Todas as informações entre colchetes `[[  ]]` são variáveis dinâmicas que devem ser preenchidas com seus respectivos valores; <br />
Todos os valores enviados ao Google Analytics devem estar sanitizados, ou seja, sem espaços, acentuação ou caracteres especiais; <br />
Caso a informação solicitada não estiver disponivel retornar o valor com tipagem undefined.

---


### Geral


**No carregamento de todas as páginas e situações de history change.**<br />

- **Onde:** Em todas as páginas do site.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'page_view',
  
  });
</script>
```

<br />


**No clique dos elementos do header.**<br />

- **Onde:** Em todas as páginas em que estiverem disponíveis.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:geral',
    'eventAction': 'clique:link:header',
    'eventLabel': '[[nome-item]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-item]] |  'whatsapp' , 'instagram' , 'entrar' , 'criar-conta' e etc. | Deve retornar o nome do item clicado do header. |

<br />


**No clique dos elementos do menu e submenu.**<br />

- **Onde:** Em todas as páginas em que estiverem disponíveis.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:geral',
    'eventAction': 'clique:menu-superior',
    'eventLabel': '[[nome-item]]',
  });
</script>
```



| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-item]] |  'acessorios' , 'cosmeticos' , 'vibradores' , 'masturbadores' , 'meu-carrinho' e etc.  | Deve retornar o nome do item clicado do menu e submenu. |

<br />

**Ao preencher o campo de busca**
<br />

- **Onde:** Em todas as páginas em que estiverem disponíveis
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:geral',
    'eventAction': 'preencheu:campo',
    'eventLabel': '[[nome-preenchido]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-preenchido]] |  'vibrador-eletrico' , 'plug-anal' e etc.  | Deve retornar com o valor preenchido pelo usuario. |


<br />

**No clique em "Buscar".**<br />

- **Onde:** Em todas as páginas em que estiverem disponíveis.
    
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:geral',
    'eventAction': 'clique:busca',
    'eventLabel': 'buscar',
  });
</script>
```

<br />

**No clique dos elementos do footer da página.**
<br />

- **Onde:** Em todas as páginas em que estiverem disponíveis.
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:geral',
    'eventAction': 'clique:footer',
    'eventLabel': '[[nome-item]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-item]] |   'termos-de-pesquisa' , 'politica-de-privacidade-e-cookies' , 'pesquisa-avancada' , 'fale-conosco' , 'assinar' e etc.   | Deve retornar o nome do item clicado do footer.  |


<br />

**Ao preencher o campo de "Digite se e-mail' no footer.**
<br />

- **Onde:** Em todas as páginas em que estiverem disponíveis.
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:geral',
    'eventAction': 'preencheu:campo',
    'eventLabel': 'e-mail',
  });
</script>
```

<br />

**Ao clicar nos botoes de chatbox e whatsapp para contato.**
<br />

- **Onde:** Em todas as páginas em que estiverem disponíveis.
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:geral',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-botao]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]] |  'chatbox' ou 'whatsapp'   | Deve retornar o nome do botao clicado pelo usuario.  |


<br />


### Home

<br />

**No clique do banner disponiveis.**
<br />

- **Onde:** Na home
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:home',
    'eventAction': 'clique:banner',
    'eventLabel': '[[nome-banner]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-banner]] |  'sex-free-masturbador' , 'gel-comestivel' e etc.    | Deve retornar o nome do banner clicado pelo usuario.   |


<br />

**No clique do icone para mudar banner.**
<br />

- **Onde:** Na home
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:home',
    'eventAction': 'clique:icone',
    'eventLabel': 'banner:[[nome-icone]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-icone]] |  'seta-direita' ou 'seta-esquerda'   | Deve retornar se o nome do item clicado pelo usuario.   |


<br />

**No clique dos cards disponiveis.**
<br />

- **Onde:** Na home
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:home',
    'eventAction': 'clique:card',
    'eventLabel': '[[nome-card]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-card]] |  'meltesao-estimulante-sexual-unissex' , 'egg-masturbador-attractive' , 'vibrador-e-estimulador' e etc.    | Deve retornar o nome do card clicado pelo usuario.   |


<br />

**No clique dos botoes disponiveis dentro dos cards.**
<br />

- **Onde:** Na home
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:home',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-botao]]:[[nome-card]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]] |  'adicionarao-carrinho' , 'adicionar-para-comprar' e etc.  | Deve retornar o nome do botao clicado pelo usuario.   |
| [[nome-card]] |  'meltesao-estimulante-sexual-unissex' , 'egg-masturbador-attractive' , 'vibrador-e-estimulador' e etc. | Deve retornar o nome do card clicado pelo usuario. |


<br />

**No clique do icone para mudar os cards.**
<br />

- **Onde:** Na home
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:home',
    'eventAction': 'clique:icone',
    'eventLabel': 'card:[[nome-icone]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-icone]] |  'seta-direita' ou 'seta-esquerda'   | Deve retornar se o nome do item clicado pelo usuario.   |


<br />

**Na visualização do modal.**
<br />

- **Onde:** Na home
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:home',
    'eventAction': '[[abrir-fechar]]',
    'eventLabel': 'modal-carrinho',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[abrir-fechar]] |   'abriu' ou 'fechou'   | Deve retornar quando o usuario abrir ou fechar o modal.   |

<br />

**No clique do botes ou links disponiveis no modal de Meu carrinho.**
<br />

- **Onde:** Na home
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:home',
    'eventAction': 'clique:[[botao-link]]',
    'eventLabel': 'modal-carrinho:[[nome-item]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[botao-link]] |   'botao' ou 'link'  | Deve retornar se é um botao ou link.  |
| [[nome-item]] |   'avancar-para-o-checkout' , 'ver-e-editar-carrinho' , 'excluir' e etc.   | Deve retornar o nome do item clicado pelo usuario.  |

<br />

**No preenchimento do campo de quantidade do produto no modal de carrinho.**
<br />

- **Onde:** Na home
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:home',
    'eventAction': 'preencheu:[[nome-campo]]',
    'eventLabel': '[[valor-preenchido]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-campo]] |   'qtd' e etc   | Deve retornar o nome do campo que o usuario esta preenchendo.  |
| [[valor-preenchido]] |  '3' , '2' , '1' e etc.  | Deve retornar com o valor preenchido pelo usuario.  |


<br />

### Produto 
<br />

**No clique dos botoes ou links disponiveis**
<br />

- **Onde:** Nas páginas de produto
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:produto',
    'eventAction': 'clique:[[botao-link]]',
    'eventLabel': '[[nome-item]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[botao-link]]  |   'botao' ou 'link'   | Deve retornar se é um botao ou link.  |
| [[nome-item]] |  'adicionar-ao-carrinho' , 'obter-cotacao' , 'inicio' , 'selecionar-tudo' e etc.   | Deve retornar o nome do botao clicado pelo usuario.   |


<br />

**Ao preencher os campos disponiveis**
<br />

- **Onde:** Nas páginas de produto
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:produto',
    'eventAction': 'preencheu:campo',
    'eventLabel': '[[valor-preenchido]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[valor-preenchido]]  |    '1' , '2' , '5' , '10' e etc.    | Deve retornar o valor preenchido pelo usuario.   |


<br />

**Ao preencher os campos de CEP**
<br />

- **Onde:** Nas páginas de produto
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:produto',
    'eventAction': 'preencheu:campo',
    'eventLabel': 'cep',
  });
</script>
```

<br />

**No clique dos cards disponiveis**
<br />

- **Onde:** Nas páginas de produto
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:produto',
    'eventAction': 'clique:card',
    'eventLabel': '[[nome-card]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-card]]  |     'meltesao-estimulante-sexual-unissex' , 'egg-masturbador-attractive' , 'vibrador-e-estimulador' e etc.    | Deve retornar o nome do card clicado pelo usuario.   |


<br />

**No clique dos checkbot disponiveis dentro dos cards para selecionar o produto**
<br />

- **Onde:** Nas páginas de produto
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:produto',
    'eventAction': 'clique:checkbox',
    'eventLabel': '[[nome-card]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-card]]  |     'meltesao-estimulante-sexual-unissex' , 'egg-masturbador-attractive' , 'vibrador-e-estimulador' e etc.    | Deve retornar o nome do card clicado pelo usuario.   |


<br />

**No clique dos botoes disponiveis no modal apos adicionar produto ao carrinho**
<br />

- **Onde:** Nas páginas de produto
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:produto',
    'eventAction': 'clique:modal',
    'eventLabel': '[[nome-botao]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]]  |   'ver-carrinho' , 'continue-comprando' ,  'fechar' e etc.   | Deve retornar o nome do botao clicado pelo usuario.    |


<br />

### Produto 
<br />

**No clique para abrir ou fechar os acordions do filtro lateal**
<br />

- **Onde:** Sempre que estiver disponivel
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:submenu',
    'eventAction': 'clique:acordion',
    'eventLabel': '[[abrir-fechar]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[abrir-fechar]]  |   'abriu' ou 'fechou'  | Deve retornar se o acordion abriu ou fechou.  |


<br />

**No clique dos checkbox de pedidos feitos recentementes**
<br />

- **Onde:** Na area logada apos ja ter efetuado uma compra recentemente
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:submenu',
    'eventAction': 'clique:checkbox',
    'eventLabel': '[[secao]]:[[nome-checkbox]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|  [[secao]]:[[nome-checkbox]]  |   'pedidos-feitos-recentemente:egg-masturbador' e etc.   | Deve retornar a secao que o checkbox esta em seguida do nome selecionado.  |


<br />

**No clique dos botoes ou links apos selecionar o checkbox de pedidos feitos recentemente**
<br />

- **Onde:** Na area logada apos ja ter efetuado uma compra recentemente
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:submenu',
    'eventAction': 'clique:[[botao-link]]',
    'eventLabel': '[[secao]]:[[nome-item]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|  [[botao-link]]  |   'botao' ou 'link'  |  Deve retornar se é um botao ou link.   |
|  [[secao]]:[[nome-item]]  |    'pedidos-feitos-recentemente:comprar' , ''pedidos-feitos-recentemente:ver-tudo'   |  Deve retornar a secao que o checkbox esta em seguida do item clicado.    |

<br />

**No clique dos accordions do filtro lateal (Opções de Compra)**
<br />

- **Onde:** Sempre que estiver disponivel
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:submenu',
    'eventAction': 'clique:acordion',
    'eventLabel': '[[nome-secao]]:[[nome-accordion]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|  [[nome-secao]]:[[nome-accordion]] |  'cosmeticos:categoria' . 'vibradores:preco' , 'vibradores:cor' e etc.   |   Deve retornar a seçao na qual o suario esta em seguida do accordion clicado.    |

<br />

**No clique dos links dentro dos acordions do filtro lateral**
<br />

- **Onde:** Sempre que estiver disponivel
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:submenu',
    'eventAction': 'clique:acordion',
    'eventLabel': '[[nome-secao]]:[[nome-acordion]]:[[nome-link]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
|  [[nome-secao]]:[[nome-acordion]]:[[nome-link]] |  'cosmeticos:categoria' , 'vibradores:'cor:rosa , 'cosmeticos:categoria:comestiveis:' e etc.   |  Deve retornar a seçao na qual o suario esta em seguida do acordio e link clicados.   |

<br />

**No clique do icone para definir o modo de exibição**
<br />

- **Onde:** Sempre que estiver disponivel
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:submenu',
    'eventAction': 'clique:icone',
    'eventLabel': '[[nome-icone]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-icone]] | 'grade' , 'lista' , 'direcao-crescente' , direcao-decrescente' e etc.    |  Deve retornar o nome do icone clicado pelo usuario.  |

<br />

**No clique do acordion para ordenar a exibição**
<br />

- **Onde:** Sempre que estiver disponivel
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:submenu',
    'eventAction': 'clique:acordion',
    'eventLabel': '[[nome-item]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-item]] |  'position' , 'nome-do-produto' , 'preco' e etc.     |  Deve retornar o nome do item clicado pelo usuario.  |

<br />

**No clique dos cards disponiveis **
<br />

- **Onde:** Sempre que estiver disponivel
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:submenu',
    'eventAction': 'clique:card',
    'eventLabel': '[[nome-secao]]:[[nome-card]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-secao]]:[[nome-card]] |   'cosmeticos:gel-beijavel' . 'vibradores:capsula-vibratoria-rosa' e etc.      |  Deve retornar o nome da secao em que o usuario esta em seguida do nome do card.   |

<br />

**No clique dos botoes ou links disponiveis nos cards**
<br />

- **Onde:** Sempre que estiver disponivel
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:submenu',
    'eventAction': 'clique:[[botao-link]]',
    'eventLabel': '[[nome-secao]]:[[nome-card]]:[[nome-item]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[botao-link]] |   'botao' ou 'link'    |  Deve retornar se é um botao ou um link.   |
| [[nome-secao]]:[[nome-card]]:[[nome-item]] |   cosmeticos:gel-beijavel:adicionar-ao-carrinho' . 'vibradores:capsula-vibratoria-rosa:ir-para-o-produto' e etc.    |  Deve retornar conforme a interação do usuario.    |


<br />

**No clique do link ou icone para limpar o filtro**
<br />

- **Onde:** Sempre que estiver disponivel
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:submenu',
    'eventAction': 'clique:i[[link-icone]]',
    'eventLabel': '[[nome-item]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[link-icone]] |   'link' ou 'icone'   |  Deve retornar se é um link ou um icone.  |
| [[nome-item]] |    'limpar-tudo' , 'fechar' e etc.   |  Deve retornar o nome do item clicado pelo usuario.    |


<br />

**No clique do acordion para exibição de produto por pagina**
<br />

- **Onde:** Sempre que estiver disponivel
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:submenu',
    'eventAction': 'clique:acordion',
    'eventLabel': '[[nome-secao]]:[[valor-exibicao]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-secao]]:[[valor-exibicao]]  |  acessorios:40' , 'vibradores:60' e etc.   |  Deve retornar a secao em que o usuario esta em seguida do valor escolhido para a exibicao dos produtos por pagina.  |


<br />

### Produto 
<br />

**Na interação com os campos de "e-mail e senha"**
<br />

- **Onde:** Na página de Login
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:login',
    'eventAction': 'interacao:campo:[[nome-secao]]',
    'eventLabel': 'preencheu:[[nome-campo]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-secao]]  |  'cliente-registrado'   | Deve retornar o nome da seção que o usuário está interagindo.  |
| [[nome-campo]] |  'email', 'senha' e etc  | Deve retornar o nome do campo preenchido.   |


<br />

### Login e Cadastro

<br />

**Após clicar no botão "Entrar" para validar os campos preenchidos**
<br />

- **Onde:** Na página de Login
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:login',
    'eventAction': 'interacao:campo:[[nome-secao]]',
    'eventLabel': 'preencheu:[[nome-campo]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-secao]]  |  'cliente-registrado'   | Deve retornar o nome da seção que o usuário está interagindo.  |
| [[nome-campo]] |  'email', 'senha' e etc  | Deve retornar o nome do campo preenchido.   |


<br />

**Após clicar no botão "Entrar" para validar os campos preenchidos**
<br />

- **Onde:** Na página de Login
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:login',
    'eventAction': 'envio:callback',
    'eventLabel': '[[sucesso ou tipo-de-erro]]',
  });
</script>
```

<br />


**No clique dos links de "Esqueci minha senha"**
<br />

- **Onde:** Na página de Login
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:login',
    'eventAction': 'clique:link',
    'eventLabel': '[[nome-link]]',
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-link]]  | 'esqueceu-a-sua-senha'   | Deve retornar o nome do link clicado.  |

<br />

**No clique dos botoes disponiveis na pagina**
<br />

- **Onde:** Na página de Login
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:login',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-botao]]',
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]] |  'entrar' , 'criar-conta' e etc.  | Deve retornar o nome do botao que o usuario clicou.  |

<br />

**Na interação com os campos**
<br />

- **Onde:** Na página de cadastro
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:cadastro',
    'eventAction': 'preencheu:campo',
    'eventLabel': '[[nome-campo]]',
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-campo]] |   'nome' , 'sobrenome' , 'cpf' , 'email' e etc.    | Deve retornar o nome do campo preenchido pelo usuario.  |

<br />

**Na interação com o botao de calendario**
<br />

- **Onde:** Na página de cadastro
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:cadastro',
    'eventAction': 'clique:botao',
    'eventLabel': 'calendario',
  });
</script>
```

<br />


**Na interação com os itens no modal para definir a data de nascimento apos clicar no botao de calendario**
<br />

- **Onde:** Na página de cadastro
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:cadastro',
    'eventAction': 'clique:item',
    'eventLabel': '[[nome-item]]',
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-item]] |  'acordion:mes' , 'acordion:ano' , 'seta:direita' , 'seta:esquerda'    |  Deve retornar o nome do item clicado pelo usuario.  |

<br />

**No clique do checkbox disponiveis na pagina**
<br />

- **Onde:** Na página de cadastro
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:cadastro',
    'eventAction': 'clique:checkbox',
    'eventLabel': '[[nome-checkbox]]',
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-checkbox]] |   'assinar-newsletter' , 'nao-sou-robo' e etc.    | Deve retornar o nome do chackbox clicado pelo usuario.  |

<br />

**No clique do acordion para selecionar o genero**
<br />

- **Onde:** Na página de cadastro
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:cadastro',
    'eventAction': 'clique:acordion',
    'eventLabel': '[[nome-selecionado]]',
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-selecionado]] |  'masculino' , 'feminino' , 'nao-especificado' e etc.     |  Deve retornar o genero selecionado pelo usuario.  |

<br />

**Após clicar no botão "Criar Conta" para validar os campos preenchidos**
<br />

- **Onde:** Na página de cadastro
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:cadastro',
    'eventAction': 'envio:callback',
    'eventLabel': '[[sucesso ou tipo-de-erro]]',
  });
</script>
```

<br />


### Area Logada - Minha Conta

<br />

**No clique dos links disponiveis**
<br />

- **Onde:** Na pagina de minha conta
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:area-logada:minha-conta',
    'eventAction': 'clique:link',
    'eventLabel': '[[nome-link]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-link]] |  'editar' , 'alterar-senha' , 'editar-o-endereco' e etc.   | Deve retornar o nome do link clicado.   |


<br />

### Area Logada - Adicionar Novo Endereço 

<br />

**Na interação com os campos**
<br />

- **Onde:** Na página de Adicionar novo endereco
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:adicionar-novo-endereco',
    'eventAction': 'preencheu:campo',
    'eventLabel': '[[nome-campo]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-campo]] |  'nome' , 'sobrenome' , 'rua' , 'numero' , 'complemento' , 'bairro' e etc.    |  Deve retornar o nome do campo preenchido pelo usuario.   |


<br />

**No clique do acordion para selecionar o Estado e País**
<br />

- **Onde:** Na página de Adicionar novo endereco
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:adicionar-novo-endereco',
    'eventAction': 'clique:acordion',
    'eventLabel': '[[nome-campo]]:[[nome-selecionado]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-campo]]:[[nome-selecionado]] |  'estado:goias' , 'estado:sao-paulo' , 'pais:brasil' e etc    |  Deve retornar o nome do campo em seguida o nome selecionado pelo usuario.  |


<br />

**No clique do botao de "Salvar endereço"**
<br />

- **Onde:** Na página de Adicionar novo endereco
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:adicionar-novo-endereco',
    'eventAction': 'clique:botao',
    'eventLabel': 'salvar-endereco',
  });
</script>
```

<br />

**Após clicar no botão "Salvar endereço" para validar os campos preenchidos**
<br />

- **Onde:** Na página de Adicionar novo endereco
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:adicionar-novo-endereco',
    'eventAction': 'envio:callback',
    'eventLabel': '[[sucesso ou tipo-de-erro]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[sucesso ou tipo-de-erro]] |  'sucesso' , 'erro:campo-obrigatorio' e etc.     |  Deve retornar sucesso ou tipo de erro ocorrido.   |


<br />

### Area Logada - Informações de Conta

<br />

**Na interação com os campos**
<br />

- **Onde:** Na página de informacoes de conta
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:informacoes-de-conta',
    'eventAction': 'preencheu:campo',
    'eventLabel': '[[nome-campo]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-campo]] |  'nome' , 'sobrenome' , 'cpf' , 'email' e etc.    |  Deve retornar o nome do campo preenchido pelo usuario.   |


<br />


**No clique do checkbox disponiveis na pagina**
<br />

- **Onde:** Na página de informacoes de conta
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:informacoes-de-conta',
    'eventAction': 'clique:checkbox',
    'eventLabel': '[[nome-checkbox]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-checkbox]] |  'alterar-e-mail' , 'alterar-senha' , 'nao-sou-robo' e etc.    |  Deve retornar o nome do chackbox clicado pelo usuario.    |


<br />

**No clique do acordion para selecionar o genero**
<br />

- **Onde:** Na página de informacoes de conta
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:informacoes-de-conta',
    'eventAction': 'clique:acordion',
    'eventLabel': '[[nome-selecionado]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-selecionado]] |  'masculino' , 'feminino' , 'nao-especificado' e etc.   |  Deve retornar o genero selecionado pelo usuario.     |


<br />

**No clique dos botoes disponiveis**
<br />

- **Onde:** Na página de informacoes de conta
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:informacoes-de-conta',
    'eventAction': 'clique:botao',
    'eventLabel': '[[[nome-botao]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]] |   'salvar' , 'delete-your-acount' e etc.   |  Deve retornar o nome do botao clicado pelo usuario.     |


<br />

**Após clicar no botão "Salvar" para validar os campos preenchidos**
<br />

- **Onde:** Na página de informacoes de conta
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:informacoes-de-conta',
    'eventAction': 'envio:callback',
    'eventLabel': '[[sucesso ou tipo-de-erro]]',
  });
</script>
```

<br />

**Na visualização do modal para cancelar conta**
<br />

- **Onde:** Na página de informacoes de conta
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:informacoes-de-conta',
    'eventAction': '[[abriu-fechou]]',
    'eventLabel': '[[nome-modal]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[abriu-fechou]] |  abriu' ou 'fechou'   |  Deve retornar se o modal abriu ou fechou.    |
| [[nome-modal]] |   'are-you-sure-you-to-delete-your-acount' e etc.  |   Deve retornar o nome do modal em que o usuario esta.     |

<br />

**No clique dos botoes no modal de cancelar conta**
<br />

- **Onde:** Na página de informacoes de conta
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:informacoes-de-conta',
    'eventAction': 'clique:botao:modal',
    'eventLabel': '[[nome-botao]] ',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]]  | 'cancel' , 'ok' e etc.   |  Deve retorar o nome do botao clicado pelo usuario.    |

<br />

### Area Logada - Assinar Newsletter

<br />

**No clique do checkbox disponivel**
<br />

- **Onde:** Na página de assinar newsletter
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:assinar-newsletter',
    'eventAction': 'click:checkbox',
    'eventLabel': '[[nome-checkbox]]',
  });
</script>
```


| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-checkbox]] |  'subscricao-geral' etc.    |  Deve retornar o nome do campo preenchido.  |


<br />

**No clique do botao de Salvar**
<br />

- **Onde:** Na página de assinar newsletter
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:assinar-newsletter',
    'eventAction': 'clique:botao',
    'eventLabel': 'salvar',
  });
</script>
```

<br />

**Após clicar no botão "Salvar" para validar os campos preenchidos**
<br />

- **Onde:** Na página de assinar newsletter
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:assinar-newsletter',
    'eventAction': 'envio:callback',
    'eventLabel': '[[sucesso ou tipo-de-erro]]',
  });
</script>
```

<br />


### Carrinho 

<br />

**Na interação com os campos de quantidade e cupom de desconto**
<br />

- **Onde:** Na página de carrinho 
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:assinar-carrinho',
    'eventAction': 'interacao:campo:campo',
    'eventLabel': '[[secao]]:[[nome-campo]]',
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[secao]]:[[nome-campo]] |  'quantidade:1' , 'resumo:cep', 'cupom-de-desconto:inserir-cupom' e etc.    |  Deve retornar o nome da secao em seguida do campo preenchido.   |

<br />

**No clique dos acordions**
<br />

- **Onde:** Na página de carrinho 
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:assinar-carrinho',
    'eventAction': 'clique:[[nome-acordion]]',
    'eventLabel': '[[nome-campo]]:[[valor-selecionado]]',
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-acordion]]  |  'consultar-valor-do-frete' , 'inserir-cupom' e etc.   |  Deve retornar o nome do acordion que o usuario clicou.  |
| [[nome-campo]]:[[valor-selecionado]]  |   'pais:brasil' , 'estado:sao-paulo' e etc.   |  Deve retornar o nome do campo em seguida o valor selecionado.   |

<br />

**No click do checkbox para selecionar modo de envio**
<br />

- **Onde:** Na página de carrinho 
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:assinar-carrinho',
    'eventAction': 'clique:checkbox',
    'eventLabel': '[[nome-checkbox]]',
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-checkbox]]  |   'sedex' , 'pac' e etc.   |  Deve retornar o valor do checkbox clicado pelo usuario.  |

<br />

**No click dos botoes disponiveis na pagina**
<br />

- **Onde:** Na página de carrinho 
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:assinar-carrinho',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-botao]]',
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]]  |   'atualizar-carrinho-de-compras' , 'avancar-para-o-checkout' , 'editar' , 'excluir' e etc.    |  Deve retornar o nome do botao clicado pelo usuario.  |

<br />

### Checkout 

<br />

**No clique do acordions para visualizar os itens do carrinho**
<br />

- **Onde:** Na página de checkout - Frete
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:checkout',
    'eventAction': 'clique:acordion',
    'eventLabel': '[[nome-acordion]]',
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-acordion]]  |   'itens-no-carrinho' e etc.    |  Deve retornar o nome do acordion clicado pelo usuario.   |

<br />

**No click do checkbox para selecionar modo de envio**
<br />

- **Onde:** Na página de checkout - Frete
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:checkout',
    'eventAction': 'clique:checkbox',
    'eventLabel': '[[secao]]:[[nome-checkbox]]',
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[secao]]  |   'metodos-de-envio" e etc.     |  Deve retornar o nome da secao.   |
| [[nome-checkbox]] | 'sedex' , 'pac' e etc.   |  Deve retornar o valor do checkbox clicado pelo usuario.    |


<br />

**No click dos botoes disponiveis na pagina**
<br />

- **Onde:** Na página de checkout - Frete
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:checkout',
    'eventAction': 'clique:botao',
    'eventLabel': '[[nome-botao]]',
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]] |   'novo-endereco' , 'proximo' e etc.     |  Deve retornar o nome do botao clicado pelo usuario.    |

<br />

**Ao visualizar o modal de Endereço de Entrega**
<br />

- **Onde:** Na página de checkout - Frete
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:checkout',
    'eventAction': '[[abrir-fechar]]',
    'eventLabel': '[[nome-modal]]',
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[abrir-fechar]] |   'novo-endereco' , 'proximo' e etc.     |  Deve retornar se o usuario abriu ou fechou o modal.  |
| [[nome-modal]] |   'endereco-de-entrega' e etc.     |  Deve retornar o nome do modal.   |

<br />

**Na interacao com os campos do modal de Endereco de Entrega**
<br />

- **Onde:** Na página de checkout - Frete
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:checkout',
    'eventAction': 'preencheu-campo',
    'eventLabel': '[[nome-campo]]',
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-campo]] |  'endereco' , 'numero' , 'complemento' , 'bairro' e etc   |  Deve retornar o nome do campo interagido pelo usuario.  |

<br />

**No clique dos acordions para selecionar Estado e Pais**
<br />

- **Onde:** Na página de checkout - Frete
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:checkout',
    'eventAction': 'clique:accordion',
    'eventLabel': '[[nome-campo]]',
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-campo]] |  'estado' , 'pais' e etc.    |  Deve retornar o nome do campo interagido pelo usuario.  |

<br />

**No clique dos botoes disponiveis no modal de Endereco de Entrega**
<br />

- **Onde:** Na página de checkout - Frete
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:checkout',
    'eventAction': 'clique:modal:botao',
    'eventLabel': '[[nome-botao]]',
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]] |   'cancelar' , 'ship-here' e etc.   |  Deve retornar o nome do botao clicado pelo usuario.  |

<br />

**No clique de qualquer botao disponivel na pagina**
<br />

- **Onde:** Na página de checkout - revisao e pagamento
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:checkout',
    'eventAction': 'clique:botao',
    'eventLabel': '[[secao]]:[[nome-botao]]',
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-botao]] |   'cancelar' , 'ship-here' e etc.   |  Deve retornar o nome do botao clicado pelo usuario.  |

<br />

**No clique dos checkbox disponiveis na pagina**
<br />

- **Onde:** Na página de checkout - revisao e pagamento
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:checkout',
    'eventAction': 'clique:checkbox',
    'eventLabel': '[[secao]]:[[nome-checkbox]]',
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[secao]] |   'metodos-de-envio" e etc.    |  Deve retornar o nome da secao.   |
| [[nome-checkbox]] |  'pix' , 'cartao-de-credito' , 'picpay' , 'boleto-bancario' e etc.   |  Deve retornar o valor do checkbox clicado pelo usuario.  |

<br />

**Ao clicar nos acordions disponiveis na pagina**
<br />

- **Onde:** Na página de checkout - revisao e pagamento
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:checkout',
    'eventAction': 'clique:acordion:[[nome-acordion]]',
    'eventLabel': '[[secao]]:[[nome-item]]',
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[nome-acordion]] |   'meu-endereco-de-pagamento-e-entrega' , 'selecione-abaixo-pix-ou-carteira-digital' , 'itens-no-carrinho' e etc.  |  Deve retornar o nome do acordion clicado pelo usuario.    |
| [[secao]]   |   'pix' , 'cartao-de-credito' , 'picpay' , 'boleto-bancario'e etc.  |  Deve retornar o nome da secao que o usuario clicou no botao.  |
| [[nome-item]]   |   'pix' , 'mercado-pago' , 'picpay' , parcelas e etc.   |  Deve retornar o nome do iten selecionado do acordion.   |

<br />

**Na interacao com o campo de aplicar cupom**
<br />

- **Onde:** Na página de checkout - revisao e pagamento
  
```html
<script>
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    'event': 'event',
    'eventCategory': 'quiosquesexshop:checkout',
    'eventAction': 'preencheu:campo',
    'eventLabel': '[[valor-campo]]',
  });
</script>
```

| Variável        | Exemplo                               | Descrição                         |
| :-------------- | :------------------------------------ | :-------------------------------- |
| [[valor-campo]] |   '10desconto' e etc.   |  Deve retornar o cupom que o usuario inseriu. |

<br />





### Purchase


- **Quando:** No carregamento da página de confirmação de pedido - Purchase
- **Onde:** Na página de pedido

```html
<script>
dataLayer.push({
	'event': 'purchase',
	'eventCategory': 'quiosquesexshop:purchase',
	'eventAction': 'options-payment',
	'eventLabel': 'installments:[[num parcelas]]',
  'noInteraction':'1',
	'ecommerce': {
		'purchase': {
			'actionField': {
				'id': '[[id-transacao]]',				//ID da transação não obrigatorio
				'revenue': '[[valor-total-transacao]]'
			},
			'products': [{
				'name': '[[nome-produto]]',				//Nome ou ID do produto não obrigatorio
				'id': '[[id-produto]]',
				'price': '[[preco-produto]]',
				'category': '[[categoria-produto]]'
				'coupon': '[[cupom-produto]]'		//Em caso de cupom de desconto
			}]
		}
	}
});
</script>
```

*VariÃ¡vel "eventLabel"*

| Variavel 				| Exemplo 											| Descrição 														|
| :--------------------	| :------------------------------------------------ | :---------------------------------------------------------------	|
| [[num parcelas]]	| '1', '2', etc	| Deve retornar o numero de parcelas usadas no cartão.	|

*Descrição Purchase:*

| Nome 			| VariÃ¡vel 					| Exemplo 			| Descrição  				|
| :------------	| :------------------------	| :----------------	| :-----------------------	|
| id 			| [[id-transacao]] 			| 't-786545s'		| ID da TransaÃ§Ã£o			|
| revenue 		| [[valor-total-transacao]] | '256.80'	 		| Valor total da transaÃ§Ã£o	|

<br />

*Descrição Produtos:*

| Nome 			| VariÃ¡vel 					| Exemplo 				| Descrição  							|
| :------------	| :------------------------	| :-----------------	| :------------------------------------	|
| name 			| [[nome-produto]] 			| 'vibrador-personal-grande'		| Nome do produto 						|
| id			| [[id-produto]] 			| '12345645'		| ID do produto 						|
| price			| [[preco-produto]] 		| '30.00'				| Preco do produto						|
| category 		| [[categoria-produto]] 	| 'vibradores'				| Categoria do produto 					|
| coupon		| [[cupom-produto]]	 		| '10OFF'	| Cupom de desconto usado no produto	|

<br />

### Enhanced E-commerce

- **Quando:** No carregamento da página de confirmação de pedido - Purchase
- **Onde:** Na página de pedido

```html
<script>
dataLayer.push({
  'event': 'productImpression',
	'ecommerce': {
    'currencyCode': 'BR',                       
    'impressions': [
     {
       'name': 'vibrador-personal-grande',       
       'id': '12345645',
       'price': '15.25',
       'brand': 'Google',
       'category': 'vibradores',
       'variant': 'Gray',
       'list': 'Search Results',
       'position': 1
     },
     {
       'name': 'anel-peniano',
       'id': '67890',
       'price': '33.75',
       'brand': 'Google',
       'category': 'acessorios',
       'variant': 'Black',
       'list': 'Search Results',
       'position': 2
     }]
  }
});
</script>
```


- **Quando:** No clique em um produto da lista
- **Onde:** Em todas as páginas que exibirem uma lista de produto


```html
<script>
dataLayer.push({
 'event': 'productClick',
    'ecommerce': {
      'click': {
        'actionField': {'list': 'Search Results'},     
        'products': [{
           'name': 'vibrador-personal-grande',       
           'id': '12345645',
           'price': '15.25',
           'brand': 'Google',
           'category': 'vibradores',
           'variant': 'Gray',
           'list': 'Search Results',
           'position': 1n
         }]
       }
     },
     'eventCallback': function() {
       document.location = productObj.url
     }
  });
}
</script>
```


- **Quando:** No carregamento da página de detalhes de produto
- **Onde:** Na página de detalhes do produto


```html
<script>
dataLayer.push({
 'ecommerce': {
    'event': 'productDetail': {
      'actionField': {'list': 'Apparel Gallery'},    // 'detail' actions have an optional list property.
      'products': [{
           'name': 'vibrador-personal-grande',       
           'id': '12345645',
           'price': '15.25',
           'brand': 'Google',
           'category': 'vibradores',
           'variant': 'Gray',
       }]
     }
   }
});
</script>
```

- **Quando:** Ao adicionar um produto ao carrinho
- **Onde:** Na página de detalhes do produto e na página de carrinho


```html
<script>
dataLayer.push({
 'ecommerce': {
    'event': 'addToCart',
  'ecommerce': {
    'currencyCode': 'BR',
    'add': {                                // 'add' actionFieldObject measures.
      'products': [{                        //  adding a product to a shopping cart.
           'name': 'vibrador-personal-grande',       
           'id': '12345645',
           'price': '15.25',
           'brand': 'Google',
           'category': 'vibradores',
           'variant': 'Gray',
           'quantity': 1
       }]
    }
  }
});
</script>
```


- **Quando:** Ao remover um produto ao carrinho
- **Onde:** Na página de carrinho


```html
<script>
dataLayer.push({
 'ecommerce': {
    'event': 'removeFromCart',
  'ecommerce': {
    'remove': {                               // 'remove' actionFieldObject measures.
      'products': [{                          //  removing a product to a shopping cart.
           'name': 'vibrador-personal-grande',       
           'id': '12345645',
           'price': '15.25',
           'brand': 'Google',
           'category': 'vibradores',
           'variant': 'Gray',
           'quantity': 1
      }]
    }
  }
});
</script>
```

- **Quando:** Nas etapas de checkout
- **Onde:** Nas páginas de checkout


```html
<script>
dataLayer.push({
 'ecommerce': {
    'event': 'checkout',
    'ecommerce': {
      'checkout': {
        'actionField': {'step': 1, 'option': 'Visa'},
        'products': [{
          'name': 'vibrador-personal-grande',       
           'id': '12345645',
           'price': '15.25',
           'brand': 'Google',
           'category': 'vibradores',
           'variant': 'Gray',
           'quantity': 1
       }]
     }
   },
   'eventCallback': function() {
      document.location = 'checkout.html';
   }
  });
}
</script>
```

- **Quando:** Ao selecionar um tipo de entrega ou tipo de pagamento
- **Onde:** Na página de checkout, etapas de pagamento ou entrega


```html
<script>
dataLayer.push({
 'ecommerce': {
    'event': 'checkoutOption',
    'ecommerce': {
      'checkout_option': {
        'actionField': {'step': step, 'option': checkoutOption}
      }
    }
  });
}
</script>
```




---
 
 
## Considerações Finais
 
> Recomendações do Google:
> 1. [Enhanced Ecommerce - Product Impressions](https://developers.google.com/tag-manager/enhanced-ecommerce#product-impressions)
> 2. [Enhanced Ecommerce - Product Clicks](https://developers.google.com/tag-manager/enhanced-ecommerce#product-clicks)
> 3. [Enhanced Ecommerce - Product Detail](https://developers.google.com/tag-manager/enhanced-ecommerce#details)
> 4. [Enhanced Ecommerce - AddToCart / Remove From Cart](https://developers.google.com/tag-manager/enhanced-ecommerce#cart)
> 5. [Enhanced Ecommerce - Promotion Impression](https://developers.google.com/tag-manager/enhanced-ecommerce#promo-impressions)
> 6. [Enhanced Ecommerce - Promotion Click](https://developers.google.com/tag-manager/enhanced-ecommerce#promo-clicks)
> 7. [Enhanced Ecommerce - Checkout](https://developers.google.com/tag-manager/enhanced-ecommerce#checkout)
> 8. [Enhanced Ecommerce - Purchase](https://developers.google.com/tag-manager/enhanced-ecommerce#purchases)

 
<script>
  document.addEventListener("DOMContentLoaded", function(event) {
    document.querySelectorAll("h1 a")[0].style.display = 'none';
  });
</script>
