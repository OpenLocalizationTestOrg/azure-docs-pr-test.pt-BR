---
title: aaaLearn como toomanage AzureML web services usando o gerenciamento de API | Microsoft Docs
description: Um guia mostrando como toomanage AzureML web services usando o gerenciamento de API.
keywords: "aprendizado de máquina, gerenciamento de api"
services: machine-learning
documentationcenter: 
author: roalexan
manager: jhubbard
editor: 
ms.assetid: 05150ae1-5b6a-4d25-ac67-fb2f24a68e8d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/19/2017
ms.author: roalexan
ms.openlocfilehash: 6e764fbfd71be6cc908a1c8d3d8889969fc651a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-how-toomanage-azureml-web-services-using-api-management"></a>Saiba como toomanage AzureML web services usando o gerenciamento de API
## <a name="overview"></a>Visão geral
Este guia mostra como tooquickly começar a usar o gerenciamento de API toomanage serviços da web do AzureML.

## <a name="what-is-azure-api-management"></a>O que é o Gerenciamento de API do Azure?
O Gerenciamento de API do Azure é um serviço do Azure que permite que você gerencie seus pontos de extremidade da API REST, definindo o acesso do usuário, a limitação de uso e o monitoramento por painel. Clique em [aqui](https://azure.microsoft.com/services/api-management/) para obter detalhes sobre o Gerenciamento de API do Azure. Clique em [aqui](../api-management/api-management-get-started.md) para um guia como tooget Introdução ao gerenciamento de API do Azure. Essa outra guia, na qual este guia se baseia, aborda mais tópicos, incluindo configurações de notificação, faixa de preços, manipulação de resposta, autenticação do usuário, criação de produtos, assinaturas de desenvolvedor e dashboarding de uso.

## <a name="what-is-azureml"></a>O que é o AzureML?
AzureML é um serviço do Azure para o aprendizado de máquina que permite construir tooeasily, implantar e compartilhar soluções de análise avançada. Clique em [aqui](https://azure.microsoft.com/services/machine-learning/) para obter detalhes sobre AzureML.

## <a name="prerequisites"></a>Pré-requisitos
toocomplete neste guia, você precisa:

* Uma conta do Azure. Se você não tiver uma conta do Azure, clique em [aqui](https://azure.microsoft.com/pricing/free-trial/) para obter detalhes sobre como toocreate uma conta de avaliação gratuita.
* Uma conta do AzureML. Se você não tiver uma conta do AzureML, clique em [aqui](https://studio.azureml.net/) para obter detalhes sobre como toocreate uma conta de avaliação gratuita.
* espaço de trabalho Hello, serviço e api_key de um experimento AzureML implantado como um serviço web. Clique em [aqui](machine-learning-create-experiment.md) para obter detalhes sobre como toocreate uma AzureML experiências. Clique em [aqui](machine-learning-publish-a-machine-learning-web-service.md) para obter detalhes sobre como toodeploy uma AzureML experimentar como um serviço web. Como alternativa, o Apêndice A tem instruções sobre como toocreate e teste uma simple AzureML experimentar e implantação-lo como um serviço web.

## <a name="create-an-api-management-instance"></a>Criar uma instância de Gerenciamento de API
Abaixo estão as etapas de Olá para usar o gerenciamento de API toomanage seu serviço de web do AzureML. Primeiro, crie uma instância de serviço. Faça logon no toohello [Portal clássico](https://manage.windowsazure.com/) e clique em **novo** > **serviços de aplicativos** > **gerenciamento de API**  >  **Criar**.

![create-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

Especifique uma **URL**exclusiva. Este guia usa **demoazureml** – você precisará toochoose algo diferente. Escolha a saudação desejada **assinatura** e **região** para sua instância de serviço. Depois de fazer suas seleções, clique no botão Avançar hello.

![create-service-1](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

Especifique um valor para Olá **nome da organização**. Este guia usa **demoazureml** – você precisará toochoose algo diferente. Insira seu endereço de email no hello **email do administrador** campo. Este endereço de email é usado para notificações do sistema de gerenciamento de API de saudação.

![create-service-2](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

Clique em toocreate de caixa de seleção Olá sua instância de serviço. *Ocupe toothirty minutos para um novo toobe de serviço criada*.

## <a name="create-hello-api"></a>Criar hello API
Depois de criar a instância do serviço hello, Olá próxima etapa é toocreate Olá API. Uma API consiste em um conjunto de operações que podem ser iniciadas a partir de uma aplicativo cliente. Operações de API são serviços da web de tooexisting por proxy. Este guia cria APIs que toohello proxy existente AzureML RRS e BES serviços da web.

APIs são criados e configurados da saudação API portal do publicador, que pode é acessada por meio de saudação Portal clássico do Azure. tooreach Olá selecione portal do publicador a sua instância de serviço.

![select-service-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

Clique em **gerenciar** em hello Portal clássico do Azure para seu serviço de gerenciamento de API.

![manage-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

Clique em **APIs** de saudação **gerenciamento de API** menu saudação à esquerda e clique **adicionar API**.

![api-management-menu](./media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

Tipo **API de demonstração do AzureML** como Olá **nome de API da Web**. Tipo **https://ussouthcentral.services.azureml.net** como Olá **URL do serviço Web**. Tipo **azureml demonstração** como Olá **sufixo de URL da API da Web**. Verificar **HTTPS** como Olá **URL da API da Web** esquema. Selecione **Iniciador** como **Produtos**. Quando terminar, clique em **salvar** toocreate Olá API.

![add-new-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-hello-operations"></a>Adicionar operações Olá
Clique em **Adicionar operação** tooadd operações toothis API.

![add-operation](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

Olá **nova operação** janela será exibida e Olá **assinatura** guia será selecionada por padrão.

## <a name="add-rrs-operation"></a>Adicionar operação RRS
Primeiro, crie uma operação para Olá serviço AzureML RRS. Selecione **POST** como Olá **verbo HTTP**. Tipo **/services/ /workspaces/ {espaço de trabalho} {serviço} / executar? api-version = {apiversion} & detalhes = {detalhes}** como Olá **modelo de URL**. Tipo **RRS executar** como Olá **nome de exibição**.

![add-rrs-operation-signature](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

Clique em **respostas** > **adicionar** em Olá esquerdo e selecione **200 Okey**. Clique em **salvar** toosave esta operação.

![add-rrs-operation-response](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a>Adicionar operações BES
Capturas de tela não estão incluídas para Olá operações BES conforme forem toothose muito semelhante para a adição de operação de RRS hello.

### <a name="submit-but-not-start-a-batch-execution-job"></a>Enviar (mas não iniciar) um trabalho de execução em lotes
Clique em **Adicionar operação** tooadd Olá BES AzureML operação toohello API. Selecione **POST** para Olá **verbo HTTP**. Tipo **/services/ /workspaces/ {espaço de trabalho} {serviço} / trabalhos? api-version = {apiversion}** para Olá **modelo de URL**. Tipo **BES enviar** para Olá **nome de exibição**. Clique em **respostas** > **adicionar** em Olá esquerdo e selecione **200 Okey**. Clique em **salvar** toosave esta operação.

### <a name="start-a-batch-execution-job"></a>Iniciar um trabalho de execução em lotes
Clique em **Adicionar operação** tooadd Olá BES AzureML operação toohello API. Selecione **POST** para Olá **verbo HTTP**. Tipo **/workspaces/ {espaço de trabalho} /services/ {serviço} /jobs/ {jobid} / iniciar? api-version = {apiversion}** para Olá **modelo de URL**. Tipo **BES iniciar** para Olá **nome de exibição**. Clique em **respostas** > **adicionar** em Olá esquerdo e selecione **200 Okey**. Clique em **salvar** toosave esta operação.

### <a name="get-hello-status-or-result-of-a-batch-execution-job"></a>Obter status de saudação ou resultado de um trabalho de execução de lote
Clique em **Adicionar operação** tooadd Olá BES AzureML operação toohello API. Selecione **obter** para Olá **verbo HTTP**. Tipo **/workspaces/ {espaço de trabalho} /services/ {serviço} /jobs/ {jobid}? api-version = {apiversion}** para Olá **modelo de URL**. Tipo **BES Status** para Olá **nome de exibição**. Clique em **respostas** > **adicionar** em Olá esquerdo e selecione **200 Okey**. Clique em **salvar** toosave esta operação.

### <a name="delete-a-batch-execution-job"></a>Excluir um trabalho de execução em lote
Clique em **Adicionar operação** tooadd Olá BES AzureML operação toohello API. Selecione **excluir** para Olá **verbo HTTP**. Tipo **/workspaces/ {espaço de trabalho} /services/ {serviço} /jobs/ {jobid}? api-version = {apiversion}** para Olá **modelo de URL**. Tipo **BES excluir** para Olá **nome de exibição**. Clique em **respostas** > **adicionar** em Olá esquerdo e selecione **200 Okey**. Clique em **salvar** toosave esta operação.

## <a name="call-an-operation-from-hello-developer-portal"></a>Chamar uma operação de saudação Portal do desenvolvedor
Operações podem ser chamadas diretamente no portal do desenvolvedor hello, que fornece uma maneira conveniente de tooview e testar as operações de saudação de uma API. Nesta etapa guia você chamará Olá **RRS executar** método foi adicionado toohello **AzureML demonstração API**. Clique em **portal do desenvolvedor** do menu de saudação à saudação parte superior direita da saudação Portal clássico.

![developer-portal](./media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

Clique em **APIs** no menu superior hello e clique **AzureML demonstração API** toosee operações de saudação disponíveis.

![demoazureml-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

Selecione **RRS executar** para operação de saudação. Clique em **Experimentar**.

![avaliar](./media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

Para parâmetros de solicitação, digite sua **espaço de trabalho**, **service**, **2.0** para Olá **apiversion**, e **true**para Olá **detalhes**. Você pode encontrar o **espaço de trabalho** e **service** no painel de serviço web do hello AzureML (consulte **testar Olá web serviço** no Apêndice A).

Para cabeçalhos Request, clique em **Adicionar cabeçalho** e digite **Content-Type** e **application/json**; em seguida, clique em **Adicionar cabeçalho** e digite **Authorization** e **Bearer<YOUR AZUREML SERVICE API-KEY>**. Você pode encontrar o **chave api** no painel de serviço web do hello AzureML (consulte **testar Olá web serviço** no Apêndice A).

Tipo **{"Entradas": {"Entrada1": {"ColumnNames": ["Col2"], "valores": [["Este é um bom dia"]]}}, "GlobalParameters": {}}** para o corpo da solicitação hello.

![azureml-demo-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

Clique em **Enviar**.

![Enviar](./media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

Depois que uma operação é invocada, portal do desenvolvedor Olá exibe Olá **URL solicitada** do serviço de back-end hello, Olá **status da resposta**, Olá **cabeçalhos de resposta**, e qualquer **conteúdo de resposta**.

![response-status](./media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a>Apêndice A - criando e testando um serviço Web do AzureML simples
### <a name="creating-hello-experiment"></a>Criando experimento Olá
Abaixo estão as etapas de saudação para criar uma experiência simples do AzureML e implantá-lo como um serviço web. Olá leva de serviço da web como uma coluna de texto arbitrário de entrada e retorna um conjunto de recursos representado como números inteiros. Por exemplo:

| Texto | Texto marcado com sustenido |
| --- | --- |
| Este é um bom dia |1 1 2 2 0 2 0 1 |

Primeiro, usando um navegador de sua escolha, navegue até: [https://studio.azureml.net/](https://studio.azureml.net/) e insira sua toolog de credenciais no. Em seguida, crie um novo teste em branco.

![search-experiment-templates](./media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

Renomeie-muito**SimpleFeatureHashingExperiment**. Expanda **Conjuntos de dados salvos** e arraste **Resenhas de livros da Amazon** para o teste.

![simple-feature-hashing-experiment](./media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

Expanda **Transformação de Dados** e **Manipulação** e arraste **Selecionar Colunas do Conjunto de Dados** para o teste. Conecte-se **revisões de livros da Amazon** muito**selecionar colunas no conjunto de dados**.

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

Clique em **Selecionar Colunas do Conjunto de Dados** e em **Iniciar seletor de colunas** e selecione **Col2**. Clique em tooapply de marca de seleção Olá essas alterações.

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

Expanda **análises de texto** e arraste **hash de recurso** no experimento hello. Conecte-se **selecionar colunas no conjunto de dados** muito**hash de recurso**.

![connect-project-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

Tipo **3** para Olá **bitsize de hash**. Isso criará 8 (23) colunas.

![hashing-bitsize](./media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

Neste ponto, convém tooclick **executar** tootest experimento de saudação.

![Executar](./media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a>Criar um serviço Web
Agora crie um serviço Web. Expanda **Serviço Web** e arraste **Entrada** para o teste. Conecte-se **entrada** muito**hash de recurso**. Também arraste **saída** para seu teste. Conecte-se **saída** muito**hash de recurso**.

![output-to-feature-hashing](./media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

Clique em **Publicar serviço Web**.

![publish-web-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

Clique em **Sim** toopublish experimento de saudação.

![yes-to-publish](./media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-hello-web-service"></a>Testar o serviço web de saudação
Um serviço Web AzureML consiste em RSS (serviço de solicitação/resposta) e pontos de extremidade BES (serviço de execução em lotes). RSS é para execução síncrona. BES é para execução do trabalho assíncrono. tootest de serviço web com fonte de Python de exemplo hello abaixo, você pode precisar toodownload e instalar hello Azure SDK para Python (consulte: [como tooinstall Python](../python-how-to-install.md)).

Você também precisará Olá **espaço de trabalho**, **service**, e **api_key** de sua experiência de fonte de exemplo hello abaixo. Você pode encontrar o espaço de trabalho de saudação e serviço clicando em **solicitação/resposta** ou **Batch Execution** para sua experiência no painel de serviço web hello.

![find-workspace-and-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

Você pode encontrar hello **api_key** clicando em sua experiência no painel de serviço web hello.

![find-api-key](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a>Testar ponto de extremidade RRS
##### <a name="test-button"></a>Botão de teste
Um ponto de extremidade maneira fácil tootest Olá RRS é tooclick **teste** no painel de serviço web hello.

![test](./media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

Digite **Este é um bom dia** para **col2**. Clique em marca de seleção de saudação.

![enter-data](./media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

Você verá algo semelhante a

![sample-output](./media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a>Exemplo de código
Outro tootest de maneira seus RRS é de código do cliente. Se você clicar em **solicitação/resposta** Olá painel e rolagem toohello inferior, você verá o código de exemplo para c#, Python e R. Você também verá sintaxe Olá Olá RRS solicitação, incluindo o URI de solicitação hello, cabeçalhos e corpo.

Este guia mostra um exemplo de trabalho do Python. Você precisará toomodify com hello **espaço de trabalho**, **service**, e **api_key** de sua experiência.

    import urllib2
    import json
    workspace = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE WORKSPACE ID>"
    service = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE SERVICE ID>"
    api_key = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE API KEY>"
    data = {
    "Inputs": {
        "input1": {
            "ColumnNames": ["Col2"],
            "Values": [ [ "This is a good day" ] ]
        },
    },
    "GlobalParameters": { }
    }
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace + "/services/" + service + "/execute?api-version=2.0&details=true"
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}
    body = str.encode(json.dumps(data))
    try:
        req = urllib2.Request(url, body, headers)
        response = urllib2.urlopen(req)
        result = response.read()
        print "result:" + result
            except urllib2.HTTPError, error:
        print("hello request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a>Testar ponto de extremidade BES
Clique em **execução em lote** em Olá painel e rolagem toohello inferior. Você verá o código de exemplo para c#, Python e R. Você também verá sintaxe Olá Olá BES solicitações toosubmit um trabalho, iniciar um trabalho, obter status de saudação ou os resultados de um trabalho e excluir um trabalho.

Este guia mostra um exemplo de trabalho do Python. Você precisa toomodify com hello **espaço de trabalho**, **service**, e **api_key** de sua experiência. Além disso, você precisa Olá toomodify **nome da conta de armazenamento**, **chave da conta de armazenamento**, e **nome do contêiner de armazenamento**. Por fim, você precisará de local de saudação toomodify de saudação **arquivo de entrada** e o local de saudação do hello **arquivo de saída**.

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH hello API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH hello LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH hello LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("hello request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading hello result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written toohello file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("hello results for " + outputName + " are available at hello following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "hello results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading hello input tooblob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded hello input tooblob storage"
    input_blob_path = "/" + storage_container_name + "/" + input_blob_name
    connection_string = "DefaultEndpointsProtocol=https;AccountName=" + storage_account_name + ";AccountKey=" + storage_account_key
    payload =  {
        "Input": {
            "ConnectionString": connection_string,
            "RelativeLocation": input_blob_path
        },
        "Outputs": {
            "output1": { "ConnectionString": connection_string, "RelativeLocation": "/" + storage_container_name + "/" + output_blob_name },
        },
        "GlobalParameters": {
        }
    }
        body = str.encode(json.dumps(payload))
    headers = { "Content-Type":"application/json", "Authorization":("Bearer " + api_key)}
    print("Submitting hello job...")
    # submit hello job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove hello enclosing double-quotes
    print("Job ID: " + job_id)
    # start hello job
    print("Starting hello job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking hello job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in hello follwing code
        req = urllib2.Request(url2, headers = { "Authorization":("Bearer " + api_key) })
        try:
            response = urllib2.urlopen(req)
        except urllib2.HTTPError, error:
            printHttpError(error)
            return
        result = json.loads(response.read())
        status = result["StatusCode"]
        print "status:" + status
        if (status == 0 or status == "NotStarted"):
            print("Job " + job_id + " not yet started...")
        elif (status == 1 or status == "Running"):
            print("Job " + job_id + " running...")
        elif (status == 2 or status == "Failed"):
            print("Job " + job_id + " failed!")
            print("Error details: " + result["Details"])
            break
        elif (status == 3 or status == "Cancelled"):
            print("Job " + job_id + " cancelled!")
            break
        elif (status == 4 or status == "Finished"):
            print("Job " + job_id + " finished!")
            processResults(result)
            break
        time.sleep(1) # wait one second
    return
    invokeBatchExecutionService()
