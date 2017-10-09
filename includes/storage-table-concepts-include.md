## <a name="what-is-table-storage"></a>O que é o Armazenamento de Tabelas
O Armazenamento de Tabelas do Microsoft Azure armazena grandes quantidades de dados estruturados. serviço de saudação é um repositório de dados NoSQL que aceita autenticado chamadas dentro e fora de saudação nuvem do Azure. As tabelas do Azure são ideais para armazenar dados estruturados não relacionais. Os usos comuns do armazenamento de tabelas incluem:

* Armazenamento de TBs de dados estruturados capazes de atender a aplicativos de dimensionamento da Web
* Armazenando conjuntos de dados que não exigem junções complexas, chaves estrangeiras ou procedimentos armazenados e que podem ser desnormalizados para acesso rápido
* Consulta rápida de dados usando um índice clusterizado
* Acessando dados usando o protocolo OData de saudação e consultas LINQ com bibliotecas .NET do WCF Data Service

Você pode usar a tabela armazenamento toostore e consultar grandes conjuntos de dados estruturados e não relacionais e suas tabelas dimensionará como aumento de demanda.

## <a name="table-storage-concepts"></a>Conceitos de armazenamento de tabelas
Armazenamento de tabela contém Olá componentes a seguir:

![Diagrama de componentes do Armazenamento de Tabelas][Table1]

* **Formato da URL:** o código aborda as tabelas em uma conta usando o formato desse endereço:   
  http://`<storage account>`.table.core.windows.net/`<table>`  
  
  Você pode abordar a tabelas do Azure diretamente usando esse endereço com hello protocolo OData. Para saber mais, veja [OData.org][OData.org].
* **Conta de armazenamento:** todos os acessos tooAzure armazenamento é feito por meio de uma conta de armazenamento. Consulte [Escalabilidade e Metas de Desempenho do Armazenamento do Azure](../articles/storage/common/storage-scalability-targets.md) para obter detalhes sobre a capacidade da conta de armazenamento.
* **Tabela**: uma tabela é uma coleção de entidades. As tabelas não impõem um esquema nas entidades, o que significa que uma única tabela pode conter entidades com diferentes conjuntos de propriedades. número de saudação de tabelas que uma conta de armazenamento pode conter é limitado somente pelo limite de capacidade da conta de armazenamento hello.
* **Entidade**: uma entidade é um conjunto de propriedades de linha de banco de dados tooa semelhante. Uma entidade pode ser a too1MB em tamanho.
* **Propriedades**: uma propriedade é um par de nome-valor. Cada entidade pode incluir os dados de toostore propriedades too252. Cada entidade possui também três propriedades do sistema que especificam uma chave de partição, uma chave de linha e um carimbo de hora. Entidades com hello a mesma chave de partição pode ser consultado com mais rapidez e inseridos/atualizados em operações atômicas. A chave de linha de uma entidade é seu identificador exclusivo dentro de uma partição.

Para obter detalhes sobre a nomeação de tabelas e propriedades, consulte [Olá Noções básicas sobre modelo de dados do serviço de tabela](/rest/api/storageservices/Understanding-the-Table-Service-Data-Model).

[Table1]: ./media/storage-table-concepts-include/table1.png
[OData.org]: http://www.odata.org/
