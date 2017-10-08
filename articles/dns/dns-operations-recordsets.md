---
title: aaaManage DNS de registros no DNS do Azure usando o Azure PowerShell | Microsoft Docs
description: "Gerenciando conjuntos de registros DNS e registros no DNS do Azure ao hospedar seu domínio no DNS do Azure. Todos os comandos do PowerShell para operações em conjuntos de registros e registros."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 7136a373-0682-471c-9c28-9e00d2add9c2
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: bfdf116e174d06db0514abdc0ec3f4fc4ee0a079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-azure-powershell"></a>Gerenciar registros e conjuntos de registros DNS no DNS do Azure usando o Azure PowerShell

> [!div class="op_single_selector"]
> * [Portal do Azure](dns-operations-recordsets-portal.md)
> * [CLI 1.0 do Azure](dns-operations-recordsets-cli-nodejs.md)
> * [CLI 2.0 do Azure](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

Este artigo mostra como toomanage DNS registros para a zona DNS usando o PowerShell do Azure. Registros DNS também podem ser gerenciados por meio de plataforma cruzada Olá [CLI do Azure](dns-operations-recordsets-cli.md) ou hello [portal do Azure](dns-operations-recordsets-portal.md).

exemplos de saudação neste artigo presumem que você já tiver [instalado Azure PowerShell, conectado e criar uma zona DNS](dns-operations-dnszones.md).

## <a name="introduction"></a>Introdução

Antes de criar os registros DNS no DNS do Azure, primeiro é necessário toounderstand como o DNS do Azure organiza os registros DNS em conjuntos de registros de DNS.

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

Para obter mais informações sobre os registros DNS no DNS do Azure, confira [Zonas e registros DNS](dns-zones-records.md).


## <a name="create-a-new-dns-record"></a>Criar um novo registro DNS

Se o novo registro tiver Olá mesmo nome e tipo como um registro existente, será necessário muito[adicioná-lo o conjunto de registros existentes toohello](#add-a-record-to-an-existing-record-set). Se o novo registro tem um tooall diferente do nome e tipo de registros existentes, será necessário toocreate um novo conjunto de registros. 

### <a name="create-a-records-in-a-new-record-set"></a>Criar registros 'A' em um novo conjunto de registros

Criar conjuntos de registros usando Olá `New-AzureRmDnsRecordSet` cmdlet. Ao criar um conjunto de registros, é necessário toospecify nome de conjunto de registros de hello, zona hello, tempo de saudação toolive (TTL), o tipo de registro hello e Olá registros toobe criados.

parâmetros de saudação para adicionar o conjunto de registros de tooa registros variam dependendo do tipo de saudação do conjunto de registros de saudação. Por exemplo, ao usar um conjunto de registros do tipo 'A', você precisa toospecify Olá IP endereço usando o parâmetro hello `-IPv4Address`. Outros parâmetros são usados para outros tipos de registro. Consulte [Exemplos adicionais dos tipos de registro](#additional-record-type-examples) para obter detalhes.

Olá, exemplo a seguir cria um conjunto de registros com o nome relativo do hello "www" hello zona DNS 'contoso.com'. nome totalmente qualificado de saudação do conjunto de registros de saudação é 'www.contoso.com'. tipo de registro de saudação é 'A' e Olá TTL é 3600 segundos. conjunto de registros de saudação contém um único registro com o endereço IP '1.2.3.4'.

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

toocreate um conjunto de registros no ápice de uma zona de saudação (nesse caso, "contoso.com"), use o nome de conjunto de registros Olá ' @' (excluindo as aspas):

```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

Se você precisar de um conjunto de registros que contém mais de um registro de toocreate, primeiro crie uma matriz de local e adicionar registros de saudação, passar a matriz de saudação muito`New-AzureRmDnsRecordSet` da seguinte maneira:

```powershell
$aRecords = @()
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4"
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "2.3.4.5"
New-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName MyResourceGroup -Ttl 3600 -RecordType A -DnsRecords $aRecords
```

[Metadados de conjunto de registros](dns-zones-records.md#tags-and-metadata) podem ser dados específicos do aplicativo de tooassociate usado com cada conjunto de registros, como pares chave-valor. Olá exemplo a seguir mostra como toocreate um conjunto de registros com duas entradas de metadados, ' departamento = Finanças ' e ' ambiente = produção '.

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") -Metadata @{ dept="finance"; environment="production" } 
```

DNS do Azure também oferece suporte a conjuntos de registros 'empty', que podem agir como um espaço reservado tooreserve um nome DNS antes de criar registros DNS. Conjuntos de registros vazios são visíveis no plano de controle de DNS do Azure hello, mas aparecem em servidores de nome DNS do Azure hello. saudação de exemplo a seguir cria um conjunto vazio de registro:

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords @()
```

## <a name="create-records-of-other-types"></a>Criar outros tipos de registro

Depois de ter visto em detalhes como registros toocreate 'A', Olá seguintes exemplos mostram como toocreate registros de outros registram tipos suportados pelo DNS do Azure.

Em cada caso, mostramos como toocreate um registro de conjunto que contém um único registro. Hello exemplos anteriores para 'A' registros podem ser adaptada toocreate conjuntos de registros de outros tipos que contém vários registros, com metadados, ou conjuntos de registros de toocreate vazio.

Não fornecemos um exemplo toocreate um conjunto de registros SOA, como SOAs são criados e excluídos com cada zona DNS e não pode ser criado ou excluído separadamente. No entanto, [Olá SOA pode ser modificado, conforme mostrado no exemplo mais adiante](#to-modify-an-SOA-record).

### <a name="create-an-aaaa-record-set-with-a-single-record"></a>Criar um conjunto de registros AAAA com um registro único

```powershell
New-AzureRmDnsRecordSet -Name "test-aaaa" -RecordType AAAA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ipv6Address "2607:f8b0:4009:1803::1005") 
```

### <a name="create-a-cname-record-set-with-a-single-record"></a>Criar um conjunto de registros CNAME com um registro único

> [!NOTE]
> padrões DNS Olá não permitem que os registros CNAME no ápice da saudação de uma zona (`-Name '@'`), nem eles permitem que os conjuntos de registro que contém mais de um registro.
> 
> Para obter mais informações, consulte [Registros CNAME](dns-zones-records.md#cname-records).


```powershell
New-AzureRmDnsRecordSet -Name "test-cname" -RecordType CNAME -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Cname "www.contoso.com") 
```

### <a name="create-an-mx-record-set-with-a-single-record"></a>Criar um conjunto de registros MX com um registro único

Neste exemplo, podemos usar o nome do conjunto de registros de saudação ' @' registro de toocreate um MX no ápice da zona de saudação (nesse caso, "contoso.com").


```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType MX -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Exchange "mail.contoso.com" -Preference 5) 
```

### <a name="create-an-ns-record-set-with-a-single-record"></a>Criar um conjunto de registros NS com um registro único

```powershell
New-AzureRmDnsRecordSet -Name "test-ns" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Nsdname "ns1.contoso.com") 
```

### <a name="create-a-ptr-record-set-with-a-single-record"></a>Criar um conjunto de registros PTR com um único registro

Nesse caso, ' Meu-arpa-zone.com' representa Olá zona de pesquisa inversa ARPA que representa o intervalo de IP. Cada registro PTR definido nesta zona corresponde endereço IP tooan dentro desse intervalo IP. nome do registro Olá '10' é último octeto saudação do endereço IP hello dentro desse intervalo IP representado por esse registro.

```powershell
New-AzureRmDnsRecordSet -Name 10 -RecordType PTR -ZoneName "my-arpa-zone.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "myservice.contoso.com") 
```

### <a name="create-an-srv-record-set-with-a-single-record"></a>Criar um conjunto de registros SRV com um registro único

Ao criar um [conjunto de registros SRV](dns-zones-records.md#srv-records), especificar Olá  *\_service* e  *\_protocolo* em Olá nome de conjunto de registros. Não há nenhuma necessidade tooinclude ' @' na Olá registro de nome do conjunto de quando criar um registro SRV definida no ápice da zona de saudação.

```powershell
New-AzureRmDnsRecordSet -Name "_sip._tls" -RecordType SRV -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Priority 0 -Weight 5 -Port 8080 -Target "sip.contoso.com") 
```


### <a name="create-a-txt-record-set-with-a-single-record"></a>Criar um conjunto de registros TXT com um registro único

Olá exemplo a seguir mostra como registrar o toocreate um TXT. Para obter mais informações sobre Olá tamanho máximo com suporte no registros TXT, consulte [registros TXT](dns-zones-records.md#txt-records).

```powershell
New-AzureRmDnsRecordSet -Name "test-txt" -RecordType TXT -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Value "This is a TXT record") 
```


## <a name="get-a-record-set"></a>Obter um conjunto de registros

tooretrieve um conjunto de registros existente, use `Get-AzureRmDnsRecordSet`. Esse cmdlet retorna um objeto local que representa Olá conjunto de registros em DNS do Azure.

Assim como acontece com `New-AzureRmDnsRecordSet`, nome de conjunto de registros de saudação fornecido deve ser um *relativo* nome, o que significa que ele deve excluir o nome da zona hello. Você também precisa toospecify tipo de registro de saudação e zona Olá que contém o conjunto de registros de saudação.

Olá exemplo a seguir mostra como tooretrieve um conjunto de registros. Neste exemplo, zona Olá é especificada usando Olá `-ZoneName` e `-ResourceGroupName` parâmetros.

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

Como alternativa, você também pode especificar zona hello usando um objeto de zona, passado usando Olá `-Zone` parâmetro.

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

## <a name="list-record-sets"></a>Listar os conjuntos de registros

Você também pode usar `Get-AzureRmDnsZone` conjuntos de registros de toolist em uma região, omitindo Olá `-Name` e/ou `-RecordType` parâmetros.

Olá exemplo a seguir retorna conjuntos de todos os registros na zona hello:

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

Olá exemplo a seguir mostra como todos os conjuntos de um determinado tipo de registro pode ser recuperado, especificando o tipo de registro de saudação enquanto o nome do conjunto de registro Olá a omissão:

```powershell
$recordsets = Get-AzureRmDnsRecordSet -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

tooretrieve conjuntos de todos os registros com um determinado nome em todos os tipos de registro, você precisa tooretrieve todos os conjuntos de registros e, em seguida, os resultados de saudação do filtro:

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | where {$_.Name.Equals("www")}
```

Em todos os Olá acima exemplos, zona Olá pode ser especificado usando Olá `-ZoneName` e `-ResourceGroupName`parâmetros (conforme mostrado), ou especificando um objeto de zona:

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$recordsets = Get-AzureRmDnsRecordSet -Zone $zone
```

## <a name="add-a-record-tooan-existing-record-set"></a>Adicionar um registro tooan existente de conjunto de registros

tooadd um registro existente do registro tooan definido, execute Olá três etapas a seguir:

1. Obter o conjunto de registros existentes Olá

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. Adicione Olá novo registro toohello local conjunto de registros. Esta é uma operação offline.

    ```powershell
    Add-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. Confirme Olá de alteração voltar toohello serviço DNS do Azure. 

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $rs
    ```

Usando `Set-AzureRmDnsRecordSet` *substitui* Olá existente conjunto de registros no DNS do Azure (e todos os registros que ele contém) com o conjunto de registros Olá especificado. [Verificações de ETag](dns-zones-records.md#etags) são usadas as alterações simultâneas de tooensure não são substituídas. Você pode usar o hello opcional `-Overwrite` alternar toosuppress essas verificações.

Essa sequência de operações também pode ser *canalizados*, que significa que você passa o objeto de conjunto de registros de saudação usando o pipe de saudação em vez de passá-lo como um parâmetro:

```powershell
Get-AzureRmDnsRecordSet -Name "www" –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Add-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

exemplos de saudação acima mostram como tooadd um registro 'A' tooan registro existente definida do tipo 'A'. Uma sequência semelhante de operações é usado tooadd registros toorecord conjuntos de outros tipos, substituindo Olá `-Ipv4Address` parâmetro `Add-AzureRmDnsRecordConfig` com outros parâmetros de tipo de registro de tooeach específico. Olá parâmetros para cada tipo de registro são Olá mesmo que para hello `New-AzureRmDnsRecordConfig` cmdlet, como mostrado no [exemplos adicionais de tipo de registro](#additional-record-type-examples) acima.

Os conjuntos de registro do tipo 'CNAME' ou 'SOA' não podem conter mais de um registro. Essa restrição surge de padrões do DNS hello. Não é uma limitação do DNS do Azure.

## <a name="remove-a-record-from-an-existing-record-set"></a>Remover um registro em um conjunto de registros existente

Olá, processo tooremove um registro de um conjunto de registros é semelhante tooadd de processo de toohello um registro tooan existente conjunto de registro:

1. Obter o conjunto de registros existentes Olá

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. Remova o registro de saudação do objeto de conjunto de registros local hello. Esta é uma operação offline. registro de saudação que está sendo removido deve ser uma correspondência exata com um registro existente em todos os parâmetros.

    ```powershell
    Remove-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. Confirme Olá de alteração voltar toohello serviço DNS do Azure. Saudação de uso opcional `-Overwrite` alternar toosuppress [Etag verifica](dns-zones-records.md#etags) alterações simultâneas.

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $Rs
    ```

Usar Olá acima sequência tooremove Olá último registro de um conjunto de registros não exclui o conjunto de registros hello, em vez disso, ele sai de um conjunto de registros vazio. tooremove um conjunto de registros totalmente, consulte [excluir um conjunto de registros](#delete-a-record-set).

Da mesma forma tooadding registros tooa registro definir, Olá sequência de operações tooremove também pode ser conectado a um conjunto de registros:

```powershell
Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Remove-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

Diferentes tipos de registro são suportados, passando parâmetros de tipo específico apropriados Olá muito`Remove-AzureRmDnsRecordSet`. Olá parâmetros para cada tipo de registro são Olá mesmo que para hello `New-AzureRmDnsRecordConfig` cmdlet, como mostrado no [exemplos adicionais de tipo de registro](#additional-record-type-examples) acima.


## <a name="modify-an-existing-record-set"></a>Modificar um conjunto de registros existente

Olá etapas para modificar um conjunto de registros existente são semelhantes toohello que levar ao adicionar ou remover registros de um conjunto de registros:

1. Recuperar Olá registro existente definido por meio de `Get-AzureRmDnsRecordSet`.
2. Modificar o objeto de conjunto de registros local Olá por:
    * adicionando ou removendo os registros
    * Alterando os parâmetros de saudação de registros existentes
    * Alterando o registro de saudação do conjunto de metadados e tempo toolive (TTL)
3. Confirmar as alterações usando Olá `Set-AzureRmDnsRecordSet` cmdlet. Isso *substitui* Olá existente conjunto de registros no DNS do Azure com o conjunto de registros Olá especificado.

Ao usar `Set-AzureRmDnsRecordSet`, [Etag verifica](dns-zones-records.md#etags) são usadas as alterações simultâneas de tooensure não são substituídas. Você pode usar o hello opcional `-Overwrite` alternar toosuppress essas verificações.

### <a name="tooupdate-a-record-in-an-existing-record-set"></a>Definir tooupdate um registro de um registro existente

Neste exemplo, podemos alterar o endereço IP de saudação de um '' registro existente:

```powershell
$rs = Get-AzureRmDnsRecordSet -name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Ipv4Address = "9.8.7.6"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-an-soa-record"></a>toomodify um registro SOA

Você não pode adicionar ou remover registros da saudação criado automaticamente o registro SOA definido no ápice da zona de saudação (`-Name "@"`, incluindo as aspas). No entanto, você pode modificar qualquer um dos parâmetros de saudação em Olá registro SOA (exceto "Host") e registro Olá definir o TTL.

Olá mostrado no exemplo a seguir como Olá toochange *Email* propriedade Olá registro SOA:

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType SOA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Email = "admin.contoso.com"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-ns-records-at-hello-zone-apex"></a>toomodify NS registros no ápice da zona de saudação

registro de NS Olá definido no ápice da zona de saudação é criado automaticamente com cada zona DNS. Ela contém nomes de saudação da zona do hello Azure DNS nome servidores toohello atribuído.

Você pode adicionar nome adicionais servidores toothis NS conjunto de registros, toosupport co-hospedagem domínios com mais de um provedor DNS. Você também pode modificar hello TTL e metadados para esse conjunto de registros. No entanto, você não pode remover ou modificar servidores de nome DNS do Azure preenchidos previamente hello.

Observe que isso se aplica apenas toohello NS conjunto de registros no ápice da zona de saudação. Outros conjuntos de registros NS na zona (como zonas de filho usado toodelegate) podem ser modificados sem restrição.

saudação de exemplo a seguir mostra como tooadd um registro NS de toohello de servidor de nome adicionais definir no ápice da zona de saudação:

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Add-AzureRmDnsRecordConfig -RecordSet $rs -Nsdname ns1.myotherdnsprovider.com
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-record-set-metadata"></a>metadados de conjunto de registros de toomodify

[Metadados de conjunto de registros](dns-zones-records.md#tags-and-metadata) podem ser dados específicos do aplicativo de tooassociate usado com cada conjunto de registros, como pares chave-valor.

Olá exemplo a seguir mostra como definir toomodify Olá metadados de um registro existente:

```powershell
# Get hello record set
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"

# Add 'dept=finance' name-value pair
$rs.Metadata.Add('dept', 'finance') 

# Remove metadata item named 'environment'
$rs.Metadata.Remove('environment')  

# Commit changes
Set-AzureRmDnsRecordSet -RecordSet $rs
```


## <a name="delete-a-record-set"></a>Excluir um conjunto de registros

Conjuntos de registros podem ser excluídos usando Olá `Remove-AzureRmDnsRecordSet` cmdlet. Excluir um conjunto de registros também exclui todos os registros no conjunto de registros de saudação.

> [!NOTE]
> Você não pode excluir Olá SOA e NS conjuntos de registros no ápice da zona de saudação (`-Name '@'`).  DNS do Azure criado essas automaticamente quando Olá zona foi criada e exclui automaticamente quando Olá zona é excluída.

Olá exemplo a seguir mostra como toodelete um conjunto de registros. Neste exemplo, nome do conjunto de registros de hello, tipo de conjunto de registros, nome da zona e grupo de recursos são cada especificados explicitamente.

```powershell
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

Como alternativa, o conjunto de registros Olá pode ser especificado por nome e tipo e Olá zona especificada usando um objeto:

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

Como uma terceira opção, o registro Olá definido pode ser especificado usando um objeto de conjunto de registros:

```powershell
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -RecordSet $rs
```

Quando você especifica o conjunto de registros de saudação toobe excluído usando um objeto de conjunto de registros, [Etag verifica](dns-zones-records.md#etags) são usadas as alterações simultâneas de tooensure não são excluídas. Você pode usar o hello opcional `-Overwrite` alternar toosuppress essas verificações.

objeto de conjunto de registros de saudação também pode ser usado em vez de ser passado como um parâmetro:

```powershell
Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | Remove-AzureRmDnsRecordSet
```

## <a name="confirmation-prompts"></a>Prompts de confirmação

Olá `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, e `Remove-AzureRmDnsRecordSet` todos os cmdlets de dar suporte a solicitações de confirmação.

Cada cmdlet solicita confirmação se hello `$ConfirmPreference` variável de preferência do PowerShell tem um valor de `Medium` ou inferior. Desde o valor padrão Olá `$ConfirmPreference` é `High`, essas solicitações não estão disponível ao usar configurações de PowerShell saudação padrão.

Você pode substituir o atual Olá `$ConfirmPreference` configuração usando Olá `-Confirm` parâmetro. Se você especificar `-Confirm` ou `-Confirm:$True` , Olá cmdlet solicita sua confirmação antes que ele é executado. Se você especificar `-Confirm:$False` , Olá cmdlet não solicita confirmação. 

Para obter mais informações sobre `-Confirm` e `$ConfirmPreference`, consulte [Sobre as Variáveis de Preferência](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre as [zonas e os registros no DNS do Azure](dns-zones-records.md).
<br>
Saiba como muito[proteger suas zonas e registros de](dns-protect-zones-recordsets.md) ao usar o DNS do Azure.
<br>
Saudação de revisão [documentação de referência do PowerShell do Azure DNS](/powershell/module/azurerm.dns).
