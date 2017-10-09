---
title: aaaDeploy QuickBooks no Azure RemoteApp | Microsoft Docs
description: Saiba como tooshare QuickBooks com o Azure RemoteApp.
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
ms.openlocfilehash: c21b1ac311449be2281f9ce157828260e856f55d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a><span data-ttu-id="bf343-103">Como implantar o QuickBooks no RemoteApp do Azure?</span><span class="sxs-lookup"><span data-stu-id="bf343-103">How do you deploy QuickBooks in Azure RemoteApp?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="bf343-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="bf343-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="bf343-105">Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="bf343-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="bf343-106">Use Olá informações tooshare QuickBooks a seguir como um aplicativo no Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="bf343-106">Use hello following information tooshare QuickBooks as an app in Azure RemoteApp.</span></span>

<span data-ttu-id="bf343-107">Você pode compartilhar o QuickBooks 2015 Enterprise com o RemoteApp do Azure em uma coleção híbrida ou de nuvem.</span><span class="sxs-lookup"><span data-stu-id="bf343-107">You can share QuickBooks 2015 Enterprise with Azure RemoteApp in either a hybrid or cloud collection.</span></span> <span data-ttu-id="bf343-108">arquivo de saudação da empresa deve residir em uma máquina virtual que está executando o servidor de banco de dados do QuickBooks que está separado dos servidores do Azure RemoteApp hello.</span><span class="sxs-lookup"><span data-stu-id="bf343-108">hello company file must reside on a VM that is running QuickBooks database server that is separate from hello Azure RemoteApp servers.</span></span> <span data-ttu-id="bf343-109">Nunca armazenar arquivo hello da empresa em sua imagem do Azure RemoteApp - perda de dados é esperada se você fizer isso.</span><span class="sxs-lookup"><span data-stu-id="bf343-109">Never store hello company file on your Azure RemoteApp image - data loss is expected if you do this.</span></span> <span data-ttu-id="bf343-110">Somente QuickBooks Enterprise dá suporte a arquivo de QuickBooks Olá hospedagem em um compartilhamento externo com o servidor de banco de dados do QuickBooks acessível por meio de rede padrão do Windows.</span><span class="sxs-lookup"><span data-stu-id="bf343-110">Only QuickBooks Enterprise supports hosting hello QuickBooks file on an external share with QuickBooks database server accessible via standard Windows networking.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="bf343-111">Olá QuickBooks servidor de banco de dados que está hospedando o arquivo da empresa Olá deve residir em uma VM separada em Olá mesmo VNET como Olá coleção do RemoteApp do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf343-111">hello QuickBooks database server that is hosting hello company file must reside on a separate VM within hello same VNET as hello Azure RemoteApp collection.</span></span>  
> 
> 

## <a name="steps-toodeploy-quickbooks"></a><span data-ttu-id="bf343-112">Etapas toodeploy QuickBooks</span><span class="sxs-lookup"><span data-stu-id="bf343-112">Steps toodeploy QuickBooks</span></span>
1. <span data-ttu-id="bf343-113">Criar uma VM do Azure e instale o QuickBooks, servidor de banco de dados do QuickBooks e colocar o arquivo hello da empresa em uma VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf343-113">Create an Azure VM and install QuickBooks, QuickBooks database server, and place hello company file on a Azure VM.</span></span>  <span data-ttu-id="bf343-114">Verifique se tooproperly configurar regras de firewall.</span><span class="sxs-lookup"><span data-stu-id="bf343-114">Make sure tooproperly configure firewall rules.</span></span>
2. <span data-ttu-id="bf343-115">Instale o QuickBooks em um [imagem personalizada](remoteapp-imageoptions.md) e criar um [coleção do RemoteApp do Azure](remoteapp-collections.md), nuvem ou híbrida, em Olá exato da mesma rede virtual onde Olá VM hospedando Olá servidor de banco de dados do QuickBooks com arquivos da empresa reside.</span><span class="sxs-lookup"><span data-stu-id="bf343-115">Install QuickBooks on a [custom image](remoteapp-imageoptions.md) and create an [Azure RemoteApp collection](remoteapp-collections.md), either cloud or hybrid, within hello exact same VNET where hello VM hosting hello QuickBooks database server with company files resides.</span></span> 
3. <span data-ttu-id="bf343-116">[Publicar](remoteapp-publish.md) QuickBooks aplicativo toousers</span><span class="sxs-lookup"><span data-stu-id="bf343-116">[Publish](remoteapp-publish.md) QuickBooks app toousers</span></span>
4. <span data-ttu-id="bf343-117">Iniciar o cliente do QuickBooks hospedado do Azure RemoteApp hello, navegar usando a rede toohello VM hospedagem Olá QuickBooks servidor banco de dados padrão do Windows e abra o arquivo hello da empresa.</span><span class="sxs-lookup"><span data-stu-id="bf343-117">Launch hello Azure RemoteApp-hosted QuickBooks client, navigate using standard Windows networking toohello VM hosting hello QuickBooks database server and open hello company file.</span></span> 

## <a name="documentation-references"></a><span data-ttu-id="bf343-118">Referências de documentação</span><span class="sxs-lookup"><span data-stu-id="bf343-118">Documentation references</span></span>
* <span data-ttu-id="bf343-119">[Configurações com suporte](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span><span class="sxs-lookup"><span data-stu-id="bf343-119">QuickBooks [supported configurations](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span></span>
* <span data-ttu-id="bf343-120">[Opções de implantação](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span><span class="sxs-lookup"><span data-stu-id="bf343-120">QuickBooks [deployment options](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span></span>

<span data-ttu-id="bf343-121">Você também pode consultar a apresentação Ignite, [conceitos básicos do Microsoft Azure RemoteApp gerenciamento e administração](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) -Avançar too1:02:45 tooget toohello QuickBooks parte.</span><span class="sxs-lookup"><span data-stu-id="bf343-121">You can also check out my Ignite presentation, [Fundamentals of Microsoft Azure RemoteApp Management and Administration](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) - fast-forward too1:02:45 tooget toohello QuickBooks part.</span></span>

## <a name="deployment-architecture"></a><span data-ttu-id="bf343-122">Arquitetura de implantação</span><span class="sxs-lookup"><span data-stu-id="bf343-122">Deployment architecture</span></span>
![Implantação do QuickBooks + RemoteApp do Azure](./media/remoteapp-quickbooks/ra-quickbooks.png)

