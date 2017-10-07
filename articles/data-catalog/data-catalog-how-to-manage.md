---
title: "ativos de dados aaaManage no catálogo de dados do Azure | Microsoft Docs"
description: "artigo Olá destaca como toocontrol visibilidade e a propriedade de ativos de dados registrados no catálogo de dados do Azure."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 623f5ed4-8da7-48f5-943a-448d0b7cba69
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 48a634b92d7da19c32c9e551f295eec257f54f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-data-assets-in-azure-data-catalog"></a><span data-ttu-id="4d3e9-103">Gerenciar ativos de dados no Catálogo de Dados do Azure</span><span class="sxs-lookup"><span data-stu-id="4d3e9-103">Manage data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="4d3e9-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="4d3e9-104">Introduction</span></span>
<span data-ttu-id="4d3e9-105">Catálogo de dados do Azure é projetado para descoberta de fonte de dados, para que você pode facilmente descobrir e entender as fontes de dados Olá necessário tooperform analysis e tomar decisões.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-105">Azure Data Catalog is designed for data-source discovery, so that you can easily discover and understand hello data sources you need tooperform analysis and make decisions.</span></span> <span data-ttu-id="4d3e9-106">Esses recursos de descoberta tornam impacto maior hello quando você e outros usuários possam localizar e compreender o intervalo mais amplo de saudação de fontes de dados disponíveis.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-106">These discovery capabilities make hello biggest impact when you and other users can find and understand hello broadest range of available data sources.</span></span> <span data-ttu-id="4d3e9-107">Com esses elementos em mente, o comportamento padrão de saudação do catálogo de dados é para todos os dados registrados fontes toobe visível tooand detectável por todos os usuários do catálogo.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-107">With these elements in mind, hello default behavior of Data Catalog is for all registered data sources toobe visible tooand discoverable by all catalog users.</span></span>

<span data-ttu-id="4d3e9-108">Catálogo de dados não dá acesso a dados toohello em si.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-108">Data Catalog does not give you access toohello data itself.</span></span> <span data-ttu-id="4d3e9-109">Acesso a dados é controlado pelo proprietário Olá Olá da fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-109">Data access is controlled by hello owner of hello data source.</span></span> <span data-ttu-id="4d3e9-110">Com o catálogo de dados, você pode descobrir fontes de dados e exibir metadados Olá fontes toohello relacionados que estão registradas no catálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-110">With Data Catalog, you can discover data sources and view hello metadata that's related toohello sources that are registered in hello catalog.</span></span>

<span data-ttu-id="4d3e9-111">Pode haver situações, porém, em que fontes de dados devem ser apenas usuários toospecific visível ou toomembers de grupos específicos.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-111">There might be situations, however, where data sources should only be visible toospecific users, or toomembers of specific groups.</span></span> <span data-ttu-id="4d3e9-112">Nesses cenários, os usuários podem assumir a propriedade de ativos de dados registrados no catálogo hello e, em seguida, controlar a visibilidade de saudação de ativos de saudação que eles possuem.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-112">In such scenarios, users can take ownership of registered data assets within hello catalog and then control hello visibility of hello assets they own.</span></span>

> [!NOTE]
> <span data-ttu-id="4d3e9-113">funcionalidade de saudação descrita neste artigo está disponível apenas no hello Standard Edition do Data Catalog do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-113">hello functionality described in this article is available only in hello Standard Edition of Azure Data Catalog.</span></span> <span data-ttu-id="4d3e9-114">Olá edição gratuita não fornece recursos para a propriedade e restringir a visibilidade de ativos de dados.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-114">hello Free Edition does not provide capabilities for ownership and restricting data-asset visibility.</span></span>
>
>

## <a name="manage-ownership-of-data-assets"></a><span data-ttu-id="4d3e9-115">Gerenciar a propriedade de ativos de dados</span><span class="sxs-lookup"><span data-stu-id="4d3e9-115">Manage ownership of data assets</span></span>
<span data-ttu-id="4d3e9-116">Por padrão, ativos de dados registrados no Catálogo de Dados não têm proprietário.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-116">By default, data assets that are registered in Data Catalog are unowned.</span></span> <span data-ttu-id="4d3e9-117">Qualquer usuário com permissão tooaccess Olá de catálogo pode descobrir e anotar esses ativos.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-117">Any user with permission tooaccess hello catalog can discover and annotate these assets.</span></span> <span data-ttu-id="4d3e9-118">Os usuários podem assumir a propriedade de ativos de dados sem proprietário e, em seguida, limitar a visibilidade de saudação de ativos de saudação que eles possuem.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-118">Users can take ownership of unowned data assets and then limit hello visibility of hello assets they own.</span></span>

<span data-ttu-id="4d3e9-119">Quando um ativo de dados no catálogo de dados é de propriedade, somente os usuários autorizados pelos proprietários de saudação podem descobrir ativos hello e exibir os metadados, e somente os proprietários de saudação podem excluir o ativo de saudação do catálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-119">When a data asset in Data Catalog is owned, only users who are authorized by hello owners can discover hello asset and view its metadata, and only hello owners can delete hello asset from hello catalog.</span></span>

> [!NOTE]
> <span data-ttu-id="4d3e9-120">Propriedade no catálogo de dados afeta apenas os metadados de saudação que são armazenados no catálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-120">Ownership in Data Catalog affects only hello metadata that's stored in hello catalog.</span></span> <span data-ttu-id="4d3e9-121">Propriedade não concede todas as permissões na fonte de dados subjacente hello.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-121">Ownership does not confer any permissions on hello underlying data source.</span></span>
>
>

### <a name="take-ownership"></a><span data-ttu-id="4d3e9-122">Apropriar-se</span><span class="sxs-lookup"><span data-stu-id="4d3e9-122">Take ownership</span></span>
<span data-ttu-id="4d3e9-123">Os usuários podem assumir a propriedade de ativos de dados selecionando Olá **Take Ownership** opção no portal do catálogo de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-123">Users can take ownership of data assets by selecting hello **Take Ownership** option in hello Data Catalog portal.</span></span> <span data-ttu-id="4d3e9-124">Nenhuma permissão especial é necessário tootake propriedade de um ativo de dados sem proprietário.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-124">No special permissions are required tootake ownership of an unowned data asset.</span></span> <span data-ttu-id="4d3e9-125">Qualquer usuário pode apropriar-se de um ativo de dados sem proprietário.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-125">Any user can take ownership of an unowned data asset.</span></span>

### <a name="add-owners-and-co-owners"></a><span data-ttu-id="4d3e9-126">Adicionar proprietários e coproprietários</span><span class="sxs-lookup"><span data-stu-id="4d3e9-126">Add owners and co-owners</span></span>
<span data-ttu-id="4d3e9-127">Se um ativo de dados já tiver um proprietário, outros usuários não poderão simplesmente assumir a propriedade.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-127">If a data asset is already owned, other users cannot simply take ownership.</span></span> <span data-ttu-id="4d3e9-128">Eles deverão ser adicionados como coproprietários por um proprietário existente.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-128">They must be added as co-owners by an existing owner.</span></span> <span data-ttu-id="4d3e9-129">Qualquer proprietário pode adicionar outros usuários ou grupos de segurança como coproprietários.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-129">Any owner can add additional users or security groups as co-owners.</span></span>

> [!NOTE]
> <span data-ttu-id="4d3e9-130">Ele é um toohave de prática recomendada pelo menos duas pessoas como proprietários para qualquer propriedade ativo de dados.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-130">It is a best practice toohave at least two individuals as owners for any owned data asset.</span></span>
>
>

### <a name="remove-owners"></a><span data-ttu-id="4d3e9-131">Remover proprietários</span><span class="sxs-lookup"><span data-stu-id="4d3e9-131">Remove owners</span></span>
<span data-ttu-id="4d3e9-132">Assim como qualquer proprietário ativo pode adicionar coproprietários, qualquer proprietário ativo pode remover qualquer coproprietário.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-132">Just as any asset owner can add co-owners, any asset owner can remove any co-owner.</span></span>

<span data-ttu-id="4d3e9-133">Um proprietário do ativo que remove a mesmo como um proprietário não poderá mais gerenciar ativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-133">An asset owner who removes him or herself as an owner can no longer manage hello asset.</span></span> <span data-ttu-id="4d3e9-134">Se o proprietário do ativo Olá remove a mesmo como um proprietário e não há nenhum outros co-proprietários, ativo Olá reverte tooan sem proprietário estado.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-134">If hello asset owner removes him or herself as an owner and there are no other co-owners, hello asset reverts tooan unowned state.</span></span>

## <a name="control-visibility"></a><span data-ttu-id="4d3e9-135">Controlar a visibilidade</span><span class="sxs-lookup"><span data-stu-id="4d3e9-135">Control visibility</span></span>
<span data-ttu-id="4d3e9-136">Os proprietários dos ativos de dados podem controlar a visibilidade de Olá Olá de ativos de dados que eles possuem.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-136">Data-asset owners can control hello visibility of hello data assets they own.</span></span> <span data-ttu-id="4d3e9-137">visibilidade toorestrict como padrão Olá, onde todos os usuários podem descobrir de catálogo de dados e exibição Olá ativo de dados, proprietário do ativo Olá pode alternar a configuração de visibilidade de saudação do **todos** muito**proprietários e esses usuários** nas propriedades de saudação para ativo hello.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-137">toorestrict visibility as hello default, where all Data Catalog users can discover and view hello data asset, hello asset owner can toggle hello visibility setting from **Everyone** too**Owners & These Users** in hello properties for hello asset.</span></span> <span data-ttu-id="4d3e9-138">Em seguida, os proprietários podem adicionar usuários e grupos de segurança específicos.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-138">Owners can then add specific users and security groups.</span></span>

> [!NOTE]
> <span data-ttu-id="4d3e9-139">Sempre que possível, devem ser atribuídas permissões de propriedade e visibilidade de ativos toosecurity grupos e usuários de tooindividual não.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-139">Whenever possible, asset ownership and visibility permissions should be assigned toosecurity groups and not tooindividual users.</span></span>
>
>

## <a name="catalog-administrators"></a><span data-ttu-id="4d3e9-140">Administradores do Catálogo</span><span class="sxs-lookup"><span data-stu-id="4d3e9-140">Catalog administrators</span></span>
<span data-ttu-id="4d3e9-141">Os administradores do catálogo de dados são implicitamente co-proprietários de todos os ativos no catálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-141">Data Catalog administrators are implicitly co-owners of all assets in hello catalog.</span></span> <span data-ttu-id="4d3e9-142">Os proprietários dos ativos não é possível remover a visibilidade dos administradores, e os administradores podem gerenciar propriedade e visibilidade de todos os ativos de dados no catálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-142">Asset owners cannot remove visibility from administrators, and administrators can manage ownership and visibility for all data assets in hello catalog.</span></span>

## <a name="summary"></a><span data-ttu-id="4d3e9-143">Resumo</span><span class="sxs-lookup"><span data-stu-id="4d3e9-143">Summary</span></span>
<span data-ttu-id="4d3e9-144">Olá catálogo de dados crowdsourcing modelo toometadata e os dados ativos descoberta permite que todos os toocontribute de usuários do catálogo e descobrir.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-144">hello Data Catalog crowdsourcing model toometadata and data asset discovery allows all catalog users toocontribute and discover.</span></span> <span data-ttu-id="4d3e9-145">Olá edição Standard do catálogo de dados destina-se a visibilidade de saudação toolimit propriedade e o gerenciamento e o uso de ativos de dados específico.</span><span class="sxs-lookup"><span data-stu-id="4d3e9-145">hello Standard Edition of Data Catalog is designed for ownership and management toolimit hello visibility and use of specific data assets.</span></span>
