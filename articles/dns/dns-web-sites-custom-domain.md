---
title: Criar registros DNS personalizados para um aplicativo Web | Microsoft Docs
description: "Como criar registros DNS de domínio personalizado para o aplicativo Web usando o DNS do Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 6c16608c-4819-44e7-ab88-306cf4d6efe5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: b054a41ecd69ee1c802d8403fe4b25128f016e3c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a><span data-ttu-id="55422-103">Criar registros DNS para um aplicativo Web em um domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="55422-103">Create DNS records for a web app in a custom domain</span></span>

<span data-ttu-id="55422-104">Você pode usar o DNS do Azure para hospedar um domínio personalizado para seus aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="55422-104">You can use Azure DNS to host a custom domain for your web apps.</span></span> <span data-ttu-id="55422-105">Por exemplo, você está criando um aplicativo Web do Azure e quer que os usuários o acessem usando contoso.com ou www.contoso.com como FQDN.</span><span class="sxs-lookup"><span data-stu-id="55422-105">For example, you are creating an Azure web app and you want your users to access it by either using contoso.com, or www.contoso.com as an FQDN.</span></span>

<span data-ttu-id="55422-106">Para isso, você precisa criar dois registros:</span><span class="sxs-lookup"><span data-stu-id="55422-106">To do this, you have to create two records:</span></span>

* <span data-ttu-id="55422-107">Um registro "A" raiz que aponta para contoso.com</span><span class="sxs-lookup"><span data-stu-id="55422-107">A root "A" record pointing to contoso.com</span></span>
* <span data-ttu-id="55422-108">Um registro "CNAME" para o nome www que aponta para o registro A</span><span class="sxs-lookup"><span data-stu-id="55422-108">A "CNAME" record for the www name that points to the A record</span></span>

<span data-ttu-id="55422-109">Tenha em mente que, se você criar um registro A para um aplicativo Web no Azure, o registro A deve ser manualmente atualizado se o endereço IP subjacente para o aplicativo Web for alterado.</span><span class="sxs-lookup"><span data-stu-id="55422-109">Keep in mind that if you create an A record for a web app in Azure, the A record must be manually updated if the underlying IP address for the web app changes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="55422-110">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="55422-110">Before you begin</span></span>

<span data-ttu-id="55422-111">Antes de começar, primeiro você deve criar uma zona DNS no DNS do Azure e delegar a zona no registrador para o DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="55422-111">Before you begin, you must first create a DNS zone in Azure DNS, and delegate the zone in your registrar to Azure DNS.</span></span>

1. <span data-ttu-id="55422-112">Para criar uma zona DNS, siga as etapas em [Criar uma zona DNS](dns-getstarted-create-dnszone.md).</span><span class="sxs-lookup"><span data-stu-id="55422-112">To create a DNS zone, follow the steps in [Create a DNS zone](dns-getstarted-create-dnszone.md).</span></span>
2. <span data-ttu-id="55422-113">Para delegar o DNS ao DNS do Azure, siga as etapas em [Delegação de domínio DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="55422-113">To delegate your DNS to Azure DNS, follow the steps in [DNS domain delegation](dns-domain-delegation.md).</span></span>

<span data-ttu-id="55422-114">Após criar uma zona e delegá-la ao DNS do Azure, você pode criar registros para seu domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="55422-114">After creating a zone and delegating it to Azure DNS, you can then create records for your custom domain.</span></span>

## <a name="1-create-an-a-record-for-your-custom-domain"></a><span data-ttu-id="55422-115">1. Criar um registro A para seu domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="55422-115">1. Create an A record for your custom domain</span></span>

<span data-ttu-id="55422-116">Um registro A é usado para mapear um nome para seu endereço IP.</span><span class="sxs-lookup"><span data-stu-id="55422-116">An A record is used to map a name to its IP address.</span></span> <span data-ttu-id="55422-117">No exemplo a seguir, atribuiremos @ como um registro A para um endereço IPv4:</span><span class="sxs-lookup"><span data-stu-id="55422-117">In the following example we will assign @ as an A record to an IPv4 address:</span></span>

### <a name="step-1"></a><span data-ttu-id="55422-118">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="55422-118">Step 1</span></span>

<span data-ttu-id="55422-119">Crie um registro A e atribuir a uma variável $rs</span><span class="sxs-lookup"><span data-stu-id="55422-119">Create an A record and assign to a variable $rs</span></span>

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a><span data-ttu-id="55422-120">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="55422-120">Step 2</span></span>

<span data-ttu-id="55422-121">Adicione o valor IPv4 ao conjunto de registros criado anteriormente "@" usando a variável $rs atribuída.</span><span class="sxs-lookup"><span data-stu-id="55422-121">Add the IPv4 value to the previously created record set "@" using the $rs variable assigned.</span></span> <span data-ttu-id="55422-122">O valor IPv4 atribuído será o endereço IP do seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="55422-122">The IPv4 value assigned will be the IP address for your web app.</span></span>

<span data-ttu-id="55422-123">Para localizar o endereço IP de um aplicativo Web, siga as etapas em [Configurar um nome de domínio personalizado no serviço de aplicativo do Azure](../app-service-web/app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="55422-123">To find the IP address for a web app, follow the steps in [Configure a custom domain name in Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a><span data-ttu-id="55422-124">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="55422-124">Step 3</span></span>

<span data-ttu-id="55422-125">Confirme as alterações no conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="55422-125">Commit the changes to the record set.</span></span> <span data-ttu-id="55422-126">Use `Set-AzureRMDnsRecordSet` para carregar as alterações no conjunto de registros para o DNS do Azure:</span><span class="sxs-lookup"><span data-stu-id="55422-126">Use `Set-AzureRMDnsRecordSet` to upload the changes to the record set to Azure DNS:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="55422-127">2. Criar um registro CNAME para seu domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="55422-127">2. Create a CNAME record for your custom domain</span></span>

<span data-ttu-id="55422-128">Se o domínio já é gerenciado pelo DNS do Azure (confira [Delegação de domínio ao DNS](dns-domain-delegation.md)), você pode usar o exemplo a seguir para criar um registro CNAME para contoso.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="55422-128">If your domain is already managed by Azure DNS (see [DNS domain delegation](dns-domain-delegation.md), you can use the following the example to create a CNAME record for contoso.azurewebsites.net.</span></span>

### <a name="step-1"></a><span data-ttu-id="55422-129">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="55422-129">Step 1</span></span>

<span data-ttu-id="55422-130">Abra o PowerShell, crie um novo conjunto de registros CNAME e atribua-o a uma variável $rs.</span><span class="sxs-lookup"><span data-stu-id="55422-130">Open PowerShell and create a new CNAME record set and assign to a variable $rs.</span></span> <span data-ttu-id="55422-131">Este exemplo cria um tipo de conjunto de registros CNAME com uma "vida útil" de 600 segundos na zona DNS denominada "contoso.com".</span><span class="sxs-lookup"><span data-stu-id="55422-131">This example will create a record set type CNAME with a "time to live" of 600 seconds in DNS zone named "contoso.com".</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="55422-132">O exemplo a seguir é a resposta.</span><span class="sxs-lookup"><span data-stu-id="55422-132">The following example is the response.</span></span>

```
Name              : www
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a><span data-ttu-id="55422-133">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="55422-133">Step 2</span></span>

<span data-ttu-id="55422-134">Depois de criar o conjunto de registros CNAME, você precisa criar um valor de alias que apontará para o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="55422-134">Once the CNAME record set is created, you need to create an alias value which will point to the web app.</span></span>

<span data-ttu-id="55422-135">Usando a variável "$rs" atribuída anteriormente, você pode usar o comando PowerShell a seguir para criar o alias para o aplicativo Web contoso.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="55422-135">Using the previously assigned variable "$rs" you can use the PowerShell command below to create the alias for the web app contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

<span data-ttu-id="55422-136">O exemplo a seguir é a resposta.</span><span class="sxs-lookup"><span data-stu-id="55422-136">The following example is the response.</span></span>

```
    Name              : www
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a><span data-ttu-id="55422-137">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="55422-137">Step 3</span></span>

<span data-ttu-id="55422-138">Confirme as alterações usando o cmdlet `Set-AzureRMDnsRecordSet` :</span><span class="sxs-lookup"><span data-stu-id="55422-138">Commit the changes using the `Set-AzureRMDnsRecordSet` cmdlet:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="55422-139">Você pode validar se o registro foi criado corretamente consultando "www.contoso.com" usando o nslookup, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="55422-139">You can validate the record was created correctly by querying the "www.contoso.com" using nslookup, as shown below:</span></span>

```
PS C:\> nslookup
Default Server:  Default
Address:  192.168.0.1

> www.contoso.com
Server:  default server
Address:  192.168.0.1

Non-authoritative answer:
Name:    <instance of web app service>.cloudapp.net
Address:  <ip of web app service>
Aliases:  www.contoso.com
contoso.azurewebsites.net
<instance of web app service>.vip.azurewebsites.windows.net
```

## <a name="create-an-awverify-record-for-web-apps"></a><span data-ttu-id="55422-140">Criar um registro "awverify" para aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="55422-140">Create an "awverify" record for web apps</span></span>

<span data-ttu-id="55422-141">Se você decidir usar um registro A do seu aplicativo Web, deverá passar por um processo de verificação para garantir que você tem o domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="55422-141">If you decide to use an A record for your web app, you must go through a verification process to ensure you own the custom domain.</span></span> <span data-ttu-id="55422-142">Essa etapa de verificação é feita criando um registro CNAME especial chamado "awverify".</span><span class="sxs-lookup"><span data-stu-id="55422-142">This verification step is done by creating a special CNAME record named "awverify".</span></span> <span data-ttu-id="55422-143">Esta seção aplica-se somente a registros A.</span><span class="sxs-lookup"><span data-stu-id="55422-143">This section applies to A records only.</span></span>

### <a name="step-1"></a><span data-ttu-id="55422-144">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="55422-144">Step 1</span></span>

<span data-ttu-id="55422-145">Crie o registro "awverify".</span><span class="sxs-lookup"><span data-stu-id="55422-145">Create the "awverify" record.</span></span> <span data-ttu-id="55422-146">No exemplo a seguir, criaremos o registro "aweverify" para contoso.com verificar a propriedade do domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="55422-146">In the example below, we will create the "aweverify" record for contoso.com to verify ownership for the custom domain.</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="55422-147">O exemplo a seguir é a resposta.</span><span class="sxs-lookup"><span data-stu-id="55422-147">The following example is the response.</span></span>

```
Name              : awverify
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a><span data-ttu-id="55422-148">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="55422-148">Step 2</span></span>

<span data-ttu-id="55422-149">Após criar o conjunto de registros "awverify", atribua o alias do conjunto de registros CNAME.</span><span class="sxs-lookup"><span data-stu-id="55422-149">Once the record set "awverify" is created, assign the CNAME record set alias.</span></span> <span data-ttu-id="55422-150">No exemplo a seguir, atribuiremos o alias do conjunto de registros CNAMe a awverify.contoso.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="55422-150">In the example below, we will assign the CNAMe record set alias to awverify.contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

<span data-ttu-id="55422-151">O exemplo a seguir é a resposta.</span><span class="sxs-lookup"><span data-stu-id="55422-151">The following example is the response.</span></span>

```
    Name              : awverify
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {awverify.contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a><span data-ttu-id="55422-152">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="55422-152">Step 3</span></span>

<span data-ttu-id="55422-153">Confirme as alterações usando o `Set-AzureRMDnsRecordSet cmdlet`, conforme mostrado no comando abaixo.</span><span class="sxs-lookup"><span data-stu-id="55422-153">Commit the changes using the `Set-AzureRMDnsRecordSet cmdlet`, as shown in the command below.</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a><span data-ttu-id="55422-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="55422-154">Next steps</span></span>

<span data-ttu-id="55422-155">Siga as etapas em [Configurar um nome de domínio personalizado para o serviço de aplicativo](../app-service-web/web-sites-custom-domain-name.md) para configurar o aplicativo Web para usar um domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="55422-155">Follow the steps in [Configuring a custom domain name for App Service](../app-service-web/web-sites-custom-domain-name.md) to configure your web app to use a custom domain.</span></span>
