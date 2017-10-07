---
title: "Hubs de Notificação do Azure: perguntas frequentes | Microsoft Docs"
description: "Perguntas frequentes sobre como projetar/implementar soluções em Hubs de Notificação"
services: notification-hubs
documentationcenter: mobile
author: ysxu
manager: erikre
keywords: "notificação por push, notificações por push, notificações por push do iOS, notificações por push do android, push do ios, push do android"
editor: 
ms.assetid: 7b385713-ef3b-4f01-8b1f-ffe3690bbd40
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 01/19/2017
ms.author: yuaxu
ms.openlocfilehash: a70efa7fc5954966847d5a173e9b10accf4b737e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="push-notifications-with-azure-notification-hubs-frequently-asked-questions"></a>Notificações por push com os Hubs de Notificação do Azure: perguntas frequentes
## <a name="general"></a>Geral
### <a name="what-is-hello-resource-structure-of-notification-hubs"></a>O que é a estrutura de saudação de recursos de Hubs de notificação?

Os Hubs de Notificação do Azure têm dois níveis de recursos: hubs e namespaces. Um hub é um recurso de envio por push único que pode conter informações de envio de plataforma cruzada de saudação de um aplicativo. Um namespace é uma coleção de hubs em uma região.

Mapeamento recomendado corresponde a um namespace com um único aplicativo. Dentro do namespace, você pode ter um hub de produção que funciona com o seu aplicativo de produção, um hub de teste que funciona com o seu aplicativo de teste e assim por diante.

### <a name="what-is-hello-price-model-for-notification-hubs"></a>O que é o modelo de preço de saudação para Hubs de notificação?
Olá detalhes de preços mais recentes podem ser encontrados no hello [preços de Hubs de notificação] página. Hubs de notificação é cobrado no nível de namespace hello. (Para a definição de saudação de um namespace, consulte "Qual é a estrutura de saudação de recursos de Hubs de notificação?") Hubs de notificação oferece três camadas:

* **Livre**: esta camada é um bom ponto de partida para explorar os recursos de envio. Não é recomendável para aplicativos de produção. Obter 500 dispositivos e 1 milhão envia incluído por namespace por mês, com nenhuma garantia (SLA) contrato de nível de serviço.
* **Básico**: essa camada (ou saudação padrão) é recomendado para aplicativos de produção menores. Obter 200.000 dispositivos e 10 milhões envia incluído por namespace por mês como uma linha de base. Opções de aumento de cota são incluídas.
* **Padrão**: essa camada é recomendada para aplicativos de produção toolarge médios. Obter 10 milhões de dispositivos e 10 milhões envia incluído por namespace por mês como uma linha de base. Recursos de telemetria cota aumento opções e recursos estão incluídos.

Recursos de camada padrão:
* **Telemetria sofisticada**: você pode usar Hubs de notificação por telemetria mensagem tootrack qualquer push solicitações e comentários de sistema de notificação de plataforma para depuração.
* **Multilocação**: você pode trabalhar com as credenciais do Sistema de Notificação de Plataforma em nível de namespace. Essa opção permite que você tooeasily dividir locatários em hubs dentro Olá mesmo namespace.
* **Agendado push**: você pode agendar toobe notificações enviada a qualquer momento.

### <a name="what-is-hello-notification-hubs-sla"></a>O que é Olá SLA de Hubs de notificação?
Para as camadas Basic e Standard de Hubs de notificação, aplicativos configurados corretamente podem enviar notificações por push ou executar operações de gerenciamento de registro de pelo menos 99,9% de tempo de saudação. toolearn mais sobre o SLA hello, vá toohello [SLA de Hubs de notificação](https://azure.microsoft.com/support/legal/sla/notification-hubs/) página.

> [!NOTE]
> Como notificações por push dependem do sistemas de notificação de plataforma de terceiros (por exemplo, Apple APNS e Google FCM), não há nenhuma garantia do SLA para entrega Olá dessas mensagens. Depois de Hubs de notificação envia lotes Olá tooPlatform sistemas de notificação (garantida de SLA), é responsabilidade de saudação do Olá Olá de toodeliver de sistemas de notificação de plataforma envia (nenhuma garantida de SLA).

### <a name="which-customers-are-using-notification-hubs"></a>Quais clientes estão usando os Hubs de Notificação?
Muitos clientes utilizam os Hubs de Notificação. Alguns dos notáveis são listados aqui:

* Sochi 2014: Centenas de 150 milhões notificações enviadas em duas semanas, 3 milhões de dispositivos e grupos de interesse. [Estudo de caso: Sochi]
* Skanska: [Estudo de caso: Skanska]
* Seattle Times: [Estudo de caso: Seattle Times]
* Mural.ly: [Estudo de caso: Mural.ly]
* 7Digital: [Estudo de caso: 7Digital]
* Aplicativos Bing: Dezenas de milhões de dispositivos de enviar notificações de 3 milhões por dia.

### <a name="how-do-i-upgrade-or-downgrade-my-hub-or-namespace-tooa-different-tier"></a>Como atualizar ou fazer downgrade meu namespace ou hub tooa outra camada?
Vá toohello  **[portal do Azure]** > **Namespaces de Hubs de notificação** ou **Hubs de notificação**. Selecione Olá recurso desejado tooupdate e ir muito**preço**. Observe Olá requisitos a seguir:

* Olá preço atualizado aplica-se também*todos os* hubs no namespace Olá estiver trabalhando com.
* Se a contagem de dispositivo excede o limite de saudação da camada de hello para que estiver fazendo downgrade, será necessário toodelete dispositivos antes de você fazer o downgrade.


## <a name="design-and-development"></a>Design e desenvolvimento
### <a name="which-server-side-platforms-do-you-support"></a>A quais plataformas do lado do servidor você oferece suporte?
Os SDKs do servidor estão disponíveis para .NET, Java, Node. js, PHP e Python. As APIs de Hubs de Notificação baseiam-se em interfaces REST, portanto, você pode trabalhar diretamente com as APIs REST se você estiver usando diferentes plataformas ou não desejar dependência extra. Para obter mais informações, consulte toohello [APIs de REST de Hubs de notificação] página.

### <a name="which-client-platforms-do-you-support"></a>A quais plataformas de cliente você oferece suporte?
As notificações por push têm suporte para plataformas [iOS](notification-hubs-ios-apple-push-notification-apns-get-started.md), [Android](notification-hubs-android-push-notification-google-gcm-get-started.md), [Universal do Windows](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md), [Windows Phone](notification-hubs-windows-mobile-push-notifications-mpns.md), [Kindle](notification-hubs-kindle-amazon-adm-push-notification.md), [Android China (via Baidu)](notification-hubs-baidu-china-android-notifications-get-started.md), Xamarin ([iOS](xamarin-notification-hubs-ios-push-notification-apns-get-started.md) e [Android](xamarin-notification-hubs-push-notifications-android-gcm.md)), [Chrome Apps](notification-hubs-chrome-push-notifications-get-started.md) e [Safari](https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSafari). Para obter mais informações, consulte toohello [tutoriais do guia de Introdução do notificação Hubs] página.

### <a name="do-you-support-text-message-email-or-web-notifications"></a>Há suporte para notificações de Web, email ou mensagem de texto?
Hubs de notificação é principalmente projetado toosend notificações toomobile aplicativos. Ele não fornece email ou texto recursos de mensagem. No entanto, as plataformas de terceiros que fornecem esses recursos podem ser integradas com notificações de push nativo toosend Hubs de notificação usando [aplicativos móveis].

Hubs de notificação também fornece um serviço de entrega de notificação de envio no navegador sem necessidade de saudação. Os clientes podem implementar esse recurso usando o SignalR sobre plataformas do hello com suporte do lado do servidor. Se você quiser toosend notificações toobrowser aplicativos na área restrita do Chrome hello, consulte Olá [tutorial Chrome aplicativos].

### <a name="how-are-mobile-apps-and-azure-notification-hubs-related-and-when-do-i-use-them"></a>Como os Aplicativos Móveis e os Hubs de Notificação do Azure estão relacionados e quando usá-los?
Se você tiver uma móveis novamente o aplicativo terminar e você deseja tooadd somente Olá recurso toosend as notificações por push, você pode usar Hubs de notificação do Azure. Se desejar tooset seu back-end de aplicativo móvel do zero, considere o uso de recurso de aplicativos móveis de saudação do serviço de aplicativo do Azure. Um aplicativo móvel automaticamente provisiona um hub de notificação para que você pode facilmente enviar notificações por push do back-end de aplicativo móvel hello. Preços para aplicativos móveis incluem encargos de saudação base para um hub de notificação. Você paga somente quando você exceder Olá incluído envia. Para obter mais detalhes sobre os custos, vá toohello [preços do serviço de aplicativo] página.

### <a name="how-many-devices-can-i-support-if-i-send-push-notifications-via-notification-hubs"></a>Para quantos dispositivos posso dar suporte se eu enviar notificações por push por meio dos Hubs de Notificação?
Consulte toohello [preços de Hubs de notificação] página para obter detalhes sobre o número de saudação de dispositivos com suporte.

Se você precisar de suporte para mais de 10 milhões de dispositivos registrados, [entre em contato conosco](https://azure.microsoft.com/overview/contact-us/) diretamente e ajudaremos você a dimensionar sua solução.

### <a name="how-many-push-notifications-can-i-send-out"></a>Quantas notificações por push posso enviar?
Dependendo do tipo selecionado do hello, Hubs de notificação do Azure automaticamente sobe com base no número de saudação de notificações que passam por sistema hello.

> [!NOTE]
> Olá custo geral de uso pode aumentar com base no número de saudação de notificações por push seja servido. Certifique-se de que você está ciente dos limites de camada Olá descritos no hello [preços de Hubs de notificação] página.
> 
> 

Os clientes usam Hubs de notificação toosend milhões de notificações por push diariamente. Você não tem toodo nada especial tooscale Olá alcançar das suas notificações por push enquanto você estiver usando os Hubs de notificação do Azure.

### <a name="how-long-does-it-take-for-sent-push-notifications-tooreach-my-device"></a>Quanto tempo take para enviados tooreach de notificações por push meu dispositivo?
Em um cenário de uso normal, onde a carga de entrada hello está consistente e até mesmo, os Hubs de notificação do Azure pode processar pelo menos *notificação por push de 1 milhão envia um minuto*. Essa taxa pode variar dependendo de número de saudação de marcas, natureza Olá Olá envios de entrada e outros fatores externos.

Durante o tempo de entrega Olá estimado, o serviço de saudação calcula destinos Olá por plataforma e roteia mensagens toohello serviço de notificação por Push (PNS) com base em marcas Olá registrado ou expressões de marca. É responsabilidade de saudação do dispositivo de toohello Olá PNS toosend notificações.

Olá PNS não garante que qualquer SLA de entrega de notificações. No entanto, a maioria das notificações de push são entregues tootarget dispositivos dentro de alguns minutos (normalmente em 10 minutos) de tempo de saudação que forem enviados tooNotification Hubs. Algumas notificações podem levar mais tempo.

> [!NOTE]
> Hubs de notificação do Azure tem uma política em vigor toodrop notificações por push que não são entregues toohello PNS dentro de 30 minutos. Esse atraso pode ocorrer por vários motivos, mas a maioria das normalmente porque Olá PNS está otimizando seu aplicativo.
> 
> 

### <a name="is-there-any-latency-guarantee"></a>Há qualquer garantia de latência?
Devido à natureza da saudação de notificações por push (são entregues por um PNS externa, específica de plataforma), não há nenhuma garantia de latência. Normalmente, a maioria de saudação de notificações por push são entregues dentro de alguns minutos.

### <a name="what-do-i-need-tooconsider-when-designing-a-solution-with-namespaces-and-notification-hubs"></a>O que eu preciso tooconsider durante a criação de uma solução com hubs de notificação e namespaces?
#### <a name="mobile-appenvironment"></a>Ambiente/aplicativo móvel
* Use um hub de notificação por aplicativo móvel, por ambiente.
* Em um cenário multilocatário, cada locatário deve ter um hub separado.
* Nunca compartilhamento Olá mesmo hub de notificação para ambientes de produção e teste. Essa prática pode causar problemas ao enviar notificações. (A Apple oferece pontos de extremidade de área restrita e push de produção, cada qual com credenciais separadas).
* Por padrão, você pode enviar teste notificações tooyour registrado dispositivos por meio do portal do Azure de saudação ou hello Azure componente integrado no Visual Studio. limite de saudação é definida too10 dispositivos que são selecionados aleatoriamente do pool de registro de saudação.

> [!NOTE]
> Se seu hub foi originalmente configurado com um certificado de área restrita Apple e, em seguida, foi reconfigurado toouse um certificado de produção da Apple, tokens de dispositivo original Olá são inválidos. Tokens inválidos causam toofail envios por push. Separe a produção e ambientes de teste e usar os hubs diferentes para ambientes diferentes.
> 
> 

#### <a name="pns-credentials"></a>Credenciais PNS
Quando um aplicativo móvel é registrado com o portal do desenvolvedor da plataforma (por exemplo, Apple ou Google), um aplicativo identificador e tokens de segurança são enviadas. back-end de aplicativo Hello fornece esses PNS tokens toohello plataforma para que as notificações por push podem ser enviadas toodevices. Tokens de segurança podem ser na forma de saudação de certificados (por exemplo, Apple iOS ou Windows Phone) ou chaves de segurança (por exemplo, Google Android ou Windows). Eles devem ser configurados em hubs de notificação. A configuração normalmente é feita no nível do hub de notificação hello, mas também pode ser feito no nível de namespace Olá em um cenário de vários locatários.

#### <a name="namespaces"></a>Namespaces
Os namespaces podem ser usados para o agrupamento de implantação. Eles também podem ser usado toorepresent todos os hubs de notificação para todos os locatários do hello mesmo aplicativo em um cenário de vários locatários.

#### <a name="geo-distribution"></a>Distribuição geográfica
A distribuição geográfica nem sempre é crítica em cenários de notificações por push. Vários PNSes (por exemplo, APNS ou GCM) que fornecem toodevices de notificações por push não são distribuídos uniformemente.

Se você tiver um aplicativo que é usado globalmente, você pode criar hubs em namespaces diferentes, usando o serviço de Hubs de notificação de saudação em diferentes regiões do Azure ao redor Olá, mundo.

> [!NOTE]
> Não recomendamos essa organização porque aumenta o custo de gerenciamento, especialmente para os registros. Deve ser feito somente se houver uma necessidade de explícita.
> 
> 

### <a name="should-i-do-registrations-from-hello-app-back-end-or-directly-through-client-devices"></a>Devo fazer registros de back-end de aplicativo hello, ou diretamente por meio do cliente dispositivos?
Registros de back-end de aplicativo hello são úteis quando você tem clientes tooauthenticate antes de criar o registro de saudação. Eles também são úteis quando você tem marcas que devem ser criadas ou modificadas por Olá aplicativo back-end com base na lógica do aplicativo. Para obter mais informações, consulte toohello [diretrizes de registro de back-end] e [diretrizes de registro de back-end 2] páginas.

### <a name="what-is-hello-push-notification-delivery-security-model"></a>O que é o modelo de segurança de entrega de notificação do hello por push?
Os Hubs de Notificação do Azure usam um modelo de segurança baseado em [assinatura de acesso compartilhado](../storage/common/storage-dotnet-shared-access-signature-part-1.md). Você pode usar tokens de assinatura de acesso compartilhado de saudação no nível de namespace de raiz de saudação ou no nível de hub de notificação granular hello. Tokens de assinatura de acesso compartilhado podem ser conjunto toofollow diferentes regras de autorização, por exemplo, permissões de mensagem toosend ou toolisten para permissões de notificação. Para obter mais informações, consulte Olá [modelo de segurança de Hubs de notificação] documento.

### <a name="how-should-i-handle-sensitive-payload-in-push-notifications"></a>Como lidar com a carga confidencial nas notificações por push?
Todas as notificações são entregues tootarget dispositivos por meio PNS da plataforma Olá. Quando uma notificação é enviada tooAzure Hubs de notificação, ele é processado e passado toohello PNS do respectivos.

Todas as conexões de saudação remetente toohello Hubs de notificação do Azure toohello PNS, usam HTTPS.

> [!NOTE]
> Hubs de notificação do Azure não registra carga Olá de mensagens de qualquer forma.
> 
> 

cargas de confidenciais toosend, recomendamos usar um padrão Push seguro. remetente Olá oferece uma notificação de ping com um dispositivo de toohello do identificador de mensagem sem carga confidenciais hello. Quando o aplicativo hello no dispositivo de saudação recebe carga Olá, o aplicativo hello chama uma API segura diretamente toofetch Olá detalhes da mensagem. Para obter um guia sobre como tooimplement esse padrão, vá toohello [tutorial notificação Hubs seguro Push] página.

## <a name="operations"></a>Operações
### <a name="what-support-is-provided-for-disaster-recovery"></a>Qual suporte é fornecido para a recuperação de desastre?
Podemos fornecer metadados cobertura de recuperação de desastres do nosso (nome de Hubs de notificação de hello, cadeia de caracteres de conexão hello e outras informações críticas). Quando um cenário de recuperação de desastres é disparado, dados de registro são hello *segmento apenas* da infraestrutura de Hubs de notificação de saudação é perdida. Você precisará tooimplement toorepopulate uma solução esses dados em seu novo hub após a recuperação:

1. Crie um hub de notificações secundário em um datacenter diferente. É recomendável criar um da saudação tooshield de início de um evento de recuperação de desastres que pode afetar os recursos de gerenciamento. Você também pode criar uma vez de saudação do evento de recuperação de desastres hello.

2. Preencha o hub de notificação secundário Olá com registros de saudação do hub de notificação primário. Não recomendamos tentar toomaintain registros em ambos os hubs e mantê-las em sincronia, à medida que os registros. Essa prática não funciona bem devido a tendência de saudação inerentes de registros tooexpire em Olá lado PNS. Os Hubs de Notificação limpa-os enquanto recebe comentários dos PNS sobre registros expirados ou inválidos.  

Temos dois recomendações para back-ends de aplicativo:

* Use um back-end de aplicativo que mantém um determinado conjunto de registros no final. Em seguida, pode executar uma inserção em massa no hub de notificação secundário hello.

* Use um back-end de aplicativo que obtém um despejo regular de registros de hub de notificação principal hello como um backup. Em seguida, pode executar uma inserção em massa no hub de notificação secundário hello.

> [!NOTE]
> Funcionalidade de importação/exportação de registros disponível na camada padrão Olá Olá descrita [registros de importação/exportação] documento.
> 
> 

Se você não tiver um back-end, quando o aplicativo hello inicia em dispositivos de destino, eles executar um novo registro no hub de notificação secundário hello. Eventualmente hello hub de notificação secundário terá todos os dispositivos ativos Olá registrados.

Haverá um período de tempo quando os dispositivos com aplicativos não abertos não recebem notificações.

### <a name="is-there-audit-log-capability"></a>Há recursos de log de auditoria?
Todas as operações de gerenciamento de Hubs de notificação vá toooperation logs, que são expostos no hello [portal clássico do Azure].

## <a name="monitoring-and-troubleshooting"></a>Monitoramento e solução de problemas
### <a name="what-troubleshooting-capabilities-are-available"></a>Quais recursos de solução de problemas estão disponíveis?
Hubs de notificação do Azure fornece vários recursos para solução de problemas, particularmente para o cenário mais comum de saudação de notificações descartadas. Para obter detalhes, consulte Olá [solução de problemas de Hubs de notificação] white paper.

### <a name="what-telemetry-features-are-available"></a>Quais recursos de telemetria estão disponíveis?
Do Azure Hubs de notificação permite que a exibição de dados de telemetria em Olá [portal clássico do Azure]. Detalhes das métricas de saudação estão disponíveis no hello [métricas de Hubs de notificação] página.

> [!NOTE]
> Notificações de sucesso simplesmente significam que as notificações por push tem sido entregue toohello PNS externo (por exemplo, APNS para Apple) ou GCM para o Google. É responsabilidade de saudação de dispositivos de tootarget Olá PNS toodeliver Olá notificações. Normalmente, Olá PNS não expõe partes de toothird de métricas de entrega.  
> 
> 

Nós também fornecemos dados de telemetria de Olá Olá recurso tooexport programaticamente (no nível padrão de saudação). Para obter detalhes, consulte Olá [exemplo as métricas de Hubs de notificação].

[portal clássico do Azure]: https://manage.windowsazure.com
[preços de Hubs de notificação]: http://azure.microsoft.com/pricing/details/notification-hubs/
[Notification Hubs SLA]: http://azure.microsoft.com/support/legal/sla/
[Estudo de caso: Sochi]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=7942
[Estudo de caso: Skanska]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5847
[Estudo de caso: Seattle Times]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=8354
[Estudo de caso: Mural.ly]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=11592
[Estudo de caso: 7Digital]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=3684
[APIs de REST de Hubs de notificação]: https://msdn.microsoft.com/library/azure/dn530746.aspx
[tutoriais do guia de Introdução do notificação Hubs]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
[tutorial Chrome aplicativos]: http://azure.microsoft.com/documentation/articles/notification-hubs-chrome-get-started/
[Mobile Services Pricing]: http://azure.microsoft.com/pricing/details/mobile-services/
[diretrizes de registro de back-end]: https://msdn.microsoft.com/library/azure/dn743807.aspx
[diretrizes de registro de back-end 2]: https://msdn.microsoft.com/library/azure/dn530747.aspx
[modelo de segurança de Hubs de notificação]: https://msdn.microsoft.com/library/azure/dn495373.aspx
[tutorial notificação Hubs seguro Push]: http://azure.microsoft.com/documentation/articles/notification-hubs-aspnet-backend-ios-secure-push/
[solução de problemas de Hubs de notificação]: http://azure.microsoft.com/documentation/articles/notification-hubs-diagnosing/
[métricas de Hubs de notificação]: https://msdn.microsoft.com/library/dn458822.aspx
[exemplo as métricas de Hubs de notificação]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/FetchNHTelemetryInExcel
[registros de importação/exportação]: https://msdn.microsoft.com/library/dn790624.aspx
[portal do Azure]: https://portal.azure.com
[complete samples]: https://github.com/Azure/azure-notificationhubs-samples
[aplicativos móveis]: https://azure.microsoft.com/services/app-service/mobile/
[preços do serviço de aplicativo]: https://azure.microsoft.com/pricing/details/app-service/
