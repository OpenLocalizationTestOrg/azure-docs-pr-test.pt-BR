---
title: 'Ferramentas do Azure Data Lake: Usar as Ferramentas do Azure Data Lake para Visual Studio Code | Microsoft Docs'
description: 'Saiba como toouse Azure Data Lake Tools para Visual Studio Code toocreate, testar e executar scripts U-SQL. '
Keywords: "O VScode, ferramentas do Azure Data Lake, execução, depuração Local, locais de depuração, visualizar o arquivo de armazenamento, Local carregar toostorage caminho"
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: 77771c5d5dae3bfce4ad2df240ea6c6ef848f288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a><span data-ttu-id="73e28-104">Usar as Ferramentas do Azure Data Lake para Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="73e28-104">Use Azure Data Lake Tools for Visual Studio Code</span></span>

<span data-ttu-id="73e28-105">Saiba como toouse Azure Data Lake Tools para o código do Visual Studio (VS código) toocreate, testar e executar scripts U-SQL.</span><span class="sxs-lookup"><span data-stu-id="73e28-105">Learn how toouse Azure Data Lake Tools for Visual Studio Code (VS Code) toocreate, test, and run U-SQL scripts.</span></span> <span data-ttu-id="73e28-106">também são abordadas informações Olá Olá vídeo a seguir:</span><span class="sxs-lookup"><span data-stu-id="73e28-106">hello information is also covered in hello following video:</span></span>

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a><span data-ttu-id="73e28-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="73e28-107">Prerequisites</span></span>

<span data-ttu-id="73e28-108">Data Lake Tools pode ser instalado em plataformas de saudação aceitas pelo código do VS.</span><span class="sxs-lookup"><span data-stu-id="73e28-108">Data Lake Tools can be installed on hello platforms supported by VS Code.</span></span> <span data-ttu-id="73e28-109">plataformas de saudação com suporte incluem Windows, Linux e MacOS.</span><span class="sxs-lookup"><span data-stu-id="73e28-109">hello supported platforms include Windows, Linux, and MacOS.</span></span> <span data-ttu-id="73e28-110">plataformas diferentes Olá têm Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="73e28-110">hello different platforms have hello following prerequisites:</span></span>

- <span data-ttu-id="73e28-111">Windows</span><span class="sxs-lookup"><span data-stu-id="73e28-111">Windows</span></span>

    - <span data-ttu-id="73e28-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="73e28-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="73e28-113">[Java SE Runtime Environment versão 8 atualização 77 ou posterior](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="73e28-113">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="73e28-114">Adicione Olá java.exe caminho toohello ambiente variável caminho do sistema.</span><span class="sxs-lookup"><span data-stu-id="73e28-114">Add hello java.exe path toohello system environment variable path.</span></span> <span data-ttu-id="73e28-115">Para obter instruções de configuração, consulte [como definir ou alterar a variável de sistema Path Olá?]( https://www.java.com/download/help/path.xml).</span><span class="sxs-lookup"><span data-stu-id="73e28-115">For configuration instructions, see [How do I set or change hello Path system variable?]( https://www.java.com/download/help/path.xml).</span></span> <span data-ttu-id="73e28-116">caminho de saudação é tooC:\Program Files\Java\jdk1.8.0_77\jre\bin semelhante.</span><span class="sxs-lookup"><span data-stu-id="73e28-116">hello path is similar tooC:\Program Files\Java\jdk1.8.0_77\jre\bin.</span></span>
    - <span data-ttu-id="73e28-117">[Tempo de execução do SDK do .NET Core 1.0.3 ou do .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="73e28-117">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
    
- <span data-ttu-id="73e28-118">Linux (é recomendável o Ubuntu 14.04 LTS)</span><span class="sxs-lookup"><span data-stu-id="73e28-118">Linux (We recommend Ubuntu 14.04 LTS)</span></span>

    - <span data-ttu-id="73e28-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="73e28-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span> <span data-ttu-id="73e28-120">tooinstall Olá código, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="73e28-120">tooinstall hello code, enter hello following command:</span></span>

              sudo dpkg -i code_<version_number>_amd64.deb

    - <span data-ttu-id="73e28-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span><span class="sxs-lookup"><span data-stu-id="73e28-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span></span> 

        - <span data-ttu-id="73e28-122">pacotes de deb Olá tooupdate de origem, digite Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="73e28-122">tooupdate hello deb package source, enter hello following commands:</span></span>

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - <span data-ttu-id="73e28-123">tooinstall Mono, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="73e28-123">tooinstall Mono, enter hello following command:</span></span>

                sudo apt-get install mono-complete

            > [!NOTE] 
            > <span data-ttu-id="73e28-124">Não há suporte para o Mono 4.6.</span><span class="sxs-lookup"><span data-stu-id="73e28-124">Mono 4.6 is not supported.</span></span> <span data-ttu-id="73e28-125">Desinstale totalmente a versão 4.6 antes de instalar a versão 4.2.x.</span><span class="sxs-lookup"><span data-stu-id="73e28-125">Uninstall version 4.6 entirely before you install 4.2.x.</span></span>  

        - <span data-ttu-id="73e28-126">[Java SE Runtime Environment versão 8 atualização 77 ou posterior](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="73e28-126">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="73e28-127">Para obter instruções sobre instalação, consulte Olá [instruções de instalação do Linux de 64 bits para Java]( https://java.com/en/download/help/linux_x64_install.xml) página.</span><span class="sxs-lookup"><span data-stu-id="73e28-127">For instructions on installation, see hello [Linux 64-bit installation instructions for Java]( https://java.com/en/download/help/linux_x64_install.xml) page.</span></span>
        - <span data-ttu-id="73e28-128">[Tempo de execução do SDK do .NET Core 1.0.3 ou do .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="73e28-128">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
- <span data-ttu-id="73e28-129">MacOS</span><span class="sxs-lookup"><span data-stu-id="73e28-129">MacOS</span></span>

    - <span data-ttu-id="73e28-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="73e28-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="73e28-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span><span class="sxs-lookup"><span data-stu-id="73e28-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span></span> 
    - <span data-ttu-id="73e28-132">[Java SE Runtime Environment versão 8 atualização 77 ou posterior](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="73e28-132">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="73e28-133">Para obter instruções sobre instalação, consulte Olá [instruções de instalação do Linux de 64 bits para Java](https://java.com/en/download/help/mac_install.xml) página.</span><span class="sxs-lookup"><span data-stu-id="73e28-133">For instructions on installation, see hello [Linux 64-bit installation instructions for Java](https://java.com/en/download/help/mac_install.xml) page.</span></span>
    - <span data-ttu-id="73e28-134">[Tempo de execução do SDK do .NET Core 1.0.3 ou do .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="73e28-134">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>

## <a name="install-data-lake-tools"></a><span data-ttu-id="73e28-135">Instalar as Ferramentas do Data Lake</span><span class="sxs-lookup"><span data-stu-id="73e28-135">Install Data Lake Tools</span></span>

<span data-ttu-id="73e28-136">Depois de instalar os pré-requisitos do hello, você pode instalar o Data Lake Tools para o código do VS.</span><span class="sxs-lookup"><span data-stu-id="73e28-136">After you install hello prerequisites, you can install Data Lake Tools for VS Code.</span></span>

<span data-ttu-id="73e28-137">**tooinstall Data Lake Tools**</span><span class="sxs-lookup"><span data-stu-id="73e28-137">**tooinstall Data Lake Tools**</span></span>

1. <span data-ttu-id="73e28-138">Abra o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="73e28-138">Open Visual Studio Code.</span></span>
2. <span data-ttu-id="73e28-139">Selecione Ctrl + P e, em seguida, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="73e28-139">Select Ctrl+P, and then enter hello following command:</span></span>
```
ext install usql-vscode-ext
```
<span data-ttu-id="73e28-140">Você pode ver uma lista de extensões de código do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="73e28-140">You can see a list of Visual Studio code extensions.</span></span> <span data-ttu-id="73e28-141">Por exemplo, as **Ferramentas do Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="73e28-141">One of them is **Azure Data Lake Tools**.</span></span>

3. <span data-ttu-id="73e28-142">Selecione **instalar** Avançar muito**ferramentas do Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="73e28-142">Select **Install** next too**Azure Data Lake Tools**.</span></span> <span data-ttu-id="73e28-143">Depois de alguns segundos, Olá **instalar** botão alterações muito**recarregar**.</span><span class="sxs-lookup"><span data-stu-id="73e28-143">After a few seconds, hello **Install** button changes too**Reload**.</span></span>
4. <span data-ttu-id="73e28-144">Selecione **recarregar** tooactivate extensão de saudação.</span><span class="sxs-lookup"><span data-stu-id="73e28-144">Select **Reload** tooactivate hello extension.</span></span>
5. <span data-ttu-id="73e28-145">Selecione **Okey** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="73e28-145">Select **OK** tooconfirm.</span></span> <span data-ttu-id="73e28-146">Você pode ver o Azure Data Lake Tools no hello **extensões** painel.</span><span class="sxs-lookup"><span data-stu-id="73e28-146">You can see Azure Data Lake Tools in hello **Extensions** pane.</span></span>
    <span data-ttu-id="73e28-147">![Painel de Extensões das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span><span class="sxs-lookup"><span data-stu-id="73e28-147">![Data Lake Tools for Visual Studio Code Extensions pane](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span></span>

## <a name="activate-azure-data-lake-tools"></a><span data-ttu-id="73e28-148">Ativar Ferramentas do Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="73e28-148">Activate Azure Data Lake Tools</span></span>
<span data-ttu-id="73e28-149">Crie um novo arquivo .usql ou abra existente .usql tooactivate Olá extensão de arquivo.</span><span class="sxs-lookup"><span data-stu-id="73e28-149">Create a new .usql file or open an existing .usql file tooactivate hello extension.</span></span> 

## <a name="connect-tooazure"></a><span data-ttu-id="73e28-150">Conecte-se tooAzure</span><span class="sxs-lookup"><span data-stu-id="73e28-150">Connect tooAzure</span></span>

<span data-ttu-id="73e28-151">Antes de compilar e executar scripts U-SQL na análise Data Lake, você deve conectar tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="73e28-151">Before you can compile and run U-SQL scripts in Data Lake Analytics, you must connect tooyour Azure account.</span></span>

<span data-ttu-id="73e28-152">**tooconnect tooAzure**</span><span class="sxs-lookup"><span data-stu-id="73e28-152">**tooconnect tooAzure**</span></span>

1.  <span data-ttu-id="73e28-153">Selecione Ctrl + Shift + P tooopen Olá comando paleta.</span><span class="sxs-lookup"><span data-stu-id="73e28-153">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2.  <span data-ttu-id="73e28-154">Digite **ADL: Logon**.</span><span class="sxs-lookup"><span data-stu-id="73e28-154">Enter **ADL: Login**.</span></span> <span data-ttu-id="73e28-155">informações de logon de saudação aparecem no hello **saída** painel.</span><span class="sxs-lookup"><span data-stu-id="73e28-155">hello login information appears in hello **Output** pane.</span></span>

    <span data-ttu-id="73e28-156">![Paleta de comandos das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![Informações de logon do dispositivo das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span><span class="sxs-lookup"><span data-stu-id="73e28-156">![Data Lake Tools for Visual Studio Code command palette](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
![Data Lake Tools for Visual Studio Code device login information](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span></span>
3. <span data-ttu-id="73e28-157">Selecione Ctrl + clique na URL de logon Olá: https://aka.ms/devicelogin tooopen Olá logon página da Web.</span><span class="sxs-lookup"><span data-stu-id="73e28-157">Select Ctrl+click on hello login URL: https://aka.ms/devicelogin tooopen hello login webpage.</span></span> <span data-ttu-id="73e28-158">Insira o código de saudação **G567LX42V** na caixa de texto de saudação e selecione **continuar**.</span><span class="sxs-lookup"><span data-stu-id="73e28-158">Enter hello code **G567LX42V** into hello text box, and then select **Continue**.</span></span>

   ![Ferramentas do Data Lake para Visual Studio Code colar código de logon](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  <span data-ttu-id="73e28-160">Siga Olá instruções toosign do hello página da Web.</span><span class="sxs-lookup"><span data-stu-id="73e28-160">Follow hello instructions toosign in from hello webpage.</span></span> <span data-ttu-id="73e28-161">Quando você estiver conectado, o nome da sua conta do Azure aparece na barra de status de Olá no canto inferior esquerdo Olá Olá **código VS** janela.</span><span class="sxs-lookup"><span data-stu-id="73e28-161">When you're connected, your Azure account name appears on hello status bar in hello lower-left corner of hello **VS Code** window.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="73e28-162">Se sua conta tiver a autenticação por dois fatores habilitada, recomendamos o uso da autenticação por telefone em vez de usar um PIN.</span><span class="sxs-lookup"><span data-stu-id="73e28-162">If your account has two factors enabled, we recommend that you use phone authentication rather than using a PIN.</span></span>

<span data-ttu-id="73e28-163">toosign, digite o comando Olá **publicitário: Logout**.</span><span class="sxs-lookup"><span data-stu-id="73e28-163">toosign out, enter hello command **ADL: Logout**.</span></span>

## <a name="list-your-data-lake-analytics-accounts"></a><span data-ttu-id="73e28-164">Listar suas contas do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="73e28-164">List your Data Lake Analytics accounts</span></span>

<span data-ttu-id="73e28-165">conexão de saudação tootest, obtenha uma lista de suas contas da análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="73e28-165">tootest hello connection, get a list of your Data Lake Analytics accounts.</span></span>

<span data-ttu-id="73e28-166">**contas de análise Data Lake Olá toolist em sua assinatura do Azure**</span><span class="sxs-lookup"><span data-stu-id="73e28-166">**toolist hello Data Lake Analytics accounts under your Azure subscription**</span></span>

1. <span data-ttu-id="73e28-167">Selecione Ctrl + Shift + P tooopen Olá comando paleta.</span><span class="sxs-lookup"><span data-stu-id="73e28-167">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2. <span data-ttu-id="73e28-168">Insira **ADL: List Accounts**.</span><span class="sxs-lookup"><span data-stu-id="73e28-168">Enter **ADL: List Accounts**.</span></span> <span data-ttu-id="73e28-169">contas de saudação aparecem no hello **saída** painel.</span><span class="sxs-lookup"><span data-stu-id="73e28-169">hello accounts appear in hello **Output** pane.</span></span>

## <a name="open-hello-sample-script"></a><span data-ttu-id="73e28-170">Script de exemplo hello aberto</span><span class="sxs-lookup"><span data-stu-id="73e28-170">Open hello sample script</span></span>
<span data-ttu-id="73e28-171">Abra a paleta de comando hello (Ctrl + Shift + P) e digite **publicitário: abrir o Script de exemplo**.</span><span class="sxs-lookup"><span data-stu-id="73e28-171">Open hello command palette (Ctrl+Shift+P) and enter **ADL: Open Sample Script**.</span></span> <span data-ttu-id="73e28-172">Isso abre outra instância deste exemplo.</span><span class="sxs-lookup"><span data-stu-id="73e28-172">This opens another instance of this sample.</span></span> <span data-ttu-id="73e28-173">Você também pode editar, configurar e enviar o script nessa instância.</span><span class="sxs-lookup"><span data-stu-id="73e28-173">You can also edit, configure, and submit script on this instance.</span></span>

## <a name="work-with-u-sql"></a><span data-ttu-id="73e28-174">Trabalhar com o U-SQL</span><span class="sxs-lookup"><span data-stu-id="73e28-174">Work with U-SQL</span></span>

<span data-ttu-id="73e28-175">Você precisa abrir um arquivo U-SQL ou uma pasta toowork com U-SQL.</span><span class="sxs-lookup"><span data-stu-id="73e28-175">You need open either a U-SQL file or a folder toowork with U-SQL.</span></span>

<span data-ttu-id="73e28-176">**tooopen uma pasta para o seu projeto U-SQL**</span><span class="sxs-lookup"><span data-stu-id="73e28-176">**tooopen a folder for your U-SQL project**</span></span>

1. <span data-ttu-id="73e28-177">No código do Visual Studio, selecione Olá **arquivo** menu e, em seguida, selecione **Abrir pasta**.</span><span class="sxs-lookup"><span data-stu-id="73e28-177">From Visual Studio Code, select hello **File** menu, and then select **Open Folder**.</span></span>
2. <span data-ttu-id="73e28-178">Especifique uma pasta e selecione **Selecionar Pasta**.</span><span class="sxs-lookup"><span data-stu-id="73e28-178">Specify a folder, and then select **Select Folder**.</span></span>
3. <span data-ttu-id="73e28-179">Selecione Olá **arquivo** menu e, em seguida, selecione **novo**.</span><span class="sxs-lookup"><span data-stu-id="73e28-179">Select hello **File** menu, and then select **New**.</span></span> <span data-ttu-id="73e28-180">Um arquivo sem título 1 é adicionado toohello projeto.</span><span class="sxs-lookup"><span data-stu-id="73e28-180">An Untitled-1 file is added toohello project.</span></span>
4. <span data-ttu-id="73e28-181">Digite hello código a seguir no arquivo hello sem título 1:</span><span class="sxs-lookup"><span data-stu-id="73e28-181">Enter hello following code into hello Untitled-1 file:</span></span>

        @departments  = 
            SELECT * FROM 
                (VALUES
                    (31,    "Sales"),
                    (33,    "Engineering"), 
                    (34,    "Clerical"),
                    (35,    "Marketing")
                ) AS 
                      D( DepID, DepName );
         
        OUTPUT @departments
            TO “/Output/departments.csv”

    <span data-ttu-id="73e28-182">script Hello cria um arquivo de departments.csv com alguns dados incluídos na pasta de /output hello.</span><span class="sxs-lookup"><span data-stu-id="73e28-182">hello script creates a departments.csv file with some data included in hello /output folder.</span></span>

5. <span data-ttu-id="73e28-183">Salve o arquivo hello como **myUSQL.usql** em Olá aberto na pasta.</span><span class="sxs-lookup"><span data-stu-id="73e28-183">Save hello file as **myUSQL.usql** in hello opened folder.</span></span> <span data-ttu-id="73e28-184">Um arquivo de configuração adltools_settings.json também é adicionado toohello projeto.</span><span class="sxs-lookup"><span data-stu-id="73e28-184">A adltools_settings.json configuration file is also added toohello project.</span></span>
4. <span data-ttu-id="73e28-185">Abrir e configurar adltools_settings.json com hello propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="73e28-185">Open and configure adltools_settings.json with hello following properties:</span></span>

    - <span data-ttu-id="73e28-186">Conta: uma conta do Data Lake Analytics na sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="73e28-186">Account:  A Data Lake Analytics account under your Azure subscription.</span></span>
    - <span data-ttu-id="73e28-187">Banco de dados: um banco de dados em sua conta.</span><span class="sxs-lookup"><span data-stu-id="73e28-187">Database: A database under your account.</span></span> <span data-ttu-id="73e28-188">saudação padrão é **mestre**.</span><span class="sxs-lookup"><span data-stu-id="73e28-188">hello default is **master**.</span></span>
    - <span data-ttu-id="73e28-189">Esquema: um esquema em seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="73e28-189">Schema: A schema under your database.</span></span> <span data-ttu-id="73e28-190">saudação padrão é **dbo**.</span><span class="sxs-lookup"><span data-stu-id="73e28-190">hello default is **dbo**.</span></span>
    - <span data-ttu-id="73e28-191">Configurações opcionais:</span><span class="sxs-lookup"><span data-stu-id="73e28-191">Optional settings:</span></span>
        - <span data-ttu-id="73e28-192">Prioridade: intervalo de prioridade de saudação é de 1 too1000 com 1 prioridade mais alta hello.</span><span class="sxs-lookup"><span data-stu-id="73e28-192">Priority: hello priority range is from 1 too1000 with 1 as hello highest priority.</span></span> <span data-ttu-id="73e28-193">valor padrão de saudação é **1000**.</span><span class="sxs-lookup"><span data-stu-id="73e28-193">hello default value is **1000**.</span></span>
        - <span data-ttu-id="73e28-194">Paralelismo: intervalo de paralelismo de saudação é de 1 too150.</span><span class="sxs-lookup"><span data-stu-id="73e28-194">Parallelism: hello parallelism range is from 1 too150.</span></span> <span data-ttu-id="73e28-195">valor padrão de saudação é permitido em sua conta da análise Azure Data Lake máximo de paralelismo do hello.</span><span class="sxs-lookup"><span data-stu-id="73e28-195">hello default value is hello maximum parallelism allowed in your Azure Data Lake Analytics account.</span></span> 
        
        > [!NOTE] 
        > <span data-ttu-id="73e28-196">Se as configurações de saudação são inválidas, são usados valores padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="73e28-196">If hello settings are invalid, hello default values are used.</span></span>

    ![Arquivo de configuração das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    <span data-ttu-id="73e28-198">Uma conta da análise Data Lake é de computação necessária toocompile e executar trabalhos de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="73e28-198">A compute Data Lake Analytics account is needed toocompile and run U-SQL jobs.</span></span> <span data-ttu-id="73e28-199">Você deve configurar a conta de computador Olá antes de compilar e executar trabalhos de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="73e28-199">You must configure hello computer account before you can compile and run U-SQL jobs.</span></span>
    
<span data-ttu-id="73e28-200">Após salva configuração hello, informações de conta, o banco de dados e o esquema de saudação aparecem na barra de status de saudação no canto inferior esquerdo de saudação do arquivo correspondente de .usql hello.</span><span class="sxs-lookup"><span data-stu-id="73e28-200">After hello configuration is saved, hello account, database, and schema information appears on hello status bar at hello bottom-left corner of hello corresponding .usql file.</span></span> 
 
 
<span data-ttu-id="73e28-201">Tooopening em comparação com um arquivo, quando você abrir uma pasta que você pode:</span><span class="sxs-lookup"><span data-stu-id="73e28-201">Compared tooopening a file, when you open a folder you can:</span></span>

- <span data-ttu-id="73e28-202">Usar um arquivo code-behind.</span><span class="sxs-lookup"><span data-stu-id="73e28-202">Use a code-behind file.</span></span> <span data-ttu-id="73e28-203">No modo de arquivo único hello, não é suportado por trás do código.</span><span class="sxs-lookup"><span data-stu-id="73e28-203">In hello single-file mode, code-behind is not supported.</span></span>
- <span data-ttu-id="73e28-204">Usar um arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="73e28-204">Use a configuration file.</span></span> <span data-ttu-id="73e28-205">Quando você abrir uma pasta, scripts Olá Olá pasta de trabalho compartilham um único arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="73e28-205">When you open a folder, hello scripts in hello working folder share a single configuration file.</span></span>


<span data-ttu-id="73e28-206">Olá script U-SQL compila remotamente por meio de saudação serviço de análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="73e28-206">hello U-SQL script compiles remotely through hello Data Lake Analytics service.</span></span> <span data-ttu-id="73e28-207">Quando você emitir Olá **compilar** o comando, a conta de análise Data Lake tooyour de saudação script U-SQL é enviada.</span><span class="sxs-lookup"><span data-stu-id="73e28-207">When you issue hello **compile** command, hello U-SQL script is sent tooyour Data Lake Analytics account.</span></span> <span data-ttu-id="73e28-208">Posteriormente, o código do Visual Studio recebe o resultado da compilação hello.</span><span class="sxs-lookup"><span data-stu-id="73e28-208">Later, Visual Studio Code receives hello compilation result.</span></span> <span data-ttu-id="73e28-209">Devido a compilação remota de toohello, código do Visual Studio requer que você listar informações Olá tooconnect tooyour análise Data Lake conta no arquivo de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="73e28-209">Due toohello remote compilation, Visual Studio Code requires that you list hello information tooconnect tooyour Data Lake Analytics account in hello configuration file.</span></span>

<span data-ttu-id="73e28-210">**toocompile um U-SQL script**</span><span class="sxs-lookup"><span data-stu-id="73e28-210">**toocompile a U-SQL script**</span></span>

1. <span data-ttu-id="73e28-211">Selecione Ctrl + Shift + P tooopen Olá comando paleta.</span><span class="sxs-lookup"><span data-stu-id="73e28-211">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2. <span data-ttu-id="73e28-212">Insira **ADL: Compilar Script**.</span><span class="sxs-lookup"><span data-stu-id="73e28-212">Enter **ADL: Compile Script**.</span></span> <span data-ttu-id="73e28-213">Olá compilação os resultados aparecem na Olá **saída** janela.</span><span class="sxs-lookup"><span data-stu-id="73e28-213">hello compile results appear in hello **Output** window.</span></span> <span data-ttu-id="73e28-214">Você pode também um arquivo de script e, em seguida, selecione **publicitário: Script de compilação** trabalho toocompile um U-SQL.</span><span class="sxs-lookup"><span data-stu-id="73e28-214">You can also right-click a script file, and then select **ADL: Compile Script** toocompile a U-SQL job.</span></span> <span data-ttu-id="73e28-215">o resultado da compilação Olá aparece no hello **saída** painel.</span><span class="sxs-lookup"><span data-stu-id="73e28-215">hello compilation result appears in hello **Output** pane.</span></span>
 

<span data-ttu-id="73e28-216">**toosubmit um U-SQL script**</span><span class="sxs-lookup"><span data-stu-id="73e28-216">**toosubmit a U-SQL script**</span></span>

1. <span data-ttu-id="73e28-217">Selecione Ctrl + Shift + P tooopen Olá comando paleta.</span><span class="sxs-lookup"><span data-stu-id="73e28-217">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2. <span data-ttu-id="73e28-218">Insira **ADL: Enviar Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="73e28-218">Enter **ADL: Submit Job**.</span></span>  <span data-ttu-id="73e28-219">Também é possível clicar com o botão direito do mouse em um arquivo de script e, depois, selecionar **ADL: Enviar Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="73e28-219">You can also right-click a script file, and then select **ADL: Submit Job**.</span></span> 

<span data-ttu-id="73e28-220">Depois que você enviar um trabalho de U-SQL, logs de envio de saudação são exibidos na Olá **saída** janela no código VS.</span><span class="sxs-lookup"><span data-stu-id="73e28-220">After you submit a U-SQL job, hello submission logs appear in hello **Output** window in VS Code.</span></span> <span data-ttu-id="73e28-221">Se o envio de saudação for bem-sucedida, Olá trabalho URL também é exibida.</span><span class="sxs-lookup"><span data-stu-id="73e28-221">If hello submission is successful, hello job URL appears as well.</span></span> <span data-ttu-id="73e28-222">Você pode abrir Olá trabalho URL em um status de trabalho em tempo real da web navegador tootrack hello.</span><span class="sxs-lookup"><span data-stu-id="73e28-222">You can open hello job URL in a web browser tootrack hello real-time job status.</span></span>

<span data-ttu-id="73e28-223">saída de hello tooenable de detalhes do trabalho Olá, definir **jobInformationOutputPath** em Olá **vs código para hello u-sql_settings.json** arquivo.</span><span class="sxs-lookup"><span data-stu-id="73e28-223">tooenable hello output of hello job details, set **jobInformationOutputPath** in hello **vs code for hello u-sql_settings.json** file.</span></span>
 
## <a name="use-a-code-behind-file"></a><span data-ttu-id="73e28-224">Usar um arquivo code-behind</span><span class="sxs-lookup"><span data-stu-id="73e28-224">Use a code-behind file</span></span>

<span data-ttu-id="73e28-225">Um arquivo code-behind é um arquivo em C# associado a um único script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="73e28-225">A code-behind file is a C# file associated with a single U-SQL script.</span></span> <span data-ttu-id="73e28-226">Você pode definir um script dedicado tooUDO UDA, UDT e UDF no arquivo de code-behind hello.</span><span class="sxs-lookup"><span data-stu-id="73e28-226">You can define a script dedicated tooUDO, UDA, UDT, and UDF in hello code-behind file.</span></span> <span data-ttu-id="73e28-227">Olá UDO, UDA, UDT e UDF podem ser usados diretamente no script hello sem registrar o assembly hello primeiro.</span><span class="sxs-lookup"><span data-stu-id="73e28-227">hello UDO, UDA, UDT, and UDF can be used directly in hello script without registering hello assembly first.</span></span> <span data-ttu-id="73e28-228">Hello arquivo code-behind é colocado em Olá mesma pasta do seu arquivo de script U-SQL emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="73e28-228">hello code-behind file is put in hello same folder as its peering U-SQL script file.</span></span> <span data-ttu-id="73e28-229">Se o script hello é denominado xxx.usql, Olá lógica é nomeada como xxx.usql.cs.</span><span class="sxs-lookup"><span data-stu-id="73e28-229">If hello script is named xxx.usql, hello code-behind is named as xxx.usql.cs.</span></span> <span data-ttu-id="73e28-230">Se você excluir manualmente o arquivo de code-behind hello, recurso de lógica de saudação está desabilitado para seu script U-SQL associado.</span><span class="sxs-lookup"><span data-stu-id="73e28-230">If you manually delete hello code-behind file, hello code-behind feature is disabled for its associated U-SQL script.</span></span> <span data-ttu-id="73e28-231">Para saber mais sobre como escrever código do cliente para script U-SQL, veja [Writing and Using Custom Code in U-SQL – User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/) (Escrevendo e usado código personalizado em U-SQL — Funções Definidas pelo Usuário).</span><span class="sxs-lookup"><span data-stu-id="73e28-231">For more information about writing customer code for U-SQL script, see [Writing and Using Custom Code in U-SQL: User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span></span>

<span data-ttu-id="73e28-232">toosupport por trás do código, você deve abrir uma pasta de trabalho.</span><span class="sxs-lookup"><span data-stu-id="73e28-232">toosupport code-behind, you must open a working folder.</span></span> 

<span data-ttu-id="73e28-233">**toogenerate um arquivo code-behind**</span><span class="sxs-lookup"><span data-stu-id="73e28-233">**toogenerate a code-behind file**</span></span>

1. <span data-ttu-id="73e28-234">Abra um arquivo de origem.</span><span class="sxs-lookup"><span data-stu-id="73e28-234">Open a source file.</span></span> 
2. <span data-ttu-id="73e28-235">Selecione Ctrl + Shift + P tooopen Olá comando paleta.</span><span class="sxs-lookup"><span data-stu-id="73e28-235">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
3. <span data-ttu-id="73e28-236">Insira **ADL: Gerar Code-Behind**.</span><span class="sxs-lookup"><span data-stu-id="73e28-236">Enter **ADL: Generate Code Behind**.</span></span> <span data-ttu-id="73e28-237">Um arquivo code-behind é criado no hello mesma pasta.</span><span class="sxs-lookup"><span data-stu-id="73e28-237">A code-behind file is created in hello same folder.</span></span> 

<span data-ttu-id="73e28-238">Também é possível clicar com o botão direito em um arquivo de script e, depois, selecionar **ADL: Gerar Code Behind**.</span><span class="sxs-lookup"><span data-stu-id="73e28-238">You can also right-click a script file, and then select **ADL: Generate Code Behind**.</span></span> 

<span data-ttu-id="73e28-239">toocompile e enviar um script U-SQL com um arquivo code-behind é Olá mesmo que o arquivo de script com hello autônomo U-SQL.</span><span class="sxs-lookup"><span data-stu-id="73e28-239">toocompile and submit a U-SQL script with a code-behind file is hello same as with hello standalone U-SQL script file.</span></span>

<span data-ttu-id="73e28-240">Olá duas capturas de tela a seguir mostra um arquivo code-behind e seu arquivo de script U-SQL associado:</span><span class="sxs-lookup"><span data-stu-id="73e28-240">hello following two screenshots show a code-behind file and its associated U-SQL script file:</span></span>
 
![Code-behind das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![Arquivo de script code-behind das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a><span data-ttu-id="73e28-243">Usar assemblies</span><span class="sxs-lookup"><span data-stu-id="73e28-243">Use assemblies</span></span>

<span data-ttu-id="73e28-244">Para obter informações sobre como desenvolver assemblies, confira [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md) (Desenvolver assemblies U-SQL para trabalhos do Azure Data Lake Analytics).</span><span class="sxs-lookup"><span data-stu-id="73e28-244">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>

<span data-ttu-id="73e28-245">Você pode usar assemblies de código personalizado do Data Lake Tools tooregister no catálogo de análise Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="73e28-245">You can use Data Lake Tools tooregister custom code assemblies in hello Data Lake Analytics catalog.</span></span>

<span data-ttu-id="73e28-246">**tooregister um assembly**</span><span class="sxs-lookup"><span data-stu-id="73e28-246">**tooregister an assembly**</span></span>

<span data-ttu-id="73e28-247">Você pode registrar o assembly hello por meio de saudação **publicitário: registrar Assembly de** ou **publicitário: registrar o Assembly por meio da configuração** comandos.</span><span class="sxs-lookup"><span data-stu-id="73e28-247">You can register hello assembly through hello **ADL: Register Assembly** or **ADL: Register Assembly through Configuration** commands.</span></span>

<span data-ttu-id="73e28-248">**tooregister por meio de saudação publicitário: comando registrar Assembly**</span><span class="sxs-lookup"><span data-stu-id="73e28-248">**tooregister through hello ADL: Register Assembly command**</span></span>
1.  <span data-ttu-id="73e28-249">Selecione Ctrl + Shift + P tooopen Olá comando paleta.</span><span class="sxs-lookup"><span data-stu-id="73e28-249">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2.  <span data-ttu-id="73e28-250">Digite **ADL: Registrar Assembly**.</span><span class="sxs-lookup"><span data-stu-id="73e28-250">Enter **ADL: Register Assembly**.</span></span> 
3.  <span data-ttu-id="73e28-251">Especifica caminho do local do assembly hello.</span><span class="sxs-lookup"><span data-stu-id="73e28-251">Specify hello local assembly path.</span></span> 
4.  <span data-ttu-id="73e28-252">Selecione uma conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="73e28-252">Select a Data Lake Analytics account.</span></span>
5.  <span data-ttu-id="73e28-253">Selecione um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="73e28-253">Select a database.</span></span>

<span data-ttu-id="73e28-254">Resultados: portal de saudação é aberto em um navegador e exibe o processo de registro do assembly hello.</span><span class="sxs-lookup"><span data-stu-id="73e28-254">Results: hello portal is opened in a browser and displays hello assembly registration process.</span></span>  

<span data-ttu-id="73e28-255">Saudação de tootrigger outra maneira conveniente **publicitário: registrar Assembly de** comando é o DLL de saudação tooright clique no Explorador de arquivos.</span><span class="sxs-lookup"><span data-stu-id="73e28-255">Another convenient way tootrigger hello **ADL: Register Assembly** command is tooright-click hello .dll file in File Explorer.</span></span> 

<span data-ttu-id="73e28-256">**tooregister embora Olá publicitário: registrar o Assembly através do comando de configuração**</span><span class="sxs-lookup"><span data-stu-id="73e28-256">**tooregister though hello ADL: Register Assembly through Configuration command**</span></span>
1.  <span data-ttu-id="73e28-257">Selecione Ctrl + Shift + P tooopen Olá comando paleta.</span><span class="sxs-lookup"><span data-stu-id="73e28-257">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2.  <span data-ttu-id="73e28-258">Digite **ADL: Registrar Assembly através da Configuração**.</span><span class="sxs-lookup"><span data-stu-id="73e28-258">Enter **ADL: Register Assembly through Configuration**.</span></span> 
3.  <span data-ttu-id="73e28-259">Especifica caminho do local do assembly hello.</span><span class="sxs-lookup"><span data-stu-id="73e28-259">Specify hello local assembly path.</span></span> 
4.  <span data-ttu-id="73e28-260">arquivo JSON de saudação é exibido.</span><span class="sxs-lookup"><span data-stu-id="73e28-260">hello JSON file is displayed.</span></span> <span data-ttu-id="73e28-261">Revise e edite as dependências de assembly hello e parâmetros de recursos, se necessário.</span><span class="sxs-lookup"><span data-stu-id="73e28-261">Review and edit hello assembly dependencies and resource parameters, if needed.</span></span> <span data-ttu-id="73e28-262">As instruções são exibidas no hello **saída** janela.</span><span class="sxs-lookup"><span data-stu-id="73e28-262">Instructions are displayed in hello **Output** window.</span></span> <span data-ttu-id="73e28-263">tooproceed toohello registro do assembly, salve o arquivo JSON de saudação (Ctrl + S).</span><span class="sxs-lookup"><span data-stu-id="73e28-263">tooproceed toohello assembly registration, save (Ctrl+S) hello JSON file.</span></span>

![Code-behind das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- <span data-ttu-id="73e28-265">As dependências de assembly: Azure Data Lake Tools este detecta automaticamente se Olá DLL tem todas as dependências.</span><span class="sxs-lookup"><span data-stu-id="73e28-265">Assembly dependencies: Azure Data Lake Tools autodetects whether hello DLL has any dependencies.</span></span> <span data-ttu-id="73e28-266">dependências de saudação são exibidas no arquivo JSON de saudação depois que eles são detectados.</span><span class="sxs-lookup"><span data-stu-id="73e28-266">hello dependencies are displayed in hello JSON file after they are detected.</span></span> 
>- <span data-ttu-id="73e28-267">Recursos: Você pode carregar os recursos DLL (por exemplo,. txt,. PNG e. csv) como parte do registro do assembly hello.</span><span class="sxs-lookup"><span data-stu-id="73e28-267">Resources: You can upload your DLL resources (for example, .txt, .png, and .csv) as part of hello assembly registration.</span></span> 

<span data-ttu-id="73e28-268">Saudação de tootrigger outra maneira **publicitário: registrar o Assembly por meio da configuração** comando é o DLL de saudação tooright clique no Explorador de arquivos.</span><span class="sxs-lookup"><span data-stu-id="73e28-268">Another way tootrigger hello **ADL: Register Assembly through Configuration** command is tooright-click hello .dll file in File Explorer.</span></span> 

<span data-ttu-id="73e28-269">Olá código U-SQL a seguir demonstra como toocall um assembly.</span><span class="sxs-lookup"><span data-stu-id="73e28-269">hello following U-SQL code demonstrates how toocall an assembly.</span></span> <span data-ttu-id="73e28-270">No exemplo hello, nome do assembly hello é *teste*.</span><span class="sxs-lookup"><span data-stu-id="73e28-270">In hello sample, hello assembly name is *test*.</span></span>

```
REFERENCE ASSEMBLY [test];

@a = 
    EXTRACT 
        Iid int,
    Starts DateTime,
    Region string,
    Query string,
    DwellTime int,
    Results string,
    ClickedUrls string 
    FROM @"Sample/SearchLog.txt" 
    USING Extractors.Tsv();

@d =
    SELECT DISTINCT Region 
    FROM @a;

@d1 = 
    PROCESS @d
    PRODUCE 
        Region string,
    Mkt string
    USING new USQLApplication_codebehind.MyProcessor();

OUTPUT @d1 
    too@"Sample/SearchLogtest.txt" 
    USING Outputters.Tsv();
```


## <a name="access-hello-data-lake-analytics-catalog"></a><span data-ttu-id="73e28-271">Acessar o catálogo do hello análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="73e28-271">Access hello Data Lake Analytics catalog</span></span>

<span data-ttu-id="73e28-272">Depois que você se conectou tooAzure, você pode usar o hello catálogo de saudação U-SQL tooaccess as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="73e28-272">After you have connected tooAzure, you can use hello following steps tooaccess hello U-SQL catalog.</span></span>

<span data-ttu-id="73e28-273">**metadados de análise do Azure Data Lake Olá tooaccess**</span><span class="sxs-lookup"><span data-stu-id="73e28-273">**tooaccess hello Azure Data Lake Analytics metadata**</span></span>

1.  <span data-ttu-id="73e28-274">Pressione CTRL+SHIFT+P e insira **ADL: Listar Tabelas**.</span><span class="sxs-lookup"><span data-stu-id="73e28-274">Select Ctrl+Shift+P, and then enter **ADL: List Tables**.</span></span>
2.  <span data-ttu-id="73e28-275">Selecione uma das contas de análise Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="73e28-275">Select one of hello Data Lake Analytics accounts.</span></span>
3.  <span data-ttu-id="73e28-276">Selecione um dos bancos de dados de análise Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="73e28-276">Select one of hello Data Lake Analytics databases.</span></span>
4.  <span data-ttu-id="73e28-277">Selecione um dos esquemas de saudação.</span><span class="sxs-lookup"><span data-stu-id="73e28-277">Select one of hello schemas.</span></span> <span data-ttu-id="73e28-278">Você pode ver a lista de saudação de tabelas.</span><span class="sxs-lookup"><span data-stu-id="73e28-278">You can see hello list of tables.</span></span>

## <a name="view-data-lake-analytics-jobs"></a><span data-ttu-id="73e28-279">Exibir trabalhos do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="73e28-279">View Data Lake Analytics jobs</span></span>

<span data-ttu-id="73e28-280">**trabalhos de análise Data Lake tooview**</span><span class="sxs-lookup"><span data-stu-id="73e28-280">**tooview Data Lake Analytics jobs**</span></span>
1.  <span data-ttu-id="73e28-281">Abra a paleta de comando hello (Ctrl + Shift + P) e selecione **publicitário: Mostrar trabalho**.</span><span class="sxs-lookup"><span data-stu-id="73e28-281">Open hello command palette (Ctrl+Shift+P) and select **ADL: Show Job**.</span></span> 
2.  <span data-ttu-id="73e28-282">Selecione uma conta do Data Lake Analytics ou local.</span><span class="sxs-lookup"><span data-stu-id="73e28-282">Select a Data Lake Analytics or local account.</span></span> 
3.  <span data-ttu-id="73e28-283">Aguarde para lista de trabalhos Olá Olá conta tooappear.</span><span class="sxs-lookup"><span data-stu-id="73e28-283">Wait for hello jobs list for hello account tooappear.</span></span>
4.  <span data-ttu-id="73e28-284">Selecione um trabalho na lista de trabalhos, Data Lake Tools abre detalhes do trabalho Olá no hello portal do Azure e exibe o arquivo de JobInfo Olá no código VS.</span><span class="sxs-lookup"><span data-stu-id="73e28-284">Select a job from job list, Data Lake Tools opens hello job details in hello Azure portal and displays hello JobInfo file in VS Code.</span></span>

![Tipos de objeto do IntelliSense das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a><span data-ttu-id="73e28-286">Integração do Armazenamento do Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="73e28-286">Azure Data Lake Storage integration</span></span>

<span data-ttu-id="73e28-287">Você pode usar comandos relacionados ao Armazenamento do Azure Data Lake:</span><span class="sxs-lookup"><span data-stu-id="73e28-287">You can use Azure Data Lake Storage-related commands to:</span></span>
 - <span data-ttu-id="73e28-288">Procure por meio de recursos de armazenamento do Azure Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="73e28-288">Browse through hello Azure Data Lake Storage resources.</span></span> 
 - <span data-ttu-id="73e28-289">Arquivo de armazenamento do Azure Data Lake Olá visualização.</span><span class="sxs-lookup"><span data-stu-id="73e28-289">Preview hello Azure Data Lake Storage file.</span></span>  
 - <span data-ttu-id="73e28-290">Saudação de carregar arquivo de tooAzure Data Lake armazenamento diretamente no código VS.</span><span class="sxs-lookup"><span data-stu-id="73e28-290">Upload hello file directly tooAzure Data Lake Storage in VS Code.</span></span> 

### <a name="list-hello-storage-path"></a><span data-ttu-id="73e28-291">Caminho de armazenamento de saudação de lista</span><span class="sxs-lookup"><span data-stu-id="73e28-291">List hello storage path</span></span> 
<span data-ttu-id="73e28-292">Você pode listar o caminho de armazenamento Olá por meio de paleta do comando hello ou com o botão direito.</span><span class="sxs-lookup"><span data-stu-id="73e28-292">You can list hello storage path through hello command palette or through right-click.</span></span>

<span data-ttu-id="73e28-293">**caminho de armazenamento toolist Olá a paleta de comando Olá**</span><span class="sxs-lookup"><span data-stu-id="73e28-293">**toolist hello storage path through hello command palette**</span></span>

1.  <span data-ttu-id="73e28-294">Abra a paleta de comando hello (Ctrl + Shift + P) e digite **publicitário: caminho de armazenamento de lista**.</span><span class="sxs-lookup"><span data-stu-id="73e28-294">Open hello command palette (Ctrl+Shift+P) and enter **ADL: List Storage Path**.</span></span>

    ![Listar caminho de armazenamento das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  <span data-ttu-id="73e28-296">Selecione sua maneira preferida para listar o caminho de armazenamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="73e28-296">Select your preferred way for listing hello storage path.</span></span> <span data-ttu-id="73e28-297">Esta passagem usa **Inserir um caminho** como exemplo.</span><span class="sxs-lookup"><span data-stu-id="73e28-297">This passage uses **Enter a path** as an example.</span></span>

    ![Data Lake Tools para Visual Studio Code caminho de armazenamento Olá toolist unidirecional](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- <span data-ttu-id="73e28-299">Código VS mantém caminho de saudação visitou por último em cada conta da análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="73e28-299">VS Code keeps hello last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="73e28-300">Por exemplo: /tt/ss.</span><span class="sxs-lookup"><span data-stu-id="73e28-300">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="73e28-301">Navegador do caminho raiz: caminho de raiz de lista de saudação da sua conta da análise Data Lake selecionada ou um caminho local.</span><span class="sxs-lookup"><span data-stu-id="73e28-301">Browser from root path: hello list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="73e28-302">Inserir um caminho: lista um caminho especificado de sua conta do Data Lake Analytics selecionada, ou um caminho local.</span><span class="sxs-lookup"><span data-stu-id="73e28-302">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>
    
3. <span data-ttu-id="73e28-303">Selecione uma conta de caminho local hello ou uma conta da análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="73e28-303">Select an account from hello local path or a Data Lake Analytics account.</span></span>

    ![Ferramentas do Data Lake para Visual Studio Code selecionar mais](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. <span data-ttu-id="73e28-305">Selecione **mais** toolist mais análise Data Lake contas e, em seguida, selecione uma conta da análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="73e28-305">Select **more** toolist more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

    ![Ferramentas do Data Lake para Visual Studio Code selecionar uma conta](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  <span data-ttu-id="73e28-307">Insira um caminho de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="73e28-307">Enter an Azure storage path.</span></span> <span data-ttu-id="73e28-308">Por exemplo, /output.</span><span class="sxs-lookup"><span data-stu-id="73e28-308">For example, /output.</span></span>

    ![Inserir caminho de armazenamento das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  <span data-ttu-id="73e28-310">Resultados: paleta de comando Olá lista informações de caminho de saudação com base nas suas entradas.</span><span class="sxs-lookup"><span data-stu-id="73e28-310">Results: hello command palette lists hello path information based on your entries.</span></span>

    ![Listar resultados do caminho de armazenamento das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

<span data-ttu-id="73e28-312">Uma maneira mais conveniente de caminho relativo do toolist Olá é por meio de saudação clique o menu de contexto.</span><span class="sxs-lookup"><span data-stu-id="73e28-312">A more convenient way toolist hello relative path is through hello right-click context menu.</span></span>

<span data-ttu-id="73e28-313">**caminho de armazenamento de saudação toolist por meio de clique**</span><span class="sxs-lookup"><span data-stu-id="73e28-313">**toolist hello storage path through right-click**</span></span>

1.  <span data-ttu-id="73e28-314">Clique com botão direito Olá tooselect de cadeia de caracteres de caminho **caminho de armazenamento de lista**.</span><span class="sxs-lookup"><span data-stu-id="73e28-314">Right-click hello path string tooselect **List Storage Path**.</span></span>

       ![Menu de contexto acessado com o botão direito das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. <span data-ttu-id="73e28-316">caminho relativo do selecionado Olá aparece na paleta de comando Olá.</span><span class="sxs-lookup"><span data-stu-id="73e28-316">hello selected relative path appears in hello command palette.</span></span>

   ![Caminho relativo selecionado das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  <span data-ttu-id="73e28-318">Selecione uma conta de caminho local hello ou uma conta da análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="73e28-318">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Ferramentas do Data Lake para Visual Studio Code selecionar uma conta](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  <span data-ttu-id="73e28-320">Resultados: paleta de comando Olá lista Olá pastas e arquivos caminho atual hello.</span><span class="sxs-lookup"><span data-stu-id="73e28-320">Results: hello command palette lists hello folders and files for hello current path.</span></span>

       ![Data Lake Tools para lista de código do Visual Studio do caminho atual Olá](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-hello-storage-file"></a><span data-ttu-id="73e28-322">Arquivo de armazenamento de saudação de visualização</span><span class="sxs-lookup"><span data-stu-id="73e28-322">Preview hello storage file</span></span>
<span data-ttu-id="73e28-323">Você pode visualizar o arquivo de armazenamento Olá por meio de paleta do comando hello ou com o botão direito.</span><span class="sxs-lookup"><span data-stu-id="73e28-323">You can preview hello storage file through hello command palette or through right-click.</span></span>

<span data-ttu-id="73e28-324">**arquivo de armazenamento de saudação toopreview por meio da paleta de comando Olá**</span><span class="sxs-lookup"><span data-stu-id="73e28-324">**toopreview hello storage file through hello command palette**</span></span>

1.  <span data-ttu-id="73e28-325">Abra a paleta de comando hello (Ctrl + Shift + P) e digite **publicitário: arquivo de armazenamento de visualização**.</span><span class="sxs-lookup"><span data-stu-id="73e28-325">Open hello command palette (Ctrl+Shift+P) and enter **ADL: Preview Storage File**.</span></span>

       ![Visualizar arquivo de armazenamento das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  <span data-ttu-id="73e28-327">Selecione uma conta de caminho local hello ou uma conta da análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="73e28-327">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Listar conta das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="73e28-329">Selecione **mais** toolist mais análise Data Lake contas e, em seguida, selecione uma conta da análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="73e28-329">Select **more** toolist more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

       ![Ferramentas do Data Lake para Visual Studio Code selecionar uma conta](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  <span data-ttu-id="73e28-331">Insira um caminho ou arquivo de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="73e28-331">Enter an Azure storage path or file.</span></span> <span data-ttu-id="73e28-332">Por exemplo: /output/SearchLog.txt.</span><span class="sxs-lookup"><span data-stu-id="73e28-332">For example, /output/SearchLog.txt.</span></span>

       ![Inserir caminho e arquivo de armazenamento das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  <span data-ttu-id="73e28-334">Resultados: paleta de comando Olá lista informações de caminho de saudação com base nas suas entradas.</span><span class="sxs-lookup"><span data-stu-id="73e28-334">Results: hello command palette lists hello path information based on your entries.</span></span>

       ![Ferramentas do Data Lake para Visual Studio Code Resultado da visualização do arquivo](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

<span data-ttu-id="73e28-336">**caminho de armazenamento de saudação toolist por meio de clique**</span><span class="sxs-lookup"><span data-stu-id="73e28-336">**toolist hello storage path through right-click**</span></span>

1.  <span data-ttu-id="73e28-337">toopreview um arquivo, clique o caminho do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="73e28-337">toopreview a file, right-click hello file path.</span></span>

   ![Menu de contexto acessado com o botão direito das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  <span data-ttu-id="73e28-339">Selecione uma conta de caminho local hello ou uma conta da análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="73e28-339">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Ferramentas do Data Lake para Visual Studio Code selecionar uma conta](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="73e28-341">Resultados: Código VS exibe os resultados de visualização de saudação do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="73e28-341">Results: VS Code displays hello preview results of hello file.</span></span>

       ![Ferramentas do Data Lake para Visual Studio Code Resultado da visualização do arquivo](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a><span data-ttu-id="73e28-343">Carregar um arquivo</span><span class="sxs-lookup"><span data-stu-id="73e28-343">Upload a file</span></span> 

<span data-ttu-id="73e28-344">Você pode carregar arquivos digitando comandos Olá **publicitário: Carregue o arquivo** ou **publicitário: Carregue o arquivo por meio da configuração**.</span><span class="sxs-lookup"><span data-stu-id="73e28-344">You can upload files by entering hello commands **ADL: Upload File** or **ADL: Upload File through Configuration**.</span></span>

<span data-ttu-id="73e28-345">**arquivos tooupload embora Olá publicitário: comando carregar arquivo**</span><span class="sxs-lookup"><span data-stu-id="73e28-345">**tooupload files though hello ADL: Upload File command**</span></span>
1. <span data-ttu-id="73e28-346">Selecione Ctrl + Shift + P tooopen Olá comando paleta ou com o botão direito editor de script hello e, em seguida, digite **carregar arquivo**.</span><span class="sxs-lookup"><span data-stu-id="73e28-346">Select Ctrl+Shift+P tooopen hello command palette or right-click hello script editor, and then enter **Upload File**.</span></span>
2.  <span data-ttu-id="73e28-347">Olá tooupload de arquivo, insira um caminho local.</span><span class="sxs-lookup"><span data-stu-id="73e28-347">tooupload hello file, enter a local path.</span></span>

    ![Inserir caminho local das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. <span data-ttu-id="73e28-349">Selecione uma das maneiras de saudação do caminho de armazenamento de saudação de listagem.</span><span class="sxs-lookup"><span data-stu-id="73e28-349">Select one of hello ways of listing hello storage path.</span></span> <span data-ttu-id="73e28-350">Esta passagem usa **Inserir um caminho** como exemplo.</span><span class="sxs-lookup"><span data-stu-id="73e28-350">This passage uses **Enter a path** as an example.</span></span>

    ![Listar caminho de armazenamento das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- <span data-ttu-id="73e28-352">Código VS mantém caminho de saudação visitou por último em cada conta da análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="73e28-352">VS Code keeps hello last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="73e28-353">Por exemplo: /tt/ss.</span><span class="sxs-lookup"><span data-stu-id="73e28-353">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="73e28-354">Navegador do caminho raiz: caminho de raiz de lista de saudação da sua conta da análise Data Lake selecionada ou um caminho local.</span><span class="sxs-lookup"><span data-stu-id="73e28-354">Browser from root path: hello list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="73e28-355">Inserir um caminho: lista um caminho especificado de sua conta do Data Lake Analytics selecionada, ou um caminho local.</span><span class="sxs-lookup"><span data-stu-id="73e28-355">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>

4. <span data-ttu-id="73e28-356">Selecione uma conta de caminho local hello ou uma conta da análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="73e28-356">Select an account from hello local path or a Data Lake Analytics account.</span></span>

    ![Armazenamento acionado pelo botão direito das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. <span data-ttu-id="73e28-358">Insira um caminho de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="73e28-358">Enter an Azure storage path.</span></span> <span data-ttu-id="73e28-359">Por exemplo: /output.</span><span class="sxs-lookup"><span data-stu-id="73e28-359">For example: /output.</span></span>

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. <span data-ttu-id="73e28-360">Encontre o caminho de seu armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="73e28-360">Find your Azure storage path.</span></span> <span data-ttu-id="73e28-361">Selecione **Escolher pasta atual**.</span><span class="sxs-lookup"><span data-stu-id="73e28-361">Select **Choose current folder**.</span></span>

    ![Selecionar uma pasta das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  <span data-ttu-id="73e28-363">Resultados: Olá **saída** janela exibe o status de carregamento de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="73e28-363">Results: hello **Output** window displays hello file upload status.</span></span>

       ![Status de upload das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

<span data-ttu-id="73e28-365">**arquivos tooupload embora Olá publicitário: Carregue o arquivo por meio do comando de configuração**</span><span class="sxs-lookup"><span data-stu-id="73e28-365">**tooupload files though hello ADL: Upload File through Configuration command**</span></span>
1.  <span data-ttu-id="73e28-366">Selecione Ctrl + Shift + P tooopen Olá comando paleta ou com o botão direito editor de script hello e, em seguida, digite **carregar o arquivo por meio da configuração**.</span><span class="sxs-lookup"><span data-stu-id="73e28-366">Select Ctrl+Shift+P tooopen hello command palette or right-click hello script editor, and then enter **Upload File through Configuration**.</span></span>
2.  <span data-ttu-id="73e28-367">O VS Code exibe um arquivo JSON.</span><span class="sxs-lookup"><span data-stu-id="73e28-367">VS Code displays a JSON file.</span></span> <span data-ttu-id="73e28-368">Você pode inserir os caminhos de arquivo e carregar vários arquivos no hello simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="73e28-368">You can enter file paths and upload multiple files at hello same time.</span></span> <span data-ttu-id="73e28-369">As instruções são exibidas no hello **saída** janela.</span><span class="sxs-lookup"><span data-stu-id="73e28-369">Instructions are displayed in hello **Output** window.</span></span> <span data-ttu-id="73e28-370">tooproceed tooupload Olá arquivo, salve (Ctrl + S) Olá JSON.</span><span class="sxs-lookup"><span data-stu-id="73e28-370">tooproceed tooupload hello file, save (Ctrl+S) hello JSON file.</span></span>

       ![Inserir arquivo das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  <span data-ttu-id="73e28-372">Resultados: Olá **saída** janela exibe o status de carregamento de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="73e28-372">Results: hello **Output** window displays hello file upload status.</span></span>

       ![Status de upload das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

<span data-ttu-id="73e28-374">Outro tooupload de maneira toostorage um arquivo é por meio de saudação de atalho no caminho completo do arquivo hello ou um caminho relativo do arquivo hello no editor de script hello.</span><span class="sxs-lookup"><span data-stu-id="73e28-374">Another way tooupload a file toostorage is through hello right-click menu on hello file's full path or hello file's relative path in hello script editor.</span></span> <span data-ttu-id="73e28-375">Insira o caminho do arquivo local hello e, em seguida, selecione a conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="73e28-375">Enter hello local file path, and then select hello account.</span></span> <span data-ttu-id="73e28-376">Olá **saída** janela exibe o status de carregamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="73e28-376">hello **Output** window displays hello upload status.</span></span> 

### <a name="open-azure-storage-explorer"></a><span data-ttu-id="73e28-377">Abra o Gerenciador de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="73e28-377">Open Azure Storage Explorer</span></span>
<span data-ttu-id="73e28-378">Você pode abrir **Azure Storage Explorer** digitando o comando Olá **publicitário: Abra o Web Azure Storage Explorer** ou selecionando-o no menu de contexto do botão direito do mouse hello.</span><span class="sxs-lookup"><span data-stu-id="73e28-378">You can open **Azure Storage Explorer** by entering hello command **ADL: Open Web Azure Storage Explorer** or by selecting it from hello right-click context menu.</span></span>

<span data-ttu-id="73e28-379">**tooopen Azure Storage Explorer**</span><span class="sxs-lookup"><span data-stu-id="73e28-379">**tooopen Azure Storage Explorer**</span></span>

1. <span data-ttu-id="73e28-380">Selecione Ctrl + Shift + P tooopen Olá comando paleta.</span><span class="sxs-lookup"><span data-stu-id="73e28-380">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2. <span data-ttu-id="73e28-381">Digite **abra Web Azure Storage Explorer** ou com o botão direito em um caminho relativo ou um caminho completo de saudação no editor de script hello e, em seguida, selecione **abra Web Azure Storage Explorer**.</span><span class="sxs-lookup"><span data-stu-id="73e28-381">Enter **Open Web Azure Storage Explorer** or right-click on a relative path or hello full path in hello script editor, and then select **Open Web Azure Storage Explorer**.</span></span>
3. <span data-ttu-id="73e28-382">Selecione uma conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="73e28-382">Select a Data Lake Analytics account.</span></span>

<span data-ttu-id="73e28-383">Ferramentas do data Lake abre caminho de armazenamento do Azure Olá no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="73e28-383">Data Lake Tools opens hello Azure storage path in hello Azure portal.</span></span> <span data-ttu-id="73e28-384">Você pode encontrar hello caminho e visualização Olá arquivo da web hello.</span><span class="sxs-lookup"><span data-stu-id="73e28-384">You can find hello path and preview hello file from hello web.</span></span>

### <a name="local-run-and-local-debug-for-windows-users"></a><span data-ttu-id="73e28-385">Depuração local e execução local para usuários do Windows</span><span class="sxs-lookup"><span data-stu-id="73e28-385">Local run and local debug for Windows users</span></span>
<span data-ttu-id="73e28-386">Local de U-SQL execute testes de seus dados locais e valida o script localmente, antes que seu código seja publicado tooData análise Lake.</span><span class="sxs-lookup"><span data-stu-id="73e28-386">U-SQL local run tests your local data and validates your script locally, before your code is published tooData Lake Analytics.</span></span> <span data-ttu-id="73e28-387">Olá depuração local recurso permite que você toocomplete Olá tarefas a seguir antes de seu código é enviada análise tooData Lake:</span><span class="sxs-lookup"><span data-stu-id="73e28-387">hello local debug feature enables you toocomplete hello following tasks before your code is submitted tooData Lake Analytics:</span></span> 
- <span data-ttu-id="73e28-388">Depure o code-behind em C#.</span><span class="sxs-lookup"><span data-stu-id="73e28-388">Debug your C# code-behind.</span></span> 
- <span data-ttu-id="73e28-389">Percorrer o código de saudação.</span><span class="sxs-lookup"><span data-stu-id="73e28-389">Step through hello code.</span></span> 
- <span data-ttu-id="73e28-390">Valide o script localmente.</span><span class="sxs-lookup"><span data-stu-id="73e28-390">Validate your script locally.</span></span>

<span data-ttu-id="73e28-391">Para obter instruções sobre a execução e a depuração local, confira [Execução local do U-SQL e depuração local com o Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="73e28-391">For instructions on local run and local debug, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>

## <a name="additional-features"></a><span data-ttu-id="73e28-392">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="73e28-392">Additional features</span></span>

<span data-ttu-id="73e28-393">Data Lake Tools para código VS dá suporte a saudação recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="73e28-393">Data Lake Tools for VS Code supports hello following features:</span></span>

-   <span data-ttu-id="73e28-394">Preenchimento automático de IntelliSense: as sugestões são exibidas em janelas pop-up ao redor dos itens, como palavras-chave, métodos e variáveis.</span><span class="sxs-lookup"><span data-stu-id="73e28-394">IntelliSense auto-complete: Suggestions appear in pop-up windows around items, such as keywords, methods, and variables.</span></span> <span data-ttu-id="73e28-395">Ícones diferentes representam tipos diferentes de objetos de saudação:</span><span class="sxs-lookup"><span data-stu-id="73e28-395">Different icons represent different types of hello objects:</span></span>

    - <span data-ttu-id="73e28-396">Tipo de dados de Scala</span><span class="sxs-lookup"><span data-stu-id="73e28-396">Scala data type</span></span>
    - <span data-ttu-id="73e28-397">Tipos de dados complexos</span><span class="sxs-lookup"><span data-stu-id="73e28-397">Complex data type</span></span>
    - <span data-ttu-id="73e28-398">UDTs Internos</span><span class="sxs-lookup"><span data-stu-id="73e28-398">Built-in UDTs</span></span>
    - <span data-ttu-id="73e28-399">Coleções e classes .Net</span><span class="sxs-lookup"><span data-stu-id="73e28-399">.NET collection and classes</span></span>
    - <span data-ttu-id="73e28-400">Expressões em C#</span><span class="sxs-lookup"><span data-stu-id="73e28-400">C# expressions</span></span>
    - <span data-ttu-id="73e28-401">UDFs, UDOs e UDAAGs internos de C#</span><span class="sxs-lookup"><span data-stu-id="73e28-401">Built-in C# UDFs, UDOs, and UDAAGs</span></span> 
    - <span data-ttu-id="73e28-402">Funções em U-SQL</span><span class="sxs-lookup"><span data-stu-id="73e28-402">U-SQL functions</span></span>
    - <span data-ttu-id="73e28-403">Função de Janelas do U-SQL</span><span class="sxs-lookup"><span data-stu-id="73e28-403">U-SQL windowing function</span></span>
 
    ![Tipos de objeto do IntelliSense das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   <span data-ttu-id="73e28-405">IntelliSense preenchimento automático nos metadados da análise Data Lake: Data Lake Tools baixa informações de metadados de análise Data Lake Olá localmente.</span><span class="sxs-lookup"><span data-stu-id="73e28-405">IntelliSense auto-complete on Data Lake Analytics metadata: Data Lake Tools downloads hello Data Lake Analytics metadata information locally.</span></span> <span data-ttu-id="73e28-406">recurso IntelliSense de saudação preenche automaticamente os objetos, inclusive Olá banco de dados, esquema, tabela, exibição, função com valor de tabela, procedimentos e c# assemblies, Olá análise Data Lake metadados.</span><span class="sxs-lookup"><span data-stu-id="73e28-406">hello IntelliSense feature automatically populates objects, including hello database, schema, table, view, table-valued function, procedures, and C# assemblies, from hello Data Lake Analytics metadata.</span></span>
 
    ![Metadados do IntelliSense das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   <span data-ttu-id="73e28-408">Marcador de erro do IntelliSense: Data Lake Tools sublinha Olá edição erros para U-SQL e c#.</span><span class="sxs-lookup"><span data-stu-id="73e28-408">IntelliSense error marker: Data Lake Tools underlines hello editing errors for U-SQL and C#.</span></span> 
-   <span data-ttu-id="73e28-409">Destaques de sintaxe: Data Lake Tools usa os itens de toodifferentiate de cores diferentes, como variáveis, palavras-chave, tipo de dados e funções.</span><span class="sxs-lookup"><span data-stu-id="73e28-409">Syntax highlights: Data Lake Tools uses different colors toodifferentiate items, such as variables, keywords, data type, and functions.</span></span> 

    ![Destaques da sintaxe das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a><span data-ttu-id="73e28-411">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="73e28-411">Next steps</span></span>

- <span data-ttu-id="73e28-412">Para saber mais sobre a execução local do U-SQL e sobre a depuração local com o Visual Studio Code, consulte [Execução local do U-SQL e depuração local com o Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="73e28-412">For U-SQL local run and local debug with Visual Studio Code, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>
- <span data-ttu-id="73e28-413">Para obter informações introdutórias sobre o Data Lake Analytics, veja [Tutorial: Introdução ao Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="73e28-413">For getting-started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="73e28-414">Para saber mais sobre as Ferramentas do Data Lake para Visual Studio, confira [Tutorial: Desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="73e28-414">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="73e28-415">Para obter informações sobre como desenvolver assemblies, confira [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md) (Desenvolver assemblies U-SQL para trabalhos do Azure Data Lake Analytics).</span><span class="sxs-lookup"><span data-stu-id="73e28-415">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>



