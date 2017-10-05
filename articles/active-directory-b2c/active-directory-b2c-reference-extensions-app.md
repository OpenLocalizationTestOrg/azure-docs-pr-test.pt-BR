---
title: "Aplicativo de extensões – Azure AD B2C | Microsoft Docs"
description: Restaurando o b2c-extensions-app
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f0392e32-0771-473c-a799-81438ca2bcff
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/17/2017
ms.author: parja
ms.openlocfilehash: 17500b572a0e92c1c233c6967840a5b6d96e21cb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-ad-b2c-extensions-app"></a><span data-ttu-id="c1092-103">Azure AD B2C: aplicativo de extensões</span><span class="sxs-lookup"><span data-stu-id="c1092-103">Azure AD B2C: Extensions app</span></span>

<span data-ttu-id="c1092-104">Quando um diretório do Azure AD B2C é criado, um aplicativo chamado `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` é criado automaticamente no novo diretório.</span><span class="sxs-lookup"><span data-stu-id="c1092-104">When an Azure AD B2C directory is created, an app called `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` is automatically created inside the new directory.</span></span> <span data-ttu-id="c1092-105">Esse aplicativo, conhecido como **b2c-extensions-app**, está visível em *Registros de aplicativo*.</span><span class="sxs-lookup"><span data-stu-id="c1092-105">This app, referred to as the **b2c-extensions-app**, is visible in *App registrations*.</span></span> <span data-ttu-id="c1092-106">Ele é usado pelo serviço Azure AD B2C para armazenar informações sobre usuários e atributos personalizados.</span><span class="sxs-lookup"><span data-stu-id="c1092-106">It is used by the Azure AD B2C service to store information about users and custom attributes.</span></span> <span data-ttu-id="c1092-107">Se o aplicativo for excluído, o Azure AD B2C não funcionará corretamente e seu ambiente de produção será afetado.</span><span class="sxs-lookup"><span data-stu-id="c1092-107">If the app is deleted, Azure AD B2C will not function correctly and your production environment will be affected.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c1092-108">Não exclua o b2c-extensions-app, a menos que esteja planejando excluir seu locatário imediatamente.</span><span class="sxs-lookup"><span data-stu-id="c1092-108">Do not delete the b2c-extensions-app unless you are planning to immediately delete your tenant.</span></span> <span data-ttu-id="c1092-109">Se o aplicativo permanecer excluído por mais de 30 dias, as informações do usuário serão permanentemente perdidas.</span><span class="sxs-lookup"><span data-stu-id="c1092-109">If the app remains deleted for more than 30 days, user information will be permanently lost.</span></span>

## <a name="verifying-that-the-extensions-app-is-present"></a><span data-ttu-id="c1092-110">Como verificar se o aplicativo de extensões está presente</span><span class="sxs-lookup"><span data-stu-id="c1092-110">Verifying that the extensions app is present</span></span>

<span data-ttu-id="c1092-111">Para verificar se o b2c-extensions-app está presente:</span><span class="sxs-lookup"><span data-stu-id="c1092-111">To verify that the b2c-extensions-app is present:</span></span>

1. <span data-ttu-id="c1092-112">No locatário Azure AD B2C, clique em **Mais serviços** no menu de navegação à esquerda.</span><span class="sxs-lookup"><span data-stu-id="c1092-112">Inside your Azure AD B2C tenant, click on **More services** in the left-hand navigation menu.</span></span>
1. <span data-ttu-id="c1092-113">Procure e abra **Registros de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="c1092-113">Search for and open **App registrations**.</span></span>
1. <span data-ttu-id="c1092-114">Procure um aplicativo que comece com **b2c-extensions-app**</span><span class="sxs-lookup"><span data-stu-id="c1092-114">Look for an app that begins with **b2c-extensions-app**</span></span>

## <a name="recover-the-extensions-app"></a><span data-ttu-id="c1092-115">Recuperar o aplicativo de extensões</span><span class="sxs-lookup"><span data-stu-id="c1092-115">Recover the extensions app</span></span>

<span data-ttu-id="c1092-116">Se você excluiu acidentalmente o b2c-extensions-app, é possível recuperá-lo em até 30 dias.</span><span class="sxs-lookup"><span data-stu-id="c1092-116">If you accidentally deleted the b2c-extensions-app, you have 30 days to recover it.</span></span> <span data-ttu-id="c1092-117">Você pode restaurar o aplicativo usando a API do Graph:</span><span class="sxs-lookup"><span data-stu-id="c1092-117">You can restore the app using the Graph API:</span></span>

1. <span data-ttu-id="c1092-118">Navegue até [https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="c1092-118">Browse to [https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).</span></span>
1. <span data-ttu-id="c1092-119">Faça logon no site como um administrador global do diretório Azure AD B2C para o qual você quer restaurar o aplicativo excluído.</span><span class="sxs-lookup"><span data-stu-id="c1092-119">Log in to the site as a global administrator for the Azure AD B2C directory that you want to restore the deleted app for.</span></span>
1. <span data-ttu-id="c1092-120">Emita um HTTP GET em relação à URL `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` com api-version=1.6.</span><span class="sxs-lookup"><span data-stu-id="c1092-120">Issue an HTTP GET against the URL `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` with api-version=1.6.</span></span> <span data-ttu-id="c1092-121">Não se esqueça de substituir `{tenantName}` pelo nome do locatário.</span><span class="sxs-lookup"><span data-stu-id="c1092-121">Make sure to replace `{tenantName}` with your tenant name.</span></span> <span data-ttu-id="c1092-122">Essa operação listará todos os aplicativos que foram excluídos nos últimos 30 dias.</span><span class="sxs-lookup"><span data-stu-id="c1092-122">This operation will list all of the applications that have been deleted within the past 30 days.</span></span>
1. <span data-ttu-id="c1092-123">Encontre na lista o aplicativo cujo nome comece com 'b2c-extension-app' e copie seu valor de propriedade `objectid`.</span><span class="sxs-lookup"><span data-stu-id="c1092-123">Find the application in the list where the name begins with 'b2c-extension-app’ and copy its `objectid` property value.</span></span>
1. <span data-ttu-id="c1092-124">Emita um HTTP POST em relação à URL `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`.</span><span class="sxs-lookup"><span data-stu-id="c1092-124">Issue an HTTP POST against the URL `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`.</span></span> <span data-ttu-id="c1092-125">Substitua a parte `{OBJECTID}` da URL por `objectid` da etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="c1092-125">Replace the `{OBJECTID}` portion of the URL with the `objectid` from the previous step.</span></span> 

<span data-ttu-id="c1092-126">Agora, deve ser possível [ver o aplicativo restaurado](#verifying-that-the-extensions-app-is-present) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c1092-126">You should now be able to [see the restored app](#verifying-that-the-extensions-app-is-present) in the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="c1092-127">Um aplicativo só poderá ser restaurado se ele tiver sido excluído nos últimos 30 dias.</span><span class="sxs-lookup"><span data-stu-id="c1092-127">An application can only be restored if it has been deleted within the last 30 days.</span></span> <span data-ttu-id="c1092-128">Se tiverem se passado mais de 30 dias, os dados serão permanentemente perdidos.</span><span class="sxs-lookup"><span data-stu-id="c1092-128">If it has been more than 30 days, data will be permanently lost.</span></span> <span data-ttu-id="c1092-129">Para obter mais ajuda, abra um tíquete de suporte.</span><span class="sxs-lookup"><span data-stu-id="c1092-129">For more assistance, file a support ticket.</span></span>