---
title: aaaAzure IoT Suite e do Active Directory do Azure | Microsoft Docs
description: "Descreve como o Azure IoT Suite usa permissões do Active Directory do Azure toomanage."
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
ms.openlocfilehash: 4768630f2de4bb431731fbd4e8929232bc80b9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-on-hello-azureiotsuitecom-site"></a><span data-ttu-id="f85cc-103">Permissões no site de azureiotsuite.com Olá</span><span class="sxs-lookup"><span data-stu-id="f85cc-103">Permissions on hello azureiotsuite.com site</span></span>

## <a name="what-happens-when-you-sign-in"></a><span data-ttu-id="f85cc-104">O que acontece quando você entra</span><span class="sxs-lookup"><span data-stu-id="f85cc-104">What happens when you sign in</span></span>

<span data-ttu-id="f85cc-105">Olá a primeira vez que você entrar no [azureiotsuite.com][lnk-azureiotsuite], site Olá determina os níveis de permissão Olá baseado em Olá atualmente selecionado locatário do Azure Active Directory (AAD) e o Azure assinatura.</span><span class="sxs-lookup"><span data-stu-id="f85cc-105">hello first time you sign in at [azureiotsuite.com][lnk-azureiotsuite], hello site determines hello permission levels you have based on hello currently selected Azure Active Directory (AAD) tenant and Azure subscription.</span></span>

1. <span data-ttu-id="f85cc-106">Primeiro, toopopulate lista de saudação de locatários vistos próximo tooyour username, site Olá encontra do Azure que locatários do AAD você pertence.</span><span class="sxs-lookup"><span data-stu-id="f85cc-106">First, toopopulate hello list of tenants seen next tooyour username, hello site finds out from Azure which AAD tenants you belong to.</span></span> <span data-ttu-id="f85cc-107">Atualmente, site Olá somente pode obter tokens de usuário para um locatário por vez.</span><span class="sxs-lookup"><span data-stu-id="f85cc-107">Currently, hello site can only obtain user tokens for one tenant at a time.</span></span> <span data-ttu-id="f85cc-108">Portanto, quando você alternar locatários usando Olá suspensa no canto superior direito da saudação, site Olá efetua login tokens de saudação do toothat locatário tooobtain para esse locatário.</span><span class="sxs-lookup"><span data-stu-id="f85cc-108">Therefore, when you switch tenants using hello dropdown in hello top right corner, hello site logs you in toothat tenant tooobtain hello tokens for that tenant.</span></span>

2. <span data-ttu-id="f85cc-109">Em seguida, site Olá encontra do Azure quais assinaturas você associou à saudação selecionado locatário.</span><span class="sxs-lookup"><span data-stu-id="f85cc-109">Next, hello site finds out from Azure which subscriptions you have associated with hello selected tenant.</span></span> <span data-ttu-id="f85cc-110">Você verá assinaturas disponíveis hello quando você cria uma nova solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="f85cc-110">You see hello available subscriptions when you create a new preconfigured solution.</span></span>

3. <span data-ttu-id="f85cc-111">Finalmente, o site Olá recupera todos os recursos de saudação em assinaturas de saudação e grupos de recursos marcados como soluções pré-configuradas e preenche blocos Olá Olá home page.</span><span class="sxs-lookup"><span data-stu-id="f85cc-111">Finally, hello site retrieves all hello resources in hello subscriptions and resource groups tagged as preconfigured solutions and populates hello tiles on hello home page.</span></span>

<span data-ttu-id="f85cc-112">Olá seções a seguir descreve funções hello que controlam o acesso toohello pré-configurado soluções.</span><span class="sxs-lookup"><span data-stu-id="f85cc-112">hello following sections describe hello roles that control access toohello preconfigured solutions.</span></span>

## <a name="aad-roles"></a><span data-ttu-id="f85cc-113">Funções do AAD</span><span class="sxs-lookup"><span data-stu-id="f85cc-113">AAD roles</span></span>

<span data-ttu-id="f85cc-114">funções AAD Olá Olá capacidade provisionar pré-configurado soluções de controle e gerenciar usuários em uma solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="f85cc-114">hello AAD roles control hello ability provision preconfigured solutions and manage users in a preconfigured solution.</span></span>

<span data-ttu-id="f85cc-115">Saiba mais sobre funções de administrador no AAD em [Atribuir funções de administrador no Azure AD][lnk-aad-admin].</span><span class="sxs-lookup"><span data-stu-id="f85cc-115">You can find more information about administrator roles in AAD in [Assigning administrator roles in Azure AD][lnk-aad-admin].</span></span> <span data-ttu-id="f85cc-116">artigo atual Olá enfoca Olá **Administrador Global** e hello **usuário** soluções pré-configuradas de funções de diretório conforme é usado pelo hello.</span><span class="sxs-lookup"><span data-stu-id="f85cc-116">hello current article focuses on hello **Global Administrator** and hello **User** directory roles as used by hello preconfigured solutions.</span></span>

### <a name="global-administrator"></a><span data-ttu-id="f85cc-117">Administrador global</span><span class="sxs-lookup"><span data-stu-id="f85cc-117">Global administrator</span></span>

<span data-ttu-id="f85cc-118">Pode haver muitos administradores globais por locatário do AAD:</span><span class="sxs-lookup"><span data-stu-id="f85cc-118">There can be many global administrators per AAD tenant:</span></span>

* <span data-ttu-id="f85cc-119">Quando você cria um locatário do AAD, você está pelo administrador global do saudação padrão do locatário.</span><span class="sxs-lookup"><span data-stu-id="f85cc-119">When you create an AAD tenant, you are by default hello global administrator of that tenant.</span></span>
* <span data-ttu-id="f85cc-120">administrador global Olá pode provisionar uma solução pré-configurada e é atribuído um **Admin** função para o aplicativo hello dentro de seu locatário do AAD.</span><span class="sxs-lookup"><span data-stu-id="f85cc-120">hello global administrator can provision a preconfigured solution and is assigned an **Admin** role for hello application inside their AAD tenant.</span></span>
* <span data-ttu-id="f85cc-121">Se outro usuário Olá mesmo locatário do AAD cria um aplicativo, a função padrão de saudação é concedido de administrador global toohello **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="f85cc-121">If another user in hello same AAD tenant creates an application, hello default role granted toohello global administrator is **ReadOnly**.</span></span>
* <span data-ttu-id="f85cc-122">Um administrador global pode atribuir usuários tooroles para aplicativos que usam Olá [portal do Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="f85cc-122">A global administrator can assign users tooroles for applications using hello [Azure portal][lnk-portal].</span></span>

### <a name="domain-user"></a><span data-ttu-id="f85cc-123">Usuário de domínio</span><span class="sxs-lookup"><span data-stu-id="f85cc-123">Domain user</span></span>

<span data-ttu-id="f85cc-124">Pode haver muitos usuários de domínio por locatário do AAD:</span><span class="sxs-lookup"><span data-stu-id="f85cc-124">There can be many domain users per AAD tenant:</span></span>

* <span data-ttu-id="f85cc-125">Um usuário de domínio pode provisionar uma solução pré-configurada por meio de saudação [azureiotsuite.com] [ lnk-azureiotsuite] site.</span><span class="sxs-lookup"><span data-stu-id="f85cc-125">A domain user can provision a preconfigured solution through hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="f85cc-126">Por padrão, o usuário de domínio Olá é concedido Olá **Admin** função no hello provisionado o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f85cc-126">By default, hello domain user is granted hello **Admin** role in hello provisioned application.</span></span>
* <span data-ttu-id="f85cc-127">Um usuário de domínio pode criar um aplicativo usando o script de build.cmd Olá Olá [azure-iot-monitoramento remoto][lnk-rm-github-repo], [azure iot-previsão manutenção] [ lnk-pm-github-repo], ou [azure iot-conectado-fábrica] [ lnk-cf-github-repo] repositório.</span><span class="sxs-lookup"><span data-stu-id="f85cc-127">A domain user can create an application using hello build.cmd script in hello [azure-iot-remote-monitoring][lnk-rm-github-repo],  [azure-iot-predictive-maintenance][lnk-pm-github-repo], or [azure-iot-connected-factory][lnk-cf-github-repo] repository.</span></span> <span data-ttu-id="f85cc-128">No entanto, a função padrão de saudação concedido toohello usuário de domínio é **ReadOnly**, porque um usuário de domínio não tem funções tooassign de permissão.</span><span class="sxs-lookup"><span data-stu-id="f85cc-128">However, hello default role granted toohello domain user is **ReadOnly**, because a domain user does not have permission tooassign roles.</span></span>
* <span data-ttu-id="f85cc-129">Se outro usuário no locatário do AAD Olá cria um aplicativo, usuário de domínio Olá recebe Olá **ReadOnly** função por padrão para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f85cc-129">If another user in hello AAD tenant creates an application, hello domain user is assigned hello **ReadOnly** role by default for that application.</span></span>
* <span data-ttu-id="f85cc-130">O usuário de domínio não terá a capacidade de atribuir funções para aplicativos, portanto, não poderá adicionar usuários ou funções para usuários para um aplicativo, mesmo se o tiver provisionado.</span><span class="sxs-lookup"><span data-stu-id="f85cc-130">A domain user cannot assign roles for applications; therefore a domain user cannot add users or roles for users for an application even if they provisioned it.</span></span>

### <a name="guest-user"></a><span data-ttu-id="f85cc-131">Usuário Convidado</span><span class="sxs-lookup"><span data-stu-id="f85cc-131">Guest User</span></span>

<span data-ttu-id="f85cc-132">Pode haver muitos usuários convidados por locatário do AAD.</span><span class="sxs-lookup"><span data-stu-id="f85cc-132">There can be many guest users per AAD tenant.</span></span> <span data-ttu-id="f85cc-133">Usuários convidados têm um conjunto limitado de direitos no locatário do AAD hello.</span><span class="sxs-lookup"><span data-stu-id="f85cc-133">Guest users have a limited set of rights in hello AAD tenant.</span></span> <span data-ttu-id="f85cc-134">Como resultado, os usuários convidados não é possível provisionar uma solução pré-configurada no locatário do AAD hello.</span><span class="sxs-lookup"><span data-stu-id="f85cc-134">As a result, guest users cannot provision a preconfigured solution in hello AAD tenant.</span></span>

<span data-ttu-id="f85cc-135">Para obter mais informações sobre usuários e funções no AAD, consulte Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="f85cc-135">For more information about users and roles in AAD, see hello following resources:</span></span>

* <span data-ttu-id="f85cc-136">[Criar usuários no Azure AD][lnk-create-edit-users]</span><span class="sxs-lookup"><span data-stu-id="f85cc-136">[Create users in Azure AD][lnk-create-edit-users]</span></span>
* <span data-ttu-id="f85cc-137">[Atribuir usuários tooapps][lnk-assign-app-roles]</span><span class="sxs-lookup"><span data-stu-id="f85cc-137">[Assign users tooapps][lnk-assign-app-roles]</span></span>

## <a name="azure-subscription-administrator-roles"></a><span data-ttu-id="f85cc-138">Funções de administrador da assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="f85cc-138">Azure subscription administrator roles</span></span>

<span data-ttu-id="f85cc-139">funções de administrador do Azure Olá controlam Olá capacidade toomap um locatário tooan AD de assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="f85cc-139">hello Azure admin roles control hello ability toomap an Azure subscription tooan AD tenant.</span></span>

<span data-ttu-id="f85cc-140">Saiba mais sobre as funções de administrador do Azure Olá artigo Olá [como tooadd ou alterar a conta de administrador, administrador de serviço e Coadministrador do Azure][lnk-admin-roles].</span><span class="sxs-lookup"><span data-stu-id="f85cc-140">Find out more about hello Azure admin roles in hello article [How tooadd or change Azure Co-Administrator, Service Administrator, and Account Administrator][lnk-admin-roles].</span></span>

## <a name="application-roles"></a><span data-ttu-id="f85cc-141">Funções de aplicativo</span><span class="sxs-lookup"><span data-stu-id="f85cc-141">Application roles</span></span>

<span data-ttu-id="f85cc-142">funções de aplicativo Hello controlam acesso toodevices em sua solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="f85cc-142">hello application roles control access toodevices in your preconfigured solution.</span></span>

<span data-ttu-id="f85cc-143">Há duas funções definidas e uma função implícita definida em um aplicativo provisionado:</span><span class="sxs-lookup"><span data-stu-id="f85cc-143">There are two defined roles and one implicit role defined in a provisioned application:</span></span>

* <span data-ttu-id="f85cc-144">**Administração:** tem controle total tooadd, remover dispositivos e modificar as configurações.</span><span class="sxs-lookup"><span data-stu-id="f85cc-144">**Admin:** Has full control tooadd, manage, remove devices, and modify settings.</span></span>
* <span data-ttu-id="f85cc-145">**Somente Leitura:** pode exibir dispositivos, regras, ações, trabalhos e telemetria.</span><span class="sxs-lookup"><span data-stu-id="f85cc-145">**ReadOnly:** Can view devices, rules, actions, jobs, and telemetry.</span></span>

<span data-ttu-id="f85cc-146">Você pode encontrar permissões Olá designado como tooeach no hello [RolePermissions.cs] [ lnk-resource-cs] arquivo de origem.</span><span class="sxs-lookup"><span data-stu-id="f85cc-146">You can find hello permissions assigned tooeach role in hello [RolePermissions.cs][lnk-resource-cs] source file.</span></span>

### <a name="changing-application-roles-for-a-user"></a><span data-ttu-id="f85cc-147">Alterando as funções de aplicativo para um usuário</span><span class="sxs-lookup"><span data-stu-id="f85cc-147">Changing application roles for a user</span></span>

<span data-ttu-id="f85cc-148">Você pode usar o hello seguindo o procedimento toomake um usuário no Active Directory do administrador de sua solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="f85cc-148">You can use hello following procedure toomake a user in your Active Directory an administrator of your preconfigured solution.</span></span>

<span data-ttu-id="f85cc-149">Você deve ter funções de toochange AAD administrador global para um usuário:</span><span class="sxs-lookup"><span data-stu-id="f85cc-149">You must be an AAD global administrator toochange roles for a user:</span></span>

1. <span data-ttu-id="f85cc-150">Vá toohello [portal do Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="f85cc-150">Go toohello [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="f85cc-151">Selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f85cc-151">Select **Azure Active Directory**.</span></span>
3. <span data-ttu-id="f85cc-152">Verifique se que você está usando diretório Olá escolhido em azureiotsuite.com quando você provisionou sua solução.</span><span class="sxs-lookup"><span data-stu-id="f85cc-152">Make sure you are using hello directory you chose on azureiotsuite.com when you provisioned your solution.</span></span> <span data-ttu-id="f85cc-153">Se você tiver vários diretórios associados à sua assinatura, você pode alternar entre eles, se você clicar no nome da conta na saudação de superior direita do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="f85cc-153">If you have multiple directories associated with your subscription, you can switch between them if you click your account name at hello top-right of hello portal.</span></span>
4. <span data-ttu-id="f85cc-154">Clique em **Aplicativos empresariais** e, em seguida, **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f85cc-154">Click **Enterprise applications**, then **All applications**.</span></span>
4. <span data-ttu-id="f85cc-155">Mostrar **Todos os aplicativos** com **Qualquer** status.</span><span class="sxs-lookup"><span data-stu-id="f85cc-155">Show **All applications** with **Any** status.</span></span> <span data-ttu-id="f85cc-156">Então pesquise um aplicativo com o nome da sua solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="f85cc-156">Then search for an application with name of your preconfigured solution.</span></span>
5. <span data-ttu-id="f85cc-157">Clique em nome de saudação do aplicativo hello que coincide com o nome de solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="f85cc-157">Click hello name of hello application that matches your preconfigured solution name.</span></span>
6. <span data-ttu-id="f85cc-158">Clique em **Usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f85cc-158">Click **Users and groups**.</span></span>
7. <span data-ttu-id="f85cc-159">Selecione o usuário a saudação ser tooswitch funções.</span><span class="sxs-lookup"><span data-stu-id="f85cc-159">Select hello user you want tooswitch roles.</span></span>
8. <span data-ttu-id="f85cc-160">Clique em **atribuir** e selecione Olá função (como **Admin**) você gostaria que tooassign toohello usuário, clique em marca de seleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="f85cc-160">Click **Assign** and select hello role (such as **Admin**) you'd like tooassign toohello user, click hello check mark.</span></span>

## <a name="faq"></a><span data-ttu-id="f85cc-161">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="f85cc-161">FAQ</span></span>

### <a name="im-a-service-administrator-and-id-like-toochange-hello-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a><span data-ttu-id="f85cc-162">Sou um administrador de serviço e gostaria de mapeamento de diretório Olá toochange entre minha assinatura e um locatário do AAD específico.</span><span class="sxs-lookup"><span data-stu-id="f85cc-162">I'm a service administrator and I'd like toochange hello directory mapping between my subscription and a specific AAD tenant.</span></span> <span data-ttu-id="f85cc-163">Como posso concluir esta tarefa?</span><span class="sxs-lookup"><span data-stu-id="f85cc-163">How do I complete this task?</span></span>

1. <span data-ttu-id="f85cc-164">Vá toohello [portal clássico do Azure][lnk-classic-portal], clique em **configurações** na lista de saudação de serviços no lado esquerdo da saudação.</span><span class="sxs-lookup"><span data-stu-id="f85cc-164">Go toohello [Azure classic portal][lnk-classic-portal], click **Settings** in hello list of services on hello left-hand side.</span></span>
2. <span data-ttu-id="f85cc-165">Selecione a assinatura de saudação você gostaria que o mapeamento de diretório toochange Olá para.</span><span class="sxs-lookup"><span data-stu-id="f85cc-165">Select hello subscription you'd like toochange hello directory mapping to.</span></span>
3. <span data-ttu-id="f85cc-166">Clique em **Editar Diretório**.</span><span class="sxs-lookup"><span data-stu-id="f85cc-166">Click **Edit Directory**.</span></span>
4. <span data-ttu-id="f85cc-167">Selecione Olá **diretório** você gostaria que toouse na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="f85cc-167">Select hello **Directory** you would like toouse in hello dropdown.</span></span> <span data-ttu-id="f85cc-168">Clique em seta Avançar hello.</span><span class="sxs-lookup"><span data-stu-id="f85cc-168">Click hello forward arrow.</span></span>
5. <span data-ttu-id="f85cc-169">Confirmar o mapeamento de diretório hello e afetados administradores.</span><span class="sxs-lookup"><span data-stu-id="f85cc-169">Confirm hello directory mapping and affected co-administrators.</span></span> <span data-ttu-id="f85cc-170">Se você estiver movendo em outro diretório, todos os administradores saudação do diretório original hello serão removidos.</span><span class="sxs-lookup"><span data-stu-id="f85cc-170">If you are moving from another directory, all hello co-administrators from hello original directory are removed.</span></span>

### <a name="im-a-domain-usermember-on-hello-aad-tenant-and-ive-created-a-preconfigured-solution-how-do-i-get-assigned-a-role-for-my-application"></a><span data-ttu-id="f85cc-171">Sou um usuário/membro do domínio no locatário do AAD hello e criei uma solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="f85cc-171">I'm a domain user/member on hello AAD tenant and I've created a preconfigured solution.</span></span> <span data-ttu-id="f85cc-172">Como recebo uma função para o meu aplicativo?</span><span class="sxs-lookup"><span data-stu-id="f85cc-172">How do I get assigned a role for my application?</span></span>

<span data-ttu-id="f85cc-173">Peça toomake um administrador global é um administrador global no hello AAD locatário e, em seguida, atribuir funções toousers por conta própria.</span><span class="sxs-lookup"><span data-stu-id="f85cc-173">Ask a global administrator toomake you a global administrator on hello AAD tenant and then assign roles toousers yourself.</span></span> <span data-ttu-id="f85cc-174">Como alternativa, peça a um administrador global tooassign é uma função diretamente.</span><span class="sxs-lookup"><span data-stu-id="f85cc-174">Alternatively, ask a global administrator tooassign you a role directly.</span></span> <span data-ttu-id="f85cc-175">Se desejar que o locatário do AAD Olá toochange que sua solução pré-configurada tiver sido implantada, consulte a saudação próxima pergunta.</span><span class="sxs-lookup"><span data-stu-id="f85cc-175">If you'd like toochange hello AAD tenant your preconfigured solution has been deployed to, see hello next question.</span></span>

### <a name="how-do-i-switch-hello-aad-tenant-my-remote-monitoring-preconfigured-solution-and-application-are-assigned-to"></a><span data-ttu-id="f85cc-176">Como alternar o locatário do AAD Olá a que minha solução pré-configurada de monitoramento remota e o aplicativo estão atribuídos?</span><span class="sxs-lookup"><span data-stu-id="f85cc-176">How do I switch hello AAD tenant my remote monitoring preconfigured solution and application are assigned to?</span></span>

<span data-ttu-id="f85cc-177">É possível executar uma implantação de nuvem do <https://github.com/Azure/azure-iot-remote-monitoring> e reimplantar com um locatário do AAD recém-criado.</span><span class="sxs-lookup"><span data-stu-id="f85cc-177">You can run a cloud deployment from <https://github.com/Azure/azure-iot-remote-monitoring> and redeploy with a newly created AAD tenant.</span></span> <span data-ttu-id="f85cc-178">Como são, por padrão, um administrador global quando você cria um locatário do AAD, você tem permissões tooadd os usuários e atribuir funções de usuários toothose.</span><span class="sxs-lookup"><span data-stu-id="f85cc-178">Because you are, by default, a global administrator when you create an AAD tenant, you have permissions tooadd users and assign roles toothose users.</span></span>

1. <span data-ttu-id="f85cc-179">Criar um diretório AAD no hello [portal do Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="f85cc-179">Create an AAD directory in hello [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="f85cc-180">Vá muito<https://github.com/Azure/azure-iot-remote-monitoring>.</span><span class="sxs-lookup"><span data-stu-id="f85cc-180">Go too<https://github.com/Azure/azure-iot-remote-monitoring>.</span></span>
3. <span data-ttu-id="f85cc-181">Execute `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (por exemplo, `build.cmd cloud debug myRMSolution`)</span><span class="sxs-lookup"><span data-stu-id="f85cc-181">Run `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (For example, `build.cmd cloud debug myRMSolution`)</span></span>
4. <span data-ttu-id="f85cc-182">Quando solicitado, defina Olá **tenantid** toobe seu locatário recém-criada em vez de seu locatário anterior.</span><span class="sxs-lookup"><span data-stu-id="f85cc-182">When prompted, set hello **tenantid** toobe your newly created tenant instead of your previous tenant.</span></span>

### <a name="i-want-toochange-a-service-administrator-or-co-administrator-when-logged-in-with-an-organisational-account"></a><span data-ttu-id="f85cc-183">Desejo toochange um administrador de serviço ou Coadministrador quando conectado com uma conta organizacionais</span><span class="sxs-lookup"><span data-stu-id="f85cc-183">I want toochange a Service Administrator or Co-Administrator when logged in with an organisational account</span></span>

<span data-ttu-id="f85cc-184">Consulte o artigo de suporte Olá [alterar administrador de serviço e co-administrador quando conectado com uma conta organizacionais][lnk-service-admins].</span><span class="sxs-lookup"><span data-stu-id="f85cc-184">See hello support article [Changing Service Administrator and Co-Administrator when logged in with an organisational account][lnk-service-admins].</span></span>

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-hello-proper-permissions-toocreate-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a><span data-ttu-id="f85cc-185">Por que vejo este erro?</span><span class="sxs-lookup"><span data-stu-id="f85cc-185">Why am I seeing this error?</span></span> <span data-ttu-id="f85cc-186">"Sua conta não tem Olá permissões adequadas toocreate uma solução.</span><span class="sxs-lookup"><span data-stu-id="f85cc-186">"Your account does not have hello proper permissions toocreate a solution.</span></span> <span data-ttu-id="f85cc-187">Verifique com o administrador da conta ou tente com uma conta diferente."</span><span class="sxs-lookup"><span data-stu-id="f85cc-187">Please check with your account administrator or try with a different account."</span></span>

<span data-ttu-id="f85cc-188">Examine Olá diagrama para obter diretrizes a seguir:</span><span class="sxs-lookup"><span data-stu-id="f85cc-188">Look at hello following diagram for guidance:</span></span>

![][img-flowchart]

> [!NOTE]
> <span data-ttu-id="f85cc-189">Se você continuar erro de saudação toosee após a validação for um administrador global no locatário do AAD hello e um coadministrador de assinatura de hello, peça ao administrador de conta remover usuário hello e reatribuir permissões necessárias nessa ordem.</span><span class="sxs-lookup"><span data-stu-id="f85cc-189">If you continue toosee hello error after validating you are a global administrator on hello AAD tenant and a co-administrator on hello subscription, have your account administrator remove hello user and reassign necessary permissions in this order.</span></span> <span data-ttu-id="f85cc-190">Primeiro, adicione usuário hello como um administrador global e, em seguida, adicionar o usuário como um coadministrador no hello assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="f85cc-190">First, add hello user as a global administrator and then add user as a co-administrator on hello Azure subscription.</span></span> <span data-ttu-id="f85cc-191">Se o problema persistir, entre em contato com [Ajuda e Suporte][lnk-help-support].</span><span class="sxs-lookup"><span data-stu-id="f85cc-191">If issues persist, contact [Help & Support][lnk-help-support].</span></span>

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-toocreate-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a><span data-ttu-id="f85cc-192">Por que estou vendo este erro se eu tenho uma assinatura do Azure?</span><span class="sxs-lookup"><span data-stu-id="f85cc-192">Why am I seeing this error when I have an Azure subscription?</span></span> <span data-ttu-id="f85cc-193">"Uma assinatura do Azure é necessário toocreate pré-configurado soluções.</span><span class="sxs-lookup"><span data-stu-id="f85cc-193">"An Azure subscription is required toocreate pre-configured solutions.</span></span> <span data-ttu-id="f85cc-194">Você pode criar uma conta de avaliação gratuita em apenas alguns minutos.”</span><span class="sxs-lookup"><span data-stu-id="f85cc-194">You can create a free trial account in just a couple of minutes."</span></span>

<span data-ttu-id="f85cc-195">Se você tiver certeza de que você tem uma assinatura do Azure, validar o mapeamento para a sua assinatura de locatário de saudação e certifique-se de locatário de saudação correto está selecionado na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="f85cc-195">If you're certain you have an Azure subscription, validate hello tenant mapping for your subscription and ensure hello correct tenant is selected in hello dropdown.</span></span> <span data-ttu-id="f85cc-196">Se você tiver validado Olá desejado de locatário está correto, execute Olá precede o diagrama e validar o mapeamento de saudação de sua assinatura e este locatário do AAD.</span><span class="sxs-lookup"><span data-stu-id="f85cc-196">If you’ve validated hello desired tenant is correct, follow hello preceding diagram and validate hello mapping of your subscription and this AAD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f85cc-197">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f85cc-197">Next steps</span></span>
<span data-ttu-id="f85cc-198">toocontinue aprendendo sobre IoT Suite, consulte como é possível [personalizar uma solução pré-configurada][lnk-customize].</span><span class="sxs-lookup"><span data-stu-id="f85cc-198">toocontinue learning about IoT Suite, see how you can [customize a preconfigured solution][lnk-customize].</span></span>

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
