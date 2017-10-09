---
title: aaaDeploy StorSimple Snapshot Manager | Microsoft Docs
description: "Saiba como toodownload e instale Olá StorSimple Snapshot Manager, um snap-in MMC do gerenciamento de recursos de backup e proteção de dados StorSimple."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: f0128f57-519e-49ec-9187-23575809cdbe
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: dd90cca2bbb3410bb8cd459fb1a3ff3fb5f2997b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-snapshot-manager-mmc-snap-in"></a>Implantar Olá snap-in MMC do Gerenciador de instantâneos StorSimple

## <a name="overview"></a>Visão geral
Olá StorSimple Snapshot Manager é um snap-in do Console de gerenciamento Microsoft (MMC) que simplifica a proteção de dados e gerenciamento de backup em um ambiente do Microsoft Azure StorSimple. Com o StorSimple Snapshot Manager, é possível gerenciar o armazenamento em nuvem e local do Microsoft Azure StorSimple como se fosse um sistema de armazenamento totalmente integrado, simplificando assim os processos de backup e restauração e reduzindo os custos. 

Este tutorial descreve os requisitos de configuração, bem como os procedimentos para instalar, remover e atualizar o StorSimple Snapshot Manager.

> [!NOTE]
> * Você não pode usar toomanage StorSimple Snapshot Manager Microsoft Azure StorSimple Virtual Arrays da (também conhecido como StorSimple local dispositivos virtuais).
> * Se você planejar tooinstall StorSimple atualização 2 em seu dispositivo StorSimple, ser se toodownload Olá versão mais recente do StorSimple Snapshot Manager e instalá-lo **antes de instalar a atualização 2 do StorSimple**. versão mais recente de saudação do StorSimple Snapshot Manager é compatível com versões anteriores e funciona com todas as versões do Microsoft Azure StorSimple. Se você estiver usando a versão anterior de saudação do StorSimple Snapshot Manager, você precisará tooupdate it (você não é necessário versão anterior do toouninstall Olá antes de instalar a nova versão de hello).


## <a name="storsimple-snapshot-manager-installation"></a>Instalação do StorSimple Snapshot Manager
Gerenciador de instantâneos StorSimple pode ser instalado em computadores que estão executando o sistema de operacional Windows Server 2008 R2 SP1, Windows Server 2012 ou Windows Server 2012 R2 hello. Em servidores que executam o Windows 2008 R2, instale também o Windows Server 2008 SP1 e o Windows Management Framework 3.0.

Antes de instalar ou atualizar o snap-in Gerenciador de instantâneos StorSimple de saudação do hello Microsoft Management Console (MMC), verifique se esse dispositivo do Microsoft Azure StorSimple hello e servidor de host estão configurados corretamente.

## <a name="configure-prerequisites"></a>Configurar pré-requisitos
Olá etapas a seguir fornecem uma visão geral das tarefas de configuração que você deve concluir antes de instalar o hello StorSimple Snapshot Manager. Para obter informações de instalação e configuração completas do Microsoft Azure StorSimple, incluindo requisitos de sistema e instruções passo a passo, consulte [Implantar seu dispositivo StorSimple local](storsimple-8000-deployment-walkthrough-u2.md).

> [!IMPORTANT]
> Antes de começar, examine Olá [lista de verificação de configuração de implantação](storsimple-8000-deployment-walkthrough-u2.md#deployment-configuration-checklist) e e [os pré-requisitos de implantação](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites) na [implantar seu dispositivo do StorSimple local](storsimple-8000-deployment-walkthrough-u2.md).
> <br>
> 
> 

### <a name="before-you-install-storsimple-snapshot-manager"></a>Antes de instalar o StorSimple Snapshot Manager
1. Desembale, monte e conecte o dispositivo do Microsoft Azure StorSimple Olá conforme descrito nas [instalar seu dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md) ou [instalar seu dispositivo 8600 StorSimple](storsimple-8600-hardware-installation.md).
2. Certifique-se de que o computador host está executando um dos Olá sistemas operacionais a seguir:
   
   * Windows Server 2008 R2 (em servidores executando o Windows 2008 R2, você também deverá instalar o Windows Server 2008 SP1 e o Windows Management Framework 3.0)
   * Windows Server 2012
   * Windows Server 2012 R2
     
     Para um dispositivo virtual StorSimple, host Olá deve ser uma máquina Virtual do Microsoft Azure.
3. Certifique-se de que você atende a todos os requisitos de configuração do Microsoft Azure StorSimple hello. Para obter detalhes, acesse muito[os pré-requisitos de implantação](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites).
4. Conectar Olá dispositivo toohello host e execute a configuração inicial hello. Para obter detalhes, acesse muito[etapas de implantação](storsimple-8000-deployment-walkthrough-u2.md#deployment-steps).
5. Crie volumes no dispositivo de saudação, atribuí-los toohello host e verifique se o host Olá pode montar e usá-los. Gerenciador de instantâneos StorSimple dá suporte a saudação seguintes tipos de volumes:
   
   * Volumes básicos
   * Volumes simples
   * Volumes dinâmicos
   * Volumes dinâmicos espelhados (RAID 1)
   * Volumes compartilhados de cluster
     
     Para obter informações sobre a criação de volumes no dispositivo do StorSimple hello ou dispositivo virtual StorSimple, vá muito[etapa 6: criar um volume](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume), na [implantar seu dispositivo do StorSimple local](storsimple-8000-deployment-walkthrough-u2.md).

## <a name="install-a-new-storsimple-snapshot-manager"></a>Instalar um novo StorSimple Snapshot Manager
Antes de instalar o Gerenciador de instantâneos do StorSimple, certifique-se de que volumes de Olá criado no dispositivo do StorSimple hello ou dispositivo virtual StorSimple são montados, inicializados e formatados como descrito no [configurar pré-requisitos](#configure-prerequisites).

> [!IMPORTANT]
> * Para um dispositivo virtual StorSimple, host Olá deve ser uma máquina Virtual do Microsoft Azure. 
> * host de saudação deve estar executando Windows 2008 R2, Windows Server 2012 ou Windows Server 2012 R2. Se seu servidor executar o Windows Server 2008 R2, você também deverá instalar o Windows Server 2008 SP1 e o Windows Management Framework 3.0.
> * Você deve configurar uma conexão iSCSI do dispositivo StorSimple do hello host toohello antes de poder conectar Olá dispositivo tooStorSimple Gerenciador de instantâneos.

Siga essas etapas toocomplete uma nova instalação do Gerenciador de instantâneos do StorSimple. Se você estiver instalando uma atualização, acesse muito[atualizar ou reinstalar o Gerenciador de instantâneos StorSimple](#upgrade-or-reinstall-storsimple-snapshot-manager).

* Etapa 1: Instalar o StorSimple Snapshot Manager 
* Etapa 2: Conectar o dispositivo StorSimple Snapshot Manager tooa 
* Etapa 3: Verifique se o dispositivo de toohello conexão Olá 

### <a name="step-1-install-storsimple-snapshot-manager"></a>Etapa 1: Instalar o StorSimple Snapshot Manager
Use Olá seguindo as etapas tooinstall StorSimple Snapshot Manager.

#### <a name="tooinstall-storsimple-snapshot-manager"></a>tooinstall Gerenciador de instantâneos StorSimple
1. Baixar o software do Gerenciador de instantâneos StorSimple hello (vá muito[StorSimple Snapshot Manager](https://www.microsoft.com/download/details.aspx?id=44220) em Olá Microsoft Download Center) e salve-o localmente no host de saudação.
2. No Explorador de arquivos, clique em pasta compactada hello e, em seguida, clique em **extrair tudo**.
3. Em Olá **extrair pastas compactadas (zipadas)** janela no hello **selecione um destino e extraia os arquivos** caixa, digite ou procure toohello caminho em que você deseja toobe toofile extraído.
   
    > [!IMPORTANT]
    > Você deve instalar o Gerenciador de instantâneos do StorSimple em Olá unidade c.
    
4. Selecione Olá **Mostrar extraiu arquivos ao concluir** caixa de seleção e, em seguida, clique em **extrair**.
   
    ![Extrair a caixa de diálogo de arquivos](./media/storsimple-snapshot-manager-deployment/HCS_SSM_extract_files.png) 
5. Quando Olá extração estiver concluída, pasta de destino de saudação é aberto. Clique duas vezes no ícone de instalação do aplicativo hello aparece na pasta de destino de saudação.
6. Olá quando **configuração bem-sucedida** mensagem for exibida, clique em **fechar**. Você deve ver o ícone do Gerenciador de instantâneos StorSimple Olá na área de trabalho.
   
    ![Ícone da área de trabalho](./media/storsimple-snapshot-manager-deployment/HCS_SSM_desktop_icon.png) 

### <a name="step-2-connect-storsimple-snapshot-manager-tooa-device"></a>Etapa 2: Conectar o dispositivo StorSimple Snapshot Manager tooa
Use Olá etapas tooconnect dispositivo StorSimple tooa Gerenciador de instantâneos StorSimple a seguir.

#### <a name="tooconnect-storsimple-snapshot-manager-tooa-device"></a>tooconnect dispositivo StorSimple Snapshot Manager tooa
1. Clique Olá StorSimple Snapshot Manager ícone na área de trabalho. janela do Gerenciador de instantâneos StorSimple Olá é exibida. Olá janela contém um **escopo** painel, um **resultados** painel e um **ações** painel. 
   
    ![Interface do usuário do StorSimple Snapshot Manager](./media/storsimple-snapshot-manager-deployment/HCS_SSM_gui_panes.png)
   
   * Olá **escopo** painel (Olá esquerdo) contém uma lista de nós organizados em uma estrutura de árvore. Você pode expandir alguns nós tooselect uma exibição ou nó de dados específicos de toothat relacionados. Clique em Olá tooexpand de ícone de seta ou recolher um nó. Clique com botão direito em Olá um item **escopo** painel toosee uma lista de ações disponíveis para aquele item.
   * Olá **resultados** painel (Olá center) contém informações detalhadas sobre o nó hello, exibição ou dados que você selecionou na Olá **escopo** painel.
   * Olá **ações** painel lista operações de saudação que você pode executar no nó hello, exibição ou dados que você selecionou na Olá **escopo** painel.
     
     Para obter uma descrição completa da interface de usuário do Gerenciador de instantâneos StorSimple hello, consulte [interface de usuário do Gerenciador de instantâneos StorSimple](storsimple-use-snapshot-manager.md).
2. Em Olá **escopo** painel, Olá atalho **dispositivos** nó e, em seguida, clique **configurar um dispositivo**. Olá **configurar um dispositivo** caixa de diálogo é exibida.
   
    ![Configurar um dispositivo](./media/storsimple-snapshot-manager-deployment/HCS_SSM_config_device.png) 
3. Em Olá **dispositivo** lista caixa, o endereço IP de saudação select de dispositivo do Microsoft Azure StorSimple hello ou virtual. Em Olá **senha** caixa de texto, a senha do Gerenciador de instantâneo do StorSimple do tipo hello que você criou para o dispositivo Olá Olá portal do Azure. Clique em **OK**.
4. Gerenciador de instantâneos StorSimple procura por dispositivo Olá que você identificou. Se o dispositivo Olá estiver disponível, Gerenciador de instantâneos StorSimple adiciona uma conexão. Você pode [Verifique Olá conexão toohello dispositivo](#to-verify-the-connection) tooconfirm que Olá conexão foi adicionada com êxito.
   
    Se dispositivo Olá estiver indisponível por qualquer motivo, o Gerenciador de instantâneos StorSimple retorna uma mensagem de erro. Clique em **Okey** tooclose Olá a mensagem de erro e, em seguida, clique em **Cancelar** tooclose Olá **configurar um dispositivo** caixa de diálogo.
5. Quando ele se conecta o dispositivo tooa, Gerenciador de instantâneos StorSimple importa cada grupo de volumes configurado para esse dispositivo, desde que hello volume grupo tenha backups associados. Grupos de volumes que não têm backups associados não são importados. Além disso, as políticas de backup que foram criadas para um grupo de volumes não são importadas. toosee Olá grupos importados, clique no principal Olá **grupos de Volume** nó Olá **escopo** painel e clique em **alternar grupos importados**.

### <a name="step-3-verify-hello-connection-toohello-device"></a>Etapa 3: Verifique se o dispositivo de toohello conexão Olá
Use Olá etapas tooverify StorSimple Snapshot Manager é o dispositivo StorSimple toohello conectados a seguir.

#### <a name="tooverify-hello-connection"></a>conexão de saudação tooverify
1. Em Olá **escopo** painel, clique em Olá **dispositivos** nó.
   
    ![Status do dispositivo StorSimple Snapshot Manager](./media/storsimple-snapshot-manager-deployment/HCS_SSM_Device_status.png) 
2. Verificar Olá **resultados** painel: 
   
   * Se um indicador verde aparecer no ícone do dispositivo hello e **disponível** aparece no hello **Status** coluna, em seguida, dispositivo de saudação está conectada. 
   * Se um indicador vermelho aparecer no ícone do dispositivo hello e indisponível é exibido no hello **Status** coluna, em seguida, dispositivo de saudação não está conectada. 
   * Se **Atualizando** aparece no hello **Status** coluna e, em seguida, StorSimple Snapshot Manager está recuperando grupos de volumes e backups associados para um dispositivo conectado.

## <a name="upgrade-or-reinstall-storsimple-snapshot-manager"></a>Atualizar ou reinstalar o StorSimple Snapshot Manager
Você deve desinstalar o Gerenciador de instantâneos StorSimple completamente antes de atualizar ou reinstalar o software de saudação. 

Antes de reinstalar o Gerenciador de instantâneos do StorSimple, faça backup Olá StorSimple Snapshot Manager banco de dados no computador de host hello. Isso salva informações de configuração e políticas de backup de saudação para que você possa restaurar facilmente esses dados de backup.

Siga essas etapas se você estiver atualizando ou reinstalando o StorSimple Snapshot Manager:

* Etapa 1: Desinstalar o StorSimple Snapshot Manager 
* Etapa 2: Fazer backup de banco de dados do Gerenciador de instantâneos StorSimple Olá 
* Etapa 3: Reinstale o Gerenciador de instantâneo do StorSimple e restaure o banco de dados de saudação 

### <a name="step-1-uninstall-storsimple-snapshot-manager"></a>Etapa 1: Desinstalar o StorSimple Snapshot Manager
Use Olá seguindo as etapas toouninstall StorSimple Snapshot Manager.

#### <a name="toouninstall-storsimple-snapshot-manager"></a>toouninstall Gerenciador de instantâneos StorSimple
1. No computador de host do hello, abra Olá **painel de controle**, clique em **programas**e, em seguida, clique em **programas e recursos**.
2. No painel esquerdo do hello, clique em **desinstalar ou alterar um programa**.
3. Clique com o botão direito do mouse em **StorSimple Snapshot Manager** e clique em **Desinstalar**.
4. Isso inicia o hello programa de instalação do Gerenciador de instantâneos do StorSimple. Clique em **Modificar Configuração** e clique em **Desinstalar**.
   
   > [!NOTE]
   > Se houver algum processo MMC em execução no plano de fundo hello, como o Gerenciador de instantâneos do StorSimple ou gerenciamento de disco, Olá desinstalação falhará e você receberá uma mensagem tooclose todas as instâncias de MMC antes de tentam toouninstall programa de saudação. Selecione **fechar aplicativos automaticamente e tentar toorestart-los após a instalação concluir**e, em seguida, clique em **Okey**.
   > 
   > 
5. Ao desinstalar o hello processo for concluído, um **configuração bem-sucedida** mensagem é exibida. Clique em **fechar**

### <a name="step-2-back-up-hello-storsimple-snapshot-manager-database"></a>Etapa 2: Fazer backup de banco de dados do Gerenciador de instantâneos StorSimple Olá
Use Olá toocreate as etapas a seguir e salve uma cópia do banco de dados do Gerenciador de instantâneos StorSimple Olá.

#### <a name="tooback-up-hello-database"></a>tooback o banco de dados de saudação
1. Pare Olá serviço de gerenciamento do Microsoft StorSimple:
   
   1. Inicie o Gerenciador do Servidor.
   2. Em Olá painel do Gerenciador do servidor, em Olá **ferramentas** menu, selecione **serviços**.
   3. Em Olá **serviços** página, selecione **serviço de gerenciamento do Microsoft StorSimple**.
   4. Em Olá direita painel, em **serviço de gerenciamento do Microsoft StorSimple**, clique em **parar serviço Olá**.
      
        ![Parar o serviço do Gerenciador de dispositivos de StorSimple Olá](./media/storsimple-snapshot-manager-deployment/HCS_SSM_stop_service.png)
2. Procure tooC:\ProgramData\Microsoft\StorSimple\BACatalog. 
   
   > [!NOTE]
   > ProgramData é uma pasta oculta.
  
3. Localize arquivo XML do catálogo hello, copiar o arquivo de saudação e armazenar Olá copiar em um local seguro ou na nuvem hello.
   
    ![Arquivo de catálogo de backup do StorSimple](./media/storsimple-snapshot-manager-deployment/HCS_SSM_bacatalog.png)
4. Reinicie Olá serviço de gerenciamento do Microsoft StorSimple: 
   
   1. Em Olá painel do Gerenciador do servidor, em Olá **ferramentas** menu, selecione **serviços**.
   2. Em Olá **serviços** página, selecione Olá **serviço de gerenciamento do Microsoft StorSimple**e.
   3. Em Olá direita painel, em **serviço de gerenciamento do Microsoft StorSimple**, clique em **reiniciar serviço Olá**. 

### <a name="step-3-reinstall-storsimple-snapshot-manager-and-restore-hello-database"></a>Etapa 3: Reinstale o Gerenciador de instantâneo do StorSimple e restaure o banco de dados de saudação
tooreinstall StorSimple Snapshot Manager, execute as etapas de saudação em [instalar um novo Gerenciador de instantâneos do StorSimple](#install-a-new-storsimple-snapshot-manager). Em seguida, use Olá após o banco de dados do procedimento toorestore Olá StorSimple Snapshot Manager.

#### <a name="toorestore-hello-database"></a>o banco de dados do toorestore Olá
1. Pare Olá serviço de gerenciamento do Microsoft StorSimple:
   
   1. Inicie o Gerenciador do Servidor.
   2. Em Olá painel do Gerenciador do servidor, em Olá **ferramentas** menu, selecione **serviços**.
   3. Em Olá **serviços** página, selecione **serviço de gerenciamento do Microsoft StorSimple**.
   4. Em Olá direita painel, em **serviço de gerenciamento do Microsoft StorSimple**, clique em **parar serviço Olá**.
2. Procure tooC:\ProgramData\Microsoft\StorSimple\BACatalog.
   
   > [!NOTE]
   > ProgramData é uma pasta oculta.
   > 
   > 
3. Excluir o arquivo XML do catálogo hello e substituí-lo com a versão de saudação que você salvou anteriormente.
4. Reinicie Olá serviço de gerenciamento do Microsoft StorSimple: 
   
   1. Em Olá painel do Gerenciador do servidor, em Olá **ferramentas** menu, selecione **serviços**.
   2. Em Olá **serviços** página, selecione **serviço de gerenciamento do Microsoft StorSimple**.
   3. Em Olá direita painel, em **serviço de gerenciamento do Microsoft StorSimple**, clique em **reiniciar serviço Olá**.

## <a name="next-steps"></a>Próximas etapas
* toolearn mais sobre o StorSimple Snapshot Manager, vá muito[o que é o Gerenciador de instantâneos StorSimple?](storsimple-what-is-snapshot-manager.md).
* toolearn mais sobre a interface de usuário do Gerenciador de instantâneos StorSimple hello, ir muito[interface de usuário do Gerenciador de instantâneos StorSimple](storsimple-use-snapshot-manager.md).
* toolearn mais sobre como usar o Gerenciador de instantâneos do StorSimple, ir muito[tooadminister Use o Gerenciador de instantâneo StorSimple sua solução StorSimple](storsimple-snapshot-manager-admin.md).

