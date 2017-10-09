1. Em uma nova janela, entrar toohello [portal do Azure](https://portal.azure.com/).
2. No painel esquerdo do hello, clique em **novo**, clique em **bancos de dados**e, em seguida, em **o banco de dados do Azure Cosmos**, clique em **criar**.
   
   ![Painel Bancos de Dados do portal do Azure](./media/cosmos-db-create-dbaccount-graph/create-nosql-db-databases-json-tutorial-1.png)

3. Em Olá **nova conta** folha, especificar a configuração de saudação que você deseja para esta conta de banco de dados do Azure Cosmos. 

    Com o Azure Cosmos DB, você pode escolher um dos quatro modelos de programação: Gremlin (gráfico), MongoDB, SQL (DocumentDB) e Tabela (chave-valor), cada um exigindo uma conta separada.
       
    Neste artigo de início rápido, podemos programações Olá API do Graph, portanto escolha **Gremlin (gráfico)** como preencher o formulário de saudação. Se você tiver dados de documento de um aplicativo de catálogo, dados de chave/valor (tabela) ou dados migrados de um aplicativo do MongoDB, perceba que o Azure Cosmos DB pode fornecer uma plataforma de serviço de banco de dados altamente disponível, distribuída globalmente para todos os aplicativos críticos.

    Preencha os campos de saudação em Olá **nova conta** folha, usando informações Olá Olá seguinte captura de tela de como um guia - seus valores podem ser diferentes valores hello na captura de tela de saudação.
 
    ![blade de nova conta Olá para o banco de dados do Azure Cosmos](./media/cosmos-db-create-dbaccount-graph/create-nosql-db-databases-json-tutorial-2.png)

    Configuração|Valor sugerido|Descrição
    ---|---|---
    ID|*Valor exclusivo*|Um nome exclusivo que identifica essa conta do Azure Cosmos DB. Porque *documents.azure.com* é acrescentado toohello ID da ID que você forneça toocreate seu URI, use um exclusivo mas identificável. Olá ID deve conter apenas letras minúsculas, números e caracteres de hífen (-) hello e ele deve conter de 3 caracteres too50.
    API|Gremlin (gráfico)|Podemos fazer programações Olá [API do Graph](../articles/cosmos-db/graph-introduction.md) posteriormente neste artigo.|
    Assinatura|*Sua assinatura*|Olá assinatura do Azure que você deseja toouse para esta conta de banco de dados do Azure Cosmos. 
    Grupo de recursos|*Olá mesmo valor ID*|Olá novo recurso nome de grupo para sua conta. Para simplificar, você pode usar o hello mesmo nome como sua ID. 
    Local|*Olá região mais próxima tooyour os usuários*|Olá localização geográfica na qual toohost sua conta de banco de dados do Azure Cosmos. Escolha o local de saudação usuários mais próximos de tooyour toogive-los Olá toohello acessar os dados mais rápidos.

4. Clique em **criar** toocreate conta de saudação.
5. Na barra de ferramentas superior hello, clique em Olá **notificações** ícone ![ícone de notificação de saudação](./media/cosmos-db-create-dbaccount-graph/notification-icon.png) toomonitor processo de implantação de saudação.

    ![Olá painel notificações do portal do Azure](./media/cosmos-db-create-dbaccount-graph/notification.png)

6.  Quando a janela de notificações de saudação indica a janela de notificação Olá implantação Olá bem-sucedido, feche e abra Olá nova conta de saudação **todos os recursos** bloco Olá painel. 

    ![Conta do DocumentDB em Olá que todos os recursos de bloco](./media/cosmos-db-create-dbaccount-graph/azure-documentdb-all-resources.png)
