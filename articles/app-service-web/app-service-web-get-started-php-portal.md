---
title: aaaDeploy um aplicativo de WordPress no hello portal do Azure em cinco minutos | Microsoft Docs
description: "Saiba como é fácil toorun os aplicativos web no serviço de aplicativo ao implantar um aplicativo de WordPress. Veja os resultados imediatamente."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: cephalin
ms.openlocfilehash: 4cd26bbacf89657997847ded1284e472288ddebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-wordpress-app-in-hello-azure-portal-in-five-minutes"></a>Implantar um aplicativo de WordPress no portal do Azure de saudação em cinco minutos

Este tutorial mostra como toodeploy seu primeiro [WordPress](https://wordpress.org/) muito de aplicativo da web[do serviço de aplicativo do Azure](../app-service/app-service-value-prop-what-is.md) em minutos.

![Site do WordPress](./media/app-service-web-get-started-php-portal/wpdashboard.png)

## <a name="prerequisites"></a>Pré-requisitos
Você precisa de uma conta do Microsoft Azure. Se não tiver uma conta, você poderá [inscrever-se para uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ou [ativar seus benefícios de assinante do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

> [!NOTE]
> Você pode [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/) sem uma conta do Azure. Criar um aplicativo de início e explorá-la para a hora de tooan – nenhum cartão de crédito necessários, nenhum investimento.
> 
> 

## <a name="deploy-hello-wordpress-app"></a>Implantar o aplicativo de WordPress Olá
1. Entrar toohello [portal do Azure](https://portal.azure.com).

2. Abra [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).

    O link é um atalho tooimmediately configurar um novo aplicativo de WordPress Olá portal do Azure.

3. Em **Nome do aplicativo**, digite um nome do aplicativo Web. Você verá uma marca de seleção verde na caixa Olá se nome hello é exclusivo no hello `azurewebsites.net` domínio.
   
5. Em **grupo de recursos**, clique em **criar novo** toocreate um novo [grupo de recursos](../azure-resource-manager/resource-group-overview.md), dê a ele um nome.

6. Em **Provedor de Banco de Dados**, selecione **CleaDB**.

7. Clique em **Plano do Serviço de Aplicativo/Local** > **Criar Novo**. Configurar Olá [plano de serviço de aplicativo](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) conforme mostrado:

    - Em **plano de serviço de aplicativo**, o nome do tipo hello desejado.
    - Em **local**, escolha um local toohost seu plano.
    - Clique em **Tipo de preço** e selecione **F1 Gratuito** ou outra camada que atenda a você e, em seguida, clique em **Selecionar**.
    - Clique em **OK**.

8. Clique em **Banco de Dados** > **Criar Novo**. Configure Olá banco de dados SQL, conforme mostrado:

    - Em **Nome do Banco de Dados**, digite um nome de banco de dados. 
    - Em **local**, escolha Olá mesmo local que Olá plano de serviço de aplicativo.
    - Clique em **Tipo de preço** e selecione **Mercúrio** ou outra camada que atenda a você e, em seguida, clique em **Selecionar**.
    - Clique em **Termos Legais** e clique em **Comprar**.
    - Clique em **OK**.

9. Clique em **Criar**.

    Agora o Azure cria seu aplicativo do WordPress com base em sua configuração. Você deve ver uma notificação **Implantação iniciada...**.

    ![Implantação iniciada – primeiro WordPress no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-php-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-wordpress-web-app"></a>Inicie e gerencie seu aplicativo Web do WordPress

Quando o Azure concluir a implantação do aplicativo você verá outra notificação.

![Implantação bem-sucedida – primeiro WordPress no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-php-portal/deployment-succeeded.png)

1. Clique em notificação de saudação. Se perdidas, você sempre pode acessá-lo clicando sino de notificação de saudação (![abaixo de notificação - WordPress primeiro no serviço de aplicativo do Azure](./media/app-service-web-get-started-dotnet-portal/notification.png)).

    Agora você deve ver a [folha](../azure-resource-manager/resource-group-portal.md#manage-resources) de gerenciamento de seu aplicativo Web (*folha*: uma página de portal que se abre horizontalmente).

3. Na parte superior de saudação da página de visão geral de saudação, clique em **procurar**.
   
    ![Procurar – primeiro WordPress no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-php-portal/browse.png)

    Agora você vê Olá WordPress **bem-vindo** página. Configurar a instalação do WordPress hello e iniciar a reprodução com ele!

    ![Configuração do WordPress – primeiro WordPress no Serviço de Aplicativo do Azure](./media/app-service-web-get-started-php-portal/wordpress-config.png)
    
## <a name="next-steps"></a>Próximas etapas
* [Criar, configurar e implantar um tooAzure de aplicativo web Laravel](app-service-web-php-get-started.md) -aprender as habilidades básicas Olá você precisa toorun qualquer aplicativo da web PHP no Azure, como:

    * Criar e configurar aplicativos no Azure do PowerShell/Bash.
    * Definir a versão do PHP.
    * Use um arquivo de início que não está no diretório de aplicativo hello raiz.
    * Habilite a automação do Composer.
    * Acessar variáveis de ambiente específicas.
    * Solucionar erros comuns.

* [Implantar seu código tooAzure do serviço de aplicativo](web-sites-deploy.md)-Saiba como toodeploy do FTP ou da origem controlar repositórios.
* [Adicionar funcionalidade tooyour primeiro aplicativo web](app-service-web-get-started-2.md) -leve toohello seu aplicativo do Azure próximo nível. Autenticar os usuários. Dimensione-o com base na demanda. Configure alguns alertas de desempenho. Tudo isso com apenas alguns cliques.
