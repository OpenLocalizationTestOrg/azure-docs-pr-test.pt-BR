---
title: projetos de grupo de recursos de Azure Studio aaaVisual | Microsoft Docs
description: "Use o Visual Studio toocreate um projeto do grupo de recursos do Azure e implante Olá tooAzure de recursos."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 4bd084c8-0842-4a10-8460-080c6a085bec
ms.service: azure-resource-manager
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: tomfitz
ms.openlocfilehash: 672c1e71fb809b3b547f0fad30240d45de1ba923
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-deploying-azure-resource-groups-through-visual-studio"></a>Criação e implantação de grupos de recurso do Azure por meio do Visual Studio
Com o Visual Studio e hello [SDK do Azure](https://azure.microsoft.com/downloads/), você pode criar um projeto que implanta tooAzure sua infraestrutura e de código. Por exemplo, você pode definir o host da web hello, site da web e banco de dados para seu aplicativo e implantar a infraestrutura que junto com o código de saudação. Ou pode definir uma Máquina Virtual, uma Rede Virtual e uma Conta de Armazenamento e implantar essa infraestrutura juntamente com um script que é executado na Máquina Virtual. Olá **o grupo de recursos do Azure** projeto de implantação permite que você toodeploy todos os recursos de Olá necessário em uma única operação repetida. Para obter mais informações sobre como implantar e gerenciar seus recursos, confira [Visão geral do Azure Resource Manager](resource-group-overview.md).

Projetos do grupo de recursos do Azure contêm modelos do Azure Resource Manager JSON que definem Olá recursos que você implante tooAzure. toolearn sobre elementos de saudação do modelo do Gerenciador de recursos de hello, consulte [modelos de autoria do Azure Resource Manager](resource-group-authoring-templates.md). Visual Studio permite que você tooedit esses modelos e fornece ferramentas para simplificam o trabalho com modelos.

Neste artigo, você pode implantar um aplicativo Web e o Banco de Dados SQL. No entanto, etapas de saudação são quase Olá mesmo para qualquer tipo de recurso. Você pode implantar facilmente uma Máquina Virtual e seus recursos relacionados. O Visual Studio fornece muitos modelos iniciais diferentes para implantar cenários comuns.

Este artigo mostra o Visual Studio 2017. Se você usar o Visual Studio 2015 atualização 2 e o SDK do Microsoft Azure para .NET 2.9 ou Visual Studio 2013 com Azure SDK 2.9, sua experiência é basicamente Olá mesmo. Você pode usar versões de saudação do SDK do Azure do 2.6 ou posterior; No entanto, sua experiência de interface do usuário Olá pode ser diferente da interface do usuário Olá mostrado neste artigo. É altamente recomendável que você instale a versão mais recente de saudação do hello [SDK do Azure](https://azure.microsoft.com/downloads/) antes de iniciar as etapas de saudação. 

## <a name="create-azure-resource-group-project"></a>Criar um projeto do Grupo de Recursos do Azure
Neste procedimento, você cria um projeto do Grupo de Recursos do Azure com um modelo do **aplicativo Web + SQL** .

1. No Visual Studio, escolha **Arquivo**, **Novo Projeto**, escolha **C#** ou **Visual Basic**. Então escolha **Nuvem** e o projeto de **Grupo de Recursos do Azure**.
   
    ![Projeto do Cloud Deployment](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-project.png)
2. Escolha o modelo de saudação que você deseja toodeploy tooAzure Gerenciador de recursos. Observe que há muitas opções diferentes com base em Olá o tipo de projeto você deseja toodeploy. Neste artigo, escolha Olá **Web app + SQL** modelo.
   
    ![Selecionar um modelo](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-project.png)
   
    modelo de saudação que você escolhe é apenas um ponto de partida; Você pode adicionar e remover recursos toofulfill seu cenário.
   
   > [!NOTE]
   > O Visual Studio recupera uma lista dos modelos disponíveis online. Olá lista pode mudar.
   > 
   > 
   
    Visual Studio cria um projeto de implantação do grupo de recursos para Olá web app e o banco de dados SQL.
3. toosee que você criou, procure no nó Olá no projeto de implantação de saudação.
   
    ![mostrar nós](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-items.png)
   
    Como escolhemos Olá Web app + modelo SQL para este exemplo, você verá Olá seguintes arquivos: 
   
   | Nome do arquivo | Descrição |
   | --- | --- |
   | Deploy-AzureResourceGroup.ps1 |Um script do PowerShell que invoca o PowerShell comandos toodeploy tooAzure Gerenciador de recursos.<br />**Observação** Visual Studio usa esse toodeploy de script do PowerShell seu modelo. Qualquer alteração feita toothis script afetam a implantação no Visual Studio, tenha cuidado. |
   | WebSiteSQLDatabase.json |modelo de Gerenciador de recursos de saudação que define infraestrutura Olá que você deseja implantar tooAzure e parâmetros de saudação, que você pode fornecer durante a implantação. Ele também define dependências de Olá entre recursos da saudação recursos Olá na ordem correta, Olá implanta o Gerenciador de recursos. |
   | WebSiteSQLDatabase.parameters.json |Um arquivo de parâmetros que contém os valores necessários pelo modelo de saudação. Você passar toocustomize de valores de parâmetro a cada implantação. |
   
    Todos os projetos de implantação do grupo de recursos do Azure contêm esses arquivos básicos. Outros projetos podem conter arquivos adicionais toosupport outras funcionalidades.

## <a name="customize-hello-resource-manager-template"></a>Personalizar o modelo do Gerenciador de recursos de saudação
Você pode personalizar um projeto de implantação modificando modelos JSON Olá que descrevem os recursos de saudação toodeploy desejado. JSON significa JavaScript Object Notation e é um formato de dados serializados que é fácil toowork com. os arquivos JSON Olá usam um esquema que você faz referência na parte superior de saudação de cada arquivo. Se desejar que o esquema de saudação toounderstand, você pode baixar e analisá-lo. Olá esquema define quais elementos são válidos, hello tipos e formatos de campos, Olá valores possíveis de valores enumerados e assim por diante. toolearn sobre elementos de saudação do modelo do Gerenciador de recursos de hello, consulte [modelos de autoria do Azure Resource Manager](resource-group-authoring-templates.md).

toowork em seu modelo, abra **WebSiteSQLDatabase.json**.

Olá Visual Studio, o editor fornece ferramentas tooassist com edição Olá modelo do Gerenciador de recursos. Olá **JSON contorno** janela torna fácil toosee elementos de saudação definidos no modelo.

![mostrar estrutura de tópicos JSON](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-json-outline.png)

Selecionando qualquer um dos elementos de saudação na estrutura de tópicos de saudação leva você toothat parte do modelo de saudação e realça Olá correspondente JSON.

![navegar o JSON](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/navigate-json.png)

Você pode adicionar um recurso, ou selecionando Olá **adicionar recurso** botão na parte superior da janela de estrutura de tópicos do JSON hello, ou clicando com o do hello **recursos** e selecionando **adicionar novo recurso**.

![adicionar recurso](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource.png)

Para este tutorial, selecione **Conta de Armazenamento** e forneça um nome. Forneça um nome que não tenha mais de 11 caracteres e contenha apenas números e letras minúsculas.

![adicionar armazenamento](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-storage.png)

Observe que não só foi adicionado de recurso hello, mas também um parâmetro para Olá digite a conta de armazenamento e uma variável de nome Olá Olá da conta de armazenamento.

![mostrar estrutura de tópicos](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-new-items.png)

Olá **storageType** parâmetro é predefinido com tipos permitidos e um tipo de padrão. Você pode deixar esses valores ou editá-los para seu cenário. Se você não deseja que qualquer pessoa toodeploy um **Premium_LRS** conta de armazenamento por meio desse modelo, remova-o do hello tipos permitido. 

```json
"storageType": {
  "type": "string",
  "defaultValue": "Standard_LRS",
  "allowedValues": [
    "Standard_LRS",
    "Standard_ZRS",
    "Standard_GRS",
    "Standard_RAGRS"
  ]
}
```

O Visual Studio também fornece intellisense toohelp entender quais propriedades estão disponíveis quando você editar o modelo de saudação. Por exemplo, propriedades de saudação tooedit para seu plano de serviço de aplicativo, navegar toohello **HostingPlan** recursos e adicione um valor para Olá **propriedades**. Observe que o intellisense mostra os valores disponíveis hello e fornece uma descrição desse valor.

![mostrar intellisense](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-intellisense.png)

Você pode definir **numberOfWorkers** too1.

```json
"properties": {
  "name": "[parameters('hostingPlanName')]",
  "numberOfWorkers": 1
}
```

## <a name="deploy-hello-resource-group-project-tooazure"></a>Implantar Olá tooAzure de projeto de grupo de recursos
Você está agora pronto toodeploy seu projeto. Quando você implanta um projeto do grupo de recursos do Azure, implantá-lo tooan grupo de recursos do Azure. grupo de recursos de saudação é um agrupamento lógico de recursos que compartilham um ciclo de vida comuns.

1. No menu de atalho de saudação do nó do projeto de implantação hello, escolha **implantar** > **novo**.
   
    ![Item de menu Implantar, Nova Implantação](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/deploy.png)
   
    Olá **implantar tooResource grupo** caixa de diálogo é exibida.
   
    ![Implantar tooResource caixa de diálogo grupo](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployment.png)
2. Em Olá **grupo de recursos** caixa suspensa, escolha um grupo de recursos existente ou crie um novo. toocreate um grupo de recursos, abra Olá **grupo de recursos** suspensa caixa e escolha **criar novo**.
   
    ![Implantar tooResource caixa de diálogo grupo](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-new-group.png)
   
    Olá **criar grupo de recursos** caixa de diálogo é exibida. Dado ao grupo um nome e local e selecione Olá **criar** botão.
   
    ![Caixa de diálogo Criar Grupo de Recursos](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-resource-group.png)
3. Editar parâmetros de saudação para implantação de saudação selecionando Olá **Editar parâmetros** botão.
   
    ![Botão Editar Parâmetros](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/edit-parameters.png)
4. Forneça valores para parâmetros de saudação vazio e selecione Olá **salvar** botão. parâmetros vazios Olá são **hostingPlanName**, **administratorLogin**, **administratorLoginPassword**, e **databaseName**.
   
    **hostingPlanName** Especifica um nome para Olá [plano de serviço de aplicativo](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) toocreate. 
   
    **administratorLogin** Especifica Olá nome de usuário de administrador do SQL Server hello. Não use nomes comuns de administração como **sa** ou **admin**. 
   
    Olá **administratorLoginPassword** Especifica uma senha de administrador do SQL Server. Olá **salvar senhas como texto sem formatação no arquivo de parâmetros de saudação** opção não é seguro; portanto, não selecione essa opção. Como Olá senha não é salva como texto sem formatação, é necessário tooprovide essa senha novamente durante a implantação. 
   
    **databaseName** Especifica um nome para Olá toocreate de banco de dados. 
   
    ![Caixa de diálogo Editar Parâmetros](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/provide-parameters.png)
5. Escolha Olá **implantar** botão toodeploy Olá projeto tooAzure. Abre um console do PowerShell fora da instância do Visual Studio hello. Insira a senha de administrador do SQL Server Olá no console do PowerShell hello quando solicitado. **O console do PowerShell pode ser oculto por trás de outros itens ou minimizado na barra de tarefas de saudação.** Procure esse console e selecione-a senha de saudação tooprovide.
   
   > [!NOTE]
   > O Visual Studio pode solicitar que você tooinstall Olá cmdlets do PowerShell do Azure. Você precisa hello Azure PowerShell cmdlets toosuccessfully implantar grupos de recursos. Se solicitado, instale-os.
   > 
   > 
6. implantação de saudação pode levar alguns minutos. Em Olá **saída** windows, consulte status Olá de implantação de saudação. Quando Olá implantação for concluída, a última mensagem de saudação indica uma implantação bem-sucedida com algo semelhante a:
   
        ... 
        18:00:58 - Successfully deployed template 'websitesqldatabase.json' tooresource group 'DemoSiteGroup'.
7. Em um navegador, abra Olá [portal do Azure](https://portal.azure.com/) e entre na conta de tooyour. grupo de recursos Olá toosee, selecione **grupos de recursos** e o grupo de recursos Olá implantada.
   
    ![selecionar grupo](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-group.png)
8. Você ver todos os recursos de saudação implantado. Observe o nome saudação do hello a conta de armazenamento não é exatamente o que você especificado ao adicionar esse recurso. conta de armazenamento Olá deve ser exclusiva. Olá modelo automaticamente adiciona uma cadeia de caracteres de nome de toohello de caracteres fornecida tooprovide um nome exclusivo. 
   
    ![mostrar recursos](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-resources.png)
9. Se você fizer alterações e quiser tooredeploy seu projeto, escolha o grupo de recursos existente Olá Olá menu de atalho do projeto do grupo de recursos do Azure. No menu de atalho hello, escolha **implantar**e em seguida, escolha o grupo de recursos de saudação é implantado.
   
    ![Grupo de recursos do Azure implantado](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/redeploy.png)

## <a name="deploy-code-with-your-infrastructure"></a>Implantar o código com sua infraestrutura
Neste ponto, você tenha implantado a infraestrutura de saudação para seu aplicativo, mas não há nenhum código real implantado com o projeto de saudação. Este artigo mostra como toodeploy um aplicativo web e o banco de dados SQL tabelas durante a implantação. Se você estiver implantando uma máquina Virtual em vez de um aplicativo web, você deseja toorun algum código na máquina hello como parte da implantação. Olá o processo de implantação de código para um aplicativo web ou para configurar uma máquina Virtual é quase Olá mesmo.

1. Adicione um projeto tooyour solução do Visual Studio. Solução de saudação e selecione **adicionar** > **novo projeto**.
   
    ![adicionar projeto](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-project.png)
2. Adicione um **Aplicativo Web ASP.NET**. 
   
    ![adicionar aplicativo Web](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-app.png)
3. Selecione **MVC**.
   
    ![selecionar MVC](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-mvc.png)
4. Depois que o Visual Studio cria seu aplicativo web, você verá ambos os projetos na solução de saudação.
   
    ![mostrar projetos](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-projects.png)
5. Agora, você precisa toomake-se de que seu projeto do grupo de recursos está ciente do novo projeto de saudação. Volte tooyour projeto do grupo de recursos (AzureResourceGroup1). Clique com botão direito do mouse em **Referências** e selecione **Adicionar Referência**.
   
    ![Adicionar Referência](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-new-reference.png)
6. Selecione o projeto de aplicativo web de saudação que você criou.
   
    ![Adicionar Referência](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-reference.png)
   
    Adicionando uma referência, você vincular Olá web aplicativo toohello recurso grupo projeto e automaticamente define três propriedades-chave. Ver essas propriedades Olá **propriedades** janela para referência de saudação.
   
      ![ver referência](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/see-reference.png)
   
    Olá propriedades são:
   
   * Olá **propriedades adicionais** contém o pacote de implantação da web hello preparo local que é enviada por push toohello armazenamento do Azure. Observe a pasta de saudação (ExampleApp) e o arquivo (package.zip). Você precisa tooknow esses valores, porque você fornecê-los como parâmetros durante a implantação de aplicativo de hello. 
   * Olá **caminho de inclusão do arquivo** contém Olá caminho onde o pacote de saudação é criado. Olá **incluir destinos** contém Olá comando que é executado de implantação. 
   * Olá valor padrão de **de compilação; Pacote** habilita Olá toobuild de implantação e criar um pacote de implantação da web (package.zip).  
     
     Não é necessário um perfil de publicação como implantação de saudação obtém informações necessárias de saudação do pacote de saudação do hello propriedades toocreate.
7. Voltar tooWebSiteSQLDatabase.json e adicione um modelo de toohello de recursos.
   
    ![adicionar recurso](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource-2.png)
8. Dessa vez, selecione **Implantação da Web para aplicativos Web**. 
   
    ![adicionar implantação da Web](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-web-deploy.png)
9. Reimplante seu grupo de recursos do toohello de projeto do grupo de recursos. Desta vez, há alguns parâmetros novos. Não é necessário para os valores tooprovide **_artifactsLocation** ou **_artifactsLocationSasToken** porque o Visual Studio gera automaticamente esses valores. No entanto, você tem a pasta de saudação tooset e nome do arquivo toohello caminho que contém o pacote de implantação de saudação (mostrado como **ExampleAppPackageFolder** e **ExampleAppPackageFileName** em Olá a imagem a seguir ). Forneça valores hello você viu anteriormente na Olá propriedades da referência (**ExampleApp** e **package.zip**).
   
    ![adicionar implantação da Web](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/set-new-parameters.png)
   
    Para Olá **conta de armazenamento do artefato**, selecione Olá uma implantada com este grupo de recursos.
10. Após a implantação do hello, selecione seu aplicativo web no portal de saudação. Selecione Olá URL toobrowse toohello site.
    
     ![procurar no site](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/browse-site.png)
11. Observe que você implantou saudação padrão ASP.NET aplicativo com êxito.
    
     ![mostrar aplicativo implantado](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-app.png)

## <a name="next-steps"></a>Próximas etapas
* toolearn sobre como gerenciar seus recursos por meio do portal hello, consulte [usando os recursos do Azure de toomanage portal do Azure Olá](resource-group-portal.md).
* toolearn mais sobre modelos, consulte [modelos de autoria do Azure Resource Manager](resource-group-authoring-templates.md).

