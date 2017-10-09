---
title: "aaaToken (HTTP/2) autenticação de APNS em Hubs de notificação do Azure | Microsoft Docs"
description: "Este tópico explica como tooleverage Olá nova autenticação de token para o APNS"
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
ms.openlocfilehash: 3353d7f16033ce0b68edec9ee9aeb98f47faa1fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="token-based-http2-authentication-for-apns"></a><span data-ttu-id="a359d-103">Autenticação baseada em token (HTTP/2) para o APNS</span><span class="sxs-lookup"><span data-stu-id="a359d-103">Token-based (HTTP/2) Authentication for APNS</span></span>
## <a name="overview"></a><span data-ttu-id="a359d-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a359d-104">Overview</span></span>
<span data-ttu-id="a359d-105">Este artigo fornece detalhes sobre como toouse Olá novo APNS HTTP/2 protocolo com token de autenticação com base em.</span><span class="sxs-lookup"><span data-stu-id="a359d-105">This article details how toouse hello new APNS HTTP/2 protocol with token based authentication.</span></span>

<span data-ttu-id="a359d-106">Olá principais benefícios de usar o novo protocolo de saudação incluem:</span><span class="sxs-lookup"><span data-stu-id="a359d-106">hello key benefits of using hello new protocol include:</span></span>
-   <span data-ttu-id="a359d-107">Geração de token é relativamente complicações livre (em comparação com toocertificates)</span><span class="sxs-lookup"><span data-stu-id="a359d-107">Token generation is relatively hassle free (compared toocertificates)</span></span>
-   <span data-ttu-id="a359d-108">Não há mais dadas de expiração – você está no controle dos seus tokens de autenticação e sua revogação</span><span class="sxs-lookup"><span data-stu-id="a359d-108">No more expiry dates – you are in control of your authentication tokens and their revocation</span></span>
-   <span data-ttu-id="a359d-109">Cargas agora podem ser o too4 KB</span><span class="sxs-lookup"><span data-stu-id="a359d-109">Payloads can now be up too4 KB</span></span>
- <span data-ttu-id="a359d-110">Comentários síncronos</span><span class="sxs-lookup"><span data-stu-id="a359d-110">Synchronous feedback</span></span>
-   <span data-ttu-id="a359d-111">Você está usando o protocolo mais recente da Apple – certificados ainda usam protocolo binário hello, que está marcado para substituição</span><span class="sxs-lookup"><span data-stu-id="a359d-111">You’re on Apple’s latest protocol – certificates still use hello binary protocol, which is marked for deprecation</span></span>

<span data-ttu-id="a359d-112">O uso desse novo mecanismo pode ser feito em duas etapas, em alguns minutos:</span><span class="sxs-lookup"><span data-stu-id="a359d-112">Using this new mechanism can be done in two steps in a few minutes:</span></span>
1.  <span data-ttu-id="a359d-113">Obter informações necessárias de saudação do portal de conta de desenvolvedor da Apple Olá</span><span class="sxs-lookup"><span data-stu-id="a359d-113">Obtain hello necessary information from hello Apple Developer Account portal</span></span>
2.  <span data-ttu-id="a359d-114">Configurar seu hub de notificação com novas informações de saudação</span><span class="sxs-lookup"><span data-stu-id="a359d-114">Configure your notification hub with hello new information</span></span>

<span data-ttu-id="a359d-115">Hubs de notificação é agora todos os conjunto toouse Olá novo sistema de autenticação com APNS.</span><span class="sxs-lookup"><span data-stu-id="a359d-115">Notification Hubs is now all set toouse hello new authentication system with APNS.</span></span> 

<span data-ttu-id="a359d-116">Observe que se você migrou usando as credenciais de certificado para APNS:</span><span class="sxs-lookup"><span data-stu-id="a359d-116">Note that if you migrated from using certificate credentials for APNS:</span></span>
- <span data-ttu-id="a359d-117">Propriedades do token Olá substituir o certificado em nosso sistema</span><span class="sxs-lookup"><span data-stu-id="a359d-117">hello token properties overwrite your certificate in our system,</span></span>
- <span data-ttu-id="a359d-118">mas o aplicativo continua tooreceive notificações perfeitamente.</span><span class="sxs-lookup"><span data-stu-id="a359d-118">but your application continues tooreceive notifications seamlessly.</span></span>

## <a name="obtaining-authentication-information-from-apple"></a><span data-ttu-id="a359d-119">Obtendo informações de autenticação da Apple</span><span class="sxs-lookup"><span data-stu-id="a359d-119">Obtaining authentication information from Apple</span></span>
<span data-ttu-id="a359d-120">a autenticação baseada em token tooenable, você precisa Olá seguintes propriedades da conta do desenvolvedor Apple:</span><span class="sxs-lookup"><span data-stu-id="a359d-120">tooenable token-based authentication, you need hello following properties from your Apple Developer Account:</span></span>
### <a name="key-identifier"></a><span data-ttu-id="a359d-121">Identificador de chave</span><span class="sxs-lookup"><span data-stu-id="a359d-121">Key Identifier</span></span>
<span data-ttu-id="a359d-122">Identificador de chave Olá pode ser obtido da página de "Chaves" hello em sua conta de desenvolvedor da Apple</span><span class="sxs-lookup"><span data-stu-id="a359d-122">hello key identifier can be obtained from hello "Keys" page in your Apple Developer Account</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a><span data-ttu-id="a359d-123">Identificador do aplicativo e nome do aplicativo</span><span class="sxs-lookup"><span data-stu-id="a359d-123">Application Identifier & Application Name</span></span>
<span data-ttu-id="a359d-124">nome do aplicativo Hello está disponível por meio de página de IDs de aplicativo Olá Olá conta de desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="a359d-124">hello application name is available via hello App IDs page in hello Developer Account.</span></span> 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

<span data-ttu-id="a359d-125">Identificador do aplicativo Hello está disponível por meio da página de detalhes de associação Olá no hello conta de desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="a359d-125">hello application identifier is available via hello membership details page in hello Developer Account.</span></span>
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a><span data-ttu-id="a359d-126">Token de autenticação</span><span class="sxs-lookup"><span data-stu-id="a359d-126">Authentication token</span></span>
<span data-ttu-id="a359d-127">o token de autenticação Olá pode ser baixado depois de gerar um token para o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a359d-127">hello authentication token can be downloaded after you generate a token for your application.</span></span> <span data-ttu-id="a359d-128">Para obter detalhes sobre como toogenerate esse token, consulte muito[documentação do desenvolvedor da Apple](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span><span class="sxs-lookup"><span data-stu-id="a359d-128">For details on how toogenerate this token, refer too[Apple’s Developer documentation](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span></span>

## <a name="configuring-your-notification-hub-toouse-token-based-authentication"></a><span data-ttu-id="a359d-129">Configurando a autenticação de baseado em token do toouse de hub de notificação</span><span class="sxs-lookup"><span data-stu-id="a359d-129">Configuring your notification hub toouse token-based authentication</span></span>
### <a name="configure-via-hello-azure-portal"></a><span data-ttu-id="a359d-130">Configurar por meio de saudação portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a359d-130">Configure via hello Azure portal</span></span>
<span data-ttu-id="a359d-131">token tooenable com base em autenticação no portal de hello, log em toohello portal do Azure e vá tooyour Hub de notificação > Serviços de notificação > Painel APNS.</span><span class="sxs-lookup"><span data-stu-id="a359d-131">tooenable token based authentication in hello portal, log in toohello Azure portal and go tooyour Notification Hub > Notification Services > APNS panel.</span></span> 

<span data-ttu-id="a359d-132">Há uma nova propriedade – *Modo de Autenticação*.</span><span class="sxs-lookup"><span data-stu-id="a359d-132">There is a new property – *Authentication Mode*.</span></span> <span data-ttu-id="a359d-133">Selecionar Token permite que você tooupdate seu hub com todas as propriedades token de relevantes de saudação.</span><span class="sxs-lookup"><span data-stu-id="a359d-133">Selecting Token allows you tooupdate your hub with all hello relevant token properties.</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- <span data-ttu-id="a359d-134">Inserir propriedades de saudação recuperados de sua conta de desenvolvedor da Apple,</span><span class="sxs-lookup"><span data-stu-id="a359d-134">Enter hello properties you retrieved from your Apple developer account,</span></span> 
- <span data-ttu-id="a359d-135">escolha o modo de aplicativo (Produção ou Área Restrita)</span><span class="sxs-lookup"><span data-stu-id="a359d-135">choose your application mode (Production or Sandbox)</span></span> 
- <span data-ttu-id="a359d-136">Clique em Salvar tooupdate suas credenciais APNS.</span><span class="sxs-lookup"><span data-stu-id="a359d-136">click Save tooupdate your APNS credentials.</span></span> 

### <a name="configure-via-management-api-rest"></a><span data-ttu-id="a359d-137">Configurar por meio da API de gerenciamento (REST)</span><span class="sxs-lookup"><span data-stu-id="a359d-137">Configure via Management API (REST)</span></span>

<span data-ttu-id="a359d-138">Você pode usar nosso [APIs de gerenciamento](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate sua autenticação notificação hub toouse baseado em token.</span><span class="sxs-lookup"><span data-stu-id="a359d-138">You can use our [management APIs](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate your notification hub toouse token-based authentication.</span></span>
<span data-ttu-id="a359d-139">Dependendo se o aplicativo hello a que você estiver configurando é um aplicativo de área restrita ou de produção (especificado na sua conta de desenvolvedor da Apple), use um dos pontos de extremidade correspondente hello:</span><span class="sxs-lookup"><span data-stu-id="a359d-139">Depending on whether hello application you’re configuring is a Sandbox or Production app (specified in your Apple Developer Account), use one of hello corresponding endpoints:</span></span>

- <span data-ttu-id="a359d-140">Ponto de extremidade da Área Restrita: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="a359d-140">Sandbox Endpoint: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span></span>
- <span data-ttu-id="a359d-141">Ponto de extremidade de Produção: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="a359d-141">Production Endpoint: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a359d-142">A autenticação baseada em token requer uma versão de API de: **2017-04 ou posterior**.</span><span class="sxs-lookup"><span data-stu-id="a359d-142">Token-based authentication requires an API version of: **2017-04 or later**.</span></span>
> 
> 

<span data-ttu-id="a359d-143">Aqui está um exemplo de uma solicitação PUT tooupdate um hub com autenticação baseada em token:</span><span class="sxs-lookup"><span data-stu-id="a359d-143">Here’s an example of a PUT request tooupdate a hub with token-based authentication:</span></span>


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
        

### <a name="configure-via-hello-net-sdk"></a><span data-ttu-id="a359d-144">Configurar por meio de saudação SDK .NET</span><span class="sxs-lookup"><span data-stu-id="a359d-144">Configure via hello .NET SDK</span></span>
<span data-ttu-id="a359d-145">Você pode configurar seu hub toouse autenticação baseada em token usando nosso [SDK mais recente do cliente](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span><span class="sxs-lookup"><span data-stu-id="a359d-145">You can configure your hub toouse token based authentication using our [latest client SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span></span> 

<span data-ttu-id="a359d-146">Aqui está um exemplo de código que ilustram o uso correto da saudação:</span><span class="sxs-lookup"><span data-stu-id="a359d-146">Here’s a code sample illustrating hello correct usage:</span></span>


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH tooYOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-toousing-certificate-based-authentication"></a><span data-ttu-id="a359d-147">Autenticação baseada em certificado do toousing reversão</span><span class="sxs-lookup"><span data-stu-id="a359d-147">Reverting toousing certificate-based authentication</span></span>
<span data-ttu-id="a359d-148">Você pode reverter em qualquer autenticação baseada em certificado do tempo toousing usando qualquer certificado de saudação do método e passando anterior em vez de propriedades de token hello.</span><span class="sxs-lookup"><span data-stu-id="a359d-148">You can revert at any time toousing certificate-based authentication by using any preceding method and passing hello certificate instead of hello token properties.</span></span> <span data-ttu-id="a359d-149">Ação substitui Olá anteriormente credenciais armazenadas.</span><span class="sxs-lookup"><span data-stu-id="a359d-149">That action overwrites hello previously stored credentials.</span></span>
