---
title: "Azure Active Directory Domain Services: habilitar a sincronização de senha | Microsoft Docs"
description: "Introdução aos Serviços de Domínio do Active Directory do Azure"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 5a32a0df-a3ca-4ebe-b980-91f58f8030fc
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 4b6da997f44860dccb2aa2571ce099ab2d0231f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-password-synchronization-to-azure-active-directory-domain-services"></a><span data-ttu-id="705f0-103">Habilitar a sincronização de senhas para o Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="705f0-103">Enable password synchronization to Azure Active Directory Domain Services</span></span>
<span data-ttu-id="705f0-104">Nas tarefas anteriores, você habilitou o Azure Active Directory Domain Services para seu locatário do Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="705f0-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="705f0-105">A próxima tarefa é habilitar a sincronização de hashes de credencial necessários para a autenticação Kerberos e NTLM para o Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="705f0-105">The next task is to enable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication to Azure AD Domain Services.</span></span> <span data-ttu-id="705f0-106">Depois que a sincronização de credenciais é configurada, os usuários podem entrar no domínio gerenciado com suas credenciais corporativas.</span><span class="sxs-lookup"><span data-stu-id="705f0-106">After you've set up credential synchronization, users can sign in to the managed domain with their corporate credentials.</span></span>

<span data-ttu-id="705f0-107">As etapas envolvidas são diferentes para as contas de usuário somente em nuvem versus contas de usuário sincronizadas do seu diretório local usando o Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="705f0-107">The steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span>  <span data-ttu-id="705f0-108">Se o seu locatário do AD do Azure tiver uma combinação de usuários somente em nuvem e os usuários do seu AD local, será necessário executar as duas etapas.</span><span class="sxs-lookup"><span data-stu-id="705f0-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need to perform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="705f0-109">**Contas de usuário somente em nuvem**: [sincronize senhas para contas de usuário somente em nuvem para seu domínio gerenciado](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="705f0-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts to your managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="705f0-110">**Contas de usuário local**: [sincronize senhas para as contas de usuário sincronizadas de seu AD local para seu domínio gerenciado](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="705f0-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD to your managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-to-your-managed-domain-for-cloud-only-user-accounts"></a><span data-ttu-id="705f0-111">Tarefa 5: habilitar a sincronização de senha para o domínio gerenciado para contas de usuário somente na nuvem</span><span class="sxs-lookup"><span data-stu-id="705f0-111">Task 5: enable password synchronization to your managed domain for cloud-only user accounts</span></span>
<span data-ttu-id="705f0-112">Para autenticar os usuários no domínio gerenciado, o Azure Active Directory Domain Services precisa de hashes de credenciais em um formato adequado para a autenticação NTLM e Kerberos.</span><span class="sxs-lookup"><span data-stu-id="705f0-112">To authenticate users on the managed domain, Azure Active Directory Domain Services needs credential hashes in a format that's suitable for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="705f0-113">O Azure AD não gera nem armazena hashes de credenciais no formato necessário para a autenticação NTLM ou Kerberos, até que você habilite o Azure Active Directory Domain Services para seu locatário.</span><span class="sxs-lookup"><span data-stu-id="705f0-113">Azure AD does not generate or store credential hashes in the format that's required for NTLM or Kerberos authentication, until you enable Azure Active Directory Domain Services for your tenant.</span></span> <span data-ttu-id="705f0-114">Por motivos de segurança óbvios, o Azure AD também não armazena credenciais de senha no formato de texto não criptografado.</span><span class="sxs-lookup"><span data-stu-id="705f0-114">For obvious security reasons, Azure AD also does not store any password credentials in clear-text form.</span></span> <span data-ttu-id="705f0-115">Portanto, o Azure AD não tem uma maneira de gerar automaticamente esses hashes de credenciais NTLM ou Kerberos com base em credenciais de usuários existentes.</span><span class="sxs-lookup"><span data-stu-id="705f0-115">Therefore, Azure AD does not have a way to automatically generate these NTLM or Kerberos credential hashes based on users' existing credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="705f0-116">Se a sua organização tiver contas de usuário somente na nuvem, os usuários que precisam usar o Azure Active Directory Domain Services deverão alterar suas senhas.</span><span class="sxs-lookup"><span data-stu-id="705f0-116">If your organization has cloud-only user accounts, users who need to use Azure Active Directory Domain Services must change their passwords.</span></span> <span data-ttu-id="705f0-117">Uma conta de usuário somente na nuvem é uma conta que foi criada no diretório do Azure AD usando o portal do Azure ou os cmdlets do Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="705f0-117">A cloud-only user account is an account that was created in your Azure AD directory using either the Azure portal or Azure AD PowerShell cmdlets.</span></span> <span data-ttu-id="705f0-118">Essas contas de usuário não são sincronizadas de um diretório local.</span><span class="sxs-lookup"><span data-stu-id="705f0-118">Such user accounts aren't synchronized from an on-premises directory.</span></span>
>
>

<span data-ttu-id="705f0-119">Esse processo de alteração de senhas faz com que os hashes de credencial requeridos pelo Azure Active Directory Domain Services para a autenticação Kerberos e NTLM sejam gerados no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="705f0-119">This password change process causes the credential hashes that are required by Azure Active Directory Domain Services for Kerberos and NTLM authentication to be generated in Azure AD.</span></span> <span data-ttu-id="705f0-120">Você também pode expirar senhas para todos os usuários no locatário que precisam usar o Azure Active Directory Domain Services ou instrui-los para alterar suas senhas.</span><span class="sxs-lookup"><span data-stu-id="705f0-120">You can either expire the passwords for all users in the tenant who need to use Azure Active Directory Domain Services or instruct them to change their passwords.</span></span>

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-user-account"></a><span data-ttu-id="705f0-121">Habilitar a geração de hashes de credencial Kerberos e NTLM para uma conta de usuário somente na nuvem</span><span class="sxs-lookup"><span data-stu-id="705f0-121">Enable NTLM and Kerberos credential hash generation for a cloud-only user account</span></span>
<span data-ttu-id="705f0-122">Aqui estão as instruções que você precisa fornecer aos usuários para que eles possam alterar suas senhas:</span><span class="sxs-lookup"><span data-stu-id="705f0-122">Here are the instructions you need to provide users, so they can change their passwords:</span></span>

1. <span data-ttu-id="705f0-123">Vá para a página do [Painel de acesso do Azure AD](http://myapps.microsoft.com) da sua organização.</span><span class="sxs-lookup"><span data-stu-id="705f0-123">Go to the [Azure AD Access Panel](http://myapps.microsoft.com) page for your organization.</span></span>

    ![Iniciar o painel de acesso do Azure AD](./media/active-directory-domain-services-getting-started/access-panel.png)

2. <span data-ttu-id="705f0-125">No canto superior direito, clique em seu nome e selecione **Perfil** no menu.</span><span class="sxs-lookup"><span data-stu-id="705f0-125">In the top right corner, click on your name and select **Profile** from the menu.</span></span>

    ![Selecionar perfil](./media/active-directory-domain-services-getting-started/select-profile.png)

3. <span data-ttu-id="705f0-127">Na página **Perfil**, clique em **Alterar senha**.</span><span class="sxs-lookup"><span data-stu-id="705f0-127">On the **Profile** page, click on **Change password**.</span></span>

    ![Clique em "Alterar senha"](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > <span data-ttu-id="705f0-129">Se a opção **Alterar senha** não for exibida na janela Painel de Acesso, verifique se sua organização configurou [gerenciamento de senhas no Azure AD](../active-directory/active-directory-passwords-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="705f0-129">If the **Change password** option is not displayed in the Access Panel window, ensure that your organization has configured [password management in Azure AD](../active-directory/active-directory-passwords-getting-started.md).</span></span>
   >
   >
4. <span data-ttu-id="705f0-130">Na página **Alterar senha** , digite sua senha (antiga) existente, digite uma nova senha e confirme-a.</span><span class="sxs-lookup"><span data-stu-id="705f0-130">On the **change password** page, type your existing (old) password, type a new password, and then confirm it.</span></span>

    ![Criar uma rede virtual para os Serviços de Domínio do AD do Azure.](./media/active-directory-domain-services-getting-started/user-change-password2.png)

5. <span data-ttu-id="705f0-132">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="705f0-132">Click **submit**.</span></span>

<span data-ttu-id="705f0-133">A nova senha poderá ser utilizada no Azure Active Directory Domain Services alguns minutos após a sua alteração.</span><span class="sxs-lookup"><span data-stu-id="705f0-133">A few minutes after you have changed your password, the new password is usable in Azure Active Directory Domain Services.</span></span> <span data-ttu-id="705f0-134">Depois de mais alguns minutos (normalmente, cerca de 20 minutos), você pode entrar computadores que ingressaram no domínio gerenciado usando a senha recém-alterada.</span><span class="sxs-lookup"><span data-stu-id="705f0-134">After a few more minutes (typically, about 20 minutes), you can sign in to computers that are joined to the managed domain by using the newly changed password.</span></span>

## <a name="related-content"></a><span data-ttu-id="705f0-135">Conteúdo relacionado</span><span class="sxs-lookup"><span data-stu-id="705f0-135">Related Content</span></span>
* [<span data-ttu-id="705f0-136">Como atualizar sua própria senha</span><span class="sxs-lookup"><span data-stu-id="705f0-136">How to update your own password</span></span>](../active-directory/active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="705f0-137">Introdução ao Gerenciamento de Senhas no Azure AD</span><span class="sxs-lookup"><span data-stu-id="705f0-137">Getting started with Password Management in Azure AD</span></span>](../active-directory/active-directory-passwords-getting-started.md)
* [<span data-ttu-id="705f0-138">Habilitar a sincronização de senhas para o Azure Active Directory Domain Services em um locatário do Azure AD sincronizado</span><span class="sxs-lookup"><span data-stu-id="705f0-138">Enable password synchronization to Azure Active Directory Domain Services for a synced Azure AD tenant</span></span>](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [<span data-ttu-id="705f0-139">Administrar um domínio gerenciado do Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="705f0-139">Administer an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="705f0-140">Ingressar em uma máquina virtual do Windows para um domínio gerenciado do Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="705f0-140">Join a Windows virtual machine to an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="705f0-141">Ingressar em uma máquina virtual do Red Hat Enterprise Linux para um domínio gerenciado do Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="705f0-141">Join a Red Hat Enterprise Linux virtual machine to an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
