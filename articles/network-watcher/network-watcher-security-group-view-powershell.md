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
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-powershell"></a>Analisar a segurança de máquina Virtual com o modo de exibição de grupo de segurança usando o PowerShell

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-security-group-view-powershell.md)
> - [CLI 1.0](network-watcher-security-group-view-cli-nodejs.md)
> - [CLI 2.0](network-watcher-security-group-view-cli.md)
> - [API REST](network-watcher-security-group-view-rest.md)

Exibição de grupo de segurança retorna as regras de segurança de rede configurados e eficiente que são aplicadas tooa virtual machine. Esse recurso é útil tooaudit e diagnosticar os grupos de segurança de rede e as regras configuradas no tráfego de tooensure VM está sendo corretamente permitido ou negado. Neste artigo, mostramos como tooretrieve Olá configurada e tooa de regras de segurança efetiva virtual máquina usando o PowerShell

## <a name="before-you-begin"></a>Antes de começar

Nesse cenário, você executa Olá `Get-AzureRmNetworkWatcherSecurityGroupView` informações de regra de segurança do cmdlet tooretrieve hello.

Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.

## <a name="scenario"></a>Cenário

cenário de saudação abordado neste artigo recupera hello configurado e regras de segurança efetiva para uma determinada máquina virtual.

## <a name="retrieve-network-watcher"></a>Recuperar o Observador de Rede

Olá primeira etapa é a instância do tooretrieve Olá observador de rede. Essa variável é passada toohello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="get-a-vm"></a>Obter uma VM

Uma máquina virtual é necessário toorun Olá `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet contra. saudação de exemplo a seguir obtém um objeto da VM.

```powershell
$VM = Get-AzurermVM -ResourceGroupName testrg -Name testvm1
```

## <a name="retrieve-security-group-view"></a>Recuperar o modo de exibição de grupo de segurança

Olá próxima etapa é o resultado de exibição de grupo de segurança do tooretrieve hello.

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="viewing-hello-results"></a>Exibindo resultados de saudação

Olá, exemplo a seguir é uma resposta reduzida de saudação resultados retornados. Olá resultados mostram todas as regras de segurança efetiva e aplicadas Olá na máquina virtual de saudação dividida em grupos de **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, e  **EffectiveSecurityRules**.

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

## <a name="next-steps"></a>Próximas etapas

Visite [auditoria rede segurança grupos (NSG) com o observador de rede](network-watcher-nsg-auditing-powershell.md) toolearn como tooautomate validação dos grupos de segurança de rede.


