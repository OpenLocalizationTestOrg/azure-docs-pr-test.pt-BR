---
title: "conversão de aaaData no gateway IoT com borda de IoT do Azure | Microsoft Docs"
description: "Use IoT gateway tooconvert Olá formato de dados de sensor por meio de um módulo personalizado de borda de IoT do Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "conversão de dados do gateway iot, transformação de dados do gateway iot"
ms.assetid: 75f2573d-500b-4405-bff7-61021c4c3500
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: ae94b1f96f36dfcb4f77fadc0ece3cff3d0bba91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-for-sensor-data-transformation-with-azure-iot-edge"></a>Usar o gateway IoT para transformação dos dados de sensor com o Azure IoT Edge

> [!NOTE]
> Antes de iniciar este tutorial, certifique-se de que ter concluído Olá lições a seguir na sequência:
> * [Configurar a NUC Intel como um gateway IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
> * [Usar IoT gateway tooconnect coisas toohello nuvem - SensorTag tooAzure IoT Hub](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

Uma finalidade de um gateway de Iot é tooprocess coletados dados antes de enviá-la toohello nuvem. Borda de IoT do Azure apresenta módulos que podem ser o fluxo de trabalho de processamento de dados de saudação tooform criado e montado. Um módulo recebe uma mensagem, executa alguma ação nele e, em seguida, movê-lo para outros módulos tooprocess.

## <a name="what-you-learn"></a>O que você aprenderá

Você aprenderá como toocreate tooconvert um módulo mensagens de saudação SensorTag em um formato diferente.

## <a name="what-you-do"></a>O que fazer

* Crie um módulo tooconvert uma mensagem recebida no formato do hello. JSON.
* Compile o módulo de saudação.
* Adicione o aplicativo de exemplo hello módulo toohello Bilitar da borda do IoT do Azure.
* Execute o aplicativo de exemplo hello.

## <a name="what-you-need"></a>O que você precisa

* Olá tutoriais concluídas na sequência a seguir:
  * [Configurar a NUC Intel como um gateway IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
  * [Usar IoT gateway tooconnect coisas toohello nuvem - SensorTag tooAzure IoT Hub](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)
* Um cliente SSH executado no computador host. Recomenda-se o PuTTY no Windows. O Linux e o macOS já vêm com um cliente SSH.
* Olá endereço IP e Olá username e password tooaccess Olá gateway de cliente SSH hello.
* Uma conexão com a Internet.

## <a name="create-a-module"></a>Criar um módulo

1. No computador de host Olá, execute o cliente SSH hello e conecte-se toohello IoT gateway.
1. Clone arquivos de origem de saudação do módulo de conversão de saudação do diretório base do GitHub toohello do gateway de IoT Olá executando Olá comandos a seguir:

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-nuc-gateway-customized-module.git
   ```

   Este é um módulo nativo do Azure borda escrito na linguagem de programação C de saudação. módulo Olá converte o formato de saudação de mensagens recebidas em Olá seguindo um:

   ```json
   {"deviceId": "Intel NUC Gateway", "messageId": 0, "temperature": 0.0}
   ```

## <a name="compile-hello-module"></a>Compilar o módulo Olá

módulo de saudação toocompile, execute Olá comandos a seguir:

```bash
cd iot-hub-c-intel-nuc-gateway-customized-module/my_module
# change hello build script runnable
chmod 777 build.sh
# remove hello invalid windows character
sed -i -e "s/\r$//" build.sh
# run hello build shell script
./build.sh
```

Você obtém um `libmy_module.so` após a compilação de saudação do arquivo. Faça uma anotação de caminho absoluto do hello desse arquivo.

## <a name="add-hello-module-toohello-ble-sample-application"></a>Adicionar o aplicativo de exemplo hello módulo toohello Bilitar

1. Pasta de exemplos toohello vá executando Olá comando a seguir:

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples
   ```

1. Abra o arquivo de configuração de saudação executando Olá comando a seguir:

   ```bash
   vi ble_gateway.json
   ```

1. Adicionar um módulo inserindo Olá toohello de código a seguir `modules` seção.

   ```json
   {
       "name": "MyModule",
       "loader": {
           "name": "native",
           "entrypoint":{
               "module.path": "[Your libmy_module.so path]"
               }
            },
        "args": null
    },
    ```

1. Substitua `[Your libmy_module.so path]` no código de saudação com caminho absoluto de saudação do hello libmy_module.so' arquivo.
1. Substitua o código Olá Olá `links` seção com hello seguindo um:

   ```json
   {
       "source": "SensorTag",
       "sink": "MyModule"
   },
   {
       "source": "MyModule",
       "sink": "mapping"
   }
   ```

1. Pressione `ESC`e, em seguida, digite `:wq` toosave arquivo de saudação.

## <a name="run-hello-sample-application"></a>Executar o aplicativo de exemplo hello

1. Ligar Olá SensorTag.
1. Definir variável de ambiente SSL_CERT_FILE Olá executando Olá comando a seguir:

   ```bash
   export SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
   ```

1. Execute o aplicativo de exemplo hello com módulo adicionado Olá executando Olá comando a seguir:

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a>Próximas etapas

Com êxito, que você use Olá IoT gateway tooconvert mensagem de saudação SensorTag em formato do hello. JSON.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
