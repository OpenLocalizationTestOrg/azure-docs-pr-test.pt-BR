---
title: "Olá aaaUnderstanding do Azure Active Directory Application Manifest | Microsoft Docs"
description: "Cobertura detalhada do manifesto de aplicativo do Active Directory do Azure hello, que representa a configuração de identidade de um aplicativo em um locatário do AD do Azure e é usado toofacilitate autorização de OAuth, experiência de consentimento e muito mais."
services: active-directory
documentationcenter: 
author: sureshja
manager: mbaldwin
editor: 
ms.assetid: 4804f3d4-0ff1-4280-b663-f8f10d54d184
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: sureshja
ms.custom: aaddev
ms.reviewer: elisol
ms.openlocfilehash: 096c9d5501edbfc08731fea670cee559d4442ad1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-azure-active-directory-application-manifest"></a>Noções básicas sobre o manifesto de aplicativo do Active Directory do Azure Olá
Aplicativos que se integram com o Azure AD (Active Directory) devem ser registrados com um locatário do AD do Azure, fornecendo uma configuração persistente de identidade para o aplicativo hello. Essa configuração é consultada em tempo de execução, permitindo cenários que permitem que um aplicativo toooutsource e agente de autenticação/autorização por meio do AD do Azure. Para obter mais informações sobre o modelo de aplicativo de saudação do AD do Azure, consulte Olá [adicionar, atualizar e remover um aplicativo] [ ADD-UPD-RMV-APP] artigo.

## <a name="updating-an-applications-identity-configuration"></a>Atualizando a configuração de identidade de um aplicativo
Na verdade, várias opções estão disponíveis para atualizar as propriedades de saudação na configuração de identidade do aplicativo, que variam em recursos e graus de dificuldade, incluindo Olá seguinte:

* Olá  **[portal do Azure] [ AZURE-PORTAL] interface de usuário da Web** permite que você tooupdate Olá propriedades mais comuns de um aplicativo. Isso é hello mais rápido e menos maneira de propensas a erro de atualização de propriedades do aplicativo, mas não oferecem propriedades tooall de acesso completo, como Olá dois métodos.
* Para cenários mais avançados em que é necessário tooupdate propriedades que não são expostas no hello portal clássico do Azure, você pode modificar Olá **o manifesto do aplicativo**. Este é o foco deste artigo hello e é discutido em mais detalhes, começando na próxima seção, Olá.
* Também é possível muito**escrever um aplicativo que usa Olá [API do Graph] [ GRAPH-API]**  tooupdate seu aplicativo, o que exige Olá maior esforço. Isso pode ser uma opção atraente, se você estiver escrevendo o software de gerenciamento, ou precisar tooupdate propriedades do aplicativo regularmente de forma automática.

## <a name="using-hello-application-manifest-tooupdate-an-applications-identity-configuration"></a>Usando tooupdate de manifesto de aplicativo hello configuração de identidade do aplicativo
Por meio de saudação [portal do Azure][AZURE-PORTAL], você pode gerenciar a configuração de identidade do aplicativo atualizando o manifesto do aplicativo hello usando o editor de manifesto do hello embutido. Você também pode baixar e carregar o manifesto do aplicativo hello como um arquivo JSON. Nenhum arquivo real é armazenado no diretório de saudação. manifesto do aplicativo Hello é simplesmente uma operação HTTP GET na entidade de aplicativo hello Azure AD Graph API e carregamento hello é uma operação HTTP PATCH na entidade de aplicativo hello.

Como resultado, no formato de saudação toounderstand ordem e as propriedades do manifesto de aplicativo hello, você precisará Olá tooreference API do Graph [entidade aplicativos] [ APPLICATION-ENTITY] documentação. Exemplos de atualizações que podem ser executadas através do carregamento do manifesto do aplicativo incluem:

* **Declarar escopos de permissão (oauth2Permissions)** expostos pela sua API Web. Consulte o tópico "TooOther APIs da Web de exposição de aplicativos" Olá [integrando aplicativos com o Active Directory do Azure] [ INTEGRATING-APPLICATIONS-AAD] para obter informações sobre como implementar a representação de usuário usando Olá oauth2Permissions escopo de permissão delegado. Conforme mencionado anteriormente, as propriedades de entidade de aplicativo estão documentadas em Olá Graph API [entidade e o tipo complexo] [ APPLICATION-ENTITY] artigo de referência, incluindo Olá oauth2Permissions propriedade que é um coleção do tipo [OAuth2Permission][APPLICATION-ENTITY-OAUTH2-PERMISSION].
* **Declarar funções de aplicativo (appRoles) expostas pelo seu aplicativo**. Olá, propriedade de appRoles da entidade do aplicativo é uma coleção de tipo [AppRole][APPLICATION-ENTITY-APP-ROLE]. Consulte Olá [controle de acesso em aplicativos de nuvem usando o AD do Azure baseado em função] [ RBAC-CLOUD-APPS-AZUREAD] artigo para obter um exemplo de implementação.
* **Declarar cliente conhecidos aplicativos (knownClientApplications)**, que permite o consentimento de saudação empate toologically de saudação especificado cliente aplicativos toohello recurso/API da web.
* **Solicitação de declaração de associações de grupo do AD do Azure tooissue** para hello (groupMembershipClaims) do usuário conectado.  Isso também pode ser configurado tooissue declarações sobre associações de funções de diretório do usuário hello. Consulte Olá [autorização em aplicativos de nuvem usando grupos do AD] [ AAD-GROUPS-FOR-AUTHORIZATION] artigo para obter um exemplo de implementação.
* **Permitir que a concessão implícita do OAuth 2.0 do aplicativo toosupport** fluxos (oauth2AllowImplicitFlow). Esse tipo de fluxo de concessão é usado com páginas da Web JavaScript ou SPA (Aplicativos de Única Página) inseridos. Para obter mais informações sobre concessão de autorização implícita hello, consulte [Olá Noções básicas sobre implícita do OAuth2 conceder fluxo no Azure Active Directory][IMPLICIT-GRANT].
* **Habilitar o uso do X509 certificados como chave secreta Olá** (keyCredentials). Consulte Olá [compilar aplicativos de serviço e o daemon no Office 365] [ O365-SERVICE-DAEMON-APPS] e [tooauth de guia do desenvolvedor com a API do Gerenciador de recursos do Azure] [ DEV-GUIDE-TO-AUTH-WITH-ARM] artigos para obter exemplos de implementação.
* **Adicionar um novo URI de ID do Aplicativo** para seu aplicativo (identifierURIs[]). URIs de ID de aplicativo são usados toouniquely identificar um aplicativo em seu locatário do AD do Azure (ou em vários locatários do AD do Azure, para cenários de multilocatários qualificado por meio do domínio personalizado verificado). Eles são usados ao solicitar o aplicativo de recurso de tooa de permissões, ou adquirir um token de acesso para um aplicativo de recurso. Quando você atualizar esse elemento, hello mesma atualização é feita servicePrincipalNames [] coleção toohello correspondente da entidade de serviço que reside no locatário inicial do aplicativo hello.

Olá manifesto do aplicativo também fornece uma boa maneira tootrack Olá o estado de seu registro de aplicativo. Porque ele está disponível no formato JSON, a representação de arquivo hello pode ser inserida no seu controle de origem, juntamente com o código-fonte do seu aplicativo.

## <a name="step-by-step-example"></a>Exemplo passo a passo
Agora permite percorrer Olá etapas necessárias tooupdate configuração de identidade do aplicativo por meio de manifesto do aplicativo hello. Vamos destacar uma saudação anterior exemplos, mostrando como toodeclare uma nova permissão de escopo em um aplicativo de recurso:

1. Entrar toohello [portal do Azure][AZURE-PORTAL].
2. Depois que você foi autenticado, escolha seu locatário do AD do Azure, selecionando-Olá parte superior direita da página de saudação.
3. Selecione **Active Directory do Azure** extensão de saudação à esquerda o painel de navegação e clique na **registros do aplicativo**.
4. Localize o aplicativo hello tooupdate na lista de saudação de desejado e clique nele.
5. Na página de aplicativo hello, clique em **manifesto** editor de manifesto tooopen Olá embutido. 
6. Você pode editar diretamente o manifesto hello usando este editor. Observe que manifesto Olá segue o esquema Olá Olá [entidade aplicativos] [ APPLICATION-ENTITY] como mencionamos anteriormente: por exemplo, supondo que queremos tooimplement/expor uma nova permissão chamado "Employees.Read.All" em nosso aplicativo de recurso (API), simplesmente adicione uma coleção de oauth2Permissions novo/segundo elemento toohello, ou seja:
   
        "oauth2Permissions": [
        {
        "adminConsentDescription": "Allow hello application tooaccess MyWebApplication on behalf of hello signed-in user.",
        "adminConsentDisplayName": "Access MyWebApplication",
        "id": "aade5b35-ea3e-481c-b38d-cba4c78682a0",
        "isEnabled": true,
        "type": "User",
        "userConsentDescription": "Allow hello application tooaccess MyWebApplication on your behalf.",
        "userConsentDisplayName": "Access MyWebApplication",
        "value": "user_impersonation"
        },
        {
        "adminConsentDescription": "Allow hello application toohave read-only access tooall Employee data.",
        "adminConsentDisplayName": "Read-only access tooEmployee records",
        "id": "2b351394-d7a7-4a84-841e-08a6a17e4cb8",
        "isEnabled": true,
        "type": "User",
        "userConsentDescription": "Allow hello application toohave read-only access tooyour Employee data.",
        "userConsentDisplayName": "Read-only access tooyour Employee records",
        "value": "Employees.Read.All"
        }
        ],
   
    saudação de entrada deve ser exclusiva e, portanto, você deve gerar um novo globalmente ID exclusiva (GUID) do hello `"id"` propriedade. Nesse caso, pois especificamos `"type": "User"`, essa permissão pode ser tooby consentido qualquer conta autenticada por Olá locatário do AD do Azure na qual Olá aplicativo/API de recursos está registrado. Este concede Olá cliente aplicativo permissão tooaccess-lo em nome da conta de saudação. cadeias de nome de exibição e a descrição Hello são usadas durante a autorização e para exibição no hello portal do Azure.
6. Quando você terminar de atualizar o manifesto de saudação, clique em **salvar** toosave manifesto de saudação.  
   
Agora que hello manifesto é salvo, você pode dar a um cliente registrado aplicativo toohello nova permissão de acesso, adicionamos acima. Neste momento, que você pode usar Olá Web da interface do usuário do portal do Azure em vez de editar o manifesto do aplicativo de cliente hello:  

1. Vá primeiro toohello **configurações** folha de saudação toowhich do aplicativo cliente desejar tooadd acesso toohello nova API, clique em **permissões necessárias** e escolha **selecionar uma API** .
2. Em seguida, você verá com lista de saudação de aplicativos (APIs) do recursos registrados no locatário Olá. Clique em tooselect de aplicativo de recurso hello, ou nome de saudação do tipo da caixa de pesquisa do hello aplicativo hello. Quando encontrar um aplicativo hello, clique em **selecione**.  
3. Isso o levará toohello **selecionar permissões** página, que mostrará Olá lista permissões de aplicativo e permissões delegadas disponíveis para o aplicativo de recurso hello. Selecione Olá nova permissão na ordem tooadd-lista de permissões solicitada pelo cliente toohello. Essa nova permissão será armazenado na configuração de identidade do aplicativo do cliente hello, na propriedade de coleção de "requiredResourceAccess" hello.


É isso. Agora seus aplicativos serão executados usando a nova configuração de identidade.

## <a name="next-steps"></a>Próximas etapas
* Para obter mais detalhes sobre a relação de saudação entre os objetos de aplicativo e entidade de serviço do aplicativo, consulte [objetos de aplicativo e serviço principal no Azure AD][AAD-APP-OBJECTS].
* Consulte Olá [Glossário de desenvolvedor do AD do Azure] [ AAD-DEVELOPER-GLOSSARY] para definições de alguns dos conceitos de desenvolvedor Olá básicos do Azure AD (Active Directory).

. Use a seção de comentários Olá abaixo tooprovide comentários e ajudar a refinar e formatar o nosso conteúdo.

<!--article references -->
[AAD-APP-OBJECTS]: active-directory-application-objects.md
[AAD-DEVELOPER-GLOSSARY]: active-directory-dev-glossary.md
[AAD-GROUPS-FOR-AUTHORIZATION]: http://www.dushyantgill.com/blog/2014/12/10/authorization-cloud-applications-using-ad-groups/
[ADD-UPD-RMV-APP]: active-directory-integrating-applications.md
[APPLICATION-ENTITY]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[APPLICATION-ENTITY-APP-ROLE]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#approle-type
[APPLICATION-ENTITY-OAUTH2-PERMISSION]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permission-type
[AZURE-PORTAL]: https://portal.azure.com
[DEV-GUIDE-TO-AUTH-WITH-ARM]: http://www.dushyantgill.com/blog/2015/05/23/developers-guide-to-auth-with-azure-resource-manager-api/
[GRAPH-API]: active-directory-graph-api.md
[IMPLICIT-GRANT]: active-directory-dev-understanding-oauth2-implicit-grant.md
[INTEGRATING-APPLICATIONS-AAD]: https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
[O365-PERM-DETAILS]: https://msdn.microsoft.com/office/office365/HowTo/application-manifest
[O365-SERVICE-DAEMON-APPS]: https://msdn.microsoft.com/office/office365/howto/building-service-apps-in-office-365
[RBAC-CLOUD-APPS-AZUREAD]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/

