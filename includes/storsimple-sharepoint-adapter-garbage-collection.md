<!--author=SharS last changed: 9/17/15-->

Neste procedimento, você vai:

1. [Preparar o executável de mantenedor Olá toorun](#to-prepare-to-run-the-maintainer) .
2. [Preparar o banco de dados de conteúdo do hello e a Lixeira para exclusão imediata de BLOBs órfãos](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).
3. [Executar o Maintainer.exe](#to-run-the-maintainer).
4. [Reverter o banco de dados de conteúdo do hello e configurações da Lixeira](#to-revert-the-content-database-and-recycle-bin-settings).

#### <a name="tooprepare-toorun-hello-maintainer"></a>tooprepare toorun Olá mantenedor
1. No servidor front-end da Web de hello, abra Olá Shell de gerenciamento do SharePoint 2013 como um administrador.
2. Navegue pasta toohello *unidade de inicialização*: \Program Files\Microsoft 10.50\Maintainer SQL Remote Blob Storage\.
3. Renomear **Microsoft.Data.sqlremoteblobs.maintainer.exe. config** muito**Web. config**.
4. Use `aspnet_regiis -pdf connectionStrings` toodecrypt Olá Web. config.
5. No arquivo de Web. config descriptografada Olá, em hello `connectionStrings` nó, adicionar Olá cadeia de caracteres de conexão para sua instância do SQL server e Olá nome do banco de dados de conteúdo. Consulte Olá exemplo a seguir.
   
    `<add name=”RBSMaintainerConnectionWSSContent” connectionString="Data Source=SHRPT13-SQL12\SHRPT13;Initial Catalog=WSS_Content;Integrated Security=True;Application Name=&quot;Remote Blob Storage Maintainer for WSS_Content&quot;" providerName="System.Data.SqlClient" />`
6. Use `aspnet_regiis –pef connectionStrings` toore-criptografar o arquivo Web. config de saudação. 
7. Renomear tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config Web. config. 

#### <a name="tooprepare-hello-content-database-and-recycle-bin-tooimmediately-delete-orphaned-blobs"></a>banco de dados conteúdo tooprepare hello e Lixeira tooimmediately excluir BLOBs órfãos
1. Em saudação do SQL Server no SQL Management Studio, execute Olá consultas de atualização para o banco de dados de destino Olá a seguir: 
   
       `use WSS_Content`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ’time 00:00:00’`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’time 00:00:00’`
2. Em Olá web servidor de front-end, em **Administração Central**, editar Olá **configurações gerais do aplicativo Web** para Olá desejado Olá de desabilitar banco de dados de conteúdo tootemporarily Lixeira. Essa ação também será vazio hello Lixeira para todas as coleções de site relacionado. toodo, clique **Administração Central** -> **gerenciamento de aplicativos** -> **Web Applications (gerenciar aplicativos de web)**  ->  **SharePoint - 80** -> **configurações gerais do aplicativo**. Saudação de conjunto **reciclar Bin Status** muito**OFF**.
   
    ![Configurações Gerais do Aplicativo Web](./media/storsimple-sharepoint-adapter-garbage-collection/HCS_WebApplicationGeneralSettings-include.png)

#### <a name="toorun-hello-maintainer"></a>Olá toorun mantenedor
* No servidor front-end da web de hello, em Olá Shell de gerenciamento do SharePoint 2013, execute Olá mantenedor da seguinte maneira:
  
      `Microsoft.Data.SqlRemoteBlobs.Maintainer.exe -ConnectionStringName RBSMaintainerConnectionWSSContent -Operation GarbageCollection -GarbageCollectionPhases rdo`
  
  > [!NOTE]
  > Olá apenas `GarbageCollection` operação tem suporte para StorSimple no momento. Observe também que os parâmetros Olá emitidos para Microsoft.Data.SqlRemoteBlobs.Maintainer.exe diferenciam maiusculas de minúsculas. 
  > 
  > 

#### <a name="toorevert-hello-content-database-and-recycle-bin-settings"></a>banco de dados do toorevert Olá conteúdo e configurações da Lixeira
1. Em saudação do SQL Server no SQL Management Studio, execute Olá consultas de atualização para o banco de dados de destino Olá a seguir:
   
      `use WSS_Content`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ‘days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘orphan_scan_period’ , ’days 30’`
2. No servidor front-end da web de hello, em **Administração Central**, editar Olá **configurações gerais do aplicativo Web** para Olá desejado saudação do banco de dados de conteúdo toore habilitar Lixeira. toodo, clique **Administração Central** -> **gerenciamento de aplicativos** -> **Web Applications (gerenciar aplicativos de web)**  ->  **SharePoint - 80** -> **configurações gerais do aplicativo**. Definir Olá reciclar Bin Status muito**ON**.

