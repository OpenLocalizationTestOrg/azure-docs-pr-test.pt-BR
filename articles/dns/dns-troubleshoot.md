---
title: "Guia de solução de problemas de DNS aaaAzure | Microsoft Docs"
description: Como tootroubleshoot comum problemas de DNS do Azure
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: 95b01dc3-ee69-4575-a259-4227131e4f9c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/20/2017
ms.author: jonatul
ms.openlocfilehash: 944aa1811c980063f739268cd2c79b647b2754a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-troubleshooting-guide"></a><span data-ttu-id="a4c15-103">Guia de solução de problemas do DNS do Azure</span><span class="sxs-lookup"><span data-stu-id="a4c15-103">Azure DNS troubleshooting guide</span></span>

<span data-ttu-id="a4c15-104">Esta página fornece informações sobre solução de questões de DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4c15-104">This page provides troubleshooting information for common Azure DNS questions.</span></span>

<span data-ttu-id="a4c15-105">Se essas etapas não resolverem o problema, você pode também procurar ou poste seu problema no nosso [Fórum de suporte da comunidade no MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span><span class="sxs-lookup"><span data-stu-id="a4c15-105">If these steps don't resolve your issue, you can also search for or post your issue on our [community support forum on MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span></span> <span data-ttu-id="a4c15-106">Como alternativa, abra uma solicitação de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4c15-106">Alternatively, open an Azure support request.</span></span>


## <a name="i-cant-create-a-dns-zone"></a><span data-ttu-id="a4c15-107">Não consigo criar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="a4c15-107">I can't create a DNS zone</span></span>

<span data-ttu-id="a4c15-108">problemas comuns de tooresolve, tente um ou mais dos Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a4c15-108">tooresolve common issues, try one or more of hello following steps:</span></span>

1.  <span data-ttu-id="a4c15-109">Olá revisão que auditoria de DNS do Azure registra o motivo da falha toodetermine hello.</span><span class="sxs-lookup"><span data-stu-id="a4c15-109">Review hello Azure DNS audit logs toodetermine hello failure reason.</span></span>
2.  <span data-ttu-id="a4c15-110">Cada nome de zona DNS deve ser exclusivo dentro de seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a4c15-110">Each DNS zone name must be unique within its resource group.</span></span> <span data-ttu-id="a4c15-111">Ou seja, duas zonas DNS com hello mesmo nome não é possível compartilhar um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a4c15-111">That is, two DNS zones with hello same name cannot share a resource group.</span></span> <span data-ttu-id="a4c15-112">Tente usar um nome de zona diferente ou outro grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a4c15-112">Try using a different zone name, or a different resource group.</span></span>
3.  <span data-ttu-id="a4c15-113">Você pode ver um erro "Você atingiu ou excedeu o número máximo de saudação de zonas na assinatura {id da assinatura}."</span><span class="sxs-lookup"><span data-stu-id="a4c15-113">You may see an error "You have reached or exceeded hello maximum number of zones in subscription {subscription id}."</span></span> <span data-ttu-id="a4c15-114">Use uma assinatura do Azure diferente, exclua algumas regiões ou entre em contato com o suporte do Azure tooraise seu limite de assinatura.</span><span class="sxs-lookup"><span data-stu-id="a4c15-114">Either use a different Azure subscription, delete some zones, or contact Azure Support tooraise your subscription limit.</span></span>
4.  <span data-ttu-id="a4c15-115">Você pode ver um erro "zona Olá '{nome da zona}' não está disponível."</span><span class="sxs-lookup"><span data-stu-id="a4c15-115">You may see an error "hello zone '{zone name}' is not available."</span></span> <span data-ttu-id="a4c15-116">Esse erro significa que o DNS do Azure foi tooallocate não é possível de servidores de nome para esta zona DNS.</span><span class="sxs-lookup"><span data-stu-id="a4c15-116">This error means that Azure DNS was unable tooallocate name servers for this DNS zone.</span></span> <span data-ttu-id="a4c15-117">Tente usar um nome de zona diferente.</span><span class="sxs-lookup"><span data-stu-id="a4c15-117">Try using a different zone name.</span></span> <span data-ttu-id="a4c15-118">Como alternativa, se você for o proprietário do nome de domínio hello, entre em contato com o suporte do Azure, que pode alocar a servidores de nomes para você.</span><span class="sxs-lookup"><span data-stu-id="a4c15-118">Alternatively, if you are hello domain name owner, contact Azure support, who can allocate name servers for you.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="a4c15-119">**Documentos recomendados**</span><span class="sxs-lookup"><span data-stu-id="a4c15-119">**Recommended documents**</span></span>

<span data-ttu-id="a4c15-120">[Zonas e registros DNS](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="a4c15-120">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="a4c15-121">
[Criar uma zona DNS](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="a4c15-121">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>

## <a name="i-cant-create-a-dns-record"></a><span data-ttu-id="a4c15-122">Não consigo criar um registro DNS</span><span class="sxs-lookup"><span data-stu-id="a4c15-122">I can't create a DNS record</span></span>

<span data-ttu-id="a4c15-123">problemas comuns de tooresolve, tente um ou mais dos Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a4c15-123">tooresolve common issues, try one or more of hello following steps:</span></span>

1.  <span data-ttu-id="a4c15-124">Olá revisão que auditoria de DNS do Azure registra o motivo da falha toodetermine hello.</span><span class="sxs-lookup"><span data-stu-id="a4c15-124">Review hello Azure DNS audit logs toodetermine hello failure reason.</span></span>
2.  <span data-ttu-id="a4c15-125">Conjunto de registros de saudação já existe?</span><span class="sxs-lookup"><span data-stu-id="a4c15-125">Does hello record set exist already?</span></span>  <span data-ttu-id="a4c15-126">DNS do Azure gerencia usando o registro de registros *define*, que são a coleção de saudação dos registros de saudação de mesmo nome e Olá mesmo tipo.</span><span class="sxs-lookup"><span data-stu-id="a4c15-126">Azure DNS manages records using record *sets*, which are hello collection of records of hello same name and hello same type.</span></span> <span data-ttu-id="a4c15-127">Se um registro com hello mesmo nome e tipo já existir, em seguida, tooadd outro registro inexistente Olá existente registro deve ser editado definido.</span><span class="sxs-lookup"><span data-stu-id="a4c15-127">If a record with hello same name and type already exists, then tooadd another such record you should edit hello existing record set.</span></span>
3.  <span data-ttu-id="a4c15-128">Você está tentando toocreate um registro no ápice de zona DNS de saudação (raiz da zona Olá Olá)?</span><span class="sxs-lookup"><span data-stu-id="a4c15-128">Are you trying toocreate a record at hello DNS zone apex (hello ‘root’ of hello zone)?</span></span> <span data-ttu-id="a4c15-129">Se assim, Olá convenção DNS é toouse Olá ' @' caractere como o nome do registro hello.</span><span class="sxs-lookup"><span data-stu-id="a4c15-129">If so, hello DNS convention is toouse hello ‘@’ character as hello record name.</span></span> <span data-ttu-id="a4c15-130">Observe também que os padrões DNS Olá não permitir registros CNAME no ápice da zona de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4c15-130">Also note that hello DNS standards do not permit CNAME records at hello zone apex.</span></span>
4.  <span data-ttu-id="a4c15-131">Existe um conflito de CNAME?</span><span class="sxs-lookup"><span data-stu-id="a4c15-131">Do you have a CNAME conflict?</span></span>  <span data-ttu-id="a4c15-132">padrões DNS Olá não permitem um registro CNAME com o mesmo nome como um registro de qualquer outro tipo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4c15-132">hello DNS standards do not allow a CNAME record with hello same name as a record of any other type.</span></span> <span data-ttu-id="a4c15-133">Se você tiver um CNAME existente, criando um registro com hello falha de mesmo nome de um tipo diferente.</span><span class="sxs-lookup"><span data-stu-id="a4c15-133">If you have an existing CNAME, creating a record with hello same name of a different type fails.</span></span>  <span data-ttu-id="a4c15-134">Da mesma forma, criar um CNAME falhará se o nome da saudação corresponde a um registro existente de um tipo diferente.</span><span class="sxs-lookup"><span data-stu-id="a4c15-134">Likewise, creating a CNAME fails if hello name matches an existing record of a different type.</span></span> <span data-ttu-id="a4c15-135">Remova conflitos Olá removendo Olá outro registro ou escolha um nome de registro diferente.</span><span class="sxs-lookup"><span data-stu-id="a4c15-135">Remove hello conflict by removing hello other record or choosing a different record name.</span></span>
5.  <span data-ttu-id="a4c15-136">Foi atingido o limite Olá número de saudação de conjuntos de registros permitido em uma zona DNS? número atual de saudação do registro define e hello número máximo de conjuntos de registros é mostrado em Olá portal do Azure, em Olá 'Propriedades' para a zona de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4c15-136">Have you reached hello limit on hello number of record sets permitted in a DNS zone? hello current number of record sets and hello maximum number of record sets are shown in hello Azure portal, under hello 'Properties' for hello zone.</span></span> <span data-ttu-id="a4c15-137">Se você atingiu o limite, em seguida, exclua alguns conjuntos de registros ou entre em contato com o suporte do Azure tooraise seu limite de conjunto de registros para esta zona, em seguida, tente novamente.</span><span class="sxs-lookup"><span data-stu-id="a4c15-137">If you have reached this limit, then either delete some record sets or contact Azure Support tooraise your record set limit for this zone, then try again.</span></span> 


### <a name="recommended-documents"></a><span data-ttu-id="a4c15-138">**Documentos recomendados**</span><span class="sxs-lookup"><span data-stu-id="a4c15-138">**Recommended documents**</span></span>

<span data-ttu-id="a4c15-139">[Zonas e registros DNS](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="a4c15-139">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="a4c15-140">
[Criar uma zona DNS](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="a4c15-140">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>



## <a name="i-cant-resolve-my-dns-record"></a><span data-ttu-id="a4c15-141">Não consigo resolver meu registro DNS</span><span class="sxs-lookup"><span data-stu-id="a4c15-141">I can't resolve my DNS record</span></span>

<span data-ttu-id="a4c15-142">A resolução de nome DNS é um processo de várias etapas que pode falhar por várias razões.</span><span class="sxs-lookup"><span data-stu-id="a4c15-142">DNS name resolution is a multi-step process, which can fail for many reasons.</span></span> <span data-ttu-id="a4c15-143">Olá seguinte ajudá-lo a investigar por que a resolução DNS está falhando para um registro DNS em uma zona hospedado no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4c15-143">hello following steps help you investigate why DNS resolution is failing for a DNS record in a zone hosted in Azure DNS.</span></span>

1.  <span data-ttu-id="a4c15-144">Confirme se os registros DNS Olá foi configurados corretamente no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4c15-144">Confirm that hello DNS records have been configured correctly in Azure DNS.</span></span> <span data-ttu-id="a4c15-145">Examine os registros DNS Olá no hello portal do Azure, verificando se o nome da zona Olá, nome do registro e tipo de registro estão corretas.</span><span class="sxs-lookup"><span data-stu-id="a4c15-145">Review hello DNS records in hello Azure portal, checking that hello zone name, record name, and record type are correct.</span></span>
2.  <span data-ttu-id="a4c15-146">Confirme que os registros DNS Olá resolver corretamente nos servidores de nome DNS do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a4c15-146">Confirm that hello DNS records resolve correctly on hello Azure DNS name servers.</span></span>
    - <span data-ttu-id="a4c15-147">Se você fizer consultas DNS do seu computador local, você poderá ver resultados em cache que não refletem o estado atual de Olá Olá de servidores de nomes.</span><span class="sxs-lookup"><span data-stu-id="a4c15-147">If you make DNS queries from your local PC, you may see cached results that don’t reflect hello current state of hello name servers.</span></span>  <span data-ttu-id="a4c15-148">Além disso, redes corporativas geralmente usam servidores de proxy DNS, que impedirá que as consultas DNS que está sendo direcionado toospecific servidores de nome.</span><span class="sxs-lookup"><span data-stu-id="a4c15-148">Also, corporate networks often use DNS proxy servers, which prevent DNS queries from being directed toospecific name servers.</span></span>  <span data-ttu-id="a4c15-149">tooavoid esses problemas, use um serviço de resolução de nome baseado na web, como [digwebinterface](http://digwebinterface.com).</span><span class="sxs-lookup"><span data-stu-id="a4c15-149">tooavoid these problems, use a web-based name resolution service such as [digwebinterface](http://digwebinterface.com).</span></span>
    - <span data-ttu-id="a4c15-150">Ser toospecify-se de que os servidores de nome correto de Olá para a zona DNS, conforme mostrado no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4c15-150">Be sure toospecify hello correct name servers for your DNS zone, as shown in hello Azure portal.</span></span>
    - <span data-ttu-id="a4c15-151">Verifique se o nome DNS de saudação está correta (tiver toospecify nome de saudação totalmente qualificada, incluindo o nome da zona Olá) e Olá tipo de registro está correto</span><span class="sxs-lookup"><span data-stu-id="a4c15-151">Check that hello DNS name is correct (you have toospecify hello fully qualified name, including hello zone name) and hello record type is correct</span></span>
3.  <span data-ttu-id="a4c15-152">Confirmar este nome de domínio DNS Olá foi corretamente [delegado servidores de nome DNS do Azure toohello](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="a4c15-152">Confirm that hello DNS domain name has been correctly [delegated toohello Azure DNS name servers](dns-domain-delegation.md).</span></span> <span data-ttu-id="a4c15-153">Há [vários sites da Web de terceiros que oferecem validação de delegação DNS](https://www.bing.com/search?q=dns+check+tool).</span><span class="sxs-lookup"><span data-stu-id="a4c15-153">There are a [many 3rd-party web sites that offer DNS delegation validation](https://www.bing.com/search?q=dns+check+tool).</span></span> <span data-ttu-id="a4c15-154">Este teste é um *zona* teste de delegação, para que você só deve digitar o nome da zona DNS hello e não Olá nome totalmente qualificado registro.</span><span class="sxs-lookup"><span data-stu-id="a4c15-154">This test is a *zone* delegation test, so you should only enter hello DNS zone name and not hello fully qualified record name.</span></span>
4.  <span data-ttu-id="a4c15-155">Tendo concluído Olá acima, o registro de DNS deve agora resolver corretamente.</span><span class="sxs-lookup"><span data-stu-id="a4c15-155">Having completed hello above, your DNS record should now resolve correctly.</span></span> <span data-ttu-id="a4c15-156">tooverify, você pode usar novamente [digwebinterface](http://digwebinterface.com), desta vez usando as configurações de servidor de nome de padrão hello.</span><span class="sxs-lookup"><span data-stu-id="a4c15-156">tooverify, you can again use [digwebinterface](http://digwebinterface.com), this time using hello default name server settings.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="a4c15-157">**Documentos recomendados**</span><span class="sxs-lookup"><span data-stu-id="a4c15-157">**Recommended documents**</span></span>

[<span data-ttu-id="a4c15-158">Delegar um tooAzure de domínio DNS</span><span class="sxs-lookup"><span data-stu-id="a4c15-158">Delegate a domain tooAzure DNS</span></span>](dns-domain-delegation.md)



## <a name="how-do-i-specify-hello-service-and-protocol-for-an-srv-record"></a><span data-ttu-id="a4c15-159">Como especificar hello 'serviço' e 'protocolo' para um registro SRV?</span><span class="sxs-lookup"><span data-stu-id="a4c15-159">How do I specify hello ‘service’ and ‘protocol’ for an SRV record?</span></span>

<span data-ttu-id="a4c15-160">DNS do Azure gerencia registros DNS como conjuntos de registros — Olá conjunto de registros com hello mesmo nome e Olá mesmo tipo.</span><span class="sxs-lookup"><span data-stu-id="a4c15-160">Azure DNS manages DNS records as record sets—hello collection of records with hello same name and hello same type.</span></span> <span data-ttu-id="a4c15-161">Para um conjunto de registros SRV, Olá 'serviço' e 'protocolo' necessário toobe especificado como parte do nome do conjunto de registros de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4c15-161">For an SRV record set, hello 'service' and 'protocol' need toobe specified as part of hello record set name.</span></span> <span data-ttu-id="a4c15-162">Olá outros SRV ('priority', 'peso', 'porta' e 'target') são especificados separadamente para cada registro no conjunto de registros de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4c15-162">hello other SRV parameters ('priority', 'weight', 'port' and 'target') are specified separately for each record in hello record set.</span></span>

<span data-ttu-id="a4c15-163">Exemplo de nomes de registro SRV (nome de serviço 'sip', protocolo 'tcp'):</span><span class="sxs-lookup"><span data-stu-id="a4c15-163">Example SRV record names (service name 'sip', protocol 'tcp'):</span></span>

- <span data-ttu-id="a4c15-164">\_SIP. \_tcp (cria um registro definida no ápice da zona de saudação)</span><span class="sxs-lookup"><span data-stu-id="a4c15-164">\_sip.\_tcp (creates a record set at hello zone apex)</span></span>
- <span data-ttu-id="a4c15-165">\_sip.\_tcp.sipservice (cria um conjunto de registros chamado 'sipservice')</span><span class="sxs-lookup"><span data-stu-id="a4c15-165">\_sip.\_tcp.sipservice (creates a record set named 'sipservice')</span></span>

### <a name="recommended-documents"></a><span data-ttu-id="a4c15-166">**Documentos recomendados**</span><span class="sxs-lookup"><span data-stu-id="a4c15-166">**Recommended documents**</span></span>

<span data-ttu-id="a4c15-167">[Zonas e registros DNS](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="a4c15-167">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="a4c15-168">
[Criar conjuntos de registros de DNS e registros usando Olá portal do Azure](dns-getstarted-create-recordset-portal.md)
</span><span class="sxs-lookup"><span data-stu-id="a4c15-168">
[Create DNS record sets and records by using hello Azure portal](dns-getstarted-create-recordset-portal.md)
</span></span><br><span data-ttu-id="a4c15-169">
[Tipo de registro SRV (Wikipédia)](https://en.wikipedia.org/wiki/SRV_record)</span><span class="sxs-lookup"><span data-stu-id="a4c15-169">
[SRV record type (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span></span>


## <a name="next-steps"></a><span data-ttu-id="a4c15-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a4c15-170">Next steps</span></span>

* <span data-ttu-id="a4c15-171">Saiba mais sobre [registros e zonas DNS do Azure](dns-zones-records.md)</span><span class="sxs-lookup"><span data-stu-id="a4c15-171">Learn about [Azure DNS zones and records](dns-zones-records.md)</span></span>
* <span data-ttu-id="a4c15-172">toostart usando o DNS do Azure, Aprenda como muito[criar uma zona DNS](dns-getstarted-create-dnszone-portal.md) e [criar registros DNS](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a4c15-172">toostart using Azure DNS, learn how too[create a DNS zone](dns-getstarted-create-dnszone-portal.md) and [create DNS records](dns-getstarted-create-recordset-portal.md).</span></span>
* <span data-ttu-id="a4c15-173">toomigrate uma zona DNS existente, saiba como muito[importar e exportar um arquivo de zona DNS](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="a4c15-173">toomigrate an existing DNS zone, learn how too[import and export a DNS zone file](dns-import-export.md).</span></span>

