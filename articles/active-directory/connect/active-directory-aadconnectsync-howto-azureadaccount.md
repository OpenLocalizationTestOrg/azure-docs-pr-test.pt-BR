---
title: "Sincronização do Azure AD Connect: como conta de serviço toomanage Olá AD do Azure | Microsoft Docs"
description: "Este tópico documenta como conta de serviço toorestore Olá AD do Azure."
services: active-directory
keywords: "AADSTS70002, AADSTS50054, como tooreset Olá senha Olá sincronização do Azure AD Connect conta de serviço do conector"
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 6077043a-27f1-4304-a44b-81dc46620f24
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: e563518eae173de42a1d40bb5a76e63f29f9da42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomanage-hello-azure-ad-service-account"></a><span data-ttu-id="4880c-104">Sincronização do Azure AD Connect: como conta de serviço toomanage Olá AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4880c-104">Azure AD Connect sync: How toomanage hello Azure AD service account</span></span>
<span data-ttu-id="4880c-105">conta de serviço de saudação usada por Olá conector AD do Azure deve toobe serviço gratuito.</span><span class="sxs-lookup"><span data-stu-id="4880c-105">hello service account used by hello Azure AD Connector is supposed toobe service free.</span></span> <span data-ttu-id="4880c-106">Se você precisar tooreset suas credenciais, este tópico é para você.</span><span class="sxs-lookup"><span data-stu-id="4880c-106">If you need tooreset its credentials, then this topic is for you.</span></span> <span data-ttu-id="4880c-107">Por exemplo, se um Administrador Global tem por engano redefinir Olá senha na conta de serviço hello usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4880c-107">For example, if a Global Administrator has by mistake reset hello password on hello service account using PowerShell.</span></span>

## <a name="reset-hello-credentials"></a><span data-ttu-id="4880c-108">Redefinir credenciais de saudação</span><span class="sxs-lookup"><span data-stu-id="4880c-108">Reset hello credentials</span></span>
<span data-ttu-id="4880c-109">Se a conta de serviço de Olá definida no hello conector AD do Azure não pode entrar em contato com o AD do Azure devido a problemas de tooauthentication, Olá poderá ser redefinida.</span><span class="sxs-lookup"><span data-stu-id="4880c-109">If hello service account defined on hello Azure AD Connector cannot contact Azure AD due tooauthentication problems, hello password can be reset.</span></span>

1. <span data-ttu-id="4880c-110">Entre no servidor de sincronização do Azure AD Connect toohello e inicie o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4880c-110">Sign in toohello Azure AD Connect sync server and start PowerShell.</span></span>
2. <span data-ttu-id="4880c-111">Execute `Add-ADSyncAADServiceAccount`.</span><span class="sxs-lookup"><span data-stu-id="4880c-111">Run `Add-ADSyncAADServiceAccount`.</span></span>  
   <span data-ttu-id="4880c-112">![Cmdlet addadsyncaadserviceaccount do PowerShell](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span><span class="sxs-lookup"><span data-stu-id="4880c-112">![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span></span>
3. <span data-ttu-id="4880c-113">Forneça credenciais de Administrador Global do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4880c-113">Provide Azure AD Global admin credentials.</span></span>

<span data-ttu-id="4880c-114">Esse cmdlet redefine a senha Olá Olá conta de serviço e atualizá-lo no AD do Azure e no mecanismo de sincronização de saudação.</span><span class="sxs-lookup"><span data-stu-id="4880c-114">This cmdlet resets hello password for hello service account and update it both in Azure AD and in hello sync engine.</span></span>

## <a name="known-issues-these-steps-can-solve"></a><span data-ttu-id="4880c-115">Problemas conhecidos que essas etapas podem resolver</span><span class="sxs-lookup"><span data-stu-id="4880c-115">Known issues these steps can solve</span></span>
<span data-ttu-id="4880c-116">Esta seção é uma lista de erros relatados por clientes que foram corrigidos por um credenciais redefinir Olá conta de serviço do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4880c-116">This section is a list of errors reported by customers that were fixed by a credentials reset on hello Azure AD service account.</span></span>

- - -
<span data-ttu-id="4880c-117">Evento 6900</span><span class="sxs-lookup"><span data-stu-id="4880c-117">Event 6900</span></span>  
<span data-ttu-id="4880c-118">servidor de saudação encontrou um erro inesperado ao processar uma notificação de alteração de senha:</span><span class="sxs-lookup"><span data-stu-id="4880c-118">hello server encountered an unexpected error while processing a password change notification:</span></span>  
<span data-ttu-id="4880c-119">AADSTS70002: erro ao validar as credenciais.</span><span class="sxs-lookup"><span data-stu-id="4880c-119">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="4880c-120">AADSTS50054: A senha antiga é usada para autenticação.</span><span class="sxs-lookup"><span data-stu-id="4880c-120">AADSTS50054: Old password is used for authentication.</span></span>

- - -
<span data-ttu-id="4880c-121">Evento 659</span><span class="sxs-lookup"><span data-stu-id="4880c-121">Event 659</span></span>  
<span data-ttu-id="4880c-122">Erro ao recuperar a configuração de sincronização de política de senha.</span><span class="sxs-lookup"><span data-stu-id="4880c-122">Error while retrieving password policy sync configuration.</span></span> <span data-ttu-id="4880c-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span><span class="sxs-lookup"><span data-stu-id="4880c-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span></span>  
<span data-ttu-id="4880c-124">AADSTS70002: erro ao validar as credenciais.</span><span class="sxs-lookup"><span data-stu-id="4880c-124">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="4880c-125">AADSTS50054: A senha antiga é usada para autenticação.</span><span class="sxs-lookup"><span data-stu-id="4880c-125">AADSTS50054: Old password is used for authentication.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4880c-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4880c-126">Next steps</span></span>
<span data-ttu-id="4880c-127">**Tópicos de visão geral**</span><span class="sxs-lookup"><span data-stu-id="4880c-127">**Overview topics**</span></span>

* [<span data-ttu-id="4880c-128">Sincronização do Azure AD Connect: compreender e personalizar a sincronização</span><span class="sxs-lookup"><span data-stu-id="4880c-128">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="4880c-129">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4880c-129">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

