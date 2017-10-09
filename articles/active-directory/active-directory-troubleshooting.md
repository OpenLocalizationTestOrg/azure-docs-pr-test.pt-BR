---
title: "Solução de problemas: O item 'Active Directory' está ausente ou não disponível | Microsoft Docs"
description: "Quais toodo quando o item de menu do Active Directory não aparece no Portal de gerenciamento de saudação."
services: active-directory
documentationcenter: na
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 3383020d-6397-43ea-b7aa-c6a9d6a1e3df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.openlocfilehash: d7355a4e39141f0b09272dc5615c309b23c8c70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-active-directory-item-is-missing-or-not-available"></a><span data-ttu-id="448d3-103">Solução de problemas: o item “Active Directory” está ausente ou não está disponível</span><span class="sxs-lookup"><span data-stu-id="448d3-103">Troubleshooting: 'Active Directory' item is missing or not available</span></span>
<span data-ttu-id="448d3-104">Muitas das instruções Olá para o uso de recursos do Active Directory do Azure e serviços começam com "Vá toohello Portal de gerenciamento do Azure e clique em **do Active Directory**."</span><span class="sxs-lookup"><span data-stu-id="448d3-104">Many of hello instructions for using Azure Active Directory features and services begin with "Go toohello Azure Management Portal and click **Active Directory**."</span></span> <span data-ttu-id="448d3-105">Mas o que fazer se o item de menu ou extensão do Active Directory Olá não aparecer ou se ele está marcado como **não disponível**?</span><span class="sxs-lookup"><span data-stu-id="448d3-105">But what do you do if hello Active Directory extension or menu item does not appear or if it is marked **Not Available**?</span></span> <span data-ttu-id="448d3-106">Este tópico é toohelp projetado.</span><span class="sxs-lookup"><span data-stu-id="448d3-106">This topic is designed toohelp.</span></span> <span data-ttu-id="448d3-107">Ele descreve as condições de saudação sob a qual **do Active Directory** não aparece ou não está disponível e explica como tooproceed.</span><span class="sxs-lookup"><span data-stu-id="448d3-107">It describes hello conditions under which **Active Directory** does not appear or is unavailable and explains how tooproceed.</span></span>

## <a name="active-directory-is-missing"></a><span data-ttu-id="448d3-108">Active Directory ausente</span><span class="sxs-lookup"><span data-stu-id="448d3-108">Active Directory is missing</span></span>
<span data-ttu-id="448d3-109">Normalmente, um **do Active Directory** item aparece no menu de navegação à esquerda de saudação.</span><span class="sxs-lookup"><span data-stu-id="448d3-109">Typically, an **Active Directory** item appears in hello left navigation menu.</span></span> <span data-ttu-id="448d3-110">instruções de Olá nos procedimentos do Azure Active Directory pressupõem que este item está no modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="448d3-110">hello instructions in Azure Active Directory procedures assume that this item is in your view.</span></span>

![Captura de tela: Active Directory no Azure](./media/active-directory-troubleshooting/typical-view.png)

<span data-ttu-id="448d3-112">o item Active Directory Olá aparece no menu de navegação à esquerda do hello quando qualquer Olá seguintes condições for verdadeira.</span><span class="sxs-lookup"><span data-stu-id="448d3-112">hello Active Directory item appears in hello left navigation menu when any of hello following conditions is true.</span></span> <span data-ttu-id="448d3-113">Caso contrário, o item de saudação não aparecerá.</span><span class="sxs-lookup"><span data-stu-id="448d3-113">Otherwise, hello item does not appear.</span></span>

* <span data-ttu-id="448d3-114">usuário atual Olá conectado com uma conta da Microsoft (anteriormente conhecida como um Windows Live ID).</span><span class="sxs-lookup"><span data-stu-id="448d3-114">hello current user signed on with a Microsoft account (formerly known as a Windows Live ID).</span></span>
  
    <span data-ttu-id="448d3-115">OU</span><span class="sxs-lookup"><span data-stu-id="448d3-115">OR</span></span>
* <span data-ttu-id="448d3-116">Olá locatário do Azure tem um diretório e conta do hello atual é um administrador de diretório.</span><span class="sxs-lookup"><span data-stu-id="448d3-116">hello Azure tenant has a directory and hello current account is a directory administrator.</span></span>
  
    <span data-ttu-id="448d3-117">OU</span><span class="sxs-lookup"><span data-stu-id="448d3-117">OR</span></span>
* <span data-ttu-id="448d3-118">Olá locatário do Azure tem pelo menos um namespace de controle de acesso do AD do Azure (ACS).</span><span class="sxs-lookup"><span data-stu-id="448d3-118">hello Azure tenant has at least one Azure AD Access Control (ACS) namespace.</span></span> <span data-ttu-id="448d3-119">Para obter mais informações, confira [Namespace de Controle de Acesso](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span><span class="sxs-lookup"><span data-stu-id="448d3-119">For more information, see [Access Control Namespace](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span></span>
  
    <span data-ttu-id="448d3-120">OU</span><span class="sxs-lookup"><span data-stu-id="448d3-120">OR</span></span>
* <span data-ttu-id="448d3-121">Olá locatário do Azure tem pelo menos um provedor de autenticação multifator do Azure.</span><span class="sxs-lookup"><span data-stu-id="448d3-121">hello Azure tenant has at least one Azure Multi-Factor Authentication provider.</span></span> <span data-ttu-id="448d3-122">Para obter mais informações, confira [Administrando Provedores do Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="448d3-122">For more information, see [Administering Azure Multi-Factor Authentication Providers](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>

<span data-ttu-id="448d3-123">toocreate um namespace de controle de acesso ou um provedor de autenticação multifator, clique em **+ novo** > **serviços de aplicativos** > **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="448d3-123">toocreate an Access Control namespace or a Multi-Factor Authentication provider, click **+New** > **App Services** > **Active Directory**.</span></span>

<span data-ttu-id="448d3-124">tooget diretório de tooa direitos administrativos, têm um administrador atribua um administrador função tooyour conta.</span><span class="sxs-lookup"><span data-stu-id="448d3-124">tooget administrative rights tooa directory, have an administrator assign an administrator role tooyour account.</span></span> <span data-ttu-id="448d3-125">Para obter detalhes, confira [Atribuindo funções de administrador](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="448d3-125">For details, see [Assigning administrator roles](active-directory-assign-admin-roles.md).</span></span>

## <a name="active-directory-is-not-available"></a><span data-ttu-id="448d3-126">Active Directory não disponível</span><span class="sxs-lookup"><span data-stu-id="448d3-126">Active Directory is not available</span></span>
<span data-ttu-id="448d3-127">Quando você clica em **+Novo** > **Serviços de Aplicativos**, um item do **Active Directory** é exibido.</span><span class="sxs-lookup"><span data-stu-id="448d3-127">When you click **+New** > **App Services**, an **Active Directory** item appears.</span></span> <span data-ttu-id="448d3-128">Especificamente, o item Active Directory Olá aparece quando qualquer um dos recursos do Active Directory hello, como diretório, controle de acesso ou provedor de autenticação multifator, são o usuário atual toohello disponíveis.</span><span class="sxs-lookup"><span data-stu-id="448d3-128">Specifically, hello Active Directory item appears when any of hello Active Directory features, such as Directory, Access Control, or Multi-Factor Auth Provider, are available toohello current user.</span></span>

<span data-ttu-id="448d3-129">No entanto, enquanto o carregamento da página hello, item Olá estiver esmaecido e está marcado como **não está disponível**.</span><span class="sxs-lookup"><span data-stu-id="448d3-129">However, while hello page is loading, hello item is dimmed and is marked **Not Available**.</span></span> <span data-ttu-id="448d3-130">Este é um estado temporário.</span><span class="sxs-lookup"><span data-stu-id="448d3-130">This is a temporary state.</span></span> <span data-ttu-id="448d3-131">Se você esperar alguns segundos, o item de saudação fica disponível.</span><span class="sxs-lookup"><span data-stu-id="448d3-131">If you wait a few seconds, hello item becomes available.</span></span> <span data-ttu-id="448d3-132">Se Olá atraso for prolongado, atualizar a página da web hello normalmente resolve o problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="448d3-132">If hello delay is prolonged, refreshing hello web page often resolves hello problem.</span></span>

![Captura de tela: Active Directory não disponível](./media/active-directory-troubleshooting/not-available.png)

