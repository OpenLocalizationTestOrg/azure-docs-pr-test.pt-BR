### <a name="create-a-new-logical-sql-server-in-hello-azure-portal"></a>Criar um novo servidor SQL lógico no hello portal do Azure

1. Clique em **Novo**, pesquise **servidor lógico** e pressione **ENTER**.

    ![pesquisar servidor lógico](./media/sql-data-warehouse-create-logical-server/search-logical-server.png)
2. Selecione **SQL server (servidor lógico)** 

    ![selecionar servidor lógico](./media/sql-data-warehouse-create-logical-server/select-logical-server.png)
  
3. Clique em **criar** tooopen Olá nova do SQL Server (servidor lógico) folha.

   <kbd>![abrir a folha de servidor lógico](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd> ![folha de servidor lógico](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png)</kbd>
  
3. Na caixa de texto Nome do servidor da folha do SQL Server (servidor lógico) hello, forneça um nome válido para o novo servidor lógico de saudação. Uma marca de seleção verde indica que você forneceu um nome válido.
    
    ![novo nome do servidor](./media/sql-data-warehouse-create-logical-server/new-name-logical-server.png)

    > [!IMPORTANT]
    > Olá nome totalmente qualificado para o novo servidor será < your_server_name >. t.
    >
    
4. Na caixa de texto do logon de administrador de servidor hello, forneça um nome de usuário para logon de autenticação de SQL Olá para este servidor. Esse logon é conhecido como logon principal do servidor de saudação. Uma marca de seleção verde indica que você forneceu um nome válido.
    
    ![Logon de administrador do SQL](./media/sql-data-warehouse-create-logical-server/sql-admin-login.png)
5. Em Olá **senha** e **Confirmar senha** caixas de texto, forneça uma senha para a conta de logon principal do servidor de saudação. Uma marca de seleção verde indica que você forneceu uma senha válida.
    
    ![Senha de administrador do SQL](./media/sql-data-warehouse-create-logical-server/sql-admin-password.png)
6. Selecione uma assinatura em que você tenha objetos toocreate de permissão.

    ![subscription](./media/sql-data-warehouse-create-logical-server/subscription.png)
7. Na caixa de texto de grupo de recursos de saudação, selecione **criar novo** e, em seguida, na caixa de texto de grupo de recursos hello, forneça um nome válido para Olá novo grupo de recursos (você também pode usar um grupo de recursos existente se você já tiver criado um). Uma marca de seleção verde indica que você forneceu um nome válido.

    ![novo grupo de recursos](./media/sql-data-warehouse-create-logical-server/new-resource-group.png)

8. Em Olá **local** caixa de texto, selecione um data center local apropriado tooyour - como "Leste da Austrália".
    
    ![local do servidor](./media/sql-data-warehouse-create-logical-server/server-location.png)
    
    > [!TIP]
    > Olá a caixa de seleção **permitir servidor de tooaccess de serviços do azure** não pode ser alterado nesta folha. Você pode alterar essa configuração na folha de firewall de servidor de saudação. Para obter mais informações, confira [Introdução à segurança](../articles/sql-database/sql-database-manage-servers-portal.md).
    >
    
9. Clique em **Criar**.

    ![botão criar](./media/sql-data-warehouse-create-logical-server/create.png)

