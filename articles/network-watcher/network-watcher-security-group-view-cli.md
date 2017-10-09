---
title: "segurança de rede aaaAnalyze com exibição de grupo de segurança do Azure rede Inspetor - 2.0 do CLI do Azure | Microsoft Docs"
description: "Este artigo descreve como tooanalyze toouse 2.0 do CLI do Azure a virtual máquinas a segurança com o modo de exibição de grupo de segurança."
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
ms.openlocfilehash: 31a4cd628f54d7548f495251fd275f099e79a060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-20"></a><span data-ttu-id="8bbab-103">Analisar a segurança de máquina Virtual com o modo de exibição de grupo de segurança usando a CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="8bbab-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="8bbab-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8bbab-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="8bbab-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8bbab-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="8bbab-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8bbab-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="8bbab-107">API REST</span><span class="sxs-lookup"><span data-stu-id="8bbab-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="8bbab-108">Exibição de grupo de segurança retorna as regras de segurança de rede configurados e eficiente que são aplicadas tooa virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8bbab-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="8bbab-109">Esse recurso é útil tooaudit e diagnosticar os grupos de segurança de rede e as regras configuradas no tráfego de tooensure VM está sendo corretamente permitido ou negado.</span><span class="sxs-lookup"><span data-stu-id="8bbab-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="8bbab-110">Neste artigo, mostramos como tooretrieve Olá configurada e segurança efetiva regras tooa VM usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="8bbab-110">In this article, we show you how tooretrieve hello configured and effective security rules tooa virtual machine using Azure CLI</span></span>


<span data-ttu-id="8bbab-111">Este artigo usa nossa próxima geração CLI para o modelo de implantação de gerenciamento de recursos do hello, 2.0 do CLI do Azure, que está disponível para Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="8bbab-111">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="8bbab-112">Olá tooperform as etapas neste artigo, é necessário muito[instalar Olá Interface de linha de comando do Azure para Mac, Linux e Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="8bbab-112">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8bbab-113">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="8bbab-113">Before you begin</span></span>

<span data-ttu-id="8bbab-114">Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.</span><span class="sxs-lookup"><span data-stu-id="8bbab-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="8bbab-115">Cenário</span><span class="sxs-lookup"><span data-stu-id="8bbab-115">Scenario</span></span>

<span data-ttu-id="8bbab-116">cenário de saudação abordado neste artigo recupera hello configurado e regras de segurança efetiva para uma determinada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8bbab-116">hello scenario covered in this article retrieves hello configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="8bbab-117">Obter uma VM</span><span class="sxs-lookup"><span data-stu-id="8bbab-117">Get a VM</span></span>

<span data-ttu-id="8bbab-118">Uma máquina virtual é necessário toorun Olá `vm list` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8bbab-118">A virtual machine is required toorun hello `vm list` cmdlet.</span></span> <span data-ttu-id="8bbab-119">Olá comando a seguir lista Olá VMs em um grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="8bbab-119">hello following command lists hello virtual machines in a resource group:</span></span>

```azurecli
az vm list -resource-group resourceGroupName
```

<span data-ttu-id="8bbab-120">Quando você souber a máquina virtual de saudação, você pode usar Olá `vm show` cmdlet tooget sua Id de recurso:</span><span class="sxs-lookup"><span data-stu-id="8bbab-120">Once you know hello virtual machine, you can use hello `vm show` cmdlet tooget its resource Id:</span></span>

```azurecli
az vm show -resource-group resourceGroupName -name virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="8bbab-121">Recuperar o modo de exibição de grupo de segurança</span><span class="sxs-lookup"><span data-stu-id="8bbab-121">Retrieve security group view</span></span>

<span data-ttu-id="8bbab-122">Olá próxima etapa é o resultado de exibição de grupo de segurança do tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="8bbab-122">hello next step is tooretrieve hello security group view result.</span></span>

```azurecli
az network watcher show-security-group-view --resource-group resourceGroupName --vm vmName
```

## <a name="viewing-hello-results"></a><span data-ttu-id="8bbab-123">Exibindo resultados de saudação</span><span class="sxs-lookup"><span data-stu-id="8bbab-123">Viewing hello results</span></span>

<span data-ttu-id="8bbab-124">Olá, exemplo a seguir é uma resposta reduzida de saudação resultados retornados.</span><span class="sxs-lookup"><span data-stu-id="8bbab-124">hello following example is a shortened response of hello results returned.</span></span> <span data-ttu-id="8bbab-125">Olá resultados mostram todas as regras de segurança efetiva e aplicadas Olá na máquina virtual de saudação dividida em grupos de **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, e  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="8bbab-125">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json
{
  "networkInterfaces": [
    {
      "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
      "resourceGroup": "{resourceGroupName}",
      "securityRuleAssociations": {
        "defaultSecurityRules": [
          {
            "access": "Allow",
            "description": "Allow inbound traffic from all VMs in VNET",
            "destinationAddressPrefix": "VirtualNetwork",
            "destinationPortRange": "*",
            "direction": "Inbound",
            "etag": null,
            "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups//providers/Microsoft.Network/networkSecurityGroups/{nsgName}/defaultSecurityRules/AllowVnetInBound",
            "name": "AllowVnetInBound",
            "priority": 65000,
            "protocol": "*",
            "provisioningState": "Succeeded",
            "resourceGroup": "",
            "sourceAddressPrefix": "VirtualNetwork",
            "sourcePortRange": "*"
          }...
        ],
        "effectiveSecurityRules": [
          {
            "access": "Deny",
            "destinationAddressPrefix": "*",
            "destinationPortRange": "0-65535",
            "direction": "Outbound",
            "expandedDestinationAddressPrefix": null,
            "expandedSourceAddressPrefix": null,
            "name": "DefaultOutboundDenyAll",
            "priority": 65500,
            "protocol": "All",
            "sourceAddressPrefix": "*",
            "sourcePortRange": "0-65535"
          },
          {
            "access": "Allow",
            "destinationAddressPrefix": "VirtualNetwork",
            "destinationPortRange": "0-65535",
            "direction": "Outbound",
            "expandedDestinationAddressPrefix": [
              "10.1.0.0/24",
              "168.63.129.16/32"
            ],
            "expandedSourceAddressPrefix": [
              "10.1.0.0/24",
              "168.63.129.16/32"
            ],
            "name": "DefaultRule_AllowVnetOutBound",
            "priority": 65000,
            "protocol": "All",
            "sourceAddressPrefix": "VirtualNetwork",
            "sourcePortRange": "0-65535"
          },...
        ],
        "networkInterfaceAssociation": {
          "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
          "resourceGroup": "{resourceGroupName}",
          "securityRules": [
            {
              "access": "Allow",
              "description": null,
              "destinationAddressPrefix": "*",
              "destinationPortRange": "3389",
              "direction": "Inbound",
              "etag": "W/\"efb606c1-2d54-475a-ab20-da3f80393577\"",
              "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/securityRules/default-allow-rdp",
              "name": "default-allow-rdp",
              "priority": 1000,
              "protocol": "TCP",
              "provisioningState": "Succeeded",
              "resourceGroup": "{resourceGroupName}",
              "sourceAddressPrefix": "*",
              "sourcePortRange": "*"
            }
          ]
        },
        "subnetAssociation": null
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="8bbab-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8bbab-126">Next steps</span></span>

<span data-ttu-id="8bbab-127">Visite [auditoria rede segurança grupos (NSG) com o observador de rede](network-watcher-nsg-auditing-powershell.md) toolearn como tooautomate validação dos grupos de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="8bbab-127">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>

<span data-ttu-id="8bbab-128">Saiba mais sobre as regras de segurança de saudação que são recursos de rede aplicada tooyour visitando [visão geral de exibição de grupo de segurança](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="8bbab-128">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
