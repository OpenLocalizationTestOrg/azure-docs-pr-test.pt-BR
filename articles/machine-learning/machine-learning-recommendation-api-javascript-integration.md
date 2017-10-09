---
title: "Recomendações de Machine Learning: integração do JavaScript | Microsoft Docs"
description: "Recomendações do Azure Machine Learning - Integração do JavaScript - documentação"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: bbbb5bb6-489d-4a62-a2ae-f36237e9e2e1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: 4c5f0eee4aa04ce823321d52985374c52850f0d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a>Recomendações do Azure Machine Learning - Integração do JavaScript
> [!NOTE]
> Deve começar a usar o hello recomendações API cognitivas serviço em vez de nesta versão. Olá serviço cognitivas recomendações será substituído por esse serviço e todos os novos recursos de saudação serão desenvolvidos existe. Ele possui novos recursos como suporte ao processamento em lotes, um Gerenciador de API aprimorado, uma superfície de API mais limpa, uma experiência de inscrição/cobrança mais consistente etc.
> Saiba mais sobre [toohello migrando novo serviço cognitivas](http://aka.ms/recomigrate)
> 
> 

Este documento descrevem como toointegrate seu site usando JavaScript. Olá JavaScript permite que você toosend eventos de aquisição de dados e as recomendações de tooconsume depois de criar um modelo de recomendação. Todas as operações realizadas via JS também podem ser feitas do lado do servidor.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a>1. Visão geral
Integrando seu site com o AM do Azure As recomendações consistem em duas fases:

1. Enviar Eventos para as Recomendações do AM do Azure. Isso permitirá toobuild um modelo de recomendação.
2. Consuma recomendações hello. Depois Olá modelo é criado, você pode consumir recomendações hello. (Este documento não explica como toobuild um modelo, ler Olá tooget do guia de início rápido para obter mais informações sobre como).

<ins>Fase I</ins>

Em Olá primeira fase, que você inserir em suas páginas html uma pequena biblioteca JavaScript que permite Olá eventos da página toosend conforme elas ocorrem na página html de saudação em servidores de recomendações de ML do Azure (por meio do mercado de dados):

![Desenho1][1]

<ins>Fase II</ins>

Em Olá segunda fase, quando você quiser tooshow recomendações de saudação na página Olá você selecionar uma das Olá as opções a seguir:

1. o servidor (na fase de saudação de renderização da página) chama recomendações de tooget do servidor do Azure ML recomendações (por meio do mercado de dados). resultados da saudação incluem uma lista de IDs de itens. O servidor precisa tooenrich Olá resultados com itens de saudação dados de metadados (por exemplo, imagens, descrição) e enviar Olá criado página toohello navegador.

![Desenho2][2]

2. hello, outra opção é toouse Olá pequeno arquivo JavaScript de fase um tooget uma lista simples de itens recomendados. dados de saudação recebidos aqui são mais enxutos que Olá na opção de saudação primeiro.

![Desenho3][3]

## <a name="2-prerequisites"></a>2. Pré-requisitos
1. Crie um novo modelo usando APIs de saudação. Consulte o guia de início rápido de saudação sobre como toodo-lo.
2. Codifique seu &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; com base64. (Isso será usado para Olá autenticação básica tooenable Olá JS código toocall Olá APIs).

## <a name="3-send-data-acquisition-events-using-javascript"></a>3. Enviar eventos de Aquisição de Dados usando o JavaScript
Olá, as etapas a seguir facilitam a enviar eventos:

1. Inclua a biblioteca JQuery em seu código. Você pode baixá-lo do nuget em Olá URL a seguir.
   
     http://www.nuget.org/packages/jQuery/1.8.2
2. Incluir a biblioteca de Script de Java recomendações Olá da saudação URL a seguir: http://aka.ms/RecoJSLib1
3. Inicialize a biblioteca do Azure ML recomendações com parâmetros adequados Olá.
   
     <script>AzureMLRecommendationsStart ("<base64encoding of username:key>", "< model_id >"); </script> 
4. Evento apropriado de saudação de envio. Confira a seção detalhada abaixo em todos os tipos de eventos (exemplo de evento de clique) <script> se (typeof AzureMLRecommendationsEvent=="undefined") {         
                     AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ evento: "clique", item: "18321116" }); </script>

### <a name="31----limitations-and-browser-support"></a>3.1.    Limitações e Suporte ao Navegador
Isso é uma implementação de referência e é fornecida como está. Deve oferecer suporte a todos os principais navegadores.

### <a name="32----type-of-events"></a>3.2.    Tipo de Eventos
Há 5 tipos de evento que Olá biblioteca oferece suporte a: clique em, clique em recomendação, adicionar tooShop carrinho, remover do carrinho de compras e compra. Há um evento adicional que é o contexto de usuário Olá tooset usado chamado logon.

#### <a name="321-click-event"></a>3.2.1. Evento Clicar
Esse evento deve ser usado sempre que um usuário clicou em um item. Normalmente quando o usuário clica em um item uma nova página é aberta com detalhes do item Olá; Esse evento deve ser disparado nesta página.

Parâmetros:

* evento (cadeia de caracteres, obrigatória) - “clique”
* item (cadeia de caracteres, obrigatória) - o identificador exclusivo do item de saudação
* nome do item (cadeia de caracteres, opcional) - nome de saudação do item de saudação
* itemDescription (cadeia de caracteres, opcional) - descrição de saudação do item de saudação
* itemCategory (cadeia de caracteres, opcional) - categoria de saudação do item de saudação
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "click", item: "3111718" });
        </script>

Ou com dados opcionais:

        <script>
            if (typeof AzureMLRecommendationsEvent === "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "click", item: "3111718", itemName: "Plane", itemDescription: "It is a big plane", itemCategory: "Aviation"});
        </script>


#### <a name="322-recommendation-click-event"></a>3.2.2. Evento do Clique de Recomendação
Esse evento deve ser usado sempre que um usuário clicou em um item que foi recebido das Recomendações do AM do Azure como um item recomendado. Normalmente quando o usuário clica em um item uma nova página é aberta com detalhes do item Olá; Esse evento deve ser disparado nesta página.

Parâmetros:

* evento (cadeia de caracteres, obrigatória) - “recommendationclick”
* item (cadeia de caracteres, obrigatória) - o identificador exclusivo do item de saudação
* nome do item (cadeia de caracteres, opcional) - nome de saudação do item de saudação
* itemDescription (cadeia de caracteres, opcional) - descrição de saudação do item de saudação
* itemCategory (cadeia de caracteres, opcional) - categoria de saudação do item de saudação
* sementes (cadeia de caracteres array, opcional) - Olá propagações que gerou a consulta de recomendação de saudação.
* recoList (cadeia de caracteres array, opcional) - Olá resultado da solicitação de recomendação de saudação que gerou o item de saudação que foi clicado.
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "recommendationclick", item: "18899918" });
        </script>

Ou com dados opcionais:

        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: eventName, item: "198", itemName: "Plane2", itemDescription: "It is a big plane2", itemCategory: "Default2", seeds: ["Seed1", "Seed2"], recoList: ["199", "198", "197"]                 });
        </script>


#### <a name="323-add-shopping-cart-event"></a>3.2.3. Evento Adicionar ao Carrinho de Compras
Esse evento deve ser usado quando o usuário Olá adiciona um toohello item carrinho de compras.
Parâmetros:

* evento (cadeia de caracteres, obrigatória) - “addshopcart”
* item (cadeia de caracteres, obrigatória) - o identificador exclusivo do item de saudação
* nome do item (cadeia de caracteres, opcional) - nome de saudação do item de saudação
* itemDescription (cadeia de caracteres, opcional) - descrição de saudação do item de saudação
* itemCategory (cadeia de caracteres, opcional) - categoria de saudação do item de saudação
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a>3.2.4. Evento Remover do Carrinho de Compras
Esse evento deve ser usado quando o usuário Olá remove um carrinho de compras de toohello do item.

Parâmetros:

* evento (cadeia de caracteres, obrigatória) - “removeshopcart”
* item (cadeia de caracteres, obrigatória) - o identificador exclusivo do item de saudação
* nome do item (cadeia de caracteres, opcional) - nome de saudação do item de saudação
* itemDescription (cadeia de caracteres, opcional) - descrição de saudação do item de saudação
* itemCategory (cadeia de caracteres, opcional) - categoria de saudação do item de saudação
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a>3.2.5. Evento Comprar
Esse evento deve ser usado quando o usuário Olá adquirido seu carrinho de compras.

Parâmetros:

* evento (cadeia de caracteres) – “adquirir”
* itens ( Adquiridos[] ) - A matriz que contém uma entrada para cada item adquirido.<br><br>
  Formato adquirido:
  * item (string) - o identificador exclusivo do item de saudação.
  * contagem (int ou cadeia de caracteres) - número de itens que foram adquiridos.
  * preço (float ou cadeia de caracteres) - campo opcional - Olá preço de item de saudação.

exemplo Hello abaixo mostra a compra de 3 itens (33, 34, 35), dois com todos os campos preenchidos (item, contagem, preço) e outro (item 34) sem um preço.

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a>3.2.6. Evento Logon do Usuário
Azure ML recomendações evento biblioteca cria e usar um cookie em eventos de tooidentify ordem que veio Olá mesmo navegador. No modelo de saudação do pedido tooimprove resultados do Azure ML recomendações permite tooset um identificador exclusivo do usuário que substituirá o uso de cookie hello.

Esse evento deve ser usado após o site de tooyour de logon de usuário hello.

Parâmetros:

* evento (cadeia de caracteres) - “userlogin”
* usuário (string) - identificação exclusiva do usuário hello.
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a>4. Usar Recomendações via JavaScript
código de saudação que consome a recomendação de saudação é disparado por algum evento JavaScript por página de Web do cliente hello. resposta de recomendação de saudação inclui Olá recomendado Ids de itens, seus nomes e suas classificações. É melhor toouse esta opção apenas para uma exibição de lista de saudação recomendada itens - mais complexos tratamento (como adicionar metadados do item Olá) deve ser feita na integração do lado do servidor de saudação.

### <a name="41-consume-recommendations"></a>4.1 Usar as Recomendações
recomendações de tooconsume que necessário tooinclude Olá necessário bibliotecas JavaScript em sua página e toocall AzureMLRecommendationsStart. Consulte a seção 2.

recomendações de tooconsume para um ou mais itens que você precisa toocall um método chamado: AzureMLRecommendationsGetI2IRecommendation.

Parâmetros:

* itens (matriz de cadeias de caracteres) - um ou mais itens tooget as recomendações para. Se você consumir um build Fbt, você poderá, então, definir somente um item aqui.
* numberOfResults (int) - número de resultados necessários.
* includeMetadata (booliano, opcional) - se definir too'true' indica o campo Olá metadados deve ser preenchido em resultados de saudação.
* Função de processamento - uma função que tratará recomendações Olá retornadas. Olá dados são retornados como uma matriz de:
  * Item - ID exclusiva do item
  * nome - nome do item (se existir no catálogo)
  * classificação - classificação da recomendação
  * metadados - uma cadeia de caracteres que representa os metadados de saudação do item de saudação

Exemplo: Olá código a seguir solicita 8 recomendações para o item "64f6eb0d-947a-4c18-a16c-888da9e228ba" (e não especificando includeMetadata - implicitamente diz que não há metadados são necessário), ele, em seguida, concatenar resultados Olá em um buffer.

        <script>
             var reco = AzureMLRecommendationsGetI2IRecommendation(["64f6eb0d-947a-4c18-a16c-888da9e228ba"], 8, false, function (reco) {
                 var buff = "";
                 for (var ii = 0; ii < reco.length; ii++) {
                       buff += reco[ii].item + "," + reco[ii].name + "," + reco[ii].rating + "\n";
                 }
                 alert(buff);
            });
        </script>


[1]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing1.png
[2]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing2.png
[3]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing3.png
