---
title: aaaRestore dados no computador do Windows ou do Azure tooa Windows Server | Microsoft Docs
description: Saiba como toorestore dados armazenados no computador do Windows ou do Azure tooa do Windows Server.
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 742f4b9e-c0ab-4eeb-8e22-ee29b83c22c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/16/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 11335495e448986a74f1733406f87e04331641d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-resource-manager-deployment-model"></a>Restaurar arquivos tooa Windows server ou o computador de cliente do Windows usando o modelo de implantação do Gerenciador de recursos
> [!div class="op_single_selector"]
> * [Portal do Azure](backup-azure-restore-windows-server.md)
> * [Portal clássico](backup-azure-restore-windows-server-classic.md)
>
>

Este artigo explica como toorestore dados de um cofre de backup. toorestore dados, você usa o Assistente de recuperar dados de saudação no agente do Microsoft Azure Recovery Services (MARS) hello. Ao restaurar dados, é possível:

* Restaurar dados toohello mesmo computador do qual os backups Olá foram realizados.
* Restaure a máquina alternativo de tooan de dados.

Em janeiro de 2017, a Microsoft lançou um agente de MARS toohello de atualização de visualização. Juntamente com correções de bug, essa atualização permite restauração instantânea, que permite que você toomount um instantâneo de ponto de recuperação gravável como um volume de recuperação. Em seguida, você pode explorar Olá recuperação volume e copiar arquivos tooa computador local restaurando assim seletivamente arquivos.

> [!NOTE]
> Olá [de janeiro de 2017 atualização de Backup do Azure](https://support.microsoft.com/en-us/help/3216528?preview) é necessária se você quiser toouse restauração instantânea toorestore dados. Também os dados de backup Olá devem ser protegidos no cofres em localidades listados no artigo de suporte de saudação. Consulte Olá [de janeiro de 2017 atualização de Backup do Azure](https://support.microsoft.com/en-us/help/3216528?preview) para a lista mais recente Olá das localidades que oferecem suporte à restauração instantânea. No momento, a Restauração Instantânea **não** está disponível em todas as localidades.
>

Restauração instantânea está disponível para uso em cofres de serviços de recuperação no hello portal do Azure e cofres de Backup no portal clássico do hello. Se você quiser toouse restauração instantânea, baixe a atualização de MARS Olá e siga os procedimentos de saudação que mencionem restauração instantânea.

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

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
    > Se você não clicar desmontagem, Olá recuperação Volume permanecerá montada por 6 horas de tempo de saudação quando ele foi montado. No entanto, o tempo de montagem de saudação é estendido até um máximo de 24 horas no caso de uma cópia de arquivo em andamento. Nenhuma operação de backup será executado enquanto Olá volume está montado. Toorun qualquer operação de backup agendada durante o tempo de saudação quando o volume de saudação estiver montado, será executado após o volume de saudação de recuperação é desmontado.
    >


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
    > Se você não clicar desmontagem, Olá recuperação Volume permanecerá montada por 6 horas de tempo de saudação quando ele foi montado. No entanto, o tempo de montagem de saudação é estendido até um máximo de 24 horas no caso de uma cópia de arquivo em andamento. Nenhuma operação de backup será executado enquanto Olá volume está montado. Toorun qualquer operação de backup agendada durante o tempo de saudação quando o volume de saudação estiver montado, será executado após o volume de saudação de recuperação é desmontado.
    >

## <a name="troubleshooting"></a>Solucionar problemas
Se Backup do Azure com êxito não montar o volume de recuperação Olá até mesmo após vários minutos clicando em **montar** ou falhar toomount Olá volume de recuperação com um ou mais erros, siga as etapas de saudação abaixo toobegin recuperando normalmente.

1.  Cancele o processo de montagem em andamento de saudação caso esteve em execução por vários minutos.

2.  Certifique-se de que você está na versão mais recente de saudação do agente de Backup do Azure hello. toofind informações de versão de saudação do agente de Backup do Azure, clique em **sobre o Microsoft Azure Recovery Services Agent** em Olá **ações** painel do Microsoft Azure Backup console e certifique-se de que Olá ** Versão** número é igual tooor superior à versão Olá mencionado na [neste artigo](https://go.microsoft.com/fwlink/?linkid=229525). Você pode baixar a versão mais recente de saudação do [aqui](https://go.microsoft.com/fwLink/?LinkID=288905)

3.  Vá muito**Gerenciador de dispositivos** -> **controladores de armazenamento** e certifique-se de que você pode localizar **iniciador Microsoft iSCSI**. Se você pode localizá-lo, vá diretamente toostep 7 abaixo. 

4.  Se você não puder localizar o serviço do iniciador Microsoft iSCSI conforme mencionado na etapa 3, verifique toosee se você pode encontrar uma entrada em **Gerenciador de dispositivos** -> **controladores de armazenamento** chamado ** Dispositivo desconhecido** com a ID de Hardware **ROOT\ISCSIPRT**.

5.  Clique com o botão direito do mouse em **Dispositivo Desconhecido** e selecione **Atualizar Software de Driver**.

6.  Atualizar o driver de hello, selecionando a opção de saudação muito **pesquisar automaticamente software de driver atualizado de**. Conclusão da atualização Olá deve alterar **dispositivo desconhecido** muito**iniciador Microsoft iSCSI** conforme mostrado abaixo. 

    ![Criptografia](./media/backup-azure-restore-windows-server/UnknowniSCSIDevice.png)

7.  Vá muito**Gerenciador de tarefas** -> **serviços (Local)** -> **serviço iniciador Microsoft iSCSI**. 

    ![Criptografia](./media/backup-azure-restore-windows-server/MicrosoftInitiatorServiceRunning.png)
    
8.  Reinicie o serviço Olá Microsoft iSCSI Initiator clicando-se no serviço hello, clicando em **parar** e mais clique direito novamente e clicando em **iniciar**.

9.  Repita a recuperação usando a Restauração Instantânea. 

Se recuperação Olá ainda falhar, reinicialize o servidor/cliente. Se uma reinicialização não é desejável ou recuperação Olá ainda falha mesmo após a reinicialização do servidor de saudação, tente recuperar de uma máquina alternativo e entre em contato com suporte do Azure indo muito[Portal do Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) e enviar uma solicitação de suporte.

## <a name="next-steps"></a>Próximas etapas
* Agora que você restaurou seus arquivos e pastas, poderá [gerenciar seus backups](backup-azure-manage-windows-server.md).
