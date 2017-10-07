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
# <a name="configure-deployment-credentials-for-azure-app-service"></a><span data-ttu-id="93aab-103">Configurar as credenciais de implantação do Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="93aab-103">Configure deployment credentials for Azure App Service</span></span>
<span data-ttu-id="93aab-104">O [Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) oferece suporte a dois tipos de credenciais para a [implantação local do Git](app-service-deploy-local-git.md) e a [implantação de FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="93aab-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) supports two types of credentials for [local Git deployment](app-service-deploy-local-git.md) and [FTP/S deployment](app-service-deploy-ftp.md).</span></span> <span data-ttu-id="93aab-105">Eles não são Olá mesmo que suas credenciais do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="93aab-105">These are not hello same as your Azure Active Directory credentials.</span></span>

* <span data-ttu-id="93aab-106">**Credenciais de usuário de nível**: um conjunto de credenciais para toda a conta do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="93aab-106">**User-level credentials**: one set of credentials for hello entire Azure account.</span></span> <span data-ttu-id="93aab-107">Ele pode ser usado toodeploy tooApp serviço para qualquer aplicativo, em qualquer assinatura, Olá conta do Azure tem permissão tooaccess.</span><span class="sxs-lookup"><span data-stu-id="93aab-107">It can be used toodeploy tooApp Service for any app, in any subscription, that hello Azure account has permission tooaccess.</span></span> <span data-ttu-id="93aab-108">Esses são o conjunto de credenciais do saudação padrão que você configurar no **serviços de aplicativos** > **&lt;app_name >** > **decredenciaisdeimplantação**.</span><span class="sxs-lookup"><span data-stu-id="93aab-108">These are hello default credentials set that you configure in **App Services** > **&lt;app_name>** > **Deployment credentials**.</span></span> <span data-ttu-id="93aab-109">Isso também é Olá conjunto padrão que é exposto no portal de saudação GUI (como Olá **visão geral** e **propriedades** do seu aplicativo [folha de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span><span class="sxs-lookup"><span data-stu-id="93aab-109">This is also hello default set that's surfaced in hello portal GUI (such as hello **Overview** and **Properties** of your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span></span>

    > [!NOTE]
    > <span data-ttu-id="93aab-110">Quando você delegar acesso tooAzure recursos por meio do controle de acesso com base da função (RBAC) ou permissões de coadministrador, cada usuário do Azure que recebe acesso tooan aplicativo pode usar suas credenciais de nível de usuário pessoais até que o acesso é revogado.</span><span class="sxs-lookup"><span data-stu-id="93aab-110">When you delegate access tooAzure resources via Role Based Access Control (RBAC) or co-admin permissions, each Azure user that receives access tooan app can use his/her personal user-level credentials until access is revoked.</span></span> <span data-ttu-id="93aab-111">Essas credenciais de implantação não devem ser compartilhadas com outros usuários do Azure.</span><span class="sxs-lookup"><span data-stu-id="93aab-111">These deployment credentials should not be shared with other Azure users.</span></span>
    >
    >

* <span data-ttu-id="93aab-112">**Credenciais de nível de aplicativo**: um conjunto de credenciais para cada aplicativo.</span><span class="sxs-lookup"><span data-stu-id="93aab-112">**App-level credentials**: one set of credentials for each app.</span></span> <span data-ttu-id="93aab-113">Ele pode ser usado toodeploy toothat somente do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="93aab-113">It can be used toodeploy toothat app only.</span></span> <span data-ttu-id="93aab-114">credenciais de saudação para cada aplicativo é gerado automaticamente na criação do aplicativo e se encontra em um aplicativo hello perfil de publicação.</span><span class="sxs-lookup"><span data-stu-id="93aab-114">hello credentials for each app is generated automatically at app creation, and is found in hello app's publish profile.</span></span> <span data-ttu-id="93aab-115">Você não pode configurar manualmente as credenciais do hello, mas você pode redefini-los para um aplicativo a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="93aab-115">You cannot manually configure hello credentials, but you can reset them for an app anytime.</span></span>

    > [!NOTE]
    > <span data-ttu-id="93aab-116">Em ordem toogive alguém acessar credenciais toothese por meio de funções com base em acesso RBAC (controle), você precisa toomake-los Colaborador ou superior no hello aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="93aab-116">In order toogive someone access toothese credentials via Role Based Access Control (RBAC), you need toomake them contributor or higher on hello Web App.</span></span> <span data-ttu-id="93aab-117">Os leitores não são permitidos toopublish e, portanto, não é possível acessar essas credenciais.</span><span class="sxs-lookup"><span data-stu-id="93aab-117">Readers are not allowed toopublish, and hence can't access those credentials.</span></span>
    >
    >

## <span data-ttu-id="93aab-118"><a name="userscope"></a>Definir e redefinir credenciais de usuário</span><span class="sxs-lookup"><span data-stu-id="93aab-118"><a name="userscope"></a>Set and reset user-level credentials</span></span>

<span data-ttu-id="93aab-119">Você pode configurar as credenciais de usuário na [folha de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources) de qualquer aplicativo.</span><span class="sxs-lookup"><span data-stu-id="93aab-119">You can configure your user-level credentials in any app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span> <span data-ttu-id="93aab-120">Independentemente em qual aplicativo você configurar essas credenciais, ela se aplica a aplicativos tooall e para todas as assinaturas do Azure da conta.</span><span class="sxs-lookup"><span data-stu-id="93aab-120">Regardless in which app you configure these credentials, it applies tooall apps and for all subscriptions in your Azure account.</span></span> 

<span data-ttu-id="93aab-121">tooconfigure suas credenciais de nível de usuário:</span><span class="sxs-lookup"><span data-stu-id="93aab-121">tooconfigure your user-level credentials:</span></span>

1. <span data-ttu-id="93aab-122">Em Olá [portal do Azure](https://portal.azure.com), clique em serviço de aplicativo >  **&lt;any_app >** > **credenciais de implantação**.</span><span class="sxs-lookup"><span data-stu-id="93aab-122">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Deployment credentials**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="93aab-123">No portal de saudação, você deve ter pelo menos um aplicativo antes de poder acessar a folha de credenciais de implantação hello.</span><span class="sxs-lookup"><span data-stu-id="93aab-123">In hello portal, you must have at least one app before you can access hello deployment credentials blade.</span></span> <span data-ttu-id="93aab-124">No entanto, com hello [CLI do Azure](app-service-web-app-azure-resource-manager-xplat-cli.md), você pode configurar credenciais de nível de usuário sem um aplicativo existente.</span><span class="sxs-lookup"><span data-stu-id="93aab-124">However, with hello [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), you can configure user-level credentials without an existing app.</span></span>

2. <span data-ttu-id="93aab-125">Configurar Olá nome de usuário e senha e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="93aab-125">Configure hello user name and password, and then click **Save**.</span></span>

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

<span data-ttu-id="93aab-126">Depois que você tiver definido suas credenciais de implantação, você pode encontrar hello *Git* nome de usuário de implantação em seu aplicativo **visão geral**,</span><span class="sxs-lookup"><span data-stu-id="93aab-126">Once you have set your deployment credentials, you can find hello *Git* deployment username in your app's **Overview**,</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

<span data-ttu-id="93aab-127">e o nome de usuário de implantação de *FTP* nas **Propriedades** de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="93aab-127">and and *FTP* deployment username in your app's **Properties**.</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> <span data-ttu-id="93aab-128">O Azure não mostra sua senha de implantação de usuário.</span><span class="sxs-lookup"><span data-stu-id="93aab-128">Azure does not show your user-level deployment password.</span></span> <span data-ttu-id="93aab-129">Se você esquecer a senha de hello, não é possível recuperá-la.</span><span class="sxs-lookup"><span data-stu-id="93aab-129">If you forget hello password, you can't retrieve it.</span></span> <span data-ttu-id="93aab-130">No entanto, você pode redefinir suas credenciais, seguindo as etapas de saudação nesta seção.</span><span class="sxs-lookup"><span data-stu-id="93aab-130">However, you can reset your credentials by following hello steps in this section.</span></span>
>
>  

## <span data-ttu-id="93aab-131"><a name="appscope"></a>Definir e redefinir credenciais de aplicativo</span><span class="sxs-lookup"><span data-stu-id="93aab-131"><a name="appscope"></a>Get and reset app-level credentials</span></span>
<span data-ttu-id="93aab-132">Para cada aplicativo no serviço de aplicativo, suas credenciais de nível de aplicativo são armazenadas no hello perfil de publicação de XML.</span><span class="sxs-lookup"><span data-stu-id="93aab-132">For each app in App Service, its app-level credentials are stored in hello XML publish profile.</span></span>

<span data-ttu-id="93aab-133">credenciais de nível de aplicativo de saudação tooget:</span><span class="sxs-lookup"><span data-stu-id="93aab-133">tooget hello app-level credentials:</span></span>

1. <span data-ttu-id="93aab-134">Em Olá [portal do Azure](https://portal.azure.com), clique em serviço de aplicativo >  **&lt;any_app >** > **visão geral**.</span><span class="sxs-lookup"><span data-stu-id="93aab-134">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="93aab-135">Clique em **...Mais** > **Obter perfil de publicação** e inicie o download de um arquivo .PublishSettings.</span><span class="sxs-lookup"><span data-stu-id="93aab-135">Click **...More** > **Get publish profile**, and download starts for a .PublishSettings file.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. <span data-ttu-id="93aab-136">Olá aberto. PublishSettings de arquivos e localizar Olá `<publishProfile>` marca com atributo Olá `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="93aab-136">Open hello .PublishSettings file and find hello `<publishProfile>` tag with hello attribute `publishMethod="FTP"`.</span></span> <span data-ttu-id="93aab-137">Em seguida, obtenha seus atributos `userName` e `password`.</span><span class="sxs-lookup"><span data-stu-id="93aab-137">Then, get its `userName` and `password` attributes.</span></span>
<span data-ttu-id="93aab-138">São as credenciais de nível de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="93aab-138">These are hello app-level credentials.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    <span data-ttu-id="93aab-139">Credenciais de usuário de nível toohello semelhante, nome de usuário de implantação Olá FTP está no formato de saudação do `<app_name>\<username>`, e o nome de usuário de implantação de Git Olá é apenas `<username>` sem saudação anterior `<app_name>\`.</span><span class="sxs-lookup"><span data-stu-id="93aab-139">Similar toohello user-level credentials, hello FTP deployment username is in hello format of `<app_name>\<username>`, and hello Git deployment username is just `<username>` without hello preceding `<app_name>\`.</span></span>

<span data-ttu-id="93aab-140">credenciais de nível de aplicativo de saudação tooreset:</span><span class="sxs-lookup"><span data-stu-id="93aab-140">tooreset hello app-level credentials:</span></span>

1. <span data-ttu-id="93aab-141">Em Olá [portal do Azure](https://portal.azure.com), clique em serviço de aplicativo >  **&lt;any_app >** > **visão geral**.</span><span class="sxs-lookup"><span data-stu-id="93aab-141">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="93aab-142">Clique em **...Mais** > **Redefinir perfil de publicação**.</span><span class="sxs-lookup"><span data-stu-id="93aab-142">Click **...More** > **Reset publish profile**.</span></span> <span data-ttu-id="93aab-143">Clique em **Sim** tooconfirm Olá redefinir.</span><span class="sxs-lookup"><span data-stu-id="93aab-143">Click **Yes** tooconfirm hello reset.</span></span>

    <span data-ttu-id="93aab-144">a ação reset Olá invalida qualquer baixados anteriormente. Arquivos PublishSettings.</span><span class="sxs-lookup"><span data-stu-id="93aab-144">hello reset action invalidates any previously-downloaded .PublishSettings files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93aab-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="93aab-145">Next steps</span></span>

<span data-ttu-id="93aab-146">Descubra como toouse toodeploy essas credenciais seu aplicativo do [Git local](app-service-deploy-local-git.md) ou usando [FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="93aab-146">Find out how toouse these credentials toodeploy your app from [local Git](app-service-deploy-local-git.md) or using [FTP/S](app-service-deploy-ftp.md).</span></span>
