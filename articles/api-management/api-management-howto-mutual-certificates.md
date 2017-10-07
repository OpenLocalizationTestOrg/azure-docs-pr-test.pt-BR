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
# <a name="how-toosecure-back-end-services-using-client-certificate-authentication-in-azure-api-management"></a>Como serviços de back-end toosecure usando o cliente de certificado autenticação no gerenciamento de API do Azure
Gerenciamento de API fornece Olá recurso toosecure acesso toohello serviço back-end de uma API usando certificados de cliente. Este guia mostra como toomanage certificados no portal do publicador Olá API e uma API de tooconfigure toouse tooaccess um certificado seu serviço de back-end.

Para obter informações sobre como gerenciar certificados usando Olá API de REST de gerenciamento de API, consulte [entidade do certificado de API de REST de gerenciamento do Azure API][Azure API Management REST API Certificate entity].

## <a name="prerequisites"> </a>Pré-requisitos
Este guia mostra como tooconfigure os gerenciamento de API serviço instância toouse cliente certificado autenticação tooaccess Olá serviço de back-end para uma API. Antes de saudação seguir as etapas neste tópico, você deve ter seu serviço de back-end configurado para autenticação de certificado de cliente ([tooconfigure certificado autenticação em sites do Azure consulte o artigo toothis] [ tooconfigure certificate authentication in Azure WebSites refer toothis article]), e ter acesso toohello certificado e hello senha Olá certificado para carregar no portal do publicador de gerenciamento de API de saudação.

## <a name="step1"> </a>Carregar um certificado do cliente
tooget iniciado, clique em **portal do publicador** em hello Portal do Azure para seu serviço de gerenciamento de API. Isso leva toohello portal do publicador de gerenciamento de API.

![Portal do editor de API][api-management-management-console]

> Se você ainda não tiver criado uma instância do serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [Introdução ao gerenciamento de API do Azure] [ Get started with Azure API Management] tutorial.
> 
> 

Clique em **segurança** de saudação **gerenciamento de API** menu Olá esquerda e clique em **certificados de cliente**.

![Certificados do cliente][api-management-security-client-certificates]

tooupload um novo certificado, clique em **Upload do certificado**.

![Carregar um certificado][api-management-upload-certificate]

Procurar o certificado de tooyour e digite senha Olá Olá certificado.

> Olá certificado deve estar na **. pfx** formato. Os certificados autoassinados são permitidos.
> 
> 

![Carregar um certificado][api-management-upload-certificate-form]

Clique em **carregar** certificado de saudação tooupload.

> senha do certificado Olá é validada no momento. Se ela estiver incorreta, é exibida uma mensagem de erro.
> 
> 

![Certificado carregado][api-management-certificate-uploaded]

Depois que o certificado Olá é carregado, ele aparecerá na Olá **certificados de cliente** guia. Se você tiver vários certificados, tome nota do assunto hello ou Olá últimos quatro caracteres da impressão digital hello, que são certificados de saudação tooselect usado ao configurar um toouse API certificados, conforme abordado na seguinte Olá [configurar uma API toouse um certificado de cliente para autenticação de gateway] [ Configure an API toouse a client certificate for gateway authentication] seção.

> tooturn desativar a validação da cadeia de certificado ao usar, por exemplo, um certificado autoassinado, execute as etapas de saudação descritas neste documento [item](api-management-faq.md#can-i-use-a-self-signed-ssl-certificate-for-a-back-end).
> 
> 

## <a name="step1a"> </a>Excluir um certificado do cliente
toodelete um certificado, clique em **excluir** ao lado de certificado de saudação desejado.

![Excluir Certificado][api-management-certificate-delete]

Clique em **Sim, excluí-la** tooconfirm.

![Confirmar exclusão][api-management-confirm-delete]

Se o certificado hello está sendo usado por uma API, uma tela de aviso é exibida. certificado de saudação toodelete você deve primeiro remover Olá certificado de quaisquer APIs toouse configurado-lo.

![Confirmar exclusão][api-management-confirm-delete-policy]

## <a name="step2"></a>Configurar toouse uma API um certificado de cliente para autenticação de gateway
Clique em **APIs** de saudação **gerenciamento de API** Olá menu à esquerda, clique em nome de saudação da API de saudação desejada e clique em Olá **segurança** guia.

![Segurança da API][api-management-api-security]

Selecione **certificados de cliente** de saudação **com credenciais** lista suspensa.

![Certificados do cliente][api-management-mutual-certificates]

Selecione Olá certificado desejado na Olá **certificado de cliente** lista suspensa. Se houver vários certificados, você pode examinar o assunto de saudação ou Olá últimos quatro caracteres da impressão digital de saudação conforme observado no certificado correto do hello anterior seção toodetermine hello.

![Selecionar certificado][api-management-select-certificate]

Clique em **salvar** toosave Olá configuração alteração toohello API.

> Essa alteração é imediatamente efetivada e chamadas toooperations essa API usará Olá tooauthenticate de certificado no servidor de back-end de saudação.
> 
> 

![Salvar alterações da API][api-management-save-api]

> Quando um certificado é especificado para autenticação de gateway para o serviço de back-end de saudação de uma API, torna-se parte da política de saudação para essa API e podem ser exibido no editor de diretiva de saudação.
> 
> 

![Política do certificado][api-management-certificate-policy]

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre outra maneiras toosecure seu serviço de back-end, como HTTP autenticação basic ou compartilhada secreta, consulte Olá vídeo a seguir.

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



