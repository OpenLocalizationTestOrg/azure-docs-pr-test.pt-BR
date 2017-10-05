---
title: Implantar QuickBooks no RemoteApp do Azure | Microsoft Docs
description: Aprenda a compartilhar QuickBooks com o RemoteApp do Azure.
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c5d00753-77c0-4f0d-a5df-9451b46a31d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: bbfac45220f6ef36c9951daae0ced1974e8ddabb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a><span data-ttu-id="778f9-103">Como implantar o QuickBooks no RemoteApp do Azure?</span><span class="sxs-lookup"><span data-stu-id="778f9-103">How do you deploy QuickBooks in Azure RemoteApp?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="778f9-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="778f9-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="778f9-105">Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="778f9-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="778f9-106">Use as seguintes informações para compartilhar QuickBooks como um aplicativo RemoteApp do Azure.</span><span class="sxs-lookup"><span data-stu-id="778f9-106">Use the following information to share QuickBooks as an app in Azure RemoteApp.</span></span>

<span data-ttu-id="778f9-107">Você pode compartilhar o QuickBooks 2015 Enterprise com o RemoteApp do Azure em uma coleção híbrida ou de nuvem.</span><span class="sxs-lookup"><span data-stu-id="778f9-107">You can share QuickBooks 2015 Enterprise with Azure RemoteApp in either a hybrid or cloud collection.</span></span> <span data-ttu-id="778f9-108">O arquivo da empresa deve residir em uma VM que esteja executando o servidor de banco de dados do QuickBooks separado dos servidores do RemoteApp do Azure.</span><span class="sxs-lookup"><span data-stu-id="778f9-108">The company file must reside on a VM that is running QuickBooks database server that is separate from the Azure RemoteApp servers.</span></span> <span data-ttu-id="778f9-109">Nunca armazene o arquivo da empresa em sua imagem do RemoteApp do Azure, pode haver perda de dados se você fizer isso.</span><span class="sxs-lookup"><span data-stu-id="778f9-109">Never store the company file on your Azure RemoteApp image - data loss is expected if you do this.</span></span> <span data-ttu-id="778f9-110">Somente o QuickBooks Enterprise dá suporte à hospedagem do arquivo QuickBooks em um compartilhamento externo com o servidor de banco de dados do QuickBooks acessível por meio de redes do Windows padrão.</span><span class="sxs-lookup"><span data-stu-id="778f9-110">Only QuickBooks Enterprise supports hosting the QuickBooks file on an external share with QuickBooks database server accessible via standard Windows networking.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="778f9-111">O servidor de banco de dados do QuickBooks que está hospedando o arquivo da empresa deve residir em uma VM separada na mesma VNET que a coleção do RemoteApp do Azure.</span><span class="sxs-lookup"><span data-stu-id="778f9-111">The QuickBooks database server that is hosting the company file must reside on a separate VM within the same VNET as the Azure RemoteApp collection.</span></span>  
> 
> 

## <a name="steps-to-deploy-quickbooks"></a><span data-ttu-id="778f9-112">Etapas para implantar o QuickBooks</span><span class="sxs-lookup"><span data-stu-id="778f9-112">Steps to deploy QuickBooks</span></span>
1. <span data-ttu-id="778f9-113">Crie uma VM do Azure e instale o QuickBooks, o servidor de banco de dados do QuickBooks e coloque o arquivo da empresa em uma VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="778f9-113">Create an Azure VM and install QuickBooks, QuickBooks database server, and place the company file on a Azure VM.</span></span>  <span data-ttu-id="778f9-114">Certifique-se de configurar corretamente as regras de firewall.</span><span class="sxs-lookup"><span data-stu-id="778f9-114">Make sure to properly configure firewall rules.</span></span>
2. <span data-ttu-id="778f9-115">Instale o QuickBooks em uma [imagem personalizada](remoteapp-imageoptions.md) e crie uma [coleção do RemoteApp do Azure](remoteapp-collections.md), em nuvem ou híbrida, com a mesma VNET em que a VM que hospeda o servidor de banco de dados do QuickBooks com os arquivos da empresa está.</span><span class="sxs-lookup"><span data-stu-id="778f9-115">Install QuickBooks on a [custom image](remoteapp-imageoptions.md) and create an [Azure RemoteApp collection](remoteapp-collections.md), either cloud or hybrid, within the exact same VNET where the VM hosting the QuickBooks database server with company files resides.</span></span> 
3. <span data-ttu-id="778f9-116">[Publicar](remoteapp-publish.md) o aplicativo QuickBooks aos usuários</span><span class="sxs-lookup"><span data-stu-id="778f9-116">[Publish](remoteapp-publish.md) QuickBooks app to users</span></span>
4. <span data-ttu-id="778f9-117">Inicie o cliente do QuickBooks hospedado no RemoteApp do Azure, navegue usando a rede padrão do Windows até a VM que hospeda o servidor de banco de dados do QuickBooks e abra o arquivo da empresa.</span><span class="sxs-lookup"><span data-stu-id="778f9-117">Launch the Azure RemoteApp-hosted QuickBooks client, navigate using standard Windows networking to the VM hosting the QuickBooks database server and open the company file.</span></span> 

## <a name="documentation-references"></a><span data-ttu-id="778f9-118">Referências de documentação</span><span class="sxs-lookup"><span data-stu-id="778f9-118">Documentation references</span></span>
* <span data-ttu-id="778f9-119">[Configurações com suporte](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span><span class="sxs-lookup"><span data-stu-id="778f9-119">QuickBooks [supported configurations](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span></span>
* <span data-ttu-id="778f9-120">[Opções de implantação](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span><span class="sxs-lookup"><span data-stu-id="778f9-120">QuickBooks [deployment options](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span></span>

<span data-ttu-id="778f9-121">Você também pode conferir minha apresentação do Ignite, [Conceitos básicos de Gerenciamento e Administração do RemoteApp do Microsoft Azure](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) ; avance até 1:02:45 para chegar à parte sobre QuickBooks.</span><span class="sxs-lookup"><span data-stu-id="778f9-121">You can also check out my Ignite presentation, [Fundamentals of Microsoft Azure RemoteApp Management and Administration](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) - fast-forward to 1:02:45 to get to the QuickBooks part.</span></span>

## <a name="deployment-architecture"></a><span data-ttu-id="778f9-122">Arquitetura de implantação</span><span class="sxs-lookup"><span data-stu-id="778f9-122">Deployment architecture</span></span>
![Implantação do QuickBooks + RemoteApp do Azure](./media/remoteapp-quickbooks/ra-quickbooks.png)

