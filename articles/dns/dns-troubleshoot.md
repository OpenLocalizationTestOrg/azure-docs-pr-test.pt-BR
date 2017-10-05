---
title: "Guia de solução de problemas de DNS do Azure | Microsoft Docs"
description: Como solucionar problemas comuns com o DNS do Azure
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
ms.openlocfilehash: 1d9bb681a864bdc3e5a2f9c9a531d9566b16ada4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-dns-troubleshooting-guide"></a><span data-ttu-id="b8627-103">Guia de solução de problemas do DNS do Azure</span><span class="sxs-lookup"><span data-stu-id="b8627-103">Azure DNS troubleshooting guide</span></span>

<span data-ttu-id="b8627-104">Esta página fornece informações sobre solução de questões de DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8627-104">This page provides troubleshooting information for common Azure DNS questions.</span></span>

<span data-ttu-id="b8627-105">Se essas etapas não resolverem o problema, você pode também procurar ou poste seu problema no nosso [Fórum de suporte da comunidade no MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span><span class="sxs-lookup"><span data-stu-id="b8627-105">If these steps don't resolve your issue, you can also search for or post your issue on our [community support forum on MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork).</span></span> <span data-ttu-id="b8627-106">Como alternativa, abra uma solicitação de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8627-106">Alternatively, open an Azure support request.</span></span>


## <a name="i-cant-create-a-dns-zone"></a><span data-ttu-id="b8627-107">Não consigo criar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="b8627-107">I can't create a DNS zone</span></span>

<span data-ttu-id="b8627-108">Para resolver problemas comuns, tente uma ou mais das etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8627-108">To resolve common issues, try one or more of the following steps:</span></span>

1.  <span data-ttu-id="b8627-109">Examine os logs de auditoria do DNS do Azure para determinar o motivo da falha.</span><span class="sxs-lookup"><span data-stu-id="b8627-109">Review the Azure DNS audit logs to determine the failure reason.</span></span>
2.  <span data-ttu-id="b8627-110">Cada nome de zona DNS deve ser exclusivo dentro de seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b8627-110">Each DNS zone name must be unique within its resource group.</span></span> <span data-ttu-id="b8627-111">Ou seja, duas zonas DNS com o mesmo nome não podem compartilhar um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b8627-111">That is, two DNS zones with the same name cannot share a resource group.</span></span> <span data-ttu-id="b8627-112">Tente usar um nome de zona diferente ou outro grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b8627-112">Try using a different zone name, or a different resource group.</span></span>
3.  <span data-ttu-id="b8627-113">Será exibido um erro "Você atingiu ou excedeu o número máximo de zonas na assinatura {ID da assinatura}."</span><span class="sxs-lookup"><span data-stu-id="b8627-113">You may see an error "You have reached or exceeded the maximum number of zones in subscription {subscription id}."</span></span> <span data-ttu-id="b8627-114">Use uma assinatura do Azure diferente, exclua algumas zonas ou entre em contato com o Suporte do Azure para aumentar o limite de sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="b8627-114">Either use a different Azure subscription, delete some zones, or contact Azure Support to raise your subscription limit.</span></span>
4.  <span data-ttu-id="b8627-115">Você verá um erro "A zona '{nome da zona}' não está disponível."</span><span class="sxs-lookup"><span data-stu-id="b8627-115">You may see an error "The zone '{zone name}' is not available."</span></span> <span data-ttu-id="b8627-116">Esse erro significa que o DNS do Azure não pôde alocar servidores de nome para esta zona DNS.</span><span class="sxs-lookup"><span data-stu-id="b8627-116">This error means that Azure DNS was unable to allocate name servers for this DNS zone.</span></span> <span data-ttu-id="b8627-117">Tente usar um nome de zona diferente.</span><span class="sxs-lookup"><span data-stu-id="b8627-117">Try using a different zone name.</span></span> <span data-ttu-id="b8627-118">Como alternativa, se você for o proprietário do nome de domínio, contate o Suporte do Azure, que poderá alocar servidores de nomes para você.</span><span class="sxs-lookup"><span data-stu-id="b8627-118">Alternatively, if you are the domain name owner, contact Azure support, who can allocate name servers for you.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="b8627-119">**Documentos recomendados**</span><span class="sxs-lookup"><span data-stu-id="b8627-119">**Recommended documents**</span></span>

<span data-ttu-id="b8627-120">[Zonas e registros DNS](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="b8627-120">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="b8627-121">
[Criar uma zona DNS](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="b8627-121">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>

## <a name="i-cant-create-a-dns-record"></a><span data-ttu-id="b8627-122">Não consigo criar um registro DNS</span><span class="sxs-lookup"><span data-stu-id="b8627-122">I can't create a DNS record</span></span>

<span data-ttu-id="b8627-123">Para resolver problemas comuns, tente uma ou mais das etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8627-123">To resolve common issues, try one or more of the following steps:</span></span>

1.  <span data-ttu-id="b8627-124">Examine os logs de auditoria do DNS do Azure para determinar o motivo da falha.</span><span class="sxs-lookup"><span data-stu-id="b8627-124">Review the Azure DNS audit logs to determine the failure reason.</span></span>
2.  <span data-ttu-id="b8627-125">O conjunto de registros já existe?</span><span class="sxs-lookup"><span data-stu-id="b8627-125">Does the record set exist already?</span></span>  <span data-ttu-id="b8627-126">O DNS do Azure gerencia registros usando *conjuntos* de registros, que são a coleção de registros com o mesmo nome e o mesmo tipo.</span><span class="sxs-lookup"><span data-stu-id="b8627-126">Azure DNS manages records using record *sets*, which are the collection of records of the same name and the same type.</span></span> <span data-ttu-id="b8627-127">Se já existe um registro com o mesmo nome e o mesmo tipo, para adicionar outro registro desse você deve editar o conjunto de registros existente.</span><span class="sxs-lookup"><span data-stu-id="b8627-127">If a record with the same name and type already exists, then to add another such record you should edit the existing record set.</span></span>
3.  <span data-ttu-id="b8627-128">Você está tentando criar um registro no ápice da zona DNS (na 'raiz' da zona)?</span><span class="sxs-lookup"><span data-stu-id="b8627-128">Are you trying to create a record at the DNS zone apex (the ‘root’ of the zone)?</span></span> <span data-ttu-id="b8627-129">Se sim, a convenção DNS é usar o caractere “@” como o nome do registro.</span><span class="sxs-lookup"><span data-stu-id="b8627-129">If so, the DNS convention is to use the ‘@’ character as the record name.</span></span> <span data-ttu-id="b8627-130">Observe também que os padrões de DNS não permitem registros CNAME no ápice da zona.</span><span class="sxs-lookup"><span data-stu-id="b8627-130">Also note that the DNS standards do not permit CNAME records at the zone apex.</span></span>
4.  <span data-ttu-id="b8627-131">Existe um conflito de CNAME?</span><span class="sxs-lookup"><span data-stu-id="b8627-131">Do you have a CNAME conflict?</span></span>  <span data-ttu-id="b8627-132">Os padrões de DNS não permitem um registro CNAME com o mesmo nome que um registro de qualquer outro tipo.</span><span class="sxs-lookup"><span data-stu-id="b8627-132">The DNS standards do not allow a CNAME record with the same name as a record of any other type.</span></span> <span data-ttu-id="b8627-133">Se já houver um CNAME existente, a criação de um registro com o mesmo nome de um tipo diferente falhará.</span><span class="sxs-lookup"><span data-stu-id="b8627-133">If you have an existing CNAME, creating a record with the same name of a different type fails.</span></span>  <span data-ttu-id="b8627-134">Da mesma forma, a criação de um CNAME falhará se o nome corresponder a um registro existente de um tipo diferente.</span><span class="sxs-lookup"><span data-stu-id="b8627-134">Likewise, creating a CNAME fails if the name matches an existing record of a different type.</span></span> <span data-ttu-id="b8627-135">Remova o conflito removendo o outro registro ou escolha um nome de registro diferente.</span><span class="sxs-lookup"><span data-stu-id="b8627-135">Remove the conflict by removing the other record or choosing a different record name.</span></span>
5.  <span data-ttu-id="b8627-136">Você atingiu o limite do número de conjuntos de registros permitidos em uma zona DNS?</span><span class="sxs-lookup"><span data-stu-id="b8627-136">Have you reached the limit on the number of record sets permitted in a DNS zone?</span></span> <span data-ttu-id="b8627-137">O número atual de conjuntos de registros e o número máximo de conjuntos de registros são mostrados no Portal do Azure, nas 'Propriedades' da zona.</span><span class="sxs-lookup"><span data-stu-id="b8627-137">The current number of record sets and the maximum number of record sets are shown in the Azure portal, under the 'Properties' for the zone.</span></span> <span data-ttu-id="b8627-138">Se você atingiu esse limite, exclua alguns conjuntos de registros ou contate o Suporte do Azure para aumentar seu limite de conjuntos de registros para esta zona. Em seguida, tente novamente.</span><span class="sxs-lookup"><span data-stu-id="b8627-138">If you have reached this limit, then either delete some record sets or contact Azure Support to raise your record set limit for this zone, then try again.</span></span> 


### <a name="recommended-documents"></a><span data-ttu-id="b8627-139">**Documentos recomendados**</span><span class="sxs-lookup"><span data-stu-id="b8627-139">**Recommended documents**</span></span>

<span data-ttu-id="b8627-140">[Zonas e registros DNS](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="b8627-140">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="b8627-141">
[Criar uma zona DNS](dns-getstarted-create-dnszone-portal.md)</span><span class="sxs-lookup"><span data-stu-id="b8627-141">
[Create a DNS zone](dns-getstarted-create-dnszone-portal.md)</span></span>



## <a name="i-cant-resolve-my-dns-record"></a><span data-ttu-id="b8627-142">Não consigo resolver meu registro DNS</span><span class="sxs-lookup"><span data-stu-id="b8627-142">I can't resolve my DNS record</span></span>

<span data-ttu-id="b8627-143">A resolução de nome DNS é um processo de várias etapas que pode falhar por várias razões.</span><span class="sxs-lookup"><span data-stu-id="b8627-143">DNS name resolution is a multi-step process, which can fail for many reasons.</span></span> <span data-ttu-id="b8627-144">As etapas abaixo ajudam a investigar por que a resolução DNS está falhando para um registro DNS em uma zona hospedada no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8627-144">The following steps help you investigate why DNS resolution is failing for a DNS record in a zone hosted in Azure DNS.</span></span>

1.  <span data-ttu-id="b8627-145">Confirme se os registros DNS foram configurados corretamente no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8627-145">Confirm that the DNS records have been configured correctly in Azure DNS.</span></span> <span data-ttu-id="b8627-146">Examine os registros DNS no Portal do Azure, verificando se o nome da zona, o nome do registro e o tipo de registro estão corretos.</span><span class="sxs-lookup"><span data-stu-id="b8627-146">Review the DNS records in the Azure portal, checking that the zone name, record name, and record type are correct.</span></span>
2.  <span data-ttu-id="b8627-147">Confirme se os registros DNS são resolvidos corretamente nos servidores de nomes DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8627-147">Confirm that the DNS records resolve correctly on the Azure DNS name servers.</span></span>
    - <span data-ttu-id="b8627-148">Se você faz consultas DNS do seu computador local, podem aparecer resultados em cache que não refletem o estado atual dos servidores de nomes.</span><span class="sxs-lookup"><span data-stu-id="b8627-148">If you make DNS queries from your local PC, you may see cached results that don’t reflect the current state of the name servers.</span></span>  <span data-ttu-id="b8627-149">Além disso, as redes corporativas geralmente usam servidores proxy DNS que impedem que as consultas DNS sejam direcionadas a servidores de nomes específicos.</span><span class="sxs-lookup"><span data-stu-id="b8627-149">Also, corporate networks often use DNS proxy servers, which prevent DNS queries from being directed to specific name servers.</span></span>  <span data-ttu-id="b8627-150">Para evitar esses problemas, use um serviço de resolução de nome baseado na Web, como [digwebinterface](http://digwebinterface.com).</span><span class="sxs-lookup"><span data-stu-id="b8627-150">To avoid these problems, use a web-based name resolution service such as [digwebinterface](http://digwebinterface.com).</span></span>
    - <span data-ttu-id="b8627-151">Especifique os servidores de nomes corretos para sua zona DNS, conforme exibido no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8627-151">Be sure to specify the correct name servers for your DNS zone, as shown in the Azure portal.</span></span>
    - <span data-ttu-id="b8627-152">Verifique se o nome DNS está correto (será necessário especificar o nome totalmente qualificado, incluindo o nome da zona) e se o tipo de registro está correto</span><span class="sxs-lookup"><span data-stu-id="b8627-152">Check that the DNS name is correct (you have to specify the fully qualified name, including the zone name) and the record type is correct</span></span>
3.  <span data-ttu-id="b8627-153">Confirme se o nome de domínio DNS foi [delegado corretamente aos servidores de nomes DNS do Azure](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="b8627-153">Confirm that the DNS domain name has been correctly [delegated to the Azure DNS name servers](dns-domain-delegation.md).</span></span> <span data-ttu-id="b8627-154">Há [vários sites da Web de terceiros que oferecem validação de delegação DNS](https://www.bing.com/search?q=dns+check+tool).</span><span class="sxs-lookup"><span data-stu-id="b8627-154">There are a [many 3rd-party web sites that offer DNS delegation validation](https://www.bing.com/search?q=dns+check+tool).</span></span> <span data-ttu-id="b8627-155">Esse é um teste de delegação de *zona*, portanto você deve inserir apenas o nome da zona DNS e não o nome totalmente qualificado do registro.</span><span class="sxs-lookup"><span data-stu-id="b8627-155">This test is a *zone* delegation test, so you should only enter the DNS zone name and not the fully qualified record name.</span></span>
4.  <span data-ttu-id="b8627-156">Após a conclusão da ação acima, o registro DNS deverá ser resolvido corretamente.</span><span class="sxs-lookup"><span data-stu-id="b8627-156">Having completed the above, your DNS record should now resolve correctly.</span></span> <span data-ttu-id="b8627-157">Para verificar, você pode usar [digwebinterface](http://digwebinterface.com) novamente, desta vez, usando as configurações de servidor de nomes padrão.</span><span class="sxs-lookup"><span data-stu-id="b8627-157">To verify, you can again use [digwebinterface](http://digwebinterface.com), this time using the default name server settings.</span></span>


### <a name="recommended-documents"></a><span data-ttu-id="b8627-158">**Documentos recomendados**</span><span class="sxs-lookup"><span data-stu-id="b8627-158">**Recommended documents**</span></span>

[<span data-ttu-id="b8627-159">Delegar um domínio ao DNS do Azure</span><span class="sxs-lookup"><span data-stu-id="b8627-159">Delegate a domain to Azure DNS</span></span>](dns-domain-delegation.md)



## <a name="how-do-i-specify-the-service-and-protocol-for-an-srv-record"></a><span data-ttu-id="b8627-160">Como especificar o 'serviço' e o 'protocolo' para um registro SRV?</span><span class="sxs-lookup"><span data-stu-id="b8627-160">How do I specify the ‘service’ and ‘protocol’ for an SRV record?</span></span>

<span data-ttu-id="b8627-161">O DNS do Azure gerencia os registros DNS como conjuntos de registros, ou seja, a coleção de registros com o mesmo nome e o mesmo tipo.</span><span class="sxs-lookup"><span data-stu-id="b8627-161">Azure DNS manages DNS records as record sets—the collection of records with the same name and the same type.</span></span> <span data-ttu-id="b8627-162">Para um conjunto de registros SRV, o 'serviço' e o 'protocolo' precisam ser especificados como parte do nome do conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="b8627-162">For an SRV record set, the 'service' and 'protocol' need to be specified as part of the record set name.</span></span> <span data-ttu-id="b8627-163">Os outros parâmetros de SRV ('prioridade', 'peso', 'porta' e 'destino') são especificados separadamente para cada registro no conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="b8627-163">The other SRV parameters ('priority', 'weight', 'port' and 'target') are specified separately for each record in the record set.</span></span>

<span data-ttu-id="b8627-164">Exemplo de nomes de registro SRV (nome de serviço 'sip', protocolo 'tcp'):</span><span class="sxs-lookup"><span data-stu-id="b8627-164">Example SRV record names (service name 'sip', protocol 'tcp'):</span></span>

- <span data-ttu-id="b8627-165">\_sip.\_tcp (cria um conjunto de registros no ápice da zona)</span><span class="sxs-lookup"><span data-stu-id="b8627-165">\_sip.\_tcp (creates a record set at the zone apex)</span></span>
- <span data-ttu-id="b8627-166">\_sip.\_tcp.sipservice (cria um conjunto de registros chamado 'sipservice')</span><span class="sxs-lookup"><span data-stu-id="b8627-166">\_sip.\_tcp.sipservice (creates a record set named 'sipservice')</span></span>

### <a name="recommended-documents"></a><span data-ttu-id="b8627-167">**Documentos recomendados**</span><span class="sxs-lookup"><span data-stu-id="b8627-167">**Recommended documents**</span></span>

<span data-ttu-id="b8627-168">[Zonas e registros DNS](dns-zones-records.md)
</span><span class="sxs-lookup"><span data-stu-id="b8627-168">[DNS zones and records](dns-zones-records.md)
</span></span><br><span data-ttu-id="b8627-169">
[Criar registros e conjuntos de registros DNS usando o portal do Azure](dns-getstarted-create-recordset-portal.md)
</span><span class="sxs-lookup"><span data-stu-id="b8627-169">
[Create DNS record sets and records by using the Azure portal](dns-getstarted-create-recordset-portal.md)
</span></span><br><span data-ttu-id="b8627-170">
[Tipo de registro SRV (Wikipédia)](https://en.wikipedia.org/wiki/SRV_record)</span><span class="sxs-lookup"><span data-stu-id="b8627-170">
[SRV record type (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)</span></span>


## <a name="next-steps"></a><span data-ttu-id="b8627-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b8627-171">Next steps</span></span>

* <span data-ttu-id="b8627-172">Saiba mais sobre [registros e zonas DNS do Azure](dns-zones-records.md)</span><span class="sxs-lookup"><span data-stu-id="b8627-172">Learn about [Azure DNS zones and records](dns-zones-records.md)</span></span>
* <span data-ttu-id="b8627-173">Para começar a usar o DNS do Azure, aprenda a [criar uma zona DNS](dns-getstarted-create-dnszone-portal.md) e a [criar registros DNS](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b8627-173">To start using Azure DNS, learn how to [create a DNS zone](dns-getstarted-create-dnszone-portal.md) and [create DNS records](dns-getstarted-create-recordset-portal.md).</span></span>
* <span data-ttu-id="b8627-174">Para migrar uma zona DNS existente, saiba como [importar e exportar um arquivo de zona DNS](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="b8627-174">To migrate an existing DNS zone, learn how to [import and export a DNS zone file](dns-import-export.md).</span></span>

