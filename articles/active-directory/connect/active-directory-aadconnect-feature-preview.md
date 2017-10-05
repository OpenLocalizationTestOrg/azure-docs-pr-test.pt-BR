---
title: "Azure AD Connect: recursos em visualização | Microsoft Docs"
description: "Este tópico descreve em mais detalhes os recursos que estão na visualização no Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c75cd8cf-3eff-4619-bbca-66276757cc07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: cbf8f729d0ebfb271bb0d8702ac043442b42c262
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="more-details-about-features-in-preview"></a><span data-ttu-id="44cba-103">Mais detalhes sobre os recursos no modo de visualização</span><span class="sxs-lookup"><span data-stu-id="44cba-103">More details about features in preview</span></span>
<span data-ttu-id="44cba-104">Este tópico descreve como usar recursos presentes atualmente na visualização.</span><span class="sxs-lookup"><span data-stu-id="44cba-104">This topic describes how to use features currently in preview.</span></span>

## <a name="group-writeback"></a><span data-ttu-id="44cba-105">Write-back de grupo</span><span class="sxs-lookup"><span data-stu-id="44cba-105">Group writeback</span></span>
<span data-ttu-id="44cba-106">A opção para write-back do grupo nos recursos opcionais permite que você faça write-back de **Grupos do Office 365** para uma floresta com o Exchange instalado.</span><span class="sxs-lookup"><span data-stu-id="44cba-106">The option for group writeback in optional features allows you to writeback **Office 365 Groups** to a forest with Exchange installed.</span></span> <span data-ttu-id="44cba-107">Esse é um grupo que é sempre controlado na nuvem.</span><span class="sxs-lookup"><span data-stu-id="44cba-107">This is a group that is always mastered in the cloud.</span></span> <span data-ttu-id="44cba-108">Se tiver o Exchange local, você pode gravar novamente esses grupos localmente, assim os usuários com uma caixa de correio do Exchange local podem enviar e receber emails destes grupos.</span><span class="sxs-lookup"><span data-stu-id="44cba-108">If you have Exchange on-premises, then you can write back these groups to on-premises so users with an on-premises Exchange mailbox can send and receive emails from these groups.</span></span>

<span data-ttu-id="44cba-109">Mais informações sobre Grupos do Office 365 e como usá-los podem ser encontradas [aqui](http://aka.ms/O365g).</span><span class="sxs-lookup"><span data-stu-id="44cba-109">More information about Office 365 Groups and how to use them can be found [here](http://aka.ms/O365g).</span></span>

<span data-ttu-id="44cba-110">Um grupo do Office 365 é representado como um grupo de distribuição no AD DS local.</span><span class="sxs-lookup"><span data-stu-id="44cba-110">An Office 365 group is represented as a distribution group in on-premises AD DS.</span></span> <span data-ttu-id="44cba-111">Seu servidor Exchange local deve estar no Exchange 2013 com atualização cumulativa 8 (lançado em março de 2015) ou no Exchange 2016 para reconhecer esse novo tipo de grupo.</span><span class="sxs-lookup"><span data-stu-id="44cba-111">Your on-premises Exchange server must be on Exchange 2013 cumulative update 8 (released in March 2015) or Exchange 2016 to recognize this new group type.</span></span>

<span data-ttu-id="44cba-112">**Observações no período de visualização**</span><span class="sxs-lookup"><span data-stu-id="44cba-112">**Notes during the preview**</span></span>

* <span data-ttu-id="44cba-113">Atualmente, o atributo de catálogo de endereços não é populado na visualização.</span><span class="sxs-lookup"><span data-stu-id="44cba-113">The address book attribute is currently not populated in the preview.</span></span> <span data-ttu-id="44cba-114">Sem esse atributo, o grupo não estará visível na GAL.</span><span class="sxs-lookup"><span data-stu-id="44cba-114">Without this attribute, the group is not visible in the GAL.</span></span> <span data-ttu-id="44cba-115">A maneira mais fácil é preencher esse atributo para usar o cmdlet `update-recipient`do PowerShell do Exchange.</span><span class="sxs-lookup"><span data-stu-id="44cba-115">The easiest way to populate this attribute is to use the Exchange PowerShell cmdlet `update-recipient`.</span></span>
* <span data-ttu-id="44cba-116">Somente as florestas com o esquema do Exchange são alvos válidos para grupos.</span><span class="sxs-lookup"><span data-stu-id="44cba-116">Only forests with the Exchange schema are valid targets for groups.</span></span> <span data-ttu-id="44cba-117">Se nenhum Exchange for detectado, não será possível habilitar o write-back de grupo.</span><span class="sxs-lookup"><span data-stu-id="44cba-117">If no Exchange was detected, then group writeback is not possible to enable.</span></span>
* <span data-ttu-id="44cba-118">Somente implantações de floresta única de organização do Exchange terão suporte atualmente.</span><span class="sxs-lookup"><span data-stu-id="44cba-118">Only single-forest Exchange organization deployments are currently supported.</span></span> <span data-ttu-id="44cba-119">Se você tiver mais de uma organização de Exchange local, será necessária uma solução de GALSync local para que esses grupos sejam exibidos em suas outras florestas.</span><span class="sxs-lookup"><span data-stu-id="44cba-119">If you have more than one Exchange organization on-premises, then you need an on-premises GALSync solution for these groups to appear in your other forests.</span></span>
* <span data-ttu-id="44cba-120">O recurso de write-back de grupo não lida com grupos de segurança ou grupos de distribuição.</span><span class="sxs-lookup"><span data-stu-id="44cba-120">The Group writeback feature does not handle security groups or distribution groups.</span></span>

> [!NOTE]
> <span data-ttu-id="44cba-121">Uma assinatura do Azure AD Premium é necessária para write-back do grupo.</span><span class="sxs-lookup"><span data-stu-id="44cba-121">A subscription to Azure AD Premium is required for group writeback.</span></span>
> 
>

## <a name="user-writeback"></a><span data-ttu-id="44cba-122">Write-back de usuário</span><span class="sxs-lookup"><span data-stu-id="44cba-122">User writeback</span></span>
> [!IMPORTANT]
> <span data-ttu-id="44cba-123">O recurso de visualização de write-back do usuário foi removido na atualização de agosto de 2015 do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="44cba-123">The user writeback preview feature was removed in the August 2015 update to Azure AD Connect.</span></span> <span data-ttu-id="44cba-124">Se você tiver habilitado, você deve desabilitar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="44cba-124">If you have enabled it, then you should disable this feature.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="44cba-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="44cba-125">Next steps</span></span>
<span data-ttu-id="44cba-126">Continuar a [Instalação personalizada do Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="44cba-126">Continue your [Custom installation of Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span></span>

<span data-ttu-id="44cba-127">Saiba mais sobre a [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="44cba-127">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
