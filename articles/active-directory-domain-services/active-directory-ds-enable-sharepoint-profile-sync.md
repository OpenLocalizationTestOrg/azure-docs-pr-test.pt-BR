---
title: "Azure Active Directory Domain Services: Habilitar o suporte para o Serviço de Perfil de Usuário do SharePoint | Microsoft Docs"
description: "Configurar os domínios gerenciados do Azure Active Directory Domain Services para dar suporte à sincronização de perfil do SharePoint Server"
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
ms.openlocfilehash: c3c923b5c9cd652f0c5b0ec98c1cda740f180122
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-managed-domain-to-support-profile-synchronization-for-sharepoint-server"></a><span data-ttu-id="7bf01-103">Configurar um domínio gerenciado para dar suporte à sincronização de perfil do SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="7bf01-103">Configure a managed domain to support profile synchronization for SharePoint Server</span></span>
<span data-ttu-id="7bf01-104">O SharePoint Server inclui um Serviço de Perfil de Usuário que é usado para sincronização de perfil do usuário.</span><span class="sxs-lookup"><span data-stu-id="7bf01-104">SharePoint Server includes a User Profile Service that is used for user profile synchronization.</span></span> <span data-ttu-id="7bf01-105">Para configurar o Serviço de Perfil de Usuário, é necessário conceder as permissões apropriadas em um domínio do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7bf01-105">To set up the User Profile Service, appropriate permissions need to be granted on an Active Directory domain.</span></span> <span data-ttu-id="7bf01-106">Para saber mais, consulte [conceder permissões do Active Directory Domain Services para sincronização de perfil no SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span><span class="sxs-lookup"><span data-stu-id="7bf01-106">For more information, see [grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span></span>

<span data-ttu-id="7bf01-107">Este artigo explica como configurar domínios gerenciados do Azure AD Domain Services para implantar o serviço de Sincronização de Perfil de Usuário do SharePoint Server.</span><span class="sxs-lookup"><span data-stu-id="7bf01-107">This article explains how you can configure Azure AD Domain Services managed domains to deploy the SharePoint Server User Profile Sync service.</span></span>

## <a name="the-aad-dc-service-accounts-group"></a><span data-ttu-id="7bf01-108">O grupo 'Contas de Serviço do Controlador de Domínio do AAD'</span><span class="sxs-lookup"><span data-stu-id="7bf01-108">The 'AAD DC Service Accounts' group</span></span>
<span data-ttu-id="7bf01-109">Um grupo de segurança chamado '**Contas de Serviço do Controlador de Domínio do AAD**' está disponível na unidade organizacional 'Usuários' em seu domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="7bf01-109">A security group called '**AAD DC Service Accounts**' is available within the 'Users' organizational unit on your managed domain.</span></span> <span data-ttu-id="7bf01-110">Veja esse grupo no snap-in do MMC **Usuários e Computadores do Active Directory** em seu domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="7bf01-110">You can see this group in the **Active Directory Users and Computers** MMC snap-in on your managed domain.</span></span>

![Grupo de segurança Contas de Serviço do Controlador de Domínio do AAD](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

<span data-ttu-id="7bf01-112">Os membros desse grupo de segurança recebem os seguintes privilégios:</span><span class="sxs-lookup"><span data-stu-id="7bf01-112">Members of this security group are delegated the following privileges:</span></span>
- <span data-ttu-id="7bf01-113">O privilégio 'Replicar Alterações de Diretório' no DSE raiz do domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="7bf01-113">The 'Replicate Directory Changes' privilege on the root DSE of the managed domain.</span></span>
- <span data-ttu-id="7bf01-114">O privilégio 'Replicar Alterações de Diretório' no contexto de nomenclatura de configuração (cn = contêiner de configuração) do domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="7bf01-114">The 'Replicate Directory Changes' privilege on the Configuration naming context (cn=configuration container) of the managed domain.</span></span>

<span data-ttu-id="7bf01-115">Esse grupo de segurança também é membro do grupo interno **Acesso compatível anterior ao Windows 2000**.</span><span class="sxs-lookup"><span data-stu-id="7bf01-115">This security group is also a member of the built-in group **Pre-Windows 2000 Compatible Access**.</span></span>

![Grupo de segurança Contas de Serviço do Controlador de Domínio do AAD](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-to-support-sharepoint-server-user-profile-sync"></a><span data-ttu-id="7bf01-117">Habilitar seu domínio gerenciado para dar suporte à sincronização de perfil de usuário do SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="7bf01-117">Enable your managed domain to support SharePoint Server user profile sync</span></span>
<span data-ttu-id="7bf01-118">Você pode adicionar a conta de serviço usada para sincronização de perfil de usuário do SharePoint ao grupo **Contas de Serviço do Controlador de Domínio do AAD**.</span><span class="sxs-lookup"><span data-stu-id="7bf01-118">You can add the service account used for SharePoint user profile synchronization to the **AAD DC Service Accounts** group.</span></span> <span data-ttu-id="7bf01-119">Como resultado, a conta de sincronização recebe privilégios adequados para replicar as alterações no diretório.</span><span class="sxs-lookup"><span data-stu-id="7bf01-119">As a result, the synchronization account gets adequate privileges to replicate changes to the directory.</span></span> <span data-ttu-id="7bf01-120">Essa etapa de configuração permite que a sincronização de perfil de usuário do SharePoint Server funcione corretamente.</span><span class="sxs-lookup"><span data-stu-id="7bf01-120">This configuration step enables SharePoint Server user profile sync to work correctly.</span></span>

![Contas de Serviço do Controlador de Domínio do AAD - adicionar membros](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![Contas de Serviço do Controlador de Domínio do AAD - adicionar membros](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a><span data-ttu-id="7bf01-123">Conteúdo relacionado</span><span class="sxs-lookup"><span data-stu-id="7bf01-123">Related Content</span></span>
* [<span data-ttu-id="7bf01-124">Referência técnica - Conceder permissões do Active Directory Domain Services para sincronização de perfil no SharePoint Server 2013</span><span class="sxs-lookup"><span data-stu-id="7bf01-124">Technical Reference - Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013</span></span>](https://technet.microsoft.com/library/hh296982.aspx)
