---
title: "listas de controle de acesso do Azure ponto de extremidade de aaaManage | PowerShell | Clássico | Microsoft Docs"
description: Saiba como toomanage ACLs com o PowerShell
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c84e40af-f351-4572-b3f0-d572d46bafe7
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: a7ca241ea108a266085bfb689b742d781e58da1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-endpoint-access-control-lists-using-powershell-in-hello-classic-deployment-model"></a>Gerenciar listas de controle de acesso do ponto de extremidade usando o PowerShell no modelo de implantação clássico Olá
Você pode criar e gerenciar a rede controle listas de acesso (ACLs) para pontos de extremidade usando o PowerShell do Azure ou no Portal de gerenciamento de saudação. Neste tópico, você encontrará procedimentos para tarefas comuns de ACL que podem ser concluídas usando o PowerShell. Para obter lista de saudação do Azure PowerShell cmdlets, consulte [Cmdlets de gerenciamento do Azure](http://go.microsoft.com/fwlink/?LinkId=317721). Para saber mais sobre ACLs, confira [O que é uma lista de controle de acesso (ACL) de rede?](virtual-networks-acl.md). Se você quiser toomanage suas ACLs usando o Portal de gerenciamento de saudação, consulte [como pontos de extremidade de tooSet tooa Máquina Virtual](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="manage-network-acls-by-using-azure-powershell"></a>Gerenciar ACLs de rede usando o PowerShell do Azure
Você pode usar toocreate de cmdlets do PowerShell do Azure, remover e configurar (definir) Network Access Control Lists (ACLs). Incluímos alguns exemplos de algumas das maneiras de saudação, que você pode configurar uma ACL usando o PowerShell.

tooretrieve uma lista completa de saudação cmdlets do PowerShell ACL, você pode usar qualquer um dos seguintes hello:

    Get-Help *AzureACL*
    Get-Command -Noun AzureACLConfig

### <a name="create-a-network-acl-with-rules-that-permit-access-from-a-remote-subnet"></a>Criar uma ACL de rede com regras que permitem o acesso de uma sub-rede remota
exemplo Hello abaixo ilustra uma maneira toocreate uma nova ACL que contém as regras. Essa ACL é então aplicado tooa ponto de extremidade de máquina virtual. regras de ACL Olá no exemplo hello abaixo permitirá o acesso de uma sub-rede remota. toocreate uma nova ACL de rede com as regras de permissão para uma sub-rede remota, abra o Azure PowerShell ISE. Copie e cole o script hello abaixo, configurando o script hello com seus próprios valores e, em seguida, execute o script hello.

1. Crie novo objeto de ACL de rede hello.
   
        $acl1 = New-AzureAclConfig
2. Defina uma regra que permite o acesso de uma sub-rede remota. O exemplo hello abaixo, você define a regra *100* (que tem prioridade sobre a regra 200 e superior) sub-rede remota de saudação tooallow *10.0.0.0/8* acessar o ponto de extremidade de máquina virtual toohello. Substitua valores hello com seus próprios requisitos de configuração. nome Hello "Configuração da ACL de SharePoint" deve ser substituído pelo nome amigável do hello que você deseja toocall essa regra.
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "SharePoint ACL config"
3. Para regras adicionais, repita o cmdlet hello, substituindo os valores hello com seus próprios requisitos de configuração. Ser-se de que toochange Olá regra número ordem tooreflect Olá ordem na qual você deseja Olá regras toobe aplicado. número mais baixo de regra Olá tem precedência sobre o número mais alto de saudação.
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
4. Em seguida, você pode criar um novo ponto de extremidade (Adicionar) ou definir hello ACL para um ponto de extremidade existente (Set). Neste exemplo, vamos adicionar que um novo ponto de extremidade de máquina virtual chamado "web" e atualização Olá máquina virtual ponto de extremidade com hello configurações de ACL.
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        | Update-AzureVM
5. Em seguida, combinar Olá cmdlets e execute o script hello. Para este exemplo hello cmdlets combinados teria esta aparência:
   
        $acl1 = New-AzureAclConfig
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "Sharepoint ACL config"
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        |Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        |Update-AzureVM

### <a name="remove-a-network-acl-rule-that-permits-access-from-a-remote-subnet"></a>Remover uma regra de ACL de rede que permite o acesso de uma sub-rede remota
exemplo Hello abaixo ilustra uma maneira tooremove uma regra ACL de rede.  regras de tooremove uma regra de ACL de rede com permissão para uma sub-rede remota, abra um Azure PowerShell ISE. Copie e cole o script hello abaixo, configurando o script hello com seus próprios valores e, em seguida, execute o script hello.

1. Primeira etapa é o objeto de ACL de rede tooget Olá para o ponto de extremidade de máquina virtual de saudação. Você, em seguida, removerá a regra de ACL de saudação. Nesse caso, estamos removendo-a através da ID de regra. Isso removerá apenas Olá ID da regra 0 da saudação ACL. Não remove o objeto de ACL de saudação do ponto de extremidade de máquina virtual de saudação.
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Get-AzureAclConfig –EndpointName "web" `
        | Set-AzureAclConfig –RemoveRule –ID 0 –ACL $acl1
2. Em seguida, você deverá aplicar o ponto de extremidade do hello ACL de rede objeto toohello máquina virtual e atualizar a máquina virtual de saudação.
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Set-AzureEndpoint –ACL $acl1 –Name "web" `
        | Update-AzureVM

### <a name="remove-a-network-acl-from-a-virtual-machine-endpoint"></a>Remover uma ACL de rede de um ponto de extremidade de máquina virtual
Em determinados cenários, você pode querer tooremove um objeto de ACL de rede de um ponto de extremidade de máquina virtual. toodo isso, abra o Azure PowerShell ISE. Copie e cole o script hello abaixo, configurando o script hello com seus próprios valores e, em seguida, execute o script hello.

        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Remove-AzureAclConfig –EndpointName "web" `
        | Update-AzureVM

## <a name="next-steps"></a>Próximas etapas
[O que é uma lista de controle de acesso (ACL) de rede?](virtual-networks-acl.md)

