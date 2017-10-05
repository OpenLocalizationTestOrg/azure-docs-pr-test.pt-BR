---
title: "Próximas etapas para o gerenciamento de acesso usando grupos | Microsoft Docs"
description: "Método avançado para gerenciamento dos grupos de segurança e como usar esses grupos para gerenciar o acesso a um recurso."
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
ms.openlocfilehash: 82fbeb379e90add09f7c569111053f6e9b1bc9c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="managing-owners-for-a-group"></a><span data-ttu-id="98e05-103">Gerenciando proprietários de um grupo</span><span class="sxs-lookup"><span data-stu-id="98e05-103">Managing owners for a group</span></span>
<span data-ttu-id="98e05-104">Após um proprietário de recurso ter o acesso a um grupo do Azure AD atribuído, a associação do grupo é gerenciada pelo proprietário do grupo.</span><span class="sxs-lookup"><span data-stu-id="98e05-104">Once a resource owner has assigned access to a resource to an Azure AD group, the membership of the group is managed by the group owner.</span></span> <span data-ttu-id="98e05-105">O proprietário do recurso delega efetivamente ao proprietário do grupo a permissão para atribuir usuários ao seu recurso.</span><span class="sxs-lookup"><span data-stu-id="98e05-105">The resource owner effectively delegates the permission to assign users to the resource to the owner of the group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="98e05-106">A Microsoft recomenda que você gerencie o Azure AD usando o [Centro de administração do AD do Azure](https://aad.portal.azure.com) no portal do Azure em vez de usar o portal clássico do Azure mencionado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="98e05-106">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> 

## <a name="assigning-group-ownership"></a><span data-ttu-id="98e05-107">Atribuindo a propriedade do grupo</span><span class="sxs-lookup"><span data-stu-id="98e05-107">Assigning group ownership</span></span>
<span data-ttu-id="98e05-108">**Para adicionar um proprietário a um grupo**</span><span class="sxs-lookup"><span data-stu-id="98e05-108">**To add an owner to a group**</span></span>

1. <span data-ttu-id="98e05-109">No [portal clássico do Azure](https://manage.windowsazure.com), selecione **Active Directory**e abra o diretório da sua organização.</span><span class="sxs-lookup"><span data-stu-id="98e05-109">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="98e05-110">Selecione a guia **Grupos** e, em seguida, abra o grupo ao qual você deseja adicionar os proprietários.</span><span class="sxs-lookup"><span data-stu-id="98e05-110">Select the **Groups** tab, and then open the group that you want to add owners to.</span></span>
3. <span data-ttu-id="98e05-111">Selecione **Adicionar Proprietários**.</span><span class="sxs-lookup"><span data-stu-id="98e05-111">Select **Add Owners**.</span></span>
4. <span data-ttu-id="98e05-112">Na página **Adicionar proprietários**, selecione o usuário que deseja adicionar como o proprietário deste grupo e verifique se esse nome é adicionado ao painel **Selecionado**.</span><span class="sxs-lookup"><span data-stu-id="98e05-112">On the **Add owners** page, select the user that you want to add as the owner of this group, and make sure this name is added to the **Selected** pane.</span></span>

<span data-ttu-id="98e05-113">**Para remover um proprietário de um grupo**</span><span class="sxs-lookup"><span data-stu-id="98e05-113">**To remove an owner from a group**</span></span>

1. <span data-ttu-id="98e05-114">No [portal clássico do Azure](https://manage.windowsazure.com), selecione **Active Directory**e abra o diretório da sua organização.</span><span class="sxs-lookup"><span data-stu-id="98e05-114">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="98e05-115">Selecione a guia **Grupos** e, em seguida, abra o grupo do qual deseja remover um proprietário.</span><span class="sxs-lookup"><span data-stu-id="98e05-115">Select the **Groups** tab, and then open the group that you want to remove an owner from.</span></span>
3. <span data-ttu-id="98e05-116">Selecione a guia **Proprietários** .</span><span class="sxs-lookup"><span data-stu-id="98e05-116">Select the **Owners** tab.</span></span>
4. <span data-ttu-id="98e05-117">Selecione o proprietário que você deseja remover deste grupo e, em seguida, selecione **Remover**.</span><span class="sxs-lookup"><span data-stu-id="98e05-117">Select the owner that you want to remove from this group, and then select **Remove**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="98e05-118">Informações adicionais</span><span class="sxs-lookup"><span data-stu-id="98e05-118">Additional information</span></span>
<span data-ttu-id="98e05-119">Esses artigos fornecem mais informações sobre o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="98e05-119">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="98e05-120">Gerenciamento de acesso a recursos com grupos do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="98e05-120">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="98e05-121">Cmdlets do Azure Active Directory para definir configurações de grupo</span><span class="sxs-lookup"><span data-stu-id="98e05-121">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="98e05-122">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="98e05-122">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="98e05-123">O que é o Active Directory do Azure?</span><span class="sxs-lookup"><span data-stu-id="98e05-123">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="98e05-124">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="98e05-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
