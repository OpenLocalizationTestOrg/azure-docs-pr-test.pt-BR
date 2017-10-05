---
title: "Sincronização do Azure AD Connect: habilitar a lixeira do AD | Microsoft Docs"
description: "Este tópico recomenda o uso do recurso Lixeira do AD com o Azure AD Connect."
services: active-directory
keywords: "Lixeira do AD, exclusão acidental, âncora de origem"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: afec4207-74f7-4cdd-b13a-574af5223a90
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: eb455477547f3db8245cf3601576eba9c6fdc56f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-enable-ad-recycle-bin"></a><span data-ttu-id="aca87-104">Sincronização do Azure AD Connect: habilitar a lixeira do AD</span><span class="sxs-lookup"><span data-stu-id="aca87-104">Azure AD Connect sync: Enable AD recycle bin</span></span>
<span data-ttu-id="aca87-105">É recomendável que você habilite o recurso Lixeira do AD para seus Active Directories locais, sincronizados com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aca87-105">It is recommended that you enable the AD Recycle Bin feature for your on-premises Active Directories, which are synchronized to Azure AD.</span></span> 

<span data-ttu-id="aca87-106">Se você excluiu acidentalmente um objeto de usuário do AD local e o restaurou usando o recurso, o Azure AD restaura o objeto de usuário do Azure AD correspondente.</span><span class="sxs-lookup"><span data-stu-id="aca87-106">If you accidentally deleted an on-premises AD user object and restore it using the feature, Azure AD restores the corresponding Azure AD user object.</span></span>  <span data-ttu-id="aca87-107">Para obter informações sobre o recurso Lixeira do AD, consulte o artigo [Scenario Overview for Restoring Deleted Active Directory Objects (Visão geral do cenário de restauração de objetos do Active Directory excluídos)](https://technet.microsoft.com/library/dd379542.aspx).</span><span class="sxs-lookup"><span data-stu-id="aca87-107">For information about the AD Recycle Bin feature, refer to article [Scenario Overview for Restoring Deleted Active Directory Objects](https://technet.microsoft.com/library/dd379542.aspx).</span></span>

## <a name="benefits-of-enabling-the-ad-recycle-bin"></a><span data-ttu-id="aca87-108">Benefícios da habilitação da lixeira do AD</span><span class="sxs-lookup"><span data-stu-id="aca87-108">Benefits of enabling the AD recycle bin</span></span>
<span data-ttu-id="aca87-109">Esse recurso ajuda a restaurar os objetos de usuário do Azure AD, fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="aca87-109">This feature helps with restoring Azure AD user objects by doing the following:</span></span>

* <span data-ttu-id="aca87-110">Se você excluiu acidentalmente um objeto de usuário do AD local, o objeto de usuário do Azure AD correspondente será excluído no próximo ciclo de sincronização.</span><span class="sxs-lookup"><span data-stu-id="aca87-110">If you accidentally deleted an on-premises AD user object, the corresponding Azure AD user object will be deleted in the next sync cycle.</span></span> <span data-ttu-id="aca87-111">Por padrão, o Azure AD mantém o objeto de usuário excluído do Azure AD em estado de exclusão temporária durante 30 dias.</span><span class="sxs-lookup"><span data-stu-id="aca87-111">By default, Azure AD keeps the deleted Azure AD user object in soft-deleted state for 30 days.</span></span>

* <span data-ttu-id="aca87-112">Se você o recurso Lixeira do AD local estiver habilitado, será possível restaurar o objeto de usuário excluído do AD local sem alterar seu valor de Âncora de origem.</span><span class="sxs-lookup"><span data-stu-id="aca87-112">If you have on-premises AD Recycle Bin feature enabled, you can restore the deleted on-premises AD user object without changing its Source Anchor value.</span></span> <span data-ttu-id="aca87-113">Quando o objeto de usuário recuperado do AD local for sincronizado com o Azure AD, o Azure AD restaurará o objeto de usuário excluído temporariamente correspondente do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aca87-113">When the recovered on-premises AD user object is synchronized to Azure AD, Azure AD will restore the corresponding soft-deleted Azure AD user object.</span></span> <span data-ttu-id="aca87-114">Para obter informações sobre o atributo Âncora de origem, consulte o artigo [Azure AD Connect: conceitos de design](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span><span class="sxs-lookup"><span data-stu-id="aca87-114">For information about Source Anchor attribute, refer to article [Azure AD Connect: Design concepts](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span></span>

* <span data-ttu-id="aca87-115">Se você não tiver o recurso Lixeira do AD local habilitado, talvez seja necessário criar um objeto de usuário do AD para substituir o objeto excluído.</span><span class="sxs-lookup"><span data-stu-id="aca87-115">If you do not have on-premises AD Recycle Bin feature enabled, you may be required to create an AD user object to replace the deleted object.</span></span> <span data-ttu-id="aca87-116">Se o Azure AD Connect Synchronization Service tiver sido configurado para usar o atributo do AD gerado pelo sistema (por exemplo, ObjectGuid) para o atributo Âncora de origem, o objeto de usuário do AD recém-criado não terá o mesmo valor de Âncora de origem que o objeto de usuário excluído do AD.</span><span class="sxs-lookup"><span data-stu-id="aca87-116">If Azure AD Connect Synchronization Service is configured to use system-generated AD attribute (such as ObjectGuid) for the Source Anchor attribute, the newly created AD user object will not have the same Source Anchor value as the deleted AD user object.</span></span> <span data-ttu-id="aca87-117">Quando o objeto de usuário recém-criado do AD for sincronizado com o Azure AD, o Azure AD criará um novo objeto de usuário do Azure AD em vez de restaurar o objeto de usuário excluído temporariamente do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aca87-117">When the newly created AD user object is synchronized to Azure AD, Azure AD creates a new Azure AD user object instead of restoring the soft-deleted Azure AD user object.</span></span>

> [!NOTE]
> <span data-ttu-id="aca87-118">Por padrão, o Azure AD mantém objetos de usuário excluídos do Azure AD em estado de exclusão temporária durante 30 dias antes que eles sejam excluídos permanentemente.</span><span class="sxs-lookup"><span data-stu-id="aca87-118">By default, Azure AD keeps deleted Azure AD user objects in soft-deleted state for 30 days before they are permanently deleted.</span></span> <span data-ttu-id="aca87-119">No entanto, os administradores podem acelerar a exclusão desses objetos.</span><span class="sxs-lookup"><span data-stu-id="aca87-119">However, administrators can accelerate the deletion of such objects.</span></span> <span data-ttu-id="aca87-120">Depois que os objetos forem excluídos permanentemente, eles não poderão mais ser recuperados, mesmo se o recurso Lixeira do AD local estiver habilitado.</span><span class="sxs-lookup"><span data-stu-id="aca87-120">Once the objects are permanently deleted, they can no longer be recovered, even if on-premises AD Recycle Bin feature is enabled.</span></span>



## <a name="next-steps"></a><span data-ttu-id="aca87-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aca87-121">Next steps</span></span>
<span data-ttu-id="aca87-122">**Tópicos de visão geral**</span><span class="sxs-lookup"><span data-stu-id="aca87-122">**Overview topics**</span></span>

* [<span data-ttu-id="aca87-123">Sincronização do Azure AD Connect: compreender e personalizar a sincronização</span><span class="sxs-lookup"><span data-stu-id="aca87-123">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="aca87-124">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="aca87-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
