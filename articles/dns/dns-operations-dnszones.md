---
title: aaaManage DNS zonas no DNS do Azure - PowerShell | Microsoft Docs
description: "Você pode gerenciar zonas DNS usando o Azure Powershell. Este artigo descreve como tooupdate, excluir e criar zonas DNS no DNS do Azure"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: a67992ab-8166-4052-9b28-554c5a39e60c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: gwallace
ms.openlocfilehash: 261b89f72213aa9784034d47ff9d1c55a4e80d65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-using-powershell"></a>Como toomanage zonas de DNS usando o PowerShell

> [!div class="op_single_selector"]
> * [Portal](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [CLI 1.0 do Azure](dns-operations-dnszones-cli-nodejs.md)
> * [CLI 2.0 do Azure](dns-operations-dnszones-cli.md)

Este artigo mostra como toomanage suas zonas DNS usando o PowerShell do Azure. Você também pode gerenciar as zonas DNS usando multiplataforma Olá [CLI do Azure](dns-operations-dnszones-cli.md) ou Olá portal do Azure.

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a>Criar uma zona DNS

Uma zona DNS é criada usando Olá `New-AzureRmDnsZone` cmdlet.

Olá, exemplo a seguir cria uma zona DNS chamada *contoso.com* no grupo de recursos de saudação chamado *MyResourceGroup*:

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

Olá exemplo a seguir mostra como toocreate um DNS da zona com dois [do Azure Resource Manager marcas](dns-zones-records.md#tags), *projeto = demonstração* e *env = test*:

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a>Obter uma zona DNS

tooretrieve uma zona DNS, use Olá `Get-AzureRmDnsZone` cmdlet. Essa operação retorna um DNS da zona objeto correspondente tooan zona existente no DNS do Azure. Olá objeto contém dados sobre a zona de saudação (como número de saudação de conjuntos de registros), mas não contém conjuntos de registros de saudação próprios (consulte `Get-AzureRmDnsRecordSet`).

```powershell
Get-AzureRmDnsZone -Name contoso.com –ResourceGroupName MyAzureResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-8ec2-f4879750d201
Tags                  : {project, env}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org.,
                        ns4-01.azure-dns.info.}
NumberOfRecordSets    : 2
MaxNumberOfRecordSets : 5000
```

## <a name="list-dns-zones"></a>Listar as zonas DNS

Omitindo o nome da zona de saudação do `Get-AzureRmDnsZone`, você pode enumerar todas as zonas em um grupo de recursos. Essa operação retorna uma matriz de objetos de zona.

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

Omitindo o nome da zona hello e o nome do grupo de recursos de saudação do `Get-AzureRmDnsZone`, você pode enumerar todas as zonas em Olá assinatura do Azure.

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a>Atualizar uma zona DNS

Alterações tooa recurso de zona do DNS pode ser feito usando `Set-AzureRmDnsZone`. Esse cmdlet não atualizar conjuntos de registros de DNS hello dentro da zona de saudação (consulte [como registros DNS tooManage](dns-operations-recordsets.md)). Ele só tem usado tooupdate propriedades do próprio recurso de zona hello. Propriedades de zona gravável Olá são atualmente limitado toohello [do Azure Resource Manager 'marcas' para o recurso de zona Olá](dns-zones-records.md#tags).

Use uma saudação tooupdate de duas maneiras a seguir uma zona DNS:

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group"></a>Especificar Olá zona usando o grupo de recursos e o nome da zona de saudação

Essa abordagem substitui marcas existentes de zona Olá com hello valores especificados.

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-hello-zone-using-a-zone-object"></a>Especifique a zona hello usando um objeto $zone

Essa abordagem recupera o objeto de zona existente hello, modifica marcas hello e, em seguida, confirma as alterações de saudação. Dessa forma, as marcas existentes podem ser preservadas.

```powershell
# Get hello zone object
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup

# Remove an existing tag
$zone.Tags.Remove("project")

# Add a new tag
$zone.Tags.Add("status","approved")

# Commit changes
Set-AzureRmDnsZone -Zone $zone
```

Ao usar `Set-AzureRmDnsZone` com um objeto $zone, [Etag verifica](dns-zones-records.md#etags) são usadas as alterações simultâneas de tooensure não são substituídas. Você pode usar o hello opcional `-Overwrite` alternar toosuppress essas verificações.

## <a name="delete-a-dns-zone"></a>Excluir uma zona DNS

As zonas DNS podem ser excluídas usando Olá `Remove-AzureRmDnsZone` cmdlet.

> [!NOTE]
> Excluir uma zona DNS também exclui todos os registros DNS na zona de saudação. Essa operação não pode ser desfeita. Se a zona DNS de saudação está em uso, serviços usando zona Olá falhará quando Olá zona é excluída.
>
>tooprotect contra a exclusão acidental de zona, consulte [como tooprotect DNS zonas e os registros](dns-protect-zones-recordsets.md).


Use uma saudação toodelete de duas maneiras a seguir uma zona DNS:

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group-name"></a>Especificar Olá zona usando o nome da zona hello e o nome do grupo de recursos

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-hello-zone-using-a-zone-object"></a>Especifique a zona hello usando um objeto $zone

Você pode especificar Olá zona toobe excluído usando um `$zone` objeto retornado por `Get-AzureRmDnsZone`.

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

objeto de zona Olá também pode ser usado em vez de ser passado como um parâmetro:

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

Assim como acontece com `Set-AzureRmDnsZone`, especificando Olá zona usando um `$zone` habilita Etag verifica as alterações simultâneas de tooensure não são excluídas do objeto. Saudação de uso `-Overwrite` alternar toosuppress essas verificações.

## <a name="confirmation-prompts"></a>Prompts de confirmação

Olá `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, e `Remove-AzureRmDnsZone` todos os cmdlets de dar suporte a solicitações de confirmação.

Ambos `New-AzureRmDnsZone` e `Set-AzureRmDnsZone` solicita confirmação se hello `$ConfirmPreference` variável de preferência do PowerShell tem um valor de `Medium` ou inferior. Devido a toohello potencialmente alto impacto da exclusão de uma zona DNS, hello `Remove-AzureRmDnsZone` cmdlet solicita confirmação se hello `$ConfirmPreference` variável do PowerShell tem qualquer valor diferente de `None`.

Desde o valor padrão Olá `$ConfirmPreference` é `High`, apenas `Remove-AzureRmDnsZone` solicita confirmação por padrão.

Você pode substituir o atual Olá `$ConfirmPreference` configuração usando Olá `-Confirm` parâmetro. Se você especificar `-Confirm` ou `-Confirm:$True` , Olá cmdlet solicita sua confirmação antes que ele é executado. Se você especificar `-Confirm:$False` , Olá cmdlet não solicita confirmação.

Para obter mais informações sobre `-Confirm` e `$ConfirmPreference`, consulte [Sobre as Variáveis de Preferência](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).

## <a name="next-steps"></a>Próximas etapas

Saiba como muito[gerenciar conjuntos de registros e registros](dns-operations-recordsets.md) na zona DNS.
<br>
Saiba como muito[delegar tooAzure seu domínio DNS](dns-domain-delegation.md).
<br>
Saudação de revisão [documentação de referência do PowerShell do Azure DNS](/powershell/module/azurerm.dns).

