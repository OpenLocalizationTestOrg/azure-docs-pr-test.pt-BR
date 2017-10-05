---
title: "Conectores de Proxy de aplicativo do portal clássico do Azure AD | Microsoft Docs"
description: Aborda como criar e gerenciar grupos de conectores no Proxy de Aplicativo do Azure AD.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b283796a-9679-4c79-b703-802bb850f65d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: fc65c4053c45d9c16c62ee0fe65924133a4bb94a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a><span data-ttu-id="3e007-103">Publicar aplicativos em redes e locais separados usando grupos de conectores</span><span class="sxs-lookup"><span data-stu-id="3e007-103">Publish applications on separate networks and locations using connector groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3e007-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3e007-104">Azure portal</span></span>](active-directory-application-proxy-connectors-azure-portal.md)
> * [<span data-ttu-id="3e007-105">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="3e007-105">Azure classic portal</span></span>](active-directory-application-proxy-connectors.md)
>
>

<span data-ttu-id="3e007-106">Os grupos de conectores são úteis para diversos cenários, incluindo:</span><span class="sxs-lookup"><span data-stu-id="3e007-106">Connector groups are useful for various scenarios, including:</span></span>

* <span data-ttu-id="3e007-107">Sites com vários datacenters interconectados.</span><span class="sxs-lookup"><span data-stu-id="3e007-107">Sites with multiple interconnected datacenters.</span></span> <span data-ttu-id="3e007-108">Nesses casos, você deseja manter o tráfego dentro do datacenter o máximo possível, porque links entre datacenters são caros e lentos.</span><span class="sxs-lookup"><span data-stu-id="3e007-108">In this case, you want to keep as much traffic within the datacenter as possible because cross-datacenter links are expensive and slow.</span></span> <span data-ttu-id="3e007-109">Você pode implantar conectores em cada datacenter para servir apenas os aplicativos que residem dentro do datacenter.</span><span class="sxs-lookup"><span data-stu-id="3e007-109">You can deploy connectors in each datacenter to serve only the applications that reside within the datacenter.</span></span> <span data-ttu-id="3e007-110">Essa abordagem minimiza os links entre datacenters e fornece uma experiência totalmente transparente para os usuários.</span><span class="sxs-lookup"><span data-stu-id="3e007-110">This approach minimizes cross-datacenter links and provides an entirely transparent experience to your users.</span></span>
* <span data-ttu-id="3e007-111">Gerenciar aplicativos instalados em redes isoladas que não fazem parte da rede corporativa principal.</span><span class="sxs-lookup"><span data-stu-id="3e007-111">Managing applications installed on isolated networks that are not part of the main corporate network.</span></span> <span data-ttu-id="3e007-112">Você pode usar grupos de conectores para instalar conectores dedicados em redes isoladas para isolar também os aplicativos para a rede.</span><span class="sxs-lookup"><span data-stu-id="3e007-112">You can use connector groups to install dedicated connectors on isolated networks to also isolate applications to the network.</span></span>
* <span data-ttu-id="3e007-113">Para aplicativos instalados no IaaS para acesso à nuvem, os grupos de conector fornecem um serviço comum para proteger o acesso a todos os aplicativos.</span><span class="sxs-lookup"><span data-stu-id="3e007-113">For applications installed on IaaS for cloud access, connector groups provide a common service to secure the access to all the apps.</span></span> <span data-ttu-id="3e007-114">Os grupos de conectores não criam dependência adicional em sua rede corporativa nem fragmentam a experiência de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3e007-114">Connector groups don't create additional dependency on your corporate network, or fragment the app experience.</span></span> <span data-ttu-id="3e007-115">Conectores podem ser instalados em cada datacenter na nuvem e servir apenas os aplicativos que residem nessa rede.</span><span class="sxs-lookup"><span data-stu-id="3e007-115">Connectors can be installed on every cloud datacenter and serve only applications that reside in this network.</span></span> <span data-ttu-id="3e007-116">Você pode instalar vários conectores para obter alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="3e007-116">You can install several connectors to achieve high availability.</span></span>
* <span data-ttu-id="3e007-117">Suporte para ambientes de várias florestas em que conectores específicos podem ser implantados por floresta e definidos para servir aplicativos específicos.</span><span class="sxs-lookup"><span data-stu-id="3e007-117">Support for multi-forest environments in which specific connectors can be deployed per forest and set to serve specific applications.</span></span>
* <span data-ttu-id="3e007-118">Grupos de Conectores podem ser usados em sites de Recuperação de desastres para detectar failover ou como backup do site principal.</span><span class="sxs-lookup"><span data-stu-id="3e007-118">Connector groups can be used in Disaster Recovery sites to either detect failover or as backup for the main site.</span></span>
* <span data-ttu-id="3e007-119">Grupos de Conectores também podem ser usados para atender a várias empresas de um único locatário.</span><span class="sxs-lookup"><span data-stu-id="3e007-119">Connector groups can also be used to serve multiple companies from a single tenant.</span></span>

## <a name="prerequisite-create-your-connectors"></a><span data-ttu-id="3e007-120">Pré-requisito: criar seus conectores</span><span class="sxs-lookup"><span data-stu-id="3e007-120">Prerequisite: Create your connectors</span></span>
<span data-ttu-id="3e007-121">Para agrupar seus conectores, [instale vários conectores](active-directory-application-proxy-enable.md), nomeie e os agrupe.</span><span class="sxs-lookup"><span data-stu-id="3e007-121">To group your connectors, [install multiple connectors](active-directory-application-proxy-enable.md), then name and group them.</span></span> <span data-ttu-id="3e007-122">Por fim, você precisa atribuí-los a aplicativos específicos.</span><span class="sxs-lookup"><span data-stu-id="3e007-122">Finally you have to assign them to specific apps.</span></span>

## <a name="step-1-create-connector-groups"></a><span data-ttu-id="3e007-123">Etapa 1: Criar grupos de conectores</span><span class="sxs-lookup"><span data-stu-id="3e007-123">Step 1: Create connector groups</span></span>
<span data-ttu-id="3e007-124">Você pode criar quantos grupos de conectores desejar.</span><span class="sxs-lookup"><span data-stu-id="3e007-124">You can create as many connector groups as you want.</span></span> <span data-ttu-id="3e007-125">A criação de grupo de Conectores é feita no portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="3e007-125">Connector group creation is accomplished in the Azure classic portal.</span></span>

1. <span data-ttu-id="3e007-126">Escolha o diretório e clique em **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="3e007-126">Select your directory and click **Configure**.</span></span>  
    <span data-ttu-id="3e007-127">![Captura de tela da configuração do proxy de aplicativo - clique em gerenciar grupos de conectores](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span><span class="sxs-lookup"><span data-stu-id="3e007-127">![Application proxy, configure screenshot - click manage connector groups](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span></span>
2. <span data-ttu-id="3e007-128">Em Proxy de Aplicativo, clique em **Gerenciar Grupos de Conectores** e crie um grupo de conectores fornecendo um nome ao grupo.</span><span class="sxs-lookup"><span data-stu-id="3e007-128">Under Application Proxy, click **Manage Connector Groups** and create a connector group by giving the group a name.</span></span>  
    <span data-ttu-id="3e007-129">![Captura de tela dos grupos de conectores do proxy de aplicativo - nomeie o novo grupo](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span><span class="sxs-lookup"><span data-stu-id="3e007-129">![Application proxy connector groups screenshot - name new group](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span></span>

## <a name="step-2-assign-connectors-to-your-groups"></a><span data-ttu-id="3e007-130">Etapa 2: Atribuir conectores aos seus grupos</span><span class="sxs-lookup"><span data-stu-id="3e007-130">Step 2: Assign connectors to your groups</span></span>
<span data-ttu-id="3e007-131">Após a criação dos grupos de conectores, mova os conectores para o grupo apropriado.</span><span class="sxs-lookup"><span data-stu-id="3e007-131">Once the connector groups are created, move the connectors to the appropriate group.</span></span>

1. <span data-ttu-id="3e007-132">Em **Proxy de Aplicativo**, clique em **Gerenciar Conectores**.</span><span class="sxs-lookup"><span data-stu-id="3e007-132">Under **Application Proxy**, click **Manage Connectors**.</span></span>
2. <span data-ttu-id="3e007-133">Em **Grupo**, escolha o grupo desejado para cada conector.</span><span class="sxs-lookup"><span data-stu-id="3e007-133">Under **Group**, select the group you want for each connector.</span></span> <span data-ttu-id="3e007-134">Podem ser necessários até 10 minutos para que os conectores fiquem ativos no novo grupo.</span><span class="sxs-lookup"><span data-stu-id="3e007-134">It might take the connectors up to 10 minutes to become active in the new group.</span></span>  
    <span data-ttu-id="3e007-135">![Captura de tela dos conectores do proxy de aplicativo - selecione o grupo no menu suspenso](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span><span class="sxs-lookup"><span data-stu-id="3e007-135">![Application proxy connectors screenshot - select group from dropdown menu](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span></span>

## <a name="step-3-assign-applications-to-your-connector-groups"></a><span data-ttu-id="3e007-136">Etapa 3: Atribuir aplicativos aos grupos de conectores</span><span class="sxs-lookup"><span data-stu-id="3e007-136">Step 3: Assign applications to your connector groups</span></span>
<span data-ttu-id="3e007-137">A última etapa é atribuir cada aplicativo ao grupo de conectores que o atende.</span><span class="sxs-lookup"><span data-stu-id="3e007-137">The last step is to set each application to the connector group that serves it.</span></span>

1. <span data-ttu-id="3e007-138">No Portal Clássico do Azure, no seu diretório, escolha o Aplicativo que você deseja atribuir ao grupo e clique em **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="3e007-138">In the Azure classic portal, in your directory, select the Application you want to assign to the group and click **Configure**.</span></span>
2. <span data-ttu-id="3e007-139">Em **Grupo de conectores**, selecione o grupo que deseja usar.</span><span class="sxs-lookup"><span data-stu-id="3e007-139">Under **Connector group**, select the group you want the application to use.</span></span> <span data-ttu-id="3e007-140">A alteração é aplicada imediatamente.</span><span class="sxs-lookup"><span data-stu-id="3e007-140">This change is immediately applied.</span></span>  
    <span data-ttu-id="3e007-141">![Captura de tela do grupo de conectores do proxy de aplicativo - selecione o grupo no menu suspenso](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span><span class="sxs-lookup"><span data-stu-id="3e007-141">![Application proxy connector group screenshot - select group from dropdown menu](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span></span>

## <a name="see-also"></a><span data-ttu-id="3e007-142">Confira também</span><span class="sxs-lookup"><span data-stu-id="3e007-142">See also</span></span>
* [<span data-ttu-id="3e007-143">Habilitar Proxy de aplicativo</span><span class="sxs-lookup"><span data-stu-id="3e007-143">Enable Application Proxy</span></span>](active-directory-application-proxy-enable.md)
* [<span data-ttu-id="3e007-144">Habilitar o logon único</span><span class="sxs-lookup"><span data-stu-id="3e007-144">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="3e007-145">Habilitar o acesso condicional</span><span class="sxs-lookup"><span data-stu-id="3e007-145">Enable conditional access</span></span>](active-directory-application-proxy-conditional-access.md)
* [<span data-ttu-id="3e007-146">Solucionar problemas que surgirem com o Proxy de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="3e007-146">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)

<span data-ttu-id="3e007-147">Para obter as últimas notícias e atualizações, confira o [blog do Proxy de Aplicativo](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="3e007-147">For the latest news and updates, check out the [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
