---
title: "Converter dados XML com transformações – Aplicativo Lógico do Azure | Microsoft Docs"
description: "Criar transformações ou mapas para converter dados XML entre formatos em aplicativos lógicos usando o SDK do Enterprise Integration"
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
ms.openlocfilehash: fb6027769377b3527b11f7831dab3bb8d7061c84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="enterprise-integration-with-xml-transforms"></a><span data-ttu-id="d7bb0-103">Integração corporativa com transformações XML</span><span class="sxs-lookup"><span data-stu-id="d7bb0-103">Enterprise integration with XML transforms</span></span>
## <a name="overview"></a><span data-ttu-id="d7bb0-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d7bb0-104">Overview</span></span>
<span data-ttu-id="d7bb0-105">O conector de Transformação da integração corporativa converte dados de um formato para outro formato.</span><span class="sxs-lookup"><span data-stu-id="d7bb0-105">The Enterprise integration Transform connector converts data from one format to another format.</span></span> <span data-ttu-id="d7bb0-106">Por exemplo, talvez você tenha uma mensagem de entrada contendo a data atual no formato AnoMêsDia.</span><span class="sxs-lookup"><span data-stu-id="d7bb0-106">For example, you may have an incoming message that contains the current date in the YearMonthDay format.</span></span> <span data-ttu-id="d7bb0-107">Você pode usar uma transformação para reformatar a data para o formato MêsDiaAno.</span><span class="sxs-lookup"><span data-stu-id="d7bb0-107">You can use a transform to reformat the date to be in the MonthDayYear format.</span></span>

## <a name="what-does-a-transform-do"></a><span data-ttu-id="d7bb0-108">O que uma transformação faz?</span><span class="sxs-lookup"><span data-stu-id="d7bb0-108">What does a transform do?</span></span>
<span data-ttu-id="d7bb0-109">Uma Transformação, que também é conhecida como um mapa, é formada por um esquema XML de origem (entrada) e um esquema XML de destino (saída).</span><span class="sxs-lookup"><span data-stu-id="d7bb0-109">A Transform, which is also known as a map, consists of a Source XML schema (the input) and a Target XML schema (the output).</span></span> <span data-ttu-id="d7bb0-110">Você pode usar funções internas diferentes para ajudar a manipular e controlar os dados, incluindo manipulações de cadeia de caracteres, atribuições condicionais, expressões aritméticas, formatadores do tempo de data e até mesmo construções em loop.</span><span class="sxs-lookup"><span data-stu-id="d7bb0-110">You can use different built-in functions to help manipulate or control the data, including string manipulations, conditional assignments, arithmetic expressions, date time formatters, and even looping constructs.</span></span>

## <a name="how-to-create-a-transform"></a><span data-ttu-id="d7bb0-111">Como criar uma transformação?</span><span class="sxs-lookup"><span data-stu-id="d7bb0-111">How to create a transform?</span></span>
<span data-ttu-id="d7bb0-112">Você pode criar uma transformação/mapa usando o [SDK do Enterprise Integration](https://aka.ms/vsmapsandschemas)do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d7bb0-112">You can create a transform/map by using the Visual Studio [Enterprise Integration SDK](https://aka.ms/vsmapsandschemas).</span></span> <span data-ttu-id="d7bb0-113">Após a conclusão da criação e do teste da transformação, carregue a transformação em sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="d7bb0-113">When you are finished creating and testing the transform, you upload the transform into your integration account.</span></span> 

## <a name="how-to-use-a-transform"></a><span data-ttu-id="d7bb0-114">Como usar uma transformação</span><span class="sxs-lookup"><span data-stu-id="d7bb0-114">How to use a transform</span></span>
<span data-ttu-id="d7bb0-115">Depois de carregar a transformação em sua conta de integração, você poderá usá-la para criar um Aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="d7bb0-115">After you upload the transform/map into your integration account, you can use it to create a Logic app.</span></span> <span data-ttu-id="d7bb0-116">O Aplicativo lógico executará suas transformações sempre que o Aplicativo lógico for acionado (e quando houver um conteúdo de entrada que exija transformação).</span><span class="sxs-lookup"><span data-stu-id="d7bb0-116">The Logic app runs your transformations whenever the Logic app is triggered (and there is input content that needs to be transformed).</span></span>

<span data-ttu-id="d7bb0-117">**Estas são as etapas para usar uma transformação**:</span><span class="sxs-lookup"><span data-stu-id="d7bb0-117">**Here are the steps to use a transform**:</span></span>

### <a name="prerequisites"></a><span data-ttu-id="d7bb0-118">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d7bb0-118">Prerequisites</span></span>

* <span data-ttu-id="d7bb0-119">Criar uma conta de integração e adicionar um mapa a ela</span><span class="sxs-lookup"><span data-stu-id="d7bb0-119">Create an integration account and add a map to it</span></span>  

<span data-ttu-id="d7bb0-120">Agora que você cuidou dos pré-requisitos, é hora de criar seu Aplicativo lógico:</span><span class="sxs-lookup"><span data-stu-id="d7bb0-120">Now that you've taken care of the prerequisites, it's time to create your Logic app:</span></span>  

1. <span data-ttu-id="d7bb0-121">Crie um Aplicativo Lógico e [vincule-o à sua conta de integração](../logic-apps/logic-apps-enterprise-integration-accounts.md "Saiba como vincular uma conta de integração a um Aplicativo lógico") que contém o mapa.</span><span class="sxs-lookup"><span data-stu-id="d7bb0-121">Create a Logic app and [link it to your integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn to link an integration account to a Logic app") that contains the map.</span></span>
2. <span data-ttu-id="d7bb0-122">Adicione um gatilho de **Solicitação** a seu Aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="d7bb0-122">Add a **Request** trigger to your Logic app</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-1.png)    
3. <span data-ttu-id="d7bb0-123">Adicione a ação **Transformar XML** selecionando primeiro **Adicionar uma ação** </span><span class="sxs-lookup"><span data-stu-id="d7bb0-123">Add the **Transform XML** action by first selecting **Add an action** </span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-2.png)   
4. <span data-ttu-id="d7bb0-124">Insira a palavra *transformação* na caixa de pesquisa para filtrar todas as ações para encontrar aquela que você deseja usar</span><span class="sxs-lookup"><span data-stu-id="d7bb0-124">Enter the word *transform* in the search box to filter all the actions to the one that you want to use</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-3.png)  
5. <span data-ttu-id="d7bb0-125">Selecione a ação **Transformar XML**</span><span class="sxs-lookup"><span data-stu-id="d7bb0-125">Select the **Transform XML** action</span></span>   
6. <span data-ttu-id="d7bb0-126">Adicione o **CONTEÚDO** XML que você transformar.</span><span class="sxs-lookup"><span data-stu-id="d7bb0-126">Add the XML **CONTENT** that you transform.</span></span> <span data-ttu-id="d7bb0-127">Você pode usar quaisquer dados XML recebidos na solicitação HTTP como o **CONTEÚDO**.</span><span class="sxs-lookup"><span data-stu-id="d7bb0-127">You can use any XML data you receive in the HTTP request as the **CONTENT**.</span></span> <span data-ttu-id="d7bb0-128">Neste exemplo, selecione o corpo da solicitação HTTP que disparou o Aplicativo Lógico.</span><span class="sxs-lookup"><span data-stu-id="d7bb0-128">In this example, select the body of the HTTP request that triggered the Logic app.</span></span>
7. <span data-ttu-id="d7bb0-129">Selecione o nome do **MAPA** que você deseja usar para executar a transformação.</span><span class="sxs-lookup"><span data-stu-id="d7bb0-129">Select the name of the **MAP** that you want to use to perform the transformation.</span></span> <span data-ttu-id="d7bb0-130">O mapa já deve estar em sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="d7bb0-130">The map must already be in your integration account.</span></span> <span data-ttu-id="d7bb0-131">Em uma etapa anterior, você já deu ao seu Aplicativo lógico acesso à sua conta de integração que contém o mapa.</span><span class="sxs-lookup"><span data-stu-id="d7bb0-131">In an earlier step, you already gave your Logic app access to your integration account that contains your map.</span></span>      
   ![](./media/logic-apps-enterprise-integration-transforms/transform-4.png) 
8. <span data-ttu-id="d7bb0-132">Salve seu trabalho </span><span class="sxs-lookup"><span data-stu-id="d7bb0-132">Save your work</span></span>  
    ![](./media/logic-apps-enterprise-integration-transforms/transform-5.png) 

<span data-ttu-id="d7bb0-133">Neste ponto, você já configurou seu mapa.</span><span class="sxs-lookup"><span data-stu-id="d7bb0-133">At this point, you are finished setting up your map.</span></span> <span data-ttu-id="d7bb0-134">Em um aplicativo real, convém armazenar os dados transformados em um aplicativo LOB, como o SalesForce.</span><span class="sxs-lookup"><span data-stu-id="d7bb0-134">In a real world application, you may want to store the transformed data in an LOB application such as SalesForce.</span></span> <span data-ttu-id="d7bb0-135">Você pode adicionar facilmente uma ação para enviar a saída da transformação para o Salesforce.</span><span class="sxs-lookup"><span data-stu-id="d7bb0-135">You can easily as an action to send the output of the transform to Salesforce.</span></span> 

<span data-ttu-id="d7bb0-136">Agora você pode testar a ação de transformação fazendo uma solicitação ao ponto de extremidade HTTP.</span><span class="sxs-lookup"><span data-stu-id="d7bb0-136">You can now test your transform by making a request to the HTTP endpoint.</span></span>  

## <a name="features-and-use-cases"></a><span data-ttu-id="d7bb0-137">Recursos e casos de uso</span><span class="sxs-lookup"><span data-stu-id="d7bb0-137">Features and use cases</span></span>
* <span data-ttu-id="d7bb0-138">A transformação criada em um mapa pode ser simples, como copiar um nome e endereço de um documento para outro.</span><span class="sxs-lookup"><span data-stu-id="d7bb0-138">The transformation created in a map can be simple, such as copying a name and address from one document to another.</span></span> <span data-ttu-id="d7bb0-139">Ou você pode criar transformações mais complexas usando as operações de mapa prontas para uso.</span><span class="sxs-lookup"><span data-stu-id="d7bb0-139">Or, you can create more complex transformations using the out-of-the-box map operations.</span></span>  
* <span data-ttu-id="d7bb0-140">Várias operações ou funções de mapeamento estão disponíveis, incluindo cadeias de caracteres, funções de data e hora, e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="d7bb0-140">Multiple map operations or functions are readily available, including strings, date time functions, and so on.</span></span>  
* <span data-ttu-id="d7bb0-141">Você pode fazer uma cópia de dados direta entre os esquemas.</span><span class="sxs-lookup"><span data-stu-id="d7bb0-141">You can do a direct data copy between the schemas.</span></span> <span data-ttu-id="d7bb0-142">No Mapeador incluído no SDK, isso é tão simples quanto desenhar uma linha que conecta os elementos no esquema de origem aos seus correspondentes no esquema de destino.</span><span class="sxs-lookup"><span data-stu-id="d7bb0-142">In the Mapper included in the SDK, this is as simple as drawing a line that connects the elements in the source schema with their counterparts in the destination schema.</span></span>  
* <span data-ttu-id="d7bb0-143">Ao criar um mapa, você exibe uma representação gráfica do mapa, que mostra todas as relações e os links que você cria.</span><span class="sxs-lookup"><span data-stu-id="d7bb0-143">When creating a map, you view a graphical representation of the map, which shows all the relationships and links you create.</span></span>
* <span data-ttu-id="d7bb0-144">Use o recurso Testar Mapa para adicionar uma mensagem XML de exemplo.</span><span class="sxs-lookup"><span data-stu-id="d7bb0-144">Use the Test Map feature to add a sample XML message.</span></span> <span data-ttu-id="d7bb0-145">Com um simples clique, você pode testar o mapa que você criou e ver a saída gerada.</span><span class="sxs-lookup"><span data-stu-id="d7bb0-145">With a simple click, you can test the map you created, and see the generated output.</span></span>  
* <span data-ttu-id="d7bb0-146">Carregar mapas existentes</span><span class="sxs-lookup"><span data-stu-id="d7bb0-146">Upload existing maps</span></span>  
* <span data-ttu-id="d7bb0-147">Inclui suporte para o formato XML.</span><span class="sxs-lookup"><span data-stu-id="d7bb0-147">Includes support for the XML format.</span></span>

## <a name="learn-more"></a><span data-ttu-id="d7bb0-148">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="d7bb0-148">Learn more</span></span>
* [<span data-ttu-id="d7bb0-149">Saiba mais sobre o Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="d7bb0-149">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Saiba mais sobre o Enterprise Integration Pack")  
* [<span data-ttu-id="d7bb0-150">Saiba mais sobre mapas</span><span class="sxs-lookup"><span data-stu-id="d7bb0-150">Learn more about maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "Saiba mais sobre mapas da integração corporativa")  

