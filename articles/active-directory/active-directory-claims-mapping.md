---
title: "Mapeamento de declarações no Azure Active Directory (visualização pública) | Microsoft Docs"
description: "Esta página descreve o mapeamento de declarações no Azure Active Directory."
services: active-directory
author: billmath
manager: femila
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: billmath
ms.openlocfilehash: ff07b9954d5c2ce71ab0ffd0db49fde15f323586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="claims-mapping-in-azure-active-directory-public-preview"></a>Mapeamento de declarações no Azure Active Directory (visualização pública)

>[!NOTE]
>Esse recurso substitui e substitui Olá [declarações personalização](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-claims-customization) oferecidos por meio do portal Olá atualmente. Se você personalizar declarações usando o portal de saudação além toohello método gráfico/PowerShell detalhadas neste documento em Olá mesmo aplicativo, os tokens emitidos para esse aplicativo irá ignorar configuração Olá no portal de saudação.
As configurações feitas por meio de métodos de saudação detalhados neste documento não serão refletidas no portal de saudação.

Esse recurso é usado pelo locatário administradores toocustomize Olá declarações emitidas nos tokens de um aplicativo específico em seu locatário. Você pode usar políticas de mapeamento de declarações para:

- Selecionar quais declarações são incluídas nos tokens.
- Crie tipos de declaração que ainda não existem.
- Escolha ou alterar Olá fonte de dados emitidos em declarações específicas.

>[!NOTE]
>Atualmente, essa capacidade está em visualização pública. Prepare-se toorevert ou remova as alterações. recurso de saudação está disponível em qualquer assinatura do Azure Active Directory (AD do Azure) durante a visualização pública. No entanto, quando o recurso de saudação se torna disponível, alguns aspectos do recurso de saudação podem exigir uma assinatura premium do Active Directory do Azure.

## <a name="claims-mapping-policy-type"></a>Tipo de política de mapeamento de declarações
No Azure AD, um objeto de **Política** representa um conjunto de regras aplicadas a todos os aplicativos ou a aplicativos individuais em uma organização. Cada tipo de política tem uma estrutura única, com um conjunto de propriedades que são, em seguida, aplicada toowhich tooobjects que são atribuídos.

Declarações de uma política de mapeamento é um tipo de **política** objeto que modifica Olá declarações emitidas em tokens emitidos para aplicativos específicos.

## <a name="claim-sets"></a>Conjuntos de declarações
Há determinados conjuntos de declarações que definem como e quando elas são usada em tokens.

### <a name="core-claim-set"></a>Conjunto de declarações de núcleo
Declarações no núcleo do hello declaração conjunto estão presentes em cada token, independentemente de política. Essas declarações também são consideradas restritas e não podem ser modificadas.

### <a name="basic-claim-set"></a>Conjunto de declarações básicas
conjunto de declarações básica de saudação inclui declarações de saudação que são emitidas por padrão para tokens (no conjunto de declarações de núcleo de toohello adição). Essas declarações podem ser omitidas ou modificadas por meio de declarações Olá mapeamento de políticas.

### <a name="restricted-claim-set"></a>Conjunto de declarações restritas
Declarações restritas não podem ser modificadas usando políticas. fonte de dados de saudação não pode ser alterado, e nenhuma transformação é aplicada ao gerar essas declarações.

#### <a name="table-1-json-web-token-jwt-restricted-claim-set"></a>Tabela 1: Conjunto de declarações restritas do JWT (Token Web JSON)
|Tipo de declaração (nome)|
| ----- |
|_claim_names|
|_claim_sources|
|access_token|
|account_type|
|acr|
|actor|
|actortoken|
|aio|
|altsecid|
|amr|
|app_chain|
|app_displayname|
|app_res|
|appctx|
|appctxsender|
|appid|
|appidacr|
|asserção|
|at_hash|
|aud|
|auth_data|
|auth_time|
|authorization_code|
|azp|
|azpacr|
|c_hash|
|ca_enf|
|cc|
|cert_token_use|
|client_id|
|cloud_graph_host_name|
|cloud_instance_name|
|cnf|
|código|
|controls|
|credential_keys|
|csr|
|csr_type|
|deviceid|
|dns_names|
|domain_dns_name|
|domain_netbios_name|
|e_exp|
|email|
|endpoint|
|enfpolids|
|exp|
|expires_on|
|grant_type|
|graph|
|group_sids|
|groups|
|hasgroups|
|hash_alg|
|home_oid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expired|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier|
|iat|
|identityprovider|
|idp|
|in_corp|
|instance|
|ipaddr|
|isbrowserhostedapp|
|iss|
|jwk|
|key_id|
|key_type|
|mam_compliance_url|
|mam_enrollment_url|
|mam_terms_of_use_url|
|mdm_compliance_url|
|mdm_enrollment_url|
|mdm_terms_of_use_url|
|nameid|
|nbf|
|netbios_name|
|nonce|
|oid|
|on_prem_id|
|onprem_sam_account_name|
|onprem_sid|
|openid2_id|
|Senha|
|platf|
|polids|
|pop_jwk|
|preferred_username|
|previous_refresh_token|
|primary_sid|
|puid|
|pwd_exp|
|pwd_url|
|redirect_uri|
|refresh_token|
|refreshtoken|
|request_nonce|
|recurso|
|função|
|roles|
|scope|
|scp|
|sid|
|signature|
|signin_state|
|src1|
|src2|
|sub|
|tbid|
|tenant_display_name|
|tenant_region_scope|
|thumbnail_photo|
|tid|
|tokenAutologonEnabled|
|trustedfordelegation|
|unique_name|
|upn|
|user_setting_sync_url|
|Nome de Usuário|
|uti|
|ver|
|verified_primary_email|
|verified_secondary_email|
|wids|
|win_ver|

#### <a name="table-2-security-assertion-markup-language-saml-restricted-claim-set"></a>Tabela 2: Conjunto de declarações restritas de SAML (Security Assertion Markup Language)
|Tipo de declaração (URI)|
| ----- |
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/expired|
|http://schemas.microsoft.com/identity/claims/accesstoken|
|http://schemas.microsoft.com/identity/claims/openid2_id|
|http://schemas.microsoft.com/identity/claims/identityprovider|
|http://schemas.microsoft.com/identity/claims/objectidentifier|
|http://schemas.microsoft.com/identity/claims/puid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1] |
|http://schemas.microsoft.com/identity/claims/tenantid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod|
|http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/groups|
|http://schemas.microsoft.com/claims/groups.link|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/role|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/wids|
|http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant|
|http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown|
|http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged|
|http://schemas.microsoft.com/2014/03/psso|
|http://schemas.microsoft.com/claims/authnmethodsreferences|
|http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn|
|http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent|
|http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier|
|http://schemas.microsoft.com/identity/claims/scope|

## <a name="claims-mapping-policy-properties"></a>Propriedades da política de mapeamento de declarações
Use propriedades de saudação do mapeamento política toocontrol quais declarações são emitidas e onde os dados de saudação foi originados em declarações. Se nenhuma política estiver definida, sistema Olá emite tokens que contém o conjunto de declarações de núcleo hello, conjunto de declarações de saudação básica e quaisquer declarações opcionais que Olá aplicativo escolhida tooreceive.

### <a name="include-basic-claim-set"></a>Incluir um conjunto de declarações básicas

**Cadeia de caracteres:** IncludeBasicClaimSet

**Tipo de dados:** booliano (True ou False)

**Resumo:** essa propriedade determina se o conjunto de declarações básica de saudação está incluído nos tokens afetados por essa política. 

- Se o conjunto tooTrue, todas as declarações no conjunto de declarações básica de saudação é emitido nos tokens afetados pela política de saudação. 
- Se set tooFalse, declarações no conjunto de declarações básica de saudação não estiverem em tokens Olá, a menos que elas são individualmente adicionadas na propriedade de esquema de declarações de saudação do hello mesmo política.

>[!NOTE] 
>Declarações no núcleo do hello declaração conjunto estão presentes em cada token, independentemente de qual essa propriedade é definida. 

### <a name="claims-schema"></a>Esquema de declarações

**Cadeia de caracteres:** ClaimsSchema

**Tipo de dados:** blob JSON com uma ou mais entradas de esquema de declaração

**Resumo:** esta propriedade define quais declarações estão presentes nos tokens de saudação afetados pela política Olá, além do conjunto de declarações toohello básica e conjunto de declarações de núcleo de saudação.
Para cada entrada de esquema de declaração definida nesta propriedade, certas informações são necessárias. Você deve especificar onde os dados de saudação for proveniente (**valor** ou **par de origem/ID**), e quais dados saudação de declaração é emitido como (**tipo de declaração de**).

### <a name="claim-schema-entry-elements"></a>Elementos de entrada do esquema de declaração

**Valor:** elemento de valor Olá define um valor estático como Olá dados toobe emitido na declaração de saudação.

**Par de origem/ID:** Olá fonte e elementos de ID definem onde dados Olá Olá declaração foi originados em. 

elemento de origem Olá deve ser definido tooone seguinte hello: 


- "usuário": dados Olá Olá declaração é uma propriedade no objeto de usuário de saudação. 
- "aplicativo": dados Olá Olá declaração é uma propriedade de entidade de serviço de aplicativo (cliente) hello. 
- "recurso": dados Olá Olá declaração é uma propriedade de entidade de serviço de recurso hello.
- "público": dados Olá Olá declaração são uma propriedade de entidade de serviço de Olá Olá público do token hello (ou Olá cliente ou o recurso de entidade de serviço).
- "company": dados Olá Olá declaração é uma propriedade no objeto de empresa do locatário do recurso de saudação.
- "transformação": solicitar dados Olá Olá de transformação de declarações (consulte a seção hello "transformação de declarações" mais adiante neste artigo). 

Se origem Olá transformação Olá **TransformationID** elemento deve ser incluído nesta definição de declaração bem.

elemento de ID Olá identifica qual propriedade na fonte de saudação fornece o valor de Olá Olá declaração. Hello tabela a seguir lista os valores de saudação de ID válida para cada valor de origem.

#### <a name="table-3-valid-id-values-per-source"></a>Tabela 3: Valores de ID válida por origem
|Fonte|ID|Descrição|
|-----|-----|-----|
|Usuário|sobrenome|Nome da família|
|Usuário|givenname|Nome|
|Usuário|displayname|Nome de exibição|
|Usuário|objectid|ObjectID|
|Usuário|mail|Endereço de Email|
|Usuário|userprincipalname|Nome UPN|
|Usuário|department|department|
|Usuário|onpremisessamaccountname|Nome da conta SAM local|
|Usuário|netbiosname|Nome NetBios|
|Usuário|dnsdomainname|Nome de domínio DNS|
|Usuário|onpremisesecurityidentifier|Identificador de segurança local|
|Usuário|companyname|Nome da Organização|
|Usuário|streetaddress|Endereço|
|Usuário|postalcode|Código postal|
|Usuário|preferredlanguange|Idioma preferencial|
|Usuário|onpremisesuserprincipalname|UPN local|
|Usuário|mailNickname|Apelido de email|
|Usuário|extensionattribute1|Atributo de extensão 1|
|Usuário|extensionattribute2|Atributo de extensão 2|
|Usuário|extensionattribute3|Atributo de extensão 3|
|Usuário|extensionattribute4|Atributo de extensão 4|
|Usuário|extensionattribute5|Atributo de extensão 5|
|Usuário|extensionattribute6|Atributo de extensão 6|
|Usuário|extensionattribute7|Atributo de extensão 7|
|Usuário|extensionattribute8|Atributo de extensão 8|
|Usuário|extensionattribute9|Atributo de extensão 9|
|Usuário|extensionattribute10|Atributo de extensão 10|
|Usuário|extensionattribute11|Atributo de extensão 11|
|Usuário|extensionattribute12|Atributo de extensão 12|
|Usuário|extensionattribute13|Atributo de extensão 13|
|Usuário|extensionattribute14|Atributo de extensão 14|
|Usuário|extensionattribute15|Atributo de extensão 15|
|Usuário|othermail|Outro email|
|Usuário|country|País|
|Usuário|city|City|
|Usuário|state|Estado|
|Usuário|jobtitle|Cargo|
|Usuário|employeeid|ID do funcionário|
|Usuário|facsimiletelephonenumber|Número de telefone de fax|
|aplicativo, recurso, público-alvo|displayname|Nome de exibição|
|aplicativo, recurso, público-alvo|objected|ObjectID|
|aplicativo, recurso, público-alvo|marcas|Marcação da entidade de serviço|
|Empresa|tenantcountry|País do locatário|

**TransformationID:** elemento do hello TransformationID deve ser fornecidos apenas se hello elemento de origem é definido muito "transformação".

- Esse elemento deve corresponder o elemento de ID de saudação da entrada de transformação Olá Olá **ClaimsTransformation** propriedade que define como os dados de saudação para esta declaração são gerados.

**Tipo de declaração:** Olá **JwtClaimType** e **SamlClaimType** elementos que definem quais declarações essa entrada de esquema de declaração se refere a.

- Olá JwtClaimType deve conter o nome de saudação do hello declaração toobe emitido em JWTs.
- Olá SamlClaimType deve conter Olá URI da saudação declaração toobe emitido nos tokens SAML.

>[!NOTE]
>Nomes e URIs de declarações em Olá restrito declaração set não pode ser usado para elementos do tipo de declaração hello. Para obter mais informações, consulte hello "Exceções e restrições" seção mais adiante neste artigo.

### <a name="claims-transformation"></a>Transformação de declarações

**Cadeia de caracteres:** ClaimsTransformation

**Tipo de dados:** blob JSON com uma ou mais entradas de transformação 

**Resumo:** usar estas propriedade tooapply comuns transformações toosource dados, dados de saída de saudação toogenerate de declarações especificada em Olá declarações de esquema.

**ID:** Use Olá ID elemento tooreference esta entrada de transformação no hello entrada TransformationID declarações esquema. Esse valor deve ser exclusivo para cada entrada de transformação nesta política.

**TransformationMethod:** elemento de TransformationMethod Olá identifica qual operação é executada toogenerate Olá dados para declaração de saudação.

Um conjunto de entradas e saídas com base no método hello escolhido, é esperado. Eles são definidos usando Olá **InputClaims**, **ParâmetrosDeEntrada** e **OutputClaims** elementos.

#### <a name="table-4-transformation-methods-and-expected-inputs-and-outputs"></a>Tabela 4: Métodos de transformação e entradas e saídas esperadas
|TransformationMethod|Entrada esperada|Saída esperada|Descrição|
|-----|-----|-----|-----|
|Ingressar|cadeia1, cadeia2, separador|outputClaim|Une cadeias de entrada usando um separador entre elas. Por exemplo: cadeia1: "foo@bar.com", cadeia2: "sandbox", separador: "." resulta no outputClaim: "foo@bar.com.sandbox"|
|ExtractMailPrefix|mail|outputClaim|Extrai a parte local de saudação do endereço de email. Por exemplo: email: "foo@bar.com" resulta no outputClaim: "foo". Se nenhum @ logon estiver presente, cadeia de entrada hello original será retornado como está.|

**InputClaims:** usar um InputClaims elemento toopass Olá de dados de uma transformação tooa de entrada de esquema de declaração. Ele tem dois atributos: **ClaimTypeReferenceId** e **TransformationClaimType**.

- **ClaimTypeReferenceId** é associada ao elemento de ID da saudação declaração esquema entrada toofind Olá apropriado declaração de entrada. 
- **TransformationClaimType** é usado toogive entrada de toothis um nome exclusivo. Esse nome deve corresponder a uma das entradas de saudação esperada para o método de transformação de saudação.

**ParâmetrosDeEntrada:** usar um elemento de ParâmetrosDeEntrada toopass uma transformação de tooa valor constante. Ele tem dois atributos: **Value** e **ID**.

- **Valor** é Olá real valor constante toobe passado.
- **ID** é usado toogive entrada de toothis um nome exclusivo. Esse nome deve corresponder a uma das entradas de saudação esperada para o método de transformação de saudação.

**OutputClaims:** usar um OutputClaims elemento toohold Olá de dados gerado por uma transformação e anexá-la de entrada do esquema de solicitação tooa. Ele tem dois atributos: **ClaimTypeReferenceId** e **TransformationClaimType**.

- **ClaimTypeReferenceId** está associado com a ID de saudação de declaração de saída apropriada Olá declaração esquema entrada toofind hello.
- **TransformationClaimType** é toogive usado um nome exclusivo de toothis de saída. Esse nome deve corresponder a uma das saídas de saudação esperada para o método de transformação de saudação.

### <a name="exceptions-and-restrictions"></a>Exceções e restrições

**NameID SAML e UPN:** saudação do qual fonte de valores de NameID e UPN Olá, e as declarações de Olá transformações que são permitidas, os atributos é limitadas.

#### <a name="table-5-attributes-allowed-as-a-data-source-for-saml-nameid"></a>Tabela 5: Atributos permitidos como fonte de dados para NameID SAML
|Fonte|ID|Descrição|
|-----|-----|-----|
|Usuário|mail|Endereço de Email|
|Usuário|userprincipalname|Nome UPN|
|Usuário|onpremisessamaccountname|Nome da conta SAM local|
|Usuário|employeeid|ID do funcionário|
|Usuário|extensionattribute1|Atributo de extensão 1|
|Usuário|extensionattribute2|Atributo de extensão 2|
|Usuário|extensionattribute3|Atributo de extensão 3|
|Usuário|extensionattribute4|Atributo de extensão 4|
|Usuário|extensionattribute5|Atributo de extensão 5|
|Usuário|extensionattribute6|Atributo de extensão 6|
|Usuário|extensionattribute7|Atributo de extensão 7|
|Usuário|extensionattribute8|Atributo de extensão 8|
|Usuário|extensionattribute9|Atributo de extensão 9|
|Usuário|extensionattribute10|Atributo de extensão 10|
|Usuário|extensionattribute11|Atributo de extensão 11|
|Usuário|extensionattribute12|Atributo de extensão 12|
|Usuário|extensionattribute13|Atributo de extensão 13|
|Usuário|extensionattribute14|Atributo de extensão 14|
|Usuário|extensionattribute15|Atributo de extensão 15|

#### <a name="table-6-transformation-methods-allowed-for-saml-nameid"></a>Tabela 6: Métodos de transformação permitidos para o NameID SAML
|TransformationMethod|Restrições|
| ----- | ----- |
|ExtractMailPrefix|Nenhum|
|Ingressar|sufixo Olá Unido deve ser um domínio verificado do locatário de recursos de saudação.|

### <a name="custom-signing-key"></a>Chave de assinatura personalizada
Uma chave de autenticação personalizada deve ser atribuída toohello objeto principal do serviço para um efeito de tootake de política de mapeamento de declarações. Todos os tokens emitidos foi afetados pela política de saudação são assinados com essa chave. Aplicativos devem ser configurado tooaccept tokens assinados com essa chave. Isso garante que a política de mapeamento de declarações de confirmação que tokens foram modificados pelo criador de saudação do hello. Isso protege os aplicativos contra políticas de mapeamento de declarações criadas por atores mal-intencionados.

### <a name="cross-tenant-scenarios"></a>Cenários entre locatários
Declarações de políticas de mapeamento não se aplicam a usuários tooguest. Se um usuário convidado tentativas tooaccess um aplicativo com declarações de mapeamento diretiva atribuída tooits serviço principal, a saudação padrão token é emitido (Olá diretiva não tem efeito).

## <a name="claims-mapping-policy-assignment"></a>Atribuição de política de mapeamento de declarações
Declarações de políticas de mapeamento podem ser atribuídas apenas objetos tooservice.

### <a name="example-claims-mapping-policies"></a>Exemplos de políticas de mapeamento de declarações

No Azure AD, muitos cenários são possíveis quando você pode personalizar as declarações emitidas em tokens para entidades de serviço específicas. Nesta seção, vemos alguns cenários comuns que podem ajudá-lo a entender como Olá toouse declarações de tipo de política de mapeamento.

#### <a name="prerequisites"></a>Pré-requisitos
Em Olá exemplos a seguir, é possível cria, atualizar, vincula e excluir políticas para entidades de serviço. Se você for novo tooAzure AD, é recomendável que você saiba mais sobre como tooget um AD do Azure locatário antes de prosseguir com esses exemplos. 

tooget iniciado, Olá etapas a seguir:


1. Baixar hello mais recente [versão de visualização pública do módulo PowerShell do AD do Azure](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.127).
2.  Execute Olá conectar comando toosign em tooyour conta de administrador do AD do Azure. Execute esse comando sempre que você iniciar uma nova sessão.
    
     ``` powershell
    Connect-AzureAD -Confirm
    
    ```
3.  toosee todas as políticas que foram criadas em sua organização, Olá execução após o comando. É recomendável que você executar esse comando após a maioria das operações no hello seguintes cenários, toocheck suas políticas estão sendo criadas como esperado.
   
    ``` powershell
        Get-AzureADPolicy
    
    ```
#### <a name="example-create-and-assign-a-policy-tooomit-hello-basic-claims-from-tokens-issued-tooa-service-principal"></a>Exemplo: Criar e atribuir declarações política tooomit Olá básica de entidade de serviço tooa tokens emitidos.
Neste exemplo, você criará uma política que remove o conjunto de declarações básica de saudação de tokens emitidos toolinked entidades de serviço.


1. Crie uma política de mapeamento de declarações. Essa política, as entidades de serviço vinculado toospecific, remove o conjunto de declaração básica de saudação de tokens.
    1. diretiva toocreate hello, execute este comando: 
    
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"false"}}') -DisplayName "OmitBasicClaims” -Type "ClaimsMappingPolicy"
    ```
    2. toosee sua nova política e política de saudação tooget ObjectId, Olá execução a seguir de comando:
    
     ``` powershell
    Get-AzureADPolicy
    ```
2.  Atribua a entidade de serviço Olá política tooyour. Você também precisa tooget Olá ObjectId sua entidade de serviço. 
    1.  toosee entidades de serviço de todas as da sua organização, você pode consultar o Microsoft Graph. Ou, no Azure AD Graph Explorer, entrar tooyour conta AD do Azure.
    2.  Quando você tiver Olá ObjectId do seu Olá de serviço principal, execute comando a seguir:  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
#### <a name="example-create-and-assign-a-policy-tooinclude-hello-employeeid-and-tenantcountry-as-claims-in-tokens-issued-tooa-service-principal"></a>Exemplo: Criar e atribuir uma política tooinclude Olá EmployeeID e TenantCountry como declarações em tokens emitidos tooa entidade de serviço.
Neste exemplo, você cria uma política que adiciona Olá EmployeeID e TenantCountry tootokens emitido toolinked entidades de serviço. Olá EmployeeID é emitido como tipo de declaração de nome de saudação em tokens SAML e JWTs. Olá TenantCountry é emitido como tipo em tokens SAML e JWTs de declaração de país hello. Neste exemplo, continuamos declarações básica de saudação tooinclude definidas nos tokens de saudação.

1. Crie uma política de mapeamento de declarações. Essa política, as entidades de serviço vinculado toospecific, adiciona Olá EmployeeID e TenantCountry tootokens de declarações.
    1. diretiva toocreate hello, execute este comando:  
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema": [{"Source":"user","ID":"employeeid","SamlClaimType":"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name","JwtClaimType":"name"},{"Source":"company","ID":" tenantcountry ","SamlClaimType":" http://schemas.xmlsoap.org/ws/2005/05/identity/claims/country ","JwtClaimType":"country"}]}}') -DisplayName "ExtraClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. toosee sua nova política e política de saudação tooget ObjectId, Olá execução a seguir de comando:
     
     ``` powershell  
    Get-AzureADPolicy
    ```
2.  Atribua a entidade de serviço Olá política tooyour. Você também precisa tooget Olá ObjectId sua entidade de serviço. 
    1.  toosee entidades de serviço de todas as da sua organização, você pode consultar o Microsoft Graph. Ou, no Azure AD Graph Explorer, entrar tooyour conta AD do Azure.
    2.  Quando você tiver Olá ObjectId do seu Olá de serviço principal, execute comando a seguir:  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
#### <a name="example-create-and-assign-a-policy-that-uses-a-claims-transformation-in-tokens-issued-tooa-service-principal"></a>Exemplo: Criar e atribuir uma política que usa uma transformação de declarações em tokens emitidos tooa serviço principal.
Neste exemplo, você deve criar uma política que emite uma declaração personalizada "JoinedData" tooJWTs emitida toolinked entidades de serviço. Esta declaração contém um valor criado unindo Olá dados armazenados no atributo de extensionattribute1 Olá no objeto de usuário Olá com ".sandbox". Neste exemplo, excluímos declarações básica de Olá definidas nos tokens de saudação.


1. Crie uma política de mapeamento de declarações. Essa política, as entidades de serviço vinculado toospecific, adiciona Olá EmployeeID e TenantCountry tootokens de declarações.
    1. diretiva toocreate hello, execute este comando: 
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema":[{"Source":"user","ID":"extensionattribute1"},{"Source":"transformation","ID":"DataJoin","TransformationId":"JoinTheData","JwtClaimType":"JoinedData"}],"ClaimsTransformation":[{"ID":"JoinTheData","TransformationMethod":"Join","InputClaims":[{"ClaimTypeReferenceId":"extensionattribute1","TransformationClaimType":"string1"}], "InputParameters": [{"Id":"string2","Value":"sandbox"},{"Id":"separator","Value":"."}],"OutputClaims":[{"ClaimTypeReferenceId":"DataJoin","TransformationClaimType":"outputClaim"}]}]}}') -DisplayName "TransformClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. toosee sua nova política e política de saudação tooget ObjectId, Olá execução a seguir de comando: 
     
     ``` powershell
    Get-AzureADPolicy
    ```
2.  Atribua a entidade de serviço Olá política tooyour. Você também precisa tooget Olá ObjectId sua entidade de serviço. 
    1.  toosee entidades de serviço de todas as da sua organização, você pode consultar o Microsoft Graph. Ou, no Azure AD Graph Explorer, entrar tooyour conta AD do Azure.
    2.  Quando você tiver Olá ObjectId do seu Olá de serviço principal, execute comando a seguir: 
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
