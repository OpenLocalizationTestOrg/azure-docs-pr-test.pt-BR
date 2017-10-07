---
title: aaaAzure Mobile Engagement Troubleshooting Guide - SDK
description: "Solucionando problemas de integração do SDK no Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: de265cf1-2f88-43ef-8616-156ada5be7b6
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1c082b81d898f4bdb47b8efe6cfbacfd83fe9279
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-sdk-integration-issues"></a>Guia de solução de problemas de integração do SDK
Olá seguem possíveis problemas que podem ocorrer com como do Azure Mobile Engagement se integra ao seu aplicativo.

## <a name="sdk-issues-discovered-by-a-failure-in-another-area-of-your-application"></a>Problemas SDK descobertos por uma falha em outra área do aplicativo
### <a name="issue"></a>Problema
* Falha de coleta de dados da interface do usuário (em Análise, Monitoramento, Segmentação ou Painéis).
* Falhas de envios por push (os envios por push não funcionam no aplicativo, fora do aplicativo ou ambos).
* Falhas de Recursos Avançados (Rastreamento, Localização geográfica ou Envios por Push de plataformas específicas que não funcionam).
* Falhas de API (geralmente, as falhas de API são silenciosas, sem mensagens de erro).
* Falhas de Serviço (nada no Azure Mobile Engagement funciona para seu aplicativo).

### <a name="causes"></a>Causas
* A maioria dos problemas que precisam toobe resolvido com hello SDK do Azure Mobile Engagement serão descobertos por uma falha em seu aplicativo (por exemplo, uma falha de coleta de dados de interface do usuário, falha de envio, falha de recurso avançado, falha da API, falhas de aplicativo ou serviço aparente interrupção).  
* Se um recurso específico do Azure Mobile Engagement nunca trabalhou em seu aplicativo antes, você precisará toocomplete integração de saudação. 
* Se um recurso específico do Azure Mobile Engagement estava trabalhando e interrompido, talvez seja necessário tooupgrade toohello a última versão com hello SDK do Azure Mobile Engagement. Lembre-se de que há uma versão diferente do hello SDK do Azure Mobile Engagement para cada plataforma com suporte pelo Azure Mobile Engagement (Android, iOS, Windows e Windows Phone).

#### <a name="sdk-integration"></a>Integração do SDK
* O Azure Mobile Engagement não está corretamente integrado no SDK (Análise).
* O Alcance não está corretamente integrado no SDK (Envio por Push No Aplicativo e Fora do Aplicativo).
* Certificado expirado ou incorreto PROD versus DEV (somente iOS).
* GCM ou ADM não estão corretamente integrados no SDK (somente Android - Envios por Push Específicos do Serviço).
* O rastreamento não está corretamente integrado no SDK (instalar rastreamento de loja).
* Localização lenta ou Localização de GPS não estão corretamente integradas no SDK (direcionamento por localização geográfica).

**Consulte também:**

* [Documentação do SDK ‑ Guias de Integração][Link 5] 
* [Guia de solução de problemas – Push][Link 23]

#### <a name="sdk-upgrade"></a>Atualização do SDK
* Precisa de problemas de tooresolve tooupgrade SDK com versões mais antigas do hello SDK (geralmente relacionados toonewer versões do SO do dispositivo Olá).
* Desinstale todas as versões anteriores do aplicativo do dispositivo e reinstale a versão mais recente de saudação do seu aplicativo, Olá registrar novamente a ID do dispositivo de tooconfirm de interface de usuário do Azure Mobile Engagement Olá que seu dispositivo está usando a versão mais recente de saudação do seu aplicativo.

**Consulte também:**

* [Documentação do SDK - Notas de versão](http://go.microsoft.com/fwlink/?LinkId= 525554) 
* [Documentação do SDK - Guias de atualização](http://go.microsoft.com/fwlink/?LinkId= 525554)

#### <a name="sdk-other"></a>Outros problemas no SDK
* Erros no manifesto do aplicativo "AndroidManifest.xml" podem fazer com que o Azure Mobile Engagement toowork (somente Android).
* Um problema comum com integração SDK e o uso da API é tooconfuse hello chave SDK e Olá chave de API.

**Consulte também:**

* [Conceitos ‑ Glossário][Link 6]

## <a name="advanced-coding-issues"></a>Problemas de codificação avançados
### <a name="issue"></a>Problema
* Código específico de plataforma não estão diretamente relacionadas tooAzure que Mobile Engagement pode causar problemas no iOS, Android e Windows Phone.

### <a name="causes"></a>Causas
* Muitos problemas de codificação com o Azure Mobile Engagement avançados são causados por plataforma escrita incorretamente o código específico não estão diretamente relacionadas tooAzure Mobile Engagement. Você precisará tooconsult plataforma de toohello específico de documentação que está desenvolvendo para além de documentação do Mobile Engagement tooAzure (Android, iOS, Web, Windows e Windows Phone).
* Configurar não corretamente "categorias", impede a vinculação de um local de tooanother notificação dentro ou fora do aplicativo hello (somente Android). 
* Não, definindo "UIKit.framework" muito "opcional" no código do iOS, exibe um "Símbolo não encontrado o erro" e/ou falhas em dispositivos mais antigos do iOS (somente iOS).
* Certificados expirados ou não corretamente usando Olá desenvolvimento ou a versão de produção do cert hello, problemas de envio de causas (somente iOS).
* Há alguns plataforma tooa inerentes limitações que não é possível controlar o Azure Mobile Engagement (como como Olá system center funciona para fora do aplicativo envia no Android e iOS).
* O Azure Mobile Engagement publica uma lista completa dos pacotes de interno Olá usado pelo Azure Mobile Engagement para Android e iOS para referência. Tenha em mente que alguns recursos do Azure Mobile Engagement são toohello específico de plataforma (Android, iOS, Web, Windows e Windows Phone).

### <a name="see-also"></a>Consulte também
* [Guia de solução de problemas – Push][Link 23] 
* [Documentação do SDK – Notas de Versão][Link 5]
* [Documentação do SDK ‑ Guias de Atualização][Link 5]

## <a name="application-crashes"></a>Falhas do aplicativo
### <a name="issue"></a>Problema
* Falhas do seu aplicativo no dispositivo Olá dos usuários finais.

### <a name="causes"></a>Causas
* Informações de falha podem ser exibidas no hello *análise de interface do usuário* ou hello *API de análise*
* Você pode encontrar hello ID do dispositivo do seu dispositivo de teste e tomar Olá mesma ação que causou toocrash seu aplicativo para um usuário final toohelp identificar a causa de saudação do sua falha.
* Problemas conhecidos com hello SDK do Azure Mobile Engagement que fazer com que aplicativos toocrash às vezes são resolvidos pela atualização toohello a versão mais recente do SDK de saudação. Verifique se toocheck Olá notas sobre sua plataforma ao investigar falhas.

### <a name="see-also"></a>Consulte também
* [Documentação do SDK – Notas de Versão][Link 5]
* [Documentação do SDK ‑ Guias de Atualização][Link 5]

## <a name="app-store-upload-failures"></a>Falhas de carregamento nas lojas de aplicativos
### <a name="issue"></a>Problema
* Erros relacionados a versão mais recente do toouploading saudação do aplicativo tooApple, Google ou armazenamento de aplicativo do Windows hello.

### <a name="causes"></a>Causas
* Aplicativo às vezes armazenar aplicativos de bloco com determinados recursos habilitados (por exemplo, Olá Apple Store impede o uso de saudação do IDFV em aplicativos no repositório de saudação e repositório de GooglePlay Olá impede Olá compartilhamento de informações de aplicativo entre aplicativos). 
* Certifique-se de que você verifique as notas de versão de hello sobre a plataforma e a versão atual do SDK de saudação se você tiver dificuldade para carregar uma loja de aplicativos toohello.

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/en-us/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/en-us/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/en-us/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

