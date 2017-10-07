---
title: "aaaAzure credenciais de implantação do serviço de aplicativo | Microsoft Docs"
description: "Saiba como toouse Olá credenciais de implantação do serviço de aplicativo do Azure."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/05/2016
ms.author: dariagrigoriu
ms.openlocfilehash: d6f9f5cc1b62a17c42643266f4c9490f827c63f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a>Configurar as credenciais de implantação do Serviço de Aplicativo do Azure
O [Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) oferece suporte a dois tipos de credenciais para a [implantação local do Git](app-service-deploy-local-git.md) e a [implantação de FTP/S](app-service-deploy-ftp.md). Eles não são Olá mesmo que suas credenciais do Active Directory do Azure.

* **Credenciais de usuário de nível**: um conjunto de credenciais para toda a conta do Azure hello. Ele pode ser usado toodeploy tooApp serviço para qualquer aplicativo, em qualquer assinatura, Olá conta do Azure tem permissão tooaccess. Esses são o conjunto de credenciais do saudação padrão que você configurar no **serviços de aplicativos** > **&lt;app_name >** > **decredenciaisdeimplantação**. Isso também é Olá conjunto padrão que é exposto no portal de saudação GUI (como Olá **visão geral** e **propriedades** do seu aplicativo [folha de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources)).

    > [!NOTE]
    > Quando você delegar acesso tooAzure recursos por meio do controle de acesso com base da função (RBAC) ou permissões de coadministrador, cada usuário do Azure que recebe acesso tooan aplicativo pode usar suas credenciais de nível de usuário pessoais até que o acesso é revogado. Essas credenciais de implantação não devem ser compartilhadas com outros usuários do Azure.
    >
    >

* **Credenciais de nível de aplicativo**: um conjunto de credenciais para cada aplicativo. Ele pode ser usado toodeploy toothat somente do aplicativo. credenciais de saudação para cada aplicativo é gerado automaticamente na criação do aplicativo e se encontra em um aplicativo hello perfil de publicação. Você não pode configurar manualmente as credenciais do hello, mas você pode redefini-los para um aplicativo a qualquer momento.

    > [!NOTE]
    > Em ordem toogive alguém acessar credenciais toothese por meio de funções com base em acesso RBAC (controle), você precisa toomake-los Colaborador ou superior no hello aplicativo Web. Os leitores não são permitidos toopublish e, portanto, não é possível acessar essas credenciais.
    >
    >

## <a name="userscope"></a>Definir e redefinir credenciais de usuário

Você pode configurar as credenciais de usuário na [folha de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources) de qualquer aplicativo. Independentemente em qual aplicativo você configurar essas credenciais, ela se aplica a aplicativos tooall e para todas as assinaturas do Azure da conta. 

tooconfigure suas credenciais de nível de usuário:

1. Em Olá [portal do Azure](https://portal.azure.com), clique em serviço de aplicativo >  **&lt;any_app >** > **credenciais de implantação**.

    > [!NOTE]
    > No portal de saudação, você deve ter pelo menos um aplicativo antes de poder acessar a folha de credenciais de implantação hello. No entanto, com hello [CLI do Azure](app-service-web-app-azure-resource-manager-xplat-cli.md), você pode configurar credenciais de nível de usuário sem um aplicativo existente.

2. Configurar Olá nome de usuário e senha e, em seguida, clique em **salvar**.

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

Depois que você tiver definido suas credenciais de implantação, você pode encontrar hello *Git* nome de usuário de implantação em seu aplicativo **visão geral**,

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

e o nome de usuário de implantação de *FTP* nas **Propriedades** de seu aplicativo.

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> O Azure não mostra sua senha de implantação de usuário. Se você esquecer a senha de hello, não é possível recuperá-la. No entanto, você pode redefinir suas credenciais, seguindo as etapas de saudação nesta seção.
>
>  

## <a name="appscope"></a>Definir e redefinir credenciais de aplicativo
Para cada aplicativo no serviço de aplicativo, suas credenciais de nível de aplicativo são armazenadas no hello perfil de publicação de XML.

credenciais de nível de aplicativo de saudação tooget:

1. Em Olá [portal do Azure](https://portal.azure.com), clique em serviço de aplicativo >  **&lt;any_app >** > **visão geral**.

2. Clique em **...Mais** > **Obter perfil de publicação** e inicie o download de um arquivo .PublishSettings.

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. Olá aberto. PublishSettings de arquivos e localizar Olá `<publishProfile>` marca com atributo Olá `publishMethod="FTP"`. Em seguida, obtenha seus atributos `userName` e `password`.
São as credenciais de nível de aplicativo hello.

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    Credenciais de usuário de nível toohello semelhante, nome de usuário de implantação Olá FTP está no formato de saudação do `<app_name>\<username>`, e o nome de usuário de implantação de Git Olá é apenas `<username>` sem saudação anterior `<app_name>\`.

credenciais de nível de aplicativo de saudação tooreset:

1. Em Olá [portal do Azure](https://portal.azure.com), clique em serviço de aplicativo >  **&lt;any_app >** > **visão geral**.

2. Clique em **...Mais** > **Redefinir perfil de publicação**. Clique em **Sim** tooconfirm Olá redefinir.

    a ação reset Olá invalida qualquer baixados anteriormente. Arquivos PublishSettings.

## <a name="next-steps"></a>Próximas etapas

Descubra como toouse toodeploy essas credenciais seu aplicativo do [Git local](app-service-deploy-local-git.md) ou usando [FTP/S](app-service-deploy-ftp.md).
