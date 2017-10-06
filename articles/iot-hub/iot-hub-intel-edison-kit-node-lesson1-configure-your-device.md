---
title: "Conecte-se Edison Intel (nó) tooAzure IoT - lição 1: Configurar dispositivo | Microsoft Docs"
description: Configurar o Intel Edison para o primeiro uso.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino configurado, conecte-se arduino toopc, arduino de instalação, arduino board"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 372c9b6d-e701-4ff6-8151-d262aa76aa55
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c0609542a49924c979f71297d808c09acefca0bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-intel-edison"></a>Configurar seu Intel Edison
## <a name="what-you-will-do"></a>O que você fará
Configurar Edison Intel para uso pela primeira vez montando o quadro hello, ligar e instalar a configuração ferramenta tooyour desktop SO tooflash firmware de Edison, definir sua senha e conecte-o tooWi-Fi. Se você tiver problemas, procure por soluções em Olá [página de solução][troubleshooting].

## <a name="what-you-will-learn"></a>O que você aprenderá
Neste artigo, você aprenderá:

* Como tooassemble Edison placa e ligue-o.
* Como o firmware de tooflash Edison, definir senha e conexão Wi-Fi.

## <a name="what-you-need"></a>O que você precisa
toocomplete essa operação, você precisa Olá seguir partes de seu Intel Edison Starter Kit:

* Módulo do Intel® Edison
* Placa de expansão Arduino
* Qualquer barras espaçador ou parafusos incluídos no pacote hello, incluindo a placa de expansão dois parafusos toofasten Olá módulo toohello e quatro conjuntos de parafusos e espaçadores plásticos.
* Um tooType Micro B um cabo
* Uma fonte de alimentação CC (corrente contínua). A fonte de alimentação deve ser classificada da seguinte maneira:
  - 7-15V CC
  - Pelo menos 1500 mA
  - pin do Hello center/interna deve ser Olá positivo polos Olá de fonte de alimentação

  ![Coisas em seu Kit de Início](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

Você também precisará de:

* Um computador executando o Windows, Mac ou Linux.
* Uma conexão sem fio para tooconnect Edison para.
* Uma ferramenta de configuração de toodownload de conexão de Internet.

## <a name="assemble-your-board"></a>Montar sua placa

Esta seção contém etapas tooattach sua placa de expansão Intel® Edison tooyour de módulo.

1. Coloque o módulo de Intel® Edison de saudação dentro da estrutura de tópicos Olá branca em seu quadro de expansão, alinhado buracos Olá no módulo Olá com parafusos Olá na placa de expansão de saudação.

2. Pressione módulo Olá logo abaixo palavras Olá `What will you make?` até que você se sentir um snapshot.

   ![montar a placa 2](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. Use Olá dois porcas hexadecimal (incluídos no pacote de saudação) toosecure Olá módulo toohello expansão quadro.

   ![montar a placa 3](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. Insira um parafuso de uma das quatro furos de canto Olá na placa de expansão de saudação. Gire e reforçar uma espaçadores de plástico Olá branca em parafuso de saudação.

   ![montar a placa 4](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. Repita para Olá espaçadores outros três canto.

   ![montar a placa 5](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

Agora, sua placa está montada.

   ![montar a placa](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a>Ligar o Edison

1. Conecte-se na fonte de alimentação hello.

   ![Conectar à fonte de alimentação](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. Um LED verde (DS1 em Olá placa de expansão Arduino *) deve acende e permanecer aceso.

3. Aguarde um minuto para Olá quadro toofinish inicialização.

   > [!NOTE]
   > Se você não tiver uma fonte de energia do controlador de domínio, você ainda pode placa de saudação de energia por meio de uma porta USB. Confira a seção `Connect Edison tooyour computer` para obter detalhes. Ligar sua placa dessa maneira pode resultar em um comportamento imprevisível da placa, especialmente ao usar Wi-Fi ou motores de acionamento.

## <a name="connect-edison-tooyour-computer"></a>Conectar o computador de tooyour Edison

1. Alternar para baixo microcomutador Olá até dois o portas USB micro hello, para que Edison está no modo de dispositivo. Veja [aqui](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode) as diferenças entre o modo de dispositivo e o modo de host.

   ![Alternar a saudação microcomutador](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. Conecte cabo micro Olá Olá superior micro porta.

   ![Porta micro USB superior](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. Plug Olá outra extremidade do cabo USB em seu computador.

   ![USB do computador](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

4. Você saberá que a placa foi inicializada completamente quando o computador montar uma nova unidade (muito semelhante a inserir um cartão SD no computador).

## <a name="download-and-run-hello-configuration-tool"></a>Baixe e execute a ferramenta de configuração de saudação
Obter a ferramenta de configuração mais recente saudação do [este link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listado em Olá `Installers` título. Execute a ferramenta hello e execute seu na tela instruções, clicar em próximo, quando necessário

### <a name="flash-firmware"></a>Atualizar o firmware
1. Em Olá `Set up options` , clique em `Flash Firmware`.
2. Selecione Olá tooflash de imagem em seu quadro seguindo um destes procedimentos hello:
   - flash e toodownload seu quadro com hello mais recente firmware imagem disponível da Intel, selecione `Download hello latest image version xxxx`.
   - tooflash seu quadro com uma imagem que você já tiver salvo em seu computador, selecione `Select hello local image`. Procure tooand Olá selecione imagem tooflash tooyour quadro.
3. ferramenta de configuração de saudação tentará tooflash seu quadro. todo o processo de intermitente Olá pode levar too10 minutos.

### <a name="set-password"></a>Definir senha
1. Em Olá `Set up options` , clique em `Enable Security`.
2. É possível definir um nome personalizado para sua placa Intel® Edison. Isso é opcional.
3. Digite uma senha para a placa e clique em `Set password`.
4. Marca uma senha hello, que é usada posteriormente.

### <a name="connect-wi-fi"></a>Conectar ao Wi-Fi
1. Em Olá `Set up options` , clique em `Connect Wi-Fi`. Aguarde o minuto tooone como verificações de seu computador para redes Wi-Fi disponíveis.
2. De saudação `Detected Networks` lista suspensa, selecione sua rede.
3. De saudação `Security` lista suspensa, o tipo de segurança da rede Olá select.
4. Forneça suas informações de logon e senha e clique em `Configure Wi-Fi`.
5. Marca Olá endereço IP, que é usado posteriormente.

> [!NOTE]
> Certifique-se de Edison é conectado toohello mesmo de rede do computador. O computador se conecta a tooyour Edison usando o endereço IP de saudação.

Parabéns! Você configurou o Edison com êxito.

## <a name="summary"></a>Resumo
Neste artigo, você aprendeu como tooassemble Olá placa Edison, flash sua senha de configuração, o firmware e conectá-lo tooWi-Fi usando a ferramenta de configuração. Observe que Olá que LED ainda não ativado. Olá próxima tarefa é o software em preparação para a execução de um aplicativo de exemplo no Edison e ferramentas necessárias de saudação tooinstall.

## <a name="next-steps"></a>Próximas etapas
[Obter ferramentas Olá][get-the-tools]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md