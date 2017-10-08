---
title: "aaaProvision e implantar microservices previsível no Azure"
description: "Saiba como toodeploy um aplicativo composto de microservices no serviço de aplicativo do Azure como uma única unidade e de maneira previsível usando modelos de grupo de recursos JSON e o script do PowerShell."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: bb51e565-e462-4c60-929a-2ff90121f41d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2016
ms.author: cephalin
ms.openlocfilehash: d32c2fc82a8b09e89224ec437e5819b65b2e9e78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-and-deploy-microservices-predictably-in-azure"></a>Provisionar e implantar microsserviços previsíveis no Azure
Este tutorial mostra como tooprovision e implantar um aplicativo composto [microservices](https://en.wikipedia.org/wiki/Microservices) na [do serviço de aplicativo do Azure](/services/app-service/) como uma única unidade e de maneira previsível usando modelos de grupo de recursos JSON e Script do PowerShell. 

Quando o provisionamento e implantação de aplicativos de grande escala que são compostos de microservices altamente desacoplada, capacidade de repetição e a previsibilidade são toosuccess crucial. [Serviço de aplicativo do Azure](/services/app-service/) permite que você microservices toocreate que incluem aplicativos web, aplicativos móveis, aplicativos de API e aplicativos lógicos. [Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-overview.md) permite que você toomanage todos os microservices de saudação como uma unidade, junto com as dependências de recurso, como configurações de controle de origem e de banco de dados. Agora, você também pode implantar esse aplicativo usando modelos JSON e scripts simples do PowerShell. 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-do"></a>O que você fará
Olá tutorial, você implantará um aplicativo que inclui:

* Dois aplicativos Web (isto é, dois microsserviços)
* Um banco de dados SQL de back-end
* Configurações do aplicativo, cadeias de conexão e controle do código-fonte
* Application Insights, alertas, configurações de dimensionamento automático

## <a name="tools-you-will-use"></a>Ferramentas que você utilizará
Neste tutorial, você usará Olá ferramentas a seguir. Pois ele não é abrangente sobre ferramentas, eu vou cenário de ponta a ponta de toohello toostick e apenas oferecem tooeach uma breve introdução, e onde você pode encontrar mais informações sobre ela. 

### <a name="azure-resource-manager-templates-json"></a>Modelos do Gerenciador de Recursos do Azure (JSON)
Toda vez que você criar um aplicativo web no serviço de aplicativo do Azure, por exemplo, o Gerenciador de recursos do Azure usa um grupo de recursos inteiro JSON modelo toocreate Olá com recursos de componente de saudação. Um modelo complexo de saudação [Azure Marketplace](/marketplace) como Olá [WordPress escalonável](/marketplace/partners/wordpress/scalablewordpress/) aplicativo pode incluir o banco de dados do hello MySQL contas de armazenamento, Olá plano de serviço de aplicativo, Olá web aplicativo em si, regras de alerta, o aplicativo as configurações, as configurações de dimensionamento automático e mais e todos esses modelos são tooyou disponível por meio do PowerShell. Para obter informações sobre como toodownload e usar esses modelos, consulte [usando o PowerShell do Azure com o Azure Resource Manager](../powershell-azure-resource-manager.md).

Para obter mais informações sobre modelos do Azure Resource Manager hello, consulte [criação de modelos de Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md)

### <a name="azure-sdk-26-for-visual-studio"></a>SDK do Azure para Visual Studio 2.6
Olá SDK mais recente contém melhorias toohello Gerenciador de recursos de suporte de modelo no editor de JSON hello. Você pode usar este tooquickly criar um modelo de grupo de recursos a partir do zero ou abrir um modelo JSON existente (como um modelo de galeria baixado) para modificação, preencher o arquivo de parâmetros de saudação e até mesmo implantar grupo de recursos de saudação diretamente a partir do Azure Solução de grupo de recursos.

Para obter mais informações, consulte [SDK do Azure para Visual Studio 2.6](https://azure.microsoft.com/blog/2015/04/29/announcing-the-azure-sdk-2-6-for-net/).

### <a name="azure-powershell-080-or-later"></a>Azure PowerShell 0.8.0 ou posterior
Começando na versão 0.8.0, Olá instalação do PowerShell do Azure inclui módulo do Azure Resource Manager Olá em adição toohello módulo do Azure. Este novo módulo permite que você tooscript implantação de saudação de grupos de recursos.

Para obter mais informações, consulte [Usando o PowerShell do Azure com o Gerenciador de Recursos do Azure](../powershell-azure-resource-manager.md)

### <a name="azure-resource-explorer"></a>Gerenciador de Recursos do Azure
Isso [ferramenta de visualização](https://resources.azure.com) permite que você tooexplore definições de JSON de saudação de todos os grupos de recursos de saudação em sua assinatura e Olá recursos individuais. Na ferramenta de hello, Editar definições de JSON de saudação de um recurso, excluir uma hierarquia inteira de recursos e criar novos recursos.  informações de saudação prontamente disponíveis nessa ferramenta serão muito útil para criação de modelo, como mostra o que propriedades que você precisa tooset para um determinado tipo de recurso, hello corrija valores, etc. Você pode até mesmo criar seu grupo de recursos no hello [Portal do Azure](https://portal.azure.com/), em seguida, verifique suas definições de JSON em Olá explorer ferramenta toohelp você templatize o grupo de recursos de saudação.

### <a name="deploy-tooazure-button"></a>TooAzure botão implantar
Se você usar o GitHub para controle de origem, você pode colocar um [implantar tooAzure botão](https://azure.microsoft.com/blog/2014/11/13/deploy-to-azure-button-for-azure-websites-2/) em seu arquivo Leiame. MD, que permite que um tooAzure de interface do usuário de implantação completas. Enquanto você pode fazer isso para qualquer aplicativo da web simples, você pode estender esse tooenable Implantando um grupo de recursos inteiro colocando um arquivo azuredeploy.json na raiz do repositório de saudação. Esse arquivo JSON, que contém o modelo de grupo de recursos hello, será usado pelo grupo de recursos Olá implantar tooAzure botão toocreate hello. Para obter um exemplo, consulte Olá [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) exemplo, que você usará neste tutorial.

## <a name="get-hello-sample-resource-group-template"></a>Obter o modelo de grupo de recursos do exemplo hello
Agora, vamos tooit à direita.

1. Navegue toohello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) exemplo de serviço de aplicativo.
2. Em readme.md, clique em **implantar tooAzure**.
3. Você é levado toohello [implantar para azure](https://deploy.azure.com) site e os parâmetros de implantação tooinput frequentes. Observe que a maioria dos campos de saudação é populada com o nome do repositório hello e algumas cadeias de caracteres aleatórias para você. Você pode alterar todos os campos de saudação se desejar, mas únicas coisas de saudação ter tooenter são Olá administrativa logon e senha hello e clique em **próximo**.
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-1-deploybuttonui.png)
4. Em seguida, clique em **implantar** toostart processo de implantação de saudação. Depois que o processo de saudação executa toocompletion, clique em Olá http://todoapp*XXXX*. saudação do azurewebsites.net link toobrowse implantou o aplicativo. 
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-2-deployprogress.png)
   
   Saudação da interface do usuário seja um pouco lenta quando você procura primeiro tooit porque Olá aplicativos estão iniciando, mas convencer-se de que se trata de um aplicativo totalmente funcional.
5. Em página de implantar hello, clique em Olá **gerenciar** link toosee Olá novo aplicativo no hello Portal do Azure.
6. Em Olá **Essentials** lista suspensa, clique no link Olá recurso grupo. Observe também que o aplicativo web hello já está conectado toohello repositório do GitHub em **projeto externo**. 
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-3-portalresourcegroup.png)
7. Na folha de grupo de recursos hello, observe que já existem dois aplicativos da web e um banco de dados do SQL no grupo de recursos de saudação.
   
   ![](./media/app-service-deploy-complex-application-predictably/gettemplate-4-portalresourcegroupclicked.png)

Tudo o que você acabou de ver em poucos minutos curtos for um aplicativo de microsserviço de dois totalmente implantado, com todos os componentes de saudação, dependências, configurações, banco de dados e publicação contínua, definido por uma orquestração automatizada no Gerenciador de recursos do Azure. Tudo isso foi feito por duas coisas:

* botão de tooAzure implantar Olá
* azuredeploy.JSON na raiz do repositório de saudação

Você pode implantar esse aplicativo mesmo dezenas, centenas ou milhares de vezes e ter Olá exatamente a mesma configuração sempre. previsibilidade de repetição e Olá Olá dessa abordagem permite que aplicativos de alta escala toodeploy com facilidade e confiança.

## <a name="examine-or-edit-azuredeployjson"></a>Examinar (ou editar) AZUREDEPLOY.JSON
Agora vamos dar uma olhada em como o repositório do GitHub Olá foi configurado. Você usará o editor de JSON Olá no hello Azure .NET SDK, portanto, se você ainda não instalou [Azure .NET SDK 2.6](/downloads/), faça isso agora.

1. Saudação de clone [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repositório usando sua ferramenta favorita git. Abaixo da captura de tela hello, estou fazendo isso no hello Team Explorer no Visual Studio 2013.
   
   ![](./media/app-service-deploy-complex-application-predictably/examinejson-1-vsclone.png)
2. Na raiz do repositório hello, abra azuredeploy.json no Visual Studio. Se você não vir o painel de estrutura de tópicos do JSON Olá, será necessário tooinstall SDK .NET do Azure.
   
   ![](./media/app-service-deploy-complex-application-predictably/examinejson-2-vsjsoneditor.png)

Estou não vai toodescribe todos os detalhes do formato JSON de hello, mas Olá [mais recursos](#resources) seção contém links para aprender a linguagem de modelo de grupo de recursos de saudação. Aqui, vou tooshow você Olá interessantes recursos que podem ajudá-lo a começar a fazer o seu próprio modelo personalizado para a implantação do aplicativo.

### <a name="parameters"></a>parâmetros
Examine Olá parâmetros seção toosee que a maioria desses parâmetros são quais Olá **implantar tooAzure** botão solicitará que você tooinput. site Olá atrás Olá **implantar tooAzure** botão preenche Olá entrada da interface do usuário usando os parâmetros de saudação definidos em azuredeploy.json. Esses parâmetros são usados em definições de recursos hello, como nomes de recursos, os valores de propriedade, etc.

### <a name="resources"></a>Recursos
No nó de recursos hello, você pode ver que os recursos de alto nível 4 são definidos, incluindo uma instância do SQL Server, um plano de serviço de aplicativo e dois aplicativos da web. 

#### <a name="app-service-plan"></a>Plano do Serviço de Aplicativo
Vamos começar com um simple recurso de nível raiz em Olá JSON. No hello JSON da estrutura de tópicos, clique em plano de serviço de aplicativo hello chamado **[hostingPlanName]** toohighlight Olá código JSON correspondente. 

![](./media/app-service-deploy-complex-application-predictably/examinejson-3-appserviceplan.png)

Observe que Olá `type` elemento Especifica a cadeia de caracteres de saudação para um plano de serviço de aplicativo (ele era chamado de um farm de servidores há um tempo longo, long) e outros elementos e propriedades são preenchidas usando Olá parâmetros definidos no arquivo JSON de saudação e este recurso não tem todos os recursos aninhados.

> [!NOTE]
> Observe também que valor Olá `apiVersion` informa qual versão do hello API REST toouse Olá JSON definição de recurso com e pode afetar como recurso Olá deve ser formatado dentro de saudação do Azure `{}`. 
> 
> 

#### <a name="sql-server"></a>SQL Server
Em seguida, clique no recurso do SQL Server Olá denominado **SQLServer** em Olá da estrutura de tópicos do JSON.

![](./media/app-service-deploy-complex-application-predictably/examinejson-4-sqlserver.png)

Saudação de observação a seguir sobre Olá realçado código JSON:

* uso de saudação de parâmetros garante que recursos Olá criado são denominados e configurados de forma que faz com que sejam consistentes entre si.
* Olá recursos do SQL Server tem dois recursos aninhados, cada um tem um valor diferente para `type`.
* Olá aninhados recursos dentro de `“resources”: […]`, onde o banco de dados de saudação e regras de firewall de saudação são definidas, ter um `dependsOn` elemento que especifica a ID de recurso de saudação do recurso do hello nível raiz SQLServer. Isso informa ao Gerenciador de recursos do Azure, "antes de criar esse recurso, que outro recurso já deve existir; e se outros recursos que é definido no modelo de hello, crie um primeiro".
  
  > [!NOTE]
  > Para obter informações detalhadas sobre como Olá toouse `resourceId()` funcionam, consulte [funções de modelo do Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-template-functions-resource.md#resourceid).
  > 
  > 
* Olá efeito de saudação `dependsOn` elemento é que o Azure Resource Manager pode saber quais recursos podem ser criados em paralelo e quais recursos devem ser criados em sequência. 

#### <a name="web-app"></a>Aplicativo Web
Agora, vamos passar toohello real aplicativos web, que são mais complicados. Clique em aplicativo web de saudação [variables('apiSiteName')] toohighlight de estrutura de tópicos do JSON Olá seu código JSON. Você perceberá que as coisas estão ficando muito mais interessantes. Para essa finalidade, vou falar sobre os recursos de saudação uma:

##### <a name="root-resource"></a>Recurso raiz
Olá web aplicativo depende de dois recursos diferentes. Isso significa que o Gerenciador de recursos do Azure criará Olá web app somente após os dois Olá Olá instância do SQL Server e plano de serviço de aplicativo são criados.

![](./media/app-service-deploy-complex-application-predictably/examinejson-5-webapproot.png)

##### <a name="app-settings"></a>Configurações do aplicativo
configurações do aplicativo Hello também são definidas como um recurso aninhado.

![](./media/app-service-deploy-complex-application-predictably/examinejson-6-webappsettings.png)

Em Olá `properties` elemento para `config/appsettings`, você tem duas configurações de aplicativo no formato de saudação `“<name>” : “<value>”`.

* `PROJECT`é um [configuração KUDU](https://github.com/projectkudu/kudu/wiki/Customizing-deployments) que informa quais toouse projeto implantação do Azure em uma solução do Visual Studio multiprojeto. Vou mostrar mais tarde como controle de origem está configurado, mas como Olá ToDoApp código está em uma solução do Visual Studio multiprojeto, precisamos que essa configuração.
* `clientUrl`é simplesmente um aplicativo definindo esse código de aplicativo hello usa.

##### <a name="connection-strings"></a>Cadeias de conexão
cadeias de caracteres de conexão Olá também são definidas como um recurso aninhado.

![](./media/app-service-deploy-complex-application-predictably/examinejson-7-webappconnstr.png)

Em Olá `properties` elemento para `config/connectionstrings`, cada cadeia de caracteres de conexão também é definida como um par de nome: valor, com o formato específico de saudação do `“<name>” : {“value”: “…”, “type”: “…”}`. Para Olá `type` elemento, os valores possíveis são `MySql`, `SQLServer`, `SQLAzure`, e `Custom`.

> [!TIP]
> Para obter uma lista definitiva de tipos de cadeia de caracteres de conexão hello, executar Olá comando no Azure PowerShell a seguir: \[Enum]::GetNames("Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.DatabaseType")
> 
> 

##### <a name="source-control"></a>Controle do código-fonte
configurações de controle de origem Olá também são definidas como um recurso aninhado. Gerenciador de recursos do Azure usa essa publicação contínua de tooconfigure de recurso (consulte limitação em `IsManualIntegration` mais tarde) e também tookick desativar a implantação de saudação do código do aplicativo automaticamente durante o processamento de saudação do arquivo JSON de saudação.

![](./media/app-service-deploy-complex-application-predictably/examinejson-8-webappsourcecontrol.png)

`RepoUrl`e `branch` devem ser bem intuitivo e deve apontar o nome de repositório e hello de Git de toohello de toopublish de ramificação de saudação do. Mais uma vez, estes são definidos pelos parâmetros de entrada. 

Observe que, no hello `dependsOn` elemento que, em adição toohello web recursos de aplicativo em si, `sourcecontrols/web` também depende de `config/appsettings` e `config/connectionstrings`. Isso ocorre porque quando `sourcecontrols/web` é configurado, Olá processo de implantação do Azure tentará automaticamente toodeploy, criar e iniciar o código do aplicativo hello. Portanto, inserindo ajuda a dependência você certifique-se de que aplicativo hello tem acesso toohello necessárias configurações e cadeias de caracteres de conexão antes de Olá código de aplicativo é executado. 

> [!NOTE]
> Observe também que `IsManualIntegration` está definido muito`true`. Essa propriedade é necessária neste tutorial, porque você não é realmente seu repositório do GitHub hello e, portanto, na verdade, não é possível conceder permissão tooAzure tooconfigure contínua a publicação de [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) (ou seja, enviar por push automático repositório de atualizações tooAzure). Você pode usar o valor padrão de saudação `false` para repositório de saudação especificado somente se você configurou as credenciais do GitHub do proprietário Olá Olá [portal do Azure](https://portal.azure.com/) antes. Em outras palavras, se você configurou o tooGitHub de controle do código-fonte ou BitBucket para qualquer aplicativo em Olá [Portal do Azure](https://portal.azure.com/) anteriormente, usando seu usuário de credenciais de Azure será lembrar credenciais hello e usá-los sempre que você implantar qualquer aplicativo do GitHub ou BitBucket em Olá futuras. No entanto, se você ainda não tiver feito isso, implantação de modelo JSON Olá falhará quando o Gerenciador de recursos do Azure tenta configurações de controle de origem do aplicativo de web hello tooconfigure porque ele não pode efetuar logon no GitHub ou BitBucket com credenciais do proprietário do repositório de saudação.
> 
> 

## <a name="compare-hello-json-template-with-deployed-resource-group"></a>Comparar o modelo JSON Olá com grupo de recursos implantados
Aqui, você pode usar folhas do aplicativo da web de saudação todos em Olá [Portal do Azure](https://portal.azure.com/), mas não há outra ferramenta que é tão útil, se não mais. Vá toohello [Gerenciador de recursos do Azure](https://resources.azure.com) ferramenta de visualização, que fornece uma representação JSON de todos os grupos de recursos de saudação em suas assinaturas, como realmente existem no hello back-end do Azure. Você também pode ver como hierarquia JSON do grupo de recursos Olá no Azure corresponde à hierarquia Olá no arquivo de modelo de saudação que usou toocreate-lo.

Por exemplo, quando vou toohello [Gerenciador de recursos do Azure](https://resources.azure.com) ferramenta e expandir nós Olá explorer hello, posso ver o grupo de recursos Olá e recursos de nível raiz de saudação que são coletados em seus tipos do respectivos recursos.

![](./media/app-service-deploy-complex-application-predictably/ARM-1-treeview.png)

Se aprofundar tooa web app, você deverá ser capaz de toosee web app configuration detalhes semelhantes toohello captura de tela abaixo:

![](./media/app-service-deploy-complex-application-predictably/ARM-2-jsonview.png)

Novamente, hello recursos aninhados devem ter um toothose muito semelhantes de hierarquia em seu arquivo de modelo JSON, e você deverá ver as configurações do aplicativo hello, cadeias de caracteres de conexão, etc., adequadamente refletidas no painel JSON de saudação. ausência de saudação de configurações pode indicar um problema com o arquivo JSON e pode ajudá-lo a solucionar problemas de seu arquivo de modelo JSON.

## <a name="deploy-hello-resource-group-template-yourself"></a>Implantar o modelo de grupo de recursos de saudação por conta própria
Olá **implantar tooAzure** botão for grande, mas permite que você toodeploy modelo de grupo de recursos de saudação em azuredeploy.json somente se você já tiver enviado azuredeploy.json tooGitHub. Olá SDK .NET do Azure também fornece ferramentas Olá para você toodeploy qualquer arquivo de modelo JSON diretamente do seu computador local. toodo isso, execute Olá estas etapas abaixo:

1. No Visual Studio, clique em **Arquivo** > **Novo** > **Projeto**.
2. Clique em **Visual C#** > **Nuvem** > **Grupo de Recursos do Azure**, em seguida, clique em **OK**.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-1-vsproject.png)
3. Em **Selecionar Modelo do Azure**, selecione **Modelo em Branco** e clique em **OK**.
4. Arraste azuredeploy.json para Olá **modelo** pasta do seu novo projeto.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-2-copyjson.png)
5. No Gerenciador de soluções, abra azuredeploy.json Olá copiado.
6. Apenas para a mesma Olá demonstração Olá, vamos adicionar alguns arquivos JSON tooour recursos de Application Insight clicando **adicionar recurso**. Se você estiver interessado apenas em implantar o arquivo JSON de hello, ignorar toohello implantar etapas.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-3-newresource.png)
7. Selecione **Application Insights para Aplicativos Web**, certifique-se de que um aplicativo Web e um Plano do Serviço de Aplicativo existentes estão selecionados e, em seguida, clique em **Adicionar**.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-4-newappinsight.png)
   
   Você agora vai ser capaz de toosee vários recursos novos que, dependendo do recurso de saudação e o que ele faz, ter dependências em um aplicativo de serviço de aplicativo plano ou Olá web hello. Esses recursos não estão habilitados por sua definição existente e você vai toochange que.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-5-appinsightresources.png)
8. No hello JSON da estrutura de tópicos, clique em **appInsights AutoEscala** toohighlight seu código JSON. Isso é hello dimensionamento de configuração para o plano de serviço de aplicativo.
9. Em Olá código JSON realçado, localize Olá `location` e `enabled` propriedades e defini-los, conforme mostrado abaixo.
   
   ![](./media/app-service-deploy-complex-application-predictably/deploy-6-autoscalesettings.png)
10. No hello JSON da estrutura de tópicos, clique em **CPUHigh appInsights** toohighlight seu código JSON. Este é um alerta.
11. Localizar Olá `location` e `isEnabled` propriedades e defini-los, conforme mostrado abaixo. Olá mesmo para Olá outros três alertas (lâmpadas roxas).
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-7-alerts.png)
12. Agora você está pronto toodeploy. Clique com botão direito hello e selecione **implantar** > **nova implantação**.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-8-newdeployment.png)
13. Faça logon na conta do Azure se ainda não fez isso.
14. Selecione um grupo de recursos existente em sua assinatura ou crie um novo, selecione **azuredeploy.json** e, em seguida, clique em **Editar parâmetros**.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-9-deployconfig.png)
    
    Agora, você será capaz de tooedit todos os parâmetros de saudação definidos no arquivo de modelo de saudação em uma tabela adequado. Parâmetros que definem padrões já terão seus valores padrão, enquanto parâmetros que definem uma lista de valores permitidos serão mostrados como listas suspensas.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-10-parametereditor.png)
15. Preencha todos os parâmetros de saudação vazio e use Olá [endereço de repositório do GitHub para ToDoApp](https://github.com/azure-appservice-samples/ToDoApp.git) na **repoUrl**. Em seguida, clique em **Salvar**.
    
    ![](./media/app-service-deploy-complex-application-predictably/deploy-11-parametereditorfilled.png)
    
    > [!NOTE]
    > O dimensionamento automático é um recurso oferecido em **padrão** nível ou superior e nível de plano de alertas são recursos oferecidos nos **básica** camada ou superior, você precisará Olá tooset **sku** parâmetro muito**padrão** ou **Premium** em ordem toosee todos os seus novos Insights do aplicativo recursos leves para cima.
    > 
    > 
16. Clique em **Implantar**. Se você selecionou **salvar senhas**, Olá senha será salva no arquivo de parâmetro hello **em texto sem formatação**. Caso contrário, será perguntado senha de banco de dados de saudação tooinput durante o processo de implantação hello.

É isso! Agora você precisa apenas toogo toohello [Portal do Azure](https://portal.azure.com/) e hello [Gerenciador de recursos do Azure](https://resources.azure.com) ferramenta toosee Olá novos alertas e configurações de dimensionamento automático adicionados tooyour JSON implantou o aplicativo.

As etapas nesta seção feito principalmente seguinte hello:

1. Arquivo de modelo Olá preparada
2. Criado um toogo do arquivo de parâmetro com o arquivo de modelo Olá
3. Arquivo de modelo Olá implantado com o arquivo de parâmetro hello

Olá última etapa facilmente será feita por um cmdlet do PowerShell. toosee o Visual Studio fez quando implantado seu aplicativo, abra Scripts\Deploy-AzureResourceGroup.ps1. Há muito código existe, mas vou toohighlight todo código pertinentes Olá precisar toodeploy Olá modelo arquivo com o arquivo de parâmetro hello.

![](./media/app-service-deploy-complex-application-predictably/deploy-12-powershellsnippet.png)

Olá última cmdlet, `New-AzureResourceGroup`, é hello que realmente executa a ação de saudação. Tudo isso deve demonstrar tooyou, com a Ajuda de saudação de ferramentas, é relativamente simples toodeploy seu aplicativo de nuvem previsível. Toda vez que você executar o cmdlet Olá em Olá Olá mesmo modelo com o mesmo arquivo de parâmetro, você vai tooget Olá mesmo resultado.

## <a name="summary"></a>Resumo
DevOps, repetição e previsibilidade são implantação bem-sucedida do tooany de chaves de um aplicativo de alta escala composto de microservices. Neste tutorial, você implantou um tooAzure do aplicativo de duas microsserviço como um único grupo de recursos usando o modelo do Azure Resource Manager hello. Espera-se que ele concede a você hello conhecimento que você precisa em ordem toostart converter seu aplicativo no Azure em um modelo e pode provisionar e implantá-lo de maneira previsível. 

## <a name="next-steps"></a>Próximas etapas
Descubra como muito[aplicar as metodologias agile e continuamente publicar seu aplicativo microservices com facilidade](app-service-agile-software-development.md) e técnicas de implantação como avançadas [flighting implantação](app-service-web-test-in-production-controlled-test-flight.md) facilmente.

<a name="resources"></a>

## <a name="more-resources"></a>Mais recursos
* [Idioma de modelo do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md)
* [Criando modelos do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md)
* [Funções de modelo do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-template-functions.md)
* [Implantar um aplicativo com o modelo do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-template-deploy.md)
* [Usando o Azure PowerShell com o Gerenciador de Recursos do Azure](../azure-resource-manager/powershell-azure-resource-manager.md)
* [Solucionando problemas de implantações de grupos de recursos no Azure](../azure-resource-manager/resource-manager-common-deployment-errors.md)

