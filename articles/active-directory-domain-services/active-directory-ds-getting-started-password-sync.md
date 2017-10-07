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
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a>Habilitar a sincronização de senha tooAzure serviços de domínio do Active Directory
Nas tarefas anteriores, você habilitou o Azure Active Directory Domain Services para seu locatário do Azure AD (Azure Active Directory). Olá próxima tarefa é tooenable sincronização de hashes de credenciais necessárias para tooAzure de autenticação NT LAN Manager (NTLM) e Kerberos dos serviços de domínio do AD. Depois de configurar a sincronização de credenciais, os usuários possam entrar toohello o domínio gerenciado com suas credenciais corporativas.

etapas de Olá envolvidas são diferentes para o usuário somente em nuvem contas vs contas de usuário que são sincronizadas do seu diretório local usando o Azure AD Connect.  Se o seu locatário do AD do Azure tem uma combinação de nuvem apenas os usuários e usuários de seu local AD, você precisa tooperform as duas etapas.

<br>

> [!div class="op_single_selector"]
> * **Contas de usuário somente em nuvem**: [sincronizar senhas para contas de usuário somente em nuvem domínio gerenciado tooyour](active-directory-ds-getting-started-password-sync.md)
> * **Contas de usuário local**: [sincronizar senhas para contas de usuário sincronizadas a partir de suas instalações AD tooyour gerenciados domínio](active-directory-ds-getting-started-password-sync-synced-tenant.md)
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-cloud-only-user-accounts"></a>Tarefa 5: habilitar tooyour de sincronização de senha gerenciado domínio para as contas de usuário somente em nuvem
usuários tooauthenticate Olá gerenciados domínio, o Azure Active Directory Domain Services precisa de credenciais hashes em um formato adequado para a autenticação NTLM e Kerberos. O AD do Azure não gerar ou armazenar hashes de credenciais no formato de saudação necessária para a autenticação NTLM ou Kerberos, até você ativar o Azure Active Directory Domain Services para seu locatário. Por motivos de segurança óbvios, o Azure AD também não armazena credenciais de senha no formato de texto não criptografado. Portanto, AD do Azure não tem uma maneira tooautomatically gerar esses hashes de credencial NTLM ou Kerberos com base nas credenciais de usuários existentes.

> [!NOTE]
> Se sua organização tiver contas de usuário somente em nuvem, os usuários que precisam de toouse do Azure Active Directory Domain Services devem alterar suas senhas. Uma conta de usuário somente em nuvem é uma conta que foi criada no diretório do AD do Azure usando cmdlets do PowerShell do Azure AD ou Olá portal do Azure. Essas contas de usuário não são sincronizadas de um diretório local.
>
>

Esse processo de alteração de senha faz com que credencial Olá hashes que são exigidos pelo Azure Active Directory Domain Services para toobe de autenticação Kerberos e NTLM gerada no Azure AD. Você ou pode expirar senhas Olá para todos os usuários em Olá locatário que precisam de toouse do Azure Active Directory Domain Services ou instruem o toochange suas senhas.

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-user-account"></a>Habilitar a geração de hashes de credencial Kerberos e NTLM para uma conta de usuário somente na nuvem
Aqui estão as instruções de saudação que tooprovide usuários, é necessário para que eles podem alterar suas senhas:

1. Vá toohello [painel de acesso do AD do Azure](http://myapps.microsoft.com) página de sua organização.

    ![Iniciar o painel de acesso do AD do Azure Olá](./media/active-directory-domain-services-getting-started/access-panel.png)

2. No hello canto superior direito, clique em seu nome e selecione **perfil** menu hello.

    ![Selecionar perfil](./media/active-directory-domain-services-getting-started/select-profile.png)

3. Em Olá **perfil** página, clique em **alterar senha**.

    ![Clique em "Alterar senha"](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > Se hello **alterar senha** opção não é exibida na janela de saudação do painel de acesso, certifique-se de que sua organização tenha configurado [gerenciamento de senhas no AD do Azure](../active-directory/active-directory-passwords-getting-started.md).
   >
   >
4. Em Olá **alterar senha** página, digite sua senha (antiga) existente, digite uma nova senha e, em seguida, confirmá-la.

    ![Criar uma rede virtual para os Serviços de Domínio do AD do Azure.](./media/active-directory-domain-services-getting-started/user-change-password2.png)

5. Clique em **Enviar**.

Alguns minutos depois que você alterou sua senha, a saudação nova senha é utilizável no Azure Active Directory Domain Services. Depois de alguns minutos (normalmente, cerca de 20 minutos), você pode entrar no toocomputers que domínio gerenciado toohello unidas usando senha Olá alterado recentemente.

## <a name="related-content"></a>Conteúdo relacionado
* [Como tooupdate sua própria senha](../active-directory/active-directory-passwords-update-your-own-password.md)
* [Introdução ao Gerenciamento de Senhas no Azure AD](../active-directory/active-directory-passwords-getting-started.md)
* [Habilitar a sincronização de senha do locatário aos serviços de domínio Active Directory de tooAzure um sincronizado do AD do Azure](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [Administrar um domínio gerenciado do Azure Active Directory Domain Services](active-directory-ds-admin-guide-administer-domain.md)
* [Ingressar em um domínio Windows máquina virtual tooan gerenciado do Azure Active Directory Domain Services](active-directory-ds-admin-guide-join-windows-vm.md)
* [Ingressar em um domínio de gerenciado do Azure Active Directory Domain Services de tooan de máquina virtual do Red Hat Enterprise Linux](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
