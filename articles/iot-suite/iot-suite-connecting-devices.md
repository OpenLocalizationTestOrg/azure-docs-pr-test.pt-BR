---
title: aaaConnect um dispositivo usando o C no Windows | Microsoft Docs
description: "Descreve como tooconnect toohello um dispositivo do Azure IoT Suite pré-configurados de solução de monitoramento remota usando um aplicativo escrito em C em execução no Windows."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 34e39a58-2434-482c-b3fa-29438a0c05e8
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 51041e0cec113a5cfa006ab2276096baf928eef5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-windows"></a>Conecte-se a toohello do dispositivo remoto monitoramento solução pré-configurada (Windows)
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-c-sample-solution-on-windows"></a>Criar um exemplo de solução C no Windows
Olá etapas a seguir mostra como toocreate um aplicativo cliente que se comunica com o monitoramento remoto Olá pré-configurado solução. Esse aplicativo é escrito em C e compilado e executado no Windows.

Criar um projeto de starter no Visual Studio 2015 ou 2017 do Visual Studio e adicione pacotes NuGet do hello Hub IoT dispositivo cliente:

1. No Visual Studio, crie um aplicativo de console C usando Olá Visual C++ **aplicativo do Console Win32** modelo. Projeto de saudação do nome **RMDevice**.
2. Em Olá **configurações do aplicativo** página Olá **Assistente de aplicativo Win32**, certifique-se de que **aplicativo de Console** está selecionado e desmarque **pré-compilado cabeçalho** e **Security Development Lifecycle (SDL) verifica**.
3. Em **Solution Explorer**, excluir arquivos de saudação Stdafx. h, targetver.h e Stdafx.
4. Em **Solution Explorer**, renomear Olá arquivo RMDevice.cpp tooRMDevice.c.
5. Em **Solution Explorer**, clique duas vezes em Olá **RMDevice** do projeto e, em seguida, clique em **gerenciar pacotes do NuGet**. Clique em **procurar**, em seguida, procurar e instalar Olá pacotes do NuGet a seguir:
   
   * Microsoft.Azure.IoTHub.Serializer
   * Microsoft.Azure.IoTHub.IoTHubClient
   * Microsoft.Azure.IoTHub.MqttTransport
6. Em **Solution Explorer**, com o botão direito em Olá **RMDevice** do projeto e, em seguida, clique em **propriedades** do projeto de saudação tooopen **páginas de propriedade**caixa de diálogo. Para obter detalhes, confira [Configurando as propriedades do projeto no Visual C++][lnk-c-project-properties]. 
7. Clique Olá **vinculador** pasta, em seguida, clique em Olá **entrada** página de propriedades.
8. Adicionar **crypt32.lib** toohello **dependências adicionais** propriedade. Clique em **Okey** e **Okey** novamente toosave Olá projeto valores de propriedade.

Adicionar Olá JSON Parson biblioteca toohello **RMDevice** do projeto e adicionar Olá necessário `#include` instruções:

1. Em uma pasta adequada no seu computador, clone repositório do GitHub Parson hello usando Olá comando a seguir:

    ```
    git clone https://github.com/kgabis/parson.git
    ```

1. Copie os arquivos de parson.h e parson.c Olá da cópia local de saudação do hello Parson repositório tooyour **RMDevice** pasta do projeto.

1. No Visual Studio, clique com botão direito Olá **RMDevice** de projeto, clique em **adicionar**e, em seguida, clique em **Item existente**.

1. Em Olá **Add Existing Item** caixa de diálogo, parson.h e parson.c arquivos em Olá Olá selecione **RMDevice** pasta do projeto. Em seguida, clique em **adicionar** tooadd esses dois arquivos projeto de tooyour.

1. No Visual Studio, abra o arquivo de RMDevice.c de saudação. Substituir saudação `#include` instruções com hello código a seguir:
   
    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"
    ```

    > [!NOTE]
    > Agora você pode verificar que o projeto tem dependências corretas de saudação configuradas pelo compilá-lo.

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a>Compilar e executar o exemplo hello

Adicionar saudação do código tooinvoke **remoto\_monitoramento\_executar** de função e, em seguida, compilar e executar o aplicativo de dispositivo hello.

1. Substituir saudação **principal** função com o seguinte Olá tooinvoke de código **remoto\_monitoramento\_executar** função:
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. Clique em **criar** e **compilar solução** aplicativo de dispositivo toobuild hello.

1. Em **Solution Explorer**, Olá com o botão direito **RMDevice** de projeto, clique em **depurar**e, em seguida, clique em **iniciar nova instância** toorun Olá exemplo. console de saudação exibe mensagens como hello aplicativo envia exemplo telemetria toohello pré-configurado solução, recebe os valores de propriedade desejados definidos no painel de solução hello e responde toomethods invocada a partir do painel de solução de saudação.

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-c-project-properties]: https://msdn.microsoft.com/library/669zx6zc.aspx
