---
title: "Proteger serviços de back-end usando autenticação de certificado do cliente - Gerenciamento de API do Azure | Microsoft Docs"
description: "Saiba como garantir serviços de back-end usando autenticação de certificado do cliente no Gerenciamento de API do Azure."
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
ms.openlocfilehash: 2ebe71c96fd9076a48f689041634dbd23d3d8414
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-secure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a><span data-ttu-id="b0272-103">Como garantir serviços de back-end usando autenticação de certificado do cliente no Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="b0272-103">How to secure back-end services using client certificate authentication in Azure API Management</span></span>
<span data-ttu-id="b0272-104">O Gerenciamento de API fornece a capacidade para garantir acesso ao serviço back-end de uma API usando certificados do cliente.</span><span class="sxs-lookup"><span data-stu-id="b0272-104">API Management provides the capability to secure access to the back-end service of an API using client certificates.</span></span> <span data-ttu-id="b0272-105">Este guia mostra como gerenciar certificados no Portal do editor de API e como configurar uma API para usar um certificado para acessar seu serviço back-end.</span><span class="sxs-lookup"><span data-stu-id="b0272-105">This guide shows how to manage certificates in the API publisher portal, and how to configure an API to use a certificate to access its back-end service.</span></span>

<span data-ttu-id="b0272-106">Para obter mais informações sobre gerenciamento de certificados usando a API REST de gerenciamento de API, consulte [Entidade de certificado da API REST de Gerenciamento de API do Azure][Azure API Management REST API Certificate entity].</span><span class="sxs-lookup"><span data-stu-id="b0272-106">For information about managing certificates using the API Management REST API, see [Azure API Management REST API Certificate entity][Azure API Management REST API Certificate entity].</span></span>

## <span data-ttu-id="b0272-107"><a name="prerequisites"> </a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b0272-107"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="b0272-108">Este guia mostra como configurar sua instância de serviço de Gerenciamento de API para usar a autenticação de certificado do cliente para acessar o serviço back-end para uma API.</span><span class="sxs-lookup"><span data-stu-id="b0272-108">This guide shows you how to configure your API Management service instance to use client certificate authentication to access the back-end service for an API.</span></span> <span data-ttu-id="b0272-109">Antes de seguir as etapas descritas neste tópico, é necessário configurar seu serviço back-end para a autenticação de certificado do cliente ([para configurar a autenticação de certificado nos Sites do Azure, consulte este artigo][to configure certificate authentication in Azure WebSites refer to this article]) e ter acesso ao certificado e à senha do certificado para carregar no portal do editor do Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="b0272-109">Before following the steps in this topic, you should have your back-end service configured for client certificate authentication ([to configure certificate authentication in Azure WebSites refer to this article][to configure certificate authentication in Azure WebSites refer to this article]), and have access to the certificate and the password for the certificate for uploading in the API Management publisher portal.</span></span>

## <span data-ttu-id="b0272-110"><a name="step1"> </a>Carregar um certificado do cliente</span><span class="sxs-lookup"><span data-stu-id="b0272-110"><a name="step1"> </a>Upload a client certificate</span></span>
<span data-ttu-id="b0272-111">Para começar, clique em **Portal do Editor** no Portal do Azure para acessar o serviço de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="b0272-111">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="b0272-112">Isso levará você ao portal do editor de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="b0272-112">This takes you to the API Management publisher portal.</span></span>

![Portal do editor de API][api-management-management-console]

> <span data-ttu-id="b0272-114">Se ainda não criou uma instância de serviço de Gerenciamento de API, confira [Criar uma instância de serviço de Gerenciamento de API][Create an API Management service instance] no tutorial [Introdução ao Gerenciamento de API do Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="b0272-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="b0272-115">Clique em **Segurança** no menu **Gerenciamento de API** à esquerda e clique em **Certificados do cliente**.</span><span class="sxs-lookup"><span data-stu-id="b0272-115">Click **Security** from the **API Management** menu on the left, and click **Client certificates**.</span></span>

![Certificados do cliente][api-management-security-client-certificates]

<span data-ttu-id="b0272-117">Para carregar um novo certificado, clique em **Carregar um certificado**.</span><span class="sxs-lookup"><span data-stu-id="b0272-117">To upload a new certificate, click **Upload certificate**.</span></span>

![Carregar um certificado][api-management-upload-certificate]

<span data-ttu-id="b0272-119">Navegue para o seu certificado e digite a senha para o certificado.</span><span class="sxs-lookup"><span data-stu-id="b0272-119">Browse to your certificate, and then enter the password for the certificate.</span></span>

> <span data-ttu-id="b0272-120">O certificado deve estar no formato **.pfx** .</span><span class="sxs-lookup"><span data-stu-id="b0272-120">The certificate must be in **.pfx** format.</span></span> <span data-ttu-id="b0272-121">Os certificados autoassinados são permitidos.</span><span class="sxs-lookup"><span data-stu-id="b0272-121">Self-signed certificates are allowed.</span></span>
> 
> 

![Carregar um certificado][api-management-upload-certificate-form]

<span data-ttu-id="b0272-123">Clique em **Carregar** para carregar o certificado.</span><span class="sxs-lookup"><span data-stu-id="b0272-123">Click **Upload** to upload the certificate.</span></span>

> <span data-ttu-id="b0272-124">A senha do certificado é validada neste momento.</span><span class="sxs-lookup"><span data-stu-id="b0272-124">The certificate password is validated at this time.</span></span> <span data-ttu-id="b0272-125">Se ela estiver incorreta, é exibida uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="b0272-125">If it is incorrect an error message is displayed.</span></span>
> 
> 

![Certificado carregado][api-management-certificate-uploaded]

<span data-ttu-id="b0272-127">Uma vez que o certificado é carregado, ele aparece na guia **Certificados do cliente** .</span><span class="sxs-lookup"><span data-stu-id="b0272-127">Once the certificate is uploaded, it appears on the **Client certificates** tab.</span></span> <span data-ttu-id="b0272-128">Se você tiver vários certificados, anote a entidade ou os últimos quatro caracteres da impressão digital, que serão usados para selecionar o certificado ao configurar uma API para usar certificados, como abordado na seção [Configurar uma API para usar um certificado do cliente para a autenticação de gateway][Configure an API to use a client certificate for gateway authentication] a seguir.</span><span class="sxs-lookup"><span data-stu-id="b0272-128">If you have multiple certificates, make a note of the subject, or the last four characters of the thumbprint, which are used to select the certificate when configuring an API to use certificates, as covered in the following [Configure an API to use a client certificate for gateway authentication][Configure an API to use a client certificate for gateway authentication] section.</span></span>

> <span data-ttu-id="b0272-129">Para desabilitar a validação da cadeia de certificados ao usar, por exemplo, um certificado autoassinado, siga as etapas descritas neste [item](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end) das Perguntas frequentes.</span><span class="sxs-lookup"><span data-stu-id="b0272-129">To turn off certificate chain validation when using, for example, a self-signed certificate, follow the steps described in this FAQ [item](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).</span></span>
> 
> 

## <span data-ttu-id="b0272-130"><a name="step1a"> </a>Excluir um certificado do cliente</span><span class="sxs-lookup"><span data-stu-id="b0272-130"><a name="step1a"> </a>Delete a client certificate</span></span>
<span data-ttu-id="b0272-131">Para excluir um certificado, clique em **Excluir** ao lado do certificado desejado.</span><span class="sxs-lookup"><span data-stu-id="b0272-131">To delete a certificate, click **Delete** beside the desired certificate.</span></span>

![Excluir Certificado][api-management-certificate-delete]

<span data-ttu-id="b0272-133">Clique em **Sim, excluir** para confirmar.</span><span class="sxs-lookup"><span data-stu-id="b0272-133">Click **Yes, delete it** to confirm.</span></span>

![Confirmar exclusão][api-management-confirm-delete]

<span data-ttu-id="b0272-135">Se o certificado está em uso por uma API, então uma tela de aviso é exibida.</span><span class="sxs-lookup"><span data-stu-id="b0272-135">If the certificate is in use by an API, then a warning screen is displayed.</span></span> <span data-ttu-id="b0272-136">Para excluir o certificado, você primeiro deve remover o certificado de quaisquer APIs que são configuradas para usá-la.</span><span class="sxs-lookup"><span data-stu-id="b0272-136">To delete the certificate you must first remove the certificate from any APIs that are configured to use it.</span></span>

![Confirmar exclusão][api-management-confirm-delete-policy]

## <span data-ttu-id="b0272-138"><a name="step2"> </a>Configurar uma API para usar um certificado do cliente para a autenticação de gateway</span><span class="sxs-lookup"><span data-stu-id="b0272-138"><a name="step2"> </a>Configure an API to use a client certificate for gateway authentication</span></span>
<span data-ttu-id="b0272-139">Clique nas **APIs** no menu **Gerenciamento de API** à esquerda, clique no nome da API desejada e clique na guia **Segurança**.</span><span class="sxs-lookup"><span data-stu-id="b0272-139">Click **APIs** from the **API Management** menu on the left, click the name of the desired API, and click the **Security** tab.</span></span>

![Segurança da API][api-management-api-security]

<span data-ttu-id="b0272-141">Selecione **Certificados do cliente** na lista suspensa **Com credenciais**.</span><span class="sxs-lookup"><span data-stu-id="b0272-141">Select **Client certificates** from the **With credentials** drop-down list.</span></span>

![Certificados do cliente][api-management-mutual-certificates]

<span data-ttu-id="b0272-143">Selecione o certificado desejado da lista suspensa **Certificado do cliente** .</span><span class="sxs-lookup"><span data-stu-id="b0272-143">Select the desired certificate from the **Client certificate** drop-down list.</span></span> <span data-ttu-id="b0272-144">Se houver certificados múltiplos, você pode olhar no assunto ou nos últimos quatro caracteres da impressão digital como observado na seção anterior para determinar o certificado correto.</span><span class="sxs-lookup"><span data-stu-id="b0272-144">If there are multiple certificates you can look at the subject or the last four characters of the thumbprint as noted in the previous section to determine the correct certificate.</span></span>

![Selecionar certificado][api-management-select-certificate]

<span data-ttu-id="b0272-146">Clique em **Salvar** para salvar as alterações de configuração para a API.</span><span class="sxs-lookup"><span data-stu-id="b0272-146">Click **Save** to save the configuration change to the API.</span></span>

> <span data-ttu-id="b0272-147">Essa alteração tem efeito imediato e chama para operações desta API, que usará o certificado para autenticar no servidor back-end.</span><span class="sxs-lookup"><span data-stu-id="b0272-147">This change is effective immediately, and calls to operations of that API will use the certificate to authenticate on the back-end server.</span></span>
> 
> 

![Salvar alterações da API][api-management-save-api]

> <span data-ttu-id="b0272-149">Quando um certificado é especificado para a autenticação de gateway para o serviço back-end de uma API, ele se torna parte da política dessa API e pode ser exibido no editor da política.</span><span class="sxs-lookup"><span data-stu-id="b0272-149">When a certificate is specified for gateway authentication for the back-end service of an API, it becomes part of the policy for that API, and can be viewed in the policy editor.</span></span>
> 
> 

![Política do certificado][api-management-certificate-policy]

## <a name="next-steps"></a><span data-ttu-id="b0272-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b0272-151">Next steps</span></span>
<span data-ttu-id="b0272-152">Para obter mais informações sobre outras maneiras de proteger seu serviço de back-end, como HTTP básica ou autenticação secreta compartilhada, consulte o vídeo a seguir.</span><span class="sxs-lookup"><span data-stu-id="b0272-152">For more information on other ways to secure your backend service, such as HTTP basic or shared secret authentication, see the following video.</span></span>

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



[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Azure API Management REST API Certificate entity]: http://msdn.microsoft.com/library/azure/dn783483.aspx
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[to configure certificate authentication in Azure WebSites refer to this article]: https://azure.microsoft.com/en-us/documentation/articles/app-service-web-configure-tls-mutual-auth/

[Prerequisites]: #prerequisites
[Upload a client certificate]: #step1
[Delete a client certificate]: #step1a
[Configure an API to use a client certificate for gateway authentication]: #step2
[Test the configuration by calling an operation in the Developer Portal]: #step3
[Next steps]: #next-steps



