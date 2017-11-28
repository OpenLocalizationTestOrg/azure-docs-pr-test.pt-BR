---
title: "Introdução ao DNS do Azure usando a CLI do Azure 1.0 | Microsoft Docs"
description: "Saiba como criar uma zona e registro DNS no DNS do Azure. Este é uma guia passo a passo para criar e gerenciar sua primeira zona e registro DNS usando a CLI do Azure 1.0."
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
ms.openlocfilehash: f7943b71bbd16c36df09436973d92539eb62b210
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-10"></a><span data-ttu-id="c71eb-104">Introdução ao DNS do Azure usando a CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="c71eb-104">Get started with Azure DNS using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c71eb-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c71eb-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="c71eb-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c71eb-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="c71eb-107">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="c71eb-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="c71eb-108">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="c71eb-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="c71eb-109">Este artigo explica as etapas de criação de sua primeira zona e registro DNS usando a CLI do Azure 1.0 entre plataformas, que está disponível para Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="c71eb-109">This article walks you through the steps to create your first DNS zone and record using the cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="c71eb-110">Você também pode executar essas etapas usando o Portal do Azure ou o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c71eb-110">You can also perform these steps using the Azure portal or Azure PowerShell.</span></span>

<span data-ttu-id="c71eb-111">Uma zona DNS é usada para hospedar os registros DNS para um domínio específico.</span><span class="sxs-lookup"><span data-stu-id="c71eb-111">A DNS zone is used to host the DNS records for a particular domain.</span></span> <span data-ttu-id="c71eb-112">Para iniciar a hospedagem do seu domínio no DNS do Azure, você precisará criar uma zona DNS para esse nome de domínio.</span><span class="sxs-lookup"><span data-stu-id="c71eb-112">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span></span> <span data-ttu-id="c71eb-113">Cada registro DNS para seu domínio é criado dentro dessa zona DNS.</span><span class="sxs-lookup"><span data-stu-id="c71eb-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="c71eb-114">Por fim, para publicar sua zona DNS na Internet, você precisa configurar os servidores de nome para o domínio.</span><span class="sxs-lookup"><span data-stu-id="c71eb-114">Finally, to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span></span> <span data-ttu-id="c71eb-115">Cada uma dessas etapas é descrita abaixo.</span><span class="sxs-lookup"><span data-stu-id="c71eb-115">Each of these steps is described below.</span></span>

<span data-ttu-id="c71eb-116">Essas instruções pressupõem que você já instalou e entrou na CLI do Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="c71eb-116">These instructions assume you have already installed and signed in to Azure CLI 1.0.</span></span> <span data-ttu-id="c71eb-117">Para obter ajuda, confira [Como gerenciar as zonas DNS usando a CLI do Azure 1.0](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c71eb-117">For help, see [How to manage DNS zones using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="c71eb-118">Criar o grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="c71eb-118">Create the resource group</span></span>

<span data-ttu-id="c71eb-119">Antes de criar a zona DNS, um grupo de recursos é criado para conter a zona DNS.</span><span class="sxs-lookup"><span data-stu-id="c71eb-119">Before creating the DNS zone, a resource group is created to contain the DNS Zone.</span></span> <span data-ttu-id="c71eb-120">O código a seguir mostra o comando.</span><span class="sxs-lookup"><span data-stu-id="c71eb-120">The following shows the command.</span></span>

```azurecli
azure group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="c71eb-121">Criar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="c71eb-121">Create a DNS zone</span></span>

<span data-ttu-id="c71eb-122">Uma zona DNS é criada usando o comando `azure network dns zone create` .</span><span class="sxs-lookup"><span data-stu-id="c71eb-122">A DNS zone is created using the `azure network dns zone create` command.</span></span> <span data-ttu-id="c71eb-123">Para ver a ajuda desse comando, digite `azure network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="c71eb-123">To see help for this command, type `azure network dns zone create -h`.</span></span>

<span data-ttu-id="c71eb-124">O exemplo a seguir cria uma zona DNS chamada *contoso.com* no grupo de recursos chamado *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="c71eb-124">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="c71eb-125">Use o exemplo para criar uma zona DNS, substituindo os valores pelos seus próprios.</span><span class="sxs-lookup"><span data-stu-id="c71eb-125">Use the example to create a DNS zone, substituting the values for your own.</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```


## <a name="create-a-dns-record"></a><span data-ttu-id="c71eb-126">Criar um registro DNS</span><span class="sxs-lookup"><span data-stu-id="c71eb-126">Create a DNS record</span></span>

<span data-ttu-id="c71eb-127">Para criar um registro DNS, use o comando `azure network dns record-set add-record`.</span><span class="sxs-lookup"><span data-stu-id="c71eb-127">To create a DNS record, use the `azure network dns record-set add-record` command.</span></span> <span data-ttu-id="c71eb-128">Para obter ajuda, consulte `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="c71eb-128">For help, see `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="c71eb-129">O exemplo a seguir cria um registro com o nome relativo "www" na Zona DNS "contoso.com", no grupo de recursos "MyResourceGroup".</span><span class="sxs-lookup"><span data-stu-id="c71eb-129">The following example creates a record with the relative name "www" in the DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="c71eb-130">O nome totalmente qualificado do conjunto de registros é “www.contoso.com”.</span><span class="sxs-lookup"><span data-stu-id="c71eb-130">The fully-qualified name of the record set is "www.contoso.com".</span></span> <span data-ttu-id="c71eb-131">O tipo de registro é "A", com o endereço IP "1.2.3.4", e um TTL padrão de 3600 segundos (1 hora) é usado.</span><span class="sxs-lookup"><span data-stu-id="c71eb-131">The record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

<span data-ttu-id="c71eb-132">Para outros tipos de registros, para conjuntos de registros com mais de um registro, para valores de TTL alternativos e para modificar registros existentes, consulte [Gerenciar registros DNS e conjuntos de registros usando a CLI do Azure 1.0](dns-operations-recordsets-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c71eb-132">For other record types, for record sets with more than one record, for alternative TTL values, and to modify existing records, see [Manage DNS records and record sets using the Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span></span>


## <a name="view-records"></a><span data-ttu-id="c71eb-133">Exibir registros</span><span class="sxs-lookup"><span data-stu-id="c71eb-133">View records</span></span>

<span data-ttu-id="c71eb-134">Para listar os registros DNS em sua zona, use:</span><span class="sxs-lookup"><span data-stu-id="c71eb-134">To list the DNS records in your zone, use:</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```


## <a name="update-name-servers"></a><span data-ttu-id="c71eb-135">Atualizar servidores de nome</span><span class="sxs-lookup"><span data-stu-id="c71eb-135">Update name servers</span></span>

<span data-ttu-id="c71eb-136">Quando você estiver satisfeito com a configuração de sua zona e registros DNS, configure seu nome de domínio para usar os servidores de nome DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="c71eb-136">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span></span> <span data-ttu-id="c71eb-137">Isso permite que outros usuários na Internet encontrem os registros DNS.</span><span class="sxs-lookup"><span data-stu-id="c71eb-137">This enables other users on the Internet to find your DNS records.</span></span>

<span data-ttu-id="c71eb-138">Os servidores de nomes de sua zona são fornecidos pelo comando `azure network dns zone show`:</span><span class="sxs-lookup"><span data-stu-id="c71eb-138">The name servers for your zone are given by the `azure network dns zone show` command:</span></span>

```azurecli
azure network dns zone show MyResourceGroup contoso.com

info:    Executing command network dns zone show
+ Looking up the dns zone "contoso.com"
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

<span data-ttu-id="c71eb-139">Esses servidores de nome devem ser configurados com o registrador de nome de domínio (onde você adquiriu o nome de domínio).</span><span class="sxs-lookup"><span data-stu-id="c71eb-139">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span></span> <span data-ttu-id="c71eb-140">Seu registrador oferecerá a opção de configurar os servidores de nome do domínio.</span><span class="sxs-lookup"><span data-stu-id="c71eb-140">Your registrar will offer the option to set up the name servers for the domain.</span></span> <span data-ttu-id="c71eb-141">Para saber mais, confira [Delegar um domínio ao DNS do Azure](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="c71eb-141">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="c71eb-142">Excluir todos os recursos</span><span class="sxs-lookup"><span data-stu-id="c71eb-142">Delete all resources</span></span>
 
<span data-ttu-id="c71eb-143">Para excluir todos os recursos criados neste artigo, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c71eb-143">To delete all resources created in this article, take the following step:</span></span>

```azurecli
azure group delete --name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="c71eb-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c71eb-144">Next steps</span></span>

<span data-ttu-id="c71eb-145">Para saber mais sobre o DNS do Azure, veja [Visão geral do DNS do Azure](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c71eb-145">To learn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="c71eb-146">Para saber mais sobre como gerenciar as zonas DNS no DNS do Azure, veja [Gerenciar zonas DNS no DNS do Azure usando a CLI do Azure 1.0](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c71eb-146">To learn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span></span>

<span data-ttu-id="c71eb-147">Para saber mais sobre como gerenciar os registros DNS no DNS do Azure, veja [Gerenciar registros DNS e conjuntos de registros no DNS do Azure usando a CLI do Azure 1.0](dns-operations-recordsets-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c71eb-147">To learn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span></span>

