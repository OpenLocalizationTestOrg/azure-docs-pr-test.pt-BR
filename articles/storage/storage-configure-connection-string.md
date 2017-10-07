---
title: "aaaConfigure uma cadeia de caracteres de conexão para o armazenamento do Azure | Microsoft Docs"
description: "Configure uma cadeia de conexão para uma conta de Armazenamento do Azure. Uma cadeia de caracteres de conexão contém informações de saudação tooauthenticate de acesso necessário tooa conta de armazenamento de seu aplicativo em tempo de execução."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: ecb0acb5-90a9-4eb2-93e6-e9860eda5e53
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: marsma
ms.openlocfilehash: 80c38a6f8f0d4f06b99e7c487647b984e01d1772
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-storage-connection-strings"></a><span data-ttu-id="5f3fa-104">Configurar cadeias de conexão do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="5f3fa-104">Configure Azure Storage connection strings</span></span>

<span data-ttu-id="5f3fa-105">Uma cadeia de caracteres de conexão inclui informações de autenticação de saudação necessárias para os dados do aplicativo tooaccess em uma conta de armazenamento do Azure em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-105">A connection string includes hello authentication information required for your application tooaccess data in an Azure Storage account at runtime.</span></span> <span data-ttu-id="5f3fa-106">Você pode configurar cadeias de conexão para:</span><span class="sxs-lookup"><span data-stu-id="5f3fa-106">You can configure connection strings to:</span></span>

* <span data-ttu-id="5f3fa-107">Conecte-se toohello emulador de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-107">Connect toohello Azure storage emulator.</span></span>
* <span data-ttu-id="5f3fa-108">Acesse uma conta de armazenamento no Azure.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-108">Access a storage account in Azure.</span></span>
* <span data-ttu-id="5f3fa-109">Acessar recursos especificados no Azure por uma SAS (Assinatura de Acesso Compartilhado).</span><span class="sxs-lookup"><span data-stu-id="5f3fa-109">Access specified resources in Azure via a shared access signature (SAS).</span></span>

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

## <a name="storing-your-connection-string"></a><span data-ttu-id="5f3fa-110">Armazenar a sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="5f3fa-110">Storing your connection string</span></span>
<span data-ttu-id="5f3fa-111">Seu aplicativo precisa de cadeia de caracteres de conexão Olá de tooaccess em tempo de execução tooauthenticate solicitações feitas tooAzure armazenamento.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-111">Your application needs tooaccess hello connection string at runtime tooauthenticate requests made tooAzure Storage.</span></span> <span data-ttu-id="5f3fa-112">Você tem várias opções diferentes para armazenar a cadeia de conexão:</span><span class="sxs-lookup"><span data-stu-id="5f3fa-112">You have several options for storing your connection string:</span></span>

* <span data-ttu-id="5f3fa-113">Um aplicativo em execução na área de trabalho hello, ou em um dispositivo pode armazenar a cadeia de caracteres de conexão de saudação em uma **App. config** ou **Web. config** arquivo.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-113">An application running on hello desktop or on a device can store hello connection string in an **app.config** or **web.config** file.</span></span> <span data-ttu-id="5f3fa-114">Adicionar toohello de cadeia de caracteres de conexão Olá **AppSettings** seção nesses arquivos.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-114">Add hello connection string toohello **AppSettings** section in these files.</span></span>
* <span data-ttu-id="5f3fa-115">Um aplicativo em execução em um serviço de nuvem do Azure pode armazenar a cadeia de caracteres de conexão de saudação em Olá [arquivo de esquema (. cscfg) de configuração de serviço do Azure](https://msdn.microsoft.com/library/ee758710.aspx).</span><span class="sxs-lookup"><span data-stu-id="5f3fa-115">An application running in an Azure cloud service can store hello connection string in hello [Azure service configuration schema (.cscfg) file](https://msdn.microsoft.com/library/ee758710.aspx).</span></span> <span data-ttu-id="5f3fa-116">Adicionar toohello de cadeia de caracteres de conexão Olá **ConfigurationSettings** seção do arquivo de configuração do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-116">Add hello connection string toohello **ConfigurationSettings** section of hello service configuration file.</span></span>
* <span data-ttu-id="5f3fa-117">Você pode usar a cadeia de conexão diretamente no seu código.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-117">You can use your connection string directly in your code.</span></span> <span data-ttu-id="5f3fa-118">Na maioria dos cenários, no entanto, recomendamos armazenar sua cadeia de conexão em um arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-118">However, we recommend that you store your connection string in a configuration file in most scenarios.</span></span>

<span data-ttu-id="5f3fa-119">Armazenar a cadeia de conexão em um arquivo de configuração torna tooswitch de cadeia de caracteres de conexão tooupdate fácil Olá entre o emulador de armazenamento hello e uma conta de armazenamento do Azure na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-119">Storing your connection string in a configuration file makes it easy tooupdate hello connection string tooswitch between hello storage emulator and an Azure storage account in hello cloud.</span></span> <span data-ttu-id="5f3fa-120">Você só precisa ambiente de destino tooedit Olá conexão cadeia de caracteres toopoint tooyour.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-120">You only need tooedit hello connection string toopoint tooyour target environment.</span></span>

<span data-ttu-id="5f3fa-121">Você pode usar o hello [Gerenciador de configuração do Microsoft Azure](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) tooaccess sua conexão de cadeia de caracteres em tempo de execução, independentemente de onde o aplicativo está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-121">You can use hello [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) tooaccess your connection string at runtime regardless of where your application is running.</span></span>

## <a name="create-a-connection-string-for-hello-storage-emulator"></a><span data-ttu-id="5f3fa-122">Criar uma cadeia de caracteres de conexão para o emulador de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="5f3fa-122">Create a connection string for hello storage emulator</span></span>
[!INCLUDE [storage-emulator-connection-string-include](../../includes/storage-emulator-connection-string-include.md)]

<span data-ttu-id="5f3fa-123">Para obter mais informações sobre o emulador de armazenamento hello, consulte [usar o emulador de armazenamento do Azure Olá para desenvolvimento e teste](storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="5f3fa-123">For more information about hello storage emulator, see [Use hello Azure storage emulator for development and testing](storage-use-emulator.md).</span></span>

## <a name="create-a-connection-string-for-an-azure-storage-account"></a><span data-ttu-id="5f3fa-124">Criar uma cadeia de conexão para uma conta de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="5f3fa-124">Create a connection string for an Azure storage account</span></span>
<span data-ttu-id="5f3fa-125">toocreate uma cadeia de caracteres de conexão para sua conta de armazenamento do Azure, formato a seguir de saudação do uso.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-125">toocreate a connection string for your Azure storage account, use hello following format.</span></span> <span data-ttu-id="5f3fa-126">Indique se deseja tooconnect toohello conta de armazenamento por meio de HTTPS (recomendado) ou HTTP, substitua `myAccountName` com o nome da saudação de sua conta de armazenamento e substitua `myAccountKey` com sua chave de acesso da conta:</span><span class="sxs-lookup"><span data-stu-id="5f3fa-126">Indicate whether you want tooconnect toohello storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with hello name of your storage account, and replace `myAccountKey` with your account access key:</span></span>

`DefaultEndpointsProtocol=[http|https];AccountName=myAccountName;AccountKey=myAccountKey`

<span data-ttu-id="5f3fa-127">Por exemplo, a cadeia de conexão pode parecer com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="5f3fa-127">For example, your connection string might look similar to:</span></span>

`DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=<account-key>`

<span data-ttu-id="5f3fa-128">Embora o Armazenamento do Azure dê suporte a HTTP e HTTPS em uma cadeia de conexão, *usar HTTPS é altamente recomendável*.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-128">Although Azure Storage supports both HTTP and HTTPS in a connection string, *HTTPS is highly recommended*.</span></span>

> [!TIP]
> <span data-ttu-id="5f3fa-129">Você pode encontrar as cadeias de caracteres de conexão da sua conta de armazenamento no hello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5f3fa-129">You can find your storage account's connection strings in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="5f3fa-130">Navegue muito**configurações** > **chaves de acesso** em cadeias de conexão de toosee da sua conta de armazenamento menu folha para ambas as chaves de acesso primária e secundária.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-130">Navigate too**SETTINGS** > **Access keys** in your storage account's menu blade toosee connection strings for both primary and secondary access keys.</span></span>
>

## <a name="create-a-connection-string-using-a-shared-access-signature"></a><span data-ttu-id="5f3fa-131">Criar uma cadeia de conexão usando uma assinatura de acesso compartilhado</span><span class="sxs-lookup"><span data-stu-id="5f3fa-131">Create a connection string using a shared access signature</span></span>
[!INCLUDE [storage-use-sas-in-connection-string-include](../../includes/storage-use-sas-in-connection-string-include.md)]

## <a name="create-a-connection-string-for-an-explicit-storage-endpoint"></a><span data-ttu-id="5f3fa-132">Criar uma cadeia de conexão para um ponto de extremidade explícito do armazenamento</span><span class="sxs-lookup"><span data-stu-id="5f3fa-132">Create a connection string for an explicit storage endpoint</span></span>
<span data-ttu-id="5f3fa-133">Você pode especificar pontos de extremidade de serviço explícito em sua cadeia de conexão em vez de usar pontos de extremidade saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-133">You can specify explicit service endpoints in your connection string instead of using hello default endpoints.</span></span> <span data-ttu-id="5f3fa-134">toocreate uma cadeia de caracteres de conexão que especifica um ponto de extremidade explícito, especificar ponto de extremidade de serviço completo Olá para cada serviço, incluindo a especificação do protocolo de saudação (HTTP ou HTTPS (recomendado)), Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="5f3fa-134">toocreate a connection string that specifies an explicit endpoint, specify hello complete service endpoint for each service, including hello protocol specification (HTTPS (recommended) or HTTP), in hello following format:</span></span>

```
DefaultEndpointsProtocol=[http|https];
BlobEndpoint=myBlobEndpoint;
FileEndpoint=myFileEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
AccountName=myAccountName;
AccountKey=myAccountKey
```

<span data-ttu-id="5f3fa-135">Um cenário em que talvez você queira toospecify um ponto de extremidade explícito é quando você mapeou o tooa de ponto de extremidade de armazenamento de Blob [domínio personalizado](storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="5f3fa-135">One scenario where you might wish toospecify an explicit endpoint is when you've mapped your Blob storage endpoint tooa [custom domain](storage-custom-domain-name.md).</span></span> <span data-ttu-id="5f3fa-136">Nesse caso, você pode especificar o ponto de extremidade personalizado para o armazenamento de Blobs em sua cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-136">In that case, you can specify your custom endpoint for Blob storage in your connection string.</span></span> <span data-ttu-id="5f3fa-137">Você pode especificar opcionalmente saudação padrão pontos de extremidade Olá outros serviços se seu aplicativo usa.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-137">You can optionally specify hello default endpoints for hello other services if your application uses them.</span></span>

<span data-ttu-id="5f3fa-138">Aqui está um exemplo de uma cadeia de caracteres de conexão que especifica um ponto de extremidade explícito para Olá serviço Blob:</span><span class="sxs-lookup"><span data-stu-id="5f3fa-138">Here is an example of a connection string that specifies an explicit endpoint for hello Blob service:</span></span>

```
# Blob endpoint only
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
AccountName=storagesample;
AccountKey=<account-key>
```

<span data-ttu-id="5f3fa-139">Este exemplo especifica os pontos de extremidade explícitos para todos os serviços, incluindo um domínio personalizado para Olá serviço Blob:</span><span class="sxs-lookup"><span data-stu-id="5f3fa-139">This example specifies explicit endpoints for all services, including a custom domain for hello Blob service:</span></span>

```
# All service endpoints
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
FileEndpoint=https://myaccount.file.core.windows.net;
QueueEndpoint=https://myaccount.queue.core.windows.net;
TableEndpoint=https://myaccount.table.core.windows.net;
AccountName=storagesample;
AccountKey=<account-key>
```

<span data-ttu-id="5f3fa-140">valores de ponto de extremidade de saudação em uma cadeia de conexão são usadas tooconstruct solicitação de saudação serviços de armazenamento toohello URIs e ditam formulário Olá URIs são retornados tooyour código.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-140">hello endpoint values in a connection string are used tooconstruct hello request URIs toohello storage services, and dictate hello form of any URIs that are returned tooyour code.</span></span>

<span data-ttu-id="5f3fa-141">Se você tiver mapeado um domínio personalizado do ponto de extremidade tooa de armazenamento e omite esse ponto de extremidade de uma cadeia de conexão, em seguida, você não será capaz de toouse essa conexão tooaccess de dados string nesse serviço no seu código.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-141">If you've mapped a storage endpoint tooa custom domain and omit that endpoint from a connection string, then you will not be able toouse that connection string tooaccess data in that service from your code.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5f3fa-142">Valores de ponto de extremidade de serviço em suas cadeias de conexão devem ser URIs bem formados, incluindo `https://` (recomendado) ou `http://`.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-142">Service endpoint values in your connection strings must be well-formed URIs, including `https://` (recommended) or `http://`.</span></span> <span data-ttu-id="5f3fa-143">Porque o armazenamento do Azure ainda não suporta o HTTPS para domínios personalizados, você *deve* especificar `http://` para qualquer ponto de extremidade URI que aponta o domínio personalizado tooa.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-143">Because Azure Storage does not yet support HTTPS for custom domains, you *must* specify `http://` for any endpoint URI that points tooa custom domain.</span></span>
>

### <a name="create-a-connection-string-with-an-endpoint-suffix"></a><span data-ttu-id="5f3fa-144">Criar uma cadeia de conexão com um sufixo de ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="5f3fa-144">Create a connection string with an endpoint suffix</span></span>
<span data-ttu-id="5f3fa-145">toocreate uma conexão de cadeia de caracteres para um serviço de armazenamento em regiões ou instâncias com sufixos de ponto de extremidade diferente, como do Azure na China ou Azure Government, Olá use formato de cadeia de caracteres de conexão a seguir.</span><span class="sxs-lookup"><span data-stu-id="5f3fa-145">toocreate a connection string for a storage service in regions or instances with different endpoint suffixes, such as for Azure China or Azure Government, use hello following connection string format.</span></span> <span data-ttu-id="5f3fa-146">Indique se deseja tooconnect toohello conta de armazenamento por meio de HTTPS (recomendado) ou HTTP, substitua `myAccountName` com nome de saudação da sua conta de armazenamento, substitua `myAccountKey` com sua chave de acesso da conta e substituir `mySuffix` com hello URI sufixo:</span><span class="sxs-lookup"><span data-stu-id="5f3fa-146">Indicate whether you want tooconnect toohello storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with hello name of your storage account, replace `myAccountKey` with your account access key, and replace `mySuffix` with hello URI suffix:</span></span>

```
DefaultEndpointsProtocol=[http|https];
AccountName=myAccountName;
AccountKey=myAccountKey;
EndpointSuffix=mySuffix;
```

<span data-ttu-id="5f3fa-147">Aqui está um exemplo de cadeia de conexão para serviços de armazenamento no Azure China:</span><span class="sxs-lookup"><span data-stu-id="5f3fa-147">Here's an example connection string for storage services in Azure China:</span></span>

```
DefaultEndpointsProtocol=https;
AccountName=storagesample;
AccountKey=<account-key>;
EndpointSuffix=core.chinacloudapi.cn;
```

## <a name="parsing-a-connection-string"></a><span data-ttu-id="5f3fa-148">Analisando uma cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="5f3fa-148">Parsing a connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="next-steps"></a><span data-ttu-id="5f3fa-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5f3fa-149">Next steps</span></span>
* [<span data-ttu-id="5f3fa-150">Usar o emulador de armazenamento do Azure Olá para desenvolvimento e teste</span><span class="sxs-lookup"><span data-stu-id="5f3fa-150">Use hello Azure storage emulator for development and testing</span></span>](storage-use-emulator.md)
* [<span data-ttu-id="5f3fa-151">Gerenciadores do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="5f3fa-151">Azure Storage explorers</span></span>](storage-explorers.md)
* [<span data-ttu-id="5f3fa-152">Uso de SAS (Assinaturas de Acesso Compartilhado)</span><span class="sxs-lookup"><span data-stu-id="5f3fa-152">Using Shared Access Signatures (SAS)</span></span>](storage-dotnet-shared-access-signature-part-1.md)

