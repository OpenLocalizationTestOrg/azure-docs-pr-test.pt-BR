---
title: aaaHow tooconfigure um aplicativo de Proxy de aplicativo | Microsoft Docs
description: Saiba como toocreate um configurar um aplicativo de Proxy de aplicativo em algumas etapas simples
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
ms.openlocfilehash: c64019098fc124e4fe10b8288830bcd2b7239d3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application"></a>Como tooconfigure um aplicativo de Proxy de aplicativo

Este artigo ajuda toounderstand como tooconfigure um aplicativo de Proxy de aplicativo no AD do Azure tooexpose seu toohello de aplicativos local nuvem.

## <a name="recommended-documents"></a>Documentos recomendados 

toolearn sobre configurações iniciais hello e criação de um aplicativo de Proxy de aplicativo por meio do Portal de administração de saudação siga Olá [publicar aplicativos usando o Proxy de aplicativo do Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).

Para obter detalhes sobre como configurar conectores, consulte [habilitar Proxy de aplicativo no portal do Azure de saudação](active-directory-application-proxy-enable.md).

Para obter informações sobre como carregar certificados e usar domínios personalizados, consulte [trabalhando com domínios personalizados no Application Proxy do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).

## <a name="create-hello-applicationsetting-hello-urls"></a>Criar hello URLs de saudação de configuração do aplicativo

Se você estiver seguindo as etapas em Olá Olá [publicar aplicativos usando o Proxy de aplicativo do Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentação e estão obtendo um erro ao criar o aplicativo hello, consulte detalhes do erro Olá para obter informações e sugestões para aplicativo de hello toofix. A maioria das mensagens de erro incluem uma correção sugerida. erros comuns de tooavoid, verifique se:

-   Você é um administrador com permissão toocreate um aplicativo de Proxy de aplicativo

-   URL interna Olá é exclusivo

-   URL externa de saudação é exclusivo

-   Olá início URLs com http ou https e terminar com um "/"

-   Olá URL deve ser um nome de domínio, não um endereço IP

mensagem de erro de saudação deve exibir no canto superior direito da saudação quando você cria o aplicativo hello. Você também pode selecionar as mensagens de erro de Olá Olá notificação ícone toosee.

   ![Prompt de notificação](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a>Configurar grupos de conectores/conectores

Se você estiver tendo dificuldades para configurar seu aplicativo por causa de aviso sobre conectores hello e grupos de conector, consulte as instruções sobre como habilitar o Proxy de aplicativo para obter detalhes sobre como conectores toodownload. Se você quiser toolearn mais sobre conectores, consulte Olá [documentação conectores](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).

Se os conectores estão inativos, isso significa que eles são o serviço de saudação tooreach não é possível. Isso geralmente é porque todas as portas de saudação necessários não estiverem abertas. toosee uma lista de portas necessárias, consulte seção pré-requisitos Olá Olá habilitando a documentação do Proxy de aplicativo.

## <a name="upload-certificates-for-custom-domains"></a>Carregar certificados para domínios personalizados

Domínios personalizados permitem que você toospecify domínio Olá suas URLs externas. toouse de domínios personalizados, você precisa de tooupload Olá certificado para esse domínio. Para obter informações sobre como usar domínios personalizados e certificados, consulte [trabalhando com domínios personalizados no Application Proxy do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains). 

Se você estiver encontrando problemas ao carregar o certificado, procure por mensagens de erro Olá no portal de saudação para obter informações adicionais sobre o problema de saudação com certificado de saudação. Problemas de certificado comuns incluem:

-   Certificado expirado

-   O certificado é auto-assinado

-   Certificado está faltando a chave privada Olá

exibição de mensagem de erro Olá no hello canto superior direito, tente o certificado de saudação tooupload. Você também pode selecionar as mensagens de erro de Olá Olá notificação ícone toosee.

   ![Prompt de notificação](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a>Próximas etapas
[Publicar aplicativos usando o Proxy de Aplicativo do AD do Azure](application-proxy-publish-azure-portal.md)
