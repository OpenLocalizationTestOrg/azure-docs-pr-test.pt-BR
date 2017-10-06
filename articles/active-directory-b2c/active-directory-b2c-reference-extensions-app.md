---
title: "Aplicativo de extensões – Azure AD B2C | Microsoft Docs"
description: "Restaurando Olá b2c extensões de aplicativo"
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
ms.openlocfilehash: b36410c18314bd893dc669b49814fdcd77fae054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-extensions-app"></a><span data-ttu-id="42a7f-103">Azure AD B2C: aplicativo de extensões</span><span class="sxs-lookup"><span data-stu-id="42a7f-103">Azure AD B2C: Extensions app</span></span>

<span data-ttu-id="42a7f-104">Quando um diretório do Azure AD B2C é criado, um aplicativo chamado `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` é criado automaticamente dentro de saudação novo diretório.</span><span class="sxs-lookup"><span data-stu-id="42a7f-104">When an Azure AD B2C directory is created, an app called `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` is automatically created inside hello new directory.</span></span> <span data-ttu-id="42a7f-105">Este aplicativo, Olá chamado tooas **b2c de extensões de aplicativo**, está visível no *registros do aplicativo*.</span><span class="sxs-lookup"><span data-stu-id="42a7f-105">This app, referred tooas hello **b2c-extensions-app**, is visible in *App registrations*.</span></span> <span data-ttu-id="42a7f-106">Ele é usado por Olá informações de toostore de serviço do Azure AD B2C sobre usuários e atributos personalizados.</span><span class="sxs-lookup"><span data-stu-id="42a7f-106">It is used by hello Azure AD B2C service toostore information about users and custom attributes.</span></span> <span data-ttu-id="42a7f-107">Se o aplicativo hello for excluído, Azure AD B2C não funcionará corretamente e seu ambiente de produção será afetado.</span><span class="sxs-lookup"><span data-stu-id="42a7f-107">If hello app is deleted, Azure AD B2C will not function correctly and your production environment will be affected.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="42a7f-108">Não exclua Olá b2c extensões de aplicativo, a menos que você pretende excluir tooimmediately seu locatário.</span><span class="sxs-lookup"><span data-stu-id="42a7f-108">Do not delete hello b2c-extensions-app unless you are planning tooimmediately delete your tenant.</span></span> <span data-ttu-id="42a7f-109">Se o aplicativo hello permaneça excluído por mais de 30 dias, informações do usuário será permanentemente perdidas.</span><span class="sxs-lookup"><span data-stu-id="42a7f-109">If hello app remains deleted for more than 30 days, user information will be permanently lost.</span></span>

## <a name="verifying-that-hello-extensions-app-is-present"></a><span data-ttu-id="42a7f-110">Verificando o aplicativo hello extensões está presente</span><span class="sxs-lookup"><span data-stu-id="42a7f-110">Verifying that hello extensions app is present</span></span>

<span data-ttu-id="42a7f-111">tooverify que Olá b2c de extensões de aplicativo está presente:</span><span class="sxs-lookup"><span data-stu-id="42a7f-111">tooverify that hello b2c-extensions-app is present:</span></span>

1. <span data-ttu-id="42a7f-112">Dentro de seu locatário do Azure AD B2C, clique em **mais serviços** no menu de navegação à esquerda de saudação.</span><span class="sxs-lookup"><span data-stu-id="42a7f-112">Inside your Azure AD B2C tenant, click on **More services** in hello left-hand navigation menu.</span></span>
1. <span data-ttu-id="42a7f-113">Procure e abra **Registros de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="42a7f-113">Search for and open **App registrations**.</span></span>
1. <span data-ttu-id="42a7f-114">Procure um aplicativo que comece com **b2c-extensions-app**</span><span class="sxs-lookup"><span data-stu-id="42a7f-114">Look for an app that begins with **b2c-extensions-app**</span></span>

## <a name="recover-hello-extensions-app"></a><span data-ttu-id="42a7f-115">Recuperar o aplicativo de extensões de saudação</span><span class="sxs-lookup"><span data-stu-id="42a7f-115">Recover hello extensions app</span></span>

<span data-ttu-id="42a7f-116">Se você excluiu acidentalmente Olá b2c extensões de aplicativo, você tem 30 dias toorecovê-lo.</span><span class="sxs-lookup"><span data-stu-id="42a7f-116">If you accidentally deleted hello b2c-extensions-app, you have 30 days toorecover it.</span></span> <span data-ttu-id="42a7f-117">Você pode restaurar o aplicativo hello usando Olá API do Graph:</span><span class="sxs-lookup"><span data-stu-id="42a7f-117">You can restore hello app using hello Graph API:</span></span>

1. <span data-ttu-id="42a7f-118">Procurar muito[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="42a7f-118">Browse too[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).</span></span>
1. <span data-ttu-id="42a7f-119">Faça logon no site toohello como um administrador global para o diretório do Azure AD B2C Olá que você deseja toorestore Olá excluído aplicativo para.</span><span class="sxs-lookup"><span data-stu-id="42a7f-119">Log in toohello site as a global administrator for hello Azure AD B2C directory that you want toorestore hello deleted app for.</span></span>
1. <span data-ttu-id="42a7f-120">Emitir um HTTP GET em relação a URL de saudação `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` com api-version = 1.6.</span><span class="sxs-lookup"><span data-stu-id="42a7f-120">Issue an HTTP GET against hello URL `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` with api-version=1.6.</span></span> <span data-ttu-id="42a7f-121">Certifique-se de que tooreplace `{tenantName}` com o nome do locatário.</span><span class="sxs-lookup"><span data-stu-id="42a7f-121">Make sure tooreplace `{tenantName}` with your tenant name.</span></span> <span data-ttu-id="42a7f-122">Esta operação irá listar todos os aplicativos de saudação que tenham sido excluídos no hello últimos 30 dias.</span><span class="sxs-lookup"><span data-stu-id="42a7f-122">This operation will list all of hello applications that have been deleted within hello past 30 days.</span></span>
1. <span data-ttu-id="42a7f-123">Encontre o aplicativo hello na lista de saudação onde nome hello começa com 'aplicativo de extensão b2c' e copie seu `objectid` o valor da propriedade.</span><span class="sxs-lookup"><span data-stu-id="42a7f-123">Find hello application in hello list where hello name begins with 'b2c-extension-app’ and copy its `objectid` property value.</span></span>
1. <span data-ttu-id="42a7f-124">Emitir um HTTP POST com relação à URL Olá `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`.</span><span class="sxs-lookup"><span data-stu-id="42a7f-124">Issue an HTTP POST against hello URL `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`.</span></span> <span data-ttu-id="42a7f-125">Substituir saudação `{OBJECTID}` parte da URL Olá Olá `objectid` da etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="42a7f-125">Replace hello `{OBJECTID}` portion of hello URL with hello `objectid` from hello previous step.</span></span> 

<span data-ttu-id="42a7f-126">Você poderá muito[consulte aplicativo hello restaurado](#verifying-that-the-extensions-app-is-present) em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="42a7f-126">You should now be able too[see hello restored app](#verifying-that-the-extensions-app-is-present) in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="42a7f-127">Um aplicativo só pode ser restaurado se ele foi excluído no hello últimos 30 dias.</span><span class="sxs-lookup"><span data-stu-id="42a7f-127">An application can only be restored if it has been deleted within hello last 30 days.</span></span> <span data-ttu-id="42a7f-128">Se tiverem se passado mais de 30 dias, os dados serão permanentemente perdidos.</span><span class="sxs-lookup"><span data-stu-id="42a7f-128">If it has been more than 30 days, data will be permanently lost.</span></span> <span data-ttu-id="42a7f-129">Para obter mais ajuda, abra um tíquete de suporte.</span><span class="sxs-lookup"><span data-stu-id="42a7f-129">For more assistance, file a support ticket.</span></span>
