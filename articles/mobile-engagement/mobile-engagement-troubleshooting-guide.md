---
title: aaaAzure Mobile Engagement Solucionando problemas de guias
description: "Guia de solução de problemas para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 31134a29-a513-4e5e-b626-f6cf6fe04769
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: dd69bfd7019907c3e1da8df590db3b5f61606173
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement---troubleshooting-guide"></a>Guia de solução de problemas do Azure Mobile Engagement
## <a name="introduction"></a>Introdução
Olá guia de solução de problemas a seguir ajudarão você a entender causas raiz de alguns problemas comuns e irá habilitar tootroubleshoot por conta própria. 

## <a name="general"></a>Geral
Em geral, você deve garantir sempre seguinte hello:

1. Certifique-se de que você ter feito todas as etapas de saudação necessárias para a integração, conforme descrito em nossa [tutoriais de Introdução](mobile-engagement-windows-store-dotnet-get-started.md)
2. Você está usando a versão mais recente de saudação do SDKs de plataforma hello. 
3. Teste em um dispositivo real e um emulador porque alguns problemas são apenas tooemulator específico. 
4. Você não está atingindo nenhum dos limites/restrições do Mobile Engagement documentados [aqui](../azure-subscription-service-limits.md)
5. Se você não puder tooconnect toohello Mobile Engagement serviço back-end ou visualização de dados não está sendo carregados continuamente, certifique-se de que não há nenhum incidente de serviço em andamento, verificando [aqui](https://azure.microsoft.com/status/)

## <a name="monitor-issues"></a>Problemas com o 'Monitor'
### <a name="i-am-not-seeing-my-device-showing-up-on-hello-monitor-tab"></a>Não vejo o meu dispositivo aparecendo na guia do Monitor de saudação
Guia monitorar mostra a plataforma de compromisso de mobilidade Olá dispositivos conectados tooyour em tempo real. Se você estiver depurando em um dispositivo e emulador, você verá pelo menos uma sessão aqui. Se o aplicativo hello tiver sido distribuído, você verá Olá medidor refletir dispositivos Olá plataforma toohello conectado em tempo real de sessões ativas. 

Se você não estiver vendo o dispositivo na guia do Monitor de saudação é provavelmente um problema de integração do SDK. Alguns tootroubleshoot de tootake etapas comuns são as seguintes:

1. Verifique se você estiver usando a cadeia de caracteres de conexão correta Olá no aplicativo móvel hello e é da seção de chaves do SDK hello e não Olá seção de chaves de API. cadeia de caracteres de conexão Olá conecta-se a instância de toohello do aplicativo móvel do aplicativo do Mobile Engagement Olá no qual você verá seu dispositivo no guia do Monitor de saudação. 
2. Para a plataforma Windows - se sua página substitui Olá `OnNavigatedTo` método, toocall se tornar `base.OnNavigatedTo(e)`.
3. Se você estiver integrando o Mobile Engagement em um aplicativo móvel existente, você também pode garantir que você não está faltando todas as etapas examinando Olá avançado etapas de integração [aqui](mobile-engagement-windows-store-integrate-engagement.md)
4. Certifique-se de que você está enviando a pelo menos uma tela/atividade substituindo página Olá com EngagementActivity dependendo da plataforma Olá você está trabalhando, conforme descrito em Olá [tutoriais de Introdução](mobile-engagement-windows-store-dotnet-get-started.md).

### <a name="i-am-seeing-hello-monitor-tab-showing-a-session-even-when-i-have-disconnected-or-closed-my-app-emulator"></a>Estou vendo mostrando uma sessão da guia monitorar Olá mesmo quando tiver desconectado ou fechado meu aplicativo / emulador.
Se você está apenas uma plataforma de toohello conectado Olá neste momento e você estiver usando um aplicativo de saudação do emulador tooopen, em seguida, provavelmente é devido tooemulator quirks. Em geral, é preciso tooensure que você volte a tela inicial toohello no emulador Olá para toodisconnect de sessão do aplicativo hello com êxito. Além disso, na plataforma Windows, durante a depuração com o Visual Studio, talvez seja necessário tooensure no Visual Studio, vá toohello **eventos de ciclo de vida** barra de menus e clique em **Suspend** tooreally fechar sessão de saudação. Vejao [Tutorial do Windows](mobile-engagement-windows-store-dotnet-get-started.md) para obter mais detalhes. 

## <a name="analytics-issues"></a>Problemas de 'Análise'
### <a name="i-am-not-seeing-any-data-refreshed-data-on-analytics-tab"></a>Eu não estou vendo nenhum dado / dado atualizado na guia Análise
Os dados de análise são recalculados regularmente e essa atualização pode levar até 24. Esses dados não são em tempo real e você os verá atualizados nesse período de 24 horas.
Certifique-se no entanto que você está enviando pelo menos uma tela ou back-end de plataforma de toohello atividade por qualquer substituição pelo menos uma página com `EngagementActivity` ou chamar `SendActivity` explcitly. 

### <a name="i-am-seeing-incorrectly-captured-datetime-for-a-device-on-hello-analytics-tab"></a>Estou vendo incorretamente capturada data/hora para um dispositivo na guia de análise de saudação
Olá período de tempo para análise é baseado nas Olá data dos usuários Olá configurações de dispositivo. Para garantir que Olá dispositivo tem date de hello definida corretamente. 

## <a name="segment-issues"></a>Problemas de 'Segmento'
### <a name="i-created-a-segment-and-it-is-showing-up-as-greyed-out-or-not-showing-any-data"></a>Criei um segmento e está aparecendo como desativado ou não mostra nenhum dado
Criação de segmento não é em tempo real no momento da saudação. Ele é calculado em Olá a mesma hora como dados de análise de saudação são agregados e, portanto, pode levar até 24 horas. Você deve verificar novamente mais tarde, mas enquanto você também deve garantir que seus aplicativos móveis realmente estão enviando dados saudação em base de saudação do qual você se formam segmentos de saudação. Por exemplo Se um evento dizer 'foo' não está sendo enviada por qualquer dispositivo móvel e não haver nenhum dado de segmento de um segmento criado com EventName = foo como critério de saudação. Você também deve verificar sua tooensure de integração do SDK seu aplicativo móvel está enviando dados saudação corretamente. 

## <a name="reach-or-push-notifications-issues"></a>Problemas de notificações por Push ou 'Reach'
### <a name="my-push-messages-are-not-being-delivered"></a>Minhas mensagens de push não estão sendo entregues
1. Tente enviar notificações tooa teste dispositivo primeiro tooensure todos os componentes de saudação - aplicativo móvel, o serviço SDK e hello são toodeliver conectado corretamente e é capaz de notificações de envio. 
2. Sempre enviar hello mais simples 'fora do aplicativo notificação' primeiro por meio de uma campanha que não está agendada e nem tem qualquer critério de público especificado. Essa é a mais tooprove conectividade de notificação está funcionando corretamente. 
3. Se você estiver tendo problemas na entrega de notificações no aplicativo, em seguida, também é recomendável primeiro etapa tootry enviar uma notificação de limite do aplicativo pela primeira vez. 
4. Certifique-se de que Olá 'Push nativo' está configurado corretamente para seu aplicativo móvel. Dependendo da plataforma de saudação Isso envolverá ou chaves (Android, Windows) ou certificados (iOS). Consulte [Interface do usuário - Configurações](mobile-engagement-user-interface-settings.md)
5. Fora do aplicativo notificações também podem ser bloqueadas por Olá usuário via Olá que sistema operacional móvel para garantir que isso não se hello. 
6. Certifique-se de que você está configurando não Olá *ignorar público, push será enviado toousers via Olá API* opção Olá **campanha** seção de um alcance da campanha porque isso irá garantir que o envio notificações só podem ser enviadas por meio de APIs. 
7. Certifique-se de que você está testando sua campanha de push com dois um dispositivo conectado via telefone e WIFI operador rede tooeliminate Olá rede conexão como uma possível fonte de problemas.
8. Certifique-se de sistema Olá data/hora no seu dispositivo/emulador está correta, porque qualquer dispositivo fora de sincronia também irá interferir com notificações de toodeliver da Olá Push Notification Service capacidade. 

Abaixo estão mais instruções de solução de problemas relacionados à plataforma:

1. **iOS** 
   
   * Verifique se certificados Olá são válidas e não expiradas para iOS notificações por Push. 
   * Certifique-se de que você está configurando corretamente um certificado de *Produção* em seu aplicativo Mobile Engagement. 
   * Certifique-se de que você esteja testando em um *dispositivo real, físico.* simulador de iOS Olá não pode processar mensagens de envio por push.
   * Certifique-se de que Olá que identificador de pacote está configurado corretamente no aplicativo móvel hello. Consulte as instruções de saudação [aqui](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)
   * Durante o teste, use a distribuição "Ad Hoc" em seu perfil de provisionamento móvel. Não será capaz de tooreceive notificação se seu aplicativo é compilado usando "Debug"
2. **Android**
   
   * Certifique-se de que você especificou o número correto de projeto Olá no arquivo AndroidManifest.xml de seu aplicativo móvel que é seguido pelo caractere \n. 
     
           <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
   * Certifique-se de que não estão ausentes ou incorretamente configurado qualquer permissão no arquivo de manifesto do Android Olá 
   * Assegure-se de que o número de projeto de saudação você está adicionando tooyour aplicativo de cliente esteja na mesma conta em que você obteve Olá GCM chave do servidor de saudação. Qualquer incompatibilidade entre hello dois impedirá que o coloca saem. 
   * Se você estiver recebendo sistema notificações, mas não no aplicativo, em seguida, examine Olá [especificar um ícone para a seção de notificações](mobile-engagement-android-get-started.md) como provavelmente você não especificar ícone correto Olá no arquivo de manifesto do Android hello. 
   * Se você está enviando uma notificação BigPicture, certifique-se de que, se você tem servidores de imagem externa, em seguida, precisam toobe capaz de toosupport HTTP "GET" e "HEAD".
3. **Windows**
   
   * Certifique-se de que você associou o aplicativo hello com um aplicativo da Windows Store válida. No Visual Studio - você terá tooright clique Olá projeto e selecione opção "Associar o aplicativo com o repositório" e selecione Olá aplicativo criado na saudação da Windows Store. Este aplicativo da Windows Store deve ser Olá mesmo de onde você obteve tooconfigure de credenciais de push nativo Olá no portal do Mobile Engagement hello.
   * Se você estiver recebendo notificações por push fora do aplicativo, mas não notificações no aplicativo com integração `EngagementOverlay` , então verifique se há um elemento de grade na raiz na sua página. EngagementOverlay usa Olá primeiro "Grade" elemento encontrar em seu xaml arquivo tooadd duas exibições da web em sua página. Se você quiser toolocate onde exibições da web serão definidas, você pode definir uma grade chamada "EngagementGrid" assim, no entanto, você terá tooensure há suficiente altura e largura para Olá subsequentes dois modos de exibição que irá mostrar notificação hello e Olá a seguir da web anúncio como notificação no aplicativo:
     
           <Grid x:Name="EngagementGrid"></Grid>

### <a name="i-created-a-push-notificationannouncement-campaign-and-even-after-it-sent-me-hello-notification-it-is-showing-as-active-what-does-it-mean"></a>Criei um notificação de push/comunicado/da campanha e mesmo depois que ele me enviou notificação hello, ele aparece como 'Active'. O que isso significa?
Olá **campanha** que você criou no Mobile Engagement é chamado de forma porque é um significado de notificação por push em tempo de execução quando novos dispositivos se conectam a plataforma do tooyour do mobile engagement, eles serão automaticamente enviados notificação Olá você configurar aqui, desde que eles atendem critério Olá definido em uma campanha de saudação. Essa não é uma configuração de notificação única. Você terá que toomanually clique em Olá **concluir** botão campanha de saudação tooterminate para que ele não envia mais notificações. 

### <a name="i-created-a-push-campaign-and-i-am-receiving-notifications-successfully-however-whenever-i-open-up-hello-app-i-get-hello-same-notification-even-when-i-had-actioned-it-before"></a>Criei uma campanha de push e estou recebendo notificações com êxito no entanto sempre que abrir o aplicativo hello, obter Olá mesmo notificação mesmo quando tive acionadas antes?
Esse é provavelmente toohappen durante o teste e se você estiver usando emuladores ou alguma estrutura de teste como TestFlight. O que está acontecendo aqui é que, em todos os aplicativos de instância de execução, ele é adquirir um novo DeviceID e enviá-la tooour back-end que está causando o tootreat de plataforma do Mobile Engagement Olá-o como um novo dispositivo e enviar a notificação de saudação. 

## <a name="getting-support"></a>Obtendo suporte
Se você estiver tooresolve não é possível problema de saudação por conta própria, em seguida, você pode:

1. Pesquise o problema em threads de saudação existente no Fórum de StackOverflow e [Fórum do MSDN](https://social.msdn.microsoft.com/Forums/windows/en-US/home?forum=azuremobileengagement) e se não, em seguida, faça uma pergunta lá. 
2. Se você encontrar um recurso ausente, em seguida, adicionar/voto para solicitação de saudação em nosso [Fórum do UserVoice](https://feedback.azure.com/forums/285737-mobile-engagement/)
3. Se você tiver aberto de suporte da Microsoft um incidente de suporte, fornecendo Olá detalhes a seguir: 
   * ID de assinatura do Azure
   * Plataforma (por exemplo, iOS, Android, etc.)
   * ID do Aplicativo
   * ID da campanha (para problemas de notificação por push)
   * Id do Dispositivo
   * Versão do SDK do Mobile Engagement (por exemplo, Android SDK v2.1.0)
   * Detalhes do erro com a mensagem de erro e cenário exatos

