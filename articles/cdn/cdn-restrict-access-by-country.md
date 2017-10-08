---
title: "aaaRestrict conteúdo da CDN do Azure por país | Microsoft Docs"
description: "Saiba como toorestrict acesso tooyour Azure CDN conteúdo usando Olá recurso filtragem de replicação geográfica."
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
ms.openlocfilehash: ffdd994612b6c9cfbf1a6e29d260709b4afa86e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-azure-cdn-content-by-country"></a><span data-ttu-id="723c3-103">Restringir conteúdo da CDN do Azure por país</span><span class="sxs-lookup"><span data-stu-id="723c3-103">Restrict Azure CDN content by country</span></span>

## <a name="overview"></a><span data-ttu-id="723c3-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="723c3-104">Overview</span></span>
<span data-ttu-id="723c3-105">Quando um usuário solicita o conteúdo, por padrão, o conteúdo de saudação é atendido, independentemente de onde o usuário Olá feita essa solicitação de.</span><span class="sxs-lookup"><span data-stu-id="723c3-105">When a user requests your content, by default, hello content is served regardless of where hello user made this request from.</span></span> <span data-ttu-id="723c3-106">Em alguns casos, convém toorestrict acessar o conteúdo de tooyour por país.</span><span class="sxs-lookup"><span data-stu-id="723c3-106">In some cases, you may want toorestrict access tooyour content by country.</span></span> <span data-ttu-id="723c3-107">Este tópico explica como Olá toouse **filtragem geográfica** recurso na ordem tooconfigure Olá tooallow ou bloquear acesso ao serviço por país.</span><span class="sxs-lookup"><span data-stu-id="723c3-107">This topic explains how toouse hello **Geo-Filtering** feature in order tooconfigure hello service tooallow or block access by country.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="723c3-108">produtos de Verizon e Akamai Olá fornecem Olá a mesma funcionalidade de filtragem de replicação geográfica, mas tem uma pequena diferença na códigos de país te dão suporte.</span><span class="sxs-lookup"><span data-stu-id="723c3-108">hello Verizon and Akamai products provide hello same geo-filtering functionality but have a small difference in te country codes they support.</span></span> <span data-ttu-id="723c3-109">Consulte a etapa 3 para diferenças de toohello um link.</span><span class="sxs-lookup"><span data-stu-id="723c3-109">See Step 3 for a link toohello differences.</span></span>


<span data-ttu-id="723c3-110">Para obter informações sobre as considerações que se aplicam a tooconfiguring esse tipo de restrição, consulte Olá [considerações](cdn-restrict-access-by-country.md#considerations) seção final Olá Olá tópico.</span><span class="sxs-lookup"><span data-stu-id="723c3-110">For information about considerations that apply tooconfiguring this type of restriction, see hello [Considerations](cdn-restrict-access-by-country.md#considerations) section at hello end of hello topic.</span></span>  

![Filtragem de País](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-hello-directory-path"></a><span data-ttu-id="723c3-112">Etapa 1: Definir o caminho do diretório Olá</span><span class="sxs-lookup"><span data-stu-id="723c3-112">Step 1: Define hello directory path</span></span>
<span data-ttu-id="723c3-113">Selecione o ponto de extremidade no portal de saudação e Olá filtragem geográfica guia Olá toofind de navegação à esquerda para acessar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="723c3-113">Select your endpoint within hello portal, and find hello Geo-Filtering tab on hello left-hand navigation toofind this feature.</span></span>

<span data-ttu-id="723c3-114">Ao configurar um filtro de país, você deve especificar os usuários do hello caminho relativo toohello local toowhich serão permitidos ou negados o acesso.</span><span class="sxs-lookup"><span data-stu-id="723c3-114">When configuring a country filter, you must specify hello relative path toohello location toowhich users will be allowed or denied access.</span></span> <span data-ttu-id="723c3-115">Você pode aplicar a filtragem geográfica para todos os arquivos com "/" ou pastas selecionadas, especificando os caminhos de diretório "/pictures/".</span><span class="sxs-lookup"><span data-stu-id="723c3-115">You can apply geo-filtering for all your files with "/" or selected folders by specifying directory paths "/pictures/".</span></span> <span data-ttu-id="723c3-116">Você também pode aplicar a filtragem geográfica tooa arquivo único, especificando o arquivo hello e omitindo Olá barra "/ imagens/cidade.png".</span><span class="sxs-lookup"><span data-stu-id="723c3-116">You can also apply geo-filtering tooa single file by specifying hello file, and leaving out hello trailing slash "/pictures/city.png".</span></span>

<span data-ttu-id="723c3-117">Filtro de caminho do diretório de exemplo:</span><span class="sxs-lookup"><span data-stu-id="723c3-117">Example directory path filter:</span></span>

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-hello-action-block-or-allow"></a><span data-ttu-id="723c3-118">Etapa 2: Definir a ação de saudação: bloquear ou permitir</span><span class="sxs-lookup"><span data-stu-id="723c3-118">Step 2: Define hello action: block or allow</span></span>
<span data-ttu-id="723c3-119">**Bloquear:** usuários de saudação especificaram países serão negadas acesso tooassets solicitada pelo caminho recursiva.</span><span class="sxs-lookup"><span data-stu-id="723c3-119">**Block:** Users from hello specified countries will be denied access tooassets requested from that recursive path.</span></span> <span data-ttu-id="723c3-120">Se nenhuma outra opção de filtragem de país tiver sido configurada para esse local, então, todos os outros usuários terão acesso permitido.</span><span class="sxs-lookup"><span data-stu-id="723c3-120">If no other country filtering options have been configured for that location, then all other users will be allowed access.</span></span>

<span data-ttu-id="723c3-121">**Permitir:** apenas os usuários de saudação especificaram países poderão ser tooassets de acesso solicitado do caminho recursiva.</span><span class="sxs-lookup"><span data-stu-id="723c3-121">**Allow:** Only users from hello specified countries will be allowed access tooassets requested from that recursive path.</span></span>

## <a name="step-3-define-hello-countries"></a><span data-ttu-id="723c3-122">Etapa 3: Definir países Olá</span><span class="sxs-lookup"><span data-stu-id="723c3-122">Step 3: Define hello countries</span></span>
<span data-ttu-id="723c3-123">Selecione Olá países que você deseja tooblock ou permitir para o caminho de saudação.</span><span class="sxs-lookup"><span data-stu-id="723c3-123">Select hello countries that you want tooblock or allow for hello path.</span></span> 

<span data-ttu-id="723c3-124">Por exemplo, a regra de saudação do bloqueio /Photos/Strasbourg/filtrará arquivos, incluindo:</span><span class="sxs-lookup"><span data-stu-id="723c3-124">For example, hello rule of blocking /Photos/Strasbourg/ will filter files including:</span></span>

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a><span data-ttu-id="723c3-125">Códigos de país</span><span class="sxs-lookup"><span data-stu-id="723c3-125">Country codes</span></span>
<span data-ttu-id="723c3-126">Olá **filtragem geográfica** recurso usa países país códigos toodefine saudação do qual uma solicitação será permitida ou bloqueada para um diretório protegido.</span><span class="sxs-lookup"><span data-stu-id="723c3-126">hello **Geo-Filtering** feature uses country codes toodefine hello countries from which a request will be allowed or blocked for a secured directory.</span></span> <span data-ttu-id="723c3-127">Você encontrará Olá códigos de país de [códigos de país do Azure CDN](https://msdn.microsoft.com/library/mt761717.aspx).</span><span class="sxs-lookup"><span data-stu-id="723c3-127">You will find hello country codes in [Azure CDN  Country Codes](https://msdn.microsoft.com/library/mt761717.aspx).</span></span> 

## <span data-ttu-id="723c3-128"><a id="considerations"></a>Considerações</span><span class="sxs-lookup"><span data-stu-id="723c3-128"><a id="considerations"></a>Considerations</span></span>
* <span data-ttu-id="723c3-129">Pode levar até too90 minutos Verizon ou alguns minutos com Akamai, para efeito de tootake do alterações tooyour país filtragem configuração.</span><span class="sxs-lookup"><span data-stu-id="723c3-129">It may take up too90 minutes for Verizon, or a couple minutes with Akamai, for changes tooyour country filtering configuration tootake effect.</span></span>
* <span data-ttu-id="723c3-130">Esse recurso não oferece suporte a caracteres curinga (por exemplo, ‘*’).</span><span class="sxs-lookup"><span data-stu-id="723c3-130">This feature does not support wildcard characters (for example, ‘*’).</span></span>
* <span data-ttu-id="723c3-131">configuração de filtragem geográfica Olá associada com o caminho relativo da saudação será aplicadas recursivamente toothat caminho.</span><span class="sxs-lookup"><span data-stu-id="723c3-131">hello geo-filtering configuration associated with hello relative path will be applied recursively toothat path.</span></span>
* <span data-ttu-id="723c3-132">Somente uma regra pode ser aplicada toohello mesmo caminho relativo (não é possível criar vários filtros de país que toohello ponto mesmo caminho relativo.</span><span class="sxs-lookup"><span data-stu-id="723c3-132">Only one rule can be applied toohello same relative path (you cannot create multiple country filters that point toohello same relative path.</span></span> <span data-ttu-id="723c3-133">No entanto, uma pasta pode ter vários filtros de país.</span><span class="sxs-lookup"><span data-stu-id="723c3-133">However, a folder may have multiple country filters.</span></span> <span data-ttu-id="723c3-134">Isso é devido a natureza de recursiva toohello de filtros de país.</span><span class="sxs-lookup"><span data-stu-id="723c3-134">This is due toohello recursive nature of country filters.</span></span> <span data-ttu-id="723c3-135">Em outras palavras, uma subpasta de uma pasta configurada anteriormente pode ter um filtro de país diferente atribuído.</span><span class="sxs-lookup"><span data-stu-id="723c3-135">In other words, a subfolder of a previously configured folder can be assigned a different country filter.</span></span>

