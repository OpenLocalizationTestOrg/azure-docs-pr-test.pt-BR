---
title: "DNS reverso para serviços do Azure | Microsoft Docs"
description: "Saiba como configurar pesquisas inversas de DNS para serviços hospedados no Azure"
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
ms.openlocfilehash: 63701e1ce0c1c6dcf2ce02ebce272b8280395e7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a><span data-ttu-id="7a3ad-103">Configurar DNS reverso para serviços hospedados no Azure</span><span class="sxs-lookup"><span data-stu-id="7a3ad-103">Configure reverse DNS for services hosted in Azure</span></span>

<span data-ttu-id="7a3ad-104">Este artigo explica como configurar pesquisas inversas de DNS para serviços hospedados no Azure.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-104">This article explains how to configure reverse DNS lookups for services hosted in Azure.</span></span>

<span data-ttu-id="7a3ad-105">Os serviços no Azure usam endereços IP atribuídos pelo Azure e de propriedade da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-105">Services in Azure use IP addresses assigned by Azure and owned by Microsoft.</span></span> <span data-ttu-id="7a3ad-106">Esses registros DNS reversos (registros PTR) devem ser criados nas zonas de pesquisa inversa de DNS de propriedade da Microsoft correspondentes.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-106">These reverse DNS records (PTR records) must be created in the corresponding Microsoft-owned reverse DNS lookup zones.</span></span> <span data-ttu-id="7a3ad-107">Esse artigo explica como fazer isso.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-107">This article explains how to do this.</span></span>

<span data-ttu-id="7a3ad-108">Este cenário não deve ser confundido com a capacidade de [hospedar as zonas de pesquisa inversa de DNS para seus intervalos de IP atribuídos no DNS do Azure](dns-reverse-dns-hosting.md).</span><span class="sxs-lookup"><span data-stu-id="7a3ad-108">This scenario should not be confused with the ability to [host the reverse DNS lookup zones for your assigned IP ranges in Azure DNS](dns-reverse-dns-hosting.md).</span></span> <span data-ttu-id="7a3ad-109">Nesse caso, os intervalos de IP representados pela zona de pesquisa inversa devem ser atribuídos à sua organização, normalmente por seu ISP.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-109">In this case, the IP ranges represented by the reverse lookup zone must be assigned to your organization, typically by your ISP.</span></span>

<span data-ttu-id="7a3ad-110">Antes de ler este artigo, você deve estar familiarizado com essa [Visão geral de DNS reverso e suporte no Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7a3ad-110">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="7a3ad-111">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7a3ad-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
* <span data-ttu-id="7a3ad-112">No modelo de implantação do Gerenciador de Recursos, os recursos de computação (como máquinas virtuais, conjuntos de escala de máquina virtual ou clusters do Service Fabric) são expostos por meio de um recurso de PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-112">In the Resource Manager deployment model, compute resources (such as virtual machines, virtual machine scale sets, or Service Fabric clusters) are exposed via a PublicIpAddress resource.</span></span> <span data-ttu-id="7a3ad-113">As pesquisas inversas de DNS são configuradas usando a propriedade 'ReverseFqdn' de PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-113">Reverse DNS lookups are configured using the 'ReverseFqdn' property of the PublicIpAddress.</span></span>
* <span data-ttu-id="7a3ad-114">No modelo de implantação clássico, os recursos de computação são expostos usando os Serviços de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-114">In the Classic deployment model, compute resources are exposed using Cloud Services.</span></span> <span data-ttu-id="7a3ad-115">As pesquisas inversas de DNS são configuradas usando a propriedade 'ReverseDnsFqdn' do Serviço de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-115">Reverse DNS lookups are configured using the 'ReverseDnsFqdn' property of the Cloud Service.</span></span>

<span data-ttu-id="7a3ad-116">O DNS reverso no momento não é suportado para o Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-116">Reverse DNS is not currently supported for the Azure App Service.</span></span>

## <a name="validation-of-reverse-dns-records"></a><span data-ttu-id="7a3ad-117">Validação de registros DNS reversos</span><span class="sxs-lookup"><span data-stu-id="7a3ad-117">Validation of reverse DNS records</span></span>

<span data-ttu-id="7a3ad-118">Uma terceira parte não deve ser capaz de criar registros DNS reversos para seu mapeamento de serviço do Azure para os domínios DNS.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-118">A third party should not be able to create reverse DNS records for their Azure service mapping to your DNS domains.</span></span> <span data-ttu-id="7a3ad-119">Para evitar isso, o Azure só permite a criação de um registro DNS reverso em que o nome de domínio especificado no registro de DNS reverso seja igual ou resolva para o nome DNS ou endereço IP de um PublicIpAddress ou um serviço de nuvem na mesma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-119">To prevent this, Azure only allows the creation of a reverse DNS record where domain name specified in the reverse DNS record is the same as, or resolves to, the DNS name or IP address of a PublicIpAddress or Cloud Service in the same Azure subscription.</span></span>

<span data-ttu-id="7a3ad-120">Essa validação é realizada somente quando o registro de DNS reverso é definido ou modificado.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-120">This validation is only performed when the reverse DNS record is set or modified.</span></span> <span data-ttu-id="7a3ad-121">Uma nova validação periódica não é executada.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-121">Periodic re-validation is not performed.</span></span>

<span data-ttu-id="7a3ad-122">Por exemplo: suponha que o recurso PublicIpAddress tenha o endereço IP 23.96.52.53 e contosoapp1.northus.cloudapp.azure.com de nome DNS.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-122">For example: suppose the PublicIpAddress resource has the DNS name contosoapp1.northus.cloudapp.azure.com and IP address 23.96.52.53.</span></span> <span data-ttu-id="7a3ad-123">O ReverseFqdn para o PublicIpAddress pode ser especificado como:</span><span class="sxs-lookup"><span data-stu-id="7a3ad-123">The ReverseFqdn for the PublicIpAddress can be specified as:</span></span>
* <span data-ttu-id="7a3ad-124">O nome DNS para o PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="7a3ad-124">The DNS name for the PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span></span>
* <span data-ttu-id="7a3ad-125">O nome DNS para um PublicIpAddress diferente na mesma assinatura, como contosoapp2.westus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="7a3ad-125">The DNS name for a different PublicIpAddress in the same subscription, such as contosoapp2.westus.cloudapp.azure.com</span></span>
* <span data-ttu-id="7a3ad-126">Um nome DNS personalizado, como app1.contoso.com, desde que esse nome seja *primeiro* configurado como um CNAME para contosoapp1.northus.cloudapp.azure.com ou um PublicIpAddress diferente na mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-126">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as a CNAME to contosoapp1.northus.cloudapp.azure.com, or to a different PublicIpAddress in the same subscription.</span></span>
* <span data-ttu-id="7a3ad-127">Um nome DNS personalizado, como app1.contoso.com, desde que esse nome seja *primeiro* configurado como um registro para o endereço IP 23.96.52.53 ou o endereço IP de um PublicIpAddress diferente na mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-127">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as an A record to the IP address 23.96.52.53, or to the IP address of a different PublicIpAddress in the same subscription.</span></span>

<span data-ttu-id="7a3ad-128">As mesmas restrições aplicam-se a DNS reverso para Serviços de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-128">The same constraints apply to reverse DNS for Cloud Services.</span></span>


## <a name="reverse-dns-for-publicipaddress-resources"></a><span data-ttu-id="7a3ad-129">DNS reverso para recursos de PublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="7a3ad-129">Reverse DNS for PublicIpAddress resources</span></span>

<span data-ttu-id="7a3ad-130">Esta seção fornece instruções detalhadas sobre como configurar o DNS reverso para recursos de PublicIpAddress no modelo de implantação do Gerenciador de Recursos, usando o Azure PowerShell, CLI 1.0 do Azure ou CLI 2.0 do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-130">This section provides detailed instructions for how to configure reverse DNS for PublicIpAddress resources in the Resource Manager deployment model, using either Azure PowerShell, Azure CLI 1.0, or Azure CLI 2.0.</span></span> <span data-ttu-id="7a3ad-131">Configurar o DNS reverso para recursos de PublicIpAddress não é suportado no momento por meio do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-131">Configuring reverse DNS for PublicIpAddress resources is not currently supported via the Azure portal.</span></span>

<span data-ttu-id="7a3ad-132">O Azure atualmente oferece suporte a DNS reverso somente para recursos PublicIpAddress de IPv4.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-132">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources.</span></span> <span data-ttu-id="7a3ad-133">Não há suporte para IPv6.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-133">It is not supported for IPv6.</span></span>

### <a name="add-reverse-dns-to-an-existing-publicipaddresses"></a><span data-ttu-id="7a3ad-134">Adicionar o DNS reverso a PublicIpAddresses existentes</span><span class="sxs-lookup"><span data-stu-id="7a3ad-134">Add reverse DNS to an existing PublicIpAddresses</span></span>

#### <a name="powershell"></a><span data-ttu-id="7a3ad-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7a3ad-135">PowerShell</span></span>

<span data-ttu-id="7a3ad-136">Para adicionar o DNS reverso ao PublicIpAddress existente:</span><span class="sxs-lookup"><span data-stu-id="7a3ad-136">To add reverse DNS to an existing PublicIpAddress:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

<span data-ttu-id="7a3ad-137">Para adicionar o DNS reverso a um PublicIpAddress existente que ainda não tenha um nome DNS, também deverá especificar um nome DNS:</span><span class="sxs-lookup"><span data-stu-id="7a3ad-137">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="7a3ad-138">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="7a3ad-138">Azure CLI 1.0</span></span>

<span data-ttu-id="7a3ad-139">Para adicionar o DNS reverso ao PublicIpAddress existente:</span><span class="sxs-lookup"><span data-stu-id="7a3ad-139">To add reverse DNS to an existing PublicIpAddress:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="7a3ad-140">Para adicionar o DNS reverso a um PublicIpAddress existente que ainda não tenha um nome DNS, também deverá especificar um nome DNS:</span><span class="sxs-lookup"><span data-stu-id="7a3ad-140">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="7a3ad-141">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="7a3ad-141">Azure CLI 2.0</span></span>

<span data-ttu-id="7a3ad-142">Para adicionar o DNS reverso ao PublicIpAddress existente:</span><span class="sxs-lookup"><span data-stu-id="7a3ad-142">To add reverse DNS to an existing PublicIpAddress:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="7a3ad-143">Para adicionar o DNS reverso a um PublicIpAddress existente que ainda não tenha um nome DNS, também deverá especificar um nome DNS:</span><span class="sxs-lookup"><span data-stu-id="7a3ad-143">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a><span data-ttu-id="7a3ad-144">Criar um Endereço IP Público com DNS reverso</span><span class="sxs-lookup"><span data-stu-id="7a3ad-144">Create a Public IP Address with reverse DNS</span></span>

<span data-ttu-id="7a3ad-145">Para criar um novo PublicIpAddress com a propriedade DNS reversa já especificada:</span><span class="sxs-lookup"><span data-stu-id="7a3ad-145">To create a new PublicIpAddress with the reverse DNS property already specified:</span></span>

#### <a name="powershell"></a><span data-ttu-id="7a3ad-146">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7a3ad-146">PowerShell</span></span>

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a><span data-ttu-id="7a3ad-147">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="7a3ad-147">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="7a3ad-148">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="7a3ad-148">Azure CLI 2.0</span></span>

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a><span data-ttu-id="7a3ad-149">Exibir o DNS reverso para um PublicIpAddress existente</span><span class="sxs-lookup"><span data-stu-id="7a3ad-149">View reverse DNS for an existing PublicIpAddress</span></span>

<span data-ttu-id="7a3ad-150">Para exibir o valor configurado para um PublicIpAddress existente:</span><span class="sxs-lookup"><span data-stu-id="7a3ad-150">To view the configured value for an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="7a3ad-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7a3ad-151">PowerShell</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a><span data-ttu-id="7a3ad-152">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="7a3ad-152">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a><span data-ttu-id="7a3ad-153">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="7a3ad-153">Azure CLI 2.0</span></span>

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a><span data-ttu-id="7a3ad-154">Remover o DNS reverso de Endereços IP Públicos existentes</span><span class="sxs-lookup"><span data-stu-id="7a3ad-154">Remove reverse DNS from existing Public IP Addresses</span></span>

<span data-ttu-id="7a3ad-155">Para remover uma propriedade de DNS reverso de um PublicIpAddress existente:</span><span class="sxs-lookup"><span data-stu-id="7a3ad-155">To remove a reverse DNS property from an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="7a3ad-156">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7a3ad-156">PowerShell</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="7a3ad-157">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="7a3ad-157">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a><span data-ttu-id="7a3ad-158">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="7a3ad-158">Azure CLI 2.0</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a><span data-ttu-id="7a3ad-159">Configurar o DNS reverso para Serviços de Nuvem</span><span class="sxs-lookup"><span data-stu-id="7a3ad-159">Configure reverse DNS for Cloud Services</span></span>

<span data-ttu-id="7a3ad-160">Esta seção fornece instruções detalhadas sobre como configurar o DNS reverso para Serviços de Nuvem no modelo de implantação clássico, usando o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-160">This section provides detailed instructions for how to configure reverse DNS for Cloud Services in the Classic deployment model, using Azure PowerShell.</span></span> <span data-ttu-id="7a3ad-161">Configurar o DNS reverso para Serviços de Nuvem não é suportado por meio do Portal do Azure, CLI 1.0 do Azure ou CLI 2.0 do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-161">Configuring reverse DNS for Cloud Services is not supported via the Azure portal, Azure CLI 1.0, or Azure CLI 2.0.</span></span>

### <a name="add-reverse-dns-to-existing-cloud-services"></a><span data-ttu-id="7a3ad-162">Adicionar DNS reverso aos Serviços de Nuvem existentes</span><span class="sxs-lookup"><span data-stu-id="7a3ad-162">Add reverse DNS to existing Cloud Services</span></span>

<span data-ttu-id="7a3ad-163">Para adicionar um registro DNS reverso a um Serviço de Nuvem existente:</span><span class="sxs-lookup"><span data-stu-id="7a3ad-163">To add a reverse DNS record to an existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a><span data-ttu-id="7a3ad-164">Criar um Serviço de Nuvem com DNS reverso</span><span class="sxs-lookup"><span data-stu-id="7a3ad-164">Create a Cloud Service with reverse DNS</span></span>

<span data-ttu-id="7a3ad-165">Para criar um novo Serviço de Nuvem com a propriedade DNS reversa já especificada:</span><span class="sxs-lookup"><span data-stu-id="7a3ad-165">To create a new Cloud Service with the reverse DNS property already specified:</span></span>

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a><span data-ttu-id="7a3ad-166">Exibir o DNS reverso dos Serviços de Nuvem existentes</span><span class="sxs-lookup"><span data-stu-id="7a3ad-166">View reverse DNS for existing Cloud Services</span></span>

<span data-ttu-id="7a3ad-167">Para exibir uma propriedade de DNS reverso para um Serviço de Nuvem existente:</span><span class="sxs-lookup"><span data-stu-id="7a3ad-167">To view the reverse DNS property for an existing Cloud Service:</span></span>

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a><span data-ttu-id="7a3ad-168">Remover o DNS reverso dos Serviços de Nuvem existentes</span><span class="sxs-lookup"><span data-stu-id="7a3ad-168">Remove reverse DNS from existing Cloud Services</span></span>

<span data-ttu-id="7a3ad-169">Para remover uma propriedade de DNS reverso de um Serviço de Nuvem existente:</span><span class="sxs-lookup"><span data-stu-id="7a3ad-169">To remove a reverse DNS property from an existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a><span data-ttu-id="7a3ad-170">FAQ</span><span class="sxs-lookup"><span data-stu-id="7a3ad-170">FAQ</span></span>

### <a name="how-much-do-reverse-dns-records-cost"></a><span data-ttu-id="7a3ad-171">Qual é o custo dos registros DNS reversos?</span><span class="sxs-lookup"><span data-stu-id="7a3ad-171">How much do reverse DNS records cost?</span></span>

<span data-ttu-id="7a3ad-172">Eles são gratuitos!</span><span class="sxs-lookup"><span data-stu-id="7a3ad-172">They're free!</span></span>  <span data-ttu-id="7a3ad-173">Não há nenhum custo adicional para registros DNS reversos ou consultas.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-173">There is no additional cost for reverse DNS records or queries.</span></span>

### <a name="will-my-reverse-dns-records-resolve-from-the-internet"></a><span data-ttu-id="7a3ad-174">Meus registros DNS reversos serão resolvidos na Internet?</span><span class="sxs-lookup"><span data-stu-id="7a3ad-174">Will my reverse DNS records resolve from the internet?</span></span>

<span data-ttu-id="7a3ad-175">Sim.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-175">Yes.</span></span> <span data-ttu-id="7a3ad-176">Depois de definir a propriedade de DNS reverso para seu Serviço do Azure, o Azure gerenciará todas as delegações de DNS e as zonas DNS necessárias para garantir que o registro DNS reverso seja resolvido para todos os usuários da Internet.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-176">Once you set the reverse DNS property for your Azure service, Azure manages all the DNS delegations and DNS zones required to ensure that reverse DNS record resolves for all Internet users.</span></span>

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a><span data-ttu-id="7a3ad-177">Os registros DNS reversos padrão serão criados para meus serviços do Azure?</span><span class="sxs-lookup"><span data-stu-id="7a3ad-177">Are default reverse DNS records created for my Azure services?</span></span>

<span data-ttu-id="7a3ad-178">Não.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-178">No.</span></span> <span data-ttu-id="7a3ad-179">O DNS reverso é um recurso opcional.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-179">Reverse DNS is an opt-in feature.</span></span> <span data-ttu-id="7a3ad-180">Nenhum registro DNS reverso padrão é criado se você optar por não configurar um.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-180">No default reverse DNS records are created if you choose not to configure them.</span></span>

### <a name="what-is-the-format-for-the-fully-qualified-domain-name-fqdn"></a><span data-ttu-id="7a3ad-181">Qual é o formato do FQDN (nome de domínio totalmente qualificado)?</span><span class="sxs-lookup"><span data-stu-id="7a3ad-181">What is the format for the fully-qualified domain name (FQDN)?</span></span>

<span data-ttu-id="7a3ad-182">Os FQDNs são especificados em ordem crescente e devem terminar com um ponto (por exemplo, “app1.contoso.com.”).</span><span class="sxs-lookup"><span data-stu-id="7a3ad-182">FQDNs are specified in forward order, and must be terminated by a dot (for example, "app1.contoso.com.").</span></span>

### <a name="what-happens-if-the-validation-check-for-the-reverse-dns-ive-specified-fails"></a><span data-ttu-id="7a3ad-183">O que acontecerá se ocorrer uma falha nas verificações de validação do DNS reverso especificado?</span><span class="sxs-lookup"><span data-stu-id="7a3ad-183">What happens if the validation check for the reverse DNS I've specified fails?</span></span>

<span data-ttu-id="7a3ad-184">Quando a verificação de validação de DNS reverso falhar, a operação para configurar o registro DNS reverso falhará.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-184">Where the reverse DNS validation check fails, the operation to configure the reverse DNS record fails.</span></span> <span data-ttu-id="7a3ad-185">Corrija o valor DNS reverso conforme necessário e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-185">Correct the reverse DNS value as required, and retry.</span></span>

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a><span data-ttu-id="7a3ad-186">Posso configurar o DNS reverso para o Serviço de Aplicativo do Azure?</span><span class="sxs-lookup"><span data-stu-id="7a3ad-186">Can I configure reverse DNS for Azure App Service?</span></span>

<span data-ttu-id="7a3ad-187">Não.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-187">No.</span></span> <span data-ttu-id="7a3ad-188">O DNS reverso não é suportado para o Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-188">Reverse DNS is not supported for the Azure App Service.</span></span>

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a><span data-ttu-id="7a3ad-189">Posso configurar vários registros DNS reversos para meu serviço do Azure?</span><span class="sxs-lookup"><span data-stu-id="7a3ad-189">Can I configure multiple reverse DNS records for my Azure service?</span></span>

<span data-ttu-id="7a3ad-190">Não.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-190">No.</span></span> <span data-ttu-id="7a3ad-191">O Azure dá suporte a um único registro DNS reverso por Serviço de Nuvem do Azure ou PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-191">Azure supports a single reverse DNS record for each Azure Cloud Service or PublicIpAddress.</span></span>

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a><span data-ttu-id="7a3ad-192">Posso configurar o DNS reverso para recursos de PublicIpAddress do IPv6?</span><span class="sxs-lookup"><span data-stu-id="7a3ad-192">Can I configure reverse DNS for IPv6 PublicIpAddress resources?</span></span>

<span data-ttu-id="7a3ad-193">Não.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-193">No.</span></span> <span data-ttu-id="7a3ad-194">O Azure atualmente oferece suporte a DNS reverso somente para recursos PublicIpAddress de IPv4 e Serviços de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-194">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources and Cloud Services.</span></span>

### <a name="can-i-send-emails-to-external-domains-from-my-azure-compute-services"></a><span data-ttu-id="7a3ad-195">Posso enviar emails a domínios externos de meus Serviços de Computação do Azure?</span><span class="sxs-lookup"><span data-stu-id="7a3ad-195">Can I send emails to external domains from my Azure Compute services?</span></span>

<span data-ttu-id="7a3ad-196">Não.</span><span class="sxs-lookup"><span data-stu-id="7a3ad-196">No.</span></span> [<span data-ttu-id="7a3ad-197">Os Serviços de Computação do Azure não oferecem suporte ao envio de emails a domínios externos</span><span class="sxs-lookup"><span data-stu-id="7a3ad-197">Azure Compute services do not support sending emails to external domains</span></span>](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)

## <a name="next-steps"></a><span data-ttu-id="7a3ad-198">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7a3ad-198">Next steps</span></span>

<span data-ttu-id="7a3ad-199">Para saber mais sobre DNS reverso, confira [Pesquisa de DNS reverso na Wikipédia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="7a3ad-199">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="7a3ad-200">Saiba como [hospedar a zona de pesquisa inversa para o intervalo de IP atribuído pelo ISP no DNS do Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="7a3ad-200">Learn how to [host the reverse lookup zone for your ISP-assigned IP range in Azure DNS](dns-reverse-dns-for-azure-services.md).</span></span>

