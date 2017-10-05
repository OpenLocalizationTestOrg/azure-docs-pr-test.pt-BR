---
title: Como usar senhas de aplicativo no Azure MFA? | Microsoft Docs
description: "Esta página ajudará os usuários a entender o que são senhas de aplicativo e para que elas são usadas em relação ao Azure MFA."
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
ms.openlocfilehash: 1ecc2bdef5ff7ef8ed8dded7dc12428ce9657821
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a><span data-ttu-id="3c03c-104">O que são as senhas de aplicativo no Azure Multi-Factor Authentication?</span><span class="sxs-lookup"><span data-stu-id="3c03c-104">What are App Passwords in Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="3c03c-105">Determinados aplicativos que não usam navegador, como o cliente de email nativo da Apple, que usa o Exchange Active Sync, atualmente, não oferecem suporte à autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="3c03c-105">Certain non-browser apps, such as the Apple native email client that uses Exchange Active Sync, currently do not support multi-factor authentication.</span></span> <span data-ttu-id="3c03c-106">O Multi-Factor Authentication é habilitado por usuário.</span><span class="sxs-lookup"><span data-stu-id="3c03c-106">Multi-factor authentication is enabled per user.</span></span>  <span data-ttu-id="3c03c-107">Isso significa que um usuário não poderá usar a autenticação multifator se:</span><span class="sxs-lookup"><span data-stu-id="3c03c-107">This means that a user can't use multi-factor authentication if:</span></span>

- <span data-ttu-id="3c03c-108">O usuário tiver sido habilitado para a autenticação multifator</span><span class="sxs-lookup"><span data-stu-id="3c03c-108">The user has been enabled for multi-factor authentication</span></span>
- <span data-ttu-id="3c03c-109">O usuário está tentando usar um aplicativo que não é navegador.</span><span class="sxs-lookup"><span data-stu-id="3c03c-109">The user is trying to use a non-browser app.</span></span>

<span data-ttu-id="3c03c-110">Uma senha de aplicativo permite que o usuário use o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3c03c-110">An app password allows the user to use the app.</span></span>

<span data-ttu-id="3c03c-111">Quando tiver uma senha de aplicativo, você poderá usá-la no lugar da senha original com esses aplicativos que não usam navegador.</span><span class="sxs-lookup"><span data-stu-id="3c03c-111">Once you have an app password, you use it in place of your original password with these non-browser apps.</span></span> <span data-ttu-id="3c03c-112">Ao aderir à verificação em duas etapas, você está dizendo à Microsoft que, se uma pessoa não puder executar a segunda verificação, ela não poderá se conectar à sua conta com a sua senha.</span><span class="sxs-lookup"><span data-stu-id="3c03c-112">When you register for two-step verification, you're telling Microsoft not to let anyone sign in with your password if they can't also perform the second verification.</span></span> <span data-ttu-id="3c03c-113">O cliente de email nativo da Apple no seu telefone não pode se conectar, pois ele não pode solicitar a verificação em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="3c03c-113">The Apple native email client on your phone can't sign in as you because it can't ask for two-step verification.</span></span> <span data-ttu-id="3c03c-114">A solução para esse problema é criar uma senha de aplicativo mais segura que você não use diariamente.</span><span class="sxs-lookup"><span data-stu-id="3c03c-114">The solution to this problem is to create a more secure app password that you don't use day-to-day.</span></span> <span data-ttu-id="3c03c-115">As senhas de aplicativo são apenas para os aplicativos que não oferecem suporte à verificação em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="3c03c-115">App passwords are only for those apps that can't support two-step verification.</span></span> <span data-ttu-id="3c03c-116">Use a senha do aplicativo para que a autenticação multifator seja ignorada e ele continue funcionando.</span><span class="sxs-lookup"><span data-stu-id="3c03c-116">Use the app password so that apps can bypass multi-factor authentication and continue to work.</span></span>


> [!NOTE]
> <span data-ttu-id="3c03c-117">Os clientes do Office 2013 (incluindo Outlook) são compatíveis com novos protocolos de autenticação e podem ser usados com a verificação em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="3c03c-117">Office 2013 clients (including Outlook) support new authentication protocols and can be used with two-step verification.</span></span> <span data-ttu-id="3c03c-118">As senhas de aplicativo não são necessárias para usar com os clientes do Office 2013.</span><span class="sxs-lookup"><span data-stu-id="3c03c-118">App passwords are not required for use with Office 2013 clients.</span></span>  <span data-ttu-id="3c03c-119">Para saber mais, veja [Anúncio da visualização pública da autenticação moderna do Office 2013](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).</span><span class="sxs-lookup"><span data-stu-id="3c03c-119">For more information, see [Office 2013 modern authentication public preview announced](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).</span></span>


## <a name="how-to-use-app-passwords"></a><span data-ttu-id="3c03c-120">Como usar senhas de aplicativo</span><span class="sxs-lookup"><span data-stu-id="3c03c-120">How to use app passwords</span></span>
<span data-ttu-id="3c03c-121">Coisas importantes a saber sobre senhas de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="3c03c-121">Here are some things to know about app passwords:</span></span>

* <span data-ttu-id="3c03c-122">Você não cria suas próprias senhas de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3c03c-122">You don't create your own app passwords.</span></span> <span data-ttu-id="3c03c-123">Elas são geradas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="3c03c-123">They are automatically generated.</span></span>
* <span data-ttu-id="3c03c-124">Atualmente, há um limite de 40 senhas por usuário.</span><span class="sxs-lookup"><span data-stu-id="3c03c-124">Currently there is a limit of 40 passwords per user.</span></span> 
* <span data-ttu-id="3c03c-125">Se você tentar criar uma senha de aplicativo depois de ter atingido o limite, será necessário excluir uma de suas senhas de aplicativo existentes antes de criar uma nova.</span><span class="sxs-lookup"><span data-stu-id="3c03c-125">If you try to create an app password after you have reached the limit, you'll have to delete one of your existing app passwords before you create a new one.</span></span>
* <span data-ttu-id="3c03c-126">Use uma senha de aplicativo por dispositivo, não por aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3c03c-126">Use one app password per device, not per application.</span></span> <span data-ttu-id="3c03c-127">Por exemplo, você pode criar uma senha de aplicativo para seu laptop e usá-la para todos os aplicativos nesse laptop.</span><span class="sxs-lookup"><span data-stu-id="3c03c-127">For example, you can create one app password for your laptop and use that app password for all of your applications on that laptop.</span></span> <span data-ttu-id="3c03c-128">Em seguida, crie uma segunda senha de aplicativo a ser usada para todos os seus aplicativos na área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="3c03c-128">Then, create a second app password to use for all your apps on your desktop.</span></span> 
* <span data-ttu-id="3c03c-129">Você receberá uma senha de aplicativo na primeira vez que se inscrever na verificação em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="3c03c-129">You are given one app password the first time you register for two-step verification.</span></span>  <span data-ttu-id="3c03c-130">Se precisar de mais, é possível criá-las.</span><span class="sxs-lookup"><span data-stu-id="3c03c-130">If you need additional ones, you can create them.</span></span>



## <a name="creating-and-deleting-app-passwords"></a><span data-ttu-id="3c03c-131">Criação e exclusão de senhas de aplicativo</span><span class="sxs-lookup"><span data-stu-id="3c03c-131">Creating and deleting app passwords</span></span>
<span data-ttu-id="3c03c-132">Durante a entrada inicial, você recebe uma senha de aplicativo que pode usar.</span><span class="sxs-lookup"><span data-stu-id="3c03c-132">During your initial sign-in, you are given an app password that you can use.</span></span>  <span data-ttu-id="3c03c-133">Você também pode criar e excluir senhas de aplicativo posteriormente.</span><span class="sxs-lookup"><span data-stu-id="3c03c-133">You can also create and delete app passwords later on.</span></span> <span data-ttu-id="3c03c-134">Como excluir senhas de aplicativo depende de como você usa a autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="3c03c-134">How you delete app passwords depends on how you use multi-factor authentication.</span></span> <span data-ttu-id="3c03c-135">Responda as perguntas a seguir para saber mais sobre como gerenciar as suas senhas de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="3c03c-135">Answer the following questions to determine where you should go to manage app passwords:</span></span> 

1. <span data-ttu-id="3c03c-136">Você usa a verificação em duas etapas em sua conta pessoal da Microsoft?</span><span class="sxs-lookup"><span data-stu-id="3c03c-136">Do you use two-step verification for your personal Microsoft account?</span></span> <span data-ttu-id="3c03c-137">Se sim, consulte o artigo [Senhas de aplicativo e verificação em duas etapas](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) para obter ajuda.</span><span class="sxs-lookup"><span data-stu-id="3c03c-137">If yes, you should refer to the [App passwords and two-step verification](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) article for help.</span></span> <span data-ttu-id="3c03c-138">Se não, prossiga para a pergunta dois.</span><span class="sxs-lookup"><span data-stu-id="3c03c-138">If no, continue to question two.</span></span>

2. <span data-ttu-id="3c03c-139">Certo, você usa a verificação de duas etapas em sua conta corporativa ou de estudante.</span><span class="sxs-lookup"><span data-stu-id="3c03c-139">Ok, so you use two-step verification for your work or school account.</span></span> <span data-ttu-id="3c03c-140">Você a utiliza para entrar em aplicativos do Office 365?</span><span class="sxs-lookup"><span data-stu-id="3c03c-140">Do you use it to sign in to Office 365 apps?</span></span> <span data-ttu-id="3c03c-141">Se Sim, consulte o artigo [Criar uma senha de aplicativo para o Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) para obter ajuda.</span><span class="sxs-lookup"><span data-stu-id="3c03c-141">If yes, you should refer to [Create an app password for Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) for help.</span></span> <span data-ttu-id="3c03c-142">Se não, prossiga para a pergunta três.</span><span class="sxs-lookup"><span data-stu-id="3c03c-142">If no, continue to question three.</span></span> 

3. <span data-ttu-id="3c03c-143">Você usa a verificação em duas etapas com o Microsoft Azure?</span><span class="sxs-lookup"><span data-stu-id="3c03c-143">Do you use two-step verification with Microsoft Azure?</span></span> <span data-ttu-id="3c03c-144">Se sim, vá para a seção [Gerenciar senhas de aplicativo no portal do Azure](#manage-app-passwords-in-the-Azure-portal) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="3c03c-144">If yes, continue to the [Manage app passwords in the Azure portal](#manage-app-passwords-in-the-Azure-portal) section of this article.</span></span> <span data-ttu-id="3c03c-145">Se não, prossiga para a pergunta quatro.</span><span class="sxs-lookup"><span data-stu-id="3c03c-145">If no, continue to question four.</span></span>

4. <span data-ttu-id="3c03c-146">Você não sabe onde utiliza a verificação em duas etapas?</span><span class="sxs-lookup"><span data-stu-id="3c03c-146">Not sure where you use two-step verification?</span></span> <span data-ttu-id="3c03c-147">Vá para a seção [Gerenciar senhas de aplicativo no portal do MyApps](#manage-app-passwords-with-the-myapps-portal) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="3c03c-147">Continue to the [Manage app passwords with the MyApps portal](#manage-app-passwords-with-the-myapps-portal) section of this article.</span></span> 


## <a name="manage-app-passwords-in-the-azure-portal"></a><span data-ttu-id="3c03c-148">Gerenciar senhas de aplicativo no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3c03c-148">Manage app passwords in the Azure portal</span></span>
<span data-ttu-id="3c03c-149">Se você usa a autenticação em duas etapas com o Azure, talvez seja conveniente criar senhas de aplicativo por meio do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c03c-149">If you use two-step verification with Azure, you want to create app passwords through the Azure portal.</span></span>

### <a name="to-create-app-passwords-in-the-azure-portal"></a><span data-ttu-id="3c03c-150">Para criar senhas de aplicativo no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3c03c-150">To create app passwords in the Azure portal</span></span>
1. <span data-ttu-id="3c03c-151">Entre no portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c03c-151">Sign in to the Azure classic portal.</span></span>
2. <span data-ttu-id="3c03c-152">Na parte superior, clique com o botão direito do mouse no seu nome de usuário e selecione Verificação de Segurança Adicional.</span><span class="sxs-lookup"><span data-stu-id="3c03c-152">At the top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="3c03c-153">Na parte superior da página de prova, selecione as senhas de aplicativo</span><span class="sxs-lookup"><span data-stu-id="3c03c-153">On the proofup page, at the top, select app passwords</span></span>
4. <span data-ttu-id="3c03c-154">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3c03c-154">Click **Create**.</span></span>
5. <span data-ttu-id="3c03c-155">Insira um nome para a senha de aplicativo e clique em **Avançar**</span><span class="sxs-lookup"><span data-stu-id="3c03c-155">Enter a name for the app password and click **Next**</span></span>
6. <span data-ttu-id="3c03c-156">Copie a senha de aplicativo na área de transferência e cole-a no seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3c03c-156">Copy the app password to the clipboard and paste it into your app.</span></span>
   
   ![Nuvem](./media/multi-factor-authentication-end-user-app-passwords/app2.png)


### <a name="to-delete-app-passwords-in-the-azure-portal"></a><span data-ttu-id="3c03c-158">Para excluir senhas de aplicativo no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3c03c-158">To delete app passwords in the Azure portal</span></span>
1. <span data-ttu-id="3c03c-159">Entre no portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c03c-159">Sign in to the Azure classic portal.</span></span>
2. <span data-ttu-id="3c03c-160">Na parte superior, clique com o botão direito do mouse no seu nome de usuário e selecione Verificação de Segurança Adicional.</span><span class="sxs-lookup"><span data-stu-id="3c03c-160">At the top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="3c03c-161">Na parte superior, ao lado de verificação de segurança adicional, clique em **senhas de aplicativo.**</span><span class="sxs-lookup"><span data-stu-id="3c03c-161">At the top, next to additional security verification, select **app passwords.**</span></span>
4. <span data-ttu-id="3c03c-162">Ao lado da senha de aplicativo que deseja excluir, selecione **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="3c03c-162">Next to the app password you want to delete, select **Delete**.</span></span>
5. <span data-ttu-id="3c03c-163">Confirme a exclusão clicando em **sim**.</span><span class="sxs-lookup"><span data-stu-id="3c03c-163">Confirm the deletion by clicking **yes**.</span></span>
6. <span data-ttu-id="3c03c-164">Quando a senha do aplicativo for excluída, clique em **Fechar**.</span><span class="sxs-lookup"><span data-stu-id="3c03c-164">Once the app password is deleted, you can click **close**.</span></span>


## <a name="manage-app-passwords-with-the-myapps-portal"></a><span data-ttu-id="3c03c-165">Gerenciar senhas de aplicativo no portal do MyApps.</span><span class="sxs-lookup"><span data-stu-id="3c03c-165">Manage app passwords with the MyApps portal.</span></span>
<span data-ttu-id="3c03c-166">Se não tiver certeza de como você usa a autenticação multifator, será possível criar e excluir senhas de aplicativo por meio do portal do Myapps.</span><span class="sxs-lookup"><span data-stu-id="3c03c-166">If you are not sure how you use multi-factor authentication, then you can always create and delete app passwords through the myapps portal.</span></span>

### <a name="to-create-an-app-password-using-the-myapps-portal"></a><span data-ttu-id="3c03c-167">Para criar uma senha de aplicativo usando o portal do Myapps</span><span class="sxs-lookup"><span data-stu-id="3c03c-167">To create an app password using the Myapps portal</span></span>
1. <span data-ttu-id="3c03c-168">Entre em [https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="3c03c-168">Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="3c03c-169">Clique no seu nome na parte superior direita e selecione **Perfil**.</span><span class="sxs-lookup"><span data-stu-id="3c03c-169">Click your name at the top right, and choose **Profile**.</span></span>
3. <span data-ttu-id="3c03c-170">Escolha **Verificação de Segurança Adicional**.</span><span class="sxs-lookup"><span data-stu-id="3c03c-170">Select **Additional Security Verification**.</span></span>
   <span data-ttu-id="3c03c-171">![Selecione Verificação de Segurança Adicional – captura de tela](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span><span class="sxs-lookup"><span data-stu-id="3c03c-171">![Select additional security verification - screenshot](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span></span>

4. <span data-ttu-id="3c03c-172">Selecione **senhas de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="3c03c-172">Select **app passwords**.</span></span>
   <span data-ttu-id="3c03c-173">![Selecione senhas de aplicativo – captura de tela](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span><span class="sxs-lookup"><span data-stu-id="3c03c-173">![Select app passwords - screenshot](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span></span>

5. <span data-ttu-id="3c03c-174">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3c03c-174">Click **Create**.</span></span>
6. <span data-ttu-id="3c03c-175">Insira um nome para a senha de aplicativo e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="3c03c-175">Enter a name for the app password and click **Next**.</span></span>
7. <span data-ttu-id="3c03c-176">Copie a senha de aplicativo na área de transferência e cole-a no seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3c03c-176">Copy the app password to the clipboard and paste it into your app.</span></span>
   <span data-ttu-id="3c03c-177">![Criar uma senha de aplicativo](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span><span class="sxs-lookup"><span data-stu-id="3c03c-177">![Create an app password](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span></span>

### <a name="to-delete-an-app-password-using-the-myapps-portal"></a><span data-ttu-id="3c03c-178">Para excluir uma senha de aplicativo usando o portal do Myapps</span><span class="sxs-lookup"><span data-stu-id="3c03c-178">To delete an app password using the Myapps portal</span></span>
1. <span data-ttu-id="3c03c-179">Entre em [https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="3c03c-179">Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="3c03c-180">Na parte superior, selecione Perfil.</span><span class="sxs-lookup"><span data-stu-id="3c03c-180">At the top, select profile.</span></span>
3. <span data-ttu-id="3c03c-181">Escolha **Verificação de Segurança Adicional**.</span><span class="sxs-lookup"><span data-stu-id="3c03c-181">Select **Additional Security Verification**.</span></span>

   ![Selecione Verificação de Segurança Adicional – captura de tela](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. <span data-ttu-id="3c03c-183">Selecione **senhas de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="3c03c-183">Select **app passwords**.</span></span>

   ![Selecione senhas de aplicativo – captura de tela](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. <span data-ttu-id="3c03c-185">Do lado da senha do aplicativo que deseja remover, selecione **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="3c03c-185">Next to the app password you want to delete, click **Delete**.</span></span>

   ![Excluir uma senha de aplicativo](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. <span data-ttu-id="3c03c-187">Confirme que deseja excluir essa senha clicando em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="3c03c-187">Confirm that you want to delete that password by clicking **yes**.</span></span>
7. <span data-ttu-id="3c03c-188">Quando a senha do aplicativo for excluída, clique em **Fechar**.</span><span class="sxs-lookup"><span data-stu-id="3c03c-188">Once the app password is deleted, you can click **close**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c03c-189">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3c03c-189">Next steps</span></span>

- [<span data-ttu-id="3c03c-190">Gerenciar suas configurações de verificação em duas etapas</span><span class="sxs-lookup"><span data-stu-id="3c03c-190">Manage your two-step verification settings</span></span>](multi-factor-authentication-end-user-manage-settings.md)

- <span data-ttu-id="3c03c-191">Experimente o [aplicativo Autenticador Microsoft](microsoft-authenticator-app-how-to.md) para verificar suas conexões com notificações de aplicativo, em vez de receber mensagens ou ligações.</span><span class="sxs-lookup"><span data-stu-id="3c03c-191">Try out the [Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) to verify your sign-ins with app notifications, instead of receiving texts or calls.</span></span> 
