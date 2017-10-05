---
title: "Criar e gerenciar máquinas virtuais em DevTest Labs com a CLI do Azure | Microsoft Docs"
description: "Saiba como usar o Azure DevTest Labs para criar e gerenciar máquinas virtuais com a CLI 2.0 do Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: lisawong19
manager: douge
editor: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: liwong
ms.openlocfilehash: 42b0448c1bcdfa909715abd5075353d63cab8389
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-virtual-machines-with-devtest-labs-using-the-azure-cli"></a><span data-ttu-id="af141-103">Criar e gerenciar máquinas virtuais com DevTest Labs usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="af141-103">Create and manage virtual machines with DevTest Labs using the Azure CLI</span></span>
<span data-ttu-id="af141-104">Este guia rápido ajudará você a criar, iniciar, conectar, atualizar e limpar um computador de desenvolvimento em seu laboratório.</span><span class="sxs-lookup"><span data-stu-id="af141-104">This quick start will guide you through creating, starting, connecting, updating and cleaning up a development machine in your lab.</span></span> 

<span data-ttu-id="af141-105">Antes de começar:</span><span class="sxs-lookup"><span data-stu-id="af141-105">Before you begin:</span></span>

* <span data-ttu-id="af141-106">Se um laboratório não tiver sido criado, as instruções poderão ser encontradas [aqui](devtest-lab-create-lab.md).</span><span class="sxs-lookup"><span data-stu-id="af141-106">If a lab has not been created, instructions can be found [here](devtest-lab-create-lab.md).</span></span>

* <span data-ttu-id="af141-107">[Instalar a CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="af141-107">[Install CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="af141-108">Para iniciar, execute az login para criar uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="af141-108">To start, run az login to create a connection with Azure.</span></span> 

## <a name="create-and-verify-the-virtual-machine"></a><span data-ttu-id="af141-109">Criar e verificar a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="af141-109">Create and verify the virtual machine</span></span> 
<span data-ttu-id="af141-110">Crie uma máquina virtual de uma imagem do marketplace com autenticação ssh.</span><span class="sxs-lookup"><span data-stu-id="af141-110">Create a VM from a marketplace image with ssh authentication.</span></span>
```azurecli
az lab vm create --lab-name sampleLabName --resource-group sampleLabResourceGroup --name sampleVMName --image "Ubuntu Server 16.04 LTS" --image-type gallery --size Standard_DS1_v2 --authentication-type  ssh --generate-ssh-keys --ip-configuration public 
```
> [!NOTE]
> <span data-ttu-id="af141-111">Coloque o nome do **grupo de recursos do laboratório** no parâmetro --resource-group.</span><span class="sxs-lookup"><span data-stu-id="af141-111">Put the **lab's resource group** name in the --resource-group parameter.</span></span>
>

<span data-ttu-id="af141-112">Se você quiser criar uma máquina virtual usando uma fórmula, use o parâmetro --formula em [az lab vm create](https://docs.microsoft.com/cli/azure/lab/vm#create).</span><span class="sxs-lookup"><span data-stu-id="af141-112">If you want to create a VM using a formula, use the --formula parameter in [az lab vm create](https://docs.microsoft.com/cli/azure/lab/vm#create).</span></span>


<span data-ttu-id="af141-113">Verifique se a VM está disponível.</span><span class="sxs-lookup"><span data-stu-id="af141-113">Verify that the VM is available.</span></span>
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand 'properties($expand=ComputeVm,NetworkInterface)' --query '{status: computeVm.statuses[0].displayStatus, fqdn: fqdn, ipAddress: networkInterface.publicIpAddress}'
```
```json
{
  "fqdn": "lisalabvm.southcentralus.cloudapp.azure.com",
  "ipAddress": "13.85.228.112",
  "status": "Provisioning succeeded"
}
```

## <a name="start-and-connect-to-the-virtual-machine"></a><span data-ttu-id="af141-114">Iniciar e conectar-se à máquina virtual</span><span class="sxs-lookup"><span data-stu-id="af141-114">Start and connect to the virtual machine</span></span>
<span data-ttu-id="af141-115">Inicie uma VM.</span><span class="sxs-lookup"><span data-stu-id="af141-115">Start a VM.</span></span>
```azurecli
az lab vm start --lab-name sampleLabName --name sampleVMName --resource-group sampleLabResourceGroup
```
> [!NOTE]
> <span data-ttu-id="af141-116">Coloque o nome do **grupo de recursos do laboratório** no parâmetro --resource-group.</span><span class="sxs-lookup"><span data-stu-id="af141-116">Put the **lab's resource group** name in the --resource-group parameter.</span></span>
>

<span data-ttu-id="af141-117">Conectar-se a uma VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) ou [Área de Trabalho Remota](../virtual-machines/windows/connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="af141-117">Connect to a VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) or [Remote Desktop](../virtual-machines/windows/connect-logon.md).</span></span>
```bash
ssh userName@ipAddressOrfqdn 
```

## <a name="update-the-virtual-machine"></a><span data-ttu-id="af141-118">Atualizar a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="af141-118">Update the virtual machine</span></span>
<span data-ttu-id="af141-119">Aplique artefatos a uma VM.</span><span class="sxs-lookup"><span data-stu-id="af141-119">Apply artifacts to a VM.</span></span>
```azurecli
az lab vm apply-artifacts --lab-name  sampleLabName --name sampleVMName  --resource-group sampleResourceGroup  --artifacts @/artifacts.json
```

```json
[
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-java",
    "parameters": []
  },
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-install-nodejs",
    "parameters": []
  },
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-apt-package",
    "parameters": [
      {
        "name": "packages",
        "value": "abcd"
      },
      {
        "name": "update",
        "value": "true"
      },
      {
        "name": "options",
        "value": ""
      }
    ]
  } 
]
```

<span data-ttu-id="af141-120">Lista de artefatos disponíveis no laboratório.</span><span class="sxs-lookup"><span data-stu-id="af141-120">List artifacts available in the lab.</span></span>
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand "properties(\$expand=artifacts)" --query 'artifacts[].{artifactId: artifactId, status: status}'
```
```json
{
  "artifactId": "/subscriptions/abcdeftgh1213123/resourceGroups/lisalab123RG822645/providers/Microsoft.DevTestLab/labs/lisalab123/artifactSources/public repo/artifacts/linux-install-nodejs",
  "status": "Succeeded"
}
```

## <a name="stop-and-delete-the-virtual-machine"></a><span data-ttu-id="af141-121">Parar e excluir a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="af141-121">Stop and delete the virtual machine</span></span>    
<span data-ttu-id="af141-122">Pare uma VM.</span><span class="sxs-lookup"><span data-stu-id="af141-122">Stop a VM.</span></span>
```azurecli
az lab vm stop --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

<span data-ttu-id="af141-123">Exclua uma VM.</span><span class="sxs-lookup"><span data-stu-id="af141-123">Delete a VM.</span></span>
```azurecli
az lab vm delete --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]