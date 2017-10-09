## <a name="specifying-structure-definition-for-rectangular-datasets"></a>Especifica a definição de estrutura para conjuntos de dados retangulares
Olá seção estrutura Olá conjuntos de dados JSON é um **opcional** seção retangulares tabelas (com linhas e colunas) e contém uma coleção de colunas da tabela de saudação. Você usará a seção de estrutura de saudação para qualquer contendo informações de tipo para conversões de tipo ou fazer mapeamentos de coluna. Olá seções a seguir descreve esses recursos em detalhes. 

Cada coluna contém Olá propriedades a seguir:

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| name |Nome da coluna de saudação. |Sim |
| type |Tipo de dados da coluna de saudação. Consulte a seção de conversões de tipo abaixo para obter mais detalhes sobre quando deve você especificar informações de tipo |Não |
| culture |.NET com base em cultura toobe usado quando o tipo é especificado e é o tipo .NET Datetime ou Datetimeoffset. O padrão é "en-us". |Não |
| formato |Formatar toobe de cadeia de caracteres usada quando o tipo é especificado e é o tipo .NET Datetime ou Datetimeoffset. |Não |

Olá exemplo a seguir mostra a saudação estrutura seção JSON para uma tabela que tem três colunas userid, nome e lastlogindate.

```json
"structure": 
[
    { "name": "userid"},
    { "name": "name"},
    { "name": "lastlogindate"}
],
```

Use Olá diretrizes a seguir para quando informações de "structure" tooinclude e quais tooinclude em Olá **estrutura** seção.

* **Para fontes de dados estruturados** que armazenam informações de esquema e o tipo de dados junto com hello dados em si (fontes como o SQL Server, Oracle, tabelas etc.), você deve especificar a seção de "estrutura" hello somente se você quiser mapeamento de coluna de específicos são colunas toospecific no coletor e os nomes de colunas de origem não Olá mesmo (consulte detalhes na seção de mapeamento de coluna abaixo). 
  
    Conforme mencionado acima, as informações de tipo de saudação serão opcionais na seção "estrutura". Para fontes estruturados, informações de tipo já estão disponíveis como parte da definição de conjunto de dados no repositório de dados Olá, portanto você não deve incluir informações de tipo quando você inclui uma seção de "structure" hello.
* **Para o esquema de fontes de dados de leitura (especificamente BLOBs do Azure)** você pode escolher dados toostore sem armazenar qualquer informação de tipo ou esquema com dados saudação. Para esses tipos de fontes de dados, você deve incluir "structure" no hello 2 casos a seguir:
  * Você deseja que o mapeamento de coluna toodo.
  * Quando Olá conjunto de dados é uma fonte em uma atividade de cópia, você pode fornecer informações de tipo em "structure" e fábrica de dados usará essas informações de tipo para tipos de toonative de conversão para o coletor de saudação. Consulte [mover tooand de dados de Blob do Azure](../articles/data-factory/data-factory-azure-blob-connector.md) artigo para obter mais informações.

### <a name="supported-net-based-types"></a>Tipos baseados em .NET para os quais há suporte
Valores de tipo para fornecer informações de tipo em "structure" para o esquema de fontes de dados de leitura, como BLOBs do Azure com base em dados fábrica dá suporte a saudação seguir .NET compatível com CLS.

* Int16
* Int32 
* Int64
* Single
* Duplo
* Decimal
* Byte[]
* Bool
* Cadeia de caracteres 
* Guid
* Datetime
* Datetimeoffset
* Timespan 

Para Datetime e Datetimeoffset você também pode especificar "culture" & toofacilitate da cadeia de caracteres "format" análise de sua cadeia de caracteres de data e hora personalizada. Consulte o exemplo de conversão de tipo abaixo.

