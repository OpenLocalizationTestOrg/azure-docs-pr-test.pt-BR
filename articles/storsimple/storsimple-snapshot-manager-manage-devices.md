---
title: "aaaManage dispositivos com o Gerenciador de instantâneos do StorSimple | Microsoft Docs"
description: "Descreve como toouse Olá MMC Gerenciador de instantâneos StorSimple snap-in tooconnect e gerenciar os dispositivos StorSimple."
services: storsimple
documentationcenter: 
author: SharS
manager: timlt
editor: 
ms.assetid: 966ecbe3-a7fa-4752-825f-6694dd949946
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 7a2a2ca830e4ea6eb4b01f2542958df3871c1700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooconnect-and-manage-storsimple-devices"></a>Use o Gerenciador de instantâneos StorSimple tooconnect e gerenciar dispositivos de StorSimple
## <a name="overview"></a>Visão geral
Você pode usar nós Olá Gerenciador de instantâneos StorSimple **escopo** tooverify painel importou os dados do dispositivo StorSimple e atualizar os dispositivos de armazenamento conectados. Além disso, quando você clica em Olá **dispositivos** nó, você pode ver uma lista de dispositivos conectados e informações de status correspondentes no hello **resultados** painel.

![Dispositivos conectados](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_connect_devices.png)

**Figura 1: Dispositivo conectado no StorSimple Snapshot Manager** 

Dependendo de sua **exibição** seleções, Olá **resultados** painel mostra Olá informações sobre cada dispositivo a seguir. (Para obter mais informações sobre como configurar um modo de exibição, vá muito[menu Exibir](storsimple-use-snapshot-manager.md#view-menu).

| Coluna de resultados | Descrição |
|:--- |:--- |
| Nome |nome de saudação do dispositivo de saudação conforme configurado no hello portal clássico do Azure |
| Modelo |número de modelo de saudação do dispositivo Olá |
| Versão |versão de saudação do software de saudação instalado no dispositivo Olá |
| Status |Se o dispositivo de saudação está disponível |
| Sincronizado pela última vez |Data e hora quando o dispositivo de saudação foi sincronizada pela última vez |
| N° de série |número de série de saudação para dispositivo Olá |

Se clicar Olá **dispositivos** nó Olá **escopo** painel, você pode selecionar Olá ações a seguir:

* Adicionar ou substituir um dispositivo
* Conectar um dispositivo e verificar as importações
* Atualizar os dispositivos conectados

Se você clicar em Olá **dispositivos** nome de nó e, em seguida, clique com botão direito um dispositivo no hello **resultados** painel, você pode selecionar Olá ações a seguir:

* Autenticar um dispositivo
* Exibir detalhes do dispositivo
* Atualizar um dispositivo
* Excluir uma configuração de dispositivo
* Alterar uma senha de dispositivo

> [!NOTE]
> Todas essas ações também estão disponíveis no hello **ações** painel.


Este tutorial explica como toouse tooconnect Gerenciador de instantâneos do StorSimple e gerenciar dispositivos e executar Olá tarefas a seguir:

* Adicionar ou substituir um dispositivo
* Conectar um dispositivo e verificar as importações
* Atualizar os dispositivos conectados
* Autenticar um dispositivo
* Exibir detalhes do dispositivo
* Atualizar um dispositivo individual
* Excluir uma configuração de dispositivo
* Alterar uma senha de dispositivo expirada
* Substituir um dispositivo com falha

> [!NOTE]
> Para obter informações gerais sobre como usar a interface do Gerenciador de instantâneos StorSimple hello, ir muito[interface de usuário do Gerenciador de instantâneos StorSimple](storsimple-use-snapshot-manager.md).


## <a name="add-or-replace-a-device"></a>Adicionar ou substituir um dispositivo
Use Olá tooadd do procedimento a seguir ou substituir um dispositivo StorSimple.

#### <a name="tooadd-or-replace-a-device"></a>tooadd ou substituir um dispositivo
1. Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager.
2. Em Olá **escopo** painel, Olá atalho **dispositivos** nó e, em seguida, clique **configurar um dispositivo**. Olá **configurar um dispositivo** caixa de diálogo é exibida.
   
    ![Configurar um dispositivo StorSimple](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_config_device.png) 
3. Em Olá **dispositivo** caixa suspensa, o endereço IP de saudação selecione de dispositivo de saudação ou virtual. 
4. Em Olá **senha** caixa de texto, a senha do Gerenciador de instantâneo do StorSimple do tipo hello que você criou para o dispositivo Olá Olá portal clássico do Azure. Clique em **OK**. Gerenciador de instantâneos StorSimple procura por dispositivo Olá que você identificou. 
   
   * Se o dispositivo Olá estiver disponível, Gerenciador de instantâneos StorSimple adiciona uma conexão.
   * Se dispositivo Olá estiver indisponível por qualquer motivo, o Gerenciador de instantâneos StorSimple retorna uma mensagem de erro. Clique em **Okey** tooclose Olá a mensagem de erro e, em seguida, clique em **Cancelar** tooclose Olá **configurar um dispositivo** caixa de diálogo.

## <a name="connect-a-device-and-verify-imports"></a>Conectar um dispositivo e verificar as importações
Use Olá seguindo o procedimento tooconnect um dispositivo StorSimple e verificar se quaisquer grupos de volume existentes que tenham backups associados são importados.

#### <a name="tooconnect-a-device-and-verify-imports"></a>tooconnect um dispositivo e verificar importações
1. tooconnect tooStorSimple um dispositivo Gerenciador de instantâneos, siga as instruções de saudação em Adicionar ou substituir um dispositivo. Quando ele se conecta o dispositivo tooa, Gerenciador de instantâneos StorSimple responde da seguinte maneira:
   
   * Se dispositivo Olá estiver indisponível por qualquer motivo, o Gerenciador de instantâneos StorSimple retorna uma mensagem de erro. 
   
   * Se o dispositivo Olá estiver disponível, Gerenciador de instantâneos StorSimple adiciona uma conexão. Quando você seleciona o dispositivo Olá, ela aparece no hello **resultados** painel, e campo de status de saudação indica que o dispositivo Olá **disponível**. Gerenciador de instantâneos StorSimple importa quaisquer grupos de volumes configurados para dispositivo Olá, desde que os grupos de volume Olá tenham backups associados. Políticas de backup não são importadas. Grupos de volumes que não têm backups associados não são importados.
2. Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager.
3. Com o botão direito Olá nó superior Olá **escopo** painel e clique **alternar a exibição das importações**.
   
    ![Selecionar Alternar Exibição de Importações](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Toggle_Imports_Display.png) 
4. Olá **alternar a exibição das importações** caixa de diálogo é exibida, mostrar o status Olá Olá importado grupos de volumes e backups. Clique em **OK**.

Depois de Olá grupos de volume e os backups são importados com êxito, você pode usar o Gerenciador de instantâneos StorSimple toomanage-los, apenas ao gerenciamento de grupos de volumes e backups que você criou e configurou com o Gerenciador de instantâneos do StorSimple. 

## <a name="refresh-connected-devices"></a>Atualizar os dispositivos conectados
Use Olá seguindo o procedimento toosynchronize Olá conectado StorSimple dispositivos com o Gerenciador de instantâneos do StorSimple.

#### <a name="toorefresh-connected-devices"></a>dispositivos conectados do toorefresh
1. Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager.
2. Em Olá **escopo** painel, clique com botão direito **dispositivos**e, em seguida, clique em **atualizar dispositivos**. Isso sincroniza o hello conectado dispositivos com o Gerenciador de instantâneos do StorSimple para que você possa exibir os grupos de volume hello e backups, incluindo quaisquer adições recentes. 
   
    ![Atualizar dispositivos de StorSimple Olá](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Refresh_devices.png)

Olá **atualizar dispositivos** ação recupera quaisquer novos grupos de volume e backups associados dos dispositivos conectados. Ao contrário de saudação **examinar volumes novamente** ação disponível para Olá **Volumes** nó **atualizar dispositivos** não restaura o backup do registro de saudação.

## <a name="authenticate-a-device"></a>Autenticar um dispositivo
Use Olá seguindo o procedimento tooauthenticate um dispositivo StorSimple com o Gerenciador de instantâneos do StorSimple.

#### <a name="tooauthenticate-a-device"></a>tooauthenticate um dispositivo
1. Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager.
2. Em Olá **escopo** painel, clique em **dispositivos**.
3. Em Olá **resultados** painel, clique o nome de saudação do dispositivo de saudação e, em seguida, clique em **autenticar**.
4. Olá **autenticar** caixa de diálogo é exibida. Digite a senha do dispositivo hello e, em seguida, clique em **Okey**.
   
    ![Caixa de diálogo Autenticar](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Authenticate.png) 

## <a name="view-device-details"></a>Exibir detalhes do dispositivo
Use Olá procedimento tooview Olá detalhes de um dispositivo StorSimple a seguir e, se necessário, ressincronizar dispositivo Olá com o Gerenciador de instantâneos do StorSimple.

#### <a name="tooview-and-resynchronize-device-details"></a>detalhes do dispositivo tooview e se sincronizem novamente
1. Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager.
2. Em Olá **escopo** painel, clique em **dispositivos**.
3. Em Olá **resultados** painel, clique o nome de saudação do dispositivo de saudação e, em seguida, clique em **detalhes**.

4. Olá **detalhes do dispositivo** caixa de diálogo é exibida. Esta caixa mostra o nome hello, modelo, versão, número de série, status, o destino iSCSI IQN (nome qualificado) e a última data de sincronização e tempo.

* Clique em **Resync** toosynchronize dispositivo de saudação.
* Clique em **Okey** ou **Cancelar** tooclose caixa de diálogo de saudação.
  
  ![Detalhes do Dispositivo](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Device_details.png) 

## <a name="refresh-an-individual-device"></a>Atualizar um dispositivo individual
Use Olá seguindo o procedimento tooresynchronize um dispositivo StorSimple individual com o Gerenciador de instantâneos do StorSimple.

#### <a name="toorefresh-a-device"></a>toorefresh um dispositivo
1. Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager. 
2. Em Olá **escopo** painel, clique em **dispositivos**. 
3. Em Olá **resultados** painel, clique o nome de saudação do dispositivo de saudação e, em seguida, clique em **atualizar dispositivo**. Isso sincroniza o dispositivo Olá com o Gerenciador de instantâneos do StorSimple.

## <a name="delete-a-device-configuration"></a>Excluir uma configuração de dispositivo
Use Olá seguindo o procedimento toodelete uma configuração de dispositivo StorSimple individual do Gerenciador de instantâneos do StorSimple.

#### <a name="toodelete-a-device-configuration"></a>toodelete uma configuração de dispositivo
1. Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager.
2. Em Olá **escopo** painel, clique em **dispositivos**. 
3. Em Olá **resultados** painel, clique o nome de saudação do dispositivo de saudação e, em seguida, clique em **excluir**. 
4. Olá a seguinte mensagem será exibida. Clique em **Sim** toodelete Olá configuração ou clique em **não** toocancel exclusão de saudação.
   
    ![Excluir configuração de dispositivo](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_DeleteDevice.png)

## <a name="change-an-expired-device-password"></a>Alterar uma senha de dispositivo expirada
Você deve digitar uma senha tooauthenticate um dispositivo StorSimple com o Gerenciador de instantâneos do StorSimple. Você configura essa senha quando você usa tooset de interface do Windows PowerShell Olá dispositivo hello. No entanto, a senha de saudação pode expirar. Se isso acontecer, você pode usar a senha de saudação do hello toochange de portal clássico do Azure. Em seguida, porque o dispositivo Olá foi configurado no Gerenciador de instantâneos do StorSimple antes Olá senha expirada, deve autenticar novamente o dispositivo Olá no Gerenciador de instantâneos do StorSimple.

#### <a name="toochange-hello-expired-password"></a>senha expirada de saudação toochange
1. No hello portal clássico do Azure, inicie o serviço StorSimple Manager hello.
2. Clique em **dispositivos** > **configurar** para dispositivo hello.
3. Role para baixo toohello seção do Gerenciador de instantâneos do StorSimple. Insira uma senha que tenha 14 ou 15 caracteres. Verifique se que essa senha Olá contém uma combinação de caracteres maiusculo, minúsculo, numérico e especial.
4. Insira novamente a saudação senha tooconfirm-lo.
5. Clique em **salvar** final Olá Olá página.

#### <a name="toore-authenticate-hello-device"></a>toore-autenticar Olá dispositivo
1. Inicie o StorSimple Snapshot Manager.
2. Em Olá **escopo** painel, clique em **dispositivos**. É exibida uma lista dos dispositivos configurados no hello **resultados** painel.
3. Selecione o dispositivo hello, com o botão direito e clique **autenticar**.
4. Em Olá **autenticar** janela, digite Olá nova senha.
5. Selecione o dispositivo hello, com o botão direito e selecione **atualização dispositivo**. Isso sincroniza o dispositivo Olá com o Gerenciador de instantâneos do StorSimple.

## <a name="replace-a-failed-device"></a>Substituir um dispositivo com falha
Se um dispositivo StorSimple falha e for substituído por um dispositivo em espera (failover), use Olá seguindo as etapas tooconnect toohello novo dispositivo e exibição Olá backups associados.

#### <a name="tooconnect-tooa-new-device-after-failover"></a>tooconnect tooa novo dispositivo após o failover
1. Reconfigure Olá iSCSI conexão toohello novo dispositivo. Para obter instruções, vá muito "etapa 7: montar, inicializar e formatar um volume" em [implantar seu dispositivo do StorSimple local](storsimple-8000-deployment-walkthrough-u2.md).

> [!NOTE]
> Se o dispositivo StorSimple novo de saudação tem hello mesmo endereço IP hello antigo, talvez seja configuração antiga do tooconnect capaz de saudação.


1. Pare Olá serviço de gerenciamento do Microsoft StorSimple:
   
   1. Inicie o Gerenciador do Servidor.
   2. Em Olá painel do Gerenciador do servidor, em Olá **ferramentas** menu, selecione **serviços**.
   3. Em Olá **serviços** janela, selecione Olá **serviço de gerenciamento do Microsoft StorSimple**.
   4. Em Olá direita painel, em **serviço de gerenciamento do Microsoft StorSimple**, clique em **parar serviço Olá**.
2. Remova Olá configuração informações relacionadas toohello antigo dispositivo:
   
   1. No Explorador de arquivos, procure tooC:\ProgramData\Microsoft\StorSimple\BACatalog.
   2. Exclua arquivos de saudação na pasta BACatalog de saudação.
3. Reinicie Olá serviço de gerenciamento do Microsoft StorSimple:
   
   1. Em Olá painel do Gerenciador do servidor, em Olá **ferramentas** menu, selecione **serviços**.
   2. Em Olá **serviços** janela, selecione Olá **serviço de gerenciamento do Microsoft StorSimple**.
   3. Em Olá direita painel, em **serviço de gerenciamento do Microsoft StorSimple**, clique em **reiniciar serviço Olá**.
4. Inicie o StorSimple Snapshot Manager.
5. Olá completa tooconfigure Olá novo StorSimple dispositivo, as etapas na etapa 2: conectar um dispositivo StorSimple no [implantar o Gerenciador de instantâneos do StorSimple](storsimple-snapshot-manager-deployment.md).
6. Nó de nível superior de saudação com o botão direito no hello **escopo** painel (Gerenciador de instantâneos do StorSimple no exemplo hello) e depois clique em **alternar a exibição das importações**. 
7. Uma mensagem aparece quando Olá importados grupos de volumes e backups ficam visíveis no Gerenciador de instantâneos do StorSimple. Clique em **OK**.

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[usar o Gerenciador de instantâneos StorSimple tooadminister sua solução StorSimple](storsimple-snapshot-manager-admin.md).
* Saiba como muito[usar Gerenciador de instantâneos StorSimple tooview e gerenciar volumes](storsimple-snapshot-manager-manage-volumes.md).

