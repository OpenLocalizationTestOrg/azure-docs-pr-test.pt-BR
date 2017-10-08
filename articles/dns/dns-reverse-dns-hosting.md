---
title: aaaHosting inverter as zonas de pesquisa DNS no DNS do Azure | Microsoft Docs
description: "Saiba como saudação do toouse DNS do Azure toohost inverter as zonas de pesquisa DNS para seus intervalos de IP"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: 24feb8ef1c75a7d91938867f348fed1190046e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a>Hospedagem de zonas de pesquisa de DNS reverso no Azure DNS

Este artigo explica como toohost Olá inverter as zonas de pesquisa DNS para seus intervalos IP atribuídos no DNS do Azure. os intervalos IP Hello representados por zona de pesquisa inversa Olá devem ser atribuídos tooyour organização, normalmente por seu ISP.

tooconfigure inversa de DNS para a propriedade Azure IP endereço atribuído tooyour serviço do Azure, consulte [Configurar pesquisa inversa Olá para endereços IP de saudação alocados tooyour serviço do Azure](dns-reverse-dns-for-azure-services.md).

Antes de ler este artigo, você deve estar familiarizado com essa [Visão geral de DNS reverso e suporte no Azure](dns-reverse-dns-overview.md).

Este artigo orienta Olá etapas toocreate sua primeira zona pesquisa inversa de DNS e o registro usando Olá portal do Azure, o PowerShell do Azure, Azure CLI 1.0 ou 2.0 do CLI do Azure.

## <a name="create-a-reverse-lookup-dns-zone"></a>Criar uma zona DNS de pesquisa inversa

1. Entrar toohello [portal do Azure](https://portal.azure.com)
1. No menu de Hub hello, clique em e clique em **novo** > **rede** > e, em seguida, clique em **zona DNS** tooopen Olá **zona DNS criar**folha.

   ![Zona DNS](./media/dns-reverse-dns-hosting/figure1.png)

1. Em Olá **zona DNS criar** folha, nomeie a zona DNS. nome de saudação da zona de saudação é criado diferente para os prefixos de IPv4 e IPv6. Use qualquer instruções Olá para [IPV4](#ipv4) ou [IPv6](#ipv6) tooname a zona. Quando concluir clique **criar** toocreate zona de saudação.

### <a name="ipv4"></a>IPv4

nome de saudação de uma zona de pesquisa inversa IPv4 é baseado no intervalo IP hello representa. Ele deve estar no hello formato a seguir: `<IPv4 network prefix in reverse order>.in-addr.arpa`. Para obter exemplos, veja [Visão geral de DNS reverso e suporte no Azure](dns-reverse-dns-overview.md#ipv4).

> [!NOTE]
> Ao criar classless zonas de pesquisa DNS inversas no DNS do Azure, você deve usar um hífen (`-`) em vez de uma barra invertida ('/ ') no nome da zona hello.
>
> Por exemplo, para Olá IP intervalo 192.0.2.128/26, você deve usar `128-26.2.0.192.in-addr.arpa` como nome da zona Olá em vez de `128/26.2.0.192.in-addr.arpa`.
>
> Isso ocorre porque, enquanto ambos têm suporte pelos padrões de DNS hello, nomes que contenham barra Olá da zona DNS (`/`) não há suporte para caracteres no DNS do Azure.

Olá exemplo a seguir mostra como toocreate uma 'classe C' Reverter zona DNS denominada `2.0.192.in-addr.arpa` no DNS do Azure por meio de saudação portal do Azure:

 ![criar zona DNS](./media/dns-reverse-dns-hosting/figure2.png)

Olá 'Local do grupo de recursos' define o local Olá Olá para grupo de recursos e não tem nenhum impacto na zona DNS de saudação. local da zona DNS Olá é sempre 'global' e não será exibida.

Olá exemplos a seguir mostram como toocomplete essa tarefa com o PowerShell do Azure e hello CLI do Azure:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a>CLI 1.0 do Azure

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a>CLI 2.0 do Azure

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a>IPv6

nome de saudação de uma zona de pesquisa inversa IPv6 deve estar no hello formulário a seguir: `<IPv6 network prefix in reverse order>.ip6.arpa`.  Para obter exemplos, veja [Visão geral de DNS reverso e suporte no Azure](dns-reverse-dns-overview.md#ipv6).


Olá exemplo a seguir mostra como toocreate uma zona de pesquisa inversa DNS IPv6 nomeados `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` no DNS do Azure por meio de saudação portal do Azure:

 ![criar zona DNS](./media/dns-reverse-dns-hosting/figure3.png)

Olá 'Local do grupo de recursos' define o local Olá Olá para grupo de recursos e não tem nenhum impacto na zona DNS de saudação. local da zona DNS Olá é sempre 'global' e não será exibida.

Olá exemplos a seguir mostram como toocomplete essa tarefa com o PowerShell do Azure e hello CLI do Azure:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a>AzureCLI 1.0

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a>AzureCLI 2.0

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a>Delegar uma zona de pesquisa inversa de DNS

Tendo criado a zona de pesquisa inversa do DNS, você deve garantir que zona Olá é delegada da zona pai de saudação. Delegação de DNS permite Olá resolução processo toofind Olá nome servidores de nome DNS hospeda a zona de pesquisa inversa do DNS. Isso permite que esses servidores tooanswer DNS inversas consultas de nomes para endereços IP de saudação em seu intervalo de endereços.

Zonas de pesquisa direta, o processo de saudação de delegação de zona DNS é descrito em [delegar tooAzure seu domínio DNS](dns-delegate-domain-azure-dns.md). A delegação para zonas de pesquisa inversa funciona Olá mesma maneira. Olá única diferença é que você precisa de servidores de nome de saudação tooconfigure com hello ISP que forneceu o intervalo de IP, em vez de seu registrador de nome de domínio.

## <a name="create-a-dns-ptr-record"></a>Criar um registro PTR DNS

### <a name="ipv4"></a>IPv4

Olá exemplo a seguir orienta Olá processo de criação de um registro PTR em uma zona DNS inversa no DNS do Azure. Para outros tipos de registro e toomodify os registros existentes, consulte [registros DNS de gerenciar e conjuntos de registros usando Olá portal do Azure](dns-operations-recordsets-portal.md).

1.  Na parte superior de saudação do hello **zona DNS** folha, selecione **+ registrar conjunto** tooopen Olá **Adicionar conjunto de registros** folha.

 ![Zona DNS](./media/dns-reverse-dns-hosting/figure4.png)

1. Em Olá **Adicionar conjunto de registros** folha. 
1. Selecione **PTR** do registro hello "**tipo**" menu.  
1. Olá nome do conjunto de registros de saudação para um registro PTR precisa toobe restante Olá Olá endereço IPv4 na ordem inversa. Neste exemplo, hello três primeiros octetos já foram preenchidos como parte do nome da zona hello (.2.0.192). Portanto, apenas Olá último octeto é fornecido no campo de nome de saudação. Por exemplo, você poderia nomear seu conjunto de registros "**15**" para um recurso cujo endereço IP é 192.0.2.15.  
1. Em hello "**nome de domínio**", digite o nome de domínio totalmente qualificado (FQDN) saudação do recurso hello usando IP hello.
1. Selecione **Okey** na parte inferior da saudação de registro DNS Olá folha toocreate hello.

 ![adicionar conjunto de registros](./media/dns-reverse-dns-hosting/figure5.png)

Olá, a seguir estão exemplos sobre como toocomplete essa tarefa com o PowerShell e hello AzureCLI:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a>AzureCLI 1.0

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a>AzureCLI 2.0

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a>IPv6

Olá exemplo a seguir orienta você pelo processo de saudação de criar um novo registro de 'PTR'. Para outros tipos de registro e toomodify os registros existentes, consulte [registros DNS de gerenciar e conjuntos de registros usando Olá portal do Azure](dns-operations-recordsets-portal.md).

1. Na parte superior de saudação do hello **folha de zona DNS**, selecione **+ registrar conjunto** tooopen Olá **Adicionar conjunto de registros** folha.

  ![folha de zona DNS](./media/dns-reverse-dns-hosting/figure6.png)

2. Em Olá **Adicionar conjunto de registros** folha. 
3. Selecione **PTR** do registro hello "**tipo**" menu.  
4. Olá nome do conjunto de registros de saudação para um registro PTR precisa toobe restante Olá Olá endereço IPv6 na ordem inversa. Ele não deve incluir compactação. Neste exemplo, Olá primeiros 64 bits do hello IPv6 já foram preenchidos como parte do nome da zona hello (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa). Portanto, Olá últimos 64 bits são fornecidos no campo de nome de saudação. Olá últimos 64 bits do endereço IP de saudação são inseridos na ordem inversa, usando um período como o delimitador de saudação entre cada número hexadecimal. Por exemplo, você poderia nomear seu conjunto de registros "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" para um recurso cujo endereço IP é 2001:0db8:abdc:0000:f524:10bc:1af9:405e.  
5. Em hello "**nome de domínio**", digite o nome de domínio totalmente qualificado (FQDN) saudação do recurso hello usando IP hello.
6. Selecione **Okey** na parte inferior da saudação de registro DNS Olá folha toocreate hello.

![adicionar conjunto de registros](./media/dns-reverse-dns-hosting/figure7.png)

Olá, a seguir estão exemplos sobre como toocomplete essa tarefa com o PowerShell e hello AzureCLI:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a>AzureCLI 1.0

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a>AzureCLI 2.0

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a>Exibir registros

registros de saudação tooview você criou, navegue tooyour zona DNS no hello portal do Azure. Em Olá diminuir parte da saudação **zona DNS** folha, você pode ver registros Olá para a zona DNS de saudação. Você deve ver o saudação padrão registros NS e SOA, que são criados em cada região, além de quaisquer novos registros que você criou.

### <a name="ipv4"></a>IPv4

Folha de zona DNS, mostrando os registros PTR de IPv4:

![folha de zona DNS](./media/dns-reverse-dns-hosting/figure8.png)

Olá exemplos a seguir mostram como tooview Olá PTR registros usando o PowerShell ou Olá CLI do Azure:

#### <a name="powershell"></a>PowerShell

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a>CLI 1.0 do Azure

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a>CLI 2.0 do Azure

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a>IPv6

Folha de zona DNS, mostrando os registros PTR de IPv6:

![folha de zona DNS](./media/dns-reverse-dns-hosting/figure9.png)

Olá seguem exemplos de como Olá tooview registros com o PowerShell e Olá AzureCLI:

#### <a name="powershell"></a>PowerShell

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a>CLI 1.0 do Azure

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a>CLI 2.0 do Azure

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a>Perguntas frequentes

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a>Posso hospedar zonas de pesquisa inversa de DNS para meus blocos IP atribuídos pelo ISP no DNS do Azure?

Sim. Hospedagem de zonas de pesquisa inversa (ARPA) Olá para seus próprios intervalos de IP no DNS do Azure tem suporte total.

Criar uma zona de pesquisa inversa de Olá em DNS do Azure como explicado neste artigo, e trabalhar com seu ISP muito[delegado Olá zona](dns-domain-delegation.md).  Você pode gerenciar os registros PTR Olá para cada pesquisa inversa no hello mesma maneira que outros tipos de registro.

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a>Quanto custa hospedar minha zona de pesquisa inverso de DNS?

Zona de pesquisa DNS inversa Olá de hospedagem para o bloco IP atribuído pelo ISP no DNS do Azure é cobrado nos [taxas de DNS do Azure padrão](https://azure.microsoft.com/pricing/details/dns/).

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a>Posso hospedar zonas de pesquisa inversa de DNS para endereços IPv4 e IPv6 no DNS do Azure?

Sim. Este artigo explica como toocreate IPv4 e IPv6 inverter as zonas de pesquisa DNS no DNS do Azure.

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a>Posso importar uma zona de pesquisa inversa de DNS existente?

Sim. Você pode usar o hello CLI do Azure tooimport existentes zonas do DNS no DNS do Azure. Isso funciona para zonas de pesquisa direta e zonas de pesquisa inversa.

Para obter mais informações, consulte [Olá importar e exportar um arquivo de zona DNS usando a CLI do Azure](dns-import-export.md).

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre DNS reverso, confira [Pesquisa de DNS reverso na Wikipédia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).
<br>
Saiba como muito[gerenciar registros DNS reversos para os serviços do Azure](dns-reverse-dns-for-azure-services.md).
