---
title: "Automatizar a auditoria do NSG com a exibição de grupo de segurança do Observador de Rede do Azure | Microsoft Docs"
description: "Esta página fornece instruções sobre como configurar a auditoria de um Grupo de Segurança de Rede"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 78a01bcf-74fe-402a-9812-285f3501f877
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a91da330e677c85f16f6f4e506613576b6507d7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="automate-nsg-auditing-with-azure-network-watcher-security-group-view"></a><span data-ttu-id="fe81b-103">Automatizar a auditoria do NSG com a exibição de grupo de segurança do Observador de Rede do Azure</span><span class="sxs-lookup"><span data-stu-id="fe81b-103">Automate NSG auditing with Azure Network Watcher Security group view</span></span>

<span data-ttu-id="fe81b-104">Os clientes normalmente enfrentam o desafio de verificar a postura de segurança de sua infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="fe81b-104">Customers are often faced with the challenge of verifying the security posture of their infrastructure.</span></span> <span data-ttu-id="fe81b-105">Esse desafio não é diferente para as VMs no Azure.</span><span class="sxs-lookup"><span data-stu-id="fe81b-105">This challenge is no different for their VMs in Azure.</span></span> <span data-ttu-id="fe81b-106">É importante ter um perfil de segurança semelhante com base nas regras do NSG (Grupo de Segurança de Rede) aplicadas.</span><span class="sxs-lookup"><span data-stu-id="fe81b-106">It is important to have a similar security profile based on the Network Security Group (NSG) rules applied.</span></span> <span data-ttu-id="fe81b-107">Com a exibição do Grupo de segurança, agora você pode obter a lista de regras aplicadas a uma VM dentro de um NSG.</span><span class="sxs-lookup"><span data-stu-id="fe81b-107">Using the Security Group View, you can now get the list of rules applied to a VM within an NSG.</span></span> <span data-ttu-id="fe81b-108">Você pode definir um perfil de ouro de segurança do NSG e iniciar a Exibição do grupo de segurança com uma cadência semanal e comparar a saída para o perfil de ouro e criar um relatório.</span><span class="sxs-lookup"><span data-stu-id="fe81b-108">You can define a golden NSG security profile and initiate Security Group View on a weekly cadence and compare the output to the golden profile and create a report.</span></span> <span data-ttu-id="fe81b-109">Dessa forma, você pode identificar com facilidade todas as VMs que não estão de acordo com o perfil de segurança recomendado.</span><span class="sxs-lookup"><span data-stu-id="fe81b-109">This way you can identify with ease all the VMs that do not conform to the prescribed security profile.</span></span>

<span data-ttu-id="fe81b-110">Se você estiver familiarizado com os Grupos de segurança de rede, visite [Visão geral de segurança de rede](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="fe81b-110">If you are unfamiliar with Network Security Groups, visit [Network Security Overview](../virtual-network/virtual-networks-nsg.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="fe81b-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="fe81b-111">Before you begin</span></span>

<span data-ttu-id="fe81b-112">Nesse cenário, você compara uma linha de base válida com os resultados da exibição do grupo de segurança retornados para uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fe81b-112">In this scenario, you compare a known good baseline to the security group view results returned for a virtual machine.</span></span>

<span data-ttu-id="fe81b-113">Este cenário pressupõe que você seguiu as etapas em [Criação de um Observador de Rede](network-watcher-create.md) para criar um Observador de Rede.</span><span class="sxs-lookup"><span data-stu-id="fe81b-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="fe81b-114">O cenário também pressupõe que exista um grupo de recursos com uma máquina virtual válida a ser usada.</span><span class="sxs-lookup"><span data-stu-id="fe81b-114">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="fe81b-115">Cenário</span><span class="sxs-lookup"><span data-stu-id="fe81b-115">Scenario</span></span>

<span data-ttu-id="fe81b-116">O cenário abordado neste artigo obtém a exibição do grupo de segurança de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fe81b-116">The scenario covered in this article gets the security group view for a virtual machine.</span></span>

<span data-ttu-id="fe81b-117">Neste cenário, você:</span><span class="sxs-lookup"><span data-stu-id="fe81b-117">In this scenario, you will:</span></span>

- <span data-ttu-id="fe81b-118">Recuperar um conjunto de regras válido</span><span class="sxs-lookup"><span data-stu-id="fe81b-118">Retrieve a known good rule set</span></span>
- <span data-ttu-id="fe81b-119">Recuperar uma máquina virtual com API Rest</span><span class="sxs-lookup"><span data-stu-id="fe81b-119">Retrieve a virtual machine with Rest API</span></span>
- <span data-ttu-id="fe81b-120">Obter a exibição de grupo de segurança para máquina virtual</span><span class="sxs-lookup"><span data-stu-id="fe81b-120">Get security group view for virtual machine</span></span>
- <span data-ttu-id="fe81b-121">Avaliar a resposta</span><span class="sxs-lookup"><span data-stu-id="fe81b-121">Evaluate Response</span></span>

## <a name="retrieve-rule-set"></a><span data-ttu-id="fe81b-122">Recuperar o conjunto de regras</span><span class="sxs-lookup"><span data-stu-id="fe81b-122">Retrieve rule set</span></span>

<span data-ttu-id="fe81b-123">A primeira etapa neste exemplo é trabalhar com uma linha de base existente.</span><span class="sxs-lookup"><span data-stu-id="fe81b-123">The first step in this example is to work with an existing baseline.</span></span> <span data-ttu-id="fe81b-124">O exemplo a seguir é um json extraído de um Grupo de Segurança de Rede existente usando o cmdlet `Get-AzureRmNetworkSecurityGroup`, que é usado como a linha de base para este exemplo.</span><span class="sxs-lookup"><span data-stu-id="fe81b-124">The following example is some json extracted from an existing Network Security Group using the `Get-AzureRmNetworkSecurityGroup` cmdlet that is used as the baseline for this example.</span></span>

```json
[
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "3389",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1000,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "default-allow-rdp",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/default-allow-rdp"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "111",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1010,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "MyRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/MyRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "112",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1020,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "My2ndRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/My2ndRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "5672",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Deny",
        "Priority":  1030,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "ThisRuleNeedsToStay",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/ThisRuleNeedsToStay"
    }
]
```

## <a name="convert-rule-set-to-powershell-objects"></a><span data-ttu-id="fe81b-125">Converter o conjunto de regras em objetos do PowerShell</span><span class="sxs-lookup"><span data-stu-id="fe81b-125">Convert rule set to PowerShell objects</span></span>

<span data-ttu-id="fe81b-126">Nesta etapa, lemos um arquivo json criado anteriormente com as regras que devem estar no Grupo de Segurança de Rede para este exemplo.</span><span class="sxs-lookup"><span data-stu-id="fe81b-126">In this step, we are reading a json file that was created earlier with the rules that are expected to be on the Network Security Group for this example.</span></span>

```powershell
$nsgbaserules = Get-Content -Path C:\temp\testvm1-nsg.json | ConvertFrom-Json
```

## <a name="retrieve-network-watcher"></a><span data-ttu-id="fe81b-127">Recuperar o Observador de Rede</span><span class="sxs-lookup"><span data-stu-id="fe81b-127">Retrieve Network Watcher</span></span>

<span data-ttu-id="fe81b-128">A próxima etapa é recuperar a instância do Observador de Rede.</span><span class="sxs-lookup"><span data-stu-id="fe81b-128">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="fe81b-129">A variável `$networkWatcher` é passada para o cmdlet `AzureRmNetworkWatcherSecurityGroupView`.</span><span class="sxs-lookup"><span data-stu-id="fe81b-129">The `$networkWatcher` variable is passed to the `AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="fe81b-130">Obter uma VM</span><span class="sxs-lookup"><span data-stu-id="fe81b-130">Get a VM</span></span>

<span data-ttu-id="fe81b-131">Uma máquina virtual é necessária para executar o cmdlet `Get-AzureRmNetworkWatcherSecurityGroupView`.</span><span class="sxs-lookup"><span data-stu-id="fe81b-131">A virtual machine is required to run the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="fe81b-132">O exemplo a seguir obtém um objeto de VM.</span><span class="sxs-lookup"><span data-stu-id="fe81b-132">The following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="fe81b-133">Recuperar o modo de exibição de grupo de segurança</span><span class="sxs-lookup"><span data-stu-id="fe81b-133">Retrieve security group view</span></span>

<span data-ttu-id="fe81b-134">A próxima etapa é recuperar o resultado de exibição do grupo de segurança.</span><span class="sxs-lookup"><span data-stu-id="fe81b-134">The next step is to retrieve the security group view result.</span></span> <span data-ttu-id="fe81b-135">Esse resultado é comparado com o json de "linha de base" mostrado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fe81b-135">This result is compared to the "baseline" json that was shown earlier.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="analyzing-the-results"></a><span data-ttu-id="fe81b-136">Analisar os resultados</span><span class="sxs-lookup"><span data-stu-id="fe81b-136">Analyzing the results</span></span>

<span data-ttu-id="fe81b-137">A resposta é agrupada por interfaces de rede.</span><span class="sxs-lookup"><span data-stu-id="fe81b-137">The response is grouped by Network interfaces.</span></span> <span data-ttu-id="fe81b-138">Os diferentes tipos de regras retornados são regras de segurança padrão e eficazes.</span><span class="sxs-lookup"><span data-stu-id="fe81b-138">The different types of rules returned are effective and default security rules.</span></span> <span data-ttu-id="fe81b-139">O resultado é dividido pela forma de aplicação, em uma sub-rede ou uma NIC virtual.</span><span class="sxs-lookup"><span data-stu-id="fe81b-139">The result is further broken down by how it is applied, either on a subnet or a virtual NIC.</span></span>

<span data-ttu-id="fe81b-140">O script PowerShell a seguir compara os resultados da Exibição de grupo de segurança para uma saída existente de um NSG.</span><span class="sxs-lookup"><span data-stu-id="fe81b-140">The following PowerShell script compares the results of the Security Group View to an existing output of an NSG.</span></span> <span data-ttu-id="fe81b-141">O exemplo a seguir é um exemplo simples de como os resultados podem ser comparados com o cmdlet `Compare-Object`.</span><span class="sxs-lookup"><span data-stu-id="fe81b-141">The following example is a simple example of how the results can be compared with `Compare-Object` cmdlet.</span></span>

```powershell
Compare-Object -ReferenceObject $nsgbaserules `
-DifferenceObject $secgroup.NetworkInterfaces[0].NetworkInterfaceSecurityRules `
-Property Name,Description,Protocol,SourcePortRange,DestinationPortRange,SourceAddressPrefix,DestinationAddressPrefix,Access,Priority,Direction
```

<span data-ttu-id="fe81b-142">O exemplo a seguir é o resultado.</span><span class="sxs-lookup"><span data-stu-id="fe81b-142">The following example is the result.</span></span> <span data-ttu-id="fe81b-143">Você pode ver que duas das regras que estavam no primeiro conjunto de regras não estavam presentes na comparação.</span><span class="sxs-lookup"><span data-stu-id="fe81b-143">You can see two of the rules that were in the first rule set were not present in the comparison.</span></span>

```
Name                     : My2ndRuleDoNotDelete
Description              : 
Protocol                 : *
SourcePortRange          : *
DestinationPortRange     : 112
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Allow
Priority                 : 1020
Direction                : Inbound
SideIndicator            : <=

Name                     : ThisRuleNeedsToStay
Description              : 
Protocol                 : TCP
SourcePortRange          : *
DestinationPortRange     : 5672
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Deny
Priority                 : 1030
Direction                : Inbound
SideIndicator            : <=
```

## <a name="next-steps"></a><span data-ttu-id="fe81b-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fe81b-144">Next steps</span></span>

<span data-ttu-id="fe81b-145">Se as configurações foram alteradas, confira [Gerenciar grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) para rastrear as regras de segurança e o Grupo de Segurança de Rede que estão em questão.</span><span class="sxs-lookup"><span data-stu-id="fe81b-145">If settings have been changed, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are in question.</span></span>













