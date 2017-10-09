---
title: "Olá aaaCreate um hub IoT do Azure usando a API REST do provedor de recursos | Microsoft Docs"
description: "Como toouse Olá toocreate de API REST do provedor de recursos um IoT Hub."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 52814ee5-bc10-4abe-9eb2-f8973096c2d8
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 98d240ccce47dec13a255bce28943b40f5354ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-resource-provider-rest-api-net"></a><span data-ttu-id="3c332-103">Criar um hub IoT usando o provedor de recursos de saudação REST API (.NET)</span><span class="sxs-lookup"><span data-stu-id="3c332-103">Create an IoT hub using hello resource provider REST API (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="3c332-104">Você pode usar o hello [provedor de recursos de IoT Hub API REST] [ lnk-rest-api] toocreate e gerenciar programaticamente os hubs de IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c332-104">You can use hello [IoT Hub resource provider REST API][lnk-rest-api] toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="3c332-105">Este tutorial mostra como toouse Olá toocreate de API REST de provedor de recursos de IoT Hub um hub IoT de um programa c#.</span><span class="sxs-lookup"><span data-stu-id="3c332-105">This tutorial shows you how toouse hello IoT Hub resource provider REST API toocreate an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="3c332-106">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3c332-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="3c332-107">Este artigo aborda usando o modelo de implantação do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="3c332-107">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="3c332-108">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c332-108">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="3c332-109">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="3c332-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="3c332-110">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c332-110">An active Azure account.</span></span> <br/><span data-ttu-id="3c332-111">Se não tiver uma conta, você poderá criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="3c332-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="3c332-112">[Azure PowerShell 1.0][lnk-powershell-install] ou posterior.</span><span class="sxs-lookup"><span data-stu-id="3c332-112">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="3c332-113">Preparar seu projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3c332-113">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="3c332-114">No Visual Studio, crie um projeto de Visual C# Windows clássico Desktop usando Olá **aplicativo de Console (.NET Framework)** modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="3c332-114">In Visual Studio, create a Visual C# Windows Classic Desktop project using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="3c332-115">Projeto de saudação do nome **CreateIoTHubREST**.</span><span class="sxs-lookup"><span data-stu-id="3c332-115">Name hello project **CreateIoTHubREST**.</span></span>

2. <span data-ttu-id="3c332-116">No Gerenciador de Soluções, clique com o botão direito do mouse no projeto e clique em **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="3c332-116">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="3c332-117">Verifique no Gerenciador de pacotes do NuGet, **incluir pré-lançamento**e em Olá **procurar** pesquisa de página para **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="3c332-117">In NuGet Package Manager, check **Include prerelease**, and on hello **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="3c332-118">Selecionar pacote de saudação, clique em **instalar**, na **Revise as alterações** clique em **Okey**, em seguida, clique em **aceito** tooaccept licenças de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c332-118">Select hello package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello licenses.</span></span>

4. <span data-ttu-id="3c332-119">No Gerenciador de Pacotes do NuGet, procure **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="3c332-119">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="3c332-120">Clique em **instalar**, na **Revise as alterações** clique **Okey**, em seguida, clique em **aceito** tooaccept licença de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c332-120">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello license.</span></span>

5. <span data-ttu-id="3c332-121">Em Program.cs, substituir Olá **usando** instruções com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c332-121">In Program.cs, replace hello existing **using** statements with hello following code:</span></span>

    ```csharp
    using System;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using System.Text;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Newtonsoft.Json;
    using Microsoft.Rest;
    using System.Linq;
    using System.Threading;
    ```

6. <span data-ttu-id="3c332-122">Em Program.cs, adicione Olá variáveis estáticas, substituindo os valores de espaço reservado Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="3c332-122">In Program.cs, add hello following static variables replacing hello placeholder values.</span></span> <span data-ttu-id="3c332-123">Você fez uma anotação de **ApplicationId**, **SubscriptionId**, **TenantId** e **Password** anteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="3c332-123">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="3c332-124">**Nome do grupo de recursos** é Olá nome do grupo de recursos de saudação usar ao criar hello IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3c332-124">**Resource group name** is hello name of hello resource group you use when you create hello IoT hub.</span></span> <span data-ttu-id="3c332-125">Use um grupo de recursos existente ou novo.</span><span class="sxs-lookup"><span data-stu-id="3c332-125">You can use a pre-existing or a new resource group.</span></span> <span data-ttu-id="3c332-126">**Nome do IoT Hub** é nome de saudação do hello IoT Hub cria, tais como **MyIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="3c332-126">**IoT Hub name** is hello name of hello IoT Hub you create, such as **MyIoTHub**.</span></span> <span data-ttu-id="3c332-127">nome de saudação do seu hub IoT deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="3c332-127">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="3c332-128">**Nome da implantação** é um nome para a implantação de saudação, como **Deployment_01**.</span><span class="sxs-lookup"><span data-stu-id="3c332-128">**Deployment name** is a name for hello deployment, such as **Deployment_01**.</span></span>

    ```csharp
    static string applicationId = "{Your ApplicationId}";
    static string subscriptionId = "{Your SubscriptionId}";
    static string tenantId = "{Your TenantId}";
    static string password = "{Your application Password}";

    static string rgName = "{Resource group name}";
    static string iotHubName = "{IoT Hub name including your initials}";
    ```
[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

[!INCLUDE [iot-hub-get-access-token](../../includes/iot-hub-get-access-token.md)]

## <a name="use-hello-resource-provider-rest-api-toocreate-an-iot-hub"></a><span data-ttu-id="3c332-129">Use Olá recurso provedor API REST toocreate um hub IoT</span><span class="sxs-lookup"><span data-stu-id="3c332-129">Use hello resource provider REST API toocreate an IoT hub</span></span>

<span data-ttu-id="3c332-130">Saudação de uso [provedor de recursos de IoT Hub API REST] [ lnk-rest-api] toocreate um hub IoT em seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3c332-130">Use hello [IoT Hub resource provider REST API][lnk-rest-api] toocreate an IoT hub in your resource group.</span></span> <span data-ttu-id="3c332-131">Você também pode usar o hello recurso provedor API REST toomake alterações tooan IoT hub existente.</span><span class="sxs-lookup"><span data-stu-id="3c332-131">You can also use hello resource provider REST API toomake changes tooan existing IoT hub.</span></span>

1. <span data-ttu-id="3c332-132">Adicione Olá tooProgram.cs do método a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c332-132">Add hello following method tooProgram.cs:</span></span>

    ```csharp
    static void CreateIoTHub(string token)
    {

    }
    ```

2. <span data-ttu-id="3c332-133">Adicionar Olá toohello de código a seguir **CreateIoTHub** método.</span><span class="sxs-lookup"><span data-stu-id="3c332-133">Add hello following code toohello **CreateIoTHub** method.</span></span> <span data-ttu-id="3c332-134">Esse código cria um **HttpClient** objeto com o token de autenticação Olá nos cabeçalhos de saudação:</span><span class="sxs-lookup"><span data-stu-id="3c332-134">This code creates an **HttpClient** object with hello authentication token in hello headers:</span></span>

    ```csharp
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    ```

3. <span data-ttu-id="3c332-135">Adicionar Olá toohello de código a seguir **CreateIoTHub** método.</span><span class="sxs-lookup"><span data-stu-id="3c332-135">Add hello following code toohello **CreateIoTHub** method.</span></span> <span data-ttu-id="3c332-136">Esse código descreve Olá IoT hub toocreate e gera uma representação JSON.</span><span class="sxs-lookup"><span data-stu-id="3c332-136">This code describes hello IoT hub toocreate and generates a JSON representation.</span></span> <span data-ttu-id="3c332-137">Para obter a lista atual Olá locais que dão suporte ao IoT Hub consulte [Status do Azure][lnk-status]:</span><span class="sxs-lookup"><span data-stu-id="3c332-137">For hello current list of locations that support IoT Hub see [Azure Status][lnk-status]:</span></span>

    ```csharp
    var description = new
    {
      name = iotHubName,
      location = "East US",
      sku = new
      {
        name = "S1",
        tier = "Standard",
        capacity = 1
      }
    };

    var json = JsonConvert.SerializeObject(description, Formatting.Indented);
    ```

4. <span data-ttu-id="3c332-138">Adicionar Olá toohello de código a seguir **CreateIoTHub** método.</span><span class="sxs-lookup"><span data-stu-id="3c332-138">Add hello following code toohello **CreateIoTHub** method.</span></span> <span data-ttu-id="3c332-139">Esse código envia Olá REST solicitação tooAzure.</span><span class="sxs-lookup"><span data-stu-id="3c332-139">This code submits hello REST request tooAzure.</span></span> <span data-ttu-id="3c332-140">Olá código verifica a resposta hello e recupera a URL de hello, você pode usar toomonitor Olá estado da tarefa de implantação de saudação:</span><span class="sxs-lookup"><span data-stu-id="3c332-140">hello code then checks hello response and retrieves hello URL you can use toomonitor hello state of hello deployment task:</span></span>

    ```csharp
    var content = new StringContent(JsonConvert.SerializeObject(description), Encoding.UTF8, "application/json");
    var requestUri = string.Format("https://management.azure.com/subscriptions/{0}/resourcegroups/{1}/providers/Microsoft.devices/IotHubs/{2}?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var result = client.PutAsync(requestUri, content).Result;

    if (!result.IsSuccessStatusCode)
    {
      Console.WriteLine("Failed {0}", result.Content.ReadAsStringAsync().Result);
      return;
    }

    var asyncStatusUri = result.Headers.GetValues("Azure-AsyncOperation").First();
    ```

5. <span data-ttu-id="3c332-141">Adicionar Olá após o final do código toohello de saudação **CreateIoTHub** método.</span><span class="sxs-lookup"><span data-stu-id="3c332-141">Add hello following code toohello end of hello **CreateIoTHub** method.</span></span> <span data-ttu-id="3c332-142">Esse código usa Olá **asyncStatusUri** endereço recuperado em Olá toowait de etapa anterior para Olá toocomplete de implantação:</span><span class="sxs-lookup"><span data-stu-id="3c332-142">This code uses hello **asyncStatusUri** address retrieved in hello previous step toowait for hello deployment toocomplete:</span></span>

    ```csharp
    string body;
    do
    {
      Thread.Sleep(10000);
      HttpResponseMessage deploymentstatus = client.GetAsync(asyncStatusUri).Result;
      body = deploymentstatus.Content.ReadAsStringAsync().Result;
    } while (body == "{\"status\":\"Running\"}");
    ```

6. <span data-ttu-id="3c332-143">Adicionar Olá após o final do código toohello de saudação **CreateIoTHub** método.</span><span class="sxs-lookup"><span data-stu-id="3c332-143">Add hello following code toohello end of hello **CreateIoTHub** method.</span></span> <span data-ttu-id="3c332-144">Este código recupera as chaves de saudação do hello hub IoT, você criou e imprime toohello console:</span><span class="sxs-lookup"><span data-stu-id="3c332-144">This code retrieves hello keys of hello IoT hub you created and prints them toohello console:</span></span>

    ```csharp
    var listKeysUri = string.Format("https://management.azure.com/subscriptions/{0}/resourceGroups/{1}/providers/Microsoft.Devices/IotHubs/{2}/IoTHubKeys/listkeys?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var keysresults = client.PostAsync(listKeysUri, null).Result;

    Console.WriteLine("Keys: {0}", keysresults.Content.ReadAsStringAsync().Result);
    ```

## <a name="complete-and-run-hello-application"></a><span data-ttu-id="3c332-145">Aplicativo hello completa e execução</span><span class="sxs-lookup"><span data-stu-id="3c332-145">Complete and run hello application</span></span>

<span data-ttu-id="3c332-146">Agora você pode concluir aplicativo hello Olá chamada **CreateIoTHub** método antes de compilar e executá-lo.</span><span class="sxs-lookup"><span data-stu-id="3c332-146">You can now complete hello application by calling hello **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="3c332-147">Adicionar Olá após o final do código toohello de saudação **principal** método:</span><span class="sxs-lookup"><span data-stu-id="3c332-147">Add hello following code toohello end of hello **Main** method:</span></span>

    ```csharp
    CreateIoTHub(token.AccessToken);
    Console.ReadLine();
    ```

2. <span data-ttu-id="3c332-148">Clique em **Criar** e **Compilar Solução**.</span><span class="sxs-lookup"><span data-stu-id="3c332-148">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="3c332-149">Corrija todos os erros.</span><span class="sxs-lookup"><span data-stu-id="3c332-149">Correct any errors.</span></span>

3. <span data-ttu-id="3c332-150">Clique em **depurar** e **iniciar depuração** aplicativo hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="3c332-150">Click **Debug** and then **Start Debugging** toorun hello application.</span></span> <span data-ttu-id="3c332-151">Ele pode levar vários minutos para Olá toorun de implantação.</span><span class="sxs-lookup"><span data-stu-id="3c332-151">It may take several minutes for hello deployment toorun.</span></span>

4. <span data-ttu-id="3c332-152">tooverify que seu aplicativo adicionado Olá novo hub IoT, visite Olá [portal do Azure] [ lnk-azure-portal] e exibir a lista de recursos.</span><span class="sxs-lookup"><span data-stu-id="3c332-152">tooverify that your application added hello new IoT hub, visit hello [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="3c332-153">Como alternativa, use Olá **Get-AzureRmResource** cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3c332-153">Alternatively, use hello **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="3c332-154">Este aplicativo de exemplo adiciona um Hub IoT Standard S1 pelo qual você será cobrado.</span><span class="sxs-lookup"><span data-stu-id="3c332-154">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="3c332-155">Quando tiver terminado, você pode excluir o hub IoT de saudação por meio de saudação [portal do Azure] [ lnk-azure-portal] ou usando Olá **Remove-AzureRmResource** cmdlet do PowerShell quando tiver terminado.</span><span class="sxs-lookup"><span data-stu-id="3c332-155">When you are finished, you can delete hello IoT hub through hello [Azure portal][lnk-azure-portal] or by using hello **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c332-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3c332-156">Next steps</span></span>
<span data-ttu-id="3c332-157">Agora que você implantou um hub IoT usando o provedor de recursos de saudação API REST, você poderá desejar tooexplore adicional:</span><span class="sxs-lookup"><span data-stu-id="3c332-157">Now you have deployed an IoT hub using hello resource provider REST API, you may want tooexplore further:</span></span>

* <span data-ttu-id="3c332-158">Leia sobre os recursos de saudação do hello [provedor de recursos de IoT Hub API REST][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="3c332-158">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="3c332-159">Leitura [visão geral do Gerenciador de recursos do Azure] [ lnk-azure-rm-overview] toolearn mais sobre os recursos de saudação do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c332-159">Read [Azure Resource Manager overview][lnk-azure-rm-overview] toolearn more about hello capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="3c332-160">toolearn mais sobre como desenvolver para o IoT Hub, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c332-160">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="3c332-161">[Introdução tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="3c332-161">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="3c332-162">[SDKs do Azure IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="3c332-162">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="3c332-163">toofurther explorar recursos de saudação do IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="3c332-163">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="3c332-164">[Simulando um dispositivo com Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="3c332-164">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
