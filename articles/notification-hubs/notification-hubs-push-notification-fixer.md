---
title: "aaaAzure Hubs de notificação - diretrizes de diagnóstico"
description: "Diretrizes sobre como toodiagnose comum problemas com Hubs de notificação do Azure."
services: notification-hubs
documentationcenter: Mobile
author: ysxu
manager: erikre
editor: 
ms.assetid: b5c89a2a-63b8-46d2-bbed-924f5a4cce61
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: NA
ms.devlang: multiple
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: e374278f2bfdfad36ba091e8846059cd184c17ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs---diagnosis-guidelines"></a>Hubs de Notificação do Azure - Diretrizes de Diagnóstico
## <a name="overview"></a>Visão geral
Uma das perguntas mais comuns de saudação ouvimos dos clientes de Hubs de notificação do Azure é como toofigure out por que eles não recebem uma notificação enviada do seu back-end do aplicativo são exibidos no dispositivo de cliente Olá - onde e por que as notificações foram removidas e como toofix isso. Neste artigo, examinaremos Olá várias razões por que as notificações podem obter descartadas ou não em dispositivos de saudação. Também vamos maneiras em que você pode analisar e descobrir a causa raiz de saudação. 

Em primeiro lugar, é toounderstand crítica, como Hubs de notificação do Azure envia dispositivos de toohello de notificações.
![][0]

Em um fluxo de notificação de envio típico, mensagem de saudação for enviada da saudação **back-end do aplicativo** muito**Hub de notificação do Azure (NH)** que por sua vez executa algum processamento em todos os registros de saudação levando em saudação de conta configurado marcas & toodetermine de expressões de marca "destinos" ou seja, todos os registros de saudação que precisam de notificação de push Olá tooreceive. Esses registros podem ser distribuídos em qualquer uma ou todas as nossas plataformas com suporte - iOS, Google, Windows, Windows Phone, Kindle e Baidu para Android na China. Após o estabelecimento de destinos hello, NH e envios por push as notificações, divididos em vários lotes de registros, toohello plataforma de dispositivo específico **serviço de notificação por Push (PNS)** -por exemplo, APNS para a Apple, GCM para Google etc. NH autentica com hello que PNS respectivos com base nas credenciais de saudação definido no hello Portal clássico do Azure na página do hello configurar Hub de notificação. Olá PNS encaminha Olá notificações toohello respectivo **dispositivos cliente**. Isso é recomendado as notificações por push do modo toodeliver e observe que o segmento final de saudação da entrega da notificação ocorre entre plataforma Olá PNS e dispositivo Olá de plataforma de saudação. Portanto, temos quatro componentes principais - *cliente*, *back-end do aplicativo*, *Hubs de Notificação do Azure (NH)* e *Serviços de Notificação por Push (PNS)* e qualquer um deles pode fazer com que as notificações sejam descartadas. Mais detalhes sobre essa arquitetura estão disponíveis em [Visão Geral dos Hubs de Notificação].

Falha toodeliver notificações podem ocorrer durante a saudação inicial fase que pode indicar um problema de configuração ou de teste/preparação pode acontecer em produção onde todos ou alguns dos Olá notificações pode ser sendo descartada indicando que alguns aplicativos mais profundo ou problema de padrão de mensagens. Na seção de saudação abaixo examinaremos vários cenários de notificações descartados desde toohello mais raras do tipo comum, que alguns dos quais você pode achar óbvia e outros não muito. 

## <a name="azure-notifications-hub-mis-configuration"></a>Configuração incorreta do Hub de Notificações do Azure
Hubs de notificação do Azure precisa tooauthenticate próprio contexto de saudação do toohello de notificações de envio do desenvolvedor Olá aplicativo toobe toosuccessfully capaz de PNS do respectivos. Isso é possibilitado pelo desenvolvedor Olá criando uma conta de desenvolvedor com hello respectivas plataformas (Google, Apple Windows etc.) e, em seguida, Registrando seu aplicativo em que ele pode obter credenciais que precisam toobe configurada no portal de saudação em notificação Seção de configuração de hubs. Se nenhuma notificação está fazendo a primeira etapa deve ser tooensure que as credenciais corretas de saudação são configuradas no hello Hub de notificação combiná-la com o aplicativo hello criado em sua conta de desenvolvedor específico de plataforma. Você encontrará nossa [obter tutoriais de Introdução] toogo úteis sobre esse processo de maneira passo a passo. Aqui estão algumas configurações incorretas comuns:

1. **Geral**
   
    um) Certifique-se de que o nome do hub de notificação (sem erros de digitação) é Olá mesmo:
   
   * Em que você está registrando saudação do cliente de, 
   * Em que você está enviando notificações de back-end Olá,  
   * Onde você configurou as credenciais PNS hello e 
   * Cujas credenciais SAS que você configurou no hello cliente e hello back-end. 
     
     b) Verifique se está usando a saudação corretas SAS configuração cadeias de caracteres no cliente de saudação e back-end de aplicativo hello. Como regra geral, você deve usar o hello **DefaultListenSharedAccessSignature** no cliente hello e **DefaultFullSharedAccessSignature** em Olá aplicativo back-end (que dá permissão toobe toosend capaz de notificação toohello NH)
2. **Configuração do Serviço de Notificação por Push da Apple (APNS)**
   
    Você deve manter dois hubs diferentes - um para produção e outro para fins de teste. Isso significa que carregar certificado Olá que for toouse hub separado de tooa de ambiente de área restrita e certificado de saudação que for toouse no hub separado de tooa de produção. Não tente tooupload diferentes tipos de certificados toohello mesmo hub como ela pode causar falhas de notificação linha hello para baixo. Se você perceber que está em uma posição em que você tenha carregado inadvertidamente diferentes tipos de certificado toohello mesmo hub, é recomendável iniciar nova e hub de saudação do toodelete. Se por algum motivo, você não toodelete capaz de hub de saudação no hello muito menos, você deve excluir todos os registros existentes de saudação do hub de saudação. 
3. **Configuração do Google Cloud Messaging (GCM)** 
   
    a) Certifique-se de que você está ativando o "Google Cloud Messaging para Android" em seu projeto de nuvem. 
   
    ![][2]
   
    b) Certifique-se de que você crie uma chave"servidor" ao obter credenciais de saudação quais NH usará tooauthenticate com GCM. 
   
    ![][3]
   
    c) Certifique-se de que você tenha configurado o "ID do projeto" no cliente de saudação que é uma entidade inteiramente numérica que você pode obter de painel hello:
   
    ![][1]

## <a name="application-issues"></a>Problemas de aplicativos
1) **Marcas/Expressões de marca**

Se você estiver usando marcas ou toosegment de expressões de marca seu público-alvo, sempre é possível que, quando você está enviando a notificação hello, não há nenhum destino foi encontrado com base em expressões de marcas/marca Olá que você está especificando no sua chamada de envio. É melhor tooreview tooensure seus registros que há marcas que correspondem ao enviar notificação e, em seguida, verifique se confirmação de notificação de saudação somente de clientes Olá com esses registros. Por exemplo Se todos os seus registros com NH foram feitos com dizem marca "Política" e você está enviando uma notificação com a marca "Esporte", ele não funcionará tooany dispositivo. Um caso complexo pode envolver a expressões de marca onde você tenha registrado apenas com a "Marca A" OU "Marca B", mas durante o envio de notificações, você tem como alvo a "Marca A & Marca B". Em Olá diagnosticar automaticamente seção dicas a seguir, há maneiras em que você pode examinar seus registros junto com marcas de saudação tiverem. 

2) **Problemas do modelo**

Se você estiver usando modelos, certifique-se de que você está seguindo as diretrizes de saudação descritas em [diretrizes de modelo]. 

3) **Registros inválidos**

Supondo que Olá que hub de notificação foi configurado corretamente e as expressões de marca/marcas foram usadas corretamente resultando em localizar Olá de destinos válidos notificações de saudação toowhich necessário toobe enviado, NH dispara vários lotes de processamento em paralelo - cada lote enviar mensagens tooa conjunto de registros. 

> [!NOTE]
> Já que estamos hello processamento em paralelo, nós não garante a ordem de saudação quais Olá notificações serão entregue. 
> 
> 

Agora o Hub de Notificações do Azure foi otimizado para um modelo de entrega de mensagem "no máximo uma vez". Isso significa que podemos tentar uma eliminação de duplicação para que nenhuma notificação é entregues mais de uma vez tooa dispositivo. tooensure isso vamos examinar os registros de saudação e certifique-se de que somente uma mensagem é enviado por um identificador de dispositivo antes de realmente enviar toohello de mensagem de saudação PNS. Como cada lote é enviada toohello PNS, que por sua vez, está aceitando e validar os registros de Olá, é possível que Olá PNS detecta um erro com um ou mais registros de saudação em um lote, retorna um erro tooAzure NH e interrompe o processamento descartando assim que lote completamente. Isso é especialmente verdadeiro com o APNS que usa um protocolo de fluxo TCP. Embora que são otimizados para no máximo uma vez entrega, neste caso, removemos Olá registro com falha do nosso banco de dados e, em seguida, entrega da notificação de repetição para rest Olá de dispositivos Olá nesse lote.

Você pode obter informações de erro para a tentativa de falha na entrega de saudação em relação a um registro usando Olá APIs de REST de Hubs de notificação do Azure: [por mensagem de telemetria: obter telemetria de mensagem de notificação](https://msdn.microsoft.com/library/azure/mt608135.aspx) e [PNS comentários](https://msdn.microsoft.com/library/azure/mt705560.aspx). Consulte Olá [SendRESTExample](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/SendRestExample) por exemplo de código.

## <a name="pns-issues"></a>Problemas PNS
Depois que a mensagem de saudação do notificação foi recebida pelo Olá respectivos PNS, em seguida, é sua responsabilidade toodeliver Olá toohello de dispositivo de notificação. Hubs de notificação do Azure está fora do imagem Olá aqui e não tem nenhum controle quando ou se a notificação Olá vai toobe entregue toohello dispositivo. Como os serviços de notificação de plataforma Olá são muito robustos, notificações tendem tooreach dispositivos de saudação em poucos segundos de saudação PNS. Se hello PNS porém é a limitação dos Hubs de notificação do Azure aplicar uma estratégia de retirada exponencial e se Olá PNS permanecer inacessível para 30 min, em seguida, temos uma política em colocar tooexpire e remover essas mensagens permanentemente. 

Se um PNS tentativas toodeliver uma notificação, mas Olá dispositivo estiver offline, notificação Olá é armazenada por Olá PNS para um período de tempo limitado e entregues toohello dispositivo quando ele estiver disponível. Apenas uma notificação recente de um aplicativo específico é armazenada. Se várias notificações são enviadas ao dispositivo Olá estiver offline, cada nova notificação faz com que notificação anterior de saudação toobe descartado. Esse comportamento de manter somente notificação mais recente da saudação é chamado tooas união de notificações no APNS e recolhendo em GCM (que usa uma chave recolha). Se o dispositivo Olá permanecer offline por um longo tempo, as notificações estão sendo armazenados para ela são descartadas. Origem - [Diretrizes do APNS] & [Diretrizes do APNS]

Com Hubs de notificação do Azure - você pode passar uma chave de união por meio de um cabeçalho HTTP usando Olá genérico `SendNotification` API (por exemplo, para o SDK do .NET – `SendNotificationAsync`) que também usa cabeçalhos HTTP que são passados como é toohello PNS do respectivos. 

## <a name="self-diagnose-tips"></a>Dicas de diagnóstico automático
Aqui vamos examinar Olá vários caminhos toodiagnose e raiz causam problemas de Hub de notificação:

### <a name="verify-credentials"></a>Verifique as credenciais
1. **Portal do desenvolvedor do PNS**
   
    Verifique-os no hello respectivos PNS developer portal (WNS, APNS, GCM, etc) usando nosso [obter tutoriais de Introdução].
2. **Portal clássico do Azure**
   
    Vá toohello configurar guia tooreview e corresponder às credenciais de saudação com aqueles obtidos no portal do desenvolvedor do PNS hello. 
   
    ![][4]

### <a name="verify-registrations"></a>Verificar registros
1. **Visual Studio**
   
    Se você usar o Visual Studio para desenvolvimento, em seguida, é possível conectar tooMicrosoft do Azure e exibir e gerenciar um grupo de serviços do Azure, incluindo o Hub de notificações "Do Gerenciador de servidores". Isso é útil principalmente para seu ambiente de desenvolvimento e teste. 
   
    ![][9]
   
    Você pode exibir e gerenciar todos os registros de saudação em seu hub que são categorizados bem para registro de modelo, plataforma ou nativo, qualquer marcas, identificador PNS, data de expiração de id e hello de registro. Você também pode editar um registro em funcionamento Olá - que é útil significa que se você quiser tooedit marcas. 
   
    ![][8]
   
   > [!NOTE]
   > Os registros do Visual Studio funcionalidade tooedit só devem ser usados durante o desenvolvimento/teste com um número limitado de registros. Se há surge uma necessidade toofix seus registros em massa, considere usando a funcionalidade de registro de importação/exportação Olá descrita aqui - [registros de importação/exportação](https://msdn.microsoft.com/library/dn790624.aspx)
   > 
   > 
2. **Gerenciador do Barramento de Serviço**
   
    Muitos clientes utilizam Gerenciador do Barramento de Serviço descrito aqui - [Gerenciador do Barramento de Serviço] para exibir e gerenciar seu hub de notificação. Ele é um projeto de software livre disponível em code.microsoft.com - [Código do Gerenciador do Barramento de Serviço]

### <a name="verify-message-notifications"></a>Verificar as notificações de mensagem
1. **Portal Clássico do Azure**
   
    Você pode ir toohello "Depuração" guia toosend teste notificações tooyour os clientes sem a necessidade de qualquer back-end do serviço para cima e em execução. 
   
    ![][7]
2. **Visual Studio**
   
    Você também pode enviar notificações de teste de comforts de saudação do Visual Studio:
   
    ![][10]
   
    Você pode ler mais sobre Olá do Azure do Visual Studio notificação Hub explorer funcionalidade aqui- 
   
   * [Visão Geral do Gerenciador do VS Server]
   * [Postagem do Blog do Gerenciador do VS Server- 1]
   * [Postagem do Blog do Gerenciador do VS Server- 2]

### <a name="debug-failed-notifications-review-notification-outcome"></a>Depurar notificações de falha/revisar resultado da notificação
**Propriedade EnableTestSend**

Quando você enviar uma notificação por meio de Hubs de notificação, inicialmente ele apenas obtém enfileirado para NH toodo toofigure-out de todos os seus destinos de processamento e eventualmente NH envia toohello PNS. Isso significa que quando você estiver usando a API REST ou qualquer cliente Olá SDK, hello retorno bem-sucedido de sua significa que somente chamada envio que Olá mensagem foi com êxito enfileirado com o Hub de notificação. Ele não fornece uma visão geral de como o que aconteceu quando NH eventualmente obteve toosend tooPNS de mensagem de saudação. Se a notificação não está sendo recebido no dispositivo de cliente hello, há uma possibilidade de que, quando NH tenta toodeliver tooPNS de mensagem de saudação, houve um erro, por exemplo, o tamanho de payload Olá excedeu o máximo de saudação permitido por Olá PNS ou credenciais de saudação configuradas no NH são tooget etc inválido. uma percepção erros PNS hello, apresentamos uma propriedade chamada [EnableTestSend recurso]. Essa propriedade é habilitada automaticamente quando você envia mensagens de saudação portal ou o cliente do Visual Studio de teste e, portanto, permite que você toosee detalhada informações de depuração. Você pode usá-lo por meio de APIs levando o exemplo hello de saudação .NET SDK onde ele está disponível no momento e será adicionado tooall SDKs de cliente eventualmente. toouse com chamada REST hello, basta acrescentar um parâmetro querystring chamado "test" no final de saudação de sua chamada de envio, por exemplo 

    https://mynamespace.servicebus.windows.net/mynotificationhub/messages?api-version=2013-10&test

*Exemplo (SDK do .NET)*

Suponha que você está usando o SDK do .NET toosend uma notificação do sistema nativo:

    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName);
    var result = await hub.SendWindowsNativeNotificationAsync(toast);
    Console.WriteLine(result.State);

`result.State`será simplesmente estado `Enqueued` final Olá execução Olá sem qualquer entender o que aconteceu tooyour push. Agora você pode usar o hello `EnableTestSend` propriedade booleana ao inicializar Olá `NotificationHubClient` e pode obter o status detalhado sobre Olá PNS erros ao enviar notificação de saudação. Olá envio chamada aqui levará mais tempo tooreturn porque ele está retornando somente após NH forneceu resultados de Olá Olá notificação tooPNS toodetermine. 

    bool enableTestSend = true;
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName, enableTestSend);

    var outcome = await hub.SendWindowsNativeNotificationAsync(toast);
    Console.WriteLine(outcome.State);

    foreach (RegistrationResult result in outcome.Results)
    {
        Console.WriteLine(result.ApplicationPlatform + "\n" + result.RegistrationId + "\n" + result.Outcome);
    }

*Saída de exemplo*

    DetailedStateAvailable
    windows
    7619785862101227384-7840974832647865618-3
    hello Token obtained from hello Token Provider is wrong

Esta mensagem indica credenciais inválidas são configuradas no hub de notificação de saudação ou um problema com registros Olá no hub hello e hello recomendado curso seria toodelete esse registro e permitem que o cliente Olá recriá-la antes de enviar Olá Mensagem. 

> [!NOTE]
> Observe que use Olá dessa propriedade é extremamente limitada e portanto você deve usar isso apenas no ambiente de desenvolvimento/teste com um conjunto limitado de registros. Nós só enviar notificações de depuração too10 dispositivos. Também há um limite de processamento de depuração envia toobe 10 por minuto. 
> 
> 

### <a name="review-telemetry"></a>Telemetria de revisão
1. **Usar o Portal Clássico do Azure**
   
    Olá portal permite a você tooget uma visão geral de todas as atividades de saudação no Hub de notificação. 
   
    a) na guia de "painel" Olá, você pode exibir uma exibição agregada de registros de hello, notificações, bem como erros por plataforma. 
   
    ![][5]
   
    b) você também pode adicionar várias outras métricas específicas de plataforma do hello "Monitor" guia tootake particularmente uma análise mais profunda sobre os erros específicos do PNS retornado quando NH tenta toosend Olá notificação toohello PNS. 
   
    ![][6]
   
    c) você deve começar com revisão Olá **mensagens de entrada**, **operações de registro**, **notificações de sucesso** e, em seguida, vá tooper Olá de tooreview de guia de plataforma Erros específicos do PNS. 
   
    d) se você tiver notificação Olá hub mal configurado com as configurações de autenticação hello, em seguida, você verá o erro de autenticação do PNS. Essa é uma boa indicação toocheck Olá PNS de credenciais. 

2) **Acesso programático**

Mais detalhes aqui - 

* [Acesso Programático de Telemetria]
* [Acesso de Telemetria por meio do exemplo de APIs] 

> [!NOTE]
> Várias telemetrias relacionados a recursos como **Importação/Exportação de Registros**, **Acesso de Telemetria via APIs** etc. só estão disponíveis na camada Standard. Se você tentar toouse esses recursos se você estiver no gratuita ou básica, em seguida, você obterá o efeito de toothis de mensagem de exceção durante o uso de saudação SDK e um HTTP 403 (proibido) quando usá-los diretamente da saudação APIs REST. Certifique-se de que você moveu o nível de tooStandard por meio do Portal clássico do Azure.  
> 
> 

<!-- IMAGES -->
[0]: ./media/notification-hubs-diagnosing/Architecture.png
[1]: ./media/notification-hubs-diagnosing/GCMConfigure.png
[2]: ./media/notification-hubs-diagnosing/GCMEnable.png
[3]: ./media/notification-hubs-diagnosing/GCMServerKey.png
[4]: ./media/notification-hubs-diagnosing/PortalConfigure.png
[5]: ./media/notification-hubs-diagnosing/PortalDashboard.png
[6]: ./media/notification-hubs-diagnosing/PortalMonitoring.png
[7]: ./media/notification-hubs-diagnosing/PortalTestNotification.png
[8]: ./media/notification-hubs-diagnosing/VSRegistrations.png
[9]: ./media/notification-hubs-diagnosing/VSServerExplorer.png
[10]: ./media/notification-hubs-diagnosing/VSTestNotification.png

<!-- LINKS -->
[Visão Geral dos Hubs de Notificação]: notification-hubs-push-notification-overview.md
[obter tutoriais de Introdução]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[diretrizes de modelo]: https://msdn.microsoft.com/library/dn530748.aspx 
[Diretrizes do APNS]: https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW4
[Diretrizes do APNS]: http://developer.android.com/google/gcm/adv.html
[Export/Import Registrations]: http://msdn.microsoft.com/library/dn790624.aspx
[Gerenciador do Barramento de Serviço]: http://msdn.microsoft.com/library/dn530751.aspx
[Código do Gerenciador do Barramento de Serviço]: https://code.msdn.microsoft.com/windowsazure/Service-Bus-Explorer-f2abca5a
[Visão Geral do Gerenciador do VS Server]: http://msdn.microsoft.com/library/windows/apps/xaml/dn792122.aspx 
[Postagem do Blog do Gerenciador do VS Server- 1]: http://azure.microsoft.com/blog/2014/04/09/deep-dive-visual-studio-2013-update-2-rc-and-azure-sdk-2-3/#NotificationHubs 
[Postagem do Blog do Gerenciador do VS Server- 2]: http://azure.microsoft.com/blog/2014/08/04/announcing-release-of-visual-studio-2013-update-3-and-azure-sdk-2-4/ 
[EnableTestSend recurso]: http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx
[Acesso Programático de Telemetria]: http://msdn.microsoft.com/library/azure/dn458823.aspx
[Acesso de Telemetria por meio do exemplo de APIs]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/FetchNHTelemetryInExcel

