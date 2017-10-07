---
title: "aaaCreate, criar e implantar aplicativos lógicos no Visual Studio - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Crie projetos do Visual Studio para projetar, compilar e implantar Aplicativo Lógico do Azure."
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e484e5ce-77e9-4fa9-bcbe-f851b4eb42a6
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 2/14/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 5154cb05f9a48e9f0f2381a6953947217f7bb114
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="design-build-and-deploy-azure-logic-apps-in-visual-studio"></a>Criar, compilar e implantar Aplicativo Lógico do Azure no Visual Studio

Embora hello [portal do Azure](https://portal.azure.com/) oferece uma ótima maneira de você toocreate e gerenciar os aplicativos lógicos do Azure, você pode usar o Visual Studio para projetar, desenvolver e implantar seus aplicativos lógicos. Visual Studio fornece ferramentas avançadas como Olá Designer de lógica do aplicativo para você toocreate os aplicativos lógicos, configurar modelos de implantação e a automação e implantar o ambiente tooany. 

Saiba tooget iniciada com os aplicativos lógicos do Azure, [como toocreate seu primeiro aplicativo lógica no portal do Azure de saudação](logic-apps-create-a-logic-app.md).

## <a name="installation-steps"></a>Etapas de instalação

tooinstall e configurar as ferramentas do Visual Studio para aplicativos do Azure lógica, siga estas etapas.

### <a name="prerequisites"></a>Pré-requisitos

* [Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) ou Visual Studio 2015
* [SDK mais recente do Azure](https://azure.microsoft.com/downloads/) (2.9.1 ou superior)
* [PowerShell do Azure](https://github.com/Azure/azure-powershell#installation)
* Web toohello de acesso ao usar o designer incorporado Olá

### <a name="install-visual-studio-tools-for-azure-logic-apps"></a>Instalar ferramentas do Visual Studio para Aplicativos Lógicos do Azure

Depois de instalar os pré-requisitos de saudação:

1. Abra o Visual Studio. Em Olá **ferramentas** menu, selecione **extensões e atualizações**.
2. Expanda Olá **Online** categoria para que você pode pesquisar online.
3. Procure por **Aplicativos Lógicos** até encontrar as **Ferramentas de Aplicativos Lógicos do Azure para Visual Studio**.
4. toodownload e extensão de saudação de instalação, clique em **baixar**.
5. Reinicie o Visual Studio após a instalação.

> [!NOTE]
> Você também pode baixar [ferramentas de aplicativos de lógica do Azure para Visual Studio de 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) e hello [ferramentas de aplicativos de lógica do Azure para Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) diretamente do Visual Studio Marketplace de saudação.

Depois de concluir a instalação, você pode usar o projeto do grupo de recursos do Azure Olá com o Designer de lógica do aplicativo.

## <a name="create-your-project"></a>Criar seu projeto

1. Em Olá **arquivo** menu Ir muito**novo**e selecione **projeto**. Ou tooadd seu tooan projeto existente a solução, ir muito**adicionar**e selecione **novo projeto**.

    ![Menu Arquivo](./media/logic-apps-deploy-from-vs/filemenu.png)

2. Em Olá **novo projeto** janela, localizar **nuvem**e selecione **o grupo de recursos do Azure**. Nomeie seu projeto e clique em **OK**.

    ![Adicionar novo projeto](./media/logic-apps-deploy-from-vs/addnewproject.png)

3. Selecione Olá **aplicativo lógico** modelo, que cria um modelo de implantação de aplicativo em branco lógica de toouse. Após selecionar o modelo, clique em **OK**.

    ![Selecione o modelo Aplicativo Lógico](./media/logic-apps-deploy-from-vs/selectazuretemplate1.png)

    Você adicionou agora sua solução de tooyour de projeto de aplicativo de lógica. 
    No Gerenciador de soluções do hello, o arquivo de implantação deve aparecer.

    ![Arquivo de implantação](./media/logic-apps-deploy-from-vs/deployment.png)

## <a name="create-your-logic-app-with-logic-app-designer"></a>Criar seu aplicativo lógico com o Designer de Aplicativos Lógicos

Quando você tiver um projeto de grupo de recursos do Azure que contém um aplicativo lógico, você pode abrir Olá lógica de aplicativo Designer no Visual Studio toocreate o fluxo de trabalho. 

> [!NOTE]
> designer de saudação requer uma conexão de internet de consulta muito conectores para dados e propriedades disponíveis. Por exemplo, se você usar o conector do Dynamics CRM Online hello, designer de saudação consulta o CRM instância tooshow disponíveis e personalizados propriedades padrão.

1. Clique com o botão direito do mouse no arquivo `<template>.json` e selecione **Abrir com o Designer de Aplicativo Lógico**. (`Ctrl+L`)

2. Escolha a assinatura do Azure, grupo de recursos e local para seu modelo de implantação.

    > [!NOTE]
    > A criação de um aplicativo lógico cria recursos de Conexão da API que consultam propriedades durante o design. O Visual Studio usa essas conexões seu toocreate do grupo de recursos selecionado durante o tempo de design. tooview ou alterar quaisquer conexões de API, vá toohello portal do Azure e procurar **API conexões**.

    ![Seletor de assinatura](./media/logic-apps-deploy-from-vs/designer_picker.png)

    designer Olá usa definição Olá em Olá `<template>.json` arquivo para renderização.

4. Crie e projete seu aplicativo lógico. Seu modelo de implantação é atualizado com suas alterações.

    ![Designer de Aplicativo Lógico no Visual Studio](./media/logic-apps-deploy-from-vs/designer_in_vs.png)

O Visual Studio adiciona `Microsoft.Web/connections` muito o recurso de arquivo de recursos para todas as conexões toofunction precisa de seu aplicativo lógico. Essas propriedades de conexão podem ser definidas quando você implanta e gerenciadas depois de implantar no **API conexões** em Olá portal do Azure.

### <a name="switch-toojson-code-view"></a>Alternar o modo de exibição de código tooJSON

Olá tooshow representação JSON para seu aplicativo lógico, selecione Olá **visualização de código** guia na parte inferior de saudação do designer de saudação.

tooswitch novamente toohello completo de recursos JSON, clique com botão direito Olá `<template>.json` de arquivo e selecione **abrir**.

### <a name="add-references-for-dependent-resources-toovisual-studio-deployment-templates"></a>Adicionar referências para modelos de implantação recursos dependentes tooVisual Studio

Quando você deseja que sua lógica aplicativo tooreference os recursos dependentes, você pode usar [funções de modelo do Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) no seu modelo de implantação do aplicativo de lógica. Por exemplo, convém seu aplicativo de lógica tooreference uma conta de função do Azure ou de integração que você deseja toodeploy juntamente com seu aplicativo lógica. Siga estas diretrizes sobre como os parâmetros de toouse em seu modelo de implantação para que Olá lógica de aplicativo Designer renderiza corretamente. 

Você pode usar parâmetros do aplicativo lógico nesses tipos de gatilhos e ações:

*   Fluxo de trabalho filho
*   Aplicativo de funções
*   Chamada APIM
*   URL do tempo de execução da conexão de API
*   Caminho de conexão da API

E você pode utilizar funções de modelo, como parâmetros, variáveis, resourceId, concat, etc. Por exemplo, aqui está como você pode substituir Olá ID de recurso de função do Azure:

```
"parameters":{
    "functionName": {
        "type":"string",
        "minLength":1,
        "defaultValue":"<FunctionName>"
    }
},
```

E onde os parâmetros seriam utilizados:

```
"MyFunction": {
    "type": "Function",
    "inputs": {
        "body":{},
        "function":{
            "id":"[resourceid('Microsoft.Web/sites/functions','functionApp',parameters('functionName'))]"
        }
    },
    "runAfter":{}
}
```
Como outro exemplo, você pode parametrizar Olá operação de mensagem de envio do barramento de serviço:

```
"Send_message": {
    "type": "ApiConnection",
        "inputs": {
            "host": {
                "connection": {
                    "name": "@parameters('$connections')['servicebus']['connectionId']"
                }
            },
            "method": "post",
            "path": "[concat('/@{encodeURIComponent(''', parameters('queueuname'), ''')}/messages')]",
            "body": {
                "ContentData": "@{base64(triggerBody())}"
            },
            "queries": {
                "systemProperties": "None"
            }
        },
        "runAfter": {}
    }
```
> [!NOTE] 
> host.runtimeUrl é opcional e pode ser removido do seu modelo, se houver.
> 


> [!NOTE] 
> Para toowork do Designer de lógica do aplicativo hello quando você usar parâmetros, você deve fornecer valores padrão, por exemplo:
> 
> ```
> "parameters": {
>     "IntegrationAccount": {
>     "type":"string",
>     "minLength":1,
>     "defaultValue":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.Logic/integrationAccounts/<integrationAccountName>"
>     }
> },
> ```

### <a name="save-your-logic-app"></a>Salve seu aplicativo lógico

toosave seu aplicativo lógico a qualquer momento, vá muito**arquivo** > **salvar**. (`Ctrl+S`) 

Se seu aplicativo lógico tem erros quando você salvar seu aplicativo, eles aparecem no hello Visual Studio **saídas** janela.

## <a name="deploy-your-logic-app-from-visual-studio"></a>Implantar seu aplicativo lógico por meio do Visual Studio

Após configurar seu aplicativo, você pode implantar diretamente do Visual Studio em apenas algumas etapas. 

1. No Gerenciador de soluções, clique com o botão direito e vá muito**implantar** > **nova implantação...**

    ![Nova implantação](./media/logic-apps-deploy-from-vs/newdeployment.png)

2. Quando você for solicitado, entre tooyour assinatura do Azure. 

3. Agora você deve selecionar detalhes de Olá Olá para grupo de recursos onde você deseja toodeploy seu aplicativo lógico. Quando terminar, selecione **Implantar**.

    > [!NOTE]
    > Certifique-se de que você selecione o modelo correto hello e arquivo de parâmetros para o grupo de recursos de saudação. Por exemplo, se desejar que o ambiente de produção tooa toodeploy, escolha o arquivo de parâmetros de produção de hello.

    ![Implantar grupo tooresource](./media/logic-apps-deploy-from-vs/deploytoresourcegroup.png)

    status da implantação Olá aparece no hello **saída** janela. 
    Você pode ter tooselect **Azure provisionamento** em Olá **Mostrar saída de** lista.

    ![Saída Status da implantação](./media/logic-apps-deploy-from-vs/output.png)

Olá futura, você pode editar o aplicativo lógico no controle de origem e usar as novas versões do Visual Studio toodeploy.

> [!NOTE]
> Se você alterar a definição de saudação em Olá portal do Azure diretamente, essas alterações serão substituídas quando você implanta no Visual Studio próxima vez. 

## <a name="add-your-logic-app-tooan-existing-resource-group-project"></a>Adicionar projeto de grupo de recursos existente sua lógica aplicativo tooan

Se você tiver um projeto existente do grupo de recursos, você pode adicionar seu projeto de toothat aplicativo lógica na janela de estrutura de tópicos do JSON hello. Você também pode adicionar outro aplicativo lógico juntamente com o aplicativo hello criado anteriormente.

1. Olá abrir `<template>.json` arquivo.

2. Olá tooopen janela estrutura de tópicos de JSON, ir muito**exibição** > **outras janelas** > **JSON tópicos**.

3. tooadd um arquivo de modelo de toohello de recursos, clique em **adicionar recurso** na parte superior de saudação da janela de estrutura de JSON de saudação. Ou na janela de estrutura de tópicos do JSON hello, clique com botão direito **recursos**e selecione **adicionar novo recurso**.

    ![Janela Estrutura de tópicos JSON](./media/logic-apps-deploy-from-vs/jsonoutline.png)
    
4. Em Olá **adicionar recurso** caixa de diálogo, encontre e selecione **aplicativo lógico**. Nomeie seu aplicativo lógico e escolha **Adicionar**.

    ![Adicionar recurso](./media/logic-apps-deploy-from-vs/addresource.png)

## <a name="next-steps"></a>Próximas etapas

* [Gerenciar aplicativos lógicos com o Visual Studio Cloud Explorer](logic-apps-manage-from-vs.md)
* [Veja exemplos e cenários comuns](logic-apps-examples-and-scenarios.md)
* [Saiba como os processos de negócios de tooautomate com os aplicativos lógicos do Azure](http://channel9.msdn.com/Events/Build/2016/T694)
* [Saiba como toointegrate seus sistemas com os aplicativos lógicos do Azure](http://channel9.msdn.com/Events/Build/2016/P462)
