---
title: aaaGet iniciado com o DNS do Azure usando o Azure CLI 1.0 | Microsoft Docs
description: "Saiba como toocreate um DNS zona e registro de DNS do Azure. Isso é um guia passo a passo toocreate e gerenciar sua primeira zona DNS e o registro usando Olá 1.0 da CLI do Azure."
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
ms.openlocfilehash: e200c848ad261160e593306dbb8a1d92bf26880b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-10"></a><span data-ttu-id="abd2a-104">Introdução ao DNS do Azure usando a CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="abd2a-104">Get started with Azure DNS using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="abd2a-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="abd2a-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="abd2a-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="abd2a-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="abd2a-107">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="abd2a-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="abd2a-108">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="abd2a-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="abd2a-109">Este artigo orienta Olá etapas toocreate sua primeira zona DNS e o registro usando Olá plataforma cruzada do Azure CLI 1.0, que está disponível para Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="abd2a-109">This article walks you through hello steps toocreate your first DNS zone and record using hello cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="abd2a-110">Você também pode executar essas etapas usando Olá portal do Azure ou o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="abd2a-110">You can also perform these steps using hello Azure portal or Azure PowerShell.</span></span>

<span data-ttu-id="abd2a-111">Uma zona DNS é usado toohost Olá registros DNS para um domínio específico.</span><span class="sxs-lookup"><span data-stu-id="abd2a-111">A DNS zone is used toohost hello DNS records for a particular domain.</span></span> <span data-ttu-id="abd2a-112">toostart hospedando seu domínio no DNS do Azure, você precisa toocreate uma zona DNS para esse nome de domínio.</span><span class="sxs-lookup"><span data-stu-id="abd2a-112">toostart hosting your domain in Azure DNS, you need toocreate a DNS zone for that domain name.</span></span> <span data-ttu-id="abd2a-113">Cada registro DNS para seu domínio é criado dentro dessa zona DNS.</span><span class="sxs-lookup"><span data-stu-id="abd2a-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="abd2a-114">Finalmente, toopublish o DNS da zona toohello da Internet, você precisa de servidores de nome de saudação tooconfigure para domínio de saudação.</span><span class="sxs-lookup"><span data-stu-id="abd2a-114">Finally, toopublish your DNS zone toohello Internet, you need tooconfigure hello name servers for hello domain.</span></span> <span data-ttu-id="abd2a-115">Cada uma dessas etapas é descrita abaixo.</span><span class="sxs-lookup"><span data-stu-id="abd2a-115">Each of these steps is described below.</span></span>

<span data-ttu-id="abd2a-116">Essas instruções presumem que você já instalado e conectado tooAzure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="abd2a-116">These instructions assume you have already installed and signed in tooAzure CLI 1.0.</span></span> <span data-ttu-id="abd2a-117">Para obter ajuda, consulte [como toomanage DNS zonas usando o Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="abd2a-117">For help, see [How toomanage DNS zones using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="abd2a-118">Criar grupo de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="abd2a-118">Create hello resource group</span></span>

<span data-ttu-id="abd2a-119">Antes de criar a zona DNS de saudação, um grupo de recursos é criado toocontain Olá DNS zona.</span><span class="sxs-lookup"><span data-stu-id="abd2a-119">Before creating hello DNS zone, a resource group is created toocontain hello DNS Zone.</span></span> <span data-ttu-id="abd2a-120">Veja a seguir de Olá comando hello.</span><span class="sxs-lookup"><span data-stu-id="abd2a-120">hello following shows hello command.</span></span>

```azurecli
azure group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="abd2a-121">Criar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="abd2a-121">Create a DNS zone</span></span>

<span data-ttu-id="abd2a-122">Uma zona DNS é criada usando Olá `azure network dns zone create` comando.</span><span class="sxs-lookup"><span data-stu-id="abd2a-122">A DNS zone is created using hello `azure network dns zone create` command.</span></span> <span data-ttu-id="abd2a-123">toosee ajuda para este comando, digite `azure network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="abd2a-123">toosee help for this command, type `azure network dns zone create -h`.</span></span>

<span data-ttu-id="abd2a-124">Olá, exemplo a seguir cria uma zona DNS chamada *contoso.com* no grupo de recursos de saudação chamado *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="abd2a-124">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="abd2a-125">Use toocreate de exemplo hello uma zona DNS, substituindo valores de saudação para seu próprio.</span><span class="sxs-lookup"><span data-stu-id="abd2a-125">Use hello example toocreate a DNS zone, substituting hello values for your own.</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```


## <a name="create-a-dns-record"></a><span data-ttu-id="abd2a-126">Criar um registro DNS</span><span class="sxs-lookup"><span data-stu-id="abd2a-126">Create a DNS record</span></span>

<span data-ttu-id="abd2a-127">toocreate um registro DNS, use Olá `azure network dns record-set add-record` comando.</span><span class="sxs-lookup"><span data-stu-id="abd2a-127">toocreate a DNS record, use hello `azure network dns record-set add-record` command.</span></span> <span data-ttu-id="abd2a-128">Para obter ajuda, consulte `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="abd2a-128">For help, see `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="abd2a-129">Olá exemplo a seguir cria um registro com o nome relativo do hello "www" hello "contoso.com", no grupo de recursos "MyResourceGroup" de zona de DNS.</span><span class="sxs-lookup"><span data-stu-id="abd2a-129">hello following example creates a record with hello relative name "www" in hello DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="abd2a-130">nome totalmente qualificado de saudação do conjunto de registros de saudação é "www.contoso.com".</span><span class="sxs-lookup"><span data-stu-id="abd2a-130">hello fully-qualified name of hello record set is "www.contoso.com".</span></span> <span data-ttu-id="abd2a-131">tipo de registro de saudação é "A", com o endereço IP "1.2.3.4" e um TTL padrão de 3600 segundos (1 hora) é usado.</span><span class="sxs-lookup"><span data-stu-id="abd2a-131">hello record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

<span data-ttu-id="abd2a-132">Para outros tipos de registro, para conjuntos de registros com mais de um registro para valores alternativos de TTL e toomodify os registros existentes, consulte [registros DNS de gerenciar e conjuntos de registros usando hello Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="abd2a-132">For other record types, for record sets with more than one record, for alternative TTL values, and toomodify existing records, see [Manage DNS records and record sets using hello Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span></span>


## <a name="view-records"></a><span data-ttu-id="abd2a-133">Exibir registros</span><span class="sxs-lookup"><span data-stu-id="abd2a-133">View records</span></span>

<span data-ttu-id="abd2a-134">registros DNS Olá toolist na zona, use:</span><span class="sxs-lookup"><span data-stu-id="abd2a-134">toolist hello DNS records in your zone, use:</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```


## <a name="update-name-servers"></a><span data-ttu-id="abd2a-135">Atualizar servidores de nome</span><span class="sxs-lookup"><span data-stu-id="abd2a-135">Update name servers</span></span>

<span data-ttu-id="abd2a-136">Quando estiver satisfeito de que a zona DNS e registros de tem sido instalados corretamente, você precisa tooconfigure seu nome de domínio toouse servidores de nome DNS do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="abd2a-136">Once you are satisfied that your DNS zone and records have been set up correctly, you need tooconfigure your domain name toouse hello Azure DNS name servers.</span></span> <span data-ttu-id="abd2a-137">Isso permite que outros usuários no hello Internet toofind seus registros DNS.</span><span class="sxs-lookup"><span data-stu-id="abd2a-137">This enables other users on hello Internet toofind your DNS records.</span></span>

<span data-ttu-id="abd2a-138">servidores de nome de saudação para sua zona são fornecidos por Olá `azure network dns zone show` comando:</span><span class="sxs-lookup"><span data-stu-id="abd2a-138">hello name servers for your zone are given by hello `azure network dns zone show` command:</span></span>

```azurecli
azure network dns zone show MyResourceGroup contoso.com

info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
data:    Id                              : /subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 3
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            :
info:    network dns zone show command OK
```

<span data-ttu-id="abd2a-139">Esses servidores de nome devem ser configurados com o registrador de nome de domínio hello (onde você adquiriu o nome de domínio Olá).</span><span class="sxs-lookup"><span data-stu-id="abd2a-139">These name servers should be configured with hello domain name registrar (where you purchased hello domain name).</span></span> <span data-ttu-id="abd2a-140">Seu registrador oferecerá Olá opção tooset os servidores de nome Olá para o domínio de saudação.</span><span class="sxs-lookup"><span data-stu-id="abd2a-140">Your registrar will offer hello option tooset up hello name servers for hello domain.</span></span> <span data-ttu-id="abd2a-141">Para obter mais informações, consulte [delegar tooAzure seu domínio DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="abd2a-141">For more information, see [Delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="abd2a-142">Excluir todos os recursos</span><span class="sxs-lookup"><span data-stu-id="abd2a-142">Delete all resources</span></span>
 
<span data-ttu-id="abd2a-143">toodelete todos os recursos criados neste artigo, Olá take etapa a seguir:</span><span class="sxs-lookup"><span data-stu-id="abd2a-143">toodelete all resources created in this article, take hello following step:</span></span>

```azurecli
azure group delete --name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="abd2a-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="abd2a-144">Next steps</span></span>

<span data-ttu-id="abd2a-145">toolearn mais sobre o DNS do Azure, consulte [visão geral do DNS do Azure](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="abd2a-145">toolearn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="abd2a-146">toolearn mais sobre o gerenciamento de zonas DNS no DNS do Azure, consulte [zonas DNS gerenciar no DNS do Azure usando o Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="abd2a-146">toolearn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span></span>

<span data-ttu-id="abd2a-147">toolearn mais sobre o gerenciamento de registros DNS no DNS do Azure, consulte [registros de DNS de gerenciar e registro define no DNS do Azure usando o Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="abd2a-147">toolearn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span></span>

