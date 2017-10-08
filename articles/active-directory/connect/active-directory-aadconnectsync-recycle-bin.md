---
title: "Sincronização do Azure AD Connect: habilitar a lixeira do AD | Microsoft Docs"
description: "Este tópico recomenda o uso de saudação do recurso Lixeira do AD do Azure AD Connect."
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
ms.openlocfilehash: 2bb4827d677ccecfd8d2861f2a2fcf73b8cc2d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-enable-ad-recycle-bin"></a><span data-ttu-id="97039-104">Sincronização do Azure AD Connect: habilitar a lixeira do AD</span><span class="sxs-lookup"><span data-stu-id="97039-104">Azure AD Connect sync: Enable AD recycle bin</span></span>
<span data-ttu-id="97039-105">É recomendável que você habilite o recurso de Lixeira Olá AD para seus diretórios Active local, que são sincronizado tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="97039-105">It is recommended that you enable hello AD Recycle Bin feature for your on-premises Active Directories, which are synchronized tooAzure AD.</span></span> 

<span data-ttu-id="97039-106">Se você excluiu acidentalmente um local o objeto de usuário do AD e restauração-o usando o recurso de hello, AD do Azure restaura o objeto de usuário do AD do Azure correspondente hello.</span><span class="sxs-lookup"><span data-stu-id="97039-106">If you accidentally deleted an on-premises AD user object and restore it using hello feature, Azure AD restores hello corresponding Azure AD user object.</span></span>  <span data-ttu-id="97039-107">Para obter informações sobre o recurso de Lixeira Olá AD, consulte tooarticle [visão geral do cenário de restauração de excluir objetos do Active Directory](https://technet.microsoft.com/library/dd379542.aspx).</span><span class="sxs-lookup"><span data-stu-id="97039-107">For information about hello AD Recycle Bin feature, refer tooarticle [Scenario Overview for Restoring Deleted Active Directory Objects](https://technet.microsoft.com/library/dd379542.aspx).</span></span>

## <a name="benefits-of-enabling-hello-ad-recycle-bin"></a><span data-ttu-id="97039-108">Benefícios da habilitação Olá AD Lixeira</span><span class="sxs-lookup"><span data-stu-id="97039-108">Benefits of enabling hello AD recycle bin</span></span>
<span data-ttu-id="97039-109">Esse recurso ajuda a restaurar objetos de usuário do AD do Azure fazendo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="97039-109">This feature helps with restoring Azure AD user objects by doing hello following:</span></span>

* <span data-ttu-id="97039-110">Se você excluiu acidentalmente um local em objeto de usuário do AD, objeto de usuário do AD do Azure correspondente Olá será excluído no hello próximo ciclo de sincronização.</span><span class="sxs-lookup"><span data-stu-id="97039-110">If you accidentally deleted an on-premises AD user object, hello corresponding Azure AD user object will be deleted in hello next sync cycle.</span></span> <span data-ttu-id="97039-111">Por padrão, o AD do Azure mantém objeto de usuário do AD do Azure Olá excluído no estado excluído por 30 dias.</span><span class="sxs-lookup"><span data-stu-id="97039-111">By default, Azure AD keeps hello deleted Azure AD user object in soft-deleted state for 30 days.</span></span>

* <span data-ttu-id="97039-112">Se você tiver local recurso Lixeira do AD habilitado, você pode restaurar Olá excluído local objeto de usuário do AD sem alterar seu valor de âncora de origem.</span><span class="sxs-lookup"><span data-stu-id="97039-112">If you have on-premises AD Recycle Bin feature enabled, you can restore hello deleted on-premises AD user object without changing its Source Anchor value.</span></span> <span data-ttu-id="97039-113">Quando a saudação recuperados no local o objeto de usuário do AD está sincronizado tooAzure AD, Azure AD irá restaurar Olá correspondente excluído o objeto de usuário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="97039-113">When hello recovered on-premises AD user object is synchronized tooAzure AD, Azure AD will restore hello corresponding soft-deleted Azure AD user object.</span></span> <span data-ttu-id="97039-114">Para obter informações sobre o atributo de âncora de origem, consulte tooarticle [do Azure AD Connect: conceitos de projeto](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span><span class="sxs-lookup"><span data-stu-id="97039-114">For information about Source Anchor attribute, refer tooarticle [Azure AD Connect: Design concepts](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span></span>

* <span data-ttu-id="97039-115">Se você não tiver local AD reciclar o recurso de compartimento habilitado, talvez seja necessário toocreate um objeto AD usuário objeto tooreplace Olá excluído.</span><span class="sxs-lookup"><span data-stu-id="97039-115">If you do not have on-premises AD Recycle Bin feature enabled, you may be required toocreate an AD user object tooreplace hello deleted object.</span></span> <span data-ttu-id="97039-116">Se serviço de sincronização do Azure AD Connect é configurado toouse gerada pelo sistema AD atributo (como o ObjectGuid) para o atributo de âncora de origem hello, hello recém-criado objeto de usuário do AD será não têm Olá mesmo valor de âncora de origem como Olá excluiu o objeto de usuário do AD.</span><span class="sxs-lookup"><span data-stu-id="97039-116">If Azure AD Connect Synchronization Service is configured toouse system-generated AD attribute (such as ObjectGuid) for hello Source Anchor attribute, hello newly created AD user object will not have hello same Source Anchor value as hello deleted AD user object.</span></span> <span data-ttu-id="97039-117">Quando hello recém-criado objeto de usuário do AD está sincronizada tooAzure AD, o AD do Azure cria um novo objeto de usuário do AD do Azure em vez de restaurar o objeto de usuário do AD do Azure Olá excluídos por software.</span><span class="sxs-lookup"><span data-stu-id="97039-117">When hello newly created AD user object is synchronized tooAzure AD, Azure AD creates a new Azure AD user object instead of restoring hello soft-deleted Azure AD user object.</span></span>

> [!NOTE]
> <span data-ttu-id="97039-118">Por padrão, o Azure AD mantém objetos de usuário excluídos do Azure AD em estado de exclusão temporária durante 30 dias antes que eles sejam excluídos permanentemente.</span><span class="sxs-lookup"><span data-stu-id="97039-118">By default, Azure AD keeps deleted Azure AD user objects in soft-deleted state for 30 days before they are permanently deleted.</span></span> <span data-ttu-id="97039-119">No entanto, os administradores podem acelerar exclusão Olá desses objetos.</span><span class="sxs-lookup"><span data-stu-id="97039-119">However, administrators can accelerate hello deletion of such objects.</span></span> <span data-ttu-id="97039-120">Depois que os objetos de saudação são excluídos permanentemente, não podem ser recuperados, mesmo se a Lixeira do AD está ativado no local.</span><span class="sxs-lookup"><span data-stu-id="97039-120">Once hello objects are permanently deleted, they can no longer be recovered, even if on-premises AD Recycle Bin feature is enabled.</span></span>



## <a name="next-steps"></a><span data-ttu-id="97039-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="97039-121">Next steps</span></span>
<span data-ttu-id="97039-122">**Tópicos de visão geral**</span><span class="sxs-lookup"><span data-stu-id="97039-122">**Overview topics**</span></span>

* [<span data-ttu-id="97039-123">Sincronização do Azure AD Connect: compreender e personalizar a sincronização</span><span class="sxs-lookup"><span data-stu-id="97039-123">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="97039-124">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="97039-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
