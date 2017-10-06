---
title: "aaaAzure Active Directory PoC guia estratégico Introdução | Microsoft Docs"
description: "Explorar e implementar rapidamente os cenários de Identidade e Gerenciamento de Acesso"
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
ms.openlocfilehash: 655524e9692de46e831fc68e1636e6c20d41958f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-introduction"></a><span data-ttu-id="04a29-104">Guia estratégico de prova de conceito do Azure Active Directory: introdução</span><span class="sxs-lookup"><span data-stu-id="04a29-104">Azure Active Directory Proof of Concept Playbook: Introduction</span></span>

<span data-ttu-id="04a29-105">Este artigo oferece diretrizes tooexplore AD Azure diferentes recursos em uma verificação de conceito (PoC).</span><span class="sxs-lookup"><span data-stu-id="04a29-105">This article provides guidelines tooexplore different Azure AD capabilities in a Proof of Concept (PoC).</span></span> <span data-ttu-id="04a29-106">Olá pretendido público deste documento é arquitetos de identidade, os profissionais de TI e os integradores de sistema</span><span class="sxs-lookup"><span data-stu-id="04a29-106">hello intended audience of this document is Identity Architects, IT Professionals, and System Integrators</span></span>

## <a name="how-toouse-this-playbook"></a><span data-ttu-id="04a29-107">Como toouse esse guia estratégico</span><span class="sxs-lookup"><span data-stu-id="04a29-107">How toouse this Playbook</span></span>

1. <span data-ttu-id="04a29-108">Saudação de uso [tema](active-directory-playbook-ingredients.md#theme) seção e escolher Olá area(s) de interesse com base em suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="04a29-108">Use hello [Theme](active-directory-playbook-ingredients.md#theme) section and pick hello area(s) of interest based on your needs.</span></span>  
2. <span data-ttu-id="04a29-109">Saudação de escopo PoC escolhendo os cenários de saudação que se alinham com suas metas de negócios.</span><span class="sxs-lookup"><span data-stu-id="04a29-109">Scope hello PoC by choosing hello scenarios that align with your business goals.</span></span> <span data-ttu-id="04a29-110">Olá menor hello melhor.</span><span class="sxs-lookup"><span data-stu-id="04a29-110">hello shorter hello better.</span></span> <span data-ttu-id="04a29-111">É recomendável fazê-lo como curto e Olá concisa como valor de saudação tooconvey possíveis participantes toohello, minimizando a complexidade toorealize-lo.</span><span class="sxs-lookup"><span data-stu-id="04a29-111">We recommend doing it as short and concise as possible tooconvey hello value toohello stakeholders while minimizing hello complexity toorealize it.</span></span>  
3. <span data-ttu-id="04a29-112">Saudação de uso [implementação](active-directory-playbook-implementation.md) cenários de saudação toounderstand seção e o que seriam significam para o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="04a29-112">Use hello [Implementation](active-directory-playbook-implementation.md) section toounderstand hello scenarios, and what would they mean for your environment.</span></span> <span data-ttu-id="04a29-113">Em cada cenário, descreveremos como tooset-o (o que chamamos [blocos de construção](active-directory-playbook-building-blocks.md)), e como toonavigate Olá cenários.</span><span class="sxs-lookup"><span data-stu-id="04a29-113">In each scenario, we describe how tooset it up (what we call [Building Blocks](active-directory-playbook-building-blocks.md)), and how toonavigate hello scenarios.</span></span> 
4. <span data-ttu-id="04a29-114">Cada bloco de construção explica Olá os pré-requisitos necessários, bem como uma toocomplete de tempo aproximado.</span><span class="sxs-lookup"><span data-stu-id="04a29-114">Each building block explains hello pre-requisites needed, as well as an approximate time toocomplete.</span></span> <span data-ttu-id="04a29-115">Isso pode ajudá-lo durante o processo de planejamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="04a29-115">This can help you during hello planning process.</span></span> 
5. <span data-ttu-id="04a29-116">Com base em 1 a 3 acima, definir Olá [ambiente](active-directory-playbook-ingredients.md#environment) no qual tooexecute.</span><span class="sxs-lookup"><span data-stu-id="04a29-116">Based on 1-3 Above, define hello [Environment](active-directory-playbook-ingredients.md#environment) in which tooexecute.</span></span> <span data-ttu-id="04a29-117">Nós o incentivamos toostrive para um ambiente de produção tooget uma boa noção da experiência de saudação para seus usuários.</span><span class="sxs-lookup"><span data-stu-id="04a29-117">We encourage toostrive for a production environment tooget a good feel of hello experience for your users.</span></span> 
6. <span data-ttu-id="04a29-118">Quando houver requisitos conflitantes, use essa matriz de compensação útil</span><span class="sxs-lookup"><span data-stu-id="04a29-118">When having conflicting requirements, use this helpful tradeoff matrix</span></span> 
   * <span data-ttu-id="04a29-119">Exibição centrada no tema do valor</span><span class="sxs-lookup"><span data-stu-id="04a29-119">Theme-centric showing of value</span></span>  
   * <span data-ttu-id="04a29-120">Cenários de suavidade tooprepare tooset backup e tooexecute Olá</span><span class="sxs-lookup"><span data-stu-id="04a29-120">Smoothness tooprepare, tooset up, and tooexecute hello scenarios</span></span> 
   * <span data-ttu-id="04a29-121">Cenários de destino do tempo mínimo tooexecute Olá</span><span class="sxs-lookup"><span data-stu-id="04a29-121">Minimal time tooexecute hello target scenarios</span></span> 
   * <span data-ttu-id="04a29-122">Como fechar tooproduction como viável dentro de suas restrições</span><span class="sxs-lookup"><span data-stu-id="04a29-122">As close tooproduction as feasible within your constraints</span></span> 

>[!NOTE]
> <span data-ttu-id="04a29-123">Ao longo deste artigo, você verá alguns aplicativos e produtos de terceiros específicos mencionados como exemplos para sua conveniência.</span><span class="sxs-lookup"><span data-stu-id="04a29-123">Throughout this article, you will see some specific third party applications and products mentioned as examples for convenience.</span></span> <span data-ttu-id="04a29-124">O Azure AD dá suporte a milhares de aplicativos em nossa [galeria de aplicativos](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) que pode ser usada com base em suas necessidades e no seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="04a29-124">Azure AD supports thousands of applications in our [application gallery](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) that you can use based on your needs and environment.</span></span> 



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]