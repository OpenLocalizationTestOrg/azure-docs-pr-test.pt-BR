---
title: aaaCreate seu primeiro aplicativo web Java no Azure
description: "Saiba como toorun aplicativos web no serviço de aplicativo ao implantar um aplicativo Java básico."
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 8bacfe3e-7f0b-4394-959a-a88618cb31e1
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: quickstart
ms.date: 6/7/2017
ms.author: cephalin;robmcm
ms.custom: mvc
ms.openlocfilehash: 81315c07b5aa84cbec50a17b2cb3914927b19c00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a>Criar seu primeiro aplicativo Web Java no Azure

Olá [aplicativos Web](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) recurso de [do serviço de aplicativo do Azure](../app-service/app-service-value-prop-what-is.md) fornece um serviço de hospedagem web altamente escalonável, aplicação de patch automática. Este guia de início rápido mostra como toodeploy um Java web aplicativo tooApp Service usando Olá [IDE do Eclipse para desenvolvedores Java EE](http://www.eclipse.org/).

!["Hello Azure"! exemplo de aplicativo Web](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a>Pré-requisitos

toocomplete este guia de início rápido, instalar:

* Olá livre [IDE do Eclipse para desenvolvedores Java EE](http://www.eclipse.org/downloads/). Este guia de início rápido usa Eclipse Neon.
* Olá [Kit de ferramentas do Azure para Eclipse](/azure/azure-toolkit-for-eclipse-installation).

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a>Criar um projeto Web dinâmico no Eclipse

No Eclipse, selecione **Arquivo** > **Novo** > **Projeto Web Dinâmico**.

Em Olá **novo projeto Web dinâmico** caixa de diálogo, o projeto de saudação do nome **MyFirstJavaOnAzureWebApp**e selecione **concluir**.
   
![Caixa de diálogo Novo Projeto Web Dinâmico](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a>Adicionar uma página JSP

Se o Explorador de projeto não for exibido, restaure-o.

![Espaço de trabalho do Java EE para Eclipse](./media/app-service-web-get-started-java/pe.png)

No Explorador de projeto, expanda Olá **MyFirstJavaOnAzureWebApp** projeto.
Clique com o botão direito do mouse em **WebContent**e selecione **Novo** > **Arquivo JSP**.

![Menu de um novo arquivo JSP no Explorador de projeto](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

Em Olá **novo arquivo JSP** caixa de diálogo:

* Arquivo de saudação do nome **index.jsp**.
* Selecione **Concluir**.

  ![Caixa de diálogo Novo Arquivo JSP](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

No arquivo JSP Olá substitua Olá `<body></body>` elemento com hello marcação a seguir:

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

Salve alterações de saudação.

## <a name="publish-hello-web-app-tooazure"></a>Publicar Olá web aplicativo tooAzure

No Explorador de projeto, clique com botão direito hello e, em seguida, selecione **Azure** > **Publicar como um aplicativo Web do Azure**.

![Publicar como menu de contexto de Aplicativo Web do Azure](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

Em Olá **Azure entrar** caixa de diálogo, mantenha Olá **interativo** opção e, em seguida, selecione **entrar**.

Siga Olá entrar instruções.

### <a name="deploy-web-app-dialog-box"></a>Caixa de diálogo Implantar Aplicativo Web

Depois de ter entrado tooyour conta do Azure, Olá **implantar aplicativo da Web** caixa de diálogo é exibida.

Selecione **Criar**.

![Caixa de diálogo Implantar Aplicativo Web](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a>Criar a caixa de diálogo Serviço de Aplicativo

Olá **criar serviço de aplicativo** caixa de diálogo é exibida com valores padrão. Olá número **170602185241** mostrado no hello seguinte imagem é diferente na caixa de diálogo.

![Criar a caixa de diálogo Serviço de Aplicativo](./media/app-service-web-get-started-java/cas1.png)

Em Olá **criar serviço de aplicativo** caixa de diálogo:

* Mantenha o nome de saudação gerada para o aplicativo web de saudação. Esse nome deve ser exclusivo no Azure. nome de saudação faz parte do endereço da URL Olá Olá web app. Por exemplo: se o nome do aplicativo web hello é **MyJavaWebApp**, Olá URL é *myjavawebapp.azurewebsites.net*.
* Manter o contêiner do saudação padrão da web.
* Selecione uma assinatura do Azure.
* Em Olá **plano do serviço de aplicativo** guia:

  * **Criar um novo**: mantenha saudação padrão, que é o nome de saudação do hello plano de serviço de aplicativo.
  * **Local**: selecione **Europa Ocidental** ou um local perto de você.
  * **Tipo de preço**: selecione Olá opção livre. Para os recursos, consulte [Preços do Serviço de Aplicativo](https://azure.microsoft.com/pricing/details/app-service/).

   ![Criar a caixa de diálogo Serviço de Aplicativo](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a>Guia Grupo de recursos

Selecione Olá **grupo de recursos** guia. Mantenha o valor de padrão gerado de Olá Olá para grupo de recursos.

![Guia Grupo de recursos](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

Selecione **Criar**.

<!--
### hello JDK tab

Select hello **JDK** tab. Keep hello default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

Olá Kit de ferramentas do Azure cria Olá web app e exibe uma caixa de diálogo de progresso.

![Criar caixa de diálogo Serviço de Aplicativo](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a>Caixa de diálogo Implantar Aplicativo Web

Em Olá **implantar aplicativo da Web** caixa de diálogo, selecione **implantar tooroot**. Se você tiver um aplicativo de serviço no *wingtiptoys.azurewebsites.net* e você não implanta toohello raiz, Olá web aplicativo chamado **MyFirstJavaOnAzureWebApp** é implantado muito *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.

![Caixa de diálogo Implantar Aplicativo Web](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

caixa de diálogo Olá mostra hello Azure JDK e as seleções de contêiner da web.

Selecione **implantar** toopublish Olá web aplicativo tooAzure.

Quando termina de publicação hello, selecione Olá **publicado** link no hello **o Log de atividades do Azure** caixa de diálogo.

![Caixa de diálogo Log de atividades do Azure](./media/app-service-web-get-started-java/aal.png)

Parabéns! Você implantou seu tooAzure de aplicativo web com êxito. 

!["Hello Azure"! exemplo de aplicativo Web](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-hello-web-app"></a>Atualizar o aplicativo web de saudação

Alterar Olá exemplo JSP código tooa mensagem diferente.

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

Salve alterações de saudação.

No Explorador de projeto, clique com botão direito hello e, em seguida, selecione **Azure** > **Publicar como um aplicativo Web do Azure**.

Olá **implantar aplicativo da Web** caixa de diálogo é exibida e mostra Olá do serviço de aplicativo que você criou anteriormente. 

> [!NOTE]
> Selecione **implantar tooroot** cada vez que você publicar.
>

Selecione o aplicativo web de saudação e selecione **implantar**, que publica as alterações de saudação.

Olá quando **publicação** link for exibida, selecione-o aplicativo de web toohello toobrowse e ver as alterações de saudação.

## <a name="manage-hello-web-app"></a>Gerenciar o aplicativo da web de saudação

Vá toohello <a href="https://portal.azure.com" target="_blank">portal do Azure</a> toosee Olá web aplicativo que você criou.

No menu à esquerda do hello, selecione **grupos de recursos**.

![Grupos de tooresource de navegação do Portal](media/app-service-web-get-started-java/rg.png)

Selecione o grupo de recursos de saudação. página Olá mostra os recursos de saudação que você criou neste guia de início rápido.

![Grupo de recursos myResourceGroup](media/app-service-web-get-started-java/rg2.png)

Selecione Olá web app (**170602193915 webapp** em Olá anterior imagem).

Olá **visão geral** página será exibida. Esta página fornece uma exibição como o aplicativo hello está fazendo. Aqui você pode executar tarefas básicas de gerenciamento como procurar, parar, iniciar, reiniciar e excluir. guias de saudação no lado esquerdo de saudação da página Olá mostram Olá configurações diferentes que você pode abrir. 

![Página Serviço de Aplicativo no portal do Azure](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Mapear domínio personalizado](app-service-web-tutorial-custom-domain.md)
