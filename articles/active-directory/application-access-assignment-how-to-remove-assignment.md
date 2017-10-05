---
title: "Como remover o acesso de um usuário a um aplicativo | Microsoft Docs"
description: "Compreenda como remover o acesso de um usuário a um aplicativo"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 497429e7bf62f7e1d67ea429d6b858725f843688
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-remove-a-users-access-to-an-application"></a><span data-ttu-id="58cb4-103">Como remover o acesso de um usuário a um aplicativo</span><span class="sxs-lookup"><span data-stu-id="58cb4-103">How to remove a user's access to an application</span></span>

<span data-ttu-id="58cb4-104">Este artigo o ajudará a compreender como remover o acesso de um usuário a um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="58cb4-104">This article help you to understand how to remove a user's access to an application.</span></span>

## <a name="i-want-to-remove-a-specific-users-or-groups-assignment-to-an-application"></a><span data-ttu-id="58cb4-105">Quero remover a atribuição de um usuário ou grupo específico a um aplicativo</span><span class="sxs-lookup"><span data-stu-id="58cb4-105">I want to remove a specific user’s or group’s assignment to an application</span></span>

<span data-ttu-id="58cb4-106">Para remover uma atribuição de um usuário ou grupo a um aplicativo, siga as etapas listadas no artigo [Remover uma atribuição de usuário ou grupo de um aplicativo empresarial no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="58cb4-106">To remove a user or group assignment to an application, follow the steps listed in the [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

<span data-ttu-id="58cb4-107">.## Quero desabilitar todo o acesso a um aplicativo para todos os usuários</span><span class="sxs-lookup"><span data-stu-id="58cb4-107">.## I want to disable all access to an application for every user</span></span>

<span data-ttu-id="58cb4-108">Para desabilitar todos os logons de usuário em um aplicativo, siga as etapas listadas no artigo [Desabilitar logons de usuário para um aplicativo empresarial no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="58cb4-108">To disable all user sign-ins to an application, follow the steps listed in the [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-to-delete-an-application-entirely"></a><span data-ttu-id="58cb4-109">Quero excluir um aplicativo completamente</span><span class="sxs-lookup"><span data-stu-id="58cb4-109">I want to delete an application entirely</span></span>

<span data-ttu-id="58cb4-110">Para **excluir um aplicativo**, siga as instruções abaixo:</span><span class="sxs-lookup"><span data-stu-id="58cb4-110">To **delete an application**, follow the instructions below:</span></span>

1.  <span data-ttu-id="58cb4-111">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="58cb4-111">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="58cb4-112">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="58cb4-112">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="58cb4-113">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="58cb4-113">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="58cb4-114">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="58cb4-114">Click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="58cb4-115">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="58cb4-115">Click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="58cb4-116">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="58cb4-116">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="58cb4-117">Selecione o aplicativo que deseja excluir.</span><span class="sxs-lookup"><span data-stu-id="58cb4-117">Select the application you want to delete.</span></span>

7.  <span data-ttu-id="58cb4-118">Após o aplicativo ser carregado, clique no ícone **Excluir** na folha **Visão Geral** superior do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="58cb4-118">Once the application loads, click **Delete** icon from the top application’s **Overview** blade.</span></span>

## <a name="i-want-to-disable-all-future-user-consent-operations-to-any-application"></a><span data-ttu-id="58cb4-119">Quero desabilitar todas as futuras operações de consentimento do usuário para qualquer aplicativo</span><span class="sxs-lookup"><span data-stu-id="58cb4-119">I want to disable all future user consent operations to any application</span></span>

<span data-ttu-id="58cb4-120">Desabilitar o consentimento do usuário para todo o seu diretório impede que os usuários finais consintam com qualquer aplicativo.</span><span class="sxs-lookup"><span data-stu-id="58cb4-120">Disabling user consent for your entire directory prevent end users from consenting to any application.</span></span> <span data-ttu-id="58cb4-121">Os administradores ainda podem consentir em nome dos usuários.</span><span class="sxs-lookup"><span data-stu-id="58cb4-121">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="58cb4-122">Para saber mais sobre o consentimento de aplicativos e por que você pode ou não querer fazer isso, leia [Entendendo o consentimento do usuário e do administrador](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span><span class="sxs-lookup"><span data-stu-id="58cb4-122">To learn more about application consent, and why you may or may not wish to do this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="58cb4-123">Para **desabilitar todas as futuras operações de consentimento do usuário no diretório inteiro**, siga as instruções abaixo:</span><span class="sxs-lookup"><span data-stu-id="58cb4-123">To **disable all future user consent operations in your entire directory**, follow the instructions below:</span></span>

1.  <span data-ttu-id="58cb4-124">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="58cb4-124">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="58cb4-125">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="58cb4-125">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="58cb4-126">Digite **"Azure Active Directory**" na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="58cb4-126">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="58cb4-127">Clique em **Usuários e grupos** no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="58cb4-127">Click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="58cb4-128">Clique em **Configurações de usuário**.</span><span class="sxs-lookup"><span data-stu-id="58cb4-128">Click **User settings**.</span></span>

6.  <span data-ttu-id="58cb4-129">Desabilite todas as futuras operações de consentimento do usuário definindo o controle de alternância **Os usuários podem permitir que os aplicativos acessem seus dados** como **Não** e clique no botão **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="58cb4-129">Disable all future user consent operations by setting the **Users can allow apps to access their data** toggle to **No** and click the **Save** button.</span></span>


# <a name="next-steps"></a><span data-ttu-id="58cb4-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="58cb4-130">Next steps</span></span>
[<span data-ttu-id="58cb4-131">Gerenciamento do acesso aos aplicativos</span><span class="sxs-lookup"><span data-stu-id="58cb4-131">Managing access to apps</span></span>](active-directory-managing-access-to-apps.md)
