---
title: "aaaAzure Active Directory PoC guia estratégico ingredientes | Microsoft Docs"
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
ms.openlocfilehash: 0a7f5cd659b9d62ac86e3c27e5727294d481f4a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-ingredients"></a><span data-ttu-id="7e8a1-104">Ingredientes do guia estratégico de prova de conceito do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7e8a1-104">Azure Active Directory Proof of Concept Playbook Ingredients</span></span> 

## <a name="theme"></a><span data-ttu-id="7e8a1-105">Tema</span><span class="sxs-lookup"><span data-stu-id="7e8a1-105">Theme</span></span>
<span data-ttu-id="7e8a1-106">AD do Azure fornece soluções de identidade e acesso de várias áreas da empresa hello.</span><span class="sxs-lookup"><span data-stu-id="7e8a1-106">Azure AD provides identity and access solutions across multiple areas in hello enterprise.</span></span> <span data-ttu-id="7e8a1-107">Classificamos cenários Olá Olá áreas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7e8a1-107">We classify hello scenarios in hello following areas:</span></span> 

* [<span data-ttu-id="7e8a1-108">Muitos aplicativos, uma identidade</span><span class="sxs-lookup"><span data-stu-id="7e8a1-108">Lots of apps, one identity</span></span>](active-directory-playbook-implementation.md#theme---lots-of-apps-one-identity) 
* [<span data-ttu-id="7e8a1-109">Aumentar sua segurança</span><span class="sxs-lookup"><span data-stu-id="7e8a1-109">Increase your security</span></span>](active-directory-playbook-implementation.md#theme---increase-your-security) 
* [<span data-ttu-id="7e8a1-110">Dimensionar com autoatendimento</span><span class="sxs-lookup"><span data-stu-id="7e8a1-110">Scale with Self Service</span></span>](active-directory-playbook-implementation.md#theme---scale-with-self-service) 

<span data-ttu-id="7e8a1-111">Definir um tema tooframe Olá PoC ajuda esforços de saudação toofocus que reflete os desejos com as metas de negócios, que são muitas vezes, os gatilhos de Olá de interesse de saudação em uma verificação de conceito em primeiro lugar de saudação.</span><span class="sxs-lookup"><span data-stu-id="7e8a1-111">Defining a theme tooframe hello PoC helps toofocus hello efforts that resonates with business goals, which oftentimes are hello triggers of hello interest in a proof of concept in hello first place.</span></span> 

## <a name="environment"></a><span data-ttu-id="7e8a1-112">Ambiente</span><span class="sxs-lookup"><span data-stu-id="7e8a1-112">Environment</span></span>

<span data-ttu-id="7e8a1-113">É toodetermine importante detalhes de saudação do ambiente Olá onde você fornecerá Olá PoC.</span><span class="sxs-lookup"><span data-stu-id="7e8a1-113">It is important toodetermine hello details of hello environment where you will deliver hello PoC.</span></span> <span data-ttu-id="7e8a1-114">Idealmente, você pode criar após ele depois Olá que POC é concluída.</span><span class="sxs-lookup"><span data-stu-id="7e8a1-114">Ideally you can build upon it after hello PoC is completed.</span></span> <span data-ttu-id="7e8a1-115">ambiente de destino Olá é crucial, e você deve encontrar o equilíbrio correto de saudação entre tornar a ele como real possível e sobrecarga de saudação de restrições ou considerações adicionais.</span><span class="sxs-lookup"><span data-stu-id="7e8a1-115">hello target environment is crucial and you should find hello right balance between making it as real as possible and hello overhead of constraints or extra considerations.</span></span> <span data-ttu-id="7e8a1-116">saudação de ambientes típicos para PoCs é:</span><span class="sxs-lookup"><span data-stu-id="7e8a1-116">hello typical environments for PoCs are:</span></span>
* <span data-ttu-id="7e8a1-117">**Produção:** cenários Olá serão implementados em seu ambiente em tempo real e já implantado os serviços do Microsoft Cloud (produção AD, Office 365, solução SSO/locatário do AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="7e8a1-117">**Production:** hello scenarios will be implemented in your live environment and already deployed Microsoft Cloud services (production AD, Office 365, Azure AD tenant/SSO solution).</span></span> 
* <span data-ttu-id="7e8a1-118">**Ambiente UAT (Teste de Aceitação do Usuário)/de desenvolvimento:** você tem uma infraestrutura de teste (AD paralelo e eventualmente a solução SSO/locatário do Azure AD) que tem dados de teste que se assemelham à produção.</span><span class="sxs-lookup"><span data-stu-id="7e8a1-118">**User Acceptance Test (UAT)/Dev environment:** You have test infrastructure (parallel AD and potentially Azure AD tenant/SSO solution) with test data that resembles production.</span></span> <span data-ttu-id="7e8a1-119">Normalmente, o ambiente de teste Olá é compartilhado entre vários projetos na empresa hello.</span><span class="sxs-lookup"><span data-stu-id="7e8a1-119">Typically, hello test environment is shared across multiple projects in hello enterprise.</span></span>

<span data-ttu-id="7e8a1-120">A maioria dos cenários deste guia são aditivos por natureza.</span><span class="sxs-lookup"><span data-stu-id="7e8a1-120">Most scenarios in this guide are additive in nature.</span></span> <span data-ttu-id="7e8a1-121">Como resultado, ele podem ser implantados em locatário de produção de hello sem afetar os usuários fora da saudação PoC.</span><span class="sxs-lookup"><span data-stu-id="7e8a1-121">As a result, they can be deployed in hello production tenant without affecting users outside hello PoC.</span></span> <span data-ttu-id="7e8a1-122">Ao longo deste documento, mencionaremos quais cenários teriam efeito em todo o locatário.</span><span class="sxs-lookup"><span data-stu-id="7e8a1-122">Throughout this document, we will be calling out which scenarios would have tenant-wide effect.</span></span> <span data-ttu-id="7e8a1-123">Nesses casos, convém tooconsider um ambiente de não produção.</span><span class="sxs-lookup"><span data-stu-id="7e8a1-123">In those cases, you might want tooconsider a non-production environment.</span></span> 


## <a name="target-users"></a><span data-ttu-id="7e8a1-124">Usuários de destino</span><span class="sxs-lookup"><span data-stu-id="7e8a1-124">Target Users</span></span>

<span data-ttu-id="7e8a1-125">É importante toodetermine Olá destino conjunto de usuários que usará cenários hello, especialmente quando o ambiente de saudação for produção ou teste.</span><span class="sxs-lookup"><span data-stu-id="7e8a1-125">It is important toodetermine hello target set of users that will exercise hello scenarios, especially when hello environment is production or test.</span></span> <span data-ttu-id="7e8a1-126">Olá categorias de usuários de destino para PoC são:</span><span class="sxs-lookup"><span data-stu-id="7e8a1-126">hello categories of target users for PoC are:</span></span>
* <span data-ttu-id="7e8a1-127">**Os usuários do piloto:** funções de trabalho de usuários reais no ambiente de saudação que vai usar solução Olá com conta Olá usam para seu tooday dia</span><span class="sxs-lookup"><span data-stu-id="7e8a1-127">**Pilot Users:** Real users in hello environment that will be using hello solution with hello account they use for their day tooday job functions</span></span>
* <span data-ttu-id="7e8a1-128">**Usuários de teste:** criadas no ambiente de saudação de contas de teste</span><span class="sxs-lookup"><span data-stu-id="7e8a1-128">**Test Users:** Test accounts created in hello environment</span></span> 

<span data-ttu-id="7e8a1-129">A maioria dos cenários neste guia pode ser exercida por usuários piloto.</span><span class="sxs-lookup"><span data-stu-id="7e8a1-129">Most scenarios in this guide can be exercised by pilot users.</span></span> <span data-ttu-id="7e8a1-130">Ao longo deste documento, mencionaremos considerações do usuário de destino, se necessário.</span><span class="sxs-lookup"><span data-stu-id="7e8a1-130">Throughout this document, we will be calling out target user considerations if needed.</span></span>


[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]