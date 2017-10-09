---
title: aaaGet iniciado com o DNS do Azure usando o Azure CLI 2.0 | Microsoft Docs
description: "Saiba como toocreate um DNS zona e registro de DNS do Azure. Isso é um guia passo a passo toocreate e gerenciar sua primeira zona DNS e o registro usando Olá 2.0 do CLI do Azure."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 8a894941e9910d5cc35394a1be9dbca9792613f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-20"></a><span data-ttu-id="aa6f2-104">Introdução ao DNS do Azure usando a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="aa6f2-104">Get started with Azure DNS using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="aa6f2-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="aa6f2-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="aa6f2-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa6f2-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="aa6f2-107">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="aa6f2-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="aa6f2-108">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="aa6f2-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="aa6f2-109">Este artigo orienta Olá etapas toocreate sua primeira zona DNS e o registro usando Olá plataforma cruzada do Azure CLI 2.0, que está disponível para Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="aa6f2-109">This article walks you through hello steps toocreate your first DNS zone and record using hello cross-platform Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="aa6f2-110">Você também pode executar essas etapas usando Olá portal do Azure ou o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aa6f2-110">You can also perform these steps using hello Azure portal or Azure PowerShell.</span></span>

<span data-ttu-id="aa6f2-111">Uma zona DNS é usado toohost Olá registros DNS para um domínio específico.</span><span class="sxs-lookup"><span data-stu-id="aa6f2-111">A DNS zone is used toohost hello DNS records for a particular domain.</span></span> <span data-ttu-id="aa6f2-112">toostart hospedando seu domínio no DNS do Azure, você precisa toocreate uma zona DNS para esse nome de domínio.</span><span class="sxs-lookup"><span data-stu-id="aa6f2-112">toostart hosting your domain in Azure DNS, you need toocreate a DNS zone for that domain name.</span></span> <span data-ttu-id="aa6f2-113">Cada registro DNS para seu domínio é criado dentro dessa zona DNS.</span><span class="sxs-lookup"><span data-stu-id="aa6f2-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="aa6f2-114">Finalmente, toopublish o DNS da zona toohello da Internet, você precisa de servidores de nome de saudação tooconfigure para domínio de saudação.</span><span class="sxs-lookup"><span data-stu-id="aa6f2-114">Finally, toopublish your DNS zone toohello Internet, you need tooconfigure hello name servers for hello domain.</span></span> <span data-ttu-id="aa6f2-115">Cada uma dessas etapas é descrita abaixo.</span><span class="sxs-lookup"><span data-stu-id="aa6f2-115">Each of these steps is described below.</span></span>

<span data-ttu-id="aa6f2-116">Essas instruções presumem que você já instalado e conectado tooAzure 2.0 do CLI.</span><span class="sxs-lookup"><span data-stu-id="aa6f2-116">These instructions assume you have already installed and signed in tooAzure CLI 2.0.</span></span> <span data-ttu-id="aa6f2-117">Para obter ajuda, consulte [como toomanage DNS zonas usando o Azure CLI 2.0](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="aa6f2-117">For help, see [How toomanage DNS zones using Azure CLI 2.0](dns-operations-dnszones-cli.md).</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="aa6f2-118">Criar grupo de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="aa6f2-118">Create hello resource group</span></span>

<span data-ttu-id="aa6f2-119">Antes de criar a zona DNS de saudação, um grupo de recursos é criado toocontain Olá DNS zona.</span><span class="sxs-lookup"><span data-stu-id="aa6f2-119">Before creating hello DNS zone, a resource group is created toocontain hello DNS Zone.</span></span> <span data-ttu-id="aa6f2-120">Veja a seguir de Olá comando hello.</span><span class="sxs-lookup"><span data-stu-id="aa6f2-120">hello following shows hello command.</span></span>

```azurecli
az group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="aa6f2-121">Criar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="aa6f2-121">Create a DNS zone</span></span>

<span data-ttu-id="aa6f2-122">Uma zona DNS é criada usando Olá `az network dns zone create` comando.</span><span class="sxs-lookup"><span data-stu-id="aa6f2-122">A DNS zone is created using hello `az network dns zone create` command.</span></span> <span data-ttu-id="aa6f2-123">toosee ajuda para este comando, digite `az network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="aa6f2-123">toosee help for this command, type `az network dns zone create -h`.</span></span>

<span data-ttu-id="aa6f2-124">Olá, exemplo a seguir cria uma zona DNS chamada *contoso.com* no grupo de recursos de saudação *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="aa6f2-124">hello following example creates a DNS zone called *contoso.com* in hello resource group *MyResourceGroup*.</span></span> <span data-ttu-id="aa6f2-125">Use toocreate de exemplo hello uma zona DNS, substituindo valores de saudação para seu próprio.</span><span class="sxs-lookup"><span data-stu-id="aa6f2-125">Use hello example toocreate a DNS zone, substituting hello values for your own.</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n contoso.com
```


## <a name="create-a-dns-record"></a><span data-ttu-id="aa6f2-126">Criar um registro DNS</span><span class="sxs-lookup"><span data-stu-id="aa6f2-126">Create a DNS record</span></span>

<span data-ttu-id="aa6f2-127">toocreate um registro DNS, use Olá `az network dns record-set [record type] add-record` comando.</span><span class="sxs-lookup"><span data-stu-id="aa6f2-127">toocreate a DNS record, use hello `az network dns record-set [record type] add-record` command.</span></span> <span data-ttu-id="aa6f2-128">Para obter ajuda, por exemplo, com os registros A, veja `azure network dns record-set A add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="aa6f2-128">For help, for A records for example, see `azure network dns record-set A add-record -h`.</span></span>

<span data-ttu-id="aa6f2-129">Olá exemplo a seguir cria um registro com o nome relativo do hello "www" hello "contoso.com", no grupo de recursos "MyResourceGroup" de zona de DNS.</span><span class="sxs-lookup"><span data-stu-id="aa6f2-129">hello following example creates a record with hello relative name "www" in hello DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="aa6f2-130">nome totalmente qualificado de saudação do conjunto de registros de saudação é "www.contoso.com".</span><span class="sxs-lookup"><span data-stu-id="aa6f2-130">hello fully-qualified name of hello record set is "www.contoso.com".</span></span> <span data-ttu-id="aa6f2-131">tipo de registro de saudação é "A", com o endereço IP "1.2.3.4" e um TTL padrão de 3600 segundos (1 hora) é usado.</span><span class="sxs-lookup"><span data-stu-id="aa6f2-131">hello record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span></span>

```azurecli
az network dns record-set a add-record -g MyResourceGroup -z contoso.com -n www -a 1.2.3.4
```

<span data-ttu-id="aa6f2-132">Para outros tipos de registro, para conjuntos de registros com mais de um registro para valores alternativos de TTL e toomodify os registros existentes, consulte [registros DNS de gerenciar e conjuntos de registros usando hello Azure CLI 2.0](dns-operations-recordsets-cli.md).</span><span class="sxs-lookup"><span data-stu-id="aa6f2-132">For other record types, for record sets with more than one record, for alternative TTL values, and toomodify existing records, see [Manage DNS records and record sets using hello Azure CLI 2.0](dns-operations-recordsets-cli.md).</span></span>


## <a name="view-records"></a><span data-ttu-id="aa6f2-133">Exibir registros</span><span class="sxs-lookup"><span data-stu-id="aa6f2-133">View records</span></span>

<span data-ttu-id="aa6f2-134">registros DNS Olá toolist na zona, use:</span><span class="sxs-lookup"><span data-stu-id="aa6f2-134">toolist hello DNS records in your zone, use:</span></span>

```azurecli
az network dns record-set list -g MyResourceGroup -z contoso.com
```


## <a name="update-name-servers"></a><span data-ttu-id="aa6f2-135">Atualizar servidores de nome</span><span class="sxs-lookup"><span data-stu-id="aa6f2-135">Update name servers</span></span>

<span data-ttu-id="aa6f2-136">Quando estiver satisfeito de que a zona DNS e registros de tem sido instalados corretamente, você precisa tooconfigure seu nome de domínio toouse servidores de nome DNS do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="aa6f2-136">Once you are satisfied that your DNS zone and records have been set up correctly, you need tooconfigure your domain name toouse hello Azure DNS name servers.</span></span> <span data-ttu-id="aa6f2-137">Isso permite que outros usuários no hello Internet toofind seus registros DNS.</span><span class="sxs-lookup"><span data-stu-id="aa6f2-137">This enables other users on hello Internet toofind your DNS records.</span></span>

<span data-ttu-id="aa6f2-138">servidores de nome de saudação para sua zona são fornecidos por Olá `az network dns zone show` comando.</span><span class="sxs-lookup"><span data-stu-id="aa6f2-138">hello name servers for your zone are given by hello `az network dns zone show` command.</span></span> <span data-ttu-id="aa6f2-139">nomes de servidores de nome de saudação toosee, use o JSON de saída, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="aa6f2-139">toosee hello name server names, use JSON output, as shown in hello following example.</span></span>

```azurecli
az network dns zone show -g MyResourceGroup -n contoso.com -o json

{
  "etag": "00000003-0000-0000-b40d-0996b97ed101",
  "id": "/subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-01.azure-dns.com.",
    "ns2-01.azure-dns.net.",
    "ns3-01.azure-dns.org.",
    "ns4-01.azure-dns.info."
  ],
  "numberOfRecordSets": 3,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="aa6f2-140">Esses servidores de nome devem ser configurados com o registrador de nome de domínio hello (onde você adquiriu o nome de domínio Olá).</span><span class="sxs-lookup"><span data-stu-id="aa6f2-140">These name servers should be configured with hello domain name registrar (where you purchased hello domain name).</span></span> <span data-ttu-id="aa6f2-141">Seu registrador oferecerá Olá opção tooset os servidores de nome Olá para o domínio de saudação.</span><span class="sxs-lookup"><span data-stu-id="aa6f2-141">Your registrar will offer hello option tooset up hello name servers for hello domain.</span></span> <span data-ttu-id="aa6f2-142">Para obter mais informações, consulte [delegar tooAzure seu domínio DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="aa6f2-142">For more information, see [Delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="aa6f2-143">Excluir todos os recursos</span><span class="sxs-lookup"><span data-stu-id="aa6f2-143">Delete all resources</span></span>
 
<span data-ttu-id="aa6f2-144">toodelete todos os recursos criados neste artigo, Olá take etapa a seguir:</span><span class="sxs-lookup"><span data-stu-id="aa6f2-144">toodelete all resources created in this article, take hello following step:</span></span>

```azurecli
az group delete --name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="aa6f2-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aa6f2-145">Next steps</span></span>

<span data-ttu-id="aa6f2-146">toolearn mais sobre o DNS do Azure, consulte [visão geral do DNS do Azure](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aa6f2-146">toolearn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="aa6f2-147">toolearn mais sobre o gerenciamento de zonas DNS no DNS do Azure, consulte [zonas DNS gerenciar no DNS do Azure usando o Azure CLI 2.0](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="aa6f2-147">toolearn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using Azure CLI 2.0](dns-operations-dnszones-cli.md).</span></span>

<span data-ttu-id="aa6f2-148">toolearn mais sobre o gerenciamento de registros DNS no DNS do Azure, consulte [registros de DNS de gerenciar e registro define no DNS do Azure usando o Azure CLI 2.0](dns-operations-recordsets-cli.md).</span><span class="sxs-lookup"><span data-stu-id="aa6f2-148">toolearn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using Azure CLI 2.0](dns-operations-recordsets-cli.md).</span></span>
