---
title: "gerenciamento de serviços de saudação do aaaHow toouse API (Python) - guia do recurso"
description: "Saiba como tooprogrammatically executar tarefas comuns de gerenciamento de serviço do Python."
services: cloud-services
documentationcenter: python
author: lmazuel
manager: wpickett
editor: 
ms.assetid: 61538ec0-1536-4a7e-ae89-95967fe35d73
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/30/2017
ms.author: lmazuel
ms.openlocfilehash: b59622203470e1586484cec4033515edb39ca4d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-management-from-python"></a><span data-ttu-id="fbfe2-103">Como toouse gerenciamento de serviço do Python</span><span class="sxs-lookup"><span data-stu-id="fbfe2-103">How toouse Service Management from Python</span></span>
<span data-ttu-id="fbfe2-104">Este guia mostra como tooprogrammatically executar tarefas comuns de gerenciamento de serviço do Python.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-104">This guide shows you how tooprogrammatically perform common service management tasks from Python.</span></span> <span data-ttu-id="fbfe2-105">Olá **ServiceManagementService** classe Olá [Azure SDK para Python](https://github.com/Azure/azure-sdk-for-python) oferece suporte a acesso programático toomuch Olá relacionadas ao gerenciamento da funcionalidade do serviço que está disponível no hello [Portal clássico do azure] [ management-portal] (como **criar, atualizar e excluir serviços de nuvem e máquinas virtuais, serviços de gerenciamento de dados e implantações**).</span><span class="sxs-lookup"><span data-stu-id="fbfe2-105">hello **ServiceManagementService** class in hello [Azure SDK for Python](https://github.com/Azure/azure-sdk-for-python) supports programmatic access toomuch of hello service management-related functionality that is available in hello [Azure classic portal][management-portal] (such as **creating, updating, and deleting cloud services, deployments, data management services, and virtual machines**).</span></span> <span data-ttu-id="fbfe2-106">Essa funcionalidade pode ser útil na criação de aplicativos que precisam de gerenciamento de acesso programático à tooservice.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-106">This functionality can be useful in building applications that need programmatic access tooservice management.</span></span>

## <span data-ttu-id="fbfe2-107"><a name="WhatIs"> </a>O que é gerenciamento de serviços</span><span class="sxs-lookup"><span data-stu-id="fbfe2-107"><a name="WhatIs"> </a>What is Service Management</span></span>
<span data-ttu-id="fbfe2-108">Olá API de gerenciamento de serviço fornece acesso programático toomuch da funcionalidade de gerenciamento de serviços de saudação disponível por meio de saudação [portal clássico do Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="fbfe2-108">hello Service Management API provides programmatic access toomuch of hello service management functionality available through hello [Azure classic portal][management-portal].</span></span> <span data-ttu-id="fbfe2-109">Hello Azure SDK para Python permite toomanage seus serviços de nuvem e contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-109">hello Azure SDK for Python allows you toomanage your cloud services and storage accounts.</span></span>

<span data-ttu-id="fbfe2-110">API de gerenciamento de serviços do toouse Olá, é necessário muito[criar uma conta do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fbfe2-110">toouse hello Service Management API, you need too[create an Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <span data-ttu-id="fbfe2-111"><a name="Concepts"> </a>Conceitos</span><span class="sxs-lookup"><span data-stu-id="fbfe2-111"><a name="Concepts"> </a>Concepts</span></span>
<span data-ttu-id="fbfe2-112">Hello Azure SDK para Python encapsula Olá [API de gerenciamento de serviços do Azure][svc-mgmt-rest-api], que é uma API REST.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-112">hello Azure SDK for Python wraps hello [Azure Service Management API][svc-mgmt-rest-api], which is a REST API.</span></span> <span data-ttu-id="fbfe2-113">Todas as operações da API são executadas por meio do SSL e mutuamente autenticadas usando certificados X.509 v3.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-113">All API operations are performed over SSL and mutually authenticated using X.509 v3 certificates.</span></span> <span data-ttu-id="fbfe2-114">serviço de gerenciamento de saudação pode ser acessado de dentro de um serviço em execução no Azure, ou diretamente na Internet de saudação de qualquer aplicativo que possa enviar uma solicitação HTTPS e receber uma resposta de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-114">hello management service may be accessed from within a service running in Azure, or directly over hello Internet from any application that can send an HTTPS request and receive an HTTPS response.</span></span>

## <span data-ttu-id="fbfe2-115"><a name="Installation"> </a>Instalação</span><span class="sxs-lookup"><span data-stu-id="fbfe2-115"><a name="Installation"> </a>Installation</span></span>
<span data-ttu-id="fbfe2-116">Todos os recursos de saudação descritos neste artigo estão disponíveis em Olá `azure-servicemanagement-legacy` pacote, que pode ser instalado usando o pip.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-116">All hello features described in this article are available in hello `azure-servicemanagement-legacy` package, which you can install using pip.</span></span> <span data-ttu-id="fbfe2-117">Para obter mais informações sobre a instalação (por exemplo, se você for novo tooPython), consulte este artigo: [instalando Python e hello SDK do Azure](../python-how-to-install.md)</span><span class="sxs-lookup"><span data-stu-id="fbfe2-117">For more information about installation (for example, if you are new tooPython), see this article: [Installing Python and hello Azure SDK](../python-how-to-install.md)</span></span>

## <span data-ttu-id="fbfe2-118"><a name="Connect"></a>Como: conectar-se gerenciamento tooservice</span><span class="sxs-lookup"><span data-stu-id="fbfe2-118"><a name="Connect"> </a>How to: Connect tooservice management</span></span>
<span data-ttu-id="fbfe2-119">ponto de extremidade de tooconnect toohello gerenciamento de serviço, você precisa sua ID de assinatura do Azure e um certificado de gerenciamento válido.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-119">tooconnect toohello Service Management endpoint, you need your Azure subscription ID and a valid management certificate.</span></span> <span data-ttu-id="fbfe2-120">Você pode obter sua ID de assinatura por meio de saudação [portal clássico do Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="fbfe2-120">You can obtain your subscription ID through hello [Azure classic portal][management-portal].</span></span>

> [!NOTE]
> <span data-ttu-id="fbfe2-121">Agora é possível toouse certificados criados com OpenSSL quando em execução no Windows.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-121">It is now possible toouse certificates created with OpenSSL when running on Windows.</span></span>  <span data-ttu-id="fbfe2-122">Isso requer o Python 2.7.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-122">It requires Python 2.7.4 or later.</span></span> <span data-ttu-id="fbfe2-123">É recomendável usuários toouse OpenSSL em vez de. pfx, já que o suporte para o. pfx certificados provavelmente serão removidos no futuro hello.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-123">We recommend users toouse OpenSSL instead of .pfx, since support for .pfx certificates will likely be removed in hello future.</span></span>
>
>

### <a name="management-certificates-on-windowsmaclinux-openssl"></a><span data-ttu-id="fbfe2-124">Certificados de gerenciamento no Windows/Mac/Linux (OpenSSL)</span><span class="sxs-lookup"><span data-stu-id="fbfe2-124">Management certificates on Windows/Mac/Linux (OpenSSL)</span></span>
<span data-ttu-id="fbfe2-125">Você pode usar [OpenSSL](http://www.openssl.org/) toocreate seu certificado de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-125">You can use [OpenSSL](http://www.openssl.org/) toocreate your management certificate.</span></span>  <span data-ttu-id="fbfe2-126">Você precisa realmente toocreate dois certificados, um servidor de saudação (uma `.cer` arquivo) e outro para o cliente da saudação (um `.pem` arquivo).</span><span class="sxs-lookup"><span data-stu-id="fbfe2-126">You actually need toocreate two certificates, one for hello server (a `.cer` file) and one for hello client (a `.pem` file).</span></span> <span data-ttu-id="fbfe2-127">Olá toocreate `.pem` de arquivos, execute:</span><span class="sxs-lookup"><span data-stu-id="fbfe2-127">toocreate hello `.pem` file, execute:</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="fbfe2-128">Olá toocreate `.cer` do certificado, execute:</span><span class="sxs-lookup"><span data-stu-id="fbfe2-128">toocreate hello `.cer` certificate, execute:</span></span>

    openssl x509 -inform pem -in mycert.pem -outform der -out mycert.cer

<span data-ttu-id="fbfe2-129">Para saber mais sobre certificados do Azure, confira [Visão geral dos Certificados de Serviços de Nuvem do Azure](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="fbfe2-129">For more information about Azure certificates, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="fbfe2-130">Para obter uma descrição completa dos parâmetros do OpenSSL, consulte a documentação de saudação em [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span><span class="sxs-lookup"><span data-stu-id="fbfe2-130">For a complete description of OpenSSL parameters, see hello documentation at [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span></span>

<span data-ttu-id="fbfe2-131">Depois de criar esses arquivos, você precisa Olá tooupload `.cer` tooAzure por meio de ação do hello "Carregar" do guia de "Configurações" hello de saudação do arquivo [portal clássico do Azure][management-portal], e você precisa toomake Anote onde você salvou Olá `.pem` arquivo.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-131">After you have created these files, you need tooupload hello `.cer` file tooAzure via hello "Upload" action of hello "Settings" tab of hello [Azure classic portal][management-portal], and you need toomake note of where you saved hello `.pem` file.</span></span>

<span data-ttu-id="fbfe2-132">Depois de obter sua ID de assinatura, um certificado criado e carregado Olá `.cer` tooAzure de arquivo, você pode conectar o ponto de extremidade de gerenciamento do Azure toohello, passando a id da assinatura hello e Olá caminho toohello `.pem` arquivo muito**ServiceManagementService**:</span><span class="sxs-lookup"><span data-stu-id="fbfe2-132">After you have obtained your subscription ID, created a certificate, and uploaded hello `.cer` file tooAzure, you can connect toohello Azure management endpoint by passing hello subscription id and hello path toohello `.pem` file too**ServiceManagementService**:</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = '<path_to_.pem_certificate>'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="fbfe2-133">Em Olá anterior como exemplo, `sms` é um **ServiceManagementService** objeto.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-133">In hello preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="fbfe2-134">Olá **ServiceManagementService** classe é Olá classe primária usada toomanage serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-134">hello **ServiceManagementService** class is hello primary class used toomanage Azure services.</span></span>

### <a name="management-certificates-on-windows-makecert"></a><span data-ttu-id="fbfe2-135">Certificados de gerenciamento no Windows (MakeCert)</span><span class="sxs-lookup"><span data-stu-id="fbfe2-135">Management certificates on Windows (MakeCert)</span></span>
<span data-ttu-id="fbfe2-136">Você pode criar um certificado de gerenciamento autoassinado em seu computador usando `makecert.exe`.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-136">You can create a self-signed management certificate on your machine using `makecert.exe`.</span></span>  <span data-ttu-id="fbfe2-137">Abra um **prompt de comando do Visual Studio** como um **administrador** e usar Olá comando a seguir, substituindo *AzureCertificate* com o nome do certificado Olá você gostaria que toouse.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-137">Open a **Visual Studio command prompt** as an **administrator** and use hello following command, replacing *AzureCertificate* with hello certificate name you would like toouse.</span></span>

    makecert -sky exchange -r -n "CN=AzureCertificate" -pe -a sha1 -len 2048 -ss My "AzureCertificate.cer"

<span data-ttu-id="fbfe2-138">comando Olá cria Olá `.cer` de arquivo e instala-o no hello **pessoal** repositório de certificados.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-138">hello command creates hello `.cer` file, and installs it in hello **Personal** certificate store.</span></span> <span data-ttu-id="fbfe2-139">Para obter mais informações, confira a [Visão geral sobre certificados para os Serviços de Nuvem do Azure](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="fbfe2-139">For more information, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span>

<span data-ttu-id="fbfe2-140">Depois de criar o certificado de saudação, você precisa Olá tooupload `.cer` tooAzure por meio de ação do hello "Carregar" do guia de "Configurações" hello de saudação do arquivo [portal clássico do Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="fbfe2-140">After you have created hello certificate, you need tooupload hello `.cer` file tooAzure via hello "Upload" action of hello "Settings" tab of hello [Azure classic portal][management-portal].</span></span>

<span data-ttu-id="fbfe2-141">Depois de obter sua ID de assinatura, um certificado criado e carregado Olá `.cer` tooAzure de arquivo, você pode conectar o ponto de extremidade de gerenciamento do Azure toohello, passando a id da assinatura hello e local de saudação do certificado de saudação em seu **Pessoal** repositório de certificados muito**ServiceManagementService** (novamente, substitua *AzureCertificate* com nome de saudação do certificado):</span><span class="sxs-lookup"><span data-stu-id="fbfe2-141">After you have obtained your subscription ID, created a certificate, and uploaded hello `.cer` file tooAzure, you can connect toohello Azure management endpoint by passing hello subscription id and hello location of hello certificate in your **Personal** certificate store too**ServiceManagementService** (again, replace *AzureCertificate* with hello name of your certificate):</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = 'CURRENT_USER\\my\\AzureCertificate'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="fbfe2-142">Em Olá anterior como exemplo, `sms` é um **ServiceManagementService** objeto.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-142">In hello preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="fbfe2-143">Olá **ServiceManagementService** classe é Olá classe primária usada toomanage serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-143">hello **ServiceManagementService** class is hello primary class used toomanage Azure services.</span></span>

## <span data-ttu-id="fbfe2-144"><a name="ListAvailableLocations"> </a>Como listar os locais disponíveis</span><span class="sxs-lookup"><span data-stu-id="fbfe2-144"><a name="ListAvailableLocations"> </a>How to: List available locations</span></span>
<span data-ttu-id="fbfe2-145">locais de saudação toolist que estão disponíveis para hospedar os serviços, use Olá **lista\_locais** método:</span><span class="sxs-lookup"><span data-stu-id="fbfe2-145">toolist hello locations that are available for hosting services, use hello **list\_locations** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_locations()
    for location in result:
        print(location.name)

<span data-ttu-id="fbfe2-146">Quando você criar um serviço de nuvem ou o serviço de armazenamento é necessário tooprovide um local válido.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-146">When you create a cloud service or storage service you need tooprovide a valid location.</span></span> <span data-ttu-id="fbfe2-147">Olá **lista\_locais** método sempre retorna uma lista de locais disponíveis no momento da saudação atualizada.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-147">hello **list\_locations** method always returns an up-to-date list of hello currently available locations.</span></span> <span data-ttu-id="fbfe2-148">Redação deste artigo, locais de saudação disponíveis são:</span><span class="sxs-lookup"><span data-stu-id="fbfe2-148">As of this writing, hello available locations are:</span></span>

* <span data-ttu-id="fbfe2-149">Europa Ocidental</span><span class="sxs-lookup"><span data-stu-id="fbfe2-149">West Europe</span></span>
* <span data-ttu-id="fbfe2-150">Norte da Europa</span><span class="sxs-lookup"><span data-stu-id="fbfe2-150">North Europe</span></span>
* <span data-ttu-id="fbfe2-151">Sudeste Asiático</span><span class="sxs-lookup"><span data-stu-id="fbfe2-151">Southeast Asia</span></span>
* <span data-ttu-id="fbfe2-152">Ásia Oriental</span><span class="sxs-lookup"><span data-stu-id="fbfe2-152">East Asia</span></span>
* <span data-ttu-id="fbfe2-153">Centro dos EUA</span><span class="sxs-lookup"><span data-stu-id="fbfe2-153">Central US</span></span>
* <span data-ttu-id="fbfe2-154">Centro-Norte dos EUA</span><span class="sxs-lookup"><span data-stu-id="fbfe2-154">North Central US</span></span>
* <span data-ttu-id="fbfe2-155">Centro-Sul dos Estados Unidos</span><span class="sxs-lookup"><span data-stu-id="fbfe2-155">South Central US</span></span>
* <span data-ttu-id="fbfe2-156">Oeste dos EUA</span><span class="sxs-lookup"><span data-stu-id="fbfe2-156">West US</span></span>
* <span data-ttu-id="fbfe2-157">Leste dos EUA</span><span class="sxs-lookup"><span data-stu-id="fbfe2-157">East US</span></span>
* <span data-ttu-id="fbfe2-158">Leste do Japão</span><span class="sxs-lookup"><span data-stu-id="fbfe2-158">Japan East</span></span>
* <span data-ttu-id="fbfe2-159">Oeste do Japão</span><span class="sxs-lookup"><span data-stu-id="fbfe2-159">Japan West</span></span>
* <span data-ttu-id="fbfe2-160">Sul do Brasil</span><span class="sxs-lookup"><span data-stu-id="fbfe2-160">Brazil South</span></span>
* <span data-ttu-id="fbfe2-161">Leste da Austrália</span><span class="sxs-lookup"><span data-stu-id="fbfe2-161">Australia East</span></span>
* <span data-ttu-id="fbfe2-162">Sudeste da Austrália</span><span class="sxs-lookup"><span data-stu-id="fbfe2-162">Australia Southeast</span></span>

## <span data-ttu-id="fbfe2-163"><a name="CreateCloudService"> </a>Como criar um serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="fbfe2-163"><a name="CreateCloudService"> </a>How to: Create a cloud service</span></span>
<span data-ttu-id="fbfe2-164">Quando você cria um aplicativo e executá-lo no Azure, código de saudação e configuração junto são chamados de um Azure [serviço de nuvem] [ cloud service] (conhecido como um *serviço hospedado* no anterior Versões do Azure).</span><span class="sxs-lookup"><span data-stu-id="fbfe2-164">When you create an application and run it in Azure, hello code and configuration together are called an Azure [cloud service][cloud service] (known as a *hosted service* in earlier Azure releases).</span></span> <span data-ttu-id="fbfe2-165">Olá **criar\_hospedado\_service** método permite toocreate um novo serviço hospedado, fornecendo um nome de serviço hospedado (que deve ser exclusivo no Azure), um rótulo (toobase64 automaticamente codificado), um Descrição e um local.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-165">hello **create\_hosted\_service** method allows you toocreate a new hosted service by providing a hosted service name (which must be unique in Azure), a label (automatically encoded toobase64), a description, and a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myhostedservice'
    label = 'myhostedservice'
    desc = 'my hosted service'
    location = 'West US'

    sms.create_hosted_service(name, label, desc, location)

<span data-ttu-id="fbfe2-166">Você pode listar todos os serviços de saudação hospedado para sua assinatura com hello **lista\_hospedado\_serviços** método:</span><span class="sxs-lookup"><span data-stu-id="fbfe2-166">You can list all hello hosted services for your subscription with hello **list\_hosted\_services** method:</span></span>

    result = sms.list_hosted_services()

    for hosted_service in result:
        print('Service name: ' + hosted_service.service_name)
        print('Management URL: ' + hosted_service.url)
        print('Location: ' + hosted_service.hosted_service_properties.location)
        print('')

<span data-ttu-id="fbfe2-167">Se você quiser tooget informações sobre um serviço hospedado em particular, você pode fazer isso passando toohello de nome de serviço hospedada de saudação **obter\_hospedado\_service\_propriedades** método:</span><span class="sxs-lookup"><span data-stu-id="fbfe2-167">If you want tooget information about a particular hosted service, you can do so by passing hello hosted service name toohello **get\_hosted\_service\_properties** method:</span></span>

    hosted_service = sms.get_hosted_service_properties('myhostedservice')

    print('Service name: ' + hosted_service.service_name)
    print('Management URL: ' + hosted_service.url)
    print('Location: ' + hosted_service.hosted_service_properties.location)

<span data-ttu-id="fbfe2-168">Depois de criar um serviço de nuvem, você pode implantar o serviço de toohello de código com hello **criar\_implantação** método.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-168">After you have created a cloud service, you can deploy your code toohello service with hello **create\_deployment** method.</span></span>

## <span data-ttu-id="fbfe2-169"><a name="DeleteCloudService"> </a>Como excluir um serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="fbfe2-169"><a name="DeleteCloudService"> </a>How to: Delete a cloud service</span></span>
<span data-ttu-id="fbfe2-170">Você pode excluir um serviço de nuvem passando Olá serviço nome toohello **excluir\_hospedado\_service** método:</span><span class="sxs-lookup"><span data-stu-id="fbfe2-170">You can delete a cloud service by passing hello service name toohello **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service('myhostedservice')

<span data-ttu-id="fbfe2-171">Antes de excluir um serviço, todas as implantações de serviço Olá devem ser excluídas primeiro.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-171">Before you can delete a service, all deployments for hello service must first be deleted.</span></span> <span data-ttu-id="fbfe2-172">(Consulte [Como excluir uma implantação](#DeleteDeployment) para obter detalhes.)</span><span class="sxs-lookup"><span data-stu-id="fbfe2-172">(See [How to: Delete a deployment](#DeleteDeployment) for details.)</span></span>

## <span data-ttu-id="fbfe2-173"><a name="DeleteDeployment"> </a>Como excluir uma implantação</span><span class="sxs-lookup"><span data-stu-id="fbfe2-173"><a name="DeleteDeployment"> </a>How to: Delete a deployment</span></span>
<span data-ttu-id="fbfe2-174">toodelete uma implantação, use Olá **excluir\_implantação** método.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-174">toodelete a deployment, use hello **delete\_deployment** method.</span></span> <span data-ttu-id="fbfe2-175">Olá exemplo a seguir mostra como toodelete uma implantação denominada `v1`.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-175">hello following example shows how toodelete a deployment named `v1`.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment('myhostedservice', 'v1')

## <span data-ttu-id="fbfe2-176"><a name="CreateStorageService"> </a>Como criar um serviço de armazenamento</span><span class="sxs-lookup"><span data-stu-id="fbfe2-176"><a name="CreateStorageService"> </a>How to: Create a storage service</span></span>
<span data-ttu-id="fbfe2-177">Um [serviço de armazenamento](../storage/common/storage-create-storage-account.md) oferece acesso tooAzure [Blobs](../storage/blobs/storage-python-how-to-use-blob-storage.md), [tabelas](../cosmos-db/table-storage-how-to-use-python.md), e [filas](../storage/queues/storage-python-how-to-use-queue-storage.md).</span><span class="sxs-lookup"><span data-stu-id="fbfe2-177">A [storage service](../storage/common/storage-create-storage-account.md) gives you access tooAzure [Blobs](../storage/blobs/storage-python-how-to-use-blob-storage.md), [Tables](../cosmos-db/table-storage-how-to-use-python.md), and [Queues](../storage/queues/storage-python-how-to-use-queue-storage.md).</span></span> <span data-ttu-id="fbfe2-178">toocreate um serviço de armazenamento, é necessário um nome para o serviço de saudação (entre 3 e 24 caracteres minúsculos e exclusivo dentro do Azure), uma descrição, um rótulo (backup too100 caracteres, toobase64 automaticamente codificada) e um local.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-178">toocreate a storage service, you need a name for hello service (between 3 and 24 lowercase characters and unique within Azure), a description, a label (up too100 characters, automatically encoded toobase64), and a location.</span></span> <span data-ttu-id="fbfe2-179">saudação de exemplo a seguir mostra como toocreate um armazenamento de serviço especificando um local.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-179">hello following example shows how toocreate a storage service by specifying a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mystorageaccount'
    label = 'mystorageaccount'
    location = 'West US'
    desc = 'My storage account description.'

    result = sms.create_storage_account(name, desc, label, location=location)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

<span data-ttu-id="fbfe2-180">Observe que esse status de saudação do hello no Olá anterior exemplo **criar\_armazenamento\_conta** operação pode ser recuperada, passando o resultado de saudação retornado por **criar\_armazenamento \_conta** toohello **obter\_operação\_status** método.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-180">Note in hello preceding example that hello status of hello **create\_storage\_account** operation can be retrieved by passing hello result returned by **create\_storage\_account** toohello **get\_operation\_status** method.</span></span>  

<span data-ttu-id="fbfe2-181">Você pode listar suas contas de armazenamento e suas propriedades com hello **lista\_armazenamento\_contas** método:</span><span class="sxs-lookup"><span data-stu-id="fbfe2-181">You can list your storage accounts and their properties with hello **list\_storage\_accounts** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_storage_accounts()
    for account in result:
        print('Service name: ' + account.service_name)
        print('Location: ' + account.storage_service_properties.location)
        print('')

## <span data-ttu-id="fbfe2-182"><a name="DeleteStorageService"> </a>Como excluir um serviço de armazenamento</span><span class="sxs-lookup"><span data-stu-id="fbfe2-182"><a name="DeleteStorageService"> </a>How to: Delete a storage service</span></span>
<span data-ttu-id="fbfe2-183">Você pode excluir um serviço de armazenamento, passando toohello de nome de serviço de armazenamento de saudação **excluir\_armazenamento\_conta** método.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-183">You can delete a storage service by passing hello storage service name toohello **delete\_storage\_account** method.</span></span> <span data-ttu-id="fbfe2-184">A exclusão de um serviço de armazenamento exclui todos os dados armazenados no serviço de saudação (blobs, tabelas e filas).</span><span class="sxs-lookup"><span data-stu-id="fbfe2-184">Deleting a storage service deletes all data stored in hello service (blobs, tables, and queues).</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_storage_account('mystorageaccount')

## <span data-ttu-id="fbfe2-185"><a name="ListOperatingSystems"> </a>Como listar os sistemas operacionais disponíveis</span><span class="sxs-lookup"><span data-stu-id="fbfe2-185"><a name="ListOperatingSystems"> </a>How to: List available operating systems</span></span>
<span data-ttu-id="fbfe2-186">toolist Olá os sistemas operacionais que estão disponíveis para hospedar os serviços, usam Olá **lista\_operacional\_sistemas** método:</span><span class="sxs-lookup"><span data-stu-id="fbfe2-186">toolist hello operating systems that are available for hosting services, use hello **list\_operating\_systems** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_operating_systems()

    for os in result:
        print('OS: ' + os.label)
        print('Family: ' + os.family_label)
        print('Active: ' + str(os.is_active))

<span data-ttu-id="fbfe2-187">Como alternativa, você pode usar o hello **lista\_operacional\_sistema\_famílias** método, que agrupa os sistemas operacionais de saudação por família:</span><span class="sxs-lookup"><span data-stu-id="fbfe2-187">Alternatively, you can use hello **list\_operating\_system\_families** method, which groups hello operating systems by family:</span></span>

    result = sms.list_operating_system_families()

    for family in result:
        print('Family: ' + family.label)
        for os in family.operating_systems:
            if os.is_active:
                print('OS: ' + os.label)
                print('Version: ' + os.version)
        print('')

## <span data-ttu-id="fbfe2-188"><a name="CreateVMImage"> </a>Como criar uma imagem do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="fbfe2-188"><a name="CreateVMImage"> </a>How to: Create an operating system image</span></span>
<span data-ttu-id="fbfe2-189">tooadd um repositório de imagens de toohello de imagem de sistema operacional, use Olá **adicionar\_os\_imagem** método:</span><span class="sxs-lookup"><span data-stu-id="fbfe2-189">tooadd an operating system image toohello image repository, use hello **add\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mycentos'
    label = 'mycentos'
    os = 'Linux' # Linux or Windows
    media_link = 'url_to_storage_blob_for_source_image_vhd'

    result = sms.add_os_image(label, media_link, name, os)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

<span data-ttu-id="fbfe2-190">imagens do sistema operacional Olá toolist que estão disponíveis, use Olá **lista\_os\_imagens** método.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-190">toolist hello operating system images that are available, use hello **list\_os\_images** method.</span></span> <span data-ttu-id="fbfe2-191">Isso inclui todas as imagens de plataforma e imagens do usuário:</span><span class="sxs-lookup"><span data-stu-id="fbfe2-191">It includes all platform images and user images:</span></span>

    result = sms.list_os_images()

    for image in result:
        print('Name: ' + image.name)
        print('Label: ' + image.label)
        print('OS: ' + image.os)
        print('Category: ' + image.category)
        print('Description: ' + image.description)
        print('Location: ' + image.location)
        print('Media link: ' + image.media_link)
        print('')

## <span data-ttu-id="fbfe2-192"><a name="DeleteVMImage"> </a>Como excluir uma imagem do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="fbfe2-192"><a name="DeleteVMImage"> </a>How to: Delete an operating system image</span></span>
<span data-ttu-id="fbfe2-193">toodelete uma imagem do usuário, use Olá **excluir\_os\_imagem** método:</span><span class="sxs-lookup"><span data-stu-id="fbfe2-193">toodelete a user image, use hello **delete\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.delete_os_image('mycentos')

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

## <span data-ttu-id="fbfe2-194"><a name="CreateVM"> </a>Como criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="fbfe2-194"><a name="CreateVM"> </a>How to: Create a virtual machine</span></span>
<span data-ttu-id="fbfe2-195">toocreate uma máquina virtual, primeiro é necessário toocreate um [serviço de nuvem](#CreateCloudService).</span><span class="sxs-lookup"><span data-stu-id="fbfe2-195">toocreate a virtual machine, you first need toocreate a [cloud service](#CreateCloudService).</span></span>  <span data-ttu-id="fbfe2-196">Criar implantação da máquina virtual hello usando Olá **criar\_virtual\_máquina\_implantação** método:</span><span class="sxs-lookup"><span data-stu-id="fbfe2-196">Then create hello virtual machine deployment using hello **create\_virtual\_machine\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    # Name of an os image as returned by list_os_images
    image_name = 'OpenLogic__OpenLogic-CentOS-62-20120531-en-us-30GB.vhd'

    # Destination storage account container/blob where hello VM disk
    # will be created
    media_link = 'url_to_target_storage_blob_for_vm_hd'

    # Linux VM configuration, you can use WindowsConfigurationSet
    # for a Windows VM instead
    linux_config = LinuxConfigurationSet('myhostname', 'myuser', 'mypassword', True)

    os_hd = OSVirtualHardDisk(image_name, media_link)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=os_hd,
        role_size='Small')

## <span data-ttu-id="fbfe2-197"><a name="DeleteVM"> </a>Como excluir uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="fbfe2-197"><a name="DeleteVM"> </a>How to: Delete a virtual machine</span></span>
<span data-ttu-id="fbfe2-198">toodelete uma máquina virtual, você primeiro excluir Olá implantação usando Olá **excluir\_implantação** método:</span><span class="sxs-lookup"><span data-stu-id="fbfe2-198">toodelete a virtual machine, you first delete hello deployment using hello **delete\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment(service_name='myvm',
        deployment_name='myvm')

<span data-ttu-id="fbfe2-199">serviço de nuvem Olá pode ser excluído usando Olá **excluir\_hospedado\_service** método:</span><span class="sxs-lookup"><span data-stu-id="fbfe2-199">hello cloud service can then be deleted using hello **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service(service_name='myvm')

## <a name="how-to-create-a-virtual-machine-from-a-captured-virtual-machine-image"></a><span data-ttu-id="fbfe2-200">Como criar uma máquina virtual por meio de uma imagem de máquina virtual capturada</span><span class="sxs-lookup"><span data-stu-id="fbfe2-200">How To: Create a Virtual Machine from a Captured Virtual Machine Image</span></span>
<span data-ttu-id="fbfe2-201">toocapture uma imagem de VM, você primeiro chamar hello **capturar\_vm\_imagem** método:</span><span class="sxs-lookup"><span data-stu-id="fbfe2-201">toocapture a VM image, you first call hello **capture\_vm\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    # replace hello below three parameters with actual values
    hosted_service_name = 'hs1'
    deployment_name = 'dep1'
    vm_name = 'vm1'

    image_name = vm_name + 'image'
    image = CaptureRoleAsVMImage    ('Specialized',
        image_name,
        image_name + 'label',
        image_name + 'description',
        'english',
        'mygroup')

    result = sms.capture_vm_image(
            hosted_service_name,
            deployment_name,
            vm_name,
            image
        )

<span data-ttu-id="fbfe2-202">Em seguida, toomake-se de que você capturou com êxito a imagem hello, use Olá **lista\_vm\_imagens** api e certifique-se de sua imagem é exibida nos resultados da saudação:</span><span class="sxs-lookup"><span data-stu-id="fbfe2-202">Next, toomake sure that you have successfully captured hello image, use hello **list\_vm\_images** api, and make sure your image is displayed in hello results:</span></span>

    images = sms.list_vm_images()

<span data-ttu-id="fbfe2-203">toofinally criar máquina virtual de saudação usando a imagem capturada hello, use Olá **criar\_virtual\_máquina\_implantação** método como antes, mas desta vez passar Olá vm_image_name em vez disso</span><span class="sxs-lookup"><span data-stu-id="fbfe2-203">toofinally create hello virtual machine using hello captured image, use hello **create\_virtual\_machine\_deployment** method as before, but this time pass in hello vm_image_name instead</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=None,
        role_size='Small',
        vm_image_name = image_name)

<span data-ttu-id="fbfe2-204">Saiba mais sobre toolearn como toocapture uma máquina Virtual Linux, consulte [como tooCapture uma máquina Virtual Linux.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="fbfe2-204">toolearn more about how toocapture a Linux Virtual Machine, see [How tooCapture a Linux Virtual Machine.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="fbfe2-205">Saiba mais sobre toolearn como toocapture uma máquina Virtual do Windows, consulte [como tooCapture uma máquina Virtual do Windows.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="fbfe2-205">toolearn more about how toocapture a Windows Virtual Machine, see [How tooCapture a Windows Virtual Machine.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="fbfe2-206"><a name="What's Next"> </a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fbfe2-206"><a name="What's Next"> </a>Next Steps</span></span>
<span data-ttu-id="fbfe2-207">Agora que você aprendeu as Noções básicas de saudação do gerenciamento de serviços, você pode acessar Olá [documentação de referência de API completa para hello Azure SDK de Python](http://azure-sdk-for-python.readthedocs.org/) e executar complexo tarefas facilmente toomanage seu aplicativo de python.</span><span class="sxs-lookup"><span data-stu-id="fbfe2-207">Now that you've learned hello basics of service management, you can access hello [Complete API reference documentation for hello Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) and perform complex tasks easily toomanage your python application.</span></span>

<span data-ttu-id="fbfe2-208">Para obter mais informações, consulte Olá [Central de desenvolvedores de Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="fbfe2-208">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

[What is Service Management]: #WhatIs
[Concepts]: #Concepts
[How to: Connect tooservice management]: #Connect
[How to: List available locations]: #ListAvailableLocations
[How to: Create a cloud service]: #CreateCloudService
[How to: Delete a cloud service]: #DeleteCloudService
[How to: Create a deployment]: #CreateDeployment
[How to: Update a deployment]: #UpdateDeployment
[How to: Move deployments between staging and production]: #MoveDeployments
[How to: Delete a deployment]: #DeleteDeployment
[How to: Create a storage service]: #CreateStorageService
[How to: Delete a storage service]: #DeleteStorageService
[How to: List available operating systems]: #ListOperatingSystems
[How to: Create an operating system image]: #CreateVMImage
[How to: Delete an operating system image]: #DeleteVMImage
[How to: Create a virtual machine]: #CreateVM
[How to: Delete a virtual machine]: #DeleteVM
[Next Steps]: #NextSteps
[management-portal]: https://manage.windowsazure.com/
[svc-mgmt-rest-api]: http://msdn.microsoft.com/library/windowsazure/ee460799.aspx


[cloud service]:/services/cloud-services/
