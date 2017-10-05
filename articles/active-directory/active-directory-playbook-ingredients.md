---
title: Ingredientes da cartilha do PoC do Azure Active Directory | Microsoft Docs
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
ms.openlocfilehash: d2a0fe280f143d390f5e4ba40e0ebe92d8a4a837
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-ingredients"></a><span data-ttu-id="5a9d7-104">Ingredientes do guia estratégico de prova de conceito do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5a9d7-104">Azure Active Directory Proof of Concept Playbook Ingredients</span></span> 

## <a name="theme"></a><span data-ttu-id="5a9d7-105">Tema</span><span class="sxs-lookup"><span data-stu-id="5a9d7-105">Theme</span></span>
<span data-ttu-id="5a9d7-106">O Azure AD fornece soluções de identidade e de acesso em várias áreas da empresa.</span><span class="sxs-lookup"><span data-stu-id="5a9d7-106">Azure AD provides identity and access solutions across multiple areas in the enterprise.</span></span> <span data-ttu-id="5a9d7-107">Classificamos os cenários nas seguintes áreas:</span><span class="sxs-lookup"><span data-stu-id="5a9d7-107">We classify the scenarios in the following areas:</span></span> 

* [<span data-ttu-id="5a9d7-108">Muitos aplicativos, uma identidade</span><span class="sxs-lookup"><span data-stu-id="5a9d7-108">Lots of apps, one identity</span></span>](active-directory-playbook-implementation.md#theme---lots-of-apps-one-identity) 
* [<span data-ttu-id="5a9d7-109">Aumentar sua segurança</span><span class="sxs-lookup"><span data-stu-id="5a9d7-109">Increase your security</span></span>](active-directory-playbook-implementation.md#theme---increase-your-security) 
* [<span data-ttu-id="5a9d7-110">Dimensionar com autoatendimento</span><span class="sxs-lookup"><span data-stu-id="5a9d7-110">Scale with Self Service</span></span>](active-directory-playbook-implementation.md#theme---scale-with-self-service) 

<span data-ttu-id="5a9d7-111">Definir um tema para estruturar o PoC ajuda a concentrar os esforços que ressoam com metas de negócios, que, geralmente, são os gatilhos de interesse em uma prova de conceito em primeiro lugar.</span><span class="sxs-lookup"><span data-stu-id="5a9d7-111">Defining a theme to frame the PoC helps to focus the efforts that resonates with business goals, which oftentimes are the triggers of the interest in a proof of concept in the first place.</span></span> 

## <a name="environment"></a><span data-ttu-id="5a9d7-112">Ambiente</span><span class="sxs-lookup"><span data-stu-id="5a9d7-112">Environment</span></span>

<span data-ttu-id="5a9d7-113">É importante determinar os detalhes do ambiente em que você fornecerá o PoC.</span><span class="sxs-lookup"><span data-stu-id="5a9d7-113">It is important to determine the details of the environment where you will deliver the PoC.</span></span> <span data-ttu-id="5a9d7-114">O ideal será você criar com base nele depois que o PoC for concluído.</span><span class="sxs-lookup"><span data-stu-id="5a9d7-114">Ideally you can build upon it after the PoC is completed.</span></span> <span data-ttu-id="5a9d7-115">O ambiente de destino é fundamental e você deve encontrar o equilíbrio certo entre torná-lo o mais real possível e a sobrecarga de restrições ou considerações adicionais.</span><span class="sxs-lookup"><span data-stu-id="5a9d7-115">The target environment is crucial and you should find the right balance between making it as real as possible and the overhead of constraints or extra considerations.</span></span> <span data-ttu-id="5a9d7-116">Os ambientes típicos para PoCs são:</span><span class="sxs-lookup"><span data-stu-id="5a9d7-116">The typical environments for PoCs are:</span></span>
* <span data-ttu-id="5a9d7-117">**Produção:** os cenários serão implementados em seu ambiente em tempo real e já implantaram os serviços do Microsoft Cloud (AD de produção, Office 365, solução SSO/locatário do Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5a9d7-117">**Production:** The scenarios will be implemented in your live environment and already deployed Microsoft Cloud services (production AD, Office 365, Azure AD tenant/SSO solution).</span></span> 
* <span data-ttu-id="5a9d7-118">**Ambiente UAT (Teste de Aceitação do Usuário)/de desenvolvimento:** você tem uma infraestrutura de teste (AD paralelo e eventualmente a solução SSO/locatário do Azure AD) que tem dados de teste que se assemelham à produção.</span><span class="sxs-lookup"><span data-stu-id="5a9d7-118">**User Acceptance Test (UAT)/Dev environment:** You have test infrastructure (parallel AD and potentially Azure AD tenant/SSO solution) with test data that resembles production.</span></span> <span data-ttu-id="5a9d7-119">Normalmente, o ambiente de teste é compartilhado em vários projetos na empresa.</span><span class="sxs-lookup"><span data-stu-id="5a9d7-119">Typically, the test environment is shared across multiple projects in the enterprise.</span></span>

<span data-ttu-id="5a9d7-120">A maioria dos cenários deste guia são aditivos por natureza.</span><span class="sxs-lookup"><span data-stu-id="5a9d7-120">Most scenarios in this guide are additive in nature.</span></span> <span data-ttu-id="5a9d7-121">Como resultado, eles podem ser implantados no locatário de produção sem afetar os usuários fora do PoC.</span><span class="sxs-lookup"><span data-stu-id="5a9d7-121">As a result, they can be deployed in the production tenant without affecting users outside the PoC.</span></span> <span data-ttu-id="5a9d7-122">Ao longo deste documento, mencionaremos quais cenários teriam efeito em todo o locatário.</span><span class="sxs-lookup"><span data-stu-id="5a9d7-122">Throughout this document, we will be calling out which scenarios would have tenant-wide effect.</span></span> <span data-ttu-id="5a9d7-123">Nesses casos, talvez convenha considerar um ambiente de não produção.</span><span class="sxs-lookup"><span data-stu-id="5a9d7-123">In those cases, you might want to consider a non-production environment.</span></span> 


## <a name="target-users"></a><span data-ttu-id="5a9d7-124">Usuários de destino</span><span class="sxs-lookup"><span data-stu-id="5a9d7-124">Target Users</span></span>

<span data-ttu-id="5a9d7-125">É importante determinar o conjunto de destino de usuários que exercerão os cenários, principalmente quando o ambiente é de produção ou de teste.</span><span class="sxs-lookup"><span data-stu-id="5a9d7-125">It is important to determine the target set of users that will exercise the scenarios, especially when the environment is production or test.</span></span> <span data-ttu-id="5a9d7-126">As categorias de usuários de destino do PoC são:</span><span class="sxs-lookup"><span data-stu-id="5a9d7-126">The categories of target users for PoC are:</span></span>
* <span data-ttu-id="5a9d7-127">**Usuários piloto:** usuários reais no ambiente que usarão a solução com a conta que eles usam para suas funções de trabalho diário</span><span class="sxs-lookup"><span data-stu-id="5a9d7-127">**Pilot Users:** Real users in the environment that will be using the solution with the account they use for their day to day job functions</span></span>
* <span data-ttu-id="5a9d7-128">**Usuários de teste:** contas de teste criadas no ambiente</span><span class="sxs-lookup"><span data-stu-id="5a9d7-128">**Test Users:** Test accounts created in the environment</span></span> 

<span data-ttu-id="5a9d7-129">A maioria dos cenários neste guia pode ser exercida por usuários piloto.</span><span class="sxs-lookup"><span data-stu-id="5a9d7-129">Most scenarios in this guide can be exercised by pilot users.</span></span> <span data-ttu-id="5a9d7-130">Ao longo deste documento, mencionaremos considerações do usuário de destino, se necessário.</span><span class="sxs-lookup"><span data-stu-id="5a9d7-130">Throughout this document, we will be calling out target user considerations if needed.</span></span>


[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]