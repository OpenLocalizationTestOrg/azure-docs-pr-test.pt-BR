---
title: "Sincronização do Azure AD Connect: como gerenciar a conta de serviço do Azure AD | Microsoft Docs"
description: "Este tópico documenta como restaurar a conta de serviço do Azure AD."
services: active-directory
keywords: "AADSTS70002, AADSTS50054: Como redefinir a senha da conta de serviço do Conector de sincronização do Azure AD Connect"
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
ms.openlocfilehash: 8e9e8192ee4fcb636b5be91d2616acbc9120c8c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-how-to-manage-the-azure-ad-service-account"></a><span data-ttu-id="6a70c-104">Sincronização do Azure AD Connect: como gerenciar a conta de serviço do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6a70c-104">Azure AD Connect sync: How to manage the Azure AD service account</span></span>
<span data-ttu-id="6a70c-105">A conta de serviço usada pelo Azure AD Connector deve ter serviço gratuito.</span><span class="sxs-lookup"><span data-stu-id="6a70c-105">The service account used by the Azure AD Connector is supposed to be service free.</span></span> <span data-ttu-id="6a70c-106">Se você precisa redefinir suas credenciais, este tópico é indicado para você.</span><span class="sxs-lookup"><span data-stu-id="6a70c-106">If you need to reset its credentials, then this topic is for you.</span></span> <span data-ttu-id="6a70c-107">Por exemplo, se um Administrador Global tiver redefinido a senha por engano na conta de serviço usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6a70c-107">For example, if a Global Administrator has by mistake reset the password on the service account using PowerShell.</span></span>

## <a name="reset-the-credentials"></a><span data-ttu-id="6a70c-108">Redefinir as credenciais</span><span class="sxs-lookup"><span data-stu-id="6a70c-108">Reset the credentials</span></span>
<span data-ttu-id="6a70c-109">Se a conta de serviço definida no Azure AD Connector não puder contatar o Azure AD devido a problemas de autenticação, a senha poderá ser redefinida.</span><span class="sxs-lookup"><span data-stu-id="6a70c-109">If the service account defined on the Azure AD Connector cannot contact Azure AD due to authentication problems, the password can be reset.</span></span>

1. <span data-ttu-id="6a70c-110">Entre no servidor de sincronização do Azure AD Connector e inicie o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6a70c-110">Sign in to the Azure AD Connect sync server and start PowerShell.</span></span>
2. <span data-ttu-id="6a70c-111">Execute `Add-ADSyncAADServiceAccount`.</span><span class="sxs-lookup"><span data-stu-id="6a70c-111">Run `Add-ADSyncAADServiceAccount`.</span></span>  
   <span data-ttu-id="6a70c-112">![Cmdlet addadsyncaadserviceaccount do PowerShell](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span><span class="sxs-lookup"><span data-stu-id="6a70c-112">![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span></span>
3. <span data-ttu-id="6a70c-113">Forneça credenciais de Administrador Global do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6a70c-113">Provide Azure AD Global admin credentials.</span></span>

<span data-ttu-id="6a70c-114">Esse cmdlet redefinirá a senha da conta de serviço e a atualizará no Azure AD e no mecanismo de sincronização.</span><span class="sxs-lookup"><span data-stu-id="6a70c-114">This cmdlet resets the password for the service account and update it both in Azure AD and in the sync engine.</span></span>

## <a name="known-issues-these-steps-can-solve"></a><span data-ttu-id="6a70c-115">Problemas conhecidos que essas etapas podem resolver</span><span class="sxs-lookup"><span data-stu-id="6a70c-115">Known issues these steps can solve</span></span>
<span data-ttu-id="6a70c-116">Esta seção é uma lista de erros relatados por clientes que foram corrigidos por uma redefinição de credenciais na conta de serviço do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6a70c-116">This section is a list of errors reported by customers that were fixed by a credentials reset on the Azure AD service account.</span></span>

- - -
<span data-ttu-id="6a70c-117">Evento 6900</span><span class="sxs-lookup"><span data-stu-id="6a70c-117">Event 6900</span></span>  
<span data-ttu-id="6a70c-118">O servidor encontrou um erro inesperado ao processar uma notificação de alteração de senha:</span><span class="sxs-lookup"><span data-stu-id="6a70c-118">The server encountered an unexpected error while processing a password change notification:</span></span>  
<span data-ttu-id="6a70c-119">AADSTS70002: erro ao validar as credenciais.</span><span class="sxs-lookup"><span data-stu-id="6a70c-119">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="6a70c-120">AADSTS50054: A senha antiga é usada para autenticação.</span><span class="sxs-lookup"><span data-stu-id="6a70c-120">AADSTS50054: Old password is used for authentication.</span></span>

- - -
<span data-ttu-id="6a70c-121">Evento 659</span><span class="sxs-lookup"><span data-stu-id="6a70c-121">Event 659</span></span>  
<span data-ttu-id="6a70c-122">Erro ao recuperar a configuração de sincronização de política de senha.</span><span class="sxs-lookup"><span data-stu-id="6a70c-122">Error while retrieving password policy sync configuration.</span></span> <span data-ttu-id="6a70c-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span><span class="sxs-lookup"><span data-stu-id="6a70c-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span></span>  
<span data-ttu-id="6a70c-124">AADSTS70002: erro ao validar as credenciais.</span><span class="sxs-lookup"><span data-stu-id="6a70c-124">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="6a70c-125">AADSTS50054: A senha antiga é usada para autenticação.</span><span class="sxs-lookup"><span data-stu-id="6a70c-125">AADSTS50054: Old password is used for authentication.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a70c-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6a70c-126">Next steps</span></span>
<span data-ttu-id="6a70c-127">**Tópicos de visão geral**</span><span class="sxs-lookup"><span data-stu-id="6a70c-127">**Overview topics**</span></span>

* [<span data-ttu-id="6a70c-128">Sincronização do Azure AD Connect: compreender e personalizar a sincronização</span><span class="sxs-lookup"><span data-stu-id="6a70c-128">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="6a70c-129">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="6a70c-129">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

