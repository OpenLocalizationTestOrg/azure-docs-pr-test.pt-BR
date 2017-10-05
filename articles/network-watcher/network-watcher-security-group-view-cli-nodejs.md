---
title: "Analisar a segurança de rede com exibição de grupo de segurança do Observador de Rede do Azure – CLI 1.0 do Azure | Microsoft Docs"
description: "Este artigo descreve como usar a CLI 1.0 do Azure para analisar um título de máquinas virtuais com o modo de exibição de grupo de segurança."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a986ff4f-7e0c-4994-95e1-4ac824986500
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2c4c494dcc4fe1a85c5feb29506c35fb03066479
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-10"></a><span data-ttu-id="1e3e2-103">Analisar a segurança de máquina Virtual com o modo de exibição de grupo de segurança usando a CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="1e3e2-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="1e3e2-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e3e2-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="1e3e2-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1e3e2-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="1e3e2-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1e3e2-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="1e3e2-107">API REST</span><span class="sxs-lookup"><span data-stu-id="1e3e2-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="1e3e2-108">Exibição de grupo de segurança retorna as regras de segurança de rede configurados e eficaz que são aplicadas a uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1e3e2-108">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span></span> <span data-ttu-id="1e3e2-109">Esse recurso é útil para auditoria e diagnosticar grupos de segurança de rede e as regras configuradas em uma VM para garantir que o tráfego está sendo corretamente permitido ou negado.</span><span class="sxs-lookup"><span data-stu-id="1e3e2-109">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="1e3e2-110">Neste artigo, mostraremos como recuperar as regras de segurança configuradas e em vigor para uma máquina virtual usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="1e3e2-110">In this article, we show you how to retrieve the configured and effective security rules to a virtual machine using Azure CLI</span></span>

<span data-ttu-id="1e3e2-111">Este artigo usa a CLI 1.0 do Azure para plataforma cruzada, que está disponível para Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="1e3e2-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="1e3e2-112">Atualmente, o Observador de Rede usa a CLI 1.0 do Azure para dar suporte à CLI.</span><span class="sxs-lookup"><span data-stu-id="1e3e2-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1e3e2-113">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="1e3e2-113">Before you begin</span></span>

<span data-ttu-id="1e3e2-114">Este cenário pressupõe que você seguiu as etapas em [Criação de um Observador de rede](network-watcher-create.md) para criar um Observador de rede.</span><span class="sxs-lookup"><span data-stu-id="1e3e2-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="1e3e2-115">Cenário</span><span class="sxs-lookup"><span data-stu-id="1e3e2-115">Scenario</span></span>

<span data-ttu-id="1e3e2-116">O cenário abordado neste artigo recupera as regras de segurança configuradas e em vigor para uma determinada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1e3e2-116">The scenario covered in this article retrieves the configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="1e3e2-117">Obter uma VM</span><span class="sxs-lookup"><span data-stu-id="1e3e2-117">Get a VM</span></span>

<span data-ttu-id="1e3e2-118">Uma máquina virtual é necessária para executar o cmdlet `vm list`.</span><span class="sxs-lookup"><span data-stu-id="1e3e2-118">A virtual machine is required to run the `vm list` cmdlet.</span></span> <span data-ttu-id="1e3e2-119">O comando a seguir lista as máquinas virtuais em um grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="1e3e2-119">The following command lists the virtual machinese in a resource group:</span></span>

```azurecli
azure vm list -g resourceGroupName
```

<span data-ttu-id="1e3e2-120">Se você conhecer a máquina virtual, poderá usar o `vm show` para obter sua Id de recurso:</span><span class="sxs-lookup"><span data-stu-id="1e3e2-120">Once you know the virtual machine, you can use the `vm show` cmdlet to get its resource Id:</span></span>

```azurecli
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="1e3e2-121">Recuperar o modo de exibição de grupo de segurança</span><span class="sxs-lookup"><span data-stu-id="1e3e2-121">Retrieve security group view</span></span>

<span data-ttu-id="1e3e2-122">A próxima etapa é recuperar o resultado de exibição do grupo de segurança.</span><span class="sxs-lookup"><span data-stu-id="1e3e2-122">The next step is to retrieve the security group view result.</span></span> <span data-ttu-id="1e3e2-123">A adição do sinalizador "– json" formatará os resultados em json.</span><span class="sxs-lookup"><span data-stu-id="1e3e2-123">Adding the "--json" flag will format the results in json.</span></span>

```azurecli
azure network watcher security-group-view -g resourceGroupName -n networkWatcherName -t targetResourceId --json
```

## <a name="viewing-the-results"></a><span data-ttu-id="1e3e2-124">Exibição dos resultados</span><span class="sxs-lookup"><span data-stu-id="1e3e2-124">Viewing the results</span></span>

<span data-ttu-id="1e3e2-125">O exemplo a seguir é uma resposta abreviada dos resultados retornados.</span><span class="sxs-lookup"><span data-stu-id="1e3e2-125">The following example is a shortened response of the results returned.</span></span> <span data-ttu-id="1e3e2-126">Os resultados mostram todas as regras de segurança efetiva e aplicados na máquina virtual dividida em grupos de **NetworkInterfaceSecurityRules**, **DefaultSecurityRules** e **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="1e3e2-126">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json
{
  "networkInterfaces": [
    {
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testnic",
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testvm",
          "securityRules": [
            {
              "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/test-nsg/securityRules/default-allow-rdp",
              "protocol": "TCP",
              "sourcePortRange": "*",
              "destinationPortRange": "3389",
              "sourceAddressPrefix": "*",
              "destinationAddressPrefix": "*",
              "access": "Allow",
              "priority": 1000,
              "direction": "Inbound",
              "provisioningState": "Succeeded",
              "name": "default-allow-rdp",
              "etag": "W/\"00000000-0000-0000-0000-000000000000\""
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/networkSecurityGroups//defaultSecurityRules/",
            "description": "Allow inbound traffic from all VMs in VNET",
            "protocol": "*",
            "sourcePortRange": "*",
            "destinationPortRange": "*",
            "sourceAddressPrefix": "VirtualNetwork",
            "destinationAddressPrefix": "VirtualNetwork",
            "access": "Allow",
            "priority": 65000,
            "direction": "Inbound",
            "provisioningState": "Succeeded",
            "name": "AllowVnetInBound"
          }
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="1e3e2-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1e3e2-127">Next steps</span></span>

<span data-ttu-id="1e3e2-128">Visite [auditoria de segurança grupos NSG (rede) com o Observador de Rede](network-watcher-nsg-auditing-powershell.md) para aprender a automatizar a validação dos grupos de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="1e3e2-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) to learn how to automate validation of Network Security Groups.</span></span>

<span data-ttu-id="1e3e2-129">Saiba mais sobre as regras de segurança que são aplicadas aos recursos de rede no artigo [Visão geral de exibição do grupo de segurança](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="1e3e2-129">Learn more about the security rules that are applied to your network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
