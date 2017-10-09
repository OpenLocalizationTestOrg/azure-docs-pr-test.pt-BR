---
title: "aaaReverse DNS para serviços do Azure | Microsoft Docs"
description: "Saiba como tooconfigure inversas DNS para serviços hospedados no Azure"
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
ms.openlocfilehash: c6fe1d80232f124be86dd7fc57abc20699be7eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a>Configurar DNS reverso para serviços hospedados no Azure

Este artigo explica como tooconfigure inversas DNS para serviços hospedados no Azure.

Os serviços no Azure usam endereços IP atribuídos pelo Azure e de propriedade da Microsoft. Esses registros DNS inversas (registros PTR) devem ser criados em Olá correspondente pertence à Microsoft inversa DNS zonas de pesquisa. Este artigo explica como toodo isso.

Este cenário não deve ser confundido com capacidade de saudação muito[host aos zonas de pesquisa inversas DNS de saudação para seus intervalos IP atribuídos no DNS do Azure](dns-reverse-dns-hosting.md). Nesse caso, os intervalos IP hello representados por zona de pesquisa inversa Olá devem ser atribuídos tooyour organização, normalmente por seu ISP.

Antes de ler este artigo, você deve estar familiarizado com essa [Visão geral de DNS reverso e suporte no Azure](dns-reverse-dns-overview.md).

O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md).
* No modelo de implantação do Gerenciador de recursos de hello, recursos de computação (como máquinas virtuais, conjuntos de escala de máquina virtual ou clusters de malha do serviço) são expostos por meio de um recurso de PublicIpAddress. Pesquisas de DNS inversa são configuradas usando a propriedade 'ReverseFqdn' Olá Olá PublicIpAddress.
* No modelo de implantação clássico hello, recursos de computação são expostos usando serviços em nuvem. Pesquisas de DNS inversa são configuradas usando a propriedade 'ReverseDnsFqdn' Olá Olá serviço de nuvem.

DNS inversa não é suportado atualmente para saudação do serviço de aplicativo do Azure.

## <a name="validation-of-reverse-dns-records"></a>Validação de registros DNS reversos

Um terceiro não deve ser capaz de toocreate inversas registros de DNS para seus domínios DNS de tooyour de mapeamento de serviço do Azure. tooprevent isso, a criação de um registro de DNS inverso, onde o nome de domínio especificado no registro DNS reverso Olá é Olá igual ou resolve para Olá nome DNS ou endereço IP de uma nuvem ou PublicIpAddress de serviço no hello mesmo Olá o Azure permite apenas assinatura do Azure.

Essa validação é realizada somente quando o registro de DNS inverso hello está definido ou modificado. Uma nova validação periódica não é executada.

Por exemplo: suponha que Olá PublicIpAddress recurso tem Olá contosoapp1.northus.cloudapp.azure.com de nome DNS e endereço IP 23.96.52.53. Olá ReverseFqdn para Olá que publicipaddress pode ser especificado como:
* nome DNS Olá Olá PublicIpAddress, contosoapp1.northus.cloudapp.azure.com
* Olá nome DNS para um PublicIpAddress diferente no hello mesmo assinatura, como contosoapp2.westus.cloudapp.azure.com
* Um banido de nome DNS, como app1.contoso.com, desde que esse nome é *primeiro* configurado como um CNAME toocontosoapp1.northus.cloudapp.azure.com ou tooa PublicIpAddress diferentes no hello mesma assinatura.
* Um banido de nome DNS, como app1.contoso.com, desde que esse nome é *primeiro* configurado como um endereço IP um registro toohello 23.96.52.53 ou endereço IP toohello um PublicIpAddress diferente no hello mesma assinatura.

Olá mesmas restrições se aplicam tooreverse DNS para serviços de nuvem.


## <a name="reverse-dns-for-publicipaddress-resources"></a>DNS reverso para recursos de PublicIpAddress

Esta seção fornece instruções detalhadas sobre como tooconfigure pesquisa reversa de DNS para os recursos de PublicIpAddress no modelo de implantação do Gerenciador de recursos de hello, usando o PowerShell do Azure, Azure CLI 1.0 ou 2.0 do CLI do Azure. Não é suportada atualmente ao configurar reversa de DNS para os recursos de PublicIpAddress via Olá portal do Azure.

O Azure atualmente oferece suporte a DNS reverso somente para recursos PublicIpAddress de IPv4. Não há suporte para IPv6.

### <a name="add-reverse-dns-tooan-existing-publicipaddresses"></a>Adicionar tooan inversa de DNS existente PublicIpAddresses

#### <a name="powershell"></a>PowerShell

tooadd inversa DNS tooan existente PublicIpAddress:

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

tooadd inversa DNS tooan existente PublicIpAddress que ainda não tiver um nome DNS, você também deve especificar um nome DNS:

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a>CLI 1.0 do Azure

tooadd inversa DNS tooan existente PublicIpAddress:

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

tooadd inversa DNS tooan existente PublicIpAddress que ainda não tiver um nome DNS, você também deve especificar um nome DNS:

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a>CLI do Azure 2.0

tooadd inversa DNS tooan existente PublicIpAddress:

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

tooadd inversa DNS tooan existente PublicIpAddress que ainda não tiver um nome DNS, você também deve especificar um nome DNS:

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a>Criar um Endereço IP Público com DNS reverso

toocreate um novo PublicIpAddress com a propriedade DNS reverso Olá já especificada:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a>CLI 1.0 do Azure

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a>CLI 2.0 do Azure

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a>Exibir o DNS reverso para um PublicIpAddress existente

Olá tooview valor configurado para um PublicIpAddress existente:

#### <a name="powershell"></a>PowerShell

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a>CLI 1.0 do Azure

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a>CLI 2.0 do Azure

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a>Remover o DNS reverso de Endereços IP Públicos existentes

tooremove uma propriedade DNS inversa de um PublicIpAddress existente:

#### <a name="powershell"></a>PowerShell

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a>CLI 1.0 do Azure

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a>CLI 2.0 do Azure

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a>Configurar o DNS reverso para Serviços de Nuvem

Esta seção fornece instruções detalhadas sobre como tooconfigure pesquisa reversa de DNS para serviços de nuvem no modelo de implantação clássico hello, usando o PowerShell do Azure. Configuração do DNS reverso para serviços de nuvem não é suportado por meio de saudação portal do Azure, Azure CLI 1.0 ou 2.0 do CLI do Azure.

### <a name="add-reverse-dns-tooexisting-cloud-services"></a>Adicionar serviços de nuvem de tooexisting DNS inversa

tooadd um tooan de registro DNS inversa existente de serviço de nuvem:

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a>Criar um Serviço de Nuvem com DNS reverso

toocreate um novo serviço de nuvem com a propriedade DNS reversa Olá já especificada:

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a>Exibir o DNS reverso dos Serviços de Nuvem existentes

propriedade inversa de DNS para um serviço de nuvem existente da saudação tooview:

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a>Remover o DNS reverso dos Serviços de Nuvem existentes

tooremove uma propriedade DNS inversa de um serviço de nuvem existente:

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a>Perguntas frequentes

### <a name="how-much-do-reverse-dns-records-cost"></a>Qual é o custo dos registros DNS reversos?

Eles são gratuitos!  Não há nenhum custo adicional para registros DNS reversos ou consultas.

### <a name="will-my-reverse-dns-records-resolve-from-hello-internet"></a>Minha solução de registros DNS inversa de Olá a internet?

Sim. Depois de definir a propriedade DNS reversa Olá para o serviço do Azure, o Azure gerencia todas as delegações de DNS hello e zonas DNS necessário tooensure que o registro de DNS inversa resolve para todos os usuários da Internet.

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a>Os registros DNS reversos padrão serão criados para meus serviços do Azure?

Não. O DNS reverso é um recurso opcional. Nenhum padrão de registros DNS reversos serão criados se você escolher não tooconfigure-los.

### <a name="what-is-hello-format-for-hello-fully-qualified-domain-name-fqdn"></a>O que é o formato de saudação para nome de domínio totalmente qualificado (FQDN) do hello?

Os FQDNs são especificados em ordem crescente e devem terminar com um ponto (por exemplo, “app1.contoso.com.”).

### <a name="what-happens-if-hello-validation-check-for-hello-reverse-dns-ive-specified-fails"></a>O que acontece se a verificação de validação de saudação de saudação inversa de DNS que você especificou falhar?

Onde hello inversa DNS a verificação de validação falha, Olá operação tooconfigure Olá inversa DNS registro falhará. Corrija o valor DNS reverso Olá conforme necessário e tente novamente.

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a>Posso configurar o DNS reverso para o Serviço de Aplicativo do Azure?

Não. Não há suporte para reversa de DNS de saudação do serviço de aplicativo do Azure.

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a>Posso configurar vários registros DNS reversos para meu serviço do Azure?

Não. O Azure dá suporte a um único registro DNS reverso por Serviço de Nuvem do Azure ou PublicIpAddress.

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a>Posso configurar o DNS reverso para recursos de PublicIpAddress do IPv6?

Não. O Azure atualmente oferece suporte a DNS reverso somente para recursos PublicIpAddress de IPv4 e Serviços de Nuvem.

### <a name="can-i-send-emails-tooexternal-domains-from-my-azure-compute-services"></a>Posso enviar emails tooexternal domínios de meus serviços de computação do Azure?

Não. [Serviços de computação do Azure não oferecem suporte a domínios de tooexternal enviando emails](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre DNS reverso, confira [Pesquisa de DNS reverso na Wikipédia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).
<br>
Saiba como muito[zona de pesquisa inversa de saudação de host para o intervalo IP atribuído pelo ISP no DNS do Azure](dns-reverse-dns-for-azure-services.md).

