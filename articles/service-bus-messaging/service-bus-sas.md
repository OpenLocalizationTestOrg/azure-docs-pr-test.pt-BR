---
title: "autenticação do barramento de serviço aaaAzure com assinaturas de acesso compartilhado | Microsoft Docs"
description: "Visão geral da Autenticação do Barramento de Serviço usando a visão geral de Assinaturas de Acesso Compartilhado, detalhes sobre a autenticação SAS com o Barramento de Serviço do Azure."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: 773bb11720384d7245820b56dc25b8e064ffa746
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-authentication-with-shared-access-signatures"></a>Autenticação do Barramento de Serviço com Assinaturas de Acesso Compartilhado

*Assinaturas de acesso compartilhado* (SAS) são o mecanismo de segurança principal de saudação para mensagens do barramento de serviço. Este artigo aborda SAS, como elas funcionam e como toouse-los de maneira independente de plataforma.

Autenticação SAS permite que aplicativos tooauthenticate tooService barramento usando uma chave de acesso configurada no namespace hello, ou em Olá entidade (fila ou tópico) de mensagens com os direitos específicos associados. Você pode usar essa chave toogenerate um token SAS que os clientes podem usar tooauthenticate tooService barramento.

Suporte para autenticação SAS está incluído no hello Azure SDK versão 2.0 e posterior.

## <a name="overview-of-sas"></a>Visão geral das SAS

Assinaturas de acesso compartilhado são um mecanismo de autenticação com base em hashes seguros SHA-256 ou URIs. As SAS são um mecanismo extremamente poderoso usado por todos os serviços do Barramento de Serviço. Na utilização real, as SAS têm dois componentes: uma *política de acesso compartilhado* e uma *Assinatura de Acesso Compartilhado* (normalmente chamada de *token*).

Autenticação de SAS no barramento de serviço envolve a configuração de saudação de uma chave criptográfica com direitos associados em um recurso de barramento de serviço. Os clientes declaração acesso tooService barramento recursos apresentando um token SAS. Este token é composto Olá URI de recurso que está sendo acessado e uma expiração assinada com hello configurado chave.

É possível configurar regras de autorização de Assinatura de Acesso Compartilhado nas [retransmissões](service-bus-fundamentals-hybrid-solutions.md#relays), [filas](service-bus-fundamentals-hybrid-solutions.md#queues) e [tópicos](service-bus-fundamentals-hybrid-solutions.md#topics) do Barramento de Serviço.

A autenticação SAS utiliza Olá elementos a seguir:

* [Regra de autorização de Acesso Compartilhado](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule): uma chave criptográfica primária de 256 bits na representação Base64, uma chave secundária opcional e um nome de chave e os direitos associados (uma coleção de direitos *Listen*, *Send* ou *Manage*).
* [Assinatura de acesso compartilhado](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) token: gerado usando hello HMAC-SHA256 de uma cadeia de caracteres de recurso, consistindo de saudação URI do recurso de saudação que é acessado e uma expiração, com a chave de criptografia de saudação. assinatura de saudação e outros elementos descritos nas seções a seguir de saudação são formatados em uma saudação tooform de cadeia de caracteres token SAS.

## <a name="shared-access-policy"></a>Política de acesso compartilhado

Um toounderstand importante sobre SAS é que ela começa com uma política. Para cada política, você toma decisões quanto a três informações: **nome**, **escopo** e **permissões**. Olá **nome** é apenas; um nome exclusivo dentro do escopo. Olá escopo é muito fácil: seu Olá URI do recurso de saudação em questão. Para um namespace de barramento de serviço, Olá escopo é nome hello de domínio totalmente qualificado (FQDN), como `https://<yournamespace>.servicebus.windows.net/`.

as permissões disponíveis para uma política de saudação são autoexplicativas amplamente:

* Enviar
* Escutar
* Gerenciar

Depois de criar a política de saudação, ela é atribuída um *chave primária* e um *chave secundária*. Essas chaves são criptograficamente fortes. Não perdê-los ou vazá-los - sempre estarão disponíveis em Olá [portal do Azure][Azure portal]. Você pode usar qualquer uma das chaves de saudação gerada, e pode gerá-los novamente a qualquer momento. No entanto, se você gerar novamente ou alterar a chave primária Olá na política de hello, quaisquer assinaturas de acesso compartilhado criado a partir dele serão invalidadas.

Quando você cria um namespace de barramento de serviço, uma política é criada automaticamente para Olá todo namespace chamado **RootManageSharedAccessKey**, e essa política tem todas as permissões. Você não faz logon como **raiz**. Você pode criar políticas adicionais em Olá **configurar** guia Olá espaço para nome no portal de saudação. É importante toonote que um nível de árvore única no barramento de serviço (namespace, fila, etc.) só pode ter até too12 políticas anexadas tooit.

## <a name="configuration-for-shared-access-signature-authentication"></a>Configuração da autenticação de Assinatura de Acesso Compartilhado
Você pode configurar Olá [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) regra em namespaces de barramento de serviço, filas ou tópicos. Configurando um [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) em um barramento de serviço de assinatura não é suportada atualmente, mas você pode usar regras configuradas em um toosubscriptions de acesso toosecure namespace ou tópico. Para obter um exemplo de trabalho que ilustra este procedimento, consulte Olá [autenticação usando SAS Shared Access Signature () com assinaturas do barramento de serviço](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c) exemplo.

Você pode configurar até 12 dessas regras em um namespace, fila ou tópico do Barramento de Serviço. As regras configuradas em um namespace de barramento de serviço aplicam tooall entidades naquele namespace.

![SAS](./media/service-bus-sas/service-bus-namespace.png)

Nesta figura, Olá *manageRuleNS*, *sendRuleNS*, e *listenRuleNS* se aplicam regras de autorização tooboth fila Q1 e tópico T1, enquanto *listenRuleQ*  e *sendRuleQ* aplicar tooqueue Q1 e *sendRuleT* aplica-se apenas tootopic T1.

Olá parâmetros de chave de um [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) são da seguinte maneira:

| Parâmetro | Descrição |
| --- | --- |
| *KeyName* |Uma cadeia de caracteres que descreve a regra de autorização de saudação. |
| *PrimaryKey* |Uma codificada em base64 de 256 bits chave primária para assinar e validar o token SAS hello. |
| *SecondaryKey* |Uma codificada em base64 de 256 bits chave secundária para assinar e validar o token SAS hello. |
| *AccessRights* |Uma lista de direitos de acesso concedidos pela regra de autorização de saudação. Esses direitos podem ser qualquer coleção de direitos Escutar, Enviar e Gerenciar. |

Quando um namespace de barramento de serviço é provisionado, um [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule), com [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName) definido muito**RootManageSharedAccessKey**, é criado por padrão.

## <a name="generate-a-shared-access-signature-token"></a>Gerar uma Assinatura de Acesso Compartilhado (token)

política de saudação em si não é token de acesso de saudação do Service Bus. É objeto de saudação do qual Olá token de acesso é gerado - usando a chave primária ou secundária de saudação. Qualquer cliente que tenha acesso toohello assinatura chaves especificadas na regra de autorização de acesso compartilhado Olá pode gerar o token SAS de saudação. Olá token é gerado ao criar cuidadosamente uma cadeia de caracteres hello formato a seguir:

```
SharedAccessSignature sig=<signature-string>&se=<expiry>&skn=<keyName>&sr=<URL-encoded-resourceURI>
```

Onde `signature-string` é Olá SHA-256 hash de escopo de saudação do token de saudação (**escopo** conforme descrito na seção anterior Olá) com CRLF anexado e uma hora de expiração (em segundos desde a época Olá: `00:00:00 UTC` em 1 de janeiro de 1970). 

> [!NOTE]
> tooavoid um tempo de expiração do token curto, é recomendável que você codifica o valor de tempo de expiração de saudação como pelo menos um inteiro de 32 bits sem sinal ou preferência um inteiro longo (64 bits).  
> 
> 

hash de saudação parece semelhante toohello pseudocódigo a seguir e retorna 32 bytes.

```
SHA-256('https://<yournamespace>.servicebus.windows.net/'+'\n'+ 1438205742)
```

valores de hash não Olá estão em Olá **SharedAccessSignature** que hello destinatário pode calcular o hash de saudação sequência com hello os mesmos parâmetros, toobe-se de que ela retorna Olá mesmo resultado. Olá URI especifica o escopo de saudação e nome da chave Olá identifica Olá política toobe usado toocompute Olá hash. Isso é importante de um ponto de vista de segurança. Se Olá não coincide com que calcula o destinatário que hello (barramento de serviço), o acesso é negado. Agora você poderá ter certeza remetente Olá tinha a chave de acesso de toohello e deve ter direitos de saudação especificado na diretiva de saudação.

Observe que você deve usar o URI do recurso Olá codificado para esta operação. URI de recurso Olá é hello que URI completo do hello acesso aos toowhich de recursos de barramento de serviço é solicitado. Por exemplo, `http://<namespace>.servicebus.windows.net/<entityPath>` ou `sb://<namespace>.servicebus.windows.net/<entityPath>`; ou seja, `http://contoso.servicebus.windows.net/contosoTopics/T1/Subscriptions/S3`.

regra de autorização de acesso compartilhado Olá usada para a assinatura deve ser configurada na entidade Olá especificada por esse URI, ou por um de seus pais hierárquicos. Por exemplo, `http://contoso.servicebus.windows.net/contosoTopics/T1` ou `http://contoso.servicebus.windows.net` no exemplo anterior de saudação.

Um token SAS é válido para todos os recursos em Olá `<resourceURI>` usado em Olá `signature-string`.

Olá [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName) Olá SAS token refere-se toohello **keyName** de saudação regra de autorização de acesso compartilhado usada toogenerate token de saudação.

Olá *URL-encoded-resourceURI* devem ser Olá mesmo Olá URI usado na cadeia de caracteres a assinar Olá durante a computação de saudação da assinatura de saudação. Ele deve ser [codificado por percentual](https://msdn.microsoft.com/library/4fkewx0t.aspx).

Recomenda-se regenerar periodicamente chaves Olá usadas em Olá [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) objeto. Aplicativos devem geralmente usar Olá [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) toogenerate um token SAS. Ao regenerar chaves hello, você deve substituir Olá [SecondaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) com primário antigo Olá chave e gerar uma nova chave de uma nova chave primária de saudação. Isso permite que você toocontinue usando tokens de autorização que foram emitidos com a chave primária antiga de saudação e que ainda não expirou.

Se uma chave estiver comprometida e você tiver toorevoke Olá chaves, você pode regenerar ambos Olá [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) e hello [SecondaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) de um [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule), substituí-los com as novas chaves. Este procedimento invalida todos os tokens assinados com chaves antigas hello.

## <a name="how-toouse-shared-access-signature-authentication-with-service-bus"></a>Como toouse autenticação de SAS com barramento de serviço

Olá os seguintes cenários incluem configuração de regras de autorização, geração de tokens SAS e autorização do cliente.

Para uma completa da amostra de funcionamento de um aplicativo de barramento de serviço que ilustra Olá configuração e utiliza a autorização SAS, consulte [autenticação SAS com barramento de serviço](http://code.msdn.microsoft.com/Shared-Access-Signature-0a88adf8). Um exemplo relacionado que ilustra o uso de saudação de regras de autorização SAS configuradas em namespaces ou tópicos assinaturas do barramento de serviço toosecure está disponível aqui: [autenticação usando SAS Shared Access Signature () com assinaturas do barramento de serviço ](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c).

## <a name="access-shared-access-authorization-rules-on-a-namespace"></a>Acessar regras de autorização de Acesso Compartilhado em um namespace

Operações na raiz do namespace de barramento de serviço Olá exigem autenticação de certificado. Você deve carregar um certificado de gerenciamento da sua assinatura do Azure. tooupload um certificado de gerenciamento, execute as etapas de saudação [aqui](../cloud-services/cloud-services-configure-ssl-certificate-portal.md#step-3-upload-a-certificate), usando Olá [portal do Azure][Azure portal]. Para obter mais informações sobre certificados de gerenciamento do Azure, consulte Olá [visão geral de certificados do Azure](../cloud-services/cloud-services-certs-create.md#what-are-management-certificates).

ponto de extremidade Olá para acessar regras de autorização de acesso compartilhado em um namespace de barramento de serviço é o seguinte:

```http
https://management.core.windows.net/{subscriptionId}/services/ServiceBus/namespaces/{namespace}/AuthorizationRules/
```

toocreate um [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) de objeto em um namespace de barramento de serviço, execute uma operação POST nesse ponto de extremidade com informações de regra de saudação serializadas como JSON ou XML. Por exemplo:

```csharp
// Base address for accessing authorization rules on a namespace
string baseAddress = @"https://management.core.windows.net/<subscriptionId>/services/ServiceBus/namespaces/<namespace>/AuthorizationRules/";

// Configure authorization rule with base64-encoded 256-bit key and Send rights
var sendRule = new SharedAccessAuthorizationRule("contosoSendAll",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Send });

// Operations on hello Service Bus namespace root require certificate authentication.
WebRequestHandler handler = new WebRequestHandler
{
    ClientCertificateOptions = ClientCertificateOption.Manual
};
// Access hello management certificate by subject name
handler.ClientCertificates.Add(GetCertificate(<certificateSN>));

HttpClient httpClient = new HttpClient(handler)
{
    BaseAddress = new Uri(baseAddress)
};
httpClient.DefaultRequestHeaders.Accept.Add(
    new MediaTypeWithQualityHeaderValue("application/json"));
httpClient.DefaultRequestHeaders.Add("x-ms-version", "2015-01-01");

// Execute a POST operation on hello baseAddress above toocreate an auth rule
var postResult = httpClient.PostAsJsonAsync("", sendRule).Result;
```

Da mesma forma, use uma operação GET hello ponto de extremidade tooread Olá das regras de autorização configuradas no namespace de saudação.

tooupdate ou excluir uma regra de autorização específica, use Olá ponto de extremidade a seguir:

```http
https://management.core.windows.net/{subscriptionId}/services/ServiceBus/namespaces/{namespace}/AuthorizationRules/{KeyName}
```

## <a name="access-shared-access-authorization-rules-on-an-entity"></a>Acessar regras de Autorização de Acesso Compartilhado em uma entidade

Você pode acessar uma [Microsoft.ServiceBus.Messaging.SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) objeto configurado em uma fila do barramento de serviço ou o tópico por Olá [AuthorizationRules](/dotnet/api/microsoft.servicebus.messaging.authorizationrules) coleção em Olá correspondente [QueueDescription](/dotnet/api/microsoft.servicebus.messaging.queuedescription) ou [TopicDescription](/dotnet/api/microsoft.servicebus.messaging.topicdescription).

saudação de código a seguir mostra como as regras de autorização tooadd para uma fila.

```csharp
// Create an instance of NamespaceManager for hello operation
NamespaceManager nsm = NamespaceManager.CreateFromConnectionString(
    <connectionString> );
QueueDescription qd = new QueueDescription( <qPath> );

// Create a rule with send rights with keyName as "contosoQSendKey"
// and add it toohello queue description.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoSendKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Send }));

// Create a rule with listen rights with keyName as "contosoQListenKey"
// and add it toohello queue description.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoQListenKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Listen }));

// Create a rule with manage rights with keyName as "contosoQManageKey"
// and add it toohello queue description.
// A rule with manage rights must also have send and receive rights.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoQManageKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] {AccessRights.Manage, AccessRights.Listen, AccessRights.Send }));

// Create hello queue.
nsm.CreateQueue(qd);
```

## <a name="use-shared-access-signature-authorization"></a>Usar a autorização de Assinatura de Acesso Compartilhado

Aplicativos usando Olá SDK .NET do Azure com bibliotecas .NET do barramento de serviço do hello podem usar autorização SAS pela Olá [SharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) classe. Olá, código a seguir ilustra Olá uso da fila de barramento de serviço do hello provedor de token toosend mensagens tooa.

```csharp
Uri runtimeUri = ServiceBusEnvironment.CreateServiceUri("sb",
    <yourServiceNamespace>, string.Empty);
MessagingFactory mf = MessagingFactory.Create(runtimeUri,
    TokenProvider.CreateSharedAccessSignatureTokenProvider(keyName, key));
QueueClient sendClient = mf.CreateQueueClient(qPath);

//Sending hello message tooqueue.
BrokeredMessage helloMessage = new BrokeredMessage("Hello, Service Bus!");
helloMessage.MessageId = "SAS-Sample-Message";
sendClient.Send(helloMessage);
```

Os aplicativos também podem usar SAS para autenticação usando uma cadeia de conexão SAS em métodos que aceitem cadeias de conexão.

Observe que autorização SAS de toouse com retransmissões do barramento de serviço, você pode utilizar chaves SAS configuradas no namespace de barramento de serviço Olá. Se você criar explicitamente uma retransmissão no namespace da saudação ([NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) com um [RelayDescription](/dotnet/api/microsoft.servicebus.messaging.relaydescription)) do objeto, você pode definir regras SAS Olá apenas para essa retransmissão. toouse a autorização SAS com assinaturas do barramento de serviço, você pode usar chaves SAS configuradas em um namespace de barramento de serviço ou em um tópico.

## <a name="use-hello-shared-access-signature-at-http-level"></a>Usar Olá assinatura de acesso compartilhado (no nível HTTP)

Agora que você sabe como toocreate assinaturas de acesso compartilhado para qualquer entidade no barramento de serviço, você está pronto tooperform um HTTP POST:

```http
POST https://<yournamespace>.servicebus.windows.net/<yourentity>/messages
Content-Type: application/json
Authorization: SharedAccessSignature sr=https%3A%2F%2F<yournamespace>.servicebus.windows.net%2F<yourentity>&sig=<yoursignature from code above>&se=1438205742&skn=KeyName
ContentType: application/atom+xml;type=entry;charset=utf-8
``` 

Lembre-se de que isso funciona para tudo. Você pode criar SAS para uma fila, tópico ou assinatura. 

Se você fornecer um remetente ou o cliente um token SAS, eles não tem chave Olá diretamente e não é possível reverter Olá hash tooobtain-lo. Dessa forma, você tem controle sobre o que eles podem acessar e por quanto tempo. Um tooremember mais importante é que, se você alterar a chave primária Olá na política hello, quaisquer assinaturas de acesso compartilhado criado a partir dele serão invalidadas.

## <a name="use-hello-shared-access-signature-at-amqp-level"></a>Olá usar assinatura de acesso compartilhado (no nível do AMQP)

Na seção anterior do hello, você viu como toouse Olá token SAS com uma solicitação HTTP POST para enviar dados toohello barramento de serviço. Como você sabe, você pode acessar o barramento de serviço usando Olá Advanced Message Queuing Protocol (AMQP) que é Olá preferencial protocolo toouse por motivos de desempenho, em muitos cenários. Olá uso do token SAS com AMQP é descrito no documento de saudação [AMQP Claim-Based Security versão 1.0](https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc) rascunho de trabalho que é em desde 2013 mas bem com suporte pelo Azure atualmente.

Antes de iniciar toosend dados tooService barramento, publisher Olá deve enviar o token SAS hello dentro de um AMQP mensagem tooa bem definido AMQP nó denominado **$cbs** (você pode vê-lo como uma fila "especial" usada pelo Olá serviço tooacquire e validar tudo tokens SAS Olá). publicador Olá deve especificar Olá **ReplyTo** campo dentro da mensagem de saudação do AMQP; isso é o nó de saudação no qual Olá serviço responde publicador toohello com resultado Olá Olá de validação de token (um padrão de solicitação/resposta entre publicador e o serviço). Este nó de resposta é criado "em Olá dinamicamente," falar "criação dinâmica de nó remoto", conforme descrito pela especificação de saudação AMQP 1.0. Depois de verificar se que esse token SAS de saudação é válido, publisher Olá pode Avançar e iniciar o serviço de toohello toosend dados.

Olá etapas a seguir mostram como toosend Olá token SAS com protocolo AMQP usando Olá [AMQP.Net Lite](https://github.com/Azure/amqpnetlite) biblioteca. Isso será útil se você não pode usar oficial Olá SDK do barramento de serviço (por exemplo, em WinRT, .net Compact Framework, o .net Framework Micro e Mono) desenvolvendo em C\#. Obviamente, essa biblioteca é útil toohelp entender como baseado em declarações funciona no nível do AMQP hello, como você viu como ele funciona no nível de saudação HTTP (com um HTTP POST solicitação e hello SAS token Olá enviados dentro do cabeçalho "Autorização"). Se não precisar de tal profundo conhecimento sobre AMQP, você pode usar oficial Olá SDK do barramento de serviço com o .net aplicativos do Framework, o que fará isso para você.

### <a name="c35"></a>C&#35;

```csharp
/// <summary>
/// Send claim-based security (CBS) token
/// </summary>
/// <param name="shareAccessSignature">Shared access signature (token) toosend</param>
private bool PutCbsToken(Connection connection, string sasToken)
{
    bool result = true;
    Session session = new Session(connection);

    string cbsClientAddress = "cbs-client-reply-to";
    var cbsSender = new SenderLink(session, "cbs-sender", "$cbs");
    var cbsReceiver = new ReceiverLink(session, cbsClientAddress, "$cbs");

    // construct hello put-token message
    var request = new Message(sasToken);
    request.Properties = new Properties();
    request.Properties.MessageId = Guid.NewGuid().ToString();
    request.Properties.ReplyTo = cbsClientAddress;
    request.ApplicationProperties = new ApplicationProperties();
    request.ApplicationProperties["operation"] = "put-token";
    request.ApplicationProperties["type"] = "servicebus.windows.net:sastoken";
    request.ApplicationProperties["name"] = Fx.Format("amqp://{0}/{1}", sbNamespace, entity);
    cbsSender.Send(request);

    // receive hello response
    var response = cbsReceiver.Receive();
    if (response == null || response.Properties == null || response.ApplicationProperties == null)
    {
        result = false;
    }
    else
    {
        int statusCode = (int)response.ApplicationProperties["status-code"];
        if (statusCode != (int)HttpStatusCode.Accepted && statusCode != (int)HttpStatusCode.OK)
        {
            result = false;
        }
    }

    // hello sender/receiver may be kept open for refreshing tokens
    cbsSender.Close();
    cbsReceiver.Close();
    session.Close();

    return result;
}
```

Olá `PutCbsToken()` método recebe Olá *conexão* (instância de classe de conexão AMQP conforme fornecido por Olá [AMQP .NET Lite biblioteca](https://github.com/Azure/amqpnetlite)) que representa o serviço de toohello de conexão de TCP hello e hello *sasToken* parâmetro hello SAS token toosend. 

> [!NOTE]
> É importante que a conexão de saudação é criado com **mecanismo de autenticação SASL definido tooEXTERNAL** (e não Olá padrão simples com o nome de usuário e a senha usada ao token SAS Olá toosend não é necessário).
> 
> 

Em seguida, o publicador de saudação cria dois links AMQP para enviar o token SAS hello e receber a resposta de saudação (resultados de validação de token Olá) do serviço de saudação.

AMQP mensagem contém um conjunto de propriedades e mais informações do que uma mensagem simples. token SAS Olá é o corpo de saudação de mensagem de saudação (usando o construtor). Olá **"ReplyTo"** está definida toohello nome do nó para receber o resultado da validação Olá no link de receptor de saudação (você pode alterar seu nome, se desejar, e ele será criado dinamicamente pelo serviço de saudação). Olá três últimas propriedades de aplicativo/personalizadas são usadas pelo Olá serviço tooindicate que tipo de operação, ele tem tooexecute. Conforme descrito pelo Olá CBS especificação de rascunho, eles devem ser Olá **nome da operação** ("put-token"), Olá **tipo de token** (no caso, um "servicebus.windows.net:sastoken") e hello **" nome"do público-alvo Olá** token de saudação toowhich aplica-se (entidade inteira de saudação).

Após enviar token SAS Olá no link de remetente Olá, publisher Olá deve ler resposta Olá no link do receptor de saudação. saudação de resposta é uma mensagem do AMQP simples com uma propriedade de aplicativo denominada **"código de status"** que pode conter Olá mesmos valores como um código de status HTTP.

## <a name="rights-required-for-service-bus-operations"></a>Direitos necessários para operações do Barramento de Serviço

Olá tabela a seguir mostra os direitos de acesso Olá necessários para diversas operações nos recursos do barramento de serviço.

| Operação | Declaração Obrigatória | Escopo da Declaração |
| --- | --- | --- |
| **Namespace** | | |
| Configurar regra de autorização em um namespace |Gerenciar |Qualquer endereço de namespace |
| **Registro do Serviço** | | |
| Enumerar Políticas de Privacidade |Gerenciar |Qualquer endereço de namespace |
| Iniciar a escuta em um namespace |Escutar |Qualquer endereço de namespace |
| Enviar o ouvinte de tooa mensagens em um namespace |Enviar |Qualquer endereço de namespace |
| **Fila** | | |
| Criar uma fila |Gerenciar |Qualquer endereço de namespace |
| Excluir uma fila |Gerenciar |Qualquer endereço de fila válido |
| Enumerar filas |Gerenciar |/$Resources/Queues |
| Obter a descrição da fila Olá |Gerenciar |Qualquer endereço de fila válido |
| Configurar regra de autorização para uma fila |Gerenciar |Qualquer endereço de fila válido |
| Enviar para fila toohello |Enviar |Qualquer endereço de fila válido |
| Receber mensagens de uma fila |Escutar |Qualquer endereço de fila válido |
| Abandonar ou preencher as mensagens após o recebimento da mensagem de saudação no modo de bloqueio de inspeção |Escutar |Qualquer endereço de fila válido |
| Adiar uma mensagem para recuperação posterior |Escutar |Qualquer endereço de fila válido |
| Colocar uma mensagem nas mensagens mortas |Escutar |Qualquer endereço de fila válido |
| Obter o estado de saudação associado a uma sessão de fila de mensagem |Escutar |Qualquer endereço de fila válido |
| Definir estado de saudação associado a uma sessão de fila de mensagem |Escutar |Qualquer endereço de fila válido |
| **Tópico** | | |
| Criar um tópico |Gerenciar |Qualquer endereço de namespace |
| Excluir um tópico |Gerenciar |Qualquer endereço de tópico válido |
| Enumerar tópicos |Gerenciar |/$Resources/Topics |
| Obter descrição do tópico Olá |Gerenciar |Qualquer endereço de tópico válido |
| Configurar regra de autorização para um tópico |Gerenciar |Qualquer endereço de tópico válido |
| Enviar toohello tópico |Enviar |Qualquer endereço de tópico válido |
| **Assinatura** | | |
| Criar uma assinatura |Gerenciar |Qualquer endereço de namespace |
| Excluir assinatura |Gerenciar |../myTopic/Subscriptions/mySubscription |
| Enumerar assinaturas |Gerenciar |../myTopic/Subscriptions |
| Obter descrição da assinatura |Gerenciar |../myTopic/Subscriptions/mySubscription |
| Abandonar ou preencher as mensagens após o recebimento da mensagem de saudação no modo de bloqueio de inspeção |Escutar |../myTopic/Subscriptions/mySubscription |
| Adiar uma mensagem para recuperação posterior |Escutar |../myTopic/Subscriptions/mySubscription |
| Colocar uma mensagem nas mensagens mortas |Escutar |../myTopic/Subscriptions/mySubscription |
| Obter o estado de saudação associado a uma sessão do tópico |Escutar |../myTopic/Subscriptions/mySubscription |
| Definir estado de saudação associado a uma sessão do tópico |Escutar |../myTopic/Subscriptions/mySubscription |
| **Regras** | | |
| Criar uma regra |Gerenciar |../myTopic/Subscriptions/mySubscription |
| Excluir uma regra |Gerenciar |../myTopic/Subscriptions/mySubscription |
| Enumerar regras |Gerenciar ou Escutar |../myTopic/Subscriptions/mySubscription/Rules 

## <a name="next-steps"></a>Próximas etapas

toolearn mais sobre o sistema de mensagens do barramento de serviço, consulte Olá tópicos a seguir.

* [Conceitos fundamentais do barramento de serviço](service-bus-fundamentals-hybrid-solutions.md)
* [Filas, tópicos e assinaturas do Barramento de Serviço](service-bus-queues-topics-subscriptions.md)
* [Como as filas do barramento de serviço toouse](service-bus-dotnet-get-started-with-queues.md)
* [Como toouse Service Bus tópicos e assinaturas](service-bus-dotnet-how-to-use-topics-subscriptions.md)

[Azure portal]: https://portal.azure.com