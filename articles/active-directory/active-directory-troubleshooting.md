---
title: "Solução de problemas: O item 'Active Directory' está ausente ou não disponível | Microsoft Docs"
description: "O que fazer quando o item de menu do Active Directory não aparece no Portal de Gerenciamento do Azure."
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
ms.openlocfilehash: be3a797c4a405fd2f6636e67f4c961dd6d143486
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-active-directory-item-is-missing-or-not-available"></a><span data-ttu-id="36523-103">Solução de problemas: o item “Active Directory” está ausente ou não está disponível</span><span class="sxs-lookup"><span data-stu-id="36523-103">Troubleshooting: 'Active Directory' item is missing or not available</span></span>
<span data-ttu-id="36523-104">Muitas das instruções para usar os recursos e serviços do Azure Active Directory começam com "Vá para o Portal de Gerenciamento do Azure e clique em **Active Directory**."</span><span class="sxs-lookup"><span data-stu-id="36523-104">Many of the instructions for using Azure Active Directory features and services begin with "Go to the Azure Management Portal and click **Active Directory**."</span></span> <span data-ttu-id="36523-105">Mas o que fazer se o item de menu ou extensão do Active Directory não for exibido ou se ele está marcado como **Não disponível**?</span><span class="sxs-lookup"><span data-stu-id="36523-105">But what do you do if the Active Directory extension or menu item does not appear or if it is marked **Not Available**?</span></span> <span data-ttu-id="36523-106">Este tópico foi criado para ajudar.</span><span class="sxs-lookup"><span data-stu-id="36523-106">This topic is designed to help.</span></span> <span data-ttu-id="36523-107">Ele descreve as condições sob as quais o **Active Directory** não é exibido ou não está disponível e explica como proceder.</span><span class="sxs-lookup"><span data-stu-id="36523-107">It describes the conditions under which **Active Directory** does not appear or is unavailable and explains how to proceed.</span></span>

## <a name="active-directory-is-missing"></a><span data-ttu-id="36523-108">Active Directory ausente</span><span class="sxs-lookup"><span data-stu-id="36523-108">Active Directory is missing</span></span>
<span data-ttu-id="36523-109">Normalmente, um item do **Active Directory** aparece no menu de navegação à esquerda.</span><span class="sxs-lookup"><span data-stu-id="36523-109">Typically, an **Active Directory** item appears in the left navigation menu.</span></span> <span data-ttu-id="36523-110">As instruções nos procedimentos do Active Directory do Azure pressupõem que este item está no modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="36523-110">The instructions in Azure Active Directory procedures assume that this item is in your view.</span></span>

![Captura de tela: Active Directory no Azure](./media/active-directory-troubleshooting/typical-view.png)

<span data-ttu-id="36523-112">O item Active Directory é exibido no menu de navegação à esquerda quando qualquer uma das seguintes condições for verdadeira.</span><span class="sxs-lookup"><span data-stu-id="36523-112">The Active Directory item appears in the left navigation menu when any of the following conditions is true.</span></span> <span data-ttu-id="36523-113">Caso contrário, o item não será exibido.</span><span class="sxs-lookup"><span data-stu-id="36523-113">Otherwise, the item does not appear.</span></span>

* <span data-ttu-id="36523-114">O usuário atual conectado com uma conta da Microsoft (anteriormente conhecida como uma Windows Live ID).</span><span class="sxs-lookup"><span data-stu-id="36523-114">The current user signed on with a Microsoft account (formerly known as a Windows Live ID).</span></span>
  
    <span data-ttu-id="36523-115">OU</span><span class="sxs-lookup"><span data-stu-id="36523-115">OR</span></span>
* <span data-ttu-id="36523-116">O locatário do Azure tem um diretório e a conta atual é um administrador do diretório.</span><span class="sxs-lookup"><span data-stu-id="36523-116">The Azure tenant has a directory and the current account is a directory administrator.</span></span>
  
    <span data-ttu-id="36523-117">OU</span><span class="sxs-lookup"><span data-stu-id="36523-117">OR</span></span>
* <span data-ttu-id="36523-118">O locatário do Azure tem pelo menos um namespace de Controle de Acesso do AD do Azure (ACS).</span><span class="sxs-lookup"><span data-stu-id="36523-118">The Azure tenant has at least one Azure AD Access Control (ACS) namespace.</span></span> <span data-ttu-id="36523-119">Para obter mais informações, confira [Namespace de Controle de Acesso](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span><span class="sxs-lookup"><span data-stu-id="36523-119">For more information, see [Access Control Namespace](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span></span>
  
    <span data-ttu-id="36523-120">OU</span><span class="sxs-lookup"><span data-stu-id="36523-120">OR</span></span>
* <span data-ttu-id="36523-121">O locatário do Azure tem pelo menos um provedor do Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="36523-121">The Azure tenant has at least one Azure Multi-Factor Authentication provider.</span></span> <span data-ttu-id="36523-122">Para obter mais informações, confira [Administrando Provedores do Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="36523-122">For more information, see [Administering Azure Multi-Factor Authentication Providers](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>

<span data-ttu-id="36523-123">Para criar um namespace de Controle de Acesso ou um provedor de Autenticação Multifator, clique em **+Novo** > **Serviços de Aplicativos** > **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="36523-123">To create an Access Control namespace or a Multi-Factor Authentication provider, click **+New** > **App Services** > **Active Directory**.</span></span>

<span data-ttu-id="36523-124">Para obter direitos administrativos em um diretório, peça que o administrador atribua uma função de administrador à sua conta.</span><span class="sxs-lookup"><span data-stu-id="36523-124">To get administrative rights to a directory, have an administrator assign an administrator role to your account.</span></span> <span data-ttu-id="36523-125">Para obter detalhes, confira [Atribuindo funções de administrador](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="36523-125">For details, see [Assigning administrator roles](active-directory-assign-admin-roles.md).</span></span>

## <a name="active-directory-is-not-available"></a><span data-ttu-id="36523-126">Active Directory não disponível</span><span class="sxs-lookup"><span data-stu-id="36523-126">Active Directory is not available</span></span>
<span data-ttu-id="36523-127">Quando você clica em **+Novo** > **Serviços de Aplicativos**, um item do **Active Directory** é exibido.</span><span class="sxs-lookup"><span data-stu-id="36523-127">When you click **+New** > **App Services**, an **Active Directory** item appears.</span></span> <span data-ttu-id="36523-128">Especificamente, o item Active Directory é exibido quando qualquer um dos recursos do Active Directory, como o Diretório, Controle de Acesso ou provedor do Multi-Factor Auth, estão disponíveis para o usuário atual.</span><span class="sxs-lookup"><span data-stu-id="36523-128">Specifically, the Active Directory item appears when any of the Active Directory features, such as Directory, Access Control, or Multi-Factor Auth Provider, are available to the current user.</span></span>

<span data-ttu-id="36523-129">No entanto, enquanto a página está carregando, o item fica esmaecido e é marcado como **Não Disponível**.</span><span class="sxs-lookup"><span data-stu-id="36523-129">However, while the page is loading, the item is dimmed and is marked **Not Available**.</span></span> <span data-ttu-id="36523-130">Este é um estado temporário.</span><span class="sxs-lookup"><span data-stu-id="36523-130">This is a temporary state.</span></span> <span data-ttu-id="36523-131">Se você aguardar alguns segundos, o item será disponibilizado.</span><span class="sxs-lookup"><span data-stu-id="36523-131">If you wait a few seconds, the item becomes available.</span></span> <span data-ttu-id="36523-132">Se o atraso for prolongado, atualizar a página da Web geralmente resolve o problema.</span><span class="sxs-lookup"><span data-stu-id="36523-132">If the delay is prolonged, refreshing the web page often resolves the problem.</span></span>

![Captura de tela: Active Directory não disponível](./media/active-directory-troubleshooting/not-available.png)

