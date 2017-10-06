---
title: aaaUse tooback de servidor de Backup do Azure a um tooAzure de farm do SharePoint | Microsoft Docs
description: "Usar o Azure Backup Server tooback e restaurar os dados do SharePoint. Este artigo fornece Olá informações tooconfigure seu farm do SharePoint para que os dados desejados podem ser armazenados no Azure. Você pode restaurar dados protegidos do SharePoint do disco ou do Azure."
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: 34ba87a4-91f1-4054-a4a1-272af1e15496
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: 350c1ac0f3518f400062f3b586bbe9710a79915a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-sharepoint-farm-tooazure"></a>Fazer backup de um tooAzure de farm do SharePoint
Fazer backup do SharePoint farm tooMicrosoft do Azure usando o Microsoft Azure Backup Server (MABS) em quantidade Olá mesma maneira que você faz backup de outras fontes de dados. O Backup do Azure oferece a flexibilidade de saudação agendamento de backup toocreate pontos de backup diários, semanais, mensais ou anuais e fornece opções de política de retenção para vários pontos de backup. Ele também fornece Olá recurso toostore disco local cópias para rápido objetivos de tempo de recuperação (RTO) e toostore copia tooAzure para retenção econômica de longo prazo.

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a>Versões do SharePoint com suporte e cenários de proteção relacionados
Backup do Azure para o DPM oferece suporte a saudação os seguintes cenários:

| Carga de trabalho | Versão | Implantação do SharePoint | Proteção e recuperação |
| --- | --- | --- | --- | --- | --- |
| SharePoint |SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0 |SharePoint implantado como um servidor físico ou em uma máquina virtual Hyper-V/VMware  <br> -------------- <br> AlwaysOn do SQL | Opções recuperação para proteger o Farm do SharePoint: farm de recuperação, banco de dados e um arquivo ou item de lista dos pontos de recuperação de disco.  Recuperação do farm e do banco de dados dos pontos de recuperação do Azure. |

## <a name="before-you-start"></a>Antes de começar
Há algumas coisas que você precisa tooconfirm antes de você fazer backup de um tooAzure de farm do SharePoint.

### <a name="prerequisites"></a>Pré-requisitos
Antes de prosseguir, certifique-se de que você tenha [instalado e preparado hello Azure Backup Server](backup-azure-microsoft-azure-backup.md) tooprotect cargas de trabalho.

### <a name="protection-agent"></a>Agente de proteção
Agente de proteção de saudação deve ser instalado no servidor de saudação que está executando o SharePoint, servidores de saudação que executam o SQL Server e todos os outros servidores que fazem parte do farm do SharePoint de saudação. Para obter mais informações sobre como tooset o agente de proteção de hello, consulte [agente de proteção de instalação](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).  Olá uma exceção é que você instale o agente de saudação apenas em um único front-end (WFE) servidor web. Como ponto de entrada hello para proteção, o DPM precisa agente Olá em um WFE tooserve de somente de servidor.

### <a name="sharepoint-farm"></a>Farm do SharePoint
Para cada 10 milhões de itens no farm hello, deve haver pelo menos 2 GB de espaço no volume de saudação onde Olá MABS pasta está localizada. Esse espaço é necessário para a geração de catálogo. Para MABS toorecover itens específicos (coleções de sites, sites, listas, bibliotecas de documentos, pastas, documentos individuais e itens de lista), a geração de catálogo cria uma lista de URLs Olá contidos em cada banco de dados de conteúdo. Você pode exibir a lista de saudação de URLs no painel item recuperável Olá Olá **recuperação** área do Console do administrador do MABS de tarefa.

### <a name="sql-server"></a>SQL Server
O MABS é executado como uma conta LocalSystem. tooback backup de bancos de dados do SQL Server, MABS precisa de privilégios de sysadmin nessa conta para o servidor de saudação que está executando o SQL Server. Definir Autoridade NT\Sistema muito*sysadmin* no servidor de saudação que está executando o SQL Server antes de fazer seu backup.

Se o farm do SharePoint Olá tiver bancos de dados do SQL Server que estão configurados com aliases do SQL Server, instale componentes de cliente do SQL Server Olá no servidor Web front-end Olá que MABS irá proteger.

### <a name="sharepoint-server"></a>SharePoint Server
Embora o desempenho dependa de muitos fatores tais como o tamanho do farm do SharePoint, as diretrizes gerais são de que um MABS pode ser usado para proteger um farm do SharePoint de 25 TB.

### <a name="whats-not-supported"></a>O que não tem suporte
* O MABS que protege um farm do SharePoint não protege os índices de pesquisa ou os bancos de dados do serviço de aplicativo. Você precisará tooconfigure proteção de saudação desses bancos de dados separadamente.
* O MABS não fornece backup dos bancos de dados do SQL Server do SharePoint hospedados em compartilhamento SOFS (Servidor de Arquivos de Escalabilidade Horizontal).

## <a name="configure-sharepoint-protection"></a>Configurar a proteção do SharePoint
Antes de usar MABS tooprotect do SharePoint, você deve configurar o serviço de gravador VSS do SharePoint de saudação (serviço de gravador WSS) usando **ConfigureSharePoint.exe**.

Você pode encontrar **ConfigureSharePoint.exe** na pasta \bin de saudação [caminho de instalação MABS] no servidor web front-end de saudação. Essa ferramenta fornece um agente de proteção de saudação com credenciais Olá Olá farm do SharePoint. Você a executa em um único servidor WFE. Se você tiver vários servidores WFE, selecione apenas um ao configurar um grupo de proteção.

### <a name="tooconfigure-hello-sharepoint-vss-writer-service"></a>Olá tooconfigure serviço de gravador VSS do SharePoint
1. No servidor WFE hello, em um prompt de comando, vá muito \bin\ [local da instalação MABS]
2. Insira ConfigureSharePoint -EnableSharePointProtection.
3. Insira as credenciais de administrador de farm hello. Essa conta deve ser um membro do grupo de administradores local Olá no servidor WFE hello. Se o administrador de farm Olá não é uma saudação de concessão de administrador local as seguintes permissões no servidor WFE hello:
   * Grant Olá WSS_Admin_WPG controle total toohello DPM pasta grupo (% programa Files%\Microsoft Azure Backup\DPM).
   * Grant Olá WSS_Admin_WPG grupo acesso de leitura toohello DPM chave do registro (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).

> [!NOTE]
> Você precisará toorerun ConfigureSharePoint.exe sempre que houver uma alteração nas credenciais de administrador de farm do SharePoint hello.
>
>

## <a name="back-up-a-sharepoint-farm-by-using-mabs"></a>Fazer backup de um farm do SharePoint usando o MABS
Depois que você configurou MABS e hello farm do SharePoint, conforme explicado anteriormente, o SharePoint pode ser protegido por MABS.

### <a name="tooprotect-a-sharepoint-farm"></a>tooprotect um farm do SharePoint
1. De saudação **proteção** guia da saudação MABS Administrator Console, clique em **novo**.
    ![Guia Nova Proteção](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)
2. Em Olá **Selecionar tipo de grupo de proteção** página de saudação **criar novo grupo de proteção** assistente, selecione **servidores**e, em seguida, clique em **próximo** .

    ![Selecionar o tipo de Grupo de Proteção](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. Em Olá **selecionar membros do grupo** tela, caixa de seleção select Olá Olá SharePoint server que deseja tooprotect e clique **próximo**.

    ![Selecionar membros do grupo](./media/backup-azure-backup-sharepoint/select-group-members2.png)

   > [!NOTE]
   > Com o agente de proteção Olá instalado, você pode ver servidor Olá no Assistente de saudação. O MABS também mostra sua estrutura. Porque você executou o ConfigureSharePoint.exe, MABS se comunica com o serviço de gravador VSS do SharePoint hello e seus bancos de dados do SQL Server correspondentes e reconhece a estrutura do farm do SharePoint hello, Olá associado bancos de dados de conteúdo e todos os itens correspondentes.
   >
   >
4. Em Olá **Selecionar método de proteção de dados** Insira nome de saudação do hello **grupo de proteção**e selecione sua preferência *métodos de proteção*. Clique em **Avançar**.

    ![Selecionar método de proteção de dados](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)

   > [!NOTE]
   > método de proteção de disco Hello ajuda toomeet curto objetivos de tempo de recuperação.
   >
   >
5. Em Olá **especificar objetivos de curto prazo** , selecione sua preferência **período de retenção** e identificar quando desejar toooccur backups.

    ![Especificar objetivos de curto prazo](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)

   > [!NOTE]
   > Como a recuperação geralmente é necessária para dados que são menos de cinco dias, é selecionado um período de retenção de cinco dias no disco e garante que o backup Olá acontece durante o horário não seja de produção, para este exemplo.
   >
   >
6. Examine Olá espaço pool de armazenamento em disco alocado para o grupo de proteção Olá e então clique **próximo**.
7. Para cada grupo de proteção, MABS aloca toostore de espaço em disco e gerenciar réplicas. Neste ponto, MABS deve criar uma cópia dos dados de saudação selecionado. Selecione como e quando você deseja réplica Olá criada e, em seguida, clique em **próximo**.

    ![Escolher método de criação de réplica](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)

   > [!NOTE]
   > toomake-se de que o tráfego de rede não é afetado, selecione uma hora fora do horário de produção.
   >
   >
8. MABS garante a integridade de dados executando verificações de consistência na réplica de saudação. Há duas opções disponíveis. Você pode definir as verificações de consistência de toorun uma agenda ou o DPM pode executar verificações de consistência automaticamente na réplica de saudação sempre que se torna inconsistente. Selecione sua opção desejada e clique em **Avançar**.

    ![Verificação de consistência](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. Em Olá **especificar dados de proteção Online** , selecione o farm do SharePoint de saudação que você deseja tooprotect e, em seguida, clique em **próximo**.

    ![Proteção do SharePoint do DPM1](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. Em Olá **especificar agendamento de Backup Online** página, selecione a agenda desejada e, em seguida, clique em **próximo**.

    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)

    > [!NOTE]
    > MABS fornece um máximo de dois tooAzure backups diários da saudação ponto backup de disco mais recente disponível. O Backup do Azure também pode controlar a quantidade de saudação de largura de banda WAN que pode ser usada para backups em horário de pico e fora de pico usando [limitação de rede de Backup do Azure](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).
    >
    >
11. Dependendo do agendamento de backup Olá que você selecionou no hello **especificar política de retenção Online** página política de retenção de saudação select para pontos de backup diárias, semanais, mensais e anuais.

    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)

    > [!NOTE]
    > O MABS usa um esquema de retenção de avô-pai-filho em que uma política de retenção diferente pode ser escolhida para pontos de backup distintos.
    >
    >
12. Toodisk semelhante, uma réplica de ponto inicial de referência deve toobe criado no Azure. Selecione sua opção preferida de toocreate tooAzure uma cópia de backup inicial e, em seguida, clique em **próximo**.

    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. Examine as configurações selecionadas no hello **resumo** página e, em seguida, clique em **criar grupo**. Você verá uma mensagem de êxito após a criação do grupo de proteção de saudação.

    ![Resumo](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-mabs"></a>Restaurar um item do SharePoint do disco usando o MABS
Em Olá exemplo a seguir, Olá *item do SharePoint recuperando* tenha sido excluído acidentalmente e precisa toobe recuperado.
![Proteção do SharePoint do MABS 4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)

1. Olá abrir **Console do administrador do DPM**. Todos os farms do SharePoint que são protegidos pelo DPM são mostrados no hello **proteção** guia.

    ![Proteção do SharePoint do MABS 3](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. item de saudação toorecover toobegin, selecione Olá **recuperação** guia.

    ![Proteção do SharePoint do MABS 5](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. É possível pesquisar no SharePoint para localizar o *item Recuperando SharePoint* usando uma pesquisa baseada em curinga dentro de um intervalo de ponto de recuperação.

    ![Proteção do SharePoint do MABS 6](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. Selecione o ponto de recuperação apropriado de Olá Olá dos resultados da pesquisa, item hello e, em seguida, selecione **recuperar**.
5. Você também pode navegar pelos vários pontos de recuperação e selecione toorecover um banco de dados ou item. Selecione **data > tempo de recuperação**e, em seguida, selecione Olá correto **banco de dados > farm do SharePoint > ponto de recuperação > Item**.

    ![Proteção do SharePoint do MABS 7](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. Item de saudação e, em seguida, selecione **recuperar** tooopen Olá **Assistente de recuperação**. Clique em **Avançar**.

    ![Rever Seleção de Recuperação](./media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. Selecionar tipo de saudação de recuperação que você deseja tooperform e, em seguida, clique em **próximo**.

    ![Tipo de Recuperação](./media/backup-azure-backup-sharepoint/select-recovery-type.png)

   > [!NOTE]
   > Olá seleção de **recuperar toooriginal** em Olá exemplo recupera o site do SharePoint para original do hello item toohello.
   >
   >
8. Selecione Olá **processo de recuperação** que você deseja toouse.

   * Selecione **recuperar sem usar um farm de recuperação** se o farm do SharePoint de saudação não foi alterado e hello, mesmo que a recuperação de saudação do ponto que é está sendo restaurado.
   * Selecione **recuperar usando um farm de recuperação** se o farm do SharePoint Olá foi alterado desde que o ponto de recuperação Olá foi criado.

     ![Processo de Recuperação](./media/backup-azure-backup-sharepoint/recovery-process.png)
9. Forneça um preparação do SQL Server instância local toorecover Olá banco de dados temporariamente e fornecer um compartilhamento de arquivo temporário em MABS e Olá no servidor que está executando o item do SharePoint toorecover hello.

    ![Local de Preparo1](./media/backup-azure-backup-sharepoint/staging-location1.png)

    MABS anexa Olá conteúdo banco de dados que está hospedando o hello SharePoint item toohello temporária instância do SQL Server. Do banco de dados de conteúdo hello, ele recupera o item de saudação e a coloca na Olá local do arquivo em MABS de preparo. Olá recuperado item que está em Olá local de preparo agora necessidades toobe exportado toohello local no farm do SharePoint de saudação de preparo.

    ![Local de Preparo2](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. Selecione **especificar opções de recuperação**e aplicar configurações de segurança toohello farm do SharePoint ou aplicar configurações de segurança Olá Olá do ponto de recuperação. Clique em **Avançar**.

    ![Opções de Recuperação](./media/backup-azure-backup-sharepoint/recovery-options.png)

    > [!NOTE]
    > Você pode escolher o uso de largura de banda de rede toothrottle hello. Isso minimiza o servidor de produção do impacto toohello durante o horário de produção.
    >
    >
11. Examine as informações de resumo hello e, em seguida, clique em **recuperar** toobegin recuperação de arquivo hello.

    ![Resumo da recuperação](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. Agora selecione Olá **monitoramento** guia Olá **Console do administrador do MABS** tooview Olá **Status** de recuperação de saudação.

    ![Status da Recuperação](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)

    > [!NOTE]
    > arquivo Hello agora é restaurado. Você pode atualizar o arquivo do hello SharePoint site toocheck Olá restaurado.
    >
    >

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a>Restaurar um banco de dados do SharePoint do Azure usando o DPM
1. toorecover banco de dados de conteúdo um SharePoint, navegue pelos vários pontos de recuperação (conforme mostrado anteriormente) e selecione Olá ponto de recuperação que você deseja toorestore.

    ![Proteção do SharePoint do MABS 8](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. Clique duas vezes em Olá SharePoint recuperação tooshow ponto Olá disponíveis do SharePoint informações do catálogo.

   > [!NOTE]
   > Porque o farm do SharePoint hello está protegido para retenção de longo prazo no Azure, não há informações de catálogo (metadados) estão disponíveis em MABS. Como resultado, sempre que um banco de dados point-in-time do SharePoint conteúdo precisa toobe recuperado, você precisa farm do SharePoint Olá toocatalog novamente.
   >
   >
3. Clique em **Recatalogar**.

    ![Proteção do SharePoint do MABS 10](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)

    Olá **nuvem recatalogar** status janela será aberta.

    ![Proteção do SharePoint do MABS 11](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)

    Depois de catalogação for concluída, o status de Olá muda muito*sucesso*. Clique em **fechar**

    ![Proteção do SharePoint do MABS 12](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. Clique Olá SharePoint objeto mostrado no hello MABS **recuperação** guia estrutura de banco de dados de conteúdo de saudação do tooget. Clique no item Olá e clique **recuperar**.

    ![Proteção do SharePoint do MABS 13](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. Neste ponto, execute Olá [recuperação as etapas neste artigo](#restore-a-sharepoint-item-from-disk-using-dpm) toorecover um banco de dados de conteúdo no SharePoint do disco.

## <a name="faqs"></a>Perguntas frequentes
P: recuperar o local original do item toohello um SharePoint se o SharePoint é configurado usando o AlwaysOn do SQL (com proteção em disco)?<br>
R: Sim, o item de saudação pode ser recuperado toohello original do SharePoint site.

P: é possível recuperar o local original do banco de dados toohello um SharePoint se o SharePoint é configurado usando o AlwaysOn do SQL?<br>
R: como bancos de dados do SharePoint são configurados no SQL AlwaysOn, não pode ser modificados, a menos que o grupo de disponibilidade de saudação é removido. Como resultado, MABS não é possível restaurar um local original do banco de dados toohello. Você pode recuperar uma instância de SQL Server do tooanother de banco de dados do SQL Server.

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre a Proteção do MABS do SharePoint: veja a [Série de vídeos – Proteção do DPM do SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)
