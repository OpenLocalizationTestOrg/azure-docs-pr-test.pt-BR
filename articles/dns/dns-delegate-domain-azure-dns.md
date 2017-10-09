---
title: "aaaDelegate tooAzure seu domínio DNS | Microsoft Docs"
description: "Entenda como usar DNS do Azure e delegação de domínio de toochange nome servidores tooprovide domínio hospedando."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 257da6ec-d6e2-4b6f-ad76-ee2dde4efbcc
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: gwallace
ms.openlocfilehash: f780bdaa416150e5e3afe6c6845dc75ba54b6203
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-a-domain-tooazure-dns"></a>Delegar um tooAzure de domínio DNS

DNS do Azure permite que você toohost uma zona DNS e gerenciar registros DNS Olá para um domínio no Azure. Para consultas DNS para um tooreach de domínio DNS do Azure, domínio Olá tem toobe delegadas tooAzure DNS do domínio pai de saudação. Tenha em mente DNS do Azure não é um registrador de domínio hello. Este artigo explica como toodelegate tooAzure seu domínio DNS.

Comprado de um registrador de domínios, seu registrador oferece Olá opção tooset esses registros NS. Você não possuem tooown toocreate um domínio uma zona DNS com esse nome de domínio DNS do Azure. No entanto, é necessário tooown Olá domínio tooset backup Olá tooAzure de delegação DNS com o registrador de saudação.

Por exemplo, suponha que você compre domínio Olá 'contoso.net' e cria uma zona com o nome de saudação 'contoso.net' no DNS do Azure. Como proprietário de saudação do domínio hello, seu registrador oferece que Olá endereços do servidor de nome hello opção tooconfigure (ou seja, registros de saudação NS) para seu domínio. registrador Olá armazena esses registros NS em Olá domínio pai, neste caso '.net'. Os clientes em torno de Olá, mundo podem ser direcionado tooyour domínio na zona DNS do Azure durante a tentativa de tooresolve registros DNS em 'contoso.net'.

## <a name="create-a-dns-zone"></a>Criar uma zona DNS

1. Entrar toohello portal do Azure
1. No menu de Hub hello, clique em e clique em **Novo > rede >** e, em seguida, clique em **zona DNS** folha de zona de DNS criar tooopen hello.

    ![Zona DNS](./media/dns-domain-delegation/dns.png)

1. Em Olá **zona DNS criar** folha digite Olá valores a seguir, clique em **criar**:

   | **Configuração** | **Valor** | **Detalhes** |
   |---|---|---|
   |**Nome**|contoso.net|nome de saudação da zona do DNS de saudação|
   |**Assinatura**|[Sua assinatura]|Selecione um assinatura toocreate Olá aplicativo gateway.|
   |**Grupo de recursos**|**Criar um novo:** contosoRG|Crie um grupos de recursos. nome do grupo de recursos Olá deve ser exclusivo na assinatura de saudação selecionado. toolearn mais sobre grupos de recursos, leia Olá [Gerenciador de recursos](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) artigo de visão geral.|
   |**Localidade**|Oeste dos EUA||

> [!NOTE]
> grupo de recursos de Olá refere-se o local de toohello saudação do grupo de recursos e não tem nenhum impacto na zona DNS de saudação. local da zona DNS Olá sempre é "global" e não é mostrado.

## <a name="retrieve-name-servers"></a>Recuperar servidores de nome

Antes de você pode delegar a zona DNS tooAzure DNS, é necessário primeiro nomes de servidor de nome tooknow Olá para a zona. O Azure DNS aloca os servidores de nomes de um pool sempre que uma zona é criada.

1. A zona DNS de saudação criada, no portal do Azure de saudação **Favoritos** painel, clique em **todos os recursos**. Clique em Olá **contoso.net** zona DNS na Olá **todos os recursos** folha. Se a assinatura de saudação selecionado já contiver vários recursos, você pode inserir **contoso.net** em Olá filtrar por nome... gateway de caixa tooeasily acesso Olá aplicativo. 

1. Recupere servidores de nome de saudação da folha de zona do DNS hello. Neste exemplo, a zona de saudação 'contoso.net' recebeu servidores de nome ' ns1-01.azure-dns.com', 'ns2-01.azure-dns .net', ' ns3-01.azure-dns.org', e ' ns4-01.azure-dns.info':

 ![Servidor de nomes DNS](./media/dns-domain-delegation/viewzonens500.png)

DNS do Azure cria automaticamente os registros NS autoritativos na zona que contém a saudação servidores de nomes atribuída.  nomes de servidor de nomes de saudação toosee por meio do Azure PowerShell ou CLI do Azure, basta tooretrieve esses registros.

Olá exemplos a seguir também fornecem etapas Olá tooretrieve servidores de nome de saudação para uma zona no DNS do Azure com o PowerShell e a CLI do Azure.

### <a name="powershell"></a>PowerShell

```powershell
# hello record name "@" is used toorefer toorecords at hello top of hello zone.
$zone = Get-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -Zone $zone
```

saudação de exemplo a seguir é a resposta de saudação.

```
Name              : @
ZoneName          : contoso.net
ResourceGroupName : contosorg
Ttl               : 172800
Etag              : 03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5
RecordType        : NS
Records           : {ns1-07.azure-dns.com., ns2-07.azure-dns.net., ns3-07.azure-dns.org.,
                    ns4-07.azure-dns.info.}
Metadata          :
```

### <a name="azure-cli"></a>CLI do Azure

```azurecli
az network dns record-set show --resource-group contosoRG --zone-name contoso.net --type NS --name @
```

saudação de exemplo a seguir é a resposta de saudação.

```json
{
  "etag": "03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosoRG/providers/Microsoft.Network/dnszones/contoso.net/NS/@",
  "metadata": null,
  "name": "@",
  "nsRecords": [
    {
      "nsdname": "ns1-07.azure-dns.com."
    },
    {
      "nsdname": "ns2-07.azure-dns.net."
    },
    {
      "nsdname": "ns3-07.azure-dns.org."
    },
    {
      "nsdname": "ns4-07.azure-dns.info."
    }
  ],
  "resourceGroup": "contosoRG",
  "ttl": 172800,
  "type": "Microsoft.Network/dnszones/NS"
}
```

## <a name="delegate-hello-domain"></a>Domínio de saudação do delegado

Agora que a zona DNS de saudação é criada e você tem servidores de nome hello, o domínio pai Olá precisa toobe atualizada com os servidores de nome DNS do Azure Olá. Cada registro tem seus próprios registros de servidor DNS management tools toochange Olá nome para um domínio. Na página de gerenciamento do DNS do registrador hello, editar os registros NS hello e substitua os registros NS Olá Olá aqueles criados de DNS do Azure.

Ao delegar tooAzure um domínio DNS, você deve usar nomes de servidor de nome hello fornecidos pelo DNS do Azure. É recomendável toouse todas as quatro nome nomes de servidor, independentemente do nome de saudação do seu domínio. Delegação de domínio não requer toouse de nome de servidor de nome Olá Olá mesmo domínio de nível superior que seu domínio.

Você não deve usar os registros de união toopoint toohello DNS do Azure nome endereços IP do servidor, desde que esses endereços IP podem mudar no futuro. Atualmente, o Azure DNS não dá suporte às delegações usando nomes do servidores de nomes em sua própria zona, às vezes chamados de 'servidores de nome intuitivos'.

## <a name="verify-name-resolution-is-working"></a>Verifique se a resolução de nomes está funcionando

Depois de concluir a delegação hello, você pode verificar se a resolução de nomes está funcionando usando uma ferramenta como 'nslookup' tooquery Olá registro SOA da zona (que é criada automaticamente quando a zona de saudação é criada).

Você não tem servidores de nome de DNS do Azure toospecify Olá, se a delegação Olá foi configurada corretamente, Olá DNS resolução processo normal localiza os servidores de nome de saudação automaticamente.

```
nslookup -type=SOA contoso.com
```

a seguir Olá é um exemplo de resposta de saudação que precedem o comando:

```
Server: ns1-04.azure-dns.com
Address: 208.76.47.4

contoso.com
primary name server = ns1-04.azure-dns.com
responsible mail addr = msnhst.microsoft.com
serial = 1
refresh = 900 (15 mins)
retry = 300 (5 mins)
expire = 604800 (7 days)
default TTL = 300 (5 mins)
```

## <a name="delegate-sub-domains-in-azure-dns"></a>Delegar subdomínios no DNS do Azure

Se você quiser tooset uma zona filho separada, você pode delegar um subdomínio no DNS do Azure. Por exemplo, tendo configurado e delegado 'contoso.net' no DNS do Azure, suponha que você gostaria que tooset uma zona filho separada, 'partners.contoso.net'.

1. Crie a zona de filho Olá 'partners.contoso.net' no DNS do Azure.
2. Pesquise registros NS autoritativos de saudação em Olá filho tooobtain Olá servidores de nome hospeda zona de filho Olá no DNS do Azure.
3. Delegar a zona de filho Olá Configurando registros NS na zona pai de saudação apontando toohello zona de filho.

### <a name="create-a-dns-zone"></a>Criar uma zona DNS

1. Entrar toohello portal do Azure
1. No menu de Hub hello, clique em e clique em **Novo > rede >** e, em seguida, clique em **zona DNS** folha de zona de DNS criar tooopen hello.

    ![Zona DNS](./media/dns-domain-delegation/dns.png)

1. Em Olá **zona DNS criar** folha digite Olá valores a seguir, clique em **criar**:

   | **Configuração** | **Valor** | **Detalhes** |
   |---|---|---|
   |**Nome**|partners.contoso.net|nome de saudação da zona do DNS de saudação|
   |**Assinatura**|[Sua assinatura]|Selecione um assinatura toocreate Olá aplicativo gateway.|
   |**Grupo de recursos**|**Usar existente:** contosoRG|Crie um grupos de recursos. nome do grupo de recursos Olá deve ser exclusivo na assinatura de saudação selecionado. toolearn mais sobre grupos de recursos, leia Olá [Gerenciador de recursos](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) artigo de visão geral.|
   |**Localidade**|Oeste dos EUA||

> [!NOTE]
> grupo de recursos de Olá refere-se o local de toohello saudação do grupo de recursos e não tem nenhum impacto na zona DNS de saudação. local da zona DNS Olá sempre é "global" e não é mostrado.

### <a name="retrieve-name-servers"></a>Recuperar servidores de nome

1. A zona DNS de saudação criada, no portal do Azure de saudação **Favoritos** painel, clique em **todos os recursos**. Clique em Olá **partners.contoso.net** zona DNS na Olá **todos os recursos** folha. Se a assinatura de saudação selecionado já contiver vários recursos, você pode inserir **partners.contoso.net** em Olá filtrar por nome... zona DNS do hello caixa tooeasily acesso.

1. Recupere servidores de nome de saudação da folha de zona do DNS hello. Neste exemplo, a zona de saudação 'contoso.net' recebeu servidores de nome ' ns1-01.azure-dns.com', 'ns2-01.azure-dns .net', ' ns3-01.azure-dns.org', e ' ns4-01.azure-dns.info':

 ![Servidor de nomes DNS](./media/dns-domain-delegation/viewzonens500.png)

DNS do Azure cria automaticamente os registros NS autoritativos na zona que contém a saudação servidores de nomes atribuída.  nomes de servidor de nomes de saudação toosee por meio do Azure PowerShell ou CLI do Azure, basta tooretrieve esses registros.

### <a name="create-name-server-record-in-parent-zone"></a>Criar registro de servidor de nomes na zona pai

1. Navegue toohello **contoso.net** zona DNS na Olá portal do Azure.
1. Clique em **+ Conjunto de registros**
1. Em Olá **Adicionar conjunto de registros** folha, digite Olá valores a seguir, clique em **Okey**:

   | **Configuração** | **Valor** | **Detalhes** |
   |---|---|---|
   |**Nome**|partners|nome de saudação da zona DNS Olá filho|
   |**Tipo**|NS|Use NS para os registros do servidor de nomes.|
   |**TTL**|1|Tempo toolive.|
   |**Unidade de TTL**|Horas|Define o tempo unidade toolive toohours|
   |**NAME SERVER**|{servidores de nome para a zona partners.contoso.net}|Insira todos os 4 Olá de servidores de nomes de partners.contoso.net zona. |

   ![Servidor de nomes DNS](./media/dns-domain-delegation/partnerzone.png)


### <a name="delegating-sub-domains-in-azure-dns-with-other-tools"></a>Delegar subdomínios no DNS do Azure com outras ferramentas

Hello exemplos a seguir fornecem as etapas de saudação toodelegate subdomínios no DNS do Azure com o PowerShell e a CLI:

#### <a name="powershell"></a>PowerShell

Olá PowerShell de exemplo a seguir demonstra como isso funciona. Olá mesmas etapas podem ser executadas por meio de saudação portal do Azure ou por meio de Olá CLI do Azure de plataforma cruzada.

```powershell
# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
$parent = New-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
$child = New-AzureRmDnsZone -Name partners.contoso.net -ResourceGroupName contosoRG

# Retrieve hello authoritative NS records from hello child zone as shown in hello next example. This contains hello name servers assigned toohello child zone.
$child_ns_recordset = Get-AzureRmDnsRecordSet -Zone $child -Name "@" -RecordType NS

# Create hello corresponding NS record set in hello parent zone toocomplete hello delegation. hello record set name in hello parent zone matches hello child zone name, in this case "partners".
$parent_ns_recordset = New-AzureRmDnsRecordSet -Zone $parent -Name "partners" -RecordType NS -Ttl 3600
$parent_ns_recordset.Records = $child_ns_recordset.Records
Set-AzureRmDnsRecordSet -RecordSet $parent_ns_recordset
```

Use `nslookup` tooverify que tudo está configurado corretamente procurando Olá registro SOA da zona de filho hello.

```
nslookup -type=SOA partners.contoso.com
```

```
Server: ns1-08.azure-dns.com
Address: 208.76.47.8

partners.contoso.com
    primary name server = ns1-08.azure-dns.com
    responsible mail addr = msnhst.microsoft.com
    serial = 1
    refresh = 900 (15 mins)
    retry = 300 (5 mins)
    expire = 604800 (7 days)
    default TTL = 300 (5 mins)
```

#### <a name="azure-cli"></a>CLI do Azure

```azurecli
#!/bin/bash

# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
az network dns zone create -g contosoRG -n contoso.net
az network dns zone create -g contosoRG -n partners.contoso.net
```

Recuperar os servidores de nome de saudação do hello `partners.contoso.net` zona de saída de hello.

```
{
  "etag": "00000003-0000-0000-418f-250de2b2d201",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosorg/providers/Microsoft.Network/dnszones/partners.contoso.net",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "partners.contoso.net",
  "nameServers": [
    "ns1-09.azure-dns.com.",
    "ns2-09.azure-dns.net.",
    "ns3-09.azure-dns.org.",
    "ns4-09.azure-dns.info."
  ],
  "numberOfRecordSets": 2,
  "resourceGroup": "contosorg",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

Crie conjunto de registros de saudação e registros NS para cada servidor de nomes.

```azurecli
#!/bin/bash

# Create hello record set
az network dns record-set ns create --resource-group contosorg --zone-name contoso.net --name partners

# Create a ns record for each name server.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns1-09.azure-dns.com.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns2-09.azure-dns.net.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns3-09.azure-dns.org.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns4-09.azure-dns.info.
```

## <a name="delete-all-resources"></a>Excluir todos os recursos

toodelete todos os recursos criados neste artigo, Olá concluir as etapas a seguir:

1. No portal do Azure de saudação **Favoritos** painel, clique em **todos os recursos**. Clique em Olá **contosorg** grupo de recursos no hello folha de todos os recursos. Se a assinatura de saudação selecionado já contiver vários recursos, você pode inserir **contosorg** em Olá **filtrar por nome...** grupo de recursos do hello caixa tooeasily acesso.
1. Em Olá **contosorg** folha, clique em Olá **excluir** botão.
1. Hello portal exige que você tootype nome de saudação do hello tooconfirm de grupo de recursos que você deseja toodelete-lo. Tipo *contosorg* para o nome do grupo de recursos hello, em seguida, clique em **excluir**. Excluir um grupo de recursos exclui todos os recursos no grupo de recursos de saudação, portanto, sempre tooconfirm-se de conteúdo de saudação de um grupo de recursos antes de excluí-lo. portal de saudação exclui todos os recursos contidos no grupo de recursos hello, em seguida, exclui o grupo de recursos de saudação em si. Esse processo leva vários minutos.

## <a name="next-steps"></a>Próximas etapas

[Gerenciar zonas DNS](dns-operations-dnszones.md)

[Gerenciar registros DNS](dns-operations-recordsets.md)
