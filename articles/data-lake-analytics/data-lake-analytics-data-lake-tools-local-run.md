---
title: "aaaTest e depuração U-SQL trabalhos usando locais executar e Olá SDK do SQL Azure Data Lake U | Microsoft Docs"
description: "Saiba como toouse Azure Data Lake Tools para Visual Studio e tootest do SDK do Azure Data Lake U-SQL hello e depuração U-SQL trabalhos em sua estação de trabalho local."
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 66dd58b1-0b28-46d1-aaae-43ee2739ae0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/15/2016
ms.author: yanacai
ms.openlocfilehash: be04558a504acf6a088e207608ee2d4a011d3ffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-hello-azure-data-lake-u-sql-sdk"></a>Testar e depurar os trabalhos de U-SQL usando local executar e Olá SDK do Azure Data Lake U-SQL

Você pode usar o Azure Data Lake Tools para Visual Studio e trabalhos do hello SDK do Azure Data Lake U-SQL toorun U-SQL em sua estação de trabalho, exatamente como é possível no serviço do Azure Data Lake hello. Esses dois recursos de execução local economizam tempo no teste e na depuração de seus trabalhos de U-SQL.

## <a name="understand-hello-data-root-folder-and-hello-file-path"></a>Entender a pasta de dados raiz hello e caminho do arquivo hello

Execução local e Olá SDK U-SQL exigem uma pasta raiz de dados. pasta de dados raiz Olá é "armazenamento local" para a conta de computação local hello. É a conta do repositório Azure Data Lake toohello equivalente de uma conta da análise Data Lake. Pasta raiz de dados diferentes alternando tooa é como alternar tooa conta de armazenamento diferente. Se você quiser tooaccess normalmente compartilhado dados com pastas raiz de dados diferentes, você deve usar caminhos absolutos em seus scripts. Criar links simbólicos do sistema de arquivo (por exemplo, **mklink** em NTFS) em Olá raiz de dados pasta toopoint toohello dados compartilhados.

pasta de dados raiz Olá é usada para:

- Armazenar metadados, incluindo bancos de dados, tabelas, TVFs (funções com valor de tabela) e assemblies.
- Pesquise hello de entrada e os caminhos de saída que são definidos como caminhos relativos no U-SQL. Usar caminhos relativos torna mais fácil toodeploy seu tooAzure de projetos de U-SQL.

Você pode usar um caminho relativo e um caminho absoluto local em scripts U-SQL. caminho relativo da saudação é relativo toohello caminho da pasta raiz de dados especificado. É recomendável que você use "/" como Olá toomake do separador de caminho seus scripts compatíveis com do lado do servidor de saudação. A seguir, alguns exemplos de caminhos relativos e os respectivos caminhos absolutos equivalentes. Nestes exemplos, C:\LocalRunDataRoot é a pasta raiz de dados de saudação.

|Caminho relativo|Caminho absoluto|
|-------------|-------------|
|/abc/def/input.csv |C:\LocalRunDataRoot\abc\def\input.csv|
|abc/def/input.csv  |C:\LocalRunDataRoot\abc\def\input.csv|
|D:/abc/def/input.csv |D:\abc\def\input.csv|

## <a name="use-local-run-from-visual-studio"></a>Usar execução local no Visual Studio

As Ferramentas do Data Lake para Visual Studio proporcionam experiência de execução local do U-SQL no Visual Studio. Usando esse recurso, você pode:

- Executar um script U-SQL localmente com os assemblies de C#.
- Depurar um assembly de C# localmente.
- Criar, exibir e excluir catálogos do U-SQL (bancos de dados locais, assemblies, esquemas e tabelas) no Gerenciador de servidores. Você também pode encontrar catálogo local Olá também do Gerenciador de servidores.

    ![Catálogo local da execução local das Ferramentas do Data Lake para Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

instalador do Data Lake Tools Olá cria um toobe de pasta C:\LocalRunRoot usado como pasta raiz de dados padrão, Olá. paralelismo de execução local saudação padrão é 1.

### <a name="tooconfigure-local-run-in-visual-studio"></a>tooconfigure local executar no Visual Studio

1. Abra o Visual Studio.
2. Abra o **Gerenciador de Servidores**.
3. Expanda **Azure** > **Data Lake Analytics**.
4. Clique em Olá **Data Lake** menu e clique **opções e configurações**.
5. Na árvore de saudação à esquerda, expanda **Azure Data Lake**e, em seguida, expanda **geral**.

    ![Definir configurações de execução local das Ferramentas do Data Lake para Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

É necessário um projeto U-SQL do Visual Studio para realizar a execução local. Essa parte é diferente de executar scripts U-SQL no Azure.

### <a name="toorun-a-u-sql-script-locally"></a>toorun um U-SQL script localmente
1. No Visual Studio, abra o projeto U-SQL.   
2. Clique com o botão direito do mouse em um script U-SQL no Gerenciador de Soluções e clique em **Enviar Script**.
3. Selecione **(Local)** como hello análise conta toorun seu script localmente.
Você também pode clicar em Olá **(Local)** conta na parte superior de saudação da janela de script e, em seguida, clique em **enviar** (ou usar Olá Ctrl + teclas de atalho F5).

    ![Enviar trabalhos de execução local das Ferramentas do Data Lake para Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a>Depurar scripts e assemblies do C# localmente

Você pode depurar c# assemblies sem enviar e registrando-tooAzure serviço de análise Data Lake. Você pode definir pontos de interrupção em ambos os Olá arquivo code-behind em um projeto c# referenciado.

#### <a name="toodebug-local-code-in-code-behind-file"></a>código de toodebug local no arquivo code-behind

1. Definir pontos de interrupção Olá arquivo code-behind.
2. Pressione o script de saudação de toodebug F5 localmente.

> [!NOTE]
   > Olá seguindo o procedimento só funciona no Visual Studio 2015. No Visual Studio mais antigos talvez seja necessário toomanually adicionar os arquivos pdb hello.  
   >
   >

#### <a name="toodebug-local-code-in-a-referenced-c-project"></a>código de toodebug local em um projeto c# referenciado

1. Criar um projeto c# Assembly e compile toogenerate Olá saída dll.
2. Registre a dll de saudação usando uma instrução U-SQL:

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. Definir pontos de interrupção Olá código c#.
4. Pressione F5 toodebug Olá script referenciando a dll de saudação c# localmente.

## <a name="use-local-run-from-hello-data-lake-u-sql-sdk"></a>Usar local executar da saudação SDK Data Lake U-SQL

Além disso toorunning U-SQL scripts localmente usando o Visual Studio, você pode usar scripts de U-SQL Olá SDK do Azure Data Lake U-SQL toorun localmente com interfaces de programação e de linha de comando. Você pode dimensionar seu teste local U-SQL com eles.

Saiba mais sobre o [SDK do U-SQL do Azure Data Lake](data-lake-analytics-u-sql-sdk.md).


## <a name="next-steps"></a>Próximas etapas

* toosee uma consulta mais complexa, consulte [analisar logs de site usando a análise do Azure Data Lake](data-lake-analytics-analyze-weblogs.md).
* detalhes do trabalho tooview, consulte [navegador de trabalho de uso e a exibição de trabalho de trabalhos da análise Azure Data Lake](data-lake-analytics-data-lake-tools-view-jobs.md).
* exibição de execuções de vértice de saudação toouse, consulte [Olá Use exibição de execuções de vértice no Data Lake Tools para Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).
