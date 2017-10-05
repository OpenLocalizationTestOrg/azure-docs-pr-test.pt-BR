---
title: Criar um Hub IoT do Azure usando a API REST do provedor de recursos | Microsoft Docs
description: Como usar a API REST do provedor de recursos para criar um Hub IoT.
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
ms.openlocfilehash: e443259507aacbefca141be4c9c1688ab19bf6ec
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-iot-hub-using-the-resource-provider-rest-api-net"></a><span data-ttu-id="941ef-103">Criar um Hub IoT usando a API REST do provedor de recursos (.NET)</span><span class="sxs-lookup"><span data-stu-id="941ef-103">Create an IoT hub using the resource provider REST API (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="941ef-104">Você pode usar a [API REST do provedor de recursos do Hub IoT][lnk-rest-api] para criar e gerenciar Hubs IoT do Azure de forma programática.</span><span class="sxs-lookup"><span data-stu-id="941ef-104">You can use the [IoT Hub resource provider REST API][lnk-rest-api] to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="941ef-105">Este tutorial mostra como usar a API de REST do Provedor de Recursos de Hub do IoT para criar um hub IoT a partir de um programa C#.</span><span class="sxs-lookup"><span data-stu-id="941ef-105">This tutorial shows you how to use the IoT Hub resource provider REST API to create an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="941ef-106">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="941ef-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="941ef-107">Este artigo aborda o uso do modelo de implantação do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="941ef-107">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="941ef-108">Para concluir este tutorial, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="941ef-108">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="941ef-109">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="941ef-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="941ef-110">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="941ef-110">An active Azure account.</span></span> <br/><span data-ttu-id="941ef-111">Se não tiver uma conta, você poderá criar uma [conta gratuita][lnk-free-trial] em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="941ef-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="941ef-112">[Azure PowerShell 1.0][lnk-powershell-install] ou posterior.</span><span class="sxs-lookup"><span data-stu-id="941ef-112">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="941ef-113">Preparar seu projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="941ef-113">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="941ef-114">No Visual Studio, adicione um projeto da Área de Trabalho Clássica do Windows no Visual C# usando o modelo de projeto **Aplicativo do Console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="941ef-114">In Visual Studio, create a Visual C# Windows Classic Desktop project using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="941ef-115">Nomeie o projeto **CreateIoTHubREST**.</span><span class="sxs-lookup"><span data-stu-id="941ef-115">Name the project **CreateIoTHubREST**.</span></span>

2. <span data-ttu-id="941ef-116">No Gerenciador de Soluções, clique com o botão direito do mouse no projeto e clique em **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="941ef-116">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="941ef-117">No Gerenciador de Pacotes NuGet, marque **Incluir pré-lançamento** e na página **Navegar** procure **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="941ef-117">In NuGet Package Manager, check **Include prerelease**, and on the **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="941ef-118">Selecione o pacote, clique em **Instalar**, em **Revisar alterações** clique em **OK** e em **Aceito** para aceitar as licenças.</span><span class="sxs-lookup"><span data-stu-id="941ef-118">Select the package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the licenses.</span></span>

4. <span data-ttu-id="941ef-119">No Gerenciador de Pacotes do NuGet, procure **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="941ef-119">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="941ef-120">Clique em **Instalar**, em **Revisar alterações**, clique em **OK** e em **Aceito** para aceitar a licença.</span><span class="sxs-lookup"><span data-stu-id="941ef-120">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the license.</span></span>

5. <span data-ttu-id="941ef-121">Em Program.cs, substitua as instruções **using** existentes pelo código a seguir:</span><span class="sxs-lookup"><span data-stu-id="941ef-121">In Program.cs, replace the existing **using** statements with the following code:</span></span>

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

6. <span data-ttu-id="941ef-122">Em Program.cs, adicione as variáveis estáticas a seguir, substituindo os valores de espaço reservado.</span><span class="sxs-lookup"><span data-stu-id="941ef-122">In Program.cs, add the following static variables replacing the placeholder values.</span></span> <span data-ttu-id="941ef-123">Você fez uma anotação de **ApplicationId**, **SubscriptionId**, **TenantId** e **Password** anteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="941ef-123">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="941ef-124">**Nome do grupo de recursos** é o nome do grupo de recursos que você usa ao criar o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="941ef-124">**Resource group name** is the name of the resource group you use when you create the IoT hub.</span></span> <span data-ttu-id="941ef-125">Use um grupo de recursos existente ou novo.</span><span class="sxs-lookup"><span data-stu-id="941ef-125">You can use a pre-existing or a new resource group.</span></span> <span data-ttu-id="941ef-126">**Nome do Hub IoT** é o nome do Hub IoT que você criou, como **MyIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="941ef-126">**IoT Hub name** is the name of the IoT Hub you create, such as **MyIoTHub**.</span></span> <span data-ttu-id="941ef-127">O nome do hub IoT deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="941ef-127">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="941ef-128">**Nome da implantação** é um nome para a implantação, como **Deployment_01**.</span><span class="sxs-lookup"><span data-stu-id="941ef-128">**Deployment name** is a name for the deployment, such as **Deployment_01**.</span></span>

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

## <a name="use-the-resource-provider-rest-api-to-create-an-iot-hub"></a><span data-ttu-id="941ef-129">Use a API REST do provedor de recursos para criar um Hub IoT</span><span class="sxs-lookup"><span data-stu-id="941ef-129">Use the resource provider REST API to create an IoT hub</span></span>

<span data-ttu-id="941ef-130">Use a [API REST do provedor de recursos do Hub IoT][lnk-rest-api] para criar um novo Hub IoT em seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="941ef-130">Use the [IoT Hub resource provider REST API][lnk-rest-api] to create an IoT hub in your resource group.</span></span> <span data-ttu-id="941ef-131">Você também pode usar a API REST do provedor de recursos para fazer alterações em um Hub IoT existente.</span><span class="sxs-lookup"><span data-stu-id="941ef-131">You can also use the resource provider REST API to make changes to an existing IoT hub.</span></span>

1. <span data-ttu-id="941ef-132">Adicione o seguinte método ao Program.cs:</span><span class="sxs-lookup"><span data-stu-id="941ef-132">Add the following method to Program.cs:</span></span>

    ```csharp
    static void CreateIoTHub(string token)
    {

    }
    ```

2. <span data-ttu-id="941ef-133">Adicione o seguinte código ao método **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="941ef-133">Add the following code to the **CreateIoTHub** method.</span></span> <span data-ttu-id="941ef-134">Esse código cria um objeto **HttpClient** com o token de autenticação nos cabeçalhos:</span><span class="sxs-lookup"><span data-stu-id="941ef-134">This code creates an **HttpClient** object with the authentication token in the headers:</span></span>

    ```csharp
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    ```

3. <span data-ttu-id="941ef-135">Adicione o seguinte código ao método **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="941ef-135">Add the following code to the **CreateIoTHub** method.</span></span> <span data-ttu-id="941ef-136">Esse código descreve o Hub IoT a ser criado e gera uma representação JSON.</span><span class="sxs-lookup"><span data-stu-id="941ef-136">This code describes the IoT hub to create and generates a JSON representation.</span></span> <span data-ttu-id="941ef-137">Para obter a lista atual de localizações que dão suporte ao Hub IoT, confira o [Status do Azure][lnk-status]:</span><span class="sxs-lookup"><span data-stu-id="941ef-137">For the current list of locations that support IoT Hub see [Azure Status][lnk-status]:</span></span>

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

4. <span data-ttu-id="941ef-138">Adicione o seguinte código ao método **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="941ef-138">Add the following code to the **CreateIoTHub** method.</span></span> <span data-ttu-id="941ef-139">Esse código envia a solicitação REST ao Azure.</span><span class="sxs-lookup"><span data-stu-id="941ef-139">This code submits the REST request to Azure.</span></span> <span data-ttu-id="941ef-140">Em seguida, o código verifica a resposta e recupera a URL, que você pode usar para monitorar o estado da tarefa de implantação:</span><span class="sxs-lookup"><span data-stu-id="941ef-140">The code then checks the response and retrieves the URL you can use to monitor the state of the deployment task:</span></span>

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

5. <span data-ttu-id="941ef-141">Adicione o código a seguir ao final do método **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="941ef-141">Add the following code to the end of the **CreateIoTHub** method.</span></span> <span data-ttu-id="941ef-142">Esse código usa o endereço **asyncStatusUri** recuperado na etapa anterior para aguardar a conclusão da implantação:</span><span class="sxs-lookup"><span data-stu-id="941ef-142">This code uses the **asyncStatusUri** address retrieved in the previous step to wait for the deployment to complete:</span></span>

    ```csharp
    string body;
    do
    {
      Thread.Sleep(10000);
      HttpResponseMessage deploymentstatus = client.GetAsync(asyncStatusUri).Result;
      body = deploymentstatus.Content.ReadAsStringAsync().Result;
    } while (body == "{\"status\":\"Running\"}");
    ```

6. <span data-ttu-id="941ef-143">Adicione o código a seguir ao final do método **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="941ef-143">Add the following code to the end of the **CreateIoTHub** method.</span></span> <span data-ttu-id="941ef-144">Este código recupera as chaves do Hub IoT criadas e impressas no console:</span><span class="sxs-lookup"><span data-stu-id="941ef-144">This code retrieves the keys of the IoT hub you created and prints them to the console:</span></span>

    ```csharp
    var listKeysUri = string.Format("https://management.azure.com/subscriptions/{0}/resourceGroups/{1}/providers/Microsoft.Devices/IotHubs/{2}/IoTHubKeys/listkeys?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var keysresults = client.PostAsync(listKeysUri, null).Result;

    Console.WriteLine("Keys: {0}", keysresults.Content.ReadAsStringAsync().Result);
    ```

## <a name="complete-and-run-the-application"></a><span data-ttu-id="941ef-145">Compilar e executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="941ef-145">Complete and run the application</span></span>

<span data-ttu-id="941ef-146">Agora, você pode concluir o aplicativo chamando o método **CreateIoTHub** antes de compilá-lo e de executá-lo.</span><span class="sxs-lookup"><span data-stu-id="941ef-146">You can now complete the application by calling the **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="941ef-147">Adicione o seguinte código ao final do método **Main** :</span><span class="sxs-lookup"><span data-stu-id="941ef-147">Add the following code to the end of the **Main** method:</span></span>

    ```csharp
    CreateIoTHub(token.AccessToken);
    Console.ReadLine();
    ```

2. <span data-ttu-id="941ef-148">Clique em **Criar** e **Compilar Solução**.</span><span class="sxs-lookup"><span data-stu-id="941ef-148">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="941ef-149">Corrija todos os erros.</span><span class="sxs-lookup"><span data-stu-id="941ef-149">Correct any errors.</span></span>

3. <span data-ttu-id="941ef-150">Clique em **Depurar** e, em seguida, **Iniciar Depuração** para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="941ef-150">Click **Debug** and then **Start Debugging** to run the application.</span></span> <span data-ttu-id="941ef-151">Pode levar vários minutos para que a implantação seja executada.</span><span class="sxs-lookup"><span data-stu-id="941ef-151">It may take several minutes for the deployment to run.</span></span>

4. <span data-ttu-id="941ef-152">Para verificar seu aplicativo adicionado ao novo hub IoT, visite o [Portal do Azure][lnk-azure-portal] e exiba sua lista de recursos.</span><span class="sxs-lookup"><span data-stu-id="941ef-152">To verify that your application added the new IoT hub, visit the [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="941ef-153">Como alternativa, use o cmdlet **Get-AzureRmResource** do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="941ef-153">Alternatively, use the **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="941ef-154">Este aplicativo de exemplo adiciona um Hub IoT Standard S1 pelo qual você será cobrado.</span><span class="sxs-lookup"><span data-stu-id="941ef-154">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="941ef-155">Ao concluir, é possível excluir o Hub IoT por meio do [portal do Azure][lnk-azure-portal] ou usando o cmdlet **Remove-AzureRmResource** do PowerShell quando tiver terminado.</span><span class="sxs-lookup"><span data-stu-id="941ef-155">When you are finished, you can delete the IoT hub through the [Azure portal][lnk-azure-portal] or by using the **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="941ef-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="941ef-156">Next steps</span></span>
<span data-ttu-id="941ef-157">Agora que você implantou um Hub IoT usando a API REST do provedor de recursos, convém explorar ainda mais:</span><span class="sxs-lookup"><span data-stu-id="941ef-157">Now you have deployed an IoT hub using the resource provider REST API, you may want to explore further:</span></span>

* <span data-ttu-id="941ef-158">Leia sobre as funcionalidades da [API REST do provedor de recursos Hub IoT][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="941ef-158">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="941ef-159">Leia a [Visão geral do Azure Resource Manager][lnk-azure-rm-overview] para saber mais sobre os recursos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="941ef-159">Read [Azure Resource Manager overview][lnk-azure-rm-overview] to learn more about the capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="941ef-160">Para saber mais sobre como desenvolver para o Hub IoT, veja os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="941ef-160">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="941ef-161">[Introdução ao SDK de C][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="941ef-161">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="941ef-162">[SDKs do Azure IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="941ef-162">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="941ef-163">Para explorar melhor as funcionalidades do Hub IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="941ef-163">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="941ef-164">[Simulando um dispositivo com Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="941ef-164">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
