---
title: aaaCreate registros de DNS personalizados para um aplicativo web | Microsoft Docs
description: "Como o DNS de domínio personalizado toocreate registros para o aplicativo web usando o DNS do Azure."
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
ms.openlocfilehash: 070c808a55bab922eb624d99ae5c275d8eaa5aaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a><span data-ttu-id="3a9b9-103">Criar registros DNS para um aplicativo Web em um domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="3a9b9-103">Create DNS records for a web app in a custom domain</span></span>

<span data-ttu-id="3a9b9-104">Você pode usar o DNS do Azure toohost um domínio personalizado para seus aplicativos web.</span><span class="sxs-lookup"><span data-stu-id="3a9b9-104">You can use Azure DNS toohost a custom domain for your web apps.</span></span> <span data-ttu-id="3a9b9-105">Por exemplo, você está criando um aplicativo web do Azure e deseja que seus usuários tooaccess-lo pelo usando contoso.com ou www.contoso.com como um FQDN.</span><span class="sxs-lookup"><span data-stu-id="3a9b9-105">For example, you are creating an Azure web app and you want your users tooaccess it by either using contoso.com, or www.contoso.com as an FQDN.</span></span>

<span data-ttu-id="3a9b9-106">toodo isso, você tem dois registros de toocreate:</span><span class="sxs-lookup"><span data-stu-id="3a9b9-106">toodo this, you have toocreate two records:</span></span>

* <span data-ttu-id="3a9b9-107">Um toocontoso.com de apontador registro raiz "A"</span><span class="sxs-lookup"><span data-stu-id="3a9b9-107">A root "A" record pointing toocontoso.com</span></span>
* <span data-ttu-id="3a9b9-108">Um "" registro CNAME para o nome de www Olá que aponta toohello um registro</span><span class="sxs-lookup"><span data-stu-id="3a9b9-108">A "CNAME" record for hello www name that points toohello A record</span></span>

<span data-ttu-id="3a9b9-109">Tenha em mente que, se você criar um registro para um aplicativo web no Azure, Olá que um registro deve ser atualizado manualmente se Olá subjacente endereço IP para alterações de aplicativo web hello.</span><span class="sxs-lookup"><span data-stu-id="3a9b9-109">Keep in mind that if you create an A record for a web app in Azure, hello A record must be manually updated if hello underlying IP address for hello web app changes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3a9b9-110">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="3a9b9-110">Before you begin</span></span>

<span data-ttu-id="3a9b9-111">Antes de começar, deve primeiro criar uma zona DNS no DNS do Azure e delegar a zona Olá no seu registrador tooAzure DNS.</span><span class="sxs-lookup"><span data-stu-id="3a9b9-111">Before you begin, you must first create a DNS zone in Azure DNS, and delegate hello zone in your registrar tooAzure DNS.</span></span>

1. <span data-ttu-id="3a9b9-112">toocreate uma zona DNS, execute as etapas de saudação em [criar uma zona DNS](dns-getstarted-create-dnszone.md).</span><span class="sxs-lookup"><span data-stu-id="3a9b9-112">toocreate a DNS zone, follow hello steps in [Create a DNS zone](dns-getstarted-create-dnszone.md).</span></span>
2. <span data-ttu-id="3a9b9-113">toodelegate tooAzure seu DNS DNS, execute as etapas de saudação em [delegação de domínio DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="3a9b9-113">toodelegate your DNS tooAzure DNS, follow hello steps in [DNS domain delegation](dns-domain-delegation.md).</span></span>

<span data-ttu-id="3a9b9-114">Depois de criar uma zona e delegação de DNS de tooAzure, em seguida, você pode criar registros para seu domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="3a9b9-114">After creating a zone and delegating it tooAzure DNS, you can then create records for your custom domain.</span></span>

## <a name="1-create-an-a-record-for-your-custom-domain"></a><span data-ttu-id="3a9b9-115">1. Criar um registro A para seu domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="3a9b9-115">1. Create an A record for your custom domain</span></span>

<span data-ttu-id="3a9b9-116">Um registro é toomap usado um endereço IP do nome tooits.</span><span class="sxs-lookup"><span data-stu-id="3a9b9-116">An A record is used toomap a name tooits IP address.</span></span> <span data-ttu-id="3a9b9-117">Saudação de exemplo a seguir é atribuirá como um tooan de registro de um endereço IPv4:</span><span class="sxs-lookup"><span data-stu-id="3a9b9-117">In hello following example we will assign @ as an A record tooan IPv4 address:</span></span>

### <a name="step-1"></a><span data-ttu-id="3a9b9-118">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="3a9b9-118">Step 1</span></span>

<span data-ttu-id="3a9b9-119">Crie um registro e atribua tooa $rs variável</span><span class="sxs-lookup"><span data-stu-id="3a9b9-119">Create an A record and assign tooa variable $rs</span></span>

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a><span data-ttu-id="3a9b9-120">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="3a9b9-120">Step 2</span></span>

<span data-ttu-id="3a9b9-121">Adicionar conjunto de registros Olá IPv4 valor toohello criado anteriormente "@" usando a variável Olá $rs atribuído.</span><span class="sxs-lookup"><span data-stu-id="3a9b9-121">Add hello IPv4 value toohello previously created record set "@" using hello $rs variable assigned.</span></span> <span data-ttu-id="3a9b9-122">Olá valor IPv4 atribuído será o endereço IP de saudação para seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="3a9b9-122">hello IPv4 value assigned will be hello IP address for your web app.</span></span>

<span data-ttu-id="3a9b9-123">endereço IP de saudação toofind para um aplicativo web, siga as etapas de saudação em [configurar um nome de domínio personalizado no serviço de aplicativo do Azure](../app-service-web/app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="3a9b9-123">toofind hello IP address for a web app, follow hello steps in [Configure a custom domain name in Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a><span data-ttu-id="3a9b9-124">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="3a9b9-124">Step 3</span></span>

<span data-ttu-id="3a9b9-125">Confirme o conjunto de registros Olá alterações toohello.</span><span class="sxs-lookup"><span data-stu-id="3a9b9-125">Commit hello changes toohello record set.</span></span> <span data-ttu-id="3a9b9-126">Use `Set-AzureRMDnsRecordSet` Olá tooupload altera toohello tooAzure de conjunto de registros DNS:</span><span class="sxs-lookup"><span data-stu-id="3a9b9-126">Use `Set-AzureRMDnsRecordSet` tooupload hello changes toohello record set tooAzure DNS:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="3a9b9-127">2. Criar um registro CNAME para seu domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="3a9b9-127">2. Create a CNAME record for your custom domain</span></span>

<span data-ttu-id="3a9b9-128">Se o domínio já é gerenciado pelo DNS do Azure (consulte [delegação de domínio DNS](dns-domain-delegation.md), você pode usar Olá Olá exemplo toocreate um registro CNAME para contoso.azurewebsites.net a seguir.</span><span class="sxs-lookup"><span data-stu-id="3a9b9-128">If your domain is already managed by Azure DNS (see [DNS domain delegation](dns-domain-delegation.md), you can use hello following hello example toocreate a CNAME record for contoso.azurewebsites.net.</span></span>

### <a name="step-1"></a><span data-ttu-id="3a9b9-129">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="3a9b9-129">Step 1</span></span>

<span data-ttu-id="3a9b9-130">Abra o PowerShell e crie um novo conjunto de registros CNAME e atribua tooa $rs variável.</span><span class="sxs-lookup"><span data-stu-id="3a9b9-130">Open PowerShell and create a new CNAME record set and assign tooa variable $rs.</span></span> <span data-ttu-id="3a9b9-131">Este exemplo criará um tipo de conjunto de registros CNAME com um "tempo toolive" de 600 segundos na zona DNS denominado "contoso.com".</span><span class="sxs-lookup"><span data-stu-id="3a9b9-131">This example will create a record set type CNAME with a "time toolive" of 600 seconds in DNS zone named "contoso.com".</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="3a9b9-132">saudação de exemplo a seguir é a resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="3a9b9-132">hello following example is hello response.</span></span>

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

### <a name="step-2"></a><span data-ttu-id="3a9b9-133">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="3a9b9-133">Step 2</span></span>

<span data-ttu-id="3a9b9-134">Após Olá conjunto de registros CNAME é criado, você precisará toocreate um valor de alias que vai apontar toohello web app.</span><span class="sxs-lookup"><span data-stu-id="3a9b9-134">Once hello CNAME record set is created, you need toocreate an alias value which will point toohello web app.</span></span>

<span data-ttu-id="3a9b9-135">Usando Olá atribuídos previamente a variável "$rs" você pode usar o comando do PowerShell Olá abaixo alias de saudação toocreate para Olá web aplicativo contoso.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="3a9b9-135">Using hello previously assigned variable "$rs" you can use hello PowerShell command below toocreate hello alias for hello web app contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

<span data-ttu-id="3a9b9-136">saudação de exemplo a seguir é a resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="3a9b9-136">hello following example is hello response.</span></span>

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

### <a name="step-3"></a><span data-ttu-id="3a9b9-137">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="3a9b9-137">Step 3</span></span>

<span data-ttu-id="3a9b9-138">Confirmar alterações de saudação usando Olá `Set-AzureRMDnsRecordSet` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3a9b9-138">Commit hello changes using hello `Set-AzureRMDnsRecordSet` cmdlet:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="3a9b9-139">Você pode validar o registro de saudação foi criado corretamente consultando hello "www.contoso.com" usando nslookup, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="3a9b9-139">You can validate hello record was created correctly by querying hello "www.contoso.com" using nslookup, as shown below:</span></span>

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

## <a name="create-an-awverify-record-for-web-apps"></a><span data-ttu-id="3a9b9-140">Criar um registro "awverify" para aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="3a9b9-140">Create an "awverify" record for web apps</span></span>

<span data-ttu-id="3a9b9-141">Se você decidir toouse um registro a para seu aplicativo web, você deve percorrer um tooensure do processo de verificação é domínio personalizado próprio hello.</span><span class="sxs-lookup"><span data-stu-id="3a9b9-141">If you decide toouse an A record for your web app, you must go through a verification process tooensure you own hello custom domain.</span></span> <span data-ttu-id="3a9b9-142">Essa etapa de verificação é feita criando um registro CNAME especial chamado "awverify".</span><span class="sxs-lookup"><span data-stu-id="3a9b9-142">This verification step is done by creating a special CNAME record named "awverify".</span></span> <span data-ttu-id="3a9b9-143">Esta seção aplica-se somente os registros de tooA.</span><span class="sxs-lookup"><span data-stu-id="3a9b9-143">This section applies tooA records only.</span></span>

### <a name="step-1"></a><span data-ttu-id="3a9b9-144">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="3a9b9-144">Step 1</span></span>

<span data-ttu-id="3a9b9-145">Crie registro de "awverify" hello.</span><span class="sxs-lookup"><span data-stu-id="3a9b9-145">Create hello "awverify" record.</span></span> <span data-ttu-id="3a9b9-146">No exemplo hello abaixo, vamos criar registro de "aweverify" Olá para contoso.com tooverify propriedade para o domínio personalizado hello.</span><span class="sxs-lookup"><span data-stu-id="3a9b9-146">In hello example below, we will create hello "aweverify" record for contoso.com tooverify ownership for hello custom domain.</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="3a9b9-147">saudação de exemplo a seguir é a resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="3a9b9-147">hello following example is hello response.</span></span>

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

### <a name="step-2"></a><span data-ttu-id="3a9b9-148">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="3a9b9-148">Step 2</span></span>

<span data-ttu-id="3a9b9-149">Depois de criar o conjunto de registros "awverify" Olá, atribua o registro CNAME Olá alias definido.</span><span class="sxs-lookup"><span data-stu-id="3a9b9-149">Once hello record set "awverify" is created, assign hello CNAME record set alias.</span></span> <span data-ttu-id="3a9b9-150">O exemplo hello abaixo, podemos atribuirá Olá tooawverify.contoso.azurewebsites.net de alias de conjunto de registros de CNAMe.</span><span class="sxs-lookup"><span data-stu-id="3a9b9-150">In hello example below, we will assign hello CNAMe record set alias tooawverify.contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

<span data-ttu-id="3a9b9-151">saudação de exemplo a seguir é a resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="3a9b9-151">hello following example is hello response.</span></span>

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

### <a name="step-3"></a><span data-ttu-id="3a9b9-152">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="3a9b9-152">Step 3</span></span>

<span data-ttu-id="3a9b9-153">Confirmar alterações de saudação usando Olá `Set-AzureRMDnsRecordSet cmdlet`, conforme mostrado no comando de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="3a9b9-153">Commit hello changes using hello `Set-AzureRMDnsRecordSet cmdlet`, as shown in hello command below.</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a><span data-ttu-id="3a9b9-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3a9b9-154">Next steps</span></span>

<span data-ttu-id="3a9b9-155">Siga as etapas de saudação em [Configurando um nome de domínio personalizado para o serviço de aplicativo](../app-service-web/web-sites-custom-domain-name.md) tooconfigure seu aplicativo de web toouse um domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="3a9b9-155">Follow hello steps in [Configuring a custom domain name for App Service](../app-service-web/web-sites-custom-domain-name.md) tooconfigure your web app toouse a custom domain.</span></span>
