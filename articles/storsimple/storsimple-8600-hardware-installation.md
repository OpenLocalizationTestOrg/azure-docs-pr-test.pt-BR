---
title: dispositivo aaaInstall Microsoft Azure StorSimple 8600 | Microsoft Docs
description: "Descreve como toounpack, montagem em rack e fazer o cabeamento do seu dispositivo 8600 StorSimple antes de implantar e configurar o software de saudação."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3d82ba5f-3e34-40dc-9c33-50f952bc6be8
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 10/24/2016
ms.author: alkohli
ms.openlocfilehash: 0fc0ddf076725fededdde33a260b950b72edc8db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="unpack-rack-mount-and-cable-your-storsimple-8600-device"></a>Desembalar, montar em rack e cabear o dispositivo StorSimple 8600.
## <a name="overview"></a>Visão geral
Seu Microsoft Azure StorSimple 8600 é um dispositivo de compartimento duplo e consiste em um compartimento principal e um EBOD. Este tutorial explica como toounpack de montagem em rack e cabo Olá hardware do dispositivo StorSimple 8600 antes de configurar o software de StorSimple hello.

## <a name="unpack-your-storsimple-8600-device"></a>Desempacotar o dispositivo StorSimple 8600
Olá etapas a seguir fornecem claras e instruções detalhadas sobre como toounpack seu dispositivo de armazenamento StorSimple 8600. Este dispositivo é enviado em duas caixas, uma para o compartimento principal hello e outra para Olá compartimento EBOD. Em seguida, essas duas caixas são colocadas em uma única caixa.

### <a name="prepare-toounpack-your-device"></a>Preparar toounpack seu dispositivo
Antes de desempacotar seu dispositivo, examine Olá informações a seguir.

![Ícone de aviso](./media/storsimple-safety/IC740879.png)![ícone de peso pesado](./media/storsimple-8600-hardware-installation/HCS_HeavyWeight_Icon.png) **AVISO!**

1. Certifique-se de que você tenha duas pessoas disponíveis toomanage Olá peso dispositivo Olá se você lidar com isso manualmente. Um compartimento completamente configurado pode pesar backup too32 kg (70 lbs).
2. Caixa de saudação do local em uma superfície plana e nivelada.

Em seguida, conclua seu dispositivo Olá toounpack as etapas a seguir.

#### <a name="toounpack-your-device"></a>toounpack seu dispositivo
1. Inspecione a caixa hello e a espuma do pacote procurando Olá para partes amassadas, cortes, danos causados pela água ou quaisquer outros danos óbvios. Olá caixa ou o pacote estiverem muito danificado, não abra Olá caixa. Por favor, [entre em contato com o Microsoft Support](storsimple-contact-microsoft-support.md) toohelp avaliar se o dispositivo hello está em bom estado de funcionamento.
2. Abrir a caixa externa Olá e, em seguida, tire duas caixas de saudação correspondente tooprimary e compartimentos EBOD. Agora é possível desempacotar hello primário e compartimentos EBOD. Olá figura a seguir mostra a exibição de saudação desempacotada de um dos compartimentos de saudação.
   
    ![Desempacotar o dispositivo de armazenamento](./media/storsimple-8600-hardware-installation/HCSUnpackyour4Udevice.png)
   
    **Exibição do dispositivo de armazenamento desempacotado**
   
   | Rótulo | Descrição |
   | --- | --- |
   |   1 |Embalagem |
   |   2 |Cabos SAS (na bandeja de acessórios e cabos) |
   |   3 |Espuma inferior |
   |   4 |Dispositivo |
   |   5 |Espuma superior |
   |   6 |Caixa de acessório |
3. Após desempacotar Olá duas caixas, certifique-se de que você tem:
   
   * 1 compartimento principal (compartimento primário hello e ebod estão em duas caixas separadas)
   * 1 compartimento EBOD
   * 4 cabos de alimentação, 2 em cada caixa
   * 2 cabos SAS (compartimento de tooEBOD tooconnect Olá compartimento principal)
   * 1 cabo cruzado Ethernet
   * 2 cabos seriais de console
   * 1 conversor serial USB para acesso serial
   * 4 adaptadores QSFP para SFP+ para serem usados com interfaces de rede de 10 GbE
   * 2 montagem kits rack (4 trilhos laterais com hardware de montagem, 2 para o compartimento primário hello e ebod), 1 em cada caixa
   * Documentação de Introdução
     
     Se você não recebeu qualquer um dos itens de saudação listados acima, [entre em contato com o Microsoft Support](storsimple-contact-microsoft-support.md).  

próxima etapa do Hello é toorack montar seu dispositivo.

## <a name="rack-mount-your-storsimple-8600-device"></a>Montar em rack o dispositivo StorSimple 8600
Siga Olá próxima etapas tooinstall seu dispositivo de armazenamento StorSimple 8600 em um rack padrão de 19 polegadas com colunas frontais e traseiras. Esse dispositivo é fornecido com dois compartimentos: um principal e um EBOD. Ambos precisam toobe montados em rack.

instalação de saudação consiste em várias etapas, cada uma delas é discutida em Olá procedimentos a seguir.

> [!IMPORTANT]
> Os dispositivos StorSimple devem ser montados em rack para a operação apropriada.
> 
> 

### <a name="site-preparation"></a>Preparação do local
compartimentos de saudação devem ser instalados em um rack padrão de 19 polegadas com colunas frontais e traseiras. Use Olá seguindo o procedimento tooprepare para instalação do rack.

#### <a name="tooprepare-hello-site-for-rack-installation"></a>site de saudação tooprepare para instalação do rack
1. Certifique-se de que Olá primário e compartimentos EBOD são repouso com segurança em uma superfície de trabalho plana, estável e nivelada (ou semelhante).
2. Verifique se o site Olá onde você pretende tooset backup tem CA alimentação de uma fonte independente ou um unidade de distribuição de alimentação (PDU) do rack com uma fonte de alimentação ininterrupta (UPS).
3. Verifique se que esse slot de um 4U (2 X 2U) está disponível no rack Olá no qual você pretende toomount compartimentos de saudação.

![Ícone de aviso](./media/storsimple-safety/IC740879.png)![ícone de peso pesado](./media/storsimple-8600-hardware-installation/HCS_HeavyWeight_Icon.png) **AVISO!**

 Certifique-se de que você tenha o peso de saudação do duas pessoas toomanage disponível se você estiver tratando a configuração do dispositivo Olá manualmente. Um compartimento completamente configurado pode pesar backup too32 kg (70 lbs).

### <a name="rack-prerequisites"></a>Pré-requisitos do rack
Olá compartimentos são projetados para instalação em um rack padrão de 19 polegadas gabinete com:

* Profundidade mínima de 27,84 polegadas de rack lançar toopost
* Peso máximo de 32 kg para o dispositivo de saudação
* Pressão de retorno máxima de 5 Pascal (medidor de água de 0,5 mm)

### <a name="rack-mounting-rail-kit"></a>Kit do trilho de montagem em rack
Um conjunto de trilhos de montagem será fornecido para uso com o gabinete do rack de 19 polegadas hello. trilhos Olá foram testados peso do toohandle Olá máximo do compartimento. Esses trilhos também permitirão a instalação de diversos compartimentos sem perda de espaço no rack hello. Instale primeiro o compartimento EBOD de saudação.

#### <a name="tooinstall-hello-ebod-enclosure-on-hello-rails"></a>Olá tooinstall compartimento EBOD nos trilhos Olá
1. Execute esta etapa somente se não houver trilhos internos instalados em seu dispositivo. Normalmente, trilhos interna Olá são instalados na fábrica de saudação. Se rails não estiverem instalados, instale os lados de toohello Olá slides trilho esquerdo e direito de compartimento do chassi hello. Elas são presas por seis parafusos métricos em cada lado. toohelp com orientação, trilho Olá deslizantes estão marcados como **LH – Front** e **RH – Front**, e o final de saudação que é afixada em direção à parte posterior de saudação do compartimento de saudação possui uma extremidade afunilada.
   
    ![Anexando trilhos deslizantes tooenclosure chassi](./media/storsimple-8600-hardware-installation/HCSAttachingRailSlidestoEnclosureChassis.png)
   
    **Anexando trilhos deslizantes toohello laterais do compartimento Olá**
   
   | Rótulo | Descrição |
   | --- | --- |
   |  1 |Parafusos de cabeça abaulada M 3x4 |
   |  2 |Corrediças dos chassis |
2. Anexe o trilho esquerdo hello e à direita assemblies toohello gabinete verticais do rack. Olá suportes estão marcados **LH**, **RH**, e **este lado para cima** tooguide você orientação correta.
3. Localize os pinos dos trilhos de saudação na frente de saudação e atrás do assembly do trilho hello. Estender Olá trilho toofit entre colunas do rack hello e inserir os pins Olá Olá post frontal e traseira rack vertical furos. Certifique-se de que o assembly do trilho Olá é nível.
4. Proteger Olá rack de toohello assembly trilho membros verticais usando dois dos parafusos métricos Olá fornecidos. Use um parafuso na frente hello e outro na traseira hello.
5. Repita essas etapas para Olá outro assembly do trilho.
   
     ![Anexando trilhos deslizantes toorack gabinete](./media/storsimple-8600-hardware-installation/HCSAttachingRailSlidestoRackCabinet.png)
   
    **Anexando trilhos assemblies toohello rack**
   
   | Rótulo | Descrição |
   | --- | --- |
   |   1 |Parafuso de travamento |
   |   2 |Parafuso da coluna do rack frontal para orifício quadrado |
   |   3 |Pinos de localização do trilho frontal esquerdo |
   |   4 |Parafuso de travamento |
   |   5 |Pinos de localização do trilho posterior esquerdo |

### <a name="mounting-hello-ebod-enclosure-in-hello-rack"></a>Montar o compartimento EBOD de saudação em rack Olá
Usando os trilhos do rack Olá que acabaram de ser instalados, execute Olá compartimento do etapas toomount Olá EBOD no rack Olá a seguir.

#### <a name="toomount-hello-ebod-enclosure"></a>Olá toomount compartimento EBOD
1. Com um assistente, levante o compartimento de saudação e alinhe-o com os trilhos do rack hello.
2. Insira cuidadosamente compartimento Olá na trilhos hello e distribuí-lo completamente em rack Olá gabinete.
   
    ![Inserindo dispositivo no rack Olá](./media/storsimple-8600-hardware-installation/HCSInsertingDeviceintheRack.png)
   
    **Montar Olá compartimento no rack Olá**
3. Remova Olá esquerda e tampas do flange frontal direito puxando as tampas hello. Tampas do flange Olá flanges encaixam nos flanges hello.
4. Fixe o compartimento de saudação em rack Olá instalando um parafuso Phillips fornecido por meio de cada flange, direito e esquerdo.
5. Instale as tampas do flange Olá pressionando-as para a posição e colocando-as no lugar.
   
     ![Instalando as tampas do flange](./media/storsimple-8600-hardware-installation/HCSInstallingFlangeCaps.png)
   
    **Instalando tampas do flange Olá**
   
   | Rótulo | Descrição |
   | --- | --- |
   |   1 |Parafuso de fixação do compartimento |

### <a name="mounting-hello-primary-enclosure-in-hello-rack"></a>Montar o compartimento principal de saudação em rack Olá
Depois de montar o compartimento do EBOD hello, você precisará de compartimento primário do toomount Olá seguinte Olá mesmas etapas.

> [!NOTE]
> * É possível toohave alguns slots vazios no hello rack entre o compartimento principal hello e compartimento do EBOD hello.
> * Use Olá fornecido 2M SAS cabo tooconnect Olá compartimento principal toohello compartimento EBOD.
> * Não há restrições na posição relativa de saudação da unidade do hello unidade principal toohello EBOD. Portanto, compartimento principal Olá pode ser colocado no slot superior hello e ebod Olá abaixo — ou vice-versa.
> 
> 

próxima etapa do Hello é toocable de energia, rede e acesso serial do seu dispositivo.

## <a name="cable-your-storsimple-8600-device"></a>Cabear o dispositivo StorSimple 8600
Olá procedimentos a seguir explicam como toocable seu dispositivo 8600 StorSimple para energia, rede e conexões de série.

### <a name="prerequisites"></a>Pré-requisitos
Antes de começar toocable seu dispositivo, você precisará:

* O compartimento principal e o compartimento do EBOD hello, totalmente desempacotados
* 4 cabos de alimentação (2 de cada para Olá primário e hello compartimento EBOD) que acompanham o dispositivo
* 2 cabos SAS fornecidos com hello tooconnect de dispositivo Olá compartimento do EBOD compartimento toohello principal
* Acesso too2 PDUs (PDUs) (recomendado)
* Cabos de rede
* Cabos seriais fornecidos
* Conversor serial USB com driver apropriado de saudação instalado em seu PC (se necessário)
* Quatro adaptadores QSFP para SFP+ para serem usados com interfaces de rede de 10 GbE
* [Hardware com suporte para interfaces de rede Olá 10 GbE no seu dispositivo StorSimple](storsimple-supported-hardware-for-10-gbe-network-interfaces.md)

### <a name="sas-and-power-cabling"></a>Cabeamento de energia e SAS
O dispositivo tem um compartimento principal e um compartimento EBOD. Isso requer Olá unidades toobe cabeada de alimentação e conectividade de SCSI Serial anexado (SAS).

Ao configurar este dispositivo para Olá primeira vez, execute as etapas de saudação para cabeamento SAS primeiro hello, em seguida, concluir etapas para cabeamento de alimentação.

[!INCLUDE [storsimple-cable-8600-for-SAS](../../includes/storsimple-sas-cable-8600.md)]

[!INCLUDE [storsimple-cable-8600-for-power](../../includes/storsimple-cable-8600-for-power.md)]

### <a name="network-cabling"></a>Cabeamento de rede
O dispositivo está em uma configuração ativa / em espera: em um determinado momento, um módulo do controlador está ativo e processa todas as operações de disco e rede durante a saudação outro módulo do controlador está em estado de espera. Se ocorrer uma falha do controlador, controlador em espera Olá ativa imediatamente e continua a todas as operações de rede e disco hello.

toosupport esse failover de controlador redundante, você precisa toocable seu dispositivo de rede conforme Olá etapas a seguir.

#### <a name="toocable-for-network-connection"></a>toocable para conexão de rede
1. Seu dispositivo tem seis interfaces de rede em cada controlador: quatro de 1 Gbps e duas portas Ethernet de 10 Gbps. Consulte toohello seguintes portas de dados ilustração tooidentify Olá Olá backplane do seu dispositivo.
   
     ![Backplane do dispositivo 8600](./media/storsimple-8600-hardware-installation/HCSBackplaneof2UDevicewithPortsLabeled.jpg)
   
    **Parte posterior do seu dispositivo mostrando Olá portas de dados**
   
   | Rótulo | Descrição |
   | --- | --- |
   |   0,1,4,5 |Interfaces de rede de 1 GbE |
   |   2,3 |Interfaces de rede de 10 GbE |
   |   6 |Portas seriais |
2. Consulte Olá diagrama de cabeamento de rede a seguir. (configuração de rede mínima de Olá é representada por linhas azuis sólidas. Para alta disponibilidade e desempenho, a configuração adicional necessária é mostrada pelas linhas pontilhadas).

![Cabear o dispositivo 4U para rede](./media/storsimple-8600-hardware-installation/HCSCableYour4UDeviceforNetwork.png)

**Cabeamento de rede para o dispositivo**

| Rótulo | Descrição |
| --- | --- |
| Uma |LAN com acesso à Internet |
| B |Controlador 0 |
| C |PCM 0 |
| D |Controlador 1 |
| E |PCM 1 |
| F |Controlador 0 do EBOD |
| G |Controlador 1 do EBOD |
| H,I |Hosts (por exemplo, servidores de arquivos) |
| 0-5 |Interfaces de rede |
| 6 |Compartimento principal |
| 7 |Compartimento EBOD |

Quando o cabeamento dispositivo hello, requer configuração mínima de saudação:

* Pelo menos duas interfaces de rede conectadas em cada controlador com uma para acesso à nuvem e outra para iSCSI. Olá DATA 0 porta é habilitada e configurada por meio do console serial do dispositivo Olá Olá automaticamente. Além da DATA 0, outra porta de dados também precisa toobe configurado por meio de saudação portal clássico do Azure. Nesse caso, conecte-se a DATA 0 porta toohello primário LAN (rede com acesso à Internet). Olá outros dados portas podem ser conectado tooSAN/iSCSI segmento de VLAN (LAN) da rede hello, dependendo da função de saudação que se destina.
* Interfaces idênticas em cada controlador conectado toohello mesma rede tooensure disponibilidade se ocorrer um failover de controlador. Por exemplo, se você escolher tooconnect DATA 0 e 3 de dados para um dos controladores Olá, você precisa tooconnect Olá correspondente DATA 0 e DATA 3 em Olá outro controlador.

Lembre-se disso no caso de alta disponibilidade e desempenho:

* Quando for possível, configure um par de interfaces de rede para acesso à nuvem (1 GbE) e outro par para iSCSI (10 GbE recomendados) em cada controlador.
* Quando possível, conecte-se interfaces de rede de cada tooensure disponibilidade do controlador tootwo opções diferentes em relação a uma falha do interruptor. Figura Olá ilustra Olá duas de 10 GbE interfaces de rede, DATA 2 e 3 de dados de cada controlador conectado tootwo diferentes comutadores. Para obter mais informações, consulte toohello **interfaces de rede** em Olá [requisitos de alta disponibilidade para seu dispositivo StorSimple](storsimple-system-requirements.md#high-availability-requirements-for-storsimple).

> [!NOTE]
> Se usar transceptores SFP + com suas interfaces de rede 10 GbE, use Olá fornecido QSFP-SFP + adaptadores. Para obter mais informações, vá muito[hardware suportado Olá 10 GbE para interfaces de rede em seu dispositivo StorSimple](storsimple-supported-hardware-for-10-gbe-network-interfaces.md).
> 
> 

### <a name="serial-port-cabling"></a>Cabeamento de porta serial
Execute Olá toocable as etapas a seguir em sua porta serial.

#### <a name="toocable-for-serial-connection"></a>toocable para conexão serial
1. O dispositivo tem uma porta serial em cada controlador que é identificada por um ícone de chave inglesa. portas seriais do toolocate hello, consulte toohello ilustração que mostra as portas de dados de saudação em Olá parte posterior do seu dispositivo.
2. Identificar controlador ativo de saudação em seu plano posterior do dispositivo. Um LED azul piscando indica que Olá controlador está ativo.
3. Use Olá fornecido o cabo serial (se necessário, conversor de saudação serial USB do seu laptop) e conecte seu console ou computador (com o dispositivo de toohello de emulação de terminal) de porta serial do controlador ativo Olá toohello.
4. Instale drivers de serial USB do hello (fornecidos com o dispositivo Olá) em seu computador.
5. Configure conexão serial Olá da seguinte maneira:
   
   * 115.200 bauds
   * 8 bits de dados
   * 1 bit de parada
   * Sem paridade
   * Controle de fluxo definido muito**None**
6. Verificar se a conexão hello está funcionando pressionando Enter no console de saudação. Um menu de console serial deve aparecer.

> [!NOTE]
> **Gerenciamento de falta de:** quando o dispositivo de saudação é instalado em um data center remoto ou em uma sala de computadores com acesso limitado, certifique-se de que controladores de tooboth Olá conexões de série são sempre conectados tooa interruptor de console de série ou equipamento similar. Isso permite operações de suporte e controle remoto fora de banda em caso de interrupção na rede ou falhas inesperadas.
> 
> 

Você concluiu a conexão dos cabos de alimentação, acesso à rede, seu dispositivo e connection.hello serial próxima etapa é um software de saudação do tooconfigure em seu dispositivo.

## <a name="next-steps"></a>Próximas etapas
Agora você está pronto muito[implantar e configurar o dispositivo StorSimple local](storsimple-deployment-walkthrough-u2.md).

