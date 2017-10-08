---
title: "aaaCreate um aplicativo web do WordPress no serviço de aplicativo do Azure | Microsoft Docs"
description: "Saiba como toocreate um novo Azure web aplicativo para um blog do WordPress usando Olá Portal do Azure."
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 193ae094-0d7c-4749-a09b-ff4b1240149e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 3a95fcb6732c15a8200921ce474b6dde2298dec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-wordpress-web-app-in-azure-app-service"></a>Criar um aplicativo Web do WordPress no Serviço de Aplicativo do Azure
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

Este tutorial mostra como toodeploy um blog do WordPress do site do hello Azure Marketplace.

Quando você concluiu o tutorial de saudação terá seu próprio site de blog do WordPress para cima e em execução na nuvem hello.

![Site do WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

Você aprenderá a:

* Como toofind um modelo de aplicativo hello Azure Marketplace.
* Como toocreate um aplicativo web no aplicativo do Azure que serviço baseado no modelo de saudação.
* Como tooconfigure as configurações de serviço de aplicativo do Azure para Olá novo web app e o banco de dados.

Hello Azure Marketplace disponibiliza uma ampla gama de aplicativos web populares desenvolvidos pela Microsoft, outras empresas e iniciativas de software de código aberto. Olá os aplicativos web são criados em uma ampla variedade de estruturas populares, como [PHP](/develop/nodejs/) neste exemplo WordPress, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), e [Python](/develop/python/), tooname alguns. toocreate um aplicativo web do hello Azure Marketplace Olá somente software que você precisa é saudação do navegador que você usa para Olá [Portal do Azure](https://portal.azure.com/). 

site de WordPress Olá que você implantar este tutorial usa MySQL Olá de banco de dados. Se você quiser usar tooinstead banco de dados SQL do banco de dados de saudação, consulte [Nami projeto](http://projectnami.org/). **Projeto Nami** também está disponível por meio de saudação Marketplace.

> [!NOTE]
> toocomplete neste tutorial, você precisa de uma conta do Microsoft Azure. Se não tiver uma conta, você poderá [ativar os benefícios de assinante do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) ou [inscrever-se em uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
> 
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de você se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/). Lá, você poderá criar imediatamente um aplicativo Web de curta duração inicial no Serviço de Aplicativo – sem exigência de cartão de crédito e sem compromissos.
> 
> 

## <a name="select-wordpress-and-configure-for-azure-app-service"></a>Selecionar WordPress e configurar o Serviço de Aplicativo do Azure
1. Faça logon no toohello [Portal do Azure](https://portal.azure.com/).
2. Clique em **Novo**.
   
    ![Criar Novo][5]
3. Procure **WordPress** e clique em **WordPress**. Se você quiser toouse banco de dados SQL em vez do MySQL, procure **Nami projeto**.
   
    ![WordPress da lista][7]
4. Depois de ler a descrição de saudação do aplicativo de WordPress hello, clique em **criar**.
   
    ![Criar](./media/web-sites-php-web-site-gallery/create.png)
5. Insira um nome para o aplicativo web de saudação em Olá **aplicativo Web** caixa.
   
    Esse nome deve ser exclusivo no domínio azurewebsites.net de saudação porque Olá URL do aplicativo web de Olá {name}. azurewebsites.net. Se o nome de saudação não for exclusivo, um ponto de exclamação vermelho é exibido na caixa de texto de saudação.
6. Se você tiver mais de uma assinatura, escolha Olá aquele que você deseja toouse. 
7. Selecione um **Grupo de Recursos** ou crie um novo.
   
    Para saber mais sobre os grupos de recursos, confira [Visão geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
8. Selecione um **Plano/Local do Serviço de Aplicativo** ou crie um novo.
   
    Para saber mais sobre os planos do Serviço de Aplicativo, confira [Visão geral dos planos do Serviço de Aplicativo do Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)    
9. Clique em **banco de dados**e, em seguida, em Olá **novo banco de dados MySQL** folha fornecem valores de saudação necessárias para configurar o banco de dados MySQL.
   
    a. Digite um novo nome ou deixe o nome padrão de saudação.
   
    b. Deixe Olá **tipo de banco de dados** definido muito**compartilhado**.
   
    c. Escolha Olá mesmo local como Olá aquele que você escolheu para o aplicativo web de saudação.
   
    d. Escolha uma camada de preços. Para este tutorial, Mercury (gratuito, com conexões e espaço em disco mínimos permitidos ) é adequado.
10. Em Olá **novo banco de dados MySQL** folha, clique em **Okey**. 
11. Em Olá **WordPress** folha, aceite os termos legais hello e, em seguida, clique em **criar**. 
    
     ![Configurar aplicativo Web](./media/web-sites-php-web-site-gallery/configure.png)
    
     Serviço de aplicativo do Azure cria Olá web app, normalmente em menos de um minuto. Você pode assistir andamento Olá clicando o ícone de sino Olá na parte superior de saudação da página de portal hello.
    
     ![Indicador de progresso](./media/web-sites-php-web-site-gallery/progress.png)

## <a name="launch-and-manage-your-wordpress-web-app"></a>Inicie e gerencie seu aplicativo Web do WordPress
1. Depois da criação do aplicativo web Olá, navegue no hello Azure Portal toohello grupo de recursos no qual você criou o aplicativo hello e você pode ver Olá web app e o banco de dados de saudação.
   
    Olá adicional do recurso com ícone de lâmpada Olá é [Application Insights](/services/application-insights/), que fornece serviços de monitoramento para seu aplicativo web.
2. Em Olá **grupo de recursos** folha, clique em linha de aplicativo web hello.
   
    ![Configurar aplicativo Web](./media/web-sites-php-web-site-gallery/resourcegroup.png)
3. Na folha de saudação do aplicativo Web, clique em **procurar**.
   
    ![URL do site][browse]
4. Em Olá WordPress **bem-vindo** página, insira as informações de configuração do hello exigidas pelo WordPress e, em seguida, clique em **instalar o WordPress**.
   
    ![Configurar WordPress](./media/web-sites-php-web-site-gallery/wpconfigure.png)
5. Faça logon usando credenciais Olá criado no hello **bem-vindo** página.  
6. A página de Painel do site é aberta.    
   
    ![Site do WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

## <a name="next-steps"></a>Próximas etapas
Você viu como toocreate e implantar um aplicativo web do PHP da Galeria de saudação. Para obter mais informações sobre como usar PHP no Azure, consulte Olá [Centro de desenvolvedores PHP](/develop/php/).

Para obter mais informações sobre como toowork com aplicativos de Web do serviço de aplicativo, consulte os links de saudação em Olá lado esquerdo da página hello (para janelas de navegador ampla) ou na parte superior de saudação da página de saudação (para janelas de navegador estreita). 

## <a name="whats-changed"></a>O que mudou
* Uma alteração de toohello do guia de sites tooApp serviço, consulte [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714).

[5]: ./media/web-sites-php-web-site-gallery/startmarketplace.png
[7]: ./media/web-sites-php-web-site-gallery/search-web-app.png
[browse]: ./media/web-sites-php-web-site-gallery/browse-web.png
