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
# <a name="automate-nsg-auditing-with-azure-network-watcher-security-group-view"></a>Automatizar a auditoria do NSG com a exibição de grupo de segurança do Observador de Rede do Azure

Os clientes são geralmente enfrentam Olá verificar postura de segurança de saudação da infra-estrutura. Esse desafio não é diferente para as VMs no Azure. É importante toohave um perfil de segurança semelhante com base nas regras de grupo de segurança de rede (NSG) de saudação aplicadas. Usando Olá exibição de grupo de segurança, agora você pode obter lista de saudação de regras aplicadas tooa VM dentro de um NSG. Você pode definir um perfil de segurança NSG dourado e iniciar o modo de exibição de grupo de segurança em um ritmo semanal e comparar Olá saída toohello dourada perfil e criar um relatório. Dessa forma você pode identificar com facilidade todas as VMs de saudação que não são compatíveis toohello prescrita perfil de segurança.

Se você estiver familiarizado com os Grupos de segurança de rede, visite [Visão geral de segurança de rede](../virtual-network/virtual-networks-nsg.md)

## <a name="before-you-begin"></a>Antes de começar

Nesse cenário, você comparar a um grupo de segurança conhecidos boa linha de base toohello exibir os resultados retornados para uma máquina virtual.

Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede. cenário de Olá também pressupõe que um grupo de recursos com uma máquina virtual válida existe toobe usado.

## <a name="scenario"></a>Cenário

cenário de saudação abordado neste artigo obtém o modo de exibição do grupo de segurança de saudação para uma máquina virtual.

Neste cenário, você:

- Recuperar um conjunto de regras válido
- Recuperar uma máquina virtual com API Rest
- Obter a exibição de grupo de segurança para máquina virtual
- Avaliar a resposta

## <a name="retrieve-rule-set"></a>Recuperar o conjunto de regras

a primeira etapa Olá neste exemplo é toowork com uma linha de base existente. Olá, exemplo a seguir é alguns json extraído de um grupo de segurança de rede existente usando Olá `Get-AzureRmNetworkSecurityGroup` cmdlet que é usada como linha de base de saudação para este exemplo.

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

## <a name="convert-rule-set-toopowershell-objects"></a>Converter objetos tooPowerShell do conjunto de regra

Nesta etapa, podemos está lendo um arquivo json que foi criado anteriormente com as regras de saudação são toobe esperado em hello grupo de segurança de rede para este exemplo.

```powershell
$nsgbaserules = Get-Content -Path C:\temp\testvm1-nsg.json | ConvertFrom-Json
```

## <a name="retrieve-network-watcher"></a>Recuperar o Observador de Rede

Olá próxima etapa é a instância do tooretrieve Olá observador de rede. Olá `$networkWatcher` variável é passada toohello `AzureRmNetworkWatcherSecurityGroupView` cmdlet.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a>Obter uma VM

Uma máquina virtual é necessário toorun Olá `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet contra. saudação de exemplo a seguir obtém um objeto da VM.

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="retrieve-security-group-view"></a>Recuperar o modo de exibição de grupo de segurança

Olá próxima etapa é o resultado de exibição de grupo de segurança do tooretrieve hello. Esse resultado é comparado toohello "baseline" json que foi mostrado anteriormente.

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="analyzing-hello-results"></a>Analisar resultados de saudação

resposta de saudação é agrupada por interfaces de rede. Olá diferentes tipos de regras retornadas são efetivos e padrão de regras de segurança. resultado de saudação é dividido por como ela é aplicada, em uma sub-rede ou uma NIC virtual.

Hello seguinte script do PowerShell compara os resultados de saudação do hello saída existente do modo de exibição de grupo de segurança tooan de um NSG. Olá, exemplo a seguir é um exemplo simples de como os resultados de saudação possam ser comparados com `Compare-Object` cmdlet.

```powershell
Compare-Object -ReferenceObject $nsgbaserules `
-DifferenceObject $secgroup.NetworkInterfaces[0].NetworkInterfaceSecurityRules `
-Property Name,Description,Protocol,SourcePortRange,DestinationPortRange,SourceAddressPrefix,DestinationAddressPrefix,Access,Priority,Direction
```

saudação de exemplo a seguir é o resultado de saudação. Você pode ver duas regras de saudação que estavam no primeiro conjunto de regras Olá não estavam presentes na comparação de saudação.

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

## <a name="next-steps"></a>Próximas etapas

Se as configurações foram alteradas, consulte [gerenciar grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack para baixo Olá rede segurança e o grupo de regras de segurança que estão em questão.













