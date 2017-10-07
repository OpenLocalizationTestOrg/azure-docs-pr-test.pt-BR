---
title: 'O Backup do Azure: Tooa de restaurar o estado do sistema Windows Server | Microsoft Docs'
description: "Explicação passo a passo para restaurar o estado do sistema do Windows Server de um backup no Azure."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/18/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: a45506507f53e2744350d3b6b2e52f1db415de4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-system-state-toowindows-server"></a>Restaurar o estado do sistema tooWindows Server

Este artigo explica como os backups de estado do sistema do Windows Server toorestore dos serviços de recuperação de um Azure cofre. toorestore estado do sistema, você deve ter um backup de estado do sistema (criados usando instruções Olá [backup de estado do sistema](backup-azure-system-state.md#back-up-windows-server-system-state-preview)) e certifique-se de ter instalado o hello [versão mais recente de saudação do Microsoft Azure Recovery O agente de serviços (MARS)](http://aka.ms/azurebackup_agent). Recuperar dados de estado do sistema do Windows Server de um cofre de serviços de recuperação do Azure é um processo de duas etapas:

1. Restaure o estado do sistema como arquivos de Backup do Azure. Ao restaurar o estado do sistema como arquivos de Backup do Azure, você pode:
  * Restaurar o estado do sistema toohello mesmo servidor em que foram feitos backups hello, ou
  * Servidor alternativo do tooan do arquivo de restauração de estado do sistema.

2. Aplica tooa arquivos de estado do sistema Olá restaurado do Windows Server.


## <a name="recover-system-state-files-toohello-same-server"></a>Recuperar o estado do sistema de arquivos toohello mesmo servidor
Olá etapas a seguir explica como fazer o seu estado anterior do Windows Server configuração tooa tooroll. Reverter o servidor de configuração tooa back conhecido, o estado estável, pode ser extremamente valioso. saudação do estado do sistema do servidor de saudação restauração etapas a seguir de um cofre de serviços de recuperação. 

1. Olá abrir **Backup do Microsoft Azure** snap-in. Se você não souber onde Olá snap-in foi instalado, pesquisar Olá computador ou servidor para **Backup do Microsoft Azure**.

    aplicativo de área de trabalho de saudação deve aparecer nos resultados da pesquisa Olá.

2. Clique em **recuperar dados** toostart Assistente de saudação.

    ![Recuperar Dados](./media/backup-azure-restore-windows-server/recover.png)

3. Em Olá **Introdução** painel, toorestore Olá dados toohello mesmo servidor ou computador, selecione **neste servidor (`<server name>`)** e clique em **próximo**.

    ![Escolha esse servidor opção toorestore Olá dados toohello mesmo computador](./media/backup-azure-restore-system-state/samemachine.png)

4. Em Olá **Selecionar modo de recuperação** painel, escolha **o estado do sistema** e, em seguida, clique em **próximo**.

    ![Procurar arquivos](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. No calendário Olá em **selecionar Volume e data** ponto do painel, selecione uma recuperação. 

    Você pode restaurar de qualquer ponto de recuperação. Datas no **negrito** indicar a disponibilidade de saudação de pelo menos um ponto de recuperação. Quando você seleciona uma data, se houver vários pontos de recuperação, escolher o ponto de recuperação específico Olá Olá **tempo** menu suspenso.

    ![Volume e data](./media/backup-azure-restore-system-state/select-date.png)

6. Depois de ter escolhido Olá toorestore de ponto de recuperação, clique em **próximo**.

    O Backup do Azure monta o ponto de recuperação locais hello e utiliza como um volume de recuperação.

7. No painel de Avançar hello, especifique o destino Olá Olá recuperar arquivos de estado do sistema e clique em **procurar** tooopen Windows Explorer e localize Olá arquivos e pastas que você deseja. Olá opção **criar cópias para ter ambas as versões**, cria cópias de arquivos individuais em um arquivo existente de estado do sistema em vez de criar a cópia de saudação de todo o arquivo de estado do sistema hello.

    ![Opções de recuperação](./media/backup-azure-restore-system-state/recover-as-files.png)

8. Verifique os detalhes de saudação de recuperação em Olá **confirmação** painel e clique em **recuperar**.

   ![Clique em recuperar tooacknowledge Olá recuperar ação](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. Saudação de cópia *WindowsImageBackup* diretório no volume não críticos de tooa do destino de recuperação do servidor de saudação do hello. Geralmente, Olá volume do sistema operacional Windows é volume crítico hello.

10. Depois que a recuperação de saudação for bem-sucedida, execute as etapas de saudação na seção Olá, [aplicar restaurado toohello de arquivos de estado do sistema Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), Olá toocomplete processo de recuperação do estado do sistema.

## <a name="recover-system-state-files-tooan-alternate-server"></a>Recuperar o estado do sistema de arquivos de servidor alternativo tooan

Se seu servidor do Windows está corrompido ou inacessível, e você quiser toorestore-tooa o estado estável, recuperando Olá estado do sistema do Windows Server, você pode restaurar o estado do sistema do servidor de saudação corrompido de outro servidor. Use Olá seguindo as etapas toohello restaurar estado do sistema em um servidor separado.  

terminologia de saudação usada essas etapas incluem:

- *Máquina de origem* – máquina original de saudação do qual backup Olá foi feita e que está disponível no momento.
- *Computador de destino* – Olá máquina toowhich Olá dados estão sendo recuperados.
- *Cofre de exemplo* – Olá Olá de toowhich de Cofre de serviços de recuperação *máquina de origem* e *máquina destino* são registrados. <br/>

> [!NOTE]
> Os backups de um computador não podem ser restaurado tooa máquina executando uma versão anterior do sistema operacional de saudação. Por exemplo, os backups de um Windows Server 2016 máquina não pode ser restaurado tooWindows Server 2012 R2. No entanto, o inverso de saudação é possível. Você pode usar os backups do Windows Server 2012 R2 toorestore Windows Server 2016.
>

1. Olá abrir **Backup do Microsoft Azure** snap-in no hello *máquina de destino*.
2. Certifique-se de que Olá *máquina destino* e hello *máquina de origem* são registrado toohello dos serviços de recuperação mesmo cofre.
3. Clique em **recuperar dados** fluxo de trabalho tooinitiate hello.

    ![Recuperar Dados](./media/backup-azure-restore-windows-server-classic/recover.png)

4. Selecione **Outro servidor**

    ![Outro servidor](./media/backup-azure-restore-system-state/anotherserver.png)

5. Fornecer o arquivo de credencial de cofre Olá correspondente toohello *cofre exemplo*. Se o arquivo de credencial de cofre Olá é inválido (ou expirado), baixe um novo arquivo de credencial de Cofre de saudação *cofre exemplo* em Olá portal do Azure. Depois que o arquivo de credencial de cofre Olá for fornecido, Cofre de serviços de recuperação de saudação associado ao arquivo de credencial de cofre Olá é exibida.

6. No painel de selecionar servidor de Backup do hello, selecione Olá *máquina de origem* da lista de saudação de máquinas exibidas.

    ![Lista de computadores](./media/backup-azure-restore-windows-server-classic/machinelist.png)

7. No painel de selecionar modo de recuperação hello, escolha **o estado do sistema** e clique em **próximo**. 

    ![Pesquisar](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. Em Olá calendário no hello **selecionar Volume e data** ponto do painel, selecione uma recuperação. Você pode restaurar de qualquer ponto de recuperação. Datas no **negrito** indicar a disponibilidade de saudação de pelo menos um ponto de recuperação. Quando você seleciona uma data, se houver vários pontos de recuperação, escolher o ponto de recuperação específico Olá Olá **tempo** menu suspenso. 

    ![Pesquisar itens](./media/backup-azure-restore-system-state/select-date.png)

9. Depois de ter escolhido Olá toorestore de ponto de recuperação, clique em **próximo**.

10. Em Olá **Selecionar modo de recuperação de estado do sistema** painel, especifique o destino Olá onde você deseja que o estado do sistema de arquivos toobe recuperado, e clique em **próximo**.

    ![Criptografia](./media/backup-azure-restore-system-state/recover-as-files.png)

    Olá opção **criar cópias para ter ambas as versões**, cria cópias de arquivos individuais em um arquivo existente de estado do sistema em vez de criar a cópia de saudação de todo o arquivo de estado do sistema hello.

11. Verifique os detalhes de saudação de recuperação no painel de confirmação hello e, em seguida, clique em **recuperar**. 

    ![Clique em processo de recuperação de Olá Olá recuperar botão tooconfirm](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. Saudação de cópia *WindowsImageBackup* volume não críticos do diretório tooa do servidor de saudação (por exemplo d:\). Geralmente Olá volume do sistema operacional Windows é volume crítico hello.

13. processo de recuperação do toocomplete hello, uso a seguir Olá seção muito[aplicar arquivos de estado do sistema Olá restaurado em um servidor Windows](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).




## <a name="apply-restored-system-state-on-a-windows-server"></a>Aplicar o estado do sistema restaurado em um Windows Server

Depois que você tiver recuperado o estado do sistema como arquivos usando o agente de serviços de recuperação do Azure, use Olá Backup do Windows Server utilitário tooapply Olá recuperado tooWindows de estado do sistema servidor. Olá utilitário de Backup do Windows Server já está disponível no servidor de saudação. Olá, as etapas a seguir explica como tooapply Olá recuperado o estado do sistema.

1. A seguir Olá use comandos tooreboot seu servidor *modo de reparo de serviços de diretório*. Em um prompt de comandos com privilégios elevados:

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. Após a reinicialização do hello, abra o snap-in de Backup do Windows Server de hello. Se você não souber onde Olá snap-in foi instalado, pesquisar Olá computador ou servidor para **Backup do Windows Server**.

    o aplicativo de área de trabalho Olá aparece nos resultados da pesquisa Olá.

3. No snap-in hello, selecione **Backup Local**.

    ![Selecione o Backup Local toorestore lá](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. No console de Backup Local hello, em Olá **painel Ações**, clique em **recuperar** tooopen Olá Assistente de recuperação.

5. Selecione a opção hello, **um backup armazenado em outro local**e clique em **próximo**.

   ![Escolha um servidor diferente do toorecover tooa](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. Ao especificar o tipo de local de saudação, selecione **pasta compartilhada remota** se o backup do estado do sistema foi recuperado tooanother server. Se o estado do sistema foi recuperado localmente, então, selecione **unidades locais**. 

    ![Selecione se toorecovery do servidor local ou outro](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. Digite hello caminho toohello *WindowsImageBackup* diretório, ou escolha Olá unidade local que contém esse diretório (por exemplo, D:\WindowsImageBackup) recuperado como parte da recuperação de arquivos de estado do sistema hello usando a recuperação do Azure Serviços de agente e clique em **próximo**.

    ![arquivo compartilhado do caminho toohello](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. Versão de estado do sistema Olá selecione que você deseja toorestore e clique em **próximo**.

9. No painel de selecionar tipo de recuperação hello, selecione **o estado do sistema** e clique em **próximo**.

10. Para obter local Olá Olá recuperação do estado do sistema, selecione **local Original**e clique em **próximo**.

11. Examine os detalhes da confirmação de saudação, verifique as configurações de reinicialização hello e clique em **recuperar** tooapplly Olá restaurado arquivos de estado do sistema.

    ![saudação de inicialização restaurar arquivos de estado do sistema](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a>Considerações especiais para recuperação de estado do sistema no servidor do Active Directory

O backup de estado do sistema inclui dados do Active Directory. Use Olá seguir etapas toorestore serviço de domínio Active Directory (AD DS) de seu estado anterior do estado tooa atual.

1. Reinicie o controlador de domínio de saudação no modo de restauração dos serviços de diretório (DSRM).
2. Siga as etapas de saudação [aqui](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) toorecover cmdlets de Backup do Windows Server toouse AD DS.


## <a name="troubleshoot-failed-system-state-restore"></a>Solucionar problemas de restauração de estado do sistema com falha

Se o processo anterior de saudação da aplicação de estado do sistema não for concluída com êxito, use Olá toorecover de ambiente de recuperação do Windows (Windows RE) do Windows Server. Olá etapas a seguir explicam como toorecover usando o Windows RE. Use esta opção somente se o Windows Server não inicia normalmente após uma restauração de estado do sistema. Olá processo a seguir apaga dados não são do sistema, tenha cuidado. 

1. Inicialize o Windows Server Olá ambiente de recuperação do Windows (Windows RE).

2. Selecione solucionar problemas de três opções disponíveis de saudação.

    ![Abrir menu](./media/backup-azure-restore-system-state/winre-1.png)

3. De saudação **opções avançadas de** tela, selecione **Prompt de comando** e forneça o nome de usuário de administrador de servidor hello e senha.

   ![Abrir menu](./media/backup-azure-restore-system-state/winre-2.png)

4. Forneça a senha e o nome de usuário de administrador de servidor hello.

    ![Abrir menu](./media/backup-azure-restore-system-state/winre-3.png)

5. Quando você abrir o prompt de comando Olá no modo de administrador, execute o seguinte versões de backup do comando tooget Olá estado do sistema.

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![obter versões de backup de estado do sistema](./media/backup-azure-restore-system-state/winre-4.png)

6. Execute Olá tooget de comando a seguir todos os volumes disponíveis no backup hello.

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![obter versões de backup de estado do sistema](./media/backup-azure-restore-system-state/winre-5.png)

7. Olá seguinte comando recupera todos os volumes que fazem parte da saudação Backup de estado do sistema. Observe que essa etapa recupera somente Olá volumes críticos que fazem parte de saudação do estado do sistema. Todos os dados que não são do sistema são apagados.

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![obter versões de backup de estado do sistema](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a>Próximas etapas
* Agora que você restaurou seus arquivos e pastas, poderá [gerenciar seus backups](backup-azure-manage-windows-server.md).
