---
title: aaaAzure Backup para cargas de trabalho do SQL Server usando o DPM | Microsoft Docs
description: "Toobacking uma introdução a bancos de dados do SQL Server usando o serviço de Backup do Azure Olá"
services: backup
documentationcenter: 
author: adigan
manager: Nkolli
editor: 
ms.assetid: 59df5bec-d959-457d-8731-7b20f7f1013e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adigan;giridham;jimpark;markgal;trinadhk
ms.openlocfilehash: ba78dbf1c7934a259a7bd0bdb7d4467ac75d05a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-sql-server-tooazure-as-a-dpm-workload"></a>Faça backup do SQL Server tooAzure como uma carga de trabalho do DPM
Este artigo o guiará pelas etapas de configuração de saudação para backup de bancos de dados do SQL Server usando o Backup do Azure.

tooback backup tooAzure de bancos de dados do SQL Server, você precisa de uma conta do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).

gerenciamento de saudação de tooAzure de backup de banco de dados do SQL Server e a recuperação do Azure envolve três etapas:

1. Crie um tooAzure de bancos de dados do SQL Server de tooprotect política de backup.
2. Crie cópias de backup sob demanda tooAzure.
3. Recupere o banco de dados de saudação do Azure.

## <a name="before-you-start"></a>Antes de começar
Antes de começar, certifique-se de que todos os Olá [pré-requisitos](backup-azure-dpm-introduction.md#prerequisites) para usar o Microsoft Azure Backup tooprotect cargas de trabalho foram atendidas. pré-requisitos de saudação abrangem tarefas como: criar um cofre de backup, baixando as credenciais do cofre, instalando hello Azure Backup Agent e registrar servidor Olá cofre hello.

## <a name="create-a-backup-policy-tooprotect-sql-server-databases-tooazure"></a>Criar um tooAzure de bancos de dados do SQL Server de tooprotect política de backup
1. No servidor DPM hello, clique em Olá **proteção** espaço de trabalho.
2. Na faixa de opções de ferramenta hello, clique em **novo** toocreate um novo grupo de proteção.

    ![Criar grupo de proteção](./media/backup-azure-backup-sql/protection-group.png)
3. DPM mostra a tela de início de saudação com diretrizes Olá sobre a criação de um **grupo de proteção**. Clique em **Avançar**.
4. Selecione **Servidores**.

    ![Selecionar o tipo de Grupo de Proteção - ‘Servidores’](./media/backup-azure-backup-sql/pg-servers.png)
5. Expanda máquina do SQL Server Olá onde Olá bancos de dados toobe backup estiverem presentes. O DPM mostra várias fontes de dados cujo backup pode vir desse servidor. Expanda Olá **todos os compartilhamentos de SQL** e selecione os bancos de dados de saudação (nesse caso selecionamos ReportServer$ MSDPM2012 e ReportServer$ MSDPM2012TempDB) toobe backup. Clique em **Avançar**.

    ![Selecione o banco de dados SQL](./media/backup-azure-backup-sql/pg-databases.png)
6. Forneça um nome para o grupo de proteção hello e selecione Olá **desejo proteção online** caixa de seleção.

    ![Método de proteção de dados: disco de curto prazo e Azure Online](./media/backup-azure-backup-sql/pg-name.png)
7. Em Olá **especificar objetivos de curto prazo** tela, incluir Olá entradas necessárias toocreate pontos backup toodisk.

    Vemos aqui que **período de retenção** está definido muito*5 dias*, **frequência de sincronização** está definida tooonce cada *15 minutos* que é Olá frequência em que o backup é realizado. **Backup completo expresso** está definido muito*8:00 PM*.

    ![Objetivos de curto prazo](./media/backup-azure-backup-sql/pg-shortterm.png)

   > [!NOTE]
   > Às 8:00 (de acordo com entrada de tela de toohello) um ponto de backup é criado diariamente transferindo dados Olá que tem sido modificados de saudação ponto de backup do dia anterior 8:00 PM. Esse processo é chamado de **Backup Completo Expresso**. Olá logs de transação são sincronizadas a cada 15 minutos, se houver um banco de dados necessário toorecover Olá às 9:00 – ponto Olá será criado repetindo logs de saudação do hello express último ponto de backup completo (8 pm neste caso).
   >
   >

8. Clique em **Avançar**

    O DPM mostra Olá geral espaço de armazenamento disponível e a utilização de espaço em disco potencial hello.

    ![Alocação de disco](./media/backup-azure-backup-sql/pg-storage.png)

    Por padrão, o DPM cria um volume de fonte de dados (banco de dados do SQL Server) que é usado para cópia de backup inicial hello. Usando essa abordagem, Olá Gerenciador de discos lógicos (LDM) limita a fontes de dados do DPM protection too300 (bancos de dados do SQL Server). toowork com essa limitação, selecione Olá **colocalizar dados no Pool de armazenamento do DPM**, opção. Se você usar essa opção, o DPM usa um único volume de várias fontes de dados, que permite que o DPM tooprotect backup too2000 bancos de dados SQL.

    Se **aumentar os volumes Olá automaticamente** opção é selecionada, o DPM pode considerar Olá maior volume de backup que os dados de produção de hello crescem. Se **aumentar os volumes Olá automaticamente** opção não estiver selecionada, o DPM limita Olá armazenamento de backup usado toohello fontes de dados no grupo de proteção de saudação.
9. Os administradores são terá a opção de saudação de transferência esse congestionamento de largura de banda inicial tooavoid backup manualmente (fora de rede) ou pela rede hello. Ele também poderá configurar o tempo de saudação no qual saudação inicial transferência pode ocorrer. Clique em **Avançar**.

    ![Método de replicação inicial](./media/backup-azure-backup-sql/pg-manual.png)

    a cópia de backup inicial Olá requer transferência Olá inteira da fonte de dados (banco de dados do SQL Server) do servidor DPM produção server (máquina do SQL Server) toohello. Esses dados podem ser grandes e transferir dados de saudação pela rede Olá poderá exceder a largura de banda. Por esse motivo, os administradores podem escolher o backup inicial do tootransfer Olá: **manualmente** (usando mídia removível) tooavoid congestionamento de largura de banda, ou **automaticamente pela rede Olá** (em determinado tempo).

    Após a conclusão do backup inicial Olá, rest Olá de backups de saudação são backups incrementais na cópia de backup inicial hello. Os backups incrementais tendem toobe pequeno e facilmente são transferidos pela rede de saudação.
10. Escolha quando você quiser Olá toorun de verificação de consistência e clique em **próximo**.

    ![Verificação de consistência](./media/backup-azure-backup-sql/pg-consistent.png)

    O DPM pode executar uma integridade de saudação consistência seleção toocheck saudação do ponto de backup. Ela calcula a soma de verificação Olá Olá do arquivo de backup no servidor de produção de hello (máquina do SQL Server neste cenário) e dados de backup de saudação do arquivo no DPM. No caso de saudação de um conflito, presume-se que Olá arquivo de backup no DPM está corrompido. O DPM rectifies dados de backup Olá enviando blocos Olá correspondente toohello incompatibilidade de soma de verificação. Como a verificação de consistência de saudação é uma operação de alto desempenho, os administradores têm a opção de saudação do agendamento de verificação de consistência de saudação ou executá-lo automaticamente.
11. toospecify proteção online de saudação de fontes de dados, selecione Olá toobe de bancos de dados protegidos tooAzure e clique em **próximo**.

    ![Selecionar fontes de dados](./media/backup-azure-backup-sql/pg-sqldatabases.png)
12. Os administradores podem escolher agendamentos de backup e políticas de retenção que atendam às políticas da organização.

    ![Agendamento e retenção](./media/backup-azure-backup-sql/pg-schedule.png)

    Neste exemplo, os backups são realizados uma vez por dia às 12h e 8 PM (parte inferior da tela hello)

    > [!NOTE]
    > É uma boa prática toohave alguns pontos de recuperação de curto prazo em disco para recuperação rápida. Esses pontos de recuperação são usados para "recuperação operacional". O Azure serve como um bom local fora do site com SLAs e garantia de disponibilidade superiores.
    >
    >

    **Prática recomendada**: Certifique-se de que os Backups do Azure estão agendados após a conclusão da saudação de backups em disco local usando o DPM. Isso permite que o hello mais recente disco toobe backup copiado tooAzure.

13. Escolha a agenda de diretiva de retenção de saudação. detalhes de saudação sobre como funciona a política de retenção de saudação são fornecidos em [tooreplace de Backup do Azure Use seu artigo de infraestrutura de fita](backup-azure-backup-cloud-as-tape.md).

    ![Política de retenção](./media/backup-azure-backup-sql/pg-retentionschedule.png)

    Neste exemplo:

    * Backups são feitos uma vez por dia às 12:00 PM e 8 PM (parte inferior da tela de saudação) e são mantidos por 180 dias.
    * backup Olá no sábado às 12:00. é retido por 104 semanas
    * backup Olá no último sábado às 12:00. é retido por 60 meses
    * backup Olá no último sábado de março às 12:00. é retido por 10 anos
14. Clique em **próximo** e selecione Olá a opção apropriada para transferir Olá tooAzure de cópia de backup inicial. Você pode escolher **automaticamente pela rede Olá** ou **Backup Offline**.

    * **Automaticamente pela rede Olá** transferências Olá tooAzure de dados de backup de acordo com a agenda de saudação escolhida para backup.
    * Como o **Backup Offline** funciona é explicado no [Fluxo de trabalho de backup offline no Backup do Azure](backup-azure-backup-import-export.md).

    Escolha a transferência relevantes Olá mecanismo toosend Olá cópia de backup inicial tooAzure e clique em **próximo**.
15. Depois que você revisar detalhes da política de saudação em Olá **resumo** tela, clique em Olá **criar grupo** fluxo de trabalho do botão toocomplete hello. Você pode clicar em Olá **fechar** andamento Olá botão e monitor do trabalho no espaço de trabalho de monitoramento.

    ![Criação de grupo de proteção em andamento](./media/backup-azure-backup-sql/pg-summary.png)

## <a name="on-demand-backup-of-a-sql-server-database"></a>Backup sob demanda de um banco de dados SQL Server
Enquanto as etapas anteriores Olá criou uma política de backup, um "ponto de recuperação" é criado somente quando o primeiro backup de saudação ocorre. Em vez de esperar Olá Agendador tookick em, etapas Olá abaixo de criação de saudação do gatilho de uma recuperação ponto manualmente.

1. Aguarde até que o status do grupo de proteção Olá mostra **Okey** para banco de dados de saudação antes de criar o ponto de recuperação de saudação.

    ![Membros do grupo de proteção](./media/backup-azure-backup-sql/sqlbackup-recoverypoint.png)
2. Clique com botão direito no banco de dados de saudação e selecione **criar ponto de recuperação**.

    ![Criar ponto de recuperação online](./media/backup-azure-backup-sql/sqlbackup-createrp.png)
3. Escolha **proteção Online** no menu suspenso de saudação e clique em **Okey**. Isso inicia a criação de saudação de um ponto de recuperação no Azure.

    ![Criar Ponto de Recuperação](./media/backup-azure-backup-sql/sqlbackup-azure.png)
4. Você pode exibir o andamento do trabalho Olá no hello **monitoramento** espaço de trabalho onde você encontrará uma em andamento do trabalho como Olá um mostrado na figura a seguir hello.

    ![Console de monitoramento](./media/backup-azure-backup-sql/sqlbackup-monitoring.png)

## <a name="recover-a-sql-server-database-from-azure"></a>Recuperar um banco de dados SQL Server no Azure
Olá, etapas a seguir são necessária toorecover uma entidade protegida (banco de dados do SQL Server) do Azure.

1. Abra o Console de gerenciamento do servidor DPM hello. Navegue muito**recuperação** onde você pode ver os servidores de saudação do espaço de trabalho feito pelo DPM. Procure banco de dados necessários (por este caso ReportServer$ MSDPM2012) hello. Selecione uma hora para **Recuperar de** que termine com **Online**.

    ![Selecione um ponto de recuperação](./media/backup-azure-backup-sql/sqlbackup-restorepoint.png)
2. Nome do banco de dados de saudação de mouse e clique em **recuperar**.

    ![Recuperar do Azure](./media/backup-azure-backup-sql/sqlbackup-recover.png)
3. O DPM mostra detalhes de Olá Olá do ponto de recuperação. Clique em **Avançar**. banco de dados de saudação de toooverwrite, tipo de recuperação selecione Olá **recuperar toooriginal instância do SQL Server**. Clique em **Avançar**.

    ![Recuperar tooOriginal local](./media/backup-azure-backup-sql/sqlbackup-recoveroriginal.png)

    Neste exemplo, o DPM permite a recuperação Olá tooanother instância do SQL Server ou pasta de rede tooa autônomo.
4. Em Olá **opções de recuperação especificar** tela, você pode selecionar opções de recuperação hello como toothrottle Olá da largura de banda usada pela recuperação de limitação do uso de largura de banda de rede. Clique em **Avançar**.
5. Em Olá **resumo** tela, você vê todas as configurações de recuperação Olá fornecidas até o momento. Clique em **Recuperar**.

    Olá status de recuperação mostra o banco de dados de hello está sendo recuperado. Você pode clicar em **fechar** tooclose Olá assistente e exibição Olá progresso na Olá **monitoramento** espaço de trabalho.

    ![Iniciar o processo de recuperação](./media/backup-azure-backup-sql/sqlbackup-recoverying.png)

    Concluída a recuperação Olá, o banco de dados de saudação restaurado é consistente com aplicativo.

### <a name="next-steps"></a>Próximas etapas:
•    [Perguntas frequentes sobre o Backup do Azure](backup-azure-backup-faq.md)
