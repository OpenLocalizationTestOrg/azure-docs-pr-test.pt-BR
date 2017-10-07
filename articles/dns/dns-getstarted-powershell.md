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
# <a name="get-started-with-azure-dns-using-powershell"></a><span data-ttu-id="ed026-104">Introdução ao DNS do Azure usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="ed026-104">Get Started with Azure DNS using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ed026-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ed026-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="ed026-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ed026-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="ed026-107">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="ed026-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="ed026-108">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="ed026-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="ed026-109">Este artigo orienta Olá etapas toocreate sua primeira zona DNS e o registro usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed026-109">This article walks you through hello steps toocreate your first DNS zone and record using Azure PowerShell.</span></span> <span data-ttu-id="ed026-110">Você também pode executar essas etapas usando o portal do Azure de saudação ou Olá CLI do Azure de plataforma cruzada.</span><span class="sxs-lookup"><span data-stu-id="ed026-110">You can also perform these steps using hello Azure portal or hello cross-platform Azure CLI.</span></span>

<span data-ttu-id="ed026-111">Uma zona DNS é usado toohost Olá registros DNS para um domínio específico.</span><span class="sxs-lookup"><span data-stu-id="ed026-111">A DNS zone is used toohost hello DNS records for a particular domain.</span></span> <span data-ttu-id="ed026-112">toostart hospedando seu domínio no DNS do Azure, você precisa toocreate uma zona DNS para esse nome de domínio.</span><span class="sxs-lookup"><span data-stu-id="ed026-112">toostart hosting your domain in Azure DNS, you need toocreate a DNS zone for that domain name.</span></span> <span data-ttu-id="ed026-113">Cada registro DNS para seu domínio é criado dentro dessa zona DNS.</span><span class="sxs-lookup"><span data-stu-id="ed026-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="ed026-114">Finalmente, toopublish o DNS da zona toohello da Internet, você precisa de servidores de nome de saudação tooconfigure para domínio de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed026-114">Finally, toopublish your DNS zone toohello Internet, you need tooconfigure hello name servers for hello domain.</span></span> <span data-ttu-id="ed026-115">Cada uma dessas etapas é descrita abaixo.</span><span class="sxs-lookup"><span data-stu-id="ed026-115">Each of these steps is described below.</span></span>

<span data-ttu-id="ed026-116">Essas instruções presumem que você já instalado e conectado tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ed026-116">These instructions assume you have already installed and signed in tooAzure PowerShell.</span></span> <span data-ttu-id="ed026-117">Para obter ajuda, consulte [como toomanage DNS zonas usando o PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="ed026-117">For help, see [How toomanage DNS zones using PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="ed026-118">Criar grupo de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="ed026-118">Create hello resource group</span></span>

<span data-ttu-id="ed026-119">Antes de criar a zona DNS de saudação, um grupo de recursos é criado toocontain Olá DNS zona.</span><span class="sxs-lookup"><span data-stu-id="ed026-119">Before creating hello DNS zone, a resource group is created toocontain hello DNS Zone.</span></span> <span data-ttu-id="ed026-120">Veja a seguir de Olá comando hello.</span><span class="sxs-lookup"><span data-stu-id="ed026-120">hello following shows hello command.</span></span>

```powershell
New-AzureRMResourceGroup -name MyResourceGroup -location "westus"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="ed026-121">Criar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="ed026-121">Create a DNS zone</span></span>

<span data-ttu-id="ed026-122">Uma zona DNS é criada usando Olá `New-AzureRmDnsZone` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ed026-122">A DNS zone is created by using hello `New-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="ed026-123">Olá, exemplo a seguir cria uma zona DNS chamada *contoso.com* no grupo de recursos de saudação chamado *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="ed026-123">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="ed026-124">Use toocreate de exemplo hello uma zona DNS, substituindo valores de saudação para seu próprio.</span><span class="sxs-lookup"><span data-stu-id="ed026-124">Use hello example toocreate a DNS zone, substituting hello values for your own.</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyResourceGroup
```

## <a name="create-a-dns-record"></a><span data-ttu-id="ed026-125">Criar um registro DNS</span><span class="sxs-lookup"><span data-stu-id="ed026-125">Create a DNS record</span></span>

<span data-ttu-id="ed026-126">Criar conjuntos de registros usando Olá `New-AzureRmDnsRecordSet` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ed026-126">You create record sets by using hello `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="ed026-127">Olá exemplo a seguir cria um registro com o nome relativo do hello "www" hello "contoso.com", no grupo de recursos "MyResourceGroup" de zona de DNS.</span><span class="sxs-lookup"><span data-stu-id="ed026-127">hello following example creates a record with hello relative name "www" in hello DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="ed026-128">nome totalmente qualificado de saudação do conjunto de registros de saudação é "www.contoso.com".</span><span class="sxs-lookup"><span data-stu-id="ed026-128">hello fully-qualified name of hello record set is "www.contoso.com".</span></span> <span data-ttu-id="ed026-129">tipo de registro de saudação é "A", com o endereço IP "1.2.3.4" e Olá TTL é 3600 segundos.</span><span class="sxs-lookup"><span data-stu-id="ed026-129">hello record type is "A", with IP address "1.2.3.4", and hello TTL is 3600 seconds.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName contoso.com -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4")
```

<span data-ttu-id="ed026-130">Para outros tipos de registro, para conjuntos de registros com mais de um registro e toomodify os registros existentes, consulte [registros DNS de gerenciar e conjuntos de registros usando o Azure PowerShell](dns-operations-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="ed026-130">For other record types, for record sets with more than one record, and toomodify existing records, see [Manage DNS records and record sets using Azure PowerShell](dns-operations-recordsets.md).</span></span> 


## <a name="view-records"></a><span data-ttu-id="ed026-131">Exibir registros</span><span class="sxs-lookup"><span data-stu-id="ed026-131">View records</span></span>

<span data-ttu-id="ed026-132">registros DNS Olá toolist na zona, use:</span><span class="sxs-lookup"><span data-stu-id="ed026-132">toolist hello DNS records in your zone, use:</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName contoso.com -ResourceGroupName MyResourceGroup
```


## <a name="update-name-servers"></a><span data-ttu-id="ed026-133">Atualizar servidores de nome</span><span class="sxs-lookup"><span data-stu-id="ed026-133">Update name servers</span></span>

<span data-ttu-id="ed026-134">Quando estiver satisfeito de que a zona DNS e registros de tem sido instalados corretamente, você precisa tooconfigure seu nome de domínio toouse servidores de nome DNS do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ed026-134">Once you are satisfied that your DNS zone and records have been set up correctly, you need tooconfigure your domain name toouse hello Azure DNS name servers.</span></span> <span data-ttu-id="ed026-135">Isso permite que outros usuários no hello Internet toofind seus registros DNS.</span><span class="sxs-lookup"><span data-stu-id="ed026-135">This enables other users on hello Internet toofind your DNS records.</span></span>

<span data-ttu-id="ed026-136">servidores de nome de saudação para sua zona são fornecidos por Olá `Get-AzureRmDnsZone` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ed026-136">hello name servers for your zone are given by hello `Get-AzureRmDnsZone` cmdlet:</span></span>

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

<span data-ttu-id="ed026-137">Esses servidores de nome devem ser configurados com o registrador de nome de domínio hello (onde você adquiriu o nome de domínio Olá).</span><span class="sxs-lookup"><span data-stu-id="ed026-137">These name servers should be configured with hello domain name registrar (where you purchased hello domain name).</span></span> <span data-ttu-id="ed026-138">Seu registrador oferecerá Olá opção tooset os servidores de nome Olá para o domínio de saudação.</span><span class="sxs-lookup"><span data-stu-id="ed026-138">Your registrar will offer hello option tooset up hello name servers for hello domain.</span></span> <span data-ttu-id="ed026-139">Para obter mais informações, consulte [delegar tooAzure seu domínio DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="ed026-139">For more information, see [Delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="ed026-140">Excluir todos os recursos</span><span class="sxs-lookup"><span data-stu-id="ed026-140">Delete all resources</span></span>

<span data-ttu-id="ed026-141">toodelete todos os recursos criados neste artigo, Olá take etapa a seguir:</span><span class="sxs-lookup"><span data-stu-id="ed026-141">toodelete all resources created in this article, take hello following step:</span></span>

```powershell
Remove-AzureRMResourceGroup -Name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="ed026-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ed026-142">Next steps</span></span>

<span data-ttu-id="ed026-143">toolearn mais sobre o DNS do Azure, consulte [visão geral do DNS do Azure](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ed026-143">toolearn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="ed026-144">toolearn mais sobre o gerenciamento de zonas DNS no DNS do Azure, consulte [zonas DNS gerenciar no DNS do Azure usando o PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="ed026-144">toolearn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using PowerShell](dns-operations-dnszones.md).</span></span>

<span data-ttu-id="ed026-145">toolearn mais sobre o gerenciamento de registros DNS no DNS do Azure, consulte [registros de DNS de gerenciar e registro define no DNS do Azure usando o PowerShell](dns-operations-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="ed026-145">toolearn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using PowerShell](dns-operations-recordsets.md).</span></span>

