---
title: "Analisar a segurança de rede com exibição de grupo de segurança do Observador de Rede do Azure - API REST | Microsoft Docs"
description: "Este artigo descreve como usar o PowerShell para analisar a segurança de uma máquina virtual com o modo de exibição de Grupo de Segurança."
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
ms.openlocfilehash: afced52b3ae6f3b7f400364f5ec7d049aa166590
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-rest-api"></a><span data-ttu-id="5217f-103">Analisar a segurança de sua máquina virtual com o modo de exibição de Grupo de Segurança usando a API REST</span><span class="sxs-lookup"><span data-stu-id="5217f-103">Analyze your Virtual Machine security with Security Group View using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="5217f-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5217f-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="5217f-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5217f-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="5217f-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5217f-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="5217f-107">API REST</span><span class="sxs-lookup"><span data-stu-id="5217f-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="5217f-108">Exibição de grupo de segurança retorna as regras de segurança de rede configurados e eficaz que são aplicadas a uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5217f-108">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span></span> <span data-ttu-id="5217f-109">Esse recurso é útil para auditoria e diagnosticar grupos de segurança de rede e as regras configuradas em uma VM para garantir que o tráfego está sendo corretamente permitido ou negado.</span><span class="sxs-lookup"><span data-stu-id="5217f-109">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="5217f-110">Neste artigo, mostraremos como recuperar as regras de segurança efetivas e aplicadas para uma máquina virtual usando a API REST</span><span class="sxs-lookup"><span data-stu-id="5217f-110">In this article, we show you how to retrieve the effective and applied security rules to a virtual machine using REST API</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5217f-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="5217f-111">Before you begin</span></span>

<span data-ttu-id="5217f-112">Nesse cenário, chame a API Rest do Observador de Rede para obter o modo de exibição do grupo de segurança de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5217f-112">In this scenario, you call the Network Watcher Rest API to get the security group view for a virtual machine.</span></span> <span data-ttu-id="5217f-113">O ARMclient é usado para chamar a API REST usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5217f-113">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="5217f-114">O ARMClient é encontrado no chocolatey em [ARMClient no Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="5217f-114">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="5217f-115">Este cenário pressupõe que você seguiu as etapas em [Criação de um Observador de Rede](network-watcher-create.md) para criar um Observador de Rede.</span><span class="sxs-lookup"><span data-stu-id="5217f-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="5217f-116">O cenário também pressupõe que exista um grupo de recursos com uma máquina virtual válida a ser usada.</span><span class="sxs-lookup"><span data-stu-id="5217f-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="5217f-117">Cenário</span><span class="sxs-lookup"><span data-stu-id="5217f-117">Scenario</span></span>

<span data-ttu-id="5217f-118">O cenário abordado neste artigo recupera as regras de segurança efetivas e aplicadas para uma determinada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5217f-118">The scenario covered in this article retrieves the effective and applied security rules for a given virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="5217f-119">Faça logon com o ARMClient</span><span class="sxs-lookup"><span data-stu-id="5217f-119">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="5217f-120">Recuperar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="5217f-120">Retrieve a virtual machine</span></span>

<span data-ttu-id="5217f-121">Execute o script a seguir para retornar uma máquina virtual. O código a seguir precisa de variáveis:</span><span class="sxs-lookup"><span data-stu-id="5217f-121">Run the following script to return a virtual machineThe following code needs variables:</span></span>

- <span data-ttu-id="5217f-122">**subscriptionId** - a id da assinatura também pode ser recuperada com o cmdlet **Get-AzureRMSubscription**.</span><span class="sxs-lookup"><span data-stu-id="5217f-122">**subscriptionId** - The subscription id can also be retrieved with the **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="5217f-123">**resourceGroupName** - o nome de um grupo de recursos que contém as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="5217f-123">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="5217f-124">As informações necessárias são a **id** no tipo `Microsoft.Compute/virtualMachines` na resposta, conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="5217f-124">The information that is needed is the **id** under the type `Microsoft.Compute/virtualMachines` in response, as seen in the following example:</span></span>

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

## <a name="get-security-group-view-for-virtual-machine"></a><span data-ttu-id="5217f-125">Obter a exibição de grupo de segurança para máquina virtual</span><span class="sxs-lookup"><span data-stu-id="5217f-125">Get security group view for virtual machine</span></span>

<span data-ttu-id="5217f-126">O exemplo a seguir solicita a exibição do grupo de segurança de uma máquina virtual de destino.</span><span class="sxs-lookup"><span data-stu-id="5217f-126">The following example requests the security group view of a targeted virtual machine.</span></span> <span data-ttu-id="5217f-127">Os resultados desse exemplo podem ser usados para comparar as regras e segurança definidas pela origem a fim de procurar os descompassos de configuração.</span><span class="sxs-lookup"><span data-stu-id="5217f-127">The results from this example can be used to compare to the rules and security defined by the origination to look for configuration drift.</span></span>

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

## <a name="view-the-response"></a><span data-ttu-id="5217f-128">Exibir a resposta</span><span class="sxs-lookup"><span data-stu-id="5217f-128">View the response</span></span>

<span data-ttu-id="5217f-129">O exemplo a seguir é a resposta retornada do comando anterior.</span><span class="sxs-lookup"><span data-stu-id="5217f-129">The following sample is the response returned from the preceding command.</span></span> <span data-ttu-id="5217f-130">Os resultados mostram todas as regras de segurança efetiva e aplicados na máquina virtual dividida em grupos de **NetworkInterfaceSecurityRules**, **DefaultSecurityRules** e **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="5217f-130">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5217f-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5217f-131">Next steps</span></span>

<span data-ttu-id="5217f-132">Visite [auditoria de segurança grupos NSG (rede) com o Observador de Rede](network-watcher-security-group-view-powershell.md) para aprender a automatizar a validação dos grupos de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="5217f-132">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-security-group-view-powershell.md) to learn how to automate validation of Network Security Groups.</span></span>


