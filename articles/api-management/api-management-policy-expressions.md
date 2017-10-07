---
title: "expressões de política de gerenciamento de API aaaAzure | Microsoft Docs"
description: "Saiba mais sobre expressões de política no Gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: ea160028-fc04-4782-aa26-4b8329df3448
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 79da0d6ca3963307ec811a33aaac3d63a7abd97d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-policy-expressions"></a>Expressões de política de Gerenciamento de API
A sintaxe de expressões de política é C# 6.0. Cada expressão tem acesso toohello fornecido implicitamente [contexto](api-management-policy-expressions.md#ContextVariables) variável e um permitido [subconjunto](api-management-policy-expressions.md#CLRTypes) tipos do .NET Framework.  
  
> [!NOTE]
>  Para obter mais informações sobre expressões de política, consulte Olá [expressões de política](https://azure.microsoft.com/documentation/videos/policy-expressions-in-azure-api-management/) vídeo.  
>   
>  Para demonstrações da configuração de políticas usando expressões de política, consulte [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Abordagem da Nuvem Episódio 177: Mais Recursos de Gerenciamento de API com Vlad Vinogradsky). Este vídeo contém Olá demonstrações de expressão de política a seguir.  
>   
>  -   10:30 - consulte como diretiva tooapply Olá API de nível de serviço toosupply contexto informações toohello back-end usando Olá [definir parâmetro de cadeia de caracteres de consulta](api-management-transformation-policies.md#SetQueryStringParameter) e [cabeçalho HTTP definir](api-management-transformation-policies.md#SetHTTPheader) políticas. Em 12:10, há uma demonstração de como chamar uma operação no portal do desenvolvedor Olá onde você pode ver essas políticas no trabalho.  
> -   13:50 - consulte como Olá toouse [validar JWT](api-management-access-restriction-policies.md#ValidateJWT) política toopre-autorizar toooperations de acesso baseado em declarações de token. Avanço too15:00 toosee políticas de saudação configuradas no editor de diretiva de saudação e, em seguida, too18:50 para ver uma demonstração de como chamar uma operação do portal do desenvolvedor do hello com e sem Olá necessário token de autorização.  
> -   21:00 - consulte como toouse uma [API Inspetor](https://azure.microsoft.com/documentation/articles/api-management-howto-api-inspector/) toosee como as políticas são avaliadas e Olá resultados de avaliações de saudação de rastreamento.  
> -   25:25 - consulte como expressões de política toouse com hello [obter do cache](api-management-caching-policies.md#GetFromCache) e [repositório toocache](api-management-caching-policies.md#StoreToCache) resposta de gerenciamento de API de tooconfigure políticas duração que corresponde ao Olá cache de resposta de saudação de cache serviço de back-end conforme especificado pelas Olá feito do serviço `Cache-Control` diretiva.  
> -   34:30 - consulte como conteúdo tooperform filtragem, removendo elementos de dados de resposta Olá recebido do serviço de back-end hello usando Olá [fluxo de controle](api-management-advanced-policies.md#choose) e [definir corpo](api-management-transformation-policies.md#SetBody) políticas. Iniciar em 31:50 toosee uma visão geral de [Olá escuro API de previsão Sky](https://developer.forecast.io/) usado para esta demonstração.  
> -   declarações de política de saudação toodownload usadas neste vídeo, consulte Olá [api de gerenciamento-exemplos/políticas](https://github.com/Azure/api-management-samples/tree/master/policies) repositório github.  
  
  
##  <a name="Syntax"></a> Sintaxe  
 Expressões de instrução única são colocadas em `@(expression)`, em que `expression` é uma instrução de expressão C# bem formada.  
  
 Expressões de várias instruções são colocadas em `@{expression}`. Todos os caminhos de código dentro de expressões de várias instruções devem terminar com uma instrução `return`.  
  
##  <a name="PolicyExpressionsExamples"></a> Exemplos  
  
```  
@(true)  
  
@((1+1).ToString())  
  
@("Hi There".Length)  
  
@(Regex.Match(context.Response.Headers.GetValueOrDefault("Cache-Control",""), @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value)  
  
@(context.Variables.ContainsKey("maxAge") ? int.Parse((string)context.Variables["maxAge"]) : 3600)  
  
@{   
  string value;   
  if (context.Request.Headers.TryGetValue("Authorization", out value))   
  {   
    return Encoding.UTF8.GetString(Convert.FromBase64String(value));  
  }   
  else   
  {   
    return null;  
  }  
}  
```  
  
##  <a name="PolicyExpressionsUsage"></a> Uso  
 Expressões podem ser usadas como valores de atributo ou texto em qualquer um dos Olá gerenciamento de API [políticas](api-management-policies.md), a menos que a referência de política de saudação especifique o contrário.  
  
> [!IMPORTANT]
>  Observe que quando você usar expressões de política, há apenas uma verificação limitada de expressões de política hello quando Olá política é definida. Como expressões de saudação são executadas em tempo de execução no pipeline de entrada ou saída Olá pelo gateway hello, as exceções de tempo de execução geradas por expressões de política Olá resultará em um erro em tempo de execução na chamada de API de saudação.  
  
##  <a name="CLRTypes"></a> Tipos do .NET framework permitidos em expressões de política  
 Olá tabela a seguir lista tipos do .NET Framework hello e seus membros que são permitidos em expressões de política.  
  
|Tipo CLR|Métodos com suporte|  
|--------------|-----------------------|  
|Newtonsoft.Json.Linq.Extensions|Há suporte para todos os métodos|  
|Newtonsoft.Json.Linq.JArray|Há suporte para todos os métodos|  
|Newtonsoft.Json.Linq.JConstructor|Há suporte para todos os métodos|  
|Newtonsoft.Json.Linq.JContainer|Há suporte para todos os métodos|  
|Newtonsoft.Json.Linq.JObject|Há suporte para todos os métodos|  
|Newtonsoft.Json.Linq.JProperty|Há suporte para todos os métodos|  
|Newtonsoft.Json.Linq.JRaw|Há suporte para todos os métodos|  
|Newtonsoft.Json.Linq.JToken|Há suporte para todos os métodos|  
|Newtonsoft.Json.Linq.JTokenType|Há suporte para todos os métodos|  
|Newtonsoft.Json.Linq.JValue|Há suporte para todos os métodos|  
|System.Collections.Generic.IReadOnlyCollection<T\>|Todos|  
|System.Collections.Generic.IReadOnlyDictionary<TKey,  TValue>|Todos|  
|System.Collections.Generic.ISet<TKey, TValue>|Todos|  
|System.Collections.Generic.KeyValuePair<TKey,  TValue>|Key, Value|  
|System.Collections.Generic.List<TKey, TValue>|Todos|  
|System.Collections.Generic.Queue<TKey, TValue>|Todos|  
|System.Collections.Generic.Stack<TKey, TValue>|Todos|  
|System.Convert|Todos|  
|System.DateTime|Todos|  
|System.DateTimeKind|Utc|  
|System.DateTimeOffset|Todos|  
|System.Decimal|Todos|  
|System.Double|Todos|  
|System.Guid|Todos|  
|System.IEnumerable<T\>|Todos|  
|System.IEnumerator<T\>|Todos|  
|System.Int16|Todos|  
|System.Int32|Todos|  
|System.Int64|Todos|  
|System.Linq.Enumerable<T\>|Há suporte para todos os métodos|  
|System.Math|Todos|  
|System.MidpointRounding|Todos|  
|System.Nullable<T\>|Todos|  
|System.Random|Todos|  
|System.SByte|Todos|  
|System.Security.Cryptography. HMACSHA384|Todos|  
|System.Security.Cryptography. HMACSHA512|Todos|  
|System.Security.Cryptography.HashAlgorithm|Todos|  
|System.Security.Cryptography.HMAC|Todos|  
|System.Security.Cryptography.HMACMD5|Todos|  
|System.Security.Cryptography.HMACSHA1|Todos|  
|System.Security.Cryptography.HMACSHA256|Todos|  
|System.Security.Cryptography.KeyedHashAlgorithm|Todos|  
|System.Security.Cryptography.MD5|Todos|  
|System.Security.Cryptography.RNGCryptoServiceProvider|Todos|  
|System.Security.Cryptography.SHA1|Todos|  
|System.Security.Cryptography.SHA1Managed|Todos|  
|System.Security.Cryptography.SHA256|Todos|  
|System.Security.Cryptography.SHA256Managed|Todos|  
|System.Security.Cryptography.SHA384|Todos|  
|System.Security.Cryptography.SHA384Managed|Todos|  
|System.Security.Cryptography.SHA512|Todos|  
|System.Security.Cryptography.SHA512Managed|Todos|  
|System.Single|Todos|  
|System.String|Todos|  
|System.StringSplitOptions|Todos|  
|System.Text.Encoding|Todos|  
|System.Text.RegularExpressions.Capture|Index, Length, Value|  
|System.Text.RegularExpressions.CaptureCollection|Count, Item|  
|System.Text.RegularExpressions.Group|Captures, Success|  
|System.Text.RegularExpressions.GroupCollection|Count, Item|  
|System.Text.RegularExpressions.Match|Empty, Groups, Result|  
|System.Text.RegularExpressions.Regex|.ctor, IsMatch, Match, Matches, Replace|  
|System.Text.RegularExpressions.RegexOptions|Compiled, IgnoreCase, IgnorePatternWhitespace, Multiline, None, RightToLeft, Singleline|  
|System.TimeSpan|Todos|  
|System.Tuple|Todos|  
|System.UInt16|Todos|  
|System.UInt32|Todos|  
|System.UInt64|Todos|  
|System.Uri|Todos|  
|System.Xml.Linq.Extensions|Há suporte para todos os métodos|  
|System.Xml.Linq.XAttribute|Há suporte para todos os métodos|  
|System.Xml.Linq.XCData|Há suporte para todos os métodos|  
|System.Xml.Linq.XComment|Há suporte para todos os métodos|  
|System.Xml.Linq.XContainer|Há suporte para todos os métodos|  
|System.Xml.Linq.XDeclaration|Há suporte para todos os métodos|  
|System.Xml.Linq.XDocument|Há suporte para todos os métodos|  
|System.Xml.Linq.XDocumentType|Há suporte para todos os métodos|  
|System.Xml.Linq.XElement|Há suporte para todos os métodos|  
|System.Xml.Linq.XName|Há suporte para todos os métodos|  
|System.Xml.Linq.XNamespace|Há suporte para todos os métodos|  
|System.Xml.Linq.XNode|Há suporte para todos os métodos|  
|System.Xml.Linq.XNodeDocumentOrderComparer|Há suporte para todos os métodos|  
|System.Xml.Linq.XNodeEqualityComparer|Há suporte para todos os métodos|  
|System.Xml.Linq.XObject|Há suporte para todos os métodos|  
|System.Xml.Linq.XProcessingInstruction|Há suporte para todos os métodos|  
|System.Xml.Linq.XText|Há suporte para todos os métodos|  
|System.Xml.XmlNodeType|Todos|  
  
##  <a name="ContextVariables"></a> Variável de contexto  
 Uma variável chamada `context` está implicitamente disponível em toda [expressão](api-management-policy-expressions.md#Syntax) de política. Seus membros fornecem toohello pertinentes informações `\request`. Todos os Olá `context` membros são somente leitura.  
  
|Variável de contexto|Valores de métodos, propriedades e parâmetros permitidos|  
|----------------------|-------------------------------------------------------|  
|context|Api: IApi<br /><br /> Implantação<br /><br /> LastError<br /><br /> Operação<br /><br /> Produto<br /><br /> Solicitação<br /><br /> RequestId: cadeia de caracteres<br /><br /> Resposta<br /><br /> Assinatura<br /><br /> Tracing: bool<br /><br /> Usuário<br /><br /> Variables:IReadOnlyDictionary<string, object><br /><br /> void Trace(message: string)|  
|context.Api|Id: string<br /><br /> Name: string<br /><br /> Path: string<br /><br /> ServiceUrl: IUrl|  
|context.Deployment|Region: string<br /><br /> ServiceName: string|  
|context.LastError|Source: string<br /><br /> Reason: string<br /><br /> Message: string<br /><br /> Scope: string<br /><br /> Section: string<br /><br /> Path: string<br /><br /> PolicyId: string<br /><br /> Para obter mais informações sobre context.LastError, consulte [Error handling](api-management-error-handling-policies.md) (Tratamento de erro).|  
|context.Operation|Id: string<br /><br /> Method: string<br /><br /> Name: string<br /><br /> UrlTemplate: string|  
|context.Product|Apis: IEnumerable<IApi\><br /><br /> ApprovalRequired: bool<br /><br /> Groups: IEnumerable<IGroup\><br /><br /> Id: string<br /><br /> Name: string<br /><br /> State: enum ProductState {NotPublished, Published}<br /><br /> SubscriptionLimit: int?<br /><br /> SubscriptionRequired: bool|  
|context.Request|Body: IMessageBody<br /><br /> Certificate: System.Security.Cryptography.X509Certificates.X509Certificate2<br /><br /> Headers: IReadOnlyDictionary<string, string[]><br /><br /> IpAddress: string<br /><br /> MatchedParameters: IReadOnlyDictionary<string, string><br /><br /> Method: string<br /><br /> OriginalUrl:IUrl<br /><br /> Url: IUrl|  
|string context.Request.Headers.GetValueOrDefault(headerName: string, defaultValue: string)|headerName: string<br /><br /> defaultValue: string<br /><br /> Valores de cabeçalho de solicitação separados por vírgulas de Retorna ou `defaultValue` se Olá cabeçalho não for encontrado.|  
|context.Response|Body: IMessageBody<br /><br /> Headers: IReadOnlyDictionary<string, string[]><br /><br /> StatusCode: int<br /><br /> StatusReason: string|  
|string context.Response.Headers.GetValueOrDefault(headerName: string, defaultValue: string)|headerName: string<br /><br /> defaultValue: string<br /><br /> Retorna valores de cabeçalho de resposta separados por vírgulas ou `defaultValue` se Olá cabeçalho não for encontrado.|  
|context.Subscription|CreatedTime: DateTime<br /><br /> EndDate: DateTime?<br /><br /> Id: string<br /><br /> Key: string<br /><br /> Name: string<br /><br /> PrimaryKey: string<br /><br /> SecondaryKey: string<br /><br /> StartDate: DateTime?|  
|context.User|Email: string<br /><br /> FirstName: string<br /><br /> Groups: IEnumerable<IGroup\><br /><br /> Id: string<br /><br /> Identities: IEnumerable<IUserIdentity\><br /><br /> LastName: string<br /><br /> Note: string<br /><br /> RegistrationDate: DateTime|  
|IApi|Id: string<br /><br /> Name: string<br /><br /> Path: string<br /><br /> Protocols: IEnumerable<string\><br /><br /> ServiceUrl: IUrl<br /><br /> SubscriptionKeyParameterNames: ISubscriptionKeyParameterNames|  
|IGroup|Id: string<br /><br /> Name: string|  
|IMessageBody|As<T\>(preserveContent: bool = false): em que T: string, JObject, JToken, JArray, XNode, XElement, XDocument<br /><br /> Olá `context.Request.Body.As<T>` e `context.Response.Body.As<T>` métodos são usado tooread agências em um tipo especificado de uma mensagem de solicitação e resposta `T`. Por padrão hello corpo de mensagem original do método usa Olá fluxo e reneders indisponível depois que ele retorna. tooavoid que operam em uma cópia do fluxo do corpo hello, Olá conjunto tendo método hello `preserveContent` parâmetro muito`true`. Vá [aqui](api-management-transformation-policies.md#SetBody) toosee um exemplo.|  
|IUrl|Host: string<br /><br /> Path: string<br /><br /> Port: int<br /><br /> Query: IReadOnlyDictionary<string, string[]><br /><br /> QueryString: string<br /><br /> Scheme: string|  
|IUserIdentity|Id: string<br /><br /> Provider: string|  
|ISubscriptionKeyParameterNames|Header: string<br /><br /> Query: string|  
|string IUrl.Query.GetValueOrDefault(queryParameterName: string, defaultValue: string)|queryParameterName: string<br /><br /> defaultValue: string<br /><br /> Valores de parâmetro de consulta separados por vírgulas de Retorna ou `defaultValue` se o parâmetro hello não foi encontrado.|  
|T context.Variables.GetValueOrDefault<T\>(variableName: string, defaultValue: T)|variableName: string<br /><br /> defaultValue: T<br /><br /> Retorna o valor da variável cast tootype `T` ou `defaultValue` se Olá variável não foi encontrada.<br /><br /> Este método lança uma exceção se hello tipo especificado não coincide com tipo real de saudação da saudação retornado variável.|  
|BasicAuthCredentials AsBasic(input: this string)|input: string<br /><br /> Se o parâmetro de entrada hello contém um valor válido de cabeçalho de solicitação de autorização autenticação básica HTTP, o método hello retorna um objeto do tipo `BasicAuthCredentials`; caso contrário, o método hello retorna nulo.|  
|bool TryParseBasic(input: this string, result: out BasicAuthCredentials)|input: string<br /><br /> result: out BasicAuthCredentials<br /><br /> Se o parâmetro de entrada hello contém um valor válido de cabeçalho de solicitação de autorização autenticação básica HTTP, o método hello retorna `true` e parâmetro de resultado Olá contém um valor do tipo `BasicAuthCredentials`; caso contrário, retorna o método hello `false`.|  
|BasicAuthCredentials|Password: string<br /><br /> UserId: string|  
|Jwt AsJwt(input: this string)|input: string<br /><br /> Se o parâmetro de entrada hello contém um valor válido de token JWT, o método hello retorna um objeto do tipo `Jwt`; caso contrário, retorna o método hello `null`.|  
|bool TryParseJwt(input: this string, result: out Jwt)|input: string<br /><br /> result: out Jwt<br /><br /> Se o parâmetro de entrada hello contém um valor válido de token JWT, o método hello retorna `true` e parâmetro de resultado Olá contém um valor do tipo `Jwt`; caso contrário, retorna o método hello `false`.|  
|Jwt|Algorithm: string<br /><br /> Audience: IEnumerable<string\><br /><br /> Claims: IReadOnlyDictionary<string, string[]><br /><br /> ExpirationTime: DateTime?<br /><br /> Id: string<br /><br /> Issuer: string<br /><br /> NotBefore: DateTime?<br /><br /> Subject: string<br /><br /> Type: string|  
|string Jwt.Claims.GetValueOrDefault(claimName: string, defaultValue: string)|claimName: string<br /><br /> defaultValue: string<br /><br /> Retorna valores de declaração separados por vírgula ou `defaultValue` se Olá cabeçalho não for encontrado.|

## <a name="next-steps"></a>Próximas etapas
Para saber mais sobre como trabalhar com políticas, veja [Políticas em Gerenciamento de API](api-management-howto-policies.md).  
