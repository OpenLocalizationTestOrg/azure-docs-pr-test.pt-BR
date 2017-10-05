---
title: 'Ferramentas do Azure Data Lake: Usar as Ferramentas do Azure Data Lake para Visual Studio Code | Microsoft Docs'
description: 'Saiba como usar as Ferramentas do Azure Data Lake para Visual Studio Code para criar, testar e executar scripts U-SQL. '
Keywords: "VSCode, Ferramentas do Azure Data Lake, Execução local, Depuração local, Depuração Local, visualizar arquivo de armazenamento, carregar no caminho de armazenamento"
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
ms.openlocfilehash: 833d14af47454a01fa3c97ffa854d688dd35871f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a><span data-ttu-id="c6fef-104">Usar as Ferramentas do Azure Data Lake para Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="c6fef-104">Use Azure Data Lake Tools for Visual Studio Code</span></span>

<span data-ttu-id="c6fef-105">Saiba como usar as Ferramentas do Azure Data Lake para Visual Studio Code (VS Code) para criar, testar e executar scripts U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c6fef-105">Learn how to use Azure Data Lake Tools for Visual Studio Code (VS Code) to create, test, and run U-SQL scripts.</span></span> <span data-ttu-id="c6fef-106">As informações também são abordadas no vídeo a seguir:</span><span class="sxs-lookup"><span data-stu-id="c6fef-106">The information is also covered in the following video:</span></span>

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a><span data-ttu-id="c6fef-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c6fef-107">Prerequisites</span></span>

<span data-ttu-id="c6fef-108">O Data Lake Tools pode ser instalado em plataformas com suporte do VS Code.</span><span class="sxs-lookup"><span data-stu-id="c6fef-108">Data Lake Tools can be installed on the platforms supported by VS Code.</span></span> <span data-ttu-id="c6fef-109">As plataformas com suporte incluem Windows, Linux e MacOS.</span><span class="sxs-lookup"><span data-stu-id="c6fef-109">The supported platforms include Windows, Linux, and MacOS.</span></span> <span data-ttu-id="c6fef-110">Cada plataformas tem os próprios pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="c6fef-110">The different platforms have the following prerequisites:</span></span>

- <span data-ttu-id="c6fef-111">Windows</span><span class="sxs-lookup"><span data-stu-id="c6fef-111">Windows</span></span>

    - <span data-ttu-id="c6fef-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="c6fef-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="c6fef-113">[Java SE Runtime Environment versão 8 atualização 77 ou posterior](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="c6fef-113">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="c6fef-114">Adicione o caminho java.exe ao caminho de variável de ambiente do sistema.</span><span class="sxs-lookup"><span data-stu-id="c6fef-114">Add the java.exe path to the system environment variable path.</span></span> <span data-ttu-id="c6fef-115">Para obter instruções de configuração, confira [Como definir ou alterar a variável do sistema do caminho?]( https://www.java.com/download/help/path.xml)</span><span class="sxs-lookup"><span data-stu-id="c6fef-115">For configuration instructions, see [How do I set or change the Path system variable?]( https://www.java.com/download/help/path.xml).</span></span> <span data-ttu-id="c6fef-116">O caminho é semelhante a C:\Arquivos de Programas\Java\jdk1.8.0_77\jre\bin.</span><span class="sxs-lookup"><span data-stu-id="c6fef-116">The path is similar to C:\Program Files\Java\jdk1.8.0_77\jre\bin.</span></span>
    - <span data-ttu-id="c6fef-117">[Tempo de execução do SDK do .NET Core 1.0.3 ou do .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="c6fef-117">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
    
- <span data-ttu-id="c6fef-118">Linux (é recomendável o Ubuntu 14.04 LTS)</span><span class="sxs-lookup"><span data-stu-id="c6fef-118">Linux (We recommend Ubuntu 14.04 LTS)</span></span>

    - <span data-ttu-id="c6fef-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="c6fef-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span> <span data-ttu-id="c6fef-120">Para instalar o código, insira o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c6fef-120">To install the code, enter the following command:</span></span>

              sudo dpkg -i code_<version_number>_amd64.deb

    - <span data-ttu-id="c6fef-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span><span class="sxs-lookup"><span data-stu-id="c6fef-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span></span> 

        - <span data-ttu-id="c6fef-122">Para atualizar a fonte do pacote deb, insira os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="c6fef-122">To update the deb package source, enter the following commands:</span></span>

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - <span data-ttu-id="c6fef-123">Para instalar o Mono, insira o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c6fef-123">To install Mono, enter the following command:</span></span>

                sudo apt-get install mono-complete

            > [!NOTE] 
            > <span data-ttu-id="c6fef-124">Não há suporte para o Mono 4.6.</span><span class="sxs-lookup"><span data-stu-id="c6fef-124">Mono 4.6 is not supported.</span></span> <span data-ttu-id="c6fef-125">Desinstale totalmente a versão 4.6 antes de instalar a versão 4.2.x.</span><span class="sxs-lookup"><span data-stu-id="c6fef-125">Uninstall version 4.6 entirely before you install 4.2.x.</span></span>  

        - <span data-ttu-id="c6fef-126">[Java SE Runtime Environment versão 8 atualização 77 ou posterior](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="c6fef-126">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="c6fef-127">Para obter instruções sobre a instalação, confira a página [Instruções de instalação do Linux de 64 bits para Java]( https://java.com/en/download/help/linux_x64_install.xml).</span><span class="sxs-lookup"><span data-stu-id="c6fef-127">For instructions on installation, see the [Linux 64-bit installation instructions for Java]( https://java.com/en/download/help/linux_x64_install.xml) page.</span></span>
        - <span data-ttu-id="c6fef-128">[Tempo de execução do SDK do .NET Core 1.0.3 ou do .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="c6fef-128">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
- <span data-ttu-id="c6fef-129">MacOS</span><span class="sxs-lookup"><span data-stu-id="c6fef-129">MacOS</span></span>

    - <span data-ttu-id="c6fef-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="c6fef-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="c6fef-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span><span class="sxs-lookup"><span data-stu-id="c6fef-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span></span> 
    - <span data-ttu-id="c6fef-132">[Java SE Runtime Environment versão 8 atualização 77 ou posterior](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="c6fef-132">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="c6fef-133">Para obter instruções sobre a instalação, confira a página [Instruções de instalação do Linux de 64 bits para Java](https://java.com/en/download/help/mac_install.xml).</span><span class="sxs-lookup"><span data-stu-id="c6fef-133">For instructions on installation, see the [Linux 64-bit installation instructions for Java](https://java.com/en/download/help/mac_install.xml) page.</span></span>
    - <span data-ttu-id="c6fef-134">[Tempo de execução do SDK do .NET Core 1.0.3 ou do .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="c6fef-134">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>

## <a name="install-data-lake-tools"></a><span data-ttu-id="c6fef-135">Instalar as Ferramentas do Data Lake</span><span class="sxs-lookup"><span data-stu-id="c6fef-135">Install Data Lake Tools</span></span>

<span data-ttu-id="c6fef-136">Após a instalação dos pré-requisitos, você pode instalar as Ferramentas do Data Lake para VS Code.</span><span class="sxs-lookup"><span data-stu-id="c6fef-136">After you install the prerequisites, you can install Data Lake Tools for VS Code.</span></span>

<span data-ttu-id="c6fef-137">**Para instalar as Ferramentas do Data Lake**</span><span class="sxs-lookup"><span data-stu-id="c6fef-137">**To install Data Lake Tools**</span></span>

1. <span data-ttu-id="c6fef-138">Abra o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="c6fef-138">Open Visual Studio Code.</span></span>
2. <span data-ttu-id="c6fef-139">Selecione Ctrl+P e insira o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c6fef-139">Select Ctrl+P, and then enter the following command:</span></span>
```
ext install usql-vscode-ext
```
<span data-ttu-id="c6fef-140">Você pode ver uma lista de extensões de código do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c6fef-140">You can see a list of Visual Studio code extensions.</span></span> <span data-ttu-id="c6fef-141">Por exemplo, as **Ferramentas do Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-141">One of them is **Azure Data Lake Tools**.</span></span>

3. <span data-ttu-id="c6fef-142">Selecione **Instalar** ao lado de **Ferramentas do Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-142">Select **Install** next to **Azure Data Lake Tools**.</span></span> <span data-ttu-id="c6fef-143">Depois de alguns segundos, o botão **Instalar** será alterado para **Recarregar**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-143">After a few seconds, the **Install** button changes to **Reload**.</span></span>
4. <span data-ttu-id="c6fef-144">Selecione **Recarregar** para ativar a extensão.</span><span class="sxs-lookup"><span data-stu-id="c6fef-144">Select **Reload** to activate the extension.</span></span>
5. <span data-ttu-id="c6fef-145">Selecione **OK** para confirmar.</span><span class="sxs-lookup"><span data-stu-id="c6fef-145">Select **OK** to confirm.</span></span> <span data-ttu-id="c6fef-146">Você pode ver as Ferramentas do Azure Data Lake no painel **Extensões**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-146">You can see Azure Data Lake Tools in the **Extensions** pane.</span></span>
    <span data-ttu-id="c6fef-147">![Painel de Extensões das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span><span class="sxs-lookup"><span data-stu-id="c6fef-147">![Data Lake Tools for Visual Studio Code Extensions pane](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span></span>

## <a name="activate-azure-data-lake-tools"></a><span data-ttu-id="c6fef-148">Ativar Ferramentas do Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="c6fef-148">Activate Azure Data Lake Tools</span></span>
<span data-ttu-id="c6fef-149">Crie um novo arquivo .usql ou abra um arquivo .usql existente para ativar a extensão.</span><span class="sxs-lookup"><span data-stu-id="c6fef-149">Create a new .usql file or open an existing .usql file to activate the extension.</span></span> 

## <a name="connect-to-azure"></a><span data-ttu-id="c6fef-150">Conecte-se ao Azure</span><span class="sxs-lookup"><span data-stu-id="c6fef-150">Connect to Azure</span></span>

<span data-ttu-id="c6fef-151">Antes de compilar e executar scripts U-SQL no Data Lake Analytics, você deve se conectar à sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6fef-151">Before you can compile and run U-SQL scripts in Data Lake Analytics, you must connect to your Azure account.</span></span>

<span data-ttu-id="c6fef-152">**Para se conectar ao Azure**</span><span class="sxs-lookup"><span data-stu-id="c6fef-152">**To connect to Azure**</span></span>

1.  <span data-ttu-id="c6fef-153">Selecione Ctrl + Shift + P para abrir a paleta de comandos.</span><span class="sxs-lookup"><span data-stu-id="c6fef-153">Select Ctrl+Shift+P to open the command palette.</span></span> 
2.  <span data-ttu-id="c6fef-154">Digite **ADL: Logon**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-154">Enter **ADL: Login**.</span></span> <span data-ttu-id="c6fef-155">As informações de logon aparecem no painel **Saída**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-155">The login information appears in the **Output** pane.</span></span>

    <span data-ttu-id="c6fef-156">![Paleta de comandos das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![Informações de logon do dispositivo das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span><span class="sxs-lookup"><span data-stu-id="c6fef-156">![Data Lake Tools for Visual Studio Code command palette](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
![Data Lake Tools for Visual Studio Code device login information](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span></span>
3. <span data-ttu-id="c6fef-157">Selecione Ctrl + clique na URL de logon: https://aka.ms/devicelogin para abrir a página da Web de logon.</span><span class="sxs-lookup"><span data-stu-id="c6fef-157">Select Ctrl+click on the login URL: https://aka.ms/devicelogin to open the login webpage.</span></span> <span data-ttu-id="c6fef-158">Insira o código **G567LX42V** na caixa de texto e selecione **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-158">Enter the code **G567LX42V** into the text box, and then select **Continue**.</span></span>

   ![Ferramentas do Data Lake para Visual Studio Code colar código de logon](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  <span data-ttu-id="c6fef-160">Siga as instruções para entrar na página da Web.</span><span class="sxs-lookup"><span data-stu-id="c6fef-160">Follow the instructions to sign in from the webpage.</span></span> <span data-ttu-id="c6fef-161">Quando você estiver conectado, o nome da conta do Azure será exibido na barra de status no canto inferior esquerdo da janela do **VS Code**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-161">When you're connected, your Azure account name appears on the status bar in the lower-left corner of the **VS Code** window.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="c6fef-162">Se sua conta tiver a autenticação por dois fatores habilitada, recomendamos o uso da autenticação por telefone em vez de usar um PIN.</span><span class="sxs-lookup"><span data-stu-id="c6fef-162">If your account has two factors enabled, we recommend that you use phone authentication rather than using a PIN.</span></span>

<span data-ttu-id="c6fef-163">Para sair, insira o comando **ADL: Logout**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-163">To sign out, enter the command **ADL: Logout**.</span></span>

## <a name="list-your-data-lake-analytics-accounts"></a><span data-ttu-id="c6fef-164">Listar suas contas do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="c6fef-164">List your Data Lake Analytics accounts</span></span>

<span data-ttu-id="c6fef-165">Para testar a conexão, obtenha uma lista de suas contas do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="c6fef-165">To test the connection, get a list of your Data Lake Analytics accounts.</span></span>

<span data-ttu-id="c6fef-166">**Para listar as contas do Data Lake Analytics em sua assinatura do Azure**</span><span class="sxs-lookup"><span data-stu-id="c6fef-166">**To list the Data Lake Analytics accounts under your Azure subscription**</span></span>

1. <span data-ttu-id="c6fef-167">Selecione Ctrl + Shift + P para abrir a paleta de comandos.</span><span class="sxs-lookup"><span data-stu-id="c6fef-167">Select Ctrl+Shift+P to open the command palette.</span></span>
2. <span data-ttu-id="c6fef-168">Insira **ADL: List Accounts**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-168">Enter **ADL: List Accounts**.</span></span> <span data-ttu-id="c6fef-169">As contas são exibidas no painel **Saída**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-169">The accounts appear in the **Output** pane.</span></span>

## <a name="open-the-sample-script"></a><span data-ttu-id="c6fef-170">Abrir o script de exemplo</span><span class="sxs-lookup"><span data-stu-id="c6fef-170">Open the sample script</span></span>
<span data-ttu-id="c6fef-171">Abra a paleta de comandos (Ctrl + Shift + P) e insira **ADL: Abrir Script de Exemplo**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-171">Open the command palette (Ctrl+Shift+P) and enter **ADL: Open Sample Script**.</span></span> <span data-ttu-id="c6fef-172">Isso abre outra instância deste exemplo.</span><span class="sxs-lookup"><span data-stu-id="c6fef-172">This opens another instance of this sample.</span></span> <span data-ttu-id="c6fef-173">Você também pode editar, configurar e enviar o script nessa instância.</span><span class="sxs-lookup"><span data-stu-id="c6fef-173">You can also edit, configure, and submit script on this instance.</span></span>

## <a name="work-with-u-sql"></a><span data-ttu-id="c6fef-174">Trabalhar com o U-SQL</span><span class="sxs-lookup"><span data-stu-id="c6fef-174">Work with U-SQL</span></span>

<span data-ttu-id="c6fef-175">Você precisa abrir um arquivo U-SQL ou uma pasta para trabalhar com o U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c6fef-175">You need open either a U-SQL file or a folder to work with U-SQL.</span></span>

<span data-ttu-id="c6fef-176">**Para abrir uma pasta para o projeto U-SQL**</span><span class="sxs-lookup"><span data-stu-id="c6fef-176">**To open a folder for your U-SQL project**</span></span>

1. <span data-ttu-id="c6fef-177">No Visual Studio Code, selecione o menu **Arquivo** e, em seguida, selecione **Abrir Pasta**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-177">From Visual Studio Code, select the **File** menu, and then select **Open Folder**.</span></span>
2. <span data-ttu-id="c6fef-178">Especifique uma pasta e selecione **Selecionar Pasta**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-178">Specify a folder, and then select **Select Folder**.</span></span>
3. <span data-ttu-id="c6fef-179">Selecione o menu **Arquivo** e selecione **Novo**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-179">Select the **File** menu, and then select **New**.</span></span> <span data-ttu-id="c6fef-180">Um arquivo Sem título-1 é adicionado ao projeto.</span><span class="sxs-lookup"><span data-stu-id="c6fef-180">An Untitled-1 file is added to the project.</span></span>
4. <span data-ttu-id="c6fef-181">Insira o código a seguir no arquivo Sem título-1:</span><span class="sxs-lookup"><span data-stu-id="c6fef-181">Enter the following code into the Untitled-1 file:</span></span>

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

    <span data-ttu-id="c6fef-182">O script cria um arquivo departments.csv com alguns dados incluídos na pasta /output.</span><span class="sxs-lookup"><span data-stu-id="c6fef-182">The script creates a departments.csv file with some data included in the /output folder.</span></span>

5. <span data-ttu-id="c6fef-183">Salve o arquivo como **myUSQL.usql** na pasta aberta.</span><span class="sxs-lookup"><span data-stu-id="c6fef-183">Save the file as **myUSQL.usql** in the opened folder.</span></span> <span data-ttu-id="c6fef-184">Um arquivo de configuração adltools_settings.json também é adicionado ao projeto.</span><span class="sxs-lookup"><span data-stu-id="c6fef-184">A adltools_settings.json configuration file is also added to the project.</span></span>
4. <span data-ttu-id="c6fef-185">Abra e configure adltools_settings.json com as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="c6fef-185">Open and configure adltools_settings.json with the following properties:</span></span>

    - <span data-ttu-id="c6fef-186">Conta: uma conta do Data Lake Analytics na sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6fef-186">Account:  A Data Lake Analytics account under your Azure subscription.</span></span>
    - <span data-ttu-id="c6fef-187">Banco de dados: um banco de dados em sua conta.</span><span class="sxs-lookup"><span data-stu-id="c6fef-187">Database: A database under your account.</span></span> <span data-ttu-id="c6fef-188">O padrão é **mestre**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-188">The default is **master**.</span></span>
    - <span data-ttu-id="c6fef-189">Esquema: um esquema em seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c6fef-189">Schema: A schema under your database.</span></span> <span data-ttu-id="c6fef-190">O padrão é **dbo**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-190">The default is **dbo**.</span></span>
    - <span data-ttu-id="c6fef-191">Configurações opcionais:</span><span class="sxs-lookup"><span data-stu-id="c6fef-191">Optional settings:</span></span>
        - <span data-ttu-id="c6fef-192">Prioridade: o intervalo de prioridade é de 1 a 1000, sendo que 1 é a prioridade mais alta.</span><span class="sxs-lookup"><span data-stu-id="c6fef-192">Priority: The priority range is from 1 to 1000 with 1 as the highest priority.</span></span> <span data-ttu-id="c6fef-193">O valor padrão é **1000**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-193">The default value is **1000**.</span></span>
        - <span data-ttu-id="c6fef-194">Paralelismo: o intervalo de paralelismo é de 1 a 150.</span><span class="sxs-lookup"><span data-stu-id="c6fef-194">Parallelism: The parallelism range is from 1 to 150.</span></span> <span data-ttu-id="c6fef-195">O valor padrão é o paralelismo máximo permitido em sua conta do Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="c6fef-195">The default value is the maximum parallelism allowed in your Azure Data Lake Analytics account.</span></span> 
        
        > [!NOTE] 
        > <span data-ttu-id="c6fef-196">Se as configurações forem inválidas, os valores padrão serão usados.</span><span class="sxs-lookup"><span data-stu-id="c6fef-196">If the settings are invalid, the default values are used.</span></span>

    ![Arquivo de configuração das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    <span data-ttu-id="c6fef-198">Uma conta de computador do Data Lake Analytics é necessária para compilar e executar trabalhos em U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c6fef-198">A compute Data Lake Analytics account is needed to compile and run U-SQL jobs.</span></span> <span data-ttu-id="c6fef-199">Você deve configurar a conta de computador para poder compilar e executar trabalho do U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c6fef-199">You must configure the computer account before you can compile and run U-SQL jobs.</span></span>
    
<span data-ttu-id="c6fef-200">Após salvar a configuração, as informações da conta, banco de dados e esquema aparecerão na barra de status na parte inferior esquerda do arquivo .usql correspondente.</span><span class="sxs-lookup"><span data-stu-id="c6fef-200">After the configuration is saved, the account, database, and schema information appears on the status bar at the bottom-left corner of the corresponding .usql file.</span></span> 
 
 
<span data-ttu-id="c6fef-201">Comparando com a abertura de um arquivo, quando você abre uma pasta, você pode:</span><span class="sxs-lookup"><span data-stu-id="c6fef-201">Compared to opening a file, when you open a folder you can:</span></span>

- <span data-ttu-id="c6fef-202">Usar um arquivo code-behind.</span><span class="sxs-lookup"><span data-stu-id="c6fef-202">Use a code-behind file.</span></span> <span data-ttu-id="c6fef-203">No modo de arquivo único, não há suporte para code-behind.</span><span class="sxs-lookup"><span data-stu-id="c6fef-203">In the single-file mode, code-behind is not supported.</span></span>
- <span data-ttu-id="c6fef-204">Usar um arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="c6fef-204">Use a configuration file.</span></span> <span data-ttu-id="c6fef-205">Quando você abre uma pasta, os scripts na pasta de trabalho compartilham um único arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="c6fef-205">When you open a folder, the scripts in the working folder share a single configuration file.</span></span>


<span data-ttu-id="c6fef-206">A compilação do script U-SQL é feita remotamente pelo serviço do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="c6fef-206">The U-SQL script compiles remotely through the Data Lake Analytics service.</span></span> <span data-ttu-id="c6fef-207">Quando você emite o comando **compile**, o script U-SQL é enviado à sua conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="c6fef-207">When you issue the **compile** command, the U-SQL script is sent to your Data Lake Analytics account.</span></span> <span data-ttu-id="c6fef-208">Mais tarde, o Visual Studio Code recebe o resultado da compilação.</span><span class="sxs-lookup"><span data-stu-id="c6fef-208">Later, Visual Studio Code receives the compilation result.</span></span> <span data-ttu-id="c6fef-209">Devido à compilação remota, o Visual Studio Code exige que você liste as informações para se conectar à conta do Data Lake Analytics no arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="c6fef-209">Due to the remote compilation, Visual Studio Code requires that you list the information to connect to your Data Lake Analytics account in the configuration file.</span></span>

<span data-ttu-id="c6fef-210">**Para compilar um script U-SQL**</span><span class="sxs-lookup"><span data-stu-id="c6fef-210">**To compile a U-SQL script**</span></span>

1. <span data-ttu-id="c6fef-211">Selecione Ctrl + Shift + P para abrir a paleta de comandos.</span><span class="sxs-lookup"><span data-stu-id="c6fef-211">Select Ctrl+Shift+P to open the command palette.</span></span> 
2. <span data-ttu-id="c6fef-212">Insira **ADL: Compilar Script**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-212">Enter **ADL: Compile Script**.</span></span> <span data-ttu-id="c6fef-213">Os resultados da compilação aparecem na janela **Saída**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-213">The compile results appear in the **Output** window.</span></span> <span data-ttu-id="c6fef-214">Também é possível clicar com o botão direito do mouse em um arquivo de script e, depois, selecionar **ADL: Compilar Script** para compilar um trabalho em U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c6fef-214">You can also right-click a script file, and then select **ADL: Compile Script** to compile a U-SQL job.</span></span> <span data-ttu-id="c6fef-215">O resultado da compilação aparece no painel **Saída**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-215">The compilation result appears in the **Output** pane.</span></span>
 

<span data-ttu-id="c6fef-216">**Para enviar um script U-SQL**</span><span class="sxs-lookup"><span data-stu-id="c6fef-216">**To submit a U-SQL script**</span></span>

1. <span data-ttu-id="c6fef-217">Selecione Ctrl + Shift + P para abrir a paleta de comandos.</span><span class="sxs-lookup"><span data-stu-id="c6fef-217">Select Ctrl+Shift+P to open the command palette.</span></span> 
2. <span data-ttu-id="c6fef-218">Insira **ADL: Enviar Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-218">Enter **ADL: Submit Job**.</span></span>  <span data-ttu-id="c6fef-219">Também é possível clicar com o botão direito do mouse em um arquivo de script e, depois, selecionar **ADL: Enviar Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-219">You can also right-click a script file, and then select **ADL: Submit Job**.</span></span> 

<span data-ttu-id="c6fef-220">Depois de enviar um trabalho em U-SQL, os logs de envio aparecerão na janela **Saída** no VS Code.</span><span class="sxs-lookup"><span data-stu-id="c6fef-220">After you submit a U-SQL job, the submission logs appear in the **Output** window in VS Code.</span></span> <span data-ttu-id="c6fef-221">Se o envio for bem-sucedido, a URL do trabalho também será exibida.</span><span class="sxs-lookup"><span data-stu-id="c6fef-221">If the submission is successful, the job URL appears as well.</span></span> <span data-ttu-id="c6fef-222">Você pode abrir a URL do trabalho em um navegador da Web para acompanhar o status do trabalho em tempo real.</span><span class="sxs-lookup"><span data-stu-id="c6fef-222">You can open the job URL in a web browser to track the real-time job status.</span></span>

<span data-ttu-id="c6fef-223">Para habilitar a saída dos detalhes do trabalho: defina **jobInformationOutputPath** no arquivo **vscode for u-sql_settings.json**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-223">To enable the output of the job details, set **jobInformationOutputPath** in the **vs code for the u-sql_settings.json** file.</span></span>
 
## <a name="use-a-code-behind-file"></a><span data-ttu-id="c6fef-224">Usar um arquivo code-behind</span><span class="sxs-lookup"><span data-stu-id="c6fef-224">Use a code-behind file</span></span>

<span data-ttu-id="c6fef-225">Um arquivo code-behind é um arquivo em C# associado a um único script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c6fef-225">A code-behind file is a C# file associated with a single U-SQL script.</span></span> <span data-ttu-id="c6fef-226">Você pode definir um script dedicado a UDO, UDA, UDT e UDF no arquivo code-behind.</span><span class="sxs-lookup"><span data-stu-id="c6fef-226">You can define a script dedicated to UDO, UDA, UDT, and UDF in the code-behind file.</span></span> <span data-ttu-id="c6fef-227">UDO, UDA, UDT e UDF podem ser usados diretamente no script sem registrar o assembly primeiro.</span><span class="sxs-lookup"><span data-stu-id="c6fef-227">The UDO, UDA, UDT, and UDF can be used directly in the script without registering the assembly first.</span></span> <span data-ttu-id="c6fef-228">O arquivo code-behind é colocado na mesma pasta que seu arquivo de script U-SQL de emparelhamento.</span><span class="sxs-lookup"><span data-stu-id="c6fef-228">The code-behind file is put in the same folder as its peering U-SQL script file.</span></span> <span data-ttu-id="c6fef-229">Se o script for chamado de xxx.usql, o code-behind será chamado de xxx.usql.cs.</span><span class="sxs-lookup"><span data-stu-id="c6fef-229">If the script is named xxx.usql, the code-behind is named as xxx.usql.cs.</span></span> <span data-ttu-id="c6fef-230">Se você excluir manualmente o arquivo code-behind, o recurso code-behind será desabilitado para seu script U-SQL associado.</span><span class="sxs-lookup"><span data-stu-id="c6fef-230">If you manually delete the code-behind file, the code-behind feature is disabled for its associated U-SQL script.</span></span> <span data-ttu-id="c6fef-231">Para saber mais sobre como escrever código do cliente para script U-SQL, veja [Writing and Using Custom Code in U-SQL – User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/) (Escrevendo e usado código personalizado em U-SQL — Funções Definidas pelo Usuário).</span><span class="sxs-lookup"><span data-stu-id="c6fef-231">For more information about writing customer code for U-SQL script, see [Writing and Using Custom Code in U-SQL: User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span></span>

<span data-ttu-id="c6fef-232">Para dar suporte ao code-behind, é necessário abrir uma pasta de trabalho.</span><span class="sxs-lookup"><span data-stu-id="c6fef-232">To support code-behind, you must open a working folder.</span></span> 

<span data-ttu-id="c6fef-233">**Para gerar um arquivo code-behind**</span><span class="sxs-lookup"><span data-stu-id="c6fef-233">**To generate a code-behind file**</span></span>

1. <span data-ttu-id="c6fef-234">Abra um arquivo de origem.</span><span class="sxs-lookup"><span data-stu-id="c6fef-234">Open a source file.</span></span> 
2. <span data-ttu-id="c6fef-235">Selecione Ctrl + Shift + P para abrir a paleta de comandos.</span><span class="sxs-lookup"><span data-stu-id="c6fef-235">Select Ctrl+Shift+P to open the command palette.</span></span>
3. <span data-ttu-id="c6fef-236">Insira **ADL: Gerar Code-Behind**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-236">Enter **ADL: Generate Code Behind**.</span></span> <span data-ttu-id="c6fef-237">Um arquivo code-behind é criado na mesma pasta.</span><span class="sxs-lookup"><span data-stu-id="c6fef-237">A code-behind file is created in the same folder.</span></span> 

<span data-ttu-id="c6fef-238">Também é possível clicar com o botão direito em um arquivo de script e, depois, selecionar **ADL: Gerar Code Behind**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-238">You can also right-click a script file, and then select **ADL: Generate Code Behind**.</span></span> 

<span data-ttu-id="c6fef-239">Compilar e enviar um script U-SQL com um arquivo code-behind é o mesmo que o arquivo de script U-SQL autônomo.</span><span class="sxs-lookup"><span data-stu-id="c6fef-239">To compile and submit a U-SQL script with a code-behind file is the same as with the standalone U-SQL script file.</span></span>

<span data-ttu-id="c6fef-240">As duas capturas de tela que se seguem mostram um arquivo code-behind e seu arquivo de script U-SQL associado:</span><span class="sxs-lookup"><span data-stu-id="c6fef-240">The following two screenshots show a code-behind file and its associated U-SQL script file:</span></span>
 
![Code-behind das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![Arquivo de script code-behind das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a><span data-ttu-id="c6fef-243">Usar assemblies</span><span class="sxs-lookup"><span data-stu-id="c6fef-243">Use assemblies</span></span>

<span data-ttu-id="c6fef-244">Para obter informações sobre como desenvolver assemblies, confira [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md) (Desenvolver assemblies U-SQL para trabalhos do Azure Data Lake Analytics).</span><span class="sxs-lookup"><span data-stu-id="c6fef-244">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>

<span data-ttu-id="c6fef-245">Use as Ferramentas do Data Lake para registrar assemblies de código personalizado no catálogo do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="c6fef-245">You can use Data Lake Tools to register custom code assemblies in the Data Lake Analytics catalog.</span></span>

<span data-ttu-id="c6fef-246">**Para registrar um assembly**</span><span class="sxs-lookup"><span data-stu-id="c6fef-246">**To register an assembly**</span></span>

<span data-ttu-id="c6fef-247">Você pode registrar o assembly por meio dos comandos **ADL: Registrar Assembly** ou **ADL: Registrar Assembly através da Configuração**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-247">You can register the assembly through the **ADL: Register Assembly** or **ADL: Register Assembly through Configuration** commands.</span></span>

<span data-ttu-id="c6fef-248">**Para registrar por meio do comando ADL: Registrar Assembly**</span><span class="sxs-lookup"><span data-stu-id="c6fef-248">**To register through the ADL: Register Assembly command**</span></span>
1.  <span data-ttu-id="c6fef-249">Selecione Ctrl + Shift + P para abrir a paleta de comandos.</span><span class="sxs-lookup"><span data-stu-id="c6fef-249">Select Ctrl+Shift+P to open the command palette.</span></span>
2.  <span data-ttu-id="c6fef-250">Digite **ADL: Registrar Assembly**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-250">Enter **ADL: Register Assembly**.</span></span> 
3.  <span data-ttu-id="c6fef-251">Especifique o caminho do assembly local.</span><span class="sxs-lookup"><span data-stu-id="c6fef-251">Specify the local assembly path.</span></span> 
4.  <span data-ttu-id="c6fef-252">Selecione uma conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="c6fef-252">Select a Data Lake Analytics account.</span></span>
5.  <span data-ttu-id="c6fef-253">Selecione um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c6fef-253">Select a database.</span></span>

<span data-ttu-id="c6fef-254">Resultados: o portal será aberto em um navegador e exibirá o processo de registro do assembly.</span><span class="sxs-lookup"><span data-stu-id="c6fef-254">Results: The portal is opened in a browser and displays the assembly registration process.</span></span>  

<span data-ttu-id="c6fef-255">Outra maneira conveniente de disparar o comando **ADL: Registrar Assembly** é clicar com o botão direito no arquivo .dll no Explorador de Arquivos.</span><span class="sxs-lookup"><span data-stu-id="c6fef-255">Another convenient way to trigger the **ADL: Register Assembly** command is to right-click the .dll file in File Explorer.</span></span> 

<span data-ttu-id="c6fef-256">**Para registrar por meio do comando ADL: Registrar o Assembly através da Configuração**</span><span class="sxs-lookup"><span data-stu-id="c6fef-256">**To register though the ADL: Register Assembly through Configuration command**</span></span>
1.  <span data-ttu-id="c6fef-257">Selecione Ctrl + Shift + P para abrir a paleta de comandos.</span><span class="sxs-lookup"><span data-stu-id="c6fef-257">Select Ctrl+Shift+P to open the command palette.</span></span>
2.  <span data-ttu-id="c6fef-258">Digite **ADL: Registrar Assembly através da Configuração**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-258">Enter **ADL: Register Assembly through Configuration**.</span></span> 
3.  <span data-ttu-id="c6fef-259">Especifique o caminho do assembly local.</span><span class="sxs-lookup"><span data-stu-id="c6fef-259">Specify the local assembly path.</span></span> 
4.  <span data-ttu-id="c6fef-260">O arquivo JSON será exibido.</span><span class="sxs-lookup"><span data-stu-id="c6fef-260">The JSON file is displayed.</span></span> <span data-ttu-id="c6fef-261">Examine e edite as dependências do assembly e os parâmetros de recursos, se necessário.</span><span class="sxs-lookup"><span data-stu-id="c6fef-261">Review and edit the assembly dependencies and resource parameters, if needed.</span></span> <span data-ttu-id="c6fef-262">As instruções serão exibidas na janela **Saída**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-262">Instructions are displayed in the **Output** window.</span></span> <span data-ttu-id="c6fef-263">Para prosseguir com o registro do assembly, salve (CTRL+S) o arquivo JSON.</span><span class="sxs-lookup"><span data-stu-id="c6fef-263">To proceed to the assembly registration, save (Ctrl+S) the JSON file.</span></span>

![Code-behind das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- <span data-ttu-id="c6fef-265">Dependências de assembly: as Ferramentas do Azure Data Lake detectam automaticamente se a DLL tem todas as dependências.</span><span class="sxs-lookup"><span data-stu-id="c6fef-265">Assembly dependencies: Azure Data Lake Tools autodetects whether the DLL has any dependencies.</span></span> <span data-ttu-id="c6fef-266">As dependências são exibidas no arquivo JSON, após a detecção.</span><span class="sxs-lookup"><span data-stu-id="c6fef-266">The dependencies are displayed in the JSON file after they are detected.</span></span> 
>- <span data-ttu-id="c6fef-267">Recursos: você pode carregar os recursos de DLL (por exemplo, .txt, .png e .csv.) como parte do registro do assembly.</span><span class="sxs-lookup"><span data-stu-id="c6fef-267">Resources: You can upload your DLL resources (for example, .txt, .png, and .csv) as part of the assembly registration.</span></span> 

<span data-ttu-id="c6fef-268">Outra maneira conveniente de disparar o comando **ADL: Registrar Assembly através da Configuração** é clicar com o botão direito no arquivo .dll no Explorador de Arquivos.</span><span class="sxs-lookup"><span data-stu-id="c6fef-268">Another way to trigger the **ADL: Register Assembly through Configuration** command is to right-click the .dll file in File Explorer.</span></span> 

<span data-ttu-id="c6fef-269">O código de U-SQL a seguir demonstra como chamar um assembly.</span><span class="sxs-lookup"><span data-stu-id="c6fef-269">The following U-SQL code demonstrates how to call an assembly.</span></span> <span data-ttu-id="c6fef-270">No exemplo, o nome do assembly é *test*.</span><span class="sxs-lookup"><span data-stu-id="c6fef-270">In the sample, the assembly name is *test*.</span></span>

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
    TO @"Sample/SearchLogtest.txt" 
    USING Outputters.Tsv();
```


## <a name="access-the-data-lake-analytics-catalog"></a><span data-ttu-id="c6fef-271">Acessar o catálogo do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="c6fef-271">Access the Data Lake Analytics catalog</span></span>

<span data-ttu-id="c6fef-272">Depois que estiver conectado ao Azure, você poderá usar as seguintes etapas para acessar o catálogo do U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c6fef-272">After you have connected to Azure, you can use the following steps to access the U-SQL catalog.</span></span>

<span data-ttu-id="c6fef-273">**Para acessar os metadados do Azure Data Lake Analytics**</span><span class="sxs-lookup"><span data-stu-id="c6fef-273">**To access the Azure Data Lake Analytics metadata**</span></span>

1.  <span data-ttu-id="c6fef-274">Pressione CTRL+SHIFT+P e insira **ADL: Listar Tabelas**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-274">Select Ctrl+Shift+P, and then enter **ADL: List Tables**.</span></span>
2.  <span data-ttu-id="c6fef-275">Selecione uma das contas do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="c6fef-275">Select one of the Data Lake Analytics accounts.</span></span>
3.  <span data-ttu-id="c6fef-276">Selecione um dos bancos de dados do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="c6fef-276">Select one of the Data Lake Analytics databases.</span></span>
4.  <span data-ttu-id="c6fef-277">Selecione um dos esquemas.</span><span class="sxs-lookup"><span data-stu-id="c6fef-277">Select one of the schemas.</span></span> <span data-ttu-id="c6fef-278">Você pode ver a lista de tabelas.</span><span class="sxs-lookup"><span data-stu-id="c6fef-278">You can see the list of tables.</span></span>

## <a name="view-data-lake-analytics-jobs"></a><span data-ttu-id="c6fef-279">Exibir trabalhos do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="c6fef-279">View Data Lake Analytics jobs</span></span>

<span data-ttu-id="c6fef-280">**Para exibir trabalhos do Data Lake Analytics**</span><span class="sxs-lookup"><span data-stu-id="c6fef-280">**To view Data Lake Analytics jobs**</span></span>
1.  <span data-ttu-id="c6fef-281">Abra a paleta de comandos (Ctrl+Shift+P) e escolha **ADL: Mostrar Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-281">Open the command palette (Ctrl+Shift+P) and select **ADL: Show Job**.</span></span> 
2.  <span data-ttu-id="c6fef-282">Selecione uma conta do Data Lake Analytics ou local.</span><span class="sxs-lookup"><span data-stu-id="c6fef-282">Select a Data Lake Analytics or local account.</span></span> 
3.  <span data-ttu-id="c6fef-283">Aguarde a exibição da lista de trabalhos da conta.</span><span class="sxs-lookup"><span data-stu-id="c6fef-283">Wait for the jobs list for the account to appear.</span></span>
4.  <span data-ttu-id="c6fef-284">Selecione um trabalho da lista. As Ferramentas do Data Lake abrem os detalhes do trabalho no Portal do Azure e exibem o arquivo JobInfo no VS Code.</span><span class="sxs-lookup"><span data-stu-id="c6fef-284">Select a job from job list, Data Lake Tools opens the job details in the Azure portal and displays the JobInfo file in VS Code.</span></span>

![Tipos de objeto do IntelliSense das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a><span data-ttu-id="c6fef-286">Integração do Armazenamento do Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="c6fef-286">Azure Data Lake Storage integration</span></span>

<span data-ttu-id="c6fef-287">Você pode usar comandos relacionados ao Armazenamento do Azure Data Lake:</span><span class="sxs-lookup"><span data-stu-id="c6fef-287">You can use Azure Data Lake Storage-related commands to:</span></span>
 - <span data-ttu-id="c6fef-288">Procure nos recursos do Armazenamento do Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="c6fef-288">Browse through the Azure Data Lake Storage resources.</span></span> 
 - <span data-ttu-id="c6fef-289">Visualize o arquivo de Armazenamento do Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="c6fef-289">Preview the Azure Data Lake Storage file.</span></span>  
 - <span data-ttu-id="c6fef-290">Carregue o arquivo diretamente no Armazenamento do Azure Data Lake no VS Code.</span><span class="sxs-lookup"><span data-stu-id="c6fef-290">Upload the file directly to Azure Data Lake Storage in VS Code.</span></span> 

### <a name="list-the-storage-path"></a><span data-ttu-id="c6fef-291">Listar caminho de armazenamento</span><span class="sxs-lookup"><span data-stu-id="c6fef-291">List the storage path</span></span> 
<span data-ttu-id="c6fef-292">Você pode listar o caminho de armazenamento por meio da paleta de comandos ou clicando com o botão direito do mouse.</span><span class="sxs-lookup"><span data-stu-id="c6fef-292">You can list the storage path through the command palette or through right-click.</span></span>

<span data-ttu-id="c6fef-293">**Para listar o caminho de armazenamento por meio da paleta de comandos**</span><span class="sxs-lookup"><span data-stu-id="c6fef-293">**To list the storage path through the command palette**</span></span>

1.  <span data-ttu-id="c6fef-294">Abra a paleta de comandos (Ctrl+Shift+P) e insira **ADL: Listar Caminho de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-294">Open the command palette (Ctrl+Shift+P) and enter **ADL: List Storage Path**.</span></span>

    ![Listar caminho de armazenamento das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  <span data-ttu-id="c6fef-296">Selecione sua maneira preferida para listar o caminho de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c6fef-296">Select your preferred way for listing the storage path.</span></span> <span data-ttu-id="c6fef-297">Esta passagem usa **Inserir um caminho** como exemplo.</span><span class="sxs-lookup"><span data-stu-id="c6fef-297">This passage uses **Enter a path** as an example.</span></span>

    ![Uma forma de listar o caminho de armazenamento das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- <span data-ttu-id="c6fef-299">O VS Code mantém o último caminho visitado em toda conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="c6fef-299">VS Code keeps the last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="c6fef-300">Por exemplo: /tt/ss.</span><span class="sxs-lookup"><span data-stu-id="c6fef-300">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="c6fef-301">Procurar do caminho raiz: o caminho raiz da lista de sua conta do Data Lake Analytics selecionada, ou um caminho local.</span><span class="sxs-lookup"><span data-stu-id="c6fef-301">Browser from root path: The list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="c6fef-302">Inserir um caminho: lista um caminho especificado de sua conta do Data Lake Analytics selecionada, ou um caminho local.</span><span class="sxs-lookup"><span data-stu-id="c6fef-302">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>
    
3. <span data-ttu-id="c6fef-303">Selecione uma conta do caminho local ou uma conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="c6fef-303">Select an account from the local path or a Data Lake Analytics account.</span></span>

    ![Ferramentas do Data Lake para Visual Studio Code selecionar mais](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. <span data-ttu-id="c6fef-305">Selecione **mais** para listar mais contas do Data Lake Analytics e, depois, selecione uma conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="c6fef-305">Select **more** to list more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

    ![Ferramentas do Data Lake para Visual Studio Code selecionar uma conta](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  <span data-ttu-id="c6fef-307">Insira um caminho de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6fef-307">Enter an Azure storage path.</span></span> <span data-ttu-id="c6fef-308">Por exemplo, /output.</span><span class="sxs-lookup"><span data-stu-id="c6fef-308">For example, /output.</span></span>

    ![Inserir caminho de armazenamento das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  <span data-ttu-id="c6fef-310">Resultados: a paleta de comandos lista as informações de caminho com base em suas entradas.</span><span class="sxs-lookup"><span data-stu-id="c6fef-310">Results: The command palette lists the path information based on your entries.</span></span>

    ![Listar resultados do caminho de armazenamento das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

<span data-ttu-id="c6fef-312">Uma maneira mais adequada de listar o caminho relativo é pelo menu de contexto do botão direito do mouse.</span><span class="sxs-lookup"><span data-stu-id="c6fef-312">A more convenient way to list the relative path is through the right-click context menu.</span></span>

<span data-ttu-id="c6fef-313">**Para listar o caminho de armazenamento clicando com o botão direito**</span><span class="sxs-lookup"><span data-stu-id="c6fef-313">**To list the storage path through right-click**</span></span>

1.  <span data-ttu-id="c6fef-314">Clique com botão direito na cadeia de caracteres do caminho para selecionar **Listar Caminho de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-314">Right-click the path string to select **List Storage Path**.</span></span>

       ![Menu de contexto acessado com o botão direito das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. <span data-ttu-id="c6fef-316">O caminho relativo selecionado aparece na paleta de comandos.</span><span class="sxs-lookup"><span data-stu-id="c6fef-316">The selected relative path appears in the command palette.</span></span>

   ![Caminho relativo selecionado das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  <span data-ttu-id="c6fef-318">Selecione uma conta do caminho local ou uma conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="c6fef-318">Select an account from the local path or a Data Lake Analytics account.</span></span>

       ![Ferramentas do Data Lake para Visual Studio Code selecionar uma conta](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  <span data-ttu-id="c6fef-320">Resultados: a paleta de comandos lista as pastas e arquivos do caminho atual.</span><span class="sxs-lookup"><span data-stu-id="c6fef-320">Results: The command palette lists the folders and files for the current path.</span></span>

       ![Ferramentas do Data Lake para Visual Studio Code no caminho atual](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-the-storage-file"></a><span data-ttu-id="c6fef-322">Visualizar arquivo de armazenamento</span><span class="sxs-lookup"><span data-stu-id="c6fef-322">Preview the storage file</span></span>
<span data-ttu-id="c6fef-323">Você pode visualizar o arquivo de armazenamento por meio da paleta de comandos ou clicando com o botão direito do mouse.</span><span class="sxs-lookup"><span data-stu-id="c6fef-323">You can preview the storage file through the command palette or through right-click.</span></span>

<span data-ttu-id="c6fef-324">**Para visualizar o arquivo de armazenamento por meio da paleta de comandos**</span><span class="sxs-lookup"><span data-stu-id="c6fef-324">**To preview the storage file through the command palette**</span></span>

1.  <span data-ttu-id="c6fef-325">Abra a paleta de comandos (Ctrl+Shift+P) e escolha **ADL: Visualizar Arquivo de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-325">Open the command palette (Ctrl+Shift+P) and enter **ADL: Preview Storage File**.</span></span>

       ![Visualizar arquivo de armazenamento das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  <span data-ttu-id="c6fef-327">Selecione uma conta do caminho local ou uma conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="c6fef-327">Select an account from the local path or a Data Lake Analytics account.</span></span>

       ![Listar conta das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="c6fef-329">Selecione **mais** para listar mais contas do Data Lake Analytics e, depois, selecione uma conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="c6fef-329">Select **more** to list more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

       ![Ferramentas do Data Lake para Visual Studio Code selecionar uma conta](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  <span data-ttu-id="c6fef-331">Insira um caminho ou arquivo de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6fef-331">Enter an Azure storage path or file.</span></span> <span data-ttu-id="c6fef-332">Por exemplo: /output/SearchLog.txt.</span><span class="sxs-lookup"><span data-stu-id="c6fef-332">For example, /output/SearchLog.txt.</span></span>

       ![Inserir caminho e arquivo de armazenamento das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  <span data-ttu-id="c6fef-334">Resultados: a paleta de comandos lista as informações de caminho com base em suas entradas.</span><span class="sxs-lookup"><span data-stu-id="c6fef-334">Results: The command palette lists the path information based on your entries.</span></span>

       ![Ferramentas do Data Lake para Visual Studio Code Resultado da visualização do arquivo](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

<span data-ttu-id="c6fef-336">**Para listar o caminho de armazenamento clicando com o botão direito**</span><span class="sxs-lookup"><span data-stu-id="c6fef-336">**To list the storage path through right-click**</span></span>

1.  <span data-ttu-id="c6fef-337">Para visualizar um arquivo, clique com botão direito do mouse no caminho do arquivo.</span><span class="sxs-lookup"><span data-stu-id="c6fef-337">To preview a file, right-click the file path.</span></span>

   ![Menu de contexto acessado com o botão direito das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  <span data-ttu-id="c6fef-339">Selecione uma conta do caminho local ou uma conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="c6fef-339">Select an account from the local path or a Data Lake Analytics account.</span></span>

       ![Ferramentas do Data Lake para Visual Studio Code selecionar uma conta](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="c6fef-341">Resultados: o VS Code exibe os resultados da visualização do arquivo.</span><span class="sxs-lookup"><span data-stu-id="c6fef-341">Results: VS Code displays the preview results of the file.</span></span>

       ![Ferramentas do Data Lake para Visual Studio Code Resultado da visualização do arquivo](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a><span data-ttu-id="c6fef-343">Carregar um arquivo</span><span class="sxs-lookup"><span data-stu-id="c6fef-343">Upload a file</span></span> 

<span data-ttu-id="c6fef-344">Você pode carregar arquivos inserindo os comandos **ADL: Carregar Arquivo** ou **ADL: Carregar Arquivo através da Configuração**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-344">You can upload files by entering the commands **ADL: Upload File** or **ADL: Upload File through Configuration**.</span></span>

<span data-ttu-id="c6fef-345">**Para carregar arquivos por meio do comando ADL: Carregar Arquivo**</span><span class="sxs-lookup"><span data-stu-id="c6fef-345">**To upload files though the ADL: Upload File command**</span></span>
1. <span data-ttu-id="c6fef-346">Pressione CTRL+SHIFT+P para abrir a paleta de comandos ou clique com o botão direito no editor de scripts e insira **Carregar Arquivo**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-346">Select Ctrl+Shift+P to open the command palette or right-click the script editor, and then enter **Upload File**.</span></span>
2.  <span data-ttu-id="c6fef-347">Para carregar o arquivo, insira um caminho local.</span><span class="sxs-lookup"><span data-stu-id="c6fef-347">To upload the file, enter a local path.</span></span>

    ![Inserir caminho local das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. <span data-ttu-id="c6fef-349">Selecione uma das maneiras de listagem do caminho de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c6fef-349">Select one of the ways of listing the storage path.</span></span> <span data-ttu-id="c6fef-350">Esta passagem usa **Inserir um caminho** como exemplo.</span><span class="sxs-lookup"><span data-stu-id="c6fef-350">This passage uses **Enter a path** as an example.</span></span>

    ![Listar caminho de armazenamento das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- <span data-ttu-id="c6fef-352">O VS Code mantém o último caminho visitado em toda conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="c6fef-352">VS Code keeps the last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="c6fef-353">Por exemplo: /tt/ss.</span><span class="sxs-lookup"><span data-stu-id="c6fef-353">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="c6fef-354">Procurar do caminho raiz: o caminho raiz da lista de sua conta do Data Lake Analytics selecionada, ou um caminho local.</span><span class="sxs-lookup"><span data-stu-id="c6fef-354">Browser from root path: The list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="c6fef-355">Inserir um caminho: lista um caminho especificado de sua conta do Data Lake Analytics selecionada, ou um caminho local.</span><span class="sxs-lookup"><span data-stu-id="c6fef-355">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>

4. <span data-ttu-id="c6fef-356">Selecione uma conta do caminho local ou uma conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="c6fef-356">Select an account from the local path or a Data Lake Analytics account.</span></span>

    ![Armazenamento acionado pelo botão direito das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. <span data-ttu-id="c6fef-358">Insira um caminho de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6fef-358">Enter an Azure storage path.</span></span> <span data-ttu-id="c6fef-359">Por exemplo: /output.</span><span class="sxs-lookup"><span data-stu-id="c6fef-359">For example: /output.</span></span>

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. <span data-ttu-id="c6fef-360">Encontre o caminho de seu armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6fef-360">Find your Azure storage path.</span></span> <span data-ttu-id="c6fef-361">Selecione **Escolher pasta atual**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-361">Select **Choose current folder**.</span></span>

    ![Selecionar uma pasta das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  <span data-ttu-id="c6fef-363">Resultado: a janela **Saída** exibe o status de upload do arquivo.</span><span class="sxs-lookup"><span data-stu-id="c6fef-363">Results: The **Output** window displays the file upload status.</span></span>

       ![Status de upload das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

<span data-ttu-id="c6fef-365">**Para carregar os arquivos por meio do comando ADL: Carregar Arquivo através da Configuração**</span><span class="sxs-lookup"><span data-stu-id="c6fef-365">**To upload files though the ADL: Upload File through Configuration command**</span></span>
1.  <span data-ttu-id="c6fef-366">Pressione CTRL+SHIFT+P para abrir a paleta de comandos ou clique com o botão direito do mouse no editor de scripts e, em seguida, insira **Carregar Arquivo através da Configuração**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-366">Select Ctrl+Shift+P to open the command palette or right-click the script editor, and then enter **Upload File through Configuration**.</span></span>
2.  <span data-ttu-id="c6fef-367">O VS Code exibe um arquivo JSON.</span><span class="sxs-lookup"><span data-stu-id="c6fef-367">VS Code displays a JSON file.</span></span> <span data-ttu-id="c6fef-368">Você pode inserir os caminhos de arquivo e carregar vários arquivos ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="c6fef-368">You can enter file paths and upload multiple files at the same time.</span></span> <span data-ttu-id="c6fef-369">As instruções serão exibidas na janela **Saída**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-369">Instructions are displayed in the **Output** window.</span></span> <span data-ttu-id="c6fef-370">para prosseguir com o upload do arquivo, salve (CTRL+S) o arquivo JSON.</span><span class="sxs-lookup"><span data-stu-id="c6fef-370">To proceed to upload the file, save (Ctrl+S) the JSON file.</span></span>

       ![Inserir arquivo das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  <span data-ttu-id="c6fef-372">Resultado: a janela **Saída** exibe o status de upload do arquivo.</span><span class="sxs-lookup"><span data-stu-id="c6fef-372">Results: The **Output** window displays the file upload status.</span></span>

       ![Status de upload das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

<span data-ttu-id="c6fef-374">Outra maneira de carregar um arquivo para armazenamento é clicar com o botão direito do mouse no menu no caminho completo do arquivo, ou no caminho relativo do arquivo no editor de scripts.</span><span class="sxs-lookup"><span data-stu-id="c6fef-374">Another way to upload a file to storage is through the right-click menu on the file's full path or the file's relative path in the script editor.</span></span> <span data-ttu-id="c6fef-375">Insira o caminho do arquivo local e selecione a conta.</span><span class="sxs-lookup"><span data-stu-id="c6fef-375">Enter the local file path, and then select the account.</span></span> <span data-ttu-id="c6fef-376">A janela **Saída** exibe o status de upload.</span><span class="sxs-lookup"><span data-stu-id="c6fef-376">The **Output** window displays the upload status.</span></span> 

### <a name="open-azure-storage-explorer"></a><span data-ttu-id="c6fef-377">Abra o Gerenciador de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="c6fef-377">Open Azure Storage Explorer</span></span>
<span data-ttu-id="c6fef-378">Você pode abrir o **Gerenciador de Armazenamento do Azure** inserindo o comando **ADL: Abrir o Gerenciador Web de Armazenamento do Azure** ou selecionando-o no menu de contexto acionado com o botão direito do mouse.</span><span class="sxs-lookup"><span data-stu-id="c6fef-378">You can open **Azure Storage Explorer** by entering the command **ADL: Open Web Azure Storage Explorer** or by selecting it from the right-click context menu.</span></span>

<span data-ttu-id="c6fef-379">**Para abrir o Gerenciador de Armazenamento do Azure**</span><span class="sxs-lookup"><span data-stu-id="c6fef-379">**To open Azure Storage Explorer**</span></span>

1. <span data-ttu-id="c6fef-380">Selecione Ctrl + Shift + P para abrir a paleta de comandos.</span><span class="sxs-lookup"><span data-stu-id="c6fef-380">Select Ctrl+Shift+P to open the command palette.</span></span>
2. <span data-ttu-id="c6fef-381">Insira **Abrir Gerenciador Web do Armazenamento do Azure** ou clique com o botão direito do mouse em um caminho relativo, ou no caminho completo no editor de scripts, e escolha **Abrir Gerenciador Web do Armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="c6fef-381">Enter **Open Web Azure Storage Explorer** or right-click on a relative path or the full path in the script editor, and then select **Open Web Azure Storage Explorer**.</span></span>
3. <span data-ttu-id="c6fef-382">Selecione uma conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="c6fef-382">Select a Data Lake Analytics account.</span></span>

<span data-ttu-id="c6fef-383">As Ferramentas do Data Lake abrem o caminho de armazenamento do Azure no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6fef-383">Data Lake Tools opens the Azure storage path in the Azure portal.</span></span> <span data-ttu-id="c6fef-384">Você pode encontrar o caminho e visualizar o arquivo na Web.</span><span class="sxs-lookup"><span data-stu-id="c6fef-384">You can find the path and preview the file from the web.</span></span>

### <a name="local-run-and-local-debug-for-windows-users"></a><span data-ttu-id="c6fef-385">Depuração local e execução local para usuários do Windows</span><span class="sxs-lookup"><span data-stu-id="c6fef-385">Local run and local debug for Windows users</span></span>
<span data-ttu-id="c6fef-386">A execução local de U-SQL testa seus dados locais e valida o script localmente, antes que seu código seja publicado no Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="c6fef-386">U-SQL local run tests your local data and validates your script locally, before your code is published to Data Lake Analytics.</span></span> <span data-ttu-id="c6fef-387">O recurso de depuração local permite que você conclua as seguintes tarefas antes que seu código seja enviado ao Data Lake Analytics:</span><span class="sxs-lookup"><span data-stu-id="c6fef-387">The local debug feature enables you to complete the following tasks before your code is submitted to Data Lake Analytics:</span></span> 
- <span data-ttu-id="c6fef-388">Depure o code-behind em C#.</span><span class="sxs-lookup"><span data-stu-id="c6fef-388">Debug your C# code-behind.</span></span> 
- <span data-ttu-id="c6fef-389">Explore o código.</span><span class="sxs-lookup"><span data-stu-id="c6fef-389">Step through the code.</span></span> 
- <span data-ttu-id="c6fef-390">Valide o script localmente.</span><span class="sxs-lookup"><span data-stu-id="c6fef-390">Validate your script locally.</span></span>

<span data-ttu-id="c6fef-391">Para obter instruções sobre a execução e a depuração local, confira [Execução local do U-SQL e depuração local com o Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="c6fef-391">For instructions on local run and local debug, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>

## <a name="additional-features"></a><span data-ttu-id="c6fef-392">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c6fef-392">Additional features</span></span>

<span data-ttu-id="c6fef-393">As Ferramentas do Data Lake para VS Code dão suporte aos seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="c6fef-393">Data Lake Tools for VS Code supports the following features:</span></span>

-   <span data-ttu-id="c6fef-394">Preenchimento automático de IntelliSense: as sugestões são exibidas em janelas pop-up ao redor dos itens, como palavras-chave, métodos e variáveis.</span><span class="sxs-lookup"><span data-stu-id="c6fef-394">IntelliSense auto-complete: Suggestions appear in pop-up windows around items, such as keywords, methods, and variables.</span></span> <span data-ttu-id="c6fef-395">Os diferentes ícones representam diferentes tipos dos objetos:</span><span class="sxs-lookup"><span data-stu-id="c6fef-395">Different icons represent different types of the objects:</span></span>

    - <span data-ttu-id="c6fef-396">Tipo de dados de Scala</span><span class="sxs-lookup"><span data-stu-id="c6fef-396">Scala data type</span></span>
    - <span data-ttu-id="c6fef-397">Tipos de dados complexos</span><span class="sxs-lookup"><span data-stu-id="c6fef-397">Complex data type</span></span>
    - <span data-ttu-id="c6fef-398">UDTs Internos</span><span class="sxs-lookup"><span data-stu-id="c6fef-398">Built-in UDTs</span></span>
    - <span data-ttu-id="c6fef-399">Coleções e classes .Net</span><span class="sxs-lookup"><span data-stu-id="c6fef-399">.NET collection and classes</span></span>
    - <span data-ttu-id="c6fef-400">Expressões em C#</span><span class="sxs-lookup"><span data-stu-id="c6fef-400">C# expressions</span></span>
    - <span data-ttu-id="c6fef-401">UDFs, UDOs e UDAAGs internos de C#</span><span class="sxs-lookup"><span data-stu-id="c6fef-401">Built-in C# UDFs, UDOs, and UDAAGs</span></span> 
    - <span data-ttu-id="c6fef-402">Funções em U-SQL</span><span class="sxs-lookup"><span data-stu-id="c6fef-402">U-SQL functions</span></span>
    - <span data-ttu-id="c6fef-403">Função de Janelas do U-SQL</span><span class="sxs-lookup"><span data-stu-id="c6fef-403">U-SQL windowing function</span></span>
 
    ![Tipos de objeto do IntelliSense das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   <span data-ttu-id="c6fef-405">Preenchimento automático de IntelliSense nos metadados do Data Lake Analytics: as Ferramentas do Data Lake baixam localmente as informações de metadados do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="c6fef-405">IntelliSense auto-complete on Data Lake Analytics metadata: Data Lake Tools downloads the Data Lake Analytics metadata information locally.</span></span> <span data-ttu-id="c6fef-406">O recurso IntelliSense preenche objetos automaticamente, incluindo o banco de dados, esquema, tabela, exibição, função com valor de tabela, procedimentos e assemblies em C#, dos metadados do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="c6fef-406">The IntelliSense feature automatically populates objects, including the database, schema, table, view, table-valued function, procedures, and C# assemblies, from the Data Lake Analytics metadata.</span></span>
 
    ![Metadados do IntelliSense das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   <span data-ttu-id="c6fef-408">Marcador de erro de IntelliSense: as Ferramentas do Data Lake sublinham os erros de edição para U-SQL e C#.</span><span class="sxs-lookup"><span data-stu-id="c6fef-408">IntelliSense error marker: Data Lake Tools underlines the editing errors for U-SQL and C#.</span></span> 
-   <span data-ttu-id="c6fef-409">Destaques de sintaxe: as Ferramentas do Data Lake usam cores diferentes para diferenciar itens, como variáveis, palavras-chave, tipo de dados e funções.</span><span class="sxs-lookup"><span data-stu-id="c6fef-409">Syntax highlights: Data Lake Tools uses different colors to differentiate items, such as variables, keywords, data type, and functions.</span></span> 

    ![Destaques da sintaxe das Ferramentas do Data Lake para Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a><span data-ttu-id="c6fef-411">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c6fef-411">Next steps</span></span>

- <span data-ttu-id="c6fef-412">Para saber mais sobre a execução local do U-SQL e sobre a depuração local com o Visual Studio Code, consulte [Execução local do U-SQL e depuração local com o Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="c6fef-412">For U-SQL local run and local debug with Visual Studio Code, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>
- <span data-ttu-id="c6fef-413">Para obter informações introdutórias sobre o Data Lake Analytics, veja [Tutorial: Introdução ao Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c6fef-413">For getting-started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="c6fef-414">Para saber mais sobre as Ferramentas do Data Lake para Visual Studio, confira [Tutorial: Desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c6fef-414">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="c6fef-415">Para obter informações sobre como desenvolver assemblies, confira [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md) (Desenvolver assemblies U-SQL para trabalhos do Azure Data Lake Analytics).</span><span class="sxs-lookup"><span data-stu-id="c6fef-415">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>



