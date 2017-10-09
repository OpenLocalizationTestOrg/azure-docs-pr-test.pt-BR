---
title: uso de Caches Redis aaaManaging hello Azure Explorer para IntelliJ | Microsoft Docs
description: Saiba como toomanage o redis do Azure armazena em cache usando hello Azure Explorer para IntelliJ.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/14/2017
ms.author: robmcm
ms.openlocfilehash: 76ba37a2a35c26d0045e17003181108992eb957d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-redis-caches-using-hello-azure-explorer-for-intellij"></a><span data-ttu-id="5eb80-103">Gerenciando Caches Redis usando hello Azure Explorer para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="5eb80-103">Managing Redis Caches using hello Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="5eb80-104">Olá Explorer do Azure, que faz parte da saudação Kit de ferramentas do Azure para IntelliJ, fornece aos desenvolvedores de Java com uma solução fácil de usar para gerenciar caches em sua conta do Azure de dentro de redis Olá IntelliJ IDE.</span><span class="sxs-lookup"><span data-stu-id="5eb80-104">hello Azure Explorer, which is part of hello Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing redis caches in their Azure account from inside hello IntelliJ IDE.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-intellij"></a><span data-ttu-id="5eb80-105">Criar um Cache Redis utilizando IntelliJ</span><span class="sxs-lookup"><span data-stu-id="5eb80-105">Create a Redis Cache by using IntelliJ</span></span>

<span data-ttu-id="5eb80-106">Olá, as etapas a seguir mostram Olá etapas toocreate um cache redis usando hello Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="5eb80-106">hello following steps walk you through hello steps toocreate a redis cache using hello Azure Explorer.</span></span>

1. <span data-ttu-id="5eb80-107">Entrar tooyour conta do Azure usando as etapas de saudação em Olá [entrada em instruções hello Azure Toolkit for IntelliJ] artigo.</span><span class="sxs-lookup"><span data-stu-id="5eb80-107">Sign in tooyour Azure account using hello steps in hello [Sign In Instructions for hello Azure Toolkit for IntelliJ] article.</span></span>

1. <span data-ttu-id="5eb80-108">Em hello **Azure Explorer** janela de ferramenta, expanda Olá **Azure** nó, clique com botão direito **Caches Redis**e, em seguida, clique em **criar Cache Redis**.</span><span class="sxs-lookup"><span data-stu-id="5eb80-108">In hello **Azure Explorer** tool window, expand hello **Azure** node, right-click **Redis Caches**, and then click **Create Redis Cache**.</span></span>

   ![Criar menu Cache Redis][CR01]

1. <span data-ttu-id="5eb80-110">Olá quando **novo Cache Redis** caixa de diálogo aparece, especifique Olá as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="5eb80-110">When hello **New Redis Cache** dialog box appears, specify hello following options:</span></span>

   ![Criar uma caixa de diálogo Novo Cache Redis][CR02]

   <span data-ttu-id="5eb80-112">a.</span><span class="sxs-lookup"><span data-stu-id="5eb80-112">a.</span></span> <span data-ttu-id="5eb80-113">**Nome DNS**: Especifica o subdomínio DNS Olá Olá novo redis cache, que são pré-anexados muito ". redis.cache.windows .net"; por exemplo: *wingtiptoys.redis.cache.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="5eb80-113">**DNS Name**: Specifies hello DNS subdomain for hello new redis cache, which are prepended too".redis.cache.windows.net"; for example: *wingtiptoys.redis.cache.windows.net*.</span></span>

   <span data-ttu-id="5eb80-114">b.</span><span class="sxs-lookup"><span data-stu-id="5eb80-114">b.</span></span> <span data-ttu-id="5eb80-115">**Assinatura**: especifica Olá assinatura do Azure que você deseja toouse para cache redis da nova hello.</span><span class="sxs-lookup"><span data-stu-id="5eb80-115">**Subscription**: Specifies hello Azure subscription you want toouse for hello new redis cache.</span></span>

   <span data-ttu-id="5eb80-116">c.</span><span class="sxs-lookup"><span data-stu-id="5eb80-116">c.</span></span> <span data-ttu-id="5eb80-117">**Grupo de recursos**: Especifica o grupo de recursos de saudação do cache redis; é necessário toochoose de saudação as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="5eb80-117">**Resource Group**: Specifies hello resource group for your redis cache; you need toochoose one of hello following options:</span></span>
      * <span data-ttu-id="5eb80-118">**Criar novo**: Especifica que você deseja toocreate um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="5eb80-118">**Create New**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="5eb80-119">**Usar Existente**: especifica que você escolherá entre uma lista dos grupos de recursos associados à sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="5eb80-119">**Use Existing**: Specifies that you will choose from a list of resource groups associated with your Azure account.</span></span>

   <span data-ttu-id="5eb80-120">d.</span><span class="sxs-lookup"><span data-stu-id="5eb80-120">d.</span></span> <span data-ttu-id="5eb80-121">**Local**: especifica Olá local em que o cache redis é criado; por exemplo, *Oeste dos EUA*.</span><span class="sxs-lookup"><span data-stu-id="5eb80-121">**Location**: Specifies hello location where your redis cache is created; for example, *West US*.</span></span>

   <span data-ttu-id="5eb80-122">e.</span><span class="sxs-lookup"><span data-stu-id="5eb80-122">e.</span></span> <span data-ttu-id="5eb80-123">**Camada de preços**: especifica qual tipo de preço usa o cache redis; essa configuração determina o número de saudação de conexões de cliente.</span><span class="sxs-lookup"><span data-stu-id="5eb80-123">**Pricing Tier**: Specifies which pricing tier your redis cache uses; this setting determines hello number of client connections.</span></span> <span data-ttu-id="5eb80-124">(Para saber mais, veja [Preço do Cache Redis]).</span><span class="sxs-lookup"><span data-stu-id="5eb80-124">(For more information, see [Redis Cache Pricing].)</span></span>

   <span data-ttu-id="5eb80-125">f.</span><span class="sxs-lookup"><span data-stu-id="5eb80-125">f.</span></span> <span data-ttu-id="5eb80-126">**Porta não SSL**: especifica se o cache redis permite conexões não SSL; por padrão, apenas as conexões SSL são permitidas.</span><span class="sxs-lookup"><span data-stu-id="5eb80-126">**Non-SSL port**: Specifies whether your redis cache allows non-SSL connections; by default, only SSL connections are allowed.</span></span>

1. <span data-ttu-id="5eb80-127">Quando tiver especificado todas as configurações de cache redis, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="5eb80-127">When you have specified all your redis cache settings, click **OK**.</span></span>

<span data-ttu-id="5eb80-128">Depois que o cache redis tiver sido criado, ele será exibido no hello Azure Explorer.</span><span class="sxs-lookup"><span data-stu-id="5eb80-128">After your redis cache has been created, it will be displayed in hello Azure Explorer.</span></span>

   ![Cache Redis no Azure Explorer][CR03]

> [!NOTE]
>
> <span data-ttu-id="5eb80-130">Para obter mais informações sobre como configurar o Azure redis as configurações de cache, consulte [como tooconfigure Cache Redis do Azure].</span><span class="sxs-lookup"><span data-stu-id="5eb80-130">For more information about configuring your Azure redis cache settings, see [How tooconfigure Azure Redis Cache].</span></span>
>

## <a name="display-hello-properties-for-your-redis-cache-in-intellij"></a><span data-ttu-id="5eb80-131">Exibir as propriedades de saudação do Cache Redis no IntelliJ</span><span class="sxs-lookup"><span data-stu-id="5eb80-131">Display hello properties for your Redis Cache in IntelliJ</span></span>

1. <span data-ttu-id="5eb80-132">Em hello Azure Explorer, mouse seu cache redis e clique em **Mostrar propriedades**.</span><span class="sxs-lookup"><span data-stu-id="5eb80-132">In hello Azure Explorer, right-click your redis cache and click **Show properties**.</span></span>

   ![Azure Explorer contexto menu toodisplay propriedades para um cache redis][SP01]

1. <span data-ttu-id="5eb80-134">Hello Azure Explorer exibe as propriedades de saudação do cache redis.</span><span class="sxs-lookup"><span data-stu-id="5eb80-134">hello Azure Explorer displays hello properties for your redis cache.</span></span>

   ![Propriedades de cache Redis][SP02]

## <a name="delete-your-redis-cache-by-using-intellij"></a><span data-ttu-id="5eb80-136">Exclua o Cache Redis utilizando o IntelliJ</span><span class="sxs-lookup"><span data-stu-id="5eb80-136">Delete your Redis Cache by using IntelliJ</span></span>

1. <span data-ttu-id="5eb80-137">Em hello Azure Explorer, mouse seu cache redis e clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="5eb80-137">In hello Azure Explorer, right-click your redis cache and click **Delete**.</span></span>

   ![Explorer contexto menu toodelete um cache redis do Azure][DE01]

1. <span data-ttu-id="5eb80-139">Clique em **Sim** quando solicitado toodelete seu cache redis.</span><span class="sxs-lookup"><span data-stu-id="5eb80-139">Click **Yes** when prompted toodelete your redis cache.</span></span>

   ![Excluir prompt do cache redis][DE02]

## <a name="next-steps"></a><span data-ttu-id="5eb80-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5eb80-141">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="5eb80-142">Para obter mais informações sobre caches redis do Azure, as definições de configuração e preços, consulte Olá links a seguir:</span><span class="sxs-lookup"><span data-stu-id="5eb80-142">For more information about Azure redis caches, configuration settings and pricing, see hello following links:</span></span>

* <span data-ttu-id="5eb80-143">[Cache Redis do Azure]</span><span class="sxs-lookup"><span data-stu-id="5eb80-143">[Azure Redis Cache]</span></span>
* <span data-ttu-id="5eb80-144">[Documentação do Cache Redis]</span><span class="sxs-lookup"><span data-stu-id="5eb80-144">[Redis Cache Documentation]</span></span>
* <span data-ttu-id="5eb80-145">[Preço do Cache Redis]</span><span class="sxs-lookup"><span data-stu-id="5eb80-145">[Redis Cache Pricing]</span></span>
* <span data-ttu-id="5eb80-146">[como tooconfigure Cache Redis do Azure]</span><span class="sxs-lookup"><span data-stu-id="5eb80-146">[How tooconfigure Azure Redis Cache]</span></span>

<!-- URL List -->

[Preço do Cache Redis]: https://azure.microsoft.com/pricing/details/cache/
[Cache Redis do Azure]: https://azure.microsoft.com/services/cache/
[Documentação do Cache Redis]: ./redis-cache/index.md
[como tooconfigure Cache Redis do Azure]: ./redis-cache/cache-configure.md
[entrada em instruções hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[CR01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE02.png
