---
title: "referência de modelo de dados de modelo de gerenciamento de API aaaAzure | Microsoft Docs"
description: "Saiba mais sobre as representações Olá de entidade e o tipo para itens comuns usados em modelos de dados de saudação para modelos de portal Olá desenvolvedor no gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: b0ad7e15-9519-4517-bb73-32e593ed6380
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 7d049d8ecc9e597cf48ce0c820c172798bcf86de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-template-data-model-reference"></a>Referência de modelo de dados de modelo do Gerenciamento de API do Azure
Este tópico descreve as representações Olá de entidade e o tipo para itens comuns usados em modelos de dados de saudação para modelos de portal Olá desenvolvedor no gerenciamento de API do Azure.  
  
 Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá portal do desenvolvedor do gerenciamento de API usando modelos](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
-   [API](#API)  
-   [Resumo da API](#APISummary)  
-   [Aplicativo](#Application)  
-   [Anexo](#Attachment)  
-   [Exemplo de código](#Sample)  
-   [Comentário](#Comment)  
-   [Filtragem](#Filtering)  
-   [Cabeçalho](#Header)  
-   [Solicitação HTTP](#HTTPRequest)  
-   [Resposta HTTP](#HTTPResponse)  
-   [Problema](#Issue)  
-   [Operação](#Operation)  
-   [Menu de operação](#Menu)  
-   [Item de menu de operação](#MenuItem)  
-   [Paginação](#Paging)  
-   [Parâmetro](#Parameter)  
-   [Produto](#Product)  
-   [Provedor](#Provider)  
-   [Representação](#Representation)  
-   [Assinatura](#Subscription)  
-   [Resumo da assinatura](#SubscriptionSummary)  
-   [Informações de conta de usuário](#UserAccountInfo)  
-   [Entrada do usuário](#UseSignIn)  
-   [Inscrição do usuário](#UserSignUp)  
  
##  <a name="API"></a> API  
 Olá `API` entidade tem Olá propriedades a seguir.  
  
|Propriedade|Tipo|Descrição|  
|--------------|----------|-----------------|  
|ID|string|Identificador de recurso. Identifica exclusivamente a API Olá na instância de serviço de gerenciamento de API atual hello. valor de saudação é uma URL relativa válida no formato de saudação do `apis/{id}` onde `{id}` é um identificador de API. Essa propriedade é somente leitura.|  
|name|string|Nome da saudação API. Não deve ficar vazio. O comprimento máximo é de 100 caracteres.|  
|description|string|Descrição da saudação API. Não deve ficar vazio. Pode incluir marcas de formatação HTML. O comprimento máximo é de 1000 caracteres.|  
|serviceUrl|string|URL absoluta do serviço de back-end Olá implementar essa API.|  
|path|string|URL relativa identificando exclusivamente esta API e todos os seus caminhos de recurso na instância do serviço de gerenciamento de API de saudação. Ele é adicionado URL base do ponto de extremidade toohello API especificada durante a saudação tooform de criação de instância de serviço uma URL pública para esta API.|  
|protocols|matriz de números|Descreve em qual Olá protocolos operações nessa API podem ser invocadas. Os valores permitidos são `1 - http` e `2 - https` ou ambos.|  
|authenticationSettings|[Authorization server authentication settings](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#AuthenticationSettings) (Configurações de autenticação do servidor de autorização)|Coleção de configurações de autenticação incluídas nessa API.|  
|subscriptionKeyParameterNames|objeto|Propriedade opcional que pode ser nomes personalizados de toospecify usado para parâmetros de consulta e/ou cabeçalho que contém a chave de assinatura de saudação. Quando essa propriedade estiver presente, ele deve conter pelo menos uma das duas propriedades a seguir hello.<br /><br /> `{   "subscriptionKeyParameterNames":   {     "query": “customQueryParameterName",     "header": “customHeaderParameterName"   } }`|  
  
##  <a name="APISummary"></a> Resumo da API  
 Olá `API summary` entidade tem Olá propriedades a seguir.  
  
|Propriedade|Tipo|Descrição|  
|--------------|----------|-----------------|  
|ID|string|Identificador de recurso. Identifica exclusivamente a API Olá na instância de serviço de gerenciamento de API atual hello. valor de saudação é uma URL relativa válida no formato de saudação do `apis/{id}` onde `{id}` é um identificador de API. Essa propriedade é somente leitura.|  
|name|string|Nome da saudação API. Não deve ficar vazio. O comprimento máximo é de 100 caracteres.|  
|description|string|Descrição da saudação API. Não deve ficar vazio. Pode incluir marcas de formatação HTML. O comprimento máximo é de 1000 caracteres.|  
  
##  <a name="Application"></a> Aplicativo  
 Olá `application` entidade tem Olá propriedades a seguir.  
  
|Propriedade|Tipo|Descrição|  
|--------------|----------|-----------------|  
|ID|string|Identificador exclusivo de saudação do aplicativo hello.|  
|Title|string|título de saudação do aplicativo hello.|  
|Descrição|string|Descrição de saudação do aplicativo hello.|  
|Url|URI|Olá URI para o aplicativo hello.|  
|Versão|string|Informações de versão para o aplicativo hello.|  
|Requisitos|string|Uma descrição dos requisitos para o aplicativo hello.|  
|Estado|número|estado atual de saudação do aplicativo hello.<br /><br /> – 0 – Registrado<br /><br /> – 1 – Enviado<br /><br /> – 2 – Publicado<br /><br /> – 3 – Rejeitado<br /><br /> – 4 – Não publicado|  
|RegistrationDate|Datetime|aplicativo de saudação de data e hora Hello foi registrado.|  
|CategoryId|número|categoria de saudação do aplicativo hello (Finanças, entretenimento, etc.)|  
|DeveloperId|string|Identificador exclusivo de saudação do desenvolvedor Olá que enviou o aplicativo hello.|  
|Anexos|Coleção de entidades de [Anexo](#Attachment).|Todos os anexos para o aplicativo hello como capturas de tela ou ícones.|  
|ícone|[Anexo](#Attachment)|Olá Olá de ícone para o aplicativo hello.|  
  
##  <a name="Attachment"></a> Anexo  
 Olá `attachment` entidade tem Olá propriedades a seguir.  
  
|Propriedade|Tipo|Descrição|  
|--------------|----------|-----------------|  
|UniqueId|string|Olá identificador exclusivo para o anexo hello.|  
|Url|string|URL de saudação do recurso de saudação.|  
|Tipo|string|tipo de saudação do anexo.|  
|ContentType|string|tipo de mídia de saudação do anexo hello.|  
  
##  <a name="Sample"></a> Exemplo de código  
  
|Propriedade|Tipo|Descrição|  
|--------------|----------|-----------------|  
|título|string|nome de saudação da operação de saudação.|  
|snippet|string|Essa propriedade foi preterida e não deve ser usada.|  
|brush|string|Qual o código de modelo toobe usada ao exibir um exemplo de código a saudação da coloração de sintaxe. Os valores permitidos são `plain`, `php`, `java`, `xml`, `objc`, `python`, `ruby` e `csharp`.|  
|template|string|nome da saudação desse modelo de exemplo de código.|  
|body|string|Um espaço reservado para a parte do exemplo de código Olá trecho hello.|  
|estático|string|método HTTP da operação de saudação do Hello.|  
|scheme|string|Olá toouse de protocolo para a solicitação de operação de saudação.|  
|path|string|caminho de saudação da operação de saudação.|  
|query|string|Exemplo de cadeia de caracteres de consulta com parâmetros definidos.|  
|host|string|URL de saudação do gateway do serviço de gerenciamento de API Olá para Olá API que contém esta operação.|  
|headers|Coleção de entidades de [Cabeçalho](#Header).|Cabeçalhos para esta operação.|  
|parameters|Coleção de entidade de [Parâmetro](#Parameter).|Parâmetros que são definidos para essa operação.|  
  
##  <a name="Comment"></a> Comentário  
 Olá `API` entidade tem Olá propriedades a seguir.  
  
|Propriedade|Tipo|Descrição|  
|--------------|----------|-----------------|  
|ID|número|id de saudação do comentário hello.|  
|CommentText|string|corpo de saudação do comentário hello. Pode incluir HTML.|  
|DeveloperCompany|string|nome da empresa do desenvolvedor Olá Olá.|  
|PostedOn|Datetime|comentário de saudação de data e hora Olá foi postado.|  
  
##  <a name="Issue"></a> Problema  
 Olá `issue` entidade tem Olá propriedades a seguir.  
  
|Propriedade|Tipo|Descrição|  
|--------------|----------|-----------------|  
|ID|string|Olá identificador exclusivo para o problema de saudação.|  
|ApiID|string|id de Olá Olá API para o qual esse problema foi relatado.|  
|Title|string|Título do problema de saudação.|  
|Descrição|string|Descrição do problema de saudação.|  
|SubscriptionDeveloperName|string|Nome do desenvolvedor de saudação que Olá problema reportado.|  
|IssueState|string|estado atual de saudação do problema de saudação. Os valores possíveis são Proposto, Aberto e Fechado.|  
|ReportedOn|Datetime|problema de saudação de data e hora Olá foi relatado.|  
|Comentários|Coleção de entidades de [Comentário](#Comment).|Comentários sobre este problema.|  
|Anexos|Coleção de entidades de [Anexo](api-management-template-data-model-reference.md#Attachment).|Qualquer problema de toohello anexos.|  
|Serviços|Coleção de entidades de [API](#API).|Olá APIs inscrito usuário Olá tooby arquivada, o problema de saudação.|  
  
##  <a name="Filtering"></a> Filtragem  
 Olá `filtering` entidade tem Olá propriedades a seguir.  
  
|Propriedade|Tipo|Descrição|  
|--------------|----------|-----------------|  
|Padrão|string|termo de pesquisa atual Olá; ou `null` se não houver nenhum termo de pesquisa.|  
|Placeholder|string|Olá toodisplay de texto na caixa de pesquisa hello quando não houver nenhum termo de pesquisa especificado.|  
  
##  <a name="Header"></a> Cabeçalho  
 Esta seção descreve Olá `parameter` representação.  
  
|Propriedade|Descrição|Tipo|  
|--------------|-----------------|----------|  
|name|string|Nome do parâmetro.|  
|description|string|Descrição do parâmetro.|  
|valor|string|Valor do cabeçalho.|  
|typeName|string|Tipo de dados do valor do cabeçalho.|  
|options|string|Opções.|  
|obrigatório|Booliano|Se o cabeçalho de saudação é necessário.|  
|readOnly|Booliano|Se o cabeçalho de saudação é somente leitura.|  
  
##  <a name="HTTPRequest"></a> Solicitação HTTP  
 Esta seção descreve Olá `request` representação.  
  
|Propriedade|Tipo|Descrição|  
|--------------|----------|-----------------|  
|description|string|Descrição da solicitação de operação.|  
|Cabeçalhos|matriz de entidades de [Cabeçalho](#Header).|Cabeçalhos de solicitação.|  
|parameters|matriz de [Parâmetro](#Parameter)|Coleção de parâmetros de solicitação da operação.|  
|representations|matriz de [Representação](#Representation)|Coleção de representações de solicitação da operação.|  
  
##  <a name="HTTPResponse"></a> Resposta HTTP  
 Esta seção descreve Olá `response` representação.  
  
|Propriedade|Tipo|Descrição|  
|--------------|----------|-----------------|  
|statusCode|número inteiro positivo|Código de status de resposta da operação.|  
|description|string|Descrição da resposta da operação.|  
|representations|matriz de [Representação](#Representation)|Coleção de representações de resposta da operação.|  
  
##  <a name="Operation"></a> Operação  
 Olá `operation` entidade tem Olá propriedades a seguir.  
  
|Propriedade|Tipo|Descrição|  
|--------------|----------|-----------------|  
|ID|string|Identificador de recurso. Identifica exclusivamente a operação de saudação na instância de serviço de gerenciamento de API atual hello. valor de saudação é uma URL relativa válida no formato de saudação do `apis/{aid}/operations/{id}` onde `{aid}` é um identificador de API e `{id}` é um identificador de operação. Essa propriedade é somente leitura.|  
|name|string|Nome da operação de saudação. Não deve ficar vazio. O comprimento máximo é de 100 caracteres.|  
|description|string|Descrição da operação de saudação. Não deve ficar vazio. Pode incluir marcas de formatação HTML. O comprimento máximo é de 1000 caracteres.|  
|scheme|string|Descreve em qual Olá protocolos operações nessa API podem ser invocadas. Os valores permitidos são `http` e `https` ou `http` e `https`.|  
|uriTemplate|string|Modelo de URL relativa identificando Olá recurso de destino para esta operação. Pode incluir parâmetros. Exemplo: `customers/{cid}/orders/{oid}/?date={date}`|  
|host|string|Olá URL de gateway de gerenciamento de API que hospeda a API de saudação.|  
|httpMethod|string|Método HTTP da operação.|  
|solicitação|[Solicitação HTTP](#HTTPRequest)|Uma entidade que contém detalhes da solicitação.|  
|responses|matriz de [Resposta HTTP](#HTTPResponse)|Matriz de entidades de [Resposta HTTP](#HTTPResponse) da operação.|  
  
##  <a name="Menu"></a> Menu de operação  
 Olá `operation menu` entidade tem Olá propriedades a seguir.  
  
|Propriedade|Tipo|Descrição|  
|--------------|----------|-----------------|  
|ApiId|string|id de saudação da API de saudação atual.|  
|CurrentOperationId|string|id de saudação da operação atual de saudação.|  
|Ação|string|tipo de menu Hello.|  
|MenuItems|Coleção de entidades de [Item de menu de operação](#MenuItem).|operações de saudação para API atual hello.|  
  
##  <a name="MenuItem"></a> Item de menu de operação  
 Olá `operation menu item` entidade tem Olá propriedades a seguir.  
  
|Propriedade|Tipo|Descrição|  
|--------------|----------|-----------------|  
|ID|string|id de saudação da operação de saudação.|  
|Title|string|Descrição de saudação da operação de saudação.|  
|HttpMethod|string|método Http da operação de saudação do Hello.|  
  
##  <a name="Paging"></a> Paginação  
 Olá `paging` entidade tem Olá propriedades a seguir.  
  
|Propriedade|Tipo|Descrição|  
|--------------|----------|-----------------|  
|Página|número|número da página atual Hello.|  
|PageSize|número|Olá toobe máximo de resultados exibido em uma única página.|  
|TotalItemCount|número|número de saudação de itens para exibição.|  
|ShowAll|Booliano|Se toosho todos os resultados em uma única página.|  
|PageCount|número|número de saudação de páginas de resultados.|  
  
##  <a name="Parameter"></a> Parâmetro  
 Esta seção descreve Olá `parameter` representação.  
  
|Propriedade|Descrição|Tipo|  
|--------------|-----------------|----------|  
|name|string|Nome do parâmetro.|  
|description|string|Descrição do parâmetro.|  
|valor|string|Valor de parâmetro.|  
|options|matriz de cadeias de caracteres|Valores definidos para os valores de parâmetro de consulta.|  
|obrigatório|booleano|Especifica se o parâmetro é necessário ou não.|  
|kind|número|Se esse parâmetro for um parâmetro de caminho (1) ou um parâmetro de cadeia de caracteres de consulta (2).|  
|typeName|string|Tipo de parâmetro.|  
  
##  <a name="Product"></a> Produto  
 Olá `product` entidade tem Olá propriedades a seguir.  
  
|Propriedade|Tipo|Descrição|  
|--------------|----------|-----------------|  
|ID|string|Identificador de recurso. Identifica exclusivamente o produto Olá na instância de serviço de gerenciamento de API atual hello. valor de saudação é uma URL relativa válida no formato de saudação do `products/{pid}` onde `{pid}` é um identificador de produto. Essa propriedade é somente leitura.|  
|Title|string|Nome do produto de saudação. Não deve ficar vazio. O comprimento máximo é de 100 caracteres.|  
|Descrição|string|Descrição do produto hello. Não deve ficar vazio. Pode incluir marcas de formatação HTML. O comprimento máximo é de 1000 caracteres.|  
|Termos|string|Termos de uso do produto. Desenvolvedores tentar toosubscribe toohello produto serão exibidos e necessário tooaccept esses termos antes de poderem concluir o processo de assinatura hello.|  
|ProductState|número|Especifica se o produto de saudação é publicado ou não. Os produtos publicados são detectáveis por desenvolvedores no portal do desenvolvedor hello. Os produtos não publicados são visíveis tooadministrators somente.<br /><br /> Olá os valores permitidos para o estado do produto são:<br /><br /> - `0 - Not Published`<br /><br /> - `1 - Published`<br /><br /> - `2 - Deleted`|  
|AllowMultipleSubscriptions|Booliano|Especifica se um usuário pode ter vários produtos de toothis de assinaturas no hello simultaneamente.|  
|MultipleSubscriptionsCount|número|Olá número de assinaturas toothis produto pelo usuário atual hello.|  
  
##  <a name="Provider"></a> Provedor  
 Olá `provider` entidade tem Olá propriedades a seguir.  
  
|Propriedade|Tipo|Descrição|  
|--------------|----------|-----------------|  
|Propriedades|dicionário de cadeia de caracteres|Propriedades desse provedor de autenticação.|  
|AuthenticationType|string|tipo de provedor de saudação. (Azure Active Directory, logon do Facebook, Conta do Google, Conta da Microsoft, Twitter).|  
|Legenda|string|Nome de exibição do provedor de saudação.|  
  
##  <a name="Representation"></a> Representação  
 Esta seção descreve uma `representation`.  
  
|Propriedade|Tipo|Descrição|  
|--------------|----------|-----------------|  
|contentType|string|Especifica um tipo de conteúdo personalizado ou registrado para essa representação, por exemplo, `application/xml`.|  
|exemplo|string|Um exemplo de representação de saudação.|  
  
##  <a name="Subscription"></a> Assinatura  
 Olá `subscription` entidade tem Olá propriedades a seguir.  
  
|Propriedade|Tipo|Descrição|  
|--------------|----------|-----------------|  
|ID|string|Identificador de recurso. Identifica exclusivamente a assinatura de saudação na instância de serviço de gerenciamento de API atual hello. valor de saudação é uma URL relativa válida no formato de saudação do `subscriptions/{sid}` onde `{sid}` é um identificador de assinatura. Essa propriedade é somente leitura.|  
|ProductId|string|Identificador de recurso de produto de saudação do hello inscrito produto. valor de saudação é uma URL relativa válida no formato de saudação do `products/{pid}` onde `{pid}` é um identificador de produto.|  
|ProductTitle|string|Nome do produto de saudação. Não deve ficar vazio. O comprimento máximo é de 100 caracteres.|  
|ProductDescription|string|Descrição do produto hello. Não deve ficar vazio. Pode incluir marcas de formatação HTML. O comprimento máximo é de 1000 caracteres.|  
|ProductDetailsUrl|string|Detalhes de produto de toohello de URL relativos.|  
|state|string|estado de saudação de assinatura de saudação. Os possíveis estados são:<br /><br /> - `0 - suspended`– Olá assinatura está bloqueada e assinante Olá não é possível chamar quaisquer APIs do produto hello.<br /><br /> - `1 - active`– Olá assinatura está ativa.<br /><br /> - `2 - expired`– Olá atingiu sua data de expiração e foi desativada.<br /><br /> - `3 - submitted`– solicitação de assinatura de saudação foi feita pelo desenvolvedor hello, mas ainda não foi aprovada ou rejeitada.<br /><br /> - `4 - rejected`– solicitação de assinatura de saudação foi negada por um administrador.<br /><br /> - `5 - cancelled`– Olá assinatura foi cancelada pelo administrador ou desenvolvedor de saudação.|  
|DisplayName|string|Nome de exibição de assinatura de saudação.|  
|CreatedDate|dateTime|assinatura de saudação do Hello data foi criada, no formato ISO 8601: `2014-06-24T16:25:00Z`.|  
|CanBeCancelled|Booliano|Se a assinatura Olá pode ser cancelada pelo usuário atual hello.|  
|IsAwaitingApproval|Booliano|Se a assinatura de saudação está aguardando aprovação.|  
|StartDate|dateTime|Olá data de início de assinatura hello, no formato ISO 8601: `2014-06-24T16:25:00Z`.|  
|ExpirationDate|dateTime|Olá data de expiração Olá assinatura, no formato ISO 8601: `2014-06-24T16:25:00Z`.|  
|NotificationDate|dateTime|Data de notificação Olá para assinatura hello, no formato ISO 8601: `2014-06-24T16:25:00Z`.|  
|primaryKey|string|chave de assinatura principal Hello. O comprimento máximo é de 256 caracteres.|  
|secondaryKey|string|chave de assinatura secundária Hello. O comprimento máximo é de 256 caracteres.|  
|CanBeRenewed|Booliano|Se a assinatura Olá poderá ser renovada pelo usuário atual hello.|  
|HasExpired|Booliano|Se a assinatura de saudação expirou.|  
|IsRejected|Booliano|Se a solicitação de assinatura de saudação foi negada.|  
|CancelUrl|string|Olá relativo Url toocancel Olá assinatura.|  
|RenewUrl|string|Olá relativo Url toorenew Olá assinatura.|  
  
##  <a name="SubscriptionSummary"></a> Resumo da assinatura  
 Olá `subscription summary` entidade tem Olá propriedades a seguir.  
  
|Propriedade|Tipo|Descrição|  
|--------------|----------|-----------------|  
|ID|string|Identificador de recurso. Identifica exclusivamente a assinatura de saudação na instância de serviço de gerenciamento de API atual hello. valor de saudação é uma URL relativa válida no formato de saudação do `subscriptions/{sid}` onde `{sid}` é um identificador de assinatura. Essa propriedade é somente leitura.|  
|DisplayName|string|Olá exibir o nome da assinatura Olá|  
  
##  <a name="UserAccountInfo"></a> Informações de conta de usuário  
 Olá `user account info` entidade tem Olá propriedades a seguir.  
  
|Propriedade|Tipo|Descrição|  
|--------------|----------|-----------------|  
|Nome|string|Nome. Não deve ficar vazio. O comprimento máximo é de 100 caracteres.|  
|Sobrenome|string|Sobrenome. Não deve ficar vazio. O comprimento máximo é de 100 caracteres.|  
|Email|string|Endereço de email. Não deve estar vazio e deve ser exclusivo na instância do serviço de saudação. O comprimento máximo é de 254 caracteres.|  
|Senha|string|Senha da conta de usuário.|  
|NameIdentifier|string|Identificador de conta, hello mesmo que o email do usuário hello.|  
|ProviderName|string|Nome do provedor de autenticação.|  
|IsBasicAccount|Booliano|True se esta conta foi registrada usando o email e senha. False se a conta de saudação foi registrada usando um provedor.|  
  
##  <a name="UseSignIn"></a> Entrada do usuário  
 Olá `user sign in` entidade tem Olá propriedades a seguir.  
  
|Propriedade|Tipo|Descrição|  
|--------------|----------|-----------------|  
|Email|string|Endereço de email. Não deve estar vazio e deve ser exclusivo na instância do serviço de saudação. O comprimento máximo é de 254 caracteres.|  
|Senha|string|Senha da conta de usuário.|  
|ReturnUrl|string|Olá o URL da página de saudação em que o usuário Olá clicou entrar.|  
|RememberMe|Booliano|Se toosave Olá informações do usuário atual.|  
|RegistrationEnabled|booleano|Se o registro está habilitado.|  
|DelegationEnabled|booleano|Se a entrada delegada está habilitada.|  
|DelegationUrl|string|Olá delegado logon na url, se habilitado.|  
|SsoSignUpUrl|string|Olá única URL de logon de usuário hello, se estiver presente.|  
|AuxServiceUrl|string|Se o usuário atual Olá for um administrador, isso é uma instância de serviço do link toohello em Olá Portal clássico do Azure.|  
|Provedores|Coleção de entidades de [Provedor](#Provider)|Olá provedores de autenticação para este usuário.|  
|UserRegistrationTerms|string|Termos que um usuário deve concordar toobefore entrar.|  
|UserRegistrationTermsEnabled|booleano|Se os termos estão habilitados.|  
  
##  <a name="UserSignUp"></a> Inscrição do usuário  
 Olá `user sign up` entidade tem Olá propriedades a seguir.  
  
|Propriedade|Tipo|Descrição|  
|--------------|----------|-----------------|  
|PasswordConfirm|Booliano|Valor usado pelo Olá [inscrição](api-management-page-controls.md#sign-up)controle inscrição.|  
|Senha|string|Senha da conta de usuário.|  
|PasswordVerdictLevel|número|Valor usado pelo Olá [inscrição](api-management-page-controls.md#sign-up)controle inscrição.|  
|UserRegistrationTerms|string|Termos que um usuário deve concordar toobefore entrar.|  
|UserRegistrationTermsOptions|número|Valor usado pelo Olá [inscrição](api-management-page-controls.md#sign-up)controle inscrição.|  
|ConsentAccepted|Booliano|Valor usado pelo Olá [inscrição](api-management-page-controls.md#sign-up)controle inscrição.|  
|Email|string|Endereço de email. Não deve estar vazio e deve ser exclusivo na instância do serviço de saudação. O comprimento máximo é de 254 caracteres.|  
|Nome|string|Nome. Não deve ficar vazio. O comprimento máximo é de 100 caracteres.|  
|Sobrenome|string|Sobrenome. Não deve ficar vazio. O comprimento máximo é de 100 caracteres.|  
|UserData|string|Valor usado pelo Olá [inscrição](api-management-page-controls.md#sign-up) controle.|  
|NameIdentifier|string|Valor usado pelo Olá [inscrição](api-management-page-controls.md#sign-up)controle inscrição.|  
|ProviderName|string|Nome do provedor de autenticação.|

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre como trabalhar com modelos, consulte [como toocustomize Olá portal do desenvolvedor do gerenciamento de API usando modelos](api-management-developer-portal-templates.md).
