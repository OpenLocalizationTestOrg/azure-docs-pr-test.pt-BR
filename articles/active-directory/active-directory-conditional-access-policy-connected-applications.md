---
title: "Configurar políticas de acesso condicional com base no dispositivo do Azure Active Directory | Microsoft Docs"
description: "Saiba como configurar políticas de acesso condicional com base no dispositivo do Azure Active Directory."
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
ms.openlocfilehash: a26c40351c6b982fd90acb4bf06220ef3f79f399
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-azure-active-directory-device-based-conditional-access-policies"></a><span data-ttu-id="2b99f-103">Configurar políticas de acesso condicional com base no dispositivo do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2b99f-103">Configure Azure Active Directory device-based conditional access policies</span></span>

<span data-ttu-id="2b99f-104">Com o [acesso condicional do Azure AD (Active Directory)](active-directory-conditional-access-azure-portal.md), você pode ajustar como usuários autorizados podem acessar seus recursos.</span><span class="sxs-lookup"><span data-stu-id="2b99f-104">With [Azure Active Directory (Azure AD) conditional access](active-directory-conditional-access-azure-portal.md), you can fine-tune how authorized users can access your resources.</span></span> <span data-ttu-id="2b99f-105">Por exemplo, é possível limitar o acesso a dispositivos confiáveis para determinados recursos.</span><span class="sxs-lookup"><span data-stu-id="2b99f-105">For example, you limit the access to certain resources to trusted devices.</span></span> <span data-ttu-id="2b99f-106">Uma política de acesso condicional que exige um dispositivo confiável também é conhecida como política de acesso condicional com base no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2b99f-106">A conditional access policy that requires a trusted device is also known as device-based conditional access policy.</span></span>

<span data-ttu-id="2b99f-107">Este tópico fornece informações sobre como configurar políticas de acesso condicional com base no dispositivo para aplicativos conectados pelo Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b99f-107">This topic provides you with information on how to configure device-based conditional access policies for Azure AD-connected applications.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="2b99f-108">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="2b99f-108">Before you begin</span></span>

<span data-ttu-id="2b99f-109">O acesso condicional com base no dispositivo associa o **acesso condicional do Azure AD** e o **gerenciamento de dispositivos do Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="2b99f-109">Device-based conditional access ties **Azure AD conditional access** and **Azure AD device management together**.</span></span> <span data-ttu-id="2b99f-110">Caso ainda não esteja familiarizado com uma dessas áreas, você deverá ler os seguintes tópicos primeiro:</span><span class="sxs-lookup"><span data-stu-id="2b99f-110">If you are not familiar with one of these areas yet, you should read the following topics, first:</span></span>

- <span data-ttu-id="2b99f-111">**[Acesso condicional no Azure Active Directory](active-directory-conditional-access-azure-portal.md)** - esse tópico fornece uma visão geral conceitual do acesso condicional e da terminologia relacionada.</span><span class="sxs-lookup"><span data-stu-id="2b99f-111">**[Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)** - This topic provides you with a conceptual overview of conditional access and the related terminology.</span></span>

- <span data-ttu-id="2b99f-112">**[Introduction to device management in Azure Active Directory](device-management-introduction.md)** (Introdução ao gerenciamento de dispositivos no Azure Active Directory) - esse tópico fornece uma visão geral das várias opções para conectar dispositivos ao Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b99f-112">**[Introduction to device management in Azure Active Directory](device-management-introduction.md)** - This topic gives you an overview of the various options you have to connect devices with Azure AD.</span></span> 


## <a name="trusted-devices"></a><span data-ttu-id="2b99f-113">Dispositivos confiáveis</span><span class="sxs-lookup"><span data-stu-id="2b99f-113">Trusted devices</span></span>

<span data-ttu-id="2b99f-114">Em um mundo móvel e em nuvem, o Azure Active Directory permite o logon único para dispositivos, aplicativos e serviços de qualquer lugar.</span><span class="sxs-lookup"><span data-stu-id="2b99f-114">In a mobile-first, cloud-first world, Azure Active Directory enables single sign-on to devices, apps, and services from anywhere.</span></span> <span data-ttu-id="2b99f-115">Para determinados recursos no seu ambiente, conceder acesso aos usuários certos talvez não seja o suficiente.</span><span class="sxs-lookup"><span data-stu-id="2b99f-115">For certain resources in your environment, granting access to the right users might not be good enough.</span></span> <span data-ttu-id="2b99f-116">Além dos usuários certos, você também pode exigir que um dispositivo confiável seja usado para acessar um recurso.</span><span class="sxs-lookup"><span data-stu-id="2b99f-116">In addition to the right users, you might also require a trusted device to be used to access a resource.</span></span> <span data-ttu-id="2b99f-117">Em seu ambiente, é possível definir em que um dispositivo confiável se baseia nos seguintes componentes:</span><span class="sxs-lookup"><span data-stu-id="2b99f-117">In your environment, you can define what a trusted device is based on the following components:</span></span>

- <span data-ttu-id="2b99f-118">As [plataformas de dispositivo](active-directory-conditional-access-azure-portal.md#device-platforms) em um dispositivo</span><span class="sxs-lookup"><span data-stu-id="2b99f-118">The [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) on a device</span></span>
- <span data-ttu-id="2b99f-119">Se um dispositivo está em conformidade</span><span class="sxs-lookup"><span data-stu-id="2b99f-119">Whether a device is compliant</span></span>
- <span data-ttu-id="2b99f-120">Se um dispositivo foi adicionado ao domínio</span><span class="sxs-lookup"><span data-stu-id="2b99f-120">Whether a device is domain-joined</span></span> 

<span data-ttu-id="2b99f-121">As [plataformas de dispositivo](active-directory-conditional-access-azure-portal.md#device-platforms) são caracterizadas pelo sistema operacional que está em execução no seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2b99f-121">The [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) is characterized by the operating system that is running on your device.</span></span> <span data-ttu-id="2b99f-122">Em sua política de acesso condicional com base no dispositivo, você pode limitar o acesso para determinados recursos a plataformas de dispositivo específicas.</span><span class="sxs-lookup"><span data-stu-id="2b99f-122">In your device-based conditional access policy, you can limit access to certain resources to specific device platforms.</span></span>



<span data-ttu-id="2b99f-123">Em uma política de acesso condicional com base no dispositivo, é possível exigir que dispositivos confiáveis sejam marcados como em conformidade.</span><span class="sxs-lookup"><span data-stu-id="2b99f-123">In a device-based conditional access policy, you can require trusted devices to be marked as compliant.</span></span>

![Aplicativos na nuvem](./media/active-directory-conditional-access-policy-connected-applications/24.png)

<span data-ttu-id="2b99f-125">Os dispositivos podem ser marcados como em conformidade no diretório por um destes recursos:</span><span class="sxs-lookup"><span data-stu-id="2b99f-125">Devices can be marked as compliant in the directory by:</span></span>

- <span data-ttu-id="2b99f-126">Intune</span><span class="sxs-lookup"><span data-stu-id="2b99f-126">Intune</span></span> 
- <span data-ttu-id="2b99f-127">Um sistema de gerenciamento de dispositivo móvel de terceiros que se integre ao Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b99f-127">A third-party mobile device management system that integrates with Azure AD</span></span>  

<span data-ttu-id="2b99f-128">Somente dispositivos que são conectados ao Azure AD podem ser marcados como em conformidade.</span><span class="sxs-lookup"><span data-stu-id="2b99f-128">Only devices that are connected to Azure AD can be marked as compliant.</span></span> <span data-ttu-id="2b99f-129">Para conectar um dispositivo ao Azure Active Directory, você tem as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="2b99f-129">To connect a device to Azure Active Directory, you have the following options:</span></span> 

- <span data-ttu-id="2b99f-130">Registrado no Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b99f-130">Azure AD registered</span></span>
- <span data-ttu-id="2b99f-131">Adicionado ao Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b99f-131">Azure AD joined</span></span>
- <span data-ttu-id="2b99f-132">Adicionado ao Azure AD híbrido</span><span class="sxs-lookup"><span data-stu-id="2b99f-132">Hybrid Azure AD joined</span></span>

    ![Aplicativos na nuvem](./media/active-directory-conditional-access-policy-connected-applications/26.png)

<span data-ttu-id="2b99f-134">Se você tiver um espaço físico do AD (Active Directory) local, é possível considerar dispositivos que não estão conectados ao Azure AD, mas adicionados ao seu AD para serem confiáveis.</span><span class="sxs-lookup"><span data-stu-id="2b99f-134">If you have an on-premises Active Directory (AD) footprint, you might consider devices that are not connected to Azure AD but joined to your AD to be trusted.</span></span>

![Aplicativos na nuvem](./media/active-directory-conditional-access-policy-connected-applications/25.png)


## <a name="next-steps"></a><span data-ttu-id="2b99f-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2b99f-136">Next steps</span></span>

<span data-ttu-id="2b99f-137">Antes de configurar uma política de acesso condicional com base no dispositivo em seu ambiente, você deve dar uma olhada nas [melhores práticas para acesso condicional no Azure Active Directory](active-directory-conditional-access-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="2b99f-137">Before configuring a device-based conditional access policy in your environment, you should take a look at the [best practices for conditional access in Azure Active Directory](active-directory-conditional-access-best-practices.md).</span></span>

