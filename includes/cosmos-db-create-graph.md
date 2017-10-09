Agora você pode usar a ferramenta de Gerenciador de dados de saudação em Olá toocreate portal do Azure um banco de dados do gráfico. 

1. No hello portal do Azure, no menu de navegação à esquerda do hello, clique em **Gerenciador de dados (visualização)**. 
2. Em Olá **Gerenciador de dados (visualização)** folha, clique em **novo gráfico**, em seguida, preencha a página hello usando Olá informações a seguir.

    ![Gerenciador de dados no hello portal do Azure](./media/cosmos-db-create-graph/azure-cosmosdb-data-explorer.png)

    Configuração|Valor sugerido|Descrição
    ---|---|---
    ID do banco de dados|banco de dados de exemplo|ID de saudação do novo banco de dados. Os nomes de banco de dados devem ter entre um e 255 caracteres e não podem conter `/ \ # ?` nem espaços à direita.
    Id do Gráfico|gráfico de exemplo|ID de saudação para seu novo gráfico. Nomes de gráfico tem Olá mesmo caractere requisitos como ids de banco de dados.
    Capacidade de Armazenamento| 10 GB|Deixe o valor padrão de saudação. Isso é a capacidade de armazenamento de saudação do banco de dados de saudação.
    Taxa de transferência|400 RUs|Deixe o valor padrão de saudação. Você pode dimensionar a taxa de transferência hello mais tarde se você quiser tooreduce latência.
    Chave de partição|/userid|Uma chave de partição que distribui dados uniformemente tooeach partição. Gráfico selecionando Olá correto de chave de partição é importante na criação de um alto desempenho, leia mais sobre ele na [Projetando para o particionamento](../articles/cosmos-db/partition-data.md#designing-for-partitioning).

3. Depois de preencher o formulário Olá, clique em **Okey**.
