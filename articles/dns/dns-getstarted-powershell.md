---
title: "Introdução ao DNS do Azure usando o PowerShell | Microsoft Docs"
description: "Saiba como criar uma zona e registro DNS no DNS do Azure. Este é uma guia passo a passo para criar e gerenciar sua primeira zona e registro DNS usando o PowerShell."
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
ms.openlocfilehash: 48f7ba325f61b4a91c0208b4c99058da801bee19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-dns-using-powershell"></a><span data-ttu-id="b9a92-104">Introdução ao DNS do Azure usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9a92-104">Get Started with Azure DNS using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b9a92-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b9a92-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="b9a92-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9a92-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="b9a92-107">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="b9a92-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="b9a92-108">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="b9a92-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="b9a92-109">Este artigo explica as etapas para criar sua primeira zona e registro DNS usando o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b9a92-109">This article walks you through the steps to create your first DNS zone and record using Azure PowerShell.</span></span> <span data-ttu-id="b9a92-110">Você também pode executar estas etapas usando o Portal do Azure ou a CLI do Azure de plataforma cruzada.</span><span class="sxs-lookup"><span data-stu-id="b9a92-110">You can also perform these steps using the Azure portal or the cross-platform Azure CLI.</span></span>

<span data-ttu-id="b9a92-111">Uma zona DNS é usada para hospedar os registros DNS para um domínio específico.</span><span class="sxs-lookup"><span data-stu-id="b9a92-111">A DNS zone is used to host the DNS records for a particular domain.</span></span> <span data-ttu-id="b9a92-112">Para iniciar a hospedagem do seu domínio no DNS do Azure, você precisará criar uma zona DNS para esse nome de domínio.</span><span class="sxs-lookup"><span data-stu-id="b9a92-112">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span></span> <span data-ttu-id="b9a92-113">Cada registro DNS para seu domínio é criado dentro dessa zona DNS.</span><span class="sxs-lookup"><span data-stu-id="b9a92-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="b9a92-114">Por fim, para publicar sua zona DNS na Internet, você precisa configurar os servidores de nome para o domínio.</span><span class="sxs-lookup"><span data-stu-id="b9a92-114">Finally, to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span></span> <span data-ttu-id="b9a92-115">Cada uma dessas etapas é descrita abaixo.</span><span class="sxs-lookup"><span data-stu-id="b9a92-115">Each of these steps is described below.</span></span>

<span data-ttu-id="b9a92-116">Essas instruções pressupõem que você já instalou e entrou no Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b9a92-116">These instructions assume you have already installed and signed in to Azure PowerShell.</span></span> <span data-ttu-id="b9a92-117">Para obter ajuda, confira [Como gerenciar as zonas DNS usando o PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="b9a92-117">For help, see [How to manage DNS zones using PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="b9a92-118">Criar o grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="b9a92-118">Create the resource group</span></span>

<span data-ttu-id="b9a92-119">Antes de criar a zona DNS, um grupo de recursos é criado para conter a zona DNS.</span><span class="sxs-lookup"><span data-stu-id="b9a92-119">Before creating the DNS zone, a resource group is created to contain the DNS Zone.</span></span> <span data-ttu-id="b9a92-120">O código a seguir mostra o comando.</span><span class="sxs-lookup"><span data-stu-id="b9a92-120">The following shows the command.</span></span>

```powershell
New-AzureRMResourceGroup -name MyResourceGroup -location "westus"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="b9a92-121">Criar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="b9a92-121">Create a DNS zone</span></span>

<span data-ttu-id="b9a92-122">Uma zona DNS é criada usando o cmdlet `New-AzureRmDnsZone` .</span><span class="sxs-lookup"><span data-stu-id="b9a92-122">A DNS zone is created by using the `New-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="b9a92-123">O exemplo a seguir cria uma zona DNS chamada *contoso.com* no grupo de recursos chamado *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="b9a92-123">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="b9a92-124">Use o exemplo para criar uma zona DNS, substituindo os valores pelos seus próprios.</span><span class="sxs-lookup"><span data-stu-id="b9a92-124">Use the example to create a DNS zone, substituting the values for your own.</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyResourceGroup
```

## <a name="create-a-dns-record"></a><span data-ttu-id="b9a92-125">Criar um registro DNS</span><span class="sxs-lookup"><span data-stu-id="b9a92-125">Create a DNS record</span></span>

<span data-ttu-id="b9a92-126">Você cria conjuntos de registros usando o cmdlet `New-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="b9a92-126">You create record sets by using the `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="b9a92-127">O exemplo a seguir cria um registro com o nome relativo "www" na Zona DNS "contoso.com", no grupo de recursos "MyResourceGroup".</span><span class="sxs-lookup"><span data-stu-id="b9a92-127">The following example creates a record with the relative name "www" in the DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="b9a92-128">O nome totalmente qualificado do conjunto de registros é “www.contoso.com”.</span><span class="sxs-lookup"><span data-stu-id="b9a92-128">The fully-qualified name of the record set is "www.contoso.com".</span></span> <span data-ttu-id="b9a92-129">O tipo de registro é "A", com o endereço IP "1.2.3.4" e a TTL de 3600 segundos.</span><span class="sxs-lookup"><span data-stu-id="b9a92-129">The record type is "A", with IP address "1.2.3.4", and the TTL is 3600 seconds.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName contoso.com -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4")
```

<span data-ttu-id="b9a92-130">Para outros tipos de registros, para conjuntos de registros com mais de um registro, e para modificar registros existentes, consulte [Gerenciar registros DNS e conjuntos de registros usando o Azure PowerShell](dns-operations-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="b9a92-130">For other record types, for record sets with more than one record, and to modify existing records, see [Manage DNS records and record sets using Azure PowerShell](dns-operations-recordsets.md).</span></span> 


## <a name="view-records"></a><span data-ttu-id="b9a92-131">Exibir registros</span><span class="sxs-lookup"><span data-stu-id="b9a92-131">View records</span></span>

<span data-ttu-id="b9a92-132">Para listar os registros DNS em sua zona, use:</span><span class="sxs-lookup"><span data-stu-id="b9a92-132">To list the DNS records in your zone, use:</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName contoso.com -ResourceGroupName MyResourceGroup
```


## <a name="update-name-servers"></a><span data-ttu-id="b9a92-133">Atualizar servidores de nome</span><span class="sxs-lookup"><span data-stu-id="b9a92-133">Update name servers</span></span>

<span data-ttu-id="b9a92-134">Quando você estiver satisfeito com a configuração de sua zona e registros DNS, configure seu nome de domínio para usar os servidores de nome DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9a92-134">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span></span> <span data-ttu-id="b9a92-135">Isso permite que outros usuários na Internet encontrem os registros DNS.</span><span class="sxs-lookup"><span data-stu-id="b9a92-135">This enables other users on the Internet to find your DNS records.</span></span>

<span data-ttu-id="b9a92-136">Os servidores de nomes de sua zona são fornecidos pelo cmdlet `Get-AzureRmDnsZone`:</span><span class="sxs-lookup"><span data-stu-id="b9a92-136">The name servers for your zone are given by the `Get-AzureRmDnsZone` cmdlet:</span></span>

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

<span data-ttu-id="b9a92-137">Esses servidores de nome devem ser configurados com o registrador de nome de domínio (onde você adquiriu o nome de domínio).</span><span class="sxs-lookup"><span data-stu-id="b9a92-137">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span></span> <span data-ttu-id="b9a92-138">Seu registrador oferecerá a opção de configurar os servidores de nome do domínio.</span><span class="sxs-lookup"><span data-stu-id="b9a92-138">Your registrar will offer the option to set up the name servers for the domain.</span></span> <span data-ttu-id="b9a92-139">Para saber mais, confira [Delegar um domínio ao DNS do Azure](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="b9a92-139">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="b9a92-140">Excluir todos os recursos</span><span class="sxs-lookup"><span data-stu-id="b9a92-140">Delete all resources</span></span>

<span data-ttu-id="b9a92-141">Para excluir todos os recursos criados neste artigo, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b9a92-141">To delete all resources created in this article, take the following step:</span></span>

```powershell
Remove-AzureRMResourceGroup -Name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="b9a92-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b9a92-142">Next steps</span></span>

<span data-ttu-id="b9a92-143">Para saber mais sobre o DNS do Azure, veja [Visão geral do DNS do Azure](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b9a92-143">To learn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="b9a92-144">Para saber mais sobre como gerenciar as zonas DNS no DNS do Azure, consulte [Gerenciar zonas DNS no DNS do Azure usando o PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="b9a92-144">To learn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using PowerShell](dns-operations-dnszones.md).</span></span>

<span data-ttu-id="b9a92-145">Para saber mais sobre como gerenciar os registros DNS no DNS do Azure, consulte [Gerenciar registros DNS e conjuntos de registros no DNS do Azure usando o PowerShell](dns-operations-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="b9a92-145">To learn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using PowerShell](dns-operations-recordsets.md).</span></span>

