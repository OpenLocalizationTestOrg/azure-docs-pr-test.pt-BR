---
title: "Serviços de back-end aaaSecure usando a autenticação de certificado de cliente - gerenciamento de API do Azure | Microsoft Docs"
description: "Saiba como serviços de back-end toosecure usando o cliente de certificado autenticação no gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 43453331-39b2-4672-80b8-0a87e4fde3c6
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 565bb61044fed1158944202c36e8abe30edf5729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a><span data-ttu-id="df8c6-103">Como serviços de back-end toosecure usando o cliente de certificado autenticação no gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="df8c6-103">How toosecure back-end services using client certificate authentication in Azure API Management</span></span>
<span data-ttu-id="df8c6-104">Gerenciamento de API fornece Olá recurso toosecure acesso toohello serviço back-end de uma API usando certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="df8c6-104">API Management provides hello capability toosecure access toohello back-end service of an API using client certificates.</span></span> <span data-ttu-id="df8c6-105">Este guia mostra como toomanage certificados no portal do publicador Olá API e uma API de tooconfigure toouse tooaccess um certificado seu serviço de back-end.</span><span class="sxs-lookup"><span data-stu-id="df8c6-105">This guide shows how toomanage certificates in hello API publisher portal, and how tooconfigure an API toouse a certificate tooaccess its back-end service.</span></span>

<span data-ttu-id="df8c6-106">Para obter informações sobre como gerenciar certificados usando Olá API de REST de gerenciamento de API, consulte [entidade do certificado de API de REST de gerenciamento do Azure API][Azure API Management REST API Certificate entity].</span><span class="sxs-lookup"><span data-stu-id="df8c6-106">For information about managing certificates using hello API Management REST API, see [Azure API Management REST API Certificate entity][Azure API Management REST API Certificate entity].</span></span>

## <span data-ttu-id="df8c6-107"><a name="prerequisites"> </a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="df8c6-107"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="df8c6-108">Este guia mostra como tooconfigure os gerenciamento de API serviço instância toouse cliente certificado autenticação tooaccess Olá serviço de back-end para uma API.</span><span class="sxs-lookup"><span data-stu-id="df8c6-108">This guide shows you how tooconfigure your API Management service instance toouse client certificate authentication tooaccess hello back-end service for an API.</span></span> <span data-ttu-id="df8c6-109">Antes de saudação seguir as etapas neste tópico, você deve ter seu serviço de back-end configurado para autenticação de certificado de cliente ([tooconfigure certificado autenticação em sites do Azure consulte o artigo toothis] [ tooconfigure certificate authentication in Azure WebSites refer toothis article]), e ter acesso toohello certificado e hello senha Olá certificado para carregar no portal do publicador de gerenciamento de API de saudação.</span><span class="sxs-lookup"><span data-stu-id="df8c6-109">Before following hello steps in this topic, you should have your back-end service configured for client certificate authentication ([tooconfigure certificate authentication in Azure WebSites refer toothis article][tooconfigure certificate authentication in Azure WebSites refer toothis article]), and have access toohello certificate and hello password for hello certificate for uploading in hello API Management publisher portal.</span></span>

## <span data-ttu-id="df8c6-110"><a name="step1"> </a>Carregar um certificado do cliente</span><span class="sxs-lookup"><span data-stu-id="df8c6-110"><a name="step1"> </a>Upload a client certificate</span></span>
<span data-ttu-id="df8c6-111">tooget iniciado, clique em **portal do publicador** em hello Portal do Azure para seu serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="df8c6-111">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="df8c6-112">Isso leva toohello portal do publicador de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="df8c6-112">This takes you toohello API Management publisher portal.</span></span>

![Portal do editor de API][api-management-management-console]

> <span data-ttu-id="df8c6-114">Se você ainda não tiver criado uma instância do serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [Introdução ao gerenciamento de API do Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="df8c6-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="df8c6-115">Clique em **segurança** de saudação **gerenciamento de API** menu Olá esquerda e clique em **certificados de cliente**.</span><span class="sxs-lookup"><span data-stu-id="df8c6-115">Click **Security** from hello **API Management** menu on hello left, and click **Client certificates**.</span></span>

![Certificados do cliente][api-management-security-client-certificates]

<span data-ttu-id="df8c6-117">tooupload um novo certificado, clique em **Upload do certificado**.</span><span class="sxs-lookup"><span data-stu-id="df8c6-117">tooupload a new certificate, click **Upload certificate**.</span></span>

![Carregar um certificado][api-management-upload-certificate]

<span data-ttu-id="df8c6-119">Procurar o certificado de tooyour e digite senha Olá Olá certificado.</span><span class="sxs-lookup"><span data-stu-id="df8c6-119">Browse tooyour certificate, and then enter hello password for hello certificate.</span></span>

> <span data-ttu-id="df8c6-120">Olá certificado deve estar na **. pfx** formato.</span><span class="sxs-lookup"><span data-stu-id="df8c6-120">hello certificate must be in **.pfx** format.</span></span> <span data-ttu-id="df8c6-121">Os certificados autoassinados são permitidos.</span><span class="sxs-lookup"><span data-stu-id="df8c6-121">Self-signed certificates are allowed.</span></span>
> 
> 

![Carregar um certificado][api-management-upload-certificate-form]

<span data-ttu-id="df8c6-123">Clique em **carregar** certificado de saudação tooupload.</span><span class="sxs-lookup"><span data-stu-id="df8c6-123">Click **Upload** tooupload hello certificate.</span></span>

> <span data-ttu-id="df8c6-124">senha do certificado Olá é validada no momento.</span><span class="sxs-lookup"><span data-stu-id="df8c6-124">hello certificate password is validated at this time.</span></span> <span data-ttu-id="df8c6-125">Se ela estiver incorreta, é exibida uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="df8c6-125">If it is incorrect an error message is displayed.</span></span>
> 
> 

![Certificado carregado][api-management-certificate-uploaded]

<span data-ttu-id="df8c6-127">Depois que o certificado Olá é carregado, ele aparecerá na Olá **certificados de cliente** guia. Se você tiver vários certificados, tome nota do assunto hello ou Olá últimos quatro caracteres da impressão digital hello, que são certificados de saudação tooselect usado ao configurar um toouse API certificados, conforme abordado na seguinte Olá [configurar uma API toouse um certificado de cliente para autenticação de gateway] [ Configure an API toouse a client certificate for gateway authentication] seção.</span><span class="sxs-lookup"><span data-stu-id="df8c6-127">Once hello certificate is uploaded, it appears on hello **Client certificates** tab. If you have multiple certificates, make a note of hello subject, or hello last four characters of hello thumbprint, which are used tooselect hello certificate when configuring an API toouse certificates, as covered in hello following [Configure an API toouse a client certificate for gateway authentication][Configure an API toouse a client certificate for gateway authentication] section.</span></span>

> <span data-ttu-id="df8c6-128">tooturn desativar a validação da cadeia de certificado ao usar, por exemplo, um certificado autoassinado, execute as etapas de saudação descritas neste documento [item](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span><span class="sxs-lookup"><span data-stu-id="df8c6-128">tooturn off certificate chain validation when using, for example, a self-signed certificate, follow hello steps described in this FAQ [item](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span></span>
> 
> 

## <span data-ttu-id="df8c6-129"><a name="step1a"> </a>Excluir um certificado do cliente</span><span class="sxs-lookup"><span data-stu-id="df8c6-129"><a name="step1a"> </a>Delete a client certificate</span></span>
<span data-ttu-id="df8c6-130">toodelete um certificado, clique em **excluir** ao lado de certificado de saudação desejado.</span><span class="sxs-lookup"><span data-stu-id="df8c6-130">toodelete a certificate, click **Delete** beside hello desired certificate.</span></span>

![Excluir Certificado][api-management-certificate-delete]

<span data-ttu-id="df8c6-132">Clique em **Sim, excluí-la** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="df8c6-132">Click **Yes, delete it** tooconfirm.</span></span>

![Confirmar exclusão][api-management-confirm-delete]

<span data-ttu-id="df8c6-134">Se o certificado hello está sendo usado por uma API, uma tela de aviso é exibida.</span><span class="sxs-lookup"><span data-stu-id="df8c6-134">If hello certificate is in use by an API, then a warning screen is displayed.</span></span> <span data-ttu-id="df8c6-135">certificado de saudação toodelete você deve primeiro remover Olá certificado de quaisquer APIs toouse configurado-lo.</span><span class="sxs-lookup"><span data-stu-id="df8c6-135">toodelete hello certificate you must first remove hello certificate from any APIs that are configured toouse it.</span></span>

![Confirmar exclusão][api-management-confirm-delete-policy]

## <span data-ttu-id="df8c6-137"><a name="step2"></a>Configurar toouse uma API um certificado de cliente para autenticação de gateway</span><span class="sxs-lookup"><span data-stu-id="df8c6-137"><a name="step2"> </a>Configure an API toouse a client certificate for gateway authentication</span></span>
<span data-ttu-id="df8c6-138">Clique em **APIs** de saudação **gerenciamento de API** Olá menu à esquerda, clique em nome de saudação da API de saudação desejada e clique em Olá **segurança** guia.</span><span class="sxs-lookup"><span data-stu-id="df8c6-138">Click **APIs** from hello **API Management** menu on hello left, click hello name of hello desired API, and click hello **Security** tab.</span></span>

![Segurança da API][api-management-api-security]

<span data-ttu-id="df8c6-140">Selecione **certificados de cliente** de saudação **com credenciais** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="df8c6-140">Select **Client certificates** from hello **With credentials** drop-down list.</span></span>

![Certificados do cliente][api-management-mutual-certificates]

<span data-ttu-id="df8c6-142">Selecione Olá certificado desejado na Olá **certificado de cliente** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="df8c6-142">Select hello desired certificate from hello **Client certificate** drop-down list.</span></span> <span data-ttu-id="df8c6-143">Se houver vários certificados, você pode examinar o assunto de saudação ou Olá últimos quatro caracteres da impressão digital de saudação conforme observado no certificado correto do hello anterior seção toodetermine hello.</span><span class="sxs-lookup"><span data-stu-id="df8c6-143">If there are multiple certificates you can look at hello subject or hello last four characters of hello thumbprint as noted in hello previous section toodetermine hello correct certificate.</span></span>

![Selecionar certificado][api-management-select-certificate]

<span data-ttu-id="df8c6-145">Clique em **salvar** toosave Olá configuração alteração toohello API.</span><span class="sxs-lookup"><span data-stu-id="df8c6-145">Click **Save** toosave hello configuration change toohello API.</span></span>

> <span data-ttu-id="df8c6-146">Essa alteração é imediatamente efetivada e chamadas toooperations essa API usará Olá tooauthenticate de certificado no servidor de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="df8c6-146">This change is effective immediately, and calls toooperations of that API will use hello certificate tooauthenticate on hello back-end server.</span></span>
> 
> 

![Salvar alterações da API][api-management-save-api]

> <span data-ttu-id="df8c6-148">Quando um certificado é especificado para autenticação de gateway para o serviço de back-end de saudação de uma API, torna-se parte da política de saudação para essa API e podem ser exibido no editor de diretiva de saudação.</span><span class="sxs-lookup"><span data-stu-id="df8c6-148">When a certificate is specified for gateway authentication for hello back-end service of an API, it becomes part of hello policy for that API, and can be viewed in hello policy editor.</span></span>
> 
> 

![Política do certificado][api-management-certificate-policy]

## <a name="next-steps"></a><span data-ttu-id="df8c6-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="df8c6-150">Next steps</span></span>
<span data-ttu-id="df8c6-151">Para obter mais informações sobre outra maneiras toosecure seu serviço de back-end, como HTTP autenticação basic ou compartilhada secreta, consulte Olá vídeo a seguir.</span><span class="sxs-lookup"><span data-stu-id="df8c6-151">For more information on other ways toosecure your backend service, such as HTTP basic or shared secret authentication, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Last-mile-Security/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-mutual-certificates/api-management-management-console.png
[api-management-security-client-certificates]: ./media/api-management-howto-mutual-certificates/api-management-security-client-certificates.png
[api-management-upload-certificate]: ./media/api-management-howto-mutual-certificates/api-management-upload-certificate.png
[api-management-upload-certificate-form]: ./media/api-management-howto-mutual-certificates/api-management-upload-certificate-form.png
[api-management-certificate-uploaded]: ./media/api-management-howto-mutual-certificates/api-management-certificate-uploaded.png
[api-management-api-security]: ./media/api-management-howto-mutual-certificates/api-management-api-security.png
[api-management-mutual-certificates]: ./media/api-management-howto-mutual-certificates/api-management-mutual-certificates.png
[api-management-select-certificate]: ./media/api-management-howto-mutual-certificates/api-management-select-certificate.png
[api-management-save-api]: ./media/api-management-howto-mutual-certificates/api-management-save-api.png
[api-management-certificate-policy]: ./media/api-management-howto-mutual-certificates/api-management-certificate-policy.png
[api-management-certificate-delete]: ./media/api-management-howto-mutual-certificates/api-management-certificate-delete.png
[api-management-confirm-delete]: ./media/api-management-howto-mutual-certificates/api-management-confirm-delete.png
[api-management-confirm-delete-policy]: ./media/api-management-howto-mutual-certificates/api-management-confirm-delete-policy.png



[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Azure API Management REST API Certificate entity]: http://msdn.microsoft.com/library/azure/dn783483.aspx
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[tooconfigure certificate authentication in Azure WebSites refer toothis article]: https://azure.microsoft.com/en-us/documentation/articles/app-service-web-configure-tls-mutual-auth/

[Prerequisites]: #prerequisites
[Upload a client certificate]: #step1
[Delete a client certificate]: #step1a
[Configure an API toouse a client certificate for gateway authentication]: #step2
[Test hello configuration by calling an operation in hello Developer Portal]: #step3
[Next steps]: #next-steps



