---
title: aaaBack backup de um servidor de Exchange tooAzure Backup com o servidor de Backup do Azure | Microsoft Docs
description: Saiba como tooback a um tooAzure do servidor Exchange Backup usando o servidor de Backup do Azure
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: e46557e8-2eaf-4ee0-99ea-00fbb8687dca
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: db874161151fc57c5b79c41531e18d577f567f66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-an-exchange-server-tooazure-backup-with-azure-backup-server"></a>Fazer backup de um servidor de Exchange tooAzure Backup com o servidor de Backup do Azure
Este artigo descreve como tooback do Microsoft Azure Backup Server (MABS) tooconfigure a um tooAzure de servidor do Microsoft Exchange.  

## <a name="prerequisites"></a>Pré-requisitos
Antes de continuar, verifique se o Servidor de Backup do Azure está [instalado e preparado](backup-azure-microsoft-azure-backup.md).

## <a name="mabs-protection-agent"></a>Agente de proteção do MABS
Agente de proteção de MABS tooinstall Olá no servidor do Exchange hello, siga estas etapas:

1. Certifique-se de que firewalls Olá estão configurados corretamente. Consulte [configurar exceções de firewall Olá agente](https://technet.microsoft.com/library/Hh758204.aspx).
2. Instale o agente de saudação no servidor do Exchange Olá clicando **gerenciamento > agentes > instalar** no Console do administrador MABS. Consulte [instalar agente de proteção de MABS de saudação](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) para obter etapas detalhadas.

## <a name="create-a-protection-group-for-hello-exchange-server"></a>Criar um grupo de proteção para o Exchange server de saudação
1. No hello MABS Administrator Console, clique em **proteção**e, em seguida, clique em **novo** em Olá Olá de tooopen de faixa de opções de ferramenta **criar novo grupo de proteção** assistente.
2. Em Olá **bem-vindo** tela hello Assistente clique **próximo**.
3. Em Olá **Selecionar tipo de grupo de proteção** tela, selecione **servidores** e clique em **próximo**.
4. Selecione Olá Exchange server banco de dados que você deseja tooprotect e clique em **próximo**.

   > [!NOTE]
   > Se você estiver protegendo o Exchange 2013, verifique Olá [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).
   >
   >

    Saudação de exemplo a seguir, banco de dados de saudação do Exchange 2010 está selecionado.

    ![Selecionar membros do grupo](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. Selecione o método de proteção de dados hello.

    Grupo de proteção de saudação do nome e, em seguida, selecione dois Olá as opções a seguir:

   * Desejo a proteção de curto prazo usando Disco.
   * Desejo a proteção online.
6. Clique em **Avançar**.
7. Selecione Olá **integridade de dados executar Eseutil toocheck** opção se você quiser que a integridade de bancos de dados do Exchange Server Olá Olá toocheck.

    Depois de selecionar essa opção, a verificação de consistência de backup será executada em MABS tooavoid hello e/s o tráfego que é gerado pela execução Olá **eseutil** comando no servidor do Exchange hello.

   > [!NOTE]
   > toouse essa opção, você deve copiar hello Ese.dll e Eseutil.exe arquivos toohello C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin diretório Olá MAB servidor. Caso contrário, é acionado Olá erro a seguir:  
   > ![erro de eseutil](./media/backup-azure-backup-exchange-server/eseutil-error.png)
   >
   >
8. Clique em **Avançar**.
9. Banco de dados selecione Olá para **Backup de cópia**e, em seguida, clique em **próximo**.

   > [!NOTE]
   > Se você não escolher "Backup completo" para pelo menos uma cópia de DAG de um banco de dados, os registros não ficarão truncados.
   >
   >
10. Configurar metas Olá para **backup de curto prazo**e, em seguida, clique em **próximo**.
11. Examine o espaço em disco disponível hello e, em seguida, clique em **próximo**.
12. Selecione Olá tempo no qual Olá MAB servidor criar a replicação inicial hello e, em seguida, clique em **próximo**.
13. Selecione as opções de verificação de consistência hello e, em seguida, clique em **próximo**.
14. Escolha Olá banco de dados que você deseja tooback backup tooAzure e, em seguida, clique em **próximo**. Por exemplo:

    ![Especificar dados de proteção online](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. Definir agendamento Olá para **Backup do Azure**e, em seguida, clique em **próximo**. Por exemplo:

    ![Especifique o cronograma do backup online](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > Observe que os Pontos de recuperação online têm base nos pontos de recuperação completos expressos. Portanto, você deve agendar o ponto de recuperação online Olá após um tempo de saudação especificado para Olá express ponto de recuperação completa.
    >
    >
16. Configurar a política de retenção Olá para **Backup do Azure**e, em seguida, clique em **próximo**.
17. Escolha uma opção de replicação online e clique em **Próximo**.

    Se você tiver um banco de dados grande, pode levar muito tempo para a saudação inicial toobe backup criado pela rede hello. tooavoid esse problema, você pode criar um backup offline.  

    ![Especificar política de retenção online](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. Confirme as configurações de saudação e, em seguida, clique em **criar grupo**.
19. Clique em **fechar**

## <a name="recover-hello-exchange-database"></a>Recuperar o banco de dados do Exchange Olá
1. toorecover um banco de dados do Exchange, clique em **recuperação** em Olá MABS Administrator Console.
2. Localize o banco de dados do Exchange Olá que você deseja toorecover.
3. Selecione um ponto de recuperação online de saudação *tempo de recuperação* lista suspensa.
4. Clique em **recuperar** toostart Olá **Assistente de recuperação**.

Há cinco tipos de recuperação para os pontos de recuperação online:

* **Recuperar o local do Exchange Server toooriginal:** Olá dados sejam recuperados toohello original Exchange server.
* **Recuperar o banco de dados tooanother em um servidor Exchange:** Olá os dados sejam recuperados tooanother banco de dados em outro servidor Exchange.
* **Recuperar o banco de dados de recuperação de tooa:** Olá os dados sejam recuperado tooan banco de dados de recuperação do Exchange (RDB).
* **Pasta de rede cópia tooa:** Olá os dados sejam recuperados tooa pasta de rede.
* **Copiar tootape:** se você tiver uma biblioteca de fitas ou uma unidade de fita autônoma MABS anexado e configurado no ponto de recuperação hello serão copiados fita livre tooa.

    ![Escolher a replicação online](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a>Próximas etapas
* [Backup do Azure - Perguntas frequentes](backup-azure-backup-faq.md)
