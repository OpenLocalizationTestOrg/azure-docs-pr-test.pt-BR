---
title: "Configurar um nome de domínio personalizado nos Serviços de Nuvem | Microsoft Docs"
description: "Saiba como expor seus dados ou seu aplicativo do Azure em um domínio personalizado definindo as configurações de DNS."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 6a62c2b7-ea47-4cce-9d6a-0cca38357f42
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 9f872fd5119042945356225a80331da18f3a6d99
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a><span data-ttu-id="3dad8-103">Configurando um nome de domínio personalizado para um serviço de nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="3dad8-103">Configuring a custom domain name for an Azure cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3dad8-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3dad8-104">Azure portal</span></span>](cloud-services-custom-domain-name-portal.md)
> * [<span data-ttu-id="3dad8-105">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="3dad8-105">Azure classic portal</span></span>](cloud-services-custom-domain-name.md)
> 
> 

<span data-ttu-id="3dad8-106">Quando você cria um Serviço de Nuvem, o Azure o atribui a um subdomínio do cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="3dad8-106">When you create a Cloud Service, Azure assigns it to a subdomain of cloudapp.net.</span></span> <span data-ttu-id="3dad8-107">Por exemplo, se o Serviço de Nuvem for denominado "contoso", os usuários poderão acessar seu aplicativo usando uma URL como http://contoso.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="3dad8-107">For example, if your Cloud Service is named "contoso", your users will be able to access your application on a URL like http://contoso.cloudapp.net.</span></span> <span data-ttu-id="3dad8-108">O Azure também fornece um endereço IP virtual.</span><span class="sxs-lookup"><span data-stu-id="3dad8-108">Azure also assigns a virtual IP address.</span></span>

<span data-ttu-id="3dad8-109">No entanto, você também pode expor sua aplicação em seu próprio nome de domínio, como contoso.com. Este artigo explica como reservar ou configurar um nome de domínio personalizado para funções Web do Serviço de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="3dad8-109">However, you can also expose your application on your own domain name, such as contoso.com. This article explains how to reserve or configure a custom domain name for Cloud Service web roles.</span></span>

<span data-ttu-id="3dad8-110">Você já entendeu o que são os registros CNAME e A?</span><span class="sxs-lookup"><span data-stu-id="3dad8-110">Do you already understand what CNAME and A records are?</span></span> <span data-ttu-id="3dad8-111">[Pule a explicação](#add-a-cname-record-for-your-custom-domain).</span><span class="sxs-lookup"><span data-stu-id="3dad8-111">[Jump past the explanation](#add-a-cname-record-for-your-custom-domain).</span></span>

> [!NOTE]
> <span data-ttu-id="3dad8-112">Agilize o trabalho!</span><span class="sxs-lookup"><span data-stu-id="3dad8-112">Get going faster!</span></span> <span data-ttu-id="3dad8-113">Use o [passo a passo guiado](http://support.microsoft.com/kb/2990804)do Azure.</span><span class="sxs-lookup"><span data-stu-id="3dad8-113">Use the Azure [guided walkthrough](http://support.microsoft.com/kb/2990804).</span></span> <span data-ttu-id="3dad8-114">Ele torna rápido a associação de um nome de domínio personalizado E a proteção da comunicação (SSL) com os Serviços de Nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="3dad8-114">It makes associating a custom domain name and securing communication (SSL) with Azure Cloud Services or Azure Websites a snap.</span></span>
> 
> 

<p/>

> [!NOTE]
> <span data-ttu-id="3dad8-115">Os procedimentos nesta tarefa se aplicam aos Serviços de Nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="3dad8-115">The procedures in this task apply to Azure Cloud Services.</span></span> <span data-ttu-id="3dad8-116">Para os Serviços de Aplicativos, veja [isto](../app-service-web/web-sites-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="3dad8-116">For App Services, see [this](../app-service-web/web-sites-custom-domain-name.md).</span></span> <span data-ttu-id="3dad8-117">Para as contas de armazenamento, veja [isto](../storage/blobs/storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="3dad8-117">For storage accounts, see [this](../storage/blobs/storage-custom-domain-name.md).</span></span>
> 
> 

## <a name="understand-cname-and-a-records"></a><span data-ttu-id="3dad8-118">Entenda os registros CNAME e A</span><span class="sxs-lookup"><span data-stu-id="3dad8-118">Understand CNAME and A records</span></span>
<span data-ttu-id="3dad8-119">Os registros CNAME (ou registros de alias) e A permitem que você associe um nome de domínio a um servidor específico (ou serviço neste caso), de qualquer forma, cada um deles funciona de modo diferente.</span><span class="sxs-lookup"><span data-stu-id="3dad8-119">CNAME (or alias records) and A records both allow you to associate a domain name with a specific server (or service in this case,) however they work differently.</span></span> <span data-ttu-id="3dad8-120">Quando você usa registros com serviços de nuvem do Azure, precisa fazer algumas considerações específicas antes de decidir qual deles usar.</span><span class="sxs-lookup"><span data-stu-id="3dad8-120">There are also some specific considerations when using A records with Azure Cloud services that you should consider before deciding which to use.</span></span>

### <a name="cname-or-alias-record"></a><span data-ttu-id="3dad8-121">Registro CNAME ou de alias</span><span class="sxs-lookup"><span data-stu-id="3dad8-121">CNAME or Alias record</span></span>
<span data-ttu-id="3dad8-122">Um registro CNAME mapeia um domínio *específico*, como **contoso.com** ou **www.contoso.com**, para um nome de domínio geral.</span><span class="sxs-lookup"><span data-stu-id="3dad8-122">A CNAME record maps a *specific* domain, such as **contoso.com** or **www.contoso.com**, to a canonical domain name.</span></span> <span data-ttu-id="3dad8-123">Neste caso, o nome de domínio geral é o nome de domínio **[myapp].cloudapp.net** do seu aplicativo hospedado no Azure.</span><span class="sxs-lookup"><span data-stu-id="3dad8-123">In this case, the canonical domain name is the **[myapp].cloudapp.net** domain name of your Azure hosted application.</span></span> <span data-ttu-id="3dad8-124">Uma vez criado, o CNAME cria um alias para **[myapp].cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="3dad8-124">Once created, the CNAME creates an alias for the **[myapp].cloudapp.net**.</span></span> <span data-ttu-id="3dad8-125">A entrada CNAME determinará o endereço IP do seu serviço **[myapp].cloudapp.net** automaticamente, portanto, se o endereço IP do serviço de nuvem for alterado, você não precisará tomar nenhuma ação.</span><span class="sxs-lookup"><span data-stu-id="3dad8-125">The CNAME entry will resolve to the IP address of your **[myapp].cloudapp.net** service automatically, so if the IP address of the cloud service changes, you do not have to take any action.</span></span>

> [!NOTE]
> <span data-ttu-id="3dad8-126">Alguns registradores de domínio só permitem mapear subdomínios ao usar um registro CNAME, como www.contoso.com, e não nomes de raiz, como contoso.com. Para obter mais informações sobre os registros CNAME, consulte a documentação fornecida por seu registrador, [a entrada da Wikipédia sobre o registro CNAME](http://en.wikipedia.org/wiki/CNAME_record) ou o documento [Nomes de Domínio IETF - Implementação e Especificação](http://tools.ietf.org/html/rfc1035).</span><span class="sxs-lookup"><span data-stu-id="3dad8-126">Some domain registrars only allow you to map subdomains when using a CNAME record, such as www.contoso.com, and not root names, such as contoso.com. For more information on CNAME records, see the documentation provided by your registrar, [the Wikipedia entry on CNAME record](http://en.wikipedia.org/wiki/CNAME_record), or the [IETF Domain Names - Implementation and Specification](http://tools.ietf.org/html/rfc1035) document.</span></span>
> 
> 

### <a name="a-record"></a><span data-ttu-id="3dad8-127">Registro A</span><span class="sxs-lookup"><span data-stu-id="3dad8-127">A record</span></span>
<span data-ttu-id="3dad8-128">Um registro A mapeia um domínio, como **contoso.com** ou **www.contoso.com** *ou um domínio curinga*, como **\*.contoso.com**, para um endereço IP.</span><span class="sxs-lookup"><span data-stu-id="3dad8-128">An A record maps a domain, such as **contoso.com** or **www.contoso.com**, *or a wildcard domain* such as **\*.contoso.com**, to an IP address.</span></span> <span data-ttu-id="3dad8-129">No caso de um serviço de nuvem do Azure, o IP virtual do serviço.</span><span class="sxs-lookup"><span data-stu-id="3dad8-129">In the case of an Azure Cloud Service, the virtual IP of the service.</span></span> <span data-ttu-id="3dad8-130">Portanto, o principal benefício de um registro A em relação ao registro CNAME é que você pode ter uma entrada que usa um caractere curinga, como \***.contoso.com**, que lidaria com as solicitações de vários subdomínios, como **mail.contoso.com**, **login.contoso.com** ou **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="3dad8-130">So the main benefit of an A record over a CNAME record is that you can have one entry that uses a wildcard, such as \***.contoso.com**, which would handle requests for multiple sub-domains such as **mail.contoso.com**, **login.contoso.com**, or **www.contso.com**.</span></span>

> [!NOTE]
> <span data-ttu-id="3dad8-131">Uma vez que um registro A é mapeado para um endereço IP estático, não é possível resolver automaticamente as alterações ao endereço IP do seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="3dad8-131">Since an A record is mapped to a static IP address, it cannot automatically resolve changes to the IP address of your Cloud Service.</span></span> <span data-ttu-id="3dad8-132">O endereço IP usado pelo seu serviço de nuvem é alocado na primeira vez que você implantar em um slot vazio (produção ou preparo.) Se você excluir a implantação para o slot, o endereço IP será liberado pelo Azure e quaisquer implantações futuras no slot poderão receber um novo endereço IP.</span><span class="sxs-lookup"><span data-stu-id="3dad8-132">The IP address used by your Cloud Service is allocated the first time you deploy to an empty slot (either production or staging.) If you delete the deployment for the slot, the IP address is released by Azure and any future deployments to the slot may be given a new IP address.</span></span>
> 
> <span data-ttu-id="3dad8-133">Convenientemente, o endereço IP do slot de uma determinada implantação (de produção ou de preparo) é mantido durante a troca entre implantações de preparo e de produção ou durante a execução de uma atualização in-loco de uma implantação existente.</span><span class="sxs-lookup"><span data-stu-id="3dad8-133">Conveniently, the IP address of a given deployment slot (production or staging) is persisted when swapping between staging and production deployments or performing an in-place upgrade of an existing deployment.</span></span> <span data-ttu-id="3dad8-134">Para saber mais sobre a execução dessas ações, consulte [Como gerenciar serviços de nuvem](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="3dad8-134">For more information on performing these actions, see [How to manage cloud services](cloud-services-how-to-manage.md).</span></span>
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="3dad8-135">Adicionar um registro CNAME para seu domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="3dad8-135">Add a CNAME record for your custom domain</span></span>
<span data-ttu-id="3dad8-136">Para criar um registro CNAME, você deve adicionar uma nova entrada na tabela DNS para seu domínio personalizado usando as ferramentas fornecidas pelo seu registrador.</span><span class="sxs-lookup"><span data-stu-id="3dad8-136">To create a CNAME record, you must add a new entry in the DNS table for your custom domain by using the tools provided by your registrar.</span></span> <span data-ttu-id="3dad8-137">Cada registrador tem um método semelhante, mas ligeiramente diferente para especificar um registro CNAME, mas os conceitos são os mesmos.</span><span class="sxs-lookup"><span data-stu-id="3dad8-137">Each registrar has a similar but slightly different method of specifying a CNAME record, but the concepts are the same.</span></span>

1. <span data-ttu-id="3dad8-138">Use um dos seguintes métodos para localizar o nome de domínio **.cloudapp.net** atribuído ao seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="3dad8-138">Use one of these methods to find the **.cloudapp.net** domain name assigned to your cloud service.</span></span>
   
   * <span data-ttu-id="3dad8-139">Faça logon no [portal clássico do Azure], selecione seu serviço de nuvem, selecione **Painel** e localize a entrada **URL do Site** na seção de **visualização rápida**.</span><span class="sxs-lookup"><span data-stu-id="3dad8-139">Login to the [Azure classic portal], select your cloud service, select **Dashboard**, and then find the **Site URL** entry in the **quick glance** section.</span></span>
     
       ![seção rapidamente mostrando a URL do site][csurl]
     
       <span data-ttu-id="3dad8-141">**OR**</span><span class="sxs-lookup"><span data-stu-id="3dad8-141">**OR**</span></span>  
   * <span data-ttu-id="3dad8-142">Instale e configure o [Azure Powershell](/powershell/azure/overview)e use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="3dad8-142">Install and configure [Azure Powershell](/powershell/azure/overview), and then use the following command:</span></span>
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     <span data-ttu-id="3dad8-143">Salve o nome de domínio usado na URL retornada por qualquer método, pois você precisará dele durante a criação de um registro CNAME.</span><span class="sxs-lookup"><span data-stu-id="3dad8-143">Save the domain name used in the URL returned by either method, as you will need it when creating a CNAME record.</span></span>
2. <span data-ttu-id="3dad8-144">Faça logon no site do registrador de DNS e acesse a página de gerenciamento de DNS.</span><span class="sxs-lookup"><span data-stu-id="3dad8-144">Log on to your DNS registrar's website and go to the page for managing DNS.</span></span> <span data-ttu-id="3dad8-145">Procure links ou áreas do site rotuladas como **Nome de Domínio**, **DNS** ou **Gerenciamento do Servidor de Nome**.</span><span class="sxs-lookup"><span data-stu-id="3dad8-145">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="3dad8-146">Agora, encontre onde você pode selecionar ou inserir registros CNAME.</span><span class="sxs-lookup"><span data-stu-id="3dad8-146">Now find where you can select or enter CNAME's.</span></span> <span data-ttu-id="3dad8-147">Você pode ter que selecionar o tipo de registro de uma lista suspensa ou acessar uma página de configurações avançadas.</span><span class="sxs-lookup"><span data-stu-id="3dad8-147">You may have to select the record type from a drop down, or go to an advanced settings page.</span></span> <span data-ttu-id="3dad8-148">Você deve procurar as palavras **CNAME**, **Alias** ou **Subdomínios**.</span><span class="sxs-lookup"><span data-stu-id="3dad8-148">You should look for the words **CNAME**, **Alias**, or **Subdomains**.</span></span>
4. <span data-ttu-id="3dad8-149">Você também deverá fornecer um alias do domínio ou subdomínio para CNAME, como **www** se quiser criar um alias para **www.customdomain.com**. Se você deseja criar um alias para o domínio raiz, ele pode estar listado como o símbolo '**@**' nas ferramentas de DNS do registrador.</span><span class="sxs-lookup"><span data-stu-id="3dad8-149">You must also provide the domain or subdomain alias for the CNAME, such as **www** if you want to create an alias for **www.customdomain.com**. If you want to create an alias for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="3dad8-150">Em seguida, você deve fornecer um nome do host canônico, que, neste caso, é o domínio **cloudapp.net** do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3dad8-150">Then, you must provide a canonical host name, which is your application's **cloudapp.net** domain in this case.</span></span>

<span data-ttu-id="3dad8-151">Por exemplo, o seguinte registro CNAME encaminha todo o tráfego de **www.contoso.com** para **contoso.cloudapp.net**, o nome de domínio personalizado do seu aplicativo implantado:</span><span class="sxs-lookup"><span data-stu-id="3dad8-151">For example, the following CNAME record forwards all traffic from **www.contoso.com** to **contoso.cloudapp.net**, the custom domain name of your deployed application:</span></span>

| <span data-ttu-id="3dad8-152">Alias/Nome do host/Subdomínio</span><span class="sxs-lookup"><span data-stu-id="3dad8-152">Alias/Host name/Subdomain</span></span> | <span data-ttu-id="3dad8-153">Domínio canônico</span><span class="sxs-lookup"><span data-stu-id="3dad8-153">Canonical domain</span></span> |
| --- | --- |
| <span data-ttu-id="3dad8-154">www</span><span class="sxs-lookup"><span data-stu-id="3dad8-154">www</span></span> |<span data-ttu-id="3dad8-155">contoso.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="3dad8-155">contoso.cloudapp.net</span></span> |

<span data-ttu-id="3dad8-156">Um visitante de **www.contoso.com** nunca verá o host verdadeiro (contoso.cloudapp.net) e, portanto, o processo de encaminhamento será invisível ao usuário final.</span><span class="sxs-lookup"><span data-stu-id="3dad8-156">A visitor of **www.contoso.com** will never see the true host (contoso.cloudapp.net), so the forwarding process is invisible to the end user.</span></span>

> [!NOTE]
> <span data-ttu-id="3dad8-157">O exemplo acima aplica-se somente ao tráfego no subdomínio **www** .</span><span class="sxs-lookup"><span data-stu-id="3dad8-157">The example above only applies to traffic at the **www** subdomain.</span></span> <span data-ttu-id="3dad8-158">Uma vez que não é possível usar caracteres curinga com registros CNAME, você deve criar um CNAME para cada domínio/subdomínio.</span><span class="sxs-lookup"><span data-stu-id="3dad8-158">Since you cannot use wildcards with CNAME records, you must create one CNAME for each domain/subdomain.</span></span> <span data-ttu-id="3dad8-159">Se você quiser direcionar o tráfego a partir dos subdomínios, como \*.contoso.com, para o endereço cloudapp.net, poderá configurar uma entrada **Redirecionamento da URL** ou **Encaminhamento da URL** em suas configurações DNS, ou criar um registro A.</span><span class="sxs-lookup"><span data-stu-id="3dad8-159">If you want to direct  traffic from subdomains, such as \*.contoso.com, to your cloudapp.net address, you can configure a **URL Redirect** or **URL Forward** entry in your DNS settings, or create an A record.</span></span>
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a><span data-ttu-id="3dad8-160">Adicionar um registro A ao seu domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="3dad8-160">Add an A record for your custom domain</span></span>
<span data-ttu-id="3dad8-161">Para criar um registro, primeiro você deve encontrar o endereço IP do seu serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="3dad8-161">To create an A record, you must first find the virtual IP address of your cloud service.</span></span> <span data-ttu-id="3dad8-162">Então, em seguida, adicione uma nova entrada na tabela DNS para seu domínio personalizado usando as ferramentas fornecidas pelo seu registrador.</span><span class="sxs-lookup"><span data-stu-id="3dad8-162">Then add a new entry in the DNS table for your custom domain by using the tools provided by your registrar.</span></span> <span data-ttu-id="3dad8-163">Cada registrador tem um método semelhante, mas ligeiramente diferente para especificar um registro A, mas os conceitos são os mesmos.</span><span class="sxs-lookup"><span data-stu-id="3dad8-163">Each registrar has a similar but slightly different method of specifying an A record, but the concepts are the same.</span></span>

1. <span data-ttu-id="3dad8-164">Use um dos seguintes métodos para obter o endereço IP do seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="3dad8-164">Use one of the following methods to get the IP address of your cloud service.</span></span>
   
   * <span data-ttu-id="3dad8-165">Faça logon no [portal clássico do Azure], selecione seu serviço de nuvem, selecione **Painel** e localize a entrada do **endereço IP Virtual Público (VIP)** na seção de **visualização rápida**.</span><span class="sxs-lookup"><span data-stu-id="3dad8-165">login to the [Azure classic portal], select your cloud service, select **Dashboard**, and then find the **Public Virtual IP (VIP) address** entry in the **quick glance** section.</span></span>
     
       ![seção rapidamente mostrando a VIP][vip]
     
       <span data-ttu-id="3dad8-167">**OR**</span><span class="sxs-lookup"><span data-stu-id="3dad8-167">**OR**</span></span>  
   * <span data-ttu-id="3dad8-168">Instale e configure o [Azure Powershell](/powershell/azure/overview)e use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="3dad8-168">Install and configure [Azure Powershell](/powershell/azure/overview), and then use the following command:</span></span>
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     <span data-ttu-id="3dad8-169">Se você tiver vários pontos de extremidade associados ao seu serviço de nuvem, você receberá várias linhas que contém o endereço IP, mas tudo deve exibir o mesmo endereço.</span><span class="sxs-lookup"><span data-stu-id="3dad8-169">If you have multiple endpoints associated with your cloud service, you will receive multiple lines containing the IP address, but all should display the same address.</span></span>
     
     <span data-ttu-id="3dad8-170">Salve o endereço IP, pois você precisará dele durante a criação de um registro.</span><span class="sxs-lookup"><span data-stu-id="3dad8-170">Save the IP address, as you will need it when creating an A record.</span></span>
2. <span data-ttu-id="3dad8-171">Faça logon no site do registrador de DNS e acesse a página de gerenciamento de DNS.</span><span class="sxs-lookup"><span data-stu-id="3dad8-171">Log on to your DNS registrar's website and go to the page for managing DNS.</span></span> <span data-ttu-id="3dad8-172">Procure links ou áreas do site rotuladas como **Nome de Domínio**, **DNS** ou **Gerenciamento do Servidor de Nome**.</span><span class="sxs-lookup"><span data-stu-id="3dad8-172">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="3dad8-173">Agora, encontre onde você pode selecionar ou inserir registros A.</span><span class="sxs-lookup"><span data-stu-id="3dad8-173">Now find where you can select or enter A record's.</span></span> <span data-ttu-id="3dad8-174">Você pode ter que selecionar o tipo de registro de uma lista suspensa ou acessar uma página de configurações avançadas.</span><span class="sxs-lookup"><span data-stu-id="3dad8-174">You may have to select the record type from a drop down, or go to an advanced settings page.</span></span>
4. <span data-ttu-id="3dad8-175">Selecione ou digite o domínio ou subdomínio que usará este registro A.</span><span class="sxs-lookup"><span data-stu-id="3dad8-175">Select or enter the domain or subdomain that will use this A record.</span></span> <span data-ttu-id="3dad8-176">Por exemplo, selecione **www** se você quiser criar um alias para **www.customdomain.com**. Se você quiser criar uma entrada curinga para todos os subdomínios, digite '__*__'.</span><span class="sxs-lookup"><span data-stu-id="3dad8-176">For example, select **www** if you want to create an alias for **www.customdomain.com**. If you want to create a wildcard entry for all subdomains, enter '__*__'.</span></span> <span data-ttu-id="3dad8-177">Isso cobrirá todos os subdomínios, como **mail.customdomain.com**, **login.customdomain.com** e **www.customdomain.com**.</span><span class="sxs-lookup"><span data-stu-id="3dad8-177">This will cover all sub-domains such as **mail.customdomain.com**, **login.customdomain.com**, and **www.customdomain.com**.</span></span>
   
    <span data-ttu-id="3dad8-178">Se você deseja criar um registro A para o domínio raiz, ele pode estar listado como o símbolo '**@**' nas ferramentas de DNS do registrador.</span><span class="sxs-lookup"><span data-stu-id="3dad8-178">If you want to create an A record for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="3dad8-179">Digite o endereço IP do seu serviço de nuvem no campo fornecido.</span><span class="sxs-lookup"><span data-stu-id="3dad8-179">Enter the IP address of your cloud service in the provided field.</span></span> <span data-ttu-id="3dad8-180">Isto associa a entrada de domínio usada no registro A com o endereço IP da sua implantação do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="3dad8-180">This associates the domain entry used in the A record with the IP address of your cloud service deployment.</span></span>

<span data-ttu-id="3dad8-181">Por exemplo, o seguinte registro A encaminha todo o tráfego de **contoso.com** para **137.135.70.239**, o endereço IP do seu aplicativo implantado:</span><span class="sxs-lookup"><span data-stu-id="3dad8-181">For example, the following A record forwards all traffic from **contoso.com** to **137.135.70.239**, the IP address of your deployed application:</span></span>

| <span data-ttu-id="3dad8-182">Nome do host/Subdomínio</span><span class="sxs-lookup"><span data-stu-id="3dad8-182">Host name/Subdomain</span></span> | <span data-ttu-id="3dad8-183">Endereço IP</span><span class="sxs-lookup"><span data-stu-id="3dad8-183">IP address</span></span> |
| --- | --- |
| @ |<span data-ttu-id="3dad8-184">137.135.70.239</span><span class="sxs-lookup"><span data-stu-id="3dad8-184">137.135.70.239</span></span> |

<span data-ttu-id="3dad8-185">Este exemplo demonstra como criar um registro A para o domínio raiz.</span><span class="sxs-lookup"><span data-stu-id="3dad8-185">This example demonstrates creating an A record for the root domain.</span></span> <span data-ttu-id="3dad8-186">Se você desejar criar uma entrada curinga para abranger todos os subdomínios, você digitaria '__*__' como o subdomínio.</span><span class="sxs-lookup"><span data-stu-id="3dad8-186">If you wish to create a wildcard entry to cover all subdomains, you would enter '__*__' as the subdomain.</span></span>

> [!WARNING]
> <span data-ttu-id="3dad8-187">Endereços IP no Azure são dinâmicos por padrão.</span><span class="sxs-lookup"><span data-stu-id="3dad8-187">IP addresses in Azure are dynamic by default.</span></span> <span data-ttu-id="3dad8-188">Você provavelmente desejará usar um [endereço IP reservado](../virtual-network/virtual-networks-reserved-public-ip.md) para garantir que seu endereço IP não seja alterado.</span><span class="sxs-lookup"><span data-stu-id="3dad8-188">You will probably want to use a [reserved IP address](../virtual-network/virtual-networks-reserved-public-ip.md) to ensure that your IP address does not change.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="3dad8-189">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3dad8-189">Next steps</span></span>
* [<span data-ttu-id="3dad8-190">Como gerenciar serviços de nuvem</span><span class="sxs-lookup"><span data-stu-id="3dad8-190">How to Manage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="3dad8-191">Como mapear o conteúdo da CDN para um domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="3dad8-191">How to Map CDN Content to a Custom Domain</span></span>](../cdn/cdn-map-content-to-custom-domain.md)
* <span data-ttu-id="3dad8-192">[Configuração geral do serviço de nuvem](cloud-services-how-to-configure.md).</span><span class="sxs-lookup"><span data-stu-id="3dad8-192">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="3dad8-193">Saiba como [implantar um serviço de nuvem](cloud-services-how-to-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="3dad8-193">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="3dad8-194">Configurar [certificados SSL](cloud-services-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="3dad8-194">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span></span>

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: http://msdn.microsoft.com/library/ee517253.aspx
[Create a CNAME record that associates the subdomain with the storage account]: #create-cname
[portal clássico do Azure]: https://manage.windowsazure.com
[Validate Custom Domain dialog box]: http://i.msdn.microsoft.com/dynimg/IC544437.jpg
[vip]: ./media/cloud-services-custom-domain-name/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name/csurl.png
