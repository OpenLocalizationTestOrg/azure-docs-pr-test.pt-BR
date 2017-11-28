---
title: "segurança de rede aaaAnalyze com exibição de grupo de segurança do Azure rede Inspetor - API REST | Microsoft Docs"
description: "Este artigo descreve como toouse PowerShell tooanalyze um virtual máquinas a segurança com o modo de exibição de grupo de segurança."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a2f418fe-f5d2-43ed-8dc3-df0ed2a4d4ac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 0858a64a9454816e05f06dadb9536ad0c755e90e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-rest-api"></a><span data-ttu-id="b1884-103">Analisar a segurança de sua máquina virtual com o modo de exibição de Grupo de Segurança usando a API REST</span><span class="sxs-lookup"><span data-stu-id="b1884-103">Analyze your Virtual Machine security with Security Group View using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="b1884-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1884-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="b1884-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="b1884-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="b1884-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b1884-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="b1884-107">API REST</span><span class="sxs-lookup"><span data-stu-id="b1884-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="b1884-108">Exibição de grupo de segurança retorna as regras de segurança de rede configurados e eficiente que são aplicadas tooa virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b1884-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="b1884-109">Esse recurso é útil tooaudit e diagnosticar os grupos de segurança de rede e as regras configuradas no tráfego de tooensure VM está sendo corretamente permitido ou negado.</span><span class="sxs-lookup"><span data-stu-id="b1884-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="b1884-110">Neste artigo, mostramos como tooretrieve Olá efetivo e aplicadas a segurança as regras de máquina virtual de tooa usando a API REST</span><span class="sxs-lookup"><span data-stu-id="b1884-110">In this article, we show you how tooretrieve hello effective and applied security rules tooa virtual machine using REST API</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b1884-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="b1884-111">Before you begin</span></span>

<span data-ttu-id="b1884-112">Nesse cenário, você pode chamar exibição de grupo de segurança tooget saudação do hello API de Rest do Inspetor de rede para uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b1884-112">In this scenario, you call hello Network Watcher Rest API tooget hello security group view for a virtual machine.</span></span> <span data-ttu-id="b1884-113">ARMclient é toocall usado Olá REST API usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b1884-113">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="b1884-114">O ARMClient é encontrado no chocolatey em [ARMClient no Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="b1884-114">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="b1884-115">Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.</span><span class="sxs-lookup"><span data-stu-id="b1884-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="b1884-116">cenário de Olá também pressupõe que um grupo de recursos com uma máquina virtual válida existe toobe usado.</span><span class="sxs-lookup"><span data-stu-id="b1884-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="b1884-117">Cenário</span><span class="sxs-lookup"><span data-stu-id="b1884-117">Scenario</span></span>

<span data-ttu-id="b1884-118">cenário de saudação abordado neste artigo recupera regras de segurança efetiva e aplicadas Olá para uma determinada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b1884-118">hello scenario covered in this article retrieves hello effective and applied security rules for a given virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="b1884-119">Fazer logon com o ARMClient</span><span class="sxs-lookup"><span data-stu-id="b1884-119">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="b1884-120">Recuperar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b1884-120">Retrieve a virtual machine</span></span>

<span data-ttu-id="b1884-121">Executar Olá script tooreturn um machineThe virtual a seguir após o código precisa variáveis:</span><span class="sxs-lookup"><span data-stu-id="b1884-121">Run hello following script tooreturn a virtual machineThe following code needs variables:</span></span>

- <span data-ttu-id="b1884-122">**subscriptionId** -id da assinatura Olá também pode ser recuperado com hello **AzureRMSubscription Get** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b1884-122">**subscriptionId** - hello subscription id can also be retrieved with hello **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="b1884-123">**resourceGroupName** - Olá nome de um grupo de recursos que contém máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="b1884-123">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="b1884-124">as informações necessárias Hello são hello **id** em tipo hello `Microsoft.Compute/virtualMachines` em resposta, como visto no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="b1884-124">hello information that is needed is hello **id** under hello type `Microsoft.Compute/virtualMachines` in response, as seen in hello following example:</span></span>

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft
.Network/networkInterfaces/{nicName}"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Com
pute/virtualMachines/{vmName}/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute
/virtualMachines/{vmName}",
      "name": "{vmName}"
    }
  ]
}
```

## <a name="get-security-group-view-for-virtual-machine"></a><span data-ttu-id="b1884-125">Obter a exibição de grupo de segurança para máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b1884-125">Get security group view for virtual machine</span></span>

<span data-ttu-id="b1884-126">Olá exemplo a seguir solicita o modo de exibição do grupo de segurança de saudação de uma máquina virtual alvo.</span><span class="sxs-lookup"><span data-stu-id="b1884-126">hello following example requests hello security group view of a targeted virtual machine.</span></span> <span data-ttu-id="b1884-127">resultados deste exemplo Hello podem ser usado toocompare toohello regras e definido pelo Olá origem toolook há descompasso na configuração de segurança.</span><span class="sxs-lookup"><span data-stu-id="b1884-127">hello results from this example can be used toocompare toohello rules and security defined by hello origination toolook for configuration drift.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.compute/virtualMachine/$vmName

$requestBody = @"
{
    'targetResourceId': '${targetUri}'

}
"@
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/securityGroupView?api-version=2016-12-01" $requestBody -verbose
```

## <a name="view-hello-response"></a><span data-ttu-id="b1884-128">Resposta de saudação do modo de exibição</span><span class="sxs-lookup"><span data-stu-id="b1884-128">View hello response</span></span>

<span data-ttu-id="b1884-129">saudação de exemplo a seguir é resposta Olá retornada de saudação que precedem o comando.</span><span class="sxs-lookup"><span data-stu-id="b1884-129">hello following sample is hello response returned from hello preceding command.</span></span> <span data-ttu-id="b1884-130">Olá resultados mostram todas as regras de segurança efetiva e aplicadas Olá na máquina virtual de saudação dividida em grupos de **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, e  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="b1884-130">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json

{
  "networkInterfaces": [
    {
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
          "securityRules": [
            {
              "name": "default-allow-rdp",
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/securityRules/default-allow-rdp",
              "etag": "W/\"d4c411d4-0d62-49dc-8092-3d4b57825740\"",
              "properties": {
                "provisioningState": "Succeeded",
                "protocol": "TCP",
                "sourcePortRange": "*",
                "destinationPortRange": "3389",
                "sourceAddressPrefix": "*",
                "destinationAddressPrefix": "*",
                "access": "Allow",
                "priority": 1000,
                "direction": "Inbound"
              }
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "name": "AllowVnetInBound",
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/defaultSecurityRules/",
            "properties": {
              "provisioningState": "Succeeded",
              "description": "Allow inbound traffic from all VMs in VNET",
              "protocol": "*",
              "sourcePortRange": "*",
              "destinationPortRange": "*",
              "sourceAddressPrefix": "VirtualNetwork",
              "destinationAddressPrefix": "VirtualNetwork",
              "access": "Allow",
              "priority": 65000,
              "direction": "Inbound"
            }
          },
          ...
        ],
        "effectiveSecurityRules": [
          {
            "name": "DefaultOutboundDenyAll",
            "protocol": "All",
            "sourcePortRange": "0-65535",
            "destinationPortRange": "0-65535",
            "sourceAddressPrefix": "*",
            "destinationAddressPrefix": "*",
            "access": "Deny",
            "priority": 65500,
            "direction": "Outbound"
          },
          ...
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="b1884-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b1884-131">Next steps</span></span>

<span data-ttu-id="b1884-132">Visite [auditoria rede segurança grupos (NSG) com o observador de rede](network-watcher-security-group-view-powershell.md) toolearn como tooautomate validação dos grupos de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="b1884-132">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-security-group-view-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>


