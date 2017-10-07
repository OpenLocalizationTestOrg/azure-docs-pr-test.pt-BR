---
title: "aaaCreate um módulo do Azure IoT borda com c# | Microsoft Docs"
description: "Este tutorial mostra como toowrite uma BELA dados conversor usando módulo Olá pacotes NuGet do Azure IoT borda mais recentes, código do Visual Studio e c#."
services: iot-hub
author: jeffreyCline
manager: timlt
keywords: azure, iot, tutorial, module, nuget, vscode, csharp, edge
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: jcline
ms.openlocfilehash: b104609c05d1613e21acc7d7bed547f311179151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-cx23"></a><span data-ttu-id="85285-104">Criar um módulo do Azure IoT Edge com o C&#x23;</span><span class="sxs-lookup"><span data-stu-id="85285-104">Create an Azure IoT Edge Module with C&#x23;</span></span>

<span data-ttu-id="85285-105">Este tutorial mostra como toocreate um módulo para `Azure IoT Edge` usando `Visual Studio Code` e `C#`.</span><span class="sxs-lookup"><span data-stu-id="85285-105">This tutorial showcases how toocreate a module for `Azure IoT Edge` using `Visual Studio Code` and `C#`.</span></span>

<span data-ttu-id="85285-106">Neste tutorial, nós o conduziremos por meio da configuração do ambiente e como toowrite uma [Bilitar](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) módulo de conversor de dados usando hello mais recente `Azure IoT Edge NuGet` pacotes.</span><span class="sxs-lookup"><span data-stu-id="85285-106">In this tutorial, we walk through environment set-up and how toowrite a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using hello latest `Azure IoT Edge NuGet` packages.</span></span> 

>[!NOTE]
<span data-ttu-id="85285-107">Este tutorial está usando Olá `.NET Core SDK`, que oferece suporte a compatibilidade de plataforma cruzada.</span><span class="sxs-lookup"><span data-stu-id="85285-107">This tutorial is using hello `.NET Core SDK`, which supports cross-platform compatibility.</span></span> <span data-ttu-id="85285-108">Olá tutorial a seguir é gravado usando Olá `Windows 10` sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="85285-108">hello following tutorial is written using hello `Windows 10` operating system.</span></span> <span data-ttu-id="85285-109">Alguns comandos de saudação neste tutorial podem ser diferente dependendo de sua `development environment`.</span><span class="sxs-lookup"><span data-stu-id="85285-109">Some of hello commands in this tutorial may be different depending on your `development environment`.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="85285-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="85285-110">Prerequisites</span></span>

<span data-ttu-id="85285-111">Nesta seção, você configura o ambiente para o desenvolvimento de módulos do `Azure IoT Edge`.</span><span class="sxs-lookup"><span data-stu-id="85285-111">In this section, we set-up your environment for `Azure IoT Edge` module development.</span></span> <span data-ttu-id="85285-112">Aplica-se tooboth **Windows de 64 bits** e **Linux de 64 bits (8 Ubuntu/Debian)** sistemas operacionais.</span><span class="sxs-lookup"><span data-stu-id="85285-112">It applies tooboth **64-bit Windows** and **64-bit Linux (Ubuntu/Debian 8)** operating systems.</span></span>

<span data-ttu-id="85285-113">saudação de software a seguir é necessária:</span><span class="sxs-lookup"><span data-stu-id="85285-113">hello following software is required:</span></span>

- [<span data-ttu-id="85285-114">Cliente Git</span><span class="sxs-lookup"><span data-stu-id="85285-114">Git Client</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="85285-115">SDK do .NET Core</span><span class="sxs-lookup"><span data-stu-id="85285-115">.NET Core SDK</span></span>](https://www.microsoft.com/net/core#windowscmd)
- [<span data-ttu-id="85285-116">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="85285-116">Visual Studio Code</span></span>](https://code.visualstudio.com/)

<span data-ttu-id="85285-117">Repositório de saudação tooclone não é necessário para este exemplo, no entanto todos Olá discutido neste tutorial do código de exemplo está localizado na Olá repositório a seguir:</span><span class="sxs-lookup"><span data-stu-id="85285-117">You do not need tooclone hello repo for this sample, however all of hello sample code discussed in this tutorial is located in hello following repository:</span></span>

- <span data-ttu-id="85285-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span><span class="sxs-lookup"><span data-stu-id="85285-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
- `cd iot-edge-samples/dotnetcore/simulated_ble`

## <a name="getting-started"></a><span data-ttu-id="85285-119">Introdução</span><span class="sxs-lookup"><span data-stu-id="85285-119">Getting started</span></span>

1. <span data-ttu-id="85285-120">Instalar `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="85285-120">Install `.NET Core SDK`.</span></span>
2. <span data-ttu-id="85285-121">Instalar `Visual Studio Code` e hello `C# extension` de saudação Marketplace de código do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="85285-121">Install `Visual Studio Code` and hello `C# extension` from hello Visual Studio Code Marketplace.</span></span>

<span data-ttu-id="85285-122">Exibir este [rápido tutorial em vídeo](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) sobre como tooget iniciado usando `Visual Studio Code` e hello `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="85285-122">View this [quick video tutorial](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) about how tooget started using `Visual Studio Code` and hello `.NET Core SDK`.</span></span>

## <a name="creating-hello-azure-iot-edge-converter-module"></a><span data-ttu-id="85285-123">Criando o módulo de conversor de Azure IoT borda Olá</span><span class="sxs-lookup"><span data-stu-id="85285-123">Creating hello Azure IoT Edge converter module</span></span>

1. <span data-ttu-id="85285-124">Inicializar um novo projeto C# da biblioteca de classes `.NET Core`:</span><span class="sxs-lookup"><span data-stu-id="85285-124">Initialize a new `.NET Core` class library C# project:</span></span>
    - <span data-ttu-id="85285-125">Abra um prompt de comando (`Windows + R` -> `cmd` -> `enter`).</span><span class="sxs-lookup"><span data-stu-id="85285-125">Open a command prompt (`Windows + R` -> `cmd` -> `enter`).</span></span>
    - <span data-ttu-id="85285-126">Navegue toohello pasta em que você deseja toocreate Olá `C#` projeto.</span><span class="sxs-lookup"><span data-stu-id="85285-126">Navigate toohello folder where you'd like toocreate hello `C#` project.</span></span>
    - <span data-ttu-id="85285-127">Digite **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span><span class="sxs-lookup"><span data-stu-id="85285-127">Type **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span></span> 
    - <span data-ttu-id="85285-128">Este comando cria uma classe vazia chamada `Class1.cs` em seu diretório de projetos.</span><span class="sxs-lookup"><span data-stu-id="85285-128">This command creates an empty class called `Class1.cs` in your projects directory.</span></span>
2. <span data-ttu-id="85285-129">Navegue toohello pasta em que acabamos de criar o projeto de biblioteca de classes Olá digitando **cd IoTEdgeConverterModule**.</span><span class="sxs-lookup"><span data-stu-id="85285-129">Navigate toohello folder where we just created hello class library project by typing **cd IoTEdgeConverterModule**.</span></span>
3. <span data-ttu-id="85285-130">Projeto aberto Olá no `Visual Studio Code` digitando **código.**.</span><span class="sxs-lookup"><span data-stu-id="85285-130">Open hello project in `Visual Studio Code` by typing **code .**.</span></span>
4. <span data-ttu-id="85285-131">Depois que o projeto Olá é aberto no `Visual Studio Code`, clique em Olá **IoTEdgeConverterModule.csproj** arquivo de saudação tooopen conforme mostrado no Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="85285-131">Once hello project is opened in `Visual Studio Code`, click on hello **IoTEdgeConverterModule.csproj** tooopen hello file as shown in hello following image:</span></span>

    ![Janela de edição do Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-edit-csproj.png)

5. <span data-ttu-id="85285-133">Inserir saudação `XML` blob mostrado no hello trecho de código a seguir entre fechamento Olá `PropertyGroup` marca e Olá fechando `Project` marca; linha seis em Olá anterior a imagem e salve o arquivo de saudação pressionando `Ctrl`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="85285-133">Insert hello `XML` blob shown in hello following code snippet between hello closing `PropertyGroup` tag and hello closing `Project` tag; line six in hello preceding image and save hello file by pressing `Ctrl` + `S`.</span></span>

   ```xml
     <ItemGroup>
       <PackageReference Include="Microsoft.Azure.Devices.Gateway.Module.NetStandard" Version="1.0.5" />
       <PackageReference Include="System.Threading.Thread" Version="4.3.0" />
       <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
     </ItemGroup> 
   ```

6. <span data-ttu-id="85285-134">Depois de salvar Olá `.csproj` arquivo, `Visual Studio Code` exibirá a um `unresolved dependencies` diálogo visto Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="85285-134">Once you save hello `.csproj` file, `Visual Studio Code` should prompt you with an `unresolved dependencies` dialog as seen in hello following image:</span></span> 

    ![Caixa de diálogo de dependências de restauração do Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-restore.png)

    <span data-ttu-id="85285-136">a) clique `Restore` toorestore todos Olá referências em projetos de saudação `.csproj` arquivo incluindo Olá `PackageReferences` adicionamos.</span><span class="sxs-lookup"><span data-stu-id="85285-136">a) Click `Restore` toorestore all of hello references in hello projects `.csproj` file including hello `PackageReferences` we have added.</span></span> 

    <span data-ttu-id="85285-137">b) `Visual Studio Code` cria automaticamente Olá `project.assets.json` arquivo em seus projetos `obj` pasta.</span><span class="sxs-lookup"><span data-stu-id="85285-137">b) `Visual Studio Code` automatically creates hello `project.assets.json` file in your projects `obj` folder.</span></span> <span data-ttu-id="85285-138">Esse arquivo contém informações sobre dependências toomake subsequentes restaurações seu projeto mais rápidas.</span><span class="sxs-lookup"><span data-stu-id="85285-138">This file contains information about your project's dependencies toomake subsequent restores quicker.</span></span>
 
    >[!NOTE]
    <span data-ttu-id="85285-139">`.NET Core Tools` agora são baseadas em MSBuild.</span><span class="sxs-lookup"><span data-stu-id="85285-139">`.NET Core Tools` are now MSBuild-based.</span></span> <span data-ttu-id="85285-140">O que significa que um arquivo de projeto `.csproj` é criado, em vez de um `project.json`.</span><span class="sxs-lookup"><span data-stu-id="85285-140">Which means a `.csproj` project file is created instead of a `project.json`.</span></span>

    - <span data-ttu-id="85285-141">Se `Visual Studio Code` não solicita a você se está ok, podemos fazer isso manualmente.</span><span class="sxs-lookup"><span data-stu-id="85285-141">If `Visual Studio Code` does not prompt you that is ok, we can do it manually.</span></span> <span data-ttu-id="85285-142">Olá abrir `Visual Studio Code` janela do terminal integrada por pressionando Olá `Ctrl`  +  `backtick` chaves ou usando menus de saudação `View`  ->  `Integrated Terminal`.</span><span class="sxs-lookup"><span data-stu-id="85285-142">Open hello `Visual Studio Code` integrated terminal window by pressing hello `Ctrl` + `backtick` keys or using hello menus `View` -> `Integrated Terminal`.</span></span>
    - <span data-ttu-id="85285-143">Em Olá `Integrated Terminal` tipo de janela **restauração dotnet**.</span><span class="sxs-lookup"><span data-stu-id="85285-143">In hello `Integrated Terminal` window type **dotnet restore**.</span></span>
    
7. <span data-ttu-id="85285-144">Renomear Olá `Class1.cs` arquivo muito`BleConverterModule.cs`.</span><span class="sxs-lookup"><span data-stu-id="85285-144">Rename hello `Class1.cs` file too`BleConverterModule.cs`.</span></span> 

    <span data-ttu-id="85285-145">a) arquivo de saudação toorename primeiro clique no arquivo hello e pressione Olá `F2` chave.</span><span class="sxs-lookup"><span data-stu-id="85285-145">a) toorename hello file first click on hello file then press hello `F2` key.</span></span>
    
    <span data-ttu-id="85285-146">b) digite Olá novo nome **BleConverterModule**, como visto no Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="85285-146">b) Type in hello new name **BleConverterModule**, as seen in hello following image:</span></span>

    ![Visual Studio Code renomeando uma classe](media/iot-hub-iot-edge-create-module/vscode-rename.png)

8. <span data-ttu-id="85285-148">Substitua o código existente Olá Olá `BleConverterModule.cs` arquivo copiando e colando Olá seguindo o trecho de código em seu `BleConverterModule.cs` arquivo.</span><span class="sxs-lookup"><span data-stu-id="85285-148">Replace hello existing code in hello `BleConverterModule.cs` file by copying and pasting hello following code snippet into your `BleConverterModule.cs` file.</span></span>

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Globalization;
   using System.Linq;
   using System.Text;
   using System.Threading;
   using System.Threading.Tasks;
   using Microsoft.Azure.Devices.Gateway;
   using Newtonsoft.Json;
   
   namespace IoTEdgeConverterModule
   {
       public class BleConverterModule : IGatewayModule, IGatewayModuleStart
       {
           private Broker broker;
           private string configuration;
           private int messageCount;

           public void Create(Broker broker, byte[] configuration)
           {
               this.broker = broker;
               this.configuration = System.Text.Encoding.UTF8.GetString(configuration);
           }
   
           public void Start()
           {
           }

           public void Destroy()
           {
           }

           public void Receive(Message received_message)
           {
               string recMsg = Encoding.UTF8.GetString(received_message.Content, 0, received_message.Content.Length);
               BleData receivedData = JsonConvert.DeserializeObject<BleData>(recMsg);

               float temperature = float.Parse(receivedData.Temperature, CultureInfo.InvariantCulture.NumberFormat); 
               Dictionary<string, string> receivedProperties = received_message.Properties;
            
               Dictionary<string, string> properties = new Dictionary<string, string>();
               properties.Add("source", receivedProperties["source"]);
               properties.Add("macAddress", receivedProperties["macAddress"]);
               properties.Add("temperatureAlert", temperature > 30 ? "true" : "false");
   
               String content = String.Format("{0} \"deviceId\": \"Intel NUC Gateway\", \"messageId\": {1}, \"temperature\": {2} {3}", "{", ++this.messageCount, temperature, "}");
               Message messageToPublish = new Message(content, properties);
   
               this.broker.Publish(messageToPublish);
           }
       }
   }
   ```

9. <span data-ttu-id="85285-149">Salve o arquivo hello pressionando `Ctrl`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="85285-149">Save hello file by pressing `Ctrl` + `S`.</span></span>

10. <span data-ttu-id="85285-150">Criar um novo arquivo chamado `Untitled-1` por pressionando Olá `Ctrl`  +  `N` chaves como visto no Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="85285-150">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys as seen in hello following image:</span></span>

    ![Novo arquivo do Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-new-file.png)

11. <span data-ttu-id="85285-152">Olá toodeserialize `JSON` objeto que recebemos de saudação simulada `BLE` dispositivo, Olá cópia código a seguir em Olá `Untitled-1` janela do editor de códigos de arquivo.</span><span class="sxs-lookup"><span data-stu-id="85285-152">toodeserialize hello `JSON` object that we receive from hello simulated `BLE` device, copy hello following code into hello `Untitled-1` file code editor window.</span></span> 

   ```csharp
   using System;
   using Newtonsoft.Json;

   namespace IoTEdgeConverterModule
   {
       public class BleData
       {
           [JsonProperty(PropertyName = "temperature")]
           public string Temperature { get; set; }
       }
   }
   ```

12. <span data-ttu-id="85285-153">Salve o arquivo hello como `BleData.cs` pressionando `Ctrl`  +  `Shift`  +  `S` chaves.</span><span class="sxs-lookup"><span data-stu-id="85285-153">Save hello file as `BleData.cs` by pressing `Ctrl` + `Shift` + `S` keys.</span></span>
    - <span data-ttu-id="85285-154">Em Olá Salvar como caixa de diálogo Olá `Save as Type` menu suspenso, selecione `C# (*.cs;*.csx)` como visto no Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="85285-154">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)` as seen in hello following image:</span></span>

    ![Caixa de diálogo Salvar como do Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-save-as.png)

13. <span data-ttu-id="85285-156">Criar um novo arquivo chamado `Untitled-1` por pressionando Olá `Ctrl`  +  `N` chaves.</span><span class="sxs-lookup"><span data-stu-id="85285-156">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

14. <span data-ttu-id="85285-157">Copie e cole Olá trecho de código a seguir em Olá `Untitled-1` arquivo.</span><span class="sxs-lookup"><span data-stu-id="85285-157">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span> <span data-ttu-id="85285-158">Essa classe é um `Azure IoT Edge` módulo, que usamos toooutput Olá dados recebidos do nosso `BleConverterModule`.</span><span class="sxs-lookup"><span data-stu-id="85285-158">This class is a `Azure IoT Edge` module, which we use toooutput hello data received from our `BleConverterModule`.</span></span>

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Text;
   using System.Threading.Tasks;
   using Microsoft.Azure.Devices.Gateway;
   using Newtonsoft.Json;
   
   namespace PrinterModule
   {
       public class DotNetPrinterModule : IGatewayModule
       {
           private string configuration;
           public void Create(Broker broker, byte[] configuration)
           {
               this.configuration = System.Text.Encoding.UTF8.GetString(configuration);
           }
   
           public void Destroy()
           {
           }
   
           public void Receive(Message received_message)
           {
               string recMsg = System.Text.Encoding.UTF8.GetString(received_message.Content, 0, received_message.Content.Length);
               Dictionary<string, string> receivedProperties = received_message.Properties;
               
               BleConverterData receivedData = JsonConvert.DeserializeObject<BleConverterData>(recMsg);
   
               Console.WriteLine();
               Console.WriteLine("Module           : [DotNetPrinterModule]");
               Console.WriteLine("received_message : {0}", recMsg);
   
               if(received_message.Properties["source"] == "bleTelemetry")
               {
                   Console.WriteLine("Source           : {0}", receivedProperties["source"]);
                   Console.WriteLine("MAC address      : {0}", receivedProperties["macAddress"]);
                   Console.WriteLine("Temperature Alert: {0}", receivedProperties["temperatureAlert"]);
                   Console.WriteLine("Deserialized Obj : [BleConverterData]");
                   Console.WriteLine("  DeviceId       : {0}", receivedData.DeviceId);
                   Console.WriteLine("  MessageId      : {0}", receivedData.MessageId);
                   Console.WriteLine("  Temperature    : {0}", receivedData.Temperature);
               }
   
               Console.WriteLine();
           }
       }
   }
   ```

15. <span data-ttu-id="85285-159">Salve o arquivo hello como `DotNetPrinterModule.cs` pressionando `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="85285-159">Save hello file as `DotNetPrinterModule.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="85285-160">Em Olá Salvar como caixa de diálogo Olá `Save as Type` menu suspenso, selecione `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="85285-160">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

16. <span data-ttu-id="85285-161">Criar um novo arquivo chamado `Untitled-1` por pressionando Olá `Ctrl`  +  `N` chaves.</span><span class="sxs-lookup"><span data-stu-id="85285-161">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

17. <span data-ttu-id="85285-162">Olá toodeserialize `JSON` objeto que recebemos de saudação `BleConverterModule`, copiar e colar a seguir Olá trecho de código em Olá `Untitled-1` arquivo.</span><span class="sxs-lookup"><span data-stu-id="85285-162">toodeserialize hello `JSON` object that we receive from hello `BleConverterModule`, Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span> 

   ```csharp
   using System;
   using Newtonsoft.Json;

   namespace PrinterModule
   {
       public class BleConverterData
       {
           [JsonProperty(PropertyName = "deviceId")]
           public string DeviceId { get; set; }
   
           [JsonProperty(PropertyName = "messageId")]
           public string MessageId { get; set; }
   
           [JsonProperty(PropertyName = "temperature")]
           public string Temperature { get; set; }
       }
   }
   ```

18. <span data-ttu-id="85285-163">Salve o arquivo hello como `BleConverterData.cs` pressionando `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="85285-163">Save hello file as `BleConverterData.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="85285-164">Em Olá Salvar como caixa de diálogo Olá `Save as Type` menu suspenso, selecione `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="85285-164">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

19. <span data-ttu-id="85285-165">Criar um novo arquivo chamado `Untitled-1` por pressionando Olá `Ctrl`  +  `N` chaves.</span><span class="sxs-lookup"><span data-stu-id="85285-165">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

20. <span data-ttu-id="85285-166">Copie e cole Olá trecho de código a seguir em Olá `Untitled-1` arquivo.</span><span class="sxs-lookup"><span data-stu-id="85285-166">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span>

   ```json
   {
       "loaders": [
           {
               "type": "dotnetcore",
               "name": "dotnetcore",
               "configuration": {
                   "binding.path": "dotnetcore.dll",
                   "binding.coreclrpath": "C:\\Program Files\\dotnet\\shared\\Microsoft.NETCore.App\\1.1.1\\coreclr.dll",
                   "binding.trustedplatformassemblieslocation": "C:\\Program Files\\dotnet\\shared\\Microsoft.NETCore.App\\1.1.1\\"
               }
           }
       ],
          "modules": [
           {
               "name": "simulated_device",
               "loader": {
                   "name": "native",
                   "entrypoint": {
                       "module.path": "simulated_device.dll"
                   }
               },
               "args": {
                   "macAddress": "01:02:03:03:02:01",
                   "messagePeriod": 500
               }
           },
           {
               "name": "ble_converter_module",
               "loader": {
                   "name": "dotnetcore",
                   "entrypoint": {
                       "assembly.name": "IoTEdgeConverterModule",
                       "entry.type": "IoTEdgeConverterModule.BleConverterModule"
                   }
               },
               "args": ""
           },
           {
               "name": "printer_module",
               "loader": {
                   "name": "dotnetcore",
                   "entrypoint": {
                       "assembly.name": "IoTEdgeConverterModule",
                       "entry.type": "PrinterModule.DotNetPrinterModule"
                   }
               },
               "args": ""
           }
       ],
       "links": [
           {
               "source": "simulated_device", "sink": "ble_converter_module"
           },
           {
               "source": "ble_converter_module", "sink": "printer_module"
           }
   ]
   }
   ```

21. <span data-ttu-id="85285-167">Salve o arquivo hello como `gw-config.json` pressionando `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="85285-167">Save hello file as `gw-config.json` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="85285-168">Em Olá Salvar como caixa de diálogo Olá `Save as Type` menu suspenso, selecione `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span><span class="sxs-lookup"><span data-stu-id="85285-168">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span></span>

22. <span data-ttu-id="85285-169">tooenable uma cópia de saudação toohello de arquivo de configuração de saída diretório, Olá atualização `IoTEdgeConverterModule.csproj` com hello blob XML a seguir:</span><span class="sxs-lookup"><span data-stu-id="85285-169">tooenable copying of hello configuration file toohello output directory, update hello `IoTEdgeConverterModule.csproj` with hello following XML blob:</span></span>

   ```xml
     <ItemGroup>
       <None Update="gw-config.json" CopyToOutputDirectory="PreserveNewest" />
     </ItemGroup>
   ```
    
   - <span data-ttu-id="85285-170">Olá atualizado `IoTEdgeConverterModule.csproj` devem aparência Olá imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="85285-170">hello updated `IoTEdgeConverterModule.csproj` should look like hello following image:</span></span>

    ![Arquivo .csproj atualizado do Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-update-csproj.png)

23. <span data-ttu-id="85285-172">Criar um novo arquivo chamado `Untitled-1` por pressionando Olá `Ctrl`  +  `N` chaves.</span><span class="sxs-lookup"><span data-stu-id="85285-172">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

24. <span data-ttu-id="85285-173">Copie e cole Olá trecho de código a seguir em Olá `Untitled-1` arquivo.</span><span class="sxs-lookup"><span data-stu-id="85285-173">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span>

   ```powershell
   Copy-Item -Path $env:userprofile\.nuget\packages\microsoft.azure.devices.gateway.native.windows.x64\1.1.3\runtimes\win-x64\native\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.formatters\4.3.0\lib\netstandard1.4\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.primitives\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\newtonsoft.json\10.0.2\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.componentmodel.typeconverter\4.3.0\lib\netstandard1.5\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.nongeneric\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.specialized\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   ```

25. <span data-ttu-id="85285-174">Salve o arquivo hello como `binplace.ps1` pressionando `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="85285-174">Save hello file as `binplace.ps1` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="85285-175">Em Olá Salvar como caixa de diálogo Olá `Save as Type` menu suspenso, selecione `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span><span class="sxs-lookup"><span data-stu-id="85285-175">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span></span>

26. <span data-ttu-id="85285-176">Criar projeto Olá Olá pressionando `Ctrl`  +  `Shift`  +  `B` chaves.</span><span class="sxs-lookup"><span data-stu-id="85285-176">Build hello project by pressing hello `Ctrl` + `Shift` + `B` keys.</span></span> <span data-ttu-id="85285-177">Quando você compila o projeto de saudação para Olá primeira vez, `Visual Studio Code` solicita Olá `No build task defined.` diálogo visto Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="85285-177">When you build hello project for hello first time, `Visual Studio Code` prompts you with hello `No build task defined.` dialog as seen in hello following image:</span></span>

    ![Caixa de diálogo de tarefa de compilação do Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-build-task.png)

    <span data-ttu-id="85285-179">a) clique em Olá `Configure Build Task` botão.</span><span class="sxs-lookup"><span data-stu-id="85285-179">a) Click hello `Configure Build Task` button.</span></span>

    <span data-ttu-id="85285-180">b) na Olá `Select a Task Runner` menu suspenso de caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="85285-180">b) In hello `Select a Task Runner` dialog dropdown menu.</span></span> <span data-ttu-id="85285-181">Selecione `.NET Core` como visto no Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="85285-181">Select `.NET Core` as seen in hello following image:</span></span> 

    ![Caixa de diálogo Selecionar uma tarefa do Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-build-task-runner.png)

    <span data-ttu-id="85285-183">Olá c) clicar em `.NET Core` item cria Olá `tasks.json` do arquivo em seu `.vscode` diretório e abre Olá arquivo hello `code editor` janela.</span><span class="sxs-lookup"><span data-stu-id="85285-183">c) Clicking hello `.NET Core` item creates hello `tasks.json` file in your `.vscode` directory and opens hello file in hello `code editor` window.</span></span> <span data-ttu-id="85285-184">Não há toomodify sem necessidade desse arquivo, guia Olá fechar.</span><span class="sxs-lookup"><span data-stu-id="85285-184">There is no need toomodify this file, close hello tab.</span></span>

27.  <span data-ttu-id="85285-185">Olá abrir `Visual Studio Code` janela do terminal integrada por pressionando Olá `Ctrl`  +  `backtick` chaves ou usando menus de saudação `View`  ->  `Integrated Terminal` e tipo **.\binplace.ps1**em Olá `PowerShell` prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="85285-185">Open hello `Visual Studio Code` integrated terminal window by pressing hello `Ctrl` + `backtick` keys or using hello menus `View` -> `Integrated Terminal` and type **.\binplace.ps1** into hello `PowerShell` command prompt.</span></span> <span data-ttu-id="85285-186">Este comando copia todos os nossos diretório de saída de toohello dependências.</span><span class="sxs-lookup"><span data-stu-id="85285-186">This command copies all our dependencies toohello output directory.</span></span>

28. <span data-ttu-id="85285-187">Navegue toohello diretório de saída de projetos em Olá `Integrated Terminal` janela digitando **.\bin\Debug\netstandard1.3 cd**.</span><span class="sxs-lookup"><span data-stu-id="85285-187">Navigate toohello projects output directory in hello `Integrated Terminal` window by typing **cd .\bin\Debug\netstandard1.3**.</span></span>

29. <span data-ttu-id="85285-188">Execute o projeto de exemplo hello digitando **. \gw.exe gw-config. JSON** em Olá `Integrated Terminal` prompt da janela.</span><span class="sxs-lookup"><span data-stu-id="85285-188">Run hello sample project by typing **.\gw.exe gw-config.json** into hello `Integrated Terminal` window prompt.</span></span> 
    - <span data-ttu-id="85285-189">Se você seguiu as etapas de saudação neste tutorial em conjunto, você deve agora estar executando Olá `Azure IoT Edge BLE Data Converter Module` projeto de exemplo como visto no Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="85285-189">If you have followed hello steps in this tutorial closely, you should now be running hello `Azure IoT Edge BLE Data Converter Module` sample project as seen in hello following image:</span></span>
    
        ![Exemplo de dispositivo simulado em execução no Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-run.png)
    
    - <span data-ttu-id="85285-191">Se você quiser tooterminate Olá aplicativo, pressione Olá `<Enter>` chave.</span><span class="sxs-lookup"><span data-stu-id="85285-191">If you want tooterminate hello application, press hello `<Enter>` key.</span></span>

>[!IMPORTANT]
<span data-ttu-id="85285-192">Não é recomendável toouse `Ctrl`  +  `C` tooterminate Olá `IoT Edge` application gateway (ou seja, **gw.exe**).</span><span class="sxs-lookup"><span data-stu-id="85285-192">It is not recommended toouse `Ctrl` + `C` tooterminate hello `IoT Edge` gateway application (that is, **gw.exe**).</span></span> <span data-ttu-id="85285-193">Como essa ação pode causar Olá tooterminate de processo anormal.</span><span class="sxs-lookup"><span data-stu-id="85285-193">As this action may cause hello process tooterminate abnormally.</span></span>

