Agora você pode usar a coleção e ferramenta Data Explorer Olá Olá toocreate portal do Azure um banco de dados. 

1. No hello portal do Azure, no menu de navegação à esquerda do hello, clique em **Gerenciador de dados (visualização)**. 

2. Em Olá **Gerenciador de dados (visualização)** folha, clique em **nova coleção**e, em seguida, fornecer Olá informações a seguir:

    ![Olá folha de dados Explorer portal do Azure](./media/cosmos-db-create-collection/azure-cosmosdb-data-explorer.png)

    Configuração|Valor sugerido|Descrição
    ---|---|---
    ID do banco de dados|Tarefas|nome de saudação para seu novo banco de dados. Os nomes de banco de dados devem conter de 1 a 255 caracteres e não podem conter /, \\, #, ?, ou um espaço à direita.
    ID da coleção|Itens|nome da saudação para a nova coleção. Nomes de coleção tem Olá mesmo requisitos de IDs de banco de dados de caractere.
    Capacidade de armazenamento| Fixo (10 GB)|Use o valor padrão de saudação. Esse valor é a capacidade de armazenamento de saudação do banco de dados de saudação.
    Taxa de transferência|400 RU|Use o valor padrão de saudação. Se você quiser tooreduce latência, você pode dimensionar a taxa de transferência hello mais tarde.
    Chave de partição|/category|Uma chave de partição que distribui dados uniformemente tooeach partição. Chave de partição correta de saudação selecionando é importante na criação de uma coleção de alto desempenho. mais, consulte toolearn [Projetando para o particionamento](../articles/cosmos-db/partition-data.md#designing-for-partitioning).    
3. Depois de preencher o formulário de saudação, clique em **Okey**.

Dados Explorer mostra Olá novo banco de dados e coleção. 
