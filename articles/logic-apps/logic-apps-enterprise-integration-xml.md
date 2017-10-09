---
title: "mensagens de aaaWorking com XML em seus fluxos de trabalho - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Processar, validar, transformar e enriquecer XML mensagens em aplicativos lógicos e o uso de negócios tooscenarios Olá Enterprise Integration Pack"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 47672dc4-1caa-44e5-b8cb-68ec3a76b7dc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 02/27/2017
ms.author: LADocs; mandia
ms.openlocfilehash: f90ae89fef0a4bd17286adbce398e573940bb790
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="validate-and-transform-xml-encode-and-decode-flat-files-and-enrich-messages-features-in-logic-apps"></a>Validar e transformar o XML, codificar e decodificar arquivos simples e enriquecer os recursos de mensagens em aplicativos lógicos

Usar aplicativos lógicos, você tem capacidade tooprocess XML mensagens de saudação do que você envia e recebe. Este recurso está incluído com hello Enterprise Integration Pack. Para os usuários com um plano de fundo do BizTalk Server, Olá Enterprise Integration Pack fornece tootransform de recursos semelhantes e validar mensagens, trabalhar com arquivos simples e até mesmo usar XPath tooenrich ou extrair propriedades específicas de uma mensagem. 

Para os usuários que são um novo espaço de toothis, esses recursos expanda como processar mensagens de fluxo de trabalho. Por exemplo, se você estiver em um cenário de business-to-business e trabalhar com esquemas XML específicos, você pode usar o hello Enterprise Integration Pack tooenhance como sua empresa processa essas mensagens. 

Olá Enterprise Integration Pack inclui: 

* [Validação de XML](logic-apps-enterprise-integration-xml-validation.md "Saiba mais sobre a validação de mensagens XML") – Validar uma mensagem XML de entrada ou de saída em relação a um esquema específico.
* [Transformação XML](../logic-apps/logic-apps-enterprise-integration-transform.md "Saiba mais sobre as transformações de mensagens XML e mapas") - converter ou personalizar uma mensagem XML com base em seus requisitos ou requisitos de saudação de um parceiro.
* [Codificação e decodificação de arquivos simples](logic-apps-enterprise-integration-flatfile.md "Saiba mais sobre a codificação/decodificação de arquivos simples") Codificar ou decodificar arquivos simples. Por exemplo, o SAP aceita e envia arquivos IDOC no formato de arquivo simples. Muitas plataformas de integração criam mensagens XML, incluindo Aplicativos Lógicos. Portanto, você pode criar um aplicativo de lógica que usa Olá arquivo simples codificador muito "converter" arquivos de tooflat de arquivos XML. 
* [XPath](https://msdn.microsoft.com/library/mt643789.aspx) - enriquecer uma mensagem e extrair propriedades específicas de mensagem de saudação. Você pode então usar Olá extraído tooa destino da mensagem de saudação propriedades tooroute ou um ponto de extremidade intermediário.

## <a name="try-it-out"></a>Experimentar
[Implantar um aplicativo totalmente operacional lógica ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (exemplo GitHub) usando recursos do XML de saudação do Azure lógica de aplicativos.

## <a name="learn-more"></a>Saiba mais
[Saiba mais sobre Olá Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise")
