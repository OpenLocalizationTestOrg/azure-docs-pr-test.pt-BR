---
title: "aaaClient e o servidor de controle de versão SDK de aplicativos móveis e serviços móveis | Microsoft Docs"
description: "Lista dos SDKs clientes e compatibilidade com versões do SDK do servidor para os Serviços Móveis e Aplicativos Móveis do Azure"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 35b19672-c9d6-49b5-b405-a6dcd1107cd5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 5874b7455ea407ca8c77fb1bd03d97d0767ebb47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a>Controle de versão de cliente e servidor em Aplicativos Móveis e Serviços Móveis
a versão mais recente Olá de serviços móveis do Azure é hello **aplicativos móveis** recurso de serviço de aplicativo do Azure.

Olá cliente de aplicativos móveis e SDKs de servidor originalmente são baseadas nos serviços móveis, mas são *não* compatíveis entre si.
Ou seja, você deve usar um SDK de cliente de *Aplicativos Móveis* com SDK de servidor de *Aplicativos Móveis* e da mesma forma para *Serviços Móveis*. Este contrato é imposto por meio de um valor de cabeçalho especial usado pelo cliente hello e servidor SDKs, `ZUMO-API-VERSION`.

Observação: sempre que este documento se refere tooa *serviços móveis* back-end, ele não necessariamente precisa toobe hospedado em serviços móveis. Agora é possível toomigrate um toorun de serviço móvel no serviço de aplicativo sem alterações de código, mas o serviço de saudação ainda usa *serviços móveis* versões do SDK.

toolearn mais sobre migração tooApp serviço sem quaisquer alterações de código, consulte o artigo de saudação [migrar tooAzure um serviço móvel do serviço de aplicativo].

## <a name="header-specification"></a>Especificação de cabeçalho
chave de saudação `ZUMO-API-VERSION` pode ser especificado no cabeçalho HTTP de saudação ou cadeia de caracteres de consulta de saudação. valor de saudação é uma cadeia de caracteres de versão no formulário Olá **x.y.z**.

Por exemplo:

GET https://service.azurewebsites.net/tables/TodoItem

CABEÇALHOS: ZUMO-API-VERSION: 2.0.0

POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0

## <a name="opting-out-of-version-checking"></a>Recusando a verificação de versão
Você pode recusar a verificação, definindo um valor de versão **true** para configuração de aplicativo hello **MS_SkipVersionCheck**. Especifique isso na Web. config ou em Olá seção configurações do aplicativo de saudação portal do Azure.

> [!NOTE]
> Há um número de alterações de comportamento entre serviços móveis e aplicativos móveis, especialmente nas áreas de saudação da sincronização offline, autenticação e notificações por push. Você só deve recusar versão verificação após a conclusão tooensure teste que essas alterações de comportamento não prejudicam a funcionalidade do aplicativo.
>
>

## <a name="summary-of-compatibility-for-all-versions"></a>Resumo de compatibilidade para todas as versões
Olá gráfico a seguir mostra a compatibilidade de saudação entre todos os tipos de cliente e servidor. Um back-end é classificado como qualquer Mobile **serviços** ou Mobile **aplicativos** com base no servidor de saudação SDK que ele usa.

|  | **Serviços Móveis**  | **Aplicativos Móveis**  |
| --- | --- | --- |
| [Clientes de Serviços Móveis] |OK |Erro\* |
| [Clientes de Aplicativos Móveis] |Erro\* |OK |

\*Isso pode ser controlado especificando**MS_SkipVersionCheck**.

<!-- IMPORTANT!  hello anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: hello fwlink toothis document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <a name="1.0.0"></a>Servidor e cliente de Serviços Móveis
cliente Olá SDKs na tabela de saudação abaixo são compatíveis com **serviços móveis**.

Observação: Olá SDKs de cliente de serviços móveis *não* enviar um valor de cabeçalho `ZUMO-API-VERSION`. Se o serviço de saudação receber este cabeçalho ou o valor de cadeia de caracteres de consulta, um erro será retornado, a menos que explicitamente incluído como descrito acima.

### <a name="MobileServicesClients"></a> SDKs de clientes de *Serviços* Móveis
| Plataforma cliente | Versão | Valor de cabeçalho de versão |
| --- | --- | --- |
| Cliente gerenciado (Windows, Xamarin) |[1.3.2](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |n/d |
| iOS |[2.2.2](http://aka.ms/gc6fex) |n/d |
| Android |[2.0.3](https://go.microsoft.com/fwLink/?LinkID=280126) |n/d |
| HTML |[1.2.7](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |n/d |

### <a name="mobile-services-server-sdks"></a>SDKs de servidor de *Serviços* Móveis
| Plataforma servidor | Versão | Cabeçalho de versão aceito |
| --- | --- | --- |
| .NET |[WindowsAzure.MobileServices.Backend.* versão 1.0. x](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |* * Nenhum cabeçalho de versão * * |
| Node.js |(em breve) |**Nenhum cabeçalho de versão** |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a>Comportamento dos back-ends de Serviços Móveis
| ZUMO-API-VERSION | Valor de MS_SkipVersionCheck | Resposta |
| --- | --- | --- |
| Não especificado |Qualquer |200 - OK |
| Qualquer valor |Verdadeiro |200 - OK |
| Qualquer valor |Falso/não especificado |400 - solicitação inválida |

## <a name="2.0.0"></a>Servidor e cliente de Aplicativos Móveis do Azure
### <a name="MobileAppsClients"></a> SDKs de cliente de *Aplicativos* Móveis
A verificação de versão foi introduzida Olá seguintes versões do SDK do cliente Olá para **aplicativos móveis do Azure**:

| Plataforma cliente | Versão | Valor de cabeçalho de versão |
| --- | --- | --- |
| Cliente gerenciado (Windows, Xamarin) |[2.0.0](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |2.0.0 |
| iOS |[3.0.0](http://go.microsoft.com/fwlink/?LinkID=529823) |2.0.0 |
| Android |[3.0.0](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |3.0.0 |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a>SDKs de servidor dos *Aplicativos* Móveis
A verificação de versão está incluída nas seguintes versões do SDK do servidor:

| Plataforma servidor | . | Cabeçalho de versão aceito |
| --- | --- | --- |
| .NET |[Microsoft.Azure.Mobile.Server](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |2.0.0 |
| Node.js |[azure-mobile-apps)](https://www.npmjs.com/package/azure-mobile-apps) |2.0.0 |

### <a name="behavior-of-mobile-apps-backends"></a>Comportamento dos back-ends de Aplicativos Móveis
| ZUMO-API-VERSION | Valor de MS_SkipVersionCheck | Resposta |
| --- | --- | --- |
| x.y.z ou Null |Verdadeiro |200 - OK |
| Nulo |Falso/não especificado |400 - solicitação inválida |
| 1.x.y |Falso/não especificado |400 - solicitação inválida |
| 2.0.0-2.x.y |Falso/não especificado |200 - OK |
| 3.0.0-3.x.y |Falso/não especificado |400 - solicitação inválida |

## <a name="next-steps"></a>Próximas etapas
* [migrar tooAzure um serviço móvel do serviço de aplicativo]

[Clientes de Serviços Móveis]: #MobileServicesClients
[Clientes de Aplicativos Móveis]: #MobileAppsClients


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[migrar tooAzure um serviço móvel do serviço de aplicativo]: app-service-mobile-migrating-from-mobile-services.md
