## <a name="log-in-toohello-azure-portal"></a>Faça logon no toohello portal do Azure

Faça logon no toohello [portal do Azure](https://portal.azure.com/).

## <a name="create-a-blank-sql-database-using-hello-azure-portal"></a>Criar um banco de dados SQL em branco usando Olá portal do Azure

Um banco de dados SQL do Azure é criado com um conjunto definido de [recursos de computação e armazenamento](../articles/sql-database/sql-database-service-tiers.md). banco de dados de saudação é criado em um [grupo de recursos do Azure](../articles/azure-resource-manager/resource-group-overview.md) e, em um [servidor lógico do banco de dados do Azure SQL](../articles/sql-database/sql-database-features.md). 

Siga essas etapas toocreate um banco de dados SQL em branco. 

1. Clique em Olá **novo** botão localizado no canto superior esquerdo de saudação do hello portal do Azure.

2. Selecione **bancos de dados** de saudação **novo** página e selecione **banco de dados SQL** de saudação **bancos de dados** página. 

   ![criar banco de dados vazio](../articles/sql-database/media/sql-database-design-first-database/create-empty-database.png)

3. Preencha formulário de banco de dados SQL Olá com hello seguintes informações, conforme mostrado na saudação anterior imagem:   

   | Configuração | Valor sugerido | Descrição |
   | --------| --------------- | ----------- | 
   | **Nome do banco de dados** | mySampleDatabase | Para ver os nomes do banco de dados válidos, consulte [Identificadores do Banco de Dados](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers). | 
   | **Assinatura** | Sua assinatura  | Para obter detalhes sobre suas assinaturas, consulte [Assinaturas](https://account.windowsazure.com/Subscriptions). |
   | **Grupo de recursos** | myResourceGroup | Para ver os nomes do grupo de recursos válidos, consulte [Regras e restrições de nomenclatura](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions). |
   | **Selecionar fonte** | Banco de dados em branco | Especifica que um banco de dados em branco deve ser criado. |
   ||||

4. Clique em **Server** toocreate e configurar um novo servidor para o novo banco de dados. Preencha Olá **novo formulário de servidor** com hello informações a seguir: 

   | Configuração | Valor sugerido | Descrição |
   | --------| --------------- | ----------- | 
   | **Nome do servidor** | Qualquer nome exclusivo globalmente. | Para ver os nomes do servidor válidos, consulte [Regras e restrições de nomenclatura](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions). | 
   | **Logon de administrador do servidor** | Qualquer nome válido. | Para ver os nomes de logon válidos, consulte [Identificadores do Banco de Dados](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).|
   | **Senha** | Qualquer senha válida. | Sua senha deve ter pelo menos oito caracteres e deve conter caracteres de três das Olá categorias a seguir: caracteres em letras maiusculas, letras minúsculas, números e caracteres não alfanuméricos. |
   | **Localidade** | Qualquer local válido. | Para obter mais informações sobre as regiões, consulte [Regiões do Azure](https://azure.microsoft.com/regions/). |
   ||||

   ![criar database-server](../articles/sql-database/media/sql-database-design-first-database/create-database-server.png)

5. Clique em **Selecionar**.

6. Clique em **preço** toospecify Olá desempenho e da camada de nível de serviço para o novo banco de dados. Para este tutorial, selecione **20 DTUs** e **250** GB de armazenamento.

   ![Criar database-s1](../articles/sql-database/media/sql-database-design-first-database/create-empty-database-pricing-tier.png)

7. Clique em **Aplicar**.  

8. Selecione um **agrupamento** para banco de dados em branco (para este tutorial, usar o valor padrão Olá) hello. Para obter mais informações sobre agrupamentos, consulte [Agrupamentos](https://docs.microsoft.com/sql/t-sql/statements/collations)

9. Clique em **criar** banco de dados do tooprovision hello. Provisionamento leva sobre toocomplete um minuto e meia. 

10. Na barra de ferramentas hello, clique em **notificações** toomonitor processo de implantação de saudação.

   ![notificação](../articles/sql-database/media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule-using-hello-azure-portal"></a>Criar uma regra de firewall de nível de servidor usando Olá portal do Azure

Olá serviço de banco de dados SQL cria um firewall no nível de servidor de saudação. Inicialmente firewall Olá impede ferramentas externas e aplicativos de conexão de servidor toohello ou tooany bancos de dados no servidor de saudação. Conexões são permitidas depois que uma regra de firewall é criada tooopen endereços IP específicos. Siga estas etapas toocreate um [regra de firewall de nível de servidor de banco de dados SQL](../articles/sql-database/sql-database-firewall-configure.md) para o endereço IP e a conectividade externa tooenable através do firewall do banco de dados SQL Olá para seu endereço de IP do cliente. 


> [!NOTE]
> O Banco de Dados SQL do Azure se comunica pela porta 1433. Você pode conectar tooSQL banco de dados somente depois que o firewall de saudação da sua rede permite o tráfego de saída pela porta 1433.


1. Após a conclusão da implantação hello, clique em **bancos de dados SQL** no menu esquerdo hello e clique **mySampleDatabase** em Olá **bancos de dados SQL** página. Olá, página de visão geral para o banco de dados abre, mostrando a você Olá totalmente qualificado nome do servidor (como **mynewserver20170313.database.windows.net**) e fornece opções de configuração adicional. Copie esse nome totalmente qualificado do servidor para um uso posterior.

   > [!IMPORTANT]
   > É necessário que este servidor de tooyour de tooconnect de nome totalmente qualificado do servidor e seus bancos de dados em início rápido subsequente.
   > 

   ![nome do servidor](../articles/sql-database/media/sql-database-get-started-portal/server-name.png) 

2. Clique em **definir o firewall do servidor** na barra de ferramentas Olá conforme mostrado na imagem anterior hello. Olá **configurações de Firewall** página para o servidor de banco de dados SQL Olá é aberta. 

   ![regra de firewall do servidor](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png) 


3. Clique em **Adicionar IP do cliente** em Olá barra de ferramentas tooadd seu atual endereço IP tooa nova regra de firewall. Uma regra de firewall pode abrir a porta 1433 para um único endereço IP ou um intervalo de endereços IP.

4. Clique em **Salvar**. Uma regra de firewall de nível de servidor é criada para seu endereço IP atual, abrir a porta 1433 no servidor lógico hello.

   ![definir regra de firewall do servidor](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. Clique em **Okey** e, em seguida, feche Olá **configurações de Firewall** página.

Agora você pode conectar o servidor de banco de dados do Azure SQL toohello e seus bancos de dados usando uma ferramenta como o SQL Server Management Studio (SSMS). conexão Hello está usando esse endereço IP e usa a conta de administrador de servidor de saudação criada anteriormente.


> [!IMPORTANT]
> Por padrão, o acesso através do firewall do banco de dados SQL hello está habilitado para todos os serviços do Azure. Clique em **OFF** em toodisable essa página para todos os serviços do Azure.


## <a name="get-connection-string-values-using-hello-azure-portal"></a>Obter valores de cadeia de caracteres de conexão usando Olá portal do Azure

Obter nome de totalmente qualificado do servidor de saudação de seu servidor de banco de dados do Azure SQL Olá portal do Azure. Você usa Olá totalmente qualificado nome tooconnect tooyour server usando o SQL Server Management Studio.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com/).

2. Selecione **bancos de dados SQL** no menu esquerdo do hello e clique em seu banco de dados em Olá **bancos de dados SQL** página. 

3. Em Olá **Essentials** painel Olá página do portal do Azure para seu banco de dados, localize e copie Olá **nome do servidor**.

   ![informações da conexão](../articles/sql-database/media/sql-database-get-started-portal/server-name.png) 
