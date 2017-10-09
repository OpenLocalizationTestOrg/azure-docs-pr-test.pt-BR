---
title: "conjuntos de dados aaaAccess com biblioteca de cliente do Python de aprendizado de máquina | Microsoft Docs"
description: "Instalar e usar o hello tooaccess de biblioteca de cliente do Python e gerenciar dados de aprendizado de máquina do Azure com segurança de um ambiente local do Python."
services: machine-learning
documentationcenter: python
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 9ab42272-c30c-4b7e-8e66-d64eafef22d0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: huvalo;bradsev
ms.openlocfilehash: f55067118f13c52bf677930a20836ce6989f8187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="access-datasets-with-python-using-hello-azure-machine-learning-python-client-library"></a><span data-ttu-id="982e4-103">Conjuntos de dados do Access com Python usando a biblioteca de cliente do Python de aprendizado de máquina do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="982e4-103">Access datasets with Python using hello Azure Machine Learning Python client library</span></span>
<span data-ttu-id="982e4-104">visualização de saudação da biblioteca de cliente do Python de aprendizado de máquina do Microsoft Azure pode habilitar o acesso seguro tooyour conjuntos de dados de aprendizado de máquina do Azure de um ambiente local do Python e permite a criação de saudação e o gerenciamento de conjuntos de dados em um espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="982e4-104">hello preview of Microsoft Azure Machine Learning Python client library can enable secure access tooyour Azure Machine Learning datasets from a local Python environment and enables hello creation and management of datasets in a workspace.</span></span>

<span data-ttu-id="982e4-105">Este tópico fornece instruções sobre como:</span><span class="sxs-lookup"><span data-stu-id="982e4-105">This topic provides instructions on how to:</span></span>

* <span data-ttu-id="982e4-106">instalar a biblioteca de cliente do Python de aprendizado de máquina Olá</span><span class="sxs-lookup"><span data-stu-id="982e4-106">install hello Machine Learning Python client library</span></span> 
* <span data-ttu-id="982e4-107">acessar e carregar conjuntos de dados, incluindo instruções sobre como tooget autorização tooaccess conjuntos de dados de aprendizado de máquina do Azure do seu ambiente local do Python</span><span class="sxs-lookup"><span data-stu-id="982e4-107">access and upload datasets, including instructions on how tooget authorization tooaccess Azure Machine Learning datasets from your local Python environment</span></span>
* <span data-ttu-id="982e4-108">acessar conjuntos de dados intermediários por meio de testes</span><span class="sxs-lookup"><span data-stu-id="982e4-108">access intermediate datasets from experiments</span></span>
* <span data-ttu-id="982e4-109">usar Olá Python cliente biblioteca tooenumerate conjuntos de dados, acessar os metadados, ler o conteúdo de saudação do conjunto de dados, criar novos conjuntos de dados e atualizar conjuntos de dados existentes</span><span class="sxs-lookup"><span data-stu-id="982e4-109">use hello Python client library tooenumerate datasets, access metadata, read hello contents of a dataset, create new datasets and update existing datasets</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <span data-ttu-id="982e4-110"><a name="prerequisites"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="982e4-110"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="982e4-111">biblioteca de cliente do Python Olá foi testada em Olá ambientes a seguir:</span><span class="sxs-lookup"><span data-stu-id="982e4-111">hello Python client library has been tested under hello following environments:</span></span>

* <span data-ttu-id="982e4-112">Windows, Mac e Linux</span><span class="sxs-lookup"><span data-stu-id="982e4-112">Windows, Mac and Linux</span></span>
* <span data-ttu-id="982e4-113">Python 2.7, 3.3 e 3.4</span><span class="sxs-lookup"><span data-stu-id="982e4-113">Python 2.7, 3.3 and 3.4</span></span>

<span data-ttu-id="982e4-114">Ele tem uma dependência em Olá pacotes a seguir:</span><span class="sxs-lookup"><span data-stu-id="982e4-114">It has a dependency on hello following packages:</span></span>

* <span data-ttu-id="982e4-115">solicitações</span><span class="sxs-lookup"><span data-stu-id="982e4-115">requests</span></span>
* <span data-ttu-id="982e4-116">python-dateutil</span><span class="sxs-lookup"><span data-stu-id="982e4-116">python-dateutil</span></span>
* <span data-ttu-id="982e4-117">pandas</span><span class="sxs-lookup"><span data-stu-id="982e4-117">pandas</span></span>

<span data-ttu-id="982e4-118">É recomendável usar uma distribuição de Python como [Anaconda](http://continuum.io/downloads#all) ou [abóbada](https://store.enthought.com/downloads/), que acompanham o Python, IPython e instalados Olá três pacotes listados acima.</span><span class="sxs-lookup"><span data-stu-id="982e4-118">We recommend using a Python distribution such as [Anaconda](http://continuum.io/downloads#all) or [Canopy](https://store.enthought.com/downloads/), which come with Python, IPython and hello three packages listed above installed.</span></span> <span data-ttu-id="982e4-119">Embora o IPython não seja estritamente necessário, é um ótimo ambiente para manipular e visualizar dados interativamente.</span><span class="sxs-lookup"><span data-stu-id="982e4-119">Although IPython is not strictly required, it is a great environment for manipulating and visualizing data interactively.</span></span>

### <span data-ttu-id="982e4-120"><a name="installation"></a>Como tooinstall Olá biblioteca de cliente do Python de aprendizado de máquina do Azure</span><span class="sxs-lookup"><span data-stu-id="982e4-120"><a name="installation"></a>How tooinstall hello Azure Machine Learning Python client library</span></span>
<span data-ttu-id="982e4-121">biblioteca de cliente do Python de aprendizado de máquina do Azure Olá também deve ser instalado toocomplete tarefas de saudação descritas neste tópico.</span><span class="sxs-lookup"><span data-stu-id="982e4-121">hello Azure Machine Learning Python client library must also be installed toocomplete hello tasks outlined in this topic.</span></span> <span data-ttu-id="982e4-122">Ele está disponível no hello [índice de pacote do Python](https://pypi.python.org/pypi/azureml).</span><span class="sxs-lookup"><span data-stu-id="982e4-122">It is available from hello [Python Package Index](https://pypi.python.org/pypi/azureml).</span></span> <span data-ttu-id="982e4-123">tooinstall-lo em seu ambiente de Python, executar Olá seguinte comando do seu ambiente local do Python:</span><span class="sxs-lookup"><span data-stu-id="982e4-123">tooinstall it in your Python environment, run hello following command from your local Python environment:</span></span>

    pip install azureml

<span data-ttu-id="982e4-124">Como alternativa, você pode baixar e instalar de origens de saudação em [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span><span class="sxs-lookup"><span data-stu-id="982e4-124">Alternatively, you can download and install from hello sources on [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span></span>

    python setup.py install

<span data-ttu-id="982e4-125">Se você tiver o git instalado em seu computador, você pode usar o pip tooinstall diretamente do repositório do git hello:</span><span class="sxs-lookup"><span data-stu-id="982e4-125">If you have git installed on your machine, you can use pip tooinstall directly from hello git repository:</span></span>

    pip install git+https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python.git


## <span data-ttu-id="982e4-126"><a name="datasetAccess"></a>Usar conjuntos de dados de tooaccess do Studio Code trechos de código</span><span class="sxs-lookup"><span data-stu-id="982e4-126"><a name="datasetAccess"></a>Use Studio Code snippets tooaccess datasets</span></span>
<span data-ttu-id="982e4-127">biblioteca de cliente do Python Olá fornece conjuntos de dados existentes do tooyour acesso programático em experiências que foram executadas.</span><span class="sxs-lookup"><span data-stu-id="982e4-127">hello Python client library gives you programmatic access tooyour existing datasets from experiments that have been run.</span></span>

<span data-ttu-id="982e4-128">Na interface de web do hello Studio, você pode gerar trechos de código que incluem todos os toodownload de informações necessárias de saudação e desserializar os conjuntos de dados como objetos Pandas DataFrame em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="982e4-128">From hello Studio web interface, you can generate code snippets that include all hello necessary information toodownload and deserialize datasets as Pandas DataFrame objects on your location machine.</span></span>

### <span data-ttu-id="982e4-129"><a name="security"></a>Segurança para acesso a dados</span><span class="sxs-lookup"><span data-stu-id="982e4-129"><a name="security"></a>Security for data access</span></span>
<span data-ttu-id="982e4-130">Olá trechos de código fornecidos pelo Studio para uso com a biblioteca de cliente do Python Olá inclui a id do espaço de trabalho e a autorização token.</span><span class="sxs-lookup"><span data-stu-id="982e4-130">hello code snippets provided by Studio for use with hello Python client library includes your workspace id and authorization token.</span></span> <span data-ttu-id="982e4-131">Esses fornecem espaço de trabalho de tooyour acesso completo e devem ser protegidos, como uma senha.</span><span class="sxs-lookup"><span data-stu-id="982e4-131">These provide full access tooyour workspace and must be protected, like a password.</span></span>

<span data-ttu-id="982e4-132">Por motivos de segurança, funcionalidade de trecho de código Olá só está disponível toousers com sua função definida como **proprietário** de espaço de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="982e4-132">For security reasons, hello code snippet functionality is only available toousers that have their role set as **Owner** for hello workspace.</span></span> <span data-ttu-id="982e4-133">Sua função é exibida no estúdio de aprendizado de máquina do Azure em Olá **usuários** página em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="982e4-133">Your role is displayed in Azure Machine Learning Studio on hello **USERS** page under **Settings**.</span></span>

![Segurança][security]

<span data-ttu-id="982e4-135">Se sua função não está definida como **proprietário**, você pode solicitar toobe novamente convidado como um proprietário ou peça ao proprietário de saudação do hello tooprovide de espaço de trabalho com o trecho de código hello.</span><span class="sxs-lookup"><span data-stu-id="982e4-135">If your role is not set as **Owner**, you can either request toobe reinvited as an owner, or ask hello owner of hello workspace tooprovide you with hello code snippet.</span></span>

<span data-ttu-id="982e4-136">token de autorização do tooobtain Olá, você pode fazer um dos seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="982e4-136">tooobtain hello authorization token, you can do one of hello following:</span></span>

* <span data-ttu-id="982e4-137">Solicitar um token de um proprietário.</span><span class="sxs-lookup"><span data-stu-id="982e4-137">Ask for a token from an owner.</span></span> <span data-ttu-id="982e4-138">Os proprietários podem acessar seus tokens de autorização na página de configurações de saudação do seu espaço de trabalho no Studio.</span><span class="sxs-lookup"><span data-stu-id="982e4-138">Owners can access their authorization tokens from hello Settings page of their workspace in Studio.</span></span> <span data-ttu-id="982e4-139">Selecione **configurações** de saudação à esquerda o painel e clique em **TOKENS de autorização** toosee Olá tokens primários e secundários.</span><span class="sxs-lookup"><span data-stu-id="982e4-139">Select **Settings** from hello left pane and click **AUTHORIZATION TOKENS** toosee hello primary and secondary tokens.</span></span>  <span data-ttu-id="982e4-140">Embora Olá primário ou tokens de autorização secundário Olá podem ser usados no trecho de código Olá, é recomendável que proprietários de compartilham somente tokens de autorização secundário hello.</span><span class="sxs-lookup"><span data-stu-id="982e4-140">Although either hello primary or hello secondary authorization tokens can be used in hello code snippet, it is recommended that owners only share hello secondary authorization tokens.</span></span>

![Tokens de autorização](./media/machine-learning-python-data-access/ml-python-access-settings-tokens.png)

* <span data-ttu-id="982e4-142">Peça toorole toobe promovido do proprietário.</span><span class="sxs-lookup"><span data-stu-id="982e4-142">Ask toobe promoted toorole of owner.</span></span>  <span data-ttu-id="982e4-143">toodo isso, um proprietário atual do toofirst de necessidades de espaço de trabalho Olá removê-lo da área de trabalho de saudação e convidá-lo novamente tooit como proprietário.</span><span class="sxs-lookup"><span data-stu-id="982e4-143">toodo this, a current owner of hello workspace needs toofirst remove you from hello workspace then re-invite you tooit as an owner.</span></span>

<span data-ttu-id="982e4-144">Assim que os desenvolvedores tem obtido Olá id e a autorização de token, eles são espaço de trabalho do hello capaz de tooaccess usando Olá trecho de código, independentemente de sua função.</span><span class="sxs-lookup"><span data-stu-id="982e4-144">Once developers have obtained hello workspace id and authorization token, they are able tooaccess hello workspace using hello code snippet regardless of their role.</span></span>

<span data-ttu-id="982e4-145">Tokens de autorização são gerenciados no hello **TOKENS de autorização** página em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="982e4-145">Authorization tokens are managed on hello **AUTHORIZATION TOKENS** page under **SETTINGS**.</span></span> <span data-ttu-id="982e4-146">Você pode gerá-los novamente, mas esse procedimento revoga anterior token de acesso de toohello.</span><span class="sxs-lookup"><span data-stu-id="982e4-146">You can regenerate them, but this procedure revokes access toohello previous token.</span></span>

### <span data-ttu-id="982e4-147"><a name="accessingDatasets"></a>Conjuntos de dados de acesso de um aplicativo Python local</span><span class="sxs-lookup"><span data-stu-id="982e4-147"><a name="accessingDatasets"></a>Access datasets from a local Python application</span></span>
1. <span data-ttu-id="982e4-148">No estúdio de aprendizado de máquina, clique em **conjuntos de dados** na barra de navegação Olá Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="982e4-148">In Machine Learning Studio, click **DATASETS** in hello navigation bar on hello left.</span></span>
2. <span data-ttu-id="982e4-149">Selecione o conjunto de dados de saudação você gostaria que tooaccess.</span><span class="sxs-lookup"><span data-stu-id="982e4-149">Select hello dataset you would like tooaccess.</span></span> <span data-ttu-id="982e4-150">Você pode selecionar qualquer um dos conjuntos de dados Olá Olá **Meus conjuntos de dados** lista ou de saudação **exemplos** lista.</span><span class="sxs-lookup"><span data-stu-id="982e4-150">You can select any of hello datasets from hello **MY DATASETS** list or from hello **SAMPLES** list.</span></span>
3. <span data-ttu-id="982e4-151">Na barra de ferramentas do hello inferior, clique em **gerar código de acesso a dados**.</span><span class="sxs-lookup"><span data-stu-id="982e4-151">From hello bottom toolbar, click **Generate Data Access Code**.</span></span> <span data-ttu-id="982e4-152">Se dados saudação estão em um formato incompatível com a biblioteca de cliente do Python hello, esse botão será desabilitado.</span><span class="sxs-lookup"><span data-stu-id="982e4-152">If hello data is in a format incompatible with hello Python client library, this button is disabled.</span></span>
   
    ![CONJUNTOS DE DADOS][datasets]
4. <span data-ttu-id="982e4-154">Selecione o trecho de código Olá da janela de saudação que aparece e copiá-lo na área de transferência tooyour.</span><span class="sxs-lookup"><span data-stu-id="982e4-154">Select hello code snippet from hello window that appears and copy it tooyour clipboard.</span></span>
   
    ![Código de acesso][dataset-access-code]
5. <span data-ttu-id="982e4-156">Cole o código de saudação no bloco de anotações de saudação do seu aplicativo local do Python.</span><span class="sxs-lookup"><span data-stu-id="982e4-156">Paste hello code into hello notebook of your local Python application.</span></span>
   
    ![Bloco de notas][ipython-dataset]

## <span data-ttu-id="982e4-158">
            <a name="accessingIntermediateDatasets">
            </a>Acesse os conjuntos intermediários de testes de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="982e4-158"><a name="accessingIntermediateDatasets"></a>Access intermediate datasets from Machine Learning experiments</span></span>
<span data-ttu-id="982e4-159">Após a execução de um experimento no hello estúdio de aprendizado de máquina, é possível tooaccess Olá intermediário conjuntos de dados de saudação nós de saída dos módulos.</span><span class="sxs-lookup"><span data-stu-id="982e4-159">After an experiment is run in hello Machine Learning Studio, it is possible tooaccess hello intermediate datasets from hello output nodes of modules.</span></span> <span data-ttu-id="982e4-160">Os conjuntos de dados intermediários são dados que foram criados e usados para etapas intermediárias quando uma ferramenta de modelo tiver sido executada.</span><span class="sxs-lookup"><span data-stu-id="982e4-160">Intermediate datasets are data that has been created and used for intermediate steps when a model tool has been run.</span></span>

<span data-ttu-id="982e4-161">Conjuntos de dados intermediários podem ser acessados como formato de dados de saudação é compatível com a biblioteca de cliente do Python hello.</span><span class="sxs-lookup"><span data-stu-id="982e4-161">Intermediate datasets can be accessed as long as hello data format is compatible with hello Python client library.</span></span>

<span data-ttu-id="982e4-162">Olá formatos a seguir são suportados (constantes para eles estão em Olá `azureml.DataTypeIds` classe):</span><span class="sxs-lookup"><span data-stu-id="982e4-162">hello following formats are supported (constants for these are in hello `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="982e4-163">Texto sem formatação</span><span class="sxs-lookup"><span data-stu-id="982e4-163">PlainText</span></span>
* <span data-ttu-id="982e4-164">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="982e4-164">GenericCSV</span></span>
* <span data-ttu-id="982e4-165">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="982e4-165">GenericTSV</span></span>
* <span data-ttu-id="982e4-166">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="982e4-166">GenericCSVNoHeader</span></span>
* <span data-ttu-id="982e4-167">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="982e4-167">GenericTSVNoHeader</span></span>

<span data-ttu-id="982e4-168">Você pode determinar o formato de saudação focalizando um nó de saída do módulo.</span><span class="sxs-lookup"><span data-stu-id="982e4-168">You can determine hello format by hovering over a module output node.</span></span> <span data-ttu-id="982e4-169">Ele é exibido junto com o nome de nó hello, em uma dica de ferramenta.</span><span class="sxs-lookup"><span data-stu-id="982e4-169">It is displayed along with hello node name, in a tooltip.</span></span>

<span data-ttu-id="982e4-170">Alguns dos módulos de saudação, como Olá [divisão] [ split] módulo, o formato da saída tooa chamado `Dataset`, que não é suportado pela biblioteca de cliente do Python hello.</span><span class="sxs-lookup"><span data-stu-id="982e4-170">Some of hello modules, such as hello [Split][split] module, output tooa format named `Dataset`, which is not supported by hello Python client library.</span></span>

![Formato de conjunto de dados][dataset-format]

<span data-ttu-id="982e4-172">Você precisa toouse um módulo de conversão, como [converter tooCSV][convert-to-csv], tooget uma saída em um formato com suporte.</span><span class="sxs-lookup"><span data-stu-id="982e4-172">You need toouse a conversion module, such as [Convert tooCSV][convert-to-csv], tooget an output into a supported format.</span></span>

![Formato de GenericCSV][csv-format]

<span data-ttu-id="982e4-174">Olá, etapas a seguir mostram um exemplo que cria um experimento, executa e acessa o conjunto de dados intermediário hello.</span><span class="sxs-lookup"><span data-stu-id="982e4-174">hello following steps show an example that creates an experiment, runs it and accesses hello intermediate dataset.</span></span>

1. <span data-ttu-id="982e4-175">Criar um novo teste.</span><span class="sxs-lookup"><span data-stu-id="982e4-175">Create a new experiment.</span></span>
2. <span data-ttu-id="982e4-176">Inserir um módulo **Conjunto de dados de Classificação Binária de Renda de Censo de Adulto** .</span><span class="sxs-lookup"><span data-stu-id="982e4-176">Insert an **Adult Census Income Binary Classification dataset** module.</span></span>
3. <span data-ttu-id="982e4-177">Inserir uma [divisão] [ split] módulo e conecte-se a sua saída de módulo de conjunto de dados de entrada toohello.</span><span class="sxs-lookup"><span data-stu-id="982e4-177">Insert a [Split][split] module, and connect its input toohello dataset module output.</span></span>
4. <span data-ttu-id="982e4-178">Inserir uma [converter tooCSV] [ convert-to-csv] módulo e conecte-se a sua entrada tooone de saudação [divisão] [ split] saídas do módulo.</span><span class="sxs-lookup"><span data-stu-id="982e4-178">Insert a [Convert tooCSV][convert-to-csv] module and connect its input tooone of hello [Split][split] module outputs.</span></span>
5. <span data-ttu-id="982e4-179">Salvar experimento hello, executá-lo e aguardar toofinish em execução.</span><span class="sxs-lookup"><span data-stu-id="982e4-179">Save hello experiment, run it, and wait for it toofinish running.</span></span>
6. <span data-ttu-id="982e4-180">Clique no nó Olá saída em Olá [converter tooCSV] [ convert-to-csv] módulo.</span><span class="sxs-lookup"><span data-stu-id="982e4-180">Click hello output node on hello [Convert tooCSV][convert-to-csv] module.</span></span>
7. <span data-ttu-id="982e4-181">Quando o menu de contexto Olá for exibida, selecione **gerar código de acesso a dados**.</span><span class="sxs-lookup"><span data-stu-id="982e4-181">When hello context menu appears, select **Generate Data Access Code**.</span></span>
   
    ![Menu de contexto][experiment]
8. <span data-ttu-id="982e4-183">Selecione o trecho de código hello e copiá-lo na área de transferência tooyour da janela de saudação que aparece.</span><span class="sxs-lookup"><span data-stu-id="982e4-183">Select hello code snippet and copy it tooyour clipboard from hello window that appears.</span></span>
   
    ![Código de acesso][intermediate-dataset-access-code]
9. <span data-ttu-id="982e4-185">Cole o código de saudação do bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="982e4-185">Paste hello code in your notebook.</span></span>
   
    ![Bloco de notas][ipython-intermediate-dataset]
10. <span data-ttu-id="982e4-187">Você pode visualizar dados hello usando matplotlib.</span><span class="sxs-lookup"><span data-stu-id="982e4-187">You can visualize hello data using matplotlib.</span></span> <span data-ttu-id="982e4-188">Isso exibe um histograma para a coluna de idade hello:</span><span class="sxs-lookup"><span data-stu-id="982e4-188">This displays in a histogram for hello age column:</span></span>
    
    ![Histograma][ipython-histogram]

## <span data-ttu-id="982e4-190"><a name="clientApis"></a>Saudação de uso tooaccess de biblioteca de cliente do Python de aprendizado de máquina, ler, criar e gerenciar conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="982e4-190"><a name="clientApis"></a>Use hello Machine Learning Python client library tooaccess, read, create, and manage datasets</span></span>
### <a name="workspace"></a><span data-ttu-id="982e4-191">Espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="982e4-191">Workspace</span></span>
<span data-ttu-id="982e4-192">espaço de trabalho de saudação é o ponto de entrada de saudação para a biblioteca de cliente do Python hello.</span><span class="sxs-lookup"><span data-stu-id="982e4-192">hello workspace is hello entry point for hello Python client library.</span></span> <span data-ttu-id="982e4-193">Fornecer Olá `Workspace` uma instância de classe com o espaço de trabalho id e a autorização toocreate token:</span><span class="sxs-lookup"><span data-stu-id="982e4-193">Provide hello `Workspace` class with your workspace id and authorization token toocreate an instance:</span></span>

    ws = Workspace(workspace_id='4c29e1adeba2e5a7cbeb0e4f4adfb4df',
                   authorization_token='f4f3ade2c6aefdb1afb043cd8bcf3daf')


### <a name="enumerate-datasets"></a><span data-ttu-id="982e4-194">Enumerar conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="982e4-194">Enumerate datasets</span></span>
<span data-ttu-id="982e4-195">tooenumerate todos os conjuntos de dados em um determinado espaço de trabalho:</span><span class="sxs-lookup"><span data-stu-id="982e4-195">tooenumerate all datasets in a given workspace:</span></span>

    for ds in ws.datasets:
        print(ds.name)

<span data-ttu-id="982e4-196">tooenumerate Olá apenas criados pelo usuário conjuntos de dados:</span><span class="sxs-lookup"><span data-stu-id="982e4-196">tooenumerate just hello user-created datasets:</span></span>

    for ds in ws.user_datasets:
        print(ds.name)

<span data-ttu-id="982e4-197">conjuntos de dados de tooenumerate Olá apenas exemplo:</span><span class="sxs-lookup"><span data-stu-id="982e4-197">tooenumerate just hello example datasets:</span></span>

    for ds in ws.example_datasets:
        print(ds.name)

<span data-ttu-id="982e4-198">Você pode acessar um conjunto de dados por nome (que diferencia maiúsculas de minúsculas):</span><span class="sxs-lookup"><span data-stu-id="982e4-198">You can access a dataset by name (which is case-sensitive):</span></span>

    ds = ws.datasets['my dataset name']

<span data-ttu-id="982e4-199">Ou você pode acessá-lo pelo índice:</span><span class="sxs-lookup"><span data-stu-id="982e4-199">Or you can access it by index:</span></span>

    ds = ws.datasets[0]


### <a name="metadata"></a><span data-ttu-id="982e4-200">Metadados</span><span class="sxs-lookup"><span data-stu-id="982e4-200">Metadata</span></span>
<span data-ttu-id="982e4-201">Conjuntos de dados contêm metadados, adição toocontent.</span><span class="sxs-lookup"><span data-stu-id="982e4-201">Datasets have metadata, in addition toocontent.</span></span> <span data-ttu-id="982e4-202">(Conjuntos de dados intermediários são uma regra de exceção de toothis e não tem nenhum metadado.)</span><span class="sxs-lookup"><span data-stu-id="982e4-202">(Intermediate datasets are an exception toothis rule and do not have any metadata.)</span></span>

<span data-ttu-id="982e4-203">Alguns valores de metadados são atribuídos pelo usuário Olá no momento da criação:</span><span class="sxs-lookup"><span data-stu-id="982e4-203">Some metadata values are assigned by hello user at creation time:</span></span>

    print(ds.name)
    print(ds.description)
    print(ds.family_id)
    print(ds.data_type_id)

<span data-ttu-id="982e4-204">Outros são valores atribuídos pelo Azure ML:</span><span class="sxs-lookup"><span data-stu-id="982e4-204">Others are values assigned by Azure ML:</span></span>

    print(ds.id)
    print(ds.created_date)
    print(ds.size)

<span data-ttu-id="982e4-205">Consulte Olá `SourceDataset` classe para mais em Olá os metadados disponíveis.</span><span class="sxs-lookup"><span data-stu-id="982e4-205">See hello `SourceDataset` class for more on hello available metadata.</span></span>

### <a name="read-contents"></a><span data-ttu-id="982e4-206">Ler conteúdo</span><span class="sxs-lookup"><span data-stu-id="982e4-206">Read contents</span></span>
<span data-ttu-id="982e4-207">trechos de código Olá fornecidos pelo estúdio de aprendizado de máquina automaticamente baixar e desserializar um objeto de Pandas DataFrame de tooa Olá conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="982e4-207">hello code snippets provided by Machine Learning Studio automatically download and deserialize hello dataset tooa Pandas DataFrame object.</span></span> <span data-ttu-id="982e4-208">Isso é feito com hello `to_dataframe` método:</span><span class="sxs-lookup"><span data-stu-id="982e4-208">This is done with hello `to_dataframe` method:</span></span>

    frame = ds.to_dataframe()

<span data-ttu-id="982e4-209">Se você preferir dados brutos do toodownload hello e executar a desserialização de saudação, que é uma opção.</span><span class="sxs-lookup"><span data-stu-id="982e4-209">If you prefer toodownload hello raw data, and perform hello deserialization yourself, that is an option.</span></span> <span data-ttu-id="982e4-210">No momento de hello, isso é Olá única opção para formatos como 'ARFF', não é possível desserializar a biblioteca de cliente do Python que hello.</span><span class="sxs-lookup"><span data-stu-id="982e4-210">At hello moment, this is hello only option for formats such as 'ARFF', which hello Python client library cannot deserialize.</span></span>

<span data-ttu-id="982e4-211">conteúdo de saudação tooread como texto:</span><span class="sxs-lookup"><span data-stu-id="982e4-211">tooread hello contents as text:</span></span>

    text_data = ds.read_as_text()

<span data-ttu-id="982e4-212">conteúdo de saudação tooread como binários:</span><span class="sxs-lookup"><span data-stu-id="982e4-212">tooread hello contents as binary:</span></span>

    binary_data = ds.read_as_binary()

<span data-ttu-id="982e4-213">Você também pode abrir um conteúdo toohello:</span><span class="sxs-lookup"><span data-stu-id="982e4-213">You can also just open a stream toohello contents:</span></span>

    with ds.open() as file:
        binary_data_chunk = file.read(1000)


### <a name="create-a-new-dataset"></a><span data-ttu-id="982e4-214">Criar um novo conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="982e4-214">Create a new dataset</span></span>
<span data-ttu-id="982e4-215">biblioteca de cliente do Python Olá permite tooupload conjuntos de dados em seu programa de Python.</span><span class="sxs-lookup"><span data-stu-id="982e4-215">hello Python client library allows you tooupload datasets from your Python program.</span></span> <span data-ttu-id="982e4-216">Esses conjuntos de dados ficarão disponíveis para uso em seu espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="982e4-216">These datasets are then available for use in your workspace.</span></span>

<span data-ttu-id="982e4-217">Se você tiver dados em um DataFrame Pandas, use Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="982e4-217">If you have your data in a Pandas DataFrame, use hello following code:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_dataframe(
        dataframe=frame,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="982e4-218">Se os seus dados já estiverem serializados, você pode usar:</span><span class="sxs-lookup"><span data-stu-id="982e4-218">If your data is already serialized, you can use:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_raw_data(
        raw_data=raw_data,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="982e4-219">biblioteca de cliente do Python Hello é capaz de tooserialize uma DataFrame de Pandas toohello a seguir formata (constantes para eles estão em Olá `azureml.DataTypeIds` classe):</span><span class="sxs-lookup"><span data-stu-id="982e4-219">hello Python client library is able tooserialize a Pandas DataFrame toohello following formats (constants for these are in hello `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="982e4-220">Texto sem formatação</span><span class="sxs-lookup"><span data-stu-id="982e4-220">PlainText</span></span>
* <span data-ttu-id="982e4-221">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="982e4-221">GenericCSV</span></span>
* <span data-ttu-id="982e4-222">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="982e4-222">GenericTSV</span></span>
* <span data-ttu-id="982e4-223">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="982e4-223">GenericCSVNoHeader</span></span>
* <span data-ttu-id="982e4-224">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="982e4-224">GenericTSVNoHeader</span></span>

### <a name="update-an-existing-dataset"></a><span data-ttu-id="982e4-225">Atualizar um conjunto de dados existente</span><span class="sxs-lookup"><span data-stu-id="982e4-225">Update an existing dataset</span></span>
<span data-ttu-id="982e4-226">Se você tentar tooupload um novo conjunto de dados com um nome que corresponda a um conjunto de dados existente, você deve obter um erro de conflito.</span><span class="sxs-lookup"><span data-stu-id="982e4-226">If you try tooupload a new dataset with a name that matches an existing dataset, you should get a conflict error.</span></span>

<span data-ttu-id="982e4-227">tooupdate um conjunto de dados existente, você precisa primeiro tooget um conjunto de dados referência toohello existente:</span><span class="sxs-lookup"><span data-stu-id="982e4-227">tooupdate an existing dataset, you first need tooget a reference toohello existing dataset:</span></span>

    dataset = ws.datasets['existing dataset']

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="982e4-228">Em seguida, use `update_from_dataframe` tooserialize e substituir conteúdo Olá Olá conjunto de dados no Azure:</span><span class="sxs-lookup"><span data-stu-id="982e4-228">Then use `update_from_dataframe` tooserialize and replace hello contents of hello dataset on Azure:</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(frame2)

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="982e4-229">Se você quiser tooserialize Olá dados tooa outro formato, especifique um valor para Olá opcional `data_type_id` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="982e4-229">If you want tooserialize hello data tooa different format, specify a value for hello optional `data_type_id` parameter.</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        data_type_id=DataTypeIds.GenericTSV,
    )

    print(dataset.data_type_id) # 'GenericTSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="982e4-230">Opcionalmente, você pode definir uma nova descrição especificando um valor para Olá `description` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="982e4-230">You can optionally set a new description by specifying a value for hello `description` parameter.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toofeb 2015'

<span data-ttu-id="982e4-231">Opcionalmente, você pode definir um novo nome especificando um valor para Olá `name` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="982e4-231">You can optionally set a new name by specifying a value for hello `name` parameter.</span></span> <span data-ttu-id="982e4-232">De agora em diante, você vai recuperar Olá dataset usando Olá nome novo.</span><span class="sxs-lookup"><span data-stu-id="982e4-232">From now on, you'll retrieve hello dataset using hello new name only.</span></span> <span data-ttu-id="982e4-233">saudação de código a seguir atualiza a descrição, nome e os dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="982e4-233">hello following code updates hello data, name and description.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        name='existing dataset v2',
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id)                    # 'GenericCSV'
    print(dataset.name)                            # 'existing dataset v2'
    print(dataset.description)                     # 'data up toofeb 2015'

    print(ws.datasets['existing dataset v2'].name) # 'existing dataset v2'
    print(ws.datasets['existing dataset'].name)    # IndexError

<span data-ttu-id="982e4-234">Olá `data_type_id`, `name` e `description` parâmetros são opcionais e o valor anterior tootheir padrão.</span><span class="sxs-lookup"><span data-stu-id="982e4-234">hello `data_type_id`, `name` and `description` parameters are optional and default tootheir previous value.</span></span> <span data-ttu-id="982e4-235">Olá `dataframe` parâmetro sempre é necessário.</span><span class="sxs-lookup"><span data-stu-id="982e4-235">hello `dataframe` parameter is always required.</span></span>

<span data-ttu-id="982e4-236">Se os seus dados já estiverem serializados, use `update_from_raw_data` em vez de `update_from_dataframe`.</span><span class="sxs-lookup"><span data-stu-id="982e4-236">If your data is already serialized, use `update_from_raw_data` instead of `update_from_dataframe`.</span></span> <span data-ttu-id="982e4-237">Se você simplesmente passar `raw_data` em vez de `dataframe`, ele funcionará da mesma forma.</span><span class="sxs-lookup"><span data-stu-id="982e4-237">If you just pass in `raw_data` instead of  `dataframe`, it works in a similar way.</span></span>

<!-- Images -->
[security]:./media/machine-learning-python-data-access/security.png
[dataset-format]:./media/machine-learning-python-data-access/dataset-format.png
[csv-format]:./media/machine-learning-python-data-access/csv-format.png
[datasets]:./media/machine-learning-python-data-access/datasets.png
[dataset-access-code]:./media/machine-learning-python-data-access/dataset-access-code.png
[ipython-dataset]:./media/machine-learning-python-data-access/ipython-dataset.png
[experiment]:./media/machine-learning-python-data-access/experiment.png
[intermediate-dataset-access-code]:./media/machine-learning-python-data-access/intermediate-dataset-access-code.png
[ipython-intermediate-dataset]:./media/machine-learning-python-data-access/ipython-intermediate-dataset.png
[ipython-histogram]:./media/machine-learning-python-data-access/ipython-histogram.png


<!-- Module References -->
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/

