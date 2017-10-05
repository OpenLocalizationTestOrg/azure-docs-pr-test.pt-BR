---
title: Criar identidade para o aplicativo do Azure no portal | Microsoft Docs
description: "Descreve como criar um novo aplicativo do Azure Active Directory e uma nova entidade de serviço, que possam ser usados com o controle de acesso baseado em função no Azure Resource Manager para gerenciar o acesso aos recursos."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 5d24fb99e1095d53e5ea547e53b80178d9cb77c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="use-portal-to-create-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a><span data-ttu-id="359f2-103">Usar o portal para criar um aplicativo e uma entidade de serviço do Azure Active Directory que possa acessar recursos</span><span class="sxs-lookup"><span data-stu-id="359f2-103">Use portal to create an Azure Active Directory application and service principal that can access resources</span></span>

<span data-ttu-id="359f2-104">Quando você tiver um aplicativo que precisa acessar ou modificar os recursos, deverá configurar um aplicativo do Azure AD (Active Directory) e atribuir as permissões necessárias a ele.</span><span class="sxs-lookup"><span data-stu-id="359f2-104">When you have an application that needs to access or modify resources, you must set up an Azure Active Directory (AD) application and assign the required permissions to it.</span></span> <span data-ttu-id="359f2-105">Esta abordagem é preferencial para executar o aplicativo com suas próprias credenciais porque:</span><span class="sxs-lookup"><span data-stu-id="359f2-105">This approach is preferable to running the app under your own credentials because:</span></span>

* <span data-ttu-id="359f2-106">Você pode atribuir permissões para a identidade do aplicativo que são diferentes de suas próprias permissões.</span><span class="sxs-lookup"><span data-stu-id="359f2-106">You can assign permissions to the app identity that are different than your own permissions.</span></span> <span data-ttu-id="359f2-107">Normalmente, essas permissões são restritas a exatamente o que o aplicativo precisa fazer.</span><span class="sxs-lookup"><span data-stu-id="359f2-107">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="359f2-108">Você não precisa alterar as credenciais do aplicativo se alterar suas responsabilidades.</span><span class="sxs-lookup"><span data-stu-id="359f2-108">You do not have to change the app's credentials if your responsibilities change.</span></span> 
* <span data-ttu-id="359f2-109">Você pode usar um certificado para automatizar a autenticação ao executar um script autônomo.</span><span class="sxs-lookup"><span data-stu-id="359f2-109">You can use a certificate to automate authentication when executing an unattended script.</span></span>

<span data-ttu-id="359f2-110">Este tópico mostra como executar essas etapas no portal.</span><span class="sxs-lookup"><span data-stu-id="359f2-110">This topic shows you how to perform those steps through the portal.</span></span> <span data-ttu-id="359f2-111">Ele se concentra em um aplicativo de locatário único que se destina a ser executado dentro de uma única organização.</span><span class="sxs-lookup"><span data-stu-id="359f2-111">It focuses on a single-tenant application where the application is intended to run within only one organization.</span></span> <span data-ttu-id="359f2-112">Você normalmente usa os aplicativos com um único locatário para os aplicativos da linha de negócios executados em sua organização.</span><span class="sxs-lookup"><span data-stu-id="359f2-112">You typically use single-tenant applications for line-of-business applications that run within your organization.</span></span>
 
## <a name="required-permissions"></a><span data-ttu-id="359f2-113">Permissões necessárias</span><span class="sxs-lookup"><span data-stu-id="359f2-113">Required permissions</span></span>
<span data-ttu-id="359f2-114">Para concluir este tópico, você deve ter permissões suficientes para registrar um aplicativo com o locatário do Azure AD e atribuir o aplicativo a uma função em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="359f2-114">To complete this topic, you must have sufficient permissions to register an application with your Azure AD tenant, and assign the application to a role in your Azure subscription.</span></span> <span data-ttu-id="359f2-115">Vamos verificar se você tem as permissões corretas para executar essas etapas.</span><span class="sxs-lookup"><span data-stu-id="359f2-115">Let's make sure you have the right permissions to perform those steps.</span></span>

### <a name="check-azure-active-directory-permissions"></a><span data-ttu-id="359f2-116">Verificar as permissões do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="359f2-116">Check Azure Active Directory permissions</span></span>
1. <span data-ttu-id="359f2-117">Entre na sua conta do Azure por meio do [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="359f2-117">Log in to your Azure Account through the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="359f2-118">Selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="359f2-118">Select **Azure Active Directory**.</span></span>

     ![selecionar azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)
3. <span data-ttu-id="359f2-120">No Azure Active Directory, selecione **Configurações de Usuário**.</span><span class="sxs-lookup"><span data-stu-id="359f2-120">In Azure Active Directory, select **User settings**.</span></span>

     ![selecionar configurações de usuário](./media/resource-group-create-service-principal-portal/select-user-settings.png)
4. <span data-ttu-id="359f2-122">Verifique a configuração **Registros do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="359f2-122">Check the **App registrations** setting.</span></span> <span data-ttu-id="359f2-123">Se estiver definida como **Sim**, usuários que não são administradores podem registrar aplicativos do AD.</span><span class="sxs-lookup"><span data-stu-id="359f2-123">If set to **Yes**, non-admin users can register AD apps.</span></span> <span data-ttu-id="359f2-124">Essa configuração significa que qualquer usuário no locatário do Azure AD pode registrar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="359f2-124">This setting means any user in the Azure AD tenant can register an app.</span></span> <span data-ttu-id="359f2-125">Você pode prosseguir com a [verificação das permissões de assinatura do Azure](#check-azure-subscription-permissions).</span><span class="sxs-lookup"><span data-stu-id="359f2-125">You can proceed to [Check Azure subscription permissions](#check-azure-subscription-permissions).</span></span>

     ![exibir registros de aplicativo](./media/resource-group-create-service-principal-portal/view-app-registrations.png)
5. <span data-ttu-id="359f2-127">Se a configuração de registros do aplicativo estiver definida como **Não**, somente usuários que são administradores podem registrar aplicativos.</span><span class="sxs-lookup"><span data-stu-id="359f2-127">If the app registrations setting is set to **No**, only admin users can register apps.</span></span> <span data-ttu-id="359f2-128">Você precisa verificar se sua conta é de administrador para o locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="359f2-128">You need to check whether your account is an admin for the Azure AD tenant.</span></span> <span data-ttu-id="359f2-129">Selecione **Visão Geral** e **Localizar um usuário** nas Tarefas Rápidas.</span><span class="sxs-lookup"><span data-stu-id="359f2-129">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![localizar usuário](./media/resource-group-create-service-principal-portal/find-user.png)
6. <span data-ttu-id="359f2-131">Procure por sua conta e selecione-a quando encontrá-la.</span><span class="sxs-lookup"><span data-stu-id="359f2-131">Search for your account, and select it when you find it.</span></span>

     ![pesquisar usuário](./media/resource-group-create-service-principal-portal/show-user.png)
7. <span data-ttu-id="359f2-133">Para sua conta, selecione **função de diretório**.</span><span class="sxs-lookup"><span data-stu-id="359f2-133">For your account, select **Directory role**.</span></span> 

     ![função de diretório](./media/resource-group-create-service-principal-portal/select-directory-role.png)
8. <span data-ttu-id="359f2-135">Veja sua função de diretório atribuída no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="359f2-135">View your assigned directory role in Azure AD.</span></span> <span data-ttu-id="359f2-136">Se sua conta estiver atribuída com a função de usuário, mas a configuração de registro de aplicativo (de etapas anteriores) estiver limitada a usuários administradores, peça ao administrador para atribuir uma função de administrador a você ou para permitir que os usuários registrem aplicativos.</span><span class="sxs-lookup"><span data-stu-id="359f2-136">If your account is assigned to the User role, but the app registration setting (from the preceding steps) is limited to admin users, ask your administrator to either assign you to an administrator role, or to enable users to register apps.</span></span>

     ![exibir função](./media/resource-group-create-service-principal-portal/view-role.png)

### <a name="check-azure-subscription-permissions"></a><span data-ttu-id="359f2-138">Verificar permissões de assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="359f2-138">Check Azure subscription permissions</span></span>
<span data-ttu-id="359f2-139">Em sua assinatura do Azure, sua conta deve ter acesso de `Microsoft.Authorization/*/Write` para atribuir um aplicativo do AD a uma função.</span><span class="sxs-lookup"><span data-stu-id="359f2-139">In your Azure subscription, your account must have `Microsoft.Authorization/*/Write` access to assign an AD app to a role.</span></span> <span data-ttu-id="359f2-140">Esta ação deve ser concedida pela função [Proprietário](../active-directory/role-based-access-built-in-roles.md#owner) ou pela função [Administrador de Acesso do Usuário](../active-directory/role-based-access-built-in-roles.md#user-access-administrator).</span><span class="sxs-lookup"><span data-stu-id="359f2-140">This action is granted through the [Owner](../active-directory/role-based-access-built-in-roles.md#owner) role or [User Access Administrator](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) role.</span></span> <span data-ttu-id="359f2-141">Se sua conta tiver a função **Colaborador**, você não tem a permissão adequada.</span><span class="sxs-lookup"><span data-stu-id="359f2-141">If your account is assigned to the **Contributor** role, you do not have adequate permission.</span></span> <span data-ttu-id="359f2-142">Você receberá um erro ao tentar atribuir a entidade de serviço a uma função.</span><span class="sxs-lookup"><span data-stu-id="359f2-142">You will receive an error when attempting to assign the service principal to a role.</span></span> 

<span data-ttu-id="359f2-143">Para verificar suas permissões de assinatura:</span><span class="sxs-lookup"><span data-stu-id="359f2-143">To check your subscription permissions:</span></span>

1. <span data-ttu-id="359f2-144">Se você ainda não está vendo sua conta do Azure AD usando as etapas anteriores, selecione **Azure Active Directory** no painel à esquerda.</span><span class="sxs-lookup"><span data-stu-id="359f2-144">If you are not already looking at your Azure AD account from the preceding steps, select **Azure Active Directory** from the left pane.</span></span>

2. <span data-ttu-id="359f2-145">Encontre sua conta do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="359f2-145">Find your Azure AD account.</span></span> <span data-ttu-id="359f2-146">Selecione **Visão Geral** e **Localizar um usuário** nas Tarefas Rápidas.</span><span class="sxs-lookup"><span data-stu-id="359f2-146">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![localizar usuário](./media/resource-group-create-service-principal-portal/find-user.png)
2. <span data-ttu-id="359f2-148">Procure por sua conta e selecione-a quando encontrá-la.</span><span class="sxs-lookup"><span data-stu-id="359f2-148">Search for your account, and select it when you find it.</span></span>

     ![pesquisar usuário](./media/resource-group-create-service-principal-portal/show-user.png) 
     
3. <span data-ttu-id="359f2-150">Selecione **Recursos do Azure**.</span><span class="sxs-lookup"><span data-stu-id="359f2-150">Select **Azure resources**.</span></span>

     ![selecionar recursos](./media/resource-group-create-service-principal-portal/select-azure-resources.png) 
3. <span data-ttu-id="359f2-152">Exiba suas funções atribuídas e determine se você tem as permissões adequadas para atribuir um aplicativo do AD a uma função.</span><span class="sxs-lookup"><span data-stu-id="359f2-152">View your assigned roles, and determine if you have adequate permissions to assign an AD app to a role.</span></span> <span data-ttu-id="359f2-153">Caso contrário, peça ao administrador da assinatura para adicioná-lo à função Administrador de Acesso do Usuário.</span><span class="sxs-lookup"><span data-stu-id="359f2-153">If not, ask your subscription administrator to add you to User Access Administrator role.</span></span> <span data-ttu-id="359f2-154">Na imagem a seguir, o usuário é atribuído à função Proprietário para duas assinaturas, o que significa que o usuário tem as permissões adequadas.</span><span class="sxs-lookup"><span data-stu-id="359f2-154">In the following image, the user is assigned to the Owner role for two subscriptions, which means that user has adequate permissions.</span></span> 

     ![mostrar permissões](./media/resource-group-create-service-principal-portal/view-assigned-roles.png)

## <a name="create-an-azure-active-directory-application"></a><span data-ttu-id="359f2-156">Criar um aplicativo do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="359f2-156">Create an Azure Active Directory application</span></span>
1. <span data-ttu-id="359f2-157">Entre na sua conta do Azure por meio do [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="359f2-157">Log in to your Azure Account through the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="359f2-158">Selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="359f2-158">Select **Azure Active Directory**.</span></span>

     ![selecionar azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)

4. <span data-ttu-id="359f2-160">Selecione **Registros do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="359f2-160">Select **App registrations**.</span></span>   

     ![selecionar registros do aplicativo](./media/resource-group-create-service-principal-portal/select-app-registrations.png)
5. <span data-ttu-id="359f2-162">Selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="359f2-162">Select **Add**.</span></span>

     ![adicionar aplicativo](./media/resource-group-create-service-principal-portal/select-add-app.png)

6. <span data-ttu-id="359f2-164">Forneça um nome e uma URL para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="359f2-164">Provide a name and URL for the application.</span></span> <span data-ttu-id="359f2-165">Selecione **aplicativo Web/API** ou **Nativo** para o tipo de aplicativo que você deseja criar.</span><span class="sxs-lookup"><span data-stu-id="359f2-165">Select either **Web app / API** or **Native** for the type of application you want to create.</span></span> <span data-ttu-id="359f2-166">Depois de definir os valores, selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="359f2-166">After setting the values, select **Create**.</span></span>

     ![nomear aplicativo](./media/resource-group-create-service-principal-portal/create-app.png)

<span data-ttu-id="359f2-168">Você criou seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="359f2-168">You have created your application.</span></span>

## <a name="get-application-id-and-authentication-key"></a><span data-ttu-id="359f2-169">Obter chave de autenticação e ID do aplicativo</span><span class="sxs-lookup"><span data-stu-id="359f2-169">Get application ID and authentication key</span></span>
<span data-ttu-id="359f2-170">Ao fazer logon por meio de programação, você precisa da ID para seu aplicativo e de uma chave de autenticação.</span><span class="sxs-lookup"><span data-stu-id="359f2-170">When programmatically logging in, you need the ID for your application and an authentication key.</span></span> <span data-ttu-id="359f2-171">Para obter esses valores, use as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="359f2-171">To get those values, use the following steps:</span></span>

1. <span data-ttu-id="359f2-172">Em **Registros do Aplicativo** no Azure Active Directory, selecione seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="359f2-172">From **App registrations** in Azure Active Directory, select your application.</span></span>

     ![selecionar aplicativo](./media/resource-group-create-service-principal-portal/select-app.png)
2. <span data-ttu-id="359f2-174">Copie a **ID do aplicativo** e armazene-a no código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="359f2-174">Copy the **Application ID** and store it in your application code.</span></span> <span data-ttu-id="359f2-175">Os aplicativos na seção [Aplicativos de exemplo](#sample-applications) referem-se a esse valor como a ID do cliente.</span><span class="sxs-lookup"><span data-stu-id="359f2-175">The applications in the [sample applications](#sample-applications) section refer to this value as the client id.</span></span>

     ![ID do CLIENTE](./media/resource-group-create-service-principal-portal/copy-app-id.png)
3. <span data-ttu-id="359f2-177">Para gerar uma chave de autenticação, selecione **Chaves**.</span><span class="sxs-lookup"><span data-stu-id="359f2-177">To generate an authentication key, select **Keys**.</span></span>

     ![selecionar chaves](./media/resource-group-create-service-principal-portal/select-keys.png)
4. <span data-ttu-id="359f2-179">Forneça uma descrição da chave e uma duração para a chave.</span><span class="sxs-lookup"><span data-stu-id="359f2-179">Provide a description of the key, and a duration for the key.</span></span> <span data-ttu-id="359f2-180">Ao terminar, escolha **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="359f2-180">When done, select **Save**.</span></span>

     ![salvar chave](./media/resource-group-create-service-principal-portal/save-key.png)

     <span data-ttu-id="359f2-182">Após salvar a chave, o valor da chave é exibido.</span><span class="sxs-lookup"><span data-stu-id="359f2-182">After saving the key, the value of the key is displayed.</span></span> <span data-ttu-id="359f2-183">Copie este valor, pois não é possível recuperar a chave posteriormente.</span><span class="sxs-lookup"><span data-stu-id="359f2-183">Copy this value because you are not able to retrieve the key later.</span></span> <span data-ttu-id="359f2-184">Forneça o valor da chave com a ID do aplicativo para fazer logon como o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="359f2-184">You provide the key value with the application ID to log in as the application.</span></span> <span data-ttu-id="359f2-185">Armazene o valor da chave onde seu aplicativo possa recuperá-lo.</span><span class="sxs-lookup"><span data-stu-id="359f2-185">Store the key value where your application can retrieve it.</span></span>

     ![chave salva](./media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a><span data-ttu-id="359f2-187">Obter a ID do locatário</span><span class="sxs-lookup"><span data-stu-id="359f2-187">Get tenant ID</span></span>
<span data-ttu-id="359f2-188">Ao fazer logon por meio de programação, você precisa passar a ID de locatário com a solicitação de autenticação.</span><span class="sxs-lookup"><span data-stu-id="359f2-188">When programmatically logging in, you need to pass the tenant ID with your authentication request.</span></span> 

1. <span data-ttu-id="359f2-189">Para obter a ID de locatário, selecione **Propriedades** do seu locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="359f2-189">To get the tenant ID, select **Properties** for your Azure AD tenant.</span></span> 

     ![selecionar propriedades do Azure AD](./media/resource-group-create-service-principal-portal/select-ad-properties.png)

2. <span data-ttu-id="359f2-191">Copie a **ID de diretório**.</span><span class="sxs-lookup"><span data-stu-id="359f2-191">Copy the **Directory ID**.</span></span> <span data-ttu-id="359f2-192">Esse valor é a ID do locatário.</span><span class="sxs-lookup"><span data-stu-id="359f2-192">This value is your tenant ID.</span></span>

     ![ID do locatário](./media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-to-role"></a><span data-ttu-id="359f2-194">Atribuir aplicativo à função</span><span class="sxs-lookup"><span data-stu-id="359f2-194">Assign application to role</span></span>
<span data-ttu-id="359f2-195">Para acessar recursos em sua assinatura, você deve atribuir o aplicativo a uma função.</span><span class="sxs-lookup"><span data-stu-id="359f2-195">To access resources in your subscription, you must assign the application to a role.</span></span> <span data-ttu-id="359f2-196">Decida qual função representa as permissões corretas para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="359f2-196">Decide which role represents the right permissions for the application.</span></span> <span data-ttu-id="359f2-197">Para saber mais sobre as funções disponíveis, consulte [RBAC: funções internas](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="359f2-197">To learn about the available roles, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="359f2-198">Você pode definir o escopo no nível da assinatura, do grupo de recursos ou do recurso.</span><span class="sxs-lookup"><span data-stu-id="359f2-198">You can set the scope at the level of the subscription, resource group, or resource.</span></span> <span data-ttu-id="359f2-199">As permissão são herdadas para níveis inferiores do escopo.</span><span class="sxs-lookup"><span data-stu-id="359f2-199">Permissions are inherited to lower levels of scope.</span></span> <span data-ttu-id="359f2-200">Por exemplo, adicionar um aplicativo à função Leitor de um grupo de recursos significa que ele pode ler o grupo de recursos e todos os recursos que ele contiver.</span><span class="sxs-lookup"><span data-stu-id="359f2-200">For example, adding an application to the Reader role for a resource group means it can read the resource group and any resources it contains.</span></span>

1. <span data-ttu-id="359f2-201">Navegue até o nível do escopo ao qual quer atribuir o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="359f2-201">Navigate to the level of scope you wish to assign the application to.</span></span> <span data-ttu-id="359f2-202">Por exemplo, para atribuir uma função no escopo da assinatura, escolha **Assinaturas**.</span><span class="sxs-lookup"><span data-stu-id="359f2-202">For example, to assign a role at the subscription scope, select **Subscriptions**.</span></span> <span data-ttu-id="359f2-203">Em vez disso, você pode selecionar um grupo de recursos ou um recurso.</span><span class="sxs-lookup"><span data-stu-id="359f2-203">You could instead select a resource group or resource.</span></span>

     ![selecione a assinatura](./media/resource-group-create-service-principal-portal/select-subscription.png)

2. <span data-ttu-id="359f2-205">Escolha a assinatura específica (grupo de recursos ou recurso) à qual atribuir o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="359f2-205">Select the particular subscription (resource group or resource) to assign the application to.</span></span>

     ![selecionar assinatura para atribuição](./media/resource-group-create-service-principal-portal/select-one-subscription.png)

3. <span data-ttu-id="359f2-207">Selecione **Controle de Acesso (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="359f2-207">Select **Access Control (IAM)**.</span></span>

     ![selecionar acesso](./media/resource-group-create-service-principal-portal/select-access-control.png)

4. <span data-ttu-id="359f2-209">Selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="359f2-209">Select **Add**.</span></span>

     ![escolher adicionar](./media/resource-group-create-service-principal-portal/select-add.png)
6. <span data-ttu-id="359f2-211">Selecione a função que deseja atribuir ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="359f2-211">Select the role you wish to assign to the application.</span></span> <span data-ttu-id="359f2-212">A imagem a seguir mostra a função **Leitor**.</span><span class="sxs-lookup"><span data-stu-id="359f2-212">The following image shows the **Reader** role.</span></span>

     ![escolher função](./media/resource-group-create-service-principal-portal/select-role.png)

8. <span data-ttu-id="359f2-214">Procure seu aplicativo e selecione-o.</span><span class="sxs-lookup"><span data-stu-id="359f2-214">Search for your application, and select it.</span></span>

     ![pesquisar aplicativo](./media/resource-group-create-service-principal-portal/search-app.png)
9. <span data-ttu-id="359f2-216">Selecione **OK** para finalizar a atribuição da função.</span><span class="sxs-lookup"><span data-stu-id="359f2-216">Select **OK** to finish assigning the role.</span></span> <span data-ttu-id="359f2-217">Agora você vê o aplicativo na lista de usuários atribuídos a uma função para esse escopo.</span><span class="sxs-lookup"><span data-stu-id="359f2-217">You see your application in the list of users assigned to a role for that scope.</span></span>

## <a name="log-in-as-the-application"></a><span data-ttu-id="359f2-218">Faça logon como o aplicativo</span><span class="sxs-lookup"><span data-stu-id="359f2-218">Log in as the application</span></span>

<span data-ttu-id="359f2-219">Seu aplicativo agora está configurado no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="359f2-219">Your application is now set up in Azure Active Directory.</span></span> <span data-ttu-id="359f2-220">Você tem uma ID e a chave a ser usada para fazer logon como o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="359f2-220">You have an ID and key to use for signing in as the application.</span></span> <span data-ttu-id="359f2-221">O aplicativo está atribuído a uma função que oferece determinadas ações que ele pode executar.</span><span class="sxs-lookup"><span data-stu-id="359f2-221">The application is assigned to a role that gives it certain actions it can perform.</span></span> <span data-ttu-id="359f2-222">Para obter informações sobre como fazer logon no aplicativo por meio de diferentes plataformas, consulte:</span><span class="sxs-lookup"><span data-stu-id="359f2-222">For information about logging in as the application through different platforms, see:</span></span>

* [<span data-ttu-id="359f2-223">PowerShell</span><span class="sxs-lookup"><span data-stu-id="359f2-223">PowerShell</span></span>](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell)
* [<span data-ttu-id="359f2-224">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="359f2-224">Azure CLI</span></span>](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli)
* [<span data-ttu-id="359f2-225">REST</span><span class="sxs-lookup"><span data-stu-id="359f2-225">REST</span></span>](/rest/api/#create-the-request)
* [<span data-ttu-id="359f2-226">.NET</span><span class="sxs-lookup"><span data-stu-id="359f2-226">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="359f2-227">Java</span><span class="sxs-lookup"><span data-stu-id="359f2-227">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="359f2-228">Node.js</span><span class="sxs-lookup"><span data-stu-id="359f2-228">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="359f2-229">Python</span><span class="sxs-lookup"><span data-stu-id="359f2-229">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="359f2-230">Ruby</span><span class="sxs-lookup"><span data-stu-id="359f2-230">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)


## <a name="next-steps"></a><span data-ttu-id="359f2-231">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="359f2-231">Next steps</span></span>
* <span data-ttu-id="359f2-232">Para configurar um aplicativo multilocatário, consulte [Guia do desenvolvedor para a autorização com a API do Azure Resource Manager](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="359f2-232">To set up a multi-tenant application, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="359f2-233">Para aprender a especificar as políticas de segurança, consulte [Controle de Acesso baseado nas Funções do Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="359f2-233">To learn about specifying security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>  
* <span data-ttu-id="359f2-234">Para obter uma lista de ações disponíveis que podem ser concedidas ou negadas a usuários, consulte [Operações do Provedor de Recursos do Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="359f2-234">For a list of available actions that can be granted or denied to users, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
