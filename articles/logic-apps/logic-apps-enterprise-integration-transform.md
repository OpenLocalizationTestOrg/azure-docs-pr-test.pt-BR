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
# <a name="enterprise-integration-with-xml-transforms"></a><span data-ttu-id="b52e7-103">Integração corporativa com transformações XML</span><span class="sxs-lookup"><span data-stu-id="b52e7-103">Enterprise integration with XML transforms</span></span>
## <a name="overview"></a><span data-ttu-id="b52e7-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="b52e7-104">Overview</span></span>
<span data-ttu-id="b52e7-105">conector de transformação de integração Olá corporativo converte dados de um formato de tooanother de formato.</span><span class="sxs-lookup"><span data-stu-id="b52e7-105">hello Enterprise integration Transform connector converts data from one format tooanother format.</span></span> <span data-ttu-id="b52e7-106">Por exemplo, você pode ter uma mensagem de entrada que contém Olá data atual no formato de YearMonthDay hello.</span><span class="sxs-lookup"><span data-stu-id="b52e7-106">For example, you may have an incoming message that contains hello current date in hello YearMonthDay format.</span></span> <span data-ttu-id="b52e7-107">Você pode usar um toobe do transformação tooreformat Olá data no formato de MonthDayYear Olá.</span><span class="sxs-lookup"><span data-stu-id="b52e7-107">You can use a transform tooreformat hello date toobe in hello MonthDayYear format.</span></span>

## <a name="what-does-a-transform-do"></a><span data-ttu-id="b52e7-108">O que uma transformação faz?</span><span class="sxs-lookup"><span data-stu-id="b52e7-108">What does a transform do?</span></span>
<span data-ttu-id="b52e7-109">Uma transformação, que é também conhecido como um mapa, consiste em um esquema XML de origem (Olá de entrada) e um esquema XML de destino (saída Olá).</span><span class="sxs-lookup"><span data-stu-id="b52e7-109">A Transform, which is also known as a map, consists of a Source XML schema (hello input) and a Target XML schema (hello output).</span></span> <span data-ttu-id="b52e7-110">Você pode usar funções internas diferentes toohelp manipular ou controlar dados Olá, incluindo manipulações de cadeia de caracteres, atribuições condicionais, expressões aritméticas, formatadores de tempo de data e até mesmo construções de loop.</span><span class="sxs-lookup"><span data-stu-id="b52e7-110">You can use different built-in functions toohelp manipulate or control hello data, including string manipulations, conditional assignments, arithmetic expressions, date time formatters, and even looping constructs.</span></span>

## <a name="how-toocreate-a-transform"></a><span data-ttu-id="b52e7-111">Como toocreate uma transformação?</span><span class="sxs-lookup"><span data-stu-id="b52e7-111">How toocreate a transform?</span></span>
<span data-ttu-id="b52e7-112">Você pode criar um mapa de transformação/usando o Visual Studio de saudação [Enterprise integração SDK](https://aka.ms/vsmapsandschemas).</span><span class="sxs-lookup"><span data-stu-id="b52e7-112">You can create a transform/map by using hello Visual Studio [Enterprise Integration SDK](https://aka.ms/vsmapsandschemas).</span></span> <span data-ttu-id="b52e7-113">Quando tiver terminado de criar e testar transformação hello, carregar transformação Olá em sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="b52e7-113">When you are finished creating and testing hello transform, you upload hello transform into your integration account.</span></span> 

## <a name="how-toouse-a-transform"></a><span data-ttu-id="b52e7-114">Como toouse uma transformação</span><span class="sxs-lookup"><span data-stu-id="b52e7-114">How toouse a transform</span></span>
<span data-ttu-id="b52e7-115">Depois de carregar transformação/mapa Olá em sua conta de integração, você pode usar um aplicativo de lógica de toocreate.</span><span class="sxs-lookup"><span data-stu-id="b52e7-115">After you upload hello transform/map into your integration account, you can use it toocreate a Logic app.</span></span> <span data-ttu-id="b52e7-116">Olá lógica aplicativo executa transformações sempre que Olá lógica aplicativo é disparado (e não há conteúdo de entrada que precisa toobe transformado).</span><span class="sxs-lookup"><span data-stu-id="b52e7-116">hello Logic app runs your transformations whenever hello Logic app is triggered (and there is input content that needs toobe transformed).</span></span>

<span data-ttu-id="b52e7-117">**Aqui está Olá etapas toouse uma transformação**:</span><span class="sxs-lookup"><span data-stu-id="b52e7-117">**Here are hello steps toouse a transform**:</span></span>

### <a name="prerequisites"></a><span data-ttu-id="b52e7-118">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b52e7-118">Prerequisites</span></span>

* <span data-ttu-id="b52e7-119">Criar uma conta de integração e adicionar um mapa tooit</span><span class="sxs-lookup"><span data-stu-id="b52e7-119">Create an integration account and add a map tooit</span></span>  

<span data-ttu-id="b52e7-120">Agora que atentar dos pré-requisitos Olá, é hora toocreate sua lógica de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="b52e7-120">Now that you've taken care of hello prerequisites, it's time toocreate your Logic app:</span></span>  

1. <span data-ttu-id="b52e7-121">Criar um aplicativo de lógica e [vinculá-lo a conta de integração de tooyour](../logic-apps/logic-apps-enterprise-integration-accounts.md "Saiba toolink um aplicativo de conta tooa lógica da integração") que contém o mapa de saudação.</span><span class="sxs-lookup"><span data-stu-id="b52e7-121">Create a Logic app and [link it tooyour integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn toolink an integration account tooa Logic app") that contains hello map.</span></span>
2. <span data-ttu-id="b52e7-122">Adicionar um **solicitação** gatilho tooyour lógica aplicativo</span><span class="sxs-lookup"><span data-stu-id="b52e7-122">Add a **Request** trigger tooyour Logic app</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-1.png)    
3. <span data-ttu-id="b52e7-123">Adicionar Olá **transformação XML** ação selecionando primeiro **adicionar uma ação** </span><span class="sxs-lookup"><span data-stu-id="b52e7-123">Add hello **Transform XML** action by first selecting **Add an action** </span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-2.png)   
4. <span data-ttu-id="b52e7-124">Inserir palavra hello *transformar* em toofilter de caixa de pesquisa Olá todos Olá toohello ações um que você deseja toouse</span><span class="sxs-lookup"><span data-stu-id="b52e7-124">Enter hello word *transform* in hello search box toofilter all hello actions toohello one that you want toouse</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-3.png)  
5. <span data-ttu-id="b52e7-125">Selecione Olá **transformação XML** ação</span><span class="sxs-lookup"><span data-stu-id="b52e7-125">Select hello **Transform XML** action</span></span>   
6. <span data-ttu-id="b52e7-126">Adicionar Olá XML **conteúdo** que você transformar.</span><span class="sxs-lookup"><span data-stu-id="b52e7-126">Add hello XML **CONTENT** that you transform.</span></span> <span data-ttu-id="b52e7-127">Você pode usar qualquer dados XML recebidos na solicitação Olá HTTP como Olá **conteúdo**.</span><span class="sxs-lookup"><span data-stu-id="b52e7-127">You can use any XML data you receive in hello HTTP request as hello **CONTENT**.</span></span> <span data-ttu-id="b52e7-128">Neste exemplo, selecione corpo Olá de solicitação HTTP Olá que disparou o aplicativo lógico de saudação.</span><span class="sxs-lookup"><span data-stu-id="b52e7-128">In this example, select hello body of hello HTTP request that triggered hello Logic app.</span></span>
7. <span data-ttu-id="b52e7-129">Nome hello Select de saudação **mapa** que você queira a transformação de saudação do toouse tooperform.</span><span class="sxs-lookup"><span data-stu-id="b52e7-129">Select hello name of hello **MAP** that you want toouse tooperform hello transformation.</span></span> <span data-ttu-id="b52e7-130">mapa de saudação já deve estar em sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="b52e7-130">hello map must already be in your integration account.</span></span> <span data-ttu-id="b52e7-131">Em uma etapa anterior, você já atribuiu sua lógica acesso tooyour integração conta do aplicativo que contém o mapa.</span><span class="sxs-lookup"><span data-stu-id="b52e7-131">In an earlier step, you already gave your Logic app access tooyour integration account that contains your map.</span></span>      
   ![](./media/logic-apps-enterprise-integration-transforms/transform-4.png) 
8. <span data-ttu-id="b52e7-132">Salve seu trabalho </span><span class="sxs-lookup"><span data-stu-id="b52e7-132">Save your work</span></span>  
    ![](./media/logic-apps-enterprise-integration-transforms/transform-5.png) 

<span data-ttu-id="b52e7-133">Neste ponto, você já configurou seu mapa.</span><span class="sxs-lookup"><span data-stu-id="b52e7-133">At this point, you are finished setting up your map.</span></span> <span data-ttu-id="b52e7-134">Em um aplicativo do mundo real, convém toostore dados de saudação transformado em um aplicativo de LOB, como a equipe de vendas.</span><span class="sxs-lookup"><span data-stu-id="b52e7-134">In a real world application, you may want toostore hello transformed data in an LOB application such as SalesForce.</span></span> <span data-ttu-id="b52e7-135">Você pode facilmente como uma saída de saudação do toosend de ação do hello transformar tooSalesforce.</span><span class="sxs-lookup"><span data-stu-id="b52e7-135">You can easily as an action toosend hello output of hello transform tooSalesforce.</span></span> 

<span data-ttu-id="b52e7-136">Agora você pode testar sua transformação fazendo um ponto de extremidade HTTP de toohello de solicitação.</span><span class="sxs-lookup"><span data-stu-id="b52e7-136">You can now test your transform by making a request toohello HTTP endpoint.</span></span>  

## <a name="features-and-use-cases"></a><span data-ttu-id="b52e7-137">Recursos e casos de uso</span><span class="sxs-lookup"><span data-stu-id="b52e7-137">Features and use cases</span></span>
* <span data-ttu-id="b52e7-138">transformação de saudação criada em um mapa pode ser simple, como copiar um nome e endereço de um tooanother de documento.</span><span class="sxs-lookup"><span data-stu-id="b52e7-138">hello transformation created in a map can be simple, such as copying a name and address from one document tooanother.</span></span> <span data-ttu-id="b52e7-139">Ou, você pode criar transformações mais complexas usando operações Olá fora da caixa.</span><span class="sxs-lookup"><span data-stu-id="b52e7-139">Or, you can create more complex transformations using hello out-of-the-box map operations.</span></span>  
* <span data-ttu-id="b52e7-140">Várias operações ou funções de mapeamento estão disponíveis, incluindo cadeias de caracteres, funções de data e hora, e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="b52e7-140">Multiple map operations or functions are readily available, including strings, date time functions, and so on.</span></span>  
* <span data-ttu-id="b52e7-141">Você pode fazer uma cópia de dados direto entre esquemas de saudação.</span><span class="sxs-lookup"><span data-stu-id="b52e7-141">You can do a direct data copy between hello schemas.</span></span> <span data-ttu-id="b52e7-142">Olá que mapeador incluído no SDK do hello, isso é simple como desenhar uma linha que conecta os elementos Olá no esquema de origem de saudação com suas contrapartes no esquema de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="b52e7-142">In hello Mapper included in hello SDK, this is as simple as drawing a line that connects hello elements in hello source schema with their counterparts in hello destination schema.</span></span>  
* <span data-ttu-id="b52e7-143">Ao criar um mapa, você pode exibir uma representação gráfica de mapa hello, que mostra todas as relações de saudação e links que você criar.</span><span class="sxs-lookup"><span data-stu-id="b52e7-143">When creating a map, you view a graphical representation of hello map, which shows all hello relationships and links you create.</span></span>
* <span data-ttu-id="b52e7-144">Use Olá mapa de teste recurso tooadd uma mensagem XML de exemplo.</span><span class="sxs-lookup"><span data-stu-id="b52e7-144">Use hello Test Map feature tooadd a sample XML message.</span></span> <span data-ttu-id="b52e7-145">Com um clique simple, você pode testar mapa Olá criado e consulte a saída de hello gerado.</span><span class="sxs-lookup"><span data-stu-id="b52e7-145">With a simple click, you can test hello map you created, and see hello generated output.</span></span>  
* <span data-ttu-id="b52e7-146">Carregar mapas existentes</span><span class="sxs-lookup"><span data-stu-id="b52e7-146">Upload existing maps</span></span>  
* <span data-ttu-id="b52e7-147">Inclui suporte para o formato do XML de saudação.</span><span class="sxs-lookup"><span data-stu-id="b52e7-147">Includes support for hello XML format.</span></span>

## <a name="learn-more"></a><span data-ttu-id="b52e7-148">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="b52e7-148">Learn more</span></span>
* [<span data-ttu-id="b52e7-149">Saiba mais sobre Olá Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="b52e7-149">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise")  
* [<span data-ttu-id="b52e7-150">Saiba mais sobre mapas</span><span class="sxs-lookup"><span data-stu-id="b52e7-150">Learn more about maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "Saiba mais sobre mapas da integração corporativa")  

