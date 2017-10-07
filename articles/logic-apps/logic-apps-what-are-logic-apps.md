---
title: "aplicativos aaaConnect e integrar dados de fluxos de trabalho - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Crie fluxos de trabalho e automatize processos ao conectar aplicativos e integrar dados com o Aplicativo Lógico do Azure."
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 07765c05-72a6-4169-a8ab-f6420bfbaf07
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/23/2017
ms.author: klam
ms.openlocfilehash: 53d4e165bb2205ddd56c1950719389725267ddea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-logic-apps"></a>O que são Aplicativos Lógicos?
Aplicativos lógicos fornecem uma maneira toosimplify e implementam integrações escalonáveis e fluxos de trabalho na nuvem hello. Ele fornece um toomodel designer visual e automatizar o processo de uma série de etapas conhecido como um fluxo de trabalho.  Há [muitos conectores](../connectors/apis-list.md) em tooquickly de nuvem e local Olá integrar em serviços e protocolos.  Um aplicativo lógico começa com um gatilho (como 'quando uma conta é adicionada tooDynamics CRM') e depois de acionamento pode começar a muitas combinações de ações, conversões e a lógica da condição.

Olá vantagens de usar aplicativos lógicos: seguinte Olá  

* Economia de tempo, a criação de processos complexos usando ferramentas de design de fácil toounderstand
* Implementação de padrões e fluxos de trabalho sem problemas, que de outra forma seria difícil tooimplement no código
* Introdução rápida devido aos modelos
* Personalização do seu aplicativo lógico com seus próprios códigos, APIs e ações personalizados
* Conecte-se e sincronizar sistemas discrepantes entre locais e Olá nuvem
* Criado com base no BizTalk Server, Gerenciamento de API, Azure Functions e Barramento de Serviço do Azure com excelente suporte à integração

Lógica de aplicativos é uma iPaaS totalmente gerenciado (integração de plataforma como serviço) que permite aos desenvolvedores não toohave tooworry sobre a criação de hospedagem, escalabilidade, disponibilidade e gerenciamento.  Lógica de aplicativos será dimensionado a demanda de toomeet automaticamente.

![Designer de aplicativo de fluxo](media/logic-apps-what-are-logic-apps/LogicAppCapture2.png)

Conforme mencionado, com Aplicativos Lógicos, você pode automatizar processos de negócios. Aqui estão alguns exemplos:  

* Mover arquivos carregados tooan servidor FTP no armazenamento do Azure
* Processar e rotear solicitações entre sistemas locais e na nuvem
* Monitorar todos os tweets sobre um determinado tópico, analisar o sentimento hello e criar alertas e tarefas para itens que precisam de acompanhamento.

Cenários como estes podem ser configurados todos do designer visual hello e sem escrever uma única linha de código. Comece a [criar seu aplicativo lógico agora][create].  Uma vez gravado, um aplicativo lógico pode ser [rapidamente implantado e reconfigurado](../logic-apps/logic-apps-create-deploy-template.md) em vários ambientes e regiões.

## <a name="why-logic-apps"></a>Por que Aplicativos Lógicos?
Lógica de aplicativos oferece velocidade e a escalabilidade no espaço de integração do hello enterprise.  facilidade de saudação do uso do designer de hello, variedade de ferramentas avançadas de gerenciamento, ações e gatilhos disponíveis Verifique centralizando suas APIs ainda mais simples.  Como as empresas se direcione digitalization, lógica de aplicativos permite que você tooconnect herdados e de última geração sistemas juntos.

Além disso, com nossas [Enterprise integração conta] [ biztalk] você pode dimensionar toomature cenários de integração com o poder de saudação de um [mensagens XML] [ xml], [comerciais gerenciamento parceiro][tpm]e muito mais.

* **Ferramentas de design de fácil toouse** -lógica de aplicativos pode ser projetado para-ponta no navegador de saudação ou com ferramentas do Visual Studio. Iniciar com um gatilho - toowhen um agendamento simples que é criado um problema do GitHub. Em seguida, orquestra qualquer número de ações usando a Galeria de saudação avançados de conectores.
* **Conecte-se a APIs facilmente** -tarefas de composição mesmo fácil toodescribe são difíceis tooimplement no código. Lógica de aplicativos torna fácil tooconnect diferentes sistemas. Deseja tooconnect sua nuvem de solução de marketing tooyour sistema de cobrança local? Deseja toocentralize mensagens através de APIs e os sistemas com um barramento de serviço corporativo? Aplicativos lógicos são hello mais rápida e mais confiável maneira toodeliver soluções toothese.
* **Começar rapidamente modelos** -toohelp começar fornecemos um [Galeria de modelos de] [ templates] que permitem que você toorapidly criar algumas soluções comuns. De B2B soluções avançadas toosimple conectividade de SaaS e alguns que são apenas 'para diversão' - Olá é Olá tooget de maneira mais rápida de Introdução ao power Olá de lógica de aplicativos.
* **Extensibilidade baked no** -não vê o conector de saudação é necessário? Lógica de aplicativos é projetado toowork com suas próprias APIs e código; Você pode facilmente criar seu próprio toouse do aplicativo de API como um conector personalizado ou chamar um [Azure função](https://functions.azure.com) tooexecute trechos de código sob demanda. 
* **Potência real de integração** – inicie com facilidade e cresça conforme necessário. Lógica de aplicativos facilmente pode aproveitar o poder de saudação do BizTalk, setor principal solução tooenable integração profissionais toobuild Olá soluções de integração da Microsoft que precisam. Saiba mais sobre Olá [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).

## <a name="logic-app-concepts"></a>Conceitos de Aplicativo Lógico
Olá Eis algumas das principais partes do hello que compõem a experiência de aplicativos lógicos hello. 

* **Fluxo de trabalho** -lógica de aplicativos fornece uma maneira gráfica toomodel seus processos de negócios como uma série de etapas ou um fluxo de trabalho.
* **Gerenciado conectores** -seus aplicativos lógicos precisam acessar toodata e serviços. Conectores gerenciados são criados especificamente tooaid quando você está se conectando tooand trabalhando com seus dados. Consulte lista de saudação de conectores disponíveis no [gerenciados conectores][managedapis].
* **Gatilhos** – alguns conectores gerenciados também podem atuar como um gatilho. Um gatilho inicia uma nova instância de fluxo de trabalho com base em um evento específico, como Olá chegada de um email ou uma alteração em sua conta de armazenamento do Azure.
* **Ações** -cada etapa Olá gatilho after em um fluxo de trabalho é chamado uma ação. Cada ação normalmente mapeia tooan operação no conector gerenciado ou aplicativos de API personalizada.
* **Enterprise Integration Pack** – para cenários de integração mais avançados, os Aplicativos Lógicos incluem recursos do BizTalk. O BizTalk é a plataforma de integração da Microsoft líder do setor. conectores do pacote de integração do Enterprise Olá permitem tooeasily incluir validação, transformação e muito mais em fluxos de trabalho de aplicativo lógico tooyour.

## <a name="getting-started"></a>Introdução
* tooget iniciado com a lógica de aplicativos, siga Olá [criar um aplicativo lógico] [ create] tutorial.  
* [Veja exemplos e cenários comuns](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Você pode automatizar processos de negócios com Aplicativos Lógicos](http://channel9.msdn.com/Events/Build/2016/T694) 
* [Saiba como tooIntegrate seus sistemas com aplicativos lógicos](http://channel9.msdn.com/Events/Build/2016/P462)

[biztalk]: logic-apps-enterprise-integration-accounts.md
[appservice]: ../app-service/app-service-value-prop-what-is.md
[create]: logic-apps-create-a-logic-app.md
[managedapis]: ../connectors/apis-list.md
[tpm]: logic-apps-enterprise-integration-accounts.md
[xml]: logic-apps-enterprise-integration-b2b.md
[templates]: logic-apps-use-logic-app-templates.md
