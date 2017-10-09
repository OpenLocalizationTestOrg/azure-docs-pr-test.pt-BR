---
title: "segurança de rede aaaAnalyze com exibição de grupo de segurança do Azure rede Inspetor - 1.0 da CLI do Azure | Microsoft Docs"
description: "Este artigo descreve como tooanalyze toouse 1.0 da CLI do Azure a virtual máquinas a segurança com o modo de exibição de grupo de segurança."
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
ms.openlocfilehash: 96383a734b94d215d5b0f3d47339e46940d700b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-10"></a><span data-ttu-id="86841-103">Analisar a segurança de máquina Virtual com o modo de exibição de grupo de segurança usando a CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="86841-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="86841-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="86841-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="86841-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="86841-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="86841-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="86841-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="86841-107">API REST</span><span class="sxs-lookup"><span data-stu-id="86841-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="86841-108">Exibição de grupo de segurança retorna as regras de segurança de rede configurados e eficiente que são aplicadas tooa virtual machine.</span><span class="sxs-lookup"><span data-stu-id="86841-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="86841-109">Esse recurso é útil tooaudit e diagnosticar os grupos de segurança de rede e as regras configuradas no tráfego de tooensure VM está sendo corretamente permitido ou negado.</span><span class="sxs-lookup"><span data-stu-id="86841-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="86841-110">Neste artigo, mostramos como tooretrieve Olá configurada e segurança efetiva regras tooa VM usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="86841-110">In this article, we show you how tooretrieve hello configured and effective security rules tooa virtual machine using Azure CLI</span></span>

<span data-ttu-id="86841-111">Este artigo usa a CLI 1.0 do Azure para plataforma cruzada, que está disponível para Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="86841-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="86841-112">Atualmente, o Observador de Rede usa a CLI 1.0 do Azure para dar suporte à CLI.</span><span class="sxs-lookup"><span data-stu-id="86841-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="86841-113">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="86841-113">Before you begin</span></span>

<span data-ttu-id="86841-114">Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.</span><span class="sxs-lookup"><span data-stu-id="86841-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="86841-115">Cenário</span><span class="sxs-lookup"><span data-stu-id="86841-115">Scenario</span></span>

<span data-ttu-id="86841-116">cenário de saudação abordado neste artigo recupera hello configurado e regras de segurança efetiva para uma determinada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="86841-116">hello scenario covered in this article retrieves hello configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="86841-117">Obter uma VM</span><span class="sxs-lookup"><span data-stu-id="86841-117">Get a VM</span></span>

<span data-ttu-id="86841-118">Uma máquina virtual é necessário toorun Olá `vm list` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="86841-118">A virtual machine is required toorun hello `vm list` cmdlet.</span></span> <span data-ttu-id="86841-119">Olá comando a seguir lista machinese de saudação virtual em um grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="86841-119">hello following command lists hello virtual machinese in a resource group:</span></span>

```azurecli
azure vm list -g resourceGroupName
```

<span data-ttu-id="86841-120">Quando você souber a máquina virtual de saudação, você pode usar Olá `vm show` cmdlet tooget sua Id de recurso:</span><span class="sxs-lookup"><span data-stu-id="86841-120">Once you know hello virtual machine, you can use hello `vm show` cmdlet tooget its resource Id:</span></span>

```azurecli
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="86841-121">Recuperar o modo de exibição de grupo de segurança</span><span class="sxs-lookup"><span data-stu-id="86841-121">Retrieve security group view</span></span>

<span data-ttu-id="86841-122">Olá próxima etapa é o resultado de exibição de grupo de segurança do tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="86841-122">hello next step is tooretrieve hello security group view result.</span></span> <span data-ttu-id="86841-123">Adicionando hello "– json" Sinalizador formatará os resultados de saudação em json.</span><span class="sxs-lookup"><span data-stu-id="86841-123">Adding hello "--json" flag will format hello results in json.</span></span>

```azurecli
azure network watcher security-group-view -g resourceGroupName -n networkWatcherName -t targetResourceId --json
```

## <a name="viewing-hello-results"></a><span data-ttu-id="86841-124">Exibindo resultados de saudação</span><span class="sxs-lookup"><span data-stu-id="86841-124">Viewing hello results</span></span>

<span data-ttu-id="86841-125">Olá, exemplo a seguir é uma resposta reduzida de saudação resultados retornados.</span><span class="sxs-lookup"><span data-stu-id="86841-125">hello following example is a shortened response of hello results returned.</span></span> <span data-ttu-id="86841-126">Olá resultados mostram todas as regras de segurança efetiva e aplicadas Olá na máquina virtual de saudação dividida em grupos de **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, e  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="86841-126">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="86841-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="86841-127">Next steps</span></span>

<span data-ttu-id="86841-128">Visite [auditoria rede segurança grupos (NSG) com o observador de rede](network-watcher-nsg-auditing-powershell.md) toolearn como tooautomate validação dos grupos de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="86841-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>

<span data-ttu-id="86841-129">Saiba mais sobre as regras de segurança de saudação que são recursos de rede aplicada tooyour visitando [visão geral de exibição de grupo de segurança](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="86841-129">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
