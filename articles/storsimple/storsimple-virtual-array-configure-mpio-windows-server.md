---
title: aaaConfigure MPIO no host conectado tooStorSimple Array Virtual | Microsoft Docs
description: Descreve como tooconfigure Multipath i/o (MPIO) para sua matriz Virtual StorSimple conectados tooa host executando o Windows Server 2012 R2.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 5b7a7f99-ee5b-4b7d-ab32-483a5a1fa504
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/01/2017
ms.author: alkohli
ms.openlocfilehash: 0e6df23bba29395329685cbf2c968675abb04cfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multipath-io-on-windows-server-host-for-hello-storsimple-virtual-array"></a>Configurar o Multipath i / o no host do Windows Server para Olá matriz Virtual StorSimple
## <a name="overview"></a>Visão geral
Este artigo descreve como tooinstall recurso de Multipath i / (o MPIO) no host do Windows Server, aplique as configurações específicas para volumes somente StorSimple e, em seguida, verificar o MPIO para volumes do StorSimple. Olá presume que sua matriz Virtual StorSimple 1200 com duas interfaces de rede está conectado tooa host do Windows Server com duas interfaces de rede. Olá informações neste artigo se aplicam apenas toohello matriz virtual. Para obter informações sobre dispositivos da série StorSimple 8000, vá muito[configurar MPIO para StorSimple host](storsimple-configure-mpio-windows-server.md). 

recurso MPIO Olá em configurações de armazenamento altamente disponível e tolerante a falhas do Windows Server ajuda a compilação. MPIO usa componentes de caminho físico com redundância – adaptadores, cabos e comutadores – toocreate de caminhos lógicos entre o servidor de saudação e o dispositivo de armazenamento hello. Se houver uma falha de componente, fazendo com que um caminho lógico toofail, lógica de múltiplos caminhos usará um caminho alternativo de e/s para que os aplicativos ainda possam acessar seus dados. Além disso dependendo da configuração do MPIO também pode melhorar desempenho, novamente no balanceamento de carga de saudação em todos esses caminhos. Para obter mais informações, consulte [Visão geral do MPIO](https://technet.microsoft.com/library/cc725907.aspx "Visão geral do MPIO and features").

Para Olá alta disponibilidade da sua solução StorSimple, configure o MPIO no hello tooyour do Windows Server hosts conectado StorSimple Virtual Array (modelo 1200). servidores de host Hello, em seguida, podem tolerar um link, rede ou falhas de interface. 

Você precisará toofollow tooconfigure essas etapas MPIO: 

* Pré-requisitos de configuração
* Etapa 1: Instalar o MPIO no host do Windows Server Olá
* Etapa 2: configurar o MPIO para os volumes StorSimple
* Etapa 3: Montar volumes do StorSimple no host de saudação

Cada Olá acima etapas é discutida em Olá seções a seguir.

## <a name="prerequisites"></a>Pré-requisitos
Esta seção fornece detalhes sobre os pré-requisitos de configuração Olá para o host do servidor Windows hello e sua matriz virtual.

### <a name="on-windows-server-host"></a>No host do Windows Server
* Verifique se o servidor do Windows Server tem duas interfaces de rede habilitadas.

### <a name="on-storsimple-virtual-array"></a>Na matriz virtual do StorSimple
* matriz de saudação virtual deve ser configurado como um servidor do iSCSI. mais, consulte toolearn [configurar virtual array como um servidor iSCSI](storsimple-virtual-array-deploy3-iscsi-setup.md). Uma ou mais interfaces de rede devem ser habilitadas na matriz de saudação.   
* interfaces de rede de saudação em sua matriz virtual devem ser acessíveis a partir do host do servidor Windows hello.
* Um ou mais volumes devem ser criados na Matriz Virtual StorSimple. mais, consulte toolearn [adicionar um volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume) no StorSimple Virtual Array. Neste procedimento, criamos 3 volumes (1 localmente fixados e 2 volumes em camadas conforme mostrado abaixo) na matriz virtual hello.
  
    ![mpio0](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio0.png)

### <a name="hardware-configuration-for-storsimple-virtual-array"></a>Configuração do hardware para Matriz Virtual do StorSimple
Olá figura a seguir mostra a configuração de hardware Olá para alta disponibilidade e de vários caminhos de balanceamento de carga para o host do Windows Server e a matriz de Virtual do StorSimple usadas nesse procedimento.

![configuração de hardware do mpio](./media/storsimple-virtual-array-configure-mpio-windows-server/1200hardwareconfig.png)

Conforme mostrado na saudação anterior Figura:

* A Matriz Virtual StorSimple provisionada no Hyper-V é um dispositivo ativo de único nó configurado como um servidor iSCSI.
* Duas interfaces de rede virtual são habilitadas na sua matriz. Em Olá interface da web local do seu virtual array, verificar que duas interfaces de rede são habilitadas, navegando muito**as configurações de rede** conforme mostrado abaixo:
  
    ![Interfaces de rede habilitadas na 1200](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio9.png)
  
    Observação Olá IPv4 endereços de saudação habilitado (Ethernet, Ethernet 2 por padrão) de interfaces de rede e salve para uso posterior no host de saudação.
* Duas interfaces de rede são habilitadas no host do Windows Server. Se hello interfaces conectadas para a matriz e o host estão em Olá mesma sub-rede, haverá 4 caminhos disponíveis. Isso aconteceu Olá neste procedimento. No entanto, se cada interface de rede na interface de matriz e o host Olá está em uma sub-rede IP diferente (e não pode ser roteado), somente 2 caminhos estará disponíveis.

## <a name="step-1-install-mpio-on-hello-windows-server-host"></a>Etapa 1: Instalar o MPIO no host do Windows Server Olá
O MPIO é um recurso opcional no Windows Server e não é instalado por padrão. Ele deve ser instalado como um recurso por meio do Gerenciador de Servidores. tooinstall esse recurso no host do Windows Server, conclua Olá procedimento a seguir.

[!INCLUDE [storsimple-install-mpio-windows-server-host](../../includes/storsimple-install-mpio-windows-server-host.md)]

## <a name="step-2-configure-mpio-for-storsimple-volumes"></a>Etapa 2: configurar o MPIO para os volumes StorSimple
MPIO precisa de volumes do StorSimple tooidentify toobe configurado. volumes do StorSimple da toorecognize tooconfigure MPIO, executar Olá etapas a seguir.

[!INCLUDE [storsimple-configure-mpio-volumes](../../includes/storsimple-configure-mpio-volumes.md)]

## <a name="step-3-mount-storsimple-volumes-on-hello-host"></a>Etapa 3: Montar volumes do StorSimple no host de saudação
Após a configuração do MPIO no Windows Server, volumes criados na matriz de StorSimple Olá podem ser montados e, em seguida, podem levar vantagem do MPIO para redundância. toomount um volume, execute Olá etapas a seguir.

#### <a name="toomount-volumes-on-hello-host"></a>toomount volumes no host de saudação
1. Olá abrir **propriedades do iniciador iSCSI** janela no host do servidor do Windows hello. Vá muito**Gerenciador do servidor > Painel de controle > Ferramentas > iniciador iSCSI**.
2. Em Olá **propriedades do iniciador iSCSI** caixa de diálogo, clique em **descoberta**e, em seguida, clique em **descobrir Portal de destino**.
3. Em Olá **descobrir Portal de destino** caixa de diálogo caixa, Olá a seguir:
   
    1. Insira o endereço IP de Olá Olá primeiro habilitada da interface de rede no StorSimple Virtual Array. Por padrão, seria **Ethernet**. 
    2. Clique em **Okey** tooreturn toohello **propriedades do iniciador iSCSI** caixa de diálogo.
     
    > [!IMPORTANT]
    > Se você estiver usando uma rede privada para as conexões iSCSI, insira o endereço IP de saudação da porta de dados de saudação é a rede privada toohello conectado.
     
4. Repita as etapas 2 e 3 para uma segunda interface de rede (por exemplo, Ethernet 2) na sua matriz. 
5. Selecione Olá **destinos** guia Olá **propriedades do iniciador iSCSI** caixa de diálogo. Para sua matriz virtual, você deve ver a superfície de cada volume como um destino em **Destinos Descobertos**. Nesse caso, três destinos (volumes toothree correspondentes) deve ser descobertos.
   
    ![mpio1](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio1.png)
6. Clique em **conectar** tooestablish uma sessão iSCSI com sua matriz Virtual StorSimple. Um **conectar tooTarget** caixa de diálogo será exibida. Selecione Olá **habilitar vários caminhos** caixa de seleção. Clique em **Avançado**.
   
    ![mpio2](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio2.png)
7. Em Olá **configurações avançadas** caixa de diálogo caixa, Olá a seguir:                                        
   
    1. Em Olá **adaptador Local** lista suspensa, selecione **iniciador Microsoft iSCSI**.
    2. Em Olá **IP do iniciador** lista suspensa, o endereço IP de saudação selecione do host de saudação.
    3. Em Olá **Portal de destino** lista suspensa IP, selecione Olá IP da interface de matriz.
    4. Clique em **Okey** tooreturn toohello **propriedades do iniciador iSCSI** caixa de diálogo.
     
        ![mpio3](./media/storsimple-ova-configure-mpio-windows-server/mpio3.png)

8. Clique em **Propriedades**. 
   
    ![mpio4](./media/storsimple-ova-configure-mpio-windows-server/mpio4.png)

9. Em Olá **propriedades** caixa de diálogo, clique em **adicionar sessão**.
   
   ![mpio5](./media/storsimple-ova-configure-mpio-windows-server/mpio5.png)
10. Em Olá **conectar tooTarget** caixa de diálogo, selecione Olá **habilitar vários caminhos** caixa de seleção. Clique em **Avançado**.
11. Em Olá **configurações avançadas** caixa de diálogo:                                        
    
    1. Em Olá **adaptador Local** lista suspensa, selecione Microsoft iSCSI Initiator.

    2. Em Olá **IP do iniciador** lista suspensa, selecione Olá IP endereço correspondente toohello host. Nesse caso, você está se conectando duas interfaces de rede Olá matriz tooa única interface de rede no host de saudação. Portanto, essa interface é Olá mesmo que é fornecida para Olá primeira sessão.

    3. Em Olá **IP do Portal de destino** lista suspensa, endereço IP selecione Olá Olá segunda interface de dados habilitada na matriz de saudação.

    4. Clique em **Okey** caixa de diálogo de propriedades do iniciador de iSCSI do tooreturn toohello. Você adicionou um segundo toohello destino da sessão.
      
       ![mpio11](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio11.png)
    
    5. Depois de adicionar sessões Olá desejada (caminhos), em Olá **propriedades do iniciador iSCSI** caixa de diálogo, destino Olá selecione e clique em **propriedades**. Na guia de sessões de saudação do hello **propriedades** caixa de diálogo, observe Olá quatro identificadores de sessão que correspondem a toohello possíveis permutações de caminho. toocancel uma sessão, selecione Olá caixa de seleção próxima tooa identificador da sessão e, em seguida, clique em **Disconnect**.

    6. dispositivos tooview apresentados dentro das sessões, selecione Olá **dispositivos** Olá tooconfigure de guia política MPIO para um dispositivo selecionado, clique em **MPIO**.

    7. Olá **detalhes** caixa de diálogo será exibida. Em Olá **MPIO** guia, você pode selecionar Olá apropriado **política de balanceamento de carga** configurações. Você também pode exibir uma saudação **Active** ou **Standby** tipo de caminho.
12. Repita o destino de toohello as etapas 8 a 11 tooadd sessões (caminhos). Com duas interfaces no host hello e duas em matriz virtual hello, você pode adicionar um total de quatro sessões para cada destino. 
    
    ![mpio14](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio14.png)
13. Você precisará toorepeat estas etapas para cada volume (aparece como um destino).
    
    ![mpio15](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio15.png)
14. Abra **gerenciamento do computador** navegando muito**Gerenciador do servidor > Painel de controle > Gerenciamento do computador**. No painel esquerdo do hello, clique em **armazenamento > Gerenciamento de disco**. Olá volumes criados em Olá matriz Virtual StorSimple que são visíveis toothis host aparecerá sob **gerenciamento de disco** como novos discos.
15. Inicializar disco hello e crie um novo volume. Durante o processo de formatação hello, selecione um tamanho de unidade de alocação (AUS) de 64 KB. Repita o processo de Olá para todos os volumes disponíveis de saudação.
    
    ![Gerenciamento de Disco](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio20.png)
16. Em **gerenciamento de disco**, Olá atalho **disco** e selecione **propriedades**.
17. Em Olá **propriedades do dispositivo de disco de vários caminhos** caixa de diálogo, clique em Olá **MPIO** guia.
    
    ![Propriedades de Disco](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio21.png)
18. Em Olá **nome DSM** seção, clique em **detalhes** e verificar se os parâmetros de saudação estão definidos toohello os parâmetros padrão. saudação padrão parâmetros são:
    
    * Período de Verificação do Caminho = 30
    * Contagem de Repetição = 3
    * Período de Remoção PDO = 20
    * Intervalo de Repetição = 1
    * Verificação do Caminho habilitada = Desmarcada.
    
    > [!NOTE]
    > **Não modifique os parâmetros padrão hello.**
   
## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador de dispositivos de StorSimple sua matriz Virtual StorSimple](storsimple-virtual-array-manager-service-administration.md).

