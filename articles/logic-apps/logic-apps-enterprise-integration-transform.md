---
title: "dados XML aaaConvert com transformações - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Criar transformações ou mapps dados XML tooconvert entre formatos de aplicativos lógicos usando Olá Enterprise integração SDK"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: add01429-21bc-4bab-8b23-bc76ba7d0bde
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: b56ec1072c5058d3aefc7f88ac9b2748ebe56456
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-integration-with-xml-transforms"></a>Integração corporativa com transformações XML
## <a name="overview"></a>Visão geral
conector de transformação de integração Olá corporativo converte dados de um formato de tooanother de formato. Por exemplo, você pode ter uma mensagem de entrada que contém Olá data atual no formato de YearMonthDay hello. Você pode usar um toobe do transformação tooreformat Olá data no formato de MonthDayYear Olá.

## <a name="what-does-a-transform-do"></a>O que uma transformação faz?
Uma transformação, que é também conhecido como um mapa, consiste em um esquema XML de origem (Olá de entrada) e um esquema XML de destino (saída Olá). Você pode usar funções internas diferentes toohelp manipular ou controlar dados Olá, incluindo manipulações de cadeia de caracteres, atribuições condicionais, expressões aritméticas, formatadores de tempo de data e até mesmo construções de loop.

## <a name="how-toocreate-a-transform"></a>Como toocreate uma transformação?
Você pode criar um mapa de transformação/usando o Visual Studio de saudação [Enterprise integração SDK](https://aka.ms/vsmapsandschemas). Quando tiver terminado de criar e testar transformação hello, carregar transformação Olá em sua conta de integração. 

## <a name="how-toouse-a-transform"></a>Como toouse uma transformação
Depois de carregar transformação/mapa Olá em sua conta de integração, você pode usar um aplicativo de lógica de toocreate. Olá lógica aplicativo executa transformações sempre que Olá lógica aplicativo é disparado (e não há conteúdo de entrada que precisa toobe transformado).

**Aqui está Olá etapas toouse uma transformação**:

### <a name="prerequisites"></a>Pré-requisitos

* Criar uma conta de integração e adicionar um mapa tooit  

Agora que atentar dos pré-requisitos Olá, é hora toocreate sua lógica de aplicativo:  

1. Criar um aplicativo de lógica e [vinculá-lo a conta de integração de tooyour](../logic-apps/logic-apps-enterprise-integration-accounts.md "Saiba toolink um aplicativo de conta tooa lógica da integração") que contém o mapa de saudação.
2. Adicionar um **solicitação** gatilho tooyour lógica aplicativo  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-1.png)    
3. Adicionar Olá **transformação XML** ação selecionando primeiro **adicionar uma ação**   
   ![](./media/logic-apps-enterprise-integration-transforms/transform-2.png)   
4. Inserir palavra hello *transformar* em toofilter de caixa de pesquisa Olá todos Olá toohello ações um que você deseja toouse  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-3.png)  
5. Selecione Olá **transformação XML** ação   
6. Adicionar Olá XML **conteúdo** que você transformar. Você pode usar qualquer dados XML recebidos na solicitação Olá HTTP como Olá **conteúdo**. Neste exemplo, selecione corpo Olá de solicitação HTTP Olá que disparou o aplicativo lógico de saudação.
7. Nome hello Select de saudação **mapa** que você queira a transformação de saudação do toouse tooperform. mapa de saudação já deve estar em sua conta de integração. Em uma etapa anterior, você já atribuiu sua lógica acesso tooyour integração conta do aplicativo que contém o mapa.      
   ![](./media/logic-apps-enterprise-integration-transforms/transform-4.png) 
8. Salve seu trabalho   
    ![](./media/logic-apps-enterprise-integration-transforms/transform-5.png) 

Neste ponto, você já configurou seu mapa. Em um aplicativo do mundo real, convém toostore dados de saudação transformado em um aplicativo de LOB, como a equipe de vendas. Você pode facilmente como uma saída de saudação do toosend de ação do hello transformar tooSalesforce. 

Agora você pode testar sua transformação fazendo um ponto de extremidade HTTP de toohello de solicitação.  

## <a name="features-and-use-cases"></a>Recursos e casos de uso
* transformação de saudação criada em um mapa pode ser simple, como copiar um nome e endereço de um tooanother de documento. Ou, você pode criar transformações mais complexas usando operações Olá fora da caixa.  
* Várias operações ou funções de mapeamento estão disponíveis, incluindo cadeias de caracteres, funções de data e hora, e assim por diante.  
* Você pode fazer uma cópia de dados direto entre esquemas de saudação. Olá que mapeador incluído no SDK do hello, isso é simple como desenhar uma linha que conecta os elementos Olá no esquema de origem de saudação com suas contrapartes no esquema de destino de saudação.  
* Ao criar um mapa, você pode exibir uma representação gráfica de mapa hello, que mostra todas as relações de saudação e links que você criar.
* Use Olá mapa de teste recurso tooadd uma mensagem XML de exemplo. Com um clique simple, você pode testar mapa Olá criado e consulte a saída de hello gerado.  
* Carregar mapas existentes  
* Inclui suporte para o formato do XML de saudação.

## <a name="learn-more"></a>Saiba mais
* [Saiba mais sobre Olá Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise")  
* [Saiba mais sobre mapas](../logic-apps/logic-apps-enterprise-integration-maps.md "Saiba mais sobre mapas da integração corporativa")  

