---
title: "aaaInteract com relatórios usando Olá API JavaScript | Microsoft Docs"
description: "Power BI inserido, interagir com relatórios usando Olá API JavaScript"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: bdd885d3-1b00-4dcf-bdff-531eb1f97bfb
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: 657e4d5cee031bdda173ab3f451cc19b93ddb17b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="interact-with-power-bi-reports-using-hello-javascript-api"></a>Interagir com relatórios do Power BI usando Olá API JavaScript
Olá API JavaScript do Power BI permite que você tooeasily inserir relatórios do Power BI em seus aplicativos. Com a API do hello, seus aplicativos podem interagir programaticamente com elementos de relatório diferente como páginas e filtros. Essa interatividade faz com que os relatórios do Power BI sejam uma parte mais integrada do seu aplicativo.

Você pode inserir um relatório do Power BI em seu aplicativo usando um iframe hospedado como parte do aplicativo hello. Olá iframe funciona como um limite entre seu aplicativo e o relatório de saudação, como você pode ver no Olá a imagem a seguir. 

![Power BI embedded iframe sem API do Javascript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-1.png)

Olá iframe torna Olá inserindo um processo muito mais fácil, mas sem Olá Olá de API JavaScript relatório e seu aplicativo não podem interagir entre si. Esta falta de interação pode facilitar a sensação relatório Olá realmente não é parte de um aplicativo hello. aplicativo e relatório Olá precisam realmente toocommunicate e para trás, como Olá a imagem a seguir.

![Power BI embedded iframe com API do Javascript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-2.png)

Olá API JavaScript do Power BI permite que você o código de toowrite que pode passar com segurança por limite de iframe hello. Isso permite que seu aplicativo tooprogrammatically executar uma ação em um relatório e toolisten para eventos de ações que os usuários fazem no relatório de saudação.

## <a name="what-can-you-do-with-hello-power-bi-javascript-api"></a>O que você pode fazer com hello API JavaScript do Power BI?
Com hello API JavaScript, você pode gerenciar relatórios, navegue toopages em um relatório, filtrar um relatório e tratar eventos de inserção. Olá diagrama a seguir mostra estrutura Olá Olá API.

![Diagrama da API JavaScript do Power BI](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-3.png)

### <a name="manage-reports"></a>Gerenciar relatórios
Olá API Javascript permite que você toomanage comportamento no nível de página e relatório hello:

* Inserir um relatório específico do Power BI com segurança em seu aplicativo - tente Olá [incorporar o aplicativo de demonstração](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)
  * Definir token de acesso
* Configurar o relatório de saudação
  * Habilitar e desabilitar o painel de filtro hello e painel de navegação de página - tente Olá [atualizar o aplicativo de demonstração de configurações](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)
  * Definir padrões para páginas e filtros - tente Olá [demonstração do conjunto de padrões](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)
* Entrar e sair do modo de tela inteira

[Saiba mais sobre como inserir um relatório](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embedding-Basics)

### <a name="navigate-toopages-in-a-report"></a>Navegue toopages em um relatório
Olá API JavaScript enbales você toodiscover todas as páginas em uma página atual de Olá do relatório e tooset. Tente Olá [aplicativo de demonstração de navegação](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).

[Saiba mais sobre a navegação de página](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Page-Navigation)

### <a name="filter-a-report"></a>Filtrar um relatório
Olá API JavaScript fornece básicos e avançados recursos de relatórios inseridos e páginas de relatório de filtragem. Tente Olá [filtragem de aplicativo de demonstração](http://azure-samples.github.io/powerbi-angular-client/#/scenario4)e examinar alguns códigos introdução aqui.  

#### <a name="basic-filters"></a>Filtros básicos
Um filtro básico é colocado em um coluna ou nível hierárquico e contém uma lista de valores tooinclude ou excluir.

```
const basicFilter: pbi.models.IBasicFilter = {
  $schema: "http://powerbi.com/product/schema#basic",
  target: {
    table: "Store",
    column: "Count"
  },
  operator: "In",
  values: [1,2,3,4]
}
```


#### <a name="advanced-filters"></a>Filtros avançados
Filtros avançados usam o operador lógico hello e ou ou e aceitar uma ou duas condições, cada um com suas próprias operador e um valor. As condições com suporte são:

* Nenhum
* LessThan
* LessThanOrEqual
* GreaterThan
* GreaterThanOrEqual
* Contém:
* DoesNotContain
* StartsWith
* DoesNotStartWith
* Is
* IsNot
* IsBlank
* IsNotBlank

```
const advancedFilter: pbi.models.IAdvancedFilter = {
  $schema: "http://powerbi.com/product/schema#advanced",
  target: {
    table: "Store",
    column: "Name"
  },
  logicalOperator: "Or",
  conditions: [
    {
      operator: "Contains",
      value: "Wash"
    },
    {
      operator: "Contains",
      value: "Park"
    }
  ]
}
```
[Saiba mais sobre filtragem](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Filters)

### <a name="handling-events"></a>Manipulação de eventos
Além disso toosending informações em iframe hello, seu aplicativo pode também receber informações sobre Olá eventos provenientes iframe Olá a seguir:

* Inserir
  * carregado
  * error
* Relatórios
  * pageChanged
  * dataSelected (em breve)

[Saiba mais sobre a manipulação de eventos](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Handling-Events)

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre Olá API JavaScript do Power BI, confira Olá links a seguir:

* [Wiki da API JavaScript](https://github.com/Microsoft/PowerBI-JavaScript/wiki)
* [Referência de modelo de objeto](https://microsoft.github.io/powerbi-models/modules/_models_.html)
* Exemplos
  * [Angular](http://azure-samples.github.io/powerbi-angular-client)
  * [Ember](https://github.com/Microsoft/powerbi-ember)
* [Demonstração ao vivo](https://microsoft.github.io/PowerBI-JavaScript/demo/)

