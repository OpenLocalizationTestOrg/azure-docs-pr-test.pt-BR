---
title: local aaaScale U-SQL execute e teste com o SDK do SQL Azure Data Lake U | Microsoft Docs
description: "Saiba como trabalhos tooscale U-SQL de SDK do Azure Data Lake U-SQL de toouse locais executar e testam com linha de comando e interfaces de programação na sua estação de trabalho local."
services: data-lake-analytics
documentationcenter: 
author: 
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: yanacai
ms.openlocfilehash: 2b0a16229789268e333f723ff6fc2c3efdc29905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-u-sql-local-run-and-test-with-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="10913-103">Escalar a execução e o teste locais do U-SQL com o SDK do U-SQL do Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="10913-103">Scale U-SQL local run and test with Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="10913-104">Ao desenvolver o script U-SQL, é comum toorun e teste U-SQL script localmente antes de enviar-toocloud.</span><span class="sxs-lookup"><span data-stu-id="10913-104">When developing U-SQL script, it is common toorun and test U-SQL script locally before submit it toocloud.</span></span> <span data-ttu-id="10913-105">O Azure Data Lake fornece um pacote NuGet chamado SDK do U-SQL do Azure Data Lake para este cenário, por meio do qual é possível escalar a execução e o teste locais do U-SQL com facilidade.</span><span class="sxs-lookup"><span data-stu-id="10913-105">Azure Data Lake provides a Nuget package called Azure Data Lake U-SQL SDK for this scenario, through which you can easily scale U-SQL local run and test.</span></span> <span data-ttu-id="10913-106">Também é possível toointegrate este U-SQL de teste com a compilação de saudação do CI (integração contínua) sistema tooautomate e teste.</span><span class="sxs-lookup"><span data-stu-id="10913-106">It is also possible toointegrate this U-SQL test with CI (Continuous Integration) system tooautomate hello compile and test.</span></span>

<span data-ttu-id="10913-107">Se você se preocupa como toomanually local executar e depurar o script U-SQL com ferramentas de interface gráfica do usuário, em seguida, você pode usar o Azure Data Lake Tools para Visual Studio para que.</span><span class="sxs-lookup"><span data-stu-id="10913-107">If you care about how toomanually local run and debug U-SQL script with GUI tooling, then you can use Azure Data Lake Tools for Visual Studio for that.</span></span> <span data-ttu-id="10913-108">Saiba mais [aqui](data-lake-analytics-data-lake-tools-local-run.md).</span><span class="sxs-lookup"><span data-stu-id="10913-108">You can learn more from [here](data-lake-analytics-data-lake-tools-local-run.md).</span></span>

## <a name="install-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="10913-109">Instalar o SDK do U-SQL do Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="10913-109">Install Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="10913-110">Você pode obter o SDK do Azure Data Lake U-SQL de saudação [aqui](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) em Nuget.org. E antes de usá-lo, você precisa toomake-se de que ter dependências da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="10913-110">You can get hello Azure Data Lake U-SQL SDK [here](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) on Nuget.org. And before using it, you need toomake sure you have dependencies as follows.</span></span>

### <a name="dependencies"></a><span data-ttu-id="10913-111">Dependências</span><span class="sxs-lookup"><span data-stu-id="10913-111">Dependencies</span></span>

<span data-ttu-id="10913-112">Olá Data Lake U-SQL SDK requer Olá dependências a seguir:</span><span class="sxs-lookup"><span data-stu-id="10913-112">hello Data Lake U-SQL SDK requires hello following dependencies:</span></span>

- <span data-ttu-id="10913-113">[Microsoft .NET Framework 4.6 ou mais recente](https://www.microsoft.com/download/details.aspx?id=17851).</span><span class="sxs-lookup"><span data-stu-id="10913-113">[Microsoft .NET Framework 4.6 or newer](https://www.microsoft.com/download/details.aspx?id=17851).</span></span>
- <span data-ttu-id="10913-114">Microsoft Visual C++ 14 e SDK do Windows 10.0.10240.0 ou mais novo (que é chamado CppSDK neste artigo).</span><span class="sxs-lookup"><span data-stu-id="10913-114">Microsoft Visual C++ 14 and Windows SDK 10.0.10240.0 or newer (which is called CppSDK in this article).</span></span> <span data-ttu-id="10913-115">Há duas maneiras tooget CppSDK:</span><span class="sxs-lookup"><span data-stu-id="10913-115">There are two ways tooget CppSDK:</span></span>

    - <span data-ttu-id="10913-116">Instalar o [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span><span class="sxs-lookup"><span data-stu-id="10913-116">Install [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span></span> <span data-ttu-id="10913-117">Você terá uma pasta \Windows Kits\10 na pasta de arquivos de programa do hello – por exemplo, C:\Program Files (x86) \Windows Kits\10\.</span><span class="sxs-lookup"><span data-stu-id="10913-117">You'll have a \Windows Kits\10 folder under hello Program Files folder--for example, C:\Program Files (x86)\Windows Kits\10\.</span></span> <span data-ttu-id="10913-118">Você também encontrará a versão do SDK do Windows 10 Olá em \Windows Kits\10\Lib.</span><span class="sxs-lookup"><span data-stu-id="10913-118">You'll also find hello Windows 10 SDK version under \Windows Kits\10\Lib.</span></span> <span data-ttu-id="10913-119">Se você não vir essas pastas, reinstalar o Visual Studio e se tooselect Olá SDK do Windows 10 durante a instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="10913-119">If you don’t see these folders, reinstall Visual Studio and be sure tooselect hello Windows 10 SDK during hello installation.</span></span> <span data-ttu-id="10913-120">Se você tiver instalado com o Visual Studio, compilador local do hello U-SQL encontrará automaticamente.</span><span class="sxs-lookup"><span data-stu-id="10913-120">If you have this installed with Visual Studio, hello U-SQL local compiler will find it automatically.</span></span>

    ![SDK para Windows 10 da execução local das Ferramentas do Data Lake para Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - <span data-ttu-id="10913-122">Instalar [Ferramentas do Data Lake para Visual Studio](http://aka.ms/adltoolsvs).</span><span class="sxs-lookup"><span data-stu-id="10913-122">Install [Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="10913-123">Você pode encontrar hello predefinida de arquivos do Visual C++ e o SDK do Windows em C:\Program Files (x86) \Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span><span class="sxs-lookup"><span data-stu-id="10913-123">You can find hello prepackaged Visual C++ and Windows SDK files at C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span></span> <span data-ttu-id="10913-124">Nesse caso, compilador local do hello U-SQL não é possível localizar as dependências de saudação automaticamente.</span><span class="sxs-lookup"><span data-stu-id="10913-124">In this case, hello U-SQL local compiler cannot find hello dependencies automatically.</span></span> <span data-ttu-id="10913-125">Você precisa de caminho de CppSDK de saudação toospecify para ele.</span><span class="sxs-lookup"><span data-stu-id="10913-125">You need toospecify hello CppSDK path for it.</span></span> <span data-ttu-id="10913-126">Você pode copiar Olá arquivos tooanother local ou usá-la como está.</span><span class="sxs-lookup"><span data-stu-id="10913-126">You can either copy hello files tooanother location or use it as is.</span></span>

## <a name="understand-basic-concepts"></a><span data-ttu-id="10913-127">Entender os conceitos básicos</span><span class="sxs-lookup"><span data-stu-id="10913-127">Understand basic concepts</span></span>

### <a name="data-root"></a><span data-ttu-id="10913-128">Raiz de dados</span><span class="sxs-lookup"><span data-stu-id="10913-128">Data root</span></span>

<span data-ttu-id="10913-129">pasta de dados raiz Olá é "armazenamento local" para a conta de computação local hello.</span><span class="sxs-lookup"><span data-stu-id="10913-129">hello data-root folder is a "local store" for hello local compute account.</span></span> <span data-ttu-id="10913-130">É a conta do repositório Azure Data Lake toohello equivalente de uma conta da análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="10913-130">It's equivalent toohello Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="10913-131">Pasta raiz de dados diferentes alternando tooa é como alternar tooa conta de armazenamento diferente.</span><span class="sxs-lookup"><span data-stu-id="10913-131">Switching tooa different data-root folder is just like switching tooa different store account.</span></span> <span data-ttu-id="10913-132">Se você quiser tooaccess normalmente compartilhado dados com pastas raiz de dados diferentes, você deve usar caminhos absolutos em seus scripts.</span><span class="sxs-lookup"><span data-stu-id="10913-132">If you want tooaccess commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="10913-133">Criar links simbólicos do sistema de arquivo (por exemplo, **mklink** em NTFS) em Olá raiz de dados pasta toopoint toohello dados compartilhados.</span><span class="sxs-lookup"><span data-stu-id="10913-133">Or, create file system symbolic links (for example, **mklink** on NTFS) under hello data-root folder toopoint toohello shared data.</span></span>

<span data-ttu-id="10913-134">pasta de dados raiz Olá é usada para:</span><span class="sxs-lookup"><span data-stu-id="10913-134">hello data-root folder is used to:</span></span>

- <span data-ttu-id="10913-135">Armazenar metadados locais, incluindo bancos de dados, tabelas, TVFs (funções com valor de tabela) e assemblies.</span><span class="sxs-lookup"><span data-stu-id="10913-135">Store local metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="10913-136">Pesquise hello de entrada e os caminhos de saída que são definidos como caminhos relativos no U-SQL.</span><span class="sxs-lookup"><span data-stu-id="10913-136">Look up hello input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="10913-137">Usar caminhos relativos torna mais fácil toodeploy seu tooAzure de projetos de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="10913-137">Using relative paths makes it easier toodeploy your U-SQL projects tooAzure.</span></span>

### <a name="file-path-in-u-sql"></a><span data-ttu-id="10913-138">Caminho de arquivo no U-SQL</span><span class="sxs-lookup"><span data-stu-id="10913-138">File path in U-SQL</span></span>

<span data-ttu-id="10913-139">Você pode usar um caminho relativo e um caminho absoluto local em scripts U-SQL.</span><span class="sxs-lookup"><span data-stu-id="10913-139">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="10913-140">caminho relativo da saudação é relativo toohello caminho da pasta raiz de dados especificado.</span><span class="sxs-lookup"><span data-stu-id="10913-140">hello relative path is relative toohello specified data-root folder path.</span></span> <span data-ttu-id="10913-141">É recomendável que você use "/" como Olá toomake do separador de caminho seus scripts compatíveis com do lado do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="10913-141">We recommend that you use "/" as hello path separator toomake your scripts compatible with hello server side.</span></span> <span data-ttu-id="10913-142">A seguir, alguns exemplos de caminhos relativos e os respectivos caminhos absolutos equivalentes.</span><span class="sxs-lookup"><span data-stu-id="10913-142">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="10913-143">Nestes exemplos, C:\LocalRunDataRoot é a pasta raiz de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="10913-143">In these examples, C:\LocalRunDataRoot is hello data-root folder.</span></span>

|<span data-ttu-id="10913-144">Caminho relativo</span><span class="sxs-lookup"><span data-stu-id="10913-144">Relative path</span></span>|<span data-ttu-id="10913-145">Caminho absoluto</span><span class="sxs-lookup"><span data-stu-id="10913-145">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="10913-146">/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="10913-146">/abc/def/input.csv</span></span> |<span data-ttu-id="10913-147">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="10913-147">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="10913-148">abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="10913-148">abc/def/input.csv</span></span>  |<span data-ttu-id="10913-149">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="10913-149">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="10913-150">D:/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="10913-150">D:/abc/def/input.csv</span></span> |<span data-ttu-id="10913-151">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="10913-151">D:\abc\def\input.csv</span></span>|

### <a name="working-directory"></a><span data-ttu-id="10913-152">Diretório de trabalho</span><span class="sxs-lookup"><span data-stu-id="10913-152">Working directory</span></span>

<span data-ttu-id="10913-153">Ao executar o script hello U-SQL localmente, um diretório de trabalho é criado durante a compilação em diretório de execução atual.</span><span class="sxs-lookup"><span data-stu-id="10913-153">When running hello U-SQL script locally, a working directory is created during compilation under current running directory.</span></span> <span data-ttu-id="10913-154">Além disso saídas de compilação toohello hello necessários arquivos de tempo de execução para execução local será diretório de trabalho toothis copiado de sombra.</span><span class="sxs-lookup"><span data-stu-id="10913-154">In addition toohello compilation outputs, hello needed runtime files for local execution will be shadow copied toothis working directory.</span></span> <span data-ttu-id="10913-155">saudação de pasta de raiz do diretório de trabalho é chamada de "ScopeWorkDir" e arquivos Olá Olá diretório de trabalho são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="10913-155">hello working directory root folder is called "ScopeWorkDir" and hello files under hello working directory are as follows:</span></span>

|<span data-ttu-id="10913-156">Diretório/arquivo</span><span class="sxs-lookup"><span data-stu-id="10913-156">Directory/file</span></span>|<span data-ttu-id="10913-157">Diretório/arquivo</span><span class="sxs-lookup"><span data-stu-id="10913-157">Directory/file</span></span>|<span data-ttu-id="10913-158">Diretório/arquivo</span><span class="sxs-lookup"><span data-stu-id="10913-158">Directory/file</span></span>|<span data-ttu-id="10913-159">Definição</span><span class="sxs-lookup"><span data-stu-id="10913-159">Definition</span></span>|<span data-ttu-id="10913-160">Descrição</span><span class="sxs-lookup"><span data-stu-id="10913-160">Description</span></span>|
|--------------|--------------|--------------|----------|-----------|
|<span data-ttu-id="10913-161">C6A101DDCB470506</span><span class="sxs-lookup"><span data-stu-id="10913-161">C6A101DDCB470506</span></span>| | |<span data-ttu-id="10913-162">Cadeia de caracteres de hash da versão do tempo de execução</span><span class="sxs-lookup"><span data-stu-id="10913-162">Hash string of runtime version</span></span>|<span data-ttu-id="10913-163">Cópia de sombra dos arquivos de tempo de execução necessários para execução local</span><span class="sxs-lookup"><span data-stu-id="10913-163">Shadow copy of runtime files needed for local execution</span></span>|
| |<span data-ttu-id="10913-164">Script_66AE4909AA0ED06C</span><span class="sxs-lookup"><span data-stu-id="10913-164">Script_66AE4909AA0ED06C</span></span>| |<span data-ttu-id="10913-165">Nome do script + cadeia de caracteres de hash do caminho do script</span><span class="sxs-lookup"><span data-stu-id="10913-165">Script name + hash string of script path</span></span>|<span data-ttu-id="10913-166">Saídas da compilação e log das etapas de execução</span><span class="sxs-lookup"><span data-stu-id="10913-166">Compilation outputs and execution step logging</span></span>|
| | |<span data-ttu-id="10913-167">\_script\_.abr</span><span class="sxs-lookup"><span data-stu-id="10913-167">\_script\_.abr</span></span>|<span data-ttu-id="10913-168">Saída do compilador</span><span class="sxs-lookup"><span data-stu-id="10913-168">Compiler output</span></span>|<span data-ttu-id="10913-169">Arquivo de álgebra</span><span class="sxs-lookup"><span data-stu-id="10913-169">Algebra file</span></span>|
| | |<span data-ttu-id="10913-170">\_ScopeCodeGen\_.*</span><span class="sxs-lookup"><span data-stu-id="10913-170">\_ScopeCodeGen\_.*</span></span>|<span data-ttu-id="10913-171">Saída do compilador</span><span class="sxs-lookup"><span data-stu-id="10913-171">Compiler output</span></span>|<span data-ttu-id="10913-172">Código gerenciado gerado</span><span class="sxs-lookup"><span data-stu-id="10913-172">Generated managed code</span></span>|
| | |<span data-ttu-id="10913-173">\_ScopeCodeGenEngine\_.*</span><span class="sxs-lookup"><span data-stu-id="10913-173">\_ScopeCodeGenEngine\_.*</span></span>|<span data-ttu-id="10913-174">Saída do compilador</span><span class="sxs-lookup"><span data-stu-id="10913-174">Compiler output</span></span>|<span data-ttu-id="10913-175">Código nativo gerado</span><span class="sxs-lookup"><span data-stu-id="10913-175">Generated native code</span></span>|
| | |<span data-ttu-id="10913-176">assemblies referenciados</span><span class="sxs-lookup"><span data-stu-id="10913-176">referenced assemblies</span></span>|<span data-ttu-id="10913-177">Referência de assembly</span><span class="sxs-lookup"><span data-stu-id="10913-177">Assembly reference</span></span>|<span data-ttu-id="10913-178">Arquivos de assembly referenciado</span><span class="sxs-lookup"><span data-stu-id="10913-178">Referenced assembly files</span></span>|
| | |<span data-ttu-id="10913-179">deployed_resources</span><span class="sxs-lookup"><span data-stu-id="10913-179">deployed_resources</span></span>|<span data-ttu-id="10913-180">Implantação de recursos</span><span class="sxs-lookup"><span data-stu-id="10913-180">Resource deployment</span></span>|<span data-ttu-id="10913-181">Arquivos da implantação de recursos</span><span class="sxs-lookup"><span data-stu-id="10913-181">Resource deployment files</span></span>|
| | |<span data-ttu-id="10913-182">xxxxxxxx.xxx[1..n]\_\*.*</span><span class="sxs-lookup"><span data-stu-id="10913-182">xxxxxxxx.xxx[1..n]\_\*.*</span></span>|<span data-ttu-id="10913-183">Log de execução</span><span class="sxs-lookup"><span data-stu-id="10913-183">Execution log</span></span>|<span data-ttu-id="10913-184">Log das etapas de execução</span><span class="sxs-lookup"><span data-stu-id="10913-184">Log of execution steps</span></span>|


## <a name="use-hello-sdk-from-hello-command-line"></a><span data-ttu-id="10913-185">Use Olá SDK da linha de comando Olá</span><span class="sxs-lookup"><span data-stu-id="10913-185">Use hello SDK from hello command line</span></span>

### <a name="command-line-interface-of-hello-helper-application"></a><span data-ttu-id="10913-186">Interface de linha de comando do aplicativo de auxiliar hello</span><span class="sxs-lookup"><span data-stu-id="10913-186">Command-line interface of hello helper application</span></span>

<span data-ttu-id="10913-187">No SDK directory\build\runtime, LocalRunHelper.exe é aplicativo de linha de comando auxiliar hello que fornece interfaces funções toomost de saudação usada execução local.</span><span class="sxs-lookup"><span data-stu-id="10913-187">Under SDK directory\build\runtime, LocalRunHelper.exe is hello command-line helper application that provides interfaces toomost of hello commonly used local-run functions.</span></span> <span data-ttu-id="10913-188">Observe que ambos Olá comando e opções de argumento Olá diferenciam maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="10913-188">Note that both hello command and hello argument switches are case-sensitive.</span></span> <span data-ttu-id="10913-189">tooinvoke-lo:</span><span class="sxs-lookup"><span data-stu-id="10913-189">tooinvoke it:</span></span>

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

<span data-ttu-id="10913-190">Execute LocalRunHelper.exe sem argumentos ou com hello **ajuda** alternar tooshow informações de ajuda de saudação:</span><span class="sxs-lookup"><span data-stu-id="10913-190">Run LocalRunHelper.exe without arguments or with hello **help** switch tooshow hello help information:</span></span>

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile hello script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

<span data-ttu-id="10913-191">Informações de Ajuda no hello:</span><span class="sxs-lookup"><span data-stu-id="10913-191">In hello help information:</span></span>

-  <span data-ttu-id="10913-192">**Comando** fornece Olá nome do comando.</span><span class="sxs-lookup"><span data-stu-id="10913-192">**Command** gives hello command’s name.</span></span>  
-  <span data-ttu-id="10913-193">**Required Argument** lista argumentos que devem ser fornecidos.</span><span class="sxs-lookup"><span data-stu-id="10913-193">**Required Argument** lists arguments that must be supplied.</span></span>  
-  <span data-ttu-id="10913-194">**Optional Argument** lista argumentos que são opcionais e com valores padrão.</span><span class="sxs-lookup"><span data-stu-id="10913-194">**Optional Argument** lists arguments that are optional, with default values.</span></span>  <span data-ttu-id="10913-195">Argumentos opcionais de boolianos não tem parâmetros e suas aparências significam o valor padrão de tootheir negativo.</span><span class="sxs-lookup"><span data-stu-id="10913-195">Optional Boolean arguments don’t have parameters, and their appearances mean negative tootheir default value.</span></span>

### <a name="return-value-and-logging"></a><span data-ttu-id="10913-196">Valor de retorno e registro em log</span><span class="sxs-lookup"><span data-stu-id="10913-196">Return value and logging</span></span>

<span data-ttu-id="10913-197">aplicativo de auxiliar Hello retorna **0** para êxito e **-1** falha.</span><span class="sxs-lookup"><span data-stu-id="10913-197">hello helper application returns **0** for success and **-1** for failure.</span></span> <span data-ttu-id="10913-198">Por padrão, o auxiliar de saudação envia todas as console atual toohello de mensagens.</span><span class="sxs-lookup"><span data-stu-id="10913-198">By default, hello helper sends all messages toohello current console.</span></span> <span data-ttu-id="10913-199">No entanto, a maioria dos comandos de saudação suporte Olá **- MessageOut caminho_para_arquivo_log** argumento opcional que redireciona hello gera o arquivo de log tooa.</span><span class="sxs-lookup"><span data-stu-id="10913-199">However, most of hello commands support hello **-MessageOut path_to_log_file** optional argument that redirects hello outputs tooa log file.</span></span>

### <a name="environment-variable-configuring"></a><span data-ttu-id="10913-200">Configurando variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="10913-200">Environment variable configuring</span></span>

<span data-ttu-id="10913-201">A execução local do U-SQL precisa de uma raiz de dados especificada como a conta de armazenamento local, bem como um caminho do CppSDK especificado para as dependências.</span><span class="sxs-lookup"><span data-stu-id="10913-201">U-SQL local run needs a specified data root as local storage account, as well as a specified CppSDK path for dependencies.</span></span> <span data-ttu-id="10913-202">Você pode ambos os argumento de conjunto de saudação na variável de ambiente de linha de comando ou definidas para eles.</span><span class="sxs-lookup"><span data-stu-id="10913-202">You can both set hello argument in command-line or set environment variable for them.</span></span>

- <span data-ttu-id="10913-203">Saudação de conjunto **SCOPE_CPP_SDK** variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="10913-203">Set hello **SCOPE_CPP_SDK** environment variable.</span></span>

    <span data-ttu-id="10913-204">Se você obtiver o Microsoft Visual C++ e hello SDK do Windows ao instalar o Data Lake Tools para Visual Studio, verifique se Olá pasta a seguir:</span><span class="sxs-lookup"><span data-stu-id="10913-204">If you get Microsoft Visual C++ and hello Windows SDK by installing Data Lake Tools for Visual Studio, verify that you have hello following folder:</span></span>

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    <span data-ttu-id="10913-205">Definir uma nova variável de ambiente chamada **SCOPE_CPP_SDK** toopoint toothis directory.</span><span class="sxs-lookup"><span data-stu-id="10913-205">Define a new environment variable called **SCOPE_CPP_SDK** toopoint toothis directory.</span></span> <span data-ttu-id="10913-206">Ou copie Olá pasta toohello outro local e especificar **SCOPE_CPP_SDK** que.</span><span class="sxs-lookup"><span data-stu-id="10913-206">Or copy hello folder toohello other location and specify **SCOPE_CPP_SDK** as that.</span></span>

    <span data-ttu-id="10913-207">Variável de ambiente do adição toosetting hello, você pode especificar Olá **- CppSDK** argumento quando você estiver usando a linha de comando hello.</span><span class="sxs-lookup"><span data-stu-id="10913-207">In addition toosetting hello environment variable, you can specify hello **-CppSDK** argument when you're using hello command line.</span></span> <span data-ttu-id="10913-208">Esse argumento substitui a variável de ambiente CppSDK padrão.</span><span class="sxs-lookup"><span data-stu-id="10913-208">This argument overwrites your default CppSDK environment variable.</span></span>

- <span data-ttu-id="10913-209">Saudação de conjunto **LOCALRUN_DATAROOT** variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="10913-209">Set hello **LOCALRUN_DATAROOT** environment variable.</span></span>

    <span data-ttu-id="10913-210">Definir uma nova variável de ambiente chamada **LOCALRUN_DATAROOT** que aponte toohello raiz de dados.</span><span class="sxs-lookup"><span data-stu-id="10913-210">Define a new environment variable called **LOCALRUN_DATAROOT** that points toohello data root.</span></span>

    <span data-ttu-id="10913-211">Variável de ambiente do adição toosetting hello, você pode especificar Olá **- DataRoot** argumento com caminho de dados raiz hello quando você estiver usando uma linha de comando.</span><span class="sxs-lookup"><span data-stu-id="10913-211">In addition toosetting hello environment variable, you can specify hello **-DataRoot** argument with hello data-root path when you're using a command line.</span></span> <span data-ttu-id="10913-212">Esse argumento substitui a variável de ambiente de raiz de dados padrão.</span><span class="sxs-lookup"><span data-stu-id="10913-212">This argument overwrites your default data-root environment variable.</span></span> <span data-ttu-id="10913-213">É necessário tooadd essa linha de comando tooevery argumento que estiver em execução para que você pode substituir uma variável de ambiente de dados raiz saudação padrão para todas as operações.</span><span class="sxs-lookup"><span data-stu-id="10913-213">You need tooadd this argument tooevery command line you're running so that you can overwrite hello default data-root environment variable for all operations.</span></span>

### <a name="sdk-command-line-usage-samples"></a><span data-ttu-id="10913-214">Amostras de uso da linha de comando do SDK</span><span class="sxs-lookup"><span data-stu-id="10913-214">SDK command line usage samples</span></span>

#### <a name="compile-and-run"></a><span data-ttu-id="10913-215">Compilar e executar</span><span class="sxs-lookup"><span data-stu-id="10913-215">Compile and run</span></span>

<span data-ttu-id="10913-216">Olá **execute** comando é usado toocompile Olá script e, em seguida, executar resultados compilados.</span><span class="sxs-lookup"><span data-stu-id="10913-216">hello **run** command is used toocompile hello script and then execute compiled results.</span></span> <span data-ttu-id="10913-217">Seus argumentos de linha de comando são uma combinação dos argumentos de **compile** e **execute**.</span><span class="sxs-lookup"><span data-stu-id="10913-217">Its command-line arguments are a combination of those from **compile** and **execute**.</span></span>

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="10913-218">Olá, a seguir é argumentos opcionais para **executar**:</span><span class="sxs-lookup"><span data-stu-id="10913-218">hello following are optional arguments for **run**:</span></span>


|<span data-ttu-id="10913-219">Argumento</span><span class="sxs-lookup"><span data-stu-id="10913-219">Argument</span></span>|<span data-ttu-id="10913-220">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="10913-220">Default value</span></span>|<span data-ttu-id="10913-221">Descrição</span><span class="sxs-lookup"><span data-stu-id="10913-221">Description</span></span>|
|--------|-------------|-----------|
|<span data-ttu-id="10913-222">-CodeBehind</span><span class="sxs-lookup"><span data-stu-id="10913-222">-CodeBehind</span></span>|<span data-ttu-id="10913-223">Falso</span><span class="sxs-lookup"><span data-stu-id="10913-223">False</span></span>|<span data-ttu-id="10913-224">script Hello possui código. cs</span><span class="sxs-lookup"><span data-stu-id="10913-224">hello script has .cs code behind</span></span>|
|<span data-ttu-id="10913-225">-CppSDK</span><span class="sxs-lookup"><span data-stu-id="10913-225">-CppSDK</span></span>| |<span data-ttu-id="10913-226">Diretório do CppSDK</span><span class="sxs-lookup"><span data-stu-id="10913-226">CppSDK Directory</span></span>|
|<span data-ttu-id="10913-227">-DataRoot</span><span class="sxs-lookup"><span data-stu-id="10913-227">-DataRoot</span></span>| <span data-ttu-id="10913-228">Variável de ambiente DataRoot</span><span class="sxs-lookup"><span data-stu-id="10913-228">DataRoot environment variable</span></span>|<span data-ttu-id="10913-229">DataRoot para execução local, padrão muito variável de ambiente 'LOCALRUN_DATAROOT'</span><span class="sxs-lookup"><span data-stu-id="10913-229">DataRoot for local run, default too'LOCALRUN_DATAROOT' environment variable</span></span>|
|<span data-ttu-id="10913-230">-MessageOut</span><span class="sxs-lookup"><span data-stu-id="10913-230">-MessageOut</span></span>| |<span data-ttu-id="10913-231">Mensagens de despejo no arquivo tooa do console</span><span class="sxs-lookup"><span data-stu-id="10913-231">Dump messages on console tooa file</span></span>|
|<span data-ttu-id="10913-232">-Parallel</span><span class="sxs-lookup"><span data-stu-id="10913-232">-Parallel</span></span>|<span data-ttu-id="10913-233">1</span><span class="sxs-lookup"><span data-stu-id="10913-233">1</span></span>|<span data-ttu-id="10913-234">Executar Olá plano com hello especificado paralelismo</span><span class="sxs-lookup"><span data-stu-id="10913-234">Run hello plan with hello specified parallelism</span></span>|
|<span data-ttu-id="10913-235">-References</span><span class="sxs-lookup"><span data-stu-id="10913-235">-References</span></span>| |<span data-ttu-id="10913-236">Lista de assemblies de referência tooextra caminhos ou arquivos de dados de code-behind, separada por ';'</span><span class="sxs-lookup"><span data-stu-id="10913-236">List of paths tooextra reference assemblies or data files of code behind, separated by ';'</span></span>|
|<span data-ttu-id="10913-237">-UdoRedirect</span><span class="sxs-lookup"><span data-stu-id="10913-237">-UdoRedirect</span></span>|<span data-ttu-id="10913-238">Falso</span><span class="sxs-lookup"><span data-stu-id="10913-238">False</span></span>|<span data-ttu-id="10913-239">Gerar configuração de redirecionamento de assembly UDO</span><span class="sxs-lookup"><span data-stu-id="10913-239">Generate Udo assembly redirect config</span></span>|
|<span data-ttu-id="10913-240">-UseDatabase</span><span class="sxs-lookup"><span data-stu-id="10913-240">-UseDatabase</span></span>|<span data-ttu-id="10913-241">mestre</span><span class="sxs-lookup"><span data-stu-id="10913-241">master</span></span>|<span data-ttu-id="10913-242">Toouse de banco de dados para o código por trás de registro de assembly temporário</span><span class="sxs-lookup"><span data-stu-id="10913-242">Database toouse for code behind temporary assembly registration</span></span>|
|<span data-ttu-id="10913-243">-Verbose</span><span class="sxs-lookup"><span data-stu-id="10913-243">-Verbose</span></span>|<span data-ttu-id="10913-244">Falso</span><span class="sxs-lookup"><span data-stu-id="10913-244">False</span></span>|<span data-ttu-id="10913-245">Mostrar saídas detalhadas do tempo de execução</span><span class="sxs-lookup"><span data-stu-id="10913-245">Show detailed outputs from runtime</span></span>|
|<span data-ttu-id="10913-246">-WorkDir</span><span class="sxs-lookup"><span data-stu-id="10913-246">-WorkDir</span></span>|<span data-ttu-id="10913-247">Diretório atual</span><span class="sxs-lookup"><span data-stu-id="10913-247">Current Directory</span></span>|<span data-ttu-id="10913-248">Diretório para uso do compilador e saídas</span><span class="sxs-lookup"><span data-stu-id="10913-248">Directory for compiler usage and outputs</span></span>|
|<span data-ttu-id="10913-249">-RunScopeCEP</span><span class="sxs-lookup"><span data-stu-id="10913-249">-RunScopeCEP</span></span>|<span data-ttu-id="10913-250">0</span><span class="sxs-lookup"><span data-stu-id="10913-250">0</span></span>|<span data-ttu-id="10913-251">ScopeCEP modo toouse</span><span class="sxs-lookup"><span data-stu-id="10913-251">ScopeCEP mode toouse</span></span>|
|<span data-ttu-id="10913-252">-ScopeCEPTempPath</span><span class="sxs-lookup"><span data-stu-id="10913-252">-ScopeCEPTempPath</span></span>|<span data-ttu-id="10913-253">temp</span><span class="sxs-lookup"><span data-stu-id="10913-253">temp</span></span>|<span data-ttu-id="10913-254">Toouse caminho temporário para o fluxo de dados</span><span class="sxs-lookup"><span data-stu-id="10913-254">Temp path toouse for streaming data</span></span>|
|<span data-ttu-id="10913-255">-OptFlags</span><span class="sxs-lookup"><span data-stu-id="10913-255">-OptFlags</span></span>| |<span data-ttu-id="10913-256">Lista separada por vírgula de sinalizadores do otimizador</span><span class="sxs-lookup"><span data-stu-id="10913-256">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="10913-257">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="10913-257">Here's an example:</span></span>

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

<span data-ttu-id="10913-258">Além de combinar **compilar** e **executar**, você pode compilar e executar executáveis Olá compilado separadamente.</span><span class="sxs-lookup"><span data-stu-id="10913-258">Besides combining **compile** and **execute**, you can compile and execute hello compiled executables separately.</span></span>

#### <a name="compile-a-u-sql-script"></a><span data-ttu-id="10913-259">Compilar um script U-SQL</span><span class="sxs-lookup"><span data-stu-id="10913-259">Compile a U-SQL script</span></span>

<span data-ttu-id="10913-260">Olá **compilar** comando é usado toocompile um U-SQL script tooexecutables.</span><span class="sxs-lookup"><span data-stu-id="10913-260">hello **compile** command is used toocompile a U-SQL script tooexecutables.</span></span>

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="10913-261">Olá, a seguir é argumentos opcionais para **compilar**:</span><span class="sxs-lookup"><span data-stu-id="10913-261">hello following are optional arguments for **compile**:</span></span>


|<span data-ttu-id="10913-262">Argumento</span><span class="sxs-lookup"><span data-stu-id="10913-262">Argument</span></span>|<span data-ttu-id="10913-263">Descrição</span><span class="sxs-lookup"><span data-stu-id="10913-263">Description</span></span>|
|--------|-----------|
| <span data-ttu-id="10913-264">-CodeBehind [valor padrão 'False']</span><span class="sxs-lookup"><span data-stu-id="10913-264">-CodeBehind [default value 'False']</span></span>|<span data-ttu-id="10913-265">script Hello possui código. cs</span><span class="sxs-lookup"><span data-stu-id="10913-265">hello script has .cs code behind</span></span>|
| <span data-ttu-id="10913-266">-CppSDK [valor padrão '']</span><span class="sxs-lookup"><span data-stu-id="10913-266">-CppSDK [default value '']</span></span>|<span data-ttu-id="10913-267">Diretório do CppSDK</span><span class="sxs-lookup"><span data-stu-id="10913-267">CppSDK Directory</span></span>|
| <span data-ttu-id="10913-268">-DataRoot [valor padrão “variável de ambiente DataRoot”]</span><span class="sxs-lookup"><span data-stu-id="10913-268">-DataRoot [default value 'DataRoot environment variable']</span></span>|<span data-ttu-id="10913-269">DataRoot para execução local, padrão muito variável de ambiente 'LOCALRUN_DATAROOT'</span><span class="sxs-lookup"><span data-stu-id="10913-269">DataRoot for local run, default too'LOCALRUN_DATAROOT' environment variable</span></span>|
| <span data-ttu-id="10913-270">-MessageOut [valor padrão '']</span><span class="sxs-lookup"><span data-stu-id="10913-270">-MessageOut [default value '']</span></span>|<span data-ttu-id="10913-271">Mensagens de despejo no arquivo tooa do console</span><span class="sxs-lookup"><span data-stu-id="10913-271">Dump messages on console tooa file</span></span>|
| <span data-ttu-id="10913-272">-References [valor padrão '']</span><span class="sxs-lookup"><span data-stu-id="10913-272">-References [default value '']</span></span>|<span data-ttu-id="10913-273">Lista de assemblies de referência tooextra caminhos ou arquivos de dados de code-behind, separada por ';'</span><span class="sxs-lookup"><span data-stu-id="10913-273">List of paths tooextra reference assemblies or data files of code behind, separated by ';'</span></span>|
| <span data-ttu-id="10913-274">-Shallow [valor padrão 'False']</span><span class="sxs-lookup"><span data-stu-id="10913-274">-Shallow [default value 'False']</span></span>|<span data-ttu-id="10913-275">Compilação superficial</span><span class="sxs-lookup"><span data-stu-id="10913-275">Shallow compile</span></span>|
| <span data-ttu-id="10913-276">-UdoRedirect [valor padrão 'False']</span><span class="sxs-lookup"><span data-stu-id="10913-276">-UdoRedirect [default value 'False']</span></span>|<span data-ttu-id="10913-277">Gerar configuração de redirecionamento de assembly UDO</span><span class="sxs-lookup"><span data-stu-id="10913-277">Generate Udo assembly redirect config</span></span>|
| <span data-ttu-id="10913-278">-UseDatabase [valor padrão 'master']</span><span class="sxs-lookup"><span data-stu-id="10913-278">-UseDatabase [default value 'master']</span></span>|<span data-ttu-id="10913-279">Toouse de banco de dados para o código por trás de registro de assembly temporário</span><span class="sxs-lookup"><span data-stu-id="10913-279">Database toouse for code behind temporary assembly registration</span></span>|
| <span data-ttu-id="10913-280">-WorkDir [valor padrão “Diretório Atual”]</span><span class="sxs-lookup"><span data-stu-id="10913-280">-WorkDir [default value 'Current Directory']</span></span>|<span data-ttu-id="10913-281">Diretório para uso do compilador e saídas</span><span class="sxs-lookup"><span data-stu-id="10913-281">Directory for compiler usage and outputs</span></span>|
| <span data-ttu-id="10913-282">-RunScopeCEP [valor padrão “0”]</span><span class="sxs-lookup"><span data-stu-id="10913-282">-RunScopeCEP [default value '0']</span></span>|<span data-ttu-id="10913-283">ScopeCEP modo toouse</span><span class="sxs-lookup"><span data-stu-id="10913-283">ScopeCEP mode toouse</span></span>|
| <span data-ttu-id="10913-284">-ScopeCEPTempPath [valor padrão “temp”]</span><span class="sxs-lookup"><span data-stu-id="10913-284">-ScopeCEPTempPath [default value 'temp']</span></span>|<span data-ttu-id="10913-285">Toouse caminho temporário para o fluxo de dados</span><span class="sxs-lookup"><span data-stu-id="10913-285">Temp path toouse for streaming data</span></span>|
| <span data-ttu-id="10913-286">-OptFlags [valor padrão '']</span><span class="sxs-lookup"><span data-stu-id="10913-286">-OptFlags [default value '']</span></span>|<span data-ttu-id="10913-287">Lista separada por vírgula de sinalizadores do otimizador</span><span class="sxs-lookup"><span data-stu-id="10913-287">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="10913-288">Veja alguns exemplos de uso.</span><span class="sxs-lookup"><span data-stu-id="10913-288">Here are some usage examples.</span></span>

<span data-ttu-id="10913-289">Compilar um script U-SQL:</span><span class="sxs-lookup"><span data-stu-id="10913-289">Compile a U-SQL script:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql

<span data-ttu-id="10913-290">Compilar um script U-SQL e defina a pasta de dados raiz hello.</span><span class="sxs-lookup"><span data-stu-id="10913-290">Compile a U-SQL script and set hello data-root folder.</span></span> <span data-ttu-id="10913-291">Observe que isto substituirá a variável de ambiente do conjunto de saudação.</span><span class="sxs-lookup"><span data-stu-id="10913-291">Note that this will overwrite hello set environment variable.</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

<span data-ttu-id="10913-292">Compilar um script U-SQL e definir um diretório de trabalho, o assembly de referência e o banco de dados:</span><span class="sxs-lookup"><span data-stu-id="10913-292">Compile a U-SQL script and set a working directory, reference assembly, and database:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a><span data-ttu-id="10913-293">Executar resultados compilados</span><span class="sxs-lookup"><span data-stu-id="10913-293">Execute compiled results</span></span>

<span data-ttu-id="10913-294">Olá **execute** comando é usado tooexecute compilado resultados.</span><span class="sxs-lookup"><span data-stu-id="10913-294">hello **execute** command is used tooexecute compiled results.</span></span>   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

<span data-ttu-id="10913-295">Olá, a seguir é argumentos opcionais para **executar**:</span><span class="sxs-lookup"><span data-stu-id="10913-295">hello following are optional arguments for **execute**:</span></span>

|<span data-ttu-id="10913-296">Argumento</span><span class="sxs-lookup"><span data-stu-id="10913-296">Argument</span></span>|<span data-ttu-id="10913-297">Descrição</span><span class="sxs-lookup"><span data-stu-id="10913-297">Description</span></span>|
|--------|-----------|
|<span data-ttu-id="10913-298">-DataRoot [valor padrão '']</span><span class="sxs-lookup"><span data-stu-id="10913-298">-DataRoot [default value '']</span></span>|<span data-ttu-id="10913-299">Raiz de dados para a execução de metadados.</span><span class="sxs-lookup"><span data-stu-id="10913-299">Data root for metadata execution.</span></span> <span data-ttu-id="10913-300">O padrão é toohello **LOCALRUN_DATAROOT** variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="10913-300">It defaults toohello **LOCALRUN_DATAROOT** environment variable.</span></span>|
|<span data-ttu-id="10913-301">-MessageOut [valor padrão '']</span><span class="sxs-lookup"><span data-stu-id="10913-301">-MessageOut [default value '']</span></span>|<span data-ttu-id="10913-302">Despeje mensagens no arquivo de tooa Olá console.</span><span class="sxs-lookup"><span data-stu-id="10913-302">Dump messages on hello console tooa file.</span></span>|
|<span data-ttu-id="10913-303">-Parallel [valor padrão '1']</span><span class="sxs-lookup"><span data-stu-id="10913-303">-Parallel [default value '1']</span></span>|<span data-ttu-id="10913-304">Etapas de execução local do indicador toorun Olá gerado com hello especificado o nível de paralelismo.</span><span class="sxs-lookup"><span data-stu-id="10913-304">Indicator toorun hello generated local-run steps with hello specified parallelism level.</span></span>|
|<span data-ttu-id="10913-305">-Verbose [valor padrão 'False']</span><span class="sxs-lookup"><span data-stu-id="10913-305">-Verbose [default value 'False']</span></span>|<span data-ttu-id="10913-306">Indicador tooshow detalhadas saídas do tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="10913-306">Indicator tooshow detailed outputs from runtime.</span></span>|

<span data-ttu-id="10913-307">Aqui está um exemplo de uso:</span><span class="sxs-lookup"><span data-stu-id="10913-307">Here's a usage example:</span></span>

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5


## <a name="use-hello-sdk-with-programming-interfaces"></a><span data-ttu-id="10913-308">Usar Olá SDK com interfaces de programação</span><span class="sxs-lookup"><span data-stu-id="10913-308">Use hello SDK with programming interfaces</span></span>

<span data-ttu-id="10913-309">interfaces de programação de saudação estão localizado em Olá LocalRunHelper.exe.</span><span class="sxs-lookup"><span data-stu-id="10913-309">hello programming interfaces are all located in hello LocalRunHelper.exe.</span></span> <span data-ttu-id="10913-310">Você pode usá-los toointegrate funcionalidade de saudação do hello SDK U-SQL e Olá c# test framework tooscale seu teste de local de script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="10913-310">You can use them toointegrate hello functionality of hello U-SQL SDK and hello C# test framework tooscale your U-SQL script local test.</span></span> <span data-ttu-id="10913-311">Neste artigo, eu usarei a saudação padrão c# unidade teste projeto tooshow como toouse essas interfaces tootest seu script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="10913-311">In this article, I will use hello standard C# unit test project tooshow how toouse these interfaces tootest your U-SQL script.</span></span>

### <a name="step-1-create-c-unit-test-project-and-configuration"></a><span data-ttu-id="10913-312">Etapa 1: Criar o projeto de teste de unidade do C# e a configuração</span><span class="sxs-lookup"><span data-stu-id="10913-312">Step 1: Create C# unit test project and configuration</span></span>

- <span data-ttu-id="10913-313">Crie um projeto de teste de unidade do C# por meio de Arquivo > Novo > Projeto > Visual C# > Teste > Projeto de Teste de Unidade.</span><span class="sxs-lookup"><span data-stu-id="10913-313">Create a C# unit test project through File > New > Project > Visual C# > Test > Unit Test Project.</span></span>
- <span data-ttu-id="10913-314">Adicione LocalRunHelper.exe como uma referência para o projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="10913-314">Add LocalRunHelper.exe as a reference for hello project.</span></span> <span data-ttu-id="10913-315">Olá LocalRunHelper.exe está localizado em \build\runtime\LocalRunHelper.exe no pacote do Nuget.</span><span class="sxs-lookup"><span data-stu-id="10913-315">hello LocalRunHelper.exe is located at \build\runtime\LocalRunHelper.exe in Nuget package.</span></span>

    ![SDK do U-SQL do Azure Data Lake – Adicionar referência](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-add-reference.png)

- <span data-ttu-id="10913-317">SDK de U-SQL **somente** suporte x64 ambiente, verifique se tooset compilação plataforma destino como x64.</span><span class="sxs-lookup"><span data-stu-id="10913-317">U-SQL SDK **only** support x64 environment, make sure tooset build platform target as x64.</span></span> <span data-ttu-id="10913-318">É possível definir isso por meio de Propriedade do Projeto > Build > Destino da plataforma.</span><span class="sxs-lookup"><span data-stu-id="10913-318">You can set that through Project Property > Build > Platform target.</span></span>

    ![SDK do U-SQL do Azure Data Lake – Configurar projeto do x64](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-x64.png)

- <span data-ttu-id="10913-320">Verifique se tooset seu ambiente de teste como x64.</span><span class="sxs-lookup"><span data-stu-id="10913-320">Make sure tooset your test environment as x64.</span></span> <span data-ttu-id="10913-321">No Visual Studio, é possível defini-lo por meio de Teste > Configurações de Teste > Arquitetura do Processador Padrão > x64.</span><span class="sxs-lookup"><span data-stu-id="10913-321">In Visual Studio, you can set it through Test > Test Settings > Default Processor Architecture > x64.</span></span>

    ![SDK do U-SQL do Azure Data Lake – Configurar ambiente de teste x64](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-test-x64.png)

- <span data-ttu-id="10913-323">Verifique se toocopy todos os arquivos de dependência no diretório de trabalho do NugetPackage\build\runtime\ tooproject que é geralmente em ProjectFolder\bin\x64\Debug.</span><span class="sxs-lookup"><span data-stu-id="10913-323">Make sure toocopy all dependency files under NugetPackage\build\runtime\ tooproject working directory which is usually under ProjectFolder\bin\x64\Debug.</span></span>

### <a name="step-2-create-u-sql-script-test-case"></a><span data-ttu-id="10913-324">Etapa 2: Criar um caso de teste do script U-SQL</span><span class="sxs-lookup"><span data-stu-id="10913-324">Step 2: Create U-SQL script test case</span></span>

<span data-ttu-id="10913-325">Abaixo está o código de exemplo hello para teste de script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="10913-325">Below is hello sample code for U-SQL script test.</span></span> <span data-ttu-id="10913-326">Para testar, você precisa tooprepare scripts, arquivos de entrada e saída esperada.</span><span class="sxs-lookup"><span data-stu-id="10913-326">For testing, you need tooprepare scripts, input files and expected output files.</span></span>

    using System;
    using Microsoft.VisualStudio.TestTools.UnitTesting;
    using System.IO;
    using System.Text;
    using System.Security.Cryptography;
    using Microsoft.Analytics.LocalRun;

    namespace UnitTestProject1
    {
        [TestClass]
        public class USQLUnitTest
        {
            [TestMethod]
            public void TestUSQLScript()
            {
                //Specify hello local run message output path
                StreamWriter MessageOutput = new StreamWriter("../../../log.txt");

                LocalRunHelper localrun = new LocalRunHelper(MessageOutput);

                //Configure hello DateRoot path, Script Path and CPPSDK path
                localrun.DataRoot = "../../../";
                localrun.ScriptPath = "../../../Script/Script.usql";
                localrun.CppSdkDir = "../../../CppSDK";

                //Run U-SQL script
                localrun.DoRun();

                //Script output 
                string Result = Path.Combine(localrun.DataRoot, "Output/result.csv");

                //Expected script output
                string ExpectedResult = "../../../ExpectedOutput/result.csv";

                Test.Helpers.FileAssert.AreEqual(Result, ExpectedResult);

                //Don't forget tooclose MessageOutput tooget logs into file
                MessageOutput.Close();
            }
        }
    }

    namespace Test.Helpers
    {
        public static class FileAssert
        {
            static string GetFileHash(string filename)
            {
                Assert.IsTrue(File.Exists(filename));

                using (var hash = new SHA1Managed())
                {
                    var clearBytes = File.ReadAllBytes(filename);
                    var hashedBytes = hash.ComputeHash(clearBytes);
                    return ConvertBytesToHex(hashedBytes);
                }
            }

            static string ConvertBytesToHex(byte[] bytes)
            {
                var sb = new StringBuilder();

                for (var i = 0; i < bytes.Length; i++)
                {
                    sb.Append(bytes[i].ToString("x"));
                }
                return sb.ToString();
            }

            public static void AreEqual(string filename1, string filename2)
            {
                string hash1 = GetFileHash(filename1);
                string hash2 = GetFileHash(filename2);

                Assert.AreEqual(hash1, hash2);
            }
        }
    }


### <a name="programming-interfaces-in-localrunhelperexe"></a><span data-ttu-id="10913-327">Interfaces de programação em LocalRunHelper.exe</span><span class="sxs-lookup"><span data-stu-id="10913-327">Programming interfaces in LocalRunHelper.exe</span></span>

<span data-ttu-id="10913-328">LocalRunHelper.exe fornece Olá interfaces de programação para compilação de local de U-SQL, execute, interfaces de saudação etc. são listadas a seguir.</span><span class="sxs-lookup"><span data-stu-id="10913-328">LocalRunHelper.exe provides hello programming interfaces for U-SQL local compile, run, etc. hello interfaces are listed as follows.</span></span>

<span data-ttu-id="10913-329">**Construtor**</span><span class="sxs-lookup"><span data-stu-id="10913-329">**Constructor**</span></span>

<span data-ttu-id="10913-330">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span><span class="sxs-lookup"><span data-stu-id="10913-330">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span></span>

|<span data-ttu-id="10913-331">.</span><span class="sxs-lookup"><span data-stu-id="10913-331">Parameter</span></span>|<span data-ttu-id="10913-332">Tipo</span><span class="sxs-lookup"><span data-stu-id="10913-332">Type</span></span>|<span data-ttu-id="10913-333">Descrição</span><span class="sxs-lookup"><span data-stu-id="10913-333">Description</span></span>|
|---------|----|-----------|
|<span data-ttu-id="10913-334">messageOutput</span><span class="sxs-lookup"><span data-stu-id="10913-334">messageOutput</span></span>|<span data-ttu-id="10913-335">System.IO.TextWriter</span><span class="sxs-lookup"><span data-stu-id="10913-335">System.IO.TextWriter</span></span>|<span data-ttu-id="10913-336">para mensagens de saída, definir toonull toouse Console</span><span class="sxs-lookup"><span data-stu-id="10913-336">for output messages, set toonull toouse Console</span></span>|

<span data-ttu-id="10913-337">**Propriedades**</span><span class="sxs-lookup"><span data-stu-id="10913-337">**Properties**</span></span>

|<span data-ttu-id="10913-338">Propriedade</span><span class="sxs-lookup"><span data-stu-id="10913-338">Property</span></span>|<span data-ttu-id="10913-339">Tipo</span><span class="sxs-lookup"><span data-stu-id="10913-339">Type</span></span>|<span data-ttu-id="10913-340">Descrição</span><span class="sxs-lookup"><span data-stu-id="10913-340">Description</span></span>|
|--------|----|-----------|
|<span data-ttu-id="10913-341">AlgebraPath</span><span class="sxs-lookup"><span data-stu-id="10913-341">AlgebraPath</span></span>|<span data-ttu-id="10913-342">string</span><span class="sxs-lookup"><span data-stu-id="10913-342">string</span></span>|<span data-ttu-id="10913-343">Olá caminho tooalgebra arquivo (arquivo álgebra é um dos resultados da compilação Olá)</span><span class="sxs-lookup"><span data-stu-id="10913-343">hello path tooalgebra file (algebra file is one of hello compilation results)</span></span>|
|<span data-ttu-id="10913-344">CodeBehindReferences</span><span class="sxs-lookup"><span data-stu-id="10913-344">CodeBehindReferences</span></span>|<span data-ttu-id="10913-345">string</span><span class="sxs-lookup"><span data-stu-id="10913-345">string</span></span>|<span data-ttu-id="10913-346">Se o script hello tem adicional code-behind referências, especificar caminhos de Olá separados por ';'</span><span class="sxs-lookup"><span data-stu-id="10913-346">If hello script has additional code behind references, specify hello paths separated with ';'</span></span>|
|<span data-ttu-id="10913-347">CppSdkDir</span><span class="sxs-lookup"><span data-stu-id="10913-347">CppSdkDir</span></span>|<span data-ttu-id="10913-348">string</span><span class="sxs-lookup"><span data-stu-id="10913-348">string</span></span>|<span data-ttu-id="10913-349">Diretório do CppSDK</span><span class="sxs-lookup"><span data-stu-id="10913-349">CppSDK directory</span></span>|
|<span data-ttu-id="10913-350">CurrentDir</span><span class="sxs-lookup"><span data-stu-id="10913-350">CurrentDir</span></span>|<span data-ttu-id="10913-351">string</span><span class="sxs-lookup"><span data-stu-id="10913-351">string</span></span>|<span data-ttu-id="10913-352">Diretório atual</span><span class="sxs-lookup"><span data-stu-id="10913-352">Current directory</span></span>|
|<span data-ttu-id="10913-353">DataRoot</span><span class="sxs-lookup"><span data-stu-id="10913-353">DataRoot</span></span>|<span data-ttu-id="10913-354">string</span><span class="sxs-lookup"><span data-stu-id="10913-354">string</span></span>|<span data-ttu-id="10913-355">Caminho da raiz de dados</span><span class="sxs-lookup"><span data-stu-id="10913-355">Data root path</span></span>|
|<span data-ttu-id="10913-356">DebuggerMailPath</span><span class="sxs-lookup"><span data-stu-id="10913-356">DebuggerMailPath</span></span>|<span data-ttu-id="10913-357">string</span><span class="sxs-lookup"><span data-stu-id="10913-357">string</span></span>|<span data-ttu-id="10913-358">Olá caminho toodebugger falhas</span><span class="sxs-lookup"><span data-stu-id="10913-358">hello path toodebugger mailslot</span></span>|
|<span data-ttu-id="10913-359">GenerateUdoRedirect</span><span class="sxs-lookup"><span data-stu-id="10913-359">GenerateUdoRedirect</span></span>|<span data-ttu-id="10913-360">bool</span><span class="sxs-lookup"><span data-stu-id="10913-360">bool</span></span>|<span data-ttu-id="10913-361">Se quisermos carregamento do assembly toogenerate redirecionamento Substituir configuração</span><span class="sxs-lookup"><span data-stu-id="10913-361">If we want toogenerate assembly loading redirection override config</span></span>|
|<span data-ttu-id="10913-362">HasCodeBehind</span><span class="sxs-lookup"><span data-stu-id="10913-362">HasCodeBehind</span></span>|<span data-ttu-id="10913-363">bool</span><span class="sxs-lookup"><span data-stu-id="10913-363">bool</span></span>|<span data-ttu-id="10913-364">Se o script hello tem code-behind</span><span class="sxs-lookup"><span data-stu-id="10913-364">If hello script has code behind</span></span>|
|<span data-ttu-id="10913-365">InputDir</span><span class="sxs-lookup"><span data-stu-id="10913-365">InputDir</span></span>|<span data-ttu-id="10913-366">string</span><span class="sxs-lookup"><span data-stu-id="10913-366">string</span></span>|<span data-ttu-id="10913-367">Diretório dos dados de entrada</span><span class="sxs-lookup"><span data-stu-id="10913-367">Directory for input data</span></span>|
|<span data-ttu-id="10913-368">MessagePath</span><span class="sxs-lookup"><span data-stu-id="10913-368">MessagePath</span></span>|<span data-ttu-id="10913-369">string</span><span class="sxs-lookup"><span data-stu-id="10913-369">string</span></span>|<span data-ttu-id="10913-370">Caminho do arquivo de despejo da mensagem</span><span class="sxs-lookup"><span data-stu-id="10913-370">Message dump file path</span></span>|
|<span data-ttu-id="10913-371">OutputDir</span><span class="sxs-lookup"><span data-stu-id="10913-371">OutputDir</span></span>|<span data-ttu-id="10913-372">string</span><span class="sxs-lookup"><span data-stu-id="10913-372">string</span></span>|<span data-ttu-id="10913-373">Diretório dos dados de saída</span><span class="sxs-lookup"><span data-stu-id="10913-373">Directory for output data</span></span>|
|<span data-ttu-id="10913-374">Paralelismo</span><span class="sxs-lookup"><span data-stu-id="10913-374">Parallelism</span></span>|<span data-ttu-id="10913-375">int</span><span class="sxs-lookup"><span data-stu-id="10913-375">int</span></span>|<span data-ttu-id="10913-376">Álgebra de saudação do paralelismo toorun</span><span class="sxs-lookup"><span data-stu-id="10913-376">Parallelism toorun hello algebra</span></span>|
|<span data-ttu-id="10913-377">ParentPid</span><span class="sxs-lookup"><span data-stu-id="10913-377">ParentPid</span></span>|<span data-ttu-id="10913-378">int</span><span class="sxs-lookup"><span data-stu-id="10913-378">int</span></span>|<span data-ttu-id="10913-379">PID do pai Olá nas quais Olá serviço monitora tooexit, conjunto too0 ou tooignore negativo</span><span class="sxs-lookup"><span data-stu-id="10913-379">PID of hello parent on which hello service monitors tooexit, set too0 or negative tooignore</span></span>|
|<span data-ttu-id="10913-380">ResultPath</span><span class="sxs-lookup"><span data-stu-id="10913-380">ResultPath</span></span>|<span data-ttu-id="10913-381">string</span><span class="sxs-lookup"><span data-stu-id="10913-381">string</span></span>|<span data-ttu-id="10913-382">Caminho do arquivo de despejo do resultado</span><span class="sxs-lookup"><span data-stu-id="10913-382">Result dump file path</span></span>|
|<span data-ttu-id="10913-383">RuntimeDir</span><span class="sxs-lookup"><span data-stu-id="10913-383">RuntimeDir</span></span>|<span data-ttu-id="10913-384">string</span><span class="sxs-lookup"><span data-stu-id="10913-384">string</span></span>|<span data-ttu-id="10913-385">Diretório do tempo de execução</span><span class="sxs-lookup"><span data-stu-id="10913-385">Runtime directory</span></span>|
|<span data-ttu-id="10913-386">ScriptPath</span><span class="sxs-lookup"><span data-stu-id="10913-386">ScriptPath</span></span>|<span data-ttu-id="10913-387">string</span><span class="sxs-lookup"><span data-stu-id="10913-387">string</span></span>|<span data-ttu-id="10913-388">Onde toofind Olá script</span><span class="sxs-lookup"><span data-stu-id="10913-388">Where toofind hello script</span></span>|
|<span data-ttu-id="10913-389">Shallow</span><span class="sxs-lookup"><span data-stu-id="10913-389">Shallow</span></span>|<span data-ttu-id="10913-390">bool</span><span class="sxs-lookup"><span data-stu-id="10913-390">bool</span></span>|<span data-ttu-id="10913-391">Compilação superficial ou não</span><span class="sxs-lookup"><span data-stu-id="10913-391">Shallow compile or not</span></span>|
|<span data-ttu-id="10913-392">TempDir</span><span class="sxs-lookup"><span data-stu-id="10913-392">TempDir</span></span>|<span data-ttu-id="10913-393">string</span><span class="sxs-lookup"><span data-stu-id="10913-393">string</span></span>|<span data-ttu-id="10913-394">Diretório temporário</span><span class="sxs-lookup"><span data-stu-id="10913-394">Temp directory</span></span>|
|<span data-ttu-id="10913-395">UseDataBase</span><span class="sxs-lookup"><span data-stu-id="10913-395">UseDataBase</span></span>|<span data-ttu-id="10913-396">string</span><span class="sxs-lookup"><span data-stu-id="10913-396">string</span></span>|<span data-ttu-id="10913-397">Especifique a saudação toouse de banco de dados para o código por trás de registro do assembly temporário, mestre por padrão</span><span class="sxs-lookup"><span data-stu-id="10913-397">Specify hello database toouse for code behind temporary assembly registration, master by default</span></span>|
|<span data-ttu-id="10913-398">WorkDir</span><span class="sxs-lookup"><span data-stu-id="10913-398">WorkDir</span></span>|<span data-ttu-id="10913-399">string</span><span class="sxs-lookup"><span data-stu-id="10913-399">string</span></span>|<span data-ttu-id="10913-400">Diretório de trabalho preferencial</span><span class="sxs-lookup"><span data-stu-id="10913-400">Preferred working directory</span></span>|


<span data-ttu-id="10913-401">**Método**</span><span class="sxs-lookup"><span data-stu-id="10913-401">**Method**</span></span>

|<span data-ttu-id="10913-402">Método</span><span class="sxs-lookup"><span data-stu-id="10913-402">Method</span></span>|<span data-ttu-id="10913-403">Descrição</span><span class="sxs-lookup"><span data-stu-id="10913-403">Description</span></span>|<span data-ttu-id="10913-404">Retorno</span><span class="sxs-lookup"><span data-stu-id="10913-404">Return</span></span>|<span data-ttu-id="10913-405">.</span><span class="sxs-lookup"><span data-stu-id="10913-405">Parameter</span></span>|
|------|-----------|------|---------|
|<span data-ttu-id="10913-406">public bool DoCompile()</span><span class="sxs-lookup"><span data-stu-id="10913-406">public bool DoCompile()</span></span>|<span data-ttu-id="10913-407">Olá U-SQL script de compilação</span><span class="sxs-lookup"><span data-stu-id="10913-407">Compile hello U-SQL script</span></span>|<span data-ttu-id="10913-408">Verdadeiro se tiver êxito</span><span class="sxs-lookup"><span data-stu-id="10913-408">True on success</span></span>| |
|<span data-ttu-id="10913-409">public bool DoExec()</span><span class="sxs-lookup"><span data-stu-id="10913-409">public bool DoExec()</span></span>|<span data-ttu-id="10913-410">Execute o resultado de saudação compilado</span><span class="sxs-lookup"><span data-stu-id="10913-410">Execute hello compiled result</span></span>|<span data-ttu-id="10913-411">Verdadeiro se tiver êxito</span><span class="sxs-lookup"><span data-stu-id="10913-411">True on success</span></span>| |
|<span data-ttu-id="10913-412">public bool DoRun()</span><span class="sxs-lookup"><span data-stu-id="10913-412">public bool DoRun()</span></span>|<span data-ttu-id="10913-413">Executar script hello U-SQL (compilar + executar)</span><span class="sxs-lookup"><span data-stu-id="10913-413">Run hello U-SQL script (Compile + Execute)</span></span>|<span data-ttu-id="10913-414">Verdadeiro se tiver êxito</span><span class="sxs-lookup"><span data-stu-id="10913-414">True on success</span></span>| |
|<span data-ttu-id="10913-415">public bool IsValidRuntimeDir(string path)</span><span class="sxs-lookup"><span data-stu-id="10913-415">public bool IsValidRuntimeDir(string path)</span></span>|<span data-ttu-id="10913-416">Verifique se Olá dado caminho é caminho válido do tempo de execução</span><span class="sxs-lookup"><span data-stu-id="10913-416">Check if hello given path is valid runtime path</span></span>|<span data-ttu-id="10913-417">Verdadeiro para válido</span><span class="sxs-lookup"><span data-stu-id="10913-417">True for valid</span></span>|<span data-ttu-id="10913-418">caminho de saudação do diretório de tempo de execução</span><span class="sxs-lookup"><span data-stu-id="10913-418">hello path of runtime directory</span></span>|


## <a name="faq-about-common-issue"></a><span data-ttu-id="10913-419">Perguntas frequentes sobre um problema comum</span><span class="sxs-lookup"><span data-stu-id="10913-419">FAQ about common issue</span></span>

### <a name="error-1"></a><span data-ttu-id="10913-420">Erro 1:</span><span class="sxs-lookup"><span data-stu-id="10913-420">Error 1:</span></span>
<span data-ttu-id="10913-421">E_CSC_SYSTEM_INTERNAL: Erro interno.</span><span class="sxs-lookup"><span data-stu-id="10913-421">E_CSC_SYSTEM_INTERNAL: Internal error!</span></span> <span data-ttu-id="10913-422">Não foi possível carregar o arquivo ou o assembly “ScopeEngineManaged.dll” ou uma de suas dependências.</span><span class="sxs-lookup"><span data-stu-id="10913-422">Could not load file or assembly 'ScopeEngineManaged.dll' or one of its dependencies.</span></span> <span data-ttu-id="10913-423">módulo especificado Olá não pôde ser encontrado.</span><span class="sxs-lookup"><span data-stu-id="10913-423">hello specified module could not be found.</span></span>

<span data-ttu-id="10913-424">Verifique o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="10913-424">Please check hello following:</span></span>

- <span data-ttu-id="10913-425">Verifique se você tem o ambiente x64.</span><span class="sxs-lookup"><span data-stu-id="10913-425">Make sure you have x64 environment.</span></span> <span data-ttu-id="10913-426">plataforma de destino de compilação Hello e ambiente de teste de saudação deve ser x64, consulte muito**etapa 1: configuração e projeto de teste de unidade criar c#** acima.</span><span class="sxs-lookup"><span data-stu-id="10913-426">hello build target platform and hello test environment should be x64, refer too**Step 1: Create C# unit test project and configuration** above.</span></span>
- <span data-ttu-id="10913-427">Verifique se que você copiou todos os arquivos de dependência no diretório de trabalho do NugetPackage\build\runtime\ tooproject.</span><span class="sxs-lookup"><span data-stu-id="10913-427">Make sure you have copied all dependency files under NugetPackage\build\runtime\ tooproject working directory.</span></span>


## <a name="next-steps"></a><span data-ttu-id="10913-428">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="10913-428">Next steps</span></span>

* <span data-ttu-id="10913-429">toolearn U-SQL, consulte [começar com a linguagem da análise Azure Data Lake U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="10913-429">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="10913-430">toolog informações de diagnóstico, consulte [acessar logs de diagnóstico para análise do Azure Data Lake](data-lake-analytics-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="10913-430">toolog diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span></span>
* <span data-ttu-id="10913-431">toosee uma consulta mais complexa, consulte [analisar logs de site usando a análise do Azure Data Lake](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="10913-431">toosee a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="10913-432">detalhes do trabalho tooview, consulte [navegador de trabalho de uso e a exibição de trabalho de trabalhos da análise Azure Data Lake](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="10913-432">tooview job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="10913-433">exibição de execuções de vértice de saudação toouse, consulte [Olá Use exibição de execuções de vértice no Data Lake Tools para Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="10913-433">toouse hello vertex execution view, see [Use hello Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
