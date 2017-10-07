---
title: "políticas de acesso condicional com base no dispositivo do Active Directory do Azure aaaConfigure | Microsoft Docs"
description: "Saiba como políticas de acesso condicional com base no dispositivo do tooconfigure Active Directory do Azure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a27862a6-d513-43ba-97c1-1c0d400bf243
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc5923b8ccee4335442c17ef63b2ee6f098e104e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-active-directory-device-based-conditional-access-policies"></a><span data-ttu-id="64b0d-103">Configurar políticas de acesso condicional com base no dispositivo do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="64b0d-103">Configure Azure Active Directory device-based conditional access policies</span></span>

<span data-ttu-id="64b0d-104">Com o [acesso condicional do Azure AD (Active Directory)](active-directory-conditional-access-azure-portal.md), você pode ajustar como usuários autorizados podem acessar seus recursos.</span><span class="sxs-lookup"><span data-stu-id="64b0d-104">With [Azure Active Directory (Azure AD) conditional access](active-directory-conditional-access-azure-portal.md), you can fine-tune how authorized users can access your resources.</span></span> <span data-ttu-id="64b0d-105">Por exemplo, você pode limitar Olá acessem toocertain recursos tootrusted dispositivos.</span><span class="sxs-lookup"><span data-stu-id="64b0d-105">For example, you limit hello access toocertain resources tootrusted devices.</span></span> <span data-ttu-id="64b0d-106">Uma política de acesso condicional que exige um dispositivo confiável também é conhecida como política de acesso condicional com base no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="64b0d-106">A conditional access policy that requires a trusted device is also known as device-based conditional access policy.</span></span>

<span data-ttu-id="64b0d-107">Este tópico fornece informações sobre como tooconfigure condicional de dispositivos com políticas de acesso para aplicativos conectados AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="64b0d-107">This topic provides you with information on how tooconfigure device-based conditional access policies for Azure AD-connected applications.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="64b0d-108">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="64b0d-108">Before you begin</span></span>

<span data-ttu-id="64b0d-109">O acesso condicional com base no dispositivo associa o **acesso condicional do Azure AD** e o **gerenciamento de dispositivos do Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="64b0d-109">Device-based conditional access ties **Azure AD conditional access** and **Azure AD device management together**.</span></span> <span data-ttu-id="64b0d-110">Se você ainda não estiver familiarizado com uma dessas áreas, você deve ler Olá tópicos a seguir primeiro:</span><span class="sxs-lookup"><span data-stu-id="64b0d-110">If you are not familiar with one of these areas yet, you should read hello following topics, first:</span></span>

- <span data-ttu-id="64b0d-111">**[Acesso condicional no Active Directory do Azure](active-directory-conditional-access-azure-portal.md)**  -este tópico fornece uma visão geral conceitual de condicional acessar e Olá terminologia relacionada.</span><span class="sxs-lookup"><span data-stu-id="64b0d-111">**[Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)** - This topic provides you with a conceptual overview of conditional access and hello related terminology.</span></span>

- <span data-ttu-id="64b0d-112">**[Gerenciamento de toodevice de Introdução no Active Directory do Azure](device-management-introduction.md)**  -este tópico fornece uma visão geral de saudação várias opções que tooconnect dispositivos com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64b0d-112">**[Introduction toodevice management in Azure Active Directory](device-management-introduction.md)** - This topic gives you an overview of hello various options you have tooconnect devices with Azure AD.</span></span> 


## <a name="trusted-devices"></a><span data-ttu-id="64b0d-113">Dispositivos confiáveis</span><span class="sxs-lookup"><span data-stu-id="64b0d-113">Trusted devices</span></span>

<span data-ttu-id="64b0d-114">Em um mundo móveis, primeiro, a nuvem, o Active Directory do Azure permite toodevices de logon único, os aplicativos e serviços de qualquer lugar.</span><span class="sxs-lookup"><span data-stu-id="64b0d-114">In a mobile-first, cloud-first world, Azure Active Directory enables single sign-on toodevices, apps, and services from anywhere.</span></span> <span data-ttu-id="64b0d-115">Para determinados recursos no seu ambiente, concedendo acesso a usuários toohello podem não ser suficiente.</span><span class="sxs-lookup"><span data-stu-id="64b0d-115">For certain resources in your environment, granting access toohello right users might not be good enough.</span></span> <span data-ttu-id="64b0d-116">Além disso toohello usuários, você pode também requer que um dispositivo confiável toobe usado tooaccess um recurso.</span><span class="sxs-lookup"><span data-stu-id="64b0d-116">In addition toohello right users, you might also require a trusted device toobe used tooaccess a resource.</span></span> <span data-ttu-id="64b0d-117">Em seu ambiente, você pode definir que um dispositivo confiável é com base em Olá seguintes componentes:</span><span class="sxs-lookup"><span data-stu-id="64b0d-117">In your environment, you can define what a trusted device is based on hello following components:</span></span>

- <span data-ttu-id="64b0d-118">Olá [plataformas de dispositivo](active-directory-conditional-access-azure-portal.md#device-platforms) em um dispositivo</span><span class="sxs-lookup"><span data-stu-id="64b0d-118">hello [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) on a device</span></span>
- <span data-ttu-id="64b0d-119">Se um dispositivo está em conformidade</span><span class="sxs-lookup"><span data-stu-id="64b0d-119">Whether a device is compliant</span></span>
- <span data-ttu-id="64b0d-120">Se um dispositivo foi adicionado ao domínio</span><span class="sxs-lookup"><span data-stu-id="64b0d-120">Whether a device is domain-joined</span></span> 

<span data-ttu-id="64b0d-121">Olá [plataformas de dispositivo](active-directory-conditional-access-azure-portal.md#device-platforms) é caracterizado por sistema operacional Olá que está em execução no seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="64b0d-121">hello [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) is characterized by hello operating system that is running on your device.</span></span> <span data-ttu-id="64b0d-122">Em sua política de acesso condicional baseado em dispositivo, você pode limitar acesso toocertain recursos toospecific as plataformas de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="64b0d-122">In your device-based conditional access policy, you can limit access toocertain resources toospecific device platforms.</span></span>



<span data-ttu-id="64b0d-123">Em uma política de acesso condicional baseado em dispositivo, você pode exigir toobe dispositivos confiáveis marcado como compatível.</span><span class="sxs-lookup"><span data-stu-id="64b0d-123">In a device-based conditional access policy, you can require trusted devices toobe marked as compliant.</span></span>

![Aplicativos na nuvem](./media/active-directory-conditional-access-policy-connected-applications/24.png)

<span data-ttu-id="64b0d-125">Dispositivos podem ser marcados como compatível no diretório Olá por:</span><span class="sxs-lookup"><span data-stu-id="64b0d-125">Devices can be marked as compliant in hello directory by:</span></span>

- <span data-ttu-id="64b0d-126">Intune</span><span class="sxs-lookup"><span data-stu-id="64b0d-126">Intune</span></span> 
- <span data-ttu-id="64b0d-127">Um sistema de gerenciamento de dispositivo móvel de terceiros que se integre ao Azure AD</span><span class="sxs-lookup"><span data-stu-id="64b0d-127">A third-party mobile device management system that integrates with Azure AD</span></span>  

<span data-ttu-id="64b0d-128">Apenas dispositivos que estão conectado tooAzure AD podem ser marcados como compatíveis.</span><span class="sxs-lookup"><span data-stu-id="64b0d-128">Only devices that are connected tooAzure AD can be marked as compliant.</span></span> <span data-ttu-id="64b0d-129">tooconnect tooAzure um dispositivo do Active Directory, você tem Olá as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="64b0d-129">tooconnect a device tooAzure Active Directory, you have hello following options:</span></span> 

- <span data-ttu-id="64b0d-130">Registrado no Azure AD</span><span class="sxs-lookup"><span data-stu-id="64b0d-130">Azure AD registered</span></span>
- <span data-ttu-id="64b0d-131">Adicionado ao Azure AD</span><span class="sxs-lookup"><span data-stu-id="64b0d-131">Azure AD joined</span></span>
- <span data-ttu-id="64b0d-132">Adicionado ao Azure AD híbrido</span><span class="sxs-lookup"><span data-stu-id="64b0d-132">Hybrid Azure AD joined</span></span>

    ![Aplicativos na nuvem](./media/active-directory-conditional-access-policy-connected-applications/26.png)

<span data-ttu-id="64b0d-134">Se você tiver um volume de AD (Active Directory) no local, você pode considerar os dispositivos que não estão conectado tooAzure AD mas toobe tooyour unidas AD confiável.</span><span class="sxs-lookup"><span data-stu-id="64b0d-134">If you have an on-premises Active Directory (AD) footprint, you might consider devices that are not connected tooAzure AD but joined tooyour AD toobe trusted.</span></span>

![Aplicativos na nuvem](./media/active-directory-conditional-access-policy-connected-applications/25.png)


## <a name="next-steps"></a><span data-ttu-id="64b0d-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="64b0d-136">Next steps</span></span>

<span data-ttu-id="64b0d-137">Antes de configurar uma política de acesso condicional com base no dispositivo em seu ambiente, você deve dar uma olhada em Olá [as práticas recomendadas para acesso condicional no Active Directory do Azure](active-directory-conditional-access-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="64b0d-137">Before configuring a device-based conditional access policy in your environment, you should take a look at hello [best practices for conditional access in Azure Active Directory](active-directory-conditional-access-best-practices.md).</span></span>

