---
title: recursos de modelo de gerenciamento de API aaaAzure | Microsoft Docs
description: "Saiba mais sobre os tipos de saudação de recursos disponíveis para uso em modelos de portal do desenvolvedor no gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 51a1b4c6-a9fd-4524-9e0e-03a9800c3e94
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2221e3852986d485d13817b483e473dfe451d3c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-template-resources"></a>Recursos de modelo no Gerenciamento de API do Azure
Gerenciamento de API do Azure fornece Olá seguintes tipos de recursos para uso em modelos portal do desenvolvedor hello.  
  
-   [Recursos de cadeia de caracteres](#strings)  
  
-   [Recursos de glifo](#glyphs)  
  
##  <a name="strings"></a> Recursos de cadeia de caracteres  
 API de gerenciamento fornece um conjunto abrangente de recursos de cadeia de caracteres para uso no portal do desenvolvedor hello. Esses recursos estão disponíveis em todos os idiomas de saudação suportados pelo gerenciamento de API. conjunto de modelos padrão de saudação utiliza esses recursos para cadeias de caracteres constantes que são exibidas no portal do desenvolvedor hello, rótulos e cabeçalhos de página. toouse um recurso de cadeia de caracteres em seus modelos, forneça o prefixo de cadeia de caracteres de recurso Olá seguido pelo nome da cadeia de caracteres de saudação, conforme mostrado no exemplo a seguir de saudação.  
  
```  
{% localized "Prefix|Name" %}  
  
```  
  
 Olá exemplo a seguir é a partir do modelo de lista do produto hello e exibe **produtos** na parte superior de saudação da página de saudação.  
  
```  
<h2>{% localized "ProductsStrings|PageTitleProducts" %}</h2>  
  
```  
  
 Consulte toohello seguintes tabelas para recursos de cadeia de caracteres de saudação disponíveis para uso em seus modelos de portal do desenvolvedor. Use o nome da tabela de saudação como prefixo Olá para recursos de cadeia de caracteres de saudação nessa tabela.  
  
-   [ApisStrings](#ApisStrings)  
  
-   [ApplicationListStrings](#ApplicationListStrings)  
  
-   [AppDetailsStrings](#AppDetailsStrings)  
  
-   [AppStrings](#AppStrings)  
  
-   [CommonResources](#CommonResources)  
  
-   [CommonStrings](#CommonStrings)  
  
-   [Documentação](#Documentation)  
  
-   [ErrorPageStrings](#ErrorPageStrings)  
  
-   [IssuesStrings](#IssuesStrings)  
  
-   [NotFoundStrings](#NotFoundStrings)  
  
-   [ProductDetailsStrings](#ProductDetailsStrings)  
  
-   [ProductsStrings](#ProductsStrings)  
  
-   [ProviderInfoStrings](#ProviderInfoStrings)  
  
-   [SigninResources](#SigninResources)  
  
-   [SigninStrings](#SigninStrings)  
  
-   [SignupStrings](#SignupStrings)  
  
-   [SubscriptionListStrings](#SubscriptionListStrings)  
  
-   [SubscriptionStrings](#SubscriptionStrings)  
  
-   [UpdateProfileStrings](#UpdateProfileStrings)  
  
-   [UserProfile](#UserProfile)  
  
###  <a name="ApisStrings"></a> ApisStrings  
  
|Nome|Texto|  
|----------|----------|  
|PageTitleApis|APIs|  
  
###  <a name="AppDetailsStrings"></a> AppDetailsStrings  
  
|Nome|Texto|  
|----------|----------|  
|WebApplicationsDetailsTitle|Visualização de aplicativo|  
|WebApplicationsRequirementsHeader|Requisitos|  
|WebApplicationsScreenshotAlt|Captura de tela|  
|WebApplicationsScreenshotsHeader|Capturas de tela|  
  
###  <a name="ApplicationListStrings"></a> ApplicationListStrings  
  
|Nome|Texto|  
|----------|----------|  
|WebDevelopersAppDeleteConfirmation|Tem certeza de que deseja que o aplicativo tooremove?|  
|WebDevelopersAppNotPublished|Não publicado|  
|WebDevelopersAppNotSubminted|Não enviado|  
|WebDevelopersAppTableCategoryHeader|Categoria|  
|WebDevelopersAppTableNameHeader|Nome|  
|WebDevelopersAppTableStateHeader|Estado|  
|WebDevelopersEditLink|Editar|  
|WebDevelopersRegisterAppLink|Registrar aplicativo|  
|WebDevelopersRemoveLink|Remover|  
|WebDevelopersSubmitLink|Enviar|  
|WebDevelopersYourApplicationsHeader|Seus aplicativos|  
  
###  <a name="AppStrings"></a> AppStrings  
  
|Nome|Texto|  
|----------|----------|  
|WebApplicationsHeader|Aplicativos|  
  
###  <a name="CommonResources"></a> CommonResources  
  
|Nome|Texto|  
|----------|----------|  
|NoItemsToDisplay|Nenhum resultado encontrado.|  
|GeneralExceptionMessage|Algo não está correto. Pode ser uma falha temporária ou um bug. Tente novamente.|  
|GeneralJsonExceptionMessage|Algo não está correto. Pode ser uma falha temporária ou um bug. Por favor, recarregar página hello e tente novamente.|  
|ConfirmationMessageUnsavedChanges|Há algumas alterações não salvas. Tem certeza de que você deseja toocancel e descartar as alterações de Olá?|  
|AzureActiveDirectory|Azure Active Directory|  
|HttpLargeRequestMessage|O corpo da solicitação HTTP é grande demais.|  
  
###  <a name="CommonStrings"></a> CommonStrings  
  
|Nome|Texto|  
|----------|----------|  
|ButtonLabelCancel|Cancelar|  
|ButtonLabelSave|Salvar|  
|GeneralExceptionMessage|Algo não está correto. Pode ser uma falha temporária ou um bug. Tente novamente.|  
|NoItemsToDisplay|Não há nenhum toodisplay de itens.|  
|PagerButtonLabelFirst|Primeiro|  
|PagerButtonLabelLast|Último|  
|PagerButtonLabelNext|Avançar|  
|PagerButtonLabelPrevious|Prev|  
|PagerLabelPageNOfM|Página {0} de {1}|  
|PasswordTooShort|Olá senha é muito curta|  
|EmailAsPassword|Não use seu email como sua senha|  
|PasswordSameAsUserName|Sua senha não pode conter seu nome de usuário|  
|PasswordTwoCharacterClasses|Use classes de caracteres diferentes|  
|PasswordTooManyRepetitions|Repetições demais|  
|PasswordSequenceFound|Sua senha contém sequências|  
|PagerLabelPageSize|Tamanho da página|  
|CurtainLabelLoading|Carregando...|  
|TablePlaceholderNothingToDisplay|Não há nenhum dado do escopo e do período de saudação selecionado|  
|ButtonLabelClose|Feche|  
  
###  <a name="Documentation"></a> Documentação  
  
|Nome|Texto|  
|----------|----------|  
|WebDocumentationInvalidHeaderErrorMessage|Cabeçalho '{0}' inválido|  
|WebDocumentationInvalidRequestErrorMessage|URL da Solicitação Inválida|  
|TextboxLabelAccessToken|Token de acesso*|  
|DropdownOptionPrimaryKeyFormat|Primário-{0}|  
|DropdownOptionSecondaryKeyFormat|Secundário-{0}|  
|WebDocumentationSubscriptionKeyText|Sua chave de assinatura|  
|WebDocumentationTemplatesAddHeaders|Adicionar cabeçalhos HTTP necessários|  
|WebDocumentationTemplatesBasicAuthSample|Amostra de Autorização Básica|  
|WebDocumentationTemplatesCurlForBasicAuth|para uso de Autorização Básica: --user {nome de usuário}:{senha}|  
|WebDocumentationTemplatesCurlValuesForPath|Especifique valores para parâmetros de caminho (mostrados como {...}), sua chave de assinatura e valores para parâmetros de consulta|  
|WebDocumentationTemplatesDeveloperKey|Especifique sua chave de assinatura|  
|WebDocumentationTemplatesJavaApache|Este exemplo usa o cliente do Apache HTTP Olá de componentes de HTTP (http://hc.apache.org/httpcomponents-client-ga/)|  
|WebDocumentationTemplatesOptionalParams|Especificar valores para parâmetros opcionais, conforme necessário|  
|WebDocumentationTemplatesPhpPackage|Este exemplo usa o pacote de saudação HTTP_Request2. (para obter mais informações: http://pear.php.net/package/HTTP_Request2)|  
|WebDocumentationTemplatesPythonValuesForPath|Especificar valores para parâmetros de caminho (mostrados como {...}) e o corpo da solicitação se necessário|  
|WebDocumentationTemplatesRequestBody|Especificar corpo da solicitação|  
|WebDocumentationTemplatesRequiredParams|Especificar valores para Olá seguindo os parâmetros necessários|  
|WebDocumentationTemplatesValuesForPath|Especificar valores para parâmetros de caminho (mostrados como {...})|  
|OAuth2AuthorizationEndpointDescription|ponto de extremidade de autorização de saudação é toointeract usado com o proprietário do recurso hello e obter uma concessão de autorização.|  
|OAuth2AuthorizationEndpointName|Ponto de extremidade de autorização|  
|OAuth2TokenEndpointDescription|ponto de extremidade token Olá é usado pelo Olá cliente tooobtain um token de acesso, apresentando sua autorização conceder ou token de atualização.|  
|OAuth2TokenEndpointName|Ponto de extremidade de token|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_Description|< p\> Olá cliente inicia o fluxo de saudação direcionando o ponto de extremidade do agente do usuário toohello autorização do proprietário do recurso de saudação.  cliente Olá inclui seu identificador de cliente, o escopo solicitado, o estado local e um servidor de autorização de saudação do redirecionamento URI toowhich enviará saudação do agente do usuário quando acesso é concedido (ou negado).     </p\> < p\> servidor de autorização Olá autentica o proprietário do recurso de saudação (por meio do agente do usuário Olá) e estabelece se o proprietário do recurso de saudação concede ou nega a solicitação de acesso do cliente hello.     </p\> < p\> supondo que o proprietário do recurso Olá concede acesso, o servidor de autorização Olá redireciona o cliente de toohello voltar de agente do usuário hello usando redirecionamento Olá URI fornecido anteriormente (na solicitação de saudação ou durante os clien registro de t).  URI de redirecionamento de saudação inclui um código de autorização e qualquer estado local fornecido pelo cliente Olá anteriormente.     </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_ErrorDescription|< p\> se o usuário Olá nega a solicitação de acesso de saudação do se Olá solicitação é inválida, cliente hello será informado usando Olá parâmetros adicionados no redirecionamento de toohello a seguir: </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_Name|Solicitação de autorização|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_RequestDescription|< p\> Olá aplicativo de cliente deve enviar o ponto de extremidade da autorização toohello Olá usuário na Olá tooinitiate de ordem processo de OAuth.          Ponto de extremidade de autorização hello, usuário Olá autentica e, em seguida, concede ou nega acesso toohello aplicativo.     </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_ResponseDescription|< p\> supondo que o proprietário do recurso Olá concede acesso, o servidor de autorização redireciona o cliente de toohello voltar de agente do usuário hello usando redirecionamento Olá URI fornecido anteriormente (na solicitação de saudação ou durante o registro de cliente).  URI de redirecionamento de saudação inclui um código de autorização e qualquer estado local fornecido pelo cliente Olá anteriormente. </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_Description|< p\> cliente Olá solicita um token de acesso de saudação do servidor de autorização ' ponto de extremidade token, incluindo o código de autorização Olá recebido na etapa anterior Olá s.  Ao fazer a solicitação de hello, Olá autentica com o servidor de autorização hello.  cliente de saudação inclui Olá redirecionamento URI usado tooobtain Olá código de autorização para verificação. </p\> < p\> servidor de autorização Olá autentica o cliente hello, valida o código de autorização hello e garante que URI de redirecionamento Olá recebidas correspondências Olá URI usado tooredirect Olá cliente na etapa (C).  Se for válida, o servidor de autorização Olá responde com um token de acesso e, opcionalmente, um token de atualização. </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_ErrorDescription|< p\> se a autenticação de cliente de solicitação Olá falha ou é inválida, o servidor de autorização Olá responde com um código de status HTTP 400 (solicitação incorreta) (a menos que especificado o contrário) e inclui Olá parâmetros com resposta Olá a seguir. </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_RequestDescription|< p\> cliente Olá faz um ponto de extremidade solicitação toohello token enviando Olá parâmetros usando hello "application/x-www-form-urlencoded" formato com uma codificação de caractere UTF-8 no corpo de entidade de solicitação de saudação HTTP a seguir. </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_ResponseDescription|< p\> servidor de autorização Olá emite um token de acesso e token de atualização opcional e construções Olá resposta adicionando Olá parâmetros toohello corpo de entidade de resposta de saudação HTTP com um código de status (Okey) 200 a seguir. </p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_Description|< p\> cliente Olá autentica com o servidor de autorização hello e solicita um token de acesso do ponto de extremidade token hello. </p\> < p\> servidor de autorização Olá autentica o cliente hello e se for válida, emite um token de acesso. </p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_ErrorDescription|< p\> se solicitação Olá Falha na autenticação de cliente ou é inválida servidor de autorização Olá responde com um código de status HTTP 400 (solicitação incorreta) (a menos que especificado o contrário) e inclui Olá parâmetros com resposta Olá a seguir. </p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_RequestDescription|< p\> cliente Olá faz um ponto de extremidade solicitação toohello token adicionando Olá parâmetros usando hello "application/x-www-form-urlencoded" formato com uma codificação de caractere UTF-8 no corpo de entidade de solicitação de saudação HTTP a seguir. </p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_ResponseDescription|< p\> se solicitação de token de acesso de saudação é válido e autorizado, o servidor de autorização Olá emite um token de acesso e token de atualização opcional e construções Olá resposta adicionando Olá parâmetros toohello corpo de entidade de saudação HTTP a seguir resposta com um código de status (Okey) 200. </p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_Description|< p\> Olá cliente inicia o fluxo de saudação direcionando o proprietário do recurso de saudação ' ponto de extremidade da autorização toohello s agente do usuário.  cliente Olá inclui seu identificador de cliente, o escopo solicitado, o estado local e um servidor de autorização de saudação do redirecionamento URI toowhich enviará saudação do agente do usuário quando acesso é concedido (ou negado). </p\> < p\> servidor de autorização Olá autentica o proprietário do recurso de saudação (por meio do agente do usuário Olá) e estabelece se o proprietário do recurso Olá concede ou nega cliente Olá ' solicitação de acesso. </p\> < p\> supondo que o proprietário do recurso Olá concede acesso, o servidor de autorização Olá redireciona o cliente de toohello voltar de agente do usuário hello usando redirecionamento Olá URI fornecido anteriormente.  URI de redirecionamento de saudação inclui o token de acesso de saudação no fragmento URI de saudação. </p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_ErrorDescription|< p\> se o proprietário do recurso Olá nega a solicitação de acesso de saudação ou se a solicitação de saudação falhar por razões diferentes de um URI de redirecionamento ausente ou inválido, o servidor de autorização Olá informa o cliente de Olá adicionando Olá parâmetros toohello fragme a seguir componente do NT do uso de URI de redirecionamento Olá Olá formato "application/x-www-form-urlencoded". </p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_RequestDescription|< p\> Olá aplicativo de cliente deve enviar o ponto de extremidade da autorização toohello Olá usuário na Olá tooinitiate de ordem processo de OAuth.      Ponto de extremidade de autorização hello, usuário Olá autentica e, em seguida, concede ou nega acesso toohello aplicativo. </p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_ResponseDescription|< p\> se o proprietário do recurso Olá concede a solicitação de acesso hello, servidor de autorização de saudação emite um token de acesso e entrega toohello cliente adicionando Olá seguinte componente de fragmento toohello parâmetros de URI de redirecionamento hello usando hello "a formato de plicativo/x-www-form-urlencoded". </p\>|  
|OAuth2Flow_ObtainAuthorization_AuthorizationCodeGrant_Description|Fluxo de código de autorização é otimizado para clientes com capacidade de manter a confidencialidade de saudação de suas credenciais (por exemplo, aplicativos de servidor web implementados usando o PHP, Java, Python, Ruby, ASP.NET, etc.).|  
|OAuth2Flow_ObtainAuthorization_AuthorizationCodeGrant_Name|Concessão de código de autorização|  
|OAuth2Flow_ObtainAuthorization_ClientCredentialsGrant_Description|Fluxo de credenciais do cliente é adequado em casos em que o cliente de saudação (seu aplicativo) está solicitando acessar os recursos protegido de toohello sob seu controle. cliente Olá é considerada como proprietário de um recurso, portanto, nenhuma interação do usuário final é necessária.|  
|OAuth2Flow_ObtainAuthorization_ClientCredentialsGrant_Name|Concessão de credenciais de cliente|  
|OAuth2Flow_ObtainAuthorization_ImplicitGrant_Description|Fluxo implícito é otimizado para clientes sem capacidade de manter a confidencialidade de saudação de seu toooperate conhecidos de credenciais um determinado URI de redirecionamento. Esses clientes são normalmente implementados em um navegador usando uma linguagem de script como JavaScript.|  
|OAuth2Flow_ObtainAuthorization_ImplicitGrant_Name|Concessão implícita|  
|OAuth2Flow_ObtainAuthorization_ResourceOwnerPasswordCredentialsGrant_Description|Fluxo de credenciais de senha de proprietário do recurso é adequado em casos em que o proprietário do recurso Olá tem uma relação de confiança com o cliente de saudação (seu aplicativo), como o sistema operacional Olá dispositivo ou um aplicativo altamente privilegiado. Esse fluxo é adequado para clientes com capacidade de obter as credenciais do proprietário do recurso de saudação (nome de usuário e senha, normalmente usando um formulário interativo).|  
|OAuth2Flow_ObtainAuthorization_ResourceOwnerPasswordCredentialsGrant_Name|Concessão de credenciais de senha de proprietário do recurso|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_Description|< p\> proprietário do recurso Olá fornece cliente Olá com seu nome de usuário e senha. </p\> < p\> cliente Olá solicita um token de acesso de saudação do servidor de autorização ' s ponto de extremidade, incluindo credenciais Olá recebidas do proprietário do recurso de saudação.  Ao fazer a solicitação de hello, Olá autentica com o servidor de autorização hello. </p\> < p\> Olá autorização servidor autentica o cliente Olá valida as credenciais do proprietário do recurso hello e se for válida, emite um token de acesso. </p\>|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_ErrorDescription|< p\> se solicitação Olá Falha na autenticação de cliente ou é inválida servidor de autorização Olá responde com um código de status HTTP 400 (solicitação incorreta) (a menos que especificado o contrário) e inclui Olá parâmetros com resposta Olá a seguir. </p\>|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_RequestDescription|< p\> cliente Olá faz um ponto de extremidade solicitação toohello token adicionando Olá parâmetros usando hello "application/x-www-form-urlencoded" formato com uma codificação de caractere UTF-8 no corpo de entidade de solicitação de saudação HTTP a seguir. </p\>|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_ResponseDescription|< p\> se solicitação de token de acesso de saudação é válido e autorizado, o servidor de autorização Olá emite um token de acesso e token de atualização opcional e construções Olá resposta adicionando Olá parâmetros toohello corpo de entidade de respo de saudação HTTP a seguir nSe com um código de status (Okey) 200. </p\>|  
|OAuth2Step_AccessTokenRequest_Name|Solicitação de token de acesso|  
|OAuth2Step_AuthorizationRequest_Name|Solicitação de autorização|  
|OAuth2AccessToken_AuthorizationCodeGrant_TokenResponse|OBRIGATÓRIO. token de acesso de saudação emitido pelo servidor de autorização de saudação.|  
|OAuth2AccessToken_ClientCredentialsGrant_TokenResponse|OBRIGATÓRIO. token de acesso de saudação emitido pelo servidor de autorização de saudação.|  
|OAuth2AccessToken_ImplicitGrant_AuthorizationResponse|OBRIGATÓRIO. token de acesso de saudação emitido pelo servidor de autorização de saudação.|  
|OAuth2AccessToken_ResourceOwnerPasswordCredentialsGrant_TokenResponse|OBRIGATÓRIO. token de acesso de saudação emitido pelo servidor de autorização de saudação.|  
|OAuth2ClientId_AuthorizationCodeGrant_AuthorizationRequest|OBRIGATÓRIO. Identificador de cliente.|  
|OAuth2ClientId_AuthorizationCodeGrant_TokenRequest|NECESSÁRIO se cliente Olá não autentica com o servidor de autorização hello.|  
|OAuth2ClientId_ImplicitGrant_AuthorizationRequest|OBRIGATÓRIO. Identificador de saudação do cliente.|  
|OAuth2Code_AuthorizationCodeGrant_AuthorizationResponse|OBRIGATÓRIO. código de autorização Olá gerado pelo servidor de autorização de saudação.|  
|OAuth2Code_AuthorizationCodeGrant_TokenRequest|OBRIGATÓRIO. código de autorização Olá recebido saudação do servidor de autorização.|  
|OAuth2ErrorDescription_AuthorizationCodeGrant_AuthorizationErrorResponse|OPCIONAL. Texto ASCII legível fornecendo informações adicionais.|  
|OAuth2ErrorDescription_AuthorizationCodeGrant_TokenErrorResponse|OPCIONAL. Texto ASCII legível fornecendo informações adicionais.|  
|OAuth2ErrorDescription_ClientCredentialsGrant_TokenErrorResponse|OPCIONAL. Texto ASCII legível fornecendo informações adicionais.|  
|OAuth2ErrorDescription_ImplicitGrant_AuthorizationErrorResponse|OPCIONAL. Texto ASCII legível fornecendo informações adicionais.|  
|OAuth2ErrorDescription_ResourceOwnerPasswordCredentialsGrant_TokenErrorResponse|OPCIONAL. Texto ASCII legível fornecendo informações adicionais.|  
|OAuth2ErrorUri_AuthorizationCodeGrant_AuthorizationErrorResponse|OPCIONAL. Um URI que identifica uma página da web legível com informações sobre o erro de saudação.|  
|OAuth2ErrorUri_AuthorizationCodeGrant_TokenErrorResponse|OPCIONAL. Um URI que identifica uma página da web legível com informações sobre o erro de saudação.|  
|OAuth2ErrorUri_ClientCredentialsGrant_TokenErrorResponse|OPCIONAL. Um URI que identifica uma página da web legível com informações sobre o erro de saudação.|  
|OAuth2ErrorUri_ImplicitGrant_AuthorizationErrorResponse|OPCIONAL. Um URI que identifica uma página da web legível com informações sobre o erro de saudação.|  
|OAuth2ErrorUri_ResourceOwnerPasswordCredentialsGrant_TokenErrorResponse|OPCIONAL. Um URI que identifica uma página da web legível com informações sobre o erro de saudação.|  
|OAuth2Error_AuthorizationCodeGrant_AuthorizationErrorResponse|OBRIGATÓRIO. Um único código de erro de ASCII da seguinte Olá: invalid_request, unauthorized_client, access_denied, unsupported_response_type, invalid_scope, server_error, temporarily_unavailable.|  
|OAuth2Error_AuthorizationCodeGrant_TokenErrorResponse|OBRIGATÓRIO. Um único código de erro de ASCII da seguinte Olá: invalid_request, invalid_client, invalid_grant, unauthorized_client, unsupported_grant_type, invalid_scope.|  
|OAuth2Error_ClientCredentialsGrant_TokenErrorResponse|OBRIGATÓRIO. Um único código de erro de ASCII da seguinte Olá: invalid_request, invalid_client, invalid_grant, unauthorized_client, unsupported_grant_type, invalid_scope.|  
|OAuth2Error_ImplicitGrant_AuthorizationErrorResponse|OBRIGATÓRIO. Um único código de erro de ASCII da seguinte Olá: invalid_request, unauthorized_client, access_denied, unsupported_response_type, invalid_scope, server_error, temporarily_unavailable.|  
|OAuth2Error_ResourceOwnerPasswordCredentialsGrant_TokenErrorResponse|OBRIGATÓRIO. Um único código de erro de ASCII da seguinte Olá: invalid_request, invalid_client, invalid_grant, unauthorized_client, unsupported_grant_type, invalid_scope.|  
|OAuth2ExpiresIn_AuthorizationCodeGrant_TokenResponse|RECOMENDADO. tempo de vida de saudação em segundos do token de acesso de saudação.|  
|OAuth2ExpiresIn_ClientCredentialsGrant_TokenResponse|RECOMENDADO. tempo de vida de saudação em segundos do token de acesso de saudação.|  
|OAuth2ExpiresIn_ImplicitGrant_AuthorizationResponse|RECOMENDADO. tempo de vida de saudação em segundos do token de acesso de saudação.|  
|OAuth2ExpiresIn_ResourceOwnerPasswordCredentialsGrant_TokenResponse|RECOMENDADO. tempo de vida de saudação em segundos do token de acesso de saudação.|  
|OAuth2GrantType_AuthorizationCodeGrant_TokenRequest|OBRIGATÓRIO. Valor deve ser definido muito "authorization_code".|  
|OAuth2GrantType_ClientCredentialsGrant_TokenRequest|OBRIGATÓRIO. Valor deve ser definido muito "client_credentials".|  
|OAuth2GrantType_ResourceOwnerPasswordCredentialsGrant_TokenRequest|OBRIGATÓRIO. Valor deve ser definido muito "senha".|  
|OAuth2Password_ResourceOwnerPasswordCredentialsGrant_TokenRequest|OBRIGATÓRIO. senha de proprietário do recurso de saudação.|  
|OAuth2RedirectUri_AuthorizationCodeGrant_AuthorizationRequest|OPCIONAL. ponto de extremidade de redirecionamento de saudação URI deve ser um URI absoluto.|  
|OAuth2RedirectUri_AuthorizationCodeGrant_TokenRequest|NECESSÁRIO se o parâmetro "redirect_uri" de saudação foi incluído na solicitação de autorização hello e seus valores devem ser idênticos.|  
|OAuth2RedirectUri_ImplicitGrant_AuthorizationRequest|OPCIONAL. ponto de extremidade de redirecionamento de saudação URI deve ser um URI absoluto.|  
|OAuth2RefreshToken_AuthorizationCodeGrant_TokenResponse|OPCIONAL. token de atualização Hello, que pode ser usado tooobtain novos tokens de acesso.|  
|OAuth2RefreshToken_ClientCredentialsGrant_TokenResponse|OPCIONAL. token de atualização Hello, que pode ser usado tooobtain novos tokens de acesso.|  
|OAuth2RefreshToken_ResourceOwnerPasswordCredentialsGrant_TokenResponse|OPCIONAL. token de atualização Hello, que pode ser usado tooobtain novos tokens de acesso.|  
|OAuth2ResponseType_AuthorizationCodeGrant_AuthorizationRequest|OBRIGATÓRIO. Valor deve ser definido muito "code".|  
|OAuth2ResponseType_ImplicitGrant_AuthorizationRequest|OBRIGATÓRIO. Valor deve ser definido muito "token".|  
|OAuth2Scope_AuthorizationCodeGrant_AuthorizationRequest|OPCIONAL. escopo de saudação de solicitação de acesso de saudação.|  
|OAuth2Scope_AuthorizationCodeGrant_TokenResponse|OPCIONAL se toohello idênticos escopo solicitado pelo cliente Olá; Caso contrário, é necessário.|  
|OAuth2Scope_ClientCredentialsGrant_TokenRequest|OPCIONAL. escopo de saudação de solicitação de acesso de saudação.|  
|OAuth2Scope_ClientCredentialsGrant_TokenResponse|OPCIONAL, se idênticos escopo toohello solicitado pelo cliente Olá; Caso contrário, é necessário.|  
|OAuth2Scope_ImplicitGrant_AuthorizationRequest|OPCIONAL. escopo de saudação de solicitação de acesso de saudação.|  
|OAuth2Scope_ImplicitGrant_AuthorizationResponse|OPCIONAL se toohello idênticos escopo solicitado pelo cliente Olá; Caso contrário, é necessário.|  
|OAuth2Scope_ResourceOwnerPasswordCredentialsGrant_TokenRequest|OPCIONAL. escopo de saudação de solicitação de acesso de saudação.|  
|OAuth2Scope_ResourceOwnerPasswordCredentialsGrant_TokenResponse|OPCIONAL, se idênticos escopo toohello solicitado pelo cliente Olá; Caso contrário, é necessário.|  
|OAuth2State_AuthorizationCodeGrant_AuthorizationErrorResponse|NECESSÁRIO se parâmetro de "estado" hello estava presente na solicitação de autorização do cliente hello.  valor exato Olá recebido do cliente hello.|  
|OAuth2State_AuthorizationCodeGrant_AuthorizationRequest|RECOMENDADO. Um valor opaco usado por Olá cliente toomaintain estado entre a solicitação de saudação e retorno de chamada.  servidor de autorização de saudação inclui esse valor ao redirecionar o cliente de toohello voltar do agente do usuário hello.  parâmetro Hello deve ser usado para evitar a falsificação de solicitação entre sites.|  
|OAuth2State_AuthorizationCodeGrant_AuthorizationResponse|NECESSÁRIO se parâmetro de "estado" hello estava presente na solicitação de autorização do cliente hello.  valor exato Olá recebido do cliente hello.|  
|OAuth2State_ImplicitGrant_AuthorizationErrorResponse|NECESSÁRIO se parâmetro de "estado" hello estava presente na solicitação de autorização do cliente hello.  valor exato Olá recebido do cliente hello.|  
|OAuth2State_ImplicitGrant_AuthorizationRequest|RECOMENDADO. Um valor opaco usado por Olá cliente toomaintain estado entre a solicitação de saudação e retorno de chamada.  servidor de autorização de saudação inclui esse valor ao redirecionar o cliente de toohello voltar do agente do usuário hello.  parâmetro Hello deve ser usado para evitar a falsificação de solicitação entre sites.|  
|OAuth2State_ImplicitGrant_AuthorizationResponse|NECESSÁRIO se parâmetro de "estado" hello estava presente na solicitação de autorização do cliente hello.  valor exato Olá recebido do cliente hello.|  
|OAuth2TokenType_AuthorizationCodeGrant_TokenResponse|OBRIGATÓRIO. tipo de saudação do hello token emitido.|  
|OAuth2TokenType_ClientCredentialsGrant_TokenResponse|OBRIGATÓRIO. tipo de saudação do hello token emitido.|  
|OAuth2TokenType_ImplicitGrant_AuthorizationResponse|OBRIGATÓRIO. tipo de saudação do hello token emitido.|  
|OAuth2TokenType_ResourceOwnerPasswordCredentialsGrant_TokenResponse|OBRIGATÓRIO. tipo de saudação do hello token emitido.|  
|OAuth2UserName_ResourceOwnerPasswordCredentialsGrant_TokenRequest|OBRIGATÓRIO. nome de proprietário do recurso Hello.|  
|OAuth2UnsupportedTokenType|Não há suporte para o tipo de token '{0}'.|  
|OAuth2InvalidState|Resposta inválida do servidor de autorização|  
|OAuth2GrantType_AuthorizationCode|Código de autorização|  
|OAuth2GrantType_Implicit|Implícito|  
|OAuth2GrantType_ClientCredentials|Credenciais do cliente|  
|OAuth2GrantType_ResourceOwnerPassword|Senha de proprietário do recurso|  
|WebDocumentation302Code|302 Encontrado|  
|WebDocumentation400Code|400 (Solicitação incorreta)|  
|OAuth2SendingMethod_AuthHeader|Cabeçalho de autorização|  
|OAuth2SendingMethod_QueryParam|Parâmetro de consulta|  
|OAuth2AuthorizationServerGeneralException|Ocorreu um erro durante a autorização de acesso por meio de {0}|  
|OAuth2AuthorizationServerCommunicationException|Um servidor de tooauthorization de conexão HTTP não pôde ser estabelecido ou ele foi fechado inesperadamente.|  
|WebDocumentationOAuth2GeneralErrorMessage|Ocorreu um erro inesperado.|  
|AuthorizationServerCommunicationException|Ocorreu uma exceção de comunicação do servidor de autorização. Entre em contato com o administrador.|  
|TextblockSubscriptionKeyHeaderDescription|Chave de assinatura que fornece acesso toothis API. Encontrada em seu <a href='/developer'\>Perfil</a\>.|  
|TextblockOAuthHeaderDescription|O token de acesso OAuth 2.0 obtido de <i\>{0}</i\>. Tipos de concessão com suporte: <i\>{1}</i\>.|  
|TextblockContentTypeHeaderDescription|Tipo de mídia do corpo de saudação enviado toohello API.|  
|ErrorMessageApiNotAccessible|Olá API que você está tentando toocall não está acessível no momento. Entre em contato com o publicador Olá API < um href = "/ emite"\>aqui < /a\>.|  
|ErrorMessageApiTimedout|Olá API que você está tentando toocall está demorando mais que o normal tooget resposta novamente. Entre em contato com o publicador Olá API < um href = "/ emite"\>aqui < /a\>.|  
|BadRequestParameterExpected|"o parâmetro '{0}' é esperado"|  
|TooltipTextDoubleClickToSelectAll|Clique duas vezes em tooselect todos.|  
|TooltipTextHideRevealSecret|Mostrar/Ocultar|  
|ButtonLinkOpenConsole|Experimente|  
|SectionHeadingRequestBody|Corpo da solicitação|  
|SectionHeadingRequestParameters|Parâmetros da solicitação|  
|SectionHeadingRequestUrl|URL de Solicitação|  
|SectionHeadingResponse|Resposta|  
|SectionHeadingRequestHeaders|Cabeçalhos da solicitação|  
|FormLabelSubtextOptional|opcional|  
|SectionHeadingCodeSamples|Exemplos de código|  
|TextblockOpenidConnectHeaderDescription|Token de ID de OpenID Connect obtido de <i\>{0}</i\>. Tipos de concessão com suporte: <i\>{1}</i\>.|  
  
###  <a name="ErrorPageStrings"></a> ErrorPageStrings  
  
|Nome|Texto|  
|----------|----------|  
|LinkLabelBack|voltar|  
|LinkLabelHomePage|home page|  
|LinkLabelSendUsEmail|Envie-nos um email|  
|PageTitleError|Houve uma página solicitada do problema atendendo Olá|  
|TextblockPotentialCauseIntermittentIssue|Isso pode ser um problema de acesso a dados intermitente que já não existe mais.|  
|TextblockPotentialCauseOldLink|link de saudação em que você clicou pode ser antiga e toohello de ponto não corrigir o local mais.|  
|TextblockPotentialCauseTechnicalProblem|Pode haver um problema técnico em nossa extremidade.|  
|TextblockPotentialSolutionRefresh|Tente atualizar a página de saudação.|  
|TextblockPotentialSolutionStartOver|Iniciar do nosso {0}.|  
|TextblockPotentialSolutionTryAgain|Vá {0} e tente a ação de saudação executada novamente.|  
|TextReportProblem|{0} descrevendo o que deu errado e nós veremos isso assim que possível.|  
|TitlePotentialCause|Possível causa|  
|TitlePotentialSolution|Provavelmente é apenas um problema temporário, algumas tootry de coisas|  
  
###  <a name="IssuesStrings"></a> IssuesStrings  
  
|Nome|Texto|  
|----------|----------|  
|WebIssuesIndexTitle|Problemas|  
|WebIssuesNoActiveSubscriptions|Você não tem nenhuma assinatura ativa. Você precisa toosubscribe para um produto tooreport um problema.|  
|WebIssuesNotSignin|Você não está conectado. Faça {0} tooreport um problema ou para postar um comentário.|  
|WebIssuesReportIssueButton|Relatar Problema|  
|WebIssuesSignIn|entrar|  
|WebIssuesStatusReportedBy|Status: {0} &#124; Relatado por {1}|  
  
###  <a name="NotFoundStrings"></a> NotFoundStrings  
  
|Nome|Texto|  
|----------|----------|  
|LinkLabelHomePage|home page|  
|LinkLabelSendUsEmail|envie-nos um email|  
|PageTitleNotFound|Infelizmente, que não foi possível encontrar página Olá que você está procurando|  
|TextblockPotentialCauseMisspelledUrl|Você pode ter digitado incorretamente Olá URL se você digitou no.|  
|TextblockPotentialCauseOldLink|link de saudação em que você clicou pode ser antiga e toohello de ponto não corrigir o local mais.|  
|TextblockPotentialSolutionRetype|Tente digitar novamente a URL de saudação.|  
|TextblockPotentialSolutionStartOver|Iniciar do nosso {0}.|  
|TextReportProblem|{0} descrevendo o que deu errado e nós veremos isso assim que possível.|  
|TitlePotentialCause|Possível causa|  
|TitlePotentialSolution|Solução em potencial|  
  
###  <a name="ProductDetailsStrings"></a> ProductDetailsStrings  
  
|Nome|Texto|  
|----------|----------|  
|WebProductsAgreement|Inscrevendo-se muito {0} produto, eu concordo toohello `<a data-toggle='modal' href='#legal-terms'\>Terms of Use</a\>`.|  
|WebProductsLegalTermsLink|Termos de Uso|  
|WebProductsSubscribeButton|Assinar|  
|WebProductsUsageLimitsHeader|Limites de uso|  
|WebProductsYouAreNotSubscribed|Você está inscrito toothis produto.|  
|WebProductsYouRequestedSubscription|Você solicitou o produto de toothis de assinatura.|  
|ErrorYouNeedtoAgreeWithLegalTerms|Você deve aceitar os termos de uso toohello antes de prosseguir.|  
|ButtonLabelAddSubscription|Adicionar assinatura|  
|LinkLabelChangeSubscriptionName|alterar|  
|ButtonLabelConfirm|Confirmar|  
|TextblockMultipleSubscriptionsCount|Você tem {0} produto de toothis de assinaturas:|  
|TextblockSingleSubscriptionsCount|Você tem {0} produto de toothis de assinatura:|  
|TextblockSingleApisCount|Este produto contém {0} API:|  
|TextblockMultipleApisCount|Este produto contém {0} APIs:|  
|TextblockHeaderSubscribe|Assinar tooproduct|  
|TextblockSubscriptionDescription|Uma nova assinatura será criada da seguinte maneira:|  
|TextblockSubscriptionLimitReached|Limite de assinaturas atingido.|  
  
###  <a name="ProductsStrings"></a> ProductsStrings  
  
|Nome|Texto|  
|----------|----------|  
|PageTitleProducts|Produtos|  
  
###  <a name="ProviderInfoStrings"></a> ProviderInfoStrings  
  
|Nome|Texto|  
|----------|----------|  
|TextboxExternalIdentitiesDisabled|Entrar está desabilitada por administradores Olá momento hello.|  
|TextboxExternalIdentitiesSigninInvitation|Como alternativa, entre com|  
|TextboxExternalIdentitiesSigninInvitationPrimary|Entre com:|  
  
###  <a name="SigninResources"></a> SigninResources  
  
|Nome|Texto|  
|----------|----------|  
|PrincipalNotFound|A entidade de segurança não foi encontrada ou a assinatura é inválida|  
|ErrorSsoAuthenticationFailed|Falha na autenticação de SSO|  
|ErrorSsoAuthenticationFailedDetailed|Não é possível verificar a assinatura ou token inválido fornecido.|  
|ErrorSsoTokenInvalid|O token de SSO é inválido|  
|ValidationErrorSpecificEmailAlreadyExists|O email '{0}' já foi registrado|  
|ValidationErrorSpecificEmailInvalid|O email '{0}' é inválido|  
|ValidationErrorPasswordInvalid|A senha é inválida. Por favor, corrija os erros de saudação e tente novamente.|  
|PropertyTooShort|{0} é muito curta|  
|WebAuthenticationAddresserEmailInvalidErrorMessage|Endereço de email inválido.|  
|ValidationMessageNewPasswordConfirmationRequired|Confirmar nova senha|  
|ValidationErrorPasswordConfirmationRequired|Confirme a senha está vazio|  
|WebAuthenticationEmailChangeNotice|Email de confirmação de alteração é muito em Olá {0}. Siga as instruções dentro dele tooconfirm seu novo endereço de email. Se email Olá não chegarem tooyour da caixa de entrada no hello próximos minutos, verifique sua pasta Lixo eletrônico.|  
|WebAuthenticationEmailChangeNoticeHeader|Sua solicitação de alteração de email foi processada com êxito|  
|WebAuthenticationEmailChangeNoticeTitle|Alteração de email solicitada|  
|WebAuthenticationEmailHasBeenRevertedNotice|O seu email já existe. A solicitação foi revertida|  
|ValidationErrorEmailAlreadyExists|O email já existe|  
|ValidationErrorEmailInvalid|Endereço de email inválido|  
|TextboxLabelEmail|Email|  
|ValidationErrorEmailRequired|O email é obrigatório.|  
|WebAuthenticationErrorNoticeHeader|Erro|  
|WebAuthenticationFieldLengthErrorMessage|{0} deve ter um comprimento máximo de {1}|  
|TextboxLabelEmailFirstName|Nome|  
|ValidationErrorFirstNameRequired|O nome é obrigatório.|  
|ValidationErrorFirstNameInvalid|Nome inválido|  
|NoticeInvalidInvitationToken|Observe que os links de confirmação são válidos por apenas 48 horas. Se você estiver ainda dentro deste período, certifique-se de que o link está correto. Se o link tiver expirado, repita ação Olá estiver tentando tooconfirm.|  
|NoticeHeaderInvalidInvitationToken|Token de convite inválido|  
|NoticeTitleInvalidInvitationToken|Erro de confirmação|  
|WebAuthenticationLastNameInvalidErrorMessage|Sobrenome inválido|  
|TextboxLabelEmailLastName|Sobrenome|  
|ValidationErrorLastNameRequired|O sobrenome é obrigatório.|  
|WebAuthenticationLinkExpiredNotice|Link de confirmação enviada tooyou expirou. `<a href={0}?token={1}>Resend confirmation email.</a\>`|  
|NoticePasswordResetLinkInvalidOrExpired|Seu link de redefinição de senha é inválido ou expirou.|  
|WebAuthenticationLinkExpiredNoticeTitle|Link enviado|  
|WebAuthenticationNewPasswordLabel|Nova senha|  
|ValidationMessageNewPasswordRequired|A nova senha é obrigatória.|  
|TextboxLabelNotificationsSenderEmail|Email do remetente das notificações|  
|TextboxLabelOrganizationName|Nome da Organização|  
|WebAuthenticationOrganizationRequiredErrorMessage|O nome da organização está vazio|  
|WebAuthenticationPasswordChangedNotice|Sua senha foi atualizada com êxito|  
|WebAuthenticationPasswordChangedNoticeTitle|Senha atualizada|  
|WebAuthenticationPasswordCompareErrorMessage|As senhas não correspondem|  
|WebAuthenticationPasswordConfirmLabel|Confirmar senha|  
|ValidationErrorPasswordInvalidDetailed|A senha é muito fraca.|  
|WebAuthenticationPasswordLabel|Senha|  
|ValidationErrorPasswordRequired|A senha é obrigatória.|  
|WebAuthenticationPasswordResetSendNotice|Alterar email de confirmação de senha é muito em Olá {0}. Siga as instruções de Olá Olá email toocontinue dentro de seu processo de alteração de senha.|  
|WebAuthenticationPasswordResetSendNoticeHeader|Sua solicitação de redefinição de senha foi processada com êxito|  
|WebAuthenticationPasswordResetSendNoticeTitle|Redefinição de senha solicitada|  
|WebAuthenticationRequestNotFoundNotice|Solicitação não encontrada|  
|WebAuthenticationSenderEmailRequiredErrorMessage|O email do remetente de notificações está vazio|  
|WebAuthenticationSigninPasswordLabel|Confirme alteração Olá inserindo uma senha|  
|WebAuthenticationSignupConfirmNotice|Email de confirmação do registro está em seu caminho muito {0}. < br /\> por favor siga as instruções em Olá email tooactivate sua conta. < br /\> Verifique se o email Olá não chegam na caixa de entrada hello dentro de alguns minutos, sua pasta Lixo eletrônico.|  
|WebAuthenticationSignupConfirmNoticeHeader|Sua conta foi criada com êxito|  
|WebAuthenticationSignupConfirmNoticeRepeatHeader|O email de confirmação do registro foi enviado novamente|  
|WebAuthenticationSignupConfirmNoticeTitle|Conta criada|  
|WebAuthenticationTokenRequiredErrorMessage|O token está vazio|  
|WebAuthenticationUserAlreadyRegisteredNotice|Parece que um usuário com este email já está registrado no sistema de saudação. Se você esqueceu sua senha, tente toorestore-la ou entre em contato com nossa equipe de suporte.|  
|WebAuthenticationUserAlreadyRegisteredNoticeHeader|Usuário já registrado|  
|WebAuthenticationUserAlreadyRegisteredNoticeTitle|Já registrado|  
|ButtonLabelChangePassword|Alterar senha|  
|ButtonLabelChangeAccountInfo|Alterar informações da conta|  
|ButtonLabelCloseAccount|Fechar conta|  
|WebAuthenticationInvalidCaptchaErrorMessage|Texto inserido não coincide com o texto na imagem de saudação. Tente novamente.|  
|ValidationErrorCredentialsInvalid|Email ou senha é inválida. Por favor, corrija os erros de saudação e tente novamente.|  
|WebAuthenticationRequestIsNotValid|A solicitação não é válida|  
|WebAuthenticationUserIsNotConfirm|Confirme seu registro antes de tentar toosign no.|  
|WebAuthenticationInvalidEmailFormated|O email é inválido: {0}|  
|WebAuthenticationUserNotFound|Usuário não encontrado|  
|WebAuthenticationTenantNotRegistered|Sua conta pertencer ao locatário do Active Directory do Azure tooa que não é autorizado tooaccess neste portal.|  
|WebAuthenticationAuthenticationFailed|Falha na autenticação.|  
|WebAuthenticationGooglePlusNotEnabled|Falha na autenticação. Se você autorizado aplicativo hello, entre em contato com Olá administrador toomake-se que a autenticação do Google está configurada corretamente.|  
|ValidationErrorAllowedTenantIsRequired|Locatário Permitido é obrigatório|  
|ValidationErrorTenantIsNotValid|locatário do Active Directory do Azure Olá '{0}' não é válido.|  
|WebAuthenticationActiveDirectoryTitle|Azure Active Directory|  
|WebAuthenticationLoginUsingYourProvider|Faça logon usando sua conta do {0}|  
|WebAuthenticationUserLimitNotice|Esse serviço atingiu o número máximo de saudação de usuários permitidos. Por favor, `<a href="mailto:{0}"\>contact hello administrator</a\>` tooupgrade seu registro de usuário do serviço e habilitar novamente.|  
|WebAuthenticationUserLimitNoticeHeader|Registro de usuário desabilitado|  
|WebAuthenticationUserLimitNoticeTitle|Registro de usuário desabilitado|  
|WebAuthenticationUserRegistrationDisabledNotice|Registro de usuários foi desabilitado pelo administrador de saudação. Faça logon com o provedor de identidade externo.|  
|WebAuthenticationUserRegistrationDisabledNoticeHeader|Registro de usuário desabilitado|  
|WebAuthenticationUserRegistrationDisabledNoticeTitle|Registro de usuário desabilitado|  
|WebAuthenticationSignupPendingConfirmationNotice|Antes, pode concluir a criação de saudação da sua conta é preciso tooverify seu endereço de email. Nós enviamos um email muito {0}. Siga as instruções de Olá Olá email tooactivate dentro de sua conta. Se o email Olá não chegarem em Olá próximos minutos, verifique sua pasta Lixo eletrônico.|  
|WebAuthenticationSignupPendingConfirmationAccountFoundNotice|Encontramos uma conta não confirmada para o endereço de email Olá {0}. criação de saudação toocomplete da sua conta, que precisamos tooverify seu endereço de email. Nós enviamos um email muito {0}. Siga as instruções de Olá Olá email tooactivate dentro de sua conta. Se o email Olá não chegarem em Olá próximos minutos, verifique sua pasta Lixo eletrônico|  
|WebAuthenticationSignupConfirmationAlmostDone|Já está quase pronto!|  
|WebAuthenticationSignupConfirmationEmailSent|Nós enviamos um email muito {0}. Siga as instruções de Olá Olá email tooactivate dentro de sua conta. Se o email Olá não chegarem em Olá próximos minutos, verifique sua pasta Lixo eletrônico.|  
|WebAuthenticationEmailSentNotificationMessage|Email enviado com êxito {0}|  
|WebAuthenticationNoAadTenantConfigured|Nenhum locatário do Active Directory do Azure configurado para o serviço de saudação.|  
|CheckboxLabelUserRegistrationTermsConsentRequired|Eu concordo toohello `<a data-toggle="modal" href="#" data-target="#terms"\>Terms of Use</a\>`.|  
|TextblockUserRegistrationTermsProvided|Examine `<a data-toggle="modal" href="#" data-target="#terms"\>Terms of Use.</a\>`|  
|DialogHeadingTermsOfUse|Termos de Uso|  
|ValidationMessageConsentNotAccepted|Você deve aceitar os termos de uso toohello antes de prosseguir.|  
  
###  <a name="SigninStrings"></a> SigninStrings  
  
|Nome|Texto|  
|----------|----------|  
|WebAuthenticationForgotPassword|Esqueceu sua senha?|  
|WebAuthenticationIfAdministrator|Se você é um administrador, você deve entrar em `<a href="{0}"\>here</a\>`.|  
|WebAuthenticationNotAMember|Você ainda não é membro? `<a href="/signup"\>Sign up now</a\>`|  
|WebAuthenticationRemember|Lembrar-me neste computador|  
|WebAuthenticationSigininWithPassword|Entrar com seu nome de usuário e senha|  
|WebAuthenticationSigninTitle|Entrar|  
|WebAuthenticationSignUpNow|Inscreva-se agora mesmo|  
  
###  <a name="SignupStrings"></a> SignupStrings  
  
|Nome|Texto|  
|----------|----------|  
|PageTitleSignup|Inscrição|  
|WebAuthenticationAlreadyAMember|Já é membro?|  
|WebAuthenticationCreateNewAccount|Criar uma nova conta de Gerenciamento de API|  
|WebAuthenticationSigninNow|Entrar agora|  
|ButtonLabelSignup|Inscrição|  
  
###  <a name="SubscriptionListStrings"></a> SubscriptionListStrings  
  
|Nome|Texto|  
|----------|----------|  
|SubscriptionCancelConfirmation|Tem certeza de que deseja toocancel esta assinatura?|  
|SubscriptionRenewConfirmation|Tem certeza de que deseja toorenew esta assinatura?|  
|WebDevelopersManageSubscriptions|Gerenciar Assinaturas|  
|WebDevelopersPrimaryKey|Chave primária|  
|WebDevelopersRegenerateLink|Regenerar|  
|WebDevelopersSecondaryKey|Chave secundária|  
|ButtonLabelShowKey|Mostrar|  
|ButtonLabelRenewSubscription|Renew|  
|WebDevelopersSubscriptionReqested|Solicitado em {0}|  
|WebDevelopersSubscriptionRequestedState|Solicitado|  
|WebDevelopersSubscriptionTableNameHeader|Nome|  
|WebDevelopersSubscriptionTableStateHeader|Estado|  
|WebDevelopersUsageStatisticsLink|Relatórios de análise|  
|WebDevelopersYourSubscriptions|Suas assinaturas|  
|SubscriptionPropertyLabelRequestedDate|Solicitado em|  
|SubscriptionPropertyLabelStartedDate|Iniciado em|  
|PageTitleRenameSubscription|Renomear assinatura|  
|SubscriptionPropertyLabelName|Nome da assinatura|  
  
###  <a name="SubscriptionStrings"></a> SubscriptionStrings  
  
|Nome|Texto|  
|----------|----------|  
|SectionHeadingCloseAccount|Procurando tooclose sua conta?|  
|PageTitleDeveloperProfile|Perfil|  
|ButtonLabelHideKey|Ocultar|  
|ButtonLabelRegenerateKey|Regenerar|  
|InformationMessageKeyWasRegenerated|Tem certeza de que deseja tooregenerate essa chave?|  
|ButtonLabelShowKey|Mostrar|  
  
###  <a name="UpdateProfileStrings"></a> UpdateProfileStrings  
  
|Nome|Texto|  
|----------|----------|  
|ButtonLabelUpdateProfile|Atualizar perfil|  
|PageTitleUpdateProfile|Atualizar informações da conta|  
  
###  <a name="UserProfile"></a> UserProfile  
  
|Nome|Texto|  
|----------|----------|  
|ButtonLabelChangeAccountInfo|Alterar informações da conta|  
|ButtonLabelChangePassword|Alterar senha|  
|ButtonLabelCloseAccount|Fechar conta|  
|TextboxLabelEmail|Email|  
|TextboxLabelEmailFirstName|Nome|  
|TextboxLabelEmailLastName|Sobrenome|  
|TextboxLabelNotificationsSenderEmail|Email do remetente das notificações|  
|TextboxLabelOrganizationName|Nome da Organização|  
|SubscriptionStateActive|Ativo|  
|SubscriptionStateCancelled|Cancelado|  
|SubscriptionStateExpired|Expirado|  
|SubscriptionStateRejected|Rejeitado|  
|SubscriptionStateRequested|Solicitado|  
|SubscriptionStateSuspended|Suspenso|  
|DefaultSubscriptionNameTemplate|{0} (padrão)|  
|SubscriptionNameTemplate|Acesso de desenvolvedor n°. {0}|  
|TextboxLabelSubscriptionName|Nome da assinatura|  
|ValidationMessageSubscriptionNameRequired|Não é possível deixar em branco o nome da assinatura.|  
|ApiManagementUserLimitReached|Esse serviço atingiu o número máximo de saudação de usuários permitidos. Atualize tooa superior a camada de preços.|  
  
##  <a name="glyphs"></a> Recursos de glifo  
 Modelos portais do desenvolvedor de gerenciamento de API podem usar os glifos de saudação do [Glyphicons de inicialização](http://getbootstrap.com/components/#glyphicons). Esse conjunto de glifos inclui mais de 250 glifos no formato de fonte da saudação [Glyphicon](http://glyphicons.com/) Halflings definido. toouse um glifo neste conjunto, use Olá sintaxe a seguir.  
  
```html  
<span class="glyphicon glyphicon-user">  
```  
  
 Para a lista completa de saudação de glifos, consulte [Glyphicons de inicialização](http://getbootstrap.com/components/#glyphicons).

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá portal do desenvolvedor do gerenciamento de API usando modelos](api-management-developer-portal-templates.md).
