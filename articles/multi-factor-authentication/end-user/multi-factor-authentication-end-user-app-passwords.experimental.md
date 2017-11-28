---
title: aaaHow toouse senhas de aplicativo no Azure MFA? | Microsoft Docs
description: "Esta página ajuda os usuários a entender quais são as senhas de aplicativo e o que são usados para com relação tooAzure MFA."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 345b757b-5a2b-48eb-953f-d363313be9e5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 3afa2003d8e87576f035bf9440a1dba67bd85f5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a><span data-ttu-id="c05ca-104">O que são as senhas de aplicativo no Azure Multi-Factor Authentication?</span><span class="sxs-lookup"><span data-stu-id="c05ca-104">What are App Passwords in Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="c05ca-105">Determinados aplicativos sem navegador, como o cliente de email nativo do hello Apple que usa o Exchange Active Sync, atualmente não dão suporte a autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="c05ca-105">Certain non-browser apps, such as hello Apple native email client that uses Exchange Active Sync, currently do not support multi-factor authentication.</span></span> <span data-ttu-id="c05ca-106">O Multi-Factor Authentication é habilitado por usuário.</span><span class="sxs-lookup"><span data-stu-id="c05ca-106">Multi-factor authentication is enabled per user.</span></span>  <span data-ttu-id="c05ca-107">Isso significa que um usuário não poderá usar a autenticação multifator se:</span><span class="sxs-lookup"><span data-stu-id="c05ca-107">This means that a user can't use multi-factor authentication if:</span></span>

- <span data-ttu-id="c05ca-108">Olá usuário foi habilitado para autenticação multifator</span><span class="sxs-lookup"><span data-stu-id="c05ca-108">hello user has been enabled for multi-factor authentication</span></span>
- <span data-ttu-id="c05ca-109">usuário Hello está tentando toouse um aplicativo sem navegador.</span><span class="sxs-lookup"><span data-stu-id="c05ca-109">hello user is trying toouse a non-browser app.</span></span>

<span data-ttu-id="c05ca-110">Uma senha de aplicativo permite Olá usuário toouse Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c05ca-110">An app password allows hello user toouse hello app.</span></span>

<span data-ttu-id="c05ca-111">Quando tiver uma senha de aplicativo, você poderá usá-la no lugar da senha original com esses aplicativos que não usam navegador.</span><span class="sxs-lookup"><span data-stu-id="c05ca-111">Once you have an app password, you use it in place of your original password with these non-browser apps.</span></span> <span data-ttu-id="c05ca-112">Quando você registrar para verificação em duas etapas, você está dizendo Microsoft não toolet qualquer pessoa entrar com sua senha se elas também não é possível executar a verificação segundo hello.</span><span class="sxs-lookup"><span data-stu-id="c05ca-112">When you register for two-step verification, you're telling Microsoft not toolet anyone sign in with your password if they can't also perform hello second verification.</span></span> <span data-ttu-id="c05ca-113">cliente de email nativo Olá Apple em seu telefone não pode entrar como você porque ele não é possível solicitar a verificação em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="c05ca-113">hello Apple native email client on your phone can't sign in as you because it can't ask for two-step verification.</span></span> <span data-ttu-id="c05ca-114">Olá, solução toothis problema é toocreate uma senha mais segura do aplicativo que você não use diárias.</span><span class="sxs-lookup"><span data-stu-id="c05ca-114">hello solution toothis problem is toocreate a more secure app password that you don't use day-to-day.</span></span> <span data-ttu-id="c05ca-115">As senhas de aplicativo são apenas para os aplicativos que não oferecem suporte à verificação em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="c05ca-115">App passwords are only for those apps that can't support two-step verification.</span></span> <span data-ttu-id="c05ca-116">Use senha de aplicativo hello para que os aplicativos podem ignorar a autenticação multifator e continuar toowork.</span><span class="sxs-lookup"><span data-stu-id="c05ca-116">Use hello app password so that apps can bypass multi-factor authentication and continue toowork.</span></span>


> [!NOTE]
> <span data-ttu-id="c05ca-117">Os clientes do Office 2013 (incluindo Outlook) são compatíveis com novos protocolos de autenticação e podem ser usados com a verificação em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="c05ca-117">Office 2013 clients (including Outlook) support new authentication protocols and can be used with two-step verification.</span></span> <span data-ttu-id="c05ca-118">As senhas de aplicativo não são necessárias para usar com os clientes do Office 2013.</span><span class="sxs-lookup"><span data-stu-id="c05ca-118">App passwords are not required for use with Office 2013 clients.</span></span>  <span data-ttu-id="c05ca-119">Para saber mais, veja [Anúncio da visualização pública da autenticação moderna do Office 2013](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).</span><span class="sxs-lookup"><span data-stu-id="c05ca-119">For more information, see [Office 2013 modern authentication public preview announced](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).</span></span>


## <a name="how-toouse-app-passwords"></a><span data-ttu-id="c05ca-120">Como as senhas de aplicativo toouse</span><span class="sxs-lookup"><span data-stu-id="c05ca-120">How toouse app passwords</span></span>
<span data-ttu-id="c05ca-121">Aqui estão alguns tooknow coisas sobre senhas de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="c05ca-121">Here are some things tooknow about app passwords:</span></span>

* <span data-ttu-id="c05ca-122">Você não cria suas próprias senhas de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c05ca-122">You don't create your own app passwords.</span></span> <span data-ttu-id="c05ca-123">Elas são geradas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c05ca-123">They are automatically generated.</span></span>
* <span data-ttu-id="c05ca-124">Atualmente, há um limite de 40 senhas por usuário.</span><span class="sxs-lookup"><span data-stu-id="c05ca-124">Currently there is a limit of 40 passwords per user.</span></span> 
* <span data-ttu-id="c05ca-125">Se você tentar toocreate uma senha de aplicativo depois que você atingiu o limite de saudação, você terá toodelete uma das senhas de aplicativo existentes antes de criar um novo.</span><span class="sxs-lookup"><span data-stu-id="c05ca-125">If you try toocreate an app password after you have reached hello limit, you'll have toodelete one of your existing app passwords before you create a new one.</span></span>
* <span data-ttu-id="c05ca-126">Use uma senha de aplicativo por dispositivo, não por aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c05ca-126">Use one app password per device, not per application.</span></span> <span data-ttu-id="c05ca-127">Por exemplo, você pode criar uma senha de aplicativo para seu laptop e usá-la para todos os aplicativos nesse laptop.</span><span class="sxs-lookup"><span data-stu-id="c05ca-127">For example, you can create one app password for your laptop and use that app password for all of your applications on that laptop.</span></span> <span data-ttu-id="c05ca-128">Em seguida, crie uma segunda toouse de senha de aplicativo para todos os seus aplicativos em sua área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="c05ca-128">Then, create a second app password toouse for all your apps on your desktop.</span></span> 
* <span data-ttu-id="c05ca-129">Você terá uma saudação de senha de aplicativo primeira vez que você se registrar para verificação em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="c05ca-129">You are given one app password hello first time you register for two-step verification.</span></span>  <span data-ttu-id="c05ca-130">Se precisar de mais, é possível criá-las.</span><span class="sxs-lookup"><span data-stu-id="c05ca-130">If you need additional ones, you can create them.</span></span>



## <a name="creating-and-deleting-app-passwords"></a><span data-ttu-id="c05ca-131">Criação e exclusão de senhas de aplicativo</span><span class="sxs-lookup"><span data-stu-id="c05ca-131">Creating and deleting app passwords</span></span>
<span data-ttu-id="c05ca-132">Durante a entrada inicial, você recebe uma senha de aplicativo que pode usar.</span><span class="sxs-lookup"><span data-stu-id="c05ca-132">During your initial sign-in, you are given an app password that you can use.</span></span>  <span data-ttu-id="c05ca-133">Você também pode criar e excluir senhas de aplicativo posteriormente.</span><span class="sxs-lookup"><span data-stu-id="c05ca-133">You can also create and delete app passwords later on.</span></span> <span data-ttu-id="c05ca-134">Como excluir senhas de aplicativo depende de como você usa a autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="c05ca-134">How you delete app passwords depends on how you use multi-factor authentication.</span></span> <span data-ttu-id="c05ca-135">Saudação de resposta a seguir perguntas toodetermine onde você deve ficar toomanage senhas de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="c05ca-135">Answer hello following questions toodetermine where you should go toomanage app passwords:</span></span> 

1. <span data-ttu-id="c05ca-136">Você usa a verificação em duas etapas em sua conta pessoal da Microsoft?</span><span class="sxs-lookup"><span data-stu-id="c05ca-136">Do you use two-step verification for your personal Microsoft account?</span></span> <span data-ttu-id="c05ca-137">Se Sim, consulte toohello [senhas de aplicativo e verificação em duas etapas](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) artigo para obter ajuda.</span><span class="sxs-lookup"><span data-stu-id="c05ca-137">If yes, you should refer toohello [App passwords and two-step verification](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) article for help.</span></span> <span data-ttu-id="c05ca-138">Se não, continue tooquestion dois.</span><span class="sxs-lookup"><span data-stu-id="c05ca-138">If no, continue tooquestion two.</span></span>

2. <span data-ttu-id="c05ca-139">Certo, você usa a verificação de duas etapas em sua conta corporativa ou de estudante.</span><span class="sxs-lookup"><span data-stu-id="c05ca-139">Ok, so you use two-step verification for your work or school account.</span></span> <span data-ttu-id="c05ca-140">Você usa ele toosign em tooOffice 365 aplicativos?</span><span class="sxs-lookup"><span data-stu-id="c05ca-140">Do you use it toosign in tooOffice 365 apps?</span></span> <span data-ttu-id="c05ca-141">Se Sim, você deve referir-se muito[criar uma senha de aplicativo para o Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) para obter ajuda.</span><span class="sxs-lookup"><span data-stu-id="c05ca-141">If yes, you should refer too[Create an app password for Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) for help.</span></span> <span data-ttu-id="c05ca-142">Se não, continue tooquestion três.</span><span class="sxs-lookup"><span data-stu-id="c05ca-142">If no, continue tooquestion three.</span></span> 

3. <span data-ttu-id="c05ca-143">Você usa a verificação em duas etapas com o Microsoft Azure?</span><span class="sxs-lookup"><span data-stu-id="c05ca-143">Do you use two-step verification with Microsoft Azure?</span></span> <span data-ttu-id="c05ca-144">Se Sim, continuar toohello [gerenciar senhas de aplicativo no portal do Azure de saudação](#manage-app-passwords-in-the-Azure-portal) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="c05ca-144">If yes, continue toohello [Manage app passwords in hello Azure portal](#manage-app-passwords-in-the-Azure-portal) section of this article.</span></span> <span data-ttu-id="c05ca-145">Se não, continue tooquestion quatro.</span><span class="sxs-lookup"><span data-stu-id="c05ca-145">If no, continue tooquestion four.</span></span>

4. <span data-ttu-id="c05ca-146">Você não sabe onde utiliza a verificação em duas etapas?</span><span class="sxs-lookup"><span data-stu-id="c05ca-146">Not sure where you use two-step verification?</span></span> <span data-ttu-id="c05ca-147">Continuar toohello [gerenciar senhas de aplicativo com o portal de MyApps Olá](#manage-app-passwords-with-the-myapps-portal) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="c05ca-147">Continue toohello [Manage app passwords with hello MyApps portal](#manage-app-passwords-with-the-myapps-portal) section of this article.</span></span> 


## <a name="manage-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="c05ca-148">Gerenciar senhas de aplicativo no portal do Azure de saudação</span><span class="sxs-lookup"><span data-stu-id="c05ca-148">Manage app passwords in hello Azure portal</span></span>
<span data-ttu-id="c05ca-149">Se você usar a verificação em duas etapas com o Azure, você deseja toocreate senhas de aplicativo por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c05ca-149">If you use two-step verification with Azure, you want toocreate app passwords through hello Azure portal.</span></span>

### <a name="toocreate-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="c05ca-150">senhas de aplicativo toocreate em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c05ca-150">toocreate app passwords in hello Azure portal</span></span>
1. <span data-ttu-id="c05ca-151">Entrar toohello portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="c05ca-151">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="c05ca-152">Na parte superior do hello, clique em seu nome de usuário e selecione verificação de segurança adicional.</span><span class="sxs-lookup"><span data-stu-id="c05ca-152">At hello top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="c05ca-153">Na página de proofup de saudação, na parte superior do hello, selecione as senhas de aplicativo</span><span class="sxs-lookup"><span data-stu-id="c05ca-153">On hello proofup page, at hello top, select app passwords</span></span>
4. <span data-ttu-id="c05ca-154">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c05ca-154">Click **Create**.</span></span>
5. <span data-ttu-id="c05ca-155">Insira um nome para a senha de aplicativo hello e clique em **Avançar**</span><span class="sxs-lookup"><span data-stu-id="c05ca-155">Enter a name for hello app password and click **Next**</span></span>
6. <span data-ttu-id="c05ca-156">Copie Olá aplicativo senha toohello da área de transferência e cole-o em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c05ca-156">Copy hello app password toohello clipboard and paste it into your app.</span></span>
   
   ![Nuvem](./media/multi-factor-authentication-end-user-app-passwords/app2.png)


### <a name="toodelete-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="c05ca-158">senhas de aplicativo toodelete em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c05ca-158">toodelete app passwords in hello Azure portal</span></span>
1. <span data-ttu-id="c05ca-159">Entrar toohello portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="c05ca-159">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="c05ca-160">Na parte superior do hello, clique em seu nome de usuário e selecione verificação de segurança adicional.</span><span class="sxs-lookup"><span data-stu-id="c05ca-160">At hello top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="c05ca-161">Na parte superior do hello, próxima verificação de segurança tooadditional, selecione **senhas de aplicativo.**</span><span class="sxs-lookup"><span data-stu-id="c05ca-161">At hello top, next tooadditional security verification, select **app passwords.**</span></span>
4. <span data-ttu-id="c05ca-162">Senha do aplicativo toohello próxima deseja toodelete, selecione **excluir**.</span><span class="sxs-lookup"><span data-stu-id="c05ca-162">Next toohello app password you want toodelete, select **Delete**.</span></span>
5. <span data-ttu-id="c05ca-163">Confirmar exclusão de saudação clicando **Sim**.</span><span class="sxs-lookup"><span data-stu-id="c05ca-163">Confirm hello deletion by clicking **yes**.</span></span>
6. <span data-ttu-id="c05ca-164">Depois que a senha de aplicativo hello for excluída, você pode clicar em **fechar**.</span><span class="sxs-lookup"><span data-stu-id="c05ca-164">Once hello app password is deleted, you can click **close**.</span></span>


## <a name="manage-app-passwords-with-hello-myapps-portal"></a><span data-ttu-id="c05ca-165">Gerencie senhas de aplicativo com o portal de MyApps hello.</span><span class="sxs-lookup"><span data-stu-id="c05ca-165">Manage app passwords with hello MyApps portal.</span></span>
<span data-ttu-id="c05ca-166">Se você não tiver certeza de como você pode usar a autenticação multifator, em seguida, você pode sempre criar e excluir as senhas de aplicativo por meio do portal myapps hello.</span><span class="sxs-lookup"><span data-stu-id="c05ca-166">If you are not sure how you use multi-factor authentication, then you can always create and delete app passwords through hello myapps portal.</span></span>

### <a name="toocreate-an-app-password-using-hello-myapps-portal"></a><span data-ttu-id="c05ca-167">toocreate uma senha de aplicativo usando Olá Myapps portal</span><span class="sxs-lookup"><span data-stu-id="c05ca-167">toocreate an app password using hello Myapps portal</span></span>
1. <span data-ttu-id="c05ca-168">Entrar muito[https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="c05ca-168">Sign in too[https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="c05ca-169">Clique no nome na parte superior de saudação à direita e escolha **perfil**.</span><span class="sxs-lookup"><span data-stu-id="c05ca-169">Click your name at hello top right, and choose **Profile**.</span></span>
3. <span data-ttu-id="c05ca-170">Escolha **Verificação de Segurança Adicional**.</span><span class="sxs-lookup"><span data-stu-id="c05ca-170">Select **Additional Security Verification**.</span></span>
   <span data-ttu-id="c05ca-171">![Selecione Verificação de Segurança Adicional – captura de tela](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span><span class="sxs-lookup"><span data-stu-id="c05ca-171">![Select additional security verification - screenshot](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span></span>

4. <span data-ttu-id="c05ca-172">Selecione **senhas de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="c05ca-172">Select **app passwords**.</span></span>
   <span data-ttu-id="c05ca-173">![Selecione senhas de aplicativo – captura de tela](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span><span class="sxs-lookup"><span data-stu-id="c05ca-173">![Select app passwords - screenshot](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span></span>

5. <span data-ttu-id="c05ca-174">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c05ca-174">Click **Create**.</span></span>
6. <span data-ttu-id="c05ca-175">Insira um nome para a senha de aplicativo hello e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="c05ca-175">Enter a name for hello app password and click **Next**.</span></span>
7. <span data-ttu-id="c05ca-176">Copie Olá aplicativo senha toohello da área de transferência e cole-o em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c05ca-176">Copy hello app password toohello clipboard and paste it into your app.</span></span>
   <span data-ttu-id="c05ca-177">![Criar uma senha de aplicativo](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span><span class="sxs-lookup"><span data-stu-id="c05ca-177">![Create an app password](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span></span>

### <a name="toodelete-an-app-password-using-hello-myapps-portal"></a><span data-ttu-id="c05ca-178">toodelete uma senha de aplicativo usando Olá Myapps portal</span><span class="sxs-lookup"><span data-stu-id="c05ca-178">toodelete an app password using hello Myapps portal</span></span>
1. <span data-ttu-id="c05ca-179">Entrar muito[https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="c05ca-179">Sign in too[https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="c05ca-180">Na parte superior do hello, selecione o perfil.</span><span class="sxs-lookup"><span data-stu-id="c05ca-180">At hello top, select profile.</span></span>
3. <span data-ttu-id="c05ca-181">Escolha **Verificação de Segurança Adicional**.</span><span class="sxs-lookup"><span data-stu-id="c05ca-181">Select **Additional Security Verification**.</span></span>

   ![Selecione Verificação de Segurança Adicional – captura de tela](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. <span data-ttu-id="c05ca-183">Selecione **senhas de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="c05ca-183">Select **app passwords**.</span></span>

   ![Selecione senhas de aplicativo – captura de tela](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. <span data-ttu-id="c05ca-185">Clique em Avançar senha de aplicativo toohello deseja toodelete, **excluir**.</span><span class="sxs-lookup"><span data-stu-id="c05ca-185">Next toohello app password you want toodelete, click **Delete**.</span></span>

   ![Excluir uma senha de aplicativo](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. <span data-ttu-id="c05ca-187">Confirme que você deseja toodelete essa senha, clicando em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="c05ca-187">Confirm that you want toodelete that password by clicking **yes**.</span></span>
7. <span data-ttu-id="c05ca-188">Depois que a senha de aplicativo hello for excluída, você pode clicar em **fechar**.</span><span class="sxs-lookup"><span data-stu-id="c05ca-188">Once hello app password is deleted, you can click **close**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c05ca-189">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c05ca-189">Next steps</span></span>

- [<span data-ttu-id="c05ca-190">Gerenciar suas configurações de verificação em duas etapas</span><span class="sxs-lookup"><span data-stu-id="c05ca-190">Manage your two-step verification settings</span></span>](multi-factor-authentication-end-user-manage-settings.md)

- <span data-ttu-id="c05ca-191">Experimente Olá [aplicativo Microsoft Authenticator](microsoft-authenticator-app-how-to.md) tooverify suas entradas com as notificações do aplicativo, em vez de recebimento de textos ou chamadas.</span><span class="sxs-lookup"><span data-stu-id="c05ca-191">Try out hello [Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) tooverify your sign-ins with app notifications, instead of receiving texts or calls.</span></span> 
