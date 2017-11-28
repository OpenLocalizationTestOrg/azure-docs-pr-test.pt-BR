---
title: aaaNext as etapas para usar grupos de gerenciamento de acesso | Microsoft Docs
description: "Avançado como-para gerenciar grupos de segurança e como toouse esses grupos toomanage acesso tooa de recursos."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 44350a3c-8ea1-4da1-aaac-7fc53933dd21
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 4fd55f893290fac3551a130f29bd12709cf551e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-owners-for-a-group"></a><span data-ttu-id="a1216-103">Gerenciando proprietários de um grupo</span><span class="sxs-lookup"><span data-stu-id="a1216-103">Managing owners for a group</span></span>
<span data-ttu-id="a1216-104">Depois de atribuir um proprietário do recurso tem o grupo de AD do Azure do acesso tooa recursos tooan, associação de saudação do grupo de saudação é gerenciada pelo proprietário do grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1216-104">Once a resource owner has assigned access tooa resource tooan Azure AD group, hello membership of hello group is managed by hello group owner.</span></span> <span data-ttu-id="a1216-105">proprietário do recurso Olá delega efetivamente Olá permissão tooassign usuários toohello toohello proprietário do recurso de grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1216-105">hello resource owner effectively delegates hello permission tooassign users toohello resource toohello owner of hello group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a1216-106">A Microsoft recomenda que você gerencie o AD do Azure usando Olá [Centro de administração do AD do Azure](https://aad.portal.azure.com) em Olá portal do Azure em vez de usar Olá portal clássico do Azure mencionado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="a1216-106">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 

## <a name="assigning-group-ownership"></a><span data-ttu-id="a1216-107">Atribuindo a propriedade do grupo</span><span class="sxs-lookup"><span data-stu-id="a1216-107">Assigning group ownership</span></span>
<span data-ttu-id="a1216-108">**tooadd um grupo de tooa do proprietário**</span><span class="sxs-lookup"><span data-stu-id="a1216-108">**tooadd an owner tooa group**</span></span>

1. <span data-ttu-id="a1216-109">Em Olá [portal clássico do Azure](https://manage.windowsazure.com), selecione **do Active Directory**e, em seguida, abra o diretório da sua organização.</span><span class="sxs-lookup"><span data-stu-id="a1216-109">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="a1216-110">Selecione Olá **grupos** guia e grupo hello, em seguida, abra que você deseja que os proprietários de tooadd.</span><span class="sxs-lookup"><span data-stu-id="a1216-110">Select hello **Groups** tab, and then open hello group that you want tooadd owners to.</span></span>
3. <span data-ttu-id="a1216-111">Selecione **Adicionar Proprietários**.</span><span class="sxs-lookup"><span data-stu-id="a1216-111">Select **Add Owners**.</span></span>
4. <span data-ttu-id="a1216-112">Em Olá **adicionar proprietários** página, o usuário selecione Olá que você deseja tooadd como proprietário Olá desse grupo e verifique se esse nome está adicionado toohello **selecionados** painel.</span><span class="sxs-lookup"><span data-stu-id="a1216-112">On hello **Add owners** page, select hello user that you want tooadd as hello owner of this group, and make sure this name is added toohello **Selected** pane.</span></span>

<span data-ttu-id="a1216-113">**tooremove um proprietário de um grupo**</span><span class="sxs-lookup"><span data-stu-id="a1216-113">**tooremove an owner from a group**</span></span>

1. <span data-ttu-id="a1216-114">Em Olá [portal clássico do Azure](https://manage.windowsazure.com), selecione **do Active Directory**e, em seguida, abra o diretório da sua organização.</span><span class="sxs-lookup"><span data-stu-id="a1216-114">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="a1216-115">Selecione Olá **grupos** guia e, em seguida, abra hello grupo que você deseja tooremove um proprietário.</span><span class="sxs-lookup"><span data-stu-id="a1216-115">Select hello **Groups** tab, and then open hello group that you want tooremove an owner from.</span></span>
3. <span data-ttu-id="a1216-116">Selecione Olá **proprietários** guia.</span><span class="sxs-lookup"><span data-stu-id="a1216-116">Select hello **Owners** tab.</span></span>
4. <span data-ttu-id="a1216-117">Proprietário Olá selecione que você deseja tooremove deste grupo e, em seguida, selecione **remover**.</span><span class="sxs-lookup"><span data-stu-id="a1216-117">Select hello owner that you want tooremove from this group, and then select **Remove**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="a1216-118">Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="a1216-118">Additional information</span></span>
<span data-ttu-id="a1216-119">Esses artigos fornecem mais informações sobre o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1216-119">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="a1216-120">Gerenciando acesso tooresources com grupos do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a1216-120">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="a1216-121">Cmdlets do Azure Active Directory para definir configurações de grupo</span><span class="sxs-lookup"><span data-stu-id="a1216-121">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="a1216-122">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a1216-122">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="a1216-123">O que é o Active Directory do Azure?</span><span class="sxs-lookup"><span data-stu-id="a1216-123">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="a1216-124">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a1216-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
