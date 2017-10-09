---
title: "Dispositivo simulado e Gateway do IoT do Azure - Lição 1: Configurar NUC| Microsoft Docs"
description: "Configurar a Intel NUC toowork como um gateway de IoT entre um sensor e informações sobre o Azure IoT Hub toocollect sensor e enviá-lo tooIoT Hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: yjianfeng
tags: 
keywords: gateway iot, intel nuc, computador nuc, DE3815TYKE
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f41d6b2e-9b00-40df-90eb-17d824bea883
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c2146c7cd8ca54adbd0af279364ec8484be1b45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a>Configurar um NUC da Intel como um gateway IoT

## <a name="what-you-will-do"></a>O que você fará

- Configure um NUC da Intel como um gateway IoT.
- Instale pacote do Azure IoT borda Olá em NUC Intel.
- Execute um aplicativo de exemplo "hello_world" na funcionalidade de gateway do Intel NUC tooverify hello.
Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>O que você aprenderá

Nesta lição, você aprenderá:

- Como tooconnect NUC Intel com periféricos.
- Como tooinstall e atualização de pacotes de saudação necessário em NUC Intel usando Olá inteligente Gerenciador de pacotes.
- Como toorun hello "hello_world" exemplo de funcionalidade de gateway do aplicativo tooverify hello.

## <a name="what-you-need"></a>O que você precisa

- Um Intel NUC Kit DE3815TYKE com hello Intel IoT Gateway Software Suite (vento rio Linux * 7.0.0.13) pré-instalado.
- Um cabo Ethernet.
- Um teclado.
- Um cabo HDMI ou VGA.
- Um monitor com uma porta HDMI ou VGA.

![Kit de Gateway](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a>Conecte-se a Intel NUC com periféricos Olá

imagem de saudação abaixo está um exemplo de NUC Intel que está conectado com vários periféricos:

1. Teclado tooa conectado.
2. Conectado toohello monitor por um cabo VGA ou HDMI.
3. Conectado tooa rede com fio por um cabo Ethernet.
4. Fonte de alimentação toohello conectado com um cabo de alimentação.

![Tooperipherals NUC Intel conectado](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a>Conecte-se o sistema do Intel NUC toohello do computador host por meio do Secure Shell (SSH)

Aqui, você precisa de teclado e monitor tooget Olá endereço IP do dispositivo NUC. Se você já souber Olá IP endereço, você pode ignorar toostep 3 nesta seção.

1. Ative Intel NUC pressionando o botão liga / desliga hello e log no sistema de saudação.

   Olá nome de usuário e senha são ambos `root`.

2. Obtenha o endereço IP de saudação do NUC executando Olá `ifconfig` comando. Esta etapa é feita no dispositivo NUC hello.

   Aqui está um exemplo de saída do comando hello.

   ![Resultado de ifconfig mostrando o IP do NUC](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   Neste exemplo, Olá valor segue `inet addr:` é o endereço IP de saudação que é necessário quando você planejar tooconnect remotamente a partir de um computador de host tooIntel NUC.

3. Use um dos Olá seguir SSH clientes de sua tooIntel de tooconnect de máquina de host NUC.

   - [PuTTY](http://www.putty.org/) para Windows.
   - Olá compilação no cliente SSH no Ubuntu ou macOS.

   É mais eficiente e produtiva toooperate no Intel NUC de um computador host. É necessário o endereço IP Olá Olá, nome de usuário e senha tooconnect Olá NUC pelo cliente do SSH. Este é o cliente SSH de uso de exemplo hello em macOS.
   ![Cliente SSH em execução no macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)

## <a name="install-hello-azure-iot-edge-package"></a>Instalar o pacote do Azure IoT borda Olá

pacote do Azure IoT borda Olá contém binários pré-compilados Olá Olá SDK e suas dependências. Esses binários são Azure IoT borda, hello Azure IoT SDK e as ferramentas de saudação correspondente. pacote de saudação também contém um aplicativo de exemplo "hello_world" que é a funcionalidade de gateway de saudação toovalidate usado. Borda de IoT é Olá fundamentais ao gateway hello. Olá tooinstall do pacote, siga estas etapas:

1. Adicione repositório de nuvem IoT Olá executando Olá comandos em uma janela de terminal a seguir:

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   Olá `rpm` comando importa Olá chave rpm. Olá `smart channel` comando adiciona rpm Olá toohello inteligente Package Manager do canal. Antes de executar Olá `smart update` comando, verá uma saída como abaixo.

   ![saída de comandos de canal inteligente e rpm](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. Instale o pacote de saudação executando Olá comando a seguir:

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   `packagegroup-cloud-azure`é o nome de saudação do pacote de saudação. Olá `smart install` comando é o pacote de saudação tooinstall usado.

   Depois de instalar o pacote de saudação, Intel NUC é esperado toowork como um gateway.

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a>Execute o aplicativo de exemplo hello Azure IoT borda "hello_world"

Vá muito`azureiotgatewaysdk/samples` e execute o aplicativo de exemplo hello exemplo "hello_world". Este aplicativo de exemplo cria um gateway de saudação `hello_world.json` de arquivo e usa componentes fundamentais de saudação do hello Azure IoT borda arquitetura toolog um arquivo de tooa mensagem hello world a cada 5 segundos.

Você pode executar o aplicativo de exemplo hello exemplo "hello_world" executando Olá comando a seguir:

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

aplicativo de exemplo Hello produz o seguinte Olá saída se a funcionalidade de gateway hello está funcionando corretamente:

![saída do aplicativo](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="summary"></a>Resumo

Parabéns! Você terminou de configurar o NUC da Intel como um gateway. Agora você está pronto toomove em toohello próxima lição tooset computador host e criar um hub IoT do Azure e registrar seu dispositivo lógico de hub IoT do Azure.

## <a name="next-steps"></a>Próximas etapas
[Prepare o computador host e o Hub IoT do Azure](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
