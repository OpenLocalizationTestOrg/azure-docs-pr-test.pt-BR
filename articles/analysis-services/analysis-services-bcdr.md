---
title: aaaAzure alta disponibilidade do Analysis Services | Microsoft Docs
description: Garantindo a alta disponibilidade do Azure Analysis Services.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 6e09536c5bd7dc7f88f9b662e1a9f42d2b8c969b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analysis-services-high-availability"></a><span data-ttu-id="7a14a-103">Alta disponibilidade do Analysis Services</span><span class="sxs-lookup"><span data-stu-id="7a14a-103">Analysis Services high availability</span></span>
<span data-ttu-id="7a14a-104">Este artigo descreve como garantir alta disponibilidade para servidores do Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="7a14a-104">This article describes assuring high availability for Azure Analysis Services servers.</span></span> 


## <a name="assuring-high-availability-during-a-service-disruption"></a><span data-ttu-id="7a14a-105">Garantindo alta disponibilidade durante uma interrupção do serviço</span><span class="sxs-lookup"><span data-stu-id="7a14a-105">Assuring high availability during a service disruption</span></span>
<span data-ttu-id="7a14a-106">Embora seja raro, um data center do Azure pode sofrer uma interrupção.</span><span class="sxs-lookup"><span data-stu-id="7a14a-106">While rare, an Azure data center can have an outage.</span></span> <span data-ttu-id="7a14a-107">Quando uma interrupção ocorre, ela causa uma parada nos negócios que pode durar alguns minutos ou até mesmo horas.</span><span class="sxs-lookup"><span data-stu-id="7a14a-107">When an outage occurs, it causes a business disruption that might last a few minutes or might last for hours.</span></span> <span data-ttu-id="7a14a-108">A alta disponibilidade geralmente é obtida com redundância do servidor.</span><span class="sxs-lookup"><span data-stu-id="7a14a-108">High availability is most often achieved with server redundancy.</span></span> <span data-ttu-id="7a14a-109">Com o Azure Analysis Services, você pode obter redundância criando servidores secundários adicionais em uma ou mais regiões.</span><span class="sxs-lookup"><span data-stu-id="7a14a-109">With Azure Analysis Services, you can achieve redundancy by creating additional, secondary servers in one or more regions.</span></span> <span data-ttu-id="7a14a-110">Ao criar servidores redundantes, dados de saudação tooassure e metadados nesses servidores está em sincronia com o servidor de saudação em uma região que ficou offline, você pode:</span><span class="sxs-lookup"><span data-stu-id="7a14a-110">When creating redundant servers, tooassure hello data and metadata on those servers is in-sync with hello server in a region that has gone offline, you can:</span></span>

* <span data-ttu-id="7a14a-111">Implante modelos tooredundant servidores em outras regiões.</span><span class="sxs-lookup"><span data-stu-id="7a14a-111">Deploy models tooredundant servers in other regions.</span></span> <span data-ttu-id="7a14a-112">Esse método requer processamento de dados no servidor primário e servidores redundantes em paralelo, garantindo que todos os servidores estejam em sincronia.</span><span class="sxs-lookup"><span data-stu-id="7a14a-112">This method requires processing data on both your primary server and redundant servers in-parallel, assuring all servers are in-sync.</span></span>

* <span data-ttu-id="7a14a-113">Faça backup dos bancos de dados do seu servidor primário e restaure em servidores redundantes.</span><span class="sxs-lookup"><span data-stu-id="7a14a-113">Back up databases from your primary server and restore on redundant servers.</span></span> <span data-ttu-id="7a14a-114">Por exemplo, você pode automatizar o armazenamento de tooAzure backups noturnos e restaurar os servidores redundantes tooother em outras regiões.</span><span class="sxs-lookup"><span data-stu-id="7a14a-114">For example, you can automate nightly backups tooAzure storage, and restore tooother redundant servers in other regions.</span></span> 

<span data-ttu-id="7a14a-115">Em ambos os casos, se o servidor primário sofrer uma interrupção, você deve alterar cadeias de caracteres de conexão de saudação em clientes tooconnect toohello servidor em um datacenter regional diferente de relatórios.</span><span class="sxs-lookup"><span data-stu-id="7a14a-115">In either case, if your primary server experiences an outage, you must change hello connection strings in reporting clients tooconnect toohello server in a different regional datacenter.</span></span> <span data-ttu-id="7a14a-116">Essa alteração deve ser considerada um último recurso e apenas caso ocorra uma interrupção catastrófica de data center regional.</span><span class="sxs-lookup"><span data-stu-id="7a14a-116">This change should be considered a last resort and only if a catastrophic regional data center outage occurs.</span></span> <span data-ttu-id="7a14a-117">É mais provável que, após uma interrupção, o data center que hospeda o servidor primário fique online novamente antes de você poder atualizar conexões em todos os clientes.</span><span class="sxs-lookup"><span data-stu-id="7a14a-117">It's more likely a data center outage hosting your primary server would come back online before you could update connections on all clients.</span></span> 



## <a name="related-information"></a><span data-ttu-id="7a14a-118">Informações relacionadas</span><span class="sxs-lookup"><span data-stu-id="7a14a-118">Related information</span></span>
<span data-ttu-id="7a14a-119">[Fazer backup e restaurar](analysis-services-backup.md) </span><span class="sxs-lookup"><span data-stu-id="7a14a-119">[Backup and restore](analysis-services-backup.md) </span></span>  
[<span data-ttu-id="7a14a-120">Gerenciar Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="7a14a-120">Manage Azure Analysis Services</span></span>](analysis-services-manage.md) 

