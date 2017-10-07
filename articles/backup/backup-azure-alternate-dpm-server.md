---
title: aaaRecover dados de um servidor de Backup do Azure | Microsoft Docs
description: "Recuperar dados Olá você protegeu Cofre de serviços de recuperação de tooa do Cofre de toothat registrado qualquer servidor de Backup do Azure."
services: backup
documentationcenter: 
author: nkolli1
manager: shreeshd
editor: 
ms.assetid: a55f8c6b-3627-42e1-9d25-ed3e4ab17b1f
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: adigan;giridham;trinadhk;markgal
ms.openlocfilehash: 74847880e646c3c4f198afe318f1db30363d137a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="recover-data-from-azure-backup-server"></a>Recuperar dados do Servidor de Backup do Azure
Você pode usar dados de saudação do servidor de Backup do Azure toorecover que tiver feito backup tooa que Cofre de serviços de recuperação. processo de saudação para fazer assim é integrado ao console de gerenciamento do Azure Backup Server hello e é semelhante toohello recuperação fluxo de trabalho para outros componentes de Backup do Azure.

> [!NOTE]
> Este artigo se aplica a [System Center Data Protection Manager 2012 R2 com UR7 ou posterior] (https://support.microsoft.com/en-us/kb/3065246), combinada com hello [agente mais recente do Backup do Azure](http://aka.ms/azurebackup_agent).
>
>

toorecover dados de um servidor de Backup do Azure:

1. De saudação **recuperação** guia da saudação console de gerenciamento do servidor de Backup do Azure, clique em **'Adicionar DPM externo'** (no hello superior esquerda da tela hello).   
    ![Adicionar DPM externo](./media/backup-azure-alternate-dpm-server/add-external-dpm.png)
2. Download novo **credenciais de cofre** do cofre Olá associado Olá **Azure Backup Server** onde dados hello está sendo recuperados, escolha hello Azure Backup Server Olá lista de servidores de Backup do Azure registrado no cofre de serviços de recuperação de saudação e fornecer Olá **senha de criptografia** associada ao servidor de saudação cujos dados estão sendo recuperados.

    ![Credenciais do DPM externo](./media/backup-azure-alternate-dpm-server/external-dpm-credentials.png)

   > [!NOTE]
   > Somente servidores de Backup do Azure associado Olá mesmo Cofre de registro pode recuperar dados.
   >
   >

    Após hello Azure Backup Server externo com êxito adicionado, você pode procurar dados de saudação do servidor externo hello e hello Azure Backup Server local da saudação **recuperação** guia.
3. Olá disponível lista de servidores de produção protegidos pelo hello Azure Backup Server externo e selecionar fonte de dados apropriada hello.

    ![Procurar o servidor DPM externo](./media/backup-azure-alternate-dpm-server/browse-external-dpm.png)
4. Selecione **Olá mês e ano** de saudação **pontos de recuperação** lista suspensa, selecione Olá necessário **data recuperação** para quando o ponto de recuperação Olá foi Olá criado e selecione **Tempo de recuperação**.

    É exibida uma lista de arquivos e pastas no painel inferior hello, o que pode ser pesquisado e recuperado tooany local.

    ![Pontos de recuperação de servidor DPM externo](./media/backup-azure-alternate-dpm-server/external-dpm-recoverypoint.png)
5. Clique com botão direito item apropriado hello e clique em **recuperar**.

    ![Recuperação do DPM externo](./media/backup-azure-alternate-dpm-server/recover.png)
6. Saudação de revisão **recuperar seleção**. Verificar dados saudação e tempo de cópia de backup hello está sendo recuperado, bem como origem de saudação do qual a cópia de backup Olá foi criada. Se a seleção Olá estiver incorreta, clique em **Cancelar** ponto de recuperação apropriado toonavigate back toorecovery guia tooselect. Se a seleção de saudação estiver correta, clique em **próximo**.

    ![Resumo de recuperação do DPM externo](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-summary.png)
7. Selecione **recuperar o local alternativo tooan**. **Procurar** toohello o local correto para a recuperação de saudação.

    ![Local alternativo de recuperação do DPM externo](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-alternate-location.png)
8. Escolha opção Olá relacionada muito**criar cópia**, **ignorar**, ou **substituir**.

   * **Criar cópia** -cria uma cópia do arquivo hello, se houver uma colisão de nomes.
   * **Ignorar** - se não houver uma colisão de nomes, não se recupera arquivo hello que deixa o arquivo original hello.
   * **Substituir** - se não houver uma colisão de nomes, substituirá a cópia existente de saudação do arquivo hello.

     Escolha a opção apropriada Olá muito**restaurar segurança**. Você pode aplicar configurações de segurança Olá Olá do computador de destino onde os dados hello está sendo recuperados ou configurações de segurança de saudação que estavam tooproduct aplicável ao tempo Olá Olá ponto de recuperação foi criado.

     Identificar se um **notificação** é enviado, após a conclusão bem-sucedida da recuperação de saudação.

     ![Notificações de recuperação do DPM externo](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-notifications.png)
9. Olá **resumo** tela lista opções Olá escolhidas até o momento. Depois de clicar em **'Recuperar'**, dados de saudação são recuperado toohello apropriado no local.

    ![Resumo de opções de recuperação do DPM externo](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-options-summary.png)

   > [!NOTE]
   > trabalho de recuperação de saudação pode ser monitorado no hello **monitoramento** guia de hello Azure Backup Server.
   >
   >

    ![Recuperação de monitoramento](./media/backup-azure-alternate-dpm-server/monitoring-recovery.png)
10. Você pode clicar em **limpar DPM externo** em Olá **recuperação** guia de modo de exibição do DPM server tooremove saudação do servidor DPM externo de saudação do hello.

    ![Limpar o DPM externo](./media/backup-azure-alternate-dpm-server/clear-external-dpm.png)

## <a name="troubleshooting-error-messages"></a>Solucionando problemas de mensagens de erro
| Nº | Mensagem de erro | Etapas para solucionar problemas |
|:---:|:--- |:--- |
| 1. |Este servidor não está registrado toohello cofre especificado pela credencial do cofre hello. |**Causa:** esse erro aparece quando o arquivo de credencial de cofre Olá selecionado não pertence toohello Cofre de serviços de recuperação associados com o servidor de Backup do Azure no qual Olá uma tentativa de recuperação. <br> **Resolução:** arquivo de credencial de cofre Download Olá de Olá dos serviços de recuperação cofre toowhich Olá Azure Backup Server está registrado. |
| 2. |O dados recuperáveis Olá não estão disponíveis ou o servidor de saudação selecionado não é um servidor DPM. |**Causa:** sem outros servidores de Backup do Azure toohello registrado recuperação Cofre de serviços, não há servidores Olá ainda não tiveram carregado Olá metadados ou servidor de saudação selecionado não é um servidor de Backup do Azure (também conhecido como Windows Server ou Windows Client). <br> **Resolução:** se houver outro Cofre de serviços de recuperação de toohello registrados servidores de Backup do Azure, certifique-se de que hello mais recente do Azure Backup agent está instalado. <br>Se houver outro Cofre de serviços de recuperação de toohello registrados servidores de Backup do Azure, aguarde um dia após o processo de recuperação de saudação de toostart de instalação. tarefa noturna Olá carregará Olá metadados para todos os toocloud de backups Olá protegido. dados de saudação estarão disponíveis para recuperação. |
| 3. |Nenhum outro servidor DPM é registrado toothis cofre. |**Causa:** não há nenhum outro servidor de Backup do Azure que são registrados toohello cofre do qual Olá recuperação está sendo tentada.<br>**Resolução:** se houver outro Cofre de serviços de recuperação de toohello registrados servidores de Backup do Azure, certifique-se de que hello mais recente do Azure Backup agent está instalado.<br>Se houver outro Cofre de serviços de recuperação de toohello registrados servidores de Backup do Azure, aguarde um dia após o processo de recuperação de saudação de toostart de instalação. tarefa noturna Olá carrega metadados Olá toocloud de todos os backups protegido. dados de saudação estarão disponíveis para recuperação. |
| 4. |Olá senha de criptografia fornecida não corresponde à senha associada à saudação servidor a seguir:**<server name>** |**Causa:** Olá senha de criptografia usada no processo de saudação de criptografar dados de saudação do servidor de saudação do Azure Backup dados de que está sendo recuperados não coincide com senha de criptografia Olá fornecida. Agente de saudação é dados de saudação toodecrypt não é possível. Olá, portanto, a recuperação falhará.<br>**Resolução:** forneça Olá exata mesma senha de criptografia associada hello Azure Backup Server cujos dados estão sendo recuperados. |

## <a name="frequently-asked-questions"></a>Perguntas frequentes

### <a name="why-cant-i-add-an-external-dpm-server-after-installing-ur7-and-latest-azure-backup-agent"></a>Por que não consigo adicionar um servidor DPM externo após instalar o UR7 e o agente de Backup do Azure mais recente?

Para hello servidores DPM com fontes de dados que são protegidos toohello nuvem (por meio de um pacote cumulativo de atualizações anteriores ao atualizar o pacote cumulativo de atualizações 7), você deve esperar pelo menos um dia após a instalação Olá UR7 e agente de Backup do Azure mais recente, toostart **server adicionar DPM externo** . Olá um dia o período de tempo é necessário tooupload Olá metadados de saudação tooAzure de grupos de proteção de DPM. Metadados do grupo de proteção é carregado Olá primeira vez por meio de um trabalho noturno.

### <a name="what-is-hello-minimum-version-of-hello-microsoft-azure-recovery-services-agent-needed"></a>O que é a versão mínima de saudação do agente de serviços de recuperação do Microsoft Azure Olá necessário?

versão mínima de saudação do agente de serviços de recuperação do Microsoft Azure hello ou agente de Backup do Azure, necessária tooenable esse recurso é 2.0.8719.0.  versão do agente de saudação tooview: Abra o painel de controle  **>**  itens do painel de controle de todos os  **>**  programas e recursos  **>**  Agente de serviços de recuperação do Microsoft Azure. Se a versão Olá é menor que 2.0.8719.0, baixe e instale Olá [agente mais recente do Backup do Azure](https://go.microsoft.com/fwLink/?LinkID=288905).

![Limpar o DPM externo](./media/backup-azure-alternate-dpm-server/external-dpm-azurebackupagentversion.png)

## <a name="next-steps"></a>Próximas etapas:
•    [Perguntas frequentes sobre o Backup do Azure](backup-azure-backup-faq.md)
