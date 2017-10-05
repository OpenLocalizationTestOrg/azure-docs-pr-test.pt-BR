---
title: Nenhum grupo do conector de trabalho encontrado para um aplicativo de Application Proxy | Microsoft Docs
description: "Solucionar problemas que podem ocorrer quando não há nenhum trabalho conector em um grupo de conector para seu aplicativo com o Application Proxy do Azure AD"
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
ms.openlocfilehash: 4945958deedc8a1d9989ff901192c03a5363b4dc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a><span data-ttu-id="9576e-103">Nenhum grupo do conector de trabalho encontrado para um aplicativo de Application Proxy</span><span class="sxs-lookup"><span data-stu-id="9576e-103">No working connector group found for an Application Proxy application</span></span>

<span data-ttu-id="9576e-104">Ajuda neste artigo você resolver os problemas mais comuns enfrentados quando não há um conector detectado para um aplicativo de Application Proxy integrado ao Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9576e-104">This article help you to resolve the common issues faced when there is not a connector detected for an Application Proxy application integrated with Azure Active Directory.</span></span>

## <a name="overview-of-steps"></a><span data-ttu-id="9576e-105">Visão geral das etapas</span><span class="sxs-lookup"><span data-stu-id="9576e-105">Overview of steps</span></span>
<span data-ttu-id="9576e-106">Se não houver nenhum conector funcionando em um grupo de conector para o seu aplicativo, haverá algumas maneiras de resolver o problema:</span><span class="sxs-lookup"><span data-stu-id="9576e-106">If there is no working Connector in a Connector Group for your application, there are a few ways to resolve the problem:</span></span>

-   <span data-ttu-id="9576e-107">Se você tiver não conectores no grupo, você poderá:</span><span class="sxs-lookup"><span data-stu-id="9576e-107">If you have no connectors in the group, you can:</span></span>

    -   <span data-ttu-id="9576e-108">Baixar um novo conector no servidor local certo e atribuí-lo a esse grupo</span><span class="sxs-lookup"><span data-stu-id="9576e-108">Download a new Connector on the right on-prem server, and assign it to this group</span></span>

    -   <span data-ttu-id="9576e-109">Mover um conector ativo para o grupo</span><span class="sxs-lookup"><span data-stu-id="9576e-109">Move an active Connector into the group</span></span>

-   <span data-ttu-id="9576e-110">Se você não tiver conectores ativos no grupo, você poderá:</span><span class="sxs-lookup"><span data-stu-id="9576e-110">If you have no active connectors in the group, you can:</span></span>

    -   <span data-ttu-id="9576e-111">Identificar o motivo pelo qual que o conector está inativo e resolver</span><span class="sxs-lookup"><span data-stu-id="9576e-111">Identify the reason your Connector is inactive and resolve</span></span>

    -   <span data-ttu-id="9576e-112">Mover um conector ativo para o grupo</span><span class="sxs-lookup"><span data-stu-id="9576e-112">Move an active Connector into the group</span></span>

<span data-ttu-id="9576e-113">Para saber qual é o problema, abra o menu "Application Proxy" no seu aplicativo e examine a mensagem de aviso do grupo de conector.</span><span class="sxs-lookup"><span data-stu-id="9576e-113">To know which of these is the issue, open the “Application Proxy” menu in your Application, and look at the Connector Group warning message.</span></span> <span data-ttu-id="9576e-114">Ela especifica que o grupo precisa de, pelo menos, um conector (você não tem nenhum no grupo) ou que não tem nenhum conector ativo (embora provavelmente tenha conectores inativos).</span><span class="sxs-lookup"><span data-stu-id="9576e-114">It specify either that the group needs at least one Connector (you have none in the group) or that it has no active Connectors (though you likely have inactive Connectors).</span></span>

   ![Seleção de grupo do conector no Portal do Azure](./media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

<span data-ttu-id="9576e-116">Para obter detalhes sobre cada uma dessas opções, consulte a seção correspondente abaixo.</span><span class="sxs-lookup"><span data-stu-id="9576e-116">For details on each of these options, see the corresponding section below.</span></span> <span data-ttu-id="9576e-117">Cada um desses pressupõe que você está começando na página de gerenciamento de conector.</span><span class="sxs-lookup"><span data-stu-id="9576e-117">Each of these assumes that you are starting from the Connector management page.</span></span> <span data-ttu-id="9576e-118">Se você estiver procurando a mensagem de erro acima, você poderá ir para essa página clicando na mensagem de aviso.</span><span class="sxs-lookup"><span data-stu-id="9576e-118">If you are looking at the error message above, you can go to this page by clicking on the warning message.</span></span> <span data-ttu-id="9576e-119">Caso contrário, isso pode ser encontrado visitando **Azure Active Directory**, clicando em **aplicativos empresariais**, em seguida, **Application Proxy.**</span><span class="sxs-lookup"><span data-stu-id="9576e-119">Otherwise this can be found by going to **Azure Active Directory**, clicking on **Enterprise Applications**, then **Application Proxy.**</span></span>

   ![Gerenciamento de grupo do conector no Portal do Azure](./media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a><span data-ttu-id="9576e-121">Baixar um novo conector</span><span class="sxs-lookup"><span data-stu-id="9576e-121">Download a new Connector</span></span>

<span data-ttu-id="9576e-122">Para baixar um novo conector, use o botão "Baixar conector" na parte superior da página.</span><span class="sxs-lookup"><span data-stu-id="9576e-122">To download a new Connector, use the “Download Connector” button at the top of the page.</span></span>

<span data-ttu-id="9576e-123">observe que o conector deve ser instalado em um computador com a linha direta de visão para o aplicativo de back-end e normalmente é colocado no mesmo servidor que o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9576e-123">note the Connector needs to be installed on a machine with direct line of sight to the backend application, and is typically placed on the same server as the application.</span></span> <span data-ttu-id="9576e-124">Após o download, o conector deve aparecer no menu.</span><span class="sxs-lookup"><span data-stu-id="9576e-124">After downloading, the Connector should appear in this menu.</span></span> <span data-ttu-id="9576e-125">Clique no conector e use a lista suspensa "Grupo do Conector" para certificar-se de que ele pertence ao grupo direito.</span><span class="sxs-lookup"><span data-stu-id="9576e-125">click the Connector, and use the “Connector Group” drop-down to make sure it belongs to the right group.</span></span> <span data-ttu-id="9576e-126">Salve a alteração.</span><span class="sxs-lookup"><span data-stu-id="9576e-126">Save the change.</span></span>

   ![Baixe o conector do Portal do Azure](./media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a><span data-ttu-id="9576e-128">Mova um conector ativo</span><span class="sxs-lookup"><span data-stu-id="9576e-128">Move an Active Connector</span></span>

<span data-ttu-id="9576e-129">Se você tiver um conector ativo que deve pertencer ao grupo e tem metas claras para o aplicativo de back-end de destino, você poderá mover o conector para o grupo atribuído.</span><span class="sxs-lookup"><span data-stu-id="9576e-129">If you have an active Connector that should belong to the group and has line of sight to the target backend application, you can move the Connector into the assigned group.</span></span> <span data-ttu-id="9576e-130">Para fazer isso, clique no conector.</span><span class="sxs-lookup"><span data-stu-id="9576e-130">To do so, click the Connector.</span></span> <span data-ttu-id="9576e-131">No campo "Conector de grupo", use a lista suspensa para selecionar o grupo correto e clique em Salvar.</span><span class="sxs-lookup"><span data-stu-id="9576e-131">In the “Connector Group” field, use the drop-down to select the correct group, and click Save.</span></span>

## <a name="resolve-an-inactive-connector"></a><span data-ttu-id="9576e-132">Resolver um conector inativo</span><span class="sxs-lookup"><span data-stu-id="9576e-132">Resolve an inactive Connector</span></span>

<span data-ttu-id="9576e-133">Se os conectores apenas no grupo estão inativos, eles estão provavelmente em um computador que não tem todas as portas desbloqueadas.</span><span class="sxs-lookup"><span data-stu-id="9576e-133">If the only Connectors in the group are inactive, they are likely on a machine that does not have all the necessary ports unblocked.</span></span>

<span data-ttu-id="9576e-134">consulte o documento de resolução de problemas das portas para obter detalhes sobre como investigar esse problema.</span><span class="sxs-lookup"><span data-stu-id="9576e-134">see the ports Troubleshoot document for details on investigating this problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9576e-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9576e-135">Next steps</span></span>
[<span data-ttu-id="9576e-136">Noções básicas sobre conectores de Proxy de Aplicativo do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9576e-136">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)


