---
title: "aaaAutomate NSG auditoria com o modo de exibição de grupo de segurança do Inspetor de rede do Azure | Microsoft Docs"
description: "Esta página fornece instruções sobre como tooconfigure a auditoria de um grupo de segurança de rede"
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
ms.openlocfilehash: 24fc418c433fceaf55a74b7c3b0e354dc46c8729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-nsg-auditing-with-azure-network-watcher-security-group-view"></a><span data-ttu-id="2aa05-103">Automatizar a auditoria do NSG com a exibição de grupo de segurança do Observador de Rede do Azure</span><span class="sxs-lookup"><span data-stu-id="2aa05-103">Automate NSG auditing with Azure Network Watcher Security group view</span></span>

<span data-ttu-id="2aa05-104">Os clientes são geralmente enfrentam Olá verificar postura de segurança de saudação da infra-estrutura.</span><span class="sxs-lookup"><span data-stu-id="2aa05-104">Customers are often faced with hello challenge of verifying hello security posture of their infrastructure.</span></span> <span data-ttu-id="2aa05-105">Esse desafio não é diferente para as VMs no Azure.</span><span class="sxs-lookup"><span data-stu-id="2aa05-105">This challenge is no different for their VMs in Azure.</span></span> <span data-ttu-id="2aa05-106">É importante toohave um perfil de segurança semelhante com base nas regras de grupo de segurança de rede (NSG) de saudação aplicadas.</span><span class="sxs-lookup"><span data-stu-id="2aa05-106">It is important toohave a similar security profile based on hello Network Security Group (NSG) rules applied.</span></span> <span data-ttu-id="2aa05-107">Usando Olá exibição de grupo de segurança, agora você pode obter lista de saudação de regras aplicadas tooa VM dentro de um NSG.</span><span class="sxs-lookup"><span data-stu-id="2aa05-107">Using hello Security Group View, you can now get hello list of rules applied tooa VM within an NSG.</span></span> <span data-ttu-id="2aa05-108">Você pode definir um perfil de segurança NSG dourado e iniciar o modo de exibição de grupo de segurança em um ritmo semanal e comparar Olá saída toohello dourada perfil e criar um relatório.</span><span class="sxs-lookup"><span data-stu-id="2aa05-108">You can define a golden NSG security profile and initiate Security Group View on a weekly cadence and compare hello output toohello golden profile and create a report.</span></span> <span data-ttu-id="2aa05-109">Dessa forma você pode identificar com facilidade todas as VMs de saudação que não são compatíveis toohello prescrita perfil de segurança.</span><span class="sxs-lookup"><span data-stu-id="2aa05-109">This way you can identify with ease all hello VMs that do not conform toohello prescribed security profile.</span></span>

<span data-ttu-id="2aa05-110">Se você estiver familiarizado com os Grupos de segurança de rede, visite [Visão geral de segurança de rede](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="2aa05-110">If you are unfamiliar with Network Security Groups, visit [Network Security Overview](../virtual-network/virtual-networks-nsg.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2aa05-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="2aa05-111">Before you begin</span></span>

<span data-ttu-id="2aa05-112">Nesse cenário, você comparar a um grupo de segurança conhecidos boa linha de base toohello exibir os resultados retornados para uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2aa05-112">In this scenario, you compare a known good baseline toohello security group view results returned for a virtual machine.</span></span>

<span data-ttu-id="2aa05-113">Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.</span><span class="sxs-lookup"><span data-stu-id="2aa05-113">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="2aa05-114">cenário de Olá também pressupõe que um grupo de recursos com uma máquina virtual válida existe toobe usado.</span><span class="sxs-lookup"><span data-stu-id="2aa05-114">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="2aa05-115">Cenário</span><span class="sxs-lookup"><span data-stu-id="2aa05-115">Scenario</span></span>

<span data-ttu-id="2aa05-116">cenário de saudação abordado neste artigo obtém o modo de exibição do grupo de segurança de saudação para uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2aa05-116">hello scenario covered in this article gets hello security group view for a virtual machine.</span></span>

<span data-ttu-id="2aa05-117">Neste cenário, você:</span><span class="sxs-lookup"><span data-stu-id="2aa05-117">In this scenario, you will:</span></span>

- <span data-ttu-id="2aa05-118">Recuperar um conjunto de regras válido</span><span class="sxs-lookup"><span data-stu-id="2aa05-118">Retrieve a known good rule set</span></span>
- <span data-ttu-id="2aa05-119">Recuperar uma máquina virtual com API Rest</span><span class="sxs-lookup"><span data-stu-id="2aa05-119">Retrieve a virtual machine with Rest API</span></span>
- <span data-ttu-id="2aa05-120">Obter a exibição de grupo de segurança para máquina virtual</span><span class="sxs-lookup"><span data-stu-id="2aa05-120">Get security group view for virtual machine</span></span>
- <span data-ttu-id="2aa05-121">Avaliar a resposta</span><span class="sxs-lookup"><span data-stu-id="2aa05-121">Evaluate Response</span></span>

## <a name="retrieve-rule-set"></a><span data-ttu-id="2aa05-122">Recuperar o conjunto de regras</span><span class="sxs-lookup"><span data-stu-id="2aa05-122">Retrieve rule set</span></span>

<span data-ttu-id="2aa05-123">a primeira etapa Olá neste exemplo é toowork com uma linha de base existente.</span><span class="sxs-lookup"><span data-stu-id="2aa05-123">hello first step in this example is toowork with an existing baseline.</span></span> <span data-ttu-id="2aa05-124">Olá, exemplo a seguir é alguns json extraído de um grupo de segurança de rede existente usando Olá `Get-AzureRmNetworkSecurityGroup` cmdlet que é usada como linha de base de saudação para este exemplo.</span><span class="sxs-lookup"><span data-stu-id="2aa05-124">hello following example is some json extracted from an existing Network Security Group using hello `Get-AzureRmNetworkSecurityGroup` cmdlet that is used as hello baseline for this example.</span></span>

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

## <a name="convert-rule-set-toopowershell-objects"></a><span data-ttu-id="2aa05-125">Converter objetos tooPowerShell do conjunto de regra</span><span class="sxs-lookup"><span data-stu-id="2aa05-125">Convert rule set tooPowerShell objects</span></span>

<span data-ttu-id="2aa05-126">Nesta etapa, podemos está lendo um arquivo json que foi criado anteriormente com as regras de saudação são toobe esperado em hello grupo de segurança de rede para este exemplo.</span><span class="sxs-lookup"><span data-stu-id="2aa05-126">In this step, we are reading a json file that was created earlier with hello rules that are expected toobe on hello Network Security Group for this example.</span></span>

```powershell
$nsgbaserules = Get-Content -Path C:\temp\testvm1-nsg.json | ConvertFrom-Json
```

## <a name="retrieve-network-watcher"></a><span data-ttu-id="2aa05-127">Recuperar o Observador de Rede</span><span class="sxs-lookup"><span data-stu-id="2aa05-127">Retrieve Network Watcher</span></span>

<span data-ttu-id="2aa05-128">Olá próxima etapa é a instância do tooretrieve Olá observador de rede.</span><span class="sxs-lookup"><span data-stu-id="2aa05-128">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="2aa05-129">Olá `$networkWatcher` variável é passada toohello `AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2aa05-129">hello `$networkWatcher` variable is passed toohello `AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="2aa05-130">Obter uma VM</span><span class="sxs-lookup"><span data-stu-id="2aa05-130">Get a VM</span></span>

<span data-ttu-id="2aa05-131">Uma máquina virtual é necessário toorun Olá `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet contra.</span><span class="sxs-lookup"><span data-stu-id="2aa05-131">A virtual machine is required toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="2aa05-132">saudação de exemplo a seguir obtém um objeto da VM.</span><span class="sxs-lookup"><span data-stu-id="2aa05-132">hello following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="2aa05-133">Recuperar o modo de exibição de grupo de segurança</span><span class="sxs-lookup"><span data-stu-id="2aa05-133">Retrieve security group view</span></span>

<span data-ttu-id="2aa05-134">Olá próxima etapa é o resultado de exibição de grupo de segurança do tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="2aa05-134">hello next step is tooretrieve hello security group view result.</span></span> <span data-ttu-id="2aa05-135">Esse resultado é comparado toohello "baseline" json que foi mostrado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2aa05-135">This result is compared toohello "baseline" json that was shown earlier.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="analyzing-hello-results"></a><span data-ttu-id="2aa05-136">Analisar resultados de saudação</span><span class="sxs-lookup"><span data-stu-id="2aa05-136">Analyzing hello results</span></span>

<span data-ttu-id="2aa05-137">resposta de saudação é agrupada por interfaces de rede.</span><span class="sxs-lookup"><span data-stu-id="2aa05-137">hello response is grouped by Network interfaces.</span></span> <span data-ttu-id="2aa05-138">Olá diferentes tipos de regras retornadas são efetivos e padrão de regras de segurança.</span><span class="sxs-lookup"><span data-stu-id="2aa05-138">hello different types of rules returned are effective and default security rules.</span></span> <span data-ttu-id="2aa05-139">resultado de saudação é dividido por como ela é aplicada, em uma sub-rede ou uma NIC virtual.</span><span class="sxs-lookup"><span data-stu-id="2aa05-139">hello result is further broken down by how it is applied, either on a subnet or a virtual NIC.</span></span>

<span data-ttu-id="2aa05-140">Hello seguinte script do PowerShell compara os resultados de saudação do hello saída existente do modo de exibição de grupo de segurança tooan de um NSG.</span><span class="sxs-lookup"><span data-stu-id="2aa05-140">hello following PowerShell script compares hello results of hello Security Group View tooan existing output of an NSG.</span></span> <span data-ttu-id="2aa05-141">Olá, exemplo a seguir é um exemplo simples de como os resultados de saudação possam ser comparados com `Compare-Object` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2aa05-141">hello following example is a simple example of how hello results can be compared with `Compare-Object` cmdlet.</span></span>

```powershell
Compare-Object -ReferenceObject $nsgbaserules `
-DifferenceObject $secgroup.NetworkInterfaces[0].NetworkInterfaceSecurityRules `
-Property Name,Description,Protocol,SourcePortRange,DestinationPortRange,SourceAddressPrefix,DestinationAddressPrefix,Access,Priority,Direction
```

<span data-ttu-id="2aa05-142">saudação de exemplo a seguir é o resultado de saudação.</span><span class="sxs-lookup"><span data-stu-id="2aa05-142">hello following example is hello result.</span></span> <span data-ttu-id="2aa05-143">Você pode ver duas regras de saudação que estavam no primeiro conjunto de regras Olá não estavam presentes na comparação de saudação.</span><span class="sxs-lookup"><span data-stu-id="2aa05-143">You can see two of hello rules that were in hello first rule set were not present in hello comparison.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2aa05-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2aa05-144">Next steps</span></span>

<span data-ttu-id="2aa05-145">Se as configurações foram alteradas, consulte [gerenciar grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack para baixo Olá rede segurança e o grupo de regras de segurança que estão em questão.</span><span class="sxs-lookup"><span data-stu-id="2aa05-145">If settings have been changed, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are in question.</span></span>













