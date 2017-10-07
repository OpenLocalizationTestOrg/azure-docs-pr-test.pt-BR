---
title: "aaaConfigure um nome de domínio personalizado em serviços de nuvem | Microsoft Docs"
description: "Saiba como tooexpose sua toohello de dados ou aplicativo do Azure internet em um domínio personalizado, definindo configurações de DNS.  Esses exemplos usam Olá portal do Azure."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 5783a246-a151-4fb1-b488-441bfb29ee44
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: a0f3186b6022fbc4570ef1ce4b921426842bde76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a><span data-ttu-id="7f886-104">Configurando um nome de domínio personalizado para um serviço de nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="7f886-104">Configuring a custom domain name for an Azure cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7f886-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7f886-105">Azure portal</span></span>](cloud-services-custom-domain-name-portal.md)
> * [<span data-ttu-id="7f886-106">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="7f886-106">Azure classic portal</span></span>](cloud-services-custom-domain-name.md)
> 
> 

<span data-ttu-id="7f886-107">Quando você cria um serviço de nuvem, Azure atribui subdomínio tooa de **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="7f886-107">When you create a Cloud Service, Azure assigns it tooa subdomain of **cloudapp.net**.</span></span> <span data-ttu-id="7f886-108">Por exemplo, se seu serviço de nuvem é denominado "contoso", os usuários serão ser capaz de tooaccess seu aplicativo em uma URL como http://contoso.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="7f886-108">For example, if your Cloud Service is named "contoso", your users will be able tooaccess your application on a URL like http://contoso.cloudapp.net.</span></span> <span data-ttu-id="7f886-109">O Azure também fornece um endereço IP virtual.</span><span class="sxs-lookup"><span data-stu-id="7f886-109">Azure also assigns a virtual IP address.</span></span>

<span data-ttu-id="7f886-110">No entanto, você também pode expor seu aplicativo em seu próprio nome de domínio, como **contoso.com**. Este artigo explica como tooreserve ou configurar um nome de domínio personalizado para funções de web do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="7f886-110">However, you can also expose your application on your own domain name, such as **contoso.com**. This article explains how tooreserve or configure a custom domain name for Cloud Service web roles.</span></span>

<span data-ttu-id="7f886-111">Você já entendeu o que são os registros CNAME e A?</span><span class="sxs-lookup"><span data-stu-id="7f886-111">Do you already understand what CNAME and A records are?</span></span> <span data-ttu-id="7f886-112">[Salto após Olá explicação](#add-a-cname-record-for-your-custom-domain).</span><span class="sxs-lookup"><span data-stu-id="7f886-112">[Jump past hello explanation](#add-a-cname-record-for-your-custom-domain).</span></span>

> [!NOTE]
> <span data-ttu-id="7f886-113">procedimentos de saudação nesta tarefa aplicam tooAzure serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="7f886-113">hello procedures in this task apply tooAzure Cloud Services.</span></span> <span data-ttu-id="7f886-114">Para os Serviços de Aplicativos, veja [isto](../app-service-web/web-sites-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="7f886-114">For App Services, see [this](../app-service-web/web-sites-custom-domain-name.md).</span></span> <span data-ttu-id="7f886-115">Para as contas de armazenamento, veja [isto](../storage/blobs/storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="7f886-115">For storage accounts, see [this](../storage/blobs/storage-custom-domain-name.md).</span></span>
> 
> 

<p/>

> [!TIP]
> <span data-ttu-id="7f886-116">Familiarize-se mais rápido – use hello Azure novo [orientada passo a passo](http://support.microsoft.com/kb/2990804)!</span><span class="sxs-lookup"><span data-stu-id="7f886-116">Get going faster--use hello NEW Azure [guided walkthrough](http://support.microsoft.com/kb/2990804)!</span></span>  <span data-ttu-id="7f886-117">Ele torna rápido a associação de um nome de domínio personalizado E a proteção da comunicação (SSL) com os Serviços de Nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f886-117">It makes associating a custom domain name AND securing communication (SSL) with Azure Cloud Services or Azure Websites a snap.</span></span>
> 
> 

## <a name="understand-cname-and-a-records"></a><span data-ttu-id="7f886-118">Entenda os registros CNAME e A</span><span class="sxs-lookup"><span data-stu-id="7f886-118">Understand CNAME and A records</span></span>
<span data-ttu-id="7f886-119">CNAME (ou registros de alias) e registros de ambos permitem que você tooassociate um nome de domínio com um servidor específico (ou serviço nesse caso,) porém eles funcionam de forma diferente.</span><span class="sxs-lookup"><span data-stu-id="7f886-119">CNAME (or alias records) and A records both allow you tooassociate a domain name with a specific server (or service in this case,) however they work differently.</span></span> <span data-ttu-id="7f886-120">Também há algumas considerações específicas ao usar registros com os serviços de nuvem do Azure que você deve considerar antes de decidir quais toouse.</span><span class="sxs-lookup"><span data-stu-id="7f886-120">There are also some specific considerations when using A records with Azure Cloud services that you should consider before deciding which toouse.</span></span>

### <a name="cname-or-alias-record"></a><span data-ttu-id="7f886-121">Registro CNAME ou de alias</span><span class="sxs-lookup"><span data-stu-id="7f886-121">CNAME or Alias record</span></span>
<span data-ttu-id="7f886-122">Um registro CNAME mapeia um *específico* domínio, como **contoso.com** ou **www.contoso.com**, nome de domínio canônico tooa.</span><span class="sxs-lookup"><span data-stu-id="7f886-122">A CNAME record maps a *specific* domain, such as **contoso.com** or **www.contoso.com**, tooa canonical domain name.</span></span> <span data-ttu-id="7f886-123">Nesse caso, o nome de domínio canônico Olá é hello **.cloudapp [myapp] .net** nome de domínio do seu Azure hospedado aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7f886-123">In this case, hello canonical domain name is hello **[myapp].cloudapp.net** domain name of your Azure hosted application.</span></span> <span data-ttu-id="7f886-124">Depois de criado, Olá CNAME cria um alias para Olá **.cloudapp [myapp] .net**.</span><span class="sxs-lookup"><span data-stu-id="7f886-124">Once created, hello CNAME creates an alias for hello **[myapp].cloudapp.net**.</span></span> <span data-ttu-id="7f886-125">Olá entrada CNAME resolverá toohello endereço IP do seu **.cloudapp [myapp] .net** serviço automaticamente, para que se mudar de endereço IP Olá Olá do serviço de nuvem, você não tem tootake qualquer ação.</span><span class="sxs-lookup"><span data-stu-id="7f886-125">hello CNAME entry will resolve toohello IP address of your **[myapp].cloudapp.net** service automatically, so if hello IP address of hello cloud service changes, you do not have tootake any action.</span></span>

> [!NOTE]
> <span data-ttu-id="7f886-126">Alguns registradores de domínio permitem subdomínios toomap ao usar um registro CNAME, como www.contoso.com e não nomes de raiz, como contoso.com. Para obter mais informações sobre os registros CNAME, consulte a documentação de saudação fornecida por seu registrador [Olá entrada da Wikipedia no registro CNAME](http://en.wikipedia.org/wiki/CNAME_record), ou hello [nomes de domínio IETF - implementação e especificação](http://tools.ietf.org/html/rfc1035) documento.</span><span class="sxs-lookup"><span data-stu-id="7f886-126">Some domain registrars only allow you toomap subdomains when using a CNAME record, such as www.contoso.com, and not root names, such as contoso.com. For more information on CNAME records, see hello documentation provided by your registrar, [hello Wikipedia entry on CNAME record](http://en.wikipedia.org/wiki/CNAME_record), or hello [IETF Domain Names - Implementation and Specification](http://tools.ietf.org/html/rfc1035) document.</span></span>
> 
> 

### <a name="a-record"></a><span data-ttu-id="7f886-127">Registro A</span><span class="sxs-lookup"><span data-stu-id="7f886-127">A record</span></span>
<span data-ttu-id="7f886-128">Um *um* registro mapeia um domínio, como **contoso.com** ou **www.contoso.com**, *ou um domínio curinga* como  **\*. contoso.com**, endereço IP tooan.</span><span class="sxs-lookup"><span data-stu-id="7f886-128">An *A* record maps a domain, such as **contoso.com** or **www.contoso.com**, *or a wildcard domain* such as **\*.contoso.com**, tooan IP address.</span></span> <span data-ttu-id="7f886-129">No caso de saudação de um serviço de nuvem do Azure, Olá IP virtual do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f886-129">In hello case of an Azure Cloud Service, hello virtual IP of hello service.</span></span> <span data-ttu-id="7f886-130">Portanto Olá principal benefício de um registro em um registro CNAME é que você pode ter uma entrada que usa um caractere curinga, como \* **. contoso.com**, que poderia tratar as solicitações de vários subdomínios como  **mail.contoso.com**, **login.contoso.com**, ou **www.contso.com**.</span><span class="sxs-lookup"><span data-stu-id="7f886-130">So hello main benefit of an A record over a CNAME record is that you can have one entry that uses a wildcard, such as \***.contoso.com**, which would handle requests for multiple sub-domains such as **mail.contoso.com**, **login.contoso.com**, or **www.contso.com**.</span></span>

> [!NOTE]
> <span data-ttu-id="7f886-131">Como um registro é mapeado tooa endereço IP, ele automaticamente não puder resolver o endereço IP de toohello alterações do seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="7f886-131">Since an A record is mapped tooa static IP address, it cannot automatically resolve changes toohello IP address of your Cloud Service.</span></span> <span data-ttu-id="7f886-132">Olá alocar endereço IP usado pelo serviço de nuvem é Olá primeira vez que você implantar tooan o slot vazio (produção ou preparo.) Se você excluir a implantação de saudação slot hello, endereço IP de saudação é liberado pelo Azure e qualquer intervalo de toohello implantações futuras pode receber um novo endereço IP.</span><span class="sxs-lookup"><span data-stu-id="7f886-132">hello IP address used by your Cloud Service is allocated hello first time you deploy tooan empty slot (either production or staging.) If you delete hello deployment for hello slot, hello IP address is released by Azure and any future deployments toohello slot may be given a new IP address.</span></span>
> 
> <span data-ttu-id="7f886-133">Convenientemente, endereço IP de saudação de um slot de implantação especificada (produção ou preparo) é mantido durante a troca entre o preparo e implantações de produção ou executar uma atualização in-loco de uma implantação existente.</span><span class="sxs-lookup"><span data-stu-id="7f886-133">Conveniently, hello IP address of a given deployment slot (production or staging) is persisted when swapping between staging and production deployments or performing an in-place upgrade of an existing deployment.</span></span> <span data-ttu-id="7f886-134">Para obter mais informações sobre como executar essas ações, consulte [como serviços em nuvem toomanage](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="7f886-134">For more information on performing these actions, see [How toomanage cloud services](cloud-services-how-to-manage.md).</span></span>
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="7f886-135">Adicionar um registro CNAME para seu domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="7f886-135">Add a CNAME record for your custom domain</span></span>
<span data-ttu-id="7f886-136">toocreate um registro CNAME, você deve adicionar uma nova entrada na tabela DNS Olá para seu domínio personalizado usando ferramentas de Olá fornecidas por seu registrador.</span><span class="sxs-lookup"><span data-stu-id="7f886-136">toocreate a CNAME record, you must add a new entry in hello DNS table for your custom domain by using hello tools provided by your registrar.</span></span> <span data-ttu-id="7f886-137">Cada registro tem um método semelhante, mas um pouco diferentes de especificar um registro CNAME, mas Olá conceitos são Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="7f886-137">Each registrar has a similar but slightly different method of specifying a CNAME record, but hello concepts are hello same.</span></span>

1. <span data-ttu-id="7f886-138">Use uma saudação de toofind esses métodos **. cloudapp.net** nome de domínio atribuído tooyour serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="7f886-138">Use one of these methods toofind hello **.cloudapp.net** domain name assigned tooyour cloud service.</span></span>
   
   * <span data-ttu-id="7f886-139">Logon toohello [portal do Azure], selecione seu serviço de nuvem, examinar Olá **Essentials** seção e, em seguida, localize Olá **URL do Site** entrada.</span><span class="sxs-lookup"><span data-stu-id="7f886-139">Login toohello [Azure portal], select your cloud service, look at hello **Essentials** section and then find hello **Site URL** entry.</span></span>
     
       ![seção visão rápida mostra a URL do site Olá][csurl]
     
       <span data-ttu-id="7f886-141">**OR**</span><span class="sxs-lookup"><span data-stu-id="7f886-141">**OR**</span></span>
   * <span data-ttu-id="7f886-142">Instalar e configurar [Azure Powershell](/powershell/azure/overview), e, em seguida, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7f886-142">Install and configure [Azure Powershell](/powershell/azure/overview), and then use hello following command:</span></span>
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     <span data-ttu-id="7f886-143">Salve o nome de domínio Olá usado na URL de saudação retornado por qualquer método, pois você precisará dele durante a criação de um registro CNAME.</span><span class="sxs-lookup"><span data-stu-id="7f886-143">Save hello domain name used in hello URL returned by either method, as you will need it when creating a CNAME record.</span></span>
2. <span data-ttu-id="7f886-144">Faça logon no site do registrador DNS tooyour e vá para a página toohello para gerenciar DNS.</span><span class="sxs-lookup"><span data-stu-id="7f886-144">Log on tooyour DNS registrar's website and go toohello page for managing DNS.</span></span> <span data-ttu-id="7f886-145">Procure links ou áreas do site de saudação rotulados como **nome de domínio**, **DNS**, ou **nome do servidor de gerenciamento**.</span><span class="sxs-lookup"><span data-stu-id="7f886-145">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="7f886-146">Agora, encontre onde você pode selecionar ou inserir registros CNAME.</span><span class="sxs-lookup"><span data-stu-id="7f886-146">Now find where you can select or enter CNAME's.</span></span> <span data-ttu-id="7f886-147">Você pode ter o registro de saudação tooselect digite uma lista suspensa ou vá tooan página de configurações avançadas.</span><span class="sxs-lookup"><span data-stu-id="7f886-147">You may have tooselect hello record type from a drop down, or go tooan advanced settings page.</span></span> <span data-ttu-id="7f886-148">Você deve procurar palavras Olá **CNAME**, **Alias**, ou **subdomínios**.</span><span class="sxs-lookup"><span data-stu-id="7f886-148">You should look for hello words **CNAME**, **Alias**, or **Subdomains**.</span></span>
4. <span data-ttu-id="7f886-149">Você também deve fornecer Olá domínio ou subdomínio alias para Olá CNAME, tais como **www** se você quiser que um alias para toocreate **www.customdomain.com**. Se você quiser toocreate um alias para o domínio raiz da saudação, ele pode estar listado como Olá '**@**' símbolo em Ferramentas DNS do registrador.</span><span class="sxs-lookup"><span data-stu-id="7f886-149">You must also provide hello domain or subdomain alias for hello CNAME, such as **www** if you want toocreate an alias for **www.customdomain.com**. If you want toocreate an alias for hello root domain, it may be listed as hello '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="7f886-150">Em seguida, você deve fornecer um nome do host canônico, que, neste caso, é o domínio **cloudapp.net** do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7f886-150">Then, you must provide a canonical host name, which is your application's **cloudapp.net** domain in this case.</span></span>

<span data-ttu-id="7f886-151">Por exemplo, a saudação após o registro CNAME encaminha todo o tráfego de **www.contoso.com** muito**contoso.cloudapp.net**, nome de domínio personalizado de saudação do seu aplicativo implantado:</span><span class="sxs-lookup"><span data-stu-id="7f886-151">For example, hello following CNAME record forwards all traffic from **www.contoso.com** too**contoso.cloudapp.net**, hello custom domain name of your deployed application:</span></span>

| <span data-ttu-id="7f886-152">Alias/Nome do host/Subdomínio</span><span class="sxs-lookup"><span data-stu-id="7f886-152">Alias/Host name/Subdomain</span></span> | <span data-ttu-id="7f886-153">Domínio canônico</span><span class="sxs-lookup"><span data-stu-id="7f886-153">Canonical domain</span></span> |
| --- | --- |
| <span data-ttu-id="7f886-154">www</span><span class="sxs-lookup"><span data-stu-id="7f886-154">www</span></span> |<span data-ttu-id="7f886-155">contoso.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="7f886-155">contoso.cloudapp.net</span></span> |

> [!NOTE]
> <span data-ttu-id="7f886-156">Um visitante de **www.contoso.com** nunca verá host true da saudação (contoso.cloudapp.net), Olá processo de encaminhamento é o usuário final de toothe invisível.</span><span class="sxs-lookup"><span data-stu-id="7f886-156">A visitor of **www.contoso.com** will never see hello true host (contoso.cloudapp.net), so hello forwarding process is invisible toothe end user.</span></span>
> 
> <span data-ttu-id="7f886-157">Olá exemplo acima se aplica apenas tootraffic em Olá **www** subdomínio.</span><span class="sxs-lookup"><span data-stu-id="7f886-157">hello example above only applies tootraffic at hello **www** subdomain.</span></span> <span data-ttu-id="7f886-158">Uma vez que não é possível usar caracteres curinga com registros CNAME, você deve criar um CNAME para cada domínio/subdomínio.</span><span class="sxs-lookup"><span data-stu-id="7f886-158">Since you cannot use wildcards with CNAME records, you must create one CNAME for each domain/subdomain.</span></span> <span data-ttu-id="7f886-159">Se você quiser toodirect tráfego de subdomínios, como *. contoso.com, tooyour cloudapp.net endereço, você pode configurar um **redirecionamento de URL** ou **URL Forward** entrada em suas configurações de DNS, ou crie um registro.</span><span class="sxs-lookup"><span data-stu-id="7f886-159">If you want toodirect  traffic from subdomains, such as *.contoso.com, tooyour cloudapp.net address, you can configure a **URL Redirect** or **URL Forward** entry in your DNS settings, or create an A record.</span></span>
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a><span data-ttu-id="7f886-160">Adicionar um registro A ao seu domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="7f886-160">Add an A record for your custom domain</span></span>
<span data-ttu-id="7f886-161">toocreate um um registro, você deve primeiro localizar endereço IP virtual de saudação do seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="7f886-161">toocreate an A record, you must first find hello virtual IP address of your cloud service.</span></span> <span data-ttu-id="7f886-162">Em seguida, adicione uma nova entrada na tabela DNS Olá para seu domínio personalizado usando ferramentas de Olá fornecidas por seu registrador.</span><span class="sxs-lookup"><span data-stu-id="7f886-162">Then add a new entry in hello DNS table for your custom domain by using hello tools provided by your registrar.</span></span> <span data-ttu-id="7f886-163">Cada registro tem um método semelhante, mas um pouco diferentes de especificar um registro, mas Olá conceitos são Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="7f886-163">Each registrar has a similar but slightly different method of specifying an A record, but hello concepts are hello same.</span></span>

1. <span data-ttu-id="7f886-164">Use um dos seguinte métodos tooget Olá endereço IP de seu serviço de nuvem de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f886-164">Use one of hello following methods tooget hello IP address of your cloud service.</span></span>
   
   * <span data-ttu-id="7f886-165">Logon toohello [portal do Azure], selecione seu serviço de nuvem, examinar Olá **Essentials** seção e, em seguida, localize Olá **endereços IP públicos** entrada.</span><span class="sxs-lookup"><span data-stu-id="7f886-165">Login toohello [Azure portal], select your cloud service, look at hello **Essentials** section and then find hello **Public IP addresses** entry.</span></span>
     
       ![seção visão rápida mostrando Olá VIP][vip]
     
       <span data-ttu-id="7f886-167">**OR**</span><span class="sxs-lookup"><span data-stu-id="7f886-167">**OR**</span></span>
   * <span data-ttu-id="7f886-168">Instalar e configurar [Azure Powershell](/powershell/azure/overview), e, em seguida, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7f886-168">Install and configure [Azure Powershell](/powershell/azure/overview), and then use hello following command:</span></span>
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     <span data-ttu-id="7f886-169">Salve endereço IP hello, pois você precisará dele durante a criação de um registro.</span><span class="sxs-lookup"><span data-stu-id="7f886-169">Save hello IP address, as you will need it when creating an A record.</span></span>
2. <span data-ttu-id="7f886-170">Faça logon no site do registrador DNS tooyour e vá para a página toohello para gerenciar DNS.</span><span class="sxs-lookup"><span data-stu-id="7f886-170">Log on tooyour DNS registrar's website and go toohello page for managing DNS.</span></span> <span data-ttu-id="7f886-171">Procure links ou áreas do site de saudação rotulados como **nome de domínio**, **DNS**, ou **nome do servidor de gerenciamento**.</span><span class="sxs-lookup"><span data-stu-id="7f886-171">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="7f886-172">Agora, encontre onde você pode selecionar ou inserir registros A.</span><span class="sxs-lookup"><span data-stu-id="7f886-172">Now find where you can select or enter A record's.</span></span> <span data-ttu-id="7f886-173">Você pode ter o registro de saudação tooselect digite uma lista suspensa ou vá tooan página de configurações avançadas.</span><span class="sxs-lookup"><span data-stu-id="7f886-173">You may have tooselect hello record type from a drop down, or go tooan advanced settings page.</span></span>
4. <span data-ttu-id="7f886-174">Selecione ou digite o domínio de saudação ou subdomínio que usará esse registro.</span><span class="sxs-lookup"><span data-stu-id="7f886-174">Select or enter hello domain or subdomain that will use this A record.</span></span> <span data-ttu-id="7f886-175">Por exemplo, selecione **www** se você quiser que um alias para toocreate **www.customdomain.com**. Se você quiser toocreate uma entrada de curinga para todos os subdomínios, digite ' * '.</span><span class="sxs-lookup"><span data-stu-id="7f886-175">For example, select **www** if you want toocreate an alias for **www.customdomain.com**. If you want toocreate a wildcard entry for all subdomains, enter '*****'.</span></span> <span data-ttu-id="7f886-176">Isso cobrirá todos os subdomínios, como **mail.customdomain.com**, **login.customdomain.com** e **www.customdomain.com**.</span><span class="sxs-lookup"><span data-stu-id="7f886-176">This will cover all sub-domains such as **mail.customdomain.com**, **login.customdomain.com**, and **www.customdomain.com**.</span></span>
   
    <span data-ttu-id="7f886-177">Se você quiser toocreate um um registro para o domínio raiz da saudação, ele pode estar listado como Olá '**@**' símbolo em Ferramentas DNS do registrador.</span><span class="sxs-lookup"><span data-stu-id="7f886-177">If you want toocreate an A record for hello root domain, it may be listed as hello '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="7f886-178">Digite o endereço IP de saudação do seu serviço de nuvem no Olá fornecido campo.</span><span class="sxs-lookup"><span data-stu-id="7f886-178">Enter hello IP address of your cloud service in hello provided field.</span></span> <span data-ttu-id="7f886-179">Isso associa a entrada de domínio Olá usada no registro Olá com o endereço IP de saudação da sua implantação do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="7f886-179">This associates hello domain entry used in hello A record with hello IP address of your cloud service deployment.</span></span>

<span data-ttu-id="7f886-180">Por exemplo, a saudação um registro a seguir encaminha todo o tráfego de **contoso.com** muito**137.135.70.239**, Olá o endereço IP do seu aplicativo implantado:</span><span class="sxs-lookup"><span data-stu-id="7f886-180">For example, hello following A record forwards all traffic from **contoso.com** too**137.135.70.239**, hello IP address of your deployed application:</span></span>

| <span data-ttu-id="7f886-181">Nome do host/Subdomínio</span><span class="sxs-lookup"><span data-stu-id="7f886-181">Host name/Subdomain</span></span> | <span data-ttu-id="7f886-182">Endereço IP</span><span class="sxs-lookup"><span data-stu-id="7f886-182">IP address</span></span> |
| --- | --- |
| @ |<span data-ttu-id="7f886-183">137.135.70.239</span><span class="sxs-lookup"><span data-stu-id="7f886-183">137.135.70.239</span></span> |

<span data-ttu-id="7f886-184">Este exemplo demonstra como criar um registro a para o domínio raiz da saudação.</span><span class="sxs-lookup"><span data-stu-id="7f886-184">This example demonstrates creating an A record for hello root domain.</span></span> <span data-ttu-id="7f886-185">Se você quiser toocreate toocover de entrada um curinga todos os subdomínios, digite ' * ' como o subdomínio hello.</span><span class="sxs-lookup"><span data-stu-id="7f886-185">If you wish toocreate a wildcard entry toocover all subdomains, you would enter '*****' as hello subdomain.</span></span>

> [!WARNING]
> <span data-ttu-id="7f886-186">Endereços IP no Azure são dinâmicos por padrão.</span><span class="sxs-lookup"><span data-stu-id="7f886-186">IP addresses in Azure are dynamic by default.</span></span> <span data-ttu-id="7f886-187">Você provavelmente desejará toouse um [do endereço IP reservado](../virtual-network/virtual-networks-reserved-public-ip.md) tooensure que seu endereço IP não é alterado.</span><span class="sxs-lookup"><span data-stu-id="7f886-187">You will probably want toouse a [reserved IP address](../virtual-network/virtual-networks-reserved-public-ip.md) tooensure that your IP address does not change.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="7f886-188">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7f886-188">Next steps</span></span>
* [<span data-ttu-id="7f886-189">Como os serviços de nuvem tooManage</span><span class="sxs-lookup"><span data-stu-id="7f886-189">How tooManage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="7f886-190">Como tooMap conteúdo CDN tooa domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="7f886-190">How tooMap CDN Content tooa Custom Domain</span></span>](../cdn/cdn-map-content-to-custom-domain.md)
* <span data-ttu-id="7f886-191">[Configuração geral do serviço de nuvem](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7f886-191">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="7f886-192">Saiba como muito[implantar um serviço de nuvem](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7f886-192">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="7f886-193">Configurar [certificados SSL](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7f886-193">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: cloud-services-how-to-manage-portal.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
[Create a CNAME record that associates hello subdomain with hello storage account]: #create-cname
[portal do Azure]: https://portal.azure.com
[vip]: ./media/cloud-services-custom-domain-name-portal/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name-portal/csurl.png
