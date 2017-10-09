### <a name="prerequisites"></a>Pré-requisitos
* Uma conta do Azure; você pode criar uma [conta gratuita](https://azure.microsoft.com/free)
* Um [banco de dados do SQL Azure](../articles/sql-database/sql-database-get-started.md) com suas informações de conexão, incluindo o nome do servidor de hello, o nome do banco de dados e o nome de usuário e senha. Essas informações estão incluídas no hello cadeia de caracteres de conexão de banco de dados SQL:
  
    Server=tcp:*yoursqlservername*.database.windows.net,1433;Initial Catalog=*yourqldbname*;Persist Security Info=False;User ID={your_username};Password={your_password};MultipleActiveResultSets=False;Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
  
    Saiba mais sobre o [Banco de Dados SQL do Azure](https://azure.microsoft.com/services/sql-database).

> [!NOTE]
> Quando você cria um banco de dados do SQL Azure, você também pode criar bancos de dados de exemplo hello incluídos com o SQL. 
> 
> 

Antes de usar o banco de dados do SQL Azure em um aplicativo lógico, conecte-se tooyour banco de dados SQL. Você pode fazer isso facilmente dentro de seu aplicativo lógica em Olá portal do Azure.  

Conecte-se tooyour banco de dados do SQL Azure usando Olá seguindo as etapas:  

1. Crie um aplicativo lógico. No designer de aplicativos lógicos hello, adicionar um gatilho e, em seguida, adicione uma ação. Selecione **APIs gerenciadas do Microsoft Mostrar** em hello lista suspensa e, em seguida, digite "sql" na caixa de pesquisa de saudação. Selecione uma das ações de saudação:  
   
    ![Etapa de criação da conexão com o SQL Azure](./media/connectors-create-api-sqlazure/sql-actions.png)
2. Se você ainda não criou nenhum tooSQL conexões banco de dados, você será solicitado para obter detalhes de conexão de saudação:  
   
    ![Etapa de criação da conexão com o SQL Azure](./media/connectors-create-api-sqlazure/connection-details.png) 
3. Insira os detalhes do banco de dados SQL de saudação. As propriedades com um asterisco são obrigatórias.
   
   | Propriedade | Detalhes |
   | --- | --- |
   | Conectar-se Usando Gateway |Deixe desmarcada. Isso é usado quando se conectar tooan local do SQL Server. |
   | Nome da Conexão * |Digite um nome para a conexão. |
   | Nome do SQL Server * |Insira o nome do servidor de saudação; qual é algo como *servername.database.windows.net*. nome do servidor de saudação é exibido nas propriedades de banco de dados SQL Olá Olá portal do Azure e também é exibido na cadeia de caracteres de conexão de saudação. |
   | Nome do Banco de Dados SQL * |Insira o nome de saudação você deu seu banco de dados SQL. Isso é listado nas propriedades do banco de dados SQL Olá na cadeia de caracteres de conexão de saudação: catálogo inicial =*yoursqldbname*. |
   | Nome de Usuário * |Insira o nome de usuário de saudação criado quando Olá banco de dados SQL foi criado. Isso é listado nas propriedades de banco de dados SQL Olá Olá portal do Azure. |
   | Senha * |Digite a senha de saudação criada quando Olá banco de dados SQL foi criado. |
   
    Essas credenciais são usada tooauthorize tooconnect de aplicativo sua lógica e acessam os dados do SQL. Uma vez concluído, os detalhes da conexão aparência a seguir toohello semelhante:  
   
    ![Etapa de criação da conexão com o SQL Azure](./media/connectors-create-api-sqlazure/sample-connection.png) 
4. Selecione **Criar**. 
5. Aviso Olá conexão foi criado. Agora, continue com hello outra etapas em seu aplicativo lógico: 
   
    ![Etapa de criação da conexão com o SQL Azure](./media/connectors-create-api-sqlazure/table.png)

