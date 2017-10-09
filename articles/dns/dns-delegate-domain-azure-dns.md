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
# <a name="delegate-a-domain-tooazure-dns"></a><span data-ttu-id="cd7c7-103">Delegar um tooAzure de domínio DNS</span><span class="sxs-lookup"><span data-stu-id="cd7c7-103">Delegate a domain tooAzure DNS</span></span>

<span data-ttu-id="cd7c7-104">DNS do Azure permite que você toohost uma zona DNS e gerenciar registros DNS Olá para um domínio no Azure.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-104">Azure DNS allows you toohost a DNS zone and manage hello DNS records for a domain in Azure.</span></span> <span data-ttu-id="cd7c7-105">Para consultas DNS para um tooreach de domínio DNS do Azure, domínio Olá tem toobe delegadas tooAzure DNS do domínio pai de saudação.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-105">In order for DNS queries for a domain tooreach Azure DNS, hello domain has toobe delegated tooAzure DNS from hello parent domain.</span></span> <span data-ttu-id="cd7c7-106">Tenha em mente DNS do Azure não é um registrador de domínio hello.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-106">Keep in mind Azure DNS is not hello domain registrar.</span></span> <span data-ttu-id="cd7c7-107">Este artigo explica como toodelegate tooAzure seu domínio DNS.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-107">This article explains how toodelegate your domain tooAzure DNS.</span></span>

<span data-ttu-id="cd7c7-108">Comprado de um registrador de domínios, seu registrador oferece Olá opção tooset esses registros NS.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-108">For domains purchased from a registrar, your registrar offers hello option tooset up these NS records.</span></span> <span data-ttu-id="cd7c7-109">Você não possuem tooown toocreate um domínio uma zona DNS com esse nome de domínio DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-109">You do not have tooown a domain toocreate a DNS zone with that domain name in Azure DNS.</span></span> <span data-ttu-id="cd7c7-110">No entanto, é necessário tooown Olá domínio tooset backup Olá tooAzure de delegação DNS com o registrador de saudação.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-110">However, you do need tooown hello domain tooset up hello delegation tooAzure DNS with hello registrar.</span></span>

<span data-ttu-id="cd7c7-111">Por exemplo, suponha que você compre domínio Olá 'contoso.net' e cria uma zona com o nome de saudação 'contoso.net' no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-111">For example, suppose you purchase hello domain 'contoso.net' and create a zone with hello name 'contoso.net' in Azure DNS.</span></span> <span data-ttu-id="cd7c7-112">Como proprietário de saudação do domínio hello, seu registrador oferece que Olá endereços do servidor de nome hello opção tooconfigure (ou seja, registros de saudação NS) para seu domínio.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-112">As hello owner of hello domain, your registrar offers you hello option tooconfigure hello name server addresses (that is, hello NS records) for your domain.</span></span> <span data-ttu-id="cd7c7-113">registrador Olá armazena esses registros NS em Olá domínio pai, neste caso '.net'.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-113">hello registrar stores these NS records in hello parent domain, in this case '.net'.</span></span> <span data-ttu-id="cd7c7-114">Os clientes em torno de Olá, mundo podem ser direcionado tooyour domínio na zona DNS do Azure durante a tentativa de tooresolve registros DNS em 'contoso.net'.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-114">Clients around hello world can then be directed tooyour domain in Azure DNS zone when trying tooresolve DNS records in 'contoso.net'.</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="cd7c7-115">Criar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="cd7c7-115">Create a DNS zone</span></span>

1. <span data-ttu-id="cd7c7-116">Entrar toohello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cd7c7-116">Sign in toohello Azure portal</span></span>
1. <span data-ttu-id="cd7c7-117">No menu de Hub hello, clique em e clique em **Novo > rede >** e, em seguida, clique em **zona DNS** folha de zona de DNS criar tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-117">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![Zona DNS](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="cd7c7-119">Em Olá **zona DNS criar** folha digite Olá valores a seguir, clique em **criar**:</span><span class="sxs-lookup"><span data-stu-id="cd7c7-119">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>

   | <span data-ttu-id="cd7c7-120">**Configuração**</span><span class="sxs-lookup"><span data-stu-id="cd7c7-120">**Setting**</span></span> | <span data-ttu-id="cd7c7-121">**Valor**</span><span class="sxs-lookup"><span data-stu-id="cd7c7-121">**Value**</span></span> | <span data-ttu-id="cd7c7-122">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="cd7c7-122">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="cd7c7-123">**Nome**</span><span class="sxs-lookup"><span data-stu-id="cd7c7-123">**Name**</span></span>|<span data-ttu-id="cd7c7-124">contoso.net</span><span class="sxs-lookup"><span data-stu-id="cd7c7-124">contoso.net</span></span>|<span data-ttu-id="cd7c7-125">nome de saudação da zona do DNS de saudação</span><span class="sxs-lookup"><span data-stu-id="cd7c7-125">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="cd7c7-126">**Assinatura**</span><span class="sxs-lookup"><span data-stu-id="cd7c7-126">**Subscription**</span></span>|<span data-ttu-id="cd7c7-127">[Sua assinatura]</span><span class="sxs-lookup"><span data-stu-id="cd7c7-127">[Your subscription]</span></span>|<span data-ttu-id="cd7c7-128">Selecione um assinatura toocreate Olá aplicativo gateway.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-128">Select a subscription toocreate hello application gateway in.</span></span>|
   |<span data-ttu-id="cd7c7-129">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="cd7c7-129">**Resource group**</span></span>|<span data-ttu-id="cd7c7-130">**Criar um novo:** contosoRG</span><span class="sxs-lookup"><span data-stu-id="cd7c7-130">**Create new:** contosoRG</span></span>|<span data-ttu-id="cd7c7-131">Crie um grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-131">Create a resource group.</span></span> <span data-ttu-id="cd7c7-132">nome do grupo de recursos Olá deve ser exclusivo na assinatura de saudação selecionado.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-132">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="cd7c7-133">toolearn mais sobre grupos de recursos, leia Olá [Gerenciador de recursos](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) artigo de visão geral.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-133">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="cd7c7-134">**Localidade**</span><span class="sxs-lookup"><span data-stu-id="cd7c7-134">**Location**</span></span>|<span data-ttu-id="cd7c7-135">Oeste dos EUA</span><span class="sxs-lookup"><span data-stu-id="cd7c7-135">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="cd7c7-136">grupo de recursos de Olá refere-se o local de toohello saudação do grupo de recursos e não tem nenhum impacto na zona DNS de saudação.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-136">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="cd7c7-137">local da zona DNS Olá sempre é "global" e não é mostrado.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-137">hello DNS zone location is always "global", and is not shown.</span></span>

## <a name="retrieve-name-servers"></a><span data-ttu-id="cd7c7-138">Recuperar servidores de nome</span><span class="sxs-lookup"><span data-stu-id="cd7c7-138">Retrieve name servers</span></span>

<span data-ttu-id="cd7c7-139">Antes de você pode delegar a zona DNS tooAzure DNS, é necessário primeiro nomes de servidor de nome tooknow Olá para a zona.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-139">Before you can delegate your DNS zone tooAzure DNS, you first need tooknow hello name server names for your zone.</span></span> <span data-ttu-id="cd7c7-140">O Azure DNS aloca os servidores de nomes de um pool sempre que uma zona é criada.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-140">Azure DNS allocates name servers from a pool each time a zone is created.</span></span>

1. <span data-ttu-id="cd7c7-141">A zona DNS de saudação criada, no portal do Azure de saudação **Favoritos** painel, clique em **todos os recursos**.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-141">With hello DNS zone created, in hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="cd7c7-142">Clique em Olá **contoso.net** zona DNS na Olá **todos os recursos** folha.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-142">Click hello **contoso.net** DNS zone in hello **All resources** blade.</span></span> <span data-ttu-id="cd7c7-143">Se a assinatura de saudação selecionado já contiver vários recursos, você pode inserir **contoso.net** em Olá filtrar por nome...</span><span class="sxs-lookup"><span data-stu-id="cd7c7-143">If hello subscription you selected already has several resources in it, you can enter **contoso.net** in hello Filter by name…</span></span> <span data-ttu-id="cd7c7-144">gateway de caixa tooeasily acesso Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-144">box tooeasily access hello application gateway.</span></span> 

1. <span data-ttu-id="cd7c7-145">Recupere servidores de nome de saudação da folha de zona do DNS hello.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-145">Retrieve hello name servers from hello DNS zone blade.</span></span> <span data-ttu-id="cd7c7-146">Neste exemplo, a zona de saudação 'contoso.net' recebeu servidores de nome ' ns1-01.azure-dns.com', 'ns2-01.azure-dns .net', ' ns3-01.azure-dns.org', e ' ns4-01.azure-dns.info':</span><span class="sxs-lookup"><span data-stu-id="cd7c7-146">In this example, hello zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Servidor de nomes DNS](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="cd7c7-148">DNS do Azure cria automaticamente os registros NS autoritativos na zona que contém a saudação servidores de nomes atribuída.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-148">Azure DNS automatically creates authoritative NS records in your zone containing hello assigned name servers.</span></span>  <span data-ttu-id="cd7c7-149">nomes de servidor de nomes de saudação toosee por meio do Azure PowerShell ou CLI do Azure, basta tooretrieve esses registros.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-149">toosee hello name server names via Azure PowerShell or Azure CLI, you simply need tooretrieve these records.</span></span>

<span data-ttu-id="cd7c7-150">Olá exemplos a seguir também fornecem etapas Olá tooretrieve servidores de nome de saudação para uma zona no DNS do Azure com o PowerShell e a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-150">hello following examples also provide hello steps tooretrieve hello name servers for a zone in Azure DNS with PowerShell and Azure CLI.</span></span>

### <a name="powershell"></a><span data-ttu-id="cd7c7-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cd7c7-151">PowerShell</span></span>

```powershell
# hello record name "@" is used toorefer toorecords at hello top of hello zone.
$zone = Get-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -Zone $zone
```

<span data-ttu-id="cd7c7-152">saudação de exemplo a seguir é a resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-152">hello following example is hello response.</span></span>

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

### <a name="azure-cli"></a><span data-ttu-id="cd7c7-153">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="cd7c7-153">Azure CLI</span></span>

```azurecli
az network dns record-set show --resource-group contosoRG --zone-name contoso.net --type NS --name @
```

<span data-ttu-id="cd7c7-154">saudação de exemplo a seguir é a resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-154">hello following example is hello response.</span></span>

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

## <a name="delegate-hello-domain"></a><span data-ttu-id="cd7c7-155">Domínio de saudação do delegado</span><span class="sxs-lookup"><span data-stu-id="cd7c7-155">Delegate hello domain</span></span>

<span data-ttu-id="cd7c7-156">Agora que a zona DNS de saudação é criada e você tem servidores de nome hello, o domínio pai Olá precisa toobe atualizada com os servidores de nome DNS do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-156">Now that hello DNS zone is created and you have hello name servers, hello parent domain needs toobe updated with hello Azure DNS name servers.</span></span> <span data-ttu-id="cd7c7-157">Cada registro tem seus próprios registros de servidor DNS management tools toochange Olá nome para um domínio.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-157">Each registrar has their own DNS management tools toochange hello name server records for a domain.</span></span> <span data-ttu-id="cd7c7-158">Na página de gerenciamento do DNS do registrador hello, editar os registros NS hello e substitua os registros NS Olá Olá aqueles criados de DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-158">In hello registrar's DNS management page, edit hello NS records and replace hello NS records with hello ones Azure DNS created.</span></span>

<span data-ttu-id="cd7c7-159">Ao delegar tooAzure um domínio DNS, você deve usar nomes de servidor de nome hello fornecidos pelo DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-159">When delegating a domain tooAzure DNS, you must use hello name server names provided by Azure DNS.</span></span> <span data-ttu-id="cd7c7-160">É recomendável toouse todas as quatro nome nomes de servidor, independentemente do nome de saudação do seu domínio.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-160">It is recommended toouse all four name server names, regardless of hello name of your domain.</span></span> <span data-ttu-id="cd7c7-161">Delegação de domínio não requer toouse de nome de servidor de nome Olá Olá mesmo domínio de nível superior que seu domínio.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-161">Domain delegation does not require hello name server name toouse hello same top-level domain as your domain.</span></span>

<span data-ttu-id="cd7c7-162">Você não deve usar os registros de união toopoint toohello DNS do Azure nome endereços IP do servidor, desde que esses endereços IP podem mudar no futuro.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-162">You should not use 'glue records' toopoint toohello Azure DNS name server IP addresses, since these IP addresses may change in future.</span></span> <span data-ttu-id="cd7c7-163">Atualmente, o Azure DNS não dá suporte às delegações usando nomes do servidores de nomes em sua própria zona, às vezes chamados de 'servidores de nome intuitivos'.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-163">Delegations using name server names in your own zone, sometimes called 'vanity name servers', are not currently supported in Azure DNS.</span></span>

## <a name="verify-name-resolution-is-working"></a><span data-ttu-id="cd7c7-164">Verifique se a resolução de nomes está funcionando</span><span class="sxs-lookup"><span data-stu-id="cd7c7-164">Verify name resolution is working</span></span>

<span data-ttu-id="cd7c7-165">Depois de concluir a delegação hello, você pode verificar se a resolução de nomes está funcionando usando uma ferramenta como 'nslookup' tooquery Olá registro SOA da zona (que é criada automaticamente quando a zona de saudação é criada).</span><span class="sxs-lookup"><span data-stu-id="cd7c7-165">After completing hello delegation, you can verify that name resolution is working by using a tool such as 'nslookup' tooquery hello SOA record for your zone (which is also automatically created when hello zone is created).</span></span>

<span data-ttu-id="cd7c7-166">Você não tem servidores de nome de DNS do Azure toospecify Olá, se a delegação Olá foi configurada corretamente, Olá DNS resolução processo normal localiza os servidores de nome de saudação automaticamente.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-166">You do not have toospecify hello Azure DNS name servers, if hello delegation has been set up correctly, hello normal DNS resolution process finds hello name servers automatically.</span></span>

```
nslookup -type=SOA contoso.com
```

<span data-ttu-id="cd7c7-167">a seguir Olá é um exemplo de resposta de saudação que precedem o comando:</span><span class="sxs-lookup"><span data-stu-id="cd7c7-167">hello following is an example response from hello preceding command:</span></span>

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

## <a name="delegate-sub-domains-in-azure-dns"></a><span data-ttu-id="cd7c7-168">Delegar subdomínios no DNS do Azure</span><span class="sxs-lookup"><span data-stu-id="cd7c7-168">Delegate sub-domains in Azure DNS</span></span>

<span data-ttu-id="cd7c7-169">Se você quiser tooset uma zona filho separada, você pode delegar um subdomínio no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-169">If you want tooset up a separate child zone, you can delegate a sub-domain in Azure DNS.</span></span> <span data-ttu-id="cd7c7-170">Por exemplo, tendo configurado e delegado 'contoso.net' no DNS do Azure, suponha que você gostaria que tooset uma zona filho separada, 'partners.contoso.net'.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-170">For example, having set up and delegated 'contoso.net' in Azure DNS, suppose you would like tooset up a separate child zone, 'partners.contoso.net'.</span></span>

1. <span data-ttu-id="cd7c7-171">Crie a zona de filho Olá 'partners.contoso.net' no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-171">Create hello child zone 'partners.contoso.net' in Azure DNS.</span></span>
2. <span data-ttu-id="cd7c7-172">Pesquise registros NS autoritativos de saudação em Olá filho tooobtain Olá servidores de nome hospeda zona de filho Olá no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-172">Look up hello authoritative NS records in hello child zone tooobtain hello name servers hosting hello child zone in Azure DNS.</span></span>
3. <span data-ttu-id="cd7c7-173">Delegar a zona de filho Olá Configurando registros NS na zona pai de saudação apontando toohello zona de filho.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-173">Delegate hello child zone by configuring NS records in hello parent zone pointing toohello child zone.</span></span>

### <a name="create-a-dns-zone"></a><span data-ttu-id="cd7c7-174">Criar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="cd7c7-174">Create a DNS zone</span></span>

1. <span data-ttu-id="cd7c7-175">Entrar toohello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cd7c7-175">Sign in toohello Azure portal</span></span>
1. <span data-ttu-id="cd7c7-176">No menu de Hub hello, clique em e clique em **Novo > rede >** e, em seguida, clique em **zona DNS** folha de zona de DNS criar tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-176">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![Zona DNS](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="cd7c7-178">Em Olá **zona DNS criar** folha digite Olá valores a seguir, clique em **criar**:</span><span class="sxs-lookup"><span data-stu-id="cd7c7-178">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>

   | <span data-ttu-id="cd7c7-179">**Configuração**</span><span class="sxs-lookup"><span data-stu-id="cd7c7-179">**Setting**</span></span> | <span data-ttu-id="cd7c7-180">**Valor**</span><span class="sxs-lookup"><span data-stu-id="cd7c7-180">**Value**</span></span> | <span data-ttu-id="cd7c7-181">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="cd7c7-181">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="cd7c7-182">**Nome**</span><span class="sxs-lookup"><span data-stu-id="cd7c7-182">**Name**</span></span>|<span data-ttu-id="cd7c7-183">partners.contoso.net</span><span class="sxs-lookup"><span data-stu-id="cd7c7-183">partners.contoso.net</span></span>|<span data-ttu-id="cd7c7-184">nome de saudação da zona do DNS de saudação</span><span class="sxs-lookup"><span data-stu-id="cd7c7-184">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="cd7c7-185">**Assinatura**</span><span class="sxs-lookup"><span data-stu-id="cd7c7-185">**Subscription**</span></span>|<span data-ttu-id="cd7c7-186">[Sua assinatura]</span><span class="sxs-lookup"><span data-stu-id="cd7c7-186">[Your subscription]</span></span>|<span data-ttu-id="cd7c7-187">Selecione um assinatura toocreate Olá aplicativo gateway.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-187">Select a subscription toocreate hello application gateway in.</span></span>|
   |<span data-ttu-id="cd7c7-188">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="cd7c7-188">**Resource group**</span></span>|<span data-ttu-id="cd7c7-189">**Usar existente:** contosoRG</span><span class="sxs-lookup"><span data-stu-id="cd7c7-189">**Use Existing:** contosoRG</span></span>|<span data-ttu-id="cd7c7-190">Crie um grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-190">Create a resource group.</span></span> <span data-ttu-id="cd7c7-191">nome do grupo de recursos Olá deve ser exclusivo na assinatura de saudação selecionado.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-191">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="cd7c7-192">toolearn mais sobre grupos de recursos, leia Olá [Gerenciador de recursos](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) artigo de visão geral.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-192">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="cd7c7-193">**Localidade**</span><span class="sxs-lookup"><span data-stu-id="cd7c7-193">**Location**</span></span>|<span data-ttu-id="cd7c7-194">Oeste dos EUA</span><span class="sxs-lookup"><span data-stu-id="cd7c7-194">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="cd7c7-195">grupo de recursos de Olá refere-se o local de toohello saudação do grupo de recursos e não tem nenhum impacto na zona DNS de saudação.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-195">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="cd7c7-196">local da zona DNS Olá sempre é "global" e não é mostrado.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-196">hello DNS zone location is always "global", and is not shown.</span></span>

### <a name="retrieve-name-servers"></a><span data-ttu-id="cd7c7-197">Recuperar servidores de nome</span><span class="sxs-lookup"><span data-stu-id="cd7c7-197">Retrieve name servers</span></span>

1. <span data-ttu-id="cd7c7-198">A zona DNS de saudação criada, no portal do Azure de saudação **Favoritos** painel, clique em **todos os recursos**.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-198">With hello DNS zone created, in hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="cd7c7-199">Clique em Olá **partners.contoso.net** zona DNS na Olá **todos os recursos** folha.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-199">Click hello **partners.contoso.net** DNS zone in hello **All resources** blade.</span></span> <span data-ttu-id="cd7c7-200">Se a assinatura de saudação selecionado já contiver vários recursos, você pode inserir **partners.contoso.net** em Olá filtrar por nome...</span><span class="sxs-lookup"><span data-stu-id="cd7c7-200">If hello subscription you selected already has several resources in it, you can enter **partners.contoso.net** in hello Filter by name…</span></span> <span data-ttu-id="cd7c7-201">zona DNS do hello caixa tooeasily acesso.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-201">box tooeasily access hello DNS zone.</span></span>

1. <span data-ttu-id="cd7c7-202">Recupere servidores de nome de saudação da folha de zona do DNS hello.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-202">Retrieve hello name servers from hello DNS zone blade.</span></span> <span data-ttu-id="cd7c7-203">Neste exemplo, a zona de saudação 'contoso.net' recebeu servidores de nome ' ns1-01.azure-dns.com', 'ns2-01.azure-dns .net', ' ns3-01.azure-dns.org', e ' ns4-01.azure-dns.info':</span><span class="sxs-lookup"><span data-stu-id="cd7c7-203">In this example, hello zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Servidor de nomes DNS](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="cd7c7-205">DNS do Azure cria automaticamente os registros NS autoritativos na zona que contém a saudação servidores de nomes atribuída.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-205">Azure DNS automatically creates authoritative NS records in your zone containing hello assigned name servers.</span></span>  <span data-ttu-id="cd7c7-206">nomes de servidor de nomes de saudação toosee por meio do Azure PowerShell ou CLI do Azure, basta tooretrieve esses registros.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-206">toosee hello name server names via Azure PowerShell or Azure CLI, you simply need tooretrieve these records.</span></span>

### <a name="create-name-server-record-in-parent-zone"></a><span data-ttu-id="cd7c7-207">Criar registro de servidor de nomes na zona pai</span><span class="sxs-lookup"><span data-stu-id="cd7c7-207">Create name server record in parent zone</span></span>

1. <span data-ttu-id="cd7c7-208">Navegue toohello **contoso.net** zona DNS na Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-208">Navigate toohello **contoso.net** DNS zone in hello Azure portal.</span></span>
1. <span data-ttu-id="cd7c7-209">Clique em **+ Conjunto de registros**</span><span class="sxs-lookup"><span data-stu-id="cd7c7-209">Click **+ Record set**</span></span>
1. <span data-ttu-id="cd7c7-210">Em Olá **Adicionar conjunto de registros** folha, digite Olá valores a seguir, clique em **Okey**:</span><span class="sxs-lookup"><span data-stu-id="cd7c7-210">On hello **Add record set** blade, enter hello following values, then click **OK**:</span></span>

   | <span data-ttu-id="cd7c7-211">**Configuração**</span><span class="sxs-lookup"><span data-stu-id="cd7c7-211">**Setting**</span></span> | <span data-ttu-id="cd7c7-212">**Valor**</span><span class="sxs-lookup"><span data-stu-id="cd7c7-212">**Value**</span></span> | <span data-ttu-id="cd7c7-213">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="cd7c7-213">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="cd7c7-214">**Nome**</span><span class="sxs-lookup"><span data-stu-id="cd7c7-214">**Name**</span></span>|<span data-ttu-id="cd7c7-215">partners</span><span class="sxs-lookup"><span data-stu-id="cd7c7-215">partners</span></span>|<span data-ttu-id="cd7c7-216">nome de saudação da zona DNS Olá filho</span><span class="sxs-lookup"><span data-stu-id="cd7c7-216">hello name of hello child DNS zone</span></span>|
   |<span data-ttu-id="cd7c7-217">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="cd7c7-217">**Type**</span></span>|<span data-ttu-id="cd7c7-218">NS</span><span class="sxs-lookup"><span data-stu-id="cd7c7-218">NS</span></span>|<span data-ttu-id="cd7c7-219">Use NS para os registros do servidor de nomes.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-219">Use NS for name server records.</span></span>|
   |<span data-ttu-id="cd7c7-220">**TTL**</span><span class="sxs-lookup"><span data-stu-id="cd7c7-220">**TTL**</span></span>|<span data-ttu-id="cd7c7-221">1</span><span class="sxs-lookup"><span data-stu-id="cd7c7-221">1</span></span>|<span data-ttu-id="cd7c7-222">Tempo toolive.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-222">Time toolive.</span></span>|
   |<span data-ttu-id="cd7c7-223">**Unidade de TTL**</span><span class="sxs-lookup"><span data-stu-id="cd7c7-223">**TTL unit**</span></span>|<span data-ttu-id="cd7c7-224">Horas</span><span class="sxs-lookup"><span data-stu-id="cd7c7-224">Hours</span></span>|<span data-ttu-id="cd7c7-225">Define o tempo unidade toolive toohours</span><span class="sxs-lookup"><span data-stu-id="cd7c7-225">sets time toolive unit toohours</span></span>|
   |<span data-ttu-id="cd7c7-226">**NAME SERVER**</span><span class="sxs-lookup"><span data-stu-id="cd7c7-226">**NAME SERVER**</span></span>|<span data-ttu-id="cd7c7-227">{servidores de nome para a zona partners.contoso.net}</span><span class="sxs-lookup"><span data-stu-id="cd7c7-227">{name servers from partners.contoso.net zone}</span></span>|<span data-ttu-id="cd7c7-228">Insira todos os 4 Olá de servidores de nomes de partners.contoso.net zona.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-228">Enter all 4 of hello name servers from partners.contoso.net zone.</span></span> |

   ![Servidor de nomes DNS](./media/dns-domain-delegation/partnerzone.png)


### <a name="delegating-sub-domains-in-azure-dns-with-other-tools"></a><span data-ttu-id="cd7c7-230">Delegar subdomínios no DNS do Azure com outras ferramentas</span><span class="sxs-lookup"><span data-stu-id="cd7c7-230">Delegating sub-domains in Azure DNS with other tools</span></span>

<span data-ttu-id="cd7c7-231">Hello exemplos a seguir fornecem as etapas de saudação toodelegate subdomínios no DNS do Azure com o PowerShell e a CLI:</span><span class="sxs-lookup"><span data-stu-id="cd7c7-231">hello following examples provide hello steps toodelegate sub-domains in Azure DNS with PowerShell and CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="cd7c7-232">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cd7c7-232">PowerShell</span></span>

<span data-ttu-id="cd7c7-233">Olá PowerShell de exemplo a seguir demonstra como isso funciona.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-233">hello following PowerShell example demonstrates how this works.</span></span> <span data-ttu-id="cd7c7-234">Olá mesmas etapas podem ser executadas por meio de saudação portal do Azure ou por meio de Olá CLI do Azure de plataforma cruzada.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-234">hello same steps can be executed via hello Azure portal, or via hello cross-platform Azure CLI.</span></span>

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

<span data-ttu-id="cd7c7-235">Use `nslookup` tooverify que tudo está configurado corretamente procurando Olá registro SOA da zona de filho hello.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-235">Use `nslookup` tooverify that everything is set up correctly by looking up hello SOA record of hello child zone.</span></span>

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

#### <a name="azure-cli"></a><span data-ttu-id="cd7c7-236">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="cd7c7-236">Azure CLI</span></span>

```azurecli
#!/bin/bash

# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
az network dns zone create -g contosoRG -n contoso.net
az network dns zone create -g contosoRG -n partners.contoso.net
```

<span data-ttu-id="cd7c7-237">Recuperar os servidores de nome de saudação do hello `partners.contoso.net` zona de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-237">Retrieve hello name servers for hello `partners.contoso.net` zone from hello output.</span></span>

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

<span data-ttu-id="cd7c7-238">Crie conjunto de registros de saudação e registros NS para cada servidor de nomes.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-238">Create hello record set and NS records for each name server.</span></span>

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

## <a name="delete-all-resources"></a><span data-ttu-id="cd7c7-239">Excluir todos os recursos</span><span class="sxs-lookup"><span data-stu-id="cd7c7-239">Delete all resources</span></span>

<span data-ttu-id="cd7c7-240">toodelete todos os recursos criados neste artigo, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="cd7c7-240">toodelete all resources created in this article, complete hello following steps:</span></span>

1. <span data-ttu-id="cd7c7-241">No portal do Azure de saudação **Favoritos** painel, clique em **todos os recursos**.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-241">In hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="cd7c7-242">Clique em Olá **contosorg** grupo de recursos no hello folha de todos os recursos.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-242">Click hello **contosorg** resource group in hello All resources blade.</span></span> <span data-ttu-id="cd7c7-243">Se a assinatura de saudação selecionado já contiver vários recursos, você pode inserir **contosorg** em Olá **filtrar por nome...**</span><span class="sxs-lookup"><span data-stu-id="cd7c7-243">If hello subscription you selected already has several resources in it, you can enter **contosorg** in hello **Filter by name…**</span></span> <span data-ttu-id="cd7c7-244">grupo de recursos do hello caixa tooeasily acesso.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-244">box tooeasily access hello resource group.</span></span>
1. <span data-ttu-id="cd7c7-245">Em Olá **contosorg** folha, clique em Olá **excluir** botão.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-245">In hello **contosorg** blade, click hello **Delete** button.</span></span>
1. <span data-ttu-id="cd7c7-246">Hello portal exige que você tootype nome de saudação do hello tooconfirm de grupo de recursos que você deseja toodelete-lo.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-246">hello portal requires you tootype hello name of hello resource group tooconfirm that you want toodelete it.</span></span> <span data-ttu-id="cd7c7-247">Tipo *contosorg* para o nome do grupo de recursos hello, em seguida, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-247">Type *contosorg* for hello resource group name, then click **Delete**.</span></span> <span data-ttu-id="cd7c7-248">Excluir um grupo de recursos exclui todos os recursos no grupo de recursos de saudação, portanto, sempre tooconfirm-se de conteúdo de saudação de um grupo de recursos antes de excluí-lo.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-248">Deleting a resource group deletes all resources within hello resource group, so always be sure tooconfirm hello contents of a resource group before deleting it.</span></span> <span data-ttu-id="cd7c7-249">portal de saudação exclui todos os recursos contidos no grupo de recursos hello, em seguida, exclui o grupo de recursos de saudação em si.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-249">hello portal deletes all resources contained within hello resource group, then deletes hello resource group itself.</span></span> <span data-ttu-id="cd7c7-250">Esse processo leva vários minutos.</span><span class="sxs-lookup"><span data-stu-id="cd7c7-250">This process takes several minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd7c7-251">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cd7c7-251">Next steps</span></span>

[<span data-ttu-id="cd7c7-252">Gerenciar zonas DNS</span><span class="sxs-lookup"><span data-stu-id="cd7c7-252">Manage DNS zones</span></span>](dns-operations-dnszones.md)

[<span data-ttu-id="cd7c7-253">Gerenciar registros DNS</span><span class="sxs-lookup"><span data-stu-id="cd7c7-253">Manage DNS records</span></span>](dns-operations-recordsets.md)
