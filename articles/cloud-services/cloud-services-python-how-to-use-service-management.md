---
title: "Como usar a API de gerenciamento de serviços (Python) - guia de recursos"
description: "Saiba como executar tarefas de gerenciamento de serviços comuns de forma programática no Python."
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
ms.openlocfilehash: 13249ba9a4b317a3154776b411ce0bb1f316b3bb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-service-management-from-python"></a><span data-ttu-id="3984a-103">Como usar o Gerenciamento de Serviços no Python</span><span class="sxs-lookup"><span data-stu-id="3984a-103">How to use Service Management from Python</span></span>
<span data-ttu-id="3984a-104">Este guia mostra como executar tarefas de gerenciamento de serviços comuns de forma programática no Python.</span><span class="sxs-lookup"><span data-stu-id="3984a-104">This guide shows you how to programmatically perform common service management tasks from Python.</span></span> <span data-ttu-id="3984a-105">A classe **ServiceManagementService** no [SDK do Azure para Python](https://github.com/Azure/azure-sdk-for-python) dá suporte a acesso programático para grande parte da funcionalidade relacionada ao gerenciamento de serviços que está disponível no [Portal Clássico do Azure][management-portal] (como **criação, atualização e exclusão de serviços de nuvem, implantações, serviços de gerenciamento de dados e máquinas virtuais**).</span><span class="sxs-lookup"><span data-stu-id="3984a-105">The **ServiceManagementService** class in the [Azure SDK for Python](https://github.com/Azure/azure-sdk-for-python) supports programmatic access to much of the service management-related functionality that is available in the [Azure classic portal][management-portal] (such as **creating, updating, and deleting cloud services, deployments, data management services, and virtual machines**).</span></span> <span data-ttu-id="3984a-106">Essa funcionalidade pode ser útil na criação de aplicativos que precisam de acesso programático ao gerenciamento de serviços.</span><span class="sxs-lookup"><span data-stu-id="3984a-106">This functionality can be useful in building applications that need programmatic access to service management.</span></span>

## <span data-ttu-id="3984a-107"><a name="WhatIs"> </a>O que é gerenciamento de serviços</span><span class="sxs-lookup"><span data-stu-id="3984a-107"><a name="WhatIs"> </a>What is Service Management</span></span>
<span data-ttu-id="3984a-108">A API de Gerenciamento de Serviços fornece acesso programático à grande parte da funcionalidade do gerenciamento de serviços disponível por meio do [Portal Clássico do Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="3984a-108">The Service Management API provides programmatic access to much of the service management functionality available through the [Azure classic portal][management-portal].</span></span> <span data-ttu-id="3984a-109">O SDK do Azure para Python permite que você gerencie os serviços de nuvem e as contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3984a-109">The Azure SDK for Python allows you to manage your cloud services and storage accounts.</span></span>

<span data-ttu-id="3984a-110">Para usar a API de Gerenciamento de Serviços, é necessário [criar uma conta do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3984a-110">To use the Service Management API, you need to [create an Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <span data-ttu-id="3984a-111"><a name="Concepts"> </a>Conceitos</span><span class="sxs-lookup"><span data-stu-id="3984a-111"><a name="Concepts"> </a>Concepts</span></span>
<span data-ttu-id="3984a-112">O SDK do Azure para Python encapsula a [API de Gerenciamento de Serviços do Azure][svc-mgmt-rest-api], que é uma API REST.</span><span class="sxs-lookup"><span data-stu-id="3984a-112">The Azure SDK for Python wraps the [Azure Service Management API][svc-mgmt-rest-api], which is a REST API.</span></span> <span data-ttu-id="3984a-113">Todas as operações da API são executadas por meio do SSL e mutuamente autenticadas usando certificados X.509 v3.</span><span class="sxs-lookup"><span data-stu-id="3984a-113">All API operations are performed over SSL and mutually authenticated using X.509 v3 certificates.</span></span> <span data-ttu-id="3984a-114">O serviço de gerenciamento pode ser acessado em um serviço em execução no Azure ou diretamente pela Internet em qualquer aplicativo que possa enviar uma solicitação HTTPS e receber uma resposta HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3984a-114">The management service may be accessed from within a service running in Azure, or directly over the Internet from any application that can send an HTTPS request and receive an HTTPS response.</span></span>

## <span data-ttu-id="3984a-115"><a name="Installation"> </a>Instalação</span><span class="sxs-lookup"><span data-stu-id="3984a-115"><a name="Installation"> </a>Installation</span></span>
<span data-ttu-id="3984a-116">Todos os recursos descritos neste artigo estão disponíveis no pacote do `azure-servicemanagement-legacy` , que pode ser instalado usando o pip.</span><span class="sxs-lookup"><span data-stu-id="3984a-116">All the features described in this article are available in the `azure-servicemanagement-legacy` package, which you can install using pip.</span></span> <span data-ttu-id="3984a-117">Para obter mais informações sobre a instalação (por exemplo, se você for novo no Python), consulte este artigo: [Instalando o Python e o SDK do Azure](../python-how-to-install.md)</span><span class="sxs-lookup"><span data-stu-id="3984a-117">For more information about installation (for example, if you are new to Python), see this article: [Installing Python and the Azure SDK](../python-how-to-install.md)</span></span>

## <span data-ttu-id="3984a-118"><a name="Connect"> </a>Como conectar-se ao gerenciamento de serviços</span><span class="sxs-lookup"><span data-stu-id="3984a-118"><a name="Connect"> </a>How to: Connect to service management</span></span>
<span data-ttu-id="3984a-119">Para conectar-se ao ponto de extremidade do Gerenciamento de Serviços, você precisa da ID de sua assinatura do Azure e um certificado de gerenciamento válido.</span><span class="sxs-lookup"><span data-stu-id="3984a-119">To connect to the Service Management endpoint, you need your Azure subscription ID and a valid management certificate.</span></span> <span data-ttu-id="3984a-120">Você pode obter sua ID de assinatura por meio do [Portal Clássico do Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="3984a-120">You can obtain your subscription ID through the [Azure classic portal][management-portal].</span></span>

> [!NOTE]
> <span data-ttu-id="3984a-121">Agora é possível usar certificados criados com o OpenSSL quando for executado no Windows.</span><span class="sxs-lookup"><span data-stu-id="3984a-121">It is now possible to use certificates created with OpenSSL when running on Windows.</span></span>  <span data-ttu-id="3984a-122">Isso requer o Python 2.7.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="3984a-122">It requires Python 2.7.4 or later.</span></span> <span data-ttu-id="3984a-123">Recomendamos que os usuários usem o OpenSSL, em vez de .pfx, já que o suporte para certificados .pfx provavelmente será removido no futuro.</span><span class="sxs-lookup"><span data-stu-id="3984a-123">We recommend users to use OpenSSL instead of .pfx, since support for .pfx certificates will likely be removed in the future.</span></span>
>
>

### <a name="management-certificates-on-windowsmaclinux-openssl"></a><span data-ttu-id="3984a-124">Certificados de gerenciamento no Windows/Mac/Linux (OpenSSL)</span><span class="sxs-lookup"><span data-stu-id="3984a-124">Management certificates on Windows/Mac/Linux (OpenSSL)</span></span>
<span data-ttu-id="3984a-125">Você também pode usar o [OpenSSL](http://www.openssl.org/) para criar o certificado de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="3984a-125">You can use [OpenSSL](http://www.openssl.org/) to create your management certificate.</span></span>  <span data-ttu-id="3984a-126">Na verdade, você precisa criar dois certificados, um para o servidor (um arquivo `.cer`) e um para o cliente (um arquivo `.pem`).</span><span class="sxs-lookup"><span data-stu-id="3984a-126">You actually need to create two certificates, one for the server (a `.cer` file) and one for the client (a `.pem` file).</span></span> <span data-ttu-id="3984a-127">Para criar o arquivo `.pem` , execute isto:</span><span class="sxs-lookup"><span data-stu-id="3984a-127">To create the `.pem` file, execute:</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="3984a-128">Para criar o certificado `.cer` , execute isto:</span><span class="sxs-lookup"><span data-stu-id="3984a-128">To create the `.cer` certificate, execute:</span></span>

    openssl x509 -inform pem -in mycert.pem -outform der -out mycert.cer

<span data-ttu-id="3984a-129">Para saber mais sobre certificados do Azure, confira [Visão geral dos Certificados de Serviços de Nuvem do Azure](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="3984a-129">For more information about Azure certificates, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="3984a-130">Para obter uma descrição completa dos parâmetros do OpenSSL, consulte a documentação em [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span><span class="sxs-lookup"><span data-stu-id="3984a-130">For a complete description of OpenSSL parameters, see the documentation at [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span></span>

<span data-ttu-id="3984a-131">Depois de criar esses arquivos, você precisará carregar o arquivo `.cer` no Azure por meio da ação "Carregar" da guia "Configurações" do [Portal Clássico do Azure][management-portal] e anotar o local no qual você salvou o arquivo `.pem`.</span><span class="sxs-lookup"><span data-stu-id="3984a-131">After you have created these files, you need to upload the `.cer` file to Azure via the "Upload" action of the "Settings" tab of the [Azure classic portal][management-portal], and you need to make note of where you saved the `.pem` file.</span></span>

<span data-ttu-id="3984a-132">Depois de ter obtido a ID de sua assinatura, criado um certificado e carregado o arquivo `.cer` no Azure, você pode conectar-se ao ponto de extremidade de gerenciamento do Azure passando a ID da assinatura e o caminho para o arquivo `.pem` para o **ServiceManagementService**:</span><span class="sxs-lookup"><span data-stu-id="3984a-132">After you have obtained your subscription ID, created a certificate, and uploaded the `.cer` file to Azure, you can connect to the Azure management endpoint by passing the subscription id and the path to the `.pem` file to **ServiceManagementService**:</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = '<path_to_.pem_certificate>'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="3984a-133">No exemplo acima, `sms` é um objeto **ServiceManagementService** .</span><span class="sxs-lookup"><span data-stu-id="3984a-133">In the preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="3984a-134">A classe **ServiceManagementService** é a classe primária usada para gerenciar os serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="3984a-134">The **ServiceManagementService** class is the primary class used to manage Azure services.</span></span>

### <a name="management-certificates-on-windows-makecert"></a><span data-ttu-id="3984a-135">Certificados de gerenciamento no Windows (MakeCert)</span><span class="sxs-lookup"><span data-stu-id="3984a-135">Management certificates on Windows (MakeCert)</span></span>
<span data-ttu-id="3984a-136">Você pode criar um certificado de gerenciamento autoassinado em seu computador usando `makecert.exe`.</span><span class="sxs-lookup"><span data-stu-id="3984a-136">You can create a self-signed management certificate on your machine using `makecert.exe`.</span></span>  <span data-ttu-id="3984a-137">Abra um **prompt de comando do Visual Studio** como **administrador** e use o seguinte comando, substituindo *AzureCertificate* pelo nome do certificado que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="3984a-137">Open a **Visual Studio command prompt** as an **administrator** and use the following command, replacing *AzureCertificate* with the certificate name you would like to use.</span></span>

    makecert -sky exchange -r -n "CN=AzureCertificate" -pe -a sha1 -len 2048 -ss My "AzureCertificate.cer"

<span data-ttu-id="3984a-138">O comando cria o arquivo `.cer` e o instala no repositório de certificados **Pessoal** .</span><span class="sxs-lookup"><span data-stu-id="3984a-138">The command creates the `.cer` file, and installs it in the **Personal** certificate store.</span></span> <span data-ttu-id="3984a-139">Para obter mais informações, confira a [Visão geral sobre certificados para os Serviços de Nuvem do Azure](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="3984a-139">For more information, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span>

<span data-ttu-id="3984a-140">Depois que tiver criado o certificado, você precisará carregar do arquivo `.cer` no Azure por meio da ação "Carregar" da guia "Configurações" no [Portal Clássico do Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="3984a-140">After you have created the certificate, you need to upload the `.cer` file to Azure via the "Upload" action of the "Settings" tab of the [Azure classic portal][management-portal].</span></span>

<span data-ttu-id="3984a-141">Depois que tiver obtido a ID da sua assinatura, criado um certificado e carregado o arquivo `.cer` para o Azure, você poderá conectar-se ao ponto de extremidade de gerenciamento do Azure, passando a ID da assinatura e a localização do certificado em seu repositório de certificados **Pessoal** para **ServiceManagementService** (novamente, substitua *AzureCertificate* pelo nome do seu certificado):</span><span class="sxs-lookup"><span data-stu-id="3984a-141">After you have obtained your subscription ID, created a certificate, and uploaded the `.cer` file to Azure, you can connect to the Azure management endpoint by passing the subscription id and the location of the certificate in your **Personal** certificate store to **ServiceManagementService** (again, replace *AzureCertificate* with the name of your certificate):</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = 'CURRENT_USER\\my\\AzureCertificate'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="3984a-142">No exemplo acima, `sms` é um objeto **ServiceManagementService** .</span><span class="sxs-lookup"><span data-stu-id="3984a-142">In the preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="3984a-143">A classe **ServiceManagementService** é a classe primária usada para gerenciar os serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="3984a-143">The **ServiceManagementService** class is the primary class used to manage Azure services.</span></span>

## <span data-ttu-id="3984a-144"><a name="ListAvailableLocations"> </a>Como listar os locais disponíveis</span><span class="sxs-lookup"><span data-stu-id="3984a-144"><a name="ListAvailableLocations"> </a>How to: List available locations</span></span>
<span data-ttu-id="3984a-145">Para listar os locais que estão disponíveis para hospedar serviços, use o método **list\_locations**:</span><span class="sxs-lookup"><span data-stu-id="3984a-145">To list the locations that are available for hosting services, use the **list\_locations** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_locations()
    for location in result:
        print(location.name)

<span data-ttu-id="3984a-146">Ao criar um serviço de nuvem ou de armazenamento, é preciso fornecer uma localização válida.</span><span class="sxs-lookup"><span data-stu-id="3984a-146">When you create a cloud service or storage service you need to provide a valid location.</span></span> <span data-ttu-id="3984a-147">O método **list\_locations** sempre retorna uma lista atualizada dos locais disponíveis no momento.</span><span class="sxs-lookup"><span data-stu-id="3984a-147">The **list\_locations** method always returns an up-to-date list of the currently available locations.</span></span> <span data-ttu-id="3984a-148">Na data da criação deste artigo, os locais disponíveis são:</span><span class="sxs-lookup"><span data-stu-id="3984a-148">As of this writing, the available locations are:</span></span>

* <span data-ttu-id="3984a-149">Europa Ocidental</span><span class="sxs-lookup"><span data-stu-id="3984a-149">West Europe</span></span>
* <span data-ttu-id="3984a-150">Norte da Europa</span><span class="sxs-lookup"><span data-stu-id="3984a-150">North Europe</span></span>
* <span data-ttu-id="3984a-151">Sudeste Asiático</span><span class="sxs-lookup"><span data-stu-id="3984a-151">Southeast Asia</span></span>
* <span data-ttu-id="3984a-152">Ásia Oriental</span><span class="sxs-lookup"><span data-stu-id="3984a-152">East Asia</span></span>
* <span data-ttu-id="3984a-153">Centro dos EUA</span><span class="sxs-lookup"><span data-stu-id="3984a-153">Central US</span></span>
* <span data-ttu-id="3984a-154">Centro-Norte dos EUA</span><span class="sxs-lookup"><span data-stu-id="3984a-154">North Central US</span></span>
* <span data-ttu-id="3984a-155">Centro-Sul dos Estados Unidos</span><span class="sxs-lookup"><span data-stu-id="3984a-155">South Central US</span></span>
* <span data-ttu-id="3984a-156">Oeste dos EUA</span><span class="sxs-lookup"><span data-stu-id="3984a-156">West US</span></span>
* <span data-ttu-id="3984a-157">Leste dos EUA</span><span class="sxs-lookup"><span data-stu-id="3984a-157">East US</span></span>
* <span data-ttu-id="3984a-158">Leste do Japão</span><span class="sxs-lookup"><span data-stu-id="3984a-158">Japan East</span></span>
* <span data-ttu-id="3984a-159">Oeste do Japão</span><span class="sxs-lookup"><span data-stu-id="3984a-159">Japan West</span></span>
* <span data-ttu-id="3984a-160">Sul do Brasil</span><span class="sxs-lookup"><span data-stu-id="3984a-160">Brazil South</span></span>
* <span data-ttu-id="3984a-161">Leste da Austrália</span><span class="sxs-lookup"><span data-stu-id="3984a-161">Australia East</span></span>
* <span data-ttu-id="3984a-162">Sudeste da Austrália</span><span class="sxs-lookup"><span data-stu-id="3984a-162">Australia Southeast</span></span>

## <span data-ttu-id="3984a-163"><a name="CreateCloudService"> </a>Como criar um serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="3984a-163"><a name="CreateCloudService"> </a>How to: Create a cloud service</span></span>
<span data-ttu-id="3984a-164">Quando você cria um aplicativo e o executa no Azure, o código e a configuração, juntos, são chamados de [serviço de nuvem][cloud service] do Azure (conhecido como *serviço hospedado* em versões anteriores do Azure).</span><span class="sxs-lookup"><span data-stu-id="3984a-164">When you create an application and run it in Azure, the code and configuration together are called an Azure [cloud service][cloud service] (known as a *hosted service* in earlier Azure releases).</span></span> <span data-ttu-id="3984a-165">O método **create\_hosted\_service** permite que você crie um novo serviço hospedado, fornecendo um nome de serviço hospedado (que deve ser exclusivo no Azure), um rótulo (automaticamente codificado em base64), uma descrição e uma localização.</span><span class="sxs-lookup"><span data-stu-id="3984a-165">The **create\_hosted\_service** method allows you to create a new hosted service by providing a hosted service name (which must be unique in Azure), a label (automatically encoded to base64), a description, and a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myhostedservice'
    label = 'myhostedservice'
    desc = 'my hosted service'
    location = 'West US'

    sms.create_hosted_service(name, label, desc, location)

<span data-ttu-id="3984a-166">Você pode listar todos os serviços hospedados para seu assinatura com o método **list\_hosted\_services**:</span><span class="sxs-lookup"><span data-stu-id="3984a-166">You can list all the hosted services for your subscription with the **list\_hosted\_services** method:</span></span>

    result = sms.list_hosted_services()

    for hosted_service in result:
        print('Service name: ' + hosted_service.service_name)
        print('Management URL: ' + hosted_service.url)
        print('Location: ' + hosted_service.hosted_service_properties.location)
        print('')

<span data-ttu-id="3984a-167">Se desejar obter informações sobre um determinado serviço hospedado, você pode fazê-lo passando o nome do serviço hospedado para o método **get\_hosted\_service\_properties**:</span><span class="sxs-lookup"><span data-stu-id="3984a-167">If you want to get information about a particular hosted service, you can do so by passing the hosted service name to the **get\_hosted\_service\_properties** method:</span></span>

    hosted_service = sms.get_hosted_service_properties('myhostedservice')

    print('Service name: ' + hosted_service.service_name)
    print('Management URL: ' + hosted_service.url)
    print('Location: ' + hosted_service.hosted_service_properties.location)

<span data-ttu-id="3984a-168">Depois de criar um serviço de nuvem, você pode implantar seu código de serviço com o método **create\_deployment**.</span><span class="sxs-lookup"><span data-stu-id="3984a-168">After you have created a cloud service, you can deploy your code to the service with the **create\_deployment** method.</span></span>

## <span data-ttu-id="3984a-169"><a name="DeleteCloudService"> </a>Como excluir um serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="3984a-169"><a name="DeleteCloudService"> </a>How to: Delete a cloud service</span></span>
<span data-ttu-id="3984a-170">Você pode excluir um serviço de nuvem passando o nome do serviço para o método **delete\_hosted\_service**:</span><span class="sxs-lookup"><span data-stu-id="3984a-170">You can delete a cloud service by passing the service name to the **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service('myhostedservice')

<span data-ttu-id="3984a-171">Para que seja possível excluir um serviço, todas as implantações do serviço devem ser excluídas primeiro.</span><span class="sxs-lookup"><span data-stu-id="3984a-171">Before you can delete a service, all deployments for the service must first be deleted.</span></span> <span data-ttu-id="3984a-172">(Consulte [Como excluir uma implantação](#DeleteDeployment) para obter detalhes.)</span><span class="sxs-lookup"><span data-stu-id="3984a-172">(See [How to: Delete a deployment](#DeleteDeployment) for details.)</span></span>

## <span data-ttu-id="3984a-173"><a name="DeleteDeployment"> </a>Como excluir uma implantação</span><span class="sxs-lookup"><span data-stu-id="3984a-173"><a name="DeleteDeployment"> </a>How to: Delete a deployment</span></span>
<span data-ttu-id="3984a-174">Para excluir uma implantação, use o método **delete\_deployment**.</span><span class="sxs-lookup"><span data-stu-id="3984a-174">To delete a deployment, use the **delete\_deployment** method.</span></span> <span data-ttu-id="3984a-175">O exemplo a seguir mostra como excluir uma implantação chamada `v1`.</span><span class="sxs-lookup"><span data-stu-id="3984a-175">The following example shows how to delete a deployment named `v1`.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment('myhostedservice', 'v1')

## <span data-ttu-id="3984a-176"><a name="CreateStorageService"> </a>Como criar um serviço de armazenamento</span><span class="sxs-lookup"><span data-stu-id="3984a-176"><a name="CreateStorageService"> </a>How to: Create a storage service</span></span>
<span data-ttu-id="3984a-177">Um [serviço de armazenamento](../storage/common/storage-create-storage-account.md) fornece acesso a [Blobs](../storage/blobs/storage-python-how-to-use-blob-storage.md), [Tables](../cosmos-db/table-storage-how-to-use-python.md) e [Queues](../storage/queues/storage-python-how-to-use-queue-storage.md) do Azure.</span><span class="sxs-lookup"><span data-stu-id="3984a-177">A [storage service](../storage/common/storage-create-storage-account.md) gives you access to Azure [Blobs](../storage/blobs/storage-python-how-to-use-blob-storage.md), [Tables](../cosmos-db/table-storage-how-to-use-python.md), and [Queues](../storage/queues/storage-python-how-to-use-queue-storage.md).</span></span> <span data-ttu-id="3984a-178">Para criar um serviço de armazenamento, você precisa de um nome para o serviço (com 3 a 24 caracteres minúsculos e exclusivo no Azure), uma descrição, um rótulo (até 100 caracteres, automaticamente codificado em base64) e um local.</span><span class="sxs-lookup"><span data-stu-id="3984a-178">To create a storage service, you need a name for the service (between 3 and 24 lowercase characters and unique within Azure), a description, a label (up to 100 characters, automatically encoded to base64), and a location.</span></span> <span data-ttu-id="3984a-179">O exemplo a seguir mostra como criar um serviço de armazenamento especificando um local.</span><span class="sxs-lookup"><span data-stu-id="3984a-179">The following example shows how to create a storage service by specifying a location.</span></span>

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

<span data-ttu-id="3984a-180">Observe no exemplo acima que o status da operação **create\_storage\_account** pode ser recuperada passando o resultado retornado pelo **create\_storage\_account** ao método **get\_operation\_status**.</span><span class="sxs-lookup"><span data-stu-id="3984a-180">Note in the preceding example that the status of the **create\_storage\_account** operation can be retrieved by passing the result returned by **create\_storage\_account** to the **get\_operation\_status** method.</span></span>  

<span data-ttu-id="3984a-181">Você pode listar suas contas de armazenamento e suas propriedades com o método **list\_storage\_accounts**:</span><span class="sxs-lookup"><span data-stu-id="3984a-181">You can list your storage accounts and their properties with the **list\_storage\_accounts** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_storage_accounts()
    for account in result:
        print('Service name: ' + account.service_name)
        print('Location: ' + account.storage_service_properties.location)
        print('')

## <span data-ttu-id="3984a-182"><a name="DeleteStorageService"> </a>Como excluir um serviço de armazenamento</span><span class="sxs-lookup"><span data-stu-id="3984a-182"><a name="DeleteStorageService"> </a>How to: Delete a storage service</span></span>
<span data-ttu-id="3984a-183">Você pode excluir um serviço de armazenamento passando o nome do serviço para o método **delete\_storage\_account**.</span><span class="sxs-lookup"><span data-stu-id="3984a-183">You can delete a storage service by passing the storage service name to the **delete\_storage\_account** method.</span></span> <span data-ttu-id="3984a-184">A exclusão de um serviço de armazenamento excluirá todos os dados armazenados no serviço (blobs, tabelas e filas).</span><span class="sxs-lookup"><span data-stu-id="3984a-184">Deleting a storage service deletes all data stored in the service (blobs, tables, and queues).</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_storage_account('mystorageaccount')

## <span data-ttu-id="3984a-185"><a name="ListOperatingSystems"> </a>Como listar os sistemas operacionais disponíveis</span><span class="sxs-lookup"><span data-stu-id="3984a-185"><a name="ListOperatingSystems"> </a>How to: List available operating systems</span></span>
<span data-ttu-id="3984a-186">Para listar os sistemas operacionais que estão disponíveis para hospedar serviços, use o método **list\_operating\_systems**:</span><span class="sxs-lookup"><span data-stu-id="3984a-186">To list the operating systems that are available for hosting services, use the **list\_operating\_systems** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_operating_systems()

    for os in result:
        print('OS: ' + os.label)
        print('Family: ' + os.family_label)
        print('Active: ' + str(os.is_active))

<span data-ttu-id="3984a-187">Como alternativa, você pode usar o método **list\_operating\_system\_families** que agrupa os sistemas operacionais por família:</span><span class="sxs-lookup"><span data-stu-id="3984a-187">Alternatively, you can use the **list\_operating\_system\_families** method, which groups the operating systems by family:</span></span>

    result = sms.list_operating_system_families()

    for family in result:
        print('Family: ' + family.label)
        for os in family.operating_systems:
            if os.is_active:
                print('OS: ' + os.label)
                print('Version: ' + os.version)
        print('')

## <span data-ttu-id="3984a-188"><a name="CreateVMImage"> </a>Como criar uma imagem do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="3984a-188"><a name="CreateVMImage"> </a>How to: Create an operating system image</span></span>
<span data-ttu-id="3984a-189">Para adicionar uma imagem do sistema operacional ao repositório de imagens, use o método **add\_os\_image**:</span><span class="sxs-lookup"><span data-stu-id="3984a-189">To add an operating system image to the image repository, use the **add\_os\_image** method:</span></span>

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

<span data-ttu-id="3984a-190">Para listar as imagens do sistema operacional estão disponíveis, use o método **list\_os\_images**.</span><span class="sxs-lookup"><span data-stu-id="3984a-190">To list the operating system images that are available, use the **list\_os\_images** method.</span></span> <span data-ttu-id="3984a-191">Isso inclui todas as imagens de plataforma e imagens do usuário:</span><span class="sxs-lookup"><span data-stu-id="3984a-191">It includes all platform images and user images:</span></span>

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

## <span data-ttu-id="3984a-192"><a name="DeleteVMImage"> </a>Como excluir uma imagem do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="3984a-192"><a name="DeleteVMImage"> </a>How to: Delete an operating system image</span></span>
<span data-ttu-id="3984a-193">Para excluir uma imagem de usuário, use o método **delete\_os\_image**:</span><span class="sxs-lookup"><span data-stu-id="3984a-193">To delete a user image, use the **delete\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.delete_os_image('mycentos')

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

## <span data-ttu-id="3984a-194"><a name="CreateVM"> </a>Como criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="3984a-194"><a name="CreateVM"> </a>How to: Create a virtual machine</span></span>
<span data-ttu-id="3984a-195">Para criar uma máquina virtual, você precisa primeiro criar um [serviço de nuvem](#CreateCloudService).</span><span class="sxs-lookup"><span data-stu-id="3984a-195">To create a virtual machine, you first need to create a [cloud service](#CreateCloudService).</span></span>  <span data-ttu-id="3984a-196">Em seguida, criar a implantação da máquina virtual usando o método **create\_virtual\_machine\_deployment**:</span><span class="sxs-lookup"><span data-stu-id="3984a-196">Then create the virtual machine deployment using the **create\_virtual\_machine\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set the location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    # Name of an os image as returned by list_os_images
    image_name = 'OpenLogic__OpenLogic-CentOS-62-20120531-en-us-30GB.vhd'

    # Destination storage account container/blob where the VM disk
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

## <span data-ttu-id="3984a-197"><a name="DeleteVM"> </a>Como excluir uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="3984a-197"><a name="DeleteVM"> </a>How to: Delete a virtual machine</span></span>
<span data-ttu-id="3984a-198">Para excluir uma máquina virtual, primeiro você exclui a implantação usando o método **delete\_deployment**:</span><span class="sxs-lookup"><span data-stu-id="3984a-198">To delete a virtual machine, you first delete the deployment using the **delete\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment(service_name='myvm',
        deployment_name='myvm')

<span data-ttu-id="3984a-199">O serviço de nuvem pode ser excluído usando o método **delete\_hosted\_service**:</span><span class="sxs-lookup"><span data-stu-id="3984a-199">The cloud service can then be deleted using the **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service(service_name='myvm')

## <a name="how-to-create-a-virtual-machine-from-a-captured-virtual-machine-image"></a><span data-ttu-id="3984a-200">Como criar uma máquina virtual por meio de uma imagem de máquina virtual capturada</span><span class="sxs-lookup"><span data-stu-id="3984a-200">How To: Create a Virtual Machine from a Captured Virtual Machine Image</span></span>
<span data-ttu-id="3984a-201">Para capturar uma imagem de VM, você primeiro chama o método **capture\_vm\_image**:</span><span class="sxs-lookup"><span data-stu-id="3984a-201">To capture a VM image, you first call the **capture\_vm\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    # replace the below three parameters with actual values
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

<span data-ttu-id="3984a-202">Em seguida, para certificar-se de que você capturou a imagem com sucesso, use a API **list\_vm\_images** e certifique-se de que a imagem seja exibida nos resultados:</span><span class="sxs-lookup"><span data-stu-id="3984a-202">Next, to make sure that you have successfully captured the image, use the **list\_vm\_images** api, and make sure your image is displayed in the results:</span></span>

    images = sms.list_vm_images()

<span data-ttu-id="3984a-203">Para criar finalmente a máquina virtual usando a imagem capturada, use o método **create\_virtual\_machine\_deployment** como antes, mas desta vez passe vm_image_name</span><span class="sxs-lookup"><span data-stu-id="3984a-203">To finally create the virtual machine using the captured image, use the **create\_virtual\_machine\_deployment** method as before, but this time pass in the vm_image_name instead</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set the location
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

<span data-ttu-id="3984a-204">Para saber mais sobre como capturar uma máquina Virtual Linux, consulte [Como capturar uma máquina Virtual Linux.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="3984a-204">To learn more about how to capture a Linux Virtual Machine, see [How to Capture a Linux Virtual Machine.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="3984a-205">Para saber mais sobre como capturar uma máquina Virtual Windows, consulte [Como capturar uma máquina Virtual Windows.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="3984a-205">To learn more about how to capture a Windows Virtual Machine, see [How to Capture a Windows Virtual Machine.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="3984a-206"><a name="What's Next"> </a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3984a-206"><a name="What's Next"> </a>Next Steps</span></span>
<span data-ttu-id="3984a-207">Agora que você aprendeu os fundamentos do gerenciamento de serviços, você pode acessar a [documentação de referência da API completa para o SDK do Azure Python](http://azure-sdk-for-python.readthedocs.org/) e realizar tarefas complexas facilmente para gerenciar seu aplicativo python.</span><span class="sxs-lookup"><span data-stu-id="3984a-207">Now that you've learned the basics of service management, you can access the [Complete API reference documentation for the Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) and perform complex tasks easily to manage your python application.</span></span>

<span data-ttu-id="3984a-208">Para saber mais, consulte o [Centro de Desenvolvedores do Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="3984a-208">For more information, see the [Python Developer Center](/develop/python/).</span></span>

[What is Service Management]: #WhatIs
[Concepts]: #Concepts
[How to: Connect to service management]: #Connect
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
