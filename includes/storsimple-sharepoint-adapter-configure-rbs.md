<!--author=SharS last changed: 1/14/2016 -->

> [!NOTE]
> Quando você faz alterações toohello adaptador StorSimple para configuração do SharePoint RBS, você deve fazer logon com uma conta de usuário que pertence o grupo de Admins. do domínio toohello. Além disso, é necessário acessar a página de configuração de saudação de um navegador em execução no hello mesmo host como a Administração Central.
> 
> 

#### <a name="tooconfigure-rbs"></a>tooconfigure RBS
1. Abra a página de Administração Central do SharePoint hello e procurar muito**configurações do sistema**. 
2. Em Olá **Azure StorSimple** seção, clique em **configurar adaptador do StorSimple**.
   
    ![Configurar Olá adaptador StorSimple](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS1-include.png) 
3. Em Olá **configurar adaptador do StorSimple** página:
   
   1. Certifique-se de que Olá **habilitar edição de caminho** caixa de seleção é marcada.
   2. Na caixa de texto de saudação, digite o caminho de convenção de nomenclatura Universal (UNC) de Olá Olá do repositório de BLOB.
      
      > [!NOTE]
      > volume de armazenamento BLOB Olá deve ser hospedado em um volume iSCSI configurado no dispositivo do StorSimple hello.

   3. Clique em Olá **habilitar** botão abaixo de cada Olá bancos de dados que você deseja tooconfigure para armazenamento remoto.
      
      > [!NOTE]
      > armazenamento de BLOB Olá deve ser compartilhado por todos os servidores web front-end (WFE) e conta de usuário de Olá configurado para o farm do SharePoint server Olá deve ter o compartilhamento de toohello de acesso.
      
      ![Habilitar provedor RBS Olá](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS2-include.png)
      
      Quando você habilita ou desabilita o RBS, você também verá seguinte mensagem de saudação.
      
      ![Configurar o Adaptador StorSimple para Habilitado/Desabilitado](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_ConfigureStorSimpleAdapterEnableDisableMessage-include.png)

   4. Clique em Olá **atualização** configuração de saudação do botão tooapply. Quando você clica em Olá **atualização** botão, Olá status de configuração de RBS será atualizado em todos os servidores WFE e toda a farm Olá será habilitado para RBS. Olá a seguinte mensagem será exibida.
      
      ![Mensagem de configuração do adaptador](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS3-include.png)
      
      > [!NOTE]
      > Se você estiver configurando o RBS para um farm do SharePoint com um número muito grande de bancos de dados (mais de 200), página de web de Administração Central do SharePoint Olá pode atingir o tempo limite. Se isso ocorrer, atualize a página de saudação. Isso não afeta o processo de configuração de saudação.

4. Verificar configuração hello:
   
   1. Faça logon no site de Administração Central do SharePoint toohello e procurar toohello **configurar adaptador do StorSimple** página.
   2. Verifique toomake detalhes de configuração de saudação se eles correspondem às configurações de saudação que você inseriu. 
5. Verifique se o RBS funciona corretamente:
   
   1. Carregar um documento tooSharePoint. 
   2. Procure caminho UNC toohello que você configurou. Certifique-se de que a estrutura de diretório RBS Olá foi criada e que ele contém o objeto Olá carregado.
6. (Opcional) Você pode usar o hello Microsoft RBS `Migrate()` cmdlet do PowerShell incluído com o SharePoint toomigrate existente BLOB conteúdo toohello dispositivo StorSimple. Para obter mais informações, consulte [migrar conteúdo para dentro ou fora do RBS no SharePoint 2013] [ 6] ou [migrar conteúdo para dentro ou fora do RBS (SharePoint Foundation 2010)] [7].
7. (Opcional) Em instalações de teste, você pode verificar que Olá BLOBs foram movidos para fora do banco de dados de conteúdo do hello da seguinte maneira: 
   
   1. Inicie o SQL Management Studio.
   2. Execute a consulta de ListBlobsInDB_2010.sql ou ListBlobsInDB_2013.sql hello, da seguinte maneira.
      
      ```
      **ListBlobsInDB_2013.sql**
      
        USE WSS_Content
        GO
      
        SELECT DocStreams.DocId,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               DocStreams.RbsId,
               TimeLastModified
      
        FROM DocStreams
      
             INNER JOIN AllDocs ON DocStreams.DocId = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      
      **ListBlobsInDB_2010.sql**
      
        USE WSS_Content
        GO
      
        SELECT AllDocStreams.Id,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               RbsId,
               TimeLastModified
        FROM AllDocStreams
      
             INNER JOIN AllDocs ON AllDocStreams.Id = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      ```
      
      Se o RBS foi configurado corretamente, um valor NULL aparece na coluna de SizeOfContentInDB Olá para qualquer objeto que foi carregado e externalizado com êxito com RBS.
8. (Opcional) Depois de configurar o RBS e mover todas as toohello conteúdo BLOB dispositivo StorSimple, você pode mover o dispositivo de toohello do banco de dados de conteúdo de saudação. Se você escolher o banco de dados conteúdo toomove Olá, é recomendável que você configure o armazenamento de banco de dados de conteúdo Olá no dispositivo hello como um volume primário. Em seguida, use estabelecida que dispositivo StorSimple do toomigrate Olá banco de dados de conteúdo toohello de práticas recomendadas do SQL Server. 
   
   > [!NOTE]
   > Dispositivo móvel de toohello de banco de dados de conteúdo Olá somente há suporte para séries Olá StorSimple 8000 (não há suporte para a série de saudação 5000 ou 7000).
   
   Se você armazenar BLOBs e banco de dados de conteúdo do hello em volumes separados no dispositivo do StorSimple Olá, é recomendável que você configure no hello mesmo contêiner de volume. Isso garante que os respectivos backups sejam feitos juntos.
   
   > [!WARNING]
   > Se você não tiver habilitado o RBS, não recomendamos mover o dispositivo de StorSimple toohello Olá conteúdo do banco de dados. Essa é uma configuração não testada.
   
9. Vá toohello próxima etapa: [configurar coleta de lixo](#configure-garbage-collection).

[6]: https://technet.microsoft.com/library/ff628254(v=office.15).aspx
[7]: https://technet.microsoft.com/library/ff628255(v=office.14).aspx
