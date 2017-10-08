---
title: "Olá de aaaRestore tooa de dados do Windows Server ou Windows Client do Azure usando o modelo de implantação clássico | Microsoft Docs"
description: Saiba como toorestore de um cliente do Windows ou Windows Server.
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 85585dfc-c764-4e8c-8f0e-40b969640ac2
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 4d1458d5233c4f55004ecfa95cbf7b3b18a03dde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-hello-classic-deployment-model"></a>Restaurar arquivos tooa Windows server ou o computador de cliente do Windows usando o modelo de implantação clássico Olá
> [!div class="op_single_selector"]
> * [Portal clássico](backup-azure-restore-windows-server-classic.md)
> * [Portal do Azure](backup-azure-restore-windows-server.md)
>
>

Este artigo explica como toorecover dados de um backup de cofre e restauração-lo tooa servidor ou computador. A partir de março de 2017, você não pode mais criar cofres de backup no portal clássico do hello.

> [!IMPORTANT]
> Agora você pode atualizar seu cofres dos serviços de tooRecovery de cofres de Backup. Para obter detalhes, consulte o artigo Olá [atualizar um tooa de Cofre de Backup Cofre de serviços de recuperação](backup-azure-upgrade-backup-to-recovery-services.md). A Microsoft incentiva tooupgrade cofres de serviços tooRecovery os cofres de Backup.<br/> **15 de outubro de 2017**, não será capaz de toouse PowerShell toocreate os cofres de Backup. <br/> **A partir de 1º de novembro de 2017**:
>- Nenhum Cofre de Backup restante será automaticamente atualizado tooRecovery cofres de serviços.
>- Você não será capaz de tooaccess os dados de backup no portal clássico do hello. Em vez disso, use Olá tooaccess portal do Azure os dados de backup em cofres de serviços de recuperação.
>

toorestore dados, você usa o Assistente de recuperar dados de saudação no agente do Microsoft Azure Recovery Services (MARS) hello. Ao restaurar dados, é possível:

* Restaurar dados toohello mesmo computador do qual os backups Olá foram realizados.
* Restaure a máquina alternativo de tooan de dados.

Em janeiro de 2017, a Microsoft lançou um agente de MARS toohello de atualização de visualização. Juntamente com correções de bug, essa atualização permite restauração instantânea, que permite que você toomount um instantâneo de ponto de recuperação gravável como um volume de recuperação. Em seguida, você pode explorar Olá recuperação volume e copiar arquivos tooa computador local restaurando assim seletivamente arquivos.

> [!NOTE]
> Olá [de janeiro de 2017 atualização de Backup do Azure](https://support.microsoft.com/en-us/help/3216528?preview) é necessária se você quiser toouse restauração instantânea toorestore dados. Também os dados de backup Olá devem ser protegidos no cofres em localidades listados no artigo de suporte de saudação. Consulte Olá [de janeiro de 2017 atualização de Backup do Azure](https://support.microsoft.com/en-us/help/3216528?preview) para a lista mais recente Olá das localidades que oferecem suporte à restauração instantânea. No momento, a Restauração Instantânea **não** está disponível em todas as localidades.
>

Restauração instantânea está disponível para uso em cofres de serviços de recuperação no hello portal do Azure e cofres de Backup no portal clássico do hello. Se você quiser toouse restauração instantânea, baixe a atualização de MARS Olá e siga os procedimentos de saudação que mencionem restauração instantânea.


## <a name="use-instant-restore-toorecover-data-toohello-same-machine"></a>Use a restauração instantânea toohello de dados toorecover mesmo computador

Se você excluiu acidentalmente um arquivo e quiser toorestore-toohello mesma máquina (do qual Olá é feito backup), Olá seguindo as etapas ajudará você a recuperar dados de saudação.

1. Olá abrir **Backup do Microsoft Azure** encaixe em. Se você não souber onde o snap-in de saudação foi instalado, pesquisar Olá computador ou servidor para **Backup do Microsoft Azure**.

    aplicativo de área de trabalho de saudação deve aparecer nos resultados da pesquisa Olá.

2. Clique em **recuperar dados** toostart Assistente de saudação.

    ![Recuperar Dados](./media/backup-azure-restore-windows-server/recover.png)

3. Em Olá **Introdução** painel, toorestore Olá dados toohello mesmo servidor ou computador, selecione **neste servidor (`<server name>`)** e clique em **próximo**.

    ![Escolha esse servidor opção toorestore Olá dados toohello mesmo computador](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. Em Olá **Selecionar modo de recuperação** painel, escolha **arquivos e pastas individuais** e, em seguida, clique em **próximo**.

    ![Procurar arquivos](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. Em Olá **selecionar Volume e data** painel, o volume de saudação select que contém arquivos de saudação e/ou pastas que você deseja toorestore.

    No calendário hello, selecione um ponto de recuperação. Você pode restaurar de qualquer ponto de recuperação. Datas no **negrito** indicar a disponibilidade de saudação de pelo menos um ponto de recuperação. Quando você seleciona uma data, se houver vários pontos de recuperação, escolher o ponto de recuperação específico Olá Olá **tempo** menu suspenso.

    ![Volume e data](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. Depois de ter escolhido Olá toorestore de ponto de recuperação, clique em **montar**.

    O Backup do Azure monta o ponto de recuperação locais hello e utiliza como um volume de recuperação.

7. Em Olá **procurar e recuperar arquivos** painel, clique em **procurar** tooopen Windows Explorer e localize Olá arquivos e pastas que você deseja.

    ![Opções de recuperação](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. No Windows Explorer, Olá copiar os arquivos e/ou pastas você deseja toorestore e colá-los tooany local toohello local servidor ou computador. Você pode abrir ou transmitir Olá arquivos diretamente do volume de recuperação hello e verificar Olá correto versões são recuperadas.

    ![Copie e cole os arquivos e pastas do local do volume montado toolocal](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. Quando você terminar de restauração Olá arquivos e/ou pastas, Olá **arquivos de recuperação e procurar** painel, clique em **desmontagem**. Em seguida, clique em **Sim** tooconfirm que você deseja que o volume de saudação toounmount.

    ![Desmontar o volume de saudação e confirmar](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > Se você não clicar desmontagem, Olá Volume de recuperação permanecerá montada por seis horas de tempo de saudação quando ele foi montado. Nenhuma operação de backup será executado enquanto Olá volume está montado. Toorun qualquer operação de backup agendada durante o tempo de saudação quando o volume de saudação estiver montado, será executado após o volume de saudação de recuperação é desmontado.
    >


## <a name="recover-data-toohello-same-machine"></a>Recuperar dados toohello mesmo computador
Se você excluiu acidentalmente um arquivo e quiser toorestore-toohello mesma máquina (do qual Olá é feito backup), Olá seguindo as etapas ajudará você a recuperar dados de saudação.

1. Olá abrir **Backup do Microsoft Azure** encaixe em.
2. Clique em **recuperar dados** fluxo de trabalho tooinitiate hello.

    ![Recuperar Dados](./media/backup-azure-restore-windows-server-classic/recover.png)
3. Olá selecione  **neste servidor (*yourmachinename*) * * saudação de toorestore opção backup arquivo hello mesmo computador.

    ![Mesmo computador](./media/backup-azure-restore-windows-server-classic/samemachine.png)
4. Escolha muito**procurar arquivos** ou **pesquisar arquivos**.

    Deixe saudação padrão opção se você planejar toorestore um ou mais arquivos cujo caminho é conhecido. Se você não tiver certeza sobre a estrutura de pasta Olá, mas desejar toosearch para um arquivo, selecione Olá **pesquisar arquivos** opção. Finalidade Olá nesta seção, vamos continuará com a opção padrão de saudação.

    ![Procurar arquivos](./media/backup-azure-restore-windows-server-classic/browseandsearch.png)
5. Selecione o volume de saudação do qual você deseja que o arquivo de saudação toorestore.

    Você pode restaurar de qualquer momento anterior. Datas que aparecem no **negrito** no controle de calendário Olá indicar a disponibilidade de saudação de um ponto de restauração. Quando uma data é selecionada, com base em seu agendamento de backup (e o sucesso de saudação de uma operação de backup), você pode selecionar um ponto no tempo de saudação **tempo** lista suspensa.

    ![Volume e data](./media/backup-azure-restore-windows-server-classic/volanddate.png)
6. Selecione Olá toorecover de itens. Você pode selecionar várias pastas/arquivos que você deseja toorestore.

    ![Selecionar arquivos](./media/backup-azure-restore-windows-server-classic/selectfiles.png)
7. Especifica parâmetros de recuperação de saudação.

    ![Opções de recuperação](./media/backup-azure-restore-windows-server-classic/recoveroptions.png)

   * Você tem a opção de restauração toohello local original (no qual Olá arquivo/pasta seria substituída) ou tooanother em Olá mesma máquina.
   * Se Olá arquivo/pasta toorestore existe no local de destino hello, você pode criar cópias (duas versões do hello mesmo arquivo), substituir arquivos Olá no local de destino hello ou ignorar a recuperação de saudação de arquivos de saudação que existe no destino hello.
   * É altamente recomendável que você deixe a opção padrão de saudação da restauração de ACLs de saudação em arquivos de saudação que estão sendo recuperados.
8. Depois que essas entradas forem fornecidas, clique em **Próximo**. Olá recuperação fluxo de trabalho, que restaura Olá arquivos toothis máquina, será iniciado.

## <a name="recover-tooan-alternate-machine"></a>Recuperar máquina alternativo tooan
Se o servidor inteiro for perdido, você ainda poderá recuperar dados de máquina do Azure Backup tooa diferente. Olá etapas a seguir ilustra o fluxo de trabalho de saudação.  

terminologia de saudação usada essas etapas incluem:

* *Máquina de origem* – máquina original de saudação do qual backup Olá foi feita e que está disponível no momento.
* *Computador de destino* – Olá máquina toowhich Olá dados estão sendo recuperados.
* *Cofre de exemplo* – Olá Olá de toowhich de Cofre de Backup *máquina de origem* e *máquina destino* são registrados. <br/>

> [!NOTE]
> Os backups de uma máquina não podem ser restaurados em um computador que está executando uma versão anterior do sistema operacional de saudação. Por exemplo, se um backup for de um computador com Windows 7, ele poderá ser restaurado em um computador com Windows 8 ou superior. No entanto, o contrário Olá não verdadeiras.
>
>

1. Olá abrir **Backup do Microsoft Azure** encaixe em Olá *máquina de destino*.
2. Certifique-se de que Olá *máquina destino* e hello *máquina de origem* são toohello registrado mesmo Cofre de backup.
3. Clique em **recuperar dados** fluxo de trabalho tooinitiate hello.

    ![Recuperar Dados](./media/backup-azure-restore-windows-server-classic/recover.png)
4. Selecione **Outro servidor**

    ![Outro servidor](./media/backup-azure-restore-windows-server-classic/anotherserver.png)
5. Fornecer o arquivo de credencial de cofre Olá correspondente toohello *cofre exemplo*. Se o arquivo de credencial de cofre Olá é inválido (ou expirados) baixar um novo arquivo de credencial de Cofre de saudação *cofre exemplo* em Olá portal clássico do Azure. Depois que o arquivo de credencial de cofre Olá for fornecido, o Cofre de backup Olá no arquivo de credencial de cofre Olá é exibido.
6. Selecione Olá *máquina de origem* da lista de saudação de máquinas exibidas.

    ![Lista de computadores](./media/backup-azure-restore-windows-server-classic/machinelist.png)
7. Selecione qualquer Olá **pesquisar arquivos** ou **procurar arquivos** opção. Para finalidade de saudação desta seção, usaremos Olá **pesquisar arquivos** opção.

    ![Pesquisar](./media/backup-azure-restore-windows-server-classic/search.png)
8. Selecione Olá volume e data na próxima tela de saudação. Pesquisa de nome de pasta/arquivo hello deseja toorestore.

    ![Pesquisar itens](./media/backup-azure-restore-windows-server-classic/searchitems.png)
9. Selecione Olá local onde os arquivos de saudação necessário toobe restaurado.

    ![Restaurar local](./media/backup-azure-restore-windows-server-classic/restorelocation.png)
10. Fornecer Olá senha de criptografia que foi fornecida durante a *máquina de origem* registro muito*cofre exemplo*.

    ![Criptografia](./media/backup-azure-restore-windows-server-classic/encryption.png)
11. Depois de entrada hello for fornecida, clique em **recuperar**, que gatilhos Olá restauração de saudação backup arquivos toohello destino fornecido.

## <a name="use-instant-restore-toorestore-data-tooan-alternate-machine"></a>Usar restauração instantânea toorestore dados tooan alternativa máquina
Se o servidor inteiro for perdido, você ainda poderá recuperar dados de máquina do Azure Backup tooa diferente. Olá etapas a seguir ilustra o fluxo de trabalho de saudação.

terminologia de saudação usada essas etapas incluem:

* *Máquina de origem* – máquina original de saudação do qual backup Olá foi feita e que está disponível no momento.
* *Computador de destino* – Olá máquina toowhich Olá dados estão sendo recuperados.
* *Cofre de exemplo* – Olá Olá de toowhich de Cofre de serviços de recuperação *máquina de origem* e *máquina destino* são registrados. <br/>

> [!NOTE]
> Os backups não podem ser restaurado tooa máquina de destino executando uma versão anterior do sistema operacional de saudação. Por exemplo, um backup feito em um computador com Windows 7 pode ser restaurado em um computador com Windows 8 ou mais recente. Um backup feito em um computador Windows 8 não pode ser o computador restaurado tooa Windows 7.
>
>

1. Olá abrir **Backup do Microsoft Azure** encaixe em Olá *máquina de destino*.

2. Certifique-se de saudação *máquina destino* e hello *máquina de origem* são registrado toohello dos serviços de recuperação mesmo cofre.

3. Clique em **recuperar dados** tooopen Olá **Assistente para recuperar dados**.

    ![Recuperar Dados](./media/backup-azure-restore-windows-server/recover.png)

4. Em Olá **Introdução** painel, selecione **outro servidor**

    ![Outro servidor](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. Fornecer o arquivo de credencial de cofre Olá correspondente toohello *cofre exemplo*e clique em **próximo**.

    Se o arquivo de credencial de cofre Olá é inválido (ou expirado), baixe um novo arquivo de credencial de Cofre de saudação *cofre exemplo* em Olá portal do Azure. Depois que você forneça uma credencial de cofre válida, Olá nome da saudação que Cofre de Backup correspondente é exibida.

6. Em Olá **Selecionar servidor de Backup** painel, selecione Olá *máquina de origem* da lista de saudação de máquinas exibidas e forneça a senha de saudação. Em seguida, clique em **Próximo**.

    ![Lista de computadores](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. Em Olá **Selecionar modo de recuperação** painel, selecione **arquivos e pastas individuais** e clique em **próximo**.

    ![Pesquisar](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. Em Olá **selecionar Volume e data** painel, o volume de saudação select que contém arquivos de saudação e/ou pastas que você deseja toorestore.

    No calendário hello, selecione um ponto de recuperação. Você pode restaurar de qualquer ponto de recuperação. Datas no **negrito** indicar a disponibilidade de saudação de pelo menos um ponto de recuperação. Quando você seleciona uma data, se houver vários pontos de recuperação, escolher o ponto de recuperação específico Olá Olá **tempo** menu suspenso.

    ![Pesquisar itens](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. Clique em **montar** toolocally montagem Olá ponto de recuperação como um volume de recuperação em seu *máquina de destino*.

10. Em Olá **procurar e recuperar arquivos** painel, clique em **procurar** tooopen Windows Explorer e localize Olá arquivos e pastas que você deseja.

    ![Criptografia](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. No Windows Explorer, copie arquivos hello e/ou pastas do volume de recuperação hello e colá-los tooyour *máquina destino* local. Você pode abrir ou transmitir Olá arquivos diretamente do volume de recuperação hello e verificar Olá correto versões são recuperadas.

    ![Criptografia](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. Quando você terminar de restauração Olá arquivos e/ou pastas, Olá **arquivos de recuperação e procurar** painel, clique em **desmontagem**. Em seguida, clique em **Sim** tooconfirm que você deseja que o volume de saudação toounmount.

    ![Criptografia](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > Se você não clicar desmontagem, Olá Volume de recuperação permanecerá montada por seis horas de tempo de saudação quando ele foi montado. Nenhuma operação de backup será executado enquanto Olá volume está montado. Toorun qualquer operação de backup agendada durante o tempo de saudação quando o volume de saudação estiver montado, será executado após o volume de saudação de recuperação é desmontado.
    >


## <a name="next-steps"></a>Próximas etapas
* [Backup do Azure - Perguntas frequentes](backup-azure-backup-faq.md)
* Visite Olá [Fórum de Backup do Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933).

## <a name="learn-more"></a>Saiba mais
* [Visão geral do backup do Azure](http://go.microsoft.com/fwlink/p/?LinkId=222425)
* [Fazer backup de máquinas virtuais do Azure](backup-azure-vms-introduction.md)
* [Fazer backup de cargas de trabalho Microsoft](backup-azure-dpm-introduction.md)
