---
title: "modelos de implantação de aaaCreate para os aplicativos lógicos do Azure | Microsoft Docs"
description: "Criar modelos do Azure Resource Manager para implantação de aplicativos lógicos e gerenciamento de versão"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 85928ec6-d7cb-488e-926e-2e5db89508ee
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 2f09445f10a376a745d6acbba94ca29d5f79fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-templates-for-logic-apps-deployment-and-release-management"></a>Criar modelos para implantação de aplicativos lógicos e gerenciamento de versão

Depois que um aplicativo lógico foi criado, você poderá toocreate-lo como um modelo do Gerenciador de recursos do Azure.
Dessa forma, você pode implantar facilmente o ambiente de tooany aplicativo hello lógica ou grupo de recursos onde você pode precisar dela.
Para obter mais informações sobre modelos do Resource Manager, consulte [Criando modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) e [Implantando recursos usando modelos do Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="logic-app-deployment-template"></a>Modelo de implantação do aplicativo lógico

Um aplicativo lógico tem três componentes básicos:

* **Recursos de aplicativo lógica**: contém informações sobre preços do plano, o local e a definição de fluxo de trabalho de saudação.
* **Definição de fluxo de trabalho**: descreve as etapas do fluxo de trabalho e como mecanismo de aplicativos lógicos Olá deve executar o fluxo de trabalho Olá lógica do aplicativo.
É possível exibir essa definição na janela **Modo de Exibição de Código** do aplicativo lógico.
No recurso de aplicativo do hello lógica, você pode encontrar essa definição no hello `definition` propriedade.
* **Conexões**: refere-se a recursos de tooseparate que armazenam com segurança os metadados sobre todas as conexões conector, como uma cadeia de caracteres de conexão e um token de acesso.
No recurso de aplicativo de lógica de saudação, seu aplicativo lógico faz referência a esses recursos em Olá `parameters` seção.

É possível exibir todas essas partes de aplicativos lógicos existentes usando uma ferramenta como o [Gerenciador de Recursos do Azure](http://resources.azure.com).

toomake um modelo para um aplicativo do lógica toouse com implantações de grupos de recursos, você deve definir recursos hello e parametrizar conforme necessário.
Por exemplo, se você estiver implantando o ambiente de produção, teste e desenvolvimento tooa, provavelmente deseja toouse conexão diferentes cadeias de caracteres tooa SQL banco de dados em cada ambiente.
Ou, talvez você queira toodeploy em assinaturas diferentes ou grupos de recursos.  

## <a name="create-a-logic-app-deployment-template"></a>Criar um modelo de implantação do aplicativo lógico

toohave de maneira mais fácil de saudação um modelo de implantação de aplicativo válido lógica é toouse o [Visual Studio Tools para aplicativos lógicos](logic-apps-deploy-from-vs.md).
ferramentas do Visual Studio Olá geram um modelo de implantação válido que pode ser usado em qualquer assinatura ou local.

Algumas ferramentas podem ajudar você a criar um modelo de implantação de aplicativo lógico.
Você pode criar manualmente, ou seja, usando Olá recursos já discutidos aqui toocreate parâmetros conforme necessário.
Outra opção é toouse uma [criador do modelo de aplicativo de lógica](https://github.com/jeffhollan/LogicAppTemplateCreator) módulo do PowerShell. Esse módulo de código-fonte aberto primeiro avalia Olá lógica aplicativo e todas as conexões que está usando e, em seguida, gera os recursos de modelo com parâmetros de saudação necessários para a implantação.
Por exemplo, se você tiver um aplicativo de lógica que recebe uma mensagem de uma fila do barramento de serviço do Azure e adiciona o banco de dados do SQL Azure data tooan, ferramenta Olá preserva toda a lógica de orquestração hello e parametriza hello SQL e cadeias de caracteres de conexão de barramento de serviço para que eles podem ser definidos na implantação.

> [!NOTE]
> As conexões devem ser em Olá mesmo grupo de recursos aplicativo lógico de saudação.
>
>

### <a name="install-hello-logic-app-template-powershell-module"></a>Instalar o módulo do PowerShell de modelo de aplicativo do hello lógica
módulo do Hello mais fácil maneira tooinstall Olá é por meio de saudação [Galeria do PowerShell](https://www.powershellgallery.com/packages/LogicAppTemplate/0.1), usando o comando Olá `Install-Module -Name LogicAppTemplate`.  

Você também pode instalar o módulo de PowerShell Olá manualmente:

1. Baixar a versão mais recente de saudação do hello [criador do modelo de aplicativo de lógica](https://github.com/jeffhollan/LogicAppTemplateCreator/releases).  
2. Extrair pasta Olá na sua pasta de módulo do PowerShell (geralmente `%UserProfile%\Documents\WindowsPowerShell\Modules`).

Para Olá módulo toowork com acesso de locatário e assinatura token, é recomendável que você o use com hello [ARMClient](https://github.com/projectkudu/ARMClient) ferramenta de linha de comando.  Esta [postagem no blog](http://blog.davidebbo.com/2015/01/azure-resource-manager-client.html) aborda o ARMClient mais detalhadamente.

### <a name="generate-a-logic-app-template-by-using-powershell"></a>Gerar um modelo de aplicativo lógico usando o PowerShell
Depois que o PowerShell é instalado, você pode gerar um modelo usando o comando a seguir de saudação:

`armclient token $SubscriptionId | Get-LogicAppTemplate -LogicApp MyApp -ResourceGroup MyRG -SubscriptionId $SubscriptionId -Verbose | Out-File C:\template.json`

`$SubscriptionId`é a ID de assinatura do Azure hello. Essa linha primeiro obtém um token de acesso por meio do cliente do ARM, e direcioná-lo por meio de toohello script do PowerShell e, em seguida, cria o modelo de saudação em um arquivo JSON.

## <a name="add-parameters-tooa-logic-app-template"></a>Adicionar modelo de aplicativo de lógica de tooa de parâmetros
Depois de criar o modelo de aplicativo da lógica, você pode continuar tooadd ou modificar os parâmetros que você pode precisar. Por exemplo, se sua definição inclui um ID de recurso tooan função do Azure ou o fluxo de trabalho aninhado que você planeje toodeploy em uma única implantação, poderá adicionar modelo de tooyour mais recursos e parametrizar IDs conforme necessário. Olá mesmo se aplica tooany referências toocustom APIs Swagger pontos de extremidade ou esperar toodeploy com cada grupo de recursos.

## <a name="deploy-a-logic-app-template"></a>Implantar um modelo de aplicativo lógico

Você pode implantar o modelo usando qualquer ferramenta como o PowerShell, API de REST, [Visual Studio Team Services Release Management](#team-services)e a implantação de modelo por meio de saudação portal do Azure.
Além disso, valores de saudação toostore para parâmetros, é recomendável que você crie um [arquivo de parâmetro](../azure-resource-manager/resource-group-template-deploy.md#parameter-files).
Saiba como muito[implantar recursos com modelos do Gerenciador de recursos do Azure e PowerShell](../azure-resource-manager/resource-group-template-deploy.md) ou [implantar recursos com modelos do Gerenciador de recursos do Azure e Olá portal do Azure](../azure-resource-manager/resource-group-template-deploy-portal.md).

### <a name="authorize-oauth-connections"></a>Autorizar Conexões OAuth

Após a implantação, o aplicativo de lógica de saudação funciona ponta a ponta com os parâmetros válidos.
No entanto, você ainda deve autorizar OAuth conexões toogenerate um token de acesso válido.
tooauthorize OAuth conexões, abra o aplicativo de lógica de Olá no hello lógica do Designer de aplicativos e autorizar essas conexões. Ou, para a implantação automática, você pode usar um tooeach de tooconsent script conexão OAuth.
Há um script de exemplo no GitHub sob o projeto [LogicAppConnectionAuth](https://github.com/logicappsio/LogicAppConnectionAuth) .

<a name="team-services"></a>
## <a name="visual-studio-team-services-release-management"></a>Visual Studio Team Services Release Management

Um cenário comum para implantar e gerenciar um ambiente é uma ferramenta como o gerenciamento de versão no Visual Studio Team Services, com um modelo de implantação do aplicativo de lógica de toouse. Visual Studio Team Services inclui um [implantar grupo de recursos do Azure](https://github.com/Microsoft/vsts-tasks/tree/master/Tasks/DeployAzureResourceGroup) tarefas que você pode adicionar tooany build ou pipeline de versão. Você precisa toohave um [entidade de serviço](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/) para autorização toodeploy e, em seguida, você pode gerar definição de versão de saudação.

1. No Release Management, selecione **Vazio** para criar uma definição vazia.

    ![Criar definição vazia][1]

2. Escolha todos os recursos que necessários para este, provavelmente incluindo Olá lógica modelo de aplicativo que é gerado manualmente ou como parte de saudação do processo de compilação.
3. Adicione uma tarefa de **Implantação do Grupo de Recursos do Azure** .
4. Configurar com um [entidade de serviço](https://blogs.msdn.microsoft.com/visualstudioalm/2015/10/04/automating-azure-resource-group-deployment-using-a-service-principal-in-visual-studio-online-buildrelease-management/)e fazer referência a arquivos de modelo e parâmetros de modelo hello.
5. Continue toobuild etapas no processo de liberação de saudação para qualquer ambiente, um teste automatizado ou aprovadores conforme necessário.

<!-- Image References -->
[1]: ./media/logic-apps-create-deploy-template/emptyreleasedefinition.png
