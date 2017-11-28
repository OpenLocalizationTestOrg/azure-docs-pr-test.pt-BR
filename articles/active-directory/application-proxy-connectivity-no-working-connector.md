---
title: grupo de conector aaaNo trabalho encontrado para um aplicativo de Proxy de aplicativo | Microsoft Docs
description: "Solucionar problemas que podem ocorrer quando não há nenhum trabalho conector em um grupo de conector para seu aplicativo com hello Proxy de aplicativo do Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4c4baf296b316db131929c9a7c618fb9960713e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a><span data-ttu-id="c4acd-103">Nenhum grupo do conector de trabalho encontrado para um aplicativo de Application Proxy</span><span class="sxs-lookup"><span data-stu-id="c4acd-103">No working connector group found for an Application Proxy application</span></span>

<span data-ttu-id="c4acd-104">Ajuda neste artigo você tooresolve Olá comuns dos problemas enfrentados quando não há um conector detectado para um aplicativo de Proxy de aplicativo integrado ao Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4acd-104">This article help you tooresolve hello common issues faced when there is not a connector detected for an Application Proxy application integrated with Azure Active Directory.</span></span>

## <a name="overview-of-steps"></a><span data-ttu-id="c4acd-105">Visão geral das etapas</span><span class="sxs-lookup"><span data-stu-id="c4acd-105">Overview of steps</span></span>
<span data-ttu-id="c4acd-106">Se não houver nenhum trabalho conector em um grupo de conector para seu aplicativo, há alguns problemas de saudação tooresolve de maneiras:</span><span class="sxs-lookup"><span data-stu-id="c4acd-106">If there is no working Connector in a Connector Group for your application, there are a few ways tooresolve hello problem:</span></span>

-   <span data-ttu-id="c4acd-107">Se você tiver não conectores no grupo hello, você pode:</span><span class="sxs-lookup"><span data-stu-id="c4acd-107">If you have no connectors in hello group, you can:</span></span>

    -   <span data-ttu-id="c4acd-108">Baixar um novo conector no servidor de local certo hello e atribua-toothis grupo</span><span class="sxs-lookup"><span data-stu-id="c4acd-108">Download a new Connector on hello right on-prem server, and assign it toothis group</span></span>

    -   <span data-ttu-id="c4acd-109">Mover um conector para active para grupo de saudação</span><span class="sxs-lookup"><span data-stu-id="c4acd-109">Move an active Connector into hello group</span></span>

-   <span data-ttu-id="c4acd-110">Se você não tiver nenhum conector ativo no grupo de saudação, você pode:</span><span class="sxs-lookup"><span data-stu-id="c4acd-110">If you have no active connectors in hello group, you can:</span></span>

    -   <span data-ttu-id="c4acd-111">Identificar o motivo Olá que seu conector está inativo e resolver</span><span class="sxs-lookup"><span data-stu-id="c4acd-111">Identify hello reason your Connector is inactive and resolve</span></span>

    -   <span data-ttu-id="c4acd-112">Mover um conector para active para grupo de saudação</span><span class="sxs-lookup"><span data-stu-id="c4acd-112">Move an active Connector into hello group</span></span>

<span data-ttu-id="c4acd-113">tooknow qual deles é problema hello, abra o menu de "Proxy de aplicativo" hello em seu aplicativo e examine a mensagem de aviso do grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4acd-113">tooknow which of these is hello issue, open hello “Application Proxy” menu in your Application, and look at hello Connector Group warning message.</span></span> <span data-ttu-id="c4acd-114">Ele especifica esse grupo de saudação precisa de pelo menos um conector (necessário nenhum grupo Olá) ou se ele tem nenhum conector active (embora provavelmente tem conectores inativos).</span><span class="sxs-lookup"><span data-stu-id="c4acd-114">It specify either that hello group needs at least one Connector (you have none in hello group) or that it has no active Connectors (though you likely have inactive Connectors).</span></span>

   ![Seleção de grupo do conector no Portal do Azure](./media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

<span data-ttu-id="c4acd-116">Para obter detalhes sobre cada uma dessas opções, consulte Olá seção correspondente.</span><span class="sxs-lookup"><span data-stu-id="c4acd-116">For details on each of these options, see hello corresponding section below.</span></span> <span data-ttu-id="c4acd-117">Cada uma dessas pressupõe que você esteja iniciando na página de gerenciamento de conector hello.</span><span class="sxs-lookup"><span data-stu-id="c4acd-117">Each of these assumes that you are starting from hello Connector management page.</span></span> <span data-ttu-id="c4acd-118">Se você estiver procurando na mensagem de erro de saudação acima, você pode ir toothis página clicando na mensagem de saudação do aviso.</span><span class="sxs-lookup"><span data-stu-id="c4acd-118">If you are looking at hello error message above, you can go toothis page by clicking on hello warning message.</span></span> <span data-ttu-id="c4acd-119">Caso contrário, isso pode ser encontrado indo muito**Active Directory do Azure**, clicando em **aplicativos empresariais**, em seguida, **Proxy de aplicativo.**</span><span class="sxs-lookup"><span data-stu-id="c4acd-119">Otherwise this can be found by going too**Azure Active Directory**, clicking on **Enterprise Applications**, then **Application Proxy.**</span></span>

   ![Gerenciamento de grupo do conector no Portal do Azure](./media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a><span data-ttu-id="c4acd-121">Baixar um novo conector</span><span class="sxs-lookup"><span data-stu-id="c4acd-121">Download a new Connector</span></span>

<span data-ttu-id="c4acd-122">toodownload um novo conector, use o botão de "Baixar conector" de saudação na parte superior de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4acd-122">toodownload a new Connector, use hello “Download Connector” button at hello top of hello page.</span></span>

<span data-ttu-id="c4acd-123">necessidades de conector de saudação Observação toobe instalado em um computador com o aplicativo de back-end toohello linha direta de visão e geralmente é posicionado no hello mesmo servidor que o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="c4acd-123">note hello Connector needs toobe installed on a machine with direct line of sight toohello backend application, and is typically placed on hello same server as hello application.</span></span> <span data-ttu-id="c4acd-124">Depois de baixar, Olá conector deve aparecer no menu.</span><span class="sxs-lookup"><span data-stu-id="c4acd-124">After downloading, hello Connector should appear in this menu.</span></span> <span data-ttu-id="c4acd-125">Clique Olá conector e use hello "Grupo" suspensa toomake-se de que o grupo correto toohello pertence.</span><span class="sxs-lookup"><span data-stu-id="c4acd-125">click hello Connector, and use hello “Connector Group” drop-down toomake sure it belongs toohello right group.</span></span> <span data-ttu-id="c4acd-126">Salve a alteração de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4acd-126">Save hello change.</span></span>

   ![Baixar o conector de saudação do hello Portal do Azure](./media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a><span data-ttu-id="c4acd-128">Mova um conector ativo</span><span class="sxs-lookup"><span data-stu-id="c4acd-128">Move an Active Connector</span></span>

<span data-ttu-id="c4acd-129">Se você tiver um conector para active que deve pertencer toohello grupo e tem o aplicativo de back-end de destino de toohello de linha de visão, você pode mover Olá conector no grupo Olá atribuído.</span><span class="sxs-lookup"><span data-stu-id="c4acd-129">If you have an active Connector that should belong toohello group and has line of sight toohello target backend application, you can move hello Connector into hello assigned group.</span></span> <span data-ttu-id="c4acd-130">toodo, clique em Olá conector.</span><span class="sxs-lookup"><span data-stu-id="c4acd-130">toodo so, click hello Connector.</span></span> <span data-ttu-id="c4acd-131">No campo de "Grupo" Olá, usar grupo correto do Olá Olá tooselect da lista suspensa e clique em Salvar.</span><span class="sxs-lookup"><span data-stu-id="c4acd-131">In hello “Connector Group” field, use hello drop-down tooselect hello correct group, and click Save.</span></span>

## <a name="resolve-an-inactive-connector"></a><span data-ttu-id="c4acd-132">Resolver um conector inativo</span><span class="sxs-lookup"><span data-stu-id="c4acd-132">Resolve an inactive Connector</span></span>

<span data-ttu-id="c4acd-133">Se hello somente conectores no grupo Olá estejam inativos, é provável que eles em um computador que não tenham todas as portas necessárias de saudação desbloqueado.</span><span class="sxs-lookup"><span data-stu-id="c4acd-133">If hello only Connectors in hello group are inactive, they are likely on a machine that does not have all hello necessary ports unblocked.</span></span>

<span data-ttu-id="c4acd-134">Consulte portas Olá documento de solução de problemas para obter detalhes sobre como investigar o problema.</span><span class="sxs-lookup"><span data-stu-id="c4acd-134">see hello ports Troubleshoot document for details on investigating this problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4acd-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c4acd-135">Next steps</span></span>
[<span data-ttu-id="c4acd-136">Noções básicas sobre conectores de Proxy de Aplicativo do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4acd-136">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)


