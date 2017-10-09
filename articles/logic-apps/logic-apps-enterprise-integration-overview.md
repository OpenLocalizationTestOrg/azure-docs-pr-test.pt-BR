---
title: "aaaEnterprise integração para B2B - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Criar fluxos de trabalho de B2B e dar suporte a cenários de integração do enterprise para os aplicativos lógicos com hello Enterprise Integration Pack"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: dd517c4d-1701-4247-b83c-183c4d8d8aae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8dc866533110b1d07f51cf446056d2ca5ce869ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-b2b-scenarios-and-communication-with-hello-enterprise-integration-pack"></a>Visão geral: Cenários B2B e comunicação com hello Enterprise Integration Pack

Para fluxos de trabalho entre empresas (B2B) e comunicação direta com os aplicativos lógicos do Azure, você pode habilitar cenários de integração do enterprise com a solução baseada em nuvem da Microsoft, Olá Enterprise Integration Pack. Organizações podem trocar mensagens eletronicamente, mesmo usando diferentes protocolos e formatos. pacote de saudação transforma formatos diferentes em um formato que sistemas de organizações podem interpretar e processar. As organizações podem trocar mensagens por meio de protocolos padrão da indústria, incluindo [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md) e [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md). Também é possível proteger mensagens com criptografia e assinaturas digitais.

Se você estiver familiarizado com o BizTalk Server ou serviços BizTalk do Microsoft Azure, recursos de integração do Enterprise Olá são toouse fácil porque a maioria dos conceitos são semelhantes. A principal diferença é que a integração da empresa usa armazenamento de saudação de toosimplify de contas de integração e gerenciamento de artefatos usados nas comunicações de B2B. 

Em termos de arquitetura, Olá Enterprise Integration Pack baseia-se em "contas de integração". Essas contas são contêineres baseados em nuvem que armazenam todos os artefatos, como esquemas, parceiros, certificados, mapas e contratos. Você pode usar toodesign esses artefatos, implantar e manter seus aplicativos B2B e também toobuild B2B fluxos de trabalho para os aplicativos lógicos. Mas, antes de usar esses artefatos, primeiro você deve vincular o seu aplicativo de conta tooyour lógica da integração. Depois disso, o aplicativo lógico poderá acessar os artefatos da sua conta de integração.

## <a name="why-should-you-use-enterprise-integration"></a>Por que você deve usar a integração corporativa?

* Com a integração corporativa, é possível armazenar todos os artefatos em um único local: sua conta de integração.
* Você pode criar fluxos de trabalho de B2B e integrar aplicativos do terceiro software como serviço (SaaS), aplicativos locais e aplicativos personalizados usando o mecanismo de aplicativos do Azure lógica hello e todos os seus conectores.
* Você pode criar código personalizado para seus aplicativos lógicos com o Azure Functions.

## <a name="how-tooget-started-with-enterprise-integration"></a>Como tooget iniciado com a integração da empresa?

Você pode criar e gerenciar aplicativos B2B com hello Enterprise Integration Pack por meio de saudação lógica de aplicativo Designer no hello **portal do Azure**. Também é possível gerenciar aplicativos lógicos com o [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Tópicos do PowerShell para aplicativos lógicos").

Aqui estão as etapas de alto nível hello, que você deve executar antes de criar aplicativos no hello portal do Azure:

![imagem da visão geral](media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a>Quais são os cenários comuns?

O Enterprise Integration oferece suporte a estes padrões do setor:

* EDI - Intercâmbio Eletrônico de Dados
* EAI - Integração de Aplicativos Empresariais

## <a name="heres-what-you-need-tooget-started"></a>Aqui está o que você precisa tooget iniciado

* Uma assinatura do Azure com uma conta de integração
* Visual Studio 2015 toocreate mapas e esquemas
* [Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0 (Ferramentas de integração corporativa do Aplicativo Lógico do Microsoft Azure para Visual Studio 2015)](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a>Teste agora

[Implantar um envio de AS2 exemplo totalmente operacional e lógica de aplicativo de recebimento](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) que usa recursos de saudação B2B para os aplicativos lógicos do Azure.

## <a name="learn-more"></a>Saiba mais
* [Contratos](../logic-apps/logic-apps-enterprise-integration-agreements.md "Saiba mais sobre contratos de integração corporativa")
* [Cenários de tooBusiness (B2B) Business](../logic-apps/logic-apps-enterprise-integration-b2b.md "Saiba como toocreate lógica aplicativos com recursos de B2B")  
* [Certificados](logic-apps-enterprise-integration-certificates.md "Saiba mais sobre certificados da integração corporativa")
* [Simples de codificação/decodificação de arquivo](logic-apps-enterprise-integration-flatfile.md "Saiba como tooencode e decodificar o conteúdo do arquivo simples")  
* [Integration accounts](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn about contas de integração")
* [Mapas](../logic-apps/logic-apps-enterprise-integration-maps.md "Saiba mais sobre mapas da integração corporativa")
* [Parceiros](logic-apps-enterprise-integration-partners.md "Saiba mais sobre parceiros da integração corporativa")
* [Esquemas](logic-apps-enterprise-integration-schemas.md "Saiba mais sobre esquemas de integração corporativa")
* [Validação de mensagem XML](logic-apps-enterprise-integration-xml.md "Saiba como toovalidate XML mensagens com aplicativos lógicos")
* [Transformação de XML](logic-apps-enterprise-integration-transform.md "Saiba mais sobre mapas da integração corporativa")
* [Conectores de integração Enterprise](../connectors/apis-list.md "Saiba mais sobre os conectores do enterprise integration pack")
* [Metadados da conta de integração](../logic-apps/logic-apps-enterprise-integration-metadata.md "Saiba mais sobre os metadados da conta de integração")
* [Monitorar mensagens B2B](logic-apps-monitor-b2b-message.md "Saiba mais sobre o monitoramento de mensagens B2B")
* [Rastreando mensagens B2B no portal do OMS](logic-apps-track-b2b-messages-omsportal.md "Saiba mais sobre o acompanhamento de mensagens B2B no portal do OMS")

