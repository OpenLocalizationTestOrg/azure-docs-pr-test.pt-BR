---
title: aaaDeploy WebJobs usando o Visual Studio
description: "Saiba como toodeploy do Azure WebJobs tooAzure aplicativos de Web do serviço do aplicativo usando o Visual Studio."
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: a3a9d320-1201-4ac8-9398-b4c9535ba755
ms.service: app-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2016
ms.author: glenga
ms.openlocfilehash: 5fc5d9562e8836348f5ab6844fb6c23ff40a321c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-webjobs-using-visual-studio"></a>Implantar Trabalhos Web usando o Visual Studio
## <a name="overview"></a>Visão geral
Este tópico explica como toouse Visual Studio toodeploy um aplicativo de Console projeto aplicativo web de tooa [do serviço de aplicativo](http://go.microsoft.com/fwlink/?LinkId=529714) como um [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226). Para obter informações sobre como toodeploy WebJobs usando Olá [Portal do Azure](https://portal.azure.com), consulte [tarefas de execução em segundo plano com o WebJobs](web-sites-create-web-jobs.md).

Ao implantar um projeto do Aplicativo de Console habilitado para Trabalhos Web, o Visual Studio realiza duas tarefas:

* Tempo de execução de cópias de arquivos toohello a pasta apropriada no aplicativo web de saudação (*App_Data/trabalhos/contínua* para trabalhos Web contínuos, *App_Data/trabalhos/disparado* para trabalhos Web agendados e sob demanda).
* Configura [trabalhos do Agendador do Azure](#scheduler) para WebJobs são agendado toorun em momentos específicos. (Isso não é necessário para Trabalhos Web contínuos.)

Um projeto habilitadas WebJobs tem Olá tooit adicionados itens a seguir:

* Olá [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) pacote NuGet.
* Um arquivo [webjob-publish-settings.json](#publishsettings) que contém configurações de implantação e agendador. 

![Diagrama mostrando o que é adicionado tooa implantação de tooenable de aplicativo de Console como um trabalho Web](./media/websites-dotnet-deploy-webjobs/convert.png)

Você pode adicionar esses tooan itens existentes do projeto de aplicativo de Console ou usar um modelo toocreate um novo projeto de aplicativo de Console WebJobs habilitado. 

Você pode implantar um projeto como um trabalho Web por si só ou vincular projeto da web de tooa para que ele implanta automaticamente sempre que você implantar o projeto da web de saudação. projetos toolink, Visual Studio inclui o nome de saudação do projeto de saudação trabalhos Web habilitados em um [webjobs list.json](#webjobslist) arquivo no projeto da web de saudação.

![Diagrama mostrando o projeto do WebJob tooweb projeto de vinculação](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a>Pré-requisitos
Recursos de implantação de trabalhos Web estão disponíveis no Visual Studio quando você instala o hello Azure SDK para .NET:

* [SDK do Azure para .NET (Visual Studio)](https://azure.microsoft.com/downloads/).

## <a id="convert"></a>Habilitar a implantação de Trabalhos Web para um projeto do Aplicativo de Console existente
Você tem duas opções:

* [Habilitar implantação automática com um projeto Web](#convertlink).
  
    Configure um projeto do Aplicativo de Console existente de forma que ele seja implantado automaticamente como um Trabalho Web quando você implanta o projeto Web. Use essa opção quando desejar toorun seu trabalho Web em Olá mesmo aplicativo da web em que você executar Olá relacionados ao aplicativo web.
* [Habilitar implantação sem um projeto Web](#convertnolink).
  
    Configure um toodeploy de projeto de aplicativo de Console existente como um trabalho Web por si só, com nenhum projeto da web do link tooa. Use essa opção quando quiser toorun um trabalho Web em um aplicativo web por si só, com nenhum aplicativo web em execução no aplicativo web de saudação. Talvez você queira toodo isso na ordem tooscale capaz de toobe seus recursos de trabalho Web independentemente dos recursos do aplicativo web.

### <a id="convertlink"></a> Habilitar a implantação de Trabalhos Web automática com um projeto Web
1. Projeto de web hello com o botão direito em **Solution Explorer**e, em seguida, clique em **adicionar** > **projeto existente como Azure WebJob**.
   
    ![Projeto Existente como Trabalho Web do Azure](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    Olá [adicionar Azure WebJob](#configure) caixa de diálogo é exibida.
2. Em Olá **nome do projeto** lista suspensa, selecione Olá tooadd de projeto de aplicativo de Console como um trabalho Web.
   
    ![Selecionando projeto na caixa de diálogo Adicionar Trabalho Web do Azure](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. Olá completa [adicionar Azure WebJob](#configure) caixa de diálogo e clique **Okey**. 

### <a id="convertnolink"></a> Habilitar a implantação de Trabalhos Web sem um projeto Web
1. Projeto de aplicativo de Console Olá com o botão direito no **Solution Explorer**e, em seguida, clique em **Publicar como Azure WebJob...** . 
   
    ![Publicar como Trabalho Web do Azure](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    Olá [adicionar Azure WebJob](#configure) caixa de diálogo é exibida com hello projeto selecionado no hello **nome do projeto** caixa.
2. Olá completa [adicionar Azure WebJob](#configure) caixa de diálogo e clique **Okey**.
   
   Olá **Publicar Web** assistente é exibido.  Se você não quiser toopublish imediatamente, feche o Assistente de saudação. configurações de saudação que você inseriu são salvos para quando você quiser muito[implantar projeto Olá](#deploy).

## <a id="create"></a>Criar um novo projeto habilitado para Trabalhos Web
toocreate um novo projeto de trabalhos Web habilitados, você pode usar Olá Console projeto modelo e habilitar trabalhos Web implantação do aplicativo conforme explicado em [Olá seção anterior](#convert). Como alternativa, você pode usar o modelo de novo projeto de trabalhos Web hello:

* [Use o modelo de novo projeto de WebJobs de saudação para um trabalho Web independente](#createnolink)
  
    Criar um projeto e configurá-lo toodeploy por si próprio como um trabalho Web com nenhum projeto da web do link tooa. Use essa opção quando quiser toorun um trabalho Web em um aplicativo web por si só, com nenhum aplicativo web em execução no aplicativo web de saudação. Talvez você queira toodo isso na ordem tooscale capaz de toobe seus recursos de trabalho Web independentemente dos recursos do aplicativo web.
* [Use o modelo de novo projeto de WebJobs de saudação para um projeto do WebJob tooa vinculado web](#createlink)
  
    Crie um projeto que é configurado toodeploy automaticamente como um trabalho Web quando um projeto da web em Olá mesma solução é implantada. Use essa opção quando desejar toorun seu trabalho Web em Olá mesmo aplicativo da web em que você executar Olá relacionados ao aplicativo web.

> [!NOTE]
> modelo de novo projeto de trabalhos Web Hello automaticamente instala pacotes NuGet e inclui o código em *Program.cs* para Olá [SDK do WebJobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs). Se você não quiser toouse Olá SDK do WebJobs, remover ou alterar Olá `host.RunAndBlock` instrução em *Program.cs*.
> 
> 

### <a id="createnolink"></a>Use o modelo de novo projeto de WebJobs de saudação para um trabalho Web independente
1. Clique em **arquivo** > **novo projeto**e, em seguida, em Olá **novo projeto** clique da caixa de diálogo **nuvem**  >   **Azure WebJob (.NET Framework)**.
   
    ![Caixa de diálogo Novo Projeto mostrando o modelo de Trabalho Web](./media/websites-dotnet-deploy-webjobs/np.png)
2. Siga as direções Olá mostradas anteriormente muito[fazer Olá projeto de aplicativo de Console em um projeto de trabalhos Web independente](#convertnolink).

### <a id="createlink"></a>Use o modelo de novo projeto de WebJobs de saudação para um projeto do WebJob tooa vinculado web
1. Projeto de web hello com o botão direito em **Solution Explorer**e, em seguida, clique em **adicionar** > **novo projeto do Azure WebJob**.
   
    ![Entrada de menu de Novo Projeto de Trabalho Web do Azure](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    Olá [adicionar Azure WebJob](#configure) caixa de diálogo é exibida.
2. Olá completa [adicionar Azure WebJob](#configure) caixa de diálogo e clique **Okey**.

## <a id="configure"></a>caixa de diálogo Olá adicionar Azure WebJob
Olá **adicionar Azure WebJob** caixa de diálogo permite que você insira o nome do trabalho Web hello e execute a configuração do modo de seu trabalho Web. 

![Caixa de diálogo Adicionar Trabalho Web do Azure](./media/websites-dotnet-deploy-webjobs/aaw2.png)

campos de saudação nesta caixa de diálogo correspondem toofields em Olá **novo trabalho** caixa de diálogo de saudação Portal do Azure. Para obter mais informações, consulte [Executar tarefas em segundo plano com o Trabalhos Web](web-sites-create-web-jobs.md).

> [!NOTE]
> * Para obter informações sobre a implantação de linha de comando, consulte [Habilitando a entrega de linha de comando ou contínua de Trabalhos Web do Azure](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).
> * Se você implantar um trabalho Web e, em seguida, decide toochange tipo de saudação do trabalho Web e reimplantação, você precisará de arquivo do toodelete Olá settings.json publicar webjobs. Isso fará com que o Visual Studio Mostrar Olá opções de publicação novamente, para que você pode alterar o tipo de saudação do WebJob.
> * Se você implantar um trabalho Web e depois altera Olá modo de execução de contínuo toonon contínua ou vice-versa, o Visual Studio cria um novo trabalho de Web no Azure ao reimplantar. Se você alterar outras configurações de agendamento, mas deixe executar modo Olá mesmo ou alternar entre programada e sob demanda, atualizações do Visual Studio Olá trabalho existente em vez de criar um novo.
> 
> 

## <a id="publishsettings"></a>webjob-publish-settings.json
Quando você configura um aplicativo de Console para a implantação de trabalhos Web, o Visual Studio instala Olá [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet pacote e armazena informações de agendamento um *settings.json publicar webjob*  arquivo no projeto Olá *propriedades* pasta do projeto de trabalhos Web hello. Aqui está um exemplo desse arquivo:

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

É possível editar esse arquivo diretamente, e o Visual Studio fornece o IntelliSense. esquema de arquivo Hello é armazenada em [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) e pode ser exibido lá.  

## <a id="webjobslist"></a>webjobs-list.json
Quando você vincula um projeto do projeto habilitadas WebJobs tooa da web, Visual Studio armazena o nome de saudação do projeto de trabalhos Web hello em um *webjobs list.json* arquivo do projeto da web hello *propriedades* pasta. lista de saudação pode conter vários projetos de trabalhos Web, conforme mostrado no exemplo a seguir de saudação:

        {
          "$schema": "http://schemastore.org/schemas/json/webjobs-list.json",
          "WebJobs": [
            {
              "filePath": "../ConsoleApplication1/ConsoleApplication1.csproj"
            },
            {
              "filePath": "../WebJob1/WebJob1.csproj"
            }
          ]
        }

É possível editar esse arquivo diretamente, e o Visual Studio fornece o IntelliSense. esquema de arquivo Hello é armazenada em [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) e pode ser exibido lá.

## <a id="deploy"></a>Implantar um projeto de Trabalhos Web
Um projeto de WebJobs que você vinculou projeto da web de tooa implanta automaticamente com o projeto da web de saudação. Para obter informações sobre a implantação de projeto da web, consulte [como toodeploy tooWeb aplicativos](web-sites-deploy.md).

toodeploy um projeto de trabalhos Web por si só, clique com botão direito Olá em **Solution Explorer** e clique em **Publicar como Azure WebJob...** . 

![Publicar como Trabalho Web do Azure](./media/websites-dotnet-deploy-webjobs/paw.png)

Para um trabalho Web independente, Olá mesmo **Publicar Web** assistente que é usado para projetos da web é exibido, mas com menos toochange disponíveis de configurações.

## <a id="nextsteps"></a>Próximas etapas
Este artigo explicou como toodeploy trabalhos Web usando o Visual Studio. Para obter mais informações sobre como toodeploy WebJobs do Azure, consulte [WebJobs do Azure - recomendado recursos - implantação](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).

