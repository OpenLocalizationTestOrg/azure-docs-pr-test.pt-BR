---
title: aaaRestore um aplicativo no Azure
description: Saiba como toorestore seu aplicativo a partir de um backup.
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 4444dbf7-363c-47e2-b24a-dbd45cb08491
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: 4b54029a9197064f990f29a3c4558c8322668714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-app-in-azure"></a>Restaurar um aplicativo no Serviço de Aplicativo do Azure
Este artigo mostra como toorestore um aplicativo em [do serviço de aplicativo do Azure](../app-service/app-service-value-prop-what-is.md) que você fez backup anteriormente (consulte [backup de seu aplicativo no Azure](web-sites-backup.md)). Você pode restaurar seu aplicativo com seu estado anterior do bancos de dados vinculados tooa sob demanda ou criar um novo aplicativo com base em um backup do seu aplicativo original. Serviço de aplicativo do Azure dá suporte a saudação bancos de dados para backup e restauração a seguir:
- [Banco de Dados SQL](https://azure.microsoft.com/en-us/services/sql-database/)
- [Banco de Dados do Azure para MySQL (Visualização)](https://azure.microsoft.com/en-us/services/mysql)
- [Banco de Dados do Azure para PostgreSQL (Visualização)](https://azure.microsoft.com/en-us/services/postgres)
- [ClearDB MySQL](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
- [MySQL no aplicativo](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)

Restaurando de backups é tooapps disponíveis em execução no **padrão** e **Premium** camada. Para obter informações sobre como escalar verticalmente seu aplicativo, veja [Escalar verticalmente um aplicativo Web no Serviço de Aplicativo do Azure](web-sites-scale.md). **Premium** nível permite que um número maior de toobe de backups diários executada que **padrão** camada.

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a>Restaurar um aplicativo por meio de um backup existente
1. Em Olá **configurações** folha do seu aplicativo em Olá Portal do Azure, clique em **Backups** toodisplay Olá **Backups** folha. Depois, clique em **Restaurar**.
   
    ![Escolha restaurar agora][ChooseRestoreNow]
2. Em Olá **restaurar** folha, uma fonte de backup Olá selecione primeiro.
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    Olá **backup do aplicativo** opção mostra todos Olá backups existentes do aplicativo atual hello e você pode facilmente selecionar um.
    Olá **armazenamento** opção permite selecionar qualquer arquivo ZIP de backup de qualquer conta de armazenamento do Azure e o contêiner na sua assinatura existente.
    Se você estiver tentando toorestore um backup de outro aplicativo, use Olá **armazenamento** opção.
3. Em seguida, especifique o destino Olá Olá restauração dos aplicativos em **destino de restauração**.
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > Se você escolher **Substituir**, todos os dados existentes em seu aplicativo atual serão apagados e substituídos. Antes de clicar em **Okey**, certifique-se de que ele é exatamente o que você deseja toodo.
   > 
   > 
   
    Você pode selecionar **aplicativo existente** toorestore Olá aplicativo tooanother backup app Olá mesmo grupo de recurso. Antes de usar essa opção, você deve já ter criado outro aplicativo no seu grupo de recursos com o espelhamento de banco de dados configuração toohello definido no backup do aplicativo hello. Você também pode criar um **novo** aplicativo toorestore seu conteúdo.

4. Clique em **OK**.

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a>Baixar ou excluir um backup de uma conta de armazenamento
1. De saudação principal **procurar** folha de saudação portal do Azure, selecione **contas de armazenamento**. Uma lista de suas contas de armazenamento existentes é exibida.
2. Selecione a conta de armazenamento de saudação que contém o backup Olá ser toodownload ou delete.hello folha Olá conta de armazenamento é exibida.
3. Na folha de conta de armazenamento hello, selecione o contêiner de saudação desejado
   
    ![Exibir contêineres][ViewContainers]
4. Selecione o arquivo de backup você deseja toodownload ou excluir.
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. Clique em **baixar** ou **excluir** dependendo do que você deseja toodo.  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a>Monitorar uma operação de restauração
toosee detalhes sobre o sucesso de saudação ou falha da operação de restauração do aplicativo hello, navegar toohello **Log de atividades** folha em Olá portal do Azure.  
 

Role para baixo toofind Olá desejado restauração operação e clique em tooselect-lo.

Olá detalhes folha exibe Olá informações disponíveis relacionadas toohello operação de restauração.

## <a name="next-steps"></a>Próximas etapas
Você pode fazer backup e restaurar aplicativos de serviço de aplicativo usando a API REST (consulte [tooback de REST de uso de backup e restauração de aplicativos de serviço de aplicativo](websites-csm-backup.md)).


<!-- IMAGES -->
[ChooseRestoreNow]: ./media/web-sites-restore/02ChooseRestoreNow1.png
[ViewContainers]: ./media/web-sites-restore/03ViewContainers.png
[StorageAccountFile]: ./media/web-sites-restore/02StorageAccountFile.png
[BrowseCloudStorage]: ./media/web-sites-restore/03BrowseCloudStorage.png
[StorageAccountFileSelected]: ./media/web-sites-restore/04StorageAccountFileSelected.png
[ChooseRestoreSettings]: ./media/web-sites-restore/05ChooseRestoreSettings.png
[ChooseDBServer]: ./media/web-sites-restore/06ChooseDBServer.png
[RestoreToNewSQLDB]: ./media/web-sites-restore/07RestoreToNewSQLDB.png
[NewSQLDBConfig]: ./media/web-sites-restore/08NewSQLDBConfig.png
[RestoredContosoWebSite]: ./media/web-sites-restore/09RestoredContosoWebSite.png
[DashboardOperationLogsLink]: ./media/web-sites-restore/10DashboardOperationLogsLink.png
[ManagementServicesOperationLogsList]: ./media/web-sites-restore/11ManagementServicesOperationLogsList.png
[DetailsButton]: ./media/web-sites-restore/12DetailsButton.png
[OperationDetails]: ./media/web-sites-restore/13OperationDetails.png
