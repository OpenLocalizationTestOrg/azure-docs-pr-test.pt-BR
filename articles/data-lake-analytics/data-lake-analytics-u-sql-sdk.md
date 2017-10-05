---
title: "Escalar a execução e o teste locais do U-SQL com o SDK do U-SQL do Azure Data Lake | Microsoft Docs"
description: "Saiba como usar o SDK do U-SQL do Azure Data Lake para escalar a execução e o teste locais de trabalhos do U-SQL com a linha de comando e interfaces de programação na estação de trabalho local."
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
ms.openlocfilehash: 55242bcf644ca0e7f30cfe7eada2130451c36e64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="scale-u-sql-local-run-and-test-with-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="b2f09-103">Escalar a execução e o teste locais do U-SQL com o SDK do U-SQL do Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="b2f09-103">Scale U-SQL local run and test with Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="b2f09-104">Ao desenvolver o script U-SQL, é comum executar e testá-lo localmente antes enviá-lo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="b2f09-104">When developing U-SQL script, it is common to run and test U-SQL script locally before submit it to cloud.</span></span> <span data-ttu-id="b2f09-105">O Azure Data Lake fornece um pacote NuGet chamado SDK do U-SQL do Azure Data Lake para este cenário, por meio do qual é possível escalar a execução e o teste locais do U-SQL com facilidade.</span><span class="sxs-lookup"><span data-stu-id="b2f09-105">Azure Data Lake provides a Nuget package called Azure Data Lake U-SQL SDK for this scenario, through which you can easily scale U-SQL local run and test.</span></span> <span data-ttu-id="b2f09-106">Também é possível integrar esse teste do U-SQL ao sistema de CI (Integração Contínua) para automatizar a compilação e o teste.</span><span class="sxs-lookup"><span data-stu-id="b2f09-106">It is also possible to integrate this U-SQL test with CI (Continuous Integration) system to automate the compile and test.</span></span>

<span data-ttu-id="b2f09-107">Se você se preocupa em como executar e depurar o script U-SQL no local manualmente com ferramentas de GUI, é possível usar as Ferramentas do Azure Data Lake para Visual Studio para essa finalidade.</span><span class="sxs-lookup"><span data-stu-id="b2f09-107">If you care about how to manually local run and debug U-SQL script with GUI tooling, then you can use Azure Data Lake Tools for Visual Studio for that.</span></span> <span data-ttu-id="b2f09-108">Saiba mais [aqui](data-lake-analytics-data-lake-tools-local-run.md).</span><span class="sxs-lookup"><span data-stu-id="b2f09-108">You can learn more from [here](data-lake-analytics-data-lake-tools-local-run.md).</span></span>

## <a name="install-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="b2f09-109">Instalar o SDK do U-SQL do Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="b2f09-109">Install Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="b2f09-110">É possível obter o SDK do U-SQL do Azure Data Lake [aqui](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) em Nuget.org.</span><span class="sxs-lookup"><span data-stu-id="b2f09-110">You can get the Azure Data Lake U-SQL SDK [here](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) on Nuget.org.</span></span> <span data-ttu-id="b2f09-111">Antes de usá-lo, você precisa verificar se tem as dependências a seguir.</span><span class="sxs-lookup"><span data-stu-id="b2f09-111">And before using it, you need to make sure you have dependencies as follows.</span></span>

### <a name="dependencies"></a><span data-ttu-id="b2f09-112">Dependências</span><span class="sxs-lookup"><span data-stu-id="b2f09-112">Dependencies</span></span>

<span data-ttu-id="b2f09-113">O SDK para U-SQL do Data Lake exige as seguintes dependências:</span><span class="sxs-lookup"><span data-stu-id="b2f09-113">The Data Lake U-SQL SDK requires the following dependencies:</span></span>

- <span data-ttu-id="b2f09-114">[Microsoft .NET Framework 4.6 ou mais recente](https://www.microsoft.com/download/details.aspx?id=17851).</span><span class="sxs-lookup"><span data-stu-id="b2f09-114">[Microsoft .NET Framework 4.6 or newer](https://www.microsoft.com/download/details.aspx?id=17851).</span></span>
- <span data-ttu-id="b2f09-115">Microsoft Visual C++ 14 e SDK do Windows 10.0.10240.0 ou mais novo (que é chamado CppSDK neste artigo).</span><span class="sxs-lookup"><span data-stu-id="b2f09-115">Microsoft Visual C++ 14 and Windows SDK 10.0.10240.0 or newer (which is called CppSDK in this article).</span></span> <span data-ttu-id="b2f09-116">Há duas maneiras de obter o CppSDK:</span><span class="sxs-lookup"><span data-stu-id="b2f09-116">There are two ways to get CppSDK:</span></span>

    - <span data-ttu-id="b2f09-117">Instalar o [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span><span class="sxs-lookup"><span data-stu-id="b2f09-117">Install [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span></span> <span data-ttu-id="b2f09-118">Você terá uma pasta \Windows Kits\10 na pasta Arquivos de Programa – por exemplo, C:\Program Files (x86) \Windows Kits\10\.</span><span class="sxs-lookup"><span data-stu-id="b2f09-118">You'll have a \Windows Kits\10 folder under the Program Files folder--for example, C:\Program Files (x86)\Windows Kits\10\.</span></span> <span data-ttu-id="b2f09-119">Você também encontrará a versão do SDK do Windows 10 em \Windows Kits\10\Lib.</span><span class="sxs-lookup"><span data-stu-id="b2f09-119">You'll also find the Windows 10 SDK version under \Windows Kits\10\Lib.</span></span> <span data-ttu-id="b2f09-120">Se você não vir essas pastas, reinstale o Visual Studio e selecione o SDK do Windows 10 durante a instalação.</span><span class="sxs-lookup"><span data-stu-id="b2f09-120">If you don’t see these folders, reinstall Visual Studio and be sure to select the Windows 10 SDK during the installation.</span></span> <span data-ttu-id="b2f09-121">Se você tiver isso instalado com o Visual Studio, o compilador local do U-SQL o encontrará automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b2f09-121">If you have this installed with Visual Studio, the U-SQL local compiler will find it automatically.</span></span>

    ![SDK para Windows 10 da execução local das Ferramentas do Data Lake para Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - <span data-ttu-id="b2f09-123">Instalar [Ferramentas do Data Lake para Visual Studio](http://aka.ms/adltoolsvs).</span><span class="sxs-lookup"><span data-stu-id="b2f09-123">Install [Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="b2f09-124">Você pode encontrar os arquivos pré-empacotados do SDK do Windows e Visual C++ em C:\Arquivos de Programas (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span><span class="sxs-lookup"><span data-stu-id="b2f09-124">You can find the prepackaged Visual C++ and Windows SDK files at C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span></span> <span data-ttu-id="b2f09-125">Nesse caso, o compilador local U-SQL não pode localizar as dependências automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b2f09-125">In this case, the U-SQL local compiler cannot find the dependencies automatically.</span></span> <span data-ttu-id="b2f09-126">Você precisa especificar o caminho CppSDK para ele.</span><span class="sxs-lookup"><span data-stu-id="b2f09-126">You need to specify the CppSDK path for it.</span></span> <span data-ttu-id="b2f09-127">Você pode copiar os arquivos para outro local ou usá-los como estão.</span><span class="sxs-lookup"><span data-stu-id="b2f09-127">You can either copy the files to another location or use it as is.</span></span>

## <a name="understand-basic-concepts"></a><span data-ttu-id="b2f09-128">Entender os conceitos básicos</span><span class="sxs-lookup"><span data-stu-id="b2f09-128">Understand basic concepts</span></span>

### <a name="data-root"></a><span data-ttu-id="b2f09-129">Raiz de dados</span><span class="sxs-lookup"><span data-stu-id="b2f09-129">Data root</span></span>

<span data-ttu-id="b2f09-130">A pasta raiz de dados é um "repositório local" para a conta de computador local.</span><span class="sxs-lookup"><span data-stu-id="b2f09-130">The data-root folder is a "local store" for the local compute account.</span></span> <span data-ttu-id="b2f09-131">Ela equivale à conta do Azure Data Lake Store de uma conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="b2f09-131">It's equivalent to the Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="b2f09-132">Alternar para uma pasta raiz de dados diferente é como alternar para uma conta de repositório diferente.</span><span class="sxs-lookup"><span data-stu-id="b2f09-132">Switching to a different data-root folder is just like switching to a different store account.</span></span> <span data-ttu-id="b2f09-133">Se você quiser acessar dados compartilhados normalmente com pastas raiz de dados diferentes, deverá usar caminhos absolutos em seus scripts.</span><span class="sxs-lookup"><span data-stu-id="b2f09-133">If you want to access commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="b2f09-134">Ou criar links simbólicos de sistema de arquivo (por exemplo, **mklink** em NTFS) na pasta raiz de dados para apontar para os dados compartilhados.</span><span class="sxs-lookup"><span data-stu-id="b2f09-134">Or, create file system symbolic links (for example, **mklink** on NTFS) under the data-root folder to point to the shared data.</span></span>

<span data-ttu-id="b2f09-135">A pasta raiz de dados é usada para:</span><span class="sxs-lookup"><span data-stu-id="b2f09-135">The data-root folder is used to:</span></span>

- <span data-ttu-id="b2f09-136">Armazenar metadados locais, incluindo bancos de dados, tabelas, TVFs (funções com valor de tabela) e assemblies.</span><span class="sxs-lookup"><span data-stu-id="b2f09-136">Store local metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="b2f09-137">Pesquisar os caminhos de entrada e saída que são definidos como caminhos relativos no U-SQL.</span><span class="sxs-lookup"><span data-stu-id="b2f09-137">Look up the input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="b2f09-138">Usar caminhos relativos facilita a implantação dos projetos U-SQL no Azure.</span><span class="sxs-lookup"><span data-stu-id="b2f09-138">Using relative paths makes it easier to deploy your U-SQL projects to Azure.</span></span>

### <a name="file-path-in-u-sql"></a><span data-ttu-id="b2f09-139">Caminho de arquivo no U-SQL</span><span class="sxs-lookup"><span data-stu-id="b2f09-139">File path in U-SQL</span></span>

<span data-ttu-id="b2f09-140">Você pode usar um caminho relativo e um caminho absoluto local em scripts U-SQL.</span><span class="sxs-lookup"><span data-stu-id="b2f09-140">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="b2f09-141">O caminho relativo é relativo ao caminho da pasta raiz de dados especificado.</span><span class="sxs-lookup"><span data-stu-id="b2f09-141">The relative path is relative to the specified data-root folder path.</span></span> <span data-ttu-id="b2f09-142">Recomendamos que você use "/" como o separador de caminho para tornar seus scripts compatíveis com o lado do servidor.</span><span class="sxs-lookup"><span data-stu-id="b2f09-142">We recommend that you use "/" as the path separator to make your scripts compatible with the server side.</span></span> <span data-ttu-id="b2f09-143">A seguir, alguns exemplos de caminhos relativos e os respectivos caminhos absolutos equivalentes.</span><span class="sxs-lookup"><span data-stu-id="b2f09-143">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="b2f09-144">Nesses exemplos, C:\LocalRunDataRoot é a pasta raiz de dados.</span><span class="sxs-lookup"><span data-stu-id="b2f09-144">In these examples, C:\LocalRunDataRoot is the data-root folder.</span></span>

|<span data-ttu-id="b2f09-145">Caminho relativo</span><span class="sxs-lookup"><span data-stu-id="b2f09-145">Relative path</span></span>|<span data-ttu-id="b2f09-146">Caminho absoluto</span><span class="sxs-lookup"><span data-stu-id="b2f09-146">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="b2f09-147">/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="b2f09-147">/abc/def/input.csv</span></span> |<span data-ttu-id="b2f09-148">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="b2f09-148">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="b2f09-149">abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="b2f09-149">abc/def/input.csv</span></span>  |<span data-ttu-id="b2f09-150">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="b2f09-150">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="b2f09-151">D:/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="b2f09-151">D:/abc/def/input.csv</span></span> |<span data-ttu-id="b2f09-152">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="b2f09-152">D:\abc\def\input.csv</span></span>|

### <a name="working-directory"></a><span data-ttu-id="b2f09-153">Diretório de trabalho</span><span class="sxs-lookup"><span data-stu-id="b2f09-153">Working directory</span></span>

<span data-ttu-id="b2f09-154">Ao executar o script U-SQL localmente, um diretório de trabalho é criado durante a compilação no diretório de execução atual.</span><span class="sxs-lookup"><span data-stu-id="b2f09-154">When running the U-SQL script locally, a working directory is created during compilation under current running directory.</span></span> <span data-ttu-id="b2f09-155">Além das saídas de compilação, os arquivos de tempo de execução necessários para execução local são copiados em sombra para esse diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b2f09-155">In addition to the compilation outputs, the needed runtime files for local execution will be shadow copied to this working directory.</span></span> <span data-ttu-id="b2f09-156">A pasta raiz do diretório de trabalho é chamada “ScopeWorkDir” e os arquivos no diretório de trabalho são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="b2f09-156">The working directory root folder is called "ScopeWorkDir" and the files under the working directory are as follows:</span></span>

|<span data-ttu-id="b2f09-157">Diretório/arquivo</span><span class="sxs-lookup"><span data-stu-id="b2f09-157">Directory/file</span></span>|<span data-ttu-id="b2f09-158">Diretório/arquivo</span><span class="sxs-lookup"><span data-stu-id="b2f09-158">Directory/file</span></span>|<span data-ttu-id="b2f09-159">Diretório/arquivo</span><span class="sxs-lookup"><span data-stu-id="b2f09-159">Directory/file</span></span>|<span data-ttu-id="b2f09-160">Definição</span><span class="sxs-lookup"><span data-stu-id="b2f09-160">Definition</span></span>|<span data-ttu-id="b2f09-161">Descrição</span><span class="sxs-lookup"><span data-stu-id="b2f09-161">Description</span></span>|
|--------------|--------------|--------------|----------|-----------|
|<span data-ttu-id="b2f09-162">C6A101DDCB470506</span><span class="sxs-lookup"><span data-stu-id="b2f09-162">C6A101DDCB470506</span></span>| | |<span data-ttu-id="b2f09-163">Cadeia de caracteres de hash da versão do tempo de execução</span><span class="sxs-lookup"><span data-stu-id="b2f09-163">Hash string of runtime version</span></span>|<span data-ttu-id="b2f09-164">Cópia de sombra dos arquivos de tempo de execução necessários para execução local</span><span class="sxs-lookup"><span data-stu-id="b2f09-164">Shadow copy of runtime files needed for local execution</span></span>|
| |<span data-ttu-id="b2f09-165">Script_66AE4909AA0ED06C</span><span class="sxs-lookup"><span data-stu-id="b2f09-165">Script_66AE4909AA0ED06C</span></span>| |<span data-ttu-id="b2f09-166">Nome do script + cadeia de caracteres de hash do caminho do script</span><span class="sxs-lookup"><span data-stu-id="b2f09-166">Script name + hash string of script path</span></span>|<span data-ttu-id="b2f09-167">Saídas da compilação e log das etapas de execução</span><span class="sxs-lookup"><span data-stu-id="b2f09-167">Compilation outputs and execution step logging</span></span>|
| | |<span data-ttu-id="b2f09-168">\_script\_.abr</span><span class="sxs-lookup"><span data-stu-id="b2f09-168">\_script\_.abr</span></span>|<span data-ttu-id="b2f09-169">Saída do compilador</span><span class="sxs-lookup"><span data-stu-id="b2f09-169">Compiler output</span></span>|<span data-ttu-id="b2f09-170">Arquivo de álgebra</span><span class="sxs-lookup"><span data-stu-id="b2f09-170">Algebra file</span></span>|
| | |<span data-ttu-id="b2f09-171">\_ScopeCodeGen\_.*</span><span class="sxs-lookup"><span data-stu-id="b2f09-171">\_ScopeCodeGen\_.*</span></span>|<span data-ttu-id="b2f09-172">Saída do compilador</span><span class="sxs-lookup"><span data-stu-id="b2f09-172">Compiler output</span></span>|<span data-ttu-id="b2f09-173">Código gerenciado gerado</span><span class="sxs-lookup"><span data-stu-id="b2f09-173">Generated managed code</span></span>|
| | |<span data-ttu-id="b2f09-174">\_ScopeCodeGenEngine\_.*</span><span class="sxs-lookup"><span data-stu-id="b2f09-174">\_ScopeCodeGenEngine\_.*</span></span>|<span data-ttu-id="b2f09-175">Saída do compilador</span><span class="sxs-lookup"><span data-stu-id="b2f09-175">Compiler output</span></span>|<span data-ttu-id="b2f09-176">Código nativo gerado</span><span class="sxs-lookup"><span data-stu-id="b2f09-176">Generated native code</span></span>|
| | |<span data-ttu-id="b2f09-177">assemblies referenciados</span><span class="sxs-lookup"><span data-stu-id="b2f09-177">referenced assemblies</span></span>|<span data-ttu-id="b2f09-178">Referência de assembly</span><span class="sxs-lookup"><span data-stu-id="b2f09-178">Assembly reference</span></span>|<span data-ttu-id="b2f09-179">Arquivos de assembly referenciado</span><span class="sxs-lookup"><span data-stu-id="b2f09-179">Referenced assembly files</span></span>|
| | |<span data-ttu-id="b2f09-180">deployed_resources</span><span class="sxs-lookup"><span data-stu-id="b2f09-180">deployed_resources</span></span>|<span data-ttu-id="b2f09-181">Implantação de recursos</span><span class="sxs-lookup"><span data-stu-id="b2f09-181">Resource deployment</span></span>|<span data-ttu-id="b2f09-182">Arquivos da implantação de recursos</span><span class="sxs-lookup"><span data-stu-id="b2f09-182">Resource deployment files</span></span>|
| | |<span data-ttu-id="b2f09-183">xxxxxxxx.xxx[1..n]\_\*.*</span><span class="sxs-lookup"><span data-stu-id="b2f09-183">xxxxxxxx.xxx[1..n]\_\*.*</span></span>|<span data-ttu-id="b2f09-184">Log de execução</span><span class="sxs-lookup"><span data-stu-id="b2f09-184">Execution log</span></span>|<span data-ttu-id="b2f09-185">Log das etapas de execução</span><span class="sxs-lookup"><span data-stu-id="b2f09-185">Log of execution steps</span></span>|


## <a name="use-the-sdk-from-the-command-line"></a><span data-ttu-id="b2f09-186">Usar o SDK da linha de comando</span><span class="sxs-lookup"><span data-stu-id="b2f09-186">Use the SDK from the command line</span></span>

### <a name="command-line-interface-of-the-helper-application"></a><span data-ttu-id="b2f09-187">Interface de linha de comando do aplicativo auxiliar</span><span class="sxs-lookup"><span data-stu-id="b2f09-187">Command-line interface of the helper application</span></span>

<span data-ttu-id="b2f09-188">Em directory\build\runtime do SDK, LocalRunHelper.exe é o aplicativo auxiliar de linha de comando que fornece interfaces para a maioria das funções de execução local frequentemente usadas.</span><span class="sxs-lookup"><span data-stu-id="b2f09-188">Under SDK directory\build\runtime, LocalRunHelper.exe is the command-line helper application that provides interfaces to most of the commonly used local-run functions.</span></span> <span data-ttu-id="b2f09-189">Observe que as opções de argumentos e de comando diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="b2f09-189">Note that both the command and the argument switches are case-sensitive.</span></span> <span data-ttu-id="b2f09-190">Para invocá-lo:</span><span class="sxs-lookup"><span data-stu-id="b2f09-190">To invoke it:</span></span>

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

<span data-ttu-id="b2f09-191">Execute LocalRunHelper.exe sem argumentos ou com a opção **help** para mostrar as informações de ajuda:</span><span class="sxs-lookup"><span data-stu-id="b2f09-191">Run LocalRunHelper.exe without arguments or with the **help** switch to show the help information:</span></span>

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile the script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

<span data-ttu-id="b2f09-192">Nas informações de ajuda:</span><span class="sxs-lookup"><span data-stu-id="b2f09-192">In the help information:</span></span>

-  <span data-ttu-id="b2f09-193">**Command** fornece o nome do comando.</span><span class="sxs-lookup"><span data-stu-id="b2f09-193">**Command** gives the command’s name.</span></span>  
-  <span data-ttu-id="b2f09-194">**Required Argument** lista argumentos que devem ser fornecidos.</span><span class="sxs-lookup"><span data-stu-id="b2f09-194">**Required Argument** lists arguments that must be supplied.</span></span>  
-  <span data-ttu-id="b2f09-195">**Optional Argument** lista argumentos que são opcionais e com valores padrão.</span><span class="sxs-lookup"><span data-stu-id="b2f09-195">**Optional Argument** lists arguments that are optional, with default values.</span></span>  <span data-ttu-id="b2f09-196">Os argumentos boolianos opcionais não têm parâmetros e as respectivas aparências são negativas para o respectivo valor padrão.</span><span class="sxs-lookup"><span data-stu-id="b2f09-196">Optional Boolean arguments don’t have parameters, and their appearances mean negative to their default value.</span></span>

### <a name="return-value-and-logging"></a><span data-ttu-id="b2f09-197">Valor de retorno e registro em log</span><span class="sxs-lookup"><span data-stu-id="b2f09-197">Return value and logging</span></span>

<span data-ttu-id="b2f09-198">O aplicativo auxiliar retorna **0** em caso de sucesso e **-1** em caso de falha.</span><span class="sxs-lookup"><span data-stu-id="b2f09-198">The helper application returns **0** for success and **-1** for failure.</span></span> <span data-ttu-id="b2f09-199">Por padrão, o auxiliar enviará todas as mensagens para o console atual.</span><span class="sxs-lookup"><span data-stu-id="b2f09-199">By default, the helper sends all messages to the current console.</span></span> <span data-ttu-id="b2f09-200">No entanto, a maioria dos comandos dá suporte ao argumento opcional **-MessageOut path_to_log_file**, que redireciona as saídas para um arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="b2f09-200">However, most of the commands support the **-MessageOut path_to_log_file** optional argument that redirects the outputs to a log file.</span></span>

### <a name="environment-variable-configuring"></a><span data-ttu-id="b2f09-201">Configurando variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="b2f09-201">Environment variable configuring</span></span>

<span data-ttu-id="b2f09-202">A execução local do U-SQL precisa de uma raiz de dados especificada como a conta de armazenamento local, bem como um caminho do CppSDK especificado para as dependências.</span><span class="sxs-lookup"><span data-stu-id="b2f09-202">U-SQL local run needs a specified data root as local storage account, as well as a specified CppSDK path for dependencies.</span></span> <span data-ttu-id="b2f09-203">É possível definir o argumento na linha de comando ou definir a variável de ambiente para elas.</span><span class="sxs-lookup"><span data-stu-id="b2f09-203">You can both set the argument in command-line or set environment variable for them.</span></span>

- <span data-ttu-id="b2f09-204">Defina a variável de ambiente **SCOPE_CPP_SDK**.</span><span class="sxs-lookup"><span data-stu-id="b2f09-204">Set the **SCOPE_CPP_SDK** environment variable.</span></span>

    <span data-ttu-id="b2f09-205">Se obtiver o SDK do Windows e Microsoft Visual C++ instalando as Ferramentas do Data Lake para Visual Studio, verifique se você tem a seguinte pasta:</span><span class="sxs-lookup"><span data-stu-id="b2f09-205">If you get Microsoft Visual C++ and the Windows SDK by installing Data Lake Tools for Visual Studio, verify that you have the following folder:</span></span>

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    <span data-ttu-id="b2f09-206">Defina uma nova variável de ambiente chamada **SCOPE_CPP_SDK** para pontar para esse diretório.</span><span class="sxs-lookup"><span data-stu-id="b2f09-206">Define a new environment variable called **SCOPE_CPP_SDK** to point to this directory.</span></span> <span data-ttu-id="b2f09-207">Ou copie a pasta para outro local e especifique **SCOPE_CPP_SDK** dessa forma.</span><span class="sxs-lookup"><span data-stu-id="b2f09-207">Or copy the folder to the other location and specify **SCOPE_CPP_SDK** as that.</span></span>

    <span data-ttu-id="b2f09-208">Além de definir a variável de ambiente, você também pode especificar o argumento **-CppSDK** ao usar a linha de comando.</span><span class="sxs-lookup"><span data-stu-id="b2f09-208">In addition to setting the environment variable, you can specify the **-CppSDK** argument when you're using the command line.</span></span> <span data-ttu-id="b2f09-209">Esse argumento substitui a variável de ambiente CppSDK padrão.</span><span class="sxs-lookup"><span data-stu-id="b2f09-209">This argument overwrites your default CppSDK environment variable.</span></span>

- <span data-ttu-id="b2f09-210">Defina a variável de ambiente **LOCALRUN_DATAROOT**.</span><span class="sxs-lookup"><span data-stu-id="b2f09-210">Set the **LOCALRUN_DATAROOT** environment variable.</span></span>

    <span data-ttu-id="b2f09-211">Defina uma nova variável de ambiente chamada **LOCALRUN_DATAROOT** que aponta para a raiz de dados.</span><span class="sxs-lookup"><span data-stu-id="b2f09-211">Define a new environment variable called **LOCALRUN_DATAROOT** that points to the data root.</span></span>

    <span data-ttu-id="b2f09-212">Além de definir a variável de ambiente, você pode especificar o argumento **-DataRoot** com o caminho raiz de dados ao usar a linha de comando.</span><span class="sxs-lookup"><span data-stu-id="b2f09-212">In addition to setting the environment variable, you can specify the **-DataRoot** argument with the data-root path when you're using a command line.</span></span> <span data-ttu-id="b2f09-213">Esse argumento substitui a variável de ambiente de raiz de dados padrão.</span><span class="sxs-lookup"><span data-stu-id="b2f09-213">This argument overwrites your default data-root environment variable.</span></span> <span data-ttu-id="b2f09-214">Você precisa adicionar esse argumento para cada linha de comando em execução para que você possa substituir a variável de ambiente de raiz de dados padrão em todas as operações.</span><span class="sxs-lookup"><span data-stu-id="b2f09-214">You need to add this argument to every command line you're running so that you can overwrite the default data-root environment variable for all operations.</span></span>

### <a name="sdk-command-line-usage-samples"></a><span data-ttu-id="b2f09-215">Amostras de uso da linha de comando do SDK</span><span class="sxs-lookup"><span data-stu-id="b2f09-215">SDK command line usage samples</span></span>

#### <a name="compile-and-run"></a><span data-ttu-id="b2f09-216">Compilar e executar</span><span class="sxs-lookup"><span data-stu-id="b2f09-216">Compile and run</span></span>

<span data-ttu-id="b2f09-217">O comando **run** é usado para compilar o script e executar resultados compilados.</span><span class="sxs-lookup"><span data-stu-id="b2f09-217">The **run** command is used to compile the script and then execute compiled results.</span></span> <span data-ttu-id="b2f09-218">Seus argumentos de linha de comando são uma combinação dos argumentos de **compile** e **execute**.</span><span class="sxs-lookup"><span data-stu-id="b2f09-218">Its command-line arguments are a combination of those from **compile** and **execute**.</span></span>

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="b2f09-219">Estes são os argumentos opcionais para **run**:</span><span class="sxs-lookup"><span data-stu-id="b2f09-219">The following are optional arguments for **run**:</span></span>


|<span data-ttu-id="b2f09-220">Argumento</span><span class="sxs-lookup"><span data-stu-id="b2f09-220">Argument</span></span>|<span data-ttu-id="b2f09-221">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="b2f09-221">Default value</span></span>|<span data-ttu-id="b2f09-222">Descrição</span><span class="sxs-lookup"><span data-stu-id="b2f09-222">Description</span></span>|
|--------|-------------|-----------|
|<span data-ttu-id="b2f09-223">-CodeBehind</span><span class="sxs-lookup"><span data-stu-id="b2f09-223">-CodeBehind</span></span>|<span data-ttu-id="b2f09-224">Falso</span><span class="sxs-lookup"><span data-stu-id="b2f09-224">False</span></span>|<span data-ttu-id="b2f09-225">O script tem o code-behind .cs</span><span class="sxs-lookup"><span data-stu-id="b2f09-225">The script has .cs code behind</span></span>|
|<span data-ttu-id="b2f09-226">-CppSDK</span><span class="sxs-lookup"><span data-stu-id="b2f09-226">-CppSDK</span></span>| |<span data-ttu-id="b2f09-227">Diretório do CppSDK</span><span class="sxs-lookup"><span data-stu-id="b2f09-227">CppSDK Directory</span></span>|
|<span data-ttu-id="b2f09-228">-DataRoot</span><span class="sxs-lookup"><span data-stu-id="b2f09-228">-DataRoot</span></span>| <span data-ttu-id="b2f09-229">Variável de ambiente DataRoot</span><span class="sxs-lookup"><span data-stu-id="b2f09-229">DataRoot environment variable</span></span>|<span data-ttu-id="b2f09-230">DataRoot para execução local, padrão para a variável de ambiente “LOCALRUN_DATAROOT”</span><span class="sxs-lookup"><span data-stu-id="b2f09-230">DataRoot for local run, default to 'LOCALRUN_DATAROOT' environment variable</span></span>|
|<span data-ttu-id="b2f09-231">-MessageOut</span><span class="sxs-lookup"><span data-stu-id="b2f09-231">-MessageOut</span></span>| |<span data-ttu-id="b2f09-232">Mensagens de despejo no console para um arquivo</span><span class="sxs-lookup"><span data-stu-id="b2f09-232">Dump messages on console to a file</span></span>|
|<span data-ttu-id="b2f09-233">-Parallel</span><span class="sxs-lookup"><span data-stu-id="b2f09-233">-Parallel</span></span>|<span data-ttu-id="b2f09-234">1</span><span class="sxs-lookup"><span data-stu-id="b2f09-234">1</span></span>|<span data-ttu-id="b2f09-235">Executar o plano com o paralelismo especificado</span><span class="sxs-lookup"><span data-stu-id="b2f09-235">Run the plan with the specified parallelism</span></span>|
|<span data-ttu-id="b2f09-236">-References</span><span class="sxs-lookup"><span data-stu-id="b2f09-236">-References</span></span>| |<span data-ttu-id="b2f09-237">Lista de caminhos para os assemblies de referência extra ou arquivos de dados do code-behind, separados por ';'</span><span class="sxs-lookup"><span data-stu-id="b2f09-237">List of paths to extra reference assemblies or data files of code behind, separated by ';'</span></span>|
|<span data-ttu-id="b2f09-238">-UdoRedirect</span><span class="sxs-lookup"><span data-stu-id="b2f09-238">-UdoRedirect</span></span>|<span data-ttu-id="b2f09-239">Falso</span><span class="sxs-lookup"><span data-stu-id="b2f09-239">False</span></span>|<span data-ttu-id="b2f09-240">Gerar configuração de redirecionamento de assembly UDO</span><span class="sxs-lookup"><span data-stu-id="b2f09-240">Generate Udo assembly redirect config</span></span>|
|<span data-ttu-id="b2f09-241">-UseDatabase</span><span class="sxs-lookup"><span data-stu-id="b2f09-241">-UseDatabase</span></span>|<span data-ttu-id="b2f09-242">mestre</span><span class="sxs-lookup"><span data-stu-id="b2f09-242">master</span></span>|<span data-ttu-id="b2f09-243">Banco de dados a ser usado para registro do assembly temporário do code-behind</span><span class="sxs-lookup"><span data-stu-id="b2f09-243">Database to use for code behind temporary assembly registration</span></span>|
|<span data-ttu-id="b2f09-244">-Verbose</span><span class="sxs-lookup"><span data-stu-id="b2f09-244">-Verbose</span></span>|<span data-ttu-id="b2f09-245">Falso</span><span class="sxs-lookup"><span data-stu-id="b2f09-245">False</span></span>|<span data-ttu-id="b2f09-246">Mostrar saídas detalhadas do tempo de execução</span><span class="sxs-lookup"><span data-stu-id="b2f09-246">Show detailed outputs from runtime</span></span>|
|<span data-ttu-id="b2f09-247">-WorkDir</span><span class="sxs-lookup"><span data-stu-id="b2f09-247">-WorkDir</span></span>|<span data-ttu-id="b2f09-248">Diretório atual</span><span class="sxs-lookup"><span data-stu-id="b2f09-248">Current Directory</span></span>|<span data-ttu-id="b2f09-249">Diretório para uso do compilador e saídas</span><span class="sxs-lookup"><span data-stu-id="b2f09-249">Directory for compiler usage and outputs</span></span>|
|<span data-ttu-id="b2f09-250">-RunScopeCEP</span><span class="sxs-lookup"><span data-stu-id="b2f09-250">-RunScopeCEP</span></span>|<span data-ttu-id="b2f09-251">0</span><span class="sxs-lookup"><span data-stu-id="b2f09-251">0</span></span>|<span data-ttu-id="b2f09-252">Modo ScopeCEP a ser usado</span><span class="sxs-lookup"><span data-stu-id="b2f09-252">ScopeCEP mode to use</span></span>|
|<span data-ttu-id="b2f09-253">-ScopeCEPTempPath</span><span class="sxs-lookup"><span data-stu-id="b2f09-253">-ScopeCEPTempPath</span></span>|<span data-ttu-id="b2f09-254">temp</span><span class="sxs-lookup"><span data-stu-id="b2f09-254">temp</span></span>|<span data-ttu-id="b2f09-255">Caminho temporário a ser usado para transmissão de dados</span><span class="sxs-lookup"><span data-stu-id="b2f09-255">Temp path to use for streaming data</span></span>|
|<span data-ttu-id="b2f09-256">-OptFlags</span><span class="sxs-lookup"><span data-stu-id="b2f09-256">-OptFlags</span></span>| |<span data-ttu-id="b2f09-257">Lista separada por vírgula de sinalizadores do otimizador</span><span class="sxs-lookup"><span data-stu-id="b2f09-257">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="b2f09-258">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="b2f09-258">Here's an example:</span></span>

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

<span data-ttu-id="b2f09-259">Além de combinar **compile** e **execute**, é possível compilar e executar os executáveis compilados separadamente.</span><span class="sxs-lookup"><span data-stu-id="b2f09-259">Besides combining **compile** and **execute**, you can compile and execute the compiled executables separately.</span></span>

#### <a name="compile-a-u-sql-script"></a><span data-ttu-id="b2f09-260">Compilar um script U-SQL</span><span class="sxs-lookup"><span data-stu-id="b2f09-260">Compile a U-SQL script</span></span>

<span data-ttu-id="b2f09-261">O comando **compile** é usado para compilar um script U-SQL para executáveis.</span><span class="sxs-lookup"><span data-stu-id="b2f09-261">The **compile** command is used to compile a U-SQL script to executables.</span></span>

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="b2f09-262">Estes são os argumentos opcionais para **compile**:</span><span class="sxs-lookup"><span data-stu-id="b2f09-262">The following are optional arguments for **compile**:</span></span>


|<span data-ttu-id="b2f09-263">Argumento</span><span class="sxs-lookup"><span data-stu-id="b2f09-263">Argument</span></span>|<span data-ttu-id="b2f09-264">Descrição</span><span class="sxs-lookup"><span data-stu-id="b2f09-264">Description</span></span>|
|--------|-----------|
| <span data-ttu-id="b2f09-265">-CodeBehind [valor padrão 'False']</span><span class="sxs-lookup"><span data-stu-id="b2f09-265">-CodeBehind [default value 'False']</span></span>|<span data-ttu-id="b2f09-266">O script tem o code-behind .cs</span><span class="sxs-lookup"><span data-stu-id="b2f09-266">The script has .cs code behind</span></span>|
| <span data-ttu-id="b2f09-267">-CppSDK [valor padrão '']</span><span class="sxs-lookup"><span data-stu-id="b2f09-267">-CppSDK [default value '']</span></span>|<span data-ttu-id="b2f09-268">Diretório do CppSDK</span><span class="sxs-lookup"><span data-stu-id="b2f09-268">CppSDK Directory</span></span>|
| <span data-ttu-id="b2f09-269">-DataRoot [valor padrão “variável de ambiente DataRoot”]</span><span class="sxs-lookup"><span data-stu-id="b2f09-269">-DataRoot [default value 'DataRoot environment variable']</span></span>|<span data-ttu-id="b2f09-270">DataRoot para execução local, padrão para a variável de ambiente “LOCALRUN_DATAROOT”</span><span class="sxs-lookup"><span data-stu-id="b2f09-270">DataRoot for local run, default to 'LOCALRUN_DATAROOT' environment variable</span></span>|
| <span data-ttu-id="b2f09-271">-MessageOut [valor padrão '']</span><span class="sxs-lookup"><span data-stu-id="b2f09-271">-MessageOut [default value '']</span></span>|<span data-ttu-id="b2f09-272">Mensagens de despejo no console para um arquivo</span><span class="sxs-lookup"><span data-stu-id="b2f09-272">Dump messages on console to a file</span></span>|
| <span data-ttu-id="b2f09-273">-References [valor padrão '']</span><span class="sxs-lookup"><span data-stu-id="b2f09-273">-References [default value '']</span></span>|<span data-ttu-id="b2f09-274">Lista de caminhos para os assemblies de referência extra ou arquivos de dados do code-behind, separados por ';'</span><span class="sxs-lookup"><span data-stu-id="b2f09-274">List of paths to extra reference assemblies or data files of code behind, separated by ';'</span></span>|
| <span data-ttu-id="b2f09-275">-Shallow [valor padrão 'False']</span><span class="sxs-lookup"><span data-stu-id="b2f09-275">-Shallow [default value 'False']</span></span>|<span data-ttu-id="b2f09-276">Compilação superficial</span><span class="sxs-lookup"><span data-stu-id="b2f09-276">Shallow compile</span></span>|
| <span data-ttu-id="b2f09-277">-UdoRedirect [valor padrão 'False']</span><span class="sxs-lookup"><span data-stu-id="b2f09-277">-UdoRedirect [default value 'False']</span></span>|<span data-ttu-id="b2f09-278">Gerar configuração de redirecionamento de assembly UDO</span><span class="sxs-lookup"><span data-stu-id="b2f09-278">Generate Udo assembly redirect config</span></span>|
| <span data-ttu-id="b2f09-279">-UseDatabase [valor padrão 'master']</span><span class="sxs-lookup"><span data-stu-id="b2f09-279">-UseDatabase [default value 'master']</span></span>|<span data-ttu-id="b2f09-280">Banco de dados a ser usado para registro do assembly temporário do code-behind</span><span class="sxs-lookup"><span data-stu-id="b2f09-280">Database to use for code behind temporary assembly registration</span></span>|
| <span data-ttu-id="b2f09-281">-WorkDir [valor padrão “Diretório Atual”]</span><span class="sxs-lookup"><span data-stu-id="b2f09-281">-WorkDir [default value 'Current Directory']</span></span>|<span data-ttu-id="b2f09-282">Diretório para uso do compilador e saídas</span><span class="sxs-lookup"><span data-stu-id="b2f09-282">Directory for compiler usage and outputs</span></span>|
| <span data-ttu-id="b2f09-283">-RunScopeCEP [valor padrão “0”]</span><span class="sxs-lookup"><span data-stu-id="b2f09-283">-RunScopeCEP [default value '0']</span></span>|<span data-ttu-id="b2f09-284">Modo ScopeCEP a ser usado</span><span class="sxs-lookup"><span data-stu-id="b2f09-284">ScopeCEP mode to use</span></span>|
| <span data-ttu-id="b2f09-285">-ScopeCEPTempPath [valor padrão “temp”]</span><span class="sxs-lookup"><span data-stu-id="b2f09-285">-ScopeCEPTempPath [default value 'temp']</span></span>|<span data-ttu-id="b2f09-286">Caminho temporário a ser usado para transmissão de dados</span><span class="sxs-lookup"><span data-stu-id="b2f09-286">Temp path to use for streaming data</span></span>|
| <span data-ttu-id="b2f09-287">-OptFlags [valor padrão '']</span><span class="sxs-lookup"><span data-stu-id="b2f09-287">-OptFlags [default value '']</span></span>|<span data-ttu-id="b2f09-288">Lista separada por vírgula de sinalizadores do otimizador</span><span class="sxs-lookup"><span data-stu-id="b2f09-288">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="b2f09-289">Veja alguns exemplos de uso.</span><span class="sxs-lookup"><span data-stu-id="b2f09-289">Here are some usage examples.</span></span>

<span data-ttu-id="b2f09-290">Compilar um script U-SQL:</span><span class="sxs-lookup"><span data-stu-id="b2f09-290">Compile a U-SQL script:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql

<span data-ttu-id="b2f09-291">Compilar um script U-SQL e definir a pasta raiz de dados.</span><span class="sxs-lookup"><span data-stu-id="b2f09-291">Compile a U-SQL script and set the data-root folder.</span></span> <span data-ttu-id="b2f09-292">Observe que isso substituirá a variável de ambiente do conjunto.</span><span class="sxs-lookup"><span data-stu-id="b2f09-292">Note that this will overwrite the set environment variable.</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

<span data-ttu-id="b2f09-293">Compilar um script U-SQL e definir um diretório de trabalho, o assembly de referência e o banco de dados:</span><span class="sxs-lookup"><span data-stu-id="b2f09-293">Compile a U-SQL script and set a working directory, reference assembly, and database:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a><span data-ttu-id="b2f09-294">Executar resultados compilados</span><span class="sxs-lookup"><span data-stu-id="b2f09-294">Execute compiled results</span></span>

<span data-ttu-id="b2f09-295">O comando **execute** é usado para executar os resultados compilados.</span><span class="sxs-lookup"><span data-stu-id="b2f09-295">The **execute** command is used to execute compiled results.</span></span>   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

<span data-ttu-id="b2f09-296">Estes são os argumentos opcionais para **execute**:</span><span class="sxs-lookup"><span data-stu-id="b2f09-296">The following are optional arguments for **execute**:</span></span>

|<span data-ttu-id="b2f09-297">Argumento</span><span class="sxs-lookup"><span data-stu-id="b2f09-297">Argument</span></span>|<span data-ttu-id="b2f09-298">Descrição</span><span class="sxs-lookup"><span data-stu-id="b2f09-298">Description</span></span>|
|--------|-----------|
|<span data-ttu-id="b2f09-299">-DataRoot [valor padrão '']</span><span class="sxs-lookup"><span data-stu-id="b2f09-299">-DataRoot [default value '']</span></span>|<span data-ttu-id="b2f09-300">Raiz de dados para a execução de metadados.</span><span class="sxs-lookup"><span data-stu-id="b2f09-300">Data root for metadata execution.</span></span> <span data-ttu-id="b2f09-301">A variável de ambiente **LOCALRUN_DATAROOT** passa a ser o padrão.</span><span class="sxs-lookup"><span data-stu-id="b2f09-301">It defaults to the **LOCALRUN_DATAROOT** environment variable.</span></span>|
|<span data-ttu-id="b2f09-302">-MessageOut [valor padrão '']</span><span class="sxs-lookup"><span data-stu-id="b2f09-302">-MessageOut [default value '']</span></span>|<span data-ttu-id="b2f09-303">Despeje as mensagens do console em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="b2f09-303">Dump messages on the console to a file.</span></span>|
|<span data-ttu-id="b2f09-304">-Parallel [valor padrão '1']</span><span class="sxs-lookup"><span data-stu-id="b2f09-304">-Parallel [default value '1']</span></span>|<span data-ttu-id="b2f09-305">Indicador para executar as etapas de execução local geradas com o nível de paralelismo especificado.</span><span class="sxs-lookup"><span data-stu-id="b2f09-305">Indicator to run the generated local-run steps with the specified parallelism level.</span></span>|
|<span data-ttu-id="b2f09-306">-Verbose [valor padrão 'False']</span><span class="sxs-lookup"><span data-stu-id="b2f09-306">-Verbose [default value 'False']</span></span>|<span data-ttu-id="b2f09-307">Indicador para mostrar saídas detalhadas do tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="b2f09-307">Indicator to show detailed outputs from runtime.</span></span>|

<span data-ttu-id="b2f09-308">Aqui está um exemplo de uso:</span><span class="sxs-lookup"><span data-stu-id="b2f09-308">Here's a usage example:</span></span>

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5


## <a name="use-the-sdk-with-programming-interfaces"></a><span data-ttu-id="b2f09-309">Usar o SDK com interfaces de programação</span><span class="sxs-lookup"><span data-stu-id="b2f09-309">Use the SDK with programming interfaces</span></span>

<span data-ttu-id="b2f09-310">As interfaces de programação estão localizadas no LocalRunHelper.exe.</span><span class="sxs-lookup"><span data-stu-id="b2f09-310">The programming interfaces are all located in the LocalRunHelper.exe.</span></span> <span data-ttu-id="b2f09-311">Você pode usá-los para integrar a funcionalidade do SDK para U-SQL e a estrutura de teste C# a fim de dimensionar o teste local do script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="b2f09-311">You can use them to integrate the functionality of the U-SQL SDK and the C# test framework to scale your U-SQL script local test.</span></span> <span data-ttu-id="b2f09-312">Neste artigo, usarei o projeto de teste de unidade padrão do C# para mostrar como usar essas interfaces para testar o script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="b2f09-312">In this article, I will use the standard C# unit test project to show how to use these interfaces to test your U-SQL script.</span></span>

### <a name="step-1-create-c-unit-test-project-and-configuration"></a><span data-ttu-id="b2f09-313">Etapa 1: Criar o projeto de teste de unidade do C# e a configuração</span><span class="sxs-lookup"><span data-stu-id="b2f09-313">Step 1: Create C# unit test project and configuration</span></span>

- <span data-ttu-id="b2f09-314">Crie um projeto de teste de unidade do C# por meio de Arquivo > Novo > Projeto > Visual C# > Teste > Projeto de Teste de Unidade.</span><span class="sxs-lookup"><span data-stu-id="b2f09-314">Create a C# unit test project through File > New > Project > Visual C# > Test > Unit Test Project.</span></span>
- <span data-ttu-id="b2f09-315">Adicione LocalRunHelper.exe como uma referência do projeto.</span><span class="sxs-lookup"><span data-stu-id="b2f09-315">Add LocalRunHelper.exe as a reference for the project.</span></span> <span data-ttu-id="b2f09-316">O LocalRunHelper.exe está localizado em \build\runtime\LocalRunHelper.exe no pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="b2f09-316">The LocalRunHelper.exe is located at \build\runtime\LocalRunHelper.exe in Nuget package.</span></span>

    ![SDK do U-SQL do Azure Data Lake – Adicionar referência](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-add-reference.png)

- <span data-ttu-id="b2f09-318">O SDK do U-SQL dá suporte **apenas** ao ambiente x64; portanto, lembre-se de definir o destino da plataforma de build como x64.</span><span class="sxs-lookup"><span data-stu-id="b2f09-318">U-SQL SDK **only** support x64 environment, make sure to set build platform target as x64.</span></span> <span data-ttu-id="b2f09-319">É possível definir isso por meio de Propriedade do Projeto > Build > Destino da plataforma.</span><span class="sxs-lookup"><span data-stu-id="b2f09-319">You can set that through Project Property > Build > Platform target.</span></span>

    ![SDK do U-SQL do Azure Data Lake – Configurar projeto do x64](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-x64.png)

- <span data-ttu-id="b2f09-321">Lembre-se de definir o ambiente de teste como x64.</span><span class="sxs-lookup"><span data-stu-id="b2f09-321">Make sure to set your test environment as x64.</span></span> <span data-ttu-id="b2f09-322">No Visual Studio, é possível defini-lo por meio de Teste > Configurações de Teste > Arquitetura do Processador Padrão > x64.</span><span class="sxs-lookup"><span data-stu-id="b2f09-322">In Visual Studio, you can set it through Test > Test Settings > Default Processor Architecture > x64.</span></span>

    ![SDK do U-SQL do Azure Data Lake – Configurar ambiente de teste x64](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-test-x64.png)

- <span data-ttu-id="b2f09-324">Lembre-se de copiar todos os arquivos de dependência em NugetPackage\build\runtime\ para o diretório de trabalho do projeto que, normalmente, está em ProjectFolder\bin\x64\Debug.</span><span class="sxs-lookup"><span data-stu-id="b2f09-324">Make sure to copy all dependency files under NugetPackage\build\runtime\ to project working directory which is usually under ProjectFolder\bin\x64\Debug.</span></span>

### <a name="step-2-create-u-sql-script-test-case"></a><span data-ttu-id="b2f09-325">Etapa 2: Criar um caso de teste do script U-SQL</span><span class="sxs-lookup"><span data-stu-id="b2f09-325">Step 2: Create U-SQL script test case</span></span>

<span data-ttu-id="b2f09-326">Veja abaixo o código de exemplo para o teste de script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="b2f09-326">Below is the sample code for U-SQL script test.</span></span> <span data-ttu-id="b2f09-327">Para testar, você precisa preparar scripts, arquivos de entrada e os arquivos de saída esperados.</span><span class="sxs-lookup"><span data-stu-id="b2f09-327">For testing, you need to prepare scripts, input files and expected output files.</span></span>

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
                //Specify the local run message output path
                StreamWriter MessageOutput = new StreamWriter("../../../log.txt");

                LocalRunHelper localrun = new LocalRunHelper(MessageOutput);

                //Configure the DateRoot path, Script Path and CPPSDK path
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

                //Don't forget to close MessageOutput to get logs into file
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


### <a name="programming-interfaces-in-localrunhelperexe"></a><span data-ttu-id="b2f09-328">Interfaces de programação em LocalRunHelper.exe</span><span class="sxs-lookup"><span data-stu-id="b2f09-328">Programming interfaces in LocalRunHelper.exe</span></span>

<span data-ttu-id="b2f09-329">O LocalRunHelper.exe fornece as interfaces de programação para a compilação e execução locais do U-SQL, etc. As interfaces são listadas a seguir.</span><span class="sxs-lookup"><span data-stu-id="b2f09-329">LocalRunHelper.exe provides the programming interfaces for U-SQL local compile, run, etc. The interfaces are listed as follows.</span></span>

<span data-ttu-id="b2f09-330">**Construtor**</span><span class="sxs-lookup"><span data-stu-id="b2f09-330">**Constructor**</span></span>

<span data-ttu-id="b2f09-331">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span><span class="sxs-lookup"><span data-stu-id="b2f09-331">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span></span>

|<span data-ttu-id="b2f09-332">.</span><span class="sxs-lookup"><span data-stu-id="b2f09-332">Parameter</span></span>|<span data-ttu-id="b2f09-333">Tipo</span><span class="sxs-lookup"><span data-stu-id="b2f09-333">Type</span></span>|<span data-ttu-id="b2f09-334">Descrição</span><span class="sxs-lookup"><span data-stu-id="b2f09-334">Description</span></span>|
|---------|----|-----------|
|<span data-ttu-id="b2f09-335">messageOutput</span><span class="sxs-lookup"><span data-stu-id="b2f09-335">messageOutput</span></span>|<span data-ttu-id="b2f09-336">System.IO.TextWriter</span><span class="sxs-lookup"><span data-stu-id="b2f09-336">System.IO.TextWriter</span></span>|<span data-ttu-id="b2f09-337">para mensagens de saída, definido como nulo para usar o Console</span><span class="sxs-lookup"><span data-stu-id="b2f09-337">for output messages, set to null to use Console</span></span>|

<span data-ttu-id="b2f09-338">**Propriedades**</span><span class="sxs-lookup"><span data-stu-id="b2f09-338">**Properties**</span></span>

|<span data-ttu-id="b2f09-339">Propriedade</span><span class="sxs-lookup"><span data-stu-id="b2f09-339">Property</span></span>|<span data-ttu-id="b2f09-340">Tipo</span><span class="sxs-lookup"><span data-stu-id="b2f09-340">Type</span></span>|<span data-ttu-id="b2f09-341">Descrição</span><span class="sxs-lookup"><span data-stu-id="b2f09-341">Description</span></span>|
|--------|----|-----------|
|<span data-ttu-id="b2f09-342">AlgebraPath</span><span class="sxs-lookup"><span data-stu-id="b2f09-342">AlgebraPath</span></span>|<span data-ttu-id="b2f09-343">string</span><span class="sxs-lookup"><span data-stu-id="b2f09-343">string</span></span>|<span data-ttu-id="b2f09-344">O caminho para o arquivo de álgebra (o arquivo de álgebra é um dos resultados da compilação)</span><span class="sxs-lookup"><span data-stu-id="b2f09-344">The path to algebra file (algebra file is one of the compilation results)</span></span>|
|<span data-ttu-id="b2f09-345">CodeBehindReferences</span><span class="sxs-lookup"><span data-stu-id="b2f09-345">CodeBehindReferences</span></span>|<span data-ttu-id="b2f09-346">string</span><span class="sxs-lookup"><span data-stu-id="b2f09-346">string</span></span>|<span data-ttu-id="b2f09-347">Se o script tiver referências code-behind adicionais, especifique os caminhos separados por “;”</span><span class="sxs-lookup"><span data-stu-id="b2f09-347">If the script has additional code behind references, specify the paths separated with ';'</span></span>|
|<span data-ttu-id="b2f09-348">CppSdkDir</span><span class="sxs-lookup"><span data-stu-id="b2f09-348">CppSdkDir</span></span>|<span data-ttu-id="b2f09-349">string</span><span class="sxs-lookup"><span data-stu-id="b2f09-349">string</span></span>|<span data-ttu-id="b2f09-350">Diretório do CppSDK</span><span class="sxs-lookup"><span data-stu-id="b2f09-350">CppSDK directory</span></span>|
|<span data-ttu-id="b2f09-351">CurrentDir</span><span class="sxs-lookup"><span data-stu-id="b2f09-351">CurrentDir</span></span>|<span data-ttu-id="b2f09-352">string</span><span class="sxs-lookup"><span data-stu-id="b2f09-352">string</span></span>|<span data-ttu-id="b2f09-353">Diretório atual</span><span class="sxs-lookup"><span data-stu-id="b2f09-353">Current directory</span></span>|
|<span data-ttu-id="b2f09-354">DataRoot</span><span class="sxs-lookup"><span data-stu-id="b2f09-354">DataRoot</span></span>|<span data-ttu-id="b2f09-355">string</span><span class="sxs-lookup"><span data-stu-id="b2f09-355">string</span></span>|<span data-ttu-id="b2f09-356">Caminho da raiz de dados</span><span class="sxs-lookup"><span data-stu-id="b2f09-356">Data root path</span></span>|
|<span data-ttu-id="b2f09-357">DebuggerMailPath</span><span class="sxs-lookup"><span data-stu-id="b2f09-357">DebuggerMailPath</span></span>|<span data-ttu-id="b2f09-358">string</span><span class="sxs-lookup"><span data-stu-id="b2f09-358">string</span></span>|<span data-ttu-id="b2f09-359">O caminho para o slot de correio do depurador</span><span class="sxs-lookup"><span data-stu-id="b2f09-359">The path to debugger mailslot</span></span>|
|<span data-ttu-id="b2f09-360">GenerateUdoRedirect</span><span class="sxs-lookup"><span data-stu-id="b2f09-360">GenerateUdoRedirect</span></span>|<span data-ttu-id="b2f09-361">bool</span><span class="sxs-lookup"><span data-stu-id="b2f09-361">bool</span></span>|<span data-ttu-id="b2f09-362">Se quisermos gerar a configuração de substituição do redirecionamento de carregamento do assembly</span><span class="sxs-lookup"><span data-stu-id="b2f09-362">If we want to generate assembly loading redirection override config</span></span>|
|<span data-ttu-id="b2f09-363">HasCodeBehind</span><span class="sxs-lookup"><span data-stu-id="b2f09-363">HasCodeBehind</span></span>|<span data-ttu-id="b2f09-364">bool</span><span class="sxs-lookup"><span data-stu-id="b2f09-364">bool</span></span>|<span data-ttu-id="b2f09-365">Se o script tiver code-behind</span><span class="sxs-lookup"><span data-stu-id="b2f09-365">If the script has code behind</span></span>|
|<span data-ttu-id="b2f09-366">InputDir</span><span class="sxs-lookup"><span data-stu-id="b2f09-366">InputDir</span></span>|<span data-ttu-id="b2f09-367">string</span><span class="sxs-lookup"><span data-stu-id="b2f09-367">string</span></span>|<span data-ttu-id="b2f09-368">Diretório dos dados de entrada</span><span class="sxs-lookup"><span data-stu-id="b2f09-368">Directory for input data</span></span>|
|<span data-ttu-id="b2f09-369">MessagePath</span><span class="sxs-lookup"><span data-stu-id="b2f09-369">MessagePath</span></span>|<span data-ttu-id="b2f09-370">string</span><span class="sxs-lookup"><span data-stu-id="b2f09-370">string</span></span>|<span data-ttu-id="b2f09-371">Caminho do arquivo de despejo da mensagem</span><span class="sxs-lookup"><span data-stu-id="b2f09-371">Message dump file path</span></span>|
|<span data-ttu-id="b2f09-372">OutputDir</span><span class="sxs-lookup"><span data-stu-id="b2f09-372">OutputDir</span></span>|<span data-ttu-id="b2f09-373">string</span><span class="sxs-lookup"><span data-stu-id="b2f09-373">string</span></span>|<span data-ttu-id="b2f09-374">Diretório dos dados de saída</span><span class="sxs-lookup"><span data-stu-id="b2f09-374">Directory for output data</span></span>|
|<span data-ttu-id="b2f09-375">Paralelismo</span><span class="sxs-lookup"><span data-stu-id="b2f09-375">Parallelism</span></span>|<span data-ttu-id="b2f09-376">int</span><span class="sxs-lookup"><span data-stu-id="b2f09-376">int</span></span>|<span data-ttu-id="b2f09-377">Paralelismo para executar a álgebra</span><span class="sxs-lookup"><span data-stu-id="b2f09-377">Parallelism to run the algebra</span></span>|
|<span data-ttu-id="b2f09-378">ParentPid</span><span class="sxs-lookup"><span data-stu-id="b2f09-378">ParentPid</span></span>|<span data-ttu-id="b2f09-379">int</span><span class="sxs-lookup"><span data-stu-id="b2f09-379">int</span></span>|<span data-ttu-id="b2f09-380">PID do pai no qual o serviço monitora a saída, definido como 0 ou negativo para ignorar</span><span class="sxs-lookup"><span data-stu-id="b2f09-380">PID of the parent on which the service monitors to exit, set to 0 or negative to ignore</span></span>|
|<span data-ttu-id="b2f09-381">ResultPath</span><span class="sxs-lookup"><span data-stu-id="b2f09-381">ResultPath</span></span>|<span data-ttu-id="b2f09-382">string</span><span class="sxs-lookup"><span data-stu-id="b2f09-382">string</span></span>|<span data-ttu-id="b2f09-383">Caminho do arquivo de despejo do resultado</span><span class="sxs-lookup"><span data-stu-id="b2f09-383">Result dump file path</span></span>|
|<span data-ttu-id="b2f09-384">RuntimeDir</span><span class="sxs-lookup"><span data-stu-id="b2f09-384">RuntimeDir</span></span>|<span data-ttu-id="b2f09-385">string</span><span class="sxs-lookup"><span data-stu-id="b2f09-385">string</span></span>|<span data-ttu-id="b2f09-386">Diretório do tempo de execução</span><span class="sxs-lookup"><span data-stu-id="b2f09-386">Runtime directory</span></span>|
|<span data-ttu-id="b2f09-387">ScriptPath</span><span class="sxs-lookup"><span data-stu-id="b2f09-387">ScriptPath</span></span>|<span data-ttu-id="b2f09-388">string</span><span class="sxs-lookup"><span data-stu-id="b2f09-388">string</span></span>|<span data-ttu-id="b2f09-389">Local em que o script pode ser encontrado</span><span class="sxs-lookup"><span data-stu-id="b2f09-389">Where to find the script</span></span>|
|<span data-ttu-id="b2f09-390">Shallow</span><span class="sxs-lookup"><span data-stu-id="b2f09-390">Shallow</span></span>|<span data-ttu-id="b2f09-391">bool</span><span class="sxs-lookup"><span data-stu-id="b2f09-391">bool</span></span>|<span data-ttu-id="b2f09-392">Compilação superficial ou não</span><span class="sxs-lookup"><span data-stu-id="b2f09-392">Shallow compile or not</span></span>|
|<span data-ttu-id="b2f09-393">TempDir</span><span class="sxs-lookup"><span data-stu-id="b2f09-393">TempDir</span></span>|<span data-ttu-id="b2f09-394">string</span><span class="sxs-lookup"><span data-stu-id="b2f09-394">string</span></span>|<span data-ttu-id="b2f09-395">Diretório temporário</span><span class="sxs-lookup"><span data-stu-id="b2f09-395">Temp directory</span></span>|
|<span data-ttu-id="b2f09-396">UseDataBase</span><span class="sxs-lookup"><span data-stu-id="b2f09-396">UseDataBase</span></span>|<span data-ttu-id="b2f09-397">string</span><span class="sxs-lookup"><span data-stu-id="b2f09-397">string</span></span>|<span data-ttu-id="b2f09-398">Especifique o banco de dados a ser usado para o registro de assembly temporário code-behind, mestre por padrão</span><span class="sxs-lookup"><span data-stu-id="b2f09-398">Specify the database to use for code behind temporary assembly registration, master by default</span></span>|
|<span data-ttu-id="b2f09-399">WorkDir</span><span class="sxs-lookup"><span data-stu-id="b2f09-399">WorkDir</span></span>|<span data-ttu-id="b2f09-400">string</span><span class="sxs-lookup"><span data-stu-id="b2f09-400">string</span></span>|<span data-ttu-id="b2f09-401">Diretório de trabalho preferencial</span><span class="sxs-lookup"><span data-stu-id="b2f09-401">Preferred working directory</span></span>|


<span data-ttu-id="b2f09-402">**Método**</span><span class="sxs-lookup"><span data-stu-id="b2f09-402">**Method**</span></span>

|<span data-ttu-id="b2f09-403">Método</span><span class="sxs-lookup"><span data-stu-id="b2f09-403">Method</span></span>|<span data-ttu-id="b2f09-404">Descrição</span><span class="sxs-lookup"><span data-stu-id="b2f09-404">Description</span></span>|<span data-ttu-id="b2f09-405">Retorno</span><span class="sxs-lookup"><span data-stu-id="b2f09-405">Return</span></span>|<span data-ttu-id="b2f09-406">.</span><span class="sxs-lookup"><span data-stu-id="b2f09-406">Parameter</span></span>|
|------|-----------|------|---------|
|<span data-ttu-id="b2f09-407">public bool DoCompile()</span><span class="sxs-lookup"><span data-stu-id="b2f09-407">public bool DoCompile()</span></span>|<span data-ttu-id="b2f09-408">Compilar o script U-SQL</span><span class="sxs-lookup"><span data-stu-id="b2f09-408">Compile the U-SQL script</span></span>|<span data-ttu-id="b2f09-409">Verdadeiro se tiver êxito</span><span class="sxs-lookup"><span data-stu-id="b2f09-409">True on success</span></span>| |
|<span data-ttu-id="b2f09-410">public bool DoExec()</span><span class="sxs-lookup"><span data-stu-id="b2f09-410">public bool DoExec()</span></span>|<span data-ttu-id="b2f09-411">Executar o resultado compilado</span><span class="sxs-lookup"><span data-stu-id="b2f09-411">Execute the compiled result</span></span>|<span data-ttu-id="b2f09-412">Verdadeiro se tiver êxito</span><span class="sxs-lookup"><span data-stu-id="b2f09-412">True on success</span></span>| |
|<span data-ttu-id="b2f09-413">public bool DoRun()</span><span class="sxs-lookup"><span data-stu-id="b2f09-413">public bool DoRun()</span></span>|<span data-ttu-id="b2f09-414">Executar o script U-SQL (Compilar + Executar)</span><span class="sxs-lookup"><span data-stu-id="b2f09-414">Run the U-SQL script (Compile + Execute)</span></span>|<span data-ttu-id="b2f09-415">Verdadeiro se tiver êxito</span><span class="sxs-lookup"><span data-stu-id="b2f09-415">True on success</span></span>| |
|<span data-ttu-id="b2f09-416">public bool IsValidRuntimeDir(string path)</span><span class="sxs-lookup"><span data-stu-id="b2f09-416">public bool IsValidRuntimeDir(string path)</span></span>|<span data-ttu-id="b2f09-417">Verificar se o caminho fornecido é um caminho de tempo de execução válido</span><span class="sxs-lookup"><span data-stu-id="b2f09-417">Check if the given path is valid runtime path</span></span>|<span data-ttu-id="b2f09-418">Verdadeiro para válido</span><span class="sxs-lookup"><span data-stu-id="b2f09-418">True for valid</span></span>|<span data-ttu-id="b2f09-419">O caminho do diretório de tempo de execução</span><span class="sxs-lookup"><span data-stu-id="b2f09-419">The path of runtime directory</span></span>|


## <a name="faq-about-common-issue"></a><span data-ttu-id="b2f09-420">Perguntas frequentes sobre um problema comum</span><span class="sxs-lookup"><span data-stu-id="b2f09-420">FAQ about common issue</span></span>

### <a name="error-1"></a><span data-ttu-id="b2f09-421">Erro 1:</span><span class="sxs-lookup"><span data-stu-id="b2f09-421">Error 1:</span></span>
<span data-ttu-id="b2f09-422">E_CSC_SYSTEM_INTERNAL: Erro interno.</span><span class="sxs-lookup"><span data-stu-id="b2f09-422">E_CSC_SYSTEM_INTERNAL: Internal error!</span></span> <span data-ttu-id="b2f09-423">Não foi possível carregar o arquivo ou o assembly “ScopeEngineManaged.dll” ou uma de suas dependências.</span><span class="sxs-lookup"><span data-stu-id="b2f09-423">Could not load file or assembly 'ScopeEngineManaged.dll' or one of its dependencies.</span></span> <span data-ttu-id="b2f09-424">O módulo especificado não pôde ser encontrado.</span><span class="sxs-lookup"><span data-stu-id="b2f09-424">The specified module could not be found.</span></span>

<span data-ttu-id="b2f09-425">Verifique o seguinte:</span><span class="sxs-lookup"><span data-stu-id="b2f09-425">Please check the following:</span></span>

- <span data-ttu-id="b2f09-426">Verifique se você tem o ambiente x64.</span><span class="sxs-lookup"><span data-stu-id="b2f09-426">Make sure you have x64 environment.</span></span> <span data-ttu-id="b2f09-427">A plataforma de destino do build e o ambiente de teste devem ser x64; consulte **Etapa 1: Criar configuração e projeto de teste de unidade do C#** acima.</span><span class="sxs-lookup"><span data-stu-id="b2f09-427">The build target platform and the test environment should be x64, refer to **Step 1: Create C# unit test project and configuration** above.</span></span>
- <span data-ttu-id="b2f09-428">Verifique se você copiou todos os arquivos de dependência em NugetPackage\build\runtime\ para o diretório de trabalho do projeto.</span><span class="sxs-lookup"><span data-stu-id="b2f09-428">Make sure you have copied all dependency files under NugetPackage\build\runtime\ to project working directory.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b2f09-429">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b2f09-429">Next steps</span></span>

* <span data-ttu-id="b2f09-430">Para aprender a usar o U-SQL, veja [Introdução à linguagem U-SQL da Análise do Azure Data Lake](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b2f09-430">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="b2f09-431">Para registrar em log as informações de diagnóstico, veja [Acessando os logs de diagnóstico para o Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="b2f09-431">To log diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span></span>
* <span data-ttu-id="b2f09-432">Para ver uma consulta mais complexa, consulte [Analisar logs de site usando o Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="b2f09-432">To see a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="b2f09-433">Para ver detalhes do trabalho, confira [Usar o Navegador de Trabalhos e o Modo de Exibição de Trabalho para trabalhos do Azure Data Lake Analytics](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="b2f09-433">To view job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="b2f09-434">Para usar o modo de exibição de execução de vértice, veja [Usar o Modo de Exibição de Execução de Vértice nas Ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="b2f09-434">To use the vertex execution view, see [Use the Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
