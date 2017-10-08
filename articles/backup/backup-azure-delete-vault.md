---
title: " Exclua um cofre de Serviços de Recuperação no Azure | Microsoft Docs "
description: "Como toodelete um Backup do Azure e serviços de recuperação do cofre. Um cofre de backup pode ser chamado de cofre de nuvem do Azure ou cofre de recuperação do Azure. Solução de problemas quando você não pode excluir um cofre de backup no portal clássico do hello ou o portal do Azure."
services: service-name
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 5fa08157-2612-4020-bd90-f9e3c3bc1806
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: markgal;trinadhk
ms.openlocfilehash: 9047f50f4b2c991fbf2454ddcad08073ec7cd975
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-recovery-services-vault"></a>Excluir um cofre dos Serviços de Recuperação
saudação de serviço de Backup do Azure tem dois tipos de cofres - Cofre de Backup hello e Olá Cofre de serviços de recuperação. Cofre de Backup Olá ocorreram primeiro. Em seguida, Olá Cofre de serviços de recuperação fornecida ao longo de implantações de Gerenciador de recursos do toosupport Olá expandido. Devido a saudação recursos expandidos e dependências de informações de saudação que devem ser armazenadas no cofre hello, excluir um cofre de Backup ou serviços de recuperação podem ser confusas. Este artigo explica como toodelete Olá cofres no portal clássico do hello e hello portal do Azure.  

| **Tipo de implantação** | **Portal** | **Nome do cofre** |
| --- | --- | --- |
| Clássico |Clássico |Cofre de backup |
| Gerenciador de Recursos |As tabelas |Cofre dos Serviços de Recuperação |

> [!NOTE]
> Cofres de backup não podem ser usados para proteger soluções implantadas pelo Resource Manager. No entanto, você pode usar um cofre de serviços de recuperação tooprotect modo clássico implantado servidores e máquinas virtuais.  
>

> [!IMPORTANT]
> Agora você pode atualizar seu cofres dos serviços de tooRecovery de cofres de Backup. Para obter detalhes, consulte o artigo Olá [atualizar um tooa de Cofre de Backup Cofre de serviços de recuperação](backup-azure-upgrade-backup-to-recovery-services.md). A Microsoft incentiva tooupgrade cofres de serviços tooRecovery os cofres de Backup.<br/> **15 de outubro de 2017**, não será capaz de toouse PowerShell toocreate os cofres de Backup. <br/> **A partir de 1º de novembro de 2017**:
>- Nenhum Cofre de Backup restante será automaticamente atualizado tooRecovery cofres de serviços.
>- Você não será capaz de tooaccess os dados de backup no portal clássico do hello. Em vez disso, use Olá tooaccess portal do Azure os dados de backup em cofres de serviços de recuperação.
>

Neste artigo, usamos o termo hello, cofre, toohello de toorefer formulário genérico do Cofre de Backup hello ou Cofre de serviços de recuperação. Usamos nome formal do hello, Cofre de Backup ou Cofre de serviços de recuperação, quando é necessário toodistinguish entre cofres hello.

## <a name="deleting-a-recovery-services-vault"></a>Excluir um cofre dos Serviços de Recuperação
Excluir um cofre de serviços de recuperação é um processo de uma etapa - *fornecido cofre Olá não contém nenhum recurso*. Antes de excluir um cofre de serviços de recuperação, você deve remover ou excluir todos os recursos no cofre hello. Se você tentar toodelete um cofre que contém recursos, você receberá um erro como Olá a imagem a seguir:

![Erro de exclusão de cofre](./media/backup-azure-delete-vault/vault-deletion-error.png) <br/>

Até que você tenha desmarcado recursos de saudação do cofre hello, clicando em **novamente** produz Olá mesmo erro. Se você está parado nessa mensagem de erro, clique em **Cancelar** e recursos de saudação toodelete no cofre Olá as etapas a seguir do uso hello.

### <a name="removing-hello-items-from-a-vault-protecting-a-vm"></a>Removendo itens de saudação de um cofre protegendo uma máquina virtual
Se você já tiver Olá abrir cofre dos serviços de recuperação, ignore toohello segunda etapa.

1. Abra o hello portal do Azure e da saudação painel abra Olá cofre toodelete.

   Se você não tiver Olá Cofre de serviços de recuperação fixado toohello painel, no menu de Hub hello, clique em **mais serviços** e, na lista de saudação de recursos, digite **dos serviços de recuperação**. Como começar a digitar, Olá filtros de lista com base em sua entrada. Clique em **Cofres dos Serviços de Recuperação**.

   ![Criar Cofre de Serviços de Recuperação - etapa 1](./media/backup-azure-delete-vault/open-recovery-services-vault.png) <br/>

   saudação de lista de cofres de serviços de recuperação é exibida. Olá, selecione lista Olá cofre toodelete.

   ![escolher o cofre na lista](./media/backup-azure-work-with-vaults/choose-vault-to-delete.png)
2. Em Olá cofre exibição, procure em Olá **Essentials** painel. toodelete um cofre, não pode haver nenhum item protegido. Se você vir um número diferente de zero, em um **itens de Backup** ou **fazer Backup de servidores de gerenciamento**, você deve remover esses itens antes de excluir cofre hello.

    ![Procurar os itens protegidos no painel Essentials](./media/backup-azure-delete-vault/contoso-bkpvault-settings.png)

    Máquinas virtuais e arquivos/pastas são consideradas itens de Backup e são listadas na Olá **itens de Backup** área do painel do Essentials hello. Um servidor DPM está listado no hello **servidor de gerenciamento de Backup** área do painel do Essentials hello. **Replicadas itens** pertencem toohello serviço Azure Site Recovery.
3. toobegin removendo Olá itens protegidos do cofre hello, encontrar hello itens no cofre hello. No painel do cofre Olá clique **configurações**e, em seguida, clique em **fazer Backup de itens** tooopen folha.

    ![escolher o cofre na lista](./media/backup-azure-delete-vault/open-settings-and-backup-items.png)

    Olá **itens de Backup** folha tem listas separadas, com base em Olá tipo de Item: máquinas virtuais do Azure ou pastas de arquivos (consulte a imagem). lista de tipo de Item padrão Olá mostrada é máquinas virtuais do Azure. lista de saudação tooview de itens de pastas de arquivos em um cofre hello, selecione **pastas de arquivos** do menu suspenso de saudação.
4. Antes de excluir um item de compartimento Olá protegendo uma máquina virtual, você deve parar o trabalho de backup do item hello e excluir dados de ponto de recuperação de saudação. Para cada item no cofre hello, siga estas etapas:

    a. Em Olá **itens de Backup** folha, Olá com o botão direito item e, no menu de contexto hello, selecione **parar backup**.

    ![parar o trabalho de backup Olá](./media/backup-azure-delete-vault/stop-the-backup-process.png)

    Abre a folha de parar Backup Hello.

    b. Em Olá **parar Backup** folha da saudação **escolher uma opção** menu, selecione **excluir dados de Backup** > nome de saudação do tipo de item de saudação > e clique em **parar backup**.

    Nome de saudação do tipo do item de hello, tooverify deseja toodelete-lo. Olá **parar Backup** botão ativa depois que você verificar item hello. Se você não vir o nome da Olá Olá diálogo caixa tootype do item de backup Olá, você escolheu Olá **reter dados de Backup** opção.

    ![Excluir dados de backup](./media/backup-azure-delete-vault/stop-backup-blade-delete-backup-data.png)

    Opcionalmente, você pode fornecer um motivo por que você está excluindo dados saudação e adicione comentários. Depois de clicar em **parar Backup**, permitir Olá excluir trabalho toocomplete antes de tentar toodelete Cofre de saudação. tooverify que Olá trabalho foi concluída, verifique as mensagens de saudação do Azure ![excluir dados de backup](./media/backup-azure-delete-vault/messages.png). <br/>
    Após a conclusão do trabalho hello, você receberá uma mensagem informando o processo de backup Olá foi interrompido e dados de backup hello, para esse item foi excluídos.

    c. Depois de excluir um item na lista hello, Olá **itens de Backup** menu, clique em **atualizar** toosee Olá restantes itens no cofre hello.

      ![Excluir dados de backup](./media/backup-azure-delete-vault/empty-items-list.png)

      Quando não há nenhum item na lista de hello, role toohello **Essentials** painel na folha de Cofre de Backup hello. Não deve haver **Itens de Backup**, **Servidores de gerenciamento de backup** ou **Itens replicados** listados. Se itens ainda aparecem no cofre hello, retornar toostep três e escolha uma lista de tipo de item diferente.  
5. Quando não há nenhuma mais itens na barra de ferramentas do hello cofre, clique em **excluir**.

    ![Excluir dados de backup](./media/backup-azure-delete-vault/delete-vault.png)
6. Clique em tooverify que você deseja que o Cofre de saudação toodelete, **Sim**.

    Olá cofre será excluído e portal Olá retorna toohello **novo** menu de serviço.

## <a name="what-if-i-stopped-hello-backup-process-but-retained-hello-data"></a>E se eu interrompido o processo de backup Olá mas Olá dados retidos?
Se você interrompeu o processo de backup Olá mas acidentalmente *retidos* dados Olá, você deve excluir os dados de backup Olá antes de excluir cofre hello. dados de backup toodelete hello:

1. Em Olá **itens de Backup** folha, atalho Olá item e, no menu de contexto de saudação clique **excluir dados de backup**.

    ![Excluir dados de backup](./media/backup-azure-delete-vault/delete-backup-data-menu.png)

    Olá **excluir dados de Backup** folha é aberta.
2. Em Olá **excluir dados de Backup** folha, digite o nome de saudação do item de saudação e clique em **excluir**.

    ![Excluir dados de backup](./media/backup-azure-delete-vault/delete-retained-vault.png)

    Depois que você excluiu dados hello, retornar toostep 4c e continuar o processo de saudação.

## <a name="delete-a-vault-used-tooprotect-a-dpm-server"></a>Excluir um tooprotect cofre usado um servidor DPM
Antes de excluir um tooprotect cofre usado um servidor DPM, você deve limpar pontos de recuperação que foram criados e, em seguida, cancelar registro do servidor de saudação do cofre hello.

dados de saudação toodelete associados a um grupo de proteção:

1. No Console do administrador do DPM de Olá, clique em **proteção** > selecione um grupo de proteção > selecione Olá membro do grupo de proteção > e na faixa de opções de ferramenta hello, clique em **remover**.

  Selecione Olá Olá de tooactivate de membro do grupo de proteção **remover** botão na faixa de opções da ferramenta de saudação. Exemplo hello, membro de saudação é **dummyvm9**. tooselect vários membros no grupo de proteção hello, mantenha Olá tecla Ctrl pressionada enquanto clica em membros de saudação.

    ![Excluir dados de backup](./media/backup-azure-delete-vault/az-portal-delete-protection-group.png)

    Olá **parar proteção** caixa de diálogo é aberta.
2. Em Olá **parar proteção** caixa de diálogo, selecione **excluir dados protegidos**e clique em **parar proteção**.

    ![Excluir dados de backup](./media/backup-azure-delete-vault/delete-dpm-protection-group.png)

    toodelete um cofre, você deve limpar ou excluir, dados protegidos do Cofre de saudação do. Dependendo do número de saudação de pontos de recuperação e dados no grupo de proteção Olá, ele pode levar de dados de saudação do alguns segundos tooseveral minutos toodelete. Olá **parar proteção** caixa de diálogo mostra o status de saudação quando Olá trabalho foi concluído.

    ![Excluir dados de backup](./media/backup-azure-delete-vault/success-deleting-protection-group.png)
3. Prossiga nesse processo para todos os membros de todos os grupos de proteção.

    Remova todos os dados protegidos e grupos de proteção.
4. Depois de excluir todos os membros do grupo de proteção hello, alterne toohello portal do Azure. Abra o painel Cofre de saudação e verifique se há nenhum **itens de Backup**, **fazer Backup de servidores de gerenciamento**, ou **replicadas itens**. Na barra de ferramentas de cofre hello, clique em **excluir**.

    ![Excluir dados de backup](./media/backup-azure-delete-vault/delete-vault.png)

    Se não houver Backup gerenciamento servidores registrados toohello cofre, você não pode excluir o Cofre de saudação mesmo se não houver nenhum dado no cofre hello. Se excluir servidores de gerenciamento de Backup Olá associados Olá cofre, mas há servidores listados Olá **Essentials** painel, consulte [localizar Olá Backup gerenciamento servidores registrados toohello cofre](backup-azure-delete-vault.md#find-the-backup-management-servers-registered-to-the-vault) .
5. Clique em tooverify que você deseja que o Cofre de saudação toodelete, **Sim**.

    Olá cofre será excluído e portal Olá retorna toohello **novo** menu de serviço.

## <a name="delete-a-vault-used-tooprotect-a-production-server"></a>Excluir um tooprotect cofre usado um servidor de produção
Antes de excluir um tooprotect cofre usado um servidor de produção, você deve excluir ou cancelar registro do servidor de saudação do cofre hello.

servidor de produção de hello toodelete associado Olá cofre:

1. No hello portal do Azure, abra o painel Cofre de saudação e clique em **configurações** > **Backup infraestrutura** > **servidores de produção**.

    ![abrir a folha Servidores de Produção](./media/backup-azure-delete-vault/delete-production-server.png)

    Olá **servidores de produção** folha é aberta e lista todos os servidores de produção no cofre hello.

    ![lista de Servidores de Produção](./media/backup-azure-delete-vault/list-of-production-servers.png)
2. Em Olá **servidores de produção** folha, clique com botão direito no servidor de saudação e clique em **excluir**.

    ![excluir servidor de produção ](./media/backup-azure-delete-vault/delete-server-on-production-server-blade.png)

    Olá **excluir** folha é aberta.

    ![excluir servidor de produção ](./media/backup-azure-delete-vault/delete-blade.png)
3. Em Olá **excluir** folha, confirme o nome do servidor de saudação e clique em **excluir**. Você deve nomear corretamente server hello, Olá tooactivate **excluir** botão.

    Depois que o cofre Olá for excluído, você receberá uma mensagem informando cofre Olá foi excluído. Após a exclusão de todos os servidores no cofre hello, painel de Essentials toohello Voltar no painel do Cofre de saudação de rolagem.
4. No painel do cofre hello, verifique se há nenhum **itens de Backup**, **fazer Backup de servidores de gerenciamento**, ou **replicadas itens**. Na barra de ferramentas de cofre hello, clique em **excluir**.
5. Clique em tooverify que você deseja que o Cofre de saudação toodelete, **Sim**.

    Olá cofre será excluído e portal Olá retorna toohello **novo** menu de serviço.

## <a name="delete-a-backup-vault-in-classic-portal"></a>Excluir um cofre de backup no portal clássico
Olá instruções a seguir são para excluir um cofre de Backup no portal clássico do hello. Antes de excluir o Cofre de Backup Olá, você deve excluir os pontos de recuperação hello, ou backup de itens e remova os servidores de saudação registrado. Olá servidores registrados são saudação do Windows Server, estação de trabalho ou máquinas virtuais que foram registrados toohello cofre.

1. Olá abrir [portal clássico](https://manage.windowsazure.com).

2. Na lista de saudação de cofres de backup, selecione Olá cofre toodelete.

    ![Excluir dados de backup](./media/backup-azure-delete-vault/classic-portal-delete-vault-open-vault.png)

    painel do cofre Olá é aberto. Veja Olá número de máquinas virtuais de servidores do Windows e/ou do Azure associado Olá cofre. Além disso, examine o armazenamento total de saudação consumido no Azure. Interrompa todos os trabalhos de backup e excluir todos os dados antes de excluir cofre hello.

3. Clique em Olá **itens protegidos** guia e, em seguida, clique em **parar proteção**

    ![Excluir dados de backup](./media/backup-azure-delete-vault/classic-portal-delete-vault-stop-protect.png)

    Olá **interromper a proteção de 'o cofre'** caixa de diálogo é exibida.
4. Em Olá **interromper a proteção de 'o cofre'** caixa de diálogo, seleção **excluir os dados de backup associados** e clique em ![marca de seleção](./media/backup-azure-delete-vault/checkmark.png). <br/>
    Opcionalmente, você pode escolher um motivo para interromper a proteção e fornecer um comentário.

    ![Excluir dados de backup](./media/backup-azure-delete-vault/classic-portal-delete-vault-verify-stop-protect.png)

    Após a exclusão de itens de saudação no cofre hello, cofre Olá estará vazio.

    ![Excluir dados de backup](./media/backup-azure-delete-vault/classic-portal-delete-vault-post-delete-data.png)
5. Na lista de saudação de guias, clique em **itens registrados**. Olá **tipo** menu suspenso, permite que você toochoose Olá tipo de servidor registrado toohello cofre. tipo de saudação pode ser Windows Server ou a máquina Virtual do Azure. No hello exemplo a seguir, selecione Olá máquina virtual registrados toohello cofre e clique em **Unregister**.

    ![Excluir dados de backup](./media/backup-azure-delete-vault/classic-portal-unregister.png)

  Se você quiser toodelete registro de saudação para um servidor do Windows, da saudação **tipo** menu suspenso, selecione **Windows Server**, clique em ![marca de seleção](./media/backup-azure-delete-vault/checkmark.png) toorefresh tela de hello, e, em seguida, clique em **excluir**. <br/>

  ![selecionar o Windows Server](./media/backup-azure-delete-vault/select-windows-server.png)

6. Na lista de saudação de guias, clique em **painel** tooopen guia. Verifique se não existem servidores registrados ou máquinas virtuais do Azure protegidas na nuvem hello. Além disso, verifique se não há dados no armazenamento. Clique em **excluir** toodelete Cofre de saudação.

    ![Excluir dados de backup](./media/backup-azure-delete-vault/classic-portal-list-of-tabs-dashboard.png)

    Abre a tela de confirmação Hello Backup excluir cofre. Selecione uma opção de por que você está excluindo cofre hello e, em seguida, clique em ![marca de seleção](./media/backup-azure-delete-vault/checkmark.png). <br/>

    ![Excluir dados de backup](./media/backup-azure-delete-vault/classic-portal-delete-vault-confirmation-1.png)

    Olá cofre será excluído e retornar toohello painel do portal clássico.

### <a name="find-hello-backup-management-servers-registered-toohello-vault"></a>Localizar Olá Backup gerenciamento servidores registrados toohello cofre
Se você tiver vários compartimentos de tooa servidores registrados, pode ser difícil tooremembê-los. toosee Olá servidores registrados toohello cofre e excluí-los:

1. Painel do cofre Olá aberto.
2. Em Olá **Essentials** painel, clique em **configurações** tooopen folha.

    ![abrir folha de configurações](./media/backup-azure-delete-vault/backup-vault-click-settings.png)
3. Em Olá **folha configurações**, clique em **Backup infraestrutura**.
4. Em Olá **Backup infraestrutura** folha, clique em **servidores de gerenciamento de Backup**. Abre a folha de servidores de gerenciamento de Backup Hello.

    ![lista de servidores de gerenciamento de backup](./media/backup-azure-delete-vault/list-of-backup-management-servers.png)
5. toodelete um servidor na lista de saudação, clique no nome de saudação do servidor de saudação e clique **excluir**.
    Olá **excluir** folha é aberta.
6. Em Olá **excluir** folha, forneça o nome de saudação do servidor de saudação. Se for um nome longo, copie e cole-o na lista de saudação dos servidores de gerenciamento de Backup. Em seguida, clique em **Excluir**.  
