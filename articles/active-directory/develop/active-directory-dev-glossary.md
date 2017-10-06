---
title: "Glossário de desenvolvedor do Active Directory de aaaAzure | Microsoft Docs"
description: "Uma lista de termos referentes a conceitos e recursos de desenvolvedor do Azure Active Directory usados com frequência."
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 551512df-46fb-4219-a14b-9c9fc23998ba
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 32a6a6194b8d01409159a2b60263bb66a87a843c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-developer-glossary"></a>Glossário de desenvolvedor do Azure Active Directory
Este artigo contém definições para algumas das Olá conceitos fundamentais do Azure AD (Active Directory) developer, que são úteis para aprender sobre o desenvolvimento de aplicativos do AD do Azure.

## <a name="access-token"></a>o token de acesso
Um tipo de [token de segurança](#security-token) emitido por uma [servidor de autorização](#authorization-server)e usado por um [aplicativo cliente](#client-application) em ordem tooaccess um [servidor de recurso protegido ](#resource-server). Normalmente na forma de saudação de um [JSON Web Token (JWT)][JWT], token Olá incorpora autorização Olá concedida cliente toohello por Olá [proprietário do recurso](#resource-owner), para um nível solicitado de acesso. Olá token contém todos os aplicável [declarações](#claim) sobre assunto hello, habilitando o Olá toouse de aplicativo de cliente-o como uma forma de credenciais ao acessar um determinado recurso. Isso também elimina a necessidade de saudação de cliente de toohello Olá recurso proprietário tooexpose credenciais.

Tokens de acesso às vezes são chamados tooas "Aplicativo + usuário" ou "Somente de aplicativo", dependendo da saudação credenciais que está sendo representado. Por exemplo, quando um aplicativo cliente usa:

* [Concessão de autorização de "Código de autorização"](#authorization-grant), usuário final de saudação autentica primeiro como proprietário do recurso hello, delegar autorização toohello tooaccess cliente Olá recursos. Olá autentica posteriormente ao obter token de acesso de saudação. token Olá às vezes pode ser chamado toomore especificamente como um token de "Usuário + aplicativo", pois ambos os usuário Olá que aplicativo de cliente hello e aplicativo hello autorizados representa.
* [Concessão de autorização "As credenciais do cliente"](#authorization-grant)cliente Olá fornece autenticação única hello, funcionando sem autenticação/autorização Olá-do proprietário do recurso, portanto token hello, às vezes, pode ser chamado tooas um token de "Somente de aplicativo".

Veja [Referência de token do Azure AD][AAD-Tokens-Claims] para saber mais.

## <a name="application-manifest"></a>manifesto do aplicativo
Um recurso fornecido pelo Olá [portal do Azure][AZURE-portal], que produz uma representação JSON de configuração de identidade do aplicativo hello, usada como um mecanismo para atualizar seus associados [ Aplicativo] [ AAD-Graph-App-Entity] e [ServicePrincipal] [ AAD-Graph-Sp-Entity] entidades. Consulte [o manifesto do aplicativo do Azure Active Directory Noções básicas sobre Olá] [ AAD-App-Manifest] para obter mais detalhes.

## <a name="application-object"></a>objeto de aplicativo
Quando você registra/atualiza um aplicativo hello [portal do Azure][AZURE-portal], Olá cria/atualizações do portal correspondente e um objeto de aplicativo [objeto principal do serviço](#service-principal-object)para esse locatário. objeto de aplicativo Hello *define* Olá configuração de identidade do aplicativo global (entre todos os locatários em que ele tenha acesso), fornecendo um modelo do qual seus objetos principal do serviço correspondente são  *derivado* para uso localmente em tempo de execução (em um locatário específico).

Veja [Objetos de aplicativo e entidade de serviço][AAD-App-SP-Objects] para saber mais.

## <a name="application-registration"></a>registro de aplicativo
Em ordem tooallow um aplicativo toointegrate com e delegado funções de gerenciamento de identidades e acesso tooAzure AD, ele deve ser registrado com o AD do Azure [locatário](#tenant). Quando você registra seu aplicativo com o AD do Azure, você está fornecendo uma configuração de identidade para seu aplicativo, permitindo que ele toointegrate com o Azure AD e usa recursos como:

* Gerenciamento robusto de Logon Único usando o Gerenciamento de Identidade do Azure AD e a implementação de protocolo [OpenID Connect][OpenIDConnect]
* Orientadas acesso muito[recursos protegidos](#resource-server) por [aplicativos cliente](#client-application), por meio OAuth 2.0 do AD do Azure [servidor de autorização](#authorization-server) implementação
* [Estrutura de consentimento](#consent) para gerenciar recursos de tooprotected de acesso de cliente, com base na autorização do proprietário do recurso.

Veja [Integrando aplicativos com o Azure Active Directory][AAD-Integrating-Apps] para saber mais.

## <a name="authentication"></a>Autenticação
ato de Olá verifica se um participante para credenciais legítimas, fornecendo a base de saudação para a criação de um toobe principal de segurança usado para controle de acesso e identidade. Durante uma [concessão de autorização de OAuth2](#authorization-grant) por exemplo, parte Olá autenticando atende a função de saudação do [proprietário do recurso](#resource-owner) ou [aplicativo cliente](#client-application), dependendo da concessão de saudação usado.

## <a name="authorization"></a>autorização
ato de saudação de conceder um toodo de permissão principal de segurança autenticada algo. Há dois casos de uso principal no modelo de programação do hello AD do Azure:

* Durante uma [concessão de autorização de OAuth2](#authorization-grant) fluxo: hello quando [proprietário do recurso](#resource-owner) concede autorização toohello [aplicativo cliente](#client-application), permitindo que os clientes Olá Olá tooaccess recursos do proprietário do recurso.
* Durante o acesso a recursos pelo cliente Olá: conforme implementado pela Olá [servidor recurso](#resource-server), usando Olá [declaração](#claim) valores presentes em Olá [token de acesso](#access-token) toomake o controle de acesso decisões com base em-los.

## <a name="authorization-code"></a>código de autorização
Uma breve viver "token" fornecido tooa [aplicativo cliente](#client-application) por Olá [ponto de extremidade de autorização](#authorization-endpoint), como parte do fluxo de "código de autorização" Olá, um dos Olá quatro OAuth2 [concessões de autorização ](#authorization-grant). código de saudação é retornado toohello aplicativo de cliente em tooauthentication de resposta de um [proprietário do recurso](#resource-owner), indicando que o proprietário do recurso Olá delegou Olá de tooaccess autorização solicitado recursos. Como parte do fluxo de hello, código hello mais tarde é trocado por um [token de acesso](#access-token).

## <a name="authorization-endpoint"></a>ponto de extremidade de autorização
Um dos pontos de extremidade Olá implementados pelo Olá [servidor de autorização](#authorization-server), usado toointeract com hello [proprietário do recurso](#resource-owner) em ordem tooprovide um [concessão de autorização](#authorization-grant) durante um fluxo de concessão de autorização OAuth2. Dependendo da autorização Olá fluxo de concessão usado, Olá real grant fornecido pode variar, incluindo um [código de autorização](#authorization-code) ou [token de segurança](#security-token).

Consulte a especificação de saudação OAuth2 [tipos de concessão de autorização] [ OAuth2-AuthZ-Grant-Types] e [ponto de extremidade de autorização] [ OAuth2-AuthZ-Endpoint] seções e Olá [Especificação OpenIDConnect] [ OpenIDConnect-AuthZ-Endpoint] para obter mais detalhes.

## <a name="authorization-grant"></a>concessão de autorização
Uma credencial que representa Olá [do proprietário do recurso](#resource-owner) [autorização](#authorization) tooaccess seus recursos protegidos, concedidos tooa [aplicativo cliente](#client-application). Um aplicativo cliente pode usar um dos Olá [quatro conceder tipos definidos pelo Olá estrutura de autorização OAuth2] [ OAuth2-AuthZ-Grant-Types] tooobtain grant, dependendo do tipo/requisitos do cliente: "concessão de código de autorização", " concessão de credenciais do cliente","concessão implícita"e"concessão de credenciais de senha de proprietário do recurso". credencial Olá retornado toohello cliente é um [token de acesso](#access-token), ou um [código de autorização](#authorization-code) (trocadas posteriormente para um token de acesso), dependendo do tipo de saudação de concessão de autorização usado.

## <a name="authorization-server"></a>servidor de autorização
Conforme definido pelo Olá [estrutura de autorização OAuth2][OAuth2-Role-Def], responsável pela emissão de acesso do servidor de saudação tokens toohello [cliente](#client-application) depois de autenticar com êxito Olá [proprietário do recurso](#resource-owner) e obter sua autorização. Um [aplicativo cliente](#client-application) interage com o servidor de autorização de saudação em tempo de execução por meio de seu [autorização](#authorization-endpoint) e [token](#token-endpoint) pontos de extremidade, conforme Olá OAuth2 definido [concessões de autorização](#authorization-grant).

No caso de saudação de integração de aplicativos do AD do Azure, o AD do Azure implementa função de servidor de autorização Olá para aplicativos do Azure AD e o serviço Microsoft APIs, por exemplo [Microsoft Graph APIs][Microsoft-Graph].

## <a name="claim"></a>declaração
Um [token de segurança](#security-token) contém declarações, que fornecem declarações sobre uma entidade (como um [aplicativo cliente](#client-application) ou [proprietário do recurso](#resource-owner)) tooanother entidade (por exemplo, Olá [server resource](#resource-server)). Declarações são pares de nome/valor que fatos sobre o assunto do token Olá de retransmissão (por exemplo, Olá entidade de segurança foi autenticada pelo Olá [servidor de autorização](#authorization-server)). Olá declarações presentes em um token de determinado variam de acordo com diversas variáveis, incluindo tipo de saudação do token, tipo de saudação da credencial usada tooauthenticate Olá assunto, configuração de aplicativo hello, etc.

Veja [Referência de token do Azure AD][AAD-Tokens-Claims] para saber mais.

## <a name="client-application"></a>aplicativo cliente
Conforme definido pelo Olá [estrutura de autorização OAuth2][OAuth2-Role-Def], protegidos de um aplicativo que faz solicitações de recursos em nome hello [proprietário do recurso](#resource-owner). termo Hello "cliente" não significa que qualquer características de implementação de hardware específica (por exemplo, se o aplicativo hello executa em um servidor, uma área de trabalho ou outros dispositivos).  

Um aplicativo cliente solicita [autorização](#authorization) de um tooparticipate de proprietário do recurso em um [concessão de autorização OAuth2](#authorization-grant) fluxo e podem acessar APIs/dados em nome do proprietário do recurso de saudação. Olá estrutura de autorização OAuth2 [define dois tipos de clientes][OAuth2-Client-Types], "confidencial" e "public", com base na confidencialidade de saudação de toomaintain do cliente Olá capacidade de suas credenciais. Os aplicativos podem implementar um [cliente Web (confidencial)](#web-client) que é executado em um servidor Web, um [cliente nativo (público)](#native-client) instalado em um dispositivo ou um [cliente baseado em agente de usuário (público)](#user-agent-based-client) que é executado no navegador do dispositivo.

## <a name="consent"></a>consentimento
Olá o processo de um [proprietário do recurso](#resource-owner) conceder autorização tooa [aplicativo cliente](#client-application), tooaccess protegido recursos específicos [permissões](#permissions), em nome de saudação proprietário do recurso. Dependendo das permissões Olá solicitadas pelo cliente hello, um administrador ou usuário deverá para dados de organização/individuais do consentimento tooallow acesso tootheir respectivamente. Observe que, em um [multilocatário](#multi-tenant-application) cenário, o aplicativo de hello [entidade de serviço](#service-principal-object) também é registrado no locatário de saudação do usuário de consentimento hello.

## <a name="id-token"></a>token de ID
Um [OpenID Connect] [ OpenIDConnect-ID-Token] [token de segurança](#security-token) fornecido por um [do servidor de autorização](#authorization-server) [dopontodeextremidadedeautorização](#authorization-endpoint), que contém [declarações](#claim) pertencentes a toohello autenticação de um usuário final [proprietário do recurso](#resource-owner). Assim como um token de acesso, os tokens de ID também são representados como um [JWT (Token Web JSON)][JWT] assinado digitalmente. Ao contrário de um token de acesso, declarações de um token de ID não são usadas para fins relacionados tooresource acesso e controle de acesso especificamente.

Veja [Referência de token do Azure AD][AAD-Tokens-Claims] para saber mais.

## <a name="multi-tenant-application"></a>Aplicativos multilocatários
Uma classe de aplicativo que permite entrar e [consentimento](#consent) por usuários provisionados no nenhum AD do Azure [locatário](#tenant), incluindo locatários diferentes Olá um onde saudação do cliente é registrada. [Cliente nativo](#native-client) vários locatários por padrão, os aplicativos são enquanto [cliente web](#web-client) e [web API/recursos](#resource-server) aplicativos têm Olá capacidade tooselect entre único ou vários locatários. Por outro lado, um aplicativo web registrado como um único locatário, permitir somente entradas de contas de usuário provisionadas no hello mesmo locatário como Olá um onde o aplicativo hello é registrado.

Consulte [como toosign em qualquer usuário do AD do Azure usando Olá padrão de aplicativo multilocatário] [ AAD-Multi-Tenant-Overview] para obter mais detalhes.

## <a name="native-client"></a>cliente nativo
Um tipo de [aplicativo cliente](#client-application) que é instalado de forma nativa em um dispositivo. Como todo o código é executado em um dispositivo, ele é considerado um "public" cliente devido tooits dificuldades toostore credenciais em particular/confidencialidade. Veja [Perfis e tipos de cliente OAuth2][OAuth2-Client-Types] para saber mais.

## <a name="permissions"></a>permissões
Um [aplicativo cliente](#client-application) ganhos acessar tooa [servidor recurso](#resource-server) declarando solicitações de permissão. Dois tipos estão disponíveis:

* "Permissões", que especificam [com base em escopo](#scopes) usando o acesso delegado a autorização de saudação conectado [proprietário do recurso](#resource-owner), são apresentados os recursos de toohello em tempo de execução como ["scp "declarações](#claim) no cliente de saudação [token de acesso](#access-token).
* Permissões de "Aplicativo", que especifiquem [baseada em função](#roles) acessar usando as credenciais/identidade do aplicativo do cliente hello, são apresentados os recursos de toohello em tempo de execução como [declarações "funções"](#claim) em Olá token de acesso do cliente.

Eles também superfície durante a saudação [consentimento](#consent) processo, oferecendo Olá administrador ou o recurso proprietário Olá oportunidade toogrant/negar Olá tooresources de acesso de cliente em seu locatário.

Solicitações de permissão são configuradas no hello "Aplicativos" / guia "Configurações" hello [portal do Azure][AZURE-portal], em "Permissões necessárias", selecionando Olá desejado "Permissões delegadas" e " Permissões do aplicativo"(Olá último requer associação na função de Administrador Global de saudação). Porque um [cliente público](#client-application) com segurança não pode manter as credenciais, ela só pode solicitar permissões delegadas, enquanto um [cliente confidencial](#client-application) tem Olá capacidade toorequest delegado e de aplicativos permissões. do cliente Olá [objeto application](#application-object) repositórios Olá declarado permissões em seu [requiredResourceAccess propriedade][AAD-Graph-App-Entity].

## <a name="resource-owner"></a>proprietário do recurso
Conforme definido pelo Olá [estrutura de autorização OAuth2][OAuth2-Role-Def], recurso protegido de uma entidade com a capacidade de conceder acesso tooa. Quando o proprietário do recurso de saudação é uma pessoa, é chamado tooas um usuário final. Por exemplo, quando um [aplicativo cliente](#client-application) quer tooaccess caixa de correio do usuário por meio de saudação [Microsoft Graph API][Microsoft-Graph], ele requer a permissão do proprietário do recurso de saudação do caixa de correio Hello.

## <a name="resource-server"></a>servidor de recursos
Conforme definido pelo Olá [estrutura de autorização OAuth2][OAuth2-Role-Def], um servidor que hospeda recursos protegidos, capazes de aceitar e responder tooprotected recurso solicitações [cliente aplicativos](#client-application) que apresentar um [token de acesso](#access-token). Também conhecido como um servidor de recursos protegidos ou aplicativo de recurso.

Um servidor de recursos expõe APIs e impõe a acessar os recursos tooits protegidos por meio de [escopos](#scopes) e [funções](#roles), usando Olá a estrutura de autorização do OAuth 2.0. Os exemplos incluem hello Azure AD Graph API, que fornece dados do access tooAzure AD locatário e Olá APIs do Office 365 que fornecem acesso toodata como o email e o calendário. Ambos também podem ser acessados pelo Olá [Microsoft Graph API][Microsoft-Graph].  

Assim como um aplicativo cliente, configuração de identidade do aplicativo de recurso é estabelecida via [registro](#application-registration) em um locatário do AD do Azure, fornecendo o aplicativo hello e o objeto de entidade de serviço. Algumas APIs fornecidas pela Microsoft, como hello Azure AD Graph API, tem registrado previamente disponibilizadas em todos os locatários durante o provisionamento de entidades de serviço.

## <a name="roles"></a>roles
Como [escopos](#scopes), funções fornecem uma maneira para um [servidor recurso](#resource-server) toogovern tooits de acesso protegido recursos. Há dois tipos: uma função de "usuário" implementa o controle de acesso baseado em função para os usuários/grupos que exigem acesso toohello recursos, enquanto que implementa uma função de "aplicativo" hello mesmo para [aplicativos cliente](#client-application) que requerem acesso.

Funções são definidas pelo recurso de cadeias de caracteres (por exemplo "aprovador de despesas," "Somente leitura", "Directory.ReadWrite.All"), gerenciado no hello [portal do Azure] [ AZURE-portal] por meio do recurso de saudação [aplicativo manifesto](#application-manifest)e armazenados no recurso de saudação [appRoles propriedade][AAD-Graph-Sp-Entity]. Olá portal do Azure é também usado tooassign usuários muito funções de "usuário" e configurar o cliente [permissões de aplicativo](#permissions) tooaccess uma função de "aplicativo".

Para obter uma discussão detalhada sobre as funções de aplicativo hello expostos pela API do Graph do AD do Azure, consulte [escopos de permissão de API do Graph][AAD-Graph-Perm-Scopes]. Para obter um exemplo de implementação passo a passo, veja [Controle de acesso com base em função em aplicativos de nuvem usando o Azure AD][Duyshant-Role-Blog].

## <a name="scopes"></a>escopos
Como [funções](#roles), escopos fornecem uma maneira para um [servidor recurso](#resource-server) toogovern tooits de acesso protegido recursos. Escopos são usada tooimplement [com base em escopo] [ OAuth2-Access-Token-Scopes] controle de acesso, para um [aplicativo cliente](#client-application) que tem acesso delegado toohello recurso pelo seu proprietário.

Escopos são definidas pelo recurso de cadeias de caracteres (por exemplo "Mail.Read", "Directory.ReadWrite.All"), gerenciados no hello [portal do Azure] [ AZURE-portal] por meio do recurso de saudação [manifesto do aplicativo](#application-manifest)e armazenados no recurso de saudação [oauth2Permissions propriedade][AAD-Graph-Sp-Entity]. Olá portal do Azure é também usado tooconfigure aplicativo cliente [permissões delegadas](#permissions) tooaccess um escopo.

Uma convenção de nomenclatura de prática recomendada, é toouse um formato "assumem". Para obter uma discussão detalhada dos escopos Olá expostos pela API do Graph do AD do Azure, consulte [escopos de permissão de API do Graph][AAD-Graph-Perm-Scopes]. Para escopos expostos por serviços do Office 365, veja [Referência de permissões de API do Office 365][O365-Perm-Ref].

## <a name="security-token"></a>token de segurança
Um documento assinado que contém declarações, como um token OAuth2 ou uma asserção SAML 2.0. Uma [concessão de autorização](#authorization-grant) OAuth2, um [token de acesso](#access-token) (OAuth2) e um [Token de ID](http://openid.net/specs/openid-connect-core-1_0.html#IDToken) são tipos de tokens de segurança, que são implementados como um [JWT (Token Web JSON)][JWT].

## <a name="service-principal-object"></a>objeto de entidade de serviço
Quando você registra/atualiza um aplicativo hello [portal do Azure][AZURE-portal], cria/atualizações do portal Olá ambos um [objeto application](#application-object) e uma entidade de serviço correspondente objeto de locatário. objeto de aplicativo Hello *define* Olá globalmente (em todos os locatários onde aplicativo hello associado recebeu acesso), a configuração de identidade do aplicativo e é o modelo de saudação do qual seu serviço correspondente objetos principais são *derivado* para uso localmente em tempo de execução (em um locatário específico).

Veja [Objetos de aplicativo e entidade de serviço][AAD-App-SP-Objects] para saber mais.

## <a name="sign-in"></a>entrada
Olá o processo de um [aplicativo cliente](#client-application) iniciando a autenticação do usuário final e captura relacionados ao estado para finalidade de saudação de aquisição de um [token de segurança](#security-token) e toothat de sessão do aplicativo hello de escopo estado. O estado pode incluir artefatos, como informações de perfil de usuário, e informações derivadas de declarações de token.

função entrada Hello de um aplicativo é geralmente usado tooimplement single-sign-on (SSO). Ele também pode ser precedido por uma função "inscrição", como ponto de entrada hello para um aplicativo de tooan de acesso do usuário final toogain (após entrar pela primeira vez). Hello inscrição função é usada toogather e manter o usuário de toohello específico de estado adicionais e pode exigir [consentimento do usuário](#consent).

## <a name="sign-out"></a>saída
Olá processo de autenticação sem um usuário final, desanexar o estado do usuário Olá associado Olá [aplicativo cliente](#client-application) sessão durante [entrar](#sign-in)

## <a name="tenant"></a>locatário
Uma instância de um diretório do AD do Azure é chamado tooas um locatário do AD do Azure. Ela fornece uma variedade de recursos, incluindo:

* um serviço de registro para aplicativos integrados
* autenticação de contas de usuário e aplicativos registrados
* Pontos de extremidade REST necessário toosupport vários protocolos, incluindo OAuth2 e SAML, incluindo Olá [ponto de extremidade de autorização](#authorization-endpoint), [ponto de extremidade token](#token-endpoint) e hello "comum" ponto de extremidade usado pelo [ aplicativos de multilocação](#multi-tenant-application).

Um locatário também é associado um AD do Azure ou assinatura do Office 365 durante o provisionamento de assinatura hello, fornecendo recursos de gerenciamento de acesso e identidade para assinatura de saudação. Consulte [como tooget um Active Directory do Azure locatário] [ AAD-How-To-Tenant] para obter detalhes sobre a saudação de várias maneiras que você pode obter acesso tooa locatário. Consulte [assinaturas do Azure como estão associadas com o Azure Active Directory] [ AAD-How-Subscriptions-Assoc] para obter detalhes sobre a relação de saudação entre assinaturas e um locatário do AD do Azure.

## <a name="token-endpoint"></a>ponto de extremidade de token
Um dos pontos de extremidade Olá implementados pelo Olá [servidor de autorização](#authorization-server) toosupport OAuth2 [concessões de autorização](#authorization-grant). Dependendo da saudação grant, pode ser usado tooacquire um [token de acesso](#access-token) (e relacionados token "atualização") tooa [cliente](#client-application), ou [token de ID](#ID-token) quando usado com hello [ OpenID Connect] [ OpenIDConnect] protocolo.

## <a name="user-agent-based-client"></a>Cliente com base em agente de usuário
Um tipo de [aplicativo cliente](#client-application) que baixa código de um servidor Web e é executado em um agente de usuário (por exemplo, um navegador da Web), como um SPA (Aplicativo de Página Única). Como todo o código é executado em um dispositivo, ele é considerado um "public" cliente devido tooits dificuldades toostore credenciais em particular/confidencialidade. Veja [Perfis e tipos de cliente OAuth2][OAuth2-Client-Types] para saber mais.

## <a name="user-principal"></a>entidade de usuário
Modo de toohello semelhante que um objeto de entidade de serviço é usado toorepresent uma instância de aplicativo, um objeto de entidade de segurança do usuário é outro tipo de entidade de segurança, que representa um usuário. saudação do Azure AD Graph [entidade usuário] [ AAD-Graph-User-Entity] define o esquema de saudação para um objeto de usuário, incluindo as propriedades relacionadas ao usuário, como nome e sobrenome, nome principal do usuário, associação à função de diretório, etc. Isso fornece a configuração de identidade de usuário Olá para AD do Azure tooestablish um usuário principal em tempo de execução. Olá, principal do usuário é usado toorepresent um usuário autenticado para o logon único, gravando [consentimento](#consent) delegação, tornando as decisões de controle de acesso, etc.

## <a name="web-client"></a>cliente Web
Um tipo de [aplicativo cliente](#client-application) que executa todo o código em um servidor web e capaz de toofunction como um cliente "confidencial" por armazenar suas credenciais com segurança no servidor de saudação. Veja [Perfis e tipos de cliente OAuth2][OAuth2-Client-Types] para saber mais.

## <a name="next-steps"></a>Próximas etapas
Olá [guia do desenvolvedor do AD do Azure] [ AAD-Dev-Guide] é Olá toouse de portal para todo o desenvolvimento do AD do Azure relacionados tópicos, incluindo uma visão geral de [integração de aplicativos] [ AAD-How-To-Integrate] e conceitos básicos de saudação de [autenticação do AD do Azure e cenários de autenticação com suporte][AAD-Auth-Scenarios].

Use Olá comentários de tooprovide seção comentários a seguir e ajudar a refinar e formatar nosso conteúdo, incluindo solicitações de novas definições ou atualizar registros existentes!

<!--Image references-->

<!--Reference style links -->
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AAD-Graph-User-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity
[AAD-How-Subscriptions-Assoc]: ../active-directory-how-subscriptions-associated-directory.md
[AAD-How-To-Integrate]: ./active-directory-how-to-integrate.md
[AAD-How-To-Tenant]: active-directory-howto-tenant.md
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Multi-Tenant-Overview]: active-directory-devhowto-multi-tenant-overview.md
[AAD-Security-Token-Claims]: ./active-directory-authentication-scenarios/#claims-in-azure-ad-security-tokens
[AAD-Tokens-Claims]: ./active-directory-token-and-claims.md
[AZURE-portal]: https://portal.azure.com
[Duyshant-Role-Blog]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/
[JWT]: https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32
[Microsoft-Graph]: https://graph.microsoft.io
[O365-Perm-Ref]: https://msdn.microsoft.com/en-us/office/office365/howto/application-manifest
[OAuth2-Access-Token-Scopes]: https://tools.ietf.org/html/rfc6749#section-3.3
[OAuth2-AuthZ-Endpoint]: https://tools.ietf.org/html/rfc6749#section-3.1
[OAuth2-AuthZ-Grant-Types]: https://tools.ietf.org/html/rfc6749#section-1.3
[OAuth2-Client-Types]: https://tools.ietf.org/html/rfc6749#section-2.1
[OAuth2-Role-Def]: https://tools.ietf.org/html/rfc6749#page-6
[OpenIDConnect]: http://openid.net/specs/openid-connect-core-1_0.html
[OpenIDConnect-AuthZ-Endpoint]: http://openid.net/specs/openid-connect-core-1_0.html#AuthorizationEndpoint
[OpenIDConnect-ID-Token]: http://openid.net/specs/openid-connect-core-1_0.html#IDToken
