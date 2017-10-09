---
title: "aaaConfigure autenticação e autorização para um aplicativo personalizado que chama hello Azure tempo série Insights API | Microsoft Docs"
description: "Este tutorial explica como tooconfigure autenticação e autorização para um aplicativo personalizado que chama hello Azure tempo série Insights API"
keywords: 
services: time-series-insights
documentationcenter: 
author: dmdenmsft
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/24/2017
ms.author: dmden
ms.openlocfilehash: 5043468bfc2af3c0d27e8602508d92ba2848409e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-azure-time-series-insights-api"></a><span data-ttu-id="932f7-103">Autenticação e autorização para API do Azure Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="932f7-103">Authentication and authorization for Azure Time Series Insights API</span></span>

<span data-ttu-id="932f7-104">Este artigo explica como tooconfigure um aplicativo personalizado que chama hello Azure tempo série Insights API.</span><span class="sxs-lookup"><span data-stu-id="932f7-104">This article explains how tooconfigure a custom application that calls hello Azure Time Series Insights API.</span></span>

## <a name="service-principal"></a><span data-ttu-id="932f7-105">Entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="932f7-105">Service principal</span></span>

<span data-ttu-id="932f7-106">Esta seção explica como tooconfigure tooaccess um aplicativo hello tempo série Insights API em nome do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="932f7-106">This section explains how tooconfigure an application tooaccess hello Time Series Insights API on behalf of hello application.</span></span> <span data-ttu-id="932f7-107">aplicativo Hello pode, em seguida, consultar dados ou publicar dados de referência no ambiente de informações da série de tempo Olá com as credenciais do aplicativo e não as credenciais do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="932f7-107">hello application can then query data or publish reference data in hello Time Series Insights environment with application credentials and not hello user credentials.</span></span>

<span data-ttu-id="932f7-108">Quando você tiver um aplicativo que necessite tooaccess Insights de série de tempo, você deve configurar um aplicativo do Active Directory do Azure e atribuir políticas de acesso de dados Olá no ambiente de informações da série de tempo de saudação.</span><span class="sxs-lookup"><span data-stu-id="932f7-108">When you have an application that needs tooaccess Time Series Insights, you must set up an Azure Active Directory application and assign hello data access policies in hello Time Series Insights environment.</span></span> <span data-ttu-id="932f7-109">Essa abordagem é preferível toorunning Olá aplicativo com suas próprias credenciais, porque:</span><span class="sxs-lookup"><span data-stu-id="932f7-109">This approach is preferable toorunning hello app under your own credentials because:</span></span>

* <span data-ttu-id="932f7-110">Você pode atribuir permissões de identidade de aplicativo toohello que são diferentes das suas próprias permissões.</span><span class="sxs-lookup"><span data-stu-id="932f7-110">You can assign permissions toohello app identity that are different from your own permissions.</span></span> <span data-ttu-id="932f7-111">Normalmente, essas permissões são restrito tooexactly toodo precisa de qual aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="932f7-111">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span> <span data-ttu-id="932f7-112">Por exemplo, você pode permitir Olá aplicativo tooonly ler dados em um ambiente de informações da série de tempo específico.</span><span class="sxs-lookup"><span data-stu-id="932f7-112">For example, you can allow hello app tooonly read data in a particular Time Series Insights environment.</span></span>
* <span data-ttu-id="932f7-113">Você não tem credenciais do aplicativo de saudação toochange se alterar suas responsabilidades.</span><span class="sxs-lookup"><span data-stu-id="932f7-113">You don't have toochange hello app's credentials if your responsibilities change.</span></span>
* <span data-ttu-id="932f7-114">Quando você estiver executando um script autônomo, você pode usar um certificado ou uma autenticação de chave tooautomate do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="932f7-114">You can use a certificate or an application key tooautomate authentication when you're running an unattended script.</span></span>

<span data-ttu-id="932f7-115">Este artigo mostra como tooperform aqueles percorre Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="932f7-115">This article shows you how tooperform those steps through hello Azure portal.</span></span> <span data-ttu-id="932f7-116">Ele se concentra em um aplicativo de único locatário em que o aplicativo hello é pretendido toorun em uma só organização.</span><span class="sxs-lookup"><span data-stu-id="932f7-116">It focuses on a single-tenant application where hello application is intended toorun in only one organization.</span></span> <span data-ttu-id="932f7-117">Você normalmente usa os aplicativos com um único locatário para os aplicativos da linha de negócios executados em sua organização.</span><span class="sxs-lookup"><span data-stu-id="932f7-117">You typically use single-tenant applications for line-of-business applications that run in your organization.</span></span>

<span data-ttu-id="932f7-118">fluxo de instalação Olá consiste em três etapas de alto nível:</span><span class="sxs-lookup"><span data-stu-id="932f7-118">hello setup flow consists of three high-level steps:</span></span>

1. <span data-ttu-id="932f7-119">Criar um aplicativo no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="932f7-119">Create an application in Azure Active Directory.</span></span>
2. <span data-ttu-id="932f7-120">Autorize este ambiente do aplicativo tooaccess Olá Insights de série de tempo.</span><span class="sxs-lookup"><span data-stu-id="932f7-120">Authorize this application tooaccess hello Time Series Insights environment.</span></span>
3. <span data-ttu-id="932f7-121">Usar identificação do aplicativo hello e toohello um token de chave tooacquire `"https://api.timeseries.azure.com/"` audiência ou recurso.</span><span class="sxs-lookup"><span data-stu-id="932f7-121">Use hello application ID and key tooacquire a token toohello `"https://api.timeseries.azure.com/"` audience or resource.</span></span> <span data-ttu-id="932f7-122">token Hello, em seguida, pode ser usado toocall Olá tempo série Insights API.</span><span class="sxs-lookup"><span data-stu-id="932f7-122">hello token can then be used toocall hello Time Series Insights API.</span></span>

<span data-ttu-id="932f7-123">Aqui estão as etapas detalhadas de hello:</span><span class="sxs-lookup"><span data-stu-id="932f7-123">Here are hello detailed steps:</span></span>

1. <span data-ttu-id="932f7-124">No portal do Azure de Olá, selecione **Active Directory do Azure** > **registros do aplicativo** > **novo registro de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="932f7-124">In hello Azure portal, select **Azure Active Directory** > **App registrations** > **New application registration**.</span></span>

   ![Novo registro do aplicativo no Azure Active Directory](media/authentication-and-authorization/active-directory-new-application-registration.png)  

2. <span data-ttu-id="932f7-126">Dê o aplicativo hello um toobe de tipo de nome, selecione Olá **aplicativo Web / API**, selecione qualquer URI válido para **URL de logon**e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="932f7-126">Give hello application a name, select hello type toobe **Web app / API**, select any valid URI for **Sign-on URL**, and click **Create**.</span></span>

   ![Criar o aplicativo hello no Active Directory do Azure](media/authentication-and-authorization/active-directory-create-web-api-application.png)

3. <span data-ttu-id="932f7-128">Selecione seu aplicativo recém-criado e copie seu editor de texto favorito de tooyour de ID do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="932f7-128">Select your newly created application and copy its application ID tooyour favorite text editor.</span></span>

   ![Copie a ID do aplicativo hello](media/authentication-and-authorization/active-directory-copy-application-id.png)

4. <span data-ttu-id="932f7-130">Selecione **chaves**, insira o nome da chave hello, expiração Olá select e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="932f7-130">Select **Keys**, enter hello key name, select hello expiration, and click **Save**.</span></span>

   ![Selecione as chaves do aplicativo](media/authentication-and-authorization/active-directory-application-keys.png)

   ![Insira o nome de chave de saudação e expiração e clique em Salvar](media/authentication-and-authorization/active-directory-application-keys-save.png)

5. <span data-ttu-id="932f7-133">Copie o editor de texto favorito Olá tooyour chave.</span><span class="sxs-lookup"><span data-stu-id="932f7-133">Copy hello key tooyour favorite text editor.</span></span>

   ![Copie a chave de aplicativo hello](media/authentication-and-authorization/active-directory-copy-application-key.png)

6. <span data-ttu-id="932f7-135">Para o ambiente de tempo série Insights hello, selecione **políticas de acesso de dados** e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="932f7-135">For hello Time Series Insights environment, select **Data Access Policies** and click **Add**.</span></span>

   ![Adicionar novos dados acesso política toohello Insights de série de tempo ambiente](media/authentication-and-authorization/time-series-insights-data-access-policies-add.png)

7. <span data-ttu-id="932f7-137">Em Olá **Selecionar usuário** caixa de diálogo, o nome do aplicativo hello Colar (da etapa 2) ou o ID do aplicativo (da etapa 3).</span><span class="sxs-lookup"><span data-stu-id="932f7-137">In hello **Select User** dialog box, paste hello application name (from step 2) or application ID (from step 3).</span></span>

   ![Localizar um aplicativo na caixa de diálogo Selecionar usuário Olá](media/authentication-and-authorization/time-series-insights-data-access-policies-select-user.png)

8. <span data-ttu-id="932f7-139">Função hello Select (**leitor** para consultar dados, **Colaborador** para consultar dados e alterar dados de referência) e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="932f7-139">Select hello role (**Reader** for querying data, **Contributor** for querying data and changing reference data) and click **Ok**.</span></span>

   ![Escolha o leitor ou colaborador na caixa de diálogo Selecionar função hello](media/authentication-and-authorization/time-series-insights-data-access-policies-select-role.png)

9. <span data-ttu-id="932f7-141">Salvar política Olá clicando **Okey**.</span><span class="sxs-lookup"><span data-stu-id="932f7-141">Save hello policy by clicking **Ok**.</span></span>

10. <span data-ttu-id="932f7-142">Usar Olá ID do aplicativo (da etapa 3) e o token de saudação do aplicativo tooacquire chave (da etapa 5) em nome do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="932f7-142">Use hello application ID (from step 3) and application key (from step 5) tooacquire hello token on behalf of hello application.</span></span> <span data-ttu-id="932f7-143">Olá token pode ser passado em Olá `Authorization` cabeçalho quando chamadas de aplicativo Olá Olá tempo série Insights API.</span><span class="sxs-lookup"><span data-stu-id="932f7-143">hello token can then be passed in hello `Authorization` header when hello application calls hello Time Series Insights API.</span></span>

    <span data-ttu-id="932f7-144">Se você estiver usando c#, você pode usar Olá token de saudação do código tooacquire em nome do aplicativo hello a seguir.</span><span class="sxs-lookup"><span data-stu-id="932f7-144">If you're using C#, you can use hello following code tooacquire hello token on behalf of hello application.</span></span> <span data-ttu-id="932f7-145">Para obter um exemplo completo, consulte [Consultar dados usando o C#](time-series-insights-query-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="932f7-145">For a complete sample, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

    ```csharp
    var authenticationContext = new AuthenticationContext(
        "https://login.microsoftonline.com/common",
        TokenCache.DefaultShared);

    AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
        // Set hello resource URI toohello Azure Time Series Insights API
        resource: "https://api.timeseries.azure.com/", 
        clientCredential: new ClientCredential(
            // Application ID of application registered in Azure Active Directory
            clientId: "1bc3af48-7e2f-4845-880a-c7649a6470b8", 
            // Application key of hello application that's registered in Azure Active Directory
            clientSecret: "aBcdEffs4XYxoAXzLB1n3R2meNCYdGpIGBc2YC5D6L2="));

    string accessToken = token.AccessToken;
    ```

## <a name="next-steps"></a><span data-ttu-id="932f7-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="932f7-146">Next steps</span></span>

<span data-ttu-id="932f7-147">Use o ID de aplicativo hello e a chave em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="932f7-147">Use hello application ID and key in your application.</span></span> <span data-ttu-id="932f7-148">Para exemplo de código que chama Olá tempo série Insights API, consulte [consultar dados usando o c#](time-series-insights-query-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="932f7-148">For sample code that calls hello Time Series Insights API, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="932f7-149">Consulte também</span><span class="sxs-lookup"><span data-stu-id="932f7-149">See also</span></span>

* <span data-ttu-id="932f7-150">[API de consulta](/rest/api/time-series-insights/time-series-insights-reference-queryapi) para referência de API de consulta completa Olá</span><span class="sxs-lookup"><span data-stu-id="932f7-150">[Query API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) for hello full Query API reference</span></span>
* [<span data-ttu-id="932f7-151">Criar um serviço principal no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="932f7-151">Create a service principal in hello Azure portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
