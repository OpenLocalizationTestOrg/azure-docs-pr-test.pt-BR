---
title: dispositivo aaaInstall Microsoft Azure StorSimple 8100 | Microsoft Docs
description: "Descreve como toounpack, montagem em rack e fazer o cabeamento do seu dispositivo StorSimple 8100 antes de implantar e configurar o software de saudação."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 6098a01e-c031-488a-a8d7-0b607ce665e1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 76b94e57318b6c25dc3333ae73edc9e4752b7d1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="unpack-rack-mount-and-cable-your-storsimple-8100-device"></a>Desembalar, montar em rack e cabear o dispositivo StorSimple 8100.
## <a name="overview"></a>Visão geral
Seu Microsoft Azure StorSimple 8100 é um dispositivo único de compartimento montado em rack. Este tutorial explica como toounpack de montagem em rack e cabo Olá hardware do dispositivo StorSimple 8100 antes de configurar e implantar o dispositivo StorSimple hello.

## <a name="unpack-your-storsimple-8100-device"></a>Desempacotar o dispositivo StorSimple 8100
Olá etapas a seguir fornecem claras e instruções detalhadas sobre como toounpack seu dispositivo de armazenamento StorSimple 8100. Este dispositivo é fornecido em uma única caixa.

### <a name="prepare-toounpack-your-device"></a>Preparar toounpack seu dispositivo
Antes de desempacotar seu dispositivo, examine Olá informações a seguir.

![Ícone de aviso](./media/storsimple-safety/IC740879.png)![ícone de peso pesado](./media/storsimple-8100-hardware-installation/HCS_HeavyWeight_Icon.png) **AVISO!**

1. Certifique-se de que você tenha duas pessoas toomanage disponível Olá peso compartimento Olá se você lidar com isso manualmente. Um compartimento completamente configurado pode pesar backup too32 kg (70 lbs).
2. Caixa de saudação do local em uma superfície plana e nivelada.

Em seguida, conclua seu dispositivo Olá toounpack as etapas a seguir.

#### <a name="toounpack-your-device"></a>toounpack seu dispositivo
1. Inspecione a caixa hello e a espuma do pacote procurando Olá para partes amassadas, cortes, danos causados pela água ou quaisquer outros danos óbvios. Olá caixa ou o pacote estiverem muito danificado, não abra Olá caixa. Por favor, [entre em contato com o Microsoft Support](storsimple-contact-microsoft-support.md) toohelp avaliar se o dispositivo hello está em bom estado de funcionamento.
2. Desempacote caixa hello. Olá a imagem a seguir mostra a exibição de Olá desempacotada do seu dispositivo StorSimple.
   
     ![Desempacotar o dispositivo de armazenamento](./media/storsimple-8100-hardware-installation/HCSUnpackyour2Udevice.png)
   
    **Exibição do dispositivo de armazenamento desempacotado**
   
   | Rótulo | Descrição |
   | --- | --- |
   |   1 |Embalagem |
   |   2 |Espuma inferior |
   |   3 |Dispositivo |
   |   4 |Espuma superior |
   |   5 |Caixa de acessório |
3. Após desempacotar a caixa de saudação, certifique-se de que você tem:
   
   * 1 único dispositivo de compartimento
   * 2 cabos de energia
   * 1 cabo cruzado Ethernet
   * 2 cabos seriais de console
   * 1 conversor serial USB para acesso serial
   * 1 chave de fenda T10 à prova de violação
   * 4 adaptadores QSFP para SFP+ para serem usados com interfaces de rede de 10 GbE
   * 1 kit de montagem em rack (2 trilhos laterais com hardware de montagem)
   * Documentação de Introdução
     
     Se você não recebeu qualquer um dos itens de saudação listados acima, [entre em contato com o Microsoft Support](storsimple-contact-microsoft-support.md).

próxima etapa do Hello é toorack montar seu dispositivo.

## <a name="rack-mount-your-storsimple-8100-device"></a>Montar em rack o dispositivo StorSimple 8100
Siga Olá próxima etapas tooinstall seu dispositivo de armazenamento StorSimple 8100 em um rack padrão de 19 polegadas com colunas frontais e traseiras. dispositivo Olá StorSimple 8100 tem um único compartimento primário.

instalação de saudação consiste em várias etapas, cada uma delas é discutida em Olá procedimentos a seguir.

> [!IMPORTANT]
> Os dispositivos StorSimple devem ser montados em rack para a operação apropriada.
> 
> 

### <a name="prepare-hello-site"></a>Preparar site Olá
dispositivo Olá deve ser instalado em um rack padrão de 19 polegadas com colunas frontais e traseiras. Use Olá seguindo o procedimento tooprepare para instalação do rack.

#### <a name="tooprepare-hello-site-for-rack-installation"></a>site de saudação tooprepare para instalação do rack
1. Certifique-se de que o dispositivo Olá fique em um trabalho plano, estável e nivelado superfície (ou semelhante).
2. Verifique se o site de saudação onde você pretende tooset backup tem alimentação de CA padrão de uma fonte independente ou fornecimento de uma unidade de distribuição de alimentação (PDU) rack com uma fonte de alimentação ininterrupta (UPS).
3. Certifique-se de que slot um 2U está disponível no rack Olá no qual você pretende que o dispositivo de saudação toomount.

![Ícone de aviso](./media/storsimple-safety/IC740879.png)![ícone de peso pesado](./media/storsimple-8100-hardware-installation/HCS_HeavyWeight_Icon.png) **AVISO!**

Certifique-se de que você tenha o peso de saudação do duas pessoas toomanage disponível se você estiver tratando a configuração do dispositivo Olá manualmente. Um compartimento completamente configurado pode pesar backup too32 kg (70 lbs).

### <a name="rack-prerequisites"></a>Pré-requisitos do rack
compartimento 8100 Olá destina-se a instalação em um rack padrão de 19 polegadas gabinete com:

* Profundidade mínima de 27,84 polegadas de rack post toopost.
* Peso máximo de 32 kg para o dispositivo de saudação
* Pressão de retorno máxima de 5 Pascal (medidor de água de 0,5 mm).

### <a name="rack-mounting-rail-kit"></a>Kit do trilho de montagem em rack
Um conjunto de trilhos de montagem é fornecido para uso com o gabinete do rack de 19 polegadas hello. trilhos Olá foram testados peso do toohandle Olá máximo do compartimento. Esses trilhos também permitirão a instalação de diversos compartimentos sem qualquer perda de espaço no rack hello.

#### <a name="tooinstall-hello-device-on-hello-rails"></a>dispositivo de saudação tooinstall trilhos Olá
1. Execute esta etapa somente se não houver trilhos internos instalados em seu dispositivo. Normalmente, trilhos interna Olá são instalados na fábrica de saudação. Se rails não estiverem instalados, instale os lados de toohello Olá slides trilho esquerdo e direito de compartimento do chassi hello. Elas são presas por seis parafusos métricos em cada lado. toohelp com orientação, trilho Olá deslizantes estão marcados como **LH – Front** e **RH – Front**, e o final de saudação que é afixada em direção à parte posterior de saudação do compartimento de saudação possui uma extremidade afunilada.<br/>
   
    ![Anexando trilhos deslizantes tooenclosure chassi](./media/storsimple-8100-hardware-installation/HCSAttachingRailSlidestoEnclosureChassis.png)

    **Anexando trilhos interno slides toohello laterais do compartimento Olá**
   
    Rótulo | Descrição
    ----- | -----------
    1     | Parafusos de cabeça abaulada M 3x4
    2     | Corrediças dos chassis

2. Anexe o trilho esquerdo externa de saudação e externa direita assemblies toohello gabinete verticais do rack. Olá suportes estão marcados **LH**, **RH**, e **este lado para cima** tooguide você durante a saudação corrigir orientação.
3. Localize os pinos dos trilhos de saudação na frente de saudação e atrás do assembly do trilho hello. Estender Olá trilho toofit entre colunas do rack hello e inserir pins Olá frontal hello e vertical do post de traseira furos. Certifique-se de que o assembly do trilho Olá é nível.
4. Use dois Olá fornecido parafusos métricos toosecure Olá trilho assembly toohello verticais do rack. Use um parafuso na frente hello e outro na traseira hello.
5. Repita essas etapas para Olá outro assembly do trilho.<br/>
   
     ![Anexando trilhos deslizantes toorack gabinete](./media/storsimple-8100-hardware-installation/HCSAttachingRailSlidestoRackCabinet.png)
   
    **Anexando trilhos externa assemblies toohello rack**
   
   | Rótulo | Descrição |
   | --- | --- |
   |   1 |Parafuso de travamento |
   |   2 |Parafuso da coluna do rack frontal para orifício quadrado |
   |   3 |Pinos de localização do trilho frontal esquerdo |
   |   4 |Parafuso de travamento |
   |   5 |Pinos de localização do trilho traseiro esquerdo |

### <a name="mounting-hello-device-in-hello-rack"></a>Montando Olá dispositivo no rack Olá
Usando os trilhos do rack Olá que acabaram de ser instalados, execute Olá após o dispositivo de saudação toomount etapas em rack Olá.

#### <a name="toomount-hello-device"></a>dispositivo de saudação toomount
1. Com um assistente, levante o compartimento de saudação e alinhe-o com os trilhos do rack hello.
2. Cuidadosamente inserir dispositivo Olá trilhos Olá e, em seguida, enviar por push dispositivo Olá completamente em rack Olá gabinete.<br/>
   
    ![Inserindo dispositivo no rack Olá](./media/storsimple-8100-hardware-installation/HCSInsertingDeviceintheRack.png)
   
    **Montando Olá dispositivo no rack Olá**
3. Remova Olá esquerda e tampas do flange frontal direito puxando as tampas hello. Tampas do flange Olá flanges encaixam nos flanges hello.
4. Fixe o compartimento de saudação em rack Olá instalando um parafuso Phillips fornecido por meio de cada flange, direito e esquerdo.
5. Instale as tampas do flange Olá pressionando-as para a posição e encaixando-as no lugar.<br/>
   
     ![Instalando as tampas do flange](./media/storsimple-8100-hardware-installation/HCSInstallingFlangeCaps.png)
   
    **Instalando tampas do flange Olá**
   
   | Rótulo | Descrição |
   | --- | --- |
   |   1 |Parafuso de fixação do compartimento |

próxima etapa do Hello é toocable de energia, rede e acesso serial do seu dispositivo.

## <a name="cable-your-storsimple-8100-device"></a>Cabear o dispositivo StorSimple 8100
Olá procedimentos a seguir explicam como toocable seu dispositivo StorSimple 8100 à energia, rede e conexões de série.

### <a name="prerequisites"></a>Pré-requisitos
Antes de começar a saudação cabeamento do seu dispositivo, você precisará:

* Seu dispositivo de armazenamento totalmente desempacotado e montado no rack.
* 2 cabos de energia que acompanham o dispositivo
* Acesso too2 PDUs (recomendado).
* Cabos de rede
* Cabos seriais fornecidos
* Conversor serial USB com o driver apropriado de saudação instalado em seu PC (se necessário)
* Quatro adaptadores QSFP para SFP+ para serem usados com interfaces de rede de 10 GbE
* [Hardware com suporte para interfaces de rede Olá 10 GbE no seu dispositivo StorSimple](storsimple-supported-hardware-for-10-gbe-network-interfaces.md)

### <a name="power-cabling"></a>Cabeamento de energia
Seu dispositivo inclui PCMs (Módulos de Energia e Refrigeração) redundantes. Ambos os PCMs devem ser instalados e conectados toodifferent power fontes tooensure alta disponibilidade.

Execute Olá toocable as etapas a seguir seu dispositivo de alimentação.

[!INCLUDE [storsimple-cable-8100-for-power](../../includes/storsimple-cable-8100-for-power.md)]

### <a name="network-cabling"></a>Cabeamento de rede
O dispositivo é uma configuração ativa / em espera: em um determinado momento, um módulo do controlador está ativo e processa todas as operações de disco e rede durante a saudação outro módulo do controlador está em estado de espera. Se um controlador falhar, o controlador em espera Olá é ativado imediatamente e continua a todas as operações de rede e disco hello.

toosupport esse failover de controlador redundante, você precisa toocable seu dispositivo de rede conforme descrito em Olá etapas a seguir.

#### <a name="toocable-for-network-connection"></a>toocable para conexão de rede
1. Seu dispositivo tem seis interfaces de rede em cada controlador: quatro de 1 Gbps e duas portas Ethernet de 10 Gbps. Identifica Olá dados de várias portas no backplane de saudação do seu dispositivo.
   
    ![Backplane do dispositivo 8100](./media/storsimple-8100-hardware-installation/HCSBackplaneof2UDevicewithPortsLabeled.jpg)
   
    **Parte posterior do dispositivo Olá mostrando as portas de dados**
   
   | Rótulo | Descrição |
   | --- | --- |
   |   0,1,4,5 |Interfaces de rede de 1 GbE |
   |   2,3 |Interfaces de rede de 10 GbE |
   |   6 |Portas seriais |
2. Consulte Olá diagrama de cabeamento de rede a seguir. (configuração de rede mínima de Olá é representada por linhas azuis sólidas. Uma configuração adicional será necessária para alta disponibilidade e desempenho e é mostrada pelas linhas pontilhadas).

    ![Cabear o dispositivo 2U para rede](./media/storsimple-8100-hardware-installation/HCSCableYour2UDeviceforNetwork.png)

    **Cabeamento de rede para o dispositivo**

   |Rótulo | Descrição |
   |----- | ----------- |
   | Uma    | LAN com acesso à Internet |
   | B    | Controlador 0 |
   | C    | PCM 0 |
   | D    | Controlador 1 |
   | E    | PCM 1 |
   | F, G | Hosts |
   | 0-5  | Interfaces de rede |



Quando o cabeamento dispositivo hello, requer configuração mínima de saudação:

* Pelo menos duas interfaces de rede conectadas em cada controlador com uma para acesso à nuvem e outra para iSCSI. Olá DATA 0 porta é habilitada e configurada por meio do console serial do dispositivo Olá Olá automaticamente. Além da DATA 0, outra porta de dados também precisa toobe configurado por meio de saudação portal clássico do Azure. Nesse caso, conecte-se a DATA 0 porta toohello primário LAN (rede com acesso à Internet). Olá outros dados portas podem ser conectado tooSAN/iSCSI segmento de VLAN (LAN) da rede hello, dependendo da função de saudação que se destina.
* Interfaces idênticas em cada controlador conectado toohello mesma rede tooensure disponibilidade se ocorrer um failover de controlador. Por exemplo, se você escolher tooconnect DATA 0 e 3 de dados para um dos controladores Olá, você precisa tooconnect Olá correspondente DATA 0 e DATA 3 em Olá outro controlador.

Lembre-se disso no caso de alta disponibilidade e desempenho:

* Quando for possível, configure um par de interfaces de rede para acesso à nuvem (1 GbE) e outro par para iSCSI (10 GbE recomendados) em cada controlador.
* Quando possível, conecte-se interfaces de rede de cada tooensure disponibilidade do controlador tootwo opções diferentes em relação a uma falha do interruptor. Figura Olá ilustra Olá duas de 10 GbE interfaces de rede, DATA 2 e 3 de dados de cada controlador conectado tootwo diferentes comutadores.

Para obter mais informações, consulte toohello **interfaces de rede** em Olá [requisitos de alta disponibilidade para seu dispositivo StorSimple](storsimple-system-requirements.md#high-availability-requirements-for-storsimple).

> [!NOTE]
> Se você estiver usando transceptores SFP + com suas interfaces de rede 10 GbE, use Olá fornecido QSFP-SFP + adaptadores. Para obter mais informações, vá muito[hardware suportado Olá 10 GbE para interfaces de rede em seu dispositivo StorSimple](storsimple-supported-hardware-for-10-gbe-network-interfaces.md).
> 
> 

### <a name="serial-port-cabling"></a>Cabeamento de porta serial
Execute Olá toocable as etapas a seguir em sua porta serial.

#### <a name="toocable-for-serial-connection"></a>toocable para conexão serial
1. O dispositivo tem uma porta serial em cada controlador que é identificada por um ícone de chave inglesa. Consulte a ilustração toohello Olá [cabeamento de rede](#network-cabling) seção toolocate Olá portas seriais backplane de saudação do seu dispositivo.
2. Identificar controlador ativo de saudação em seu plano posterior do dispositivo. Um LED azul piscando indica que Olá controlador está ativo.
3. Use os cabos de série do hello fornecido (se necessário, conversor de saudação serial USB do seu laptop) e conecte seu console ou computador (com o dispositivo de toohello de emulação de terminal) de porta serial do controlador ativo Olá toohello.
4. Instale drivers de serial USB do hello (fornecidos com o dispositivo Olá) em seu computador.
5. Configurar conexão serial Olá da seguinte maneira: 115.200 baud, 8 bits de dados, 1 bit de parada, sem paridade e controle de fluxo definem tooNone.
6. Verificar se a conexão hello está funcionando pressionando Enter no console de saudação. Um menu de console serial deve aparecer.

> [!NOTE]
> **Gerenciamento de falta de**: quando o dispositivo de saudação é instalado em um data center remoto ou em uma sala de computadores com acesso limitado, certifique-se de que controladores de tooboth Olá conexões de série são sempre conectados tooa interruptor de console de série ou equipamento similar. Isso permite operações de suporte e controle remoto fora de banda se houver interrupções na rede ou falhas inesperadas.
> 
> 

Agora o dispositivo está cabeado para energia, acesso à rede e conectividade serial. Olá próxima etapa é tooconfigure Olá software e implantar seu dispositivo.

## <a name="next-steps"></a>Próximas etapas
Saiba como muito[implantar e configurar o dispositivo StorSimple local](storsimple-deployment-walkthrough-u2.md).

