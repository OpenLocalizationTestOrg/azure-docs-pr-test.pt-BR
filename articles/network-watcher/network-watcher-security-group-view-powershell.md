---
title: "segurança de rede aaaAnalyze com exibição de grupo de segurança do Azure rede Inspetor - PowerShell | Microsoft Docs"
description: "Este artigo descreve como toouse PowerShell tooanalyze um virtual máquinas a segurança com o modo de exibição de grupo de segurança."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 04e76b49-6a1b-4d0f-9a9b-51cf2f4df5a2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 5e1990d97899bd8585025ec13dd556ab2e034c3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-powershell"></a><span data-ttu-id="0a4a4-103">Analisar a segurança de máquina Virtual com o modo de exibição de grupo de segurança usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="0a4a4-103">Analyze your Virtual Machine security with Security Group View using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="0a4a4-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0a4a4-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="0a4a4-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0a4a4-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="0a4a4-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0a4a4-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="0a4a4-107">API REST</span><span class="sxs-lookup"><span data-stu-id="0a4a4-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="0a4a4-108">Exibição de grupo de segurança retorna as regras de segurança de rede configurados e eficiente que são aplicadas tooa virtual machine.</span><span class="sxs-lookup"><span data-stu-id="0a4a4-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="0a4a4-109">Esse recurso é útil tooaudit e diagnosticar os grupos de segurança de rede e as regras configuradas no tráfego de tooensure VM está sendo corretamente permitido ou negado.</span><span class="sxs-lookup"><span data-stu-id="0a4a4-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="0a4a4-110">Neste artigo, mostramos como tooretrieve Olá configurada e tooa de regras de segurança efetiva virtual máquina usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="0a4a4-110">In this article, we show you how tooretrieve hello configured and effective security rules tooa virtual machine using PowerShell</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0a4a4-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="0a4a4-111">Before you begin</span></span>

<span data-ttu-id="0a4a4-112">Nesse cenário, você executa Olá `Get-AzureRmNetworkWatcherSecurityGroupView` informações de regra de segurança do cmdlet tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="0a4a4-112">In this scenario, you run hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet tooretrieve hello security rule information.</span></span>

<span data-ttu-id="0a4a4-113">Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.</span><span class="sxs-lookup"><span data-stu-id="0a4a4-113">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="0a4a4-114">Cenário</span><span class="sxs-lookup"><span data-stu-id="0a4a4-114">Scenario</span></span>

<span data-ttu-id="0a4a4-115">cenário de saudação abordado neste artigo recupera hello configurado e regras de segurança efetiva para uma determinada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0a4a4-115">hello scenario covered in this article retrieves hello configured and effective security rules for a given virtual machine.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="0a4a4-116">Recuperar o Observador de Rede</span><span class="sxs-lookup"><span data-stu-id="0a4a4-116">Retrieve Network Watcher</span></span>

<span data-ttu-id="0a4a4-117">Olá primeira etapa é a instância do tooretrieve Olá observador de rede.</span><span class="sxs-lookup"><span data-stu-id="0a4a4-117">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="0a4a4-118">Essa variável é passada toohello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0a4a4-118">This variable is passed toohello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="get-a-vm"></a><span data-ttu-id="0a4a4-119">Obter uma VM</span><span class="sxs-lookup"><span data-stu-id="0a4a4-119">Get a VM</span></span>

<span data-ttu-id="0a4a4-120">Uma máquina virtual é necessário toorun Olá `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet contra.</span><span class="sxs-lookup"><span data-stu-id="0a4a4-120">A virtual machine is required toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="0a4a4-121">saudação de exemplo a seguir obtém um objeto da VM.</span><span class="sxs-lookup"><span data-stu-id="0a4a4-121">hello following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName testrg -Name testvm1
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="0a4a4-122">Recuperar o modo de exibição de grupo de segurança</span><span class="sxs-lookup"><span data-stu-id="0a4a4-122">Retrieve security group view</span></span>

<span data-ttu-id="0a4a4-123">Olá próxima etapa é o resultado de exibição de grupo de segurança do tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="0a4a4-123">hello next step is tooretrieve hello security group view result.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="viewing-hello-results"></a><span data-ttu-id="0a4a4-124">Exibindo resultados de saudação</span><span class="sxs-lookup"><span data-stu-id="0a4a4-124">Viewing hello results</span></span>

<span data-ttu-id="0a4a4-125">Olá, exemplo a seguir é uma resposta reduzida de saudação resultados retornados.</span><span class="sxs-lookup"><span data-stu-id="0a4a4-125">hello following example is a shortened response of hello results returned.</span></span> <span data-ttu-id="0a4a4-126">Olá resultados mostram todas as regras de segurança efetiva e aplicadas Olá na máquina virtual de saudação dividida em grupos de **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, e  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="0a4a4-126">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```
NetworkInterfaces : [
                      {
                        "NetworkInterfaceSecurityRules": [
                          {
                            "Name": "default-allow-rdp",
                            "Etag": "W/\"d4c411d4-0d62-49dc-8092-3d4b57825740\"",
                            "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg2/providers/Microsoft.Network/networkSecurityGroups/testvm2-nsg/securityRules/default-allow-rdp",
                            "Protocol": "TCP",
                            "SourcePortRange": "*",
                            "DestinationPortRange": "3389",
                            "SourceAddressPrefix": "*",
                            "DestinationAddressPrefix": "*",
                            "Access": "Allow",
                            "Priority": 1000,
                            "Direction": "Inbound",
                            "ProvisioningState": "Succeeded"
                          }
                          ...
                        ],
                        "DefaultSecurityRules": [
                          {
                            "Name": "AllowVnetInBound",
                            "Id": "/subscriptions00000000-0000-0000-0000-000000000000/resourceGroups/testrg2/providers/Microsoft.Network/networkSecurityGroups/testvm2-nsg/defaultSecurityRules/",
                            "Description": "Allow inbound traffic from all VMs in VNET",
                            "Protocol": "*",
                            "SourcePortRange": "*",
                            "DestinationPortRange": "*",
                            "SourceAddressPrefix": "VirtualNetwork",
                            "DestinationAddressPrefix": "VirtualNetwork",
                            "Access": "Allow",
                            "Priority": 65000,
                            "Direction": "Inbound",
                            "ProvisioningState": "Succeeded"
                          }
                          ...
                        ],
                        "EffectiveSecurityRules": [
                          {
                            "Name": "DefaultOutboundDenyAll",
                            "Protocol": "All",
                            "SourcePortRange": "0-65535",
                            "DestinationPortRange": "0-65535",
                            "SourceAddressPrefix": "*",
                            "DestinationAddressPrefix": "*",
                            "ExpandedSourceAddressPrefix": [],
                            "ExpandedDestinationAddressPrefix": [],
                            "Access": "Deny",
                            "Priority": 65500,
                            "Direction": "Outbound"
                          },
                          ...
                        ]
                      }
                    ]
```

## <a name="next-steps"></a><span data-ttu-id="0a4a4-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0a4a4-127">Next steps</span></span>

<span data-ttu-id="0a4a4-128">Visite [auditoria rede segurança grupos (NSG) com o observador de rede](network-watcher-nsg-auditing-powershell.md) toolearn como tooautomate validação dos grupos de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="0a4a4-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>


