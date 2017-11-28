---
title: Criar FQDN para uma VM do Windows no Portal do Azure | Microsoft Docs
description: "Saiba como criar um nome de domínio totalmente qualificado, ou FQDN, para uma máquina virtual baseada no Resource Manager no Portal do Azure."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a2ae5887-76df-485e-ae19-0efd96df8600
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2d5a555cd873222efcdb29e8eb3aaf128a24414b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-fully-qualified-domain-name-in-the-azure-portal-for-a-windows-vm"></a><span data-ttu-id="d0d8a-103">Criar um nome de domínio totalmente qualificado no Portal do Azure para uma VM Windows</span><span class="sxs-lookup"><span data-stu-id="d0d8a-103">Create a fully qualified domain name in the Azure portal for a Windows VM</span></span>

<span data-ttu-id="d0d8a-104">Quando você cria uma máquina virtual (VM) no [portal do Azure](https://portal.azure.com), um recurso de IP público para a máquina virtual é criado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d0d8a-104">When you create a virtual machine (VM) in the [Azure portal](https://portal.azure.com), a public IP resource for the virtual machine is automatically created.</span></span> <span data-ttu-id="d0d8a-105">Use esse endereço IP para acessar a VM remotamente.</span><span class="sxs-lookup"><span data-stu-id="d0d8a-105">You use this IP address to remotely access the VM.</span></span> <span data-ttu-id="d0d8a-106">Embora o portal não crie um [nome de domínio totalmente qualificado](https://en.wikipedia.org/wiki/Fully_qualified_domain_name) ou FQDN, você poderá criar um depois que a VM for criada.</span><span class="sxs-lookup"><span data-stu-id="d0d8a-106">Although the portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, you can create one once the VM is created.</span></span> <span data-ttu-id="d0d8a-107">Este artigo apresenta as etapas para criar um nome DNS ou FQDN.</span><span class="sxs-lookup"><span data-stu-id="d0d8a-107">This article demonstrates the steps to create a DNS name or FQDN.</span></span>

## <a name="create-a-fqdn"></a><span data-ttu-id="d0d8a-108">Criar um FQDN</span><span class="sxs-lookup"><span data-stu-id="d0d8a-108">Create a FQDN</span></span>
<span data-ttu-id="d0d8a-109">Este artigo pressupõe que você já tenha criado uma VM.</span><span class="sxs-lookup"><span data-stu-id="d0d8a-109">This article assumes that you have already created a VM.</span></span> <span data-ttu-id="d0d8a-110">Se necessário, [crie uma VM no portal](quick-create-portal.md) ou [com Azure PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d0d8a-110">If needed, you can [create a VM in the portal](quick-create-portal.md) or [with Azure PowerShell](quick-create-powershell.md).</span></span> <span data-ttu-id="d0d8a-111">Siga estas etapas depois que a VM estiver em execução:</span><span class="sxs-lookup"><span data-stu-id="d0d8a-111">Follow these steps once your VM is up and running:</span></span>

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

<span data-ttu-id="d0d8a-112">Agora você pode se conectar à VM remotamente usando esse nome DNS, como para o protocolo RDP.</span><span class="sxs-lookup"><span data-stu-id="d0d8a-112">You can now connect remotely to the VM using this DNS name such as for Remote Desktop Protocol (RDP).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0d8a-113">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d0d8a-113">Next steps</span></span>
<span data-ttu-id="d0d8a-114">Agora que sua VM tem um IP público e um nome DNS, é possível implantar estruturas comuns do aplicativo ou serviços, como IIS, SQL ou SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d0d8a-114">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as IIS, SQL, or SharePoint.</span></span>

<span data-ttu-id="d0d8a-115">Leia mais sobre como [usar o Resource Manager](../../azure-resource-manager/resource-group-overview.md) para obter dicas sobre a criação de implantações do Azure.</span><span class="sxs-lookup"><span data-stu-id="d0d8a-115">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span></span>

