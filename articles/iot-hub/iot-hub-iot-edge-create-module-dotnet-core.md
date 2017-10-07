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
# <a name="create-an-azure-iot-edge-module-with-cx23"></a>Criar um módulo do Azure IoT Edge com o C&#x23;

Este tutorial mostra como toocreate um módulo para `Azure IoT Edge` usando `Visual Studio Code` e `C#`.

Neste tutorial, nós o conduziremos por meio da configuração do ambiente e como toowrite uma [Bilitar](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) módulo de conversor de dados usando hello mais recente `Azure IoT Edge NuGet` pacotes. 

>[!NOTE]
Este tutorial está usando Olá `.NET Core SDK`, que oferece suporte a compatibilidade de plataforma cruzada. Olá tutorial a seguir é gravado usando Olá `Windows 10` sistema operacional. Alguns comandos de saudação neste tutorial podem ser diferente dependendo de sua `development environment`. 

## <a name="prerequisites"></a>Pré-requisitos

Nesta seção, você configura o ambiente para o desenvolvimento de módulos do `Azure IoT Edge`. Aplica-se tooboth **Windows de 64 bits** e **Linux de 64 bits (8 Ubuntu/Debian)** sistemas operacionais.

saudação de software a seguir é necessária:

- [Cliente Git](https://git-scm.com/downloads)
- [SDK do .NET Core](https://www.microsoft.com/net/core#windowscmd)
- [Visual Studio Code](https://code.visualstudio.com/)

Repositório de saudação tooclone não é necessário para este exemplo, no entanto todos Olá discutido neste tutorial do código de exemplo está localizado na Olá repositório a seguir:

- `git clone https://github.com/Azure-Samples/iot-edge-samples.git`.
- `cd iot-edge-samples/dotnetcore/simulated_ble`

## <a name="getting-started"></a>Introdução

1. Instalar `.NET Core SDK`.
2. Instalar `Visual Studio Code` e hello `C# extension` de saudação Marketplace de código do Visual Studio.

Exibir este [rápido tutorial em vídeo](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) sobre como tooget iniciado usando `Visual Studio Code` e hello `.NET Core SDK`.

## <a name="creating-hello-azure-iot-edge-converter-module"></a>Criando o módulo de conversor de Azure IoT borda Olá

1. Inicializar um novo projeto C# da biblioteca de classes `.NET Core`:
    - Abra um prompt de comando (`Windows + R` -> `cmd` -> `enter`).
    - Navegue toohello pasta em que você deseja toocreate Olá `C#` projeto.
    - Digite **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**. 
    - Este comando cria uma classe vazia chamada `Class1.cs` em seu diretório de projetos.
2. Navegue toohello pasta em que acabamos de criar o projeto de biblioteca de classes Olá digitando **cd IoTEdgeConverterModule**.
3. Projeto aberto Olá no `Visual Studio Code` digitando **código.**.
4. Depois que o projeto Olá é aberto no `Visual Studio Code`, clique em Olá **IoTEdgeConverterModule.csproj** arquivo de saudação tooopen conforme mostrado no Olá a imagem a seguir:

    ![Janela de edição do Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-edit-csproj.png)

5. Inserir saudação `XML` blob mostrado no hello trecho de código a seguir entre fechamento Olá `PropertyGroup` marca e Olá fechando `Project` marca; linha seis em Olá anterior a imagem e salve o arquivo de saudação pressionando `Ctrl`  +  `S`.

   ```xml
     <ItemGroup>
       <PackageReference Include="Microsoft.Azure.Devices.Gateway.Module.NetStandard" Version="1.0.5" />
       <PackageReference Include="System.Threading.Thread" Version="4.3.0" />
       <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
     </ItemGroup> 
   ```

6. Depois de salvar Olá `.csproj` arquivo, `Visual Studio Code` exibirá a um `unresolved dependencies` diálogo visto Olá a imagem a seguir: 

    ![Caixa de diálogo de dependências de restauração do Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-restore.png)

    a) clique `Restore` toorestore todos Olá referências em projetos de saudação `.csproj` arquivo incluindo Olá `PackageReferences` adicionamos. 

    b) `Visual Studio Code` cria automaticamente Olá `project.assets.json` arquivo em seus projetos `obj` pasta. Esse arquivo contém informações sobre dependências toomake subsequentes restaurações seu projeto mais rápidas.
 
    >[!NOTE]
    `.NET Core Tools` agora são baseadas em MSBuild. O que significa que um arquivo de projeto `.csproj` é criado, em vez de um `project.json`.

    - Se `Visual Studio Code` não solicita a você se está ok, podemos fazer isso manualmente. Olá abrir `Visual Studio Code` janela do terminal integrada por pressionando Olá `Ctrl`  +  `backtick` chaves ou usando menus de saudação `View`  ->  `Integrated Terminal`.
    - Em Olá `Integrated Terminal` tipo de janela **restauração dotnet**.
    
7. Renomear Olá `Class1.cs` arquivo muito`BleConverterModule.cs`. 

    a) arquivo de saudação toorename primeiro clique no arquivo hello e pressione Olá `F2` chave.
    
    b) digite Olá novo nome **BleConverterModule**, como visto no Olá a imagem a seguir:

    ![Visual Studio Code renomeando uma classe](media/iot-hub-iot-edge-create-module/vscode-rename.png)

8. Substitua o código existente Olá Olá `BleConverterModule.cs` arquivo copiando e colando Olá seguindo o trecho de código em seu `BleConverterModule.cs` arquivo.

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

9. Salve o arquivo hello pressionando `Ctrl`  +  `S`.

10. Criar um novo arquivo chamado `Untitled-1` por pressionando Olá `Ctrl`  +  `N` chaves como visto no Olá a imagem a seguir:

    ![Novo arquivo do Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-new-file.png)

11. Olá toodeserialize `JSON` objeto que recebemos de saudação simulada `BLE` dispositivo, Olá cópia código a seguir em Olá `Untitled-1` janela do editor de códigos de arquivo. 

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

12. Salve o arquivo hello como `BleData.cs` pressionando `Ctrl`  +  `Shift`  +  `S` chaves.
    - Em Olá Salvar como caixa de diálogo Olá `Save as Type` menu suspenso, selecione `C# (*.cs;*.csx)` como visto no Olá a imagem a seguir:

    ![Caixa de diálogo Salvar como do Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-save-as.png)

13. Criar um novo arquivo chamado `Untitled-1` por pressionando Olá `Ctrl`  +  `N` chaves.

14. Copie e cole Olá trecho de código a seguir em Olá `Untitled-1` arquivo. Essa classe é um `Azure IoT Edge` módulo, que usamos toooutput Olá dados recebidos do nosso `BleConverterModule`.

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

15. Salve o arquivo hello como `DotNetPrinterModule.cs` pressionando `Ctrl`  +  `Shift`  +  `S`.
    - Em Olá Salvar como caixa de diálogo Olá `Save as Type` menu suspenso, selecione `C# (*.cs;*.csx)`.

16. Criar um novo arquivo chamado `Untitled-1` por pressionando Olá `Ctrl`  +  `N` chaves.

17. Olá toodeserialize `JSON` objeto que recebemos de saudação `BleConverterModule`, copiar e colar a seguir Olá trecho de código em Olá `Untitled-1` arquivo. 

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

18. Salve o arquivo hello como `BleConverterData.cs` pressionando `Ctrl`  +  `Shift`  +  `S`.
    - Em Olá Salvar como caixa de diálogo Olá `Save as Type` menu suspenso, selecione `C# (*.cs;*.csx)`.

19. Criar um novo arquivo chamado `Untitled-1` por pressionando Olá `Ctrl`  +  `N` chaves.

20. Copie e cole Olá trecho de código a seguir em Olá `Untitled-1` arquivo.

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

21. Salve o arquivo hello como `gw-config.json` pressionando `Ctrl`  +  `Shift`  +  `S`.
    - Em Olá Salvar como caixa de diálogo Olá `Save as Type` menu suspenso, selecione `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.

22. tooenable uma cópia de saudação toohello de arquivo de configuração de saída diretório, Olá atualização `IoTEdgeConverterModule.csproj` com hello blob XML a seguir:

   ```xml
     <ItemGroup>
       <None Update="gw-config.json" CopyToOutputDirectory="PreserveNewest" />
     </ItemGroup>
   ```
    
   - Olá atualizado `IoTEdgeConverterModule.csproj` devem aparência Olá imagem a seguir:

    ![Arquivo .csproj atualizado do Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-update-csproj.png)

23. Criar um novo arquivo chamado `Untitled-1` por pressionando Olá `Ctrl`  +  `N` chaves.

24. Copie e cole Olá trecho de código a seguir em Olá `Untitled-1` arquivo.

   ```powershell
   Copy-Item -Path $env:userprofile\.nuget\packages\microsoft.azure.devices.gateway.native.windows.x64\1.1.3\runtimes\win-x64\native\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.formatters\4.3.0\lib\netstandard1.4\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.primitives\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\newtonsoft.json\10.0.2\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.componentmodel.typeconverter\4.3.0\lib\netstandard1.5\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.nongeneric\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.specialized\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   ```

25. Salve o arquivo hello como `binplace.ps1` pressionando `Ctrl`  +  `Shift`  +  `S`.
    - Em Olá Salvar como caixa de diálogo Olá `Save as Type` menu suspenso, selecione `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.

26. Criar projeto Olá Olá pressionando `Ctrl`  +  `Shift`  +  `B` chaves. Quando você compila o projeto de saudação para Olá primeira vez, `Visual Studio Code` solicita Olá `No build task defined.` diálogo visto Olá a imagem a seguir:

    ![Caixa de diálogo de tarefa de compilação do Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-build-task.png)

    a) clique em Olá `Configure Build Task` botão.

    b) na Olá `Select a Task Runner` menu suspenso de caixa de diálogo. Selecione `.NET Core` como visto no Olá a imagem a seguir: 

    ![Caixa de diálogo Selecionar uma tarefa do Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-build-task-runner.png)

    Olá c) clicar em `.NET Core` item cria Olá `tasks.json` do arquivo em seu `.vscode` diretório e abre Olá arquivo hello `code editor` janela. Não há toomodify sem necessidade desse arquivo, guia Olá fechar.

27.  Olá abrir `Visual Studio Code` janela do terminal integrada por pressionando Olá `Ctrl`  +  `backtick` chaves ou usando menus de saudação `View`  ->  `Integrated Terminal` e tipo **.\binplace.ps1**em Olá `PowerShell` prompt de comando. Este comando copia todos os nossos diretório de saída de toohello dependências.

28. Navegue toohello diretório de saída de projetos em Olá `Integrated Terminal` janela digitando **.\bin\Debug\netstandard1.3 cd**.

29. Execute o projeto de exemplo hello digitando **. \gw.exe gw-config. JSON** em Olá `Integrated Terminal` prompt da janela. 
    - Se você seguiu as etapas de saudação neste tutorial em conjunto, você deve agora estar executando Olá `Azure IoT Edge BLE Data Converter Module` projeto de exemplo como visto no Olá a imagem a seguir:
    
        ![Exemplo de dispositivo simulado em execução no Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-run.png)
    
    - Se você quiser tooterminate Olá aplicativo, pressione Olá `<Enter>` chave.

>[!IMPORTANT]
Não é recomendável toouse `Ctrl`  +  `C` tooterminate Olá `IoT Edge` application gateway (ou seja, **gw.exe**). Como essa ação pode causar Olá tooterminate de processo anormal.

