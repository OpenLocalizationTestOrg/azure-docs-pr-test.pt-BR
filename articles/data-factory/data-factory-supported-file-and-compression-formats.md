---
title: "formatos de compactação e aaaFile na fábrica de dados do Azure | Microsoft Docs"
description: Saiba mais sobre os formatos de arquivo hello com suporte do Azure Data Factory.
keywords: "dados de blob, cópia de blobs do azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 9d40517b059fc533776bcc088db8c531ee5b003d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="file-and-compression-formats-supported-by-azure-data-factory"></a><span data-ttu-id="f2f76-104">Formatos de arquivo aos quais o Azure Data Factory dá suporte</span><span class="sxs-lookup"><span data-stu-id="f2f76-104">File and compression formats supported by Azure Data Factory</span></span>
<span data-ttu-id="f2f76-105">*Este tópico se aplica a toohello conectores a seguir: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [BLOBs do Azure](data-factory-azure-blob-connector.md), [repositório Azure Data Lake](data-factory-azure-datalake-connector.md), [sistema de arquivos](data-factory-onprem-file-system-connector.md), [ FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), e [SFTP](data-factory-sftp-connector.md).*</span><span class="sxs-lookup"><span data-stu-id="f2f76-105">*This topic applies toohello following connectors: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [File System](data-factory-onprem-file-system-connector.md), [FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), and [SFTP](data-factory-sftp-connector.md).*</span></span>

<span data-ttu-id="f2f76-106">A fábrica de dados do Azure dá suporte a saudação tipos de arquivo de formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2f76-106">Azure Data Factory supports hello following file format types:</span></span>

* [<span data-ttu-id="f2f76-107">Formato de texto</span><span class="sxs-lookup"><span data-stu-id="f2f76-107">Text format</span></span>](#text-format)
* [<span data-ttu-id="f2f76-108">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="f2f76-108">JSON format</span></span>](#json-format)
* [<span data-ttu-id="f2f76-109">Formato Avro</span><span class="sxs-lookup"><span data-stu-id="f2f76-109">Avro format</span></span>](#avro-format)
* [<span data-ttu-id="f2f76-110">Formato ORC</span><span class="sxs-lookup"><span data-stu-id="f2f76-110">ORC format</span></span>](#orc-format)
* [<span data-ttu-id="f2f76-111">Formato Parquet</span><span class="sxs-lookup"><span data-stu-id="f2f76-111">Parquet format</span></span>](#parquet-format)

## <a name="text-format"></a><span data-ttu-id="f2f76-112">Formato de texto</span><span class="sxs-lookup"><span data-stu-id="f2f76-112">Text format</span></span>
<span data-ttu-id="f2f76-113">Se você desejar tooread de um arquivo de texto ou gravar o arquivo de texto tooa, defina Olá `type` propriedade Olá `format` seção do conjunto de dados de saudação muito**TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="f2f76-113">If you want tooread from a text file or write tooa text file, set hello `type` property in hello `format` section of hello dataset too**TextFormat**.</span></span> <span data-ttu-id="f2f76-114">Você também pode especificar o seguinte Olá **opcional** propriedades no hello `format` seção.</span><span class="sxs-lookup"><span data-stu-id="f2f76-114">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="f2f76-115">Consulte [TextFormat exemplo](#textformat-example) seção sobre como tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="f2f76-115">See [TextFormat example](#textformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="f2f76-116">Propriedade</span><span class="sxs-lookup"><span data-stu-id="f2f76-116">Property</span></span> | <span data-ttu-id="f2f76-117">Descrição</span><span class="sxs-lookup"><span data-stu-id="f2f76-117">Description</span></span> | <span data-ttu-id="f2f76-118">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="f2f76-118">Allowed values</span></span> | <span data-ttu-id="f2f76-119">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="f2f76-119">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f2f76-120">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="f2f76-120">columnDelimiter</span></span> |<span data-ttu-id="f2f76-121">caractere de saudação usado tooseparate colunas em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="f2f76-121">hello character used tooseparate columns in a file.</span></span> <span data-ttu-id="f2f76-122">Você pode considerar toouse um caractere não imprimível raro que provavelmente não pode existe em seus dados.</span><span class="sxs-lookup"><span data-stu-id="f2f76-122">You can consider toouse a rare unprintable char that may not likely exists in your data.</span></span> <span data-ttu-id="f2f76-123">Por exemplo, especifique "\u0001", que representa o SOH (início do título).</span><span class="sxs-lookup"><span data-stu-id="f2f76-123">For example, specify "\u0001", which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="f2f76-124">Somente um caractere é permitido.</span><span class="sxs-lookup"><span data-stu-id="f2f76-124">Only one character is allowed.</span></span> <span data-ttu-id="f2f76-125">Olá **padrão** valor é **vírgula (',')**.</span><span class="sxs-lookup"><span data-stu-id="f2f76-125">hello **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="f2f76-126">toouse um caractere Unicode, consulte muito[caracteres Unicode](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello código correspondente para ele.</span><span class="sxs-lookup"><span data-stu-id="f2f76-126">toouse a Unicode character, refer too[Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello corresponding code for it.</span></span> |<span data-ttu-id="f2f76-127">Não</span><span class="sxs-lookup"><span data-stu-id="f2f76-127">No</span></span> |
| <span data-ttu-id="f2f76-128">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="f2f76-128">rowDelimiter</span></span> |<span data-ttu-id="f2f76-129">caractere de saudação usado tooseparate linhas em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="f2f76-129">hello character used tooseparate rows in a file.</span></span> |<span data-ttu-id="f2f76-130">Somente um caractere é permitido.</span><span class="sxs-lookup"><span data-stu-id="f2f76-130">Only one character is allowed.</span></span> <span data-ttu-id="f2f76-131">Olá **padrão** valor é qualquer um dos valores a seguir na leitura de saudação: **["\r\n", "\r", "\n"]** e **"\r\n"** na gravação.</span><span class="sxs-lookup"><span data-stu-id="f2f76-131">hello **default** value is any of hello following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="f2f76-132">Não</span><span class="sxs-lookup"><span data-stu-id="f2f76-132">No</span></span> |
| <span data-ttu-id="f2f76-133">escapeChar</span><span class="sxs-lookup"><span data-stu-id="f2f76-133">escapeChar</span></span> |<span data-ttu-id="f2f76-134">caractere especial Olá usado tooescape um delimitador de coluna no conteúdo de saudação do arquivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="f2f76-134">hello special character used tooescape a column delimiter in hello content of input file.</span></span> <br/><br/><span data-ttu-id="f2f76-135">Não é possível especificar ambos escapeChar e quoteChar para uma tabela.</span><span class="sxs-lookup"><span data-stu-id="f2f76-135">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="f2f76-136">Somente um caractere é permitido.</span><span class="sxs-lookup"><span data-stu-id="f2f76-136">Only one character is allowed.</span></span> <span data-ttu-id="f2f76-137">Nenhum valor padrão.</span><span class="sxs-lookup"><span data-stu-id="f2f76-137">No default value.</span></span> <br/><br/><span data-ttu-id="f2f76-138">Exemplo: se você tem vírgula (', ') como delimitador de coluna hello, mas você deseja o caractere de vírgula Olá toohave no texto de saudação (exemplo: "Olá, mundo"), você pode definir o '$' como o caractere de escape hello e usar a cadeia de caracteres "$Oi, mundo" na fonte de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2f76-138">Example: if you have comma (',') as hello column delimiter but you want toohave hello comma character in hello text (example: "Hello, world"), you can define ‘$’ as hello escape character and use string "Hello$, world" in hello source.</span></span> |<span data-ttu-id="f2f76-139">Não</span><span class="sxs-lookup"><span data-stu-id="f2f76-139">No</span></span> |
| <span data-ttu-id="f2f76-140">quoteChar</span><span class="sxs-lookup"><span data-stu-id="f2f76-140">quoteChar</span></span> |<span data-ttu-id="f2f76-141">caractere de saudação usado tooquote um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="f2f76-141">hello character used tooquote a string value.</span></span> <span data-ttu-id="f2f76-142">delimitadores de coluna e linha Hello dentro de caracteres de aspas Olá seriam tratadas como parte do valor de cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2f76-142">hello column and row delimiters inside hello quote characters would be treated as part of hello string value.</span></span> <span data-ttu-id="f2f76-143">Essa propriedade é aplicável tooboth entrada e conjuntos de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="f2f76-143">This property is applicable tooboth input and output datasets.</span></span><br/><br/><span data-ttu-id="f2f76-144">Não é possível especificar ambos escapeChar e quoteChar para uma tabela.</span><span class="sxs-lookup"><span data-stu-id="f2f76-144">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="f2f76-145">Somente um caractere é permitido.</span><span class="sxs-lookup"><span data-stu-id="f2f76-145">Only one character is allowed.</span></span> <span data-ttu-id="f2f76-146">Nenhum valor padrão.</span><span class="sxs-lookup"><span data-stu-id="f2f76-146">No default value.</span></span> <br/><br/><span data-ttu-id="f2f76-147">Por exemplo, se você tem vírgula (', ') como delimitador de coluna hello, mas você deseja toohave caractere de vírgula no texto de saudação (exemplo: < Olá, mundo >), você pode definir "(aspas duplas) como Olá caractere de aspas e usar a cadeia de caracteres hello"Olá, mundo"na fonte de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2f76-147">For example, if you have comma (',') as hello column delimiter but you want toohave comma character in hello text (example: <Hello, world>), you can define " (double quote) as hello quote character and use hello string "Hello, world" in hello source.</span></span> |<span data-ttu-id="f2f76-148">Não</span><span class="sxs-lookup"><span data-stu-id="f2f76-148">No</span></span> |
| <span data-ttu-id="f2f76-149">nullValue</span><span class="sxs-lookup"><span data-stu-id="f2f76-149">nullValue</span></span> |<span data-ttu-id="f2f76-150">Um ou mais caracteres usados toorepresent um valor nulo.</span><span class="sxs-lookup"><span data-stu-id="f2f76-150">One or more characters used toorepresent a null value.</span></span> |<span data-ttu-id="f2f76-151">Um ou mais caracteres.</span><span class="sxs-lookup"><span data-stu-id="f2f76-151">One or more characters.</span></span> <span data-ttu-id="f2f76-152">Olá **padrão** os valores são **"\N" e "NULL"** na leitura e **"\N"** na gravação.</span><span class="sxs-lookup"><span data-stu-id="f2f76-152">hello **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="f2f76-153">Não</span><span class="sxs-lookup"><span data-stu-id="f2f76-153">No</span></span> |
| <span data-ttu-id="f2f76-154">encodingName</span><span class="sxs-lookup"><span data-stu-id="f2f76-154">encodingName</span></span> |<span data-ttu-id="f2f76-155">Especifique o nome de codificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2f76-155">Specify hello encoding name.</span></span> |<span data-ttu-id="f2f76-156">Um nomes de codificação válido.</span><span class="sxs-lookup"><span data-stu-id="f2f76-156">A valid encoding name.</span></span> <span data-ttu-id="f2f76-157">Consulte [Propriedade Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2f76-157">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="f2f76-158">Por exemplo: windows-1250 ou shift_jis.</span><span class="sxs-lookup"><span data-stu-id="f2f76-158">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="f2f76-159">Olá **padrão** valor é **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="f2f76-159">hello **default** value is **UTF-8**.</span></span> |<span data-ttu-id="f2f76-160">Não</span><span class="sxs-lookup"><span data-stu-id="f2f76-160">No</span></span> |
| <span data-ttu-id="f2f76-161">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="f2f76-161">firstRowAsHeader</span></span> |<span data-ttu-id="f2f76-162">Especifica se tooconsider Olá a primeira linha como cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="f2f76-162">Specifies whether tooconsider hello first row as a header.</span></span> <span data-ttu-id="f2f76-163">Para um conjunto de dados de entrada, o Data Factory lê a primeira linha como cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="f2f76-163">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="f2f76-164">Para um conjunto de dados de saída, o Data Factory lê a primeira linha como cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="f2f76-164">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="f2f76-165">Veja [Cenários para usar o `firstRowAsHeader` e o `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) para cenários de exemplo.</span><span class="sxs-lookup"><span data-stu-id="f2f76-165">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="f2f76-166">True </span><span class="sxs-lookup"><span data-stu-id="f2f76-166">True</span></span><br/><span data-ttu-id="f2f76-167"><b>False (padrão)</b></span><span class="sxs-lookup"><span data-stu-id="f2f76-167"><b>False (default)</b></span></span> |<span data-ttu-id="f2f76-168">Não</span><span class="sxs-lookup"><span data-stu-id="f2f76-168">No</span></span> |
| <span data-ttu-id="f2f76-169">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="f2f76-169">skipLineCount</span></span> |<span data-ttu-id="f2f76-170">Indica o número de saudação de linhas tooskip ao ler dados de arquivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="f2f76-170">Indicates hello number of rows tooskip when reading data from input files.</span></span> <span data-ttu-id="f2f76-171">Se skipLineCount e firstRowAsHeader forem especificados, linhas de saudação são ignoradas primeiro e, em seguida, as informações de cabeçalho de saudação é lido do arquivo de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="f2f76-171">If both skipLineCount and firstRowAsHeader are specified, hello lines are skipped first and then hello header information is read from hello input file.</span></span> <br/><br/><span data-ttu-id="f2f76-172">Veja [Cenários para usar o `firstRowAsHeader` e o `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) para cenários de exemplo.</span><span class="sxs-lookup"><span data-stu-id="f2f76-172">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="f2f76-173">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="f2f76-173">Integer</span></span> |<span data-ttu-id="f2f76-174">Não</span><span class="sxs-lookup"><span data-stu-id="f2f76-174">No</span></span> |
| <span data-ttu-id="f2f76-175">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="f2f76-175">treatEmptyAsNull</span></span> |<span data-ttu-id="f2f76-176">Especifica se a cadeia de tootreat nula ou vazia como nula valor quando ler dados de um arquivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="f2f76-176">Specifies whether tootreat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="f2f76-177">**True (padrão)**</span><span class="sxs-lookup"><span data-stu-id="f2f76-177">**True (default)**</span></span><br/><span data-ttu-id="f2f76-178">Falso</span><span class="sxs-lookup"><span data-stu-id="f2f76-178">False</span></span> |<span data-ttu-id="f2f76-179">Não</span><span class="sxs-lookup"><span data-stu-id="f2f76-179">No</span></span> |

### <a name="textformat-example"></a><span data-ttu-id="f2f76-180">Exemplo de TextFormat</span><span class="sxs-lookup"><span data-stu-id="f2f76-180">TextFormat example</span></span>
<span data-ttu-id="f2f76-181">Em Olá definição JSON para um conjunto de dados a seguir, algumas das propriedades opcionais Olá são especificadas.</span><span class="sxs-lookup"><span data-stu-id="f2f76-181">In hello following JSON definition for a dataset, some of hello optional properties are specified.</span></span>

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

<span data-ttu-id="f2f76-182">toouse um `escapeChar` em vez de `quoteChar`, substitua a linha hello com `quoteChar` com hello escapeChar a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2f76-182">toouse an `escapeChar` instead of `quoteChar`, replace hello line with `quoteChar` with hello following escapeChar:</span></span>

```json
"escapeChar": "$",
```

### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="f2f76-183">Cenários de uso de firstRowAsHeader e skipLineCount</span><span class="sxs-lookup"><span data-stu-id="f2f76-183">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="f2f76-184">Você está copiando um arquivo de texto do arquivo fonte tooa e gostaria de tooadd uma linha de cabeçalho que contém metadados do esquema de saudação (por exemplo: esquema SQL).</span><span class="sxs-lookup"><span data-stu-id="f2f76-184">You are copying from a non-file source tooa text file and would like tooadd a header line containing hello schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="f2f76-185">Especifique `firstRowAsHeader` como true no conjunto de dados de saída de saudação para esse cenário.</span><span class="sxs-lookup"><span data-stu-id="f2f76-185">Specify `firstRowAsHeader` as true in hello output dataset for this scenario.</span></span>
* <span data-ttu-id="f2f76-186">Você está copiando um arquivo de texto que contém um coletor de arquivo do cabeçalho linha tooa e deseja toodrop de linha.</span><span class="sxs-lookup"><span data-stu-id="f2f76-186">You are copying from a text file containing a header line tooa non-file sink and would like toodrop that line.</span></span> <span data-ttu-id="f2f76-187">Especifique `firstRowAsHeader` como true no conjunto de dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="f2f76-187">Specify `firstRowAsHeader` as true in hello input dataset.</span></span>
* <span data-ttu-id="f2f76-188">Você está copiando um arquivo de texto e deseja tooskip algumas linhas no início de saudação que não contêm nenhuma informação de cabeçalho ou de dados.</span><span class="sxs-lookup"><span data-stu-id="f2f76-188">You are copying from a text file and want tooskip a few lines at hello beginning that contain no data or header information.</span></span> <span data-ttu-id="f2f76-189">Especifique `skipLineCount` tooindicate Olá número de linhas toobe ignorados.</span><span class="sxs-lookup"><span data-stu-id="f2f76-189">Specify `skipLineCount` tooindicate hello number of lines toobe skipped.</span></span> <span data-ttu-id="f2f76-190">Se o resto de saudação do arquivo hello contém uma linha de cabeçalho, você também pode especificar `firstRowAsHeader`.</span><span class="sxs-lookup"><span data-stu-id="f2f76-190">If hello rest of hello file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="f2f76-191">Se ambos os `skipLineCount` e `firstRowAsHeader` forem especificados, linhas de saudação são ignoradas pela primeira vez e, em seguida, as informações de cabeçalho de saudação é lido do arquivo de entrada hello</span><span class="sxs-lookup"><span data-stu-id="f2f76-191">If both `skipLineCount` and `firstRowAsHeader` are specified, hello lines are skipped first and then hello header information is read from hello input file</span></span>

## <a name="json-format"></a><span data-ttu-id="f2f76-192">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="f2f76-192">JSON format</span></span>
<span data-ttu-id="f2f76-193">muito**importação/exportação de um arquivo JSON como-está em de banco de dados do Azure Cosmos**, consulte Olá [documentos JSON de importação/exportação](data-factory-azure-documentdb-connector.md#importexport-json-documents) seção [mover dados para/de banco de dados do Azure Cosmos](data-factory-azure-documentdb-connector.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="f2f76-193">too**import/export a JSON file as-is into/from Azure Cosmos DB**, hello see [Import/export JSON documents](data-factory-azure-documentdb-connector.md#importexport-json-documents) section in [Move data to/from Azure Cosmos DB](data-factory-azure-documentdb-connector.md) article.</span></span>

<span data-ttu-id="f2f76-194">Se você deseja tooparse Olá JSON arquivos ou gravar dados saudação no formato JSON, defina Olá `type` propriedade Olá `format` seção muito**JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="f2f76-194">If you want tooparse hello JSON files or write hello data in JSON format, set hello `type` property in hello `format` section too**JsonFormat**.</span></span> <span data-ttu-id="f2f76-195">Você também pode especificar o seguinte Olá **opcional** propriedades no hello `format` seção.</span><span class="sxs-lookup"><span data-stu-id="f2f76-195">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="f2f76-196">Consulte [JsonFormat exemplo](#jsonformat-example) seção sobre como tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="f2f76-196">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="f2f76-197">Propriedade</span><span class="sxs-lookup"><span data-stu-id="f2f76-197">Property</span></span> | <span data-ttu-id="f2f76-198">Descrição</span><span class="sxs-lookup"><span data-stu-id="f2f76-198">Description</span></span> | <span data-ttu-id="f2f76-199">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="f2f76-199">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f2f76-200">filePattern</span><span class="sxs-lookup"><span data-stu-id="f2f76-200">filePattern</span></span> |<span data-ttu-id="f2f76-201">Indica padrão Olá dos dados armazenados em cada arquivo JSON.</span><span class="sxs-lookup"><span data-stu-id="f2f76-201">Indicate hello pattern of data stored in each JSON file.</span></span> <span data-ttu-id="f2f76-202">Os valores permitidos são: **setOfObjects** e **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="f2f76-202">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="f2f76-203">Olá **padrão** valor é **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="f2f76-203">hello **default** value is **setOfObjects**.</span></span> <span data-ttu-id="f2f76-204">Veja a seção [Padrões de arquivo JSON](#json-file-patterns) para obter detalhes sobre esses padrões.</span><span class="sxs-lookup"><span data-stu-id="f2f76-204">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="f2f76-205">Não</span><span class="sxs-lookup"><span data-stu-id="f2f76-205">No</span></span> |
| <span data-ttu-id="f2f76-206">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="f2f76-206">jsonNodeReference</span></span> | <span data-ttu-id="f2f76-207">Se você deseja tooiterate e extrair dados de objetos hello dentro de uma matriz de campo com hello mesmo padrão, especifique o caminho do JSON Olá dessa matriz.</span><span class="sxs-lookup"><span data-stu-id="f2f76-207">If you want tooiterate and extract data from hello objects inside an array field with hello same pattern, specify hello JSON path of that array.</span></span> <span data-ttu-id="f2f76-208">Esta propriedade só terá suporte na cópia de dados de arquivos JSON.</span><span class="sxs-lookup"><span data-stu-id="f2f76-208">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="f2f76-209">Não</span><span class="sxs-lookup"><span data-stu-id="f2f76-209">No</span></span> |
| <span data-ttu-id="f2f76-210">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="f2f76-210">jsonPathDefinition</span></span> | <span data-ttu-id="f2f76-211">Especifique a expressão de caminho JSON Olá para cada mapeamento de coluna com um nome de coluna personalizada (começam com letras minúsculas).</span><span class="sxs-lookup"><span data-stu-id="f2f76-211">Specify hello JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="f2f76-212">Esta propriedade só terá suporte na cópia de dados de arquivos JSON, e você pode extrair dados de objeto ou de matriz.</span><span class="sxs-lookup"><span data-stu-id="f2f76-212">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="f2f76-213">Para os campos no objeto raiz, começar com $ raiz; para campos de matriz de saudação escolhida pelo `jsonNodeReference` propriedade, início do elemento da matriz hello.</span><span class="sxs-lookup"><span data-stu-id="f2f76-213">For fields under root object, start with root $; for fields inside hello array chosen by `jsonNodeReference` property, start from hello array element.</span></span> <span data-ttu-id="f2f76-214">Consulte [JsonFormat exemplo](#jsonformat-example) seção sobre como tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="f2f76-214">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span> | <span data-ttu-id="f2f76-215">Não</span><span class="sxs-lookup"><span data-stu-id="f2f76-215">No</span></span> |
| <span data-ttu-id="f2f76-216">encodingName</span><span class="sxs-lookup"><span data-stu-id="f2f76-216">encodingName</span></span> |<span data-ttu-id="f2f76-217">Especifique o nome de codificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2f76-217">Specify hello encoding name.</span></span> <span data-ttu-id="f2f76-218">Para obter lista de saudação de nomes válidos de codificação, consulte: [encodingname](https://msdn.microsoft.com/library/system.text.encoding.aspx) propriedade.</span><span class="sxs-lookup"><span data-stu-id="f2f76-218">For hello list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="f2f76-219">Por exemplo: windows-1250 ou shift_jis.</span><span class="sxs-lookup"><span data-stu-id="f2f76-219">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="f2f76-220">Olá **padrão** valor é: **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="f2f76-220">hello **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="f2f76-221">Não</span><span class="sxs-lookup"><span data-stu-id="f2f76-221">No</span></span> |
| <span data-ttu-id="f2f76-222">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="f2f76-222">nestingSeparator</span></span> |<span data-ttu-id="f2f76-223">Caractere usado tooseparate níveis de aninhamento.</span><span class="sxs-lookup"><span data-stu-id="f2f76-223">Character that is used tooseparate nesting levels.</span></span> <span data-ttu-id="f2f76-224">valor padrão de saudação é '.' (ponto).</span><span class="sxs-lookup"><span data-stu-id="f2f76-224">hello default value is '.' (dot).</span></span> |<span data-ttu-id="f2f76-225">Não</span><span class="sxs-lookup"><span data-stu-id="f2f76-225">No</span></span> |

### <a name="json-file-patterns"></a><span data-ttu-id="f2f76-226">Padrões de arquivo JSON</span><span class="sxs-lookup"><span data-stu-id="f2f76-226">JSON file patterns</span></span>

<span data-ttu-id="f2f76-227">Atividade de cópia pode analisar Olá padrões dos arquivos JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2f76-227">Copy activity can parse hello following patterns of JSON files:</span></span>

- <span data-ttu-id="f2f76-228">**Tipo I: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="f2f76-228">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="f2f76-229">Cada arquivo contém um único objeto ou vários objetos concatenados/delimitados por linhas.</span><span class="sxs-lookup"><span data-stu-id="f2f76-229">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="f2f76-230">Quando essa opção é escolhida em um conjunto de dados de saída, a atividade de cópia produz um único arquivo JSON com cada objeto por linha (delimitados por linha).</span><span class="sxs-lookup"><span data-stu-id="f2f76-230">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="f2f76-231">**Exemplo de JSON de objeto único**</span><span class="sxs-lookup"><span data-stu-id="f2f76-231">**single object JSON example**</span></span>

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

    * <span data-ttu-id="f2f76-232">**Exemplo de JSON delimitado por linha**</span><span class="sxs-lookup"><span data-stu-id="f2f76-232">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="f2f76-233">**Exemplo de JSON concatenado**</span><span class="sxs-lookup"><span data-stu-id="f2f76-233">**concatenated JSON example**</span></span>

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

- <span data-ttu-id="f2f76-234">**Tipo II: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="f2f76-234">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="f2f76-235">Cada arquivo contém uma matriz de objetos.</span><span class="sxs-lookup"><span data-stu-id="f2f76-235">Each file contains an array of objects.</span></span>

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

### <a name="jsonformat-example"></a><span data-ttu-id="f2f76-236">Exemplo de JsonFormat</span><span class="sxs-lookup"><span data-stu-id="f2f76-236">JsonFormat example</span></span>

<span data-ttu-id="f2f76-237">**Caso 1: copiar dados de arquivos JSON**</span><span class="sxs-lookup"><span data-stu-id="f2f76-237">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="f2f76-238">Consulte Olá dois exemplos a seguir ao copiar dados de arquivos JSON.</span><span class="sxs-lookup"><span data-stu-id="f2f76-238">See hello following two samples when copying data from JSON files.</span></span> <span data-ttu-id="f2f76-239">Olá toonote pontos genérico:</span><span class="sxs-lookup"><span data-stu-id="f2f76-239">hello generic points toonote:</span></span>

<span data-ttu-id="f2f76-240">**Exemplo 1: extrair dados de objeto e de matriz**</span><span class="sxs-lookup"><span data-stu-id="f2f76-240">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="f2f76-241">Neste exemplo, você espera que um objeto JSON de raiz mapeia toosingle registro na tabela de resultados.</span><span class="sxs-lookup"><span data-stu-id="f2f76-241">In this sample, you expect one root JSON object maps toosingle record in tabular result.</span></span> <span data-ttu-id="f2f76-242">Se você tiver um arquivo JSON com hello conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2f76-242">If you have a JSON file with hello following content:</span></span>  

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
<span data-ttu-id="f2f76-243">e você deseja toocopy-lo em uma tabela do SQL Azure no seguinte Olá Formatar, extraindo dados de objetos e a matriz:</span><span class="sxs-lookup"><span data-stu-id="f2f76-243">and you want toocopy it into an Azure SQL table in hello following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="f2f76-244">ID</span><span class="sxs-lookup"><span data-stu-id="f2f76-244">id</span></span> | <span data-ttu-id="f2f76-245">deviceType</span><span class="sxs-lookup"><span data-stu-id="f2f76-245">deviceType</span></span> | <span data-ttu-id="f2f76-246">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="f2f76-246">targetResourceType</span></span> | <span data-ttu-id="f2f76-247">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="f2f76-247">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="f2f76-248">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="f2f76-248">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="f2f76-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="f2f76-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="f2f76-250">Computador</span><span class="sxs-lookup"><span data-stu-id="f2f76-250">PC</span></span> | <span data-ttu-id="f2f76-251">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="f2f76-251">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="f2f76-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="f2f76-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="f2f76-253">13/01/2017 11:24:37</span><span class="sxs-lookup"><span data-stu-id="f2f76-253">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="f2f76-254">conjunto de dados de entrada de saudação com **JsonFormat** tipo é definido da seguinte maneira: (definição parcial com partes relevantes apenas Olá).</span><span class="sxs-lookup"><span data-stu-id="f2f76-254">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="f2f76-255">Mais especificamente:</span><span class="sxs-lookup"><span data-stu-id="f2f76-255">More specifically:</span></span>

- <span data-ttu-id="f2f76-256">`structure`seção define os nomes de coluna de saudação personalizada e o tipo de dados correspondente Olá ao converter dados tootabular.</span><span class="sxs-lookup"><span data-stu-id="f2f76-256">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="f2f76-257">Esta seção é **opcional** , a menos que você precisa toodo mapeamento de coluna.</span><span class="sxs-lookup"><span data-stu-id="f2f76-257">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="f2f76-258">Consulte [mapear colunas de conjunto de dados fonte dataset colunas toodestination](data-factory-map-columns.md) seção para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="f2f76-258">See [Map source dataset columns toodestination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="f2f76-259">`jsonPathDefinition`Especifica o caminho JSON de saudação para cada coluna que indica onde tooextract Olá dados.</span><span class="sxs-lookup"><span data-stu-id="f2f76-259">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="f2f76-260">toocopy dados da matriz, você pode usar **array [x] .property** tooextract valor Olá considerando a propriedade do objeto de x ª hello, ou você pode usar  **matriz [*] .property** toofind valor de saudação de qualquer objeto que contém essa propriedade.</span><span class="sxs-lookup"><span data-stu-id="f2f76-260">toocopy data from array, you can use **array[x].property** tooextract value of hello given property from hello xth object, or you can use **array[*].property** toofind hello value from any object containing such property.</span></span>

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

<span data-ttu-id="f2f76-261">**Exemplo 2: cruzada aplicar vários objetos com o mesmo padrão da matriz de saudação**</span><span class="sxs-lookup"><span data-stu-id="f2f76-261">**Sample 2: cross apply multiple objects with hello same pattern from array**</span></span>

<span data-ttu-id="f2f76-262">Neste exemplo, você espera que um objeto JSON de raiz tootransform em vários registros na tabela de resultados.</span><span class="sxs-lookup"><span data-stu-id="f2f76-262">In this sample, you expect tootransform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="f2f76-263">Se você tiver um arquivo JSON com hello conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2f76-263">If you have a JSON file with hello following content:</span></span>  

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
<span data-ttu-id="f2f76-264">e você deseja toocopy-lo em uma tabela do SQL Azure no seguinte Olá Formatar, mesclando dados hello dentro da matriz de saudação e cross join com informações de raiz comum hello:</span><span class="sxs-lookup"><span data-stu-id="f2f76-264">and you want toocopy it into an Azure SQL table in hello following format, by flattening hello data inside hello array and cross join with hello common root info:</span></span>

| <span data-ttu-id="f2f76-265">ordernumber</span><span class="sxs-lookup"><span data-stu-id="f2f76-265">ordernumber</span></span> | <span data-ttu-id="f2f76-266">orderdate</span><span class="sxs-lookup"><span data-stu-id="f2f76-266">orderdate</span></span> | <span data-ttu-id="f2f76-267">order_pd</span><span class="sxs-lookup"><span data-stu-id="f2f76-267">order_pd</span></span> | <span data-ttu-id="f2f76-268">order_price</span><span class="sxs-lookup"><span data-stu-id="f2f76-268">order_price</span></span> | <span data-ttu-id="f2f76-269">city</span><span class="sxs-lookup"><span data-stu-id="f2f76-269">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="f2f76-270">01</span><span class="sxs-lookup"><span data-stu-id="f2f76-270">01</span></span> | <span data-ttu-id="f2f76-271">20170122</span><span class="sxs-lookup"><span data-stu-id="f2f76-271">20170122</span></span> | <span data-ttu-id="f2f76-272">P1</span><span class="sxs-lookup"><span data-stu-id="f2f76-272">P1</span></span> | <span data-ttu-id="f2f76-273">23</span><span class="sxs-lookup"><span data-stu-id="f2f76-273">23</span></span> | <span data-ttu-id="f2f76-274">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="f2f76-274">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="f2f76-275">01</span><span class="sxs-lookup"><span data-stu-id="f2f76-275">01</span></span> | <span data-ttu-id="f2f76-276">20170122</span><span class="sxs-lookup"><span data-stu-id="f2f76-276">20170122</span></span> | <span data-ttu-id="f2f76-277">P2</span><span class="sxs-lookup"><span data-stu-id="f2f76-277">P2</span></span> | <span data-ttu-id="f2f76-278">13</span><span class="sxs-lookup"><span data-stu-id="f2f76-278">13</span></span> | <span data-ttu-id="f2f76-279">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="f2f76-279">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="f2f76-280">01</span><span class="sxs-lookup"><span data-stu-id="f2f76-280">01</span></span> | <span data-ttu-id="f2f76-281">20170122</span><span class="sxs-lookup"><span data-stu-id="f2f76-281">20170122</span></span> | <span data-ttu-id="f2f76-282">P3</span><span class="sxs-lookup"><span data-stu-id="f2f76-282">P3</span></span> | <span data-ttu-id="f2f76-283">231</span><span class="sxs-lookup"><span data-stu-id="f2f76-283">231</span></span> | <span data-ttu-id="f2f76-284">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="f2f76-284">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="f2f76-285">conjunto de dados de entrada de saudação com **JsonFormat** tipo é definido da seguinte maneira: (definição parcial com partes relevantes apenas Olá).</span><span class="sxs-lookup"><span data-stu-id="f2f76-285">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="f2f76-286">Mais especificamente:</span><span class="sxs-lookup"><span data-stu-id="f2f76-286">More specifically:</span></span>

- <span data-ttu-id="f2f76-287">`structure`seção define os nomes de coluna de saudação personalizada e o tipo de dados correspondente Olá ao converter dados tootabular.</span><span class="sxs-lookup"><span data-stu-id="f2f76-287">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="f2f76-288">Esta seção é **opcional** , a menos que você precisa toodo mapeamento de coluna.</span><span class="sxs-lookup"><span data-stu-id="f2f76-288">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="f2f76-289">Consulte [mapear colunas de conjunto de dados fonte dataset colunas toodestination](data-factory-map-columns.md) seção para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="f2f76-289">See [Map source dataset columns toodestination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="f2f76-290">`jsonNodeReference`indica tooiterate e extrair dados de objetos Olá Olá mesmo padrão em **matriz** orderlines.</span><span class="sxs-lookup"><span data-stu-id="f2f76-290">`jsonNodeReference` indicates tooiterate and extract data from hello objects with hello same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="f2f76-291">`jsonPathDefinition`Especifica o caminho JSON de saudação para cada coluna que indica onde tooextract Olá dados.</span><span class="sxs-lookup"><span data-stu-id="f2f76-291">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="f2f76-292">Neste exemplo, "ordernumber", "orderdate" e "cidade" estão no objeto raiz com o caminho JSON iniciar com"$", enquanto "order_pd" e "order_price" são definidos com caminho derivado do elemento de matriz Olá sem "$"..</span><span class="sxs-lookup"><span data-stu-id="f2f76-292">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from hello array element without "$.".</span></span>

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

<span data-ttu-id="f2f76-293">**Observe Olá pontos a seguir:**</span><span class="sxs-lookup"><span data-stu-id="f2f76-293">**Note hello following points:**</span></span>

* <span data-ttu-id="f2f76-294">Se hello `structure` e `jsonPathDefinition` não estão definidos no conjunto de dados de Data Factory hello, hello atividade de cópia detecta Olá esquema do objeto primeiro hello e mesclar objeto inteiro hello.</span><span class="sxs-lookup"><span data-stu-id="f2f76-294">If hello `structure` and `jsonPathDefinition` are not defined in hello Data Factory dataset, hello Copy Activity detects hello schema from hello first object and flatten hello whole object.</span></span>
* <span data-ttu-id="f2f76-295">Se a entrada JSON Olá tem uma matriz, por padrão hello atividade de cópia converte Olá matriz inteira valor em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="f2f76-295">If hello JSON input has an array, by default hello Copy Activity converts hello entire array value into a string.</span></span> <span data-ttu-id="f2f76-296">Você pode escolher dados tooextract usando `jsonNodeReference` e/ou `jsonPathDefinition`, ou ignorá-la não especificando na `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="f2f76-296">You can choose tooextract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="f2f76-297">Se não houver duplicados Olá de nomes no mesmo nível, hello atividade de cópia selecionará Olá último.</span><span class="sxs-lookup"><span data-stu-id="f2f76-297">If there are duplicate names at hello same level, hello Copy Activity picks hello last one.</span></span>
* <span data-ttu-id="f2f76-298">Os nomes de propriedade diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="f2f76-298">Property names are case-sensitive.</span></span> <span data-ttu-id="f2f76-299">Duas propriedades com o mesmo nome, mas com maiúsculas e minúsculas diferentes são tratadas como duas propriedades separadas.</span><span class="sxs-lookup"><span data-stu-id="f2f76-299">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="f2f76-300">**Caso 2: Gravando dados tooJSON arquivo**</span><span class="sxs-lookup"><span data-stu-id="f2f76-300">**Case 2: Writing data tooJSON file**</span></span>

<span data-ttu-id="f2f76-301">Se você tiver Olá a tabela no banco de dados SQL a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2f76-301">If you have hello following table in SQL Database:</span></span>

| <span data-ttu-id="f2f76-302">ID</span><span class="sxs-lookup"><span data-stu-id="f2f76-302">id</span></span> | <span data-ttu-id="f2f76-303">order_date</span><span class="sxs-lookup"><span data-stu-id="f2f76-303">order_date</span></span> | <span data-ttu-id="f2f76-304">order_price</span><span class="sxs-lookup"><span data-stu-id="f2f76-304">order_price</span></span> | <span data-ttu-id="f2f76-305">order_by</span><span class="sxs-lookup"><span data-stu-id="f2f76-305">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f2f76-306">1</span><span class="sxs-lookup"><span data-stu-id="f2f76-306">1</span></span> | <span data-ttu-id="f2f76-307">20170119</span><span class="sxs-lookup"><span data-stu-id="f2f76-307">20170119</span></span> | <span data-ttu-id="f2f76-308">2000</span><span class="sxs-lookup"><span data-stu-id="f2f76-308">2000</span></span> | <span data-ttu-id="f2f76-309">Davi</span><span class="sxs-lookup"><span data-stu-id="f2f76-309">David</span></span> |
| <span data-ttu-id="f2f76-310">2</span><span class="sxs-lookup"><span data-stu-id="f2f76-310">2</span></span> | <span data-ttu-id="f2f76-311">20170120</span><span class="sxs-lookup"><span data-stu-id="f2f76-311">20170120</span></span> | <span data-ttu-id="f2f76-312">3500</span><span class="sxs-lookup"><span data-stu-id="f2f76-312">3500</span></span> | <span data-ttu-id="f2f76-313">Pedro</span><span class="sxs-lookup"><span data-stu-id="f2f76-313">Patrick</span></span> |
| <span data-ttu-id="f2f76-314">3</span><span class="sxs-lookup"><span data-stu-id="f2f76-314">3</span></span> | <span data-ttu-id="f2f76-315">20170121</span><span class="sxs-lookup"><span data-stu-id="f2f76-315">20170121</span></span> | <span data-ttu-id="f2f76-316">4000</span><span class="sxs-lookup"><span data-stu-id="f2f76-316">4000</span></span> | <span data-ttu-id="f2f76-317">Jason</span><span class="sxs-lookup"><span data-stu-id="f2f76-317">Jason</span></span> |

<span data-ttu-id="f2f76-318">e, para cada registro, você espera que o objeto JSON tooa toowrite em Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2f76-318">and for each record, you expect toowrite tooa JSON object in hello following format:</span></span>
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

<span data-ttu-id="f2f76-319">saudação de conjunto de dados com saída **JsonFormat** tipo é definido da seguinte maneira: (definição parcial com partes relevantes apenas Olá).</span><span class="sxs-lookup"><span data-stu-id="f2f76-319">hello output dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="f2f76-320">Mais especificamente, `structure` seção define os nomes de propriedade Olá personalizado no arquivo de destino, `nestingSeparator` (o padrão é ".") são usados tooidentify Olá aninhar camada do nome de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2f76-320">More specifically, `structure` section defines hello customized property names in destination file, `nestingSeparator` (default is ".") are used tooidentify hello nest layer from hello name.</span></span> <span data-ttu-id="f2f76-321">Esta seção é **opcional** a menos que você deseja o nome da propriedade Olá toochange comparando com o nome da coluna de origem ou aninhar algumas das propriedades de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2f76-321">This section is **optional** unless you want toochange hello property name comparing with source column name, or nest some of hello properties.</span></span>

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

## <a name="avro-format"></a><span data-ttu-id="f2f76-322">Formato AVRO</span><span class="sxs-lookup"><span data-stu-id="f2f76-322">AVRO format</span></span>
<span data-ttu-id="f2f76-323">Se você deseja tooparse Olá Avro arquivos ou gravar dados saudação no formato Avro, defina Olá `format` `type` propriedade muito**AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="f2f76-323">If you want tooparse hello Avro files or write hello data in Avro format, set hello `format` `type` property too**AvroFormat**.</span></span> <span data-ttu-id="f2f76-324">Não é necessário toospecify as propriedades na seção de formato de saudação na seção de typeProperties hello.</span><span class="sxs-lookup"><span data-stu-id="f2f76-324">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="f2f76-325">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="f2f76-325">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="f2f76-326">formato de Avro toouse em uma tabela de Hive, você pode consultar muito[tutorial do Apache Hive](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span><span class="sxs-lookup"><span data-stu-id="f2f76-326">toouse Avro format in a Hive table, you can refer too[Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="f2f76-327">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2f76-327">Note hello following points:</span></span>  

* <span data-ttu-id="f2f76-328">Não há suporte para [tipos de dados complexos](http://avro.apache.org/docs/current/spec.html#schema_complex) (registros, enumerações, matrizes, mapas, uniões e fixo).</span><span class="sxs-lookup"><span data-stu-id="f2f76-328">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions, and fixed).</span></span>

## <a name="orc-format"></a><span data-ttu-id="f2f76-329">Formato ORC</span><span class="sxs-lookup"><span data-stu-id="f2f76-329">ORC format</span></span>
<span data-ttu-id="f2f76-330">Se você deseja tooparse Olá ORC arquivos ou gravar dados saudação no formato ORC, defina Olá `format` `type` propriedade muito**OrcFormat**.</span><span class="sxs-lookup"><span data-stu-id="f2f76-330">If you want tooparse hello ORC files or write hello data in ORC format, set hello `format` `type` property too**OrcFormat**.</span></span> <span data-ttu-id="f2f76-331">Não é necessário toospecify as propriedades na seção de formato de saudação na seção de typeProperties hello.</span><span class="sxs-lookup"><span data-stu-id="f2f76-331">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="f2f76-332">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="f2f76-332">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="f2f76-333">Se você não estiver copiando arquivos ORC **como-é** entre local e nuvem armazenamentos de dados, precisa tooinstall Olá 8 JRE (Java Runtime Environment) no seu computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="f2f76-333">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="f2f76-334">Um gateway de 64 bits exige JRE de 64 bits, enquanto um gateway de 32 bits exige JRE de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="f2f76-334">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="f2f76-335">Você pode encontrar as duas versões [aqui](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="f2f76-335">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="f2f76-336">Escolha Olá apropriado.</span><span class="sxs-lookup"><span data-stu-id="f2f76-336">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="f2f76-337">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2f76-337">Note hello following points:</span></span>

* <span data-ttu-id="f2f76-338">Não há suporte para tipos de dados complexos (STRUCT, MAP, LIST e UNION)</span><span class="sxs-lookup"><span data-stu-id="f2f76-338">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="f2f76-339">O arquivo ORC tem três [opções de compactação](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB e SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="f2f76-339">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="f2f76-340">O Data Factory dá suporte à leitura de dados de arquivo ORC em qualquer um dos formatos compactados acima.</span><span class="sxs-lookup"><span data-stu-id="f2f76-340">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="f2f76-341">Ele usa compactação Olá codec está nos dados de Olá Olá metadados tooread.</span><span class="sxs-lookup"><span data-stu-id="f2f76-341">It uses hello compression codec is in hello metadata tooread hello data.</span></span> <span data-ttu-id="f2f76-342">No entanto, ao gravar o arquivo ORC tooan, fábrica de dados escolhe ZLIB, que é o padrão de saudação para ORC.</span><span class="sxs-lookup"><span data-stu-id="f2f76-342">However, when writing tooan ORC file, Data Factory chooses ZLIB, which is hello default for ORC.</span></span> <span data-ttu-id="f2f76-343">Atualmente, não há nenhuma opção toooverride esse comportamento.</span><span class="sxs-lookup"><span data-stu-id="f2f76-343">Currently, there is no option toooverride this behavior.</span></span>

## <a name="parquet-format"></a><span data-ttu-id="f2f76-344">Formato Parquet</span><span class="sxs-lookup"><span data-stu-id="f2f76-344">Parquet format</span></span>
<span data-ttu-id="f2f76-345">Se você deseja tooparse Olá Parquet arquivos ou gravar dados saudação no formato Parquet, defina Olá `format` `type` propriedade muito**ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="f2f76-345">If you want tooparse hello Parquet files or write hello data in Parquet format, set hello `format` `type` property too**ParquetFormat**.</span></span> <span data-ttu-id="f2f76-346">Não é necessário toospecify as propriedades na seção de formato de saudação na seção de typeProperties hello.</span><span class="sxs-lookup"><span data-stu-id="f2f76-346">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="f2f76-347">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="f2f76-347">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="f2f76-348">Se você não estiver copiando arquivos Parquet **como-é** entre local e nuvem armazenamentos de dados, precisa tooinstall Olá 8 JRE (Java Runtime Environment) no seu computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="f2f76-348">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="f2f76-349">Um gateway de 64 bits exige JRE de 64 bits, enquanto um gateway de 32 bits exige JRE de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="f2f76-349">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="f2f76-350">Você pode encontrar as duas versões [aqui](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="f2f76-350">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="f2f76-351">Escolha Olá apropriado.</span><span class="sxs-lookup"><span data-stu-id="f2f76-351">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="f2f76-352">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2f76-352">Note hello following points:</span></span>

* <span data-ttu-id="f2f76-353">Não há suporte para tipos de dados complexos (MAP, LIST)</span><span class="sxs-lookup"><span data-stu-id="f2f76-353">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="f2f76-354">Arquivo parquet tem Olá opções de compactação a seguir: NONE, SNAPPY, GZIP e LZO.</span><span class="sxs-lookup"><span data-stu-id="f2f76-354">Parquet file has hello following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="f2f76-355">O Data Factory dá suporte à leitura de dados de arquivo ORC em qualquer um dos formatos compactados acima.</span><span class="sxs-lookup"><span data-stu-id="f2f76-355">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="f2f76-356">Ele usa o codec de compactação de saudação nos dados de Olá Olá metadados tooread.</span><span class="sxs-lookup"><span data-stu-id="f2f76-356">It uses hello compression codec in hello metadata tooread hello data.</span></span> <span data-ttu-id="f2f76-357">No entanto, ao gravar o arquivo de Parquet tooa, fábrica de dados escolhe SNAPPY, que é saudação padrão para o formato de Parquet.</span><span class="sxs-lookup"><span data-stu-id="f2f76-357">However, when writing tooa Parquet file, Data Factory chooses SNAPPY, which is hello default for Parquet format.</span></span> <span data-ttu-id="f2f76-358">Atualmente, não há nenhuma opção toooverride esse comportamento.</span><span class="sxs-lookup"><span data-stu-id="f2f76-358">Currently, there is no option toooverride this behavior.</span></span>

## <a name="compression-support"></a><span data-ttu-id="f2f76-359">Suporte à compactação</span><span class="sxs-lookup"><span data-stu-id="f2f76-359">Compression support</span></span>
<span data-ttu-id="f2f76-360">O processamento de grandes conjuntos de dados pode causar afunilamentos de E/S e de rede.</span><span class="sxs-lookup"><span data-stu-id="f2f76-360">Processing large data sets can cause I/O and network bottlenecks.</span></span> <span data-ttu-id="f2f76-361">Portanto, dados compactados em repositórios podem não apenas acelerar a transferência de dados pela rede hello e economizar espaço em disco, mas também abrir melhorias significativas de desempenho no processamento de big data.</span><span class="sxs-lookup"><span data-stu-id="f2f76-361">Therefore, compressed data in stores can not only speed up data transfer across hello network and save disk space, but also bring significant performance improvements in processing big data.</span></span> <span data-ttu-id="f2f76-362">No momento, a compactação tem suporte para repositórios de dados baseados em arquivo, por exemplo, Blob do Azure ou o Sistema de Arquivos Local.</span><span class="sxs-lookup"><span data-stu-id="f2f76-362">Currently, compression is supported for file-based data stores such as Azure Blob or On-premises File System.</span></span>  

<span data-ttu-id="f2f76-363">compactação toospecify para um conjunto de dados, use Olá **compactação** propriedade do conjunto de dados do hello JSON como Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2f76-363">toospecify compression for a dataset, use hello **compression** property in hello dataset JSON as in hello following example:</span></span>   

```json
{  
    "name": "AzureBlobDataSet",  
    "properties": {  
        "availability": {  
            "frequency": "Day",  
              "interval": 1  
        },  
        "type": "AzureBlob",  
        "linkedServiceName": "StorageLinkedService",  
        "typeProperties": {  
            "fileName": "pagecounts.csv.gz",  
            "folderPath": "compression/file/",  
            "compression": {  
                "type": "GZip",  
                "level": "Optimal"  
            }  
        }  
    }  
}  
```

<span data-ttu-id="f2f76-364">Suponha que o conjunto de dados de exemplo hello é usado como saída de saudação de uma atividade de cópia, Olá Copiar atividade compacta Olá dados de saída com codec GZIP usando taxa ideal e, em seguida, gravar dados saudação compactado em um arquivo denominado pagecounts.csv.gz em Olá armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2f76-364">Suppose hello sample dataset is used as hello output of a copy activity, hello copy activity compresses hello output data with GZIP codec using optimal ratio and then write hello compressed data into a file named pagecounts.csv.gz in hello Azure Blob Storage.</span></span>

> [!NOTE]
> <span data-ttu-id="f2f76-365">Não há suporte para configurações de compactação de dados em Olá **AvroFormat**, **OrcFormat**, ou **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="f2f76-365">Compression settings are not supported for data in hello **AvroFormat**, **OrcFormat**, or **ParquetFormat**.</span></span> <span data-ttu-id="f2f76-366">Ao ler os arquivos nos seguintes formatos, fábrica de dados detecta e usa o codec de compactação de saudação nos metadados de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2f76-366">When reading files in these formats, Data Factory detects and uses hello compression codec in hello metadata.</span></span> <span data-ttu-id="f2f76-367">Ao escrever toofiles nesses formatos, fábrica de dados escolhe o codec de compactação saudação padrão para esse formato.</span><span class="sxs-lookup"><span data-stu-id="f2f76-367">When writing toofiles in these formats, Data Factory chooses hello default compression codec for that format.</span></span> <span data-ttu-id="f2f76-368">Por exemplo, ZLIB para OrcFormat e SNAPPY para ParquetFormat.</span><span class="sxs-lookup"><span data-stu-id="f2f76-368">For example, ZLIB for OrcFormat and SNAPPY for ParquetFormat.</span></span>   

<span data-ttu-id="f2f76-369">Olá **compactação** seção tem duas propriedades:</span><span class="sxs-lookup"><span data-stu-id="f2f76-369">hello **compression** section has two properties:</span></span>  

* <span data-ttu-id="f2f76-370">**Tipo:** codec de compactação hello, que pode ser **GZIP**, **Deflate**, **BZIP2**, ou **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="f2f76-370">**Type:** hello compression codec, which can be **GZIP**, **Deflate**, **BZIP2**, or **ZipDeflate**.</span></span>  
* <span data-ttu-id="f2f76-371">**Nível:** taxa de compactação hello, que pode ser **ideal** ou **mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="f2f76-371">**Level:** hello compression ratio, which can be **Optimal** or **Fastest**.</span></span>

  * <span data-ttu-id="f2f76-372">**Mais rápido:** operação de compactação de saudação deve ser concluída assim que possível, mesmo se o arquivo resultante Olá ideal não é compactado.</span><span class="sxs-lookup"><span data-stu-id="f2f76-372">**Fastest:** hello compression operation should complete as quickly as possible, even if hello resulting file is not optimally compressed.</span></span>
  * <span data-ttu-id="f2f76-373">**Ideal**: operação de compactação Olá deve ser ideal compactada, mesmo se a operação Olá leva um toocomplete de tempo mais longo.</span><span class="sxs-lookup"><span data-stu-id="f2f76-373">**Optimal**: hello compression operation should be optimally compressed, even if hello operation takes a longer time toocomplete.</span></span>

    <span data-ttu-id="f2f76-374">Para saber mais, veja o tópico [Nível de compactação](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) .</span><span class="sxs-lookup"><span data-stu-id="f2f76-374">For more information, see [Compression Level](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) topic.</span></span>

<span data-ttu-id="f2f76-375">Quando você especifica `compression` propriedade em um conjunto de dados de entrada JSON, pipeline Olá pode ler dados compactados fonte Olá; e quando você especificar a propriedade de saudação em um conjunto de dados de saída JSON, atividade de cópia Olá pode gravar o destino de toohello dados compactados.</span><span class="sxs-lookup"><span data-stu-id="f2f76-375">When you specify `compression` property in an input dataset JSON, hello pipeline can read compressed data from hello source; and when you specify hello property in an output dataset JSON, hello copy activity can write compressed data toohello destination.</span></span> <span data-ttu-id="f2f76-376">Aqui estão alguns exemplos de cenários:</span><span class="sxs-lookup"><span data-stu-id="f2f76-376">Here are a few sample scenarios:</span></span>

* <span data-ttu-id="f2f76-377">Ler dados GZIP compactado de um blob do Azure, descompactam e gravar o banco de dados SQL do Azure tooan de dados de resultado.</span><span class="sxs-lookup"><span data-stu-id="f2f76-377">Read GZIP compressed data from an Azure blob, decompress it, and write result data tooan Azure SQL database.</span></span> <span data-ttu-id="f2f76-378">Definir o conjunto de dados entrado de BLOBs do Azure do hello com hello `compression` `type` propriedade JSON como GZIP.</span><span class="sxs-lookup"><span data-stu-id="f2f76-378">You define hello input Azure Blob dataset with hello `compression` `type` JSON property as GZIP.</span></span>
* <span data-ttu-id="f2f76-379">Ler dados de um arquivo de texto sem formatação do sistema de arquivos local, compactá-los usando o formato GZip e gravar Olá compactado dados tooan BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2f76-379">Read data from a plain-text file from on-premises File System, compress it using GZip format, and write hello compressed data tooan Azure blob.</span></span> <span data-ttu-id="f2f76-380">Definir um conjunto de dados de Blob do Azure de saída com hello `compression` `type` propriedade JSON como GZip.</span><span class="sxs-lookup"><span data-stu-id="f2f76-380">You define an output Azure Blob dataset with hello `compression` `type` JSON property as GZip.</span></span>
* <span data-ttu-id="f2f76-381">Arquivo. zip de leitura de servidor FTP, descompactam arquivos Olá tooget e levadas para esses arquivos no repositório Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="f2f76-381">Read .zip file from FTP server, decompress it tooget hello files inside, and land those files into Azure Data Lake Store.</span></span> <span data-ttu-id="f2f76-382">Definir um conjunto de dados FTP de entrada com hello `compression` `type` propriedade JSON como ZipDeflate.</span><span class="sxs-lookup"><span data-stu-id="f2f76-382">You define an input FTP dataset with hello `compression` `type` JSON property as ZipDeflate.</span></span>
* <span data-ttu-id="f2f76-383">Ler dados de compactado GZIP de um blob do Azure, descompactam, compactá-los usando BZIP2 e gravar dados de resultado tooan BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2f76-383">Read a GZIP-compressed data from an Azure blob, decompress it, compress it using BZIP2, and write result data tooan Azure blob.</span></span> <span data-ttu-id="f2f76-384">Definir entrada dataset de BLOBs do Azure Olá com `compression` `type` definir tooGZIP e Olá conjunto de dados de saída com `compression` `type` definido tooBZIP2 nesse caso.</span><span class="sxs-lookup"><span data-stu-id="f2f76-384">You define hello input Azure Blob dataset with `compression` `type` set tooGZIP and hello output dataset with `compression` `type` set tooBZIP2 in this case.</span></span>   


## <a name="next-steps"></a><span data-ttu-id="f2f76-385">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f2f76-385">Next steps</span></span>
<span data-ttu-id="f2f76-386">Consulte Olá artigos para repositórios de dados baseada em arquivo com suporte do Azure Data Factory a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2f76-386">See hello following articles for file-based data stores supported by Azure Data Factory:</span></span>

- [<span data-ttu-id="f2f76-387">Armazenamento de Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="f2f76-387">Azure Blob Storage</span></span>](data-factory-azure-blob-connector.md)
- [<span data-ttu-id="f2f76-388">Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="f2f76-388">Azure Data Lake Store</span></span>](data-factory-azure-datalake-connector.md)
- [<span data-ttu-id="f2f76-389">FTP</span><span class="sxs-lookup"><span data-stu-id="f2f76-389">FTP</span></span>](data-factory-ftp-connector.md)
- [<span data-ttu-id="f2f76-390">HDFS</span><span class="sxs-lookup"><span data-stu-id="f2f76-390">HDFS</span></span>](data-factory-hdfs-connector.md)
- [<span data-ttu-id="f2f76-391">Sistema de Arquivos</span><span class="sxs-lookup"><span data-stu-id="f2f76-391">File System</span></span>](data-factory-onprem-file-system-connector.md)
- [<span data-ttu-id="f2f76-392">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="f2f76-392">Amazon S3</span></span>](data-factory-amazon-simple-storage-service-connector.md)
