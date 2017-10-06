---
title: "aaaLearn como toouse Olá conector Twitter em aplicativos lógicos | Microsoft Docs"
description: "Visão geral do conector do Twitter com os parâmetros da API REST"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8bce2183-544d-4668-a2dc-9a62c152d9fa
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: ead4e4dc95bf894fd72b908c5375b407ba27642d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twitter-connector"></a>Introdução ao conector do Twitter Olá
Com o conector do Twitter hello, você pode:

* Postar tweets e obter tweets
* Acessar linhas do tempo, amigos e seguidores
* Executar qualquer Olá outras ações e gatilhos descritos abaixo  

toouse [qualquer conector](apis-list.md), primeiro é necessário toocreate um aplicativo lógico. Você pode começar [criando um aplicativo lógico agora mesmo](../logic-apps/logic-apps-create-a-logic-app.md).  

## <a name="connect-tootwitter"></a>Conecte-se tooTwitter
Antes de sua lógica de aplicativo pode acessar qualquer serviço, primeiro é necessário toocreate um *conexão* toohello service. Uma [conexão](connectors-overview.md) fornece uma conectividade entre um aplicativo lógico e outro serviço.  

### <a name="create-a-connection-tootwitter"></a>Criar uma conexão tooTwitter
> [!INCLUDE [Steps toocreate a connection tooTwitter](../../includes/connectors-create-api-twitter.md)]
> 
> 

## <a name="use-a-twitter-trigger"></a>Usar um gatilho do Twitter
Um gatilho é um evento que pode ser o fluxo de trabalho do hello toostart usado definido em um aplicativo lógico. [Saiba mais sobre gatilhos](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

Neste exemplo, mostrarei como Olá toouse **quando um novo tweet for lançado** disparar toosearch para #Seattle e, se #Seattle for encontrado, atualizar um arquivo em Dropbox com o texto de saudação do tweet hello. Um exemplo de empresa, você pode pesquisar por nome de saudação da sua empresa e atualizar um banco de dados do SQL com o texto de saudação do tweet hello.

1. Digite *twitter* na caixa de pesquisa Olá no designer de aplicativos de lógica de saudação selecione Olá **Twitter - quando um novo tweet é postado** gatilho   
   ![Imagem 1 do gatilho do Twitter](./media/connectors-create-api-twitter/trigger-1.png)  
2. Digite *#Seattle* em Olá **texto de pesquisa** controle  
   ![Imagem 2 do gatilho do Twitter](./media/connectors-create-api-twitter/trigger-2.png) 

Neste ponto, seu aplicativo lógica foi configurado com um gatilho que iniciará uma execução de saudação outros gatilhos e ações no fluxo de trabalho de saudação. 

> [!NOTE]
> Para uma lógica aplicativo toobe funcional, ele deve conter pelo menos um gatilho e uma ação. Siga as etapas de Olá Olá tooadd próximo da seção uma ação.  
> 
> 

## <a name="add-a-condition"></a>Adicionar uma condição
Como estamos interessados apenas em tweets de usuários com mais de 50 usuários, uma condição que confirma o número de saudação do seguidores deve primeiro ser adicionada toohello lógica aplicativo.  

1. Selecione **+ nova etapa** ação de saudação tooadd você gostaria que tootake quando #Seattle é encontrado em um tweet novo  
   ![Imagem 1 da ação do Twitter](../../includes/media/connectors-create-api-twitter/action-1.png)  
2. Selecione Olá **adicionar uma condição** link.  
   ![Imagem 1 da condição do Twitter](../../includes/media/connectors-create-api-twitter/condition-1.png)   
   Isso abre o hello **condição** controle onde você pode verificar condições como *é igual a*, *é menor que*, *é maior do que*, *contém*, etc.  
   ![Imagem 2 da condição do Twitter](../../includes/media/connectors-create-api-twitter/condition-2.png)   
3. Selecione Olá **escolha um valor** controle.  
   Nesse controle, você pode selecionar uma ou mais das propriedades de saudação de todas as ações anteriores ou disparadores como valor Olá cuja condição será avaliado tootrue ou false.
   ![Imagem 3 da condição do Twitter](../../includes/media/connectors-create-api-twitter/condition-3.png)   
4. Selecione Olá **...**  tooexpand lista de saudação de propriedades para ver todas as propriedades de saudação que estão disponíveis.        
   ![Imagem 4 da condição do Twitter](../../includes/media/connectors-create-api-twitter/condition-4.png)   
5. Selecione Olá **contagem seguidores** propriedade.    
   ![Imagem 5 da condição do Twitter](../../includes/media/connectors-create-api-twitter/condition-5.png)   
6. Observe seguidores Olá propriedade count agora está no controle de valor de saudação.    
   ![Imagem 6 da condição do Twitter](../../includes/media/connectors-create-api-twitter/condition-6.png)   
7. Selecione **é maior do que** na lista de operadores de saudação.    
   ![Imagem 7 da condição do Twitter](../../includes/media/connectors-create-api-twitter/condition-7.png)   
8. Digite 50 como Olá operando para Olá *é maior do que* operador.  
   condição de saudação agora é adicionada. Salve seu trabalho usando Olá **salvar** link no menu de saudação acima.    
   ![Imagem 8 da condição do Twitter](../../includes/media/connectors-create-api-twitter/condition-8.png)   

## <a name="use-a-twitter-action"></a>Usar uma ação do Twitter
Uma ação é uma operação executada pelo fluxo de trabalho Olá definido em um aplicativo lógico. [Saiba mais sobre ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

Agora que você adicionou um gatilho, siga essas etapas tooadd uma ação que publicará um tweet novo com conteúdo Olá Olá tweets encontrados pelo gatilho hello. Para fins de saudação deste passo a passo somente tweets de usuários com mais de 50 seguidores serão lançadas.  

Na próxima etapa de saudação, você irá adicionar uma ação do Twitter que publicará um tweet usando algumas das propriedades de saudação de cada tweet que foi lançado por um usuário que tem mais de 50 seguidores.  

1. Escolha **Adicionar uma ação**. Isso abre o controle de pesquisa Olá onde você pode procurar outras ações e gatilhos.  
   ![Imagem 9 da condição do Twitter](../../includes/media/connectors-create-api-twitter/condition-9.png)   
2. Digite *twitter* na caixa de pesquisa Olá selecione Olá **Twitter - lançar um tweet** ação. Isso abre o hello **lançar um tweet** controlar onde você irá inserir todos os detalhes para tweet hello está sendo lançada.      
   ![Imagem de 1 a 5 da ação do Twitter](../../includes/media/connectors-create-api-twitter/action-1-5.png)   
3. Selecione Olá **Tweet texto** controle. Todas as saídas de ações anteriores e gatilhos no aplicativo de lógica de saudação agora estão visíveis. Você pode selecionar qualquer uma dessas e usá-los como parte do texto de tweet Olá de tweet novo hello.     
   ![Imagem 2 da ação do Twitter](../../includes/media/connectors-create-api-twitter/action-2.png)   
4. Escolha **Nome de usuário**   
5. Digite *diz:* no controle de texto tweet hello. Faça isso logo após o Nome de usuário.  
6. Escolha *Texto do tweet*.       
   ![Imagem 3 da ação do Twitter](../../includes/media/connectors-create-api-twitter/action-3.png)   
7. Salve seu trabalho e enviar um tweet com hello #Seattle hashtag tooactivate seu fluxo de trabalho.  


## <a name="connector-specific-details"></a>Detalhes específicos do conector

Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/twitterconnector/). 

## <a name="next-steps"></a>Próximas etapas
[Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md)

