---
title: aaaBack backup de seu aplicativo no Azure
description: "Saiba como toocreate backups de seus aplicativos no serviço de aplicativo do Azure."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 6223b6bd-84ec-48df-943f-461d84605694
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: e41d93d322bbc48b45b28eeaa817928d83c2b9d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-your-app-in-azure"></a>Fazer backup de seu aplicativo no Azure
Olá fazer backup e restaurar o recurso no [do serviço de aplicativo do Azure](../app-service/app-service-value-prop-what-is.md) permite que você crie facilmente os backups de aplicativos manualmente ou em uma agenda. Você pode restaurar o instantâneo de tooa aplicativo hello de um estado anterior por sobrescrever app existente de saudação ou restauração tooanother. 

Para obter informações sobre como restaurar um aplicativo por um backup, veja [Restaurar um aplicativo no Serviço de Aplicativo do Azure](web-sites-restore.md).

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a>Do que é feito backup
Serviço de aplicativo pode fazer o backup do seguinte Olá conta de armazenamento do Azure tooan informações e contêiner que você tenha configurado toouse seu aplicativo. 

* Configuração do aplicativo
* Conteúdo do arquivo
* Banco de dados conectado tooyour aplicativo

Olá soluções de banco de dados a seguir têm suporte com o recurso de backup: 
   - [Banco de Dados SQL](https://azure.microsoft.com/en-us/services/sql-database/)
   - [Banco de Dados do Azure para MySQL (Visualização)](https://azure.microsoft.com/en-us/services/mysql)
   - [Banco de Dados do Azure para PostgreSQL (Visualização)](https://azure.microsoft.com/en-us/services/postgres)
   - [ClearDB MySQL](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
   - [MySQL no aplicativo](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)
 

> [!NOTE]
>  Cada backup é uma cópia offline completa do aplicativo, não uma atualização incremental.
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a>Requisitos e restrições
* Olá fazer backup e o recurso de restauração requer Olá toobe do plano de serviço de aplicativo no hello **padrão** camada ou **Premium** camada. Para obter mais informações sobre como dimensionar seu plano de serviço de aplicativo toouse uma camada superior, consulte [dimensionar um aplicativo no Azure](web-sites-scale.md).  
  A camada **Premium** permite um número maior de backups diários do que a camada **Standard**.
* Você precisa de uma conta de armazenamento do Azure e o contêiner no hello mesma assinatura que você deseja toobackup de aplicativo de saudação. Para obter mais informações sobre contas de armazenamento do Azure, consulte Olá [links](#moreaboutstorage) final Olá deste artigo.
* Backups podem ser a too10 GB de conteúdo do aplicativo e banco de dados. Se o tamanho do backup Olá exceder esse limite, você receberá um erro.

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a>Criar um backup manual
1. Em Olá [Portal do Azure](https://portal.azure.com), navegue folha tooyour do aplicativo, selecione **Backups**. Olá **Backups** folha será exibida.
   
    ![Página Backups][ChooseBackupsPage]
   
   > [!NOTE]
   > Se você vir a mensagem de saudação abaixo, clique nele tooupgrade seu plano de serviço de aplicativo antes de prosseguir com backups.
   > Veja [Escalar verticalmente um aplicativo no Azure](web-sites-scale.md) para obter mais informações.  
   > ![Escolher uma conta de armazenamento](./media/web-sites-backup/01UpgradePlan1.png)
   > 
   > 

2. Em Olá **Backup** folha, clique em **configurar**
![clique em configurar](./media/web-sites-backup/ClickConfigure1.png)
3. Em Olá **configuração de Backup** folha, clique em **armazenamento: não configurado** tooconfigure uma conta de armazenamento.
   
    ![Escolher uma conta de armazenamento][ChooseStorageAccount]
4. Escolha o destino de seu backup selecionando uma **Conta de Armazenamento** e um **Contêiner**. conta de armazenamento Olá deve pertencer toohello mesma assinatura que o aplicativo hello desejar tooback. Se desejar, você pode criar uma nova conta de armazenamento ou um novo contêiner folhas respectivos hello. Quando terminar, clique em **Selecionar**.
   
    ![Escolher uma conta de armazenamento](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. Em Olá **configuração de Backup** folha que for deixada aberta, você pode configurar **banco de dados de Backup**, em seguida, selecione os bancos de dados de saudação desejado tooinclude nos backups de saudação (banco de dados SQL ou MySQL) e clique em **Okey**.  
   
    ![Escolher uma conta de armazenamento](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > Para um tooappear de banco de dados nessa lista, sua cadeia de caracteres de conexão deve existir no hello **cadeias de caracteres de Conexão** seção Olá **configurações de aplicativo** folha para seu aplicativo.
   > 
   > 
6. Em Olá **configuração de Backup** folha, clique em **salvar**.    
7. Em Olá **Backups** folha, clique em **Backup**.
   
    ![Botão BackUpNow][BackUpNow]
   
    Você verá uma mensagem de progresso durante o processo de backup hello.

Depois da configuração do contêiner e a conta de armazenamento hello, você pode iniciar um backup manual a qualquer momento.  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a>Configurar backups automáticos
1. Em Olá **configuração de Backup** folha, defina **backup agendado** muito**em**. 
   
    ![Escolher uma conta de armazenamento](./media/web-sites-backup/05ScheduleBackup1.png)
2. Definir opções de serão exibida, agendamento de backup **Backup agendado** muito**na**, em seguida, configurar o agendamento de backup Olá conforme desejado e clique em **Okey**.
   
    ![Habilitar backups automatizados][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a>Configurar backups parciais
Às vezes, você não quer toobackup tudo em seu aplicativo. Veja alguns exemplos:

* Você [configura backups semanais](web-sites-backup.md#configure-automated-backups) do aplicativo que contém conteúdo estático que nunca muda, como imagens ou postagens antigas no blog.
* Seu aplicativo tem mais de 10 GB de conteúdo (que é o valor máximo hello, que você pode fazer backup de cada vez).
* Você não deseja que os arquivos de log Olá toobackup.

Backups parciais permite que você escolha exatamente quais arquivos que você deseja toobackup.

### <a name="exclude-files-from-your-backup"></a>Excluir arquivos do backup
Suponha que você tenha um aplicativo que contém os arquivos de log e imagens estáticas que tenham sido backup uma vez e não serão toochange. Nesses casos, você pode excluir a exclusão desses arquivos e pastas em backups futuros. tooexclude arquivos e pastas de seus backups, criar um `_backup.filter` arquivo hello `D:\home\site\wwwroot` pasta do seu aplicativo. Especifica Olá lista de arquivos e pastas que você deseja tooexclude neste arquivo. 

Um tooaccess de maneira fácil seus arquivos é toouse Kudu. Clique em **ferramentas avançadas -> Go** configuração para seu aplicativo de web tooaccess Kudu.

![Kudu usando o Portal][kudu-portal]

Identifica Olá pastas que você deseja tooexclude de seus backups.  Por exemplo, você deseja toofilter pasta realçado hello e arquivos.

![Pasta Imagens][ImagesFolder]

Crie um arquivo chamado `_backup.filter` e colocar a lista de saudação acima no arquivo hello, mas remover `D:\home`. Liste um diretório ou arquivo por linha. Então o conteúdo de saudação do arquivo hello deve ser:
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

Carregar `_backup.filter` arquivo toohello `D:\home\site\wwwroot\` diretório de seu site usando [ftp](web-sites-deploy.md#ftp) ou qualquer outro método. Se desejar, você pode criar o arquivo hello diretamente usando Kudu `DebugConsole` e inserir seu conteúdo hello.

Executar backups Olá mesmo como você faria normalmente, [manualmente](#create-a-manual-backup) ou [automaticamente](#configure-automated-backups). Agora, todos os arquivos e pastas que são especificadas em `_backup.filter` é excluído da saudação futuros backups agendados ou iniciado manualmente. 

> [!NOTE]
> Restaurar backups parciais de saudação seu site mesma maneira que faria [restaurar um backup regular](web-sites-restore.md). o processo de restauração Olá Olá certo.
> 
> Quando um backup completo for restaurado, todo o conteúdo no site de saudação é substituído por tudo o que está em backup de saudação. Se um arquivo estiver no site hello, mas não no backup Olá é excluído. Mas, quando um backup parcial é restaurado, qualquer conteúdo que está localizado em um dos diretórios de saudação na lista negra ou qualquer arquivo na lista negra, será deixado como está.
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a>Como os backups são armazenados
Depois de ter feito uma ou mais backups para seu aplicativo, backups de saudação são visíveis em Olá **contêineres** folha de sua conta de armazenamento e seu aplicativo. Conta de armazenamento hello, cada backup consiste em uma`.zip` arquivo que contém os dados de backup hello e um `.xml` arquivo que contém um manifesto de saudação `.zip` o conteúdo do arquivo. Você pode descompactar e procurar esses arquivos se você quiser tooaccess seus backups sem realmente executar uma restauração do aplicativo.

backup de banco de dados Olá para o aplicativo hello é armazenado na raiz de saudação do arquivo the.zip. Para um banco de dados SQL, este é um arquivo BACPAC (sem extensão de arquivo) e pode ser importado. toocreate um banco de dados do SQL com base em Olá exportação do BACPAC, consulte [importar um arquivo BACPAC de tooCreate um novo banco de dados de usuário](http://technet.microsoft.com/library/hh710052.aspx).

> [!WARNING]
> Alterar qualquer um dos arquivos Olá no seu **websitebackups** contêiner pode fazer com que o hello toobecome de backup inválido e, portanto, não recuperáveis.
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a>Próximas etapas
Para obter informações sobre como restaurar um aplicativo por um backup, veja [Restaurar um aplicativo no Serviço de Aplicativo do Azure](web-sites-restore.md). Você também pode fazer backup e restaurar aplicativos de serviço de aplicativo usando a API REST (consulte [REST de uso toobackup e restauração de aplicativos de serviço de aplicativo](websites-csm-backup.md)).


<!-- IMAGES -->
[ChooseBackupsPage]: ./media/web-sites-backup/01ChooseBackupsPage1.png
[ChooseStorageAccount]: ./media/web-sites-backup/02ChooseStorageAccount-1.png
[IncludedDatabases]: ./media/web-sites-backup/03IncludedDatabases.png
[BackUpNow]: ./media/web-sites-backup/04BackUpNow1.png
[BackupProgress]: ./media/web-sites-backup/05BackupProgress.png
[SetAutomatedBackupOn]: ./media/web-sites-backup/06SetAutomatedBackupOn1.png
[Frequency]: ./media/web-sites-backup/07Frequency.png
[StartDate]: ./media/web-sites-backup/08StartDate.png
[StartTime]: ./media/web-sites-backup/09StartTime.png
[SaveIcon]: ./media/web-sites-backup/10SaveIcon.png
[ImagesFolder]: ./media/web-sites-backup/11Images.png
[LogsFolder]: ./media/web-sites-backup/12Logs.png
[GhostUpgradeWarning]: ./media/web-sites-backup/13GhostUpgradeWarning.png
[kudu-portal]:./media/web-sites-backup/kudu-portal.PNG

