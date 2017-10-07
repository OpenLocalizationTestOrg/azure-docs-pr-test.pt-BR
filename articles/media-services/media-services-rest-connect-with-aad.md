---
title: "aaaUse tooaccess de autenticação do AD do Azure API de serviços de mídia do Azure com REST | Microsoft Docs"
description: "Saiba como tooaccess API de serviços de mídia do Azure com a autenticação do Active Directory do Azure usando REST."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: willzhan;juliako
ms.openlocfilehash: 114f7bdde3a8f5fe6189d712e05b6afdc8a8787a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-ad-authentication-tooaccess-hello-azure-media-services-api-with-rest"></a>Uso do Azure AD authentication tooaccess Olá API de serviços de mídia do Azure com REST

equipe de serviços de mídia do Azure Olá lançou o suporte da autenticação do Azure Active Directory (AD do Azure) para acessar os serviços de mídia do Azure. Ele também anunciou a autenticação do serviço de controle de acesso do Azure planos toodeprecate para acesso de serviços de mídia. Como cada assinatura do Azure e todas as contas de serviços de mídia, locatário anexado tooan AD do Azure, o suporte de autenticação do AD do Azure traz muitos benefícios de segurança. Para obter detalhes sobre essa alteração e a migração (se você usar o SDK do Media Services .NET de saudação para seu aplicativo), consulte o seguinte Olá postagens de blog e artigos:

- [Os Serviços de Mídia do Azure anuncia suporte para o Azure AD e substituição da autenticação de Controle de Acesso](https://azure.microsoft.com/blog/azure%20media%20service%20aad%20auth%20and%20acs%20deprecation)
- [Acessar a API dos Serviços de Mídia do Azure utilizando a autenticação do Azure AD](media-services-use-aad-auth-to-access-ams-api.md)
- [Usar tooaccess de autenticação do AD do Azure API de serviços de mídia do Azure usando o Microsoft .NET](media-services-dotnet-get-started-with-aad.md)
- [Guia de Introdução com a autenticação do AD do Azure usando Olá portal do Azure](media-services-portal-get-started-with-aad.md)

Alguns clientes precisam toodevelop suas soluções de serviços de mídia em Olá restrições a seguir:

*   Eles usam uma linguagem de programação que não seja Microsoft .NET ou c#, ou ambiente de tempo de execução de saudação não é Windows.
*   Bibliotecas do AD do Azure, como bibliotecas de autenticação do Active Directory não estão disponíveis para a linguagem de programação de saudação ou não podem ser usadas para o seu ambiente de tempo de execução.

Alguns clientes desenvolveram aplicativos utilizando API REST tanto para autenticação de Controle de Acesso quanto para acesso aos Serviços de Mídia do Azure. Para esses clientes, você precisará Olá somente uma maneira toouse API REST para autenticação do AD do Azure e acessar os serviços de mídia do Azure subsequentes. Você precisa toonot confiar em qualquer uma das bibliotecas de saudação do AD do Azure ou em Olá SDK do Media Services .NET. Este artigo descreve uma solução e fornece o código de exemplo para esse cenário. Como o código de saudação é todas as chamadas da API REST, sem dependência no nenhum AD do Azure ou biblioteca de serviços de mídia do Azure, o código de saudação pode facilmente ser traduzido tooany outra linguagem de programação.

> [!IMPORTANT]
> Atualmente, os serviços de mídia oferece suporte a modelo de autenticação de serviços de controle de acesso do Azure hello. No entanto, a autenticação de Controle de Acesso será preterida em 1º de junho de 2018. É recomendável que você migre o modelo de autenticação toohello AD do Azure assim que possível.


## <a name="design"></a>Design

Neste artigo, usamos Olá autenticação e autorização de design a seguir:

*  Protocolo de autorização: OAuth 2.0. OAuth 2.0 é um padrão de segurança na Web que abrange a autenticação e autorização. Há suporte pela Microsoft, Google, Facebook e PayPal. Ele foi ratificado em outubro de 2012. A Microsoft suporta firmemente OAuth 2.0 e OpenID Connect. Ambos os padrões são suportados em vários serviços e bibliotecas de clientes, incluindo Azure Active Directory, Open Web Interface para Katana .NET (OWIN) e bibliotecas do Azure AD.
*  Tipo de concessão: tipo de concessão de credenciais do cliente. As credenciais do cliente é um dos tipos de concessão de quatro Olá no OAuth 2.0. Muitas vezes é utilizado para acessar API do Microsoft Azure AD Graph.
*  Modo de autenticação: entidade de serviço. Olá outro modo de autenticação é usuário ou autenticação interativa.

Um total de quatro aplicativos ou serviços estão envolvidos no fluxo de autenticação e autorização de saudação do AD do Azure para usar os serviços de mídia. Olá aplicativos e serviços e fluxo de hello, são descritos na Olá a tabela a seguir:

|Tipo de aplicativo |Aplicativo |Flow|
|---|---|---|
|Cliente | Aplicativo ou solução de cliente | Este aplicativo (na verdade, seu proxy) é registrado no locatário do AD do Azure Olá em qual mídia do Azure de assinatura e Olá Olá residem conta de serviço. Hello entidade de serviço de aplicativo hello registrado é, em seguida, concedida com a função de proprietário ou colaborador em hello controle de acesso (IAM) da conta de serviço de mídia hello. entidade de serviço Olá é representada por Olá aplicativo cliente e ID de segredo do cliente. |
|IDP (Provedor de identidade) | Azure AD como IDP | entidade de serviço de aplicativo registrado Hello (ID do cliente e o segredo do cliente) é autenticada pelo Azure AD como Olá IDP. Essa autenticação é executada internamente e implicitamente. Como o fluxo de credenciais do cliente, o cliente de Olá é autenticado em vez de usuário de saudação. |
|STS (Serviço de Token de Segurança)/servidor OAuth | Azure AD como STS | Após a autenticação por Olá IDP (ou servidor OAuth em termos do OAuth 2.0), um token de acesso ou JSON Web Token (JWT) é emitido pelo AD do Azure como servidor de STS/OAuth para o recurso de camada intermediária do acesso toohello: em nosso caso, Olá ponto de extremidade de API de REST de serviços de mídia. |
|Recurso | API REST dos Serviços de Mídia | Todas as chamadas de API de REST de serviços de mídia é autorizada por um token de acesso que é emitido pelo AD do Azure como STS ou Olá OAuth. |

Se você executar o código de exemplo hello e captura um JWT ou um token de acesso, Olá JWT tem Olá seguintes atributos:

    aud: "https://rest.media.azure.net",

    iss: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",

    iat: 1497146280,

    nbf: 1497146280,
    exp: 1497150180,

    aio: "Y2ZgYDjuy7SptPzO/muf+uRu1B+ZDQA=",

    appid: "02ed1e8e-af8b-477e-af3d-7e7219a99ac6",

    appidacr: "1",

    idp: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",

    oid: "a938cfcc-d3de-479c-b0dd-d4ffe6f50f7c",

    sub: "a938cfcc-d3de-479c-b0dd-d4ffe6f50f7c",

    tid: "72f988bf-86f1-41af-91ab-2d7cd011db47",

Aqui estão os mapeamentos de saudação entre atributos Olá Olá JWT e hello quatro aplicativos ou serviços na saudação anterior da tabela:

|Tipo de aplicativo |Aplicativo |Atributo JWT |
|---|---|---|
|Cliente |Aplicativo ou solução de cliente |appid: "02ed1e8e-af8b-477e-af3d-7e7219a99ac6". ID de saudação do cliente de um aplicativo, você registrará o tooAzure AD na próxima seção, Olá. |
|IDP (Provedor de identidade) | Azure AD como IDP |idp: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/".  Olá GUID é o locatário da ID da Microsoft hello (microsoft.onmicrosoft.com). Cada locatário tem sua própria ID exclusiva. |
|STS (Serviço de Token de Segurança)/servidor OAuth |Azure AD como STS | iss: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/". Olá GUID é o locatário da ID da Microsoft hello (microsoft.onmicrosoft.com). |
|Recurso | API REST dos Serviços de Mídia |aud: "https://rest.media.azure.net". destinatário de saudação ou audiência do token de acesso de saudação. |

## <a name="steps-for-setup"></a>Etapas para configuração

tooregister e configurar um aplicativo do AD do Azure para autenticação do AD do Azure e tooobtain um token de acesso para chamar o ponto de extremidade de API de REST de serviços de mídia do Azure de hello, Olá concluir as etapas a seguir:

1.  Em Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885), registre um locatário de toohello AD do Azure do aplicativo (por exemplo, wzmediaservice) do AD do Azure (por exemplo, microsoft.onmicrosoft.com). Independe se foi registrado como aplicativo Web ou nativo. Além disso, é possível escolher qualquer URL de login e URL de resposta (por exemplo, http://wzmediaservice.com para ambos).
2. Em Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885), vá toohello **configurar** guia de seu aplicativo. Saudação de Observação **ID do cliente**. Em seguida, em **Chaves**, gere uma **chave do cliente** (segredo do cliente). 

    > [!NOTE] 
    > Anote o segredo de saudação do cliente. Não será mostrado novamente.
    
3.  Em Olá [portal do Azure](http://ms.portal.azure.com), vá toohello conta de serviços de mídia. Selecione Olá **controle de acesso** painel (IAM). Adicione um novo membro que tem Olá proprietário ou função de Colaborador hello. Para principal Olá, pesquise o nome do aplicativo hello registrado na etapa 1 (por exemplo, wzmediaservice).

## <a name="info-toocollect"></a>Informações toocollect

tooprepare REST de codificação, coletar Olá tooinclude de pontos de dados no código Olá a seguir:

*   Azure AD como um ponto de extremidade STS: https://login.microsoftonline.com/microsoft.onmicrosoft.com/oauth2/token. A partir deste ponto de extremidade, um token de acesso JWT é solicitado. Além disso tooserving como um IDP, o AD do Azure também serve como um STS. O Azure AD emite um JWT para acesso ao recurso (um token de acesso). Um token JWT tem várias declarações.
*   API REST dos Serviços de Mídia do Azure como recurso ou audiência: https://rest.media.azure.net.
*   ID do cliente: consulte a etapa 2 em[Etapas para configuração](#steps-for-setup).
*   Segredo do cliente: veja o passo 2 em  [Etapas para configuração](#steps-for-setup).
*   Os serviços de mídia da conta do ponto de extremidade de API REST em Olá formato a seguir:

    https://[media_service_account_name].restv2.[data_center].media.azure.net/API 

    Este é o ponto de extremidade de saudação em relação a quais API REST do Media Services todas as chamadas em seu aplicativo são feitas. Por exemplo, https://willzhanmswjapan.restv2.japanwest.media.azure.net/API.

Você pode colocar esses cinco parâmetros em seu arquivo App. config ou Web. config, toouse em seu código.

## <a name="sample-code"></a>Exemplo de código

Você pode encontrar o código de exemplo hello [autenticação do AD do Azure para acesso de serviços de mídia do Azure: tanto por meio da API REST](https://github.com/willzhan/WAMSRESTSoln).

o código de exemplo Hello tem duas partes:

*   Um projeto de biblioteca DLL que tem todos os códigos de API REST Olá para autenticação e autorização do Azure AD. Ele também tem um método para fazer a API REST chamadas toohello API REST do Media Services ponto de extremidade, com o token de acesso de saudação.
*   Um cliente de teste de console que inicia a autenticação do Azure AD e chama diferentes API REST de Serviços de Mídia.

projeto de exemplo Hello tem três recursos:

*   Autenticações de AD do Azure por meio de credenciais de cliente Olá conceder usando Olá API REST.
*   Acesso de serviços de mídia do Azure usando Olá API REST.
*   Acesso de armazenamento do Azure usando apenas Olá API REST (como toocreate usada uma conta de serviços de mídia, usando a API REST).


## <a name="where-is-hello-refresh-token"></a>Onde está o token de atualização Olá?

Alguns leitores podem solicitar: onde está o token de atualização Olá? Por que não utilizar um token de atualização aqui?

finalidade de saudação de um token de atualização não é toorefresh um token de acesso. Em vez disso, é projetado toobypass intervenção do usuário ou autenticação do usuário final e ainda obter um token de acesso válido quando um token anterior expira. Um nome melhor para um token de atualização pode ser algo como "token de re-entada de usuário de bypass."

Se você usar o hello (nome de usuário e senha, atuar em nome do usuário) de fluxo de concessão de autorização do OAuth 2.0, um token de atualização ajuda a obter acesso a um renovado token sem solicitar a intervenção do usuário. No entanto, para Olá OAuth 2.0 que descrevemos neste artigo fluxo de concessão de credenciais do cliente, cliente Olá atua em seu próprio nome. Intervenção do usuário não é necessário em todos os, e o servidor de autorização Olá não precisa muito (e não) fornecem um token de atualização. Se você depurar Olá **GetUrlEncodedJWT** método, observe que a resposta de saudação do ponto de extremidade token Olá tem um token de acesso, mas nenhum token de atualização.

## <a name="next-steps"></a>Próximas etapas

Introdução ao [carregando arquivos tooyour conta](media-services-dotnet-upload-files.md).
