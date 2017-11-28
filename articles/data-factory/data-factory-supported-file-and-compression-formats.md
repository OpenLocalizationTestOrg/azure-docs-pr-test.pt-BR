---
title: "Formatos de arquivo e de compactação no Azure Data Factory | Microsoft Docs"
description: "Saiba mais sobre os formatos de arquivo aos quais o Azure Data Factory dá suporte."
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
ms.openlocfilehash: f4746e0dd249e417b8077a9bc733d2886daafdf2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="file-and-compression-formats-supported-by-azure-data-factory"></a><span data-ttu-id="26fcb-104">Formatos de arquivo aos quais o Azure Data Factory dá suporte</span><span class="sxs-lookup"><span data-stu-id="26fcb-104">File and compression formats supported by Azure Data Factory</span></span>
<span data-ttu-id="26fcb-105">*Este tópico se aplica aos seguintes conectores: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Blob do Azure](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [Sistema de Arquivos](data-factory-onprem-file-system-connector.md), [FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md) e [SFTP](data-factory-sftp-connector.md).*</span><span class="sxs-lookup"><span data-stu-id="26fcb-105">*This topic applies to the following connectors: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [File System](data-factory-onprem-file-system-connector.md), [FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), and [SFTP](data-factory-sftp-connector.md).*</span></span>

<span data-ttu-id="26fcb-106">O Azure Data Factory dá suporte aos tipos de formato de arquivo a seguir:</span><span class="sxs-lookup"><span data-stu-id="26fcb-106">Azure Data Factory supports the following file format types:</span></span>

* [<span data-ttu-id="26fcb-107">Formato de texto</span><span class="sxs-lookup"><span data-stu-id="26fcb-107">Text format</span></span>](#text-format)
* [<span data-ttu-id="26fcb-108">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="26fcb-108">JSON format</span></span>](#json-format)
* [<span data-ttu-id="26fcb-109">Formato Avro</span><span class="sxs-lookup"><span data-stu-id="26fcb-109">Avro format</span></span>](#avro-format)
* [<span data-ttu-id="26fcb-110">Formato ORC</span><span class="sxs-lookup"><span data-stu-id="26fcb-110">ORC format</span></span>](#orc-format)
* [<span data-ttu-id="26fcb-111">Formato Parquet</span><span class="sxs-lookup"><span data-stu-id="26fcb-111">Parquet format</span></span>](#parquet-format)

## <a name="text-format"></a><span data-ttu-id="26fcb-112">Formato de texto</span><span class="sxs-lookup"><span data-stu-id="26fcb-112">Text format</span></span>
<span data-ttu-id="26fcb-113">Se você quiser ler um arquivo de texto ou gravar em um arquivo de texto, defina a propriedade `type` na seção `format` do conjunto de dados para **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="26fcb-113">If you want to read from a text file or write to a text file, set the `type` property in the `format` section of the dataset to **TextFormat**.</span></span> <span data-ttu-id="26fcb-114">Você também pode especificar as seguintes propriedades **opcionais** na seção `format`.</span><span class="sxs-lookup"><span data-stu-id="26fcb-114">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="26fcb-115">Veja a seção [Exemplo de TextFormat](#textformat-example) sobre a configuração.</span><span class="sxs-lookup"><span data-stu-id="26fcb-115">See [TextFormat example](#textformat-example) section on how to configure.</span></span>

| <span data-ttu-id="26fcb-116">Propriedade</span><span class="sxs-lookup"><span data-stu-id="26fcb-116">Property</span></span> | <span data-ttu-id="26fcb-117">Descrição</span><span class="sxs-lookup"><span data-stu-id="26fcb-117">Description</span></span> | <span data-ttu-id="26fcb-118">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="26fcb-118">Allowed values</span></span> | <span data-ttu-id="26fcb-119">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="26fcb-119">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="26fcb-120">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="26fcb-120">columnDelimiter</span></span> |<span data-ttu-id="26fcb-121">O caractere usado para separar as colunas em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="26fcb-121">The character used to separate columns in a file.</span></span> <span data-ttu-id="26fcb-122">Você pode considerar usar um caractere não imprimível raro que provavelmente exista em seus dados.</span><span class="sxs-lookup"><span data-stu-id="26fcb-122">You can consider to use a rare unprintable char that may not likely exists in your data.</span></span> <span data-ttu-id="26fcb-123">Por exemplo, especifique "\u0001", que representa o SOH (início do título).</span><span class="sxs-lookup"><span data-stu-id="26fcb-123">For example, specify "\u0001", which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="26fcb-124">Somente um caractere é permitido.</span><span class="sxs-lookup"><span data-stu-id="26fcb-124">Only one character is allowed.</span></span> <span data-ttu-id="26fcb-125">O valor **padrão** é **vírgula (‘,’)**.</span><span class="sxs-lookup"><span data-stu-id="26fcb-125">The **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="26fcb-126">Para usar um caractere Unicode, consulte [Caracteres Unicode](https://en.wikipedia.org/wiki/List_of_Unicode_characters) para obter o código correspondente.</span><span class="sxs-lookup"><span data-stu-id="26fcb-126">To use a Unicode character, refer to [Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) to get the corresponding code for it.</span></span> |<span data-ttu-id="26fcb-127">Não</span><span class="sxs-lookup"><span data-stu-id="26fcb-127">No</span></span> |
| <span data-ttu-id="26fcb-128">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="26fcb-128">rowDelimiter</span></span> |<span data-ttu-id="26fcb-129">O caractere usado para separar as linhas em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="26fcb-129">The character used to separate rows in a file.</span></span> |<span data-ttu-id="26fcb-130">Somente um caractere é permitido.</span><span class="sxs-lookup"><span data-stu-id="26fcb-130">Only one character is allowed.</span></span> <span data-ttu-id="26fcb-131">O valor **padrão** é um dos seguintes valores na leitura: **["\r\n", "\r" e "\n"]** e **"\r\n"** na gravação.</span><span class="sxs-lookup"><span data-stu-id="26fcb-131">The **default** value is any of the following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="26fcb-132">Não</span><span class="sxs-lookup"><span data-stu-id="26fcb-132">No</span></span> |
| <span data-ttu-id="26fcb-133">escapeChar</span><span class="sxs-lookup"><span data-stu-id="26fcb-133">escapeChar</span></span> |<span data-ttu-id="26fcb-134">O caractere especial usado como escape do delimitador de coluna no conteúdo do arquivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="26fcb-134">The special character used to escape a column delimiter in the content of input file.</span></span> <br/><br/><span data-ttu-id="26fcb-135">Não é possível especificar ambos escapeChar e quoteChar para uma tabela.</span><span class="sxs-lookup"><span data-stu-id="26fcb-135">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="26fcb-136">Somente um caractere é permitido.</span><span class="sxs-lookup"><span data-stu-id="26fcb-136">Only one character is allowed.</span></span> <span data-ttu-id="26fcb-137">Nenhum valor padrão.</span><span class="sxs-lookup"><span data-stu-id="26fcb-137">No default value.</span></span> <br/><br/><span data-ttu-id="26fcb-138">Por exemplo, se tiver a vírgula (,) como o delimitador de coluna, mas quiser ter o caractere de vírgula no texto (exemplo: "Hello, world"), você poderá definir '$' como o caractere de escape e usar a cadeia de caracteres "Hello$, world" na fonte.</span><span class="sxs-lookup"><span data-stu-id="26fcb-138">Example: if you have comma (',') as the column delimiter but you want to have the comma character in the text (example: "Hello, world"), you can define ‘$’ as the escape character and use string "Hello$, world" in the source.</span></span> |<span data-ttu-id="26fcb-139">Não</span><span class="sxs-lookup"><span data-stu-id="26fcb-139">No</span></span> |
| <span data-ttu-id="26fcb-140">quoteChar</span><span class="sxs-lookup"><span data-stu-id="26fcb-140">quoteChar</span></span> |<span data-ttu-id="26fcb-141">O caractere usado para citar um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="26fcb-141">The character used to quote a string value.</span></span> <span data-ttu-id="26fcb-142">Os delimitadores de linha e coluna dentro dos caracteres de aspas seriam tratados como parte do valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="26fcb-142">The column and row delimiters inside the quote characters would be treated as part of the string value.</span></span> <span data-ttu-id="26fcb-143">Essa propriedade é aplicável a ambos os conjuntos de dados de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="26fcb-143">This property is applicable to both input and output datasets.</span></span><br/><br/><span data-ttu-id="26fcb-144">Não é possível especificar ambos escapeChar e quoteChar para uma tabela.</span><span class="sxs-lookup"><span data-stu-id="26fcb-144">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="26fcb-145">Somente um caractere é permitido.</span><span class="sxs-lookup"><span data-stu-id="26fcb-145">Only one character is allowed.</span></span> <span data-ttu-id="26fcb-146">Nenhum valor padrão.</span><span class="sxs-lookup"><span data-stu-id="26fcb-146">No default value.</span></span> <br/><br/><span data-ttu-id="26fcb-147">Por exemplo, se tiver a vírgula (,) como o delimitador de coluna, mas quiser ter o caractere de vírgula no texto (exemplo: <Hello, world>), você poderá definir " (aspas duplas) como o caractere de citação e usar a cadeia de caracteres "Hello, world" na origem.</span><span class="sxs-lookup"><span data-stu-id="26fcb-147">For example, if you have comma (',') as the column delimiter but you want to have comma character in the text (example: <Hello, world>), you can define " (double quote) as the quote character and use the string "Hello, world" in the source.</span></span> |<span data-ttu-id="26fcb-148">Não</span><span class="sxs-lookup"><span data-stu-id="26fcb-148">No</span></span> |
| <span data-ttu-id="26fcb-149">nullValue</span><span class="sxs-lookup"><span data-stu-id="26fcb-149">nullValue</span></span> |<span data-ttu-id="26fcb-150">Um ou mais caracteres usados para representar um valor nulo.</span><span class="sxs-lookup"><span data-stu-id="26fcb-150">One or more characters used to represent a null value.</span></span> |<span data-ttu-id="26fcb-151">Um ou mais caracteres.</span><span class="sxs-lookup"><span data-stu-id="26fcb-151">One or more characters.</span></span> <span data-ttu-id="26fcb-152">Os valores **padrão** são **"\N" e "NULL"** na leitura e **"\N"** na gravação.</span><span class="sxs-lookup"><span data-stu-id="26fcb-152">The **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="26fcb-153">Não</span><span class="sxs-lookup"><span data-stu-id="26fcb-153">No</span></span> |
| <span data-ttu-id="26fcb-154">encodingName</span><span class="sxs-lookup"><span data-stu-id="26fcb-154">encodingName</span></span> |<span data-ttu-id="26fcb-155">Especifique o nome de codificação.</span><span class="sxs-lookup"><span data-stu-id="26fcb-155">Specify the encoding name.</span></span> |<span data-ttu-id="26fcb-156">Um nomes de codificação válido.</span><span class="sxs-lookup"><span data-stu-id="26fcb-156">A valid encoding name.</span></span> <span data-ttu-id="26fcb-157">Consulte [Propriedade Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="26fcb-157">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="26fcb-158">Por exemplo: windows-1250 ou shift_jis.</span><span class="sxs-lookup"><span data-stu-id="26fcb-158">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="26fcb-159">O valor **padrão** é **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="26fcb-159">The **default** value is **UTF-8**.</span></span> |<span data-ttu-id="26fcb-160">Não</span><span class="sxs-lookup"><span data-stu-id="26fcb-160">No</span></span> |
| <span data-ttu-id="26fcb-161">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="26fcb-161">firstRowAsHeader</span></span> |<span data-ttu-id="26fcb-162">Especifica se a primeira linha será considerada como cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="26fcb-162">Specifies whether to consider the first row as a header.</span></span> <span data-ttu-id="26fcb-163">Para um conjunto de dados de entrada, o Data Factory lê a primeira linha como cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="26fcb-163">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="26fcb-164">Para um conjunto de dados de saída, o Data Factory lê a primeira linha como cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="26fcb-164">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="26fcb-165">Veja [Cenários para usar o `firstRowAsHeader` e o `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) para cenários de exemplo.</span><span class="sxs-lookup"><span data-stu-id="26fcb-165">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="26fcb-166">True </span><span class="sxs-lookup"><span data-stu-id="26fcb-166">True</span></span><br/><span data-ttu-id="26fcb-167"><b>False (padrão)</b></span><span class="sxs-lookup"><span data-stu-id="26fcb-167"><b>False (default)</b></span></span> |<span data-ttu-id="26fcb-168">Não</span><span class="sxs-lookup"><span data-stu-id="26fcb-168">No</span></span> |
| <span data-ttu-id="26fcb-169">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="26fcb-169">skipLineCount</span></span> |<span data-ttu-id="26fcb-170">Indica o número de linhas a serem ignoradas ao ler dados de arquivos de entrada.</span><span class="sxs-lookup"><span data-stu-id="26fcb-170">Indicates the number of rows to skip when reading data from input files.</span></span> <span data-ttu-id="26fcb-171">Se skipLineCount e firstRowAsHeader forem especificados, as linhas serão ignoradas pela primeira vez e, em seguida, as informações de cabeçalho serão lidas do arquivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="26fcb-171">If both skipLineCount and firstRowAsHeader are specified, the lines are skipped first and then the header information is read from the input file.</span></span> <br/><br/><span data-ttu-id="26fcb-172">Veja [Cenários para usar o `firstRowAsHeader` e o `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) para cenários de exemplo.</span><span class="sxs-lookup"><span data-stu-id="26fcb-172">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="26fcb-173">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="26fcb-173">Integer</span></span> |<span data-ttu-id="26fcb-174">Não</span><span class="sxs-lookup"><span data-stu-id="26fcb-174">No</span></span> |
| <span data-ttu-id="26fcb-175">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="26fcb-175">treatEmptyAsNull</span></span> |<span data-ttu-id="26fcb-176">Especifica se uma cadeia de caracteres nula ou vazia será ou não tratada como um valor nulo ao ler dados de um arquivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="26fcb-176">Specifies whether to treat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="26fcb-177">**True (padrão)**</span><span class="sxs-lookup"><span data-stu-id="26fcb-177">**True (default)**</span></span><br/><span data-ttu-id="26fcb-178">Falso</span><span class="sxs-lookup"><span data-stu-id="26fcb-178">False</span></span> |<span data-ttu-id="26fcb-179">Não</span><span class="sxs-lookup"><span data-stu-id="26fcb-179">No</span></span> |

### <a name="textformat-example"></a><span data-ttu-id="26fcb-180">Exemplo de TextFormat</span><span class="sxs-lookup"><span data-stu-id="26fcb-180">TextFormat example</span></span>
<span data-ttu-id="26fcb-181">Na definição de JSON a seguir para um conjunto de dados, algumas das propriedades opcionais são especificadas.</span><span class="sxs-lookup"><span data-stu-id="26fcb-181">In the following JSON definition for a dataset, some of the optional properties are specified.</span></span>

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

<span data-ttu-id="26fcb-182">Para usar um `escapeChar` em vez de `quoteChar`, substitua a linha com `quoteChar` por este escapeChar:</span><span class="sxs-lookup"><span data-stu-id="26fcb-182">To use an `escapeChar` instead of `quoteChar`, replace the line with `quoteChar` with the following escapeChar:</span></span>

```json
"escapeChar": "$",
```

### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="26fcb-183">Cenários de uso de firstRowAsHeader e skipLineCount</span><span class="sxs-lookup"><span data-stu-id="26fcb-183">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="26fcb-184">Você está copiando de uma fonte que não é de arquivo para um arquivo de texto e deseja adicionar uma linha de cabeçalho que contém os metadados de esquema (por exemplo: esquema SQL).</span><span class="sxs-lookup"><span data-stu-id="26fcb-184">You are copying from a non-file source to a text file and would like to add a header line containing the schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="26fcb-185">Especifique `firstRowAsHeader` como true no conjunto de dados de saída para esse cenário.</span><span class="sxs-lookup"><span data-stu-id="26fcb-185">Specify `firstRowAsHeader` as true in the output dataset for this scenario.</span></span>
* <span data-ttu-id="26fcb-186">Você está copiando de um arquivo de texto contendo uma linha de cabeçalho para um coletor que não é em arquivo e gostaria de remover essa linha.</span><span class="sxs-lookup"><span data-stu-id="26fcb-186">You are copying from a text file containing a header line to a non-file sink and would like to drop that line.</span></span> <span data-ttu-id="26fcb-187">Especifique `firstRowAsHeader` como true no conjunto de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="26fcb-187">Specify `firstRowAsHeader` as true in the input dataset.</span></span>
* <span data-ttu-id="26fcb-188">Você está copiando de um arquivo de texto e deseja ignorar algumas linhas no início que não são informações de dados nem de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="26fcb-188">You are copying from a text file and want to skip a few lines at the beginning that contain no data or header information.</span></span> <span data-ttu-id="26fcb-189">Especifique `skipLineCount` para indicar o número de linhas a serem ignoradas.</span><span class="sxs-lookup"><span data-stu-id="26fcb-189">Specify `skipLineCount` to indicate the number of lines to be skipped.</span></span> <span data-ttu-id="26fcb-190">Se o restante do arquivo contiver uma linha de cabeçalho, você também poderá especificar `firstRowAsHeader`.</span><span class="sxs-lookup"><span data-stu-id="26fcb-190">If the rest of the file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="26fcb-191">Se `skipLineCount` e `firstRowAsHeader` forem especificados, as linhas serão ignoradas pela primeira vez e, em seguida, as informações de cabeçalho serão lidas do arquivo de entrada</span><span class="sxs-lookup"><span data-stu-id="26fcb-191">If both `skipLineCount` and `firstRowAsHeader` are specified, the lines are skipped first and then the header information is read from the input file</span></span>

## <a name="json-format"></a><span data-ttu-id="26fcb-192">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="26fcb-192">JSON format</span></span>
<span data-ttu-id="26fcb-193">Para **importar/exportar um arquivo JSON no estado em que se encontra de/para o Azure Cosmos DB**, consulte a seção [Importar/exportar documentos JSON](data-factory-azure-documentdb-connector.md#importexport-json-documents) do artigo [Mover dados de/para o Azure Cosmos DB](data-factory-azure-documentdb-connector.md).</span><span class="sxs-lookup"><span data-stu-id="26fcb-193">To **import/export a JSON file as-is into/from Azure Cosmos DB**, the see [Import/export JSON documents](data-factory-azure-documentdb-connector.md#importexport-json-documents) section in [Move data to/from Azure Cosmos DB](data-factory-azure-documentdb-connector.md) article.</span></span>

<span data-ttu-id="26fcb-194">Se você quiser analisar os arquivos de JSON ou gravar os dados no formato JSON, defina a propriedade `type` na seção `format` como **JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="26fcb-194">If you want to parse the JSON files or write the data in JSON format, set the `type` property in the `format` section to **JsonFormat**.</span></span> <span data-ttu-id="26fcb-195">Você também pode especificar as seguintes propriedades **opcionais** na seção `format`.</span><span class="sxs-lookup"><span data-stu-id="26fcb-195">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="26fcb-196">Veja a seção [Exemplo de JsonFormat](#jsonformat-example) sobre como configurar.</span><span class="sxs-lookup"><span data-stu-id="26fcb-196">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span>

| <span data-ttu-id="26fcb-197">Propriedade</span><span class="sxs-lookup"><span data-stu-id="26fcb-197">Property</span></span> | <span data-ttu-id="26fcb-198">Descrição</span><span class="sxs-lookup"><span data-stu-id="26fcb-198">Description</span></span> | <span data-ttu-id="26fcb-199">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="26fcb-199">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="26fcb-200">filePattern</span><span class="sxs-lookup"><span data-stu-id="26fcb-200">filePattern</span></span> |<span data-ttu-id="26fcb-201">Indique o padrão de dados armazenados em cada arquivo JSON.</span><span class="sxs-lookup"><span data-stu-id="26fcb-201">Indicate the pattern of data stored in each JSON file.</span></span> <span data-ttu-id="26fcb-202">Os valores permitidos são: **setOfObjects** e **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="26fcb-202">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="26fcb-203">O valor **padrão** é **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="26fcb-203">The **default** value is **setOfObjects**.</span></span> <span data-ttu-id="26fcb-204">Veja a seção [Padrões de arquivo JSON](#json-file-patterns) para obter detalhes sobre esses padrões.</span><span class="sxs-lookup"><span data-stu-id="26fcb-204">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="26fcb-205">Não</span><span class="sxs-lookup"><span data-stu-id="26fcb-205">No</span></span> |
| <span data-ttu-id="26fcb-206">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="26fcb-206">jsonNodeReference</span></span> | <span data-ttu-id="26fcb-207">Se você quiser fazer uma iteração e extrair dados de objetos dentro de um campo de matriz com o mesmo padrão, especifique o caminho JSON da matriz.</span><span class="sxs-lookup"><span data-stu-id="26fcb-207">If you want to iterate and extract data from the objects inside an array field with the same pattern, specify the JSON path of that array.</span></span> <span data-ttu-id="26fcb-208">Esta propriedade só terá suporte na cópia de dados de arquivos JSON.</span><span class="sxs-lookup"><span data-stu-id="26fcb-208">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="26fcb-209">Não</span><span class="sxs-lookup"><span data-stu-id="26fcb-209">No</span></span> |
| <span data-ttu-id="26fcb-210">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="26fcb-210">jsonPathDefinition</span></span> | <span data-ttu-id="26fcb-211">Especifique a expressão de caminho JSON para cada mapeamento de coluna com um nome de coluna personalizado (iniciar com letra minúscula).</span><span class="sxs-lookup"><span data-stu-id="26fcb-211">Specify the JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="26fcb-212">Esta propriedade só terá suporte na cópia de dados de arquivos JSON, e você pode extrair dados de objeto ou de matriz.</span><span class="sxs-lookup"><span data-stu-id="26fcb-212">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="26fcb-213">Para os campos sob o objeto root, comece com root $; para os campos dentro da matriz escolhidos pela propriedade `jsonNodeReference`, comece do elemento de matriz.</span><span class="sxs-lookup"><span data-stu-id="26fcb-213">For fields under root object, start with root $; for fields inside the array chosen by `jsonNodeReference` property, start from the array element.</span></span> <span data-ttu-id="26fcb-214">Veja a seção [Exemplo de JsonFormat](#jsonformat-example) sobre como configurar.</span><span class="sxs-lookup"><span data-stu-id="26fcb-214">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span> | <span data-ttu-id="26fcb-215">Não</span><span class="sxs-lookup"><span data-stu-id="26fcb-215">No</span></span> |
| <span data-ttu-id="26fcb-216">encodingName</span><span class="sxs-lookup"><span data-stu-id="26fcb-216">encodingName</span></span> |<span data-ttu-id="26fcb-217">Especifique o nome de codificação.</span><span class="sxs-lookup"><span data-stu-id="26fcb-217">Specify the encoding name.</span></span> <span data-ttu-id="26fcb-218">Para obter a lista de nomes de codificação válidos, consulte: Propriedade [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) .</span><span class="sxs-lookup"><span data-stu-id="26fcb-218">For the list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="26fcb-219">Por exemplo: windows-1250 ou shift_jis.</span><span class="sxs-lookup"><span data-stu-id="26fcb-219">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="26fcb-220">O valor **padrão** é **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="26fcb-220">The **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="26fcb-221">Não</span><span class="sxs-lookup"><span data-stu-id="26fcb-221">No</span></span> |
| <span data-ttu-id="26fcb-222">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="26fcb-222">nestingSeparator</span></span> |<span data-ttu-id="26fcb-223">Caractere que é usado para separar os níveis de aninhamento.</span><span class="sxs-lookup"><span data-stu-id="26fcb-223">Character that is used to separate nesting levels.</span></span> <span data-ttu-id="26fcb-224">O valor padrão é '.' (ponto).</span><span class="sxs-lookup"><span data-stu-id="26fcb-224">The default value is '.' (dot).</span></span> |<span data-ttu-id="26fcb-225">Não</span><span class="sxs-lookup"><span data-stu-id="26fcb-225">No</span></span> |

### <a name="json-file-patterns"></a><span data-ttu-id="26fcb-226">Padrões de arquivo JSON</span><span class="sxs-lookup"><span data-stu-id="26fcb-226">JSON file patterns</span></span>

<span data-ttu-id="26fcb-227">A atividade de cópia pode analisar os padrões de arquivos JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="26fcb-227">Copy activity can parse the following patterns of JSON files:</span></span>

- <span data-ttu-id="26fcb-228">**Tipo I: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="26fcb-228">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="26fcb-229">Cada arquivo contém um único objeto ou vários objetos concatenados/delimitados por linhas.</span><span class="sxs-lookup"><span data-stu-id="26fcb-229">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="26fcb-230">Quando essa opção é escolhida em um conjunto de dados de saída, a atividade de cópia produz um único arquivo JSON com cada objeto por linha (delimitados por linha).</span><span class="sxs-lookup"><span data-stu-id="26fcb-230">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="26fcb-231">**Exemplo de JSON de objeto único**</span><span class="sxs-lookup"><span data-stu-id="26fcb-231">**single object JSON example**</span></span>

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

    * <span data-ttu-id="26fcb-232">**Exemplo de JSON delimitado por linha**</span><span class="sxs-lookup"><span data-stu-id="26fcb-232">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="26fcb-233">**Exemplo de JSON concatenado**</span><span class="sxs-lookup"><span data-stu-id="26fcb-233">**concatenated JSON example**</span></span>

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

- <span data-ttu-id="26fcb-234">**Tipo II: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="26fcb-234">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="26fcb-235">Cada arquivo contém uma matriz de objetos.</span><span class="sxs-lookup"><span data-stu-id="26fcb-235">Each file contains an array of objects.</span></span>

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

### <a name="jsonformat-example"></a><span data-ttu-id="26fcb-236">Exemplo de JsonFormat</span><span class="sxs-lookup"><span data-stu-id="26fcb-236">JsonFormat example</span></span>

<span data-ttu-id="26fcb-237">**Caso 1: copiar dados de arquivos JSON**</span><span class="sxs-lookup"><span data-stu-id="26fcb-237">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="26fcb-238">Consulte os exemplos a seguir ao copiar dados de arquivos JSON.</span><span class="sxs-lookup"><span data-stu-id="26fcb-238">See the following two samples when copying data from JSON files.</span></span> <span data-ttu-id="26fcb-239">Os pontos genéricos a serem observados:</span><span class="sxs-lookup"><span data-stu-id="26fcb-239">The generic points to note:</span></span>

<span data-ttu-id="26fcb-240">**Exemplo 1: extrair dados de objeto e de matriz**</span><span class="sxs-lookup"><span data-stu-id="26fcb-240">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="26fcb-241">Neste exemplo, você espera que um objeto JSON de raiz seja mapeado para um único registro no resultado tabular.</span><span class="sxs-lookup"><span data-stu-id="26fcb-241">In this sample, you expect one root JSON object maps to single record in tabular result.</span></span> <span data-ttu-id="26fcb-242">Se você tiver um arquivo JSON com o seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="26fcb-242">If you have a JSON file with the following content:</span></span>  

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
<span data-ttu-id="26fcb-243">e quiser copiá-lo para uma tabela SQL do Azure no formato a seguir, ao extrair dados dos objetos e da matriz:</span><span class="sxs-lookup"><span data-stu-id="26fcb-243">and you want to copy it into an Azure SQL table in the following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="26fcb-244">ID</span><span class="sxs-lookup"><span data-stu-id="26fcb-244">id</span></span> | <span data-ttu-id="26fcb-245">deviceType</span><span class="sxs-lookup"><span data-stu-id="26fcb-245">deviceType</span></span> | <span data-ttu-id="26fcb-246">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="26fcb-246">targetResourceType</span></span> | <span data-ttu-id="26fcb-247">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="26fcb-247">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="26fcb-248">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="26fcb-248">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="26fcb-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="26fcb-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="26fcb-250">Computador</span><span class="sxs-lookup"><span data-stu-id="26fcb-250">PC</span></span> | <span data-ttu-id="26fcb-251">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="26fcb-251">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="26fcb-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="26fcb-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="26fcb-253">13/01/2017 11:24:37</span><span class="sxs-lookup"><span data-stu-id="26fcb-253">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="26fcb-254">O conjunto de dados de entrada com o tipo **JsonFormat** é definido da seguinte maneira: (definição parcial com apenas as partes relevantes).</span><span class="sxs-lookup"><span data-stu-id="26fcb-254">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="26fcb-255">Mais especificamente:</span><span class="sxs-lookup"><span data-stu-id="26fcb-255">More specifically:</span></span>

- <span data-ttu-id="26fcb-256">A seção `structure` define os nomes de coluna personalizada e o tipo de dados correspondente ao converter em dados tabulares.</span><span class="sxs-lookup"><span data-stu-id="26fcb-256">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="26fcb-257">Esta seção é **opcional**, a menos que você tenha de fazer o mapeamento de colunas.</span><span class="sxs-lookup"><span data-stu-id="26fcb-257">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="26fcb-258">Veja a seção [Mapear colunas de conjunto de dados de origem para colunas do conjunto de dados de destino](data-factory-map-columns.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="26fcb-258">See [Map source dataset columns to destination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="26fcb-259">`jsonPathDefinition` especifica o caminho JSON para cada coluna que indica de onde extrair os dados.</span><span class="sxs-lookup"><span data-stu-id="26fcb-259">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="26fcb-260">Para copiar dados da matriz, você pode usar **array[x].property** para extrair o valor da propriedade do objeto xth, ou você pode usar  **matriz[*].property** para localizar o valor de qualquer objeto que contém essa propriedade.</span><span class="sxs-lookup"><span data-stu-id="26fcb-260">To copy data from array, you can use **array[x].property** to extract value of the given property from the xth object, or you can use **array[*].property** to find the value from any object containing such property.</span></span>

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

<span data-ttu-id="26fcb-261">**Exemplo 2: cruzar aplicar vários objetos com o mesmo padrão da matriz**</span><span class="sxs-lookup"><span data-stu-id="26fcb-261">**Sample 2: cross apply multiple objects with the same pattern from array**</span></span>

<span data-ttu-id="26fcb-262">Neste exemplo, você espera transformar um objeto JSON de raiz em vários registros no resultado tabular.</span><span class="sxs-lookup"><span data-stu-id="26fcb-262">In this sample, you expect to transform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="26fcb-263">Se você tiver um arquivo JSON com o seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="26fcb-263">If you have a JSON file with the following content:</span></span>  

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
<span data-ttu-id="26fcb-264">e você deseja copiá-lo para uma tabela do Azure SQL no formato a seguir, ao nivelar os dados de dentro da matriz e fazer uma união cruzada com as informações comuns de root:</span><span class="sxs-lookup"><span data-stu-id="26fcb-264">and you want to copy it into an Azure SQL table in the following format, by flattening the data inside the array and cross join with the common root info:</span></span>

| <span data-ttu-id="26fcb-265">ordernumber</span><span class="sxs-lookup"><span data-stu-id="26fcb-265">ordernumber</span></span> | <span data-ttu-id="26fcb-266">orderdate</span><span class="sxs-lookup"><span data-stu-id="26fcb-266">orderdate</span></span> | <span data-ttu-id="26fcb-267">order_pd</span><span class="sxs-lookup"><span data-stu-id="26fcb-267">order_pd</span></span> | <span data-ttu-id="26fcb-268">order_price</span><span class="sxs-lookup"><span data-stu-id="26fcb-268">order_price</span></span> | <span data-ttu-id="26fcb-269">city</span><span class="sxs-lookup"><span data-stu-id="26fcb-269">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="26fcb-270">01</span><span class="sxs-lookup"><span data-stu-id="26fcb-270">01</span></span> | <span data-ttu-id="26fcb-271">20170122</span><span class="sxs-lookup"><span data-stu-id="26fcb-271">20170122</span></span> | <span data-ttu-id="26fcb-272">P1</span><span class="sxs-lookup"><span data-stu-id="26fcb-272">P1</span></span> | <span data-ttu-id="26fcb-273">23</span><span class="sxs-lookup"><span data-stu-id="26fcb-273">23</span></span> | <span data-ttu-id="26fcb-274">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="26fcb-274">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="26fcb-275">01</span><span class="sxs-lookup"><span data-stu-id="26fcb-275">01</span></span> | <span data-ttu-id="26fcb-276">20170122</span><span class="sxs-lookup"><span data-stu-id="26fcb-276">20170122</span></span> | <span data-ttu-id="26fcb-277">P2</span><span class="sxs-lookup"><span data-stu-id="26fcb-277">P2</span></span> | <span data-ttu-id="26fcb-278">13</span><span class="sxs-lookup"><span data-stu-id="26fcb-278">13</span></span> | <span data-ttu-id="26fcb-279">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="26fcb-279">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="26fcb-280">01</span><span class="sxs-lookup"><span data-stu-id="26fcb-280">01</span></span> | <span data-ttu-id="26fcb-281">20170122</span><span class="sxs-lookup"><span data-stu-id="26fcb-281">20170122</span></span> | <span data-ttu-id="26fcb-282">P3</span><span class="sxs-lookup"><span data-stu-id="26fcb-282">P3</span></span> | <span data-ttu-id="26fcb-283">231</span><span class="sxs-lookup"><span data-stu-id="26fcb-283">231</span></span> | <span data-ttu-id="26fcb-284">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="26fcb-284">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="26fcb-285">O conjunto de dados de entrada com o tipo **JsonFormat** é definido da seguinte maneira: (definição parcial com apenas as partes relevantes).</span><span class="sxs-lookup"><span data-stu-id="26fcb-285">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="26fcb-286">Mais especificamente:</span><span class="sxs-lookup"><span data-stu-id="26fcb-286">More specifically:</span></span>

- <span data-ttu-id="26fcb-287">A seção `structure` define os nomes de coluna personalizada e o tipo de dados correspondente ao converter em dados tabulares.</span><span class="sxs-lookup"><span data-stu-id="26fcb-287">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="26fcb-288">Esta seção é **opcional**, a menos que você tenha de fazer o mapeamento de colunas.</span><span class="sxs-lookup"><span data-stu-id="26fcb-288">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="26fcb-289">Veja a seção [Mapear colunas de conjunto de dados de origem para colunas do conjunto de dados de destino](data-factory-map-columns.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="26fcb-289">See [Map source dataset columns to destination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="26fcb-290">`jsonNodeReference` indica iterar e extrair dados dos objetos com o mesmo padrão em linhas da ordem da **matriz**.</span><span class="sxs-lookup"><span data-stu-id="26fcb-290">`jsonNodeReference` indicates to iterate and extract data from the objects with the same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="26fcb-291">`jsonPathDefinition` especifica o caminho JSON para cada coluna que indica de onde extrair os dados.</span><span class="sxs-lookup"><span data-stu-id="26fcb-291">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="26fcb-292">Neste exemplo, "ordernumber", "orderdate" e "city" estão sob o objeto root com caminho JSON começando com"$.", enquanto "order_pd" e "order_price" são definidos com caminho derivado do elemento de matriz sem "$.".</span><span class="sxs-lookup"><span data-stu-id="26fcb-292">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from the array element without "$.".</span></span>

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

<span data-ttu-id="26fcb-293">**Observe os seguintes pontos:**</span><span class="sxs-lookup"><span data-stu-id="26fcb-293">**Note the following points:**</span></span>

* <span data-ttu-id="26fcb-294">Se `structure` e `jsonPathDefinition` não forem definidos no conjunto de dados do Data Factory, a atividade de cópia detectará o esquema do primeiro objeto e mesclará todo o objeto.</span><span class="sxs-lookup"><span data-stu-id="26fcb-294">If the `structure` and `jsonPathDefinition` are not defined in the Data Factory dataset, the Copy Activity detects the schema from the first object and flatten the whole object.</span></span>
* <span data-ttu-id="26fcb-295">Se a entrada JSON tiver uma matriz por padrão, a atividade de cópia converterá o valor da matriz inteira em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="26fcb-295">If the JSON input has an array, by default the Copy Activity converts the entire array value into a string.</span></span> <span data-ttu-id="26fcb-296">Você pode optar por extrair dados dele usando o `jsonNodeReference` e/ou o `jsonPathDefinition` ou ignorá-lo ao não especificá-lo no `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="26fcb-296">You can choose to extract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="26fcb-297">Se houver nomes duplicados no mesmo nível, a atividade de cópia selecionará o último entre eles.</span><span class="sxs-lookup"><span data-stu-id="26fcb-297">If there are duplicate names at the same level, the Copy Activity picks the last one.</span></span>
* <span data-ttu-id="26fcb-298">Os nomes de propriedade diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="26fcb-298">Property names are case-sensitive.</span></span> <span data-ttu-id="26fcb-299">Duas propriedades com o mesmo nome, mas com maiúsculas e minúsculas diferentes são tratadas como duas propriedades separadas.</span><span class="sxs-lookup"><span data-stu-id="26fcb-299">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="26fcb-300">**Caso 2: gravação de dados no arquivo JSON**</span><span class="sxs-lookup"><span data-stu-id="26fcb-300">**Case 2: Writing data to JSON file**</span></span>

<span data-ttu-id="26fcb-301">Se você tiver a tabela a seguir no Banco de Dados SQL:</span><span class="sxs-lookup"><span data-stu-id="26fcb-301">If you have the following table in SQL Database:</span></span>

| <span data-ttu-id="26fcb-302">ID</span><span class="sxs-lookup"><span data-stu-id="26fcb-302">id</span></span> | <span data-ttu-id="26fcb-303">order_date</span><span class="sxs-lookup"><span data-stu-id="26fcb-303">order_date</span></span> | <span data-ttu-id="26fcb-304">order_price</span><span class="sxs-lookup"><span data-stu-id="26fcb-304">order_price</span></span> | <span data-ttu-id="26fcb-305">order_by</span><span class="sxs-lookup"><span data-stu-id="26fcb-305">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="26fcb-306">1</span><span class="sxs-lookup"><span data-stu-id="26fcb-306">1</span></span> | <span data-ttu-id="26fcb-307">20170119</span><span class="sxs-lookup"><span data-stu-id="26fcb-307">20170119</span></span> | <span data-ttu-id="26fcb-308">2000</span><span class="sxs-lookup"><span data-stu-id="26fcb-308">2000</span></span> | <span data-ttu-id="26fcb-309">Davi</span><span class="sxs-lookup"><span data-stu-id="26fcb-309">David</span></span> |
| <span data-ttu-id="26fcb-310">2</span><span class="sxs-lookup"><span data-stu-id="26fcb-310">2</span></span> | <span data-ttu-id="26fcb-311">20170120</span><span class="sxs-lookup"><span data-stu-id="26fcb-311">20170120</span></span> | <span data-ttu-id="26fcb-312">3500</span><span class="sxs-lookup"><span data-stu-id="26fcb-312">3500</span></span> | <span data-ttu-id="26fcb-313">Pedro</span><span class="sxs-lookup"><span data-stu-id="26fcb-313">Patrick</span></span> |
| <span data-ttu-id="26fcb-314">3</span><span class="sxs-lookup"><span data-stu-id="26fcb-314">3</span></span> | <span data-ttu-id="26fcb-315">20170121</span><span class="sxs-lookup"><span data-stu-id="26fcb-315">20170121</span></span> | <span data-ttu-id="26fcb-316">4000</span><span class="sxs-lookup"><span data-stu-id="26fcb-316">4000</span></span> | <span data-ttu-id="26fcb-317">Jason</span><span class="sxs-lookup"><span data-stu-id="26fcb-317">Jason</span></span> |

<span data-ttu-id="26fcb-318">e, para cada registro, você espera gravar em um objeto JSON neste formato:</span><span class="sxs-lookup"><span data-stu-id="26fcb-318">and for each record, you expect to write to a JSON object in the following format:</span></span>
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

<span data-ttu-id="26fcb-319">O conjunto de dados de saída com o tipo **JsonFormat** é definido da seguinte maneira: (definição parcial com apenas as partes relevantes).</span><span class="sxs-lookup"><span data-stu-id="26fcb-319">The output dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="26fcb-320">Mais especificamente, a seção `structure` define os nomes de propriedade personalizada no arquivo de destino, `nestingSeparator` (o padrão é ".") que são usados para identificar a camada de aninhamento do nome.</span><span class="sxs-lookup"><span data-stu-id="26fcb-320">More specifically, `structure` section defines the customized property names in destination file, `nestingSeparator` (default is ".") are used to identify the nest layer from the name.</span></span> <span data-ttu-id="26fcb-321">Esta seção é **opcional**, a menos que você queira alterar o nome da propriedade em comparação ao nome da coluna de origem ou aninhar algumas das propriedades.</span><span class="sxs-lookup"><span data-stu-id="26fcb-321">This section is **optional** unless you want to change the property name comparing with source column name, or nest some of the properties.</span></span>

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

## <a name="avro-format"></a><span data-ttu-id="26fcb-322">Formato AVRO</span><span class="sxs-lookup"><span data-stu-id="26fcb-322">AVRO format</span></span>
<span data-ttu-id="26fcb-323">Se você quiser analisar os arquivos Avro ou gravar os dados no formato Avro, defina a propriedade `format` `type` como **AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="26fcb-323">If you want to parse the Avro files or write the data in Avro format, set the `format` `type` property to **AvroFormat**.</span></span> <span data-ttu-id="26fcb-324">Não será necessário especificar nenhuma propriedade na seção Formato dentro da seção typeProperties.</span><span class="sxs-lookup"><span data-stu-id="26fcb-324">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="26fcb-325">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="26fcb-325">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="26fcb-326">Para usar o formato Avro em uma tabela de Hive, confira [Tutorial do Apache Hive](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span><span class="sxs-lookup"><span data-stu-id="26fcb-326">To use Avro format in a Hive table, you can refer to [Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="26fcb-327">Observe os seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="26fcb-327">Note the following points:</span></span>  

* <span data-ttu-id="26fcb-328">Não há suporte para [tipos de dados complexos](http://avro.apache.org/docs/current/spec.html#schema_complex) (registros, enumerações, matrizes, mapas, uniões e fixo).</span><span class="sxs-lookup"><span data-stu-id="26fcb-328">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions, and fixed).</span></span>

## <a name="orc-format"></a><span data-ttu-id="26fcb-329">Formato ORC</span><span class="sxs-lookup"><span data-stu-id="26fcb-329">ORC format</span></span>
<span data-ttu-id="26fcb-330">Se você quiser analisar os arquivos ORC ou gravar os dados no formato ORC, defina a propriedade `format` `type` como **OrcFormat**.</span><span class="sxs-lookup"><span data-stu-id="26fcb-330">If you want to parse the ORC files or write the data in ORC format, set the `format` `type` property to **OrcFormat**.</span></span> <span data-ttu-id="26fcb-331">Não será necessário especificar nenhuma propriedade na seção Formato dentro da seção typeProperties.</span><span class="sxs-lookup"><span data-stu-id="26fcb-331">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="26fcb-332">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="26fcb-332">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="26fcb-333">Se você não estiver copiando arquivos ORC **como são** entre repositórios de dados locais e na nuvem, você precisará instalar o JRE 8 (Java Runtime Environment) no computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="26fcb-333">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="26fcb-334">Um gateway de 64 bits exige JRE de 64 bits, enquanto um gateway de 32 bits exige JRE de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="26fcb-334">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="26fcb-335">Você pode encontrar as duas versões [aqui](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="26fcb-335">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="26fcb-336">Escolha aquela que for apropriada.</span><span class="sxs-lookup"><span data-stu-id="26fcb-336">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="26fcb-337">Observe os seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="26fcb-337">Note the following points:</span></span>

* <span data-ttu-id="26fcb-338">Não há suporte para tipos de dados complexos (STRUCT, MAP, LIST e UNION)</span><span class="sxs-lookup"><span data-stu-id="26fcb-338">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="26fcb-339">O arquivo ORC tem três [opções de compactação](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB e SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="26fcb-339">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="26fcb-340">O Data Factory dá suporte à leitura de dados de arquivo ORC em qualquer um dos formatos compactados acima.</span><span class="sxs-lookup"><span data-stu-id="26fcb-340">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="26fcb-341">Ele usa o codec de compactação nos metadados para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="26fcb-341">It uses the compression codec is in the metadata to read the data.</span></span> <span data-ttu-id="26fcb-342">No entanto, ao gravar um arquivo ORC, o Data Factory escolhe ZLIB, que é o padrão para ORC.</span><span class="sxs-lookup"><span data-stu-id="26fcb-342">However, when writing to an ORC file, Data Factory chooses ZLIB, which is the default for ORC.</span></span> <span data-ttu-id="26fcb-343">Não há nenhuma opção para substituir esse comportamento neste momento.</span><span class="sxs-lookup"><span data-stu-id="26fcb-343">Currently, there is no option to override this behavior.</span></span>

## <a name="parquet-format"></a><span data-ttu-id="26fcb-344">Formato Parquet</span><span class="sxs-lookup"><span data-stu-id="26fcb-344">Parquet format</span></span>
<span data-ttu-id="26fcb-345">Se você quiser analisar os arquivos Parquet ou gravar os dados no formato Parquet, defina a propriedade `format` `type` como **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="26fcb-345">If you want to parse the Parquet files or write the data in Parquet format, set the `format` `type` property to **ParquetFormat**.</span></span> <span data-ttu-id="26fcb-346">Não será necessário especificar nenhuma propriedade na seção Formato dentro da seção typeProperties.</span><span class="sxs-lookup"><span data-stu-id="26fcb-346">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="26fcb-347">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="26fcb-347">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="26fcb-348">Se você não estiver copiando arquivos Parquet **no estado em que se encontram** entre armazenamentos de dados locais e na nuvem, você precisará instalar o JRE 8 (Java Runtime Environment) no computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="26fcb-348">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="26fcb-349">Um gateway de 64 bits exige JRE de 64 bits, enquanto um gateway de 32 bits exige JRE de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="26fcb-349">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="26fcb-350">Você pode encontrar as duas versões [aqui](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="26fcb-350">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="26fcb-351">Escolha aquela que for apropriada.</span><span class="sxs-lookup"><span data-stu-id="26fcb-351">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="26fcb-352">Observe os seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="26fcb-352">Note the following points:</span></span>

* <span data-ttu-id="26fcb-353">Não há suporte para tipos de dados complexos (MAP, LIST)</span><span class="sxs-lookup"><span data-stu-id="26fcb-353">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="26fcb-354">O arquivo Parquet tem as seguintes opções relacionadas à compactação: NONE, SNAPPY, GZIP e LZO.</span><span class="sxs-lookup"><span data-stu-id="26fcb-354">Parquet file has the following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="26fcb-355">O Data Factory dá suporte à leitura de dados de arquivo ORC em qualquer um dos formatos compactados acima.</span><span class="sxs-lookup"><span data-stu-id="26fcb-355">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="26fcb-356">Ele usa o codec de compactação nos metadados para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="26fcb-356">It uses the compression codec in the metadata to read the data.</span></span> <span data-ttu-id="26fcb-357">No entanto, ao gravar um arquivo Parquet, o Data Factory escolhe SNAPPY, que é o padrão para o formato Parquet.</span><span class="sxs-lookup"><span data-stu-id="26fcb-357">However, when writing to a Parquet file, Data Factory chooses SNAPPY, which is the default for Parquet format.</span></span> <span data-ttu-id="26fcb-358">Não há nenhuma opção para substituir esse comportamento neste momento.</span><span class="sxs-lookup"><span data-stu-id="26fcb-358">Currently, there is no option to override this behavior.</span></span>

## <a name="compression-support"></a><span data-ttu-id="26fcb-359">Suporte à compactação</span><span class="sxs-lookup"><span data-stu-id="26fcb-359">Compression support</span></span>
<span data-ttu-id="26fcb-360">O processamento de grandes conjuntos de dados pode causar afunilamentos de E/S e de rede.</span><span class="sxs-lookup"><span data-stu-id="26fcb-360">Processing large data sets can cause I/O and network bottlenecks.</span></span> <span data-ttu-id="26fcb-361">Portanto, os dados compactados em repositórios não apenas aceleram a transferência de dados pela rede e economizam espaço em disco, mas também oferecem aprimoramentos consideráveis de desempenho no processamento de Big Data.</span><span class="sxs-lookup"><span data-stu-id="26fcb-361">Therefore, compressed data in stores can not only speed up data transfer across the network and save disk space, but also bring significant performance improvements in processing big data.</span></span> <span data-ttu-id="26fcb-362">No momento, a compactação tem suporte para repositórios de dados baseados em arquivo, por exemplo, Blob do Azure ou o Sistema de Arquivos Local.</span><span class="sxs-lookup"><span data-stu-id="26fcb-362">Currently, compression is supported for file-based data stores such as Azure Blob or On-premises File System.</span></span>  

<span data-ttu-id="26fcb-363">Para especificar a compactação de um conjunto de dados, use a propriedade **compactação** no conjunto de dados JSON, como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="26fcb-363">To specify compression for a dataset, use the **compression** property in the dataset JSON as in the following example:</span></span>   

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

<span data-ttu-id="26fcb-364">Suponhamos que o conjunto de dados de exemplo seja usado como a saída de uma atividade de cópia. A atividade de cópia compacta os dados de saída com o codec GZIP usando a melhor taxa e, em seguida, grava os dados compactados em um arquivo chamado pagecounts.csv.gz no Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="26fcb-364">Suppose the sample dataset is used as the output of a copy activity, the copy activity compresses the output data with GZIP codec using optimal ratio and then write the compressed data into a file named pagecounts.csv.gz in the Azure Blob Storage.</span></span>

> [!NOTE]
> <span data-ttu-id="26fcb-365">Não há suporte para configurações de compactação de dados no **AvroFormat**, **OrcFormat** ou **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="26fcb-365">Compression settings are not supported for data in the **AvroFormat**, **OrcFormat**, or **ParquetFormat**.</span></span> <span data-ttu-id="26fcb-366">Ao ler arquivos nesses formatos, o Data Factory detecta e usa o codec de compactação nos metadados.</span><span class="sxs-lookup"><span data-stu-id="26fcb-366">When reading files in these formats, Data Factory detects and uses the compression codec in the metadata.</span></span> <span data-ttu-id="26fcb-367">Ao gravar em arquivos em um desses formatos, o Data Factory escolhe o codec de compactação padrão para esse formato.</span><span class="sxs-lookup"><span data-stu-id="26fcb-367">When writing to files in these formats, Data Factory chooses the default compression codec for that format.</span></span> <span data-ttu-id="26fcb-368">Por exemplo, ZLIB para OrcFormat e SNAPPY para ParquetFormat.</span><span class="sxs-lookup"><span data-stu-id="26fcb-368">For example, ZLIB for OrcFormat and SNAPPY for ParquetFormat.</span></span>   

<span data-ttu-id="26fcb-369">A seção **compactação** tem duas propriedades:</span><span class="sxs-lookup"><span data-stu-id="26fcb-369">The **compression** section has two properties:</span></span>  

* <span data-ttu-id="26fcb-370">**Tipo:** o codec de compactação, que pode ser **GZIP**, **Deflate**, **BZIP2** ou **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="26fcb-370">**Type:** the compression codec, which can be **GZIP**, **Deflate**, **BZIP2**, or **ZipDeflate**.</span></span>  
* <span data-ttu-id="26fcb-371">**Nível:** a taxa de compactação, que pode ser **Ideal** ou **Mais rápida**.</span><span class="sxs-lookup"><span data-stu-id="26fcb-371">**Level:** the compression ratio, which can be **Optimal** or **Fastest**.</span></span>

  * <span data-ttu-id="26fcb-372">**Mais rápida:** a operação de compactação deve ser concluída o mais rápido possível, mesmo se o arquivo resultante não for compactado da maneira ideal.</span><span class="sxs-lookup"><span data-stu-id="26fcb-372">**Fastest:** The compression operation should complete as quickly as possible, even if the resulting file is not optimally compressed.</span></span>
  * <span data-ttu-id="26fcb-373">**Ideal**: a operação de compactação deve ser concluída da maneira ideal, mesmo se a operação demorar mais tempo para ser concluída.</span><span class="sxs-lookup"><span data-stu-id="26fcb-373">**Optimal**: The compression operation should be optimally compressed, even if the operation takes a longer time to complete.</span></span>

    <span data-ttu-id="26fcb-374">Para saber mais, veja o tópico [Nível de compactação](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) .</span><span class="sxs-lookup"><span data-stu-id="26fcb-374">For more information, see [Compression Level](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) topic.</span></span>

<span data-ttu-id="26fcb-375">Quando você especifica a propriedade `compression` em um conjunto de dados de entrada JSON, o pipeline pode ler os dados compactados da origem e, quando você especifica a propriedade em um conjunto de dados de saída JSON, a atividade de cópia pode gravar dados compactados no destino.</span><span class="sxs-lookup"><span data-stu-id="26fcb-375">When you specify `compression` property in an input dataset JSON, the pipeline can read compressed data from the source; and when you specify the property in an output dataset JSON, the copy activity can write compressed data to the destination.</span></span> <span data-ttu-id="26fcb-376">Aqui estão alguns exemplos de cenários:</span><span class="sxs-lookup"><span data-stu-id="26fcb-376">Here are a few sample scenarios:</span></span>

* <span data-ttu-id="26fcb-377">Ler dados compactados em GZIP de um blob do Azure, descompactá-los e gravar os dados resultantes em um banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="26fcb-377">Read GZIP compressed data from an Azure blob, decompress it, and write result data to an Azure SQL database.</span></span> <span data-ttu-id="26fcb-378">Você define o conjunto de dados de Blob do Azure de entrada com `compression` `type` a propriedade JSON como GZIP.</span><span class="sxs-lookup"><span data-stu-id="26fcb-378">You define the input Azure Blob dataset with the `compression` `type` JSON property as GZIP.</span></span>
* <span data-ttu-id="26fcb-379">Ler dados de um arquivo de texto sem formatação do Sistema de arquivos local, compactá-los usando o formato GZip e gravar os dados compactados em um blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="26fcb-379">Read data from a plain-text file from on-premises File System, compress it using GZip format, and write the compressed data to an Azure blob.</span></span> <span data-ttu-id="26fcb-380">Você define um conjunto de dados de Blob do Azure de saída com a `compression` `type` propriedade JSON como GZip.</span><span class="sxs-lookup"><span data-stu-id="26fcb-380">You define an output Azure Blob dataset with the `compression` `type` JSON property as GZip.</span></span>
* <span data-ttu-id="26fcb-381">Leia o arquivo .zip de servidor FTP, descompacte-o para obter os arquivos contidos nele e inclua-os no Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="26fcb-381">Read .zip file from FTP server, decompress it to get the files inside, and land those files into Azure Data Lake Store.</span></span> <span data-ttu-id="26fcb-382">Você define um conjunto de dados FTP de entrada com a `compression` `type` propriedade JSON como ZipDeflate.</span><span class="sxs-lookup"><span data-stu-id="26fcb-382">You define an input FTP dataset with the `compression` `type` JSON property as ZipDeflate.</span></span>
* <span data-ttu-id="26fcb-383">Ler dados compactados em GZIP de um blob do Azure, descompactá-los, compactá-los usando BZIP2 e gravar os dados de resultado em um blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="26fcb-383">Read a GZIP-compressed data from an Azure blob, decompress it, compress it using BZIP2, and write result data to an Azure blob.</span></span> <span data-ttu-id="26fcb-384">Você define o conjunto de dados de Blob do Azure entradas com `compression` `type` definido como GZIP e o conjunto de dados de saída com `compression` `type` definido como BZIP2 nesse caso.</span><span class="sxs-lookup"><span data-stu-id="26fcb-384">You define the input Azure Blob dataset with `compression` `type` set to GZIP and the output dataset with `compression` `type` set to BZIP2 in this case.</span></span>   


## <a name="next-steps"></a><span data-ttu-id="26fcb-385">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="26fcb-385">Next steps</span></span>
<span data-ttu-id="26fcb-386">Consulte os artigos a seguir para armazenamentos de dados baseados em arquivo com suporte pelo Azure Data Factory:</span><span class="sxs-lookup"><span data-stu-id="26fcb-386">See the following articles for file-based data stores supported by Azure Data Factory:</span></span>

- [<span data-ttu-id="26fcb-387">Armazenamento de Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="26fcb-387">Azure Blob Storage</span></span>](data-factory-azure-blob-connector.md)
- [<span data-ttu-id="26fcb-388">Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="26fcb-388">Azure Data Lake Store</span></span>](data-factory-azure-datalake-connector.md)
- [<span data-ttu-id="26fcb-389">FTP</span><span class="sxs-lookup"><span data-stu-id="26fcb-389">FTP</span></span>](data-factory-ftp-connector.md)
- [<span data-ttu-id="26fcb-390">HDFS</span><span class="sxs-lookup"><span data-stu-id="26fcb-390">HDFS</span></span>](data-factory-hdfs-connector.md)
- [<span data-ttu-id="26fcb-391">Sistema de Arquivos</span><span class="sxs-lookup"><span data-stu-id="26fcb-391">File System</span></span>](data-factory-onprem-file-system-connector.md)
- [<span data-ttu-id="26fcb-392">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="26fcb-392">Amazon S3</span></span>](data-factory-amazon-simple-storage-service-connector.md)
