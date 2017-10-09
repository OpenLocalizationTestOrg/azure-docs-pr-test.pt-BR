---
title: aaaValidate hello Azure VNET toouse com o Azure RemoteApp | Microsoft Docs
description: "Saiba como toomake-se de que sua rede virtual do Azure está pronto toouse com o Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b573ba02-4587-4be5-9821-27bd891a73b2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 5587556c264356e6ab6039b983a38cb2b95ed268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="validate-hello-azure-vnet-toouse-with-azure-remoteapp"></a><span data-ttu-id="9140f-103">Validar Olá toouse de rede virtual do Azure com o Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="9140f-103">Validate hello Azure VNET toouse with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9140f-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="9140f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="9140f-105">Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="9140f-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="9140f-106">Antes de usar uma rede virtual do Azure com o Azure RemoteApp, talvez você queira Olá toovalidate VNET.</span><span class="sxs-lookup"><span data-stu-id="9140f-106">Before you use an Azure VNET with Azure RemoteApp, you might want toovalidate hello VNET.</span></span> <span data-ttu-id="9140f-107">Isso ajuda a evitar problemas com conectividade.</span><span class="sxs-lookup"><span data-stu-id="9140f-107">This helps prevent issues with connectivity.</span></span>

<span data-ttu-id="9140f-108">toovalidate VNET do Azure, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="9140f-108">toovalidate your Azure VNET, do hello following:</span></span>

1. <span data-ttu-id="9140f-109">Crie uma máquina virtual do Azure Olá sub-rede de saudação VNET do Azure que você deseja toouse com o Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="9140f-109">Create an Azure virtual machine inside hello subnet of hello Azure VNET you want toouse with Azure RemoteApp.</span></span>
2. <span data-ttu-id="9140f-110">Conecte-se toothat VM usando Olá **conectar** opção no portal de gerenciamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="9140f-110">Connect toothat VM by using hello **Connect** option in hello management portal.</span></span>
3. <span data-ttu-id="9140f-111">Unir Olá máquina virtual toohello mesmo domínio que você deseja toouse com o Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="9140f-111">Join hello virtual machine toohello same domain that you want toouse with Azure RemoteApp.</span></span> <span data-ttu-id="9140f-112">Se você estiver criando uma coleção híbrida que se conecta a rede de local de tooyour, ingresse no domínio local do tooyour Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9140f-112">If you are creating a hybrid collection that connects tooyour on-premises network, join hello virtual machine tooyour local domain.</span></span>

<span data-ttu-id="9140f-113">Se for bem-sucedida, Olá VNET do Azure está pronto toouse com o RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="9140f-113">If this is successful, hello Azure VNET is ready toouse with RemoteApp.</span></span>

<span data-ttu-id="9140f-114">Para obter mais informações sobre o fluxo de trabalho de coleta do hello híbrida de ponta a ponta, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="9140f-114">For more information about hello end-to-end hybrid collection workflow, see hello following articles:</span></span>

* [<span data-ttu-id="9140f-115">Como tooplan sua rede virtual do Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="9140f-115">How tooplan your virtual network for Azure RemoteApp</span></span>](remoteapp-planvnet.md)
* [<span data-ttu-id="9140f-116">Criar uma coleção híbrida</span><span class="sxs-lookup"><span data-stu-id="9140f-116">Create a hybrid collection</span></span>](remoteapp-create-hybrid-deployment.md)
* [<span data-ttu-id="9140f-117">Implantar o Azure RemoteApp coleção tooyour rede Virtual do Azure (com suporte para o ExpressRoute)</span><span class="sxs-lookup"><span data-stu-id="9140f-117">Deploy Azure RemoteApp collection tooyour Azure Virtual Network (with support for ExpressRoute)</span></span>](http://blogs.msdn.com/b/rds/archive/2015/04/23/deploy-azure-remoteapp-collection-to-your-azure-virtual-network-with-support-for-expressroute.aspx)

