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
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a><span data-ttu-id="a2bd0-103">Configurar DNS reverso para serviços hospedados no Azure</span><span class="sxs-lookup"><span data-stu-id="a2bd0-103">Configure reverse DNS for services hosted in Azure</span></span>

<span data-ttu-id="a2bd0-104">Este artigo explica como tooconfigure inversas DNS para serviços hospedados no Azure.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-104">This article explains how tooconfigure reverse DNS lookups for services hosted in Azure.</span></span>

<span data-ttu-id="a2bd0-105">Os serviços no Azure usam endereços IP atribuídos pelo Azure e de propriedade da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-105">Services in Azure use IP addresses assigned by Azure and owned by Microsoft.</span></span> <span data-ttu-id="a2bd0-106">Esses registros DNS inversas (registros PTR) devem ser criados em Olá correspondente pertence à Microsoft inversa DNS zonas de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-106">These reverse DNS records (PTR records) must be created in hello corresponding Microsoft-owned reverse DNS lookup zones.</span></span> <span data-ttu-id="a2bd0-107">Este artigo explica como toodo isso.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-107">This article explains how toodo this.</span></span>

<span data-ttu-id="a2bd0-108">Este cenário não deve ser confundido com capacidade de saudação muito[host aos zonas de pesquisa inversas DNS de saudação para seus intervalos IP atribuídos no DNS do Azure](dns-reverse-dns-hosting.md).</span><span class="sxs-lookup"><span data-stu-id="a2bd0-108">This scenario should not be confused with hello ability too[host hello reverse DNS lookup zones for your assigned IP ranges in Azure DNS](dns-reverse-dns-hosting.md).</span></span> <span data-ttu-id="a2bd0-109">Nesse caso, os intervalos IP hello representados por zona de pesquisa inversa Olá devem ser atribuídos tooyour organização, normalmente por seu ISP.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-109">In this case, hello IP ranges represented by hello reverse lookup zone must be assigned tooyour organization, typically by your ISP.</span></span>

<span data-ttu-id="a2bd0-110">Antes de ler este artigo, você deve estar familiarizado com essa [Visão geral de DNS reverso e suporte no Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a2bd0-110">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="a2bd0-111">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a2bd0-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
* <span data-ttu-id="a2bd0-112">No modelo de implantação do Gerenciador de recursos de hello, recursos de computação (como máquinas virtuais, conjuntos de escala de máquina virtual ou clusters de malha do serviço) são expostos por meio de um recurso de PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-112">In hello Resource Manager deployment model, compute resources (such as virtual machines, virtual machine scale sets, or Service Fabric clusters) are exposed via a PublicIpAddress resource.</span></span> <span data-ttu-id="a2bd0-113">Pesquisas de DNS inversa são configuradas usando a propriedade 'ReverseFqdn' Olá Olá PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-113">Reverse DNS lookups are configured using hello 'ReverseFqdn' property of hello PublicIpAddress.</span></span>
* <span data-ttu-id="a2bd0-114">No modelo de implantação clássico hello, recursos de computação são expostos usando serviços em nuvem.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-114">In hello Classic deployment model, compute resources are exposed using Cloud Services.</span></span> <span data-ttu-id="a2bd0-115">Pesquisas de DNS inversa são configuradas usando a propriedade 'ReverseDnsFqdn' Olá Olá serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-115">Reverse DNS lookups are configured using hello 'ReverseDnsFqdn' property of hello Cloud Service.</span></span>

<span data-ttu-id="a2bd0-116">DNS inversa não é suportado atualmente para saudação do serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-116">Reverse DNS is not currently supported for hello Azure App Service.</span></span>

## <a name="validation-of-reverse-dns-records"></a><span data-ttu-id="a2bd0-117">Validação de registros DNS reversos</span><span class="sxs-lookup"><span data-stu-id="a2bd0-117">Validation of reverse DNS records</span></span>

<span data-ttu-id="a2bd0-118">Um terceiro não deve ser capaz de toocreate inversas registros de DNS para seus domínios DNS de tooyour de mapeamento de serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-118">A third party should not be able toocreate reverse DNS records for their Azure service mapping tooyour DNS domains.</span></span> <span data-ttu-id="a2bd0-119">tooprevent isso, a criação de um registro de DNS inverso, onde o nome de domínio especificado no registro DNS reverso Olá é Olá igual ou resolve para Olá nome DNS ou endereço IP de uma nuvem ou PublicIpAddress de serviço no hello mesmo Olá o Azure permite apenas assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-119">tooprevent this, Azure only allows hello creation of a reverse DNS record where domain name specified in hello reverse DNS record is hello same as, or resolves to, hello DNS name or IP address of a PublicIpAddress or Cloud Service in hello same Azure subscription.</span></span>

<span data-ttu-id="a2bd0-120">Essa validação é realizada somente quando o registro de DNS inverso hello está definido ou modificado.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-120">This validation is only performed when hello reverse DNS record is set or modified.</span></span> <span data-ttu-id="a2bd0-121">Uma nova validação periódica não é executada.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-121">Periodic re-validation is not performed.</span></span>

<span data-ttu-id="a2bd0-122">Por exemplo: suponha que Olá PublicIpAddress recurso tem Olá contosoapp1.northus.cloudapp.azure.com de nome DNS e endereço IP 23.96.52.53.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-122">For example: suppose hello PublicIpAddress resource has hello DNS name contosoapp1.northus.cloudapp.azure.com and IP address 23.96.52.53.</span></span> <span data-ttu-id="a2bd0-123">Olá ReverseFqdn para Olá que publicipaddress pode ser especificado como:</span><span class="sxs-lookup"><span data-stu-id="a2bd0-123">hello ReverseFqdn for hello PublicIpAddress can be specified as:</span></span>
* <span data-ttu-id="a2bd0-124">nome DNS Olá Olá PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="a2bd0-124">hello DNS name for hello PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span></span>
* <span data-ttu-id="a2bd0-125">Olá nome DNS para um PublicIpAddress diferente no hello mesmo assinatura, como contosoapp2.westus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="a2bd0-125">hello DNS name for a different PublicIpAddress in hello same subscription, such as contosoapp2.westus.cloudapp.azure.com</span></span>
* <span data-ttu-id="a2bd0-126">Um banido de nome DNS, como app1.contoso.com, desde que esse nome é *primeiro* configurado como um CNAME toocontosoapp1.northus.cloudapp.azure.com ou tooa PublicIpAddress diferentes no hello mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-126">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as a CNAME toocontosoapp1.northus.cloudapp.azure.com, or tooa different PublicIpAddress in hello same subscription.</span></span>
* <span data-ttu-id="a2bd0-127">Um banido de nome DNS, como app1.contoso.com, desde que esse nome é *primeiro* configurado como um endereço IP um registro toohello 23.96.52.53 ou endereço IP toohello um PublicIpAddress diferente no hello mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-127">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as an A record toohello IP address 23.96.52.53, or toohello IP address of a different PublicIpAddress in hello same subscription.</span></span>

<span data-ttu-id="a2bd0-128">Olá mesmas restrições se aplicam tooreverse DNS para serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-128">hello same constraints apply tooreverse DNS for Cloud Services.</span></span>


## <a name="reverse-dns-for-publicipaddress-resources"></a><span data-ttu-id="a2bd0-129">DNS reverso para recursos de PublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="a2bd0-129">Reverse DNS for PublicIpAddress resources</span></span>

<span data-ttu-id="a2bd0-130">Esta seção fornece instruções detalhadas sobre como tooconfigure pesquisa reversa de DNS para os recursos de PublicIpAddress no modelo de implantação do Gerenciador de recursos de hello, usando o PowerShell do Azure, Azure CLI 1.0 ou 2.0 do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-130">This section provides detailed instructions for how tooconfigure reverse DNS for PublicIpAddress resources in hello Resource Manager deployment model, using either Azure PowerShell, Azure CLI 1.0, or Azure CLI 2.0.</span></span> <span data-ttu-id="a2bd0-131">Não é suportada atualmente ao configurar reversa de DNS para os recursos de PublicIpAddress via Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-131">Configuring reverse DNS for PublicIpAddress resources is not currently supported via hello Azure portal.</span></span>

<span data-ttu-id="a2bd0-132">O Azure atualmente oferece suporte a DNS reverso somente para recursos PublicIpAddress de IPv4.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-132">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources.</span></span> <span data-ttu-id="a2bd0-133">Não há suporte para IPv6.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-133">It is not supported for IPv6.</span></span>

### <a name="add-reverse-dns-tooan-existing-publicipaddresses"></a><span data-ttu-id="a2bd0-134">Adicionar tooan inversa de DNS existente PublicIpAddresses</span><span class="sxs-lookup"><span data-stu-id="a2bd0-134">Add reverse DNS tooan existing PublicIpAddresses</span></span>

#### <a name="powershell"></a><span data-ttu-id="a2bd0-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2bd0-135">PowerShell</span></span>

<span data-ttu-id="a2bd0-136">tooadd inversa DNS tooan existente PublicIpAddress:</span><span class="sxs-lookup"><span data-stu-id="a2bd0-136">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

<span data-ttu-id="a2bd0-137">tooadd inversa DNS tooan existente PublicIpAddress que ainda não tiver um nome DNS, você também deve especificar um nome DNS:</span><span class="sxs-lookup"><span data-stu-id="a2bd0-137">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="a2bd0-138">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="a2bd0-138">Azure CLI 1.0</span></span>

<span data-ttu-id="a2bd0-139">tooadd inversa DNS tooan existente PublicIpAddress:</span><span class="sxs-lookup"><span data-stu-id="a2bd0-139">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="a2bd0-140">tooadd inversa DNS tooan existente PublicIpAddress que ainda não tiver um nome DNS, você também deve especificar um nome DNS:</span><span class="sxs-lookup"><span data-stu-id="a2bd0-140">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="a2bd0-141">CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="a2bd0-141">Azure CLI 2.0</span></span>

<span data-ttu-id="a2bd0-142">tooadd inversa DNS tooan existente PublicIpAddress:</span><span class="sxs-lookup"><span data-stu-id="a2bd0-142">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="a2bd0-143">tooadd inversa DNS tooan existente PublicIpAddress que ainda não tiver um nome DNS, você também deve especificar um nome DNS:</span><span class="sxs-lookup"><span data-stu-id="a2bd0-143">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a><span data-ttu-id="a2bd0-144">Criar um Endereço IP Público com DNS reverso</span><span class="sxs-lookup"><span data-stu-id="a2bd0-144">Create a Public IP Address with reverse DNS</span></span>

<span data-ttu-id="a2bd0-145">toocreate um novo PublicIpAddress com a propriedade DNS reverso Olá já especificada:</span><span class="sxs-lookup"><span data-stu-id="a2bd0-145">toocreate a new PublicIpAddress with hello reverse DNS property already specified:</span></span>

#### <a name="powershell"></a><span data-ttu-id="a2bd0-146">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2bd0-146">PowerShell</span></span>

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a><span data-ttu-id="a2bd0-147">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="a2bd0-147">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="a2bd0-148">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="a2bd0-148">Azure CLI 2.0</span></span>

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a><span data-ttu-id="a2bd0-149">Exibir o DNS reverso para um PublicIpAddress existente</span><span class="sxs-lookup"><span data-stu-id="a2bd0-149">View reverse DNS for an existing PublicIpAddress</span></span>

<span data-ttu-id="a2bd0-150">Olá tooview valor configurado para um PublicIpAddress existente:</span><span class="sxs-lookup"><span data-stu-id="a2bd0-150">tooview hello configured value for an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="a2bd0-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2bd0-151">PowerShell</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a><span data-ttu-id="a2bd0-152">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="a2bd0-152">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a><span data-ttu-id="a2bd0-153">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="a2bd0-153">Azure CLI 2.0</span></span>

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a><span data-ttu-id="a2bd0-154">Remover o DNS reverso de Endereços IP Públicos existentes</span><span class="sxs-lookup"><span data-stu-id="a2bd0-154">Remove reverse DNS from existing Public IP Addresses</span></span>

<span data-ttu-id="a2bd0-155">tooremove uma propriedade DNS inversa de um PublicIpAddress existente:</span><span class="sxs-lookup"><span data-stu-id="a2bd0-155">tooremove a reverse DNS property from an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="a2bd0-156">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2bd0-156">PowerShell</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="a2bd0-157">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="a2bd0-157">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a><span data-ttu-id="a2bd0-158">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="a2bd0-158">Azure CLI 2.0</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a><span data-ttu-id="a2bd0-159">Configurar o DNS reverso para Serviços de Nuvem</span><span class="sxs-lookup"><span data-stu-id="a2bd0-159">Configure reverse DNS for Cloud Services</span></span>

<span data-ttu-id="a2bd0-160">Esta seção fornece instruções detalhadas sobre como tooconfigure pesquisa reversa de DNS para serviços de nuvem no modelo de implantação clássico hello, usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-160">This section provides detailed instructions for how tooconfigure reverse DNS for Cloud Services in hello Classic deployment model, using Azure PowerShell.</span></span> <span data-ttu-id="a2bd0-161">Configuração do DNS reverso para serviços de nuvem não é suportado por meio de saudação portal do Azure, Azure CLI 1.0 ou 2.0 do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-161">Configuring reverse DNS for Cloud Services is not supported via hello Azure portal, Azure CLI 1.0, or Azure CLI 2.0.</span></span>

### <a name="add-reverse-dns-tooexisting-cloud-services"></a><span data-ttu-id="a2bd0-162">Adicionar serviços de nuvem de tooexisting DNS inversa</span><span class="sxs-lookup"><span data-stu-id="a2bd0-162">Add reverse DNS tooexisting Cloud Services</span></span>

<span data-ttu-id="a2bd0-163">tooadd um tooan de registro DNS inversa existente de serviço de nuvem:</span><span class="sxs-lookup"><span data-stu-id="a2bd0-163">tooadd a reverse DNS record tooan existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a><span data-ttu-id="a2bd0-164">Criar um Serviço de Nuvem com DNS reverso</span><span class="sxs-lookup"><span data-stu-id="a2bd0-164">Create a Cloud Service with reverse DNS</span></span>

<span data-ttu-id="a2bd0-165">toocreate um novo serviço de nuvem com a propriedade DNS reversa Olá já especificada:</span><span class="sxs-lookup"><span data-stu-id="a2bd0-165">toocreate a new Cloud Service with hello reverse DNS property already specified:</span></span>

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a><span data-ttu-id="a2bd0-166">Exibir o DNS reverso dos Serviços de Nuvem existentes</span><span class="sxs-lookup"><span data-stu-id="a2bd0-166">View reverse DNS for existing Cloud Services</span></span>

<span data-ttu-id="a2bd0-167">propriedade inversa de DNS para um serviço de nuvem existente da saudação tooview:</span><span class="sxs-lookup"><span data-stu-id="a2bd0-167">tooview hello reverse DNS property for an existing Cloud Service:</span></span>

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a><span data-ttu-id="a2bd0-168">Remover o DNS reverso dos Serviços de Nuvem existentes</span><span class="sxs-lookup"><span data-stu-id="a2bd0-168">Remove reverse DNS from existing Cloud Services</span></span>

<span data-ttu-id="a2bd0-169">tooremove uma propriedade DNS inversa de um serviço de nuvem existente:</span><span class="sxs-lookup"><span data-stu-id="a2bd0-169">tooremove a reverse DNS property from an existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a><span data-ttu-id="a2bd0-170">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="a2bd0-170">FAQ</span></span>

### <a name="how-much-do-reverse-dns-records-cost"></a><span data-ttu-id="a2bd0-171">Qual é o custo dos registros DNS reversos?</span><span class="sxs-lookup"><span data-stu-id="a2bd0-171">How much do reverse DNS records cost?</span></span>

<span data-ttu-id="a2bd0-172">Eles são gratuitos!</span><span class="sxs-lookup"><span data-stu-id="a2bd0-172">They're free!</span></span>  <span data-ttu-id="a2bd0-173">Não há nenhum custo adicional para registros DNS reversos ou consultas.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-173">There is no additional cost for reverse DNS records or queries.</span></span>

### <a name="will-my-reverse-dns-records-resolve-from-hello-internet"></a><span data-ttu-id="a2bd0-174">Minha solução de registros DNS inversa de Olá a internet?</span><span class="sxs-lookup"><span data-stu-id="a2bd0-174">Will my reverse DNS records resolve from hello internet?</span></span>

<span data-ttu-id="a2bd0-175">Sim.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-175">Yes.</span></span> <span data-ttu-id="a2bd0-176">Depois de definir a propriedade DNS reversa Olá para o serviço do Azure, o Azure gerencia todas as delegações de DNS hello e zonas DNS necessário tooensure que o registro de DNS inversa resolve para todos os usuários da Internet.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-176">Once you set hello reverse DNS property for your Azure service, Azure manages all hello DNS delegations and DNS zones required tooensure that reverse DNS record resolves for all Internet users.</span></span>

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a><span data-ttu-id="a2bd0-177">Os registros DNS reversos padrão serão criados para meus serviços do Azure?</span><span class="sxs-lookup"><span data-stu-id="a2bd0-177">Are default reverse DNS records created for my Azure services?</span></span>

<span data-ttu-id="a2bd0-178">Não.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-178">No.</span></span> <span data-ttu-id="a2bd0-179">O DNS reverso é um recurso opcional.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-179">Reverse DNS is an opt-in feature.</span></span> <span data-ttu-id="a2bd0-180">Nenhum padrão de registros DNS reversos serão criados se você escolher não tooconfigure-los.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-180">No default reverse DNS records are created if you choose not tooconfigure them.</span></span>

### <a name="what-is-hello-format-for-hello-fully-qualified-domain-name-fqdn"></a><span data-ttu-id="a2bd0-181">O que é o formato de saudação para nome de domínio totalmente qualificado (FQDN) do hello?</span><span class="sxs-lookup"><span data-stu-id="a2bd0-181">What is hello format for hello fully-qualified domain name (FQDN)?</span></span>

<span data-ttu-id="a2bd0-182">Os FQDNs são especificados em ordem crescente e devem terminar com um ponto (por exemplo, “app1.contoso.com.”).</span><span class="sxs-lookup"><span data-stu-id="a2bd0-182">FQDNs are specified in forward order, and must be terminated by a dot (for example, "app1.contoso.com.").</span></span>

### <a name="what-happens-if-hello-validation-check-for-hello-reverse-dns-ive-specified-fails"></a><span data-ttu-id="a2bd0-183">O que acontece se a verificação de validação de saudação de saudação inversa de DNS que você especificou falhar?</span><span class="sxs-lookup"><span data-stu-id="a2bd0-183">What happens if hello validation check for hello reverse DNS I've specified fails?</span></span>

<span data-ttu-id="a2bd0-184">Onde hello inversa DNS a verificação de validação falha, Olá operação tooconfigure Olá inversa DNS registro falhará.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-184">Where hello reverse DNS validation check fails, hello operation tooconfigure hello reverse DNS record fails.</span></span> <span data-ttu-id="a2bd0-185">Corrija o valor DNS reverso Olá conforme necessário e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-185">Correct hello reverse DNS value as required, and retry.</span></span>

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a><span data-ttu-id="a2bd0-186">Posso configurar o DNS reverso para o Serviço de Aplicativo do Azure?</span><span class="sxs-lookup"><span data-stu-id="a2bd0-186">Can I configure reverse DNS for Azure App Service?</span></span>

<span data-ttu-id="a2bd0-187">Não.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-187">No.</span></span> <span data-ttu-id="a2bd0-188">Não há suporte para reversa de DNS de saudação do serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-188">Reverse DNS is not supported for hello Azure App Service.</span></span>

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a><span data-ttu-id="a2bd0-189">Posso configurar vários registros DNS reversos para meu serviço do Azure?</span><span class="sxs-lookup"><span data-stu-id="a2bd0-189">Can I configure multiple reverse DNS records for my Azure service?</span></span>

<span data-ttu-id="a2bd0-190">Não.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-190">No.</span></span> <span data-ttu-id="a2bd0-191">O Azure dá suporte a um único registro DNS reverso por Serviço de Nuvem do Azure ou PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-191">Azure supports a single reverse DNS record for each Azure Cloud Service or PublicIpAddress.</span></span>

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a><span data-ttu-id="a2bd0-192">Posso configurar o DNS reverso para recursos de PublicIpAddress do IPv6?</span><span class="sxs-lookup"><span data-stu-id="a2bd0-192">Can I configure reverse DNS for IPv6 PublicIpAddress resources?</span></span>

<span data-ttu-id="a2bd0-193">Não.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-193">No.</span></span> <span data-ttu-id="a2bd0-194">O Azure atualmente oferece suporte a DNS reverso somente para recursos PublicIpAddress de IPv4 e Serviços de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-194">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources and Cloud Services.</span></span>

### <a name="can-i-send-emails-tooexternal-domains-from-my-azure-compute-services"></a><span data-ttu-id="a2bd0-195">Posso enviar emails tooexternal domínios de meus serviços de computação do Azure?</span><span class="sxs-lookup"><span data-stu-id="a2bd0-195">Can I send emails tooexternal domains from my Azure Compute services?</span></span>

<span data-ttu-id="a2bd0-196">Não.</span><span class="sxs-lookup"><span data-stu-id="a2bd0-196">No.</span></span> [<span data-ttu-id="a2bd0-197">Serviços de computação do Azure não oferecem suporte a domínios de tooexternal enviando emails</span><span class="sxs-lookup"><span data-stu-id="a2bd0-197">Azure Compute services do not support sending emails tooexternal domains</span></span>](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)

## <a name="next-steps"></a><span data-ttu-id="a2bd0-198">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a2bd0-198">Next steps</span></span>

<span data-ttu-id="a2bd0-199">Para saber mais sobre DNS reverso, confira [Pesquisa de DNS reverso na Wikipédia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="a2bd0-199">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="a2bd0-200">Saiba como muito[zona de pesquisa inversa de saudação de host para o intervalo IP atribuído pelo ISP no DNS do Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="a2bd0-200">Learn how too[host hello reverse lookup zone for your ISP-assigned IP range in Azure DNS](dns-reverse-dns-for-azure-services.md).</span></span>

