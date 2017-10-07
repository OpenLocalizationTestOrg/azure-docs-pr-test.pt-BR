---
title: aaaConfigure MPIO para seu dispositivo StorSimple | Microsoft Docs
description: Descreve como tooconfigure Multipath i/o (MPIO) para seu dispositivo StorSimple conectados tooa host executando o Windows Server 2012 R2.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 879fd0f9-c763-4fa0-a5ba-f589a825b2df
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/03/2017
ms.author: alkohli
ms.openlocfilehash: 08cd53039b3868217c7d28e97d7c3c695c06e399
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multipath-io-for-your-storsimple-device"></a>Configurar o MPIO (Multipath I/O) para seu dispositivo StorSimple
Microsoft criado suporte ao recurso de e/s de vários caminhos (MPIO) Olá no Windows Server toohelp criar as configurações de SAN altamente disponíveis e tolerante a falhas. MPIO usa componentes de caminho físico com redundância – adaptadores, cabos e comutadores – toocreate de caminhos lógicos entre o servidor de saudação e o dispositivo de armazenamento hello. Se houver uma falha de componente, fazendo com que um caminho lógico toofail, lógica de múltiplos caminhos usará um caminho alternativo de e/s para que os aplicativos ainda possam acessar seus dados. Além disso dependendo da configuração do MPIO também pode melhorar desempenho, novamente no balanceamento de carga de saudação em todos esses caminhos. Para obter mais informações, consulte [Visão geral do MPIO](https://technet.microsoft.com/library/cc725907.aspx "Visão geral do MPIO and features").  

Para Olá alta disponibilidade da sua solução StorSimple, MPIO deve ser configurado em seu dispositivo StorSimple. Quando o MPIO é instalado em servidores host executando o Windows Server 2012 R2, servidores hello, em seguida, podem tolerar um link, rede ou falhas de interface. 

O MPIO é um recurso opcional no Windows Server e não é instalado por padrão. Ele deve ser instalado como um recurso por meio do Gerenciador de Servidores. Este tópico descreve etapas Olá deve seguir tooinstall e usar o recurso MPIO Olá em um host executando o Windows Server 2012 R2 e conectado tooa dispositivo físico StorSimple.

> [!NOTE]
> **Esse procedimento é aplicável somente para a série StorSimple 8000. Atualmente, não há suporte para MPIO em um dispositivo virtual StorSimple.**
> 
> 

Você precisará toofollow tooconfigure essas etapas MPIO em seu dispositivo StorSimple:

* Etapa 1: Instalar o MPIO no host do Windows Server Olá
* Etapa 2: configurar o MPIO para os volumes StorSimple
* Etapa 3: Montar volumes do StorSimple no host de saudação
* Etapa 4: configurar o MPIO para ter alta disponibilidade e balanceamento de carga

Cada Olá acima etapas é discutida em Olá seções a seguir.

## <a name="step-1-install-mpio-on-hello-windows-server-host"></a>Etapa 1: Instalar o MPIO no host do Windows Server Olá
tooinstall esse recurso no host do Windows Server, conclua Olá procedimento a seguir.

#### <a name="tooinstall-mpio-on-hello-host"></a>tooinstall MPIO no host de saudação
1. Abra o Gerenciador de Servidores no host do Windows Server. Por padrão, o Gerenciador do servidor começa quando um membro do grupo de administradores Olá logon tooa computador que está executando o Windows Server 2012 R2 ou Windows Server 2012. Se o Gerenciador do servidor de saudação já não estiver aberta, clique em **Iniciar > Gerenciador de servidores**.
   ![Gerenciador de Servidores](./media/storsimple-configure-mpio-windows-server/IC740997.png)
2. Clique em **Gerenciador de Servidores > Painel de Controle > Adicionar funções e recursos**. Isso inicia o hello **adicionar funções e recursos** assistente.
   ![Adicionar Assistente de Funções e Recursos 1](./media/storsimple-configure-mpio-windows-server/IC740998.png)
3. Em Olá **adicionar funções e recursos** assistente, Olá a seguir:
   
   * Em Olá **antes de começar a** , clique em **próximo**.
   * Em Olá **Selecionar tipo de instalação** página, aceite a configuração padrão de saudação do **baseada em função ou recurso** instalação. Clique em **Próximo**.![Adicionar Assistente de Funções e Recursos 2](./media/storsimple-configure-mpio-windows-server/IC740999.png)
   * Em Olá **Selecionar servidor de destino** escolha **selecionar um servidor do pool do servidor de saudação**. O servidor host deve ser descoberto automaticamente. Clique em **Avançar**.
   * Em Olá **selecionar funções de servidor** , clique em **próximo**.
   * Em Olá **selecionar recursos** , selecione **Multipath i / o**e clique em **próximo**.![ Adicionar Assistente de funções e recursos 5](./media/storsimple-configure-mpio-windows-server/IC741000.png)
   * Em Olá **confirmar seleções de instalação** página, confirmar seleção hello e, em seguida, selecione **reinicialização do servidor de destino Olá automaticamente, se necessário**, conforme mostrado abaixo. Clique em **Instalar**.![Adicionar Assistente de Funções e Recursos 8](./media/storsimple-configure-mpio-windows-server/IC741001.png)
   * Você será notificado quando Olá instalação for concluída. Clique em **fechar** Assistente de saudação tooclose.![ Adicionar Assistente de funções e recursos 9](./media/storsimple-configure-mpio-windows-server/IC741002.png)

## <a name="step-2-configure-mpio-for-storsimple-volumes"></a>Etapa 2: configurar o MPIO para os volumes StorSimple
MPIO precisa de volumes do StorSimple tooidentify toobe configurado. volumes do StorSimple da toorecognize tooconfigure MPIO, executar Olá etapas a seguir.

#### <a name="tooconfigure-mpio-for-storsimple-volumes"></a>tooconfigure MPIO para volumes do StorSimple
1. Olá abrir **configuração do MPIO**. Clique em **Gerenciador de Servidores > Painel de Controle > Ferramentas > MPIO**.
2. Em Olá **propriedades do MPIO** caixa de diálogo, selecione Olá **descobrir vários caminhos** guia.
3. Selecione **Adicionar suporte para dispositivos iSCSI** e clique em **Adicionar**.  
   ![Propriedades do MPIO para Descobrir Vários Caminhos](./media/storsimple-configure-mpio-windows-server/IC741003.png)
4. Reinicialize o servidor de saudação quando solicitado.
5. Em Olá **propriedades do MPIO** caixa de diálogo, clique em Olá **dispositivos MPIO** guia. Clique em **adicionar**.
    </br>![Propriedades do MPIO para Dispositivos do MPIO](./media/storsimple-configure-mpio-windows-server/IC741004.png)
6. Em Olá **adicionar suporte a MPIO** caixa de diálogo **ID de Hardware do dispositivo**, insira o número de série do dispositivo. Você pode obter o número de série do dispositivo Olá acessando seu serviço StorSimple Manager e navegando muito**dispositivos > painel**. Olá número de série do dispositivo é exibido no hello direito **rápidos** painel do painel de dispositivo hello.
    </br>![Adicionar Suporte do MPIO](./media/storsimple-configure-mpio-windows-server/IC741005.png)
7. Reinicialize o servidor de saudação quando solicitado.

## <a name="step-3-mount-storsimple-volumes-on-hello-host"></a>Etapa 3: Montar volumes do StorSimple no host de saudação
Depois que o MPIO é configurado no Windows Server, volumes criados no dispositivo do StorSimple Olá podem ser montados e, em seguida, podem levar vantagem do MPIO para redundância. toomount um volume, execute Olá etapas a seguir.

#### <a name="toomount-volumes-on-hello-host"></a>toomount volumes no host de saudação
1. Olá abrir **propriedades do iniciador iSCSI** janela no host do servidor do Windows hello. Clique em **Gerenciador do Servidor > Painel > Ferramentas > Iniciador iSCSI**.
2. Em Olá **propriedades do iniciador iSCSI** caixa de diálogo, clique Olá descoberta guia e, em seguida, clique em **descobrir Portal de destino**.
3. Em Olá **descobrir Portal de destino** caixa de diálogo caixa, Olá a seguir:
   
   * Inserir endereço IP de saudação do hello a porta de dados do seu dispositivo StorSimple (por exemplo, inserir dados 0).
   * Clique em **Okey** tooreturn toohello **propriedades do iniciador iSCSI** caixa de diálogo.
     
     > [!IMPORTANT]
     > **Se você estiver usando uma rede privada para as conexões iSCSI, insira o endereço IP de saudação da porta de dados de saudação é a rede privada toohello conectado.**
     > 
     > 
4. Repita as etapas de 2 a 3 para uma segunda interface de rede (por exemplo, DADOS 1) em seu dispositivo. Lembre-se que essas interfaces devem ser habilitadas para o iSCSI. toolearn mais sobre isso, consulte [modificar interfaces de rede](storsimple-modify-device-config.md#modify-network-interfaces).
5. Selecione Olá **destinos** guia Olá **propriedades do iniciador iSCSI** caixa de diálogo. Você verá o dispositivo StorSimple Olá destino IQN em **destinos detectados**.

   ![Guia Destinos para Propriedades do Iniciador iSCSI](./media/storsimple-configure-mpio-windows-server/IC741007.png)
   
6. Clique em **conectar** tooestablish uma sessão iSCSI com seu dispositivo StorSimple. Um **conectar tooTarget** caixa de diálogo será exibida.
7. Em Olá **conectar tooTarget** caixa de diálogo, selecione Olá **habilitar vários caminhos** caixa de seleção. Clique em **Avançado**.
8. Em Olá **configurações avançadas** caixa de diálogo caixa, Olá a seguir:                                        
   
   * Em Olá **adaptador Local** lista suspensa, selecione **iniciador Microsoft iSCSI**.
   * Em Olá **IP do iniciador** lista suspensa, o endereço IP de saudação selecione do host de saudação.
   * Em Olá **Portal de destino** lista suspensa IP, selecione Olá IP da interface de dispositivo.
   * Clique em **Okey** tooreturn toohello **propriedades do iniciador iSCSI** caixa de diálogo.
9. Clique em **Propriedades**. Em Olá **propriedades** caixa de diálogo, clique em **adicionar sessão**.
10. Em Olá **conectar tooTarget** caixa de diálogo, selecione Olá **habilitar vários caminhos** caixa de seleção. Clique em **Avançado**.
11. Em Olá **configurações avançadas** caixa de diálogo:                                        
    
    * Em Olá **adaptador Local** lista suspensa, selecione Microsoft iSCSI Initiator.
    * Em Olá **IP do iniciador** lista suspensa, selecione Olá IP endereço correspondente toohello host. Nesse caso, você está se conectando duas interfaces de rede Olá dispositivo tooa única interface de rede no host de saudação. Portanto, essa interface é Olá mesmo que é fornecida para Olá primeira sessão.
    * Em Olá **IP do Portal de destino** lista suspensa, endereço IP selecione Olá Olá segunda interface de dados habilitada no dispositivo de saudação.
    * Clique em **Okey** caixa de diálogo de propriedades do iniciador de iSCSI do tooreturn toohello. Você adicionou um segundo toohello destino da sessão.
12. Abra **gerenciamento do computador** navegando muito**Gerenciador do servidor > Painel de controle > Gerenciamento do computador**. No painel esquerdo do hello, clique em **armazenamento > Gerenciamento de disco**. Olá volumes criados no dispositivo StorSimple de saudação que são visíveis toothis host aparecerá sob **gerenciamento de disco** como novos discos.
13. Inicializar disco hello e crie um novo volume. Durante o processo de formatação hello, selecione um tamanho de bloco de 64 KB.
    ![Gerenciamento de Disco](./media/storsimple-configure-mpio-windows-server/IC741008.png)
14. Em **gerenciamento de disco**, Olá atalho **disco** e selecione **propriedades**.
15. Em Olá StorSimple modelo # # # **propriedades do dispositivo de disco de vários caminhos** caixa de diálogo, clique em Olá **MPIO** guia. ![Prop do Dispositivo de Disco com Vários Caminhos do StorSimple 8100.](./media/storsimple-configure-mpio-windows-server/IC741009.png)
16. Em Olá **nome DSM** seção, clique em **detalhes** e verificar se os parâmetros de saudação estão definidos toohello os parâmetros padrão. saudação padrão parâmetros são:
    
    * Período de Verificação do Caminho = 30
    * Contagem de Repetição = 3
    * Período de Remoção PDO = 20
    * Intervalo de Repetição = 1
    * Verificação do Caminho habilitada = Desmarcada.

> [!NOTE]
> **Não modifique os parâmetros padrão hello.**


## <a name="step-4-configure-mpio-for-high-availability-and-load-balancing"></a>Etapa 4: configurar o MPIO para ter alta disponibilidade e balanceamento de carga
Para vários caminhos com alta disponibilidade e balanceamento de carga, várias sessões devem ser adicionadas manualmente toodeclare Olá diferentes caminhos disponíveis. Por exemplo, se host Olá tiver duas interfaces conectadas o dispositivo de tooSAN e hello tem duas interfaces de tooSAN conectado, em seguida, são necessárias quatro sessões configuradas com permutações de caminho adequado (somente duas sessões serão necessárias se cada interface DATA e interface host estiver em uma sub-rede IP diferente e não forem roteáveis).

**É recomendável que você tenha pelo menos 8 sessões ativas de paralelas entre o dispositivo hello e seu host de aplicativo.** Isso pode ser obtido habilitando quatro interfaces de rede em seu sistema Windows Server. Use interfaces de rede física ou virtuais interfaces por meio de tecnologias de virtualização de rede no nível de sistema operacional ou hardware Olá no host do Windows Server. Com hello duas interfaces de rede no dispositivo hello, essa configuração resulta em 8 de sessões ativas. Essa configuração ajuda a otimizar o throughput de dispositivo e nuvem hello.

> [!IMPORTANT]
> **É recomendável que você não misture as interfaces de rede com 1 GbE e 10 GbE. Se você usar duas interfaces de rede, ambas as interfaces devem ser Olá mesmo tipo.**

Olá procedimento a seguir descreve como sessões tooadd quando um dispositivo StorSimple com duas interfaces de rede está conectado tooa hospedam com duas interfaces de rede. Isso proporciona apenas duas sessões ativas. Use esse mesmo procedimento com um dispositivo StorSimple com o host de tooa conectado de interfaces de rede dois com quatro interfaces de rede. Você precisará tooconfigure 8 em vez da saudação 4 sessões descritas aqui.

### <a name="tooconfigure-mpio-for-high-availability-and-load-balancing"></a>tooconfigure MPIO para alta disponibilidade e balanceamento de carga
1. Executar uma descoberta do destino Olá: no hello **propriedades do iniciador iSCSI** caixa de diálogo Olá **descoberta** , clique em **descobrir Portal**.
2. Em Olá **conectar tooTarget** caixa de diálogo, digite o endereço IP de saudação de uma das interfaces de rede hello.
3. Clique em **Okey** tooreturn toohello **propriedades do iniciador iSCSI** caixa de diálogo.
4. Em Olá **propriedades do iniciador iSCSI** caixa de diálogo, selecione Olá **destinos** guia, realce destino Olá descoberto e, em seguida, clique em **conectar**. Olá **conectar tooTarget** caixa de diálogo é exibida.
5. Em Olá **conectar tooTarget** caixa de diálogo:
   
   * Deixe saudação padrão selecionado configuração de destino para **adicionar esta conexão** toohello lista de destinos favoritos. Isso fará com que o dispositivo de saudação automaticamente tentativa de conexão de saudação toorestart toda vez que este computador for reiniciado.
   * Selecione Olá **habilitar vários caminhos** caixa de seleção.
   * Clique em **Avançado**.
6. Em Olá **configurações avançadas** caixa de diálogo:
   
   * Em Olá **adaptador Local** lista suspensa, selecione **iniciador Microsoft iSCSI**.
   * Em Olá **IP do iniciador** lista suspensa, o endereço IP de saudação selecione do host de saudação.
   * Em Olá **IP do Portal de destino** lista suspensa, o endereço IP de saudação select da interface de dados Olá habilitado no dispositivo de saudação.
   * Clique em **Okey** caixa de diálogo de propriedades do iniciador de iSCSI do tooreturn toohello.
7. Clique em **propriedades**e em Olá **propriedades** caixa de diálogo, clique em **adicionar sessão**.
8. Em Olá **conectar tooTarget** caixa de diálogo, selecione Olá **habilitar vários caminhos** caixa de seleção e, em seguida, clique em **avançado**.
9. Em Olá **configurações avançadas** caixa de diálogo:
   
   1. Em Olá **adaptador Local** lista suspensa, selecione **iniciador Microsoft iSCSI**.
   2. Em Olá **IP do iniciador** lista suspensa, selecione Olá endereço IP correspondente toohello segunda interface no host de saudação.
   3. Em Olá **IP do Portal de destino** lista suspensa, endereço IP selecione Olá Olá segunda interface de dados habilitada no dispositivo de saudação.
   4. Clique em **Okey** tooreturn toohello **propriedades do iniciador iSCSI** caixa de diálogo. Você acaba de adicionar um segundo toohello destino da sessão.
10. Repita o destino de toohello as etapas 8 a 10 tooadd sessões (caminhos). Com duas interfaces no host hello e duas em dispositivo hello, você pode adicionar um total de quatro sessões.
11. Depois de adicionar sessões Olá desejada (caminhos), em Olá **propriedades do iniciador iSCSI** caixa de diálogo, destino Olá selecione e clique em **propriedades**. Na guia de sessões de saudação do hello **propriedades** caixa de diálogo, observe Olá quatro identificadores de sessão que correspondem a toohello possíveis permutações de caminho. toocancel uma sessão, selecione Olá caixa de seleção próxima tooa identificador da sessão e, em seguida, clique em **Disconnect**.
12. dispositivos tooview apresentados dentro das sessões, selecione Olá **dispositivos** Olá tooconfigure de guia política MPIO para um dispositivo selecionado, clique em **MPIO**. Olá **detalhes do dispositivo** caixa de diálogo será exibida. Em Olá **MPIO** guia, você pode selecionar Olá apropriado **política de balanceamento de carga** configurações. Você também pode exibir uma saudação **Active** ou **Standby** tipo de caminho.

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [usando Olá toomodify do serviço StorSimple Manager a configuração do dispositivo StorSimple](storsimple-modify-device-config.md).

