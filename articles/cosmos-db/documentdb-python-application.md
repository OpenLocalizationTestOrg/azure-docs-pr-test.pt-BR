---
title: Tutorial do aplicativo Web do Python Flask para o Azure Cosmos DB | Microsoft Docs
description: "Analise um tutorial de banco de dados sobre como usar o Azure Cosmos DB para armazenar e acessar dados de um aplicativo Web Python Flask hospedado no Azure. Encontre soluções de desenvolvimento de aplicativo."
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
ms.openlocfilehash: ed5284b5a265840c43dbc9890082a7c038d22975
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-python-flask-web-application-using-azure-cosmos-db"></a><span data-ttu-id="861a3-105">Compilar um aplicativo Web do Python Flask usando o Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="861a3-105">Build a Python Flask web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="861a3-106">.NET</span><span class="sxs-lookup"><span data-stu-id="861a3-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="861a3-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="861a3-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="861a3-108">Java</span><span class="sxs-lookup"><span data-stu-id="861a3-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="861a3-109">Python</span><span class="sxs-lookup"><span data-stu-id="861a3-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="861a3-110">Este tutorial mostra como usar o serviço do Azure Cosmos DB para armazenar e acessar dados de um aplicativo Web Python hospedado no Azure e supõe que você tenha experiência prévia com o uso do Python e os sites do Azure.</span><span class="sxs-lookup"><span data-stu-id="861a3-110">This tutorial shows you how to use Azure Cosmos DB to store and access data from a Python web application hosted on Azure and presumes that you have some prior experience using Python and Azure websites.</span></span>

<span data-ttu-id="861a3-111">Este tutorial de banco de dados aborda:</span><span class="sxs-lookup"><span data-stu-id="861a3-111">This database tutorial covers:</span></span>

1. <span data-ttu-id="861a3-112">Crie e provisione uma conta do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="861a3-112">Creating and provisioning a Cosmos DB account.</span></span>
2. <span data-ttu-id="861a3-113">Crie um aplicativo Python Flask.</span><span class="sxs-lookup"><span data-stu-id="861a3-113">Creating a Python Flask application.</span></span>
3. <span data-ttu-id="861a3-114">Conectar-se a e usar o Azure Cosmos DB de seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="861a3-114">Connecting to and using Cosmos DB from your web application.</span></span>
4. <span data-ttu-id="861a3-115">Implante o aplicativo Web no Azure.</span><span class="sxs-lookup"><span data-stu-id="861a3-115">Deploying the web application to Azure.</span></span>

<span data-ttu-id="861a3-116">Seguindo este tutorial, você criará um aplicativo simples de votação que permite que você vote em uma votação.</span><span class="sxs-lookup"><span data-stu-id="861a3-116">By following this tutorial, you will build a simple voting application that allows you to vote for a poll.</span></span>

![Captura de tela do aplicativo de votação criado por este tutorial de banco de dados](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)

## <a name="database-tutorial-prerequisites"></a><span data-ttu-id="861a3-118">Pré-requisitos do tutorial de banco de dados</span><span class="sxs-lookup"><span data-stu-id="861a3-118">Database tutorial prerequisites</span></span>
<span data-ttu-id="861a3-119">Antes de seguir as instruções deste artigo, verifique se você tem os seguintes itens instalados:</span><span class="sxs-lookup"><span data-stu-id="861a3-119">Before following the instructions in this article, you should ensure that you have the following installed:</span></span>

* <span data-ttu-id="861a3-120">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="861a3-120">An active Azure account.</span></span> <span data-ttu-id="861a3-121">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="861a3-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="861a3-122">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="861a3-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
 
    <span data-ttu-id="861a3-123">OU</span><span class="sxs-lookup"><span data-stu-id="861a3-123">OR</span></span> 

    <span data-ttu-id="861a3-124">Uma instalação local do [Emulador do Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="861a3-124">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="861a3-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="861a3-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="861a3-126">[Ferramentas Python para Visual Studio](https://github.com/Microsoft/PTVS/).</span><span class="sxs-lookup"><span data-stu-id="861a3-126">[Python Tools for Visual Studio](https://github.com/Microsoft/PTVS/).</span></span>  
* <span data-ttu-id="861a3-127">[SDK do Microsoft Azure para Python 2.7](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="861a3-127">[Microsoft Azure SDK for Python 2.7](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="861a3-128">[Python 2.7.13](https://www.python.org/downloads/windows/).</span><span class="sxs-lookup"><span data-stu-id="861a3-128">[Python 2.7.13](https://www.python.org/downloads/windows/).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="861a3-129">Se você estiver instalando o Python 2.7 pela primeira vez, escolha **Adicionar python.exe ao Caminho** na tela Personalizar o Python 2.7.13.</span><span class="sxs-lookup"><span data-stu-id="861a3-129">If you are installing Python 2.7 for the first time, ensure that in the Customize Python 2.7.13 screen, you select **Add python.exe to Path**.</span></span>
> 
> ![Captura da tela de Personalizar o Python 2.7.11 em que você precisa escolher Adicionar python.exe ao Caminho](./media/documentdb-python-application/cosmos-db-python-install.png)
> 
> 

* <span data-ttu-id="861a3-131">[Compilador do Microsoft Visual C++ para Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).</span><span class="sxs-lookup"><span data-stu-id="861a3-131">[Microsoft Visual C++ Compiler for Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="861a3-132">Etapa 1: Criar uma conta de banco de dados do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="861a3-132">Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="861a3-133">Vamos começar criando uma conta do BD Cosmos.</span><span class="sxs-lookup"><span data-stu-id="861a3-133">Let's start by creating an Cosmos DB account.</span></span> <span data-ttu-id="861a3-134">Se você já tiver uma conta ou se estiver usando o Emulador do Azure Cosmos DB para este tutorial, pule para a [Etapa 2: Criar um novo aplicativo web do Python Flask](#step-2-create-a-new-python-flask-web-application).</span><span class="sxs-lookup"><span data-stu-id="861a3-134">If you already have an account or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Step 2: Create a new Python Flask web application](#step-2-create-a-new-python-flask-web-application).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<br/>
<span data-ttu-id="861a3-135">Agora vamos mostrar como criar um novo aplicativo Web Python Flask desde o início.</span><span class="sxs-lookup"><span data-stu-id="861a3-135">We will now walk through how to create a new Python Flask web application from the ground up.</span></span>

## <a name="step-2-create-a-new-python-flask-web-application"></a><span data-ttu-id="861a3-136">Etapa 2: Criar um novo aplicativo Web Python Flask</span><span class="sxs-lookup"><span data-stu-id="861a3-136">Step 2: Create a new Python Flask web application</span></span>
1. <span data-ttu-id="861a3-137">No Visual Studio, no menu **Arquivo**, aponte para **Novo** e clique em **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="861a3-137">In Visual Studio, on the **File** menu, point to **New**, and then click **Project**.</span></span>
   
    <span data-ttu-id="861a3-138">A caixa de diálogo **Novo Projeto** aparecerá.</span><span class="sxs-lookup"><span data-stu-id="861a3-138">The **New Project** dialog box appears.</span></span>
2. <span data-ttu-id="861a3-139">No painel esquerdo, expanda **Modelos** e **Python** e clique em **Web**.</span><span class="sxs-lookup"><span data-stu-id="861a3-139">In the left pane, expand **Templates** and then **Python**, and then click **Web**.</span></span> 
3. <span data-ttu-id="861a3-140">Selecione **Projeto Web Flask** no painel central, digite **tutorial** na caixa **Nome** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="861a3-140">Select **Flask  Web Project** in the center pane, then in the **Name** box type **tutorial**, and then click **OK**.</span></span> <span data-ttu-id="861a3-141">Lembre-se de que os nomes de pacote do Python devem ser escritos em letras minúsculas, como descrito no [Guia de estilo do Código Python](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span><span class="sxs-lookup"><span data-stu-id="861a3-141">Remember that Python package names should be all lowercase, as described in the [Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span></span>
   
    <span data-ttu-id="861a3-142">Para aqueles que não estejam familiarizados com o Python Flask, trata-se de uma estrutura de desenvolvimento de aplicativos Web que ajuda você a compilar aplicativos Web no Python mais rapidamente.</span><span class="sxs-lookup"><span data-stu-id="861a3-142">For those new to Python Flask, it is a web application development framework that helps you build web applications in Python faster.</span></span>
   
    ![Captura de tela da janela Novo Projeto no Visual Studio com o Python realçado à esquerda, o Projeto Web do Python Flask selecionado no meio e o tutorial do nome na caixa Nome](./media/documentdb-python-application/image9.png)
4. <span data-ttu-id="861a3-144">Na janela **Ferramentas Python para Visual Studio**, clique em **Instalar em um ambiente virtual**.</span><span class="sxs-lookup"><span data-stu-id="861a3-144">In the **Python Tools for Visual Studio** window, click **Install into a virtual environment**.</span></span> 
   
    ![Captura de tela do tutorial de banco de dados — janela Ferramentas Python para Visual Studio](./media/documentdb-python-application/python-install-virtual-environment.png)
5. <span data-ttu-id="861a3-146">Na janela **Adicionar Ambiente Virtual**, você pode aceitar os padrões e usar o Python 2.7 como o ambiente base, pois o PyDocumentDB no momento não oferece suporte ao Python 3. x, e depois clicar em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="861a3-146">In the **Add Virtual Environment** window, you can accept the defaults and use Python 2.7 as the base environment because PyDocumentDB does not currently support Python 3.x, and then click **Create**.</span></span> <span data-ttu-id="861a3-147">Isso configura o ambiente virtual do Python necessário ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="861a3-147">This sets up the required Python virtual environment for your project.</span></span>
   
    ![Captura de tela do tutorial de banco de dados — janela Ferramentas Python para Visual Studio](./media/documentdb-python-application/image10_A.png)
   
    <span data-ttu-id="861a3-149">A janela de saída exibe `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` quando o ambiente é instalado com êxito.</span><span class="sxs-lookup"><span data-stu-id="861a3-149">The output window displays `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` when the environment is successfully installed.</span></span>

## <a name="step-3-modify-the-python-flask-web-application"></a><span data-ttu-id="861a3-150">Etapa 3: Modificar o aplicativo Web Python Flask</span><span class="sxs-lookup"><span data-stu-id="861a3-150">Step 3: Modify the Python Flask web application</span></span>
### <a name="add-the-python-flask-packages-to-your-project"></a><span data-ttu-id="861a3-151">Adicionar pacotes do Python Flask ao seu projeto</span><span class="sxs-lookup"><span data-stu-id="861a3-151">Add the Python Flask packages to your project</span></span>
<span data-ttu-id="861a3-152">Depois que seu projeto estiver configurado, você precisará adicionar alguns pacotes Flask necessários ao projeto, incluindo pydocumentdb, o pacote do Python para o DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="861a3-152">After your project is set up, you'll need to add the required Flask packages to your project, including pydocumentdb, the Python package for DocumentDB.</span></span>

1. <span data-ttu-id="861a3-153">No Gerenciador de Soluções, abra o arquivo denominado **requirements.txt** e substitua o conteúdo pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="861a3-153">In Solution Explorer, open the file named **requirements.txt** and replace the contents with the following:</span></span>
   
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
2. <span data-ttu-id="861a3-154">Salve o arquivo **requirements.txt** .</span><span class="sxs-lookup"><span data-stu-id="861a3-154">Save the **requirements.txt** file.</span></span> 
3. <span data-ttu-id="861a3-155">No Gerenciador de Soluções, clique com o botão direito do mouse em **env** e clique em **Instalar de requirements.txt**.</span><span class="sxs-lookup"><span data-stu-id="861a3-155">In Solution Explorer, right-click **env** and click **Install from requirements.txt**.</span></span>
   
    ![Captura de tela mostrando env (Python 2.7) selecionado com a Instalação de requirements.txt realçada na lista](./media/documentdb-python-application/cosmos-db-python-install-from-requirements.png)
   
    <span data-ttu-id="861a3-157">Após a instalação bem-sucedida, a janela de saída exibirá o seguinte:</span><span class="sxs-lookup"><span data-stu-id="861a3-157">After successful installation, the output window displays the following:</span></span>
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > <span data-ttu-id="861a3-158">Em casos raros, você poderá ver uma falha na janela de saída.</span><span class="sxs-lookup"><span data-stu-id="861a3-158">In rare cases, you might see a failure in the output window.</span></span> <span data-ttu-id="861a3-159">Se isso ocorrer, verifique se o erro está relacionado à limpeza.</span><span class="sxs-lookup"><span data-stu-id="861a3-159">If this happens, check if the error is related to cleanup.</span></span> <span data-ttu-id="861a3-160">Algumas vezes, há falha na limpeza, mas a instalação ainda será bem-sucedida (role para cima na janela de saída para verificar isso).</span><span class="sxs-lookup"><span data-stu-id="861a3-160">Sometimes the cleanup fails, but the installation will still be successful (scroll up in the output window to verify this).</span></span> <span data-ttu-id="861a3-161">Você pode verificar a instalação [Como verificar o ambiente virtual](#verify-the-virtual-environment).</span><span class="sxs-lookup"><span data-stu-id="861a3-161">You can check your installation by [Verifying the virtual environment](#verify-the-virtual-environment).</span></span> <span data-ttu-id="861a3-162">Se houver falha na instalação, mas se a verificação for bem-sucedida, você poderá prosseguir.</span><span class="sxs-lookup"><span data-stu-id="861a3-162">If the installation failed but the verification is successful, it's OK to continue.</span></span>
   > 
   > 

### <a name="verify-the-virtual-environment"></a><span data-ttu-id="861a3-163">Verifique o ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="861a3-163">Verify the virtual environment</span></span>
<span data-ttu-id="861a3-164">Vamos garantir que tudo esteja instalado corretamente.</span><span class="sxs-lookup"><span data-stu-id="861a3-164">Let's make sure that everything is installed correctly.</span></span>

1. <span data-ttu-id="861a3-165">Crie a solução ao pressionar **Ctrl**+**Shift**+**B**.</span><span class="sxs-lookup"><span data-stu-id="861a3-165">Build the solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="861a3-166">Se a compilação for bem-sucedida, inicie o site pressionando **F5**.</span><span class="sxs-lookup"><span data-stu-id="861a3-166">Once the build succeeds, start the website by pressing **F5**.</span></span> <span data-ttu-id="861a3-167">Isso iniciará o servidor de desenvolvimento do Flask e iniciará o navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="861a3-167">This launches the Flask development server and starts your web browser.</span></span> <span data-ttu-id="861a3-168">Você deve ver a página a seguir.</span><span class="sxs-lookup"><span data-stu-id="861a3-168">You should see the following page.</span></span>
   
    ![O projeto de desenvolvimento da Web Python Flask vazio exibido em um navegador](./media/documentdb-python-application/image12.png)
3. <span data-ttu-id="861a3-170">Pare a depuração do site pressionando **Shift**+**F5** no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="861a3-170">Stop debugging the website by pressing **Shift**+**F5** in Visual Studio.</span></span>

### <a name="create-database-collection-and-document-definitions"></a><span data-ttu-id="861a3-171">Criar definições de banco de dados, de coleção e de documentos</span><span class="sxs-lookup"><span data-stu-id="861a3-171">Create database, collection, and document definitions</span></span>
<span data-ttu-id="861a3-172">Agora vamos criar seu aplicativo de votação adicionando novos arquivos e enviando atualizações para outras pessoas.</span><span class="sxs-lookup"><span data-stu-id="861a3-172">Now let's create your voting application by adding new files and updating others.</span></span>

1. <span data-ttu-id="861a3-173">No Gerenciador de Soluções, clique com o botão direito do mouse no **tutorial** do projeto e clique em **Adicionar** e em **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="861a3-173">In Solution Explorer, right-click the **tutorial** project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="861a3-174">Escolha **Arquivo Python Vazio** e nomeie o arquivo como **forms.py**.</span><span class="sxs-lookup"><span data-stu-id="861a3-174">Select **Empty Python File** and name the file **forms.py**.</span></span>  
2. <span data-ttu-id="861a3-175">Adicione o código a seguir ao arquivo forms.py e salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="861a3-175">Add the following code to the forms.py file, and then save the file.</span></span>

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-the-required-imports-to-viewspy"></a><span data-ttu-id="861a3-176">Adicione as importações necessárias a views.py</span><span class="sxs-lookup"><span data-stu-id="861a3-176">Add the required imports to views.py</span></span>
1. <span data-ttu-id="861a3-177">No Gerenciador de Soluções, expanda a pasta **tutorial** e abra o arquivo **views.py**.</span><span class="sxs-lookup"><span data-stu-id="861a3-177">In Solution Explorer, expand the **tutorial** folder, and open the **views.py** file.</span></span> 
2. <span data-ttu-id="861a3-178">Adicione as seguintes instruções de importação à parte superior do arquivo **views.py** , então salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="861a3-178">Add the following import statements to the top of the **views.py** file, then save the file.</span></span> <span data-ttu-id="861a3-179">Elas importarão o SDK de Python do Azure Cosmos DB e os pacotes Flask.</span><span class="sxs-lookup"><span data-stu-id="861a3-179">These import Cosmos DB's PythonSDK and the Flask packages.</span></span>
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a><span data-ttu-id="861a3-180">Criar banco de dados, coleção e documento</span><span class="sxs-lookup"><span data-stu-id="861a3-180">Create database, collection, and document</span></span>
* <span data-ttu-id="861a3-181">Ainda em **views.py**, adicione o código a seguir ao final do arquivo.</span><span class="sxs-lookup"><span data-stu-id="861a3-181">Still in **views.py**, add the following code to the end of the file.</span></span> <span data-ttu-id="861a3-182">Ele se encarrega de criar o banco de dados usado pelo formulário.</span><span class="sxs-lookup"><span data-stu-id="861a3-182">This takes care of creating the database used by the form.</span></span> <span data-ttu-id="861a3-183">Não exclua nenhum código existente em **views.py**.</span><span class="sxs-lookup"><span data-stu-id="861a3-183">Do not delete any of the existing code in **views.py**.</span></span> <span data-ttu-id="861a3-184">Basta acrescentá-lo ao final.</span><span class="sxs-lookup"><span data-stu-id="861a3-184">Simply append this to the end.</span></span>

```python
@app.route('/create')
def create():
    """Renders the contact page."""
    client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

    # Attempt to delete the database.  This allows this to be used to recreate as well as create
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


### <a name="read-database-collection-document-and-submit-form"></a><span data-ttu-id="861a3-185">Ler o banco de dados, a coleção, o documento e enviar o formulário</span><span class="sxs-lookup"><span data-stu-id="861a3-185">Read database, collection, document, and submit form</span></span>
* <span data-ttu-id="861a3-186">Ainda em **views.py**, adicione o código a seguir ao final do arquivo.</span><span class="sxs-lookup"><span data-stu-id="861a3-186">Still in **views.py**, add the following code to the end of the file.</span></span> <span data-ttu-id="861a3-187">Ele cuida da configuração do formulário, da leitura do banco de dados, da coleção e do documento.</span><span class="sxs-lookup"><span data-stu-id="861a3-187">This takes care of setting up the form, reading the database, collection, and document.</span></span> <span data-ttu-id="861a3-188">Não exclua nenhum código existente em **views.py**.</span><span class="sxs-lookup"><span data-stu-id="861a3-188">Do not delete any of the existing code in **views.py**.</span></span> <span data-ttu-id="861a3-189">Basta acrescentá-lo ao final.</span><span class="sxs-lookup"><span data-stu-id="861a3-189">Simply append this to the end.</span></span>

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

        # Take the data from the deploy_preference and increment our database
        doc[form.deploy_preference.data] = doc[form.deploy_preference.data] + 1
        replaced_document = client.ReplaceDocument(doc['_self'], doc)

        # Create a model to pass to results.html
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


### <a name="create-the-html-files"></a><span data-ttu-id="861a3-190">Criar os arquivos HTML</span><span class="sxs-lookup"><span data-stu-id="861a3-190">Create the HTML files</span></span>
1. <span data-ttu-id="861a3-191">No Gerenciador de Soluções, na pasta **tutorial**, clique com o botão direito do mouse na pasta **templates**, clique em **Adicionar** e clique em **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="861a3-191">In Solution Explorer, in the **tutorial** folder, right click the **templates** folder, click **Add**, and then click **New Item**.</span></span> 
2. <span data-ttu-id="861a3-192">Escolha **Página HTML** e, na caixa Nome, digite **create.html**.</span><span class="sxs-lookup"><span data-stu-id="861a3-192">Select **HTML Page**, and then in the name box type **create.html**.</span></span> 
3. <span data-ttu-id="861a3-193">Repita as etapas 1 e 2 para criar dois arquivos HTML adicionais: results.html e vote.html.</span><span class="sxs-lookup"><span data-stu-id="861a3-193">Repeat steps 1 and 2 to create two additional HTML files: results.html and vote.html.</span></span>
4. <span data-ttu-id="861a3-194">Adicione o código a seguir a **create.html** in the `<body>` .</span><span class="sxs-lookup"><span data-stu-id="861a3-194">Add the following code to **create.html** in the `<body>` element.</span></span> <span data-ttu-id="861a3-195">Ele exibe uma mensagem indicando que um banco de dados, uma coleção e um documento novos foram criados.</span><span class="sxs-lookup"><span data-stu-id="861a3-195">It displays a message stating that we created a new database, collection, and document.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. <span data-ttu-id="861a3-196">Adicione o código a seguir a **results.html** no elemento `<body`>.</span><span class="sxs-lookup"><span data-stu-id="861a3-196">Add the following code to **results.html** in the `<body`> element.</span></span> <span data-ttu-id="861a3-197">Ele exibe os resultados da votação.</span><span class="sxs-lookup"><span data-stu-id="861a3-197">It displays the results of the poll.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Results of the vote</h2>
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
6. <span data-ttu-id="861a3-198">Adicione o código a seguir a **vote.html** no elemento `<body`>.</span><span class="sxs-lookup"><span data-stu-id="861a3-198">Add the following code to **vote.html** in the `<body`> element.</span></span> <span data-ttu-id="861a3-199">Ele exibe a votação e aceita os votos.</span><span class="sxs-lookup"><span data-stu-id="861a3-199">It displays the poll and accepts the votes.</span></span> <span data-ttu-id="861a3-200">Ao registrar os votos, o controle será passado a views.py, onde reconheceremos os votos realizados e atualizaremos o documento de acordo com eles.</span><span class="sxs-lookup"><span data-stu-id="861a3-200">On registering the votes, the control is passed over to views.py where we will recognize the vote cast and append the document accordingly.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>What is your favorite way to host an application on Azure?</h2>
    <form action="" method="post" name="vote">
        {{form.hidden_tag()}}
            {{form.deploy_preference}}
            <button class="btn btn-primary" type="submit">Vote</button>
    </form>
    {% endblock %}
    ```
7. <span data-ttu-id="861a3-201">Na pasta **templates**, substitua o conteúdo de **index.html** pelo seguinte.</span><span class="sxs-lookup"><span data-stu-id="861a3-201">In the **templates** folder, replace the contents of **index.html** with the following.</span></span> <span data-ttu-id="861a3-202">Ele serve como a página de chegada de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="861a3-202">This serves as the landing page for your application.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + Azure Cosmos DB Voting Application.</h2>
    <h3>This is a sample Cosmos DB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear the Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-the-initpy"></a><span data-ttu-id="861a3-203">Adicione um arquivo de configuração e altere \_\_init\_\_.py</span><span class="sxs-lookup"><span data-stu-id="861a3-203">Add a configuration file and change the \_\_init\_\_.py</span></span>
1. <span data-ttu-id="861a3-204">No Gerenciador de Soluções, clique com o botão direito do mouse no **tutorial** do projeto, clique em **Adicionar**, clique em **Novo Item**, escolha **Arquivo Python Vazio** e nomeie o arquivo como **config.py**.</span><span class="sxs-lookup"><span data-stu-id="861a3-204">In Solution Explorer, right-click the **tutorial** project, click **Add**, click **New Item**, select **Empty Python File**, and then name the file **config.py**.</span></span> <span data-ttu-id="861a3-205">Esse arquivo de configuração é exigido por formulários no flask.</span><span class="sxs-lookup"><span data-stu-id="861a3-205">This config file is required by forms in Flask.</span></span> <span data-ttu-id="861a3-206">Você também pode usá-lo para fornecer uma chave secreta.</span><span class="sxs-lookup"><span data-stu-id="861a3-206">You can use it to provide a secret key as well.</span></span> <span data-ttu-id="861a3-207">Essa chave não será necessária neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="861a3-207">This key is not needed for this tutorial though.</span></span>
2. <span data-ttu-id="861a3-208">Adicione o código a seguir a config.py. Você precisará alterar os valores de **DOCUMENTDB\_HOST** e de **DOCUMENTDB\_KEY** na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="861a3-208">Add the following code to config.py, you'll need to alter the values of **DOCUMENTDB\_HOST** and **DOCUMENTDB\_KEY** in the next step.</span></span>
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. <span data-ttu-id="861a3-209">No [portal do Azure](https://portal.azure.com/), navegue até a folha **Chaves** clicando em **Procurar**, **Contas do Azure Cosmos DB**, clique duas vezes no nome da conta a usar e clique no botão **Chaves** na área **Essentials**.</span><span class="sxs-lookup"><span data-stu-id="861a3-209">In the [Azure portal](https://portal.azure.com/), navigate to the **Keys** blade by clicking **Browse**, **Azure Cosmos DB Accounts**, double-click the name of the account to use, and then click the **Keys** button in the **Essentials** area.</span></span> <span data-ttu-id="861a3-210">Na folha **Chaves**, copie o valor de **URI** e cole-o no arquivo **config.py** como o valor da propriedade **DOCUMENTDB\_HOST**.</span><span class="sxs-lookup"><span data-stu-id="861a3-210">In the **Keys** blade, copy the **URI** value and paste it into the **config.py** file, as the value for the **DOCUMENTDB\_HOST** property.</span></span> 
4. <span data-ttu-id="861a3-211">Novamente no portal do Azure, na folha **Chaves**, copie o valor da **Chave Primária** ou da **Chave Secundária** e cole-o no arquivo **config.py** como o valor da propriedade **DOCUMENTDB\_KEY**.</span><span class="sxs-lookup"><span data-stu-id="861a3-211">Back in the Azure portal, in the **Keys** blade, copy the value of the **Primary Key** or the **Secondary Key**, and paste it into the **config.py** file, as the value for the **DOCUMENTDB\_KEY** property.</span></span>
5. <span data-ttu-id="861a3-212">No arquivo **\_\_init\_\_.py**, adicione a linha a seguir.</span><span class="sxs-lookup"><span data-stu-id="861a3-212">In the **\_\_init\_\_.py** file, add the following line.</span></span> 
   
        app.config.from_object('config')
   
    <span data-ttu-id="861a3-213">Portanto, o conteúdo do arquivo deve ser:</span><span class="sxs-lookup"><span data-stu-id="861a3-213">So that the content of the file is:</span></span>
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. <span data-ttu-id="861a3-214">Depois de adicionar todos os arquivos, o Gerenciador de Soluções deve ficar assim:</span><span class="sxs-lookup"><span data-stu-id="861a3-214">After adding all the files, Solution Explorer should look like this:</span></span>
   
    ![Captura de tela da janela do Gerenciador de Soluções do Visual Studio](./media/documentdb-python-application/cosmos-db-python-solution-explorer.png)

## <a name="step-4-run-your-web-application-locally"></a><span data-ttu-id="861a3-216">Etapa 4: executar o aplicativo localmente</span><span class="sxs-lookup"><span data-stu-id="861a3-216">Step 4: Run your web application locally</span></span>
1. <span data-ttu-id="861a3-217">Crie a solução ao pressionar **Ctrl**+**Shift**+**B**.</span><span class="sxs-lookup"><span data-stu-id="861a3-217">Build the solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="861a3-218">Se a compilação for bem-sucedida, inicie o site pressionando **F5**.</span><span class="sxs-lookup"><span data-stu-id="861a3-218">Once the build succeeds, start the website by pressing **F5**.</span></span> <span data-ttu-id="861a3-219">Você deverá ver o seguinte na tela.</span><span class="sxs-lookup"><span data-stu-id="861a3-219">You should see the following on your screen.</span></span>
   
    ![Captura de tela do Aplicativo de votação do Python + Azure Cosmos DB exibido em um navegador da Web](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)
3. <span data-ttu-id="861a3-221">Clique em **Criar/limpar o banco de dados de votação** para gerar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="861a3-221">Click **Create/Clear the Voting Database** to generate the database.</span></span>
   
    ![Captura de tela de Criar Página do aplicativo Web — detalhes de desenvolvimento](./media/documentdb-python-application/cosmos-db-python-run-create-page.png)
4. <span data-ttu-id="861a3-223">Em seguida, clique em **Votar** e selecione sua opção.</span><span class="sxs-lookup"><span data-stu-id="861a3-223">Then, click **Vote** and select your option.</span></span>
   
    ![Captura de tela do aplicativo Web com uma pergunta de votação publicada](./media/documentdb-python-application/cosmos-db-vote.png)
5. <span data-ttu-id="861a3-225">Para cada voto enviado, o contador adequado será incrementado.</span><span class="sxs-lookup"><span data-stu-id="861a3-225">For every vote you cast, it increments the appropriate counter.</span></span>
   
    ![Captura de tela da página de Resultados da votação](./media/documentdb-python-application/cosmos-db-voting-results.png)
6. <span data-ttu-id="861a3-227">Pare a depuração do projeto pressionando Shift+F5.</span><span class="sxs-lookup"><span data-stu-id="861a3-227">Stop debugging the project by pressing Shift+F5.</span></span>

## <a name="step-5-deploy-the-web-application-to-azure"></a><span data-ttu-id="861a3-228">Etapa 5: Implantar o aplicativo Web no Azure</span><span class="sxs-lookup"><span data-stu-id="861a3-228">Step 5: Deploy the web application to Azure</span></span>
<span data-ttu-id="861a3-229">Agora que você tem o aplicativo completo funcionando corretamente no Azure Cosmos DB, vamos implantá-lo no Azure.</span><span class="sxs-lookup"><span data-stu-id="861a3-229">Now that you have the complete application working correctly against Cosmos DB, we're going to deploy this to Azure.</span></span>

1. <span data-ttu-id="861a3-230">Clique com o botão direito do mouse no projeto no Gerenciador de Soluções (verifique se ele não está sendo executado localmente) e selecione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="861a3-230">Right-click the project in Solution Explorer (make sure you're not still running it locally) and select **Publish**.</span></span>  
   
     ![Captura de tela do tutorial selecionado no Gerenciador de Soluções, com a opção de Publicar realçada](./media/documentdb-python-application/image20.png)
2. <span data-ttu-id="861a3-232">Na caixa de diálogo, **Publicar**, escolha **Serviço de Aplicativo do Microsoft Azure**, escolha **Criar novo** e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="861a3-232">In the **Publish** dialog box, select **Microsoft Azure App Service**, select **Create New**, and then click **Publish**.</span></span>
   
    ![Captura de tela da janela Publicar Web com o Serviço de Aplicativo do Microsoft Azure realçado](./media/documentdb-python-application/cosmos-db-python-publish.png)
3. <span data-ttu-id="861a3-234">Na caixa de diálogo **Criar Serviço de Aplicativo**, digite o nome do aplicativo Web com a **Assinatura**, o **Grupo de Recursos** e o **Plano do Serviço de Aplicativo** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="861a3-234">In the **Create App Service** dialog box, enter the name for your web app along with your **Subscription**, **Resource Group**, and **App Service Plan**, then click **Create**.</span></span>
   
    ![Captura de tela da Janela de Aplicativos Web do Microsoft Azure](./media/documentdb-python-application/cosmos-db-python-create-app-service.png)
4. <span data-ttu-id="861a3-236">Em poucos segundos, o Visual Studio terminará de publicar seu serviço de aplicativo e iniciará um navegador no qual você poderá ver seu trabalho sendo executado no Azure!</span><span class="sxs-lookup"><span data-stu-id="861a3-236">In a few seconds, Visual Studio will finish publishing your app service and launch a browser where you can see your handiwork running in Azure!</span></span>

    ![Captura de tela da Janela de Aplicativos Web do Microsoft Azure](./media/documentdb-python-application/cosmos-db-python-appservice-created.png)

## <a name="troubleshooting"></a><span data-ttu-id="861a3-238">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="861a3-238">Troubleshooting</span></span>
<span data-ttu-id="861a3-239">Se esse for o primeiro aplicativo Python executado em seu computador, verifique se as pastas a seguir (ou os locais de instalação equivalentes) estão incluídos na variável PATH:</span><span class="sxs-lookup"><span data-stu-id="861a3-239">If this is the first Python app you've run on your computer, ensure that the following folders (or the equivalent installation locations) are included in your PATH variable:</span></span>

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

<span data-ttu-id="861a3-240">Se receber um erro em sua página de votação, e se tiver nomeado seu projeto com algo diferente de **tutorial**, verifique se **\_\_init\_\_.py** faz referência ao nome de projeto correto na linha: `import tutorial.view`.</span><span class="sxs-lookup"><span data-stu-id="861a3-240">If you receive an error on your vote page, and you named your project something other than **tutorial**, make sure that **\_\_init\_\_.py** references the correct project name in the line: `import tutorial.view`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="861a3-241">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="861a3-241">Next steps</span></span>
<span data-ttu-id="861a3-242">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="861a3-242">Congratulations!</span></span> <span data-ttu-id="861a3-243">Você acabou de concluir seu primeiro aplicativo Web Python usando o Cosmos DB e o publicou no Azure.</span><span class="sxs-lookup"><span data-stu-id="861a3-243">You have just completed your first Python web application using Cosmos DB and published it to Azure.</span></span>

<span data-ttu-id="861a3-244">Atualizamos e aperfeiçoamos este tópico com frequência, de acordo com seus comentários.</span><span class="sxs-lookup"><span data-stu-id="861a3-244">We update and improve this topic frequently based on your feedback.</span></span>  <span data-ttu-id="861a3-245">Depois de concluir o tutorial, use os botões de votação nas partes superior e inferior desta página e lembre-se de incluir seus comentários sobre os aperfeiçoamentos que deseja ver.</span><span class="sxs-lookup"><span data-stu-id="861a3-245">Once you've completed the tutorial, please using the voting buttons at the top and bottom of this page, and be sure to include your feedback on what improvements you want to see made.</span></span> <span data-ttu-id="861a3-246">Se quiser que entremos em contato com você diretamente, inclua seu endereço de email em seu comentário.</span><span class="sxs-lookup"><span data-stu-id="861a3-246">If you'd like us to contact you directly, feel free to include your email address in your comments.</span></span>

<span data-ttu-id="861a3-247">Para incluir funcionalidade adicional no aplicativo Web, examine as APIs disponíveis no [SDK do Python do Azure Cosmos DB](documentdb-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="861a3-247">To add additional functionality to your web application, review the APIs available in the [Azure Cosmos DB Python SDK](documentdb-sdk-python.md).</span></span>

<span data-ttu-id="861a3-248">Para saber mais sobre o Azure, o Visual Studio e o Python, consulte o [Centro de desenvolvedores do Python](https://azure.microsoft.com/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="861a3-248">For more information about Azure, Visual Studio, and Python, see the [Python Developer Center](https://azure.microsoft.com/develop/python/).</span></span> 

<span data-ttu-id="861a3-249">Para obter outros tutoriais do Python Flask, consulte [The Flask Mega-Tutorial, Part I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span><span class="sxs-lookup"><span data-stu-id="861a3-249">For additional Python Flask tutorials, see [The Flask Mega-Tutorial, Part I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span></span> 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com
