---
title: "Azure Active Directory Domain Services: Habilitar o suporte para o Serviço de Perfil de Usuário do SharePoint | Microsoft Docs"
description: "Configurar a sincronização de perfil do Azure Active Directory Domain Services domínios gerenciados toosupport para o SharePoint Server"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 9de4f810380309e8f6436fc24412701645978f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-managed-domain-toosupport-profile-synchronization-for-sharepoint-server"></a><span data-ttu-id="516a9-103">Configurar a sincronização de perfil do domínio gerenciado toosupport para o SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="516a9-103">Configure a managed domain toosupport profile synchronization for SharePoint Server</span></span>
<span data-ttu-id="516a9-104">O SharePoint Server inclui um Serviço de Perfil de Usuário que é usado para sincronização de perfil do usuário.</span><span class="sxs-lookup"><span data-stu-id="516a9-104">SharePoint Server includes a User Profile Service that is used for user profile synchronization.</span></span> <span data-ttu-id="516a9-105">tooset backup Olá serviço de perfil de usuário, as permissões apropriadas necessário toobe concedida em um domínio do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="516a9-105">tooset up hello User Profile Service, appropriate permissions need toobe granted on an Active Directory domain.</span></span> <span data-ttu-id="516a9-106">Para saber mais, consulte [conceder permissões do Active Directory Domain Services para sincronização de perfil no SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span><span class="sxs-lookup"><span data-stu-id="516a9-106">For more information, see [grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span></span>

<span data-ttu-id="516a9-107">Este artigo explica como você pode configurar o serviço de sincronização de perfil de usuário do servidor do SharePoint do serviços de domínio do AD do Azure domínios gerenciados toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="516a9-107">This article explains how you can configure Azure AD Domain Services managed domains toodeploy hello SharePoint Server User Profile Sync service.</span></span>

## <a name="hello-aad-dc-service-accounts-group"></a><span data-ttu-id="516a9-108">grupo de 'Contas de serviço de controlador de domínio do AAD' Hello</span><span class="sxs-lookup"><span data-stu-id="516a9-108">hello 'AAD DC Service Accounts' group</span></span>
<span data-ttu-id="516a9-109">Um grupo de segurança chamado '**contas de serviço de controlador de domínio do AAD**' está disponível na unidade organizacional do hello 'Usuários' em seu domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="516a9-109">A security group called '**AAD DC Service Accounts**' is available within hello 'Users' organizational unit on your managed domain.</span></span> <span data-ttu-id="516a9-110">Você pode ver esse grupo em Olá **computadores e usuários do Active Directory** snap-in do MMC no seu domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="516a9-110">You can see this group in hello **Active Directory Users and Computers** MMC snap-in on your managed domain.</span></span>

![Grupo de segurança Contas de Serviço do Controlador de Domínio do AAD](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

<span data-ttu-id="516a9-112">Os membros desse grupo de segurança são delegada Olá privilégios a seguir:</span><span class="sxs-lookup"><span data-stu-id="516a9-112">Members of this security group are delegated hello following privileges:</span></span>
- <span data-ttu-id="516a9-113">privilégio de 'Replicar alterações de diretório' Hello na raiz de saudação DSE de saudação gerenciadas de domínio.</span><span class="sxs-lookup"><span data-stu-id="516a9-113">hello 'Replicate Directory Changes' privilege on hello root DSE of hello managed domain.</span></span>
- <span data-ttu-id="516a9-114">Olá privilégio 'Replicar alterações de diretório' no contexto de nomenclatura de configuração de saudação (cn = contêiner de configuração) do hello gerenciados no domínio.</span><span class="sxs-lookup"><span data-stu-id="516a9-114">hello 'Replicate Directory Changes' privilege on hello Configuration naming context (cn=configuration container) of hello managed domain.</span></span>

<span data-ttu-id="516a9-115">Esse grupo de segurança também é um membro do grupo interno Olá **acesso compatível do Windows 2000**.</span><span class="sxs-lookup"><span data-stu-id="516a9-115">This security group is also a member of hello built-in group **Pre-Windows 2000 Compatible Access**.</span></span>

![Grupo de segurança Contas de Serviço do Controlador de Domínio do AAD](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-toosupport-sharepoint-server-user-profile-sync"></a><span data-ttu-id="516a9-117">Habilitar toosupport seu domínio gerenciado sincronização de perfil de usuário do SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="516a9-117">Enable your managed domain toosupport SharePoint Server user profile sync</span></span>
<span data-ttu-id="516a9-118">Você pode adicionar a conta de serviço de saudação usada para toohello de sincronização de perfil de usuário do SharePoint **contas de serviço de controlador de domínio do AAD** grupo.</span><span class="sxs-lookup"><span data-stu-id="516a9-118">You can add hello service account used for SharePoint user profile synchronization toohello **AAD DC Service Accounts** group.</span></span> <span data-ttu-id="516a9-119">Como resultado, conta de sincronização de saudação obtém o diretório de toohello privilégios adequados tooreplicate alterações.</span><span class="sxs-lookup"><span data-stu-id="516a9-119">As a result, hello synchronization account gets adequate privileges tooreplicate changes toohello directory.</span></span> <span data-ttu-id="516a9-120">Essa etapa de configuração permite que o SharePoint Server toowork de sincronização de perfil de usuário corretamente.</span><span class="sxs-lookup"><span data-stu-id="516a9-120">This configuration step enables SharePoint Server user profile sync toowork correctly.</span></span>

![Contas de Serviço do Controlador de Domínio do AAD - adicionar membros](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![Contas de Serviço do Controlador de Domínio do AAD - adicionar membros](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a><span data-ttu-id="516a9-123">Conteúdo relacionado</span><span class="sxs-lookup"><span data-stu-id="516a9-123">Related Content</span></span>
* [<span data-ttu-id="516a9-124">Referência técnica - Conceder permissões do Active Directory Domain Services para sincronização de perfil no SharePoint Server 2013</span><span class="sxs-lookup"><span data-stu-id="516a9-124">Technical Reference - Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013</span></span>](https://technet.microsoft.com/library/hh296982.aspx)
