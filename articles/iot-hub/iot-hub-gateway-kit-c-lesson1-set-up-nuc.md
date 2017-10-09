---
title: "Dispositivo SensorTag e Gateway do IoT do Azure – Lição 1: configurar NUC da Intel | Microsoft Docs"
description: "Configurar a Intel NUC toowork como um gateway de IoT entre um sensor e informações sobre o Azure IoT Hub toocollect sensor e enviá-lo tooIoT Hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: gateway iot, intel nuc, computador nuc, DE3815TYKE
ms.assetid: 917090d6-35c2-495b-a620-ca6f9c02b317
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7c3ab3b014713c7facb86b8e8622d70e60a960e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a>Configurar um NUC da Intel como um gateway IoT
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

## <a name="what-you-will-do"></a>O que você fará

- Configure um NUC da Intel como um gateway IoT.
- Instale pacote do Azure IoT borda Olá em Olá NUC Intel.
- Execute um aplicativo de exemplo "hello_world" em Olá funcionalidade de gateway do Intel NUC tooverify hello.

  > Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>O que você aprenderá

Nesta lição, você aprenderá:

- Como tooconnect NUC Intel com periféricos.
- Como tooinstall e atualização de pacotes de saudação necessário em NUC Intel usando Olá inteligente Gerenciador de pacotes.
- Como toorun hello "hello_world" exemplo de funcionalidade de gateway do aplicativo tooverify hello.

## <a name="what-you-need"></a>O que você precisa

- Um Intel NUC Kit DE3815TYKE com hello Intel IoT Gateway Software Suite (vento rio Linux * 7.0.0.13) pré-instalado. [Clique aqui toopurchase Grove IoT comercial Gateway Kit](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).
- Um cabo Ethernet.
- Um teclado.
- Um cabo HDMI ou VGA.
- Um monitor com uma porta HDMI ou VGA.
- Opcional: [Marcação de Sensor Texas Instruments (CC2650STK)](http://www.ti.com/tool/cc2650stk)

![Kit de Gateway](media/iot-hub-gateway-kit-lessons/lesson1/kit.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a>Conecte-se a Intel NUC com periféricos Olá

imagem de saudação abaixo está um exemplo de NUC Intel que está conectado com vários periféricos:

1. Teclado tooa conectado.
2. Conectado tooa monitor com um cabo VGA ou HDMI.
3. Tooa conectado a rede com um cabo Ethernet com fio.
4. Fonte de alimentação tooa conectado com um cabo de alimentação.

![Tooperipherals NUC Intel conectado](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a>Conecte-se o sistema do Intel NUC toohello do computador host por meio do Secure Shell (SSH)

Você precisará de um teclado e um endereço IP do monitor tooget saudação do seu dispositivo NUC Intel. Se você já souber Olá IP endereço, você pode ignorar toostep ahead 3 nesta seção.

1. Ativar Olá Intel NUC pressionando o botão liga / desliga hello e, em seguida, faça logon.

   Olá nome de usuário e senha são ambos `root`.

       > Hit hello enter key on your keyboard if you see either of hello following errors when you boot: 'A TPM error (7) occurred attempting tooread a pcr value.' or 'Timeout, No TPM chip found, activating TPM-bypass!'

2. Obter o endereço IP Olá Olá Intel NUC executando Olá `ifconfig` comando no dispositivo de NUC Intel hello.

   Aqui está um exemplo de saída do comando hello.

   ![Saída ifconfig mostrando o IP do NUC da Intel](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   Neste exemplo, Olá valor segue `inet addr:` é Olá endereço IP que você precisa conectar quando toohello Intel NUC de um computador host.

3. Use um dos Olá seguir SSH clientes de sua tooIntel de tooconnect do computador host NUC.

    - [PuTTY](http://www.putty.org/) para Windows.
    - Olá SSH do cliente interno Ubuntu ou macOS.

   É mais eficiente e produtiva toooperate um NUC Intel de um computador host. Você vai precisar Olá endereço IP do Intel NUC, tooit do tooconnect de nome e a senha do usuário por meio de um cliente SSH. Aqui está um exemplo que usa um cliente SSH no macOS.
   ![Cliente SSH em execução no macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)

## <a name="install-hello-azure-iot-edge-package"></a>Instalar o pacote do Azure IoT borda Olá

pacote do Azure IoT borda Olá contém binários pré-compilados Olá IoT borda e suas dependências. Esses binários são Azure IoT borda, hello Azure IoT SDK e as ferramentas de saudação correspondente. Olá pacote também contém um "hello_world" aplicativo de exemplo é a funcionalidade de gateway de saudação toovalidate usado. Borda de IoT é Olá fundamentais ao gateway hello. 

Execute o pacote de saudação de tooinstall essas etapas.

1. Adicione Olá repositório IoT nuvem executando Olá comandos em uma janela de terminal a seguir:

   ```bash
   rpm --import https://iotdk.intel.com/misc/iot_pub2.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
   ```

   > Digite 'y', quando você solicita too'Include esse canal?'
   
   Se você receber um `import read failed(-1)` erro, use Olá problema de saudação tooresolve comandos a seguir:
   ```bash
   wget http://iotdk.intel.com/misc/iot_pub2.key 
   rpm --import iot_pub2.key  
   ```

   Olá `rpm` comando importa Olá chave rpm. Olá `smart channel` comando adiciona rpm Olá toohello inteligente Package Manager do canal. Antes de executar Olá `smart update` de comando, você verá uma saída como abaixo.

   ![saída de comandos de canal inteligente e rpm](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

2. Execute o comando de atualização inteligente hello:

   ```bash
   smart update
   ```

3. Instale pacote de Gateway do Azure IoT Olá executando Olá comando a seguir:

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   `packagegroup-cloud-azure`é o nome de saudação do pacote de saudação. Olá `smart install` comando é o pacote de saudação tooinstall usado.

    > Comando a seguir de execução Olá se você vir esse erro: 'não está disponível de chave pública'

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```
    > Reinicializar Olá Intel NUC se você vir esse erro: 'Nenhum pacote fornece util-linux-dev'

   Depois de instalar o pacote de saudação, Intel NUC é toofunction pronto como um gateway.

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a>Execute o aplicativo de exemplo hello Azure IoT borda "hello_world"

saudação de aplicativo de exemplo a seguir cria um gateway de um `hello_world.json` de arquivo e usa componentes fundamentais de saudação do Azure IoT borda arquitetura toolog um arquivo de tooa de mensagem hello world (txt) a cada 5 segundos.

Você pode executar o exemplo hello World Olá executando Olá comandos a seguir:

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

Permitir que o aplicativo hello World Olá executar alguns minutos e, em seguida, pressione Olá Enter chave toostop-lo.
![saída do aplicativo](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

> Você pode ignorar quaisquer erros de 'identificador de argumento inválido(NULL)' que apareçam depois que você pressionar Enter.

Você pode verificar o gateway Olá foi executado com êxito abrindo o arquivo de log. txt Olá que agora está na pasta hello_world ![exibição de diretório de log. txt](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)

Abra o log usando o comando a seguir de saudação:

```bash
vim log.txt
```

Você verá conteúdo de saudação do log. txt, que será uma saída JSON formatado log das mensagens de saudação que foram gravados 5 segundos pelo módulo de Hello World gateway hello.
![exibição de diretório de log.txt](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)

Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="summary"></a>Resumo

Parabéns! Você terminou de configurar o NUC da Intel como um gateway. Agora você está pronto toomove em toohello próxima lição tooset computador host e criar um Hub de IoT do Azure e registrar seu dispositivo lógico de Azure IoT Hub.

## <a name="next-steps"></a>Próximas etapas
[Use um gateway de IoT tooconnect tooAzure um dispositivo IoT Hub](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

