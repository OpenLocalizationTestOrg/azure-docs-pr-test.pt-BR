---
title: "Restringir o conteúdo da CDN do Azure por país | Microsoft Docs"
description: "Aprenda a restringir o acesso ao seu conteúdo da CDN do Azure usando o recurso Filtragem geográfica."
services: cdn
documentationcenter: 
author: lichard
manager: akucer
editor: 
ms.assetid: 12c17cc5-28ee-4b0b-ba22-2266be2e786a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 30160088d9c770400f342e67527e1cf1cabc4f6b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="restrict-azure-cdn-content-by-country"></a><span data-ttu-id="95193-103">Restringir conteúdo da CDN do Azure por país</span><span class="sxs-lookup"><span data-stu-id="95193-103">Restrict Azure CDN content by country</span></span>

## <a name="overview"></a><span data-ttu-id="95193-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="95193-104">Overview</span></span>
<span data-ttu-id="95193-105">Quando um usuário solicita o conteúdo, por padrão, o conteúdo é apresentado, independentemente de onde o usuário fez essa solicitação.</span><span class="sxs-lookup"><span data-stu-id="95193-105">When a user requests your content, by default, the content is served regardless of where the user made this request from.</span></span> <span data-ttu-id="95193-106">Em alguns casos, você talvez queira restringir o acesso ao seu conteúdo por país.</span><span class="sxs-lookup"><span data-stu-id="95193-106">In some cases, you may want to restrict access to your content by country.</span></span> <span data-ttu-id="95193-107">Este tópico explica como usar o recurso **Filtragem geográfica** para configurar o serviço para permitir ou bloquear o acesso por país.</span><span class="sxs-lookup"><span data-stu-id="95193-107">This topic explains how to use the **Geo-Filtering** feature in order to configure the service to allow or block access by country.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="95193-108">Os produtos Verizon e Akamai fornecem a mesma funcionalidade de filtragem geográfica mas possuem uma pequena diferença nos códigos do país que suportam.</span><span class="sxs-lookup"><span data-stu-id="95193-108">The Verizon and Akamai products provide the same geo-filtering functionality but have a small difference in te country codes they support.</span></span> <span data-ttu-id="95193-109">Confira a Etapa 3 para obter um link para as diferenças.</span><span class="sxs-lookup"><span data-stu-id="95193-109">See Step 3 for a link to the differences.</span></span>


<span data-ttu-id="95193-110">Para obter informações sobre as considerações que se aplicam à configuração desse tipo de restrições, consulte a seção [Considerações](cdn-restrict-access-by-country.md#considerations) no final do tópico.</span><span class="sxs-lookup"><span data-stu-id="95193-110">For information about considerations that apply to configuring this type of restriction, see the [Considerations](cdn-restrict-access-by-country.md#considerations) section at the end of the topic.</span></span>  

![Filtragem de País](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-the-directory-path"></a><span data-ttu-id="95193-112">Etapa 1: Definir o caminho de diretório</span><span class="sxs-lookup"><span data-stu-id="95193-112">Step 1: Define the directory path</span></span>
<span data-ttu-id="95193-113">Selecione o ponto de extremidade no portal e localize a guia Filtragem geográfica na barra de navegação à esquerda para localizar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="95193-113">Select your endpoint within the portal, and find the Geo-Filtering tab on the left-hand navigation to find this feature.</span></span>

<span data-ttu-id="95193-114">Ao configurar um filtro de país, você deve especificar o caminho relativo para o local o acesso dos usuários será permitido ou negado.</span><span class="sxs-lookup"><span data-stu-id="95193-114">When configuring a country filter, you must specify the relative path to the location to which users will be allowed or denied access.</span></span> <span data-ttu-id="95193-115">Você pode aplicar a filtragem geográfica para todos os arquivos com "/" ou pastas selecionadas, especificando os caminhos de diretório "/pictures/".</span><span class="sxs-lookup"><span data-stu-id="95193-115">You can apply geo-filtering for all your files with "/" or selected folders by specifying directory paths "/pictures/".</span></span> <span data-ttu-id="95193-116">Você também pode aplicar a filtragem geográfica a um único arquivo, especificando o arquivo e omitindo a barra à direita "/pictures/city.png".</span><span class="sxs-lookup"><span data-stu-id="95193-116">You can also apply geo-filtering to a single file by specifying the file, and leaving out the trailing slash "/pictures/city.png".</span></span>

<span data-ttu-id="95193-117">Filtro de caminho do diretório de exemplo:</span><span class="sxs-lookup"><span data-stu-id="95193-117">Example directory path filter:</span></span>

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-the-action-block-or-allow"></a><span data-ttu-id="95193-118">Etapa 2: Definir a ação: bloquear ou permitir</span><span class="sxs-lookup"><span data-stu-id="95193-118">Step 2: Define the action: block or allow</span></span>
<span data-ttu-id="95193-119">**Bloqueio** : os usuários dos países especificados terão o acesso negado a ativos solicitados nesse caminho recursivo.</span><span class="sxs-lookup"><span data-stu-id="95193-119">**Block:** Users from the specified countries will be denied access to assets requested from that recursive path.</span></span> <span data-ttu-id="95193-120">Se nenhuma outra opção de filtragem de país tiver sido configurada para esse local, então, todos os outros usuários terão acesso permitido.</span><span class="sxs-lookup"><span data-stu-id="95193-120">If no other country filtering options have been configured for that location, then all other users will be allowed access.</span></span>

<span data-ttu-id="95193-121">**Permissão** : somente os usuários dos países especificados terão o acesso permitido aos ativos solicitados desse caminho recursivo.</span><span class="sxs-lookup"><span data-stu-id="95193-121">**Allow:** Only users from the specified countries will be allowed access to assets requested from that recursive path.</span></span>

## <a name="step-3-define-the-countries"></a><span data-ttu-id="95193-122">Etapa 3: Definir os países</span><span class="sxs-lookup"><span data-stu-id="95193-122">Step 3: Define the countries</span></span>
<span data-ttu-id="95193-123">Selecione os países que você deseja bloquear ou permitir para o caminho.</span><span class="sxs-lookup"><span data-stu-id="95193-123">Select the countries that you want to block or allow for the path.</span></span> 

<span data-ttu-id="95193-124">Por exemplo, a regra de bloqueio /Photos/Strasbourg/ filtrará arquivos, incluindo:</span><span class="sxs-lookup"><span data-stu-id="95193-124">For example, the rule of blocking /Photos/Strasbourg/ will filter files including:</span></span>

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a><span data-ttu-id="95193-125">Códigos de país</span><span class="sxs-lookup"><span data-stu-id="95193-125">Country codes</span></span>
<span data-ttu-id="95193-126">O recurso **Filtragem geográfica** usa códigos de país para definir os países nos quais uma solicitação será permitida ou bloqueada para um diretório protegido.</span><span class="sxs-lookup"><span data-stu-id="95193-126">The **Geo-Filtering** feature uses country codes to define the countries from which a request will be allowed or blocked for a secured directory.</span></span> <span data-ttu-id="95193-127">Você encontrará os códigos do país na [Códigos do País da CDN do Azure](https://msdn.microsoft.com/library/mt761717.aspx).</span><span class="sxs-lookup"><span data-stu-id="95193-127">You will find the country codes in [Azure CDN  Country Codes](https://msdn.microsoft.com/library/mt761717.aspx).</span></span> 

## <span data-ttu-id="95193-128"><a id="considerations"></a>Considerações</span><span class="sxs-lookup"><span data-stu-id="95193-128"><a id="considerations"></a>Considerations</span></span>
* <span data-ttu-id="95193-129">Pode levar até 90 minutos para a Verizon ou alguns minutos com Akamai, para que as alterações em sua configuração de filtragem do país entrem em vigor.</span><span class="sxs-lookup"><span data-stu-id="95193-129">It may take up to 90 minutes for Verizon, or a couple minutes with Akamai, for changes to your country filtering configuration to take effect.</span></span>
* <span data-ttu-id="95193-130">Esse recurso não oferece suporte a caracteres curinga (por exemplo, ‘*’).</span><span class="sxs-lookup"><span data-stu-id="95193-130">This feature does not support wildcard characters (for example, ‘*’).</span></span>
* <span data-ttu-id="95193-131">A configuração de filtragem geográfica associada com o caminho relativo será aplicada recursivamente para esse caminho.</span><span class="sxs-lookup"><span data-stu-id="95193-131">The geo-filtering configuration associated with the relative path will be applied recursively to that path.</span></span>
* <span data-ttu-id="95193-132">Apenas uma regra pode ser aplicada no mesmo caminho relativo (você não pode criar vários filtros de país que apontam para o mesmo caminho relativo).</span><span class="sxs-lookup"><span data-stu-id="95193-132">Only one rule can be applied to the same relative path (you cannot create multiple country filters that point to the same relative path.</span></span> <span data-ttu-id="95193-133">No entanto, uma pasta pode ter vários filtros de país.</span><span class="sxs-lookup"><span data-stu-id="95193-133">However, a folder may have multiple country filters.</span></span> <span data-ttu-id="95193-134">Isso é devido à natureza recursiva de filtros de país.</span><span class="sxs-lookup"><span data-stu-id="95193-134">This is due to the recursive nature of country filters.</span></span> <span data-ttu-id="95193-135">Em outras palavras, uma subpasta de uma pasta configurada anteriormente pode ter um filtro de país diferente atribuído.</span><span class="sxs-lookup"><span data-stu-id="95193-135">In other words, a subfolder of a previously configured folder can be assigned a different country filter.</span></span>

