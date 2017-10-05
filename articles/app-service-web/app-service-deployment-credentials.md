---
title: "Credenciais de implantação do Serviço de Aplicativo do Azure | Microsoft Docs"
description: "Saiba como usar as credenciais de implantação do Serviço de Aplicativo do Azure."
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
ms.openlocfilehash: 86a2cd8ae9f97c606a378452e44eec8941700531
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a><span data-ttu-id="21e80-103">Configurar as credenciais de implantação do Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="21e80-103">Configure deployment credentials for Azure App Service</span></span>
<span data-ttu-id="21e80-104">O [Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) oferece suporte a dois tipos de credenciais para a [implantação local do Git](app-service-deploy-local-git.md) e a [implantação de FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="21e80-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) supports two types of credentials for [local Git deployment](app-service-deploy-local-git.md) and [FTP/S deployment](app-service-deploy-ftp.md).</span></span> <span data-ttu-id="21e80-105">Elas não são as mesmas credenciais do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="21e80-105">These are not the same as your Azure Active Directory credentials.</span></span>

* <span data-ttu-id="21e80-106">**Credenciais de nível de usuário**: um conjunto de credenciais para toda a conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="21e80-106">**User-level credentials**: one set of credentials for the entire Azure account.</span></span> <span data-ttu-id="21e80-107">Ele pode ser usado para implantar no Serviço de Aplicativo para qualquer aplicativo e em qualquer assinatura que a conta do Azure tem permissão para acessar.</span><span class="sxs-lookup"><span data-stu-id="21e80-107">It can be used to deploy to App Service for any app, in any subscription, that the Azure account has permission to access.</span></span> <span data-ttu-id="21e80-108">Esses são os conjuntos de credenciais padrão que você configura nos **Serviços de Aplicativos** > **&lt;nome_do_aplicativo>** > **Credenciais de implantação**.</span><span class="sxs-lookup"><span data-stu-id="21e80-108">These are the default credentials set that you configure in **App Services** > **&lt;app_name>** > **Deployment credentials**.</span></span> <span data-ttu-id="21e80-109">Esse também é o conjunto padrão exibido no portal da interface gráfica do usuário (como **Visão geral** e **Propriedades** da [folha de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources) do seu aplicativo).</span><span class="sxs-lookup"><span data-stu-id="21e80-109">This is also the default set that's surfaced in the portal GUI (such as the **Overview** and **Properties** of your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span></span>

    > [!NOTE]
    > <span data-ttu-id="21e80-110">Ao delegar acesso a recursos do Azure por meio de RBAC (Controle de Acesso Baseado em Função) ou permissões de coadministrador, cada usuário do Azure que está recebendo acesso a um aplicativo pode usar suas próprias credenciais no escopo do usuário até que o acesso seja revogado.</span><span class="sxs-lookup"><span data-stu-id="21e80-110">When you delegate access to Azure resources via Role Based Access Control (RBAC) or co-admin permissions, each Azure user that receives access to an app can use his/her personal user-level credentials until access is revoked.</span></span> <span data-ttu-id="21e80-111">Essas credenciais de implantação não devem ser compartilhadas com outros usuários do Azure.</span><span class="sxs-lookup"><span data-stu-id="21e80-111">These deployment credentials should not be shared with other Azure users.</span></span>
    >
    >

* <span data-ttu-id="21e80-112">**Credenciais de nível de aplicativo**: um conjunto de credenciais para cada aplicativo.</span><span class="sxs-lookup"><span data-stu-id="21e80-112">**App-level credentials**: one set of credentials for each app.</span></span> <span data-ttu-id="21e80-113">Podem ser usadas para implantar nesse aplicativo somente.</span><span class="sxs-lookup"><span data-stu-id="21e80-113">It can be used to deploy to that app only.</span></span> <span data-ttu-id="21e80-114">As credenciais para cada aplicativo são geradas automaticamente na criação do aplicativo e são encontradas no aplicativo de publicação do perfil.</span><span class="sxs-lookup"><span data-stu-id="21e80-114">The credentials for each app is generated automatically at app creation, and is found in the app's publish profile.</span></span> <span data-ttu-id="21e80-115">Não é possível configurar manualmente as credenciais, mas é possível redefini-las para um aplicativo a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="21e80-115">You cannot manually configure the credentials, but you can reset them for an app anytime.</span></span>

    > [!NOTE]
    > <span data-ttu-id="21e80-116">Para conceder a alguém o acesso a essas credenciais por meio do RBAC (Controle de Acesso Baseado em Função), você precisa torná-lo colaborador ou conceder a ele uma função superior no Aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="21e80-116">In order to give someone access to these credentials via Role Based Access Control (RBAC), you need to make them contributor or higher on the Web App.</span></span> <span data-ttu-id="21e80-117">Os leitores não têm permissão para publicar e, portanto, não podem acessar essas credenciais.</span><span class="sxs-lookup"><span data-stu-id="21e80-117">Readers are not allowed to publish, and hence can't access those credentials.</span></span>
    >
    >

## <span data-ttu-id="21e80-118"><a name="userscope"></a>Definir e redefinir credenciais de usuário</span><span class="sxs-lookup"><span data-stu-id="21e80-118"><a name="userscope"></a>Set and reset user-level credentials</span></span>

<span data-ttu-id="21e80-119">Você pode configurar as credenciais de usuário na [folha de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources) de qualquer aplicativo.</span><span class="sxs-lookup"><span data-stu-id="21e80-119">You can configure your user-level credentials in any app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span> <span data-ttu-id="21e80-120">Independentemente de para qual aplicativo você configura essas credenciais, elas se aplicam a todos os aplicativos e a todas as assinaturas na conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="21e80-120">Regardless in which app you configure these credentials, it applies to all apps and for all subscriptions in your Azure account.</span></span> 

<span data-ttu-id="21e80-121">Para configurar as credenciais de usuário:</span><span class="sxs-lookup"><span data-stu-id="21e80-121">To configure your user-level credentials:</span></span>

1. <span data-ttu-id="21e80-122">No [Portal do Azure](https://portal.azure.com), clique em Serviço de Aplicativo > **&lt;qualquer_aplicativo>** > **Credenciais de implantação**.</span><span class="sxs-lookup"><span data-stu-id="21e80-122">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Deployment credentials**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="21e80-123">No portal, você deve ter pelo menos um aplicativo antes de poder acessar a folha de credenciais de implantação.</span><span class="sxs-lookup"><span data-stu-id="21e80-123">In the portal, you must have at least one app before you can access the deployment credentials blade.</span></span> <span data-ttu-id="21e80-124">No entanto, com a [CLI do Azure](app-service-web-app-azure-resource-manager-xplat-cli.md), é possível configurar credenciais de usuário sem um aplicativo existente.</span><span class="sxs-lookup"><span data-stu-id="21e80-124">However, with the [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), you can configure user-level credentials without an existing app.</span></span>

2. <span data-ttu-id="21e80-125">Configure o nome de usuário e a senha e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="21e80-125">Configure the user name and password, and then click **Save**.</span></span>

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

<span data-ttu-id="21e80-126">Depois que você tiver configurado suas credenciais de implantação, é possível encontrar o nome de usuário de implantação do *Git* na **Visão geral** de seu aplicativo,</span><span class="sxs-lookup"><span data-stu-id="21e80-126">Once you have set your deployment credentials, you can find the *Git* deployment username in your app's **Overview**,</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

<span data-ttu-id="21e80-127">e o nome de usuário de implantação de *FTP* nas **Propriedades** de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="21e80-127">and and *FTP* deployment username in your app's **Properties**.</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> <span data-ttu-id="21e80-128">O Azure não mostra sua senha de implantação de usuário.</span><span class="sxs-lookup"><span data-stu-id="21e80-128">Azure does not show your user-level deployment password.</span></span> <span data-ttu-id="21e80-129">Se você esquecer a senha, não é possível recuperá-la.</span><span class="sxs-lookup"><span data-stu-id="21e80-129">If you forget the password, you can't retrieve it.</span></span> <span data-ttu-id="21e80-130">No entanto, você pode redefinir suas credenciais seguindo as etapas nesta seção.</span><span class="sxs-lookup"><span data-stu-id="21e80-130">However, you can reset your credentials by following the steps in this section.</span></span>
>
>  

## <span data-ttu-id="21e80-131"><a name="appscope"></a>Definir e redefinir credenciais de aplicativo</span><span class="sxs-lookup"><span data-stu-id="21e80-131"><a name="appscope"></a>Get and reset app-level credentials</span></span>
<span data-ttu-id="21e80-132">Para cada aplicativo no Serviço de Aplicativo, suas credenciais de aplicativo são armazenadas no perfil de publicação XML.</span><span class="sxs-lookup"><span data-stu-id="21e80-132">For each app in App Service, its app-level credentials are stored in the XML publish profile.</span></span>

<span data-ttu-id="21e80-133">Para definir e redefinir credenciais de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="21e80-133">To get the app-level credentials:</span></span>

1. <span data-ttu-id="21e80-134">No [Portal do Azure](https://portal.azure.com), clique em Serviço de Aplicativo > **&lt;qualquer_aplicativo>** > **Visão geral**.</span><span class="sxs-lookup"><span data-stu-id="21e80-134">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="21e80-135">Clique em **...Mais** > **Obter perfil de publicação** e inicie o download de um arquivo .PublishSettings.</span><span class="sxs-lookup"><span data-stu-id="21e80-135">Click **...More** > **Get publish profile**, and download starts for a .PublishSettings file.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. <span data-ttu-id="21e80-136">Abra o arquivo .PublishSettings e localize a marca `<publishProfile>` com o atributo `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="21e80-136">Open the .PublishSettings file and find the `<publishProfile>` tag with the attribute `publishMethod="FTP"`.</span></span> <span data-ttu-id="21e80-137">Em seguida, obtenha seus atributos `userName` e `password`.</span><span class="sxs-lookup"><span data-stu-id="21e80-137">Then, get its `userName` and `password` attributes.</span></span>
<span data-ttu-id="21e80-138">Essas são as credenciais de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="21e80-138">These are the app-level credentials.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    <span data-ttu-id="21e80-139">Assim como as credenciais de usuário, o nome de usuário de implantação de FTP está no formato `<app_name>\<username>` e o nome de usuário de implantação do Git é apenas o `<username>` sem o `<app_name>\` precedente.</span><span class="sxs-lookup"><span data-stu-id="21e80-139">Similar to the user-level credentials, the FTP deployment username is in the format of `<app_name>\<username>`, and the Git deployment username is just `<username>` without the preceding `<app_name>\`.</span></span>

<span data-ttu-id="21e80-140">Para redefinir as credenciais de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="21e80-140">To reset the app-level credentials:</span></span>

1. <span data-ttu-id="21e80-141">No [Portal do Azure](https://portal.azure.com), clique em Serviço de Aplicativo > **&lt;qualquer_aplicativo>** > **Visão geral**.</span><span class="sxs-lookup"><span data-stu-id="21e80-141">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="21e80-142">Clique em **...Mais** > **Redefinir perfil de publicação**.</span><span class="sxs-lookup"><span data-stu-id="21e80-142">Click **...More** > **Reset publish profile**.</span></span> <span data-ttu-id="21e80-143">Clique em **Sim** para confirmar a redefinição.</span><span class="sxs-lookup"><span data-stu-id="21e80-143">Click **Yes** to confirm the reset.</span></span>

    <span data-ttu-id="21e80-144">A ação de redefinição invalida quaisquer arquivos .PublishSettings baixados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="21e80-144">The reset action invalidates any previously-downloaded .PublishSettings files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21e80-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="21e80-145">Next steps</span></span>

<span data-ttu-id="21e80-146">Saiba como usar essas credenciais para implantar seu aplicativo do [Git local](app-service-deploy-local-git.md) ou usando [FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="21e80-146">Find out how to use these credentials to deploy your app from [local Git](app-service-deploy-local-git.md) or using [FTP/S](app-service-deploy-ftp.md).</span></span>
