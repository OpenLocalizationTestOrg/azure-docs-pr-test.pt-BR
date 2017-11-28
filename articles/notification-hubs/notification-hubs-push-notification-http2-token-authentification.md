---
title: "Autenticação baseada em token (HTTP/2) para o APNS em Hubs de Notificação do Azure | Microsoft Docs"
description: "Este tópico explica como aproveitar a nova autenticação de token para o APNS"
services: notification-hubs
documentationcenter: .net
author: kpiteira
manager: erikre
editor: 
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 05/17/2017
ms.author: kapiteir
ms.openlocfilehash: 5a21bcd9f12fc3f96b17a556ba15526c35ababe2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="token-based-http2-authentication-for-apns"></a><span data-ttu-id="63a47-103">Autenticação baseada em token (HTTP/2) para o APNS</span><span class="sxs-lookup"><span data-stu-id="63a47-103">Token-based (HTTP/2) Authentication for APNS</span></span>
## <a name="overview"></a><span data-ttu-id="63a47-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="63a47-104">Overview</span></span>
<span data-ttu-id="63a47-105">Este artigo fornece detalhes sobre como usar o novo protocolo HTTP/2 do APNS com autenticação baseada em token.</span><span class="sxs-lookup"><span data-stu-id="63a47-105">This article details how to use the new APNS HTTP/2 protocol with token based authentication.</span></span>

<span data-ttu-id="63a47-106">Os principais benefícios de usar o novo protocolo incluem:</span><span class="sxs-lookup"><span data-stu-id="63a47-106">The key benefits of using the new protocol include:</span></span>
-   <span data-ttu-id="63a47-107">A geração de token é relativamente sem complicações (em comparação com certificados)</span><span class="sxs-lookup"><span data-stu-id="63a47-107">Token generation is relatively hassle free (compared to certificates)</span></span>
-   <span data-ttu-id="63a47-108">Não há mais dadas de expiração – você está no controle dos seus tokens de autenticação e sua revogação</span><span class="sxs-lookup"><span data-stu-id="63a47-108">No more expiry dates – you are in control of your authentication tokens and their revocation</span></span>
-   <span data-ttu-id="63a47-109">O conteúdo agora pode ser de até 4 KB</span><span class="sxs-lookup"><span data-stu-id="63a47-109">Payloads can now be up to 4 KB</span></span>
- <span data-ttu-id="63a47-110">Comentários síncronos</span><span class="sxs-lookup"><span data-stu-id="63a47-110">Synchronous feedback</span></span>
-   <span data-ttu-id="63a47-111">Você está usando o protocolo mais recente da Apple – os certificados ainda usam o protocolo binário, que está marcado para substituição</span><span class="sxs-lookup"><span data-stu-id="63a47-111">You’re on Apple’s latest protocol – certificates still use the binary protocol, which is marked for deprecation</span></span>

<span data-ttu-id="63a47-112">O uso desse novo mecanismo pode ser feito em duas etapas, em alguns minutos:</span><span class="sxs-lookup"><span data-stu-id="63a47-112">Using this new mechanism can be done in two steps in a few minutes:</span></span>
1.  <span data-ttu-id="63a47-113">Obtenha as informações necessárias do portal da Conta de Desenvolvedor da Apple</span><span class="sxs-lookup"><span data-stu-id="63a47-113">Obtain the necessary information from the Apple Developer Account portal</span></span>
2.  <span data-ttu-id="63a47-114">Configure seu hub de notificações com as novas informações</span><span class="sxs-lookup"><span data-stu-id="63a47-114">Configure your notification hub with the new information</span></span>

<span data-ttu-id="63a47-115">Os Hubs de Notificação agora estão configurados para usar o novo sistema de autenticação com APNS.</span><span class="sxs-lookup"><span data-stu-id="63a47-115">Notification Hubs is now all set to use the new authentication system with APNS.</span></span> 

<span data-ttu-id="63a47-116">Observe que se você migrou usando as credenciais de certificado para APNS:</span><span class="sxs-lookup"><span data-stu-id="63a47-116">Note that if you migrated from using certificate credentials for APNS:</span></span>
- <span data-ttu-id="63a47-117">as propriedades de token substituem o certificado em nosso sistema,</span><span class="sxs-lookup"><span data-stu-id="63a47-117">the token properties overwrite your certificate in our system,</span></span>
- <span data-ttu-id="63a47-118">mas o aplicativo continua a receber notificações perfeitamente.</span><span class="sxs-lookup"><span data-stu-id="63a47-118">but your application continues to receive notifications seamlessly.</span></span>

## <a name="obtaining-authentication-information-from-apple"></a><span data-ttu-id="63a47-119">Obtendo informações de autenticação da Apple</span><span class="sxs-lookup"><span data-stu-id="63a47-119">Obtaining authentication information from Apple</span></span>
<span data-ttu-id="63a47-120">Para habilitar a autenticação baseada em token, você precisará das seguintes propriedades da Conta de Desenvolvedor da Apple:</span><span class="sxs-lookup"><span data-stu-id="63a47-120">To enable token-based authentication, you need the following properties from your Apple Developer Account:</span></span>
### <a name="key-identifier"></a><span data-ttu-id="63a47-121">Identificador de chave</span><span class="sxs-lookup"><span data-stu-id="63a47-121">Key Identifier</span></span>
<span data-ttu-id="63a47-122">O identificador de chave pode ser obtido na página "Chaves" em sua Conta de Desenvolvedor da Apple</span><span class="sxs-lookup"><span data-stu-id="63a47-122">The key identifier can be obtained from the "Keys" page in your Apple Developer Account</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a><span data-ttu-id="63a47-123">Identificador do aplicativo e nome do aplicativo</span><span class="sxs-lookup"><span data-stu-id="63a47-123">Application Identifier & Application Name</span></span>
<span data-ttu-id="63a47-124">O nome do aplicativo está disponível por meio da página de IDs de Aplicativo na Conta de Desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="63a47-124">The application name is available via the App IDs page in the Developer Account.</span></span> 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

<span data-ttu-id="63a47-125">O identificador do aplicativo está disponível por meio da página de detalhes da associação na Conta de Desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="63a47-125">The application identifier is available via the membership details page in the Developer Account.</span></span>
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a><span data-ttu-id="63a47-126">Token de autenticação</span><span class="sxs-lookup"><span data-stu-id="63a47-126">Authentication token</span></span>
<span data-ttu-id="63a47-127">O token de autenticação pode ser baixado depois de gerar um token para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="63a47-127">The authentication token can be downloaded after you generate a token for your application.</span></span> <span data-ttu-id="63a47-128">Para obter detalhes sobre como gerar esse token, consulte a [documentação do Desenvolvedor da Apple](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span><span class="sxs-lookup"><span data-stu-id="63a47-128">For details on how to generate this token, refer to [Apple’s Developer documentation](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span></span>

## <a name="configuring-your-notification-hub-to-use-token-based-authentication"></a><span data-ttu-id="63a47-129">Configurando seu hub de notificações para usar a autenticação baseada em token</span><span class="sxs-lookup"><span data-stu-id="63a47-129">Configuring your notification hub to use token-based authentication</span></span>
### <a name="configure-via-the-azure-portal"></a><span data-ttu-id="63a47-130">Configurar por meio do Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="63a47-130">Configure via the Azure portal</span></span>
<span data-ttu-id="63a47-131">Para habilitar a autenticação baseada em token no portal, faça logon no Portal do Azure e vá para o painel Hub de Notificações > Serviços de Notificação > APNS.</span><span class="sxs-lookup"><span data-stu-id="63a47-131">To enable token based authentication in the portal, log in to the Azure portal and go to your Notification Hub > Notification Services > APNS panel.</span></span> 

<span data-ttu-id="63a47-132">Há uma nova propriedade – *Modo de Autenticação*.</span><span class="sxs-lookup"><span data-stu-id="63a47-132">There is a new property – *Authentication Mode*.</span></span> <span data-ttu-id="63a47-133">Selecionar Token permite que você atualize seu hub com todas as propriedades relevantes de token.</span><span class="sxs-lookup"><span data-stu-id="63a47-133">Selecting Token allows you to update your hub with all the relevant token properties.</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- <span data-ttu-id="63a47-134">Insira as propriedades que você recuperou da sua conta de desenvolvedor da Apple,</span><span class="sxs-lookup"><span data-stu-id="63a47-134">Enter the properties you retrieved from your Apple developer account,</span></span> 
- <span data-ttu-id="63a47-135">escolha o modo de aplicativo (Produção ou Área Restrita)</span><span class="sxs-lookup"><span data-stu-id="63a47-135">choose your application mode (Production or Sandbox)</span></span> 
- <span data-ttu-id="63a47-136">clique em Salvar para atualizar suas credenciais APNS.</span><span class="sxs-lookup"><span data-stu-id="63a47-136">click Save to update your APNS credentials.</span></span> 

### <a name="configure-via-management-api-rest"></a><span data-ttu-id="63a47-137">Configurar por meio da API de gerenciamento (REST)</span><span class="sxs-lookup"><span data-stu-id="63a47-137">Configure via Management API (REST)</span></span>

<span data-ttu-id="63a47-138">Você pode usar nossas [APIs de gerenciamento](https://msdn.microsoft.com/library/azure/dn495827.aspx) para atualizar o hub de notificações para usar a autenticação baseada em token.</span><span class="sxs-lookup"><span data-stu-id="63a47-138">You can use our [management APIs](https://msdn.microsoft.com/library/azure/dn495827.aspx) to update your notification hub to use token-based authentication.</span></span>
<span data-ttu-id="63a47-139">Dependendo se o aplicativo que você está configurando é um aplicativo de Área Restrita ou de Produção (especificado na sua Conta de Desenvolvedor da Apple), use um dos pontos de extremidade correspondentes:</span><span class="sxs-lookup"><span data-stu-id="63a47-139">Depending on whether the application you’re configuring is a Sandbox or Production app (specified in your Apple Developer Account), use one of the corresponding endpoints:</span></span>

- <span data-ttu-id="63a47-140">Ponto de extremidade da Área Restrita: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="63a47-140">Sandbox Endpoint: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span></span>
- <span data-ttu-id="63a47-141">Ponto de extremidade de Produção: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="63a47-141">Production Endpoint: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="63a47-142">A autenticação baseada em token requer uma versão de API de: **2017-04 ou posterior**.</span><span class="sxs-lookup"><span data-stu-id="63a47-142">Token-based authentication requires an API version of: **2017-04 or later**.</span></span>
> 
> 

<span data-ttu-id="63a47-143">Aqui está um exemplo de uma solicitação PUT para atualizar um hub com autenticação baseada em token:</span><span class="sxs-lookup"><span data-stu-id="63a47-143">Here’s an example of a PUT request to update a hub with token-based authentication:</span></span>


        PUT https://{namespace}.servicebus.windows.net/{Notification Hub}?api-version=2017-04
          "Properties": {
            "ApnsCredential": {
              "Properties": {
                "KeyId": "<Your Key Id>",
                "Token": "<Your Authentication Token>",
                "AppName": "<Your Application Name>",
                "AppId": "<Your Application Id>",
                "Endpoint":"<Sandbox/Production Endpoint>"
              }
            }
          }
        

### <a name="configure-via-the-net-sdk"></a><span data-ttu-id="63a47-144">Configurar por meio do SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="63a47-144">Configure via the .NET SDK</span></span>
<span data-ttu-id="63a47-145">Você pode configurar seu hub para usar a autenticação baseada em token usando nosso [SDK de cliente mais recente](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span><span class="sxs-lookup"><span data-stu-id="63a47-145">You can configure your hub to use token based authentication using our [latest client SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span></span> 

<span data-ttu-id="63a47-146">Aqui está um exemplo de código que ilustra o uso correto:</span><span class="sxs-lookup"><span data-stu-id="63a47-146">Here’s a code sample illustrating the correct usage:</span></span>


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH TO YOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-to-using-certificate-based-authentication"></a><span data-ttu-id="63a47-147">Revertendo para usar a autenticação baseada em certificado</span><span class="sxs-lookup"><span data-stu-id="63a47-147">Reverting to using certificate-based authentication</span></span>
<span data-ttu-id="63a47-148">Você pode reverter a qualquer momento para usar autenticação baseada em certificado usando qualquer método anterior e passando o certificado em vez de as propriedades de token.</span><span class="sxs-lookup"><span data-stu-id="63a47-148">You can revert at any time to using certificate-based authentication by using any preceding method and passing the certificate instead of the token properties.</span></span> <span data-ttu-id="63a47-149">Essa ação substitui as credenciais armazenadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="63a47-149">That action overwrites the previously stored credentials.</span></span>
