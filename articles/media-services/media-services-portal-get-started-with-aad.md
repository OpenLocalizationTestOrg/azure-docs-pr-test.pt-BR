---
title: "aaaGet iniciado com a autenticação do AD do Azure usando Olá portal do Azure | Microsoft Docs"
description: "Saiba como toouse hello Azure tooaccess portal do Azure Active Directory (AD do Azure) autenticação tooconsume Olá API de serviços de mídia do Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 497ad1806b3fd1262802adefb6e12b65ee9f2d61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-ad-authentication-by-using-hello-azure-portal"></a><span data-ttu-id="7ffd5-103">Introdução à autenticação do AD do Azure usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7ffd5-103">Get started with Azure AD authentication by using hello Azure portal</span></span>

<span data-ttu-id="7ffd5-104">Saiba como toouse hello Azure tooaccess portal do Azure Active Directory (AD do Azure) autenticação tooaccess Olá API de serviços de mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-104">Learn how toouse hello Azure portal tooaccess Azure Active Directory (Azure AD) authentication tooaccess hello Azure Media Services API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ffd5-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7ffd5-105">Prerequisites</span></span>

- <span data-ttu-id="7ffd5-106">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-106">An Azure account.</span></span> <span data-ttu-id="7ffd5-107">Se você não tiver uma conta, comece com uma [avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7ffd5-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="7ffd5-108">Uma conta dos Serviços de Mídia.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-108">A Media Services account.</span></span> <span data-ttu-id="7ffd5-109">Para obter mais informações, consulte [criar uma conta de serviços de mídia do Azure usando o portal do Azure de saudação](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="7ffd5-109">For more information, see [Create an Azure Media Services account by using hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="7ffd5-110">Certifique-se de examinar Olá [acessar API do Azure Media Services visão geral de autenticação do AD do Azure](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="7ffd5-110">Make sure you review hello [Accessing Azure Media Services API with Azure AD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="7ffd5-111">Quando você usar a autenticação do AD Azure com Serviços de Mídia do Azure haverá duas opções de autenticação:</span><span class="sxs-lookup"><span data-stu-id="7ffd5-111">When you use Azure AD authentication with Azure Media Services, you have two authentication options:</span></span>

- <span data-ttu-id="7ffd5-112">**Autenticação de usuário**.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-112">**User authentication**.</span></span> <span data-ttu-id="7ffd5-113">Autentica um usuário que está usando Olá aplicativo toointeract com recursos de serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-113">Authenticate a person who is using hello app toointeract with Media Services resources.</span></span> <span data-ttu-id="7ffd5-114">aplicativo interativo do Hello primeiro deve solicitar credenciais ao usuário Olá.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-114">hello interactive application should first prompt hello user for credentials.</span></span> <span data-ttu-id="7ffd5-115">Um exemplo é um aplicativo de console de gerenciamento usado por trabalhos de codificação de toomonitor de usuários autorizados ou transmissão ao vivo.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-115">An example is a management console app used by authorized users toomonitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="7ffd5-116">**Autenticação de entidade de serviço**.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-116">**Service principal authentication**.</span></span> <span data-ttu-id="7ffd5-117">Autentica um serviço.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-117">Authenticate a service.</span></span> <span data-ttu-id="7ffd5-118">Os aplicativos que geralmente usam esse método de autenticação são aplicativos que executam serviços de daemon, serviços de camada intermediária ou trabalhos agendados: aplicativos Web, aplicativos de funções, aplicativos lógicos, APIs ou um microsserviço.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs: web apps, function apps, logic apps, APIs, or a microservice.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7ffd5-119">Atualmente, os serviços de mídia oferece suporte a modelo de autenticação de serviço de controle de acesso do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-119">Currently, Media Services supports hello Azure Access Control service authentication model.</span></span> <span data-ttu-id="7ffd5-120">No entanto, a autorização de Controle de Acesso será preterida em 1º de junho de 2018.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-120">However, Access Control authorization will be deprecated on June 1, 2018.</span></span> <span data-ttu-id="7ffd5-121">É recomendável que você migre o modelo de autenticação toohello AD do Azure assim que possível.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-121">We recommend that you migrate toohello Azure AD authentication model as soon as possible.</span></span>

## <a name="select-hello-authentication-method"></a><span data-ttu-id="7ffd5-122">Selecionar método de autenticação de saudação</span><span class="sxs-lookup"><span data-stu-id="7ffd5-122">Select hello authentication method</span></span>

1. <span data-ttu-id="7ffd5-123">Em Olá [portal do Azure](https://portal.azure.com/), selecione sua conta de serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-123">In hello [Azure portal](https://portal.azure.com/), select your Media Services account.</span></span>
2. <span data-ttu-id="7ffd5-124">Selecione como tooconnect toohello API de serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-124">Select how tooconnect toohello Media Services API.</span></span>

    ![Selecione a página do método de conexão](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started01.png)

## <a name="user-authentication"></a><span data-ttu-id="7ffd5-126">Autenticação de usuário</span><span class="sxs-lookup"><span data-stu-id="7ffd5-126">User authentication</span></span>

<span data-ttu-id="7ffd5-127">tooconnect toohello API de serviços de mídia usando Olá a opção de autenticação de usuário, aplicativo de cliente Olá precisa toorequest um token do AD do Azure que tem Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="7ffd5-127">tooconnect toohello Media Services API by using hello user authentication option, hello client app needs toorequest an Azure AD token that has hello following parameters:</span></span>  

* <span data-ttu-id="7ffd5-128">Ponto de extremidade de locatário do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ffd5-128">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="7ffd5-129">URI de recursos dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="7ffd5-129">Media Services resource URI</span></span>
* <span data-ttu-id="7ffd5-130">ID do cliente do aplicativo (nativo) dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="7ffd5-130">Media Services (native) application client ID</span></span> 
* <span data-ttu-id="7ffd5-131">URI de redirecionamento do aplicativo (nativo) dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="7ffd5-131">Media Services (native) application redirect URI</span></span> 
* <span data-ttu-id="7ffd5-132">URI de recurso dos Serviços de Mídia REST</span><span class="sxs-lookup"><span data-stu-id="7ffd5-132">Resource URI for REST Media Services</span></span>

<span data-ttu-id="7ffd5-133">Você pode obter valores de saudação para esses parâmetros no hello **API de serviços de mídia com a autenticação do usuário** página.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-133">You can get hello values for these parameters on hello **Media Services API with user authentication** page.</span></span> 

![Conecte-se com a página de autenticação de usuário](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started02.png)

<span data-ttu-id="7ffd5-135">Se você conectar toohello API de serviços de mídia usando Olá SDK do Media Services Microsoft .NET, Olá necessário valores são tooyou disponível como parte da saudação SDK.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-135">If you connect toohello Media Services API by using hello Media Services Microsoft .NET SDK, hello required values are available tooyou as part of hello SDK.</span></span> <span data-ttu-id="7ffd5-136">Para obter mais informações, consulte [tooaccess de autenticação de uso do AD do Azure Olá API de serviços de mídia do Azure com o .NET](media-services-dotnet-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="7ffd5-136">For more information, see [Use Azure AD authentication tooaccess hello Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="7ffd5-137">Se você não estiver usando o SDK de cliente .NET de serviços de mídia Olá, você deve criar manualmente uma solicitação de token do AD do Azure usando os parâmetros de saudação discutidos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-137">If you're not using hello Media Services .NET client SDK, you must manually create an Azure AD token request by using hello parameters discussed earlier.</span></span> <span data-ttu-id="7ffd5-138">Para obter mais informações, consulte [como tooget de biblioteca de autenticação de saudação do AD do Azure toouse Olá token do AD do Azure](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="7ffd5-138">For more information, see [How toouse hello Azure AD Authentication Library tooget hello Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

## <a name="service-principal-authentication"></a><span data-ttu-id="7ffd5-139">Autenticação de entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="7ffd5-139">Service principal authentication</span></span>

<span data-ttu-id="7ffd5-140">tooconnect toohello API de serviços de mídia usando Olá opção principal do serviço, seu aplicativo de camada intermediária (API da web ou aplicativo web) precisa toorequest um token do AD do Azure que tem Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="7ffd5-140">tooconnect toohello Media Services API by using hello service principal option, your middle-tier app (web API or web application) needs toorequest an Azure AD token that has hello following parameters:</span></span>  

* <span data-ttu-id="7ffd5-141">Ponto de extremidade de locatário do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ffd5-141">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="7ffd5-142">URI de recursos dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="7ffd5-142">Media Services resource URI</span></span> 
* <span data-ttu-id="7ffd5-143">URI de recurso dos Serviços de Mídia REST</span><span class="sxs-lookup"><span data-stu-id="7ffd5-143">Resource URI for REST Media Services</span></span>
* <span data-ttu-id="7ffd5-144">Valores de aplicativo do Azure AD: Olá **ID do cliente** e **segredo do cliente**</span><span class="sxs-lookup"><span data-stu-id="7ffd5-144">Azure AD application values: hello **client ID** and **client secret**</span></span>

<span data-ttu-id="7ffd5-145">Você pode obter valores de saudação para esses parâmetros no hello **conectar tooMedia API de serviços com a entidade de serviço** página.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-145">You can get hello values for these parameters on hello **Connect tooMedia Services API with service principal** page.</span></span> <span data-ttu-id="7ffd5-146">Use este toocreate página Azure um novo aplicativo do AD ou tooselect um existente.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-146">Use this page toocreate a new Azure AD application or tooselect an existing one.</span></span> <span data-ttu-id="7ffd5-147">Depois de selecionar o aplicativo do Azure AD Olá, você pode obter ID saudação do cliente (ID do aplicativo) e gerar valores de segredo (chave) de cliente hello.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-147">After you select hello Azure AD app, you can get hello client ID (Application ID) and generate hello client secret (key) values.</span></span> 

![Conecte-se com a página da entidade de serviço](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started04.png)

<span data-ttu-id="7ffd5-149">Olá quando **entidade de serviço** folha é aberto, o aplicativo do Azure AD de primeiro hello que atenda aos critérios a seguir de saudação é selecionado:</span><span class="sxs-lookup"><span data-stu-id="7ffd5-149">When hello **Service Principal** blade opens, hello first Azure AD application that meets hello following criteria is selected:</span></span>

- <span data-ttu-id="7ffd5-150">Trata-se de um aplicativo do AD Azure registrado.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-150">It is a registered Azure AD application.</span></span>
- <span data-ttu-id="7ffd5-151">Ele tem permissões de Colaborador ou controle de acesso de Owner Role-Based na conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-151">It has Contributor or Owner Role-Based Access Control permissions on hello account.</span></span>

<span data-ttu-id="7ffd5-152">Depois de criar ou selecionar um aplicativo do AD do Azure, você pode criar e copiar um segredo do cliente (chave) e Olá ID do cliente (ID do aplicativo).</span><span class="sxs-lookup"><span data-stu-id="7ffd5-152">After you create or select an Azure AD app, you can create and copy a client secret (key) and hello client ID (Application ID).</span></span> <span data-ttu-id="7ffd5-153">ID do cliente e o segredo do cliente Olá são token de acesso de saudação tooget necessário nesse cenário.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-153">hello client secret and client ID are required tooget hello access token in this scenario.</span></span>

<span data-ttu-id="7ffd5-154">Se você não tiver permissões toocreate AD do Azure aplicativos em seu domínio, controles de aplicativo do AD do Azure Olá da folha de saudação não são mostrados, e uma mensagem de aviso é exibida.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-154">If you don't have permissions toocreate Azure AD apps in your domain, hello Azure AD app controls of hello blade are not shown, and a warning message is displayed.</span></span>

<span data-ttu-id="7ffd5-155">Se você conectar toohello API de serviços de mídia usando o SDK do Media Services .NET de hello, consulte [tooaccess de autenticação de uso do AD do Azure Olá API de serviços de mídia do Azure com o .NET](media-services-dotnet-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="7ffd5-155">If you connect toohello Media Services API by using hello Media Services .NET SDK, see [Use Azure AD authentication tooaccess hello Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="7ffd5-156">Se você não estiver usando o SDK de cliente .NET de serviços de mídia hello, você deve criar manualmente uma solicitação de token do AD do Azure usando os parâmetros de saudação discutidos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-156">If you are not using hello Media Services .NET client SDK, you must manually create an Azure AD token request using hello parameters discussed earlier.</span></span> <span data-ttu-id="7ffd5-157">Para obter mais informações, consulte [como tooget de biblioteca de autenticação de saudação do AD do Azure toouse Olá token do AD do Azure](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="7ffd5-157">For more information, see [How toouse hello Azure AD Authentication Library tooget hello Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

### <a name="get-hello-client-id-and-client-secret"></a><span data-ttu-id="7ffd5-158">Obter segredo do cliente e a ID de cliente de saudação</span><span class="sxs-lookup"><span data-stu-id="7ffd5-158">Get hello client ID and client secret</span></span>

<span data-ttu-id="7ffd5-159">Depois de selecionar um aplicativo AD do Azure existente ou selecione Olá opção toocreate um novo, Olá botões a seguir são exibidos:</span><span class="sxs-lookup"><span data-stu-id="7ffd5-159">After you select an existing Azure AD app or select hello option toocreate a new one, hello following buttons appear:</span></span>

![Botão de gerenciar permissões e botão de gerenciar aplicativo](./media/media-services-portal-get-started-with-aad/media-services-portal-manage.png)

<span data-ttu-id="7ffd5-161">Olá tooopen folha de aplicativo do AD do Azure, clique em **gerenciar aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-161">tooopen hello Azure AD application blade, click **Manage application**.</span></span> <span data-ttu-id="7ffd5-162">Em Olá **gerenciar aplicativo** folha, você pode obter a ID do cliente do aplicativo hello (ID do aplicativo).</span><span class="sxs-lookup"><span data-stu-id="7ffd5-162">On hello **Manage application** blade, you can get hello app's client ID (Application ID).</span></span> <span data-ttu-id="7ffd5-163">toogenerate um segredo do cliente (chave), selecione **chaves**.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-163">toogenerate a client secret (key), select **Keys**.</span></span>

![Gerenciar a opção Chaves da folha do aplicativo](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started06.png) 

### <a name="manage-permissions-and-hello-application"></a><span data-ttu-id="7ffd5-165">Gerenciar permissões e o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="7ffd5-165">Manage permissions and hello application</span></span>

<span data-ttu-id="7ffd5-166">Depois de selecionar o aplicativo do AD do Azure hello, você pode gerenciar permissões e o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-166">After you select hello Azure AD application, you can manage hello application and permissions.</span></span> <span data-ttu-id="7ffd5-167">tooset a sua tooaccess de aplicativo do AD do Azure outros aplicativos, clique em **gerenciar permissões**.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-167">tooset up your Azure AD application tooaccess other applications, click **Manage permissions**.</span></span> <span data-ttu-id="7ffd5-168">Para tarefas de gerenciamento, como alterar as chaves e as URLs de resposta ou manifesto do aplicativo do tooedit Olá, clique em **gerenciar aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-168">For management tasks, such as changing keys and reply URLs, or tooedit hello application’s manifest, click **Manage application**.</span></span>

### <a name="edit-hello-apps-settings-or-manifest"></a><span data-ttu-id="7ffd5-169">Editar configurações do aplicativo hello ou manifesto</span><span class="sxs-lookup"><span data-stu-id="7ffd5-169">Edit hello app's settings or manifest</span></span>

<span data-ttu-id="7ffd5-170">configurações do aplicativo do tooedit hello ou o manifesto, clique em **gerenciar aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="7ffd5-170">tooedit hello app's settings or manifest, click **Manage application**.</span></span>

![Gerenciar a página do aplicativo](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started05.png)

## <a name="next-steps"></a><span data-ttu-id="7ffd5-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7ffd5-172">Next steps</span></span>

<span data-ttu-id="7ffd5-173">Introdução ao [carregando arquivos tooyour conta](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="7ffd5-173">Get started with [uploading files tooyour account](media-services-portal-upload-files.md).</span></span>
