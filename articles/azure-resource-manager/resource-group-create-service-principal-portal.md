---
title: aaaCreate identidade para o aplicativo no portal do Azure | Microsoft Docs
description: "Descreve como toocreate um novo aplicativo do Active Directory do Azure e o serviço principal que pode ser usado com o controle de acesso baseado em função hello no Gerenciador de recursos do Azure toomanage acessam tooresources."
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
ms.openlocfilehash: 9624715ac612f42df6f9e9e67b8233bd4b914174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-portal-toocreate-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a><span data-ttu-id="454fd-103">Use o portal toocreate um aplicativo do Azure Active Directory e a entidade de serviço que pode acessar os recursos</span><span class="sxs-lookup"><span data-stu-id="454fd-103">Use portal toocreate an Azure Active Directory application and service principal that can access resources</span></span>

<span data-ttu-id="454fd-104">Quando você tiver um aplicativo que precisa tooaccess ou modificar os recursos, você deve configurar um aplicativo do Azure AD (Active Directory) e atribuir Olá necessárias permissões tooit.</span><span class="sxs-lookup"><span data-stu-id="454fd-104">When you have an application that needs tooaccess or modify resources, you must set up an Azure Active Directory (AD) application and assign hello required permissions tooit.</span></span> <span data-ttu-id="454fd-105">Essa abordagem é preferível toorunning Olá aplicativo com suas próprias credenciais, porque:</span><span class="sxs-lookup"><span data-stu-id="454fd-105">This approach is preferable toorunning hello app under your own credentials because:</span></span>

* <span data-ttu-id="454fd-106">Você pode atribuir permissões de identidade de aplicativo toohello que são diferentes de suas próprias permissões.</span><span class="sxs-lookup"><span data-stu-id="454fd-106">You can assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="454fd-107">Normalmente, essas permissões são restrito tooexactly toodo precisa de qual aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="454fd-107">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="454fd-108">Você não tem credenciais do aplicativo de saudação toochange se alterar suas responsabilidades.</span><span class="sxs-lookup"><span data-stu-id="454fd-108">You do not have toochange hello app's credentials if your responsibilities change.</span></span> 
* <span data-ttu-id="454fd-109">Você pode usar uma autenticação de certificado de tooautomate ao executar um script autônomo.</span><span class="sxs-lookup"><span data-stu-id="454fd-109">You can use a certificate tooautomate authentication when executing an unattended script.</span></span>

<span data-ttu-id="454fd-110">Este tópico mostra como tooperform aqueles percorre portal hello.</span><span class="sxs-lookup"><span data-stu-id="454fd-110">This topic shows you how tooperform those steps through hello portal.</span></span> <span data-ttu-id="454fd-111">Ele se concentra em um aplicativo de único locatário em que o aplicativo hello é pretendido toorun dentro de uma só organização.</span><span class="sxs-lookup"><span data-stu-id="454fd-111">It focuses on a single-tenant application where hello application is intended toorun within only one organization.</span></span> <span data-ttu-id="454fd-112">Você normalmente usa os aplicativos com um único locatário para os aplicativos da linha de negócios executados em sua organização.</span><span class="sxs-lookup"><span data-stu-id="454fd-112">You typically use single-tenant applications for line-of-business applications that run within your organization.</span></span>
 
## <a name="required-permissions"></a><span data-ttu-id="454fd-113">Permissões necessárias</span><span class="sxs-lookup"><span data-stu-id="454fd-113">Required permissions</span></span>
<span data-ttu-id="454fd-114">toocomplete neste tópico, você deve ter um aplicativo de tooregister de permissões suficientes com seu locatário do AD do Azure e atribuir a função de tooa aplicativo hello em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="454fd-114">toocomplete this topic, you must have sufficient permissions tooregister an application with your Azure AD tenant, and assign hello application tooa role in your Azure subscription.</span></span> <span data-ttu-id="454fd-115">Vamos garantir que você tenha Olá permissões corretas tooperform essas etapas.</span><span class="sxs-lookup"><span data-stu-id="454fd-115">Let's make sure you have hello right permissions tooperform those steps.</span></span>

### <a name="check-azure-active-directory-permissions"></a><span data-ttu-id="454fd-116">Verificar as permissões do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="454fd-116">Check Azure Active Directory permissions</span></span>
1. <span data-ttu-id="454fd-117">Fazer logon no tooyour conta do Azure por meio de saudação [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="454fd-117">Log in tooyour Azure Account through hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="454fd-118">Selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="454fd-118">Select **Azure Active Directory**.</span></span>

     ![selecionar azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)
3. <span data-ttu-id="454fd-120">No Azure Active Directory, selecione **Configurações de Usuário**.</span><span class="sxs-lookup"><span data-stu-id="454fd-120">In Azure Active Directory, select **User settings**.</span></span>

     ![selecionar configurações de usuário](./media/resource-group-create-service-principal-portal/select-user-settings.png)
4. <span data-ttu-id="454fd-122">Verificar Olá **registros do aplicativo** configuração.</span><span class="sxs-lookup"><span data-stu-id="454fd-122">Check hello **App registrations** setting.</span></span> <span data-ttu-id="454fd-123">Se definir muito**Sim**, os usuários não administradores podem registrar aplicativos do AD.</span><span class="sxs-lookup"><span data-stu-id="454fd-123">If set too**Yes**, non-admin users can register AD apps.</span></span> <span data-ttu-id="454fd-124">Essa configuração significa que qualquer usuário no locatário do AD do Azure Olá pode registrar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="454fd-124">This setting means any user in hello Azure AD tenant can register an app.</span></span> <span data-ttu-id="454fd-125">Você pode continuar muito[permissões de assinatura do Azure verificar](#check-azure-subscription-permissions).</span><span class="sxs-lookup"><span data-stu-id="454fd-125">You can proceed too[Check Azure subscription permissions](#check-azure-subscription-permissions).</span></span>

     ![exibir registros de aplicativo](./media/resource-group-create-service-principal-portal/view-app-registrations.png)
5. <span data-ttu-id="454fd-127">Se os registros do aplicativo hello configuração está definido muito**não**, somente os usuários administrativos podem registrar aplicativos.</span><span class="sxs-lookup"><span data-stu-id="454fd-127">If hello app registrations setting is set too**No**, only admin users can register apps.</span></span> <span data-ttu-id="454fd-128">É necessário toocheck se sua conta é um administrador de locatário do AD do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="454fd-128">You need toocheck whether your account is an admin for hello Azure AD tenant.</span></span> <span data-ttu-id="454fd-129">Selecione **Visão Geral** e **Localizar um usuário** nas Tarefas Rápidas.</span><span class="sxs-lookup"><span data-stu-id="454fd-129">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![localizar usuário](./media/resource-group-create-service-principal-portal/find-user.png)
6. <span data-ttu-id="454fd-131">Procure por sua conta e selecione-a quando encontrá-la.</span><span class="sxs-lookup"><span data-stu-id="454fd-131">Search for your account, and select it when you find it.</span></span>

     ![pesquisar usuário](./media/resource-group-create-service-principal-portal/show-user.png)
7. <span data-ttu-id="454fd-133">Para sua conta, selecione **função de diretório**.</span><span class="sxs-lookup"><span data-stu-id="454fd-133">For your account, select **Directory role**.</span></span> 

     ![função de diretório](./media/resource-group-create-service-principal-portal/select-directory-role.png)
8. <span data-ttu-id="454fd-135">Veja sua função de diretório atribuída no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="454fd-135">View your assigned directory role in Azure AD.</span></span> <span data-ttu-id="454fd-136">Se sua conta é atribuída a função de usuário toohello, mas hello, configuração de registro de aplicativo (da saudação etapas anteriores) é limitado tooadmin usuários, peça ao seu administrador tooeither atribuir a função administrador tooan ou tooenable usuários tooregister aplicativos.</span><span class="sxs-lookup"><span data-stu-id="454fd-136">If your account is assigned toohello User role, but hello app registration setting (from hello preceding steps) is limited tooadmin users, ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

     ![exibir função](./media/resource-group-create-service-principal-portal/view-role.png)

### <a name="check-azure-subscription-permissions"></a><span data-ttu-id="454fd-138">Verificar permissões de assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="454fd-138">Check Azure subscription permissions</span></span>
<span data-ttu-id="454fd-139">Sua assinatura do Azure, sua conta deve ter `Microsoft.Authorization/*/Write` acessar tooassign uma função de tooa de aplicativo do AD.</span><span class="sxs-lookup"><span data-stu-id="454fd-139">In your Azure subscription, your account must have `Microsoft.Authorization/*/Write` access tooassign an AD app tooa role.</span></span> <span data-ttu-id="454fd-140">Essa ação é concedida por meio de saudação [proprietário](../active-directory/role-based-access-built-in-roles.md#owner) função ou [administrador de acesso do usuário](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) função.</span><span class="sxs-lookup"><span data-stu-id="454fd-140">This action is granted through hello [Owner](../active-directory/role-based-access-built-in-roles.md#owner) role or [User Access Administrator](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) role.</span></span> <span data-ttu-id="454fd-141">Se sua conta é atribuída toohello **Colaborador** função, você não tem permissão suficiente.</span><span class="sxs-lookup"><span data-stu-id="454fd-141">If your account is assigned toohello **Contributor** role, you do not have adequate permission.</span></span> <span data-ttu-id="454fd-142">Você receberá um erro durante a tentativa de função de principal tooa tooassign Olá serviço.</span><span class="sxs-lookup"><span data-stu-id="454fd-142">You will receive an error when attempting tooassign hello service principal tooa role.</span></span> 

<span data-ttu-id="454fd-143">toocheck suas permissões de assinatura:</span><span class="sxs-lookup"><span data-stu-id="454fd-143">toocheck your subscription permissions:</span></span>

1. <span data-ttu-id="454fd-144">Se você estiver não já em sua conta do AD do Azure de saudação etapas anteriores, selecione **Active Directory do Azure** no painel esquerdo do hello.</span><span class="sxs-lookup"><span data-stu-id="454fd-144">If you are not already looking at your Azure AD account from hello preceding steps, select **Azure Active Directory** from hello left pane.</span></span>

2. <span data-ttu-id="454fd-145">Encontre sua conta do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="454fd-145">Find your Azure AD account.</span></span> <span data-ttu-id="454fd-146">Selecione **Visão Geral** e **Localizar um usuário** nas Tarefas Rápidas.</span><span class="sxs-lookup"><span data-stu-id="454fd-146">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![localizar usuário](./media/resource-group-create-service-principal-portal/find-user.png)
2. <span data-ttu-id="454fd-148">Procure por sua conta e selecione-a quando encontrá-la.</span><span class="sxs-lookup"><span data-stu-id="454fd-148">Search for your account, and select it when you find it.</span></span>

     ![pesquisar usuário](./media/resource-group-create-service-principal-portal/show-user.png) 
     
3. <span data-ttu-id="454fd-150">Selecione **Recursos do Azure**.</span><span class="sxs-lookup"><span data-stu-id="454fd-150">Select **Azure resources**.</span></span>

     ![selecionar recursos](./media/resource-group-create-service-principal-portal/select-azure-resources.png) 
3. <span data-ttu-id="454fd-152">Exibir as funções atribuídas e determinar se você tem as permissões adequadas tooassign uma função de tooa de aplicativo do AD.</span><span class="sxs-lookup"><span data-stu-id="454fd-152">View your assigned roles, and determine if you have adequate permissions tooassign an AD app tooa role.</span></span> <span data-ttu-id="454fd-153">Se não, peça ao seu tooadd do administrador de assinatura função administrador do acesso tooUser.</span><span class="sxs-lookup"><span data-stu-id="454fd-153">If not, ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span> <span data-ttu-id="454fd-154">Olá a imagem a seguir, o usuário de Olá é função proprietário toohello atribuído para duas assinaturas, que significa que o usuário tem permissões suficientes.</span><span class="sxs-lookup"><span data-stu-id="454fd-154">In hello following image, hello user is assigned toohello Owner role for two subscriptions, which means that user has adequate permissions.</span></span> 

     ![mostrar permissões](./media/resource-group-create-service-principal-portal/view-assigned-roles.png)

## <a name="create-an-azure-active-directory-application"></a><span data-ttu-id="454fd-156">Criar um aplicativo do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="454fd-156">Create an Azure Active Directory application</span></span>
1. <span data-ttu-id="454fd-157">Fazer logon no tooyour conta do Azure por meio de saudação [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="454fd-157">Log in tooyour Azure Account through hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="454fd-158">Selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="454fd-158">Select **Azure Active Directory**.</span></span>

     ![selecionar azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)

4. <span data-ttu-id="454fd-160">Selecione **Registros do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="454fd-160">Select **App registrations**.</span></span>   

     ![selecionar registros do aplicativo](./media/resource-group-create-service-principal-portal/select-app-registrations.png)
5. <span data-ttu-id="454fd-162">Selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="454fd-162">Select **Add**.</span></span>

     ![adicionar aplicativo](./media/resource-group-create-service-principal-portal/select-add-app.png)

6. <span data-ttu-id="454fd-164">Forneça um nome e uma URL para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="454fd-164">Provide a name and URL for hello application.</span></span> <span data-ttu-id="454fd-165">Selecione **aplicativo Web / API** ou **nativo** para o tipo de saudação do aplicativo que você deseja toocreate.</span><span class="sxs-lookup"><span data-stu-id="454fd-165">Select either **Web app / API** or **Native** for hello type of application you want toocreate.</span></span> <span data-ttu-id="454fd-166">Depois de definir os valores hello, selecione **criar**.</span><span class="sxs-lookup"><span data-stu-id="454fd-166">After setting hello values, select **Create**.</span></span>

     ![nomear aplicativo](./media/resource-group-create-service-principal-portal/create-app.png)

<span data-ttu-id="454fd-168">Você criou seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="454fd-168">You have created your application.</span></span>

## <a name="get-application-id-and-authentication-key"></a><span data-ttu-id="454fd-169">Obter chave de autenticação e ID do aplicativo</span><span class="sxs-lookup"><span data-stu-id="454fd-169">Get application ID and authentication key</span></span>
<span data-ttu-id="454fd-170">Ao fazer logon por meio de programação, é necessário Olá ID para seu aplicativo e uma chave de autenticação.</span><span class="sxs-lookup"><span data-stu-id="454fd-170">When programmatically logging in, you need hello ID for your application and an authentication key.</span></span> <span data-ttu-id="454fd-171">tooget esses valores, Olá use as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="454fd-171">tooget those values, use hello following steps:</span></span>

1. <span data-ttu-id="454fd-172">Em **Registros do Aplicativo** no Azure Active Directory, selecione seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="454fd-172">From **App registrations** in Azure Active Directory, select your application.</span></span>

     ![selecionar aplicativo](./media/resource-group-create-service-principal-portal/select-app.png)
2. <span data-ttu-id="454fd-174">Saudação de cópia **ID do aplicativo** e armazená-la no código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="454fd-174">Copy hello **Application ID** and store it in your application code.</span></span> <span data-ttu-id="454fd-175">Olá aplicativos Olá [aplicativos de exemplo](#sample-applications) seção Consulte valor toothis como id de saudação do cliente.</span><span class="sxs-lookup"><span data-stu-id="454fd-175">hello applications in hello [sample applications](#sample-applications) section refer toothis value as hello client id.</span></span>

     ![ID do CLIENTE](./media/resource-group-create-service-principal-portal/copy-app-id.png)
3. <span data-ttu-id="454fd-177">toogenerate uma chave de autenticação, selecione **chaves**.</span><span class="sxs-lookup"><span data-stu-id="454fd-177">toogenerate an authentication key, select **Keys**.</span></span>

     ![selecionar chaves](./media/resource-group-create-service-principal-portal/select-keys.png)
4. <span data-ttu-id="454fd-179">Forneça uma descrição da chave de saudação e uma duração para a chave de saudação.</span><span class="sxs-lookup"><span data-stu-id="454fd-179">Provide a description of hello key, and a duration for hello key.</span></span> <span data-ttu-id="454fd-180">Ao terminar, escolha **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="454fd-180">When done, select **Save**.</span></span>

     ![salvar chave](./media/resource-group-create-service-principal-portal/save-key.png)

     <span data-ttu-id="454fd-182">Depois de salvar chave hello, Olá valor chave Olá é exibido.</span><span class="sxs-lookup"><span data-stu-id="454fd-182">After saving hello key, hello value of hello key is displayed.</span></span> <span data-ttu-id="454fd-183">Copie esse valor, porque não é capaz de tooretrieve chave de saudação mais tarde.</span><span class="sxs-lookup"><span data-stu-id="454fd-183">Copy this value because you are not able tooretrieve hello key later.</span></span> <span data-ttu-id="454fd-184">Você fornece o valor de chave Olá Olá toolog de ID de aplicativo em como o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="454fd-184">You provide hello key value with hello application ID toolog in as hello application.</span></span> <span data-ttu-id="454fd-185">Armazena o valor de chave Olá onde seu aplicativo pode recuperá-lo.</span><span class="sxs-lookup"><span data-stu-id="454fd-185">Store hello key value where your application can retrieve it.</span></span>

     ![chave salva](./media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a><span data-ttu-id="454fd-187">Obter a ID do locatário</span><span class="sxs-lookup"><span data-stu-id="454fd-187">Get tenant ID</span></span>
<span data-ttu-id="454fd-188">Quando programaticamente o logon, é preciso toopass Olá locatário ID com a solicitação de autenticação.</span><span class="sxs-lookup"><span data-stu-id="454fd-188">When programmatically logging in, you need toopass hello tenant ID with your authentication request.</span></span> 

1. <span data-ttu-id="454fd-189">ID de locatário Olá tooget, selecione **propriedades** para seu locatário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="454fd-189">tooget hello tenant ID, select **Properties** for your Azure AD tenant.</span></span> 

     ![selecionar propriedades do Azure AD](./media/resource-group-create-service-principal-portal/select-ad-properties.png)

2. <span data-ttu-id="454fd-191">Saudação de cópia **ID de diretório**.</span><span class="sxs-lookup"><span data-stu-id="454fd-191">Copy hello **Directory ID**.</span></span> <span data-ttu-id="454fd-192">Esse valor é a ID do locatário.</span><span class="sxs-lookup"><span data-stu-id="454fd-192">This value is your tenant ID.</span></span>

     ![ID do locatário](./media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-toorole"></a><span data-ttu-id="454fd-194">Atribuir o aplicativo toorole</span><span class="sxs-lookup"><span data-stu-id="454fd-194">Assign application toorole</span></span>
<span data-ttu-id="454fd-195">tooaccess recursos em sua assinatura, você deve atribuir a função de tooa aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="454fd-195">tooaccess resources in your subscription, you must assign hello application tooa role.</span></span> <span data-ttu-id="454fd-196">Decida qual função representa permissões corretas de saudação para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="454fd-196">Decide which role represents hello right permissions for hello application.</span></span> <span data-ttu-id="454fd-197">toolearn sobre as funções disponíveis do hello, consulte [RBAC: criado em funções](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="454fd-197">toolearn about hello available roles, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="454fd-198">Você pode definir o escopo de saudação no nível de saudação de assinatura de saudação, o grupo de recursos ou o recurso.</span><span class="sxs-lookup"><span data-stu-id="454fd-198">You can set hello scope at hello level of hello subscription, resource group, or resource.</span></span> <span data-ttu-id="454fd-199">As permissões são herdadas toolower níveis de escopo.</span><span class="sxs-lookup"><span data-stu-id="454fd-199">Permissions are inherited toolower levels of scope.</span></span> <span data-ttu-id="454fd-200">Por exemplo, adicionar que uma função de leitor de toohello de aplicativo para um grupo de recursos significa que ele pode ler o grupo de recursos hello e recursos que ela contém.</span><span class="sxs-lookup"><span data-stu-id="454fd-200">For example, adding an application toohello Reader role for a resource group means it can read hello resource group and any resources it contains.</span></span>

1. <span data-ttu-id="454fd-201">Navegar um nível de toohello de escopo que você deseja que o aplicativo hello tooassign.</span><span class="sxs-lookup"><span data-stu-id="454fd-201">Navigate toohello level of scope you wish tooassign hello application to.</span></span> <span data-ttu-id="454fd-202">Por exemplo, tooassign uma função no escopo de assinatura hello, selecione **assinaturas**.</span><span class="sxs-lookup"><span data-stu-id="454fd-202">For example, tooassign a role at hello subscription scope, select **Subscriptions**.</span></span> <span data-ttu-id="454fd-203">Em vez disso, você pode selecionar um grupo de recursos ou um recurso.</span><span class="sxs-lookup"><span data-stu-id="454fd-203">You could instead select a resource group or resource.</span></span>

     ![selecione a assinatura](./media/resource-group-create-service-principal-portal/select-subscription.png)

2. <span data-ttu-id="454fd-205">Selecione Olá determinada assinatura (grupo de recursos ou recursos) tooassign Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="454fd-205">Select hello particular subscription (resource group or resource) tooassign hello application to.</span></span>

     ![selecionar assinatura para atribuição](./media/resource-group-create-service-principal-portal/select-one-subscription.png)

3. <span data-ttu-id="454fd-207">Selecione **Controle de Acesso (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="454fd-207">Select **Access Control (IAM)**.</span></span>

     ![selecionar acesso](./media/resource-group-create-service-principal-portal/select-access-control.png)

4. <span data-ttu-id="454fd-209">Selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="454fd-209">Select **Add**.</span></span>

     ![escolher adicionar](./media/resource-group-create-service-principal-portal/select-add.png)
6. <span data-ttu-id="454fd-211">Selecione a função de saudação desejar tooassign toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="454fd-211">Select hello role you wish tooassign toohello application.</span></span> <span data-ttu-id="454fd-212">Olá, imagem a seguir mostra Olá **leitor** função.</span><span class="sxs-lookup"><span data-stu-id="454fd-212">hello following image shows hello **Reader** role.</span></span>

     ![escolher função](./media/resource-group-create-service-principal-portal/select-role.png)

8. <span data-ttu-id="454fd-214">Procure seu aplicativo e selecione-o.</span><span class="sxs-lookup"><span data-stu-id="454fd-214">Search for your application, and select it.</span></span>

     ![pesquisar aplicativo](./media/resource-group-create-service-principal-portal/search-app.png)
9. <span data-ttu-id="454fd-216">Selecione **Okey** toofinish atribuição de função hello.</span><span class="sxs-lookup"><span data-stu-id="454fd-216">Select **OK** toofinish assigning hello role.</span></span> <span data-ttu-id="454fd-217">Consulte o seu aplicativo na lista de saudação de usuários atribuídos a função tooa para esse escopo.</span><span class="sxs-lookup"><span data-stu-id="454fd-217">You see your application in hello list of users assigned tooa role for that scope.</span></span>

## <a name="log-in-as-hello-application"></a><span data-ttu-id="454fd-218">Faça logon como um aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="454fd-218">Log in as hello application</span></span>

<span data-ttu-id="454fd-219">Seu aplicativo agora está configurado no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="454fd-219">Your application is now set up in Azure Active Directory.</span></span> <span data-ttu-id="454fd-220">Você tem uma ID e uma chave toouse para fazer logon como um aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="454fd-220">You have an ID and key toouse for signing in as hello application.</span></span> <span data-ttu-id="454fd-221">aplicativo Hello é designado como tooa que concede determinadas ações que ele possa executar.</span><span class="sxs-lookup"><span data-stu-id="454fd-221">hello application is assigned tooa role that gives it certain actions it can perform.</span></span> <span data-ttu-id="454fd-222">Para obter informações sobre como fazer logon como um aplicativo hello através de diferentes plataformas, consulte:</span><span class="sxs-lookup"><span data-stu-id="454fd-222">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="454fd-223">PowerShell</span><span class="sxs-lookup"><span data-stu-id="454fd-223">PowerShell</span></span>](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell)
* [<span data-ttu-id="454fd-224">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="454fd-224">Azure CLI</span></span>](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli)
* [<span data-ttu-id="454fd-225">REST</span><span class="sxs-lookup"><span data-stu-id="454fd-225">REST</span></span>](/rest/api/#create-the-request)
* [<span data-ttu-id="454fd-226">.NET</span><span class="sxs-lookup"><span data-stu-id="454fd-226">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="454fd-227">Java</span><span class="sxs-lookup"><span data-stu-id="454fd-227">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="454fd-228">Node.js</span><span class="sxs-lookup"><span data-stu-id="454fd-228">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="454fd-229">Python</span><span class="sxs-lookup"><span data-stu-id="454fd-229">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="454fd-230">Ruby</span><span class="sxs-lookup"><span data-stu-id="454fd-230">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)


## <a name="next-steps"></a><span data-ttu-id="454fd-231">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="454fd-231">Next steps</span></span>
* <span data-ttu-id="454fd-232">tooset um aplicativo multilocatário, consulte [tooauthorization de guia do desenvolvedor com hello API do Gerenciador de recursos do Azure](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="454fd-232">tooset up a multi-tenant application, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="454fd-233">toolearn sobre como especificar políticas de segurança, consulte [controle de acesso baseado em função do Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="454fd-233">toolearn about specifying security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>  
* <span data-ttu-id="454fd-234">Para obter uma lista de ações disponíveis que podem ser concedidas ou negadas toousers, consulte [operações do provedor de recursos do Gerenciador de recursos do Azure](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="454fd-234">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
