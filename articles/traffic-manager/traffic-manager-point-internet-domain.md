---
title: "aaaPoint um nome de domínio da empresa Internet domínio tooa Traffic Manager | Microsoft Docs"
description: "Este artigo o ajudará a apontar seu nome de domínio da empresa domínio nome tooa Gerenciador de tráfego."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 29822946-2d45-4434-ba47-fc180a445cc3
ms.service: traffic-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: kumud
ms.openlocfilehash: 84c428f60a1dc70452bf957d98a68c95e0b51715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="point-a-company-internet-domain-tooan-azure-traffic-manager-domain"></a><span data-ttu-id="ebb96-103">Apontar um domínio de Gerenciador de tráfego do Azure da empresa Internet domínio tooan</span><span class="sxs-lookup"><span data-stu-id="ebb96-103">Point a company Internet domain tooan Azure Traffic Manager domain</span></span>

<span data-ttu-id="ebb96-104">Quando você cria um perfil do Gerenciador de tráfego, o Azure atribui automaticamente um nome DNS ao perfil.</span><span class="sxs-lookup"><span data-stu-id="ebb96-104">When you create a Traffic Manager profile, Azure automatically assigns a DNS name for that profile.</span></span> <span data-ttu-id="ebb96-105">toouse um nome de zona DNS, crie um registro de DNS CNAME que mapeia o nome de domínio toohello do seu perfil do Gerenciador de tráfego.</span><span class="sxs-lookup"><span data-stu-id="ebb96-105">toouse a name from your DNS zone, create a CNAME DNS record that maps toohello domain name of your Traffic Manager profile.</span></span> <span data-ttu-id="ebb96-106">Você pode encontrar o nome de domínio do Traffic Manager Olá no hello **geral** seção na página de configuração Olá Olá perfil do Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="ebb96-106">You can find hello Traffic Manager domain name in hello **General** section on hello Configuration page of hello Traffic Manager profile.</span></span>

<span data-ttu-id="ebb96-107">Por exemplo, toopoint nome www.contoso.com toohello contoso.trafficmanager.net de nome DNS do Traffic Manager, você deve criar Olá registro de recurso DNS a seguir:</span><span class="sxs-lookup"><span data-stu-id="ebb96-107">For example, toopoint name www.contoso.com toohello Traffic Manager DNS name contoso.trafficmanager.net, you would create hello following DNS resource record:</span></span>

    www.contoso.com IN CNAME contoso.trafficmanager.net

<span data-ttu-id="ebb96-108">Todo o tráfego de solicitações muito*www.contoso.com* obter direcionado muito*contoso.trafficmanager.net*.</span><span class="sxs-lookup"><span data-stu-id="ebb96-108">All traffic requests too*www.contoso.com* get directed too*contoso.trafficmanager.net*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ebb96-109">Você não pode apontar um domínio de segundo nível, como *contoso.com*, domínio do Traffic Manager toohello.</span><span class="sxs-lookup"><span data-stu-id="ebb96-109">You cannot point a second-level domain, such as *contoso.com*, toohello Traffic Manager domain.</span></span> <span data-ttu-id="ebb96-110">Os padrões de protocolo DNS não permitem registros CNAME para nomes de domínio de segundo nível.</span><span class="sxs-lookup"><span data-stu-id="ebb96-110">DNS protocol standards do not allow CNAME records for second-level domain names.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebb96-111">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ebb96-111">Next steps</span></span>

* [<span data-ttu-id="ebb96-112">Métodos de roteamento do Gerenciador de Tráfego</span><span class="sxs-lookup"><span data-stu-id="ebb96-112">Traffic Manager routing methods</span></span>](traffic-manager-routing-methods.md)
* [<span data-ttu-id="ebb96-113">Gerenciador de Tráfego - Desabilitar, habilitar ou excluir um perfil</span><span class="sxs-lookup"><span data-stu-id="ebb96-113">Traffic Manager - Disable, enable or delete a profile</span></span>](disable-enable-or-delete-a-profile.md)
* [<span data-ttu-id="ebb96-114">Gerenciador de Tráfego - Desabilitar ou habilitar um ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="ebb96-114">Traffic Manager - Disable or enable an endpoint</span></span>](disable-or-enable-an-endpoint.md)
