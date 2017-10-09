---
title: aaaConnect um dispositivo usando C em mbed | Microsoft Docs
description: "Descreve como tooconnect toohello um dispositivo do Azure IoT Suite pré-configurados de solução de monitoramento remota usando um aplicativo escrito em C em execução em um dispositivo mbed."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 9551075e-dcf9-488f-943e-d0eb0e6260be
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ROBOTS: NOINDEX
ms.openlocfilehash: dcd1e74635e8dec678a59bff060a73f7cfabd124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-mbed"></a>Conecte-se a sua solução pré-configurada (mbed) de monitoramento remoto de toohello de dispositivo

## <a name="scenario-overview"></a>Visão geral do cenário
Nesse cenário, você cria um dispositivo que envia Olá toohello telemetria de monitoramento remoto a seguir [pré-configurado solução][lnk-what-are-preconfig-solutions]:

* Temperatura externa
* Temperatura interna
* Umidade

Para simplificar, código de saudação no dispositivo hello gera valores de exemplo, mas recomendamos exemplo hello tooextend conectar sensores real tooyour dispositivo e enviar telemetria real.

dispositivo Olá também é capaz de toorespond toomethods invocada a partir do painel de solução de saudação e desejado valores de propriedade definidos no painel de solução de saudação.

toocomplete neste tutorial, você precisa de uma conta ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure][lnk-free-trial].

## <a name="before-you-start"></a>Antes de começar
Antes de escrever qualquer código para o seu dispositivo, você precisa provisionar a solução pré-configurada de monitoramento remoto e provisionar um novo dispositivo personalizado nessa solução.

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a>Provisionar sua solução pré-configurada de monitoramento remoto
dispositivo Olá criado por você neste tutorial envia a instância de saudação tooan de dados [monitoramento remoto] [ lnk-remote-monitoring] pré-configurado de solução. Se você já não tiver provisionado Olá solução pré-configurada em sua conta do Azure de monitoramento remoto, use Olá etapas a seguir:

1. Em Olá <https://www.azureiotsuite.com/> , clique em  **+**  toocreate uma solução.
2. Clique em **selecione** em Olá **monitoramento remoto** painel toocreate sua solução.
3. Em hello **criar monitoramento remoto solução** , insira um **nome da solução** de sua escolha, selecione Olá **região** você deseja toodeploy para e selecione saudação do Azure assinatura toowant toouse. Clique em **Criar solução**.
4. Aguarde até que a saudação processo de provisionamento for concluído.

> [!WARNING]
> soluções de Olá pré-configurado usam os serviços do Azure faturáveis. Certifique-se de que tooremove Olá solução pré-configurada de sua assinatura, quando você tiver realizado tooavoid quaisquer encargos desnecessários. Você pode remover completamente uma solução pré-configurada de sua assinatura visitando Olá <https://www.azureiotsuite.com/> página.
> 
> 

Quando concluir a saudação processo para Olá remota de solução de monitoramento de provisionamento, clique em **iniciar** tooopen painel de solução de saudação em seu navegador.

![Painel da solução][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a>Configurar seu dispositivo no hello remota de solução de monitoramento
> [!NOTE]
> Se você já configurou um dispositivo em sua solução, poderá ignorar esta etapa. Você precisa ter credenciais de dispositivo de saudação do tooknow quando você cria o aplicativo de cliente hello.
> 
> 

Para uma solução de toohello pré-configurado de tooconnect do dispositivo, ele deve se identificar tooIoT Hub usando credenciais válidas. Você pode recuperar credenciais do dispositivo de saudação do painel de solução de saudação. Você pode incluir credenciais do dispositivo Olá em seu aplicativo cliente posteriormente neste tutorial.

tooadd uma solução de monitoramento remoto do tooyour dispositivo, Olá completo a seguir as etapas no painel de solução de saudação:

1. No hello canto inferior esquerdo do painel do hello, clique em **adicionar um dispositivo**.
   
   ![Adicionar um dispositivo][1]
2. Em Olá **dispositivo personalizado** do painel, clique em **adicionar novo**.
   
   ![Adicionar um dispositivo personalizado][2]
3. Escolha **Deixe-me definir minha própria ID de Dispositivo**. Insira uma ID de dispositivo como **meudispositivo**, clique em **verificar ID** tooverify esse nome não está em uso e, em seguida, clique em **criar** tooprovision dispositivo de saudação.
   
   ![Adicionar ID do dispositivo][3]
4. Tornar um dispositivo de saudação de Observação credenciais (ID do dispositivo, nome de host de Hub IoT e chave do dispositivo). Seu aplicativo cliente precisa de solução de monitoramento remoto toohello de tooconnect esses valores. Em seguida, clique em **Concluído**.
   
    ![Exibir credenciais do dispositivo][4]
5. Selecione o dispositivo na lista de dispositivos de saudação no painel de solução de saudação. Em seguida, no hello **detalhes do dispositivo** do painel, clique em **Ativar dispositivo**. status de saudação do seu dispositivo agora é **executando**. solução de monitoramento remoto Olá agora pode receber telemetria do seu dispositivo e chamar métodos no dispositivo de saudação.

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-hello-c-sample-solution"></a>Compilar e executar a solução de exemplo hello C

Olá, instruções a seguir descrevem as etapas de saudação para se conectar um [habilitado mbed Freescale FRDM-K64F] [ lnk-mbed-home] toohello de dispositivo remoto de solução de monitoramento.

### <a name="connect-hello-mbed-device-tooyour-network-and-desktop-machine"></a>Conecte-se a rede de tooyour Olá mbed dispositivo e o computador desktop

1. Conecte Olá mbed dispositivo tooyour rede usando um cabo Ethernet. Esta etapa é necessária porque o aplicativo de exemplo hello requer acesso à internet.

1. Consulte [guia de Introdução ao mbed] [ lnk-mbed-getstarted] tooconnect mbed dispositivo tooyour área de trabalho do computador.

1. Se seu computador desktop que executam o Windows, consulte [configuração PC] [ lnk-mbed-pcconnect] tooconfigure dispositivo de mbed tooyour acesso à porta serial.

### <a name="create-an-mbed-project-and-import-hello-sample-code"></a>Criar um projeto de mbed e importar o código de exemplo hello

Siga estas etapas tooadd alguns projeto mbed de tooan de código de exemplo. Importar Olá projeto de starter de monitoramento remoto e, em seguida, alterar Olá toouse de projeto Olá protocolo MQTT em vez da saudação protocolo AMQP. No momento, você precisa toouse Olá MQTT protocolo toouse Olá dispositivo recursos de gerenciamento do IoT Hub.

1. No navegador da web, vá toohello mbed.org [site do desenvolvedor](https://developer.mbed.org/). Se você ainda não fez, você verá um toocreate opção uma conta (é gratuito). Caso contrário, faça logon com suas credenciais de conta. Em seguida, clique em **compilador** no canto superior direito de saudação da página de saudação. Essa ação coloca toohello *espaço de trabalho* interface.

1. Certifique-se de plataforma de hardware Olá você está usando aparece no canto superior direito de saudação da janela hello, ou clique em ícone Olá tooselect de canto superior direito da saudação sua plataforma de hardware.

1. Clique em **importação** no menu principal da saudação. Em seguida, clique em **clique aqui tooimport de URL**.
   
    ![Iniciar o espaço de trabalho de importação toombed][6]

1. Na janela pop-up do hello, insira o link de saudação para Olá exemplo código https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ e clique em **importação**.
   
    ![Importar o espaço de trabalho do exemplo código toombed][7]

1. Você pode ver na janela de compilador mbed Olá que importar este projeto também importa várias bibliotecas. Alguns são fornecidas e mantidas pela equipe do Azure IoT hello ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), enquanto outros são bibliotecas de terceiros disponíveis no catálogo do hello mbed bibliotecas.
   
    ![Exibir projeto mbed][8]

1. Em hello **espaço de trabalho do programa**, atalho Olá **hub IOT\_amqp\_transporte** biblioteca, clique em **excluir**e, em seguida, clique em **Okey** tooconfirm.

1. Em hello **espaço de trabalho do programa**, atalho Olá **azure\_amqp\_c** biblioteca, clique em **excluir**e, em seguida, clique em **Okey**  tooconfirm.

1. Saudação do botão direito do mouse **remote_monitoring** projeto no hello **espaço de trabalho do programa**, selecione **biblioteca de importação**, em seguida, selecione **From URL**.
   
    ![Iniciar o espaço de trabalho de toombed de importação de biblioteca][6]

1. Na janela pop-up do hello, insira o link de saudação para Olá MQTT transporte biblioteca https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_de transporte / clique **importação**.
   
    ![Importar o espaço de trabalho biblioteca toombed][12]

1. Olá repetição etapa tooadd Olá MQTT biblioteca anterior de https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c /.

1. Seu espaço de trabalho agora Olá seguinte aparência:

    ![Exibir espaço de trabalho mbed][13]

1. Abra Olá remoto\_monitoring\remote_monitoring.c arquivo e substituir Olá existente `#include` instruções com hello código a seguir:

    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"

    #ifdef MBED_BUILD_TIMESTAMP
    #include "certs.h"
    #endif // MBED_BUILD_TIMESTAMP
    ```
1. Excluir Olá todos os restantes código Olá remoto\_monitoring\remote\_monitoring.c arquivo.

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a>Compilar e executar o exemplo hello

Adicionar saudação do código tooinvoke **remoto\_monitoramento\_executar** de função e, em seguida, compilar e executar o aplicativo de dispositivo hello.

1. Adicionar um **principal** função com o código a seguir no final de saudação do hello remoto\_saudação do monitoring.c arquivo tooinvoke **remoto\_monitoramento\_executar** função:
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. Clique em **compilar** toobuild programa de saudação. Com segurança, você pode ignorar os avisos mas se a compilação hello gera erros, corrija-os antes de continuar.

1. Se compilação Olá for bem-sucedida, o site de compilador mbed hello gera um arquivo. bin com nome de saudação do seu projeto e baixa máquina local tooyour. Copie o dispositivo de toohello de arquivo hello. bin. Salvar o dispositivo de toohello de arquivo hello. bin faz Olá dispositivo toorestart e executa programa hello contido no arquivo. bin de saudação. Você pode reiniciar manualmente o programa hello a qualquer momento, pressionando o botão de redefinição de saudação no dispositivo de mbed hello.

1. Conecte o dispositivo de toohello usando um aplicativo de cliente SSH, como PuTTY. Você pode determinar a porta serial hello, que o dispositivo usa verificando o Gerenciador de dispositivos do Windows.
   
    ![][11]

1. Em PuTTY, clique em Olá **Serial** tipo de conexão. Olá dispositivo normalmente se conecta a 9600 baud, insira assim 9600 em Olá **velocidade** caixa. Em seguida, clique em **Abrir**.

1. programa Hello inicia a execução. Você pode ter tooreset placa de saudação (pressione CTRL + Break ou botão de redefinição da placa de saudação pressione) se o programa de saudação não for iniciado automaticamente quando você se conectar.
   
    ![][10]

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[6]: ./media/iot-suite-connecting-devices-mbed/mbed1.png
[7]: ./media/iot-suite-connecting-devices-mbed/mbed2a.png
[8]: ./media/iot-suite-connecting-devices-mbed/mbed3a.png
[10]: ./media/iot-suite-connecting-devices-mbed/putty.png
[11]: ./media/iot-suite-connecting-devices-mbed/mbed6.png
[12]: ./media/iot-suite-connecting-devices-mbed/mbed7.png
[13]: ./media/iot-suite-connecting-devices-mbed/mbed8.png

[lnk-mbed-home]: https://developer.mbed.org/platforms/FRDM-K64F/
[lnk-mbed-getstarted]: https://developer.mbed.org/platforms/FRDM-K64F/#getting-started-with-mbed
[lnk-mbed-pcconnect]: https://developer.mbed.org/platforms/FRDM-K64F/#pc-configuration
