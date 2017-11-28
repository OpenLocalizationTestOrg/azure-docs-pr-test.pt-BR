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
ms.openlocfilehash: bcfc710861b19d8f86f094ced0d1c691e0911f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="more-details-about-features-in-preview"></a><span data-ttu-id="d7b65-103">Mais detalhes sobre os recursos no modo de visualização</span><span class="sxs-lookup"><span data-stu-id="d7b65-103">More details about features in preview</span></span>
<span data-ttu-id="d7b65-104">Este tópico descreve como toouse recursos atualmente na visualização.</span><span class="sxs-lookup"><span data-stu-id="d7b65-104">This topic describes how toouse features currently in preview.</span></span>

## <a name="group-writeback"></a><span data-ttu-id="d7b65-105">Write-back de grupo</span><span class="sxs-lookup"><span data-stu-id="d7b65-105">Group writeback</span></span>
<span data-ttu-id="d7b65-106">opção de saudação para write-back de grupo de recursos opcionais permite toowriteback **grupos do Office 365** tooa floresta com o Exchange instalado.</span><span class="sxs-lookup"><span data-stu-id="d7b65-106">hello option for group writeback in optional features allows you toowriteback **Office 365 Groups** tooa forest with Exchange installed.</span></span> <span data-ttu-id="d7b65-107">Esse é um grupo que é sempre controlado na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="d7b65-107">This is a group that is always mastered in hello cloud.</span></span> <span data-ttu-id="d7b65-108">Se você tiver o Exchange no local, em seguida, você pode write-back esses grupos tooon local para enviar e receber emails destes grupos de usuários com uma caixa de correio do Exchange no local.</span><span class="sxs-lookup"><span data-stu-id="d7b65-108">If you have Exchange on-premises, then you can write back these groups tooon-premises so users with an on-premises Exchange mailbox can send and receive emails from these groups.</span></span>

<span data-ttu-id="d7b65-109">Para obter mais informações sobre grupos do Office 365 e como toouse-los podem ser encontrados [aqui](http://aka.ms/O365g).</span><span class="sxs-lookup"><span data-stu-id="d7b65-109">More information about Office 365 Groups and how toouse them can be found [here](http://aka.ms/O365g).</span></span>

<span data-ttu-id="d7b65-110">Um grupo do Office 365 é representado como um grupo de distribuição no AD DS local.</span><span class="sxs-lookup"><span data-stu-id="d7b65-110">An Office 365 group is represented as a distribution group in on-premises AD DS.</span></span> <span data-ttu-id="d7b65-111">Seu Exchange server local deve ser no Exchange 2013 atualização cumulativa 8 (lançado em março de 2015) ou Exchange 2016 toorecognize esse novo tipo de grupo.</span><span class="sxs-lookup"><span data-stu-id="d7b65-111">Your on-premises Exchange server must be on Exchange 2013 cumulative update 8 (released in March 2015) or Exchange 2016 toorecognize this new group type.</span></span>

<span data-ttu-id="d7b65-112">**Anotações durante a visualização de saudação**</span><span class="sxs-lookup"><span data-stu-id="d7b65-112">**Notes during hello preview**</span></span>

* <span data-ttu-id="d7b65-113">atributo de catálogo de endereço Olá não é populado atualmente na visualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="d7b65-113">hello address book attribute is currently not populated in hello preview.</span></span> <span data-ttu-id="d7b65-114">Sem esse atributo, o grupo de saudação não está visível no hello GAL.</span><span class="sxs-lookup"><span data-stu-id="d7b65-114">Without this attribute, hello group is not visible in hello GAL.</span></span> <span data-ttu-id="d7b65-115">Olá toopopulate de maneira mais fácil esse atributo é um cmdlet de PowerShell do Exchange Olá toouse `update-recipient`.</span><span class="sxs-lookup"><span data-stu-id="d7b65-115">hello easiest way toopopulate this attribute is toouse hello Exchange PowerShell cmdlet `update-recipient`.</span></span>
* <span data-ttu-id="d7b65-116">Somente as florestas com o esquema de saudação do Exchange são destinos válidos para grupos.</span><span class="sxs-lookup"><span data-stu-id="d7b65-116">Only forests with hello Exchange schema are valid targets for groups.</span></span> <span data-ttu-id="d7b65-117">Se nenhum Exchange for detectado, Write-back de grupo não é possível tooenable.</span><span class="sxs-lookup"><span data-stu-id="d7b65-117">If no Exchange was detected, then group writeback is not possible tooenable.</span></span>
* <span data-ttu-id="d7b65-118">Somente implantações de floresta única de organização do Exchange terão suporte atualmente.</span><span class="sxs-lookup"><span data-stu-id="d7b65-118">Only single-forest Exchange organization deployments are currently supported.</span></span> <span data-ttu-id="d7b65-119">Se você tiver mais de uma organização de Exchange no local, em seguida, você precisa uma solução GALSync de local para tooappear esses grupos em sua outras florestas.</span><span class="sxs-lookup"><span data-stu-id="d7b65-119">If you have more than one Exchange organization on-premises, then you need an on-premises GALSync solution for these groups tooappear in your other forests.</span></span>
* <span data-ttu-id="d7b65-120">recurso de write-back de grupo Olá não lida com grupos de segurança ou grupos de distribuição.</span><span class="sxs-lookup"><span data-stu-id="d7b65-120">hello Group writeback feature does not handle security groups or distribution groups.</span></span>

> [!NOTE]
> <span data-ttu-id="d7b65-121">TooAzure uma assinatura Premium do AD é necessária para write-back de grupo.</span><span class="sxs-lookup"><span data-stu-id="d7b65-121">A subscription tooAzure AD Premium is required for group writeback.</span></span>
> 
>

## <a name="user-writeback"></a><span data-ttu-id="d7b65-122">Write-back de usuário</span><span class="sxs-lookup"><span data-stu-id="d7b65-122">User writeback</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d7b65-123">Olá recurso de visualização de write-back de usuário foi removido na tooAzure de atualização de agosto de 2015 Olá AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d7b65-123">hello user writeback preview feature was removed in hello August 2015 update tooAzure AD Connect.</span></span> <span data-ttu-id="d7b65-124">Se você tiver habilitado, você deve desabilitar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="d7b65-124">If you have enabled it, then you should disable this feature.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="d7b65-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d7b65-125">Next steps</span></span>
<span data-ttu-id="d7b65-126">Continuar a [Instalação personalizada do Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="d7b65-126">Continue your [Custom installation of Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span></span>

<span data-ttu-id="d7b65-127">Saiba mais sobre a [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="d7b65-127">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
