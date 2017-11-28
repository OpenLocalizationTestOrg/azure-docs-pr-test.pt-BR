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
ms.openlocfilehash: 8e073df9de2996f5ad159dda746881c014ea3d66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a><span data-ttu-id="de8fa-103">Habilitar a sincronização de senha tooAzure serviços de domínio do Active Directory</span><span class="sxs-lookup"><span data-stu-id="de8fa-103">Enable password synchronization tooAzure Active Directory Domain Services</span></span>
<span data-ttu-id="de8fa-104">Nas tarefas anteriores, você habilitou o Azure Active Directory Domain Services para seu locatário do Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="de8fa-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="de8fa-105">Olá próxima tarefa é tooenable sincronização de hashes de credenciais necessárias para tooAzure de autenticação NT LAN Manager (NTLM) e Kerberos dos serviços de domínio do AD.</span><span class="sxs-lookup"><span data-stu-id="de8fa-105">hello next task is tooenable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication tooAzure AD Domain Services.</span></span> <span data-ttu-id="de8fa-106">Depois de configurar a sincronização de credenciais, os usuários possam entrar toohello o domínio gerenciado com suas credenciais corporativas.</span><span class="sxs-lookup"><span data-stu-id="de8fa-106">After you've set up credential synchronization, users can sign in toohello managed domain with their corporate credentials.</span></span>

<span data-ttu-id="de8fa-107">etapas de Olá envolvidas são diferentes para o usuário somente em nuvem contas vs contas de usuário que são sincronizadas do seu diretório local usando o Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="de8fa-107">hello steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span>  <span data-ttu-id="de8fa-108">Se o seu locatário do AD do Azure tem uma combinação de nuvem apenas os usuários e usuários de seu local AD, você precisa tooperform as duas etapas.</span><span class="sxs-lookup"><span data-stu-id="de8fa-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need tooperform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="de8fa-109">**Contas de usuário somente em nuvem**: [sincronizar senhas para contas de usuário somente em nuvem domínio gerenciado tooyour](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="de8fa-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts tooyour managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="de8fa-110">**Contas de usuário local**: [sincronizar senhas para contas de usuário sincronizadas a partir de suas instalações AD tooyour gerenciados domínio](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="de8fa-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD tooyour managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-cloud-only-user-accounts"></a><span data-ttu-id="de8fa-111">Tarefa 5: habilitar tooyour de sincronização de senha gerenciado domínio para as contas de usuário somente em nuvem</span><span class="sxs-lookup"><span data-stu-id="de8fa-111">Task 5: enable password synchronization tooyour managed domain for cloud-only user accounts</span></span>
<span data-ttu-id="de8fa-112">usuários tooauthenticate Olá gerenciados domínio, o Azure Active Directory Domain Services precisa de credenciais hashes em um formato adequado para a autenticação NTLM e Kerberos.</span><span class="sxs-lookup"><span data-stu-id="de8fa-112">tooauthenticate users on hello managed domain, Azure Active Directory Domain Services needs credential hashes in a format that's suitable for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="de8fa-113">O AD do Azure não gerar ou armazenar hashes de credenciais no formato de saudação necessária para a autenticação NTLM ou Kerberos, até você ativar o Azure Active Directory Domain Services para seu locatário.</span><span class="sxs-lookup"><span data-stu-id="de8fa-113">Azure AD does not generate or store credential hashes in hello format that's required for NTLM or Kerberos authentication, until you enable Azure Active Directory Domain Services for your tenant.</span></span> <span data-ttu-id="de8fa-114">Por motivos de segurança óbvios, o Azure AD também não armazena credenciais de senha no formato de texto não criptografado.</span><span class="sxs-lookup"><span data-stu-id="de8fa-114">For obvious security reasons, Azure AD also does not store any password credentials in clear-text form.</span></span> <span data-ttu-id="de8fa-115">Portanto, AD do Azure não tem uma maneira tooautomatically gerar esses hashes de credencial NTLM ou Kerberos com base nas credenciais de usuários existentes.</span><span class="sxs-lookup"><span data-stu-id="de8fa-115">Therefore, Azure AD does not have a way tooautomatically generate these NTLM or Kerberos credential hashes based on users' existing credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="de8fa-116">Se sua organização tiver contas de usuário somente em nuvem, os usuários que precisam de toouse do Azure Active Directory Domain Services devem alterar suas senhas.</span><span class="sxs-lookup"><span data-stu-id="de8fa-116">If your organization has cloud-only user accounts, users who need toouse Azure Active Directory Domain Services must change their passwords.</span></span> <span data-ttu-id="de8fa-117">Uma conta de usuário somente em nuvem é uma conta que foi criada no diretório do AD do Azure usando cmdlets do PowerShell do Azure AD ou Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="de8fa-117">A cloud-only user account is an account that was created in your Azure AD directory using either hello Azure portal or Azure AD PowerShell cmdlets.</span></span> <span data-ttu-id="de8fa-118">Essas contas de usuário não são sincronizadas de um diretório local.</span><span class="sxs-lookup"><span data-stu-id="de8fa-118">Such user accounts aren't synchronized from an on-premises directory.</span></span>
>
>

<span data-ttu-id="de8fa-119">Esse processo de alteração de senha faz com que credencial Olá hashes que são exigidos pelo Azure Active Directory Domain Services para toobe de autenticação Kerberos e NTLM gerada no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de8fa-119">This password change process causes hello credential hashes that are required by Azure Active Directory Domain Services for Kerberos and NTLM authentication toobe generated in Azure AD.</span></span> <span data-ttu-id="de8fa-120">Você ou pode expirar senhas Olá para todos os usuários em Olá locatário que precisam de toouse do Azure Active Directory Domain Services ou instruem o toochange suas senhas.</span><span class="sxs-lookup"><span data-stu-id="de8fa-120">You can either expire hello passwords for all users in hello tenant who need toouse Azure Active Directory Domain Services or instruct them toochange their passwords.</span></span>

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-user-account"></a><span data-ttu-id="de8fa-121">Habilitar a geração de hashes de credencial Kerberos e NTLM para uma conta de usuário somente na nuvem</span><span class="sxs-lookup"><span data-stu-id="de8fa-121">Enable NTLM and Kerberos credential hash generation for a cloud-only user account</span></span>
<span data-ttu-id="de8fa-122">Aqui estão as instruções de saudação que tooprovide usuários, é necessário para que eles podem alterar suas senhas:</span><span class="sxs-lookup"><span data-stu-id="de8fa-122">Here are hello instructions you need tooprovide users, so they can change their passwords:</span></span>

1. <span data-ttu-id="de8fa-123">Vá toohello [painel de acesso do AD do Azure](http://myapps.microsoft.com) página de sua organização.</span><span class="sxs-lookup"><span data-stu-id="de8fa-123">Go toohello [Azure AD Access Panel](http://myapps.microsoft.com) page for your organization.</span></span>

    ![Iniciar o painel de acesso do AD do Azure Olá](./media/active-directory-domain-services-getting-started/access-panel.png)

2. <span data-ttu-id="de8fa-125">No hello canto superior direito, clique em seu nome e selecione **perfil** menu hello.</span><span class="sxs-lookup"><span data-stu-id="de8fa-125">In hello top right corner, click on your name and select **Profile** from hello menu.</span></span>

    ![Selecionar perfil](./media/active-directory-domain-services-getting-started/select-profile.png)

3. <span data-ttu-id="de8fa-127">Em Olá **perfil** página, clique em **alterar senha**.</span><span class="sxs-lookup"><span data-stu-id="de8fa-127">On hello **Profile** page, click on **Change password**.</span></span>

    ![Clique em "Alterar senha"](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > <span data-ttu-id="de8fa-129">Se hello **alterar senha** opção não é exibida na janela de saudação do painel de acesso, certifique-se de que sua organização tenha configurado [gerenciamento de senhas no AD do Azure](../active-directory/active-directory-passwords-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="de8fa-129">If hello **Change password** option is not displayed in hello Access Panel window, ensure that your organization has configured [password management in Azure AD](../active-directory/active-directory-passwords-getting-started.md).</span></span>
   >
   >
4. <span data-ttu-id="de8fa-130">Em Olá **alterar senha** página, digite sua senha (antiga) existente, digite uma nova senha e, em seguida, confirmá-la.</span><span class="sxs-lookup"><span data-stu-id="de8fa-130">On hello **change password** page, type your existing (old) password, type a new password, and then confirm it.</span></span>

    ![Criar uma rede virtual para os Serviços de Domínio do AD do Azure.](./media/active-directory-domain-services-getting-started/user-change-password2.png)

5. <span data-ttu-id="de8fa-132">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="de8fa-132">Click **submit**.</span></span>

<span data-ttu-id="de8fa-133">Alguns minutos depois que você alterou sua senha, a saudação nova senha é utilizável no Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="de8fa-133">A few minutes after you have changed your password, hello new password is usable in Azure Active Directory Domain Services.</span></span> <span data-ttu-id="de8fa-134">Depois de alguns minutos (normalmente, cerca de 20 minutos), você pode entrar no toocomputers que domínio gerenciado toohello unidas usando senha Olá alterado recentemente.</span><span class="sxs-lookup"><span data-stu-id="de8fa-134">After a few more minutes (typically, about 20 minutes), you can sign in toocomputers that are joined toohello managed domain by using hello newly changed password.</span></span>

## <a name="related-content"></a><span data-ttu-id="de8fa-135">Conteúdo relacionado</span><span class="sxs-lookup"><span data-stu-id="de8fa-135">Related Content</span></span>
* [<span data-ttu-id="de8fa-136">Como tooupdate sua própria senha</span><span class="sxs-lookup"><span data-stu-id="de8fa-136">How tooupdate your own password</span></span>](../active-directory/active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="de8fa-137">Introdução ao Gerenciamento de Senhas no Azure AD</span><span class="sxs-lookup"><span data-stu-id="de8fa-137">Getting started with Password Management in Azure AD</span></span>](../active-directory/active-directory-passwords-getting-started.md)
* [<span data-ttu-id="de8fa-138">Habilitar a sincronização de senha do locatário aos serviços de domínio Active Directory de tooAzure um sincronizado do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="de8fa-138">Enable password synchronization tooAzure Active Directory Domain Services for a synced Azure AD tenant</span></span>](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [<span data-ttu-id="de8fa-139">Administrar um domínio gerenciado do Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="de8fa-139">Administer an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="de8fa-140">Ingressar em um domínio Windows máquina virtual tooan gerenciado do Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="de8fa-140">Join a Windows virtual machine tooan Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="de8fa-141">Ingressar em um domínio de gerenciado do Azure Active Directory Domain Services de tooan de máquina virtual do Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="de8fa-141">Join a Red Hat Enterprise Linux virtual machine tooan Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
