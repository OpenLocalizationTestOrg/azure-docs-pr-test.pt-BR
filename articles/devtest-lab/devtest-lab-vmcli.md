---
title: "aaaCreate e gerenciar máquinas virtuais no DevTest Labs CLI do Azure | Microsoft Docs"
description: "Saiba como toouse Azure DevTest Labs toocreate e gerenciar máquinas virtuais com 2.0 do CLI do Azure"
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
ms.openlocfilehash: 98ea3aa7b2489bff61971573aaf584984cd811e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-virtual-machines-with-devtest-labs-using-hello-azure-cli"></a><span data-ttu-id="2b257-103">Criar e gerenciar máquinas virtuais com DevTest Labs usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="2b257-103">Create and manage virtual machines with DevTest Labs using hello Azure CLI</span></span>
<span data-ttu-id="2b257-104">Este guia rápido ajudará você a criar, iniciar, conectar, atualizar e limpar um computador de desenvolvimento em seu laboratório.</span><span class="sxs-lookup"><span data-stu-id="2b257-104">This quick start will guide you through creating, starting, connecting, updating and cleaning up a development machine in your lab.</span></span> 

<span data-ttu-id="2b257-105">Antes de começar:</span><span class="sxs-lookup"><span data-stu-id="2b257-105">Before you begin:</span></span>

* <span data-ttu-id="2b257-106">Se um laboratório não tiver sido criado, as instruções poderão ser encontradas [aqui](devtest-lab-create-lab.md).</span><span class="sxs-lookup"><span data-stu-id="2b257-106">If a lab has not been created, instructions can be found [here](devtest-lab-create-lab.md).</span></span>

* <span data-ttu-id="2b257-107">[Instalar a CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2b257-107">[Install CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="2b257-108">toostart, toocreate de logon execução az uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="2b257-108">toostart, run az login toocreate a connection with Azure.</span></span> 

## <a name="create-and-verify-hello-virtual-machine"></a><span data-ttu-id="2b257-109">Criar e verificar Olá a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="2b257-109">Create and verify hello virtual machine</span></span> 
<span data-ttu-id="2b257-110">Crie uma máquina virtual de uma imagem do marketplace com autenticação ssh.</span><span class="sxs-lookup"><span data-stu-id="2b257-110">Create a VM from a marketplace image with ssh authentication.</span></span>
```azurecli
az lab vm create --lab-name sampleLabName --resource-group sampleLabResourceGroup --name sampleVMName --image "Ubuntu Server 16.04 LTS" --image-type gallery --size Standard_DS1_v2 --authentication-type  ssh --generate-ssh-keys --ip-configuration public 
```
> [!NOTE]
> <span data-ttu-id="2b257-111">Colocar Olá **o grupo de recursos do laboratório** no hello – o parâmetro do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2b257-111">Put hello **lab's resource group** name in hello --resource-group parameter.</span></span>
>

<span data-ttu-id="2b257-112">Se você quiser toocreate uma máquina virtual usando uma fórmula, use hello – parâmetro fórmulas em [az laboratório vm criar](https://docs.microsoft.com/cli/azure/lab/vm#create).</span><span class="sxs-lookup"><span data-stu-id="2b257-112">If you want toocreate a VM using a formula, use hello --formula parameter in [az lab vm create](https://docs.microsoft.com/cli/azure/lab/vm#create).</span></span>


<span data-ttu-id="2b257-113">Verifique se que esse Olá VM está disponível.</span><span class="sxs-lookup"><span data-stu-id="2b257-113">Verify that hello VM is available.</span></span>
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

## <a name="start-and-connect-toohello-virtual-machine"></a><span data-ttu-id="2b257-114">Iniciar e conectar-se a máquina virtual de toohello</span><span class="sxs-lookup"><span data-stu-id="2b257-114">Start and connect toohello virtual machine</span></span>
<span data-ttu-id="2b257-115">Inicie uma VM.</span><span class="sxs-lookup"><span data-stu-id="2b257-115">Start a VM.</span></span>
```azurecli
az lab vm start --lab-name sampleLabName --name sampleVMName --resource-group sampleLabResourceGroup
```
> [!NOTE]
> <span data-ttu-id="2b257-116">Colocar Olá **o grupo de recursos do laboratório** no hello – o parâmetro do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2b257-116">Put hello **lab's resource group** name in hello --resource-group parameter.</span></span>
>

<span data-ttu-id="2b257-117">Conecte-se tooa VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) ou [área de trabalho remota](../virtual-machines/windows/connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="2b257-117">Connect tooa VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) or [Remote Desktop](../virtual-machines/windows/connect-logon.md).</span></span>
```bash
ssh userName@ipAddressOrfqdn 
```

## <a name="update-hello-virtual-machine"></a><span data-ttu-id="2b257-118">Atualizar a máquina virtual de saudação</span><span class="sxs-lookup"><span data-stu-id="2b257-118">Update hello virtual machine</span></span>
<span data-ttu-id="2b257-119">Aplica artefatos tooa VM.</span><span class="sxs-lookup"><span data-stu-id="2b257-119">Apply artifacts tooa VM.</span></span>
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

<span data-ttu-id="2b257-120">Artefatos de lista disponíveis no laboratório de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b257-120">List artifacts available in hello lab.</span></span>
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand "properties(\$expand=artifacts)" --query 'artifacts[].{artifactId: artifactId, status: status}'
```
```json
{
  "artifactId": "/subscriptions/abcdeftgh1213123/resourceGroups/lisalab123RG822645/providers/Microsoft.DevTestLab/labs/lisalab123/artifactSources/public repo/artifacts/linux-install-nodejs",
  "status": "Succeeded"
}
```

## <a name="stop-and-delete-hello-virtual-machine"></a><span data-ttu-id="2b257-121">Parar e excluir a máquina virtual de saudação</span><span class="sxs-lookup"><span data-stu-id="2b257-121">Stop and delete hello virtual machine</span></span>    
<span data-ttu-id="2b257-122">Pare uma VM.</span><span class="sxs-lookup"><span data-stu-id="2b257-122">Stop a VM.</span></span>
```azurecli
az lab vm stop --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

<span data-ttu-id="2b257-123">Exclua uma VM.</span><span class="sxs-lookup"><span data-stu-id="2b257-123">Delete a VM.</span></span>
```azurecli
az lab vm delete --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]