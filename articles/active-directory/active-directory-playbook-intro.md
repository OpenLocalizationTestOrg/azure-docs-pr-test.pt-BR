---
title: "Introdução à cartilha do PoC do Azure Active Directory | Microsoft Docs"
description: "Explorar e implementar rapidamente os cenários de gerenciamento de identidades e acesso"
services: active-directory
keywords: azure active directory, cartilha, prova de conceito, PoC
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: 567f3373594bc53435e8c0bd0a3445dd318af1cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-introduction"></a><span data-ttu-id="9d671-104">Guia estratégico de prova de conceito do Azure Active Directory: introdução</span><span class="sxs-lookup"><span data-stu-id="9d671-104">Azure Active Directory Proof of Concept Playbook: Introduction</span></span>

<span data-ttu-id="9d671-105">Este artigo fornece diretrizes para explorar os diferentes recursos do Azure AD em um PoC (Prova de Conceito).</span><span class="sxs-lookup"><span data-stu-id="9d671-105">This article provides guidelines to explore different Azure AD capabilities in a Proof of Concept (PoC).</span></span> <span data-ttu-id="9d671-106">O público-alvo deste documento são Arquitetos de identidade, profissionais de TI e integradores de sistema</span><span class="sxs-lookup"><span data-stu-id="9d671-106">The intended audience of this document is Identity Architects, IT Professionals, and System Integrators</span></span>

## <a name="how-to-use-this-playbook"></a><span data-ttu-id="9d671-107">Como usar este guia estratégico</span><span class="sxs-lookup"><span data-stu-id="9d671-107">How to use this Playbook</span></span>

1. <span data-ttu-id="9d671-108">Use a seção [Tema](active-directory-playbook-ingredients.md#theme) e escolha as áreas de interesse com base em suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="9d671-108">Use the [Theme](active-directory-playbook-ingredients.md#theme) section and pick the area(s) of interest based on your needs.</span></span>  
2. <span data-ttu-id="9d671-109">Defina o escopo do PoC escolhendo os cenários que se alinham com suas metas de negócios.</span><span class="sxs-lookup"><span data-stu-id="9d671-109">Scope the PoC by choosing the scenarios that align with your business goals.</span></span> <span data-ttu-id="9d671-110">Quanto menor, melhor.</span><span class="sxs-lookup"><span data-stu-id="9d671-110">The shorter the better.</span></span> <span data-ttu-id="9d671-111">É recomendável fazer isso da forma mais curta e concisa possível para transmitir o valor às partes interessadas, minimizando a complexidade para a realização.</span><span class="sxs-lookup"><span data-stu-id="9d671-111">We recommend doing it as short and concise as possible to convey the value to the stakeholders while minimizing the complexity to realize it.</span></span>  
3. <span data-ttu-id="9d671-112">Use a seção [Implementação](active-directory-playbook-implementation.md) para compreender os cenários e o que eles significam para o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="9d671-112">Use the [Implementation](active-directory-playbook-implementation.md) section to understand the scenarios, and what would they mean for your environment.</span></span> <span data-ttu-id="9d671-113">Em cada cenário, descreveremos como configurá-lo (o que chamamos de [Blocos de construção](active-directory-playbook-building-blocks.md)) e como navegar nos cenários.</span><span class="sxs-lookup"><span data-stu-id="9d671-113">In each scenario, we describe how to set it up (what we call [Building Blocks](active-directory-playbook-building-blocks.md)), and how to navigate the scenarios.</span></span> 
4. <span data-ttu-id="9d671-114">Cada bloco de construção explica os pré-requisitos necessários, bem como o tempo aproximado para a conclusão.</span><span class="sxs-lookup"><span data-stu-id="9d671-114">Each building block explains the pre-requisites needed, as well as an approximate time to complete.</span></span> <span data-ttu-id="9d671-115">Isso pode ajudá-lo durante o processo de planejamento.</span><span class="sxs-lookup"><span data-stu-id="9d671-115">This can help you during the planning process.</span></span> 
5. <span data-ttu-id="9d671-116">Com base em 1 a 3 acima, defina o [Ambiente](active-directory-playbook-ingredients.md#environment) no qual executar.</span><span class="sxs-lookup"><span data-stu-id="9d671-116">Based on 1-3 Above, define the [Environment](active-directory-playbook-ingredients.md#environment) in which to execute.</span></span> <span data-ttu-id="9d671-117">Recomendamos procurar um ambiente de produção ter uma boa noção da experiência para seus usuários.</span><span class="sxs-lookup"><span data-stu-id="9d671-117">We encourage to strive for a production environment to get a good feel of the experience for your users.</span></span> 
6. <span data-ttu-id="9d671-118">Quando houver requisitos conflitantes, use essa matriz de compensação útil</span><span class="sxs-lookup"><span data-stu-id="9d671-118">When having conflicting requirements, use this helpful tradeoff matrix</span></span> 
   * <span data-ttu-id="9d671-119">Exibição centrada no tema do valor</span><span class="sxs-lookup"><span data-stu-id="9d671-119">Theme-centric showing of value</span></span>  
   * <span data-ttu-id="9d671-120">Suavidade para preparar, para configurar e para executar os cenários</span><span class="sxs-lookup"><span data-stu-id="9d671-120">Smoothness to prepare, to set up, and to execute the scenarios</span></span> 
   * <span data-ttu-id="9d671-121">Tempo mínimo para executar os cenários de destino</span><span class="sxs-lookup"><span data-stu-id="9d671-121">Minimal time to execute the target scenarios</span></span> 
   * <span data-ttu-id="9d671-122">O mais parecido possível com a produção dentro de suas restrições</span><span class="sxs-lookup"><span data-stu-id="9d671-122">As close to production as feasible within your constraints</span></span> 

>[!NOTE]
> <span data-ttu-id="9d671-123">Ao longo deste artigo, você verá alguns aplicativos e produtos de terceiros específicos mencionados como exemplos para sua conveniência.</span><span class="sxs-lookup"><span data-stu-id="9d671-123">Throughout this article, you will see some specific third party applications and products mentioned as examples for convenience.</span></span> <span data-ttu-id="9d671-124">O Azure AD dá suporte a milhares de aplicativos em nossa [galeria de aplicativos](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) que pode ser usada com base em suas necessidades e no seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="9d671-124">Azure AD supports thousands of applications in our [application gallery](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) that you can use based on your needs and environment.</span></span> 



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]