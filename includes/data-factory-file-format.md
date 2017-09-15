## <a name="specifying-formats"></a><span data-ttu-id="14ebc-101">Especificando formatos</span><span class="sxs-lookup"><span data-stu-id="14ebc-101">Specifying formats</span></span>
<span data-ttu-id="14ebc-102">O Azure Data Factory dá suporte aos tipos de formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="14ebc-102">Azure Data Factory supports the following format types:</span></span>

* [<span data-ttu-id="14ebc-103">Formato de texto</span><span class="sxs-lookup"><span data-stu-id="14ebc-103">Text Format</span></span>](#specifying-textformat)
* [<span data-ttu-id="14ebc-104">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="14ebc-104">JSON Format</span></span>](#specifying-jsonformat)
* [<span data-ttu-id="14ebc-105">Formato Avro</span><span class="sxs-lookup"><span data-stu-id="14ebc-105">Avro Format</span></span>](#specifying-avroformat)
* [<span data-ttu-id="14ebc-106">Formato ORC</span><span class="sxs-lookup"><span data-stu-id="14ebc-106">ORC Format</span></span>](#specifying-orcformat)
* [<span data-ttu-id="14ebc-107">Formato de Parquet</span><span class="sxs-lookup"><span data-stu-id="14ebc-107">Parquet Format</span></span>](#specifying-parquetformat)

### <a name="specifying-textformat"></a><span data-ttu-id="14ebc-108">Especificando TextFormat</span><span class="sxs-lookup"><span data-stu-id="14ebc-108">Specifying TextFormat</span></span>
<span data-ttu-id="14ebc-109">Se você quiser analisar os arquivos de texto ou gravar os dados no formato de texto, defina a propriedade `format` `type` como **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="14ebc-109">If you want to parse the text files or write the data in text format, set the `format` `type` property to **TextFormat**.</span></span> <span data-ttu-id="14ebc-110">Você também pode especificar as seguintes propriedades **opcionais** na seção `format`.</span><span class="sxs-lookup"><span data-stu-id="14ebc-110">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="14ebc-111">Veja a seção [Exemplo de TextFormat](#textformat-example) sobre a configuração.</span><span class="sxs-lookup"><span data-stu-id="14ebc-111">See [TextFormat example](#textformat-example) section on how to configure.</span></span>

| <span data-ttu-id="14ebc-112">Propriedade</span><span class="sxs-lookup"><span data-stu-id="14ebc-112">Property</span></span> | <span data-ttu-id="14ebc-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="14ebc-113">Description</span></span> | <span data-ttu-id="14ebc-114">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="14ebc-114">Allowed values</span></span> | <span data-ttu-id="14ebc-115">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="14ebc-115">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="14ebc-116">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="14ebc-116">columnDelimiter</span></span> |<span data-ttu-id="14ebc-117">O caractere usado para separar as colunas em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="14ebc-117">The character used to separate columns in a file.</span></span> <span data-ttu-id="14ebc-118">Você pode considerar o uso de um caractere raro não imprimível que provavelmente não existe nos dados: por exemplo, especifique "\u0001" que representa o Início do Título (SOH).</span><span class="sxs-lookup"><span data-stu-id="14ebc-118">You can consider to use a rare unprintable char which not likely exists in your data: e.g. specify "\u0001" which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="14ebc-119">Somente um caractere é permitido.</span><span class="sxs-lookup"><span data-stu-id="14ebc-119">Only one character is allowed.</span></span> <span data-ttu-id="14ebc-120">O valor **padrão** é **vírgula (‘,’)**.</span><span class="sxs-lookup"><span data-stu-id="14ebc-120">The **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="14ebc-121">Para usar um caractere Unicode, consulte [Caracteres Unicode](https://en.wikipedia.org/wiki/List_of_Unicode_characters) para obter o código correspondente.</span><span class="sxs-lookup"><span data-stu-id="14ebc-121">To use an Unicode character, refer to [Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) to get the corresponding code for it.</span></span> |<span data-ttu-id="14ebc-122">Não</span><span class="sxs-lookup"><span data-stu-id="14ebc-122">No</span></span> |
| <span data-ttu-id="14ebc-123">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="14ebc-123">rowDelimiter</span></span> |<span data-ttu-id="14ebc-124">O caractere usado para separar as linhas em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="14ebc-124">The character used to separate rows in a file.</span></span> |<span data-ttu-id="14ebc-125">Somente um caractere é permitido.</span><span class="sxs-lookup"><span data-stu-id="14ebc-125">Only one character is allowed.</span></span> <span data-ttu-id="14ebc-126">O valor **padrão** é um dos seguintes valores na leitura: **["\r\n", "\r" e "\n"]** e **"\r\n"** na gravação.</span><span class="sxs-lookup"><span data-stu-id="14ebc-126">The **default** value is any of the following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="14ebc-127">Não</span><span class="sxs-lookup"><span data-stu-id="14ebc-127">No</span></span> |
| <span data-ttu-id="14ebc-128">escapeChar</span><span class="sxs-lookup"><span data-stu-id="14ebc-128">escapeChar</span></span> |<span data-ttu-id="14ebc-129">O caractere especial usado como escape do delimitador de coluna no conteúdo do arquivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="14ebc-129">The special character used to escape a column delimiter in the content of input file.</span></span> <br/><br/><span data-ttu-id="14ebc-130">Não é possível especificar ambos escapeChar e quoteChar para uma tabela.</span><span class="sxs-lookup"><span data-stu-id="14ebc-130">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="14ebc-131">Somente um caractere é permitido.</span><span class="sxs-lookup"><span data-stu-id="14ebc-131">Only one character is allowed.</span></span> <span data-ttu-id="14ebc-132">Nenhum valor padrão.</span><span class="sxs-lookup"><span data-stu-id="14ebc-132">No default value.</span></span> <br/><br/><span data-ttu-id="14ebc-133">Por exemplo, se tiver a vírgula (,) como o delimitador de coluna, mas quiser ter o caractere de vírgula no texto (exemplo: "Hello, world"), você poderá definir '$' como o caractere de escape e usar a cadeia de caracteres "Hello$, world" na fonte.</span><span class="sxs-lookup"><span data-stu-id="14ebc-133">Example: if you have comma (',') as the column delimiter but you want to have the comma character in the text (example: "Hello, world"), you can define ‘$’ as the escape character and use string "Hello$, world" in the source.</span></span> |<span data-ttu-id="14ebc-134">Não</span><span class="sxs-lookup"><span data-stu-id="14ebc-134">No</span></span> |
| <span data-ttu-id="14ebc-135">quoteChar</span><span class="sxs-lookup"><span data-stu-id="14ebc-135">quoteChar</span></span> |<span data-ttu-id="14ebc-136">O caractere usado para citar um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="14ebc-136">The character used to quote a string value.</span></span> <span data-ttu-id="14ebc-137">Os delimitadores de linha e coluna dentro dos caracteres de aspas seriam tratados como parte do valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="14ebc-137">The column and row delimiters inside the quote characters would be treated as part of the string value.</span></span> <span data-ttu-id="14ebc-138">Essa propriedade é aplicável a ambos os conjuntos de dados de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="14ebc-138">This property is applicable to both input and output datasets.</span></span><br/><br/><span data-ttu-id="14ebc-139">Não é possível especificar ambos escapeChar e quoteChar para uma tabela.</span><span class="sxs-lookup"><span data-stu-id="14ebc-139">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="14ebc-140">Somente um caractere é permitido.</span><span class="sxs-lookup"><span data-stu-id="14ebc-140">Only one character is allowed.</span></span> <span data-ttu-id="14ebc-141">Nenhum valor padrão.</span><span class="sxs-lookup"><span data-stu-id="14ebc-141">No default value.</span></span> <br/><br/><span data-ttu-id="14ebc-142">Por exemplo, se tiver a vírgula (,) como o delimitador de coluna, mas quiser ter o caractere de vírgula no texto (exemplo: <Hello, world>), você poderá definir " (aspas duplas) como o caractere de citação e usar a cadeia de caracteres "Hello, world" na origem.</span><span class="sxs-lookup"><span data-stu-id="14ebc-142">For example, if you have comma (',') as the column delimiter but you want to have comma character in the text (example: <Hello, world>), you can define " (double quote) as the quote character and use the string "Hello, world" in the source.</span></span> |<span data-ttu-id="14ebc-143">Não</span><span class="sxs-lookup"><span data-stu-id="14ebc-143">No</span></span> |
| <span data-ttu-id="14ebc-144">nullValue</span><span class="sxs-lookup"><span data-stu-id="14ebc-144">nullValue</span></span> |<span data-ttu-id="14ebc-145">Um ou mais caracteres usados para representar um valor nulo.</span><span class="sxs-lookup"><span data-stu-id="14ebc-145">One or more characters used to represent a null value.</span></span> |<span data-ttu-id="14ebc-146">Um ou mais caracteres.</span><span class="sxs-lookup"><span data-stu-id="14ebc-146">One or more characters.</span></span> <span data-ttu-id="14ebc-147">Os valores **padrão** são **"\N" e "NULL"** na leitura e **"\N"** na gravação.</span><span class="sxs-lookup"><span data-stu-id="14ebc-147">The **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="14ebc-148">Não</span><span class="sxs-lookup"><span data-stu-id="14ebc-148">No</span></span> |
| <span data-ttu-id="14ebc-149">encodingName</span><span class="sxs-lookup"><span data-stu-id="14ebc-149">encodingName</span></span> |<span data-ttu-id="14ebc-150">Especifique o nome de codificação.</span><span class="sxs-lookup"><span data-stu-id="14ebc-150">Specify the encoding name.</span></span> |<span data-ttu-id="14ebc-151">Um nomes de codificação válido.</span><span class="sxs-lookup"><span data-stu-id="14ebc-151">A valid encoding name.</span></span> <span data-ttu-id="14ebc-152">Consulte [Propriedade Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="14ebc-152">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="14ebc-153">Por exemplo: windows-1250 ou shift_jis.</span><span class="sxs-lookup"><span data-stu-id="14ebc-153">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="14ebc-154">O valor **padrão** é **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="14ebc-154">The **default** value is **UTF-8**.</span></span> |<span data-ttu-id="14ebc-155">Não</span><span class="sxs-lookup"><span data-stu-id="14ebc-155">No</span></span> |
| <span data-ttu-id="14ebc-156">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="14ebc-156">firstRowAsHeader</span></span> |<span data-ttu-id="14ebc-157">Especifica se a primeira linha será considerada como cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="14ebc-157">Specifies whether to consider the first row as a header.</span></span> <span data-ttu-id="14ebc-158">Para um conjunto de dados de entrada, o Data Factory lê a primeira linha como cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="14ebc-158">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="14ebc-159">Para um conjunto de dados de saída, o Data Factory lê a primeira linha como cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="14ebc-159">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="14ebc-160">Veja [Cenários para usar o `firstRowAsHeader` e o `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) para cenários de exemplo.</span><span class="sxs-lookup"><span data-stu-id="14ebc-160">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="14ebc-161">True </span><span class="sxs-lookup"><span data-stu-id="14ebc-161">True</span></span><br/><span data-ttu-id="14ebc-162">**False (padrão)**</span><span class="sxs-lookup"><span data-stu-id="14ebc-162">**False (default)**</span></span> |<span data-ttu-id="14ebc-163">Não</span><span class="sxs-lookup"><span data-stu-id="14ebc-163">No</span></span> |
| <span data-ttu-id="14ebc-164">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="14ebc-164">skipLineCount</span></span> |<span data-ttu-id="14ebc-165">Indica o número de linhas a serem ignoradas ao ler dados de arquivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="14ebc-165">Indicates the number of rows to skip when reading data from input files.</span></span> <span data-ttu-id="14ebc-166">Se skipLineCount e firstRowAsHeader forem especificados, as linhas serão ignoradas pela primeira vez e, em seguida, as informações de cabeçalho serão lidas do arquivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="14ebc-166">If both skipLineCount and firstRowAsHeader are specified, the lines are skipped first and then the header information is read from the input file.</span></span> <br/><br/><span data-ttu-id="14ebc-167">Veja [Cenários para usar o `firstRowAsHeader` e o `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) para cenários de exemplo.</span><span class="sxs-lookup"><span data-stu-id="14ebc-167">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="14ebc-168">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="14ebc-168">Integer</span></span> |<span data-ttu-id="14ebc-169">Não</span><span class="sxs-lookup"><span data-stu-id="14ebc-169">No</span></span> |
| <span data-ttu-id="14ebc-170">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="14ebc-170">treatEmptyAsNull</span></span> |<span data-ttu-id="14ebc-171">Especifica se uma cadeia de caracteres nula ou vazia será ou não tratada como um valor nulo ao ler dados de um arquivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="14ebc-171">Specifies whether to treat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="14ebc-172">**True (padrão)**</span><span class="sxs-lookup"><span data-stu-id="14ebc-172">**True (default)**</span></span><br/><span data-ttu-id="14ebc-173">Falso</span><span class="sxs-lookup"><span data-stu-id="14ebc-173">False</span></span> |<span data-ttu-id="14ebc-174">Não</span><span class="sxs-lookup"><span data-stu-id="14ebc-174">No</span></span> |

#### <a name="textformat-example"></a><span data-ttu-id="14ebc-175">Exemplo de TextFormat</span><span class="sxs-lookup"><span data-stu-id="14ebc-175">TextFormat example</span></span>
<span data-ttu-id="14ebc-176">O exemplo a seguir mostra algumas das propriedades de formato para TextFormat.</span><span class="sxs-lookup"><span data-stu-id="14ebc-176">The following sample shows some of the format properties for TextFormat.</span></span>

```json
"typeProperties":
{
    "folderPath": "mycontainer/myfolder",
    "fileName": "myblobname",
    "format":
    {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";",
        "quoteChar": "\"",
        "NullValue": "NaN",
        "firstRowAsHeader": true,
        "skipLineCount": 0,
        "treatEmptyAsNull": true
    }
},
```

<span data-ttu-id="14ebc-177">Para usar um `escapeChar` em vez de `quoteChar`, substitua a linha com `quoteChar` por este escapeChar:</span><span class="sxs-lookup"><span data-stu-id="14ebc-177">To use an `escapeChar` instead of `quoteChar`, replace the line with `quoteChar` with the following escapeChar:</span></span>

```json
"escapeChar": "$",
```

#### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="14ebc-178">Cenários de uso de firstRowAsHeader e skipLineCount</span><span class="sxs-lookup"><span data-stu-id="14ebc-178">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="14ebc-179">Você está copiando de uma fonte que não é de arquivo para um arquivo de texto e deseja adicionar uma linha de cabeçalho que contém os metadados de esquema (por exemplo: esquema SQL).</span><span class="sxs-lookup"><span data-stu-id="14ebc-179">You are copying from a non-file source to a text file and would like to add a header line containing the schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="14ebc-180">Especifique `firstRowAsHeader` como true no conjunto de dados de saída para esse cenário.</span><span class="sxs-lookup"><span data-stu-id="14ebc-180">Specify `firstRowAsHeader` as true in the output dataset for this scenario.</span></span>
* <span data-ttu-id="14ebc-181">Você está copiando de um arquivo de texto contendo uma linha de cabeçalho para um coletor que não é em arquivo e gostaria de remover essa linha.</span><span class="sxs-lookup"><span data-stu-id="14ebc-181">You are copying from a text file containing a header line to a non-file sink and would like to drop that line.</span></span> <span data-ttu-id="14ebc-182">Especifique `firstRowAsHeader` como true no conjunto de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="14ebc-182">Specify `firstRowAsHeader` as true in the input dataset.</span></span>
* <span data-ttu-id="14ebc-183">Você está copiando de um arquivo de texto e deseja ignorar algumas linhas no início que não são informações de dados nem de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="14ebc-183">You are copying from a text file and want to skip a few lines at the beginning that contain no data or header information.</span></span> <span data-ttu-id="14ebc-184">Especifique `skipLineCount` para indicar o número de linhas a serem ignoradas.</span><span class="sxs-lookup"><span data-stu-id="14ebc-184">Specify `skipLineCount` to indicate the number of lines to be skipped.</span></span> <span data-ttu-id="14ebc-185">Se o restante do arquivo contiver uma linha de cabeçalho, você também poderá especificar `firstRowAsHeader`.</span><span class="sxs-lookup"><span data-stu-id="14ebc-185">If the rest of the file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="14ebc-186">Se `skipLineCount` e `firstRowAsHeader` forem especificados, as linhas serão ignoradas pela primeira vez e, em seguida, as informações de cabeçalho serão lidas do arquivo de entrada</span><span class="sxs-lookup"><span data-stu-id="14ebc-186">If both `skipLineCount` and `firstRowAsHeader` are specified, the lines are skipped first and then the header information is read from the input file</span></span>

### <a name="specifying-jsonformat"></a><span data-ttu-id="14ebc-187">Especificando JsonFormat</span><span class="sxs-lookup"><span data-stu-id="14ebc-187">Specifying JsonFormat</span></span>
<span data-ttu-id="14ebc-188">Para **importar/exportar arquivos JSON como estão de/para o Azure Cosmos DB**, veja a seção [Importar/exportar documentos JSON](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) no conector do Azure Cosmos DB com detalhes.</span><span class="sxs-lookup"><span data-stu-id="14ebc-188">To **import/export JSON files as-is into/from Azure Cosmos DB**, see [Import/export JSON documents](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) section in the Azure Cosmos DB connector with details.</span></span>

<span data-ttu-id="14ebc-189">Se você quiser analisar os arquivos de JSON ou gravar os dados no formato JSON, defina a propriedade `format` `type` como **JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="14ebc-189">If you want to parse the JSON files or write the data in JSON format, set the `format` `type` property to **JsonFormat**.</span></span> <span data-ttu-id="14ebc-190">Você também pode especificar as seguintes propriedades **opcionais** na seção `format`.</span><span class="sxs-lookup"><span data-stu-id="14ebc-190">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="14ebc-191">Veja a seção [Exemplo de JsonFormat](#jsonformat-example) sobre como configurar.</span><span class="sxs-lookup"><span data-stu-id="14ebc-191">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span>

| <span data-ttu-id="14ebc-192">Propriedade</span><span class="sxs-lookup"><span data-stu-id="14ebc-192">Property</span></span> | <span data-ttu-id="14ebc-193">Descrição</span><span class="sxs-lookup"><span data-stu-id="14ebc-193">Description</span></span> | <span data-ttu-id="14ebc-194">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="14ebc-194">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="14ebc-195">filePattern</span><span class="sxs-lookup"><span data-stu-id="14ebc-195">filePattern</span></span> |<span data-ttu-id="14ebc-196">Indique o padrão de dados armazenados em cada arquivo JSON.</span><span class="sxs-lookup"><span data-stu-id="14ebc-196">Indicate the pattern of data stored in each JSON file.</span></span> <span data-ttu-id="14ebc-197">Os valores permitidos são: **setOfObjects** e **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="14ebc-197">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="14ebc-198">O valor **padrão** é **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="14ebc-198">The **default** value is **setOfObjects**.</span></span> <span data-ttu-id="14ebc-199">Veja a seção [Padrões de arquivo JSON](#json-file-patterns) para obter detalhes sobre esses padrões.</span><span class="sxs-lookup"><span data-stu-id="14ebc-199">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="14ebc-200">Não</span><span class="sxs-lookup"><span data-stu-id="14ebc-200">No</span></span> |
| <span data-ttu-id="14ebc-201">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="14ebc-201">jsonNodeReference</span></span> | <span data-ttu-id="14ebc-202">Se você quiser fazer uma iteração e extrair dados de objetos dentro de um campo de matriz com o mesmo padrão, especifique o caminho JSON da matriz.</span><span class="sxs-lookup"><span data-stu-id="14ebc-202">If you want to iterate and extract data from the objects inside an array field with the same pattern, specify the JSON path of that array.</span></span> <span data-ttu-id="14ebc-203">Esta propriedade só terá suporte na cópia de dados de arquivos JSON.</span><span class="sxs-lookup"><span data-stu-id="14ebc-203">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="14ebc-204">Não</span><span class="sxs-lookup"><span data-stu-id="14ebc-204">No</span></span> |
| <span data-ttu-id="14ebc-205">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="14ebc-205">jsonPathDefinition</span></span> | <span data-ttu-id="14ebc-206">Especifique a expressão de caminho JSON para cada mapeamento de coluna com um nome de coluna personalizado (iniciar com letra minúscula).</span><span class="sxs-lookup"><span data-stu-id="14ebc-206">Specify the JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="14ebc-207">Esta propriedade só terá suporte na cópia de dados de arquivos JSON, e você pode extrair dados de objeto ou de matriz.</span><span class="sxs-lookup"><span data-stu-id="14ebc-207">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="14ebc-208">Para os campos sob o objeto root, comece com root $; para os campos dentro da matriz escolhidos pela propriedade `jsonNodeReference`, comece do elemento de matriz.</span><span class="sxs-lookup"><span data-stu-id="14ebc-208">For fields under root object, start with root $; for fields inside the array chosen by `jsonNodeReference` property, start from the array element.</span></span> <span data-ttu-id="14ebc-209">Veja a seção [Exemplo de JsonFormat](#jsonformat-example) sobre como configurar.</span><span class="sxs-lookup"><span data-stu-id="14ebc-209">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span> | <span data-ttu-id="14ebc-210">Não</span><span class="sxs-lookup"><span data-stu-id="14ebc-210">No</span></span> |
| <span data-ttu-id="14ebc-211">encodingName</span><span class="sxs-lookup"><span data-stu-id="14ebc-211">encodingName</span></span> |<span data-ttu-id="14ebc-212">Especifique o nome de codificação.</span><span class="sxs-lookup"><span data-stu-id="14ebc-212">Specify the encoding name.</span></span> <span data-ttu-id="14ebc-213">Para obter a lista de nomes de codificação válidos, consulte: Propriedade [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) .</span><span class="sxs-lookup"><span data-stu-id="14ebc-213">For the list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="14ebc-214">Por exemplo: windows-1250 ou shift_jis.</span><span class="sxs-lookup"><span data-stu-id="14ebc-214">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="14ebc-215">O valor **padrão** é **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="14ebc-215">The **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="14ebc-216">Não</span><span class="sxs-lookup"><span data-stu-id="14ebc-216">No</span></span> |
| <span data-ttu-id="14ebc-217">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="14ebc-217">nestingSeparator</span></span> |<span data-ttu-id="14ebc-218">Caractere que é usado para separar os níveis de aninhamento.</span><span class="sxs-lookup"><span data-stu-id="14ebc-218">Character that is used to separate nesting levels.</span></span> <span data-ttu-id="14ebc-219">O valor padrão é '.' (ponto).</span><span class="sxs-lookup"><span data-stu-id="14ebc-219">The default value is '.' (dot).</span></span> |<span data-ttu-id="14ebc-220">Não</span><span class="sxs-lookup"><span data-stu-id="14ebc-220">No</span></span> |

#### <a name="json-file-patterns"></a><span data-ttu-id="14ebc-221">Padrões de arquivo JSON</span><span class="sxs-lookup"><span data-stu-id="14ebc-221">JSON file patterns</span></span>

<span data-ttu-id="14ebc-222">A atividade de cópia pode analisar os padrões dos arquivos JSON abaixo:</span><span class="sxs-lookup"><span data-stu-id="14ebc-222">Copy activity can parse below patterns of JSON files:</span></span>

- <span data-ttu-id="14ebc-223">**Tipo I: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="14ebc-223">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="14ebc-224">Cada arquivo contém um único objeto ou vários objetos concatenados/delimitados por linhas.</span><span class="sxs-lookup"><span data-stu-id="14ebc-224">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="14ebc-225">Quando essa opção é escolhida em um conjunto de dados de saída, a atividade de cópia produz um único arquivo JSON com cada objeto por linha (delimitados por linha).</span><span class="sxs-lookup"><span data-stu-id="14ebc-225">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="14ebc-226">**Exemplo de JSON de objeto único**</span><span class="sxs-lookup"><span data-stu-id="14ebc-226">**single object JSON example**</span></span>

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        ```

    * <span data-ttu-id="14ebc-227">**Exemplo de JSON delimitado por linha**</span><span class="sxs-lookup"><span data-stu-id="14ebc-227">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="14ebc-228">**Exemplo de JSON concatenado**</span><span class="sxs-lookup"><span data-stu-id="14ebc-228">**concatenated JSON example**</span></span>

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        }
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
        ```

- <span data-ttu-id="14ebc-229">**Tipo II: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="14ebc-229">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="14ebc-230">Cada arquivo contém uma matriz de objetos.</span><span class="sxs-lookup"><span data-stu-id="14ebc-230">Each file contains an array of objects.</span></span>

    ```json
    [
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        },
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        },
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
    ]
    ```

#### <a name="jsonformat-example"></a><span data-ttu-id="14ebc-231">Exemplo de JsonFormat</span><span class="sxs-lookup"><span data-stu-id="14ebc-231">JsonFormat example</span></span>

<span data-ttu-id="14ebc-232">**Caso 1: copiar dados de arquivos JSON**</span><span class="sxs-lookup"><span data-stu-id="14ebc-232">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="14ebc-233">Confira abaixo dois tipos de exemplos ao copiar dados de arquivos JSON e os pontos genéricos para observar:</span><span class="sxs-lookup"><span data-stu-id="14ebc-233">See below two types of samples when copying data from JSON files, and the generic points to note:</span></span>

<span data-ttu-id="14ebc-234">**Exemplo 1: extrair dados de objeto e de matriz**</span><span class="sxs-lookup"><span data-stu-id="14ebc-234">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="14ebc-235">Neste exemplo, você espera que um objeto JSON de raiz seja mapeado para um único registro no resultado tabular.</span><span class="sxs-lookup"><span data-stu-id="14ebc-235">In this sample, you expect one root JSON object maps to single record in tabular result.</span></span> <span data-ttu-id="14ebc-236">Se você tiver um arquivo JSON com o seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="14ebc-236">If you have a JSON file with the following content:</span></span>  

```json
{
    "id": "ed0e4960-d9c5-11e6-85dc-d7996816aad3",
    "context": {
        "device": {
            "type": "PC"
        },
        "custom": {
            "dimensions": [
                {
                    "TargetResourceType": "Microsoft.Compute/virtualMachines"
                },
                {
                    "ResourceManagmentProcessRunId": "827f8aaa-ab72-437c-ba48-d8917a7336a3"
                },
                {
                    "OccurrenceTime": "1/13/2017 11:24:37 AM"
                }
            ]
        }
    }
}
```
<span data-ttu-id="14ebc-237">e quiser copiá-lo para uma tabela SQL do Azure no formato a seguir, ao extrair dados dos objetos e da matriz:</span><span class="sxs-lookup"><span data-stu-id="14ebc-237">and you want to copy it into an Azure SQL table in the following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="14ebc-238">ID</span><span class="sxs-lookup"><span data-stu-id="14ebc-238">id</span></span> | <span data-ttu-id="14ebc-239">deviceType</span><span class="sxs-lookup"><span data-stu-id="14ebc-239">deviceType</span></span> | <span data-ttu-id="14ebc-240">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="14ebc-240">targetResourceType</span></span> | <span data-ttu-id="14ebc-241">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="14ebc-241">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="14ebc-242">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="14ebc-242">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="14ebc-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="14ebc-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="14ebc-244">Computador</span><span class="sxs-lookup"><span data-stu-id="14ebc-244">PC</span></span> | <span data-ttu-id="14ebc-245">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="14ebc-245">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="14ebc-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="14ebc-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="14ebc-247">13/01/2017 11:24:37</span><span class="sxs-lookup"><span data-stu-id="14ebc-247">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="14ebc-248">O conjunto de dados de entrada com o tipo **JsonFormat** é definido da seguinte maneira: (definição parcial com apenas as partes relevantes).</span><span class="sxs-lookup"><span data-stu-id="14ebc-248">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="14ebc-249">Mais especificamente:</span><span class="sxs-lookup"><span data-stu-id="14ebc-249">More specifically:</span></span>

- <span data-ttu-id="14ebc-250">A seção `structure` define os nomes de coluna personalizada e o tipo de dados correspondente ao converter em dados tabulares.</span><span class="sxs-lookup"><span data-stu-id="14ebc-250">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="14ebc-251">Esta seção é **opcional**, a menos que você tenha de fazer o mapeamento de colunas.</span><span class="sxs-lookup"><span data-stu-id="14ebc-251">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="14ebc-252">Veja a seção [Especificar a definição de estrutura para conjuntos de dados retangulares](#specifying-structure-definition-for-rectangular-datasets) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="14ebc-252">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="14ebc-253">`jsonPathDefinition` especifica o caminho JSON para cada coluna que indica de onde extrair os dados.</span><span class="sxs-lookup"><span data-stu-id="14ebc-253">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="14ebc-254">Para copiar dados da matriz, você pode usar **array[x].property** para extrair o valor da propriedade do objeto xth, ou você pode usar  **matriz[*].property** para localizar o valor de qualquer objeto que contém essa propriedade.</span><span class="sxs-lookup"><span data-stu-id="14ebc-254">To copy data from array, you can use **array[x].property** to extract value of the given property from the xth object, or you can use **array[*].property** to find the value from any object containing such property.</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "deviceType",
            "type": "String"
        },
        {
            "name": "targetResourceType",
            "type": "String"
        },
        {
            "name": "resourceManagmentProcessRunId",
            "type": "String"
        },
        {
            "name": "occurrenceTime",
            "type": "DateTime"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonPathDefinition": {"id": "$.id", "deviceType": "$.context.device.type", "targetResourceType": "$.context.custom.dimensions[0].TargetResourceType", "resourceManagmentProcessRunId": "$.context.custom.dimensions[1].ResourceManagmentProcessRunId", "occurrenceTime": " $.context.custom.dimensions[2].OccurrenceTime"}      
        }
    }
}
```

<span data-ttu-id="14ebc-255">**Exemplo 2: cruzar aplicar vários objetos com o mesmo padrão da matriz**</span><span class="sxs-lookup"><span data-stu-id="14ebc-255">**Sample 2: cross apply multiple objects with the same pattern from array**</span></span>

<span data-ttu-id="14ebc-256">Neste exemplo, você espera transformar um objeto JSON de raiz em vários registros no resultado tabular.</span><span class="sxs-lookup"><span data-stu-id="14ebc-256">In this sample, you expect to transform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="14ebc-257">Se você tiver um arquivo JSON com o seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="14ebc-257">If you have a JSON file with the following content:</span></span>  

```json
{
    "ordernumber": "01",
    "orderdate": "20170122",
    "orderlines": [
        {
            "prod": "p1",
            "price": 23
        },
        {
            "prod": "p2",
            "price": 13
        },
        {
            "prod": "p3",
            "price": 231
        }
    ],
    "city": [ { "sanmateo": "No 1" } ]
}
```
<span data-ttu-id="14ebc-258">e você deseja copiá-lo para uma tabela do Azure SQL no formato a seguir, ao nivelar os dados de dentro da matriz e fazer uma união cruzada com as informações comuns de root:</span><span class="sxs-lookup"><span data-stu-id="14ebc-258">and you want to copy it into an Azure SQL table in the following format, by flattening the data inside the array and cross join with the common root info:</span></span>

| <span data-ttu-id="14ebc-259">ordernumber</span><span class="sxs-lookup"><span data-stu-id="14ebc-259">ordernumber</span></span> | <span data-ttu-id="14ebc-260">orderdate</span><span class="sxs-lookup"><span data-stu-id="14ebc-260">orderdate</span></span> | <span data-ttu-id="14ebc-261">order_pd</span><span class="sxs-lookup"><span data-stu-id="14ebc-261">order_pd</span></span> | <span data-ttu-id="14ebc-262">order_price</span><span class="sxs-lookup"><span data-stu-id="14ebc-262">order_price</span></span> | <span data-ttu-id="14ebc-263">city</span><span class="sxs-lookup"><span data-stu-id="14ebc-263">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="14ebc-264">01</span><span class="sxs-lookup"><span data-stu-id="14ebc-264">01</span></span> | <span data-ttu-id="14ebc-265">20170122</span><span class="sxs-lookup"><span data-stu-id="14ebc-265">20170122</span></span> | <span data-ttu-id="14ebc-266">P1</span><span class="sxs-lookup"><span data-stu-id="14ebc-266">P1</span></span> | <span data-ttu-id="14ebc-267">23</span><span class="sxs-lookup"><span data-stu-id="14ebc-267">23</span></span> | <span data-ttu-id="14ebc-268">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="14ebc-268">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="14ebc-269">01</span><span class="sxs-lookup"><span data-stu-id="14ebc-269">01</span></span> | <span data-ttu-id="14ebc-270">20170122</span><span class="sxs-lookup"><span data-stu-id="14ebc-270">20170122</span></span> | <span data-ttu-id="14ebc-271">P2</span><span class="sxs-lookup"><span data-stu-id="14ebc-271">P2</span></span> | <span data-ttu-id="14ebc-272">13</span><span class="sxs-lookup"><span data-stu-id="14ebc-272">13</span></span> | <span data-ttu-id="14ebc-273">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="14ebc-273">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="14ebc-274">01</span><span class="sxs-lookup"><span data-stu-id="14ebc-274">01</span></span> | <span data-ttu-id="14ebc-275">20170122</span><span class="sxs-lookup"><span data-stu-id="14ebc-275">20170122</span></span> | <span data-ttu-id="14ebc-276">P3</span><span class="sxs-lookup"><span data-stu-id="14ebc-276">P3</span></span> | <span data-ttu-id="14ebc-277">231</span><span class="sxs-lookup"><span data-stu-id="14ebc-277">231</span></span> | <span data-ttu-id="14ebc-278">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="14ebc-278">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="14ebc-279">O conjunto de dados de entrada com o tipo **JsonFormat** é definido da seguinte maneira: (definição parcial com apenas as partes relevantes).</span><span class="sxs-lookup"><span data-stu-id="14ebc-279">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="14ebc-280">Mais especificamente:</span><span class="sxs-lookup"><span data-stu-id="14ebc-280">More specifically:</span></span>

- <span data-ttu-id="14ebc-281">A seção `structure` define os nomes de coluna personalizada e o tipo de dados correspondente ao converter em dados tabulares.</span><span class="sxs-lookup"><span data-stu-id="14ebc-281">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="14ebc-282">Esta seção é **opcional**, a menos que você tenha de fazer o mapeamento de colunas.</span><span class="sxs-lookup"><span data-stu-id="14ebc-282">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="14ebc-283">Veja a seção [Especificar a definição de estrutura para conjuntos de dados retangulares](#specifying-structure-definition-for-rectangular-datasets) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="14ebc-283">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="14ebc-284">`jsonNodeReference` indica iterar e extrair dados dos objetos com o mesmo padrão em linhas da ordem da **matriz**.</span><span class="sxs-lookup"><span data-stu-id="14ebc-284">`jsonNodeReference` indicates to iterate and extract data from the objects with the same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="14ebc-285">`jsonPathDefinition` especifica o caminho JSON para cada coluna que indica de onde extrair os dados.</span><span class="sxs-lookup"><span data-stu-id="14ebc-285">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="14ebc-286">Neste exemplo, "ordernumber", "orderdate" e "city" estão sob o objeto root com caminho JSON começando com"$.", enquanto "order_pd" e "order_price" são definidos com caminho derivado do elemento de matriz sem "$.".</span><span class="sxs-lookup"><span data-stu-id="14ebc-286">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from the array element without "$.".</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "ordernumber",
            "type": "String"
        },
        {
            "name": "orderdate",
            "type": "String"
        },
        {
            "name": "order_pd",
            "type": "String"
        },
        {
            "name": "order_price",
            "type": "Int64"
        },
        {
            "name": "city",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonNodeReference": "$.orderlines",
            "jsonPathDefinition": {"ordernumber": "$.ordernumber", "orderdate": "$.orderdate", "order_pd": "prod", "order_price": "price", "city": " $.city"}         
        }
    }
}
```

<span data-ttu-id="14ebc-287">**Observe os seguintes pontos:**</span><span class="sxs-lookup"><span data-stu-id="14ebc-287">**Note the following points:**</span></span>

* <span data-ttu-id="14ebc-288">Se `structure` e `jsonPathDefinition` não forem definidos no conjunto de dados do Data Factory, a atividade de cópia detectará o esquema do primeiro objeto e mesclará todo o objeto.</span><span class="sxs-lookup"><span data-stu-id="14ebc-288">If the `structure` and `jsonPathDefinition` are not defined in the Data Factory dataset, the Copy Activity detects the schema from the first object and flatten the whole object.</span></span>
* <span data-ttu-id="14ebc-289">Se a entrada JSON tiver uma matriz por padrão, a atividade de cópia converterá o valor da matriz inteira em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="14ebc-289">If the JSON input has an array, by default the Copy Activity converts the entire array value into a string.</span></span> <span data-ttu-id="14ebc-290">Você pode optar por extrair dados dele usando o `jsonNodeReference` e/ou o `jsonPathDefinition` ou ignorá-lo ao não especificá-lo no `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="14ebc-290">You can choose to extract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="14ebc-291">Se houver nomes duplicados no mesmo nível, a atividade de cópia selecionará o último entre eles.</span><span class="sxs-lookup"><span data-stu-id="14ebc-291">If there are duplicate names at the same level, the Copy Activity picks the last one.</span></span>
* <span data-ttu-id="14ebc-292">Os nomes de propriedade diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="14ebc-292">Property names are case-sensitive.</span></span> <span data-ttu-id="14ebc-293">Duas propriedades com o mesmo nome, mas com maiúsculas e minúsculas diferentes são tratadas como duas propriedades separadas.</span><span class="sxs-lookup"><span data-stu-id="14ebc-293">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="14ebc-294">**Caso 2: gravação de dados no arquivo JSON**</span><span class="sxs-lookup"><span data-stu-id="14ebc-294">**Case 2: Writing data to JSON file**</span></span>

<span data-ttu-id="14ebc-295">Se você tiver a tabela a seguir no Banco de Dados SQL:</span><span class="sxs-lookup"><span data-stu-id="14ebc-295">If you have below table in SQL Database:</span></span>

| <span data-ttu-id="14ebc-296">ID</span><span class="sxs-lookup"><span data-stu-id="14ebc-296">id</span></span> | <span data-ttu-id="14ebc-297">order_date</span><span class="sxs-lookup"><span data-stu-id="14ebc-297">order_date</span></span> | <span data-ttu-id="14ebc-298">order_price</span><span class="sxs-lookup"><span data-stu-id="14ebc-298">order_price</span></span> | <span data-ttu-id="14ebc-299">order_by</span><span class="sxs-lookup"><span data-stu-id="14ebc-299">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="14ebc-300">1</span><span class="sxs-lookup"><span data-stu-id="14ebc-300">1</span></span> | <span data-ttu-id="14ebc-301">20170119</span><span class="sxs-lookup"><span data-stu-id="14ebc-301">20170119</span></span> | <span data-ttu-id="14ebc-302">2000</span><span class="sxs-lookup"><span data-stu-id="14ebc-302">2000</span></span> | <span data-ttu-id="14ebc-303">Davi</span><span class="sxs-lookup"><span data-stu-id="14ebc-303">David</span></span> |
| <span data-ttu-id="14ebc-304">2</span><span class="sxs-lookup"><span data-stu-id="14ebc-304">2</span></span> | <span data-ttu-id="14ebc-305">20170120</span><span class="sxs-lookup"><span data-stu-id="14ebc-305">20170120</span></span> | <span data-ttu-id="14ebc-306">3500</span><span class="sxs-lookup"><span data-stu-id="14ebc-306">3500</span></span> | <span data-ttu-id="14ebc-307">Pedro</span><span class="sxs-lookup"><span data-stu-id="14ebc-307">Patrick</span></span> |
| <span data-ttu-id="14ebc-308">3</span><span class="sxs-lookup"><span data-stu-id="14ebc-308">3</span></span> | <span data-ttu-id="14ebc-309">20170121</span><span class="sxs-lookup"><span data-stu-id="14ebc-309">20170121</span></span> | <span data-ttu-id="14ebc-310">4000</span><span class="sxs-lookup"><span data-stu-id="14ebc-310">4000</span></span> | <span data-ttu-id="14ebc-311">Jason</span><span class="sxs-lookup"><span data-stu-id="14ebc-311">Jason</span></span> |

<span data-ttu-id="14ebc-312">e, para cada registro, você espera gravar em um objeto JSON neste formato:</span><span class="sxs-lookup"><span data-stu-id="14ebc-312">and for each record, you expect to write to a JSON object in below format:</span></span>
```json
{
    "id": "1",
    "order": {
        "date": "20170119",
        "price": 2000,
        "customer": "David"
    }
}
```

<span data-ttu-id="14ebc-313">O conjunto de dados de saída com o tipo **JsonFormat** é definido da seguinte maneira: (definição parcial com apenas as partes relevantes).</span><span class="sxs-lookup"><span data-stu-id="14ebc-313">The output dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="14ebc-314">Mais especificamente, a seção `structure` define os nomes de propriedade personalizada no arquivo de destino, `nestingSeparator` (o padrão é ".") será usado para identificar a camada de aninhamento do nome.</span><span class="sxs-lookup"><span data-stu-id="14ebc-314">More specifically, `structure` section defines the customized property names in destination file, `nestingSeparator` (default is ".") will be used to identify the nest layer from the name.</span></span> <span data-ttu-id="14ebc-315">Esta seção é **opcional**, a menos que você queira alterar o nome da propriedade em comparação ao nome da coluna de origem ou aninhar algumas das propriedades.</span><span class="sxs-lookup"><span data-stu-id="14ebc-315">This section is **optional** unless you want to change the property name comparing with source column name, or nest some of the properties.</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "order.date",
            "type": "String"
        },
        {
            "name": "order.price",
            "type": "Int64"
        },
        {
            "name": "order.customer",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat"
        }
    }
}
```

### <a name="specifying-avroformat"></a><span data-ttu-id="14ebc-316">Especificando AvroFormat</span><span class="sxs-lookup"><span data-stu-id="14ebc-316">Specifying AvroFormat</span></span>
<span data-ttu-id="14ebc-317">Se você quiser analisar os arquivos Avro ou gravar os dados no formato Avro, defina a propriedade `format` `type` como **AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="14ebc-317">If you want to parse the Avro files or write the data in Avro format, set the `format` `type` property to **AvroFormat**.</span></span> <span data-ttu-id="14ebc-318">Não será necessário especificar nenhuma propriedade na seção Formato dentro da seção typeProperties.</span><span class="sxs-lookup"><span data-stu-id="14ebc-318">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="14ebc-319">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="14ebc-319">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="14ebc-320">Para usar o formato Avro em uma tabela de Hive, confira [Tutorial do Apache Hive](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span><span class="sxs-lookup"><span data-stu-id="14ebc-320">To use Avro format in a Hive table, you can refer to [Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="14ebc-321">Observe os seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="14ebc-321">Note the following points:</span></span>  

* <span data-ttu-id="14ebc-322">Não há suporte para [Tipos de dados complexos](http://avro.apache.org/docs/current/spec.html#schema_complex) (registros, enumerações, matrizes, mapas, uniões e fixo).</span><span class="sxs-lookup"><span data-stu-id="14ebc-322">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions and fixed).</span></span>

### <a name="specifying-orcformat"></a><span data-ttu-id="14ebc-323">Especificando OrcFormat</span><span class="sxs-lookup"><span data-stu-id="14ebc-323">Specifying OrcFormat</span></span>
<span data-ttu-id="14ebc-324">Se você quiser analisar os arquivos ORC ou gravar os dados no formato ORC, defina a propriedade `format` `type` como **OrcFormat**.</span><span class="sxs-lookup"><span data-stu-id="14ebc-324">If you want to parse the ORC files or write the data in ORC format, set the `format` `type` property to **OrcFormat**.</span></span> <span data-ttu-id="14ebc-325">Não será necessário especificar nenhuma propriedade na seção Formato dentro da seção typeProperties.</span><span class="sxs-lookup"><span data-stu-id="14ebc-325">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="14ebc-326">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="14ebc-326">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="14ebc-327">Se você não estiver copiando arquivos ORC **como são** entre repositórios de dados locais e na nuvem, você precisará instalar o JRE 8 (Java Runtime Environment) no computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="14ebc-327">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="14ebc-328">Um gateway de 64 bits exige JRE de 64 bits, enquanto um gateway de 32 bits exige JRE de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="14ebc-328">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="14ebc-329">Você pode encontrar as duas versões [aqui](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="14ebc-329">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="14ebc-330">Escolha aquela que for apropriada.</span><span class="sxs-lookup"><span data-stu-id="14ebc-330">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="14ebc-331">Observe os seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="14ebc-331">Note the following points:</span></span>

* <span data-ttu-id="14ebc-332">Não há suporte para tipos de dados complexos (STRUCT, MAP, LIST e UNION)</span><span class="sxs-lookup"><span data-stu-id="14ebc-332">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="14ebc-333">O arquivo ORC tem três [opções de compactação](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB e SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="14ebc-333">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="14ebc-334">O Data Factory dá suporte à leitura de dados de arquivo ORC em qualquer um dos formatos compactados acima.</span><span class="sxs-lookup"><span data-stu-id="14ebc-334">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="14ebc-335">Ele usa o codec de compactação nos metadados para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="14ebc-335">It uses the compression codec is in the metadata to read the data.</span></span> <span data-ttu-id="14ebc-336">No entanto, ao gravar um arquivo ORC, o Data Factory escolhe ZLIB, que é o padrão para ORC.</span><span class="sxs-lookup"><span data-stu-id="14ebc-336">However, when writing to an ORC file, Data Factory chooses ZLIB, which is the default for ORC.</span></span> <span data-ttu-id="14ebc-337">Não há nenhuma opção para substituir esse comportamento neste momento.</span><span class="sxs-lookup"><span data-stu-id="14ebc-337">Currently, there is no option to override this behavior.</span></span>

### <a name="specifying-parquetformat"></a><span data-ttu-id="14ebc-338">Especificando ParquetFormat</span><span class="sxs-lookup"><span data-stu-id="14ebc-338">Specifying ParquetFormat</span></span>
<span data-ttu-id="14ebc-339">Se você quiser analisar os arquivos Parquet ou gravar os dados no formato Parquet, defina a propriedade `format` `type` como **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="14ebc-339">If you want to parse the Parquet files or write the data in Parquet format, set the `format` `type` property to **ParquetFormat**.</span></span> <span data-ttu-id="14ebc-340">Não será necessário especificar nenhuma propriedade na seção Formato dentro da seção typeProperties.</span><span class="sxs-lookup"><span data-stu-id="14ebc-340">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="14ebc-341">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="14ebc-341">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="14ebc-342">Se você não estiver copiando arquivos Parquet **no estado em que se encontram** entre armazenamentos de dados locais e na nuvem, você precisará instalar o JRE 8 (Java Runtime Environment) no computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="14ebc-342">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="14ebc-343">Um gateway de 64 bits exige JRE de 64 bits, enquanto um gateway de 32 bits exige JRE de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="14ebc-343">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="14ebc-344">Você pode encontrar as duas versões [aqui](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="14ebc-344">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="14ebc-345">Escolha aquela que for apropriada.</span><span class="sxs-lookup"><span data-stu-id="14ebc-345">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="14ebc-346">Observe os seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="14ebc-346">Note the following points:</span></span>

* <span data-ttu-id="14ebc-347">Não há suporte para tipos de dados complexos (MAP, LIST)</span><span class="sxs-lookup"><span data-stu-id="14ebc-347">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="14ebc-348">O arquivo Parquet tem as seguintes opções relacionadas à compactação: NONE, SNAPPY, GZIP e LZO.</span><span class="sxs-lookup"><span data-stu-id="14ebc-348">Parquet file has the following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="14ebc-349">O Data Factory dá suporte à leitura de dados de arquivo ORC em qualquer um dos formatos compactados acima.</span><span class="sxs-lookup"><span data-stu-id="14ebc-349">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="14ebc-350">Ele usa o codec de compactação nos metadados para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="14ebc-350">It uses the compression codec in the metadata to read the data.</span></span> <span data-ttu-id="14ebc-351">No entanto, ao gravar um arquivo Parquet, o Data Factory escolhe SNAPPY, que é o padrão para o formato Parquet.</span><span class="sxs-lookup"><span data-stu-id="14ebc-351">However, when writing to a Parquet file, Data Factory chooses SNAPPY, which is the default for Parquet format.</span></span> <span data-ttu-id="14ebc-352">Não há nenhuma opção para substituir esse comportamento neste momento.</span><span class="sxs-lookup"><span data-stu-id="14ebc-352">Currently, there is no option to override this behavior.</span></span>
