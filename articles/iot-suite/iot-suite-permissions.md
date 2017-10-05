---
title: Azure IoT Suite e Azure Active Directory | Microsoft Docs
description: "Descreve como o Pacote IoT do Azure usa o Active Directory do Azure para gerenciar permissões."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 246228ba-954a-4d96-b6d6-e53e4590cb4f
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: dobett
ms.openlocfilehash: 518e6a481ab6385b03dd3ddc2e155fb724e677fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="permissions-on-the-azureiotsuitecom-site"></a><span data-ttu-id="c6397-103">Permissões no site azureiotsuite.com</span><span class="sxs-lookup"><span data-stu-id="c6397-103">Permissions on the azureiotsuite.com site</span></span>

## <a name="what-happens-when-you-sign-in"></a><span data-ttu-id="c6397-104">O que acontece quando você entra</span><span class="sxs-lookup"><span data-stu-id="c6397-104">What happens when you sign in</span></span>

<span data-ttu-id="c6397-105">Quando você entra pela primeira vez no [azureiotsuite.com][lnk-azureiotsuite], o site determina os níveis de permissão que você tem com base no locatário do AAD (Azure Active Directory) e na assinatura do Azure selecionados no momento.</span><span class="sxs-lookup"><span data-stu-id="c6397-105">The first time you sign in at [azureiotsuite.com][lnk-azureiotsuite], the site determines the permission levels you have based on the currently selected Azure Active Directory (AAD) tenant and Azure subscription.</span></span>

1. <span data-ttu-id="c6397-106">Primeiro, para preencher a lista de locatários logo ao lado de seu nome de usuário, site descobre a quais locatários do AAD no Azure você pertence.</span><span class="sxs-lookup"><span data-stu-id="c6397-106">First, to populate the list of tenants seen next to your username, the site finds out from Azure which AAD tenants you belong to.</span></span> <span data-ttu-id="c6397-107">No momento, o site só consegue obter os tokens de usuário de um locatário por vez.</span><span class="sxs-lookup"><span data-stu-id="c6397-107">Currently, the site can only obtain user tokens for one tenant at a time.</span></span> <span data-ttu-id="c6397-108">Por isso, quando você alternar locatários usando o menu suspenso no canto superior direito, o site conectará você a esse locatário para obter os tokens para ele.</span><span class="sxs-lookup"><span data-stu-id="c6397-108">Therefore, when you switch tenants using the dropdown in the top right corner, the site logs you in to that tenant to obtain the tokens for that tenant.</span></span>

2. <span data-ttu-id="c6397-109">Em seguida, o site descobre no Azure quais assinaturas estão associadas ao locatário selecionado.</span><span class="sxs-lookup"><span data-stu-id="c6397-109">Next, the site finds out from Azure which subscriptions you have associated with the selected tenant.</span></span> <span data-ttu-id="c6397-110">Você verá as assinaturas quando criar uma nova solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="c6397-110">You see the available subscriptions when you create a new preconfigured solution.</span></span>

3. <span data-ttu-id="c6397-111">Por fim, o site recuperará todos os recursos nas assinaturas e nos grupos de recursos marcados como soluções pré-configuradas e preencherá os blocos na home page.</span><span class="sxs-lookup"><span data-stu-id="c6397-111">Finally, the site retrieves all the resources in the subscriptions and resource groups tagged as preconfigured solutions and populates the tiles on the home page.</span></span>

<span data-ttu-id="c6397-112">As seções a seguir descrevem as funções que controlam o acesso às soluções pré-configuradas.</span><span class="sxs-lookup"><span data-stu-id="c6397-112">The following sections describe the roles that control access to the preconfigured solutions.</span></span>

## <a name="aad-roles"></a><span data-ttu-id="c6397-113">Funções do AAD</span><span class="sxs-lookup"><span data-stu-id="c6397-113">AAD roles</span></span>

<span data-ttu-id="c6397-114">As funções do AAD controlam as soluções pré-configuradas de provisão de capacidade e gerenciam usuários em uma solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="c6397-114">The AAD roles control the ability provision preconfigured solutions and manage users in a preconfigured solution.</span></span>

<span data-ttu-id="c6397-115">Saiba mais sobre funções de administrador no AAD em [Atribuir funções de administrador no Azure AD][lnk-aad-admin].</span><span class="sxs-lookup"><span data-stu-id="c6397-115">You can find more information about administrator roles in AAD in [Assigning administrator roles in Azure AD][lnk-aad-admin].</span></span> <span data-ttu-id="c6397-116">O artigo atual enfoca as funções do diretório **Administrador Global** e **Usuário** conforme utilizadas pelas soluções pré-configuradas.</span><span class="sxs-lookup"><span data-stu-id="c6397-116">The current article focuses on the **Global Administrator** and the **User** directory roles as used by the preconfigured solutions.</span></span>

### <a name="global-administrator"></a><span data-ttu-id="c6397-117">Administrador global</span><span class="sxs-lookup"><span data-stu-id="c6397-117">Global administrator</span></span>

<span data-ttu-id="c6397-118">Pode haver muitos administradores globais por locatário do AAD:</span><span class="sxs-lookup"><span data-stu-id="c6397-118">There can be many global administrators per AAD tenant:</span></span>

* <span data-ttu-id="c6397-119">Quando você cria um locatário do AAD, por padrão vira o administrador global desse locatário.</span><span class="sxs-lookup"><span data-stu-id="c6397-119">When you create an AAD tenant, you are by default the global administrator of that tenant.</span></span>
* <span data-ttu-id="c6397-120">O administrador global pode provisionar uma solução pré-configurada e recebe uma função de **Administrador** para o aplicativo dentro do seu locatário do AAD.</span><span class="sxs-lookup"><span data-stu-id="c6397-120">The global administrator can provision a preconfigured solution and is assigned an **Admin** role for the application inside their AAD tenant.</span></span>
* <span data-ttu-id="c6397-121">Se outro usuário no mesmo locatário do AAD criar um aplicativo, a função padrão concedida ao administrador global será **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="c6397-121">If another user in the same AAD tenant creates an application, the default role granted to the global administrator is **ReadOnly**.</span></span>
* <span data-ttu-id="c6397-122">Um administrador global pode atribuir usuários a funções para aplicativos usando o [Portal do Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="c6397-122">A global administrator can assign users to roles for applications using the [Azure portal][lnk-portal].</span></span>

### <a name="domain-user"></a><span data-ttu-id="c6397-123">Usuário de domínio</span><span class="sxs-lookup"><span data-stu-id="c6397-123">Domain user</span></span>

<span data-ttu-id="c6397-124">Pode haver muitos usuários de domínio por locatário do AAD:</span><span class="sxs-lookup"><span data-stu-id="c6397-124">There can be many domain users per AAD tenant:</span></span>

* <span data-ttu-id="c6397-125">Um usuário do domínio pode provisionar uma solução pré-configurada por meio do site [azureiotsuite.com][lnk-azureiotsuite].</span><span class="sxs-lookup"><span data-stu-id="c6397-125">A domain user can provision a preconfigured solution through the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="c6397-126">Por padrão, a função **Admin** é concedida ao usuário de domínio no aplicativo provisionado.</span><span class="sxs-lookup"><span data-stu-id="c6397-126">By default, the domain user is granted the **Admin** role in the provisioned application.</span></span>
* <span data-ttu-id="c6397-127">Um usuário de domínio pode criar um aplicativo usando o script build.cmd no repositório [azure-iot-remote-monitoring][lnk-rm-github-repo], [azure-iot-predictive-maintenance][lnk-pm-github-repo] ou [azure-iot-connected-factory][lnk-cf-github-repo].</span><span class="sxs-lookup"><span data-stu-id="c6397-127">A domain user can create an application using the build.cmd script in the [azure-iot-remote-monitoring][lnk-rm-github-repo],  [azure-iot-predictive-maintenance][lnk-pm-github-repo], or [azure-iot-connected-factory][lnk-cf-github-repo] repository.</span></span> <span data-ttu-id="c6397-128">No entanto, a função padrão concedida ao usuário de domínio é **ReadOnly**, porque um usuário de domínio não tem permissão para atribuir funções.</span><span class="sxs-lookup"><span data-stu-id="c6397-128">However, the default role granted to the domain user is **ReadOnly**, because a domain user does not have permission to assign roles.</span></span>
* <span data-ttu-id="c6397-129">Se outro usuário no locatário do AAD criar um aplicativo, o usuário de domínio será atribuído à função **ReadOnly** por padrão para esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c6397-129">If another user in the AAD tenant creates an application, the domain user is assigned the **ReadOnly** role by default for that application.</span></span>
* <span data-ttu-id="c6397-130">O usuário de domínio não terá a capacidade de atribuir funções para aplicativos, portanto, não poderá adicionar usuários ou funções para usuários para um aplicativo, mesmo se o tiver provisionado.</span><span class="sxs-lookup"><span data-stu-id="c6397-130">A domain user cannot assign roles for applications; therefore a domain user cannot add users or roles for users for an application even if they provisioned it.</span></span>

### <a name="guest-user"></a><span data-ttu-id="c6397-131">Usuário Convidado</span><span class="sxs-lookup"><span data-stu-id="c6397-131">Guest User</span></span>

<span data-ttu-id="c6397-132">Pode haver muitos usuários convidados por locatário do AAD.</span><span class="sxs-lookup"><span data-stu-id="c6397-132">There can be many guest users per AAD tenant.</span></span> <span data-ttu-id="c6397-133">Os usuários convidados têm um conjunto limitado de direitos no locatário do AAD.</span><span class="sxs-lookup"><span data-stu-id="c6397-133">Guest users have a limited set of rights in the AAD tenant.</span></span> <span data-ttu-id="c6397-134">Como resultado, os usuários convidados não podem provisionar uma solução pré-configurada no locatário do AAD.</span><span class="sxs-lookup"><span data-stu-id="c6397-134">As a result, guest users cannot provision a preconfigured solution in the AAD tenant.</span></span>

<span data-ttu-id="c6397-135">Para obter mais informações sobre usuários e funções no AAD, confira os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="c6397-135">For more information about users and roles in AAD, see the following resources:</span></span>

* <span data-ttu-id="c6397-136">[Criar usuários no Azure AD][lnk-create-edit-users]</span><span class="sxs-lookup"><span data-stu-id="c6397-136">[Create users in Azure AD][lnk-create-edit-users]</span></span>
* <span data-ttu-id="c6397-137">[Atribuir usuários a aplicativos][lnk-assign-app-roles]</span><span class="sxs-lookup"><span data-stu-id="c6397-137">[Assign users to apps][lnk-assign-app-roles]</span></span>

## <a name="azure-subscription-administrator-roles"></a><span data-ttu-id="c6397-138">Funções de administrador da assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="c6397-138">Azure subscription administrator roles</span></span>

<span data-ttu-id="c6397-139">As funções de administrador do Azure controlam a capacidade de mapear uma assinatura do Azure para um locatário do AD.</span><span class="sxs-lookup"><span data-stu-id="c6397-139">The Azure admin roles control the ability to map an Azure subscription to an AD tenant.</span></span>

<span data-ttu-id="c6397-140">Descubra mais sobre as funções de administrador do Azure no artigo [Como adicionar ou alterar o Coadministrador, o Administrador de Serviços e o Administrador da Conta do Azure][lnk-admin-roles].</span><span class="sxs-lookup"><span data-stu-id="c6397-140">Find out more about the Azure admin roles in the article [How to add or change Azure Co-Administrator, Service Administrator, and Account Administrator][lnk-admin-roles].</span></span>

## <a name="application-roles"></a><span data-ttu-id="c6397-141">Funções de aplicativo</span><span class="sxs-lookup"><span data-stu-id="c6397-141">Application roles</span></span>

<span data-ttu-id="c6397-142">As funções do aplicativo controlam o acesso a dispositivos em sua solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="c6397-142">The application roles control access to devices in your preconfigured solution.</span></span>

<span data-ttu-id="c6397-143">Há duas funções definidas e uma função implícita definida em um aplicativo provisionado:</span><span class="sxs-lookup"><span data-stu-id="c6397-143">There are two defined roles and one implicit role defined in a provisioned application:</span></span>

* <span data-ttu-id="c6397-144">**Administrador:** tem controle total para adicionar, gerenciar, remover dispositivos e modificar configurações.</span><span class="sxs-lookup"><span data-stu-id="c6397-144">**Admin:** Has full control to add, manage, remove devices, and modify settings.</span></span>
* <span data-ttu-id="c6397-145">**Somente Leitura:** pode exibir dispositivos, regras, ações, trabalhos e telemetria.</span><span class="sxs-lookup"><span data-stu-id="c6397-145">**ReadOnly:** Can view devices, rules, actions, jobs, and telemetry.</span></span>

<span data-ttu-id="c6397-146">Você pode encontrar as permissões atribuídas a cada função no arquivo de origem [RolePermissions.cs][lnk-resource-cs].</span><span class="sxs-lookup"><span data-stu-id="c6397-146">You can find the permissions assigned to each role in the [RolePermissions.cs][lnk-resource-cs] source file.</span></span>

### <a name="changing-application-roles-for-a-user"></a><span data-ttu-id="c6397-147">Alterando as funções de aplicativo para um usuário</span><span class="sxs-lookup"><span data-stu-id="c6397-147">Changing application roles for a user</span></span>

<span data-ttu-id="c6397-148">Você pode usar o procedimento a seguir para tornar um usuário em seu Active Directory um administrador de sua solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="c6397-148">You can use the following procedure to make a user in your Active Directory an administrator of your preconfigured solution.</span></span>

<span data-ttu-id="c6397-149">Você deve ser um administrador global do AAD para alterar funções para um usuário:</span><span class="sxs-lookup"><span data-stu-id="c6397-149">You must be an AAD global administrator to change roles for a user:</span></span>

1. <span data-ttu-id="c6397-150">Acesse o [Portal do Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="c6397-150">Go to the [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="c6397-151">Selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c6397-151">Select **Azure Active Directory**.</span></span>
3. <span data-ttu-id="c6397-152">Verifique se que você está usando o diretório que você escolheu em azureiotsuite.com ao provisionar sua solução.</span><span class="sxs-lookup"><span data-stu-id="c6397-152">Make sure you are using the directory you chose on azureiotsuite.com when you provisioned your solution.</span></span> <span data-ttu-id="c6397-153">Se você tiver vários diretórios associados à sua assinatura, poderá alternar entre eles se clicar no nome da conta na parte superior direita do portal.</span><span class="sxs-lookup"><span data-stu-id="c6397-153">If you have multiple directories associated with your subscription, you can switch between them if you click your account name at the top-right of the portal.</span></span>
4. <span data-ttu-id="c6397-154">Clique em **Aplicativos empresariais** e, em seguida, **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c6397-154">Click **Enterprise applications**, then **All applications**.</span></span>
4. <span data-ttu-id="c6397-155">Mostrar **Todos os aplicativos** com **Qualquer** status.</span><span class="sxs-lookup"><span data-stu-id="c6397-155">Show **All applications** with **Any** status.</span></span> <span data-ttu-id="c6397-156">Então pesquise um aplicativo com o nome da sua solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="c6397-156">Then search for an application with name of your preconfigured solution.</span></span>
5. <span data-ttu-id="c6397-157">Clique no nome do aplicativo que corresponda ao nome da solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="c6397-157">Click the name of the application that matches your preconfigured solution name.</span></span>
6. <span data-ttu-id="c6397-158">Clique em **Usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c6397-158">Click **Users and groups**.</span></span>
7. <span data-ttu-id="c6397-159">Selecione o usuário para o qual você deseja alternar funções.</span><span class="sxs-lookup"><span data-stu-id="c6397-159">Select the user you want to switch roles.</span></span>
8. <span data-ttu-id="c6397-160">Clique em **Atribuir** e selecione a função (como **Administrador**) que você deseja atribuir ao usuário, então clique na marca de seleção.</span><span class="sxs-lookup"><span data-stu-id="c6397-160">Click **Assign** and select the role (such as **Admin**) you'd like to assign to the user, click the check mark.</span></span>

## <a name="faq"></a><span data-ttu-id="c6397-161">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="c6397-161">FAQ</span></span>

### <a name="im-a-service-administrator-and-id-like-to-change-the-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a><span data-ttu-id="c6397-162">Sou um administrador de serviços e gostaria de alterar o mapeamento de diretório entre minha assinatura e um locatário do AAD específico.</span><span class="sxs-lookup"><span data-stu-id="c6397-162">I'm a service administrator and I'd like to change the directory mapping between my subscription and a specific AAD tenant.</span></span> <span data-ttu-id="c6397-163">Como posso concluir esta tarefa?</span><span class="sxs-lookup"><span data-stu-id="c6397-163">How do I complete this task?</span></span>

1. <span data-ttu-id="c6397-164">Vá para o [Portal Clássico do Azure][lnk-classic-portal], clique em **Configurações** na lista de serviços no lado esquerdo.</span><span class="sxs-lookup"><span data-stu-id="c6397-164">Go to the [Azure classic portal][lnk-classic-portal], click **Settings** in the list of services on the left-hand side.</span></span>
2. <span data-ttu-id="c6397-165">Selecione a assinatura para a qual você deseja alterar o mapeamento de diretórios.</span><span class="sxs-lookup"><span data-stu-id="c6397-165">Select the subscription you'd like to change the directory mapping to.</span></span>
3. <span data-ttu-id="c6397-166">Clique em **Editar Diretório**.</span><span class="sxs-lookup"><span data-stu-id="c6397-166">Click **Edit Directory**.</span></span>
4. <span data-ttu-id="c6397-167">Selecione o **Diretório** que você deseja usar na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="c6397-167">Select the **Directory** you would like to use in the dropdown.</span></span> <span data-ttu-id="c6397-168">Clique na seta para frente.</span><span class="sxs-lookup"><span data-stu-id="c6397-168">Click the forward arrow.</span></span>
5. <span data-ttu-id="c6397-169">Confirme o mapeamento de diretórios e os coadministradores afetados.</span><span class="sxs-lookup"><span data-stu-id="c6397-169">Confirm the directory mapping and affected co-administrators.</span></span> <span data-ttu-id="c6397-170">Se você estiver fazendo a transferência de outro diretório, todos os administradores do diretório original serão removidos.</span><span class="sxs-lookup"><span data-stu-id="c6397-170">If you are moving from another directory, all the co-administrators from the original directory are removed.</span></span>

### <a name="im-a-domain-usermember-on-the-aad-tenant-and-ive-created-a-preconfigured-solution-how-do-i-get-assigned-a-role-for-my-application"></a><span data-ttu-id="c6397-171">Sou um usuário/membro do domínio no locatário do AAD e criei uma solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="c6397-171">I'm a domain user/member on the AAD tenant and I've created a preconfigured solution.</span></span> <span data-ttu-id="c6397-172">Como recebo uma função para o meu aplicativo?</span><span class="sxs-lookup"><span data-stu-id="c6397-172">How do I get assigned a role for my application?</span></span>

<span data-ttu-id="c6397-173">Peça ao administrador global para tornar você um administrador global no locatário AAD e, em seguida, atribua funções aos usuários por conta própria.</span><span class="sxs-lookup"><span data-stu-id="c6397-173">Ask a global administrator to make you a global administrator on the AAD tenant and then assign roles to users yourself.</span></span> <span data-ttu-id="c6397-174">Como alternativa, peça ao administrador global para atribuir uma função a você diretamente.</span><span class="sxs-lookup"><span data-stu-id="c6397-174">Alternatively, ask a global administrator to assign you a role directly.</span></span> <span data-ttu-id="c6397-175">Se desejar alterar o locatário do AAD em que sua solução pré-configurada foi implantada, consulte a próxima pergunta.</span><span class="sxs-lookup"><span data-stu-id="c6397-175">If you'd like to change the AAD tenant your preconfigured solution has been deployed to, see the next question.</span></span>

### <a name="how-do-i-switch-the-aad-tenant-my-remote-monitoring-preconfigured-solution-and-application-are-assigned-to"></a><span data-ttu-id="c6397-176">Como alternar o locatário do AAD ao qual minha solução pré-configurada de monitoramento remoto e o aplicativo estão atribuídos?</span><span class="sxs-lookup"><span data-stu-id="c6397-176">How do I switch the AAD tenant my remote monitoring preconfigured solution and application are assigned to?</span></span>

<span data-ttu-id="c6397-177">É possível executar uma implantação de nuvem do <https://github.com/Azure/azure-iot-remote-monitoring> e reimplantar com um locatário do AAD recém-criado.</span><span class="sxs-lookup"><span data-stu-id="c6397-177">You can run a cloud deployment from <https://github.com/Azure/azure-iot-remote-monitoring> and redeploy with a newly created AAD tenant.</span></span> <span data-ttu-id="c6397-178">Já que você é, por padrão, um administrador global quando cria um novo locatário do AAD, você tem permissões para adicionar usuários e atribuir funções a eles.</span><span class="sxs-lookup"><span data-stu-id="c6397-178">Because you are, by default, a global administrator when you create an AAD tenant, you have permissions to add users and assign roles to those users.</span></span>

1. <span data-ttu-id="c6397-179">Crie um diretório do AAD no [Portal do Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="c6397-179">Create an AAD directory in the [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="c6397-180">Acesse <https://github.com/Azure/azure-iot-remote-monitoring>.</span><span class="sxs-lookup"><span data-stu-id="c6397-180">Go to <https://github.com/Azure/azure-iot-remote-monitoring>.</span></span>
3. <span data-ttu-id="c6397-181">Execute `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (por exemplo, `build.cmd cloud debug myRMSolution`)</span><span class="sxs-lookup"><span data-stu-id="c6397-181">Run `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (For example, `build.cmd cloud debug myRMSolution`)</span></span>
4. <span data-ttu-id="c6397-182">Quando solicitado, defina a **tenantid** para seu locatário recém-criado em vez do locatário anterior.</span><span class="sxs-lookup"><span data-stu-id="c6397-182">When prompted, set the **tenantid** to be your newly created tenant instead of your previous tenant.</span></span>

### <a name="i-want-to-change-a-service-administrator-or-co-administrator-when-logged-in-with-an-organisational-account"></a><span data-ttu-id="c6397-183">Quero alterar um Administrador de Serviços ou um Coadministrador quando o logon for feito com uma conta organizacional</span><span class="sxs-lookup"><span data-stu-id="c6397-183">I want to change a Service Administrator or Co-Administrator when logged in with an organisational account</span></span>

<span data-ttu-id="c6397-184">Consulte o artigo de suporte [Alterando um Administrador de Serviços e um Coadministrador quando o logon for feito com uma conta organizacional][lnk-service-admins].</span><span class="sxs-lookup"><span data-stu-id="c6397-184">See the support article [Changing Service Administrator and Co-Administrator when logged in with an organisational account][lnk-service-admins].</span></span>

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-the-proper-permissions-to-create-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a><span data-ttu-id="c6397-185">Por que vejo este erro?</span><span class="sxs-lookup"><span data-stu-id="c6397-185">Why am I seeing this error?</span></span> <span data-ttu-id="c6397-186">"Sua conta não tem as permissões adequadas para criar uma solução.</span><span class="sxs-lookup"><span data-stu-id="c6397-186">"Your account does not have the proper permissions to create a solution.</span></span> <span data-ttu-id="c6397-187">Verifique com o administrador da conta ou tente com uma conta diferente."</span><span class="sxs-lookup"><span data-stu-id="c6397-187">Please check with your account administrator or try with a different account."</span></span>

<span data-ttu-id="c6397-188">Observe o seguinte diagrama para obter orientação:</span><span class="sxs-lookup"><span data-stu-id="c6397-188">Look at the following diagram for guidance:</span></span>

![][img-flowchart]

> [!NOTE]
> <span data-ttu-id="c6397-189">Se você continuar recebendo o erro após validar que é um administrador global no locatário do AAD e um coadministrador na assinatura, peça ao administrador da conta que remova o usuário e reatribua as permissões necessárias nesta ordem.</span><span class="sxs-lookup"><span data-stu-id="c6397-189">If you continue to see the error after validating you are a global administrator on the AAD tenant and a co-administrator on the subscription, have your account administrator remove the user and reassign necessary permissions in this order.</span></span> <span data-ttu-id="c6397-190">Primeiro, adicione o usuário como um administrador global e adicionar o usuário como um coadministrador na assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6397-190">First, add the user as a global administrator and then add user as a co-administrator on the Azure subscription.</span></span> <span data-ttu-id="c6397-191">Se o problema persistir, entre em contato com [Ajuda e Suporte][lnk-help-support].</span><span class="sxs-lookup"><span data-stu-id="c6397-191">If issues persist, contact [Help & Support][lnk-help-support].</span></span>

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-to-create-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a><span data-ttu-id="c6397-192">Por que estou vendo este erro se eu tenho uma assinatura do Azure?</span><span class="sxs-lookup"><span data-stu-id="c6397-192">Why am I seeing this error when I have an Azure subscription?</span></span> <span data-ttu-id="c6397-193">“Uma assinatura do Azure é necessária para criar soluções pré-configuradas.</span><span class="sxs-lookup"><span data-stu-id="c6397-193">"An Azure subscription is required to create pre-configured solutions.</span></span> <span data-ttu-id="c6397-194">Você pode criar uma conta de avaliação gratuita em apenas alguns minutos.”</span><span class="sxs-lookup"><span data-stu-id="c6397-194">You can create a free trial account in just a couple of minutes."</span></span>

<span data-ttu-id="c6397-195">Se você tiver certeza de que tem uma assinatura do Azure, valide o mapeamento do locatário para a sua assinatura e certifique-se de que o locatário correto tenha sido selecionado na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="c6397-195">If you're certain you have an Azure subscription, validate the tenant mapping for your subscription and ensure the correct tenant is selected in the dropdown.</span></span> <span data-ttu-id="c6397-196">Se você tiver validado corretamente o locatário desejado, siga o diagrama acima e valide o mapeamento de sua assinatura e este locatário do AAD.</span><span class="sxs-lookup"><span data-stu-id="c6397-196">If you’ve validated the desired tenant is correct, follow the preceding diagram and validate the mapping of your subscription and this AAD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6397-197">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c6397-197">Next steps</span></span>
<span data-ttu-id="c6397-198">Para continuar aprendendo sobre o IoT Suite, veja como é possível [personalizar uma solução pré-configurada][lnk-customize].</span><span class="sxs-lookup"><span data-stu-id="c6397-198">To continue learning about IoT Suite, see how you can [customize a preconfigured solution][lnk-customize].</span></span>

[img-flowchart]: media/iot-suite-permissions/flowchart.png

[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-rm-github-repo]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-pm-github-repo]: https://github.com/Azure/azure-iot-predictive-maintenance
[lnk-cf-github-repo]: https://github.com/Azure/azure-iot-connected-factory
[lnk-aad-admin]: ../active-directory/active-directory-assign-admin-roles.md
[lnk-classic-portal]: https://manage.windowsazure.com/
[lnk-portal]: https://portal.azure.com/
[lnk-create-edit-users]: ../active-directory/active-directory-create-users.md
[lnk-assign-app-roles]: ../active-directory/active-directory-coreapps-assign-user-azure-portal.md
[lnk-service-admins]: https://azure.microsoft.com/support/changing-service-admin-and-co-admin/
[lnk-admin-roles]: ../billing/billing-add-change-azure-subscription-administrator.md
[lnk-resource-cs]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/DeviceAdministration/Web/Security/RolePermissions.cs
[lnk-help-support]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
