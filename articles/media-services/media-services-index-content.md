---
title: "aaaIndexing arquivos de mídia com o Azure Media Indexer"
description: "Indexador de mídia do Azure permite que você toomake conteúdo de seus arquivos de mídia pesquisáveis e toogenerate uma transcrição de texto completo para legendas e palavras-chave. Este tópico mostra como toouse indexador de mídia."
services: media-services
documentationcenter: 
author: Asolanki
manager: cfowler
editor: 
ms.assetid: 827a56b2-58a5-4044-8d5c-3e5356488271
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/20/2017
ms.author: adsolank;juliako;johndeu
ms.openlocfilehash: c1bed774e302e61ca3510668645dc2015b434a0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-media-files-with-azure-media-indexer"></a>Indexando arquivos de mídia com o Indexador de Mídia do Azure
Indexador de mídia do Azure permite que você toomake conteúdo de seus arquivos de mídia pesquisáveis e toogenerate uma transcrição de texto completo para legendas e palavras-chave. É possível processar um arquivo de mídia ou vários arquivos de mídia em um lote.  

> [!IMPORTANT]
> Quando a indexação de conteúdo, verifique se toouse arquivos de mídia com fala muito clara (sem música em segundo plano, ruído, efeitos ou assovio de microfone). Alguns exemplos de conteúdo apropriado são: reuniões, palestras e apresentações registradas. Olá seguinte conteúdo pode não ser adequado para indexação: filmes, programas de TV, tudo com misto de áudio e efeitos sonoros, conteúdo mal registrado com ruídos de fundo (assovio).
> 
> 

Um trabalho de indexação pode gerar Olá saídas a seguir:

* Arquivos de legenda no hello formatos a seguir: **SAMI**, **TTML**, e **WebVTT**.
  
    Arquivos de legenda codificada incluem uma marca chamada Recognizability, que classifica um trabalho de indexação com base no nível de reconhecimento de fala de saudação vídeo de origem Olá é.  Você pode usar o valor de saudação Recognizability tooscreen de arquivos de saída para uso. Uma baixa pontuação significará resultados fracos de indexação devido tooaudio qualidade.
* Arquivo de palavra-chave (XML).
* Áudio de indexação de arquivo de blob (AIB) para uso com o SQL Server.
  
    Para obter mais informações, consulte [Usando arquivos de AIB com o indexador de mídia do Azure e SQL Server](https://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/).

Este tópico mostra como a indexação de toocreate trabalhos muito**indexar um ativo** e **indexar vários arquivos**.

Atualizações mais recentes de indexador de mídia do Azure hello, consulte [blogs dos serviços de mídia](#preset).

## <a name="using-configuration-and-manifest-files-for-indexing-tasks"></a>Usando arquivos de configuração e de manifesto para tarefas de indexação
Você pode especificar mais detalhes para as tarefas de indexação usando uma configuração de tarefa. Por exemplo, você pode especificar quais toouse metadados para o arquivo de mídia. Esses metadados são usados pelo Olá idioma mecanismo tooexpand seu vocabulário e melhora significativamente a precisão do reconhecimento de fala hello.  Você também é toospecify capaz de seus arquivos de saída desejada.

Você também pode processar vários arquivos de mídia ao mesmo tempo usando um arquivo de manifesto.

Para saber mais, consulte [Predefinição de tarefa para o Indexador de Mídia do Azure](https://msdn.microsoft.com/library/dn783454.aspx).

## <a name="index-an-asset"></a>Indexe um ativo
Olá método a seguir carrega um arquivo de mídia como um ativo e cria um ativo de saudação do tooindex de trabalho.

Observe que, se nenhum arquivo de configuração for especificado, o arquivo de mídia Olá será indexado com todas as configurações padrão.

    static bool RunIndexingJob(string inputMediaFilePath, string outputFolder, string configurationFile = "")
    {
        // Create an asset and upload hello input media file toostorage.
        IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Indexing Input Asset",
            AssetCreationOptions.None);

        // Declare a new job.
        IJob job = _context.Jobs.Create("My Indexing Job");

        // Get a reference toohello Azure Media Indexer.
        string MediaProcessorName = "Azure Media Indexer";
        IMediaProcessor processor = GetLatestMediaProcessorByName(MediaProcessorName);

        // Read configuration from file if specified.
        string configuration = string.IsNullOrEmpty(configurationFile) ? "" : File.ReadAllText(configurationFile);

        // Create a task with hello encoding details, using a string preset.
        ITask task = job.Tasks.AddNew("My Indexing Task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input asset toobe indexed.
        task.InputAssets.Add(asset);

        // Add an output asset toocontain hello results of hello job.
        task.OutputAssets.AddNew("My Indexing Output Asset", AssetCreationOptions.None);

        // Use hello following event handler toocheck job progress.  
        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

        // Launch hello job.
        job.Submit();

        // Check job execution and wait for job toofinish.
        Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
        progressJobTask.Wait();

        // If job state is Error, hello event handling
        // method for job progress should log errors.  Here we check
        // for error state and exit if needed.
        if (job.State == JobState.Error)
        {
            Console.WriteLine("Exiting method due toojob error.");
            return false;
        }

        // Download hello job outputs.
        DownloadAsset(task.OutputAssets.First(), outputFolder);

        return true;
    }

    static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
    {
        IAsset asset = _context.Assets.Create(assetName, options);

        var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
        assetFile.Upload(filePath);

        return asset;
    }

    static void DownloadAsset(IAsset asset, string outputDirectory)
    {
        foreach (IAssetFile file in asset.AssetFiles)
        {
            file.Download(Path.Combine(outputDirectory, file.Name));
        }
    }

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors
        .Where(p => p.Name == mediaProcessorName)
        .ToList()
        .OrderBy(p => new Version(p.Version))
        .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }  
<!-- __ -->
### <a id="output_files"></a>Arquivos de saída
Por padrão, um trabalho de indexação gera Olá arquivos de saída a seguir. Olá arquivos serão armazenados no primeiro ativo de saída hello.

Quando há mais de um arquivo de mídia de entrada, o indexador irá gerar um arquivo de manifesto para saídas de trabalho hello, chamado 'JobResult.txt'. Para cada arquivo de mídia de entrada, hello resultante AIB, SAMI, TTML, WebVTT e arquivos de palavra-chave são sequencialmente numerados e nomeados usando hello "Alias".

| Nome do arquivo | Descrição |
| --- | --- |
| **InputFileName.aib** |Arquivo de blob de indexação de áudio. <br/><br/> O arquivo de Blob de Indexação de Áudio (AIB) é um arquivo binário que pode ser pesquisado no Microsoft SQL Server usando a pesquisa de texto completa.  arquivo AIB de saudação é mais eficiente do que arquivos de legenda simples hello, porque ele contém alternativas para cada palavra, permitindo uma experiência de pesquisa mais rica. <br/> <br/>Ele requer a instalação de saudação do complemento do indexador SQL Olá em um computador executando Microsoft SQL server 2008 ou posterior. Pesquisa de texto completo do servidor pesquisando Olá AIB usando o Microsoft SQL fornece resultados mais precisos que pesquisa Olá fechado arquivos de legenda gerados por WAMI. Isso ocorre porque Olá AIB contém alternativas de palavras som semelhante enquanto Olá fechado arquivos de legenda contêm a palavra de maior confiança Olá para cada segmento de áudio hello. Se a pesquisa de palavras faladas for imprescindível, em seguida, é recomendável toouse Olá AIB em conjunto com o Microsoft SQL Server.<br/><br/> toodownload Olá complemento, clique em <a href="http://aka.ms/indexersql">complemento de SQL do Azure Media indexador</a>. <br/><br/>Ele também é possível tooutilize outros mecanismos de pesquisa, como Apache Lucene/Solr vídeo de saudação de índice de toosimply baseados em legenda Olá fechado e a palavra-chave arquivos XML, mas isso resultará em resultados da pesquisa menos precisos. |
| **InputFileName.smi**<br/>**InputFileName.ttml**<br/>**InputFileName.vtt** |Arquivos de Legenda Oculta (CC) nos formatos SAMI, TTML e WebVTT.<br/><br/>Eles podem ser usados toomake áudio e vídeo arquivos toopeople acessível com deficiência auditiva.<br/><br/>Arquivos de legenda codificados incluem uma marca chamada <b>Recognizability</b> que classifica um trabalho de indexação com base no nível de reconhecimento de fala de saudação vídeo de origem Olá é.  Você pode usar o valor de saudação do <b>Recognizability</b> tooscreen os arquivos para facilitar o uso de saída. Uma baixa pontuação significará resultados fracos de indexação devido tooaudio qualidade. |
| **InputFileName.kw.xml<br/>InputFileName.info** |Arquivos de palavra-chave e de informações. <br/><br/>Arquivo de palavra-chave é um arquivo XML que contém as palavras-chave extraídas do conteúdo de fala hello, com frequência e a informação de deslocamento. <br/><br/>Um arquivo de informações é um arquivo de texto sem formatação com informações completas sobre cada termo reconhecido. Olá primeira linha é especial e contém Olá Recognizability pontuação. Cada linha subsequente é uma lista separada por guia de saudação seguintes dados: iniciar o tempo, a hora de término, o word/frase, confiança. Olá tempos são fornecidos em segundos e confiança Olá é fornecida como um número de 0-1. <br/><br/>Linha de exemplo: "1.20    1.45    word    0.67" <br/><br/>Esses arquivos podem ser usados para diversos fins, como análise de fala tooperform ou toosearch exposto mecanismos, como o Bing, Google ou Microsoft SharePoint toomake Olá arquivos de mídia mais detectáveis, ou até mesmo utilizada toodeliver anúncios mais relevantes. |
| **JobResult.txt** |Manifesto de saída, presente somente quando a indexação de vários arquivos, que contém a saudação informações a seguir:<br/><br/><table border="1"><tr><th>InputFile</th><th>Alias</th><th>MediaLength</th><th>Erro</th></tr><tr><td>a.mp4</td><td>Media_1</td><td>300</td><td>0</td></tr><tr><td>b.mp4</td><td>Media_2</td><td>0</td><td>3000</td></tr><tr><td>c.mp4</td><td>Media_3</td><td>600</td><td>0</td></tr></table><br/> |

Se nem todos os arquivos de mídia de entrada forem indexados com êxito, o trabalho de indexação Olá falhará com o código de erro 4000. Para saber mais, consulte [Códigos de erro](#error_codes).

## <a name="index-multiple-files"></a>Indexar vários arquivos
Olá método a seguir carrega vários arquivos de mídia como um ativo e cria um trabalho tooindex todos esses arquivos em um lote.

Um arquivo de manifesto com extensão. lst de saudação é criado e carregado no ativo de saudação. arquivo de manifesto Olá contém a lista de saudação de todos os arquivos de ativo de saudação. Para saber mais, consulte [Predefinição de tarefa para o Indexador de Mídia do Azure](https://msdn.microsoft.com/library/dn783454.aspx).

    static bool RunBatchIndexingJob(string[] inputMediaFiles, string outputFolder)
    {
        // Create an asset and upload toostorage.
        IAsset asset = CreateAssetAndUploadMultipleFiles(inputMediaFiles,
            "My Indexing Input Asset - Batch Mode",
            AssetCreationOptions.None);

        // Create a manifest file that contains all hello asset file names and upload toostorage.
        string manifestFile = "input.lst";            
        File.WriteAllLines(manifestFile, asset.AssetFiles.Select(f => f.Name).ToArray());
        var assetFile = asset.AssetFiles.Create(Path.GetFileName(manifestFile));
        assetFile.Upload(manifestFile);

        // Declare a new job.
        IJob job = _context.Jobs.Create("My Indexing Job - Batch Mode");

        // Get a reference toohello Azure Media Indexer.
        string MediaProcessorName = "Azure Media Indexer";
        IMediaProcessor processor = GetLatestMediaProcessorByName(MediaProcessorName);

        // Read configuration.
        string configuration = File.ReadAllText("batch.config");

        // Create a task with hello encoding details, using a string preset.
        ITask task = job.Tasks.AddNew("My Indexing Task - Batch Mode",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input asset toobe indexed.
        task.InputAssets.Add(asset);

        // Add an output asset toocontain hello results of hello job.
        task.OutputAssets.AddNew("My Indexing Output Asset - Batch Mode", AssetCreationOptions.None);

        // Use hello following event handler toocheck job progress.  
        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

        // Launch hello job.
        job.Submit();

        // Check job execution and wait for job toofinish.
        Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
        progressJobTask.Wait();

        // If job state is Error, hello event handling
        // method for job progress should log errors.  Here we check
        // for error state and exit if needed.
        if (job.State == JobState.Error)
        {
            Console.WriteLine("Exiting method due toojob error.");
            return false;
        }

        // Download hello job outputs.
        DownloadAsset(task.OutputAssets.First(), outputFolder);

        return true;
    }

    private static IAsset CreateAssetAndUploadMultipleFiles(string[] filePaths, string assetName, AssetCreationOptions options)
    {
        IAsset asset = _context.Assets.Create(assetName, options);

        foreach (string filePath in filePaths)
        {
            var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
            assetFile.Upload(filePath);
        }

        return asset;
    }

### <a name="partially-succeeded-job"></a>Trabalho parcialmente bem-sucedido
Se nem todos os arquivos de mídia de entrada forem indexados com êxito, o trabalho de indexação Olá falhará com o código de erro 4000. Para saber mais, consulte [Códigos de erro](#error_codes).

Olá mesmas saídas (como tarefas bem-sucedidas) são gerados. Você pode consultar toohello saída arquivo de manifesto toofind quais arquivos de entrada falharam, de acordo com toohello valores de coluna de erro. Para arquivos de entrada com falha, Olá resultante AIB, SAMI, TTML, WebVTT e não serão gerados arquivos de palavra-chave.

### <a id="preset"></a> Predefinição de tarefa para o Indexador de Mídia do Azure
saudação de processamento do indexador de mídia do Azure pode ser personalizada, fornecendo uma tarefa opcional predefinição junto com a tarefa de saudação.  a seguir Olá descreve o formato de saudação desse XML de configuração.

| Nome | Exigência | Descrição |
| --- | --- | --- |
| **input** |false |Arquivos de ativo que você deseja tooindex.</p><p>Indexador de mídia do Azure oferece suporte a saudação formatos de arquivo de mídia a seguir: MP4, WMV, MP3, M4A, WMA, AAC, WAV.</p><p>Você pode especificar o nome do arquivo hello (s) em Olá **nome** ou **lista** atributo de saudação **entrada** elemento (conforme mostrado abaixo). Se você não especificar qual tooindex de arquivo ativo, o arquivo primário Olá é escolhido. Se nenhum arquivo de ativo primário for definido, o primeiro arquivo hello ativo de entrada hello é indexado.</p><p>tooexplicitly especificar nome de arquivo de ativo hello, faça:<br/>`<input name="TestFile.wmv">`<br/><br/>Você também pode indexar vários arquivos de ativo de uma vez (backup de arquivos de too10). toodo isso:<br/><br/><ol class="ordered"><li><p>Crie um arquivo de texto (arquivo de manifesto) e dê a ele uma extensão .lst. </p></li><li><p>Adicione uma lista de todos os nomes de arquivo de ativo de saudação em seu arquivo de manifesto toothis ativo de entrada. </p></li><li><p>Adicione (carregue) ativo de toohello de arquivo de manifesto.  </p></li><li><p>Especifique o nome de Olá Olá do arquivo de manifesto no atributo de lista de entrada hello.<br/>`<input list="input.lst">`</li></ol><br/><br/>Observação: Se você adicionar mais de 10 arquivos toohello o arquivo de manifesto, Olá trabalho de indexação falhará com o código de erro 2006 hello. |
| **metadados** |false |Metadados de saudação especificado usados para adaptação vocabulário de arquivos de ativo.  Palavras de vocabulário padronizado tooprepare útil indexador toorecognize como substantivos.<br/>`<metadata key="..." value="..."/>` <br/><br/>Você pode fornecer **valores** para **chaves** predefinidas. Atualmente, Olá chaves a seguir têm suporte:<br/><br/>"título" e "description" - usados para o idioma de saudação do vocabulário adaptação tootweak de modelo para o seu trabalho e melhorar a precisão do reconhecimento de fala.  os valores Hello propagação pesquisas toofind texto relevantes contextualmente documentos da Internet, usando o dicionário interno do Olá Olá conteúdo tooaugment durante saudação sua tarefa de indexação.<br/>`<metadata key="title" value="[Title of hello media file]" />`<br/>`<metadata key="description" value="[Description of hello media file] />"` |
| **funcionalidades** <br/><br/> Adicionado na versão 1.2. Atualmente, o recurso Olá só tem suportada é o reconhecimento de fala ("ASR"). |false |recurso de reconhecimento de fala Olá tem Olá chaves de configurações a seguir:<table><tr><th><p>Chave</p></th>        <th><p>Descrição</p></th><th><p>Valor de exemplo</p></th></tr><tr><td><p>idioma</p></td><td><p>Olá toobe de linguagem natural reconhecido no arquivo de multimídia hello.</p></td><td><p>Inglês, espanhol</p></td></tr><tr><td><p>CaptionFormats</p></td><td><p>uma lista separada por vírgulas dos formatos de legenda de saída Olá desejado (se houver)</p></td><td><p>ttml;sami;webvtt</p></td></tr><tr><td><p>GenerateAIB</p></td><td><p>Um sinalizador booleano que especifica se um arquivo AIB é necessário (para uso com o SQL Server e hello IFilter do indexador cliente).  Para obter mais informações, consulte <a href="http://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/">Usando arquivos de AIB com o indexador de mídia do Azure e SQL Server</a>.</p></td><td><p>Verdadeiro, Falso</p></td></tr><tr><td><p>GenerateKeywords</p></td><td><p>Um sinalizador booliano que especifica se um arquivo XML de palavras-chave é necessário.</p></td><td><p>True; False. </p></td></tr><tr><td><p>ForceFullCaption</p></td><td><p>Um sinalizador booliano que especifica se ou não tooforce completo legendas (independentemente do nível de confiança).  </p><p>Padrão é false, nesse caso, palavras e frases que têm um valor menor que o nível de confiança de 50% são omitidas da saudação legenda final saídas e substituídas por reticências ("...").  reticências Olá são úteis para auditoria e controle de qualidade de legenda.</p></td><td><p>True; False. </p></td></tr></table> |

### <a id="error_codes"></a>Códigos de erro
No caso de saudação de um erro, o indexador de mídia do Azure devem relatar fazer uma saudação códigos de erro a seguir:

| Código | Nome | Possíveis motivos |
| --- | --- | --- |
| 2000 |Configuração inválida |Configuração inválida |
| 2001 |Ativos de entrada inválidos |Faltando ativos de entrada ou um ativo vazio. |
| 2002 |Manifesto inválido |O manifesto está vazio ou o manifesto contém itens inválidos. |
| 2003 |Arquivo de mídia toodownload com falha |URL inválida no arquivo de manifesto. |
| 2004 |Protocolo não suportado |Não há suporte para o protocolo de URL de mídia. |
| 2005 |Tipo de arquivo sem suporte |Não há suporte para o tipo de arquivo de mídia de entrada. |
| 2006 |Muitos arquivos de entrada |Há mais de 10 arquivos no manifesto de entrada hello. |
| 3000 |Arquivo de mídia toodecode com falha |Codec de mídia sem suporte  <br/>ou o<br/> Arquivo de mídia corrompido <br/>ou o<br/> Nenhum fluxo de áudio na mídia de entrada. |
| 4000 |Indexação de lotes parcialmente bem-sucedida |Falha em algumas de mídia de entrada hello são arquivos toobe indexado. Para obter mais informações, consulte <a href="#output_files">Arquivos de saída</a>. |
| outros |Erros internos |Entre em contato com a equipe de suporte. indexer@microsoft.com |

## <a id="supported_languages"></a>Idiomas com suporte
Atualmente, há suporte para idiomas de saudação em inglês e espanhol. Para obter mais informações, consulte [Olá postagem de blog de versão v 1.2](https://azure.microsoft.com/blog/2015/04/13/azure-media-indexer-spanish-v1-2/).

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Links relacionados
[Visão geral da Análise dos Serviços de Mídia do Azure](media-services-analytics-overview.md)

[Usando arquivos AIB com o indexador de mídia do Azure e SQL Server](https://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/)

[Indexando arquivos de mídia com a Preview do Indexador de Mídia do Azure 2](media-services-process-content-with-indexer2.md)

