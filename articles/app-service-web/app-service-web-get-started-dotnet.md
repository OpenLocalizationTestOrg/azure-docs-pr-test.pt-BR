---
title: aaaCreate uma ASP.NET web aplicativo no Azure | Microsoft Docs
description: "Saiba como aplicativo da web de aplicativos web de toorun no serviço de aplicativo do Azure com a implantação padrão de saudação ASP.NET."
services: app-service\web
documentationcenter: 
author: cephalin
manager: wpickett
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 06/14/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: eec916b3c32b6c8b68083177938c5c822a9782b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-in-azure"></a>Criar um aplicativo Web ASP.NET no Azure

Os [aplicativos Web do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fornecem um serviço de hospedagem na Web altamente escalonável,com aplicação automática de patches.  Este guia de início rápido mostra como toodeploy primeiro ASP.NET web aplicativo tooAzure aplicativos Web. Quando terminar, você terá um grupo de recursos que consiste em um plano do Serviço de Aplicativo e um aplicativo Web do Azure com um aplicativo Web implantado.

Assista a este guia de início rápido na ação toosee vídeo hello e, em seguida, execute Olá etapas por conta própria toopublish seu primeiro aplicativo .NET no Azure.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-NET-Developers/Create-a-NET-app-in-Azure-Quickstart/player]

## <a name="prerequisites"></a>Pré-requisitos

toocomplete este tutorial:

* Instalar [2017 do Visual Studio](https://www.visualstudio.com/downloads/) com hello cargas de trabalho a seguir:
    - **Desenvolvimento Web e do ASP.NET**
    - **Desenvolvimento do Azure**

    ![ASP.NET, desenvolvimento Web e desenvolvimento do Azure (na Web e na nuvem)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-an-aspnet-web-app"></a>Criar um aplicativo Web ASP .NET

No Visual Studio, crie um projeto selecionando **Arquivo > Novo > Projeto**. 

Em Olá **novo projeto** caixa de diálogo, selecione **Visual C# > Web > aplicativo Web do ASP.NET (.NET Framework)**.

Nome do aplicativo hello _myFirstAzureWebApp_e, em seguida, selecione **Okey**.
   
![Caixa de diálogo Novo Projeto](./media/app-service-web-get-started-dotnet/new-project.png)

Você pode implantar qualquer tipo de tooAzure de aplicativo web ASP.NET. Para este guia de início rápido, selecione Olá **MVC** modelo e certifique-se de autenticação está definida muito**sem autenticação**.
      
Selecione **OK**.

![Caixa de diálogo Novo Projeto ASP .NET](./media/app-service-web-get-started-dotnet/select-mvc-template.png)

No menu de saudação, selecione **Depurar > Iniciar sem depuração** toorun Olá web aplicativo localmente.

![Executar o aplicativo localmente](./media/app-service-web-get-started-dotnet/local-web-app.png)

## <a name="publish-tooazure"></a>Publicar tooAzure

Em Olá **Solution Explorer**, Olá do botão direito do mouse **myFirstAzureWebApp** do projeto e selecione **publicar**.

![Publicar no Gerenciador de Soluções](./media/app-service-web-get-started-dotnet/solution-explorer-publish.png)

Verifique se o **Serviço de Aplicativo do Microsoft Azure** está selecionado e clique em **Publicar**.

![Publicar na página de visão geral do projeto](./media/app-service-web-get-started-dotnet/publish-to-app-service.png)

Isso abre o hello **criar serviço de aplicativo** caixa de diálogo, o que ajuda a criar todos os Olá recursos do Azure necessários toorun Olá ASP.NET web aplicativo no Azure.

## <a name="sign-in-tooazure"></a>Entrar tooAzure

Em Olá **criar serviço de aplicativo** caixa de diálogo, selecione **adicionar uma conta**e entre tooyour assinatura do Azure. Se você já entrou, conta de saudação select contendo Olá desejado assinatura na lista suspensa de saudação.

> [!NOTE]
> Se você já estiver conectado, não selecione **Criar** ainda.
>
>
   
![Entrar tooAzure](./media/app-service-web-get-started-dotnet/sign-in-azure.png)

## <a name="create-a-resource-group"></a>Criar um grupo de recursos

[!INCLUDE [resource group intro text](../../includes/resource-group.md)]

Avançar muito**grupo de recursos**, selecione **novo**.

Grupo de recursos do nome hello **myResourceGroup** e selecione **Okey**.

## <a name="create-an-app-service-plan"></a>Criar um plano de Serviço de Aplicativo

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Avançar muito**plano do serviço de aplicativo**, selecione **novo**. 

Em Olá **configurar o plano de serviço de aplicativo** caixa de diálogo, use Olá configurações na tabela Olá Olá captura de tela a seguir.

![Criar plano de Serviço de Aplicativo](./media/app-service-web-get-started-dotnet/configure-app-service-plan.png)

| Configuração | Valor sugerido | Descrição |
|-|-|-|
|Plano do Serviço de Aplicativo| myAppServicePlan | Nome da saudação plano de serviço de aplicativo. |
| Local | Europa Ocidental | Olá datacenter onde o aplicativo da web de saudação está hospedado. |
| Tamanho | Grátis | O [Tipo de preço](https://azure.microsoft.com/pricing/details/app-service/) determina os recursos de hospedagem. |

Selecione **OK**.

## <a name="create-and-publish-hello-web-app"></a>Criar e publicar o aplicativo da web de saudação

Em **nome do aplicativo Web**, digite um nome exclusivo do aplicativo (os caracteres válidos são `a-z`, `0-9`, e `-`), ou aceite Olá nome exclusivo gerado automaticamente. Olá URL do aplicativo web de saudação é `http://<app_name>.azurewebsites.net`, onde `<app_name>` é o nome do aplicativo web.

Selecione **criar** toostart criando Olá recursos do Azure.

![Configurar o nome do aplicativo Web](./media/app-service-web-get-started-dotnet/web-app-name.png)

Após a conclusão do assistente Olá, ela publica Olá ASP.NET web aplicativo tooAzure e, em seguida, inicia Olá aplicativo no navegador padrão de saudação.

![Aplicativo Web ASP.NET publicado no Azure](./media/app-service-web-get-started-dotnet/published-azure-web-app.png)

nome do aplicativo web Hello especificado no hello [criar e publicar etapa](#create-and-publish-the-web-app) é usado como Olá prefixo de URL no formato Olá `http://<app_name>.azurewebsites.net`.

Parabéns, seu primeiro aplicativo Web ASP.NET está em execução no Serviço de Aplicativo do Azure.

## <a name="update-hello-app-and-redeploy"></a>Aplicativo de saudação de atualização e reimplantação

De saudação **Solution Explorer**, abra _Views\Home\Index.cshtml_.

Localize Olá `<div class="jumbotron">` HTML marca superior hello e substitua todo o elemento Olá Olá código a seguir:

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how toodeploy a .NET app tooAzure App Service.</p>
</div>
```

tooredeploy tooAzure, Olá atalho **myFirstAzureWebApp** project no **Solution Explorer** e selecione **publicar**.

Olá página de publicação, selecione **publicar**.

Quando a publicação for concluído, o Visual Studio inicia uma URL de toohello do navegador do aplicativo web de saudação.

![Aplicativo Web ASP.NET atualizado no Azure](./media/app-service-web-get-started-dotnet/updated-azure-web-app.png)

## <a name="manage-hello-azure-web-app"></a>Gerenciar o aplicativo da web do Azure de saudação

Vá toohello <a href="https://portal.azure.com" target="_blank">portal do Azure</a> toomanage Olá web app.

No menu à esquerda do hello, selecione **serviços de aplicativos**e, em seguida, selecione o nome de saudação do seu aplicativo web do Azure.

![Aplicativo de web de tooAzure de navegação do Portal](./media/app-service-web-get-started-dotnet/access-portal.png)

A página Visão Geral do seu aplicativo Web é exibida. Aqui você pode executar tarefas básicas de gerenciamento como procurar, parar, iniciar, reiniciar e excluir. 

![Folha Serviço de Aplicativo no portal do Azure](./media/app-service-web-get-started-dotnet/web-app-blade.png)

menu esquerdo Olá fornece diferentes páginas para configurar seu aplicativo. 

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [ASP.NET com o Banco de dados SQL](app-service-web-tutorial-dotnet-sqldatabase.md)
