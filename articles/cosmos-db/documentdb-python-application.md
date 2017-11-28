---
title: tutorial do aplicativo web aaaPython bulbo para o banco de dados do Azure Cosmos | Microsoft Docs
description: "Examine um tutorial do banco de dados usando o banco de dados do Azure Cosmos toostore e acessar dados de um aplicativo web do Python bulbo hospedado no Azure. Encontre soluções de desenvolvimento de aplicativo."
keywords: Desenvolvimento de aplicativos, python flask, aplicativo Web python, desenvolvimento Web do python
services: cosmos-db
documentationcenter: python
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 20ebec18-67c2-4988-a760-be7c30cfb745
ms.service: cosmos-db
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/09/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 87b73c656ed96a7efbd162843a1529d435f027f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-python-flask-web-application-using-azure-cosmos-db"></a><span data-ttu-id="f42d0-105">Compilar um aplicativo Web do Python Flask usando o Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f42d0-105">Build a Python Flask web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f42d0-106">.NET</span><span class="sxs-lookup"><span data-stu-id="f42d0-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="f42d0-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="f42d0-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="f42d0-108">Java</span><span class="sxs-lookup"><span data-stu-id="f42d0-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="f42d0-109">Python</span><span class="sxs-lookup"><span data-stu-id="f42d0-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="f42d0-110">Este tutorial mostra como toouse o banco de dados do Azure Cosmos toostore e acessar dados de um Python hospedado no Azure do aplicativo web e presume que você tenha alguma experiência anterior com Python e sites do Azure.</span><span class="sxs-lookup"><span data-stu-id="f42d0-110">This tutorial shows you how toouse Azure Cosmos DB toostore and access data from a Python web application hosted on Azure and presumes that you have some prior experience using Python and Azure websites.</span></span>

<span data-ttu-id="f42d0-111">Este tutorial de banco de dados aborda:</span><span class="sxs-lookup"><span data-stu-id="f42d0-111">This database tutorial covers:</span></span>

1. <span data-ttu-id="f42d0-112">Crie e provisione uma conta do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f42d0-112">Creating and provisioning a Cosmos DB account.</span></span>
2. <span data-ttu-id="f42d0-113">Crie um aplicativo Python Flask.</span><span class="sxs-lookup"><span data-stu-id="f42d0-113">Creating a Python Flask application.</span></span>
3. <span data-ttu-id="f42d0-114">Conectando tooand usando o banco de dados do Cosmos de seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="f42d0-114">Connecting tooand using Cosmos DB from your web application.</span></span>
4. <span data-ttu-id="f42d0-115">Implantando Olá web aplicativo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f42d0-115">Deploying hello web application tooAzure.</span></span>

<span data-ttu-id="f42d0-116">Ao seguir este tutorial, você criará um aplicativo simples de votação que permite que você toovote para uma pesquisa.</span><span class="sxs-lookup"><span data-stu-id="f42d0-116">By following this tutorial, you will build a simple voting application that allows you toovote for a poll.</span></span>

![Captura de tela do aplicativo de votação hello criado por este tutorial do banco de dados](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)

## <a name="database-tutorial-prerequisites"></a><span data-ttu-id="f42d0-118">Pré-requisitos do tutorial de banco de dados</span><span class="sxs-lookup"><span data-stu-id="f42d0-118">Database tutorial prerequisites</span></span>
<span data-ttu-id="f42d0-119">Antes de seguir as instruções neste artigo hello, você deve garantir que você tenha a seguinte Olá instalado:</span><span class="sxs-lookup"><span data-stu-id="f42d0-119">Before following hello instructions in this article, you should ensure that you have hello following installed:</span></span>

* <span data-ttu-id="f42d0-120">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="f42d0-120">An active Azure account.</span></span> <span data-ttu-id="f42d0-121">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="f42d0-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f42d0-122">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f42d0-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
 
    <span data-ttu-id="f42d0-123">OU</span><span class="sxs-lookup"><span data-stu-id="f42d0-123">OR</span></span> 

    <span data-ttu-id="f42d0-124">Uma instalação local do hello [emulador de banco de dados do Azure Cosmos](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="f42d0-124">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="f42d0-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="f42d0-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="f42d0-126">[Ferramentas Python para Visual Studio](https://github.com/Microsoft/PTVS/).</span><span class="sxs-lookup"><span data-stu-id="f42d0-126">[Python Tools for Visual Studio](https://github.com/Microsoft/PTVS/).</span></span>  
* <span data-ttu-id="f42d0-127">[SDK do Microsoft Azure para Python 2.7](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="f42d0-127">[Microsoft Azure SDK for Python 2.7](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="f42d0-128">[Python 2.7.13](https://www.python.org/downloads/windows/).</span><span class="sxs-lookup"><span data-stu-id="f42d0-128">[Python 2.7.13](https://www.python.org/downloads/windows/).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f42d0-129">Se você estiver instalando o Python 2.7 para Olá primeira vez, certifique-se de que na tela de Python personalizar 2.7.13 hello, você selecionar **adicionar python.exe tooPath**.</span><span class="sxs-lookup"><span data-stu-id="f42d0-129">If you are installing Python 2.7 for hello first time, ensure that in hello Customize Python 2.7.13 screen, you select **Add python.exe tooPath**.</span></span>
> 
> ![Captura de tela da tela de Python personalizar 2.7.11 hello, em que você precisa tooselect adicionar python.exe tooPath](./media/documentdb-python-application/cosmos-db-python-install.png)
> 
> 

* <span data-ttu-id="f42d0-131">[Compilador do Microsoft Visual C++ para Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).</span><span class="sxs-lookup"><span data-stu-id="f42d0-131">[Microsoft Visual C++ Compiler for Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="f42d0-132">Etapa 1: Criar uma conta de banco de dados do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f42d0-132">Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="f42d0-133">Vamos começar criando uma conta do BD Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f42d0-133">Let's start by creating an Cosmos DB account.</span></span> <span data-ttu-id="f42d0-134">Se você já tiver uma conta ou se você estiver usando hello Azure Cosmos DB emulador para este tutorial, você poderá ignorar muito[etapa 2: criar um novo aplicativo web Python bulbo](#step-2-create-a-new-python-flask-web-application).</span><span class="sxs-lookup"><span data-stu-id="f42d0-134">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create a new Python Flask web application](#step-2-create-a-new-python-flask-web-application).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<br/>
<span data-ttu-id="f42d0-135">Percorreremos agora como toocreate um novo aplicativo web Python bulbo da saudação plano de fundo do.</span><span class="sxs-lookup"><span data-stu-id="f42d0-135">We will now walk through how toocreate a new Python Flask web application from hello ground up.</span></span>

## <a name="step-2-create-a-new-python-flask-web-application"></a><span data-ttu-id="f42d0-136">Etapa 2: Criar um novo aplicativo Web Python Flask</span><span class="sxs-lookup"><span data-stu-id="f42d0-136">Step 2: Create a new Python Flask web application</span></span>
1. <span data-ttu-id="f42d0-137">No Visual Studio, no hello **arquivo** menus, aponte muito**novo**e, em seguida, clique em **projeto**.</span><span class="sxs-lookup"><span data-stu-id="f42d0-137">In Visual Studio, on hello **File** menu, point too**New**, and then click **Project**.</span></span>
   
    <span data-ttu-id="f42d0-138">Olá **novo projeto** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="f42d0-138">hello **New Project** dialog box appears.</span></span>
2. <span data-ttu-id="f42d0-139">No painel esquerdo do hello, expanda **modelos** e **Python**e, em seguida, clique em **Web**.</span><span class="sxs-lookup"><span data-stu-id="f42d0-139">In hello left pane, expand **Templates** and then **Python**, and then click **Web**.</span></span> 
3. <span data-ttu-id="f42d0-140">Selecione **bulbo Web projeto** no painel de central hello, em Olá **nome** caixa tipo **tutorial**e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="f42d0-140">Select **Flask  Web Project** in hello center pane, then in hello **Name** box type **tutorial**, and then click **OK**.</span></span> <span data-ttu-id="f42d0-141">Lembre-se de que os nomes de pacote do Python devem ser letras minúsculos, conforme descrito em Olá [guia de estilo para o código Python](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span><span class="sxs-lookup"><span data-stu-id="f42d0-141">Remember that Python package names should be all lowercase, as described in hello [Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span></span>
   
    <span data-ttu-id="f42d0-142">Para esses novos tooPython bulbo, é uma estrutura de desenvolvimento de aplicativos web que ajuda você a criar aplicativos web no Python mais rapidamente.</span><span class="sxs-lookup"><span data-stu-id="f42d0-142">For those new tooPython Flask, it is a web application development framework that helps you build web applications in Python faster.</span></span>
   
    ![Captura de tela da janela do novo projeto Olá no Visual Studio com Python realçado em Olá Python bulbo Web projeto selecionado no meio de saudação e tutorial de nome de saudação na caixa de nome de saudação à esquerda](./media/documentdb-python-application/image9.png)
4. <span data-ttu-id="f42d0-144">Em Olá **ferramentas Python para Visual Studio** janela, clique em **instalar em um ambiente virtual**.</span><span class="sxs-lookup"><span data-stu-id="f42d0-144">In hello **Python Tools for Visual Studio** window, click **Install into a virtual environment**.</span></span> 
   
    ![Captura de tela do tutorial do banco de dados de saudação - ferramentas Python para a janela do Visual Studio](./media/documentdb-python-application/python-install-virtual-environment.png)
5. <span data-ttu-id="f42d0-146">Em Olá **adicionar ambiente Virtual** janela, você pode aceitar os padrões de saudação e usar Python 2.7 ambiente base Olá porque PyDocumentDB não oferece suporte a Python 3. x e, em seguida, clique **criar**.</span><span class="sxs-lookup"><span data-stu-id="f42d0-146">In hello **Add Virtual Environment** window, you can accept hello defaults and use Python 2.7 as hello base environment because PyDocumentDB does not currently support Python 3.x, and then click **Create**.</span></span> <span data-ttu-id="f42d0-147">Isso configura o ambiente virtual do Python Olá necessários para seu projeto.</span><span class="sxs-lookup"><span data-stu-id="f42d0-147">This sets up hello required Python virtual environment for your project.</span></span>
   
    ![Captura de tela do tutorial do banco de dados de saudação - ferramentas Python para a janela do Visual Studio](./media/documentdb-python-application/image10_A.png)
   
    <span data-ttu-id="f42d0-149">Olá saída janela exibe `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` quando o ambiente de saudação for instalado com êxito.</span><span class="sxs-lookup"><span data-stu-id="f42d0-149">hello output window displays `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` when hello environment is successfully installed.</span></span>

## <a name="step-3-modify-hello-python-flask-web-application"></a><span data-ttu-id="f42d0-150">Etapa 3: Modificar o aplicativo de web hello bulbo Python</span><span class="sxs-lookup"><span data-stu-id="f42d0-150">Step 3: Modify hello Python Flask web application</span></span>
### <a name="add-hello-python-flask-packages-tooyour-project"></a><span data-ttu-id="f42d0-151">Adicionar Olá Python bulbo pacotes tooyour projeto</span><span class="sxs-lookup"><span data-stu-id="f42d0-151">Add hello Python Flask packages tooyour project</span></span>
<span data-ttu-id="f42d0-152">Depois de configurar o seu projeto, você precisará tooadd Olá necessário bulbo pacotes tooyour projeto, incluindo pydocumentdb, pacote de Python de saudação do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="f42d0-152">After your project is set up, you'll need tooadd hello required Flask packages tooyour project, including pydocumentdb, hello Python package for DocumentDB.</span></span>

1. <span data-ttu-id="f42d0-153">No Solution Explorer, abra o arquivo de saudação chamado **requirements.txt** e substitua o conteúdo de saudação pelo seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="f42d0-153">In Solution Explorer, open hello file named **requirements.txt** and replace hello contents with hello following:</span></span>
   
        flask==0.9
        flask-mail==0.7.6
        sqlalchemy==0.7.9
        flask-sqlalchemy==0.16
        sqlalchemy-migrate==0.7.2
        flask-whooshalchemy==0.55a
        flask-wtf==0.8.4
        pytz==2013b
        flask-babel==0.8
        flup
        pydocumentdb>=1.0.0
2. <span data-ttu-id="f42d0-154">Salvar Olá **requirements.txt** arquivo.</span><span class="sxs-lookup"><span data-stu-id="f42d0-154">Save hello **requirements.txt** file.</span></span> 
3. <span data-ttu-id="f42d0-155">No Gerenciador de Soluções, clique com o botão direito do mouse em **env** e clique em **Instalar de requirements.txt**.</span><span class="sxs-lookup"><span data-stu-id="f42d0-155">In Solution Explorer, right-click **env** and click **Install from requirements.txt**.</span></span>
   
    ![Captura de tela mostrando env (Python 2.7) selecionado com a instalação do requirements.txt realçado na lista de saudação](./media/documentdb-python-application/cosmos-db-python-install-from-requirements.png)
   
    <span data-ttu-id="f42d0-157">Após a instalação bem-sucedida, a janela de saída de hello exibe seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="f42d0-157">After successful installation, hello output window displays hello following:</span></span>
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > <span data-ttu-id="f42d0-158">Em casos raros, talvez você veja uma falha na janela de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="f42d0-158">In rare cases, you might see a failure in hello output window.</span></span> <span data-ttu-id="f42d0-159">Se isso acontecer, verifique se o erro de saudação é toocleanup relacionado.</span><span class="sxs-lookup"><span data-stu-id="f42d0-159">If this happens, check if hello error is related toocleanup.</span></span> <span data-ttu-id="f42d0-160">Às vezes, a limpeza de saudação falha, mas instalação Olá ainda será bem-sucedida (rolar para cima na tooverify de janela de saída de hello isso).</span><span class="sxs-lookup"><span data-stu-id="f42d0-160">Sometimes hello cleanup fails, but hello installation will still be successful (scroll up in hello output window tooverify this).</span></span> <span data-ttu-id="f42d0-161">Você pode verificar a instalação por [ambiente virtual do verificando Olá](#verify-the-virtual-environment).</span><span class="sxs-lookup"><span data-stu-id="f42d0-161">You can check your installation by [Verifying hello virtual environment](#verify-the-virtual-environment).</span></span> <span data-ttu-id="f42d0-162">Se a falha na instalação de saudação mas Olá verificação for bem-sucedida, é toocontinue Okey.</span><span class="sxs-lookup"><span data-stu-id="f42d0-162">If hello installation failed but hello verification is successful, it's OK toocontinue.</span></span>
   > 
   > 

### <a name="verify-hello-virtual-environment"></a><span data-ttu-id="f42d0-163">Verifique se o ambiente virtual Olá</span><span class="sxs-lookup"><span data-stu-id="f42d0-163">Verify hello virtual environment</span></span>
<span data-ttu-id="f42d0-164">Vamos garantir que tudo esteja instalado corretamente.</span><span class="sxs-lookup"><span data-stu-id="f42d0-164">Let's make sure that everything is installed correctly.</span></span>

1. <span data-ttu-id="f42d0-165">Compile a solução Olá pressionando **Ctrl**+**Shift**+**B**.</span><span class="sxs-lookup"><span data-stu-id="f42d0-165">Build hello solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="f42d0-166">Quando Olá compilação for bem-sucedida, iniciar o site de saudação pressionando **F5**.</span><span class="sxs-lookup"><span data-stu-id="f42d0-166">Once hello build succeeds, start hello website by pressing **F5**.</span></span> <span data-ttu-id="f42d0-167">Isso inicia o servidor de desenvolvimento do bulbo hello e inicia o navegador da web.</span><span class="sxs-lookup"><span data-stu-id="f42d0-167">This launches hello Flask development server and starts your web browser.</span></span> <span data-ttu-id="f42d0-168">Você deve ver Olá página a seguir.</span><span class="sxs-lookup"><span data-stu-id="f42d0-168">You should see hello following page.</span></span>
   
    ![Olá vazio Python bulbo desenvolvimento projeto web exibido em um navegador](./media/documentdb-python-application/image12.png)
3. <span data-ttu-id="f42d0-170">Parar a depuração site Olá pressionando **Shift**+**F5** no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f42d0-170">Stop debugging hello website by pressing **Shift**+**F5** in Visual Studio.</span></span>

### <a name="create-database-collection-and-document-definitions"></a><span data-ttu-id="f42d0-171">Criar definições de banco de dados, de coleção e de documentos</span><span class="sxs-lookup"><span data-stu-id="f42d0-171">Create database, collection, and document definitions</span></span>
<span data-ttu-id="f42d0-172">Agora vamos criar seu aplicativo de votação adicionando novos arquivos e enviando atualizações para outras pessoas.</span><span class="sxs-lookup"><span data-stu-id="f42d0-172">Now let's create your voting application by adding new files and updating others.</span></span>

1. <span data-ttu-id="f42d0-173">No Gerenciador de soluções, clique com botão direito Olá **tutorial** de projeto, clique em **adicionar**e, em seguida, clique em **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="f42d0-173">In Solution Explorer, right-click hello **tutorial** project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="f42d0-174">Selecione **arquivo vazio do Python** e nome hello arquivo **forms.py**.</span><span class="sxs-lookup"><span data-stu-id="f42d0-174">Select **Empty Python File** and name hello file **forms.py**.</span></span>  
2. <span data-ttu-id="f42d0-175">Adicionar Olá seguir código toohello forms.py arquivo e, em seguida, salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="f42d0-175">Add hello following code toohello forms.py file, and then save hello file.</span></span>

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-hello-required-imports-tooviewspy"></a><span data-ttu-id="f42d0-176">Adicionar Olá necessário importações tooviews.py</span><span class="sxs-lookup"><span data-stu-id="f42d0-176">Add hello required imports tooviews.py</span></span>
1. <span data-ttu-id="f42d0-177">No Gerenciador de soluções, expanda Olá **tutorial** pasta e abra Olá **views.py** arquivo.</span><span class="sxs-lookup"><span data-stu-id="f42d0-177">In Solution Explorer, expand hello **tutorial** folder, and open hello **views.py** file.</span></span> 
2. <span data-ttu-id="f42d0-178">Adicionar Olá após a importação instruções toohello superior de saudação **views.py** de arquivo e salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="f42d0-178">Add hello following import statements toohello top of hello **views.py** file, then save hello file.</span></span> <span data-ttu-id="f42d0-179">Esses importar PythonSDK do banco de dados Cosmos e Olá pacotes bulbo.</span><span class="sxs-lookup"><span data-stu-id="f42d0-179">These import Cosmos DB's PythonSDK and hello Flask packages.</span></span>
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a><span data-ttu-id="f42d0-180">Criar banco de dados, coleção e documento</span><span class="sxs-lookup"><span data-stu-id="f42d0-180">Create database, collection, and document</span></span>
* <span data-ttu-id="f42d0-181">Ainda no **views.py**, adicionar Olá seguindo código toohello final do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="f42d0-181">Still in **views.py**, add hello following code toohello end of hello file.</span></span> <span data-ttu-id="f42d0-182">Isso cuida de criação de banco de dados de saudação usado pelo formulário hello.</span><span class="sxs-lookup"><span data-stu-id="f42d0-182">This takes care of creating hello database used by hello form.</span></span> <span data-ttu-id="f42d0-183">Não exclua nenhum código existente Olá **views.py**.</span><span class="sxs-lookup"><span data-stu-id="f42d0-183">Do not delete any of hello existing code in **views.py**.</span></span> <span data-ttu-id="f42d0-184">Basta acrescente essa extremidade toohello.</span><span class="sxs-lookup"><span data-stu-id="f42d0-184">Simply append this toohello end.</span></span>

```python
@app.route('/create')
def create():
    """Renders hello contact page."""
    client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

    # Attempt toodelete hello database.  This allows this toobe used toorecreate as well as create
    try:
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))
        client.DeleteDatabase(db['_self'])
    except:
        pass

    # Create database
    db = client.CreateDatabase({ 'id': config.DOCUMENTDB_DATABASE })

    # Create collection
    collection = client.CreateCollection(db['_self'],{ 'id': config.DOCUMENTDB_COLLECTION })

    # Create document
    document = client.CreateDocument(collection['_self'],
        { 'id': config.DOCUMENTDB_DOCUMENT,
          'Web Site': 0,
          'Cloud Service': 0,
          'Virtual Machine': 0,
          'name': config.DOCUMENTDB_DOCUMENT 
        })

    return render_template(
       'create.html',
        title='Create Page',
        year=datetime.now().year,
        message='You just created a new database, collection, and document.  Your old votes have been deleted')
```


### <a name="read-database-collection-document-and-submit-form"></a><span data-ttu-id="f42d0-185">Ler o banco de dados, a coleção, o documento e enviar o formulário</span><span class="sxs-lookup"><span data-stu-id="f42d0-185">Read database, collection, document, and submit form</span></span>
* <span data-ttu-id="f42d0-186">Ainda no **views.py**, adicionar Olá seguindo código toohello final do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="f42d0-186">Still in **views.py**, add hello following code toohello end of hello file.</span></span> <span data-ttu-id="f42d0-187">Isso cuida da configuração de formulário de hello, ler o documento, coleção e banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="f42d0-187">This takes care of setting up hello form, reading hello database, collection, and document.</span></span> <span data-ttu-id="f42d0-188">Não exclua nenhum código existente Olá **views.py**.</span><span class="sxs-lookup"><span data-stu-id="f42d0-188">Do not delete any of hello existing code in **views.py**.</span></span> <span data-ttu-id="f42d0-189">Basta acrescente essa extremidade toohello.</span><span class="sxs-lookup"><span data-stu-id="f42d0-189">Simply append this toohello end.</span></span>

```python
@app.route('/vote', methods=['GET', 'POST'])
def vote(): 
    form = VoteForm()
    replaced_document ={}
    if form.validate_on_submit(): # is user submitted vote  
        client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

        # Read databases and take first since id should not be duplicated.
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))

        # Read collections and take first since id should not be duplicated.
        coll = next((coll for coll in client.ReadCollections(db['_self']) if coll['id'] == config.DOCUMENTDB_COLLECTION))

        # Read documents and take first since id should not be duplicated.
        doc = next((doc for doc in client.ReadDocuments(coll['_self']) if doc['id'] == config.DOCUMENTDB_DOCUMENT))

        # Take hello data from hello deploy_preference and increment our database
        doc[form.deploy_preference.data] = doc[form.deploy_preference.data] + 1
        replaced_document = client.ReplaceDocument(doc['_self'], doc)

        # Create a model toopass tooresults.html
        class VoteObject:
            choices = dict()
            total_votes = 0

        vote_object = VoteObject()
        vote_object.choices = {
            "Web Site" : doc['Web Site'],
            "Cloud Service" : doc['Cloud Service'],
            "Virtual Machine" : doc['Virtual Machine']
        }
        vote_object.total_votes = sum(vote_object.choices.values())

        return render_template(
            'results.html', 
            year=datetime.now().year, 
            vote_object = vote_object)

    else :
        return render_template(
            'vote.html', 
            title = 'Vote',
            year=datetime.now().year,
            form = form)
```


### <a name="create-hello-html-files"></a><span data-ttu-id="f42d0-190">Criar hello arquivos HTML</span><span class="sxs-lookup"><span data-stu-id="f42d0-190">Create hello HTML files</span></span>
1. <span data-ttu-id="f42d0-191">No Solution Explorer, no hello **tutorial** pasta, direito clique Olá **modelos** pasta, clique em **adicionar**e, em seguida, clique em **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="f42d0-191">In Solution Explorer, in hello **tutorial** folder, right click hello **templates** folder, click **Add**, and then click **New Item**.</span></span> 
2. <span data-ttu-id="f42d0-192">Selecione **página HTML**e, em seguida, na caixa, digite Olá nome **create.html**.</span><span class="sxs-lookup"><span data-stu-id="f42d0-192">Select **HTML Page**, and then in hello name box type **create.html**.</span></span> 
3. <span data-ttu-id="f42d0-193">Repita as etapas 1 e 2 toocreate dois outros HTML arquivos: results.html e vote.html.</span><span class="sxs-lookup"><span data-stu-id="f42d0-193">Repeat steps 1 and 2 toocreate two additional HTML files: results.html and vote.html.</span></span>
4. <span data-ttu-id="f42d0-194">Adicionar Olá código a seguir muito**create.html** em Olá `<body>` elemento.</span><span class="sxs-lookup"><span data-stu-id="f42d0-194">Add hello following code too**create.html** in hello `<body>` element.</span></span> <span data-ttu-id="f42d0-195">Ele exibe uma mensagem indicando que um banco de dados, uma coleção e um documento novos foram criados.</span><span class="sxs-lookup"><span data-stu-id="f42d0-195">It displays a message stating that we created a new database, collection, and document.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. <span data-ttu-id="f42d0-196">Adicionar Olá código a seguir muito**results.html** em Olá `<body`> elemento.</span><span class="sxs-lookup"><span data-stu-id="f42d0-196">Add hello following code too**results.html** in hello `<body`> element.</span></span> <span data-ttu-id="f42d0-197">Ele exibe os resultados de saudação de sondagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="f42d0-197">It displays hello results of hello poll.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Results of hello vote</h2>
        <br />
   
    {% for choice in vote_object.choices %}
    <div class="row">
        <div class="col-sm-5">{{choice}}</div>
            <div class="col-sm-5">
                <div class="progress">
                    <div class="progress-bar" role="progressbar" aria-valuenow="{{vote_object.choices[choice]}}" aria-valuemin="0" aria-valuemax="{{vote_object.total_votes}}" style="width: {{(vote_object.choices[choice]/vote_object.total_votes)*100}}%;">
                                {{vote_object.choices[choice]}}
                </div>
            </div>
            </div>
    </div>
    {% endfor %}
   
    <br />
    <a class="btn btn-primary" href="{{ url_for('vote') }}">Vote again?</a>
    {% endblock %}
    ```
6. <span data-ttu-id="f42d0-198">Adicionar Olá código a seguir muito**vote.html** em Olá `<body`> elemento.</span><span class="sxs-lookup"><span data-stu-id="f42d0-198">Add hello following code too**vote.html** in hello `<body`> element.</span></span> <span data-ttu-id="f42d0-199">Exibe a sondagem hello e aceita Olá votos.</span><span class="sxs-lookup"><span data-stu-id="f42d0-199">It displays hello poll and accepts hello votes.</span></span> <span data-ttu-id="f42d0-200">Sobre como registrar votos hello, controle Olá é passada pela tooviews.py onde podemos reconhecerá Olá voto cast e acrescentar documento hello adequadamente.</span><span class="sxs-lookup"><span data-stu-id="f42d0-200">On registering hello votes, hello control is passed over tooviews.py where we will recognize hello vote cast and append hello document accordingly.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>What is your favorite way toohost an application on Azure?</h2>
    <form action="" method="post" name="vote">
        {{form.hidden_tag()}}
            {{form.deploy_preference}}
            <button class="btn btn-primary" type="submit">Vote</button>
    </form>
    {% endblock %}
    ```
7. <span data-ttu-id="f42d0-201">Em Olá **modelos** substituir Olá conteúdo da pasta **index** com os seguintes hello.</span><span class="sxs-lookup"><span data-stu-id="f42d0-201">In hello **templates** folder, replace hello contents of **index.html** with hello following.</span></span> <span data-ttu-id="f42d0-202">Isso serve como a saudação inicial da página do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f42d0-202">This serves as hello landing page for your application.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + Azure Cosmos DB Voting Application.</h2>
    <h3>This is a sample Cosmos DB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear hello Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-hello-initpy"></a><span data-ttu-id="f42d0-203">Adicionar um arquivo de configuração e alterar Olá \_ \_init\_\_py</span><span class="sxs-lookup"><span data-stu-id="f42d0-203">Add a configuration file and change hello \_\_init\_\_.py</span></span>
1. <span data-ttu-id="f42d0-204">No Gerenciador de soluções, clique com botão direito Olá **tutorial** de projeto, clique em **adicionar**, clique em **Novo Item**, selecione **arquivo vazio do Python**e, em seguida, arquivo de saudação do nome **config.py**.</span><span class="sxs-lookup"><span data-stu-id="f42d0-204">In Solution Explorer, right-click hello **tutorial** project, click **Add**, click **New Item**, select **Empty Python File**, and then name hello file **config.py**.</span></span> <span data-ttu-id="f42d0-205">Esse arquivo de configuração é exigido por formulários no flask.</span><span class="sxs-lookup"><span data-stu-id="f42d0-205">This config file is required by forms in Flask.</span></span> <span data-ttu-id="f42d0-206">Você pode usá-lo tooprovide também uma chave secreta.</span><span class="sxs-lookup"><span data-stu-id="f42d0-206">You can use it tooprovide a secret key as well.</span></span> <span data-ttu-id="f42d0-207">Essa chave não será necessária neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="f42d0-207">This key is not needed for this tutorial though.</span></span>
2. <span data-ttu-id="f42d0-208">Adicione Olá seguinte tooconfig.py de código, você precisará valores hello tooalter **DOCUMENTDB\_HOST** e **DOCUMENTDB\_chave** na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="f42d0-208">Add hello following code tooconfig.py, you'll need tooalter hello values of **DOCUMENTDB\_HOST** and **DOCUMENTDB\_KEY** in hello next step.</span></span>
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. <span data-ttu-id="f42d0-209">Em Olá [portal do Azure](https://portal.azure.com/), navegar toohello **chaves** folha clicando **procurar**, **contas de banco de dados do Azure Cosmos**, clique duas vezes no nome da saudação de saudação toouse da conta e, em seguida, clique em Olá **chaves** botão Olá **Essentials** área.</span><span class="sxs-lookup"><span data-stu-id="f42d0-209">In hello [Azure portal](https://portal.azure.com/), navigate toohello **Keys** blade by clicking **Browse**, **Azure Cosmos DB Accounts**, double-click hello name of hello account toouse, and then click hello **Keys** button in hello **Essentials** area.</span></span> <span data-ttu-id="f42d0-210">Em Olá **chaves** folha, Olá cópia **URI** valor e cole-a saudação **config.py** arquivo, como valor Olá Olá **DOCUMENTDB\_HOST**  propriedade.</span><span class="sxs-lookup"><span data-stu-id="f42d0-210">In hello **Keys** blade, copy hello **URI** value and paste it into hello **config.py** file, as hello value for hello **DOCUMENTDB\_HOST** property.</span></span> 
4. <span data-ttu-id="f42d0-211">Em Olá portal do Azure, na Olá **chaves** folha, copiar o valor de saudação do hello **chave primária** ou hello **chave secundária**e cole-a saudação **config.py**  arquivo, como valor Olá Olá **DOCUMENTDB\_chave** propriedade.</span><span class="sxs-lookup"><span data-stu-id="f42d0-211">Back in hello Azure portal, in hello **Keys** blade, copy hello value of hello **Primary Key** or hello **Secondary Key**, and paste it into hello **config.py** file, as hello value for hello **DOCUMENTDB\_KEY** property.</span></span>
5. <span data-ttu-id="f42d0-212">Em Olá  **\_ \_init\_\_py** de arquivos, adicionar a seguinte linha de saudação.</span><span class="sxs-lookup"><span data-stu-id="f42d0-212">In hello **\_\_init\_\_.py** file, add hello following line.</span></span> 
   
        app.config.from_object('config')
   
    <span data-ttu-id="f42d0-213">Assim que o conteúdo do arquivo hello Olá é:</span><span class="sxs-lookup"><span data-stu-id="f42d0-213">So that hello content of hello file is:</span></span>
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. <span data-ttu-id="f42d0-214">Depois de adicionar todos os arquivos de hello, Solution Explorer deve ser assim:</span><span class="sxs-lookup"><span data-stu-id="f42d0-214">After adding all hello files, Solution Explorer should look like this:</span></span>
   
    ![Captura de tela da janela do Gerenciador de soluções do Visual Studio Olá](./media/documentdb-python-application/cosmos-db-python-solution-explorer.png)

## <a name="step-4-run-your-web-application-locally"></a><span data-ttu-id="f42d0-216">Etapa 4: executar o aplicativo localmente</span><span class="sxs-lookup"><span data-stu-id="f42d0-216">Step 4: Run your web application locally</span></span>
1. <span data-ttu-id="f42d0-217">Compile a solução Olá pressionando **Ctrl**+**Shift**+**B**.</span><span class="sxs-lookup"><span data-stu-id="f42d0-217">Build hello solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="f42d0-218">Quando Olá compilação for bem-sucedida, iniciar o site de saudação pressionando **F5**.</span><span class="sxs-lookup"><span data-stu-id="f42d0-218">Once hello build succeeds, start hello website by pressing **F5**.</span></span> <span data-ttu-id="f42d0-219">Você deve ver o seguinte de saudação na tela.</span><span class="sxs-lookup"><span data-stu-id="f42d0-219">You should see hello following on your screen.</span></span>
   
    ![Captura de tela de Olá Python + do aplicativo do Azure Cosmos DB votação exibido em um navegador da web](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)
3. <span data-ttu-id="f42d0-221">Clique em **criar/limpar Olá votação de banco de dados** banco de dados do toogenerate hello.</span><span class="sxs-lookup"><span data-stu-id="f42d0-221">Click **Create/Clear hello Voting Database** toogenerate hello database.</span></span>
   
    ![Captura de tela de Olá Criar página de aplicativo de web hello – detalhes do desenvolvimento](./media/documentdb-python-application/cosmos-db-python-run-create-page.png)
4. <span data-ttu-id="f42d0-223">Em seguida, clique em **Votar** e selecione sua opção.</span><span class="sxs-lookup"><span data-stu-id="f42d0-223">Then, click **Vote** and select your option.</span></span>
   
    ![Captura de tela do aplicativo de web hello com uma pergunta votação apresentado](./media/documentdb-python-application/cosmos-db-vote.png)
5. <span data-ttu-id="f42d0-225">Para cada voto converter, ele incrementa o contador de apropriada de saudação.</span><span class="sxs-lookup"><span data-stu-id="f42d0-225">For every vote you cast, it increments hello appropriate counter.</span></span>
   
    ![Captura de tela de saudação resultados da página de voto Olá mostrado](./media/documentdb-python-application/cosmos-db-voting-results.png)
6. <span data-ttu-id="f42d0-227">Pare a depuração de projeto Olá pressionando Shift + F5.</span><span class="sxs-lookup"><span data-stu-id="f42d0-227">Stop debugging hello project by pressing Shift+F5.</span></span>

## <a name="step-5-deploy-hello-web-application-tooazure"></a><span data-ttu-id="f42d0-228">Etapa 5: Implantar Olá web aplicativo tooAzure</span><span class="sxs-lookup"><span data-stu-id="f42d0-228">Step 5: Deploy hello web application tooAzure</span></span>
<span data-ttu-id="f42d0-229">Agora que você tem um aplicativo completo de saudação funcionando corretamente no banco de dados do Cosmos, vamos toodeploy este tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f42d0-229">Now that you have hello complete application working correctly against Cosmos DB, we're going toodeploy this tooAzure.</span></span>

1. <span data-ttu-id="f42d0-230">Projeto de saudação com o botão direito no Gerenciador de soluções (Verifique se você não tiver ainda executá-lo localmente) e selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="f42d0-230">Right-click hello project in Solution Explorer (make sure you're not still running it locally) and select **Publish**.</span></span>  
   
     ![Captura de tela do tutorial de saudação selecionado no Gerenciador de soluções, com a opção de publicar Olá realçada](./media/documentdb-python-application/image20.png)
2. <span data-ttu-id="f42d0-232">Em Olá **publicar** caixa de diálogo, selecione **serviço de aplicativo do Microsoft Azure**, selecione **criar novo**e, em seguida, clique em **publicar**.</span><span class="sxs-lookup"><span data-stu-id="f42d0-232">In hello **Publish** dialog box, select **Microsoft Azure App Service**, select **Create New**, and then click **Publish**.</span></span>
   
    ![Captura de tela da janela de publicar Web hello com o serviço de aplicativo do Microsoft Azure realçado](./media/documentdb-python-application/cosmos-db-python-publish.png)
3. <span data-ttu-id="f42d0-234">Em Olá **criar serviço de aplicativo** caixa de diálogo, digite o nome de saudação para seu aplicativo web junto com seus **assinatura**, **grupo de recursos**, e **plano do serviço de aplicativo** , em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="f42d0-234">In hello **Create App Service** dialog box, enter hello name for your web app along with your **Subscription**, **Resource Group**, and **App Service Plan**, then click **Create**.</span></span>
   
    ![Captura de tela da janela de janela de aplicativos do Microsoft Azure Web Olá](./media/documentdb-python-application/cosmos-db-python-create-app-service.png)
4. <span data-ttu-id="f42d0-236">Em poucos segundos, o Visual Studio terminará de publicar seu serviço de aplicativo e iniciará um navegador no qual você poderá ver seu trabalho sendo executado no Azure!</span><span class="sxs-lookup"><span data-stu-id="f42d0-236">In a few seconds, Visual Studio will finish publishing your app service and launch a browser where you can see your handiwork running in Azure!</span></span>

    ![Captura de tela da janela de janela de aplicativos do Microsoft Azure Web Olá](./media/documentdb-python-application/cosmos-db-python-appservice-created.png)

## <a name="troubleshooting"></a><span data-ttu-id="f42d0-238">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="f42d0-238">Troubleshooting</span></span>
<span data-ttu-id="f42d0-239">Se esse for o hello primeiro Python aplicativo executar no seu computador, certifique-se de que seguinte Olá pastas (ou locais de instalação equivalente Olá) são incluídos na sua variável de caminho:</span><span class="sxs-lookup"><span data-stu-id="f42d0-239">If this is hello first Python app you've run on your computer, ensure that hello following folders (or hello equivalent installation locations) are included in your PATH variable:</span></span>

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

<span data-ttu-id="f42d0-240">Se você receber um erro em sua página de voto e você nomeou seu projeto diferente de **tutorial**, certifique-se de que  **\_ \_init\_\_py** referências Olá nome correto do projeto na linha de saudação: `import tutorial.view`.</span><span class="sxs-lookup"><span data-stu-id="f42d0-240">If you receive an error on your vote page, and you named your project something other than **tutorial**, make sure that **\_\_init\_\_.py** references hello correct project name in hello line: `import tutorial.view`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f42d0-241">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f42d0-241">Next steps</span></span>
<span data-ttu-id="f42d0-242">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="f42d0-242">Congratulations!</span></span> <span data-ttu-id="f42d0-243">Apenas ter concluído seu primeiro aplicativo web de Python usando o banco de dados do Cosmos e publicá-la tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f42d0-243">You have just completed your first Python web application using Cosmos DB and published it tooAzure.</span></span>

<span data-ttu-id="f42d0-244">Atualizamos e aperfeiçoamos este tópico com frequência, de acordo com seus comentários.</span><span class="sxs-lookup"><span data-stu-id="f42d0-244">We update and improve this topic frequently based on your feedback.</span></span>  <span data-ttu-id="f42d0-245">Uma vez que você concluiu o tutorial hello, a. usando Olá votação botões na Olá superior e na parte inferior desta página e ser tooinclude-se de que seus comentários sobre quais melhorias você deseja toosee feita.</span><span class="sxs-lookup"><span data-stu-id="f42d0-245">Once you've completed hello tutorial, please using hello voting buttons at hello top and bottom of this page, and be sure tooinclude your feedback on what improvements you want toosee made.</span></span> <span data-ttu-id="f42d0-246">Se você deseja toocontact você diretamente, sinta-se livre tooinclude endereço do seu email em seus comentários.</span><span class="sxs-lookup"><span data-stu-id="f42d0-246">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="f42d0-247">aplicativo de web do tooadd funcionalidade adicional tooyour, Olá revisão APIs disponíveis no hello [SDK de Python de banco de dados do Azure Cosmos](documentdb-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="f42d0-247">tooadd additional functionality tooyour web application, review hello APIs available in hello [Azure Cosmos DB Python SDK](documentdb-sdk-python.md).</span></span>

<span data-ttu-id="f42d0-248">Para obter mais informações sobre o Azure, o Visual Studio e Python, consulte Olá [Central de desenvolvedores de Python](https://azure.microsoft.com/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="f42d0-248">For more information about Azure, Visual Studio, and Python, see hello [Python Developer Center](https://azure.microsoft.com/develop/python/).</span></span> 

<span data-ttu-id="f42d0-249">Para tutoriais do Python bulbo adicionais, consulte [Olá bulbo Mega-Tutorial, parte i: Olá, mundo!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span><span class="sxs-lookup"><span data-stu-id="f42d0-249">For additional Python Flask tutorials, see [hello Flask Mega-Tutorial, Part I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span></span> 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com
