---
title: conectores de Proxy de aplicativo do AD do Azure portais aaaClassic | Microsoft Docs
description: Aborda como toocreate e gerenciar grupos de conectores no Proxy de aplicativo do Azure AD.
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
ms.openlocfilehash: 43559b0f4ffc3c7dbbf00901e89ac276d01796e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a><span data-ttu-id="204fd-103">Publicar aplicativos em redes e locais separados usando grupos de conectores</span><span class="sxs-lookup"><span data-stu-id="204fd-103">Publish applications on separate networks and locations using connector groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="204fd-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="204fd-104">Azure portal</span></span>](active-directory-application-proxy-connectors-azure-portal.md)
> * [<span data-ttu-id="204fd-105">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="204fd-105">Azure classic portal</span></span>](active-directory-application-proxy-connectors.md)
>
>

<span data-ttu-id="204fd-106">Os grupos de conectores são úteis para diversos cenários, incluindo:</span><span class="sxs-lookup"><span data-stu-id="204fd-106">Connector groups are useful for various scenarios, including:</span></span>

* <span data-ttu-id="204fd-107">Sites com vários datacenters interconectados.</span><span class="sxs-lookup"><span data-stu-id="204fd-107">Sites with multiple interconnected datacenters.</span></span> <span data-ttu-id="204fd-108">Nesse caso, você deseja tookeep como a quantidade de tráfego dentro do datacenter Olá possível porque os links entre data centers são caros e lentos.</span><span class="sxs-lookup"><span data-stu-id="204fd-108">In this case, you want tookeep as much traffic within hello datacenter as possible because cross-datacenter links are expensive and slow.</span></span> <span data-ttu-id="204fd-109">Você pode implantar conectores em cada datacenter tooserve somente Olá aplicativos que residem dentro do datacenter hello.</span><span class="sxs-lookup"><span data-stu-id="204fd-109">You can deploy connectors in each datacenter tooserve only hello applications that reside within hello datacenter.</span></span> <span data-ttu-id="204fd-110">Essa abordagem minimiza os links entre data centers e fornece uma experiência totalmente transparente tooyour usuários.</span><span class="sxs-lookup"><span data-stu-id="204fd-110">This approach minimizes cross-datacenter links and provides an entirely transparent experience tooyour users.</span></span>
* <span data-ttu-id="204fd-111">Gerenciamento de aplicativos instalados em redes isoladas que não fazem parte da rede corporativa principal de saudação.</span><span class="sxs-lookup"><span data-stu-id="204fd-111">Managing applications installed on isolated networks that are not part of hello main corporate network.</span></span> <span data-ttu-id="204fd-112">É possível usar conectores de tooinstall dedicado de grupos de conector em redes isoladas tooalso isolar aplicativos toohello de rede.</span><span class="sxs-lookup"><span data-stu-id="204fd-112">You can use connector groups tooinstall dedicated connectors on isolated networks tooalso isolate applications toohello network.</span></span>
* <span data-ttu-id="204fd-113">Para aplicativos instalados para o acesso à nuvem IaaS, grupos de conector fornecem um comuns toosecure Olá acesso tooall Olá os aplicativos de serviço.</span><span class="sxs-lookup"><span data-stu-id="204fd-113">For applications installed on IaaS for cloud access, connector groups provide a common service toosecure hello access tooall hello apps.</span></span> <span data-ttu-id="204fd-114">Grupos de conector não criar dependências adicionais em sua rede corporativa ou fragmento de experiência de saudação do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="204fd-114">Connector groups don't create additional dependency on your corporate network, or fragment hello app experience.</span></span> <span data-ttu-id="204fd-115">Conectores podem ser instalados em cada datacenter na nuvem e servir apenas os aplicativos que residem nessa rede.</span><span class="sxs-lookup"><span data-stu-id="204fd-115">Connectors can be installed on every cloud datacenter and serve only applications that reside in this network.</span></span> <span data-ttu-id="204fd-116">Você pode instalar vários conectores tooachieve alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="204fd-116">You can install several connectors tooachieve high availability.</span></span>
* <span data-ttu-id="204fd-117">Suporte para ambientes de várias florestas em que os conectores específicos podem ser implantados por floresta e definir aplicativos específicos tooserve.</span><span class="sxs-lookup"><span data-stu-id="204fd-117">Support for multi-forest environments in which specific connectors can be deployed per forest and set tooserve specific applications.</span></span>
* <span data-ttu-id="204fd-118">Grupos de conector podem ser usados em sites de recuperação de desastres tooeither detectar failover ou como backup para Olá principal site.</span><span class="sxs-lookup"><span data-stu-id="204fd-118">Connector groups can be used in Disaster Recovery sites tooeither detect failover or as backup for hello main site.</span></span>
* <span data-ttu-id="204fd-119">Grupos de conector também podem ser usado tooserve várias empresas de um único locatário.</span><span class="sxs-lookup"><span data-stu-id="204fd-119">Connector groups can also be used tooserve multiple companies from a single tenant.</span></span>

## <a name="prerequisite-create-your-connectors"></a><span data-ttu-id="204fd-120">Pré-requisito: criar seus conectores</span><span class="sxs-lookup"><span data-stu-id="204fd-120">Prerequisite: Create your connectors</span></span>
<span data-ttu-id="204fd-121">toogroup seus conectores, [instalar vários conectores](active-directory-application-proxy-enable.md), em seguida, nome e agrupá-los.</span><span class="sxs-lookup"><span data-stu-id="204fd-121">toogroup your connectors, [install multiple connectors](active-directory-application-proxy-enable.md), then name and group them.</span></span> <span data-ttu-id="204fd-122">Finalmente tiver tooassign-los toospecific aplicativos.</span><span class="sxs-lookup"><span data-stu-id="204fd-122">Finally you have tooassign them toospecific apps.</span></span>

## <a name="step-1-create-connector-groups"></a><span data-ttu-id="204fd-123">Etapa 1: Criar grupos de conectores</span><span class="sxs-lookup"><span data-stu-id="204fd-123">Step 1: Create connector groups</span></span>
<span data-ttu-id="204fd-124">Você pode criar quantos grupos de conectores desejar.</span><span class="sxs-lookup"><span data-stu-id="204fd-124">You can create as many connector groups as you want.</span></span> <span data-ttu-id="204fd-125">Criação de grupo do conector é realizada em Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="204fd-125">Connector group creation is accomplished in hello Azure classic portal.</span></span>

1. <span data-ttu-id="204fd-126">Escolha o diretório e clique em **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="204fd-126">Select your directory and click **Configure**.</span></span>  
    <span data-ttu-id="204fd-127">![Captura de tela da configuração do proxy de aplicativo - clique em gerenciar grupos de conectores](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span><span class="sxs-lookup"><span data-stu-id="204fd-127">![Application proxy, configure screenshot - click manage connector groups](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span></span>
2. <span data-ttu-id="204fd-128">Em Proxy de aplicativo, clique em **gerenciar grupos de conector** e criar um grupo, fornecendo um nome de grupo hello.</span><span class="sxs-lookup"><span data-stu-id="204fd-128">Under Application Proxy, click **Manage Connector Groups** and create a connector group by giving hello group a name.</span></span>  
    <span data-ttu-id="204fd-129">![Captura de tela dos grupos de conectores do proxy de aplicativo - nomeie o novo grupo](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span><span class="sxs-lookup"><span data-stu-id="204fd-129">![Application proxy connector groups screenshot - name new group](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span></span>

## <a name="step-2-assign-connectors-tooyour-groups"></a><span data-ttu-id="204fd-130">Etapa 2: Atribuir conectores tooyour grupos</span><span class="sxs-lookup"><span data-stu-id="204fd-130">Step 2: Assign connectors tooyour groups</span></span>
<span data-ttu-id="204fd-131">Após a criação de grupos de conector Olá, mova o grupo apropriado do hello conectores toohello.</span><span class="sxs-lookup"><span data-stu-id="204fd-131">Once hello connector groups are created, move hello connectors toohello appropriate group.</span></span>

1. <span data-ttu-id="204fd-132">Em **Proxy de Aplicativo**, clique em **Gerenciar Conectores**.</span><span class="sxs-lookup"><span data-stu-id="204fd-132">Under **Application Proxy**, click **Manage Connectors**.</span></span>
2. <span data-ttu-id="204fd-133">Em **grupo**, selecione grupo Olá desejado para cada conector.</span><span class="sxs-lookup"><span data-stu-id="204fd-133">Under **Group**, select hello group you want for each connector.</span></span> <span data-ttu-id="204fd-134">Pode levar conectores Olá backup too10 minutos toobecome ativos no novo grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="204fd-134">It might take hello connectors up too10 minutes toobecome active in hello new group.</span></span>  
    <span data-ttu-id="204fd-135">![Captura de tela dos conectores do proxy de aplicativo - selecione o grupo no menu suspenso](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span><span class="sxs-lookup"><span data-stu-id="204fd-135">![Application proxy connectors screenshot - select group from dropdown menu](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span></span>

## <a name="step-3-assign-applications-tooyour-connector-groups"></a><span data-ttu-id="204fd-136">Etapa 3: Atribuir grupos de conector tooyour de aplicativos</span><span class="sxs-lookup"><span data-stu-id="204fd-136">Step 3: Assign applications tooyour connector groups</span></span>
<span data-ttu-id="204fd-137">última etapa de saudação é tooset cada grupo de conector toohello de aplicativos que atende.</span><span class="sxs-lookup"><span data-stu-id="204fd-137">hello last step is tooset each application toohello connector group that serves it.</span></span>

1. <span data-ttu-id="204fd-138">Em Olá portal clássico do Azure, em seu diretório, selecione Olá aplicativo deseja tooassign toohello grupo e clique em **configurar**.</span><span class="sxs-lookup"><span data-stu-id="204fd-138">In hello Azure classic portal, in your directory, select hello Application you want tooassign toohello group and click **Configure**.</span></span>
2. <span data-ttu-id="204fd-139">Em **grupo**, selecione grupo Olá deseja Olá toouse de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="204fd-139">Under **Connector group**, select hello group you want hello application toouse.</span></span> <span data-ttu-id="204fd-140">A alteração é aplicada imediatamente.</span><span class="sxs-lookup"><span data-stu-id="204fd-140">This change is immediately applied.</span></span>  
    <span data-ttu-id="204fd-141">![Captura de tela do grupo de conectores do proxy de aplicativo - selecione o grupo no menu suspenso](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span><span class="sxs-lookup"><span data-stu-id="204fd-141">![Application proxy connector group screenshot - select group from dropdown menu](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span></span>

## <a name="see-also"></a><span data-ttu-id="204fd-142">Confira também</span><span class="sxs-lookup"><span data-stu-id="204fd-142">See also</span></span>
* [<span data-ttu-id="204fd-143">Habilitar Proxy de aplicativo</span><span class="sxs-lookup"><span data-stu-id="204fd-143">Enable Application Proxy</span></span>](active-directory-application-proxy-enable.md)
* [<span data-ttu-id="204fd-144">Habilitar o logon único</span><span class="sxs-lookup"><span data-stu-id="204fd-144">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="204fd-145">Habilitar o acesso condicional</span><span class="sxs-lookup"><span data-stu-id="204fd-145">Enable conditional access</span></span>](active-directory-application-proxy-conditional-access.md)
* [<span data-ttu-id="204fd-146">Solucionar problemas que surgirem com o Proxy de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="204fd-146">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)

<span data-ttu-id="204fd-147">Para Olá últimas notícias e atualizações, confira Olá [blog de Proxy de aplicativo](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="204fd-147">For hello latest news and updates, check out hello [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
