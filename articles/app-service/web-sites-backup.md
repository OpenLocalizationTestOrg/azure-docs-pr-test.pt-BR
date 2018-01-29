---
title: Fazer backup de seu aplicativo no Azure
description: "Saiba como criar backups de seus aplicativos no Serviço de Aplicativo do Azure."
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
ms.openlocfilehash: 435370a8758d439a5fcce2e04efd11b4aaaf0357
ms.sourcegitcommit: 933af6219266cc685d0c9009f533ca1be03aa5e9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="back-up-your-app-in-azure"></a>Fazer backup de seu aplicativo no Azure
O recurso de Backup e Restauração no [Serviço de Aplicativo do Azure](app-service-web-overview.md) permite que você crie backups de aplicativos facilmente, de modo manual ou agendado. Você pode restaurar o aplicativo em um instantâneo de um estado anterior, substituindo o aplicativo existente ou restaurando em outro aplicativo. 

Para obter informações sobre como restaurar um aplicativo por um backup, veja [Restaurar um aplicativo no Serviço de Aplicativo do Azure](web-sites-restore.md).

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a>Do que é feito backup
O Serviço de Aplicativo pode fazer backup das seguintes em uma conta de armazenamento do Azure e um contêiner que você configurou para uso de seu aplicativo. 

* Configuração do aplicativo
* Conteúdo do arquivo
* Banco de dados conectado ao seu aplicativo

As soluções de banco de dados a seguir são compatíveis com o recurso de backup: 
   - [Banco de Dados SQL](https://azure.microsoft.com/en-us/services/sql-database/)
   - [Banco de Dados do Azure para MySQL (Visualização)](https://azure.microsoft.com/en-us/services/mysql)
   - [Banco de Dados do Azure para PostgreSQL (Visualização)](https://azure.microsoft.com/en-us/services/postgres)
   - [MySQL no aplicativo](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)
 

> [!NOTE]
>  Cada backup é uma cópia offline completa do aplicativo, não uma atualização incremental.
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a>Requisitos e restrições
* O recurso de Backup e Restauração exige que o plano de Serviço de Aplicativo esteja na camada **Standard** ou **Premium**. Para obter mais informações sobre como dimensionar seu plano do Serviço de Aplicativo para usar uma camada superior, veja [Escalar verticalmente um aplicativo Web no Serviço de Aplicativo do Azure](web-sites-scale.md).  
  A camada **Premium** permite um número maior de backups diários do que a camada **Standard**.
* Você precisa de uma conta de armazenamento do Azure e do contêiner na mesma assinatura do aplicativo do qual você deseja fazer backup. Para obter mais informações sobre contas de armazenamento do Azure, consulte os [links](#moreaboutstorage) no final deste artigo.
* Backups podem ter até 10 GB de conteúdo do aplicativo e do banco de dados. Se o tamanho do backup ultrapassar esse limite, você receberá um erro.

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a>Criar um backup manual
1. No [Portal do Azure](https://portal.azure.com), navegue até a página do seu aplicativo e selecione **Backups**. A página **Backups** é exibida.
   
    ![Página Backups][ChooseBackupsPage]
   
   > [!NOTE]
   > Se você vir a seguinte mensagem, clique nela para atualizar seu plano de Serviço de Aplicativo antes de continuar com os backups.
   > Para obter mais informações, consulte [Escalar verticalmente um aplicativo no Azure](web-sites-scale.md).  
   > ![Escolher uma conta de armazenamento](./media/web-sites-backup/01UpgradePlan1.png)
   > 
   > 

2. Na página **Backup**, clique em **Configurar**
![Clique em Configurar](./media/web-sites-backup/ClickConfigure1.png)
3. Na página **Configuração de backup**, clique em **Armazenamento: não configurado** para configurar uma conta de armazenamento.
   
    ![Escolher uma conta de armazenamento][ChooseStorageAccount]
4. Escolha o destino de seu backup selecionando uma **Conta de Armazenamento** e um **Contêiner**. A conta de armazenamento deve pertencer à mesma assinatura do aplicativo do qual você deseja fazer backup. Se desejar, será possível criar uma nova conta de armazenamento ou um novo contêiner nas respectivas páginas. Quando terminar, clique em **Selecionar**.
   
    ![Escolher uma conta de armazenamento](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. Na página **Configuração de backup** que ainda está aberta, é possível configurar o **Banco de dados de backup**, então selecione os bancos de dados que deseja incluir nos backups (banco de dados SQL ou MySQL) e clique em **OK**.  
   
    ![Escolher uma conta de armazenamento](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > Para que um banco de dados seja exibido nessa lista, sua cadeia de conexão deve constar na seção **Cadeias de conexão** da página **Configurações de aplicativo** do aplicativo.
   > 
   > 
6. Na página **Configuração de backup**, clique em **Salvar**.    
7. Na página **Backups**, clique em **Backup**.
   
    ![Botão BackUpNow][BackUpNow]
   
    Você verá uma mensagem informando o andamento do processo de backup.

Após a configuração da conta de armazenamento e do contêiner, será possível iniciar um backup manual a qualquer momento.  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a>Configurar backups automáticos
1. Na página **Configuração de backup**, defina **Backup agendado** como **Ativado**. 
   
    ![Escolher uma conta de armazenamento](./media/web-sites-backup/05ScheduleBackup1.png)
2. Opções de Agendamento de Backups serão exibidas, defina **Backup Agendado** para **Ativado**, configure o agendamento de backup conforme desejado e clique em **OK**.
   
    ![Habilitar backups automatizados][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a>Configurar backups parciais
Às vezes, você não quer fazer backup de tudo em seu aplicativo. Veja alguns exemplos:

* Você [configura backups semanais](web-sites-backup.md#configure-automated-backups) do aplicativo que contém conteúdo estático que nunca muda, como imagens ou postagens antigas no blog.
* Seu aplicativo tem mais de 10 GB de conteúdo (que é o volume máximo de backup por vez).
* Você não deseja fazer backup dos arquivos de log.

Os backups parciais permitem que você escolha exatamente quais arquivos deseja incluir no backup.

### <a name="exclude-files-from-your-backup"></a>Excluir arquivos do backup
Vamos supor que você tenha um aplicativo que contém arquivos de log e imagens estáticas que passaram por backup e não vão mais sofrer alteração. Nesses casos, é possível excluir essas pastas e arquivos de serem armazenadas em seus backups futuros. Para excluir arquivos e pastas de seus backups, crie um arquivo `_backup.filter` na pasta `D:\home\site\wwwroot` de seu aplicativo. Especifique a lista de arquivos e pastas que você excluir deste arquivo. 

Uma maneira fácil de acessar seus arquivos é usar o Kudu. Clique na configuração **Ferramentas Avançadas-> Ir** em seu aplicativo Web para acessar o Kudu.

![Kudu usando o Portal][kudu-portal]

Identifique as pastas que você quer excluir de seus backups.  Por exemplo, você deseja filtrar a pasta e os arquivos realçados.

![Pasta Imagens][ImagesFolder]

Crie um arquivo chamado `_backup.filter` e coloque a lista anterior no arquivo, mas remova `D:\home`. Liste um diretório ou arquivo por linha. Portanto, o conteúdo do arquivo deve ser:
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

Carregue o arquivo `_backup.filter` no diretório `D:\home\site\wwwroot\` de seu site usando o [ftp](app-service-deploy-ftp.md) ou qualquer outro método. Se quiser, você pode criar o arquivo diretamente usando Kudu `DebugConsole` e inserir o conteúdo nesse local.

Execute backups da mesma maneira que faria normalmente, de modo [manual](#create-a-manual-backup) ou [automático](#configure-automated-backups). Agora, quaisquer arquivos e pastas especificados em `_backup.filter` serão excluídos dos backups futuros agendados ou iniciados manualmente. 

> [!NOTE]
> Você restaura backups parciais de seu site da mesma maneira como [restauraria um backup regular](web-sites-restore.md). O processo de restauração faz a coisa certa.
> 
> Quando um backup completo é restaurado, todo o conteúdo do site é substituído por tudo o que está no backup. Se um arquivo estiver no site mas não no backup, será excluído. Mas, quando um backup parcial é restaurado, qualquer conteúdo que esteja localizado em um dos diretórios não autorizados ou qualquer arquivo não autorizado, é deixado como está.
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a>Como os backups são armazenados
Depois de ter feito um ou mais backups para seu aplicativo, os backups estarão visíveis na página **Contêineres** de sua conta de armazenamento e em seu aplicativo. Na conta de armazenamento, cada backup é formado por um arquivo `.zip` que contém os dados de backup e um arquivo `.xml` que contém um manifesto do conteúdo do arquivo `.zip`. Será possível descompactar e procurar esses arquivos se você quiser acessar seus backups sem realmente executar uma restauração do aplicativo.

O backup de banco de dados do aplicativo é armazenado na raiz do arquivo .zip. Para um banco de dados SQL, este é um arquivo BACPAC (sem extensão de arquivo) e pode ser importado. Para criar um banco de dados SQL com base na exportação do BACPAC, veja [Importar um arquivo BACPAC para criar um novo banco de dados de usuário](http://technet.microsoft.com/library/hh710052.aspx).

> [!WARNING]
> A alteração de qualquer um dos arquivos no contêiner **websitebackups** pode fazer com que o backup se torne inválido e, portanto, não restaurável.
> 
> 

## <a name="automate-with-scripts"></a>Automatizar com scripts

É possível automatizar o gerenciamento de backup com scripts, usando a [CLI do Azure](/cli/azure/install-azure-cli) ou o [Azure PowerShell](/powershell/azure/overview).

Para obter exemplos, consulte:

- [Exemplos da CLI do Azure](app-service-cli-samples.md)
- [Exemplos do Azure PowerShell](app-service-powershell-samples.md)

<a name="nextsteps"></a>

## <a name="next-steps"></a>Próximas etapas
Para obter informações sobre como restaurar um aplicativo por um backup, veja [Restaurar um aplicativo no Serviço de Aplicativo do Azure](web-sites-restore.md). 


<!-- IMAGES -->
[ChooseBackupsPage]: ./media/web-sites-backup/01ChooseBackupsPage1.png
[ChooseStorageAccount]: ./media/web-sites-backup/02ChooseStorageAccount-1.png
[BackUpNow]: ./media/web-sites-backup/04BackUpNow1.png
[SetAutomatedBackupOn]: ./media/web-sites-backup/06SetAutomatedBackupOn1.png
[SaveIcon]: ./media/web-sites-backup/10SaveIcon.png
[ImagesFolder]: ./media/web-sites-backup/11Images.png
[LogsFolder]: ./media/web-sites-backup/12Logs.png
[GhostUpgradeWarning]: ./media/web-sites-backup/13GhostUpgradeWarning.png
[kudu-portal]:./media/web-sites-backup/kudu-portal.PNG

