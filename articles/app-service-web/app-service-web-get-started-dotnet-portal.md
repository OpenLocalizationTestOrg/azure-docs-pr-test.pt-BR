---
title: "aaaDeploy um aplicativo web de Umbraco Olá portal do Azure em cinco minutos | Microsoft Docs"
description: "Saiba como é fácil toorun os aplicativos web no serviço de aplicativo ao implantar um aplicativo ASP.NET de exemplo. Veja os resultados imediatamente."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: cephalin
ms.openlocfilehash: 6da45f99b3043a3684e3d99c14e6443d597b5212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-umbraco-web-app-in-hello-azure-portal-in-five-minutes"></a>Implantar um aplicativo web de Umbraco Olá portal do Azure em cinco minutos

Esse tutorial ajudará você a implantar n [Umbraco](https://our.umbraco.org/) muito de aplicativo da web[do serviço de aplicativo do Azure](../app-service/app-service-value-prop-what-is.md) em minutos.

![Aplicativo do Umbraco](./media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a>Pré-requisitos
Você precisa de uma conta do Microsoft Azure. Se não tiver uma conta, você poderá [inscrever-se para uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ou [ativar seus benefícios de assinante do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

> [!NOTE]
> Você pode [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/) sem uma conta do Azure. Criar um aplicativo de início e explorá-la para a hora de tooan – nenhum cartão de crédito necessários, nenhum investimento.
> 
> 

## <a name="deploy-hello-aspnet-app"></a>Implantar o aplicativo de saudação do ASP.NET
1. Entrar toohello [portal do Azure](https://portal.azure.com).

2. Abra [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).

    O link é um atalho tooimmediately configurar um novo aplicativo Umbraco Olá portal do Azure.

3. Em **Nome do aplicativo**, digite um nome do aplicativo Web. Você verá uma marca de seleção verde na caixa Olá se nome hello é exclusivo no hello `azurewebsites.net` domínio.
   
5. Em **grupo de recursos**, clique em **criar novo** toocreate um novo [grupo de recursos](../azure-resource-manager/resource-group-overview.md), dê a ele um nome.

7. Clique em **Plano do Serviço de Aplicativo/Local** > **Criar Novo**. Configurar Olá [plano de serviço de aplicativo](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) conforme mostrado:

    - Em **plano de serviço de aplicativo**, o nome do tipo hello desejado.
    - Em **local**, escolha um local toohost seu plano.
    - Clique em **Tipo de preço** e selecione **F1 Gratuito** ou outra camada que atenda a você e, em seguida, clique em **Selecionar**.
    - Clique em **OK**.

    Sua configuração Umbraco CMS deve agora ser semelhante Olá captura de tela a seguir:

    ![Configuração em andamento – primeiro Umbraco no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. Clique em **Banco de Dados SQL** > **Criar um novo banco de dados**. Configure Olá banco de dados SQL, conforme mostrado:

    - Em **Nome**, digite um nome, como **myDB**.
    - Clique em **Tipo de preço** e selecione **F Gratuito** ou outra camada que atenda a você e, em seguida, clique em **Selecionar**.
    - Clique em **Servidor de destino** > **Criar um novo servidor**. Configure o servidor de banco de dados de saudação conforme mostrado:

        - Em **Nome do servidor**, digite um nome do servidor. Você verá uma marca de seleção verde na caixa Olá se nome hello é exclusivo no hello `.database.windows.net` domínio.
        - Em **logon de administrador de servidor**, Olá tipo desejado de nome de usuário administrador.
        - Em **senha** e **Confirmar senha**, digite a senha desejada hello.
        - No local, selecione Olá mesmo local que você pode usar para o aplicativo web de saudação.
        - Certifique-se de **permitir servidor de tooaccess de serviços do azure** está selecionado.
        - Clique em **Selecionar**.
    
    - Clique em **Selecionar**.

13. Clique em **configurações de aplicativo da Web**, especificar o nome de usuário de banco de dados de saudação e a senha e clique em **Okey**.

    Sua configuração Umbraco CMS deve agora ser semelhante Olá captura de tela a seguir:

    ![Configuração concluída – primeiro Umbraco no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. Clique em **Criar**.
    
    Agora o Azure cria seu aplicativo do Umbraco com base em sua configuração. Você deve ver uma notificação **Implantação iniciada...**.

    ![Implantação bem-sucedida – primeiro Umbraco no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a>Iniciar e gerenciar seu aplicativo Web Umbraco

Quando o Azure concluir a implantação do aplicativo você verá outra notificação.

![Implantação bem-sucedida – primeiro Umbraco no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. Clique em notificação de saudação. Se perdidas, você sempre pode acessá-lo clicando sino de notificação de saudação (![abaixo de notificação - Umbraco primeiro no serviço de aplicativo do Azure](./media/app-service-web-get-started-dotnet-portal/notification.png)).

    Agora você deve ver a [folha](../azure-resource-manager/resource-group-portal.md#manage-resources) de gerenciamento de seu aplicativo Web (*folha*: uma página de portal que se abre horizontalmente).

3. Na parte superior de saudação da página de visão geral de saudação, clique em **procurar**.
   
    ![Procurar – primeiro Umbraco no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-dotnet-portal/browse.png)

    Agora você vê Olá Umbraco **bem-vindo** página. Configurar Olá Umbraco instalação e iniciar a reprodução com ele!

    ![Configuração do Umbraco – primeiro Umbraco no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a>Próximas etapas
* [Implantar um tooAzure de aplicativo web do ASP.NET do serviço de aplicativo, usando o Visual Studio](app-service-web-get-started-dotnet.md) -Saiba como toocreate um novo aplicativo web do Azure no Visual Studio, usando qualquer um dos Olá incluído modelos do aplicativo.
* [Implantar seu código tooAzure do serviço de aplicativo](web-sites-deploy.md)-Saiba como toodeploy do FTP ou da origem controlar repositórios.
* [Adicionar funcionalidade tooyour primeiro aplicativo web](app-service-web-get-started-2.md) -leve toohello seu aplicativo do Azure próximo nível. Autenticar os usuários. Dimensione-o com base na demanda. Configure alguns alertas de desempenho. Tudo isso com apenas alguns cliques.
