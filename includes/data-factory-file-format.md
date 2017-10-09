## <a name="specifying-formats"></a><span data-ttu-id="6eba6-101">Especificando formatos</span><span class="sxs-lookup"><span data-stu-id="6eba6-101">Specifying formats</span></span>
<span data-ttu-id="6eba6-102">A fábrica de dados do Azure dá suporte a saudação tipos de formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="6eba6-102">Azure Data Factory supports hello following format types:</span></span>

* [<span data-ttu-id="6eba6-103">Formato de texto</span><span class="sxs-lookup"><span data-stu-id="6eba6-103">Text Format</span></span>](#specifying-textformat)
* [<span data-ttu-id="6eba6-104">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="6eba6-104">JSON Format</span></span>](#specifying-jsonformat)
* [<span data-ttu-id="6eba6-105">Formato Avro</span><span class="sxs-lookup"><span data-stu-id="6eba6-105">Avro Format</span></span>](#specifying-avroformat)
* [<span data-ttu-id="6eba6-106">Formato ORC</span><span class="sxs-lookup"><span data-stu-id="6eba6-106">ORC Format</span></span>](#specifying-orcformat)
* [<span data-ttu-id="6eba6-107">Formato de Parquet</span><span class="sxs-lookup"><span data-stu-id="6eba6-107">Parquet Format</span></span>](#specifying-parquetformat)

### <a name="specifying-textformat"></a><span data-ttu-id="6eba6-108">Especificando TextFormat</span><span class="sxs-lookup"><span data-stu-id="6eba6-108">Specifying TextFormat</span></span>
<span data-ttu-id="6eba6-109">Se você quiser tooparse arquivos de texto de saudação ou gravar dados saudação em formato de texto, defina Olá `format` `type` propriedade muito**TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="6eba6-109">If you want tooparse hello text files or write hello data in text format, set hello `format` `type` property too**TextFormat**.</span></span> <span data-ttu-id="6eba6-110">Você também pode especificar o seguinte Olá **opcional** propriedades no hello `format` seção.</span><span class="sxs-lookup"><span data-stu-id="6eba6-110">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="6eba6-111">Consulte [TextFormat exemplo](#textformat-example) seção sobre como tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="6eba6-111">See [TextFormat example](#textformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="6eba6-112">Propriedade</span><span class="sxs-lookup"><span data-stu-id="6eba6-112">Property</span></span> | <span data-ttu-id="6eba6-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="6eba6-113">Description</span></span> | <span data-ttu-id="6eba6-114">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="6eba6-114">Allowed values</span></span> | <span data-ttu-id="6eba6-115">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="6eba6-115">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6eba6-116">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="6eba6-116">columnDelimiter</span></span> |<span data-ttu-id="6eba6-117">caractere de saudação usado tooseparate colunas em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="6eba6-117">hello character used tooseparate columns in a file.</span></span> <span data-ttu-id="6eba6-118">Você pode considerar toouse um caractere não imprimível raro que provavelmente não existe em seus dados: por exemplo, especifique "\u0001" que representa o início do título (SOH).</span><span class="sxs-lookup"><span data-stu-id="6eba6-118">You can consider toouse a rare unprintable char which not likely exists in your data: e.g. specify "\u0001" which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="6eba6-119">Somente um caractere é permitido.</span><span class="sxs-lookup"><span data-stu-id="6eba6-119">Only one character is allowed.</span></span> <span data-ttu-id="6eba6-120">Olá **padrão** valor é **vírgula (',')**.</span><span class="sxs-lookup"><span data-stu-id="6eba6-120">hello **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="6eba6-121">toouse um caractere Unicode, consulte muito[caracteres Unicode](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello código correspondente para ele.</span><span class="sxs-lookup"><span data-stu-id="6eba6-121">toouse an Unicode character, refer too[Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello corresponding code for it.</span></span> |<span data-ttu-id="6eba6-122">Não</span><span class="sxs-lookup"><span data-stu-id="6eba6-122">No</span></span> |
| <span data-ttu-id="6eba6-123">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="6eba6-123">rowDelimiter</span></span> |<span data-ttu-id="6eba6-124">caractere de saudação usado tooseparate linhas em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="6eba6-124">hello character used tooseparate rows in a file.</span></span> |<span data-ttu-id="6eba6-125">Somente um caractere é permitido.</span><span class="sxs-lookup"><span data-stu-id="6eba6-125">Only one character is allowed.</span></span> <span data-ttu-id="6eba6-126">Olá **padrão** valor é qualquer um dos valores a seguir na leitura de saudação: **["\r\n", "\r", "\n"]** e **"\r\n"** na gravação.</span><span class="sxs-lookup"><span data-stu-id="6eba6-126">hello **default** value is any of hello following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="6eba6-127">Não</span><span class="sxs-lookup"><span data-stu-id="6eba6-127">No</span></span> |
| <span data-ttu-id="6eba6-128">escapeChar</span><span class="sxs-lookup"><span data-stu-id="6eba6-128">escapeChar</span></span> |<span data-ttu-id="6eba6-129">caractere especial Olá usado tooescape um delimitador de coluna no conteúdo de saudação do arquivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="6eba6-129">hello special character used tooescape a column delimiter in hello content of input file.</span></span> <br/><br/><span data-ttu-id="6eba6-130">Não é possível especificar ambos escapeChar e quoteChar para uma tabela.</span><span class="sxs-lookup"><span data-stu-id="6eba6-130">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="6eba6-131">Somente um caractere é permitido.</span><span class="sxs-lookup"><span data-stu-id="6eba6-131">Only one character is allowed.</span></span> <span data-ttu-id="6eba6-132">Nenhum valor padrão.</span><span class="sxs-lookup"><span data-stu-id="6eba6-132">No default value.</span></span> <br/><br/><span data-ttu-id="6eba6-133">Exemplo: se você tem vírgula (', ') como delimitador de coluna hello, mas você deseja o caractere de vírgula Olá toohave no texto de saudação (exemplo: "Olá, mundo"), você pode definir o '$' como o caractere de escape hello e usar a cadeia de caracteres "$Oi, mundo" na fonte de saudação.</span><span class="sxs-lookup"><span data-stu-id="6eba6-133">Example: if you have comma (',') as hello column delimiter but you want toohave hello comma character in hello text (example: "Hello, world"), you can define ‘$’ as hello escape character and use string "Hello$, world" in hello source.</span></span> |<span data-ttu-id="6eba6-134">Não</span><span class="sxs-lookup"><span data-stu-id="6eba6-134">No</span></span> |
| <span data-ttu-id="6eba6-135">quoteChar</span><span class="sxs-lookup"><span data-stu-id="6eba6-135">quoteChar</span></span> |<span data-ttu-id="6eba6-136">caractere de saudação usado tooquote um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="6eba6-136">hello character used tooquote a string value.</span></span> <span data-ttu-id="6eba6-137">delimitadores de coluna e linha Hello dentro de caracteres de aspas Olá seriam tratadas como parte do valor de cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="6eba6-137">hello column and row delimiters inside hello quote characters would be treated as part of hello string value.</span></span> <span data-ttu-id="6eba6-138">Essa propriedade é aplicável tooboth entrada e conjuntos de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="6eba6-138">This property is applicable tooboth input and output datasets.</span></span><br/><br/><span data-ttu-id="6eba6-139">Não é possível especificar ambos escapeChar e quoteChar para uma tabela.</span><span class="sxs-lookup"><span data-stu-id="6eba6-139">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="6eba6-140">Somente um caractere é permitido.</span><span class="sxs-lookup"><span data-stu-id="6eba6-140">Only one character is allowed.</span></span> <span data-ttu-id="6eba6-141">Nenhum valor padrão.</span><span class="sxs-lookup"><span data-stu-id="6eba6-141">No default value.</span></span> <br/><br/><span data-ttu-id="6eba6-142">Por exemplo, se você tem vírgula (', ') como delimitador de coluna hello, mas você deseja toohave caractere de vírgula no texto de saudação (exemplo: < Olá, mundo >), você pode definir "(aspas duplas) como Olá caractere de aspas e usar a cadeia de caracteres hello"Olá, mundo"na fonte de saudação.</span><span class="sxs-lookup"><span data-stu-id="6eba6-142">For example, if you have comma (',') as hello column delimiter but you want toohave comma character in hello text (example: <Hello, world>), you can define " (double quote) as hello quote character and use hello string "Hello, world" in hello source.</span></span> |<span data-ttu-id="6eba6-143">Não</span><span class="sxs-lookup"><span data-stu-id="6eba6-143">No</span></span> |
| <span data-ttu-id="6eba6-144">nullValue</span><span class="sxs-lookup"><span data-stu-id="6eba6-144">nullValue</span></span> |<span data-ttu-id="6eba6-145">Um ou mais caracteres usados toorepresent um valor nulo.</span><span class="sxs-lookup"><span data-stu-id="6eba6-145">One or more characters used toorepresent a null value.</span></span> |<span data-ttu-id="6eba6-146">Um ou mais caracteres.</span><span class="sxs-lookup"><span data-stu-id="6eba6-146">One or more characters.</span></span> <span data-ttu-id="6eba6-147">Olá **padrão** os valores são **"\N" e "NULL"** na leitura e **"\N"** na gravação.</span><span class="sxs-lookup"><span data-stu-id="6eba6-147">hello **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="6eba6-148">Não</span><span class="sxs-lookup"><span data-stu-id="6eba6-148">No</span></span> |
| <span data-ttu-id="6eba6-149">encodingName</span><span class="sxs-lookup"><span data-stu-id="6eba6-149">encodingName</span></span> |<span data-ttu-id="6eba6-150">Especifique o nome de codificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6eba6-150">Specify hello encoding name.</span></span> |<span data-ttu-id="6eba6-151">Um nomes de codificação válido.</span><span class="sxs-lookup"><span data-stu-id="6eba6-151">A valid encoding name.</span></span> <span data-ttu-id="6eba6-152">Consulte [Propriedade Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="6eba6-152">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="6eba6-153">Por exemplo: windows-1250 ou shift_jis.</span><span class="sxs-lookup"><span data-stu-id="6eba6-153">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="6eba6-154">Olá **padrão** valor é **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="6eba6-154">hello **default** value is **UTF-8**.</span></span> |<span data-ttu-id="6eba6-155">Não</span><span class="sxs-lookup"><span data-stu-id="6eba6-155">No</span></span> |
| <span data-ttu-id="6eba6-156">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="6eba6-156">firstRowAsHeader</span></span> |<span data-ttu-id="6eba6-157">Especifica se tooconsider Olá a primeira linha como cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="6eba6-157">Specifies whether tooconsider hello first row as a header.</span></span> <span data-ttu-id="6eba6-158">Para um conjunto de dados de entrada, o Data Factory lê a primeira linha como cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="6eba6-158">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="6eba6-159">Para um conjunto de dados de saída, o Data Factory lê a primeira linha como cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="6eba6-159">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="6eba6-160">Veja [Cenários para usar o `firstRowAsHeader` e o `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) para cenários de exemplo.</span><span class="sxs-lookup"><span data-stu-id="6eba6-160">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="6eba6-161">True </span><span class="sxs-lookup"><span data-stu-id="6eba6-161">True</span></span><br/><span data-ttu-id="6eba6-162">**False (padrão)**</span><span class="sxs-lookup"><span data-stu-id="6eba6-162">**False (default)**</span></span> |<span data-ttu-id="6eba6-163">Não</span><span class="sxs-lookup"><span data-stu-id="6eba6-163">No</span></span> |
| <span data-ttu-id="6eba6-164">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="6eba6-164">skipLineCount</span></span> |<span data-ttu-id="6eba6-165">Indica o número de saudação de linhas tooskip ao ler dados de arquivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="6eba6-165">Indicates hello number of rows tooskip when reading data from input files.</span></span> <span data-ttu-id="6eba6-166">Se skipLineCount e firstRowAsHeader forem especificados, linhas de saudação são ignoradas primeiro e, em seguida, as informações de cabeçalho de saudação é lido do arquivo de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="6eba6-166">If both skipLineCount and firstRowAsHeader are specified, hello lines are skipped first and then hello header information is read from hello input file.</span></span> <br/><br/><span data-ttu-id="6eba6-167">Veja [Cenários para usar o `firstRowAsHeader` e o `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) para cenários de exemplo.</span><span class="sxs-lookup"><span data-stu-id="6eba6-167">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="6eba6-168">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="6eba6-168">Integer</span></span> |<span data-ttu-id="6eba6-169">Não</span><span class="sxs-lookup"><span data-stu-id="6eba6-169">No</span></span> |
| <span data-ttu-id="6eba6-170">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="6eba6-170">treatEmptyAsNull</span></span> |<span data-ttu-id="6eba6-171">Especifica se a cadeia de tootreat nula ou vazia como nula valor quando ler dados de um arquivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="6eba6-171">Specifies whether tootreat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="6eba6-172">**True (padrão)**</span><span class="sxs-lookup"><span data-stu-id="6eba6-172">**True (default)**</span></span><br/><span data-ttu-id="6eba6-173">Falso</span><span class="sxs-lookup"><span data-stu-id="6eba6-173">False</span></span> |<span data-ttu-id="6eba6-174">Não</span><span class="sxs-lookup"><span data-stu-id="6eba6-174">No</span></span> |

#### <a name="textformat-example"></a><span data-ttu-id="6eba6-175">Exemplo de TextFormat</span><span class="sxs-lookup"><span data-stu-id="6eba6-175">TextFormat example</span></span>
<span data-ttu-id="6eba6-176">Olá exemplo a seguir mostra algumas das propriedades de formato de saudação para TextFormat.</span><span class="sxs-lookup"><span data-stu-id="6eba6-176">hello following sample shows some of hello format properties for TextFormat.</span></span>

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

<span data-ttu-id="6eba6-177">toouse um `escapeChar` em vez de `quoteChar`, substitua a linha hello com `quoteChar` com hello escapeChar a seguir:</span><span class="sxs-lookup"><span data-stu-id="6eba6-177">toouse an `escapeChar` instead of `quoteChar`, replace hello line with `quoteChar` with hello following escapeChar:</span></span>

```json
"escapeChar": "$",
```

#### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="6eba6-178">Cenários de uso de firstRowAsHeader e skipLineCount</span><span class="sxs-lookup"><span data-stu-id="6eba6-178">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="6eba6-179">Você está copiando um arquivo de texto do arquivo fonte tooa e gostaria de tooadd uma linha de cabeçalho que contém metadados do esquema de saudação (por exemplo: esquema SQL).</span><span class="sxs-lookup"><span data-stu-id="6eba6-179">You are copying from a non-file source tooa text file and would like tooadd a header line containing hello schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="6eba6-180">Especifique `firstRowAsHeader` como true no conjunto de dados de saída de saudação para esse cenário.</span><span class="sxs-lookup"><span data-stu-id="6eba6-180">Specify `firstRowAsHeader` as true in hello output dataset for this scenario.</span></span>
* <span data-ttu-id="6eba6-181">Você está copiando um arquivo de texto que contém um coletor de arquivo do cabeçalho linha tooa e deseja toodrop de linha.</span><span class="sxs-lookup"><span data-stu-id="6eba6-181">You are copying from a text file containing a header line tooa non-file sink and would like toodrop that line.</span></span> <span data-ttu-id="6eba6-182">Especifique `firstRowAsHeader` como true no conjunto de dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="6eba6-182">Specify `firstRowAsHeader` as true in hello input dataset.</span></span>
* <span data-ttu-id="6eba6-183">Você está copiando um arquivo de texto e deseja tooskip algumas linhas no início de saudação que não contêm nenhuma informação de cabeçalho ou de dados.</span><span class="sxs-lookup"><span data-stu-id="6eba6-183">You are copying from a text file and want tooskip a few lines at hello beginning that contain no data or header information.</span></span> <span data-ttu-id="6eba6-184">Especifique `skipLineCount` tooindicate Olá número de linhas toobe ignorados.</span><span class="sxs-lookup"><span data-stu-id="6eba6-184">Specify `skipLineCount` tooindicate hello number of lines toobe skipped.</span></span> <span data-ttu-id="6eba6-185">Se o resto de saudação do arquivo hello contém uma linha de cabeçalho, você também pode especificar `firstRowAsHeader`.</span><span class="sxs-lookup"><span data-stu-id="6eba6-185">If hello rest of hello file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="6eba6-186">Se ambos os `skipLineCount` e `firstRowAsHeader` forem especificados, linhas de saudação são ignoradas pela primeira vez e, em seguida, as informações de cabeçalho de saudação é lido do arquivo de entrada hello</span><span class="sxs-lookup"><span data-stu-id="6eba6-186">If both `skipLineCount` and `firstRowAsHeader` are specified, hello lines are skipped first and then hello header information is read from hello input file</span></span>

### <a name="specifying-jsonformat"></a><span data-ttu-id="6eba6-187">Especificando JsonFormat</span><span class="sxs-lookup"><span data-stu-id="6eba6-187">Specifying JsonFormat</span></span>
<span data-ttu-id="6eba6-188">muito**arquivos JSON como importação/exportação-está em de banco de dados do Azure Cosmos**, consulte [documentos JSON de importação/exportação](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) seção no conector do banco de dados do Azure Cosmos Olá com detalhes.</span><span class="sxs-lookup"><span data-stu-id="6eba6-188">too**import/export JSON files as-is into/from Azure Cosmos DB**, see [Import/export JSON documents](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) section in hello Azure Cosmos DB connector with details.</span></span>

<span data-ttu-id="6eba6-189">Se você deseja tooparse Olá JSON arquivos ou gravar dados saudação no formato JSON, defina Olá `format` `type` propriedade muito**JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="6eba6-189">If you want tooparse hello JSON files or write hello data in JSON format, set hello `format` `type` property too**JsonFormat**.</span></span> <span data-ttu-id="6eba6-190">Você também pode especificar o seguinte Olá **opcional** propriedades no hello `format` seção.</span><span class="sxs-lookup"><span data-stu-id="6eba6-190">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="6eba6-191">Consulte [JsonFormat exemplo](#jsonformat-example) seção sobre como tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="6eba6-191">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="6eba6-192">Propriedade</span><span class="sxs-lookup"><span data-stu-id="6eba6-192">Property</span></span> | <span data-ttu-id="6eba6-193">Descrição</span><span class="sxs-lookup"><span data-stu-id="6eba6-193">Description</span></span> | <span data-ttu-id="6eba6-194">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="6eba6-194">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6eba6-195">filePattern</span><span class="sxs-lookup"><span data-stu-id="6eba6-195">filePattern</span></span> |<span data-ttu-id="6eba6-196">Indica padrão Olá dos dados armazenados em cada arquivo JSON.</span><span class="sxs-lookup"><span data-stu-id="6eba6-196">Indicate hello pattern of data stored in each JSON file.</span></span> <span data-ttu-id="6eba6-197">Os valores permitidos são: **setOfObjects** e **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="6eba6-197">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="6eba6-198">Olá **padrão** valor é **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="6eba6-198">hello **default** value is **setOfObjects**.</span></span> <span data-ttu-id="6eba6-199">Veja a seção [Padrões de arquivo JSON](#json-file-patterns) para obter detalhes sobre esses padrões.</span><span class="sxs-lookup"><span data-stu-id="6eba6-199">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="6eba6-200">Não</span><span class="sxs-lookup"><span data-stu-id="6eba6-200">No</span></span> |
| <span data-ttu-id="6eba6-201">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="6eba6-201">jsonNodeReference</span></span> | <span data-ttu-id="6eba6-202">Se você deseja tooiterate e extrair dados de objetos hello dentro de uma matriz de campo com hello mesmo padrão, especifique o caminho do JSON Olá dessa matriz.</span><span class="sxs-lookup"><span data-stu-id="6eba6-202">If you want tooiterate and extract data from hello objects inside an array field with hello same pattern, specify hello JSON path of that array.</span></span> <span data-ttu-id="6eba6-203">Esta propriedade só terá suporte na cópia de dados de arquivos JSON.</span><span class="sxs-lookup"><span data-stu-id="6eba6-203">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="6eba6-204">Não</span><span class="sxs-lookup"><span data-stu-id="6eba6-204">No</span></span> |
| <span data-ttu-id="6eba6-205">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="6eba6-205">jsonPathDefinition</span></span> | <span data-ttu-id="6eba6-206">Especifique a expressão de caminho JSON Olá para cada mapeamento de coluna com um nome de coluna personalizada (começam com letras minúsculas).</span><span class="sxs-lookup"><span data-stu-id="6eba6-206">Specify hello JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="6eba6-207">Esta propriedade só terá suporte na cópia de dados de arquivos JSON, e você pode extrair dados de objeto ou de matriz.</span><span class="sxs-lookup"><span data-stu-id="6eba6-207">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="6eba6-208">Para os campos no objeto raiz, começar com $ raiz; para campos de matriz de saudação escolhida pelo `jsonNodeReference` propriedade, início do elemento da matriz hello.</span><span class="sxs-lookup"><span data-stu-id="6eba6-208">For fields under root object, start with root $; for fields inside hello array chosen by `jsonNodeReference` property, start from hello array element.</span></span> <span data-ttu-id="6eba6-209">Consulte [JsonFormat exemplo](#jsonformat-example) seção sobre como tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="6eba6-209">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span> | <span data-ttu-id="6eba6-210">Não</span><span class="sxs-lookup"><span data-stu-id="6eba6-210">No</span></span> |
| <span data-ttu-id="6eba6-211">encodingName</span><span class="sxs-lookup"><span data-stu-id="6eba6-211">encodingName</span></span> |<span data-ttu-id="6eba6-212">Especifique o nome de codificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6eba6-212">Specify hello encoding name.</span></span> <span data-ttu-id="6eba6-213">Para obter lista de saudação de nomes válidos de codificação, consulte: [encodingname](https://msdn.microsoft.com/library/system.text.encoding.aspx) propriedade.</span><span class="sxs-lookup"><span data-stu-id="6eba6-213">For hello list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="6eba6-214">Por exemplo: windows-1250 ou shift_jis.</span><span class="sxs-lookup"><span data-stu-id="6eba6-214">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="6eba6-215">Olá **padrão** valor é: **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="6eba6-215">hello **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="6eba6-216">Não</span><span class="sxs-lookup"><span data-stu-id="6eba6-216">No</span></span> |
| <span data-ttu-id="6eba6-217">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="6eba6-217">nestingSeparator</span></span> |<span data-ttu-id="6eba6-218">Caractere usado tooseparate níveis de aninhamento.</span><span class="sxs-lookup"><span data-stu-id="6eba6-218">Character that is used tooseparate nesting levels.</span></span> <span data-ttu-id="6eba6-219">valor padrão de saudação é '.' (ponto).</span><span class="sxs-lookup"><span data-stu-id="6eba6-219">hello default value is '.' (dot).</span></span> |<span data-ttu-id="6eba6-220">Não</span><span class="sxs-lookup"><span data-stu-id="6eba6-220">No</span></span> |

#### <a name="json-file-patterns"></a><span data-ttu-id="6eba6-221">Padrões de arquivo JSON</span><span class="sxs-lookup"><span data-stu-id="6eba6-221">JSON file patterns</span></span>

<span data-ttu-id="6eba6-222">A atividade de cópia pode analisar os padrões dos arquivos JSON abaixo:</span><span class="sxs-lookup"><span data-stu-id="6eba6-222">Copy activity can parse below patterns of JSON files:</span></span>

- <span data-ttu-id="6eba6-223">**Tipo I: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="6eba6-223">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="6eba6-224">Cada arquivo contém um único objeto ou vários objetos concatenados/delimitados por linhas.</span><span class="sxs-lookup"><span data-stu-id="6eba6-224">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="6eba6-225">Quando essa opção é escolhida em um conjunto de dados de saída, a atividade de cópia produz um único arquivo JSON com cada objeto por linha (delimitados por linha).</span><span class="sxs-lookup"><span data-stu-id="6eba6-225">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="6eba6-226">**Exemplo de JSON de objeto único**</span><span class="sxs-lookup"><span data-stu-id="6eba6-226">**single object JSON example**</span></span>

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

    * <span data-ttu-id="6eba6-227">**Exemplo de JSON delimitado por linha**</span><span class="sxs-lookup"><span data-stu-id="6eba6-227">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="6eba6-228">**Exemplo de JSON concatenado**</span><span class="sxs-lookup"><span data-stu-id="6eba6-228">**concatenated JSON example**</span></span>

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

- <span data-ttu-id="6eba6-229">**Tipo II: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="6eba6-229">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="6eba6-230">Cada arquivo contém uma matriz de objetos.</span><span class="sxs-lookup"><span data-stu-id="6eba6-230">Each file contains an array of objects.</span></span>

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

#### <a name="jsonformat-example"></a><span data-ttu-id="6eba6-231">Exemplo de JsonFormat</span><span class="sxs-lookup"><span data-stu-id="6eba6-231">JsonFormat example</span></span>

<span data-ttu-id="6eba6-232">**Caso 1: copiar dados de arquivos JSON**</span><span class="sxs-lookup"><span data-stu-id="6eba6-232">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="6eba6-233">Veja abaixo dois tipos de amostras ao copiar dados de arquivos JSON e Olá toonote pontos genérico:</span><span class="sxs-lookup"><span data-stu-id="6eba6-233">See below two types of samples when copying data from JSON files, and hello generic points toonote:</span></span>

<span data-ttu-id="6eba6-234">**Exemplo 1: extrair dados de objeto e de matriz**</span><span class="sxs-lookup"><span data-stu-id="6eba6-234">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="6eba6-235">Neste exemplo, você espera que um objeto JSON de raiz mapeia toosingle registro na tabela de resultados.</span><span class="sxs-lookup"><span data-stu-id="6eba6-235">In this sample, you expect one root JSON object maps toosingle record in tabular result.</span></span> <span data-ttu-id="6eba6-236">Se você tiver um arquivo JSON com hello conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="6eba6-236">If you have a JSON file with hello following content:</span></span>  

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
<span data-ttu-id="6eba6-237">e você deseja toocopy-lo em uma tabela do SQL Azure no seguinte Olá Formatar, extraindo dados de objetos e a matriz:</span><span class="sxs-lookup"><span data-stu-id="6eba6-237">and you want toocopy it into an Azure SQL table in hello following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="6eba6-238">ID</span><span class="sxs-lookup"><span data-stu-id="6eba6-238">id</span></span> | <span data-ttu-id="6eba6-239">deviceType</span><span class="sxs-lookup"><span data-stu-id="6eba6-239">deviceType</span></span> | <span data-ttu-id="6eba6-240">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="6eba6-240">targetResourceType</span></span> | <span data-ttu-id="6eba6-241">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="6eba6-241">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="6eba6-242">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="6eba6-242">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="6eba6-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="6eba6-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="6eba6-244">Computador</span><span class="sxs-lookup"><span data-stu-id="6eba6-244">PC</span></span> | <span data-ttu-id="6eba6-245">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="6eba6-245">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="6eba6-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="6eba6-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="6eba6-247">13/01/2017 11:24:37</span><span class="sxs-lookup"><span data-stu-id="6eba6-247">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="6eba6-248">conjunto de dados de entrada de saudação com **JsonFormat** tipo é definido da seguinte maneira: (definição parcial com partes relevantes apenas Olá).</span><span class="sxs-lookup"><span data-stu-id="6eba6-248">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="6eba6-249">Mais especificamente:</span><span class="sxs-lookup"><span data-stu-id="6eba6-249">More specifically:</span></span>

- <span data-ttu-id="6eba6-250">`structure`seção define os nomes de coluna de saudação personalizada e o tipo de dados correspondente Olá ao converter dados tootabular.</span><span class="sxs-lookup"><span data-stu-id="6eba6-250">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="6eba6-251">Esta seção é **opcional** , a menos que você precisa toodo mapeamento de coluna.</span><span class="sxs-lookup"><span data-stu-id="6eba6-251">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="6eba6-252">Veja a seção [Especificar a definição de estrutura para conjuntos de dados retangulares](#specifying-structure-definition-for-rectangular-datasets) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="6eba6-252">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="6eba6-253">`jsonPathDefinition`Especifica o caminho JSON de saudação para cada coluna que indica onde tooextract Olá dados.</span><span class="sxs-lookup"><span data-stu-id="6eba6-253">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="6eba6-254">toocopy dados da matriz, você pode usar **array [x] .property** tooextract valor Olá considerando a propriedade do objeto de x ª hello, ou você pode usar  **matriz [*] .property** toofind valor de saudação de qualquer objeto que contém essa propriedade.</span><span class="sxs-lookup"><span data-stu-id="6eba6-254">toocopy data from array, you can use **array[x].property** tooextract value of hello given property from hello xth object, or you can use **array[*].property** toofind hello value from any object containing such property.</span></span>

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

<span data-ttu-id="6eba6-255">**Exemplo 2: cruzada aplicar vários objetos com o mesmo padrão da matriz de saudação**</span><span class="sxs-lookup"><span data-stu-id="6eba6-255">**Sample 2: cross apply multiple objects with hello same pattern from array**</span></span>

<span data-ttu-id="6eba6-256">Neste exemplo, você espera que um objeto JSON de raiz tootransform em vários registros na tabela de resultados.</span><span class="sxs-lookup"><span data-stu-id="6eba6-256">In this sample, you expect tootransform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="6eba6-257">Se você tiver um arquivo JSON com hello conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="6eba6-257">If you have a JSON file with hello following content:</span></span>  

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
<span data-ttu-id="6eba6-258">e você deseja toocopy-lo em uma tabela do SQL Azure no seguinte Olá Formatar, mesclando dados hello dentro da matriz de saudação e cross join com informações de raiz comum hello:</span><span class="sxs-lookup"><span data-stu-id="6eba6-258">and you want toocopy it into an Azure SQL table in hello following format, by flattening hello data inside hello array and cross join with hello common root info:</span></span>

| <span data-ttu-id="6eba6-259">ordernumber</span><span class="sxs-lookup"><span data-stu-id="6eba6-259">ordernumber</span></span> | <span data-ttu-id="6eba6-260">orderdate</span><span class="sxs-lookup"><span data-stu-id="6eba6-260">orderdate</span></span> | <span data-ttu-id="6eba6-261">order_pd</span><span class="sxs-lookup"><span data-stu-id="6eba6-261">order_pd</span></span> | <span data-ttu-id="6eba6-262">order_price</span><span class="sxs-lookup"><span data-stu-id="6eba6-262">order_price</span></span> | <span data-ttu-id="6eba6-263">city</span><span class="sxs-lookup"><span data-stu-id="6eba6-263">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="6eba6-264">01</span><span class="sxs-lookup"><span data-stu-id="6eba6-264">01</span></span> | <span data-ttu-id="6eba6-265">20170122</span><span class="sxs-lookup"><span data-stu-id="6eba6-265">20170122</span></span> | <span data-ttu-id="6eba6-266">P1</span><span class="sxs-lookup"><span data-stu-id="6eba6-266">P1</span></span> | <span data-ttu-id="6eba6-267">23</span><span class="sxs-lookup"><span data-stu-id="6eba6-267">23</span></span> | <span data-ttu-id="6eba6-268">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="6eba6-268">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="6eba6-269">01</span><span class="sxs-lookup"><span data-stu-id="6eba6-269">01</span></span> | <span data-ttu-id="6eba6-270">20170122</span><span class="sxs-lookup"><span data-stu-id="6eba6-270">20170122</span></span> | <span data-ttu-id="6eba6-271">P2</span><span class="sxs-lookup"><span data-stu-id="6eba6-271">P2</span></span> | <span data-ttu-id="6eba6-272">13</span><span class="sxs-lookup"><span data-stu-id="6eba6-272">13</span></span> | <span data-ttu-id="6eba6-273">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="6eba6-273">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="6eba6-274">01</span><span class="sxs-lookup"><span data-stu-id="6eba6-274">01</span></span> | <span data-ttu-id="6eba6-275">20170122</span><span class="sxs-lookup"><span data-stu-id="6eba6-275">20170122</span></span> | <span data-ttu-id="6eba6-276">P3</span><span class="sxs-lookup"><span data-stu-id="6eba6-276">P3</span></span> | <span data-ttu-id="6eba6-277">231</span><span class="sxs-lookup"><span data-stu-id="6eba6-277">231</span></span> | <span data-ttu-id="6eba6-278">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="6eba6-278">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="6eba6-279">conjunto de dados de entrada de saudação com **JsonFormat** tipo é definido da seguinte maneira: (definição parcial com partes relevantes apenas Olá).</span><span class="sxs-lookup"><span data-stu-id="6eba6-279">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="6eba6-280">Mais especificamente:</span><span class="sxs-lookup"><span data-stu-id="6eba6-280">More specifically:</span></span>

- <span data-ttu-id="6eba6-281">`structure`seção define os nomes de coluna de saudação personalizada e o tipo de dados correspondente Olá ao converter dados tootabular.</span><span class="sxs-lookup"><span data-stu-id="6eba6-281">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="6eba6-282">Esta seção é **opcional** , a menos que você precisa toodo mapeamento de coluna.</span><span class="sxs-lookup"><span data-stu-id="6eba6-282">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="6eba6-283">Veja a seção [Especificar a definição de estrutura para conjuntos de dados retangulares](#specifying-structure-definition-for-rectangular-datasets) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="6eba6-283">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="6eba6-284">`jsonNodeReference`indica tooiterate e extrair dados de objetos Olá Olá mesmo padrão em **matriz** orderlines.</span><span class="sxs-lookup"><span data-stu-id="6eba6-284">`jsonNodeReference` indicates tooiterate and extract data from hello objects with hello same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="6eba6-285">`jsonPathDefinition`Especifica o caminho JSON de saudação para cada coluna que indica onde tooextract Olá dados.</span><span class="sxs-lookup"><span data-stu-id="6eba6-285">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="6eba6-286">Neste exemplo, "ordernumber", "orderdate" e "cidade" estão no objeto raiz com o caminho JSON iniciar com"$", enquanto "order_pd" e "order_price" são definidos com caminho derivado do elemento de matriz Olá sem "$"..</span><span class="sxs-lookup"><span data-stu-id="6eba6-286">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from hello array element without "$.".</span></span>

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

<span data-ttu-id="6eba6-287">**Observe Olá pontos a seguir:**</span><span class="sxs-lookup"><span data-stu-id="6eba6-287">**Note hello following points:**</span></span>

* <span data-ttu-id="6eba6-288">Se hello `structure` e `jsonPathDefinition` não estão definidos no conjunto de dados de Data Factory hello, hello atividade de cópia detecta Olá esquema do objeto primeiro hello e mesclar objeto inteiro hello.</span><span class="sxs-lookup"><span data-stu-id="6eba6-288">If hello `structure` and `jsonPathDefinition` are not defined in hello Data Factory dataset, hello Copy Activity detects hello schema from hello first object and flatten hello whole object.</span></span>
* <span data-ttu-id="6eba6-289">Se a entrada JSON Olá tem uma matriz, por padrão hello atividade de cópia converte Olá matriz inteira valor em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="6eba6-289">If hello JSON input has an array, by default hello Copy Activity converts hello entire array value into a string.</span></span> <span data-ttu-id="6eba6-290">Você pode escolher dados tooextract usando `jsonNodeReference` e/ou `jsonPathDefinition`, ou ignorá-la não especificando na `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="6eba6-290">You can choose tooextract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="6eba6-291">Se não houver duplicados Olá de nomes no mesmo nível, hello atividade de cópia selecionará Olá último.</span><span class="sxs-lookup"><span data-stu-id="6eba6-291">If there are duplicate names at hello same level, hello Copy Activity picks hello last one.</span></span>
* <span data-ttu-id="6eba6-292">Os nomes de propriedade diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="6eba6-292">Property names are case-sensitive.</span></span> <span data-ttu-id="6eba6-293">Duas propriedades com o mesmo nome, mas com maiúsculas e minúsculas diferentes são tratadas como duas propriedades separadas.</span><span class="sxs-lookup"><span data-stu-id="6eba6-293">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="6eba6-294">**Caso 2: Gravando dados tooJSON arquivo**</span><span class="sxs-lookup"><span data-stu-id="6eba6-294">**Case 2: Writing data tooJSON file**</span></span>

<span data-ttu-id="6eba6-295">Se você tiver a tabela a seguir no Banco de Dados SQL:</span><span class="sxs-lookup"><span data-stu-id="6eba6-295">If you have below table in SQL Database:</span></span>

| <span data-ttu-id="6eba6-296">ID</span><span class="sxs-lookup"><span data-stu-id="6eba6-296">id</span></span> | <span data-ttu-id="6eba6-297">order_date</span><span class="sxs-lookup"><span data-stu-id="6eba6-297">order_date</span></span> | <span data-ttu-id="6eba6-298">order_price</span><span class="sxs-lookup"><span data-stu-id="6eba6-298">order_price</span></span> | <span data-ttu-id="6eba6-299">order_by</span><span class="sxs-lookup"><span data-stu-id="6eba6-299">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6eba6-300">1</span><span class="sxs-lookup"><span data-stu-id="6eba6-300">1</span></span> | <span data-ttu-id="6eba6-301">20170119</span><span class="sxs-lookup"><span data-stu-id="6eba6-301">20170119</span></span> | <span data-ttu-id="6eba6-302">2000</span><span class="sxs-lookup"><span data-stu-id="6eba6-302">2000</span></span> | <span data-ttu-id="6eba6-303">Davi</span><span class="sxs-lookup"><span data-stu-id="6eba6-303">David</span></span> |
| <span data-ttu-id="6eba6-304">2</span><span class="sxs-lookup"><span data-stu-id="6eba6-304">2</span></span> | <span data-ttu-id="6eba6-305">20170120</span><span class="sxs-lookup"><span data-stu-id="6eba6-305">20170120</span></span> | <span data-ttu-id="6eba6-306">3500</span><span class="sxs-lookup"><span data-stu-id="6eba6-306">3500</span></span> | <span data-ttu-id="6eba6-307">Pedro</span><span class="sxs-lookup"><span data-stu-id="6eba6-307">Patrick</span></span> |
| <span data-ttu-id="6eba6-308">3</span><span class="sxs-lookup"><span data-stu-id="6eba6-308">3</span></span> | <span data-ttu-id="6eba6-309">20170121</span><span class="sxs-lookup"><span data-stu-id="6eba6-309">20170121</span></span> | <span data-ttu-id="6eba6-310">4000</span><span class="sxs-lookup"><span data-stu-id="6eba6-310">4000</span></span> | <span data-ttu-id="6eba6-311">Jason</span><span class="sxs-lookup"><span data-stu-id="6eba6-311">Jason</span></span> |

<span data-ttu-id="6eba6-312">e, para cada registro, você espera que o objeto JSON de tooa toowrite no abaixo formato:</span><span class="sxs-lookup"><span data-stu-id="6eba6-312">and for each record, you expect toowrite tooa JSON object in below format:</span></span>
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

<span data-ttu-id="6eba6-313">saudação de conjunto de dados com saída **JsonFormat** tipo é definido da seguinte maneira: (definição parcial com partes relevantes apenas Olá).</span><span class="sxs-lookup"><span data-stu-id="6eba6-313">hello output dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="6eba6-314">Mais especificamente, `structure` seção define os nomes de propriedade Olá personalizado no arquivo de destino, `nestingSeparator` (o padrão é ".") será a camada de aninhar Olá tooidentify usado do nome de saudação.</span><span class="sxs-lookup"><span data-stu-id="6eba6-314">More specifically, `structure` section defines hello customized property names in destination file, `nestingSeparator` (default is ".") will be used tooidentify hello nest layer from hello name.</span></span> <span data-ttu-id="6eba6-315">Esta seção é **opcional** a menos que você deseja o nome da propriedade Olá toochange comparando com o nome da coluna de origem ou aninhar algumas das propriedades de saudação.</span><span class="sxs-lookup"><span data-stu-id="6eba6-315">This section is **optional** unless you want toochange hello property name comparing with source column name, or nest some of hello properties.</span></span>

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

### <a name="specifying-avroformat"></a><span data-ttu-id="6eba6-316">Especificando AvroFormat</span><span class="sxs-lookup"><span data-stu-id="6eba6-316">Specifying AvroFormat</span></span>
<span data-ttu-id="6eba6-317">Se você deseja tooparse Olá Avro arquivos ou gravar dados saudação no formato Avro, defina Olá `format` `type` propriedade muito**AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="6eba6-317">If you want tooparse hello Avro files or write hello data in Avro format, set hello `format` `type` property too**AvroFormat**.</span></span> <span data-ttu-id="6eba6-318">Não é necessário toospecify as propriedades na seção de formato de saudação na seção de typeProperties hello.</span><span class="sxs-lookup"><span data-stu-id="6eba6-318">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="6eba6-319">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="6eba6-319">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="6eba6-320">formato de Avro toouse em uma tabela de Hive, você pode consultar muito[tutorial do Apache Hive](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span><span class="sxs-lookup"><span data-stu-id="6eba6-320">toouse Avro format in a Hive table, you can refer too[Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="6eba6-321">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="6eba6-321">Note hello following points:</span></span>  

* <span data-ttu-id="6eba6-322">Não há suporte para [Tipos de dados complexos](http://avro.apache.org/docs/current/spec.html#schema_complex) (registros, enumerações, matrizes, mapas, uniões e fixo).</span><span class="sxs-lookup"><span data-stu-id="6eba6-322">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions and fixed).</span></span>

### <a name="specifying-orcformat"></a><span data-ttu-id="6eba6-323">Especificando OrcFormat</span><span class="sxs-lookup"><span data-stu-id="6eba6-323">Specifying OrcFormat</span></span>
<span data-ttu-id="6eba6-324">Se você deseja tooparse Olá ORC arquivos ou gravar dados saudação no formato ORC, defina Olá `format` `type` propriedade muito**OrcFormat**.</span><span class="sxs-lookup"><span data-stu-id="6eba6-324">If you want tooparse hello ORC files or write hello data in ORC format, set hello `format` `type` property too**OrcFormat**.</span></span> <span data-ttu-id="6eba6-325">Não é necessário toospecify as propriedades na seção de formato de saudação na seção de typeProperties hello.</span><span class="sxs-lookup"><span data-stu-id="6eba6-325">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="6eba6-326">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="6eba6-326">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="6eba6-327">Se você não estiver copiando arquivos ORC **como-é** entre local e nuvem armazenamentos de dados, precisa tooinstall Olá 8 JRE (Java Runtime Environment) no seu computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="6eba6-327">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="6eba6-328">Um gateway de 64 bits exige JRE de 64 bits, enquanto um gateway de 32 bits exige JRE de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="6eba6-328">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="6eba6-329">Você pode encontrar as duas versões [aqui](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="6eba6-329">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="6eba6-330">Escolha Olá apropriado.</span><span class="sxs-lookup"><span data-stu-id="6eba6-330">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="6eba6-331">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="6eba6-331">Note hello following points:</span></span>

* <span data-ttu-id="6eba6-332">Não há suporte para tipos de dados complexos (STRUCT, MAP, LIST e UNION)</span><span class="sxs-lookup"><span data-stu-id="6eba6-332">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="6eba6-333">O arquivo ORC tem três [opções de compactação](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB e SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="6eba6-333">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="6eba6-334">O Data Factory dá suporte à leitura de dados de arquivo ORC em qualquer um dos formatos compactados acima.</span><span class="sxs-lookup"><span data-stu-id="6eba6-334">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="6eba6-335">Ele usa compactação Olá codec está nos dados de Olá Olá metadados tooread.</span><span class="sxs-lookup"><span data-stu-id="6eba6-335">It uses hello compression codec is in hello metadata tooread hello data.</span></span> <span data-ttu-id="6eba6-336">No entanto, ao gravar o arquivo ORC tooan, fábrica de dados escolhe ZLIB, que é o padrão de saudação para ORC.</span><span class="sxs-lookup"><span data-stu-id="6eba6-336">However, when writing tooan ORC file, Data Factory chooses ZLIB, which is hello default for ORC.</span></span> <span data-ttu-id="6eba6-337">Atualmente, não há nenhuma opção toooverride esse comportamento.</span><span class="sxs-lookup"><span data-stu-id="6eba6-337">Currently, there is no option toooverride this behavior.</span></span>

### <a name="specifying-parquetformat"></a><span data-ttu-id="6eba6-338">Especificando ParquetFormat</span><span class="sxs-lookup"><span data-stu-id="6eba6-338">Specifying ParquetFormat</span></span>
<span data-ttu-id="6eba6-339">Se você deseja tooparse Olá Parquet arquivos ou gravar dados saudação no formato Parquet, defina Olá `format` `type` propriedade muito**ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="6eba6-339">If you want tooparse hello Parquet files or write hello data in Parquet format, set hello `format` `type` property too**ParquetFormat**.</span></span> <span data-ttu-id="6eba6-340">Não é necessário toospecify as propriedades na seção de formato de saudação na seção de typeProperties hello.</span><span class="sxs-lookup"><span data-stu-id="6eba6-340">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="6eba6-341">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="6eba6-341">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="6eba6-342">Se você não estiver copiando arquivos Parquet **como-é** entre local e nuvem armazenamentos de dados, precisa tooinstall Olá 8 JRE (Java Runtime Environment) no seu computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="6eba6-342">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="6eba6-343">Um gateway de 64 bits exige JRE de 64 bits, enquanto um gateway de 32 bits exige JRE de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="6eba6-343">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="6eba6-344">Você pode encontrar as duas versões [aqui](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="6eba6-344">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="6eba6-345">Escolha Olá apropriado.</span><span class="sxs-lookup"><span data-stu-id="6eba6-345">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="6eba6-346">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="6eba6-346">Note hello following points:</span></span>

* <span data-ttu-id="6eba6-347">Não há suporte para tipos de dados complexos (MAP, LIST)</span><span class="sxs-lookup"><span data-stu-id="6eba6-347">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="6eba6-348">Arquivo parquet tem Olá opções de compactação a seguir: NONE, SNAPPY, GZIP e LZO.</span><span class="sxs-lookup"><span data-stu-id="6eba6-348">Parquet file has hello following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="6eba6-349">O Data Factory dá suporte à leitura de dados de arquivo ORC em qualquer um dos formatos compactados acima.</span><span class="sxs-lookup"><span data-stu-id="6eba6-349">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="6eba6-350">Ele usa o codec de compactação de saudação nos dados de Olá Olá metadados tooread.</span><span class="sxs-lookup"><span data-stu-id="6eba6-350">It uses hello compression codec in hello metadata tooread hello data.</span></span> <span data-ttu-id="6eba6-351">No entanto, ao gravar o arquivo de Parquet tooa, fábrica de dados escolhe SNAPPY, que é saudação padrão para o formato de Parquet.</span><span class="sxs-lookup"><span data-stu-id="6eba6-351">However, when writing tooa Parquet file, Data Factory chooses SNAPPY, which is hello default for Parquet format.</span></span> <span data-ttu-id="6eba6-352">Atualmente, não há nenhuma opção toooverride esse comportamento.</span><span class="sxs-lookup"><span data-stu-id="6eba6-352">Currently, there is no option toooverride this behavior.</span></span>
