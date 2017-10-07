---
title: aaaGet iniciado com o DNS do Azure usando o PowerShell | Microsoft Docs
description: "Saiba como toocreate um DNS zona e registro de DNS do Azure. Este é um guia passo a passo toocreate e gerenciar sua primeira zona DNS e registrar usando o PowerShell."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 0f9dead1e4b44fcc74c84a024c41cdfaeb02b5d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-powershell"></a>Introdução ao DNS do Azure usando o PowerShell

> [!div class="op_single_selector"]
> * [Portal do Azure](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [CLI 1.0 do Azure](dns-getstarted-cli-nodejs.md)
> * [CLI 2.0 do Azure](dns-getstarted-cli.md)

Este artigo orienta Olá etapas toocreate sua primeira zona DNS e o registro usando o PowerShell do Azure. Você também pode executar essas etapas usando o portal do Azure de saudação ou Olá CLI do Azure de plataforma cruzada.

Uma zona DNS é usado toohost Olá registros DNS para um domínio específico. toostart hospedando seu domínio no DNS do Azure, você precisa toocreate uma zona DNS para esse nome de domínio. Cada registro DNS para seu domínio é criado dentro dessa zona DNS. Finalmente, toopublish o DNS da zona toohello da Internet, você precisa de servidores de nome de saudação tooconfigure para domínio de saudação. Cada uma dessas etapas é descrita abaixo.

Essas instruções presumem que você já instalado e conectado tooAzure PowerShell. Para obter ajuda, consulte [como toomanage DNS zonas usando o PowerShell](dns-operations-dnszones.md).

## <a name="create-hello-resource-group"></a>Criar grupo de recursos de saudação

Antes de criar a zona DNS de saudação, um grupo de recursos é criado toocontain Olá DNS zona. Veja a seguir de Olá comando hello.

```powershell
New-AzureRMResourceGroup -name MyResourceGroup -location "westus"
```

## <a name="create-a-dns-zone"></a>Criar uma zona DNS

Uma zona DNS é criada usando Olá `New-AzureRmDnsZone` cmdlet. Olá, exemplo a seguir cria uma zona DNS chamada *contoso.com* no grupo de recursos de saudação chamado *MyResourceGroup*. Use toocreate de exemplo hello uma zona DNS, substituindo valores de saudação para seu próprio.

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyResourceGroup
```

## <a name="create-a-dns-record"></a>Criar um registro DNS

Criar conjuntos de registros usando Olá `New-AzureRmDnsRecordSet` cmdlet. Olá exemplo a seguir cria um registro com o nome relativo do hello "www" hello "contoso.com", no grupo de recursos "MyResourceGroup" de zona de DNS. nome totalmente qualificado de saudação do conjunto de registros de saudação é "www.contoso.com". tipo de registro de saudação é "A", com o endereço IP "1.2.3.4" e Olá TTL é 3600 segundos.

```powershell
New-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName contoso.com -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4")
```

Para outros tipos de registro, para conjuntos de registros com mais de um registro e toomodify os registros existentes, consulte [registros DNS de gerenciar e conjuntos de registros usando o Azure PowerShell](dns-operations-recordsets.md). 


## <a name="view-records"></a>Exibir registros

registros DNS Olá toolist na zona, use:

```powershell
Get-AzureRmDnsRecordSet -ZoneName contoso.com -ResourceGroupName MyResourceGroup
```


## <a name="update-name-servers"></a>Atualizar servidores de nome

Quando estiver satisfeito de que a zona DNS e registros de tem sido instalados corretamente, você precisa tooconfigure seu nome de domínio toouse servidores de nome DNS do Azure hello. Isso permite que outros usuários no hello Internet toofind seus registros DNS.

servidores de nome de saudação para sua zona são fornecidos por Olá `Get-AzureRmDnsZone` cmdlet:

```powershell
Get-AzureRmDnsZone -ZoneName contoso.com -ResourceGroupName MyResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-b40d-0996b97ed101
Tags                  : {}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org., ns4-01.azure-dns.info.}
NumberOfRecordSets    : 3
MaxNumberOfRecordSets : 5000
```

Esses servidores de nome devem ser configurados com o registrador de nome de domínio hello (onde você adquiriu o nome de domínio Olá). Seu registrador oferecerá Olá opção tooset os servidores de nome Olá para o domínio de saudação. Para obter mais informações, consulte [delegar tooAzure seu domínio DNS](dns-domain-delegation.md).

## <a name="delete-all-resources"></a>Excluir todos os recursos

toodelete todos os recursos criados neste artigo, Olá take etapa a seguir:

```powershell
Remove-AzureRMResourceGroup -Name MyResourceGroup
```

## <a name="next-steps"></a>Próximas etapas

toolearn mais sobre o DNS do Azure, consulte [visão geral do DNS do Azure](dns-overview.md).

toolearn mais sobre o gerenciamento de zonas DNS no DNS do Azure, consulte [zonas DNS gerenciar no DNS do Azure usando o PowerShell](dns-operations-dnszones.md).

toolearn mais sobre o gerenciamento de registros DNS no DNS do Azure, consulte [registros de DNS de gerenciar e registro define no DNS do Azure usando o PowerShell](dns-operations-recordsets.md).

