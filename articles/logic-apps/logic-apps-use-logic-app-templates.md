---
title: "fluxos de trabalho aaaCreate de modelos - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Introdução - criar fluxos de trabalho rapidamente usando o aplicativo do Azure lógica modelos tooconnect aplicativos e integrar os dados."
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 3656acfb-eefd-4e75-b5d2-73da56c424c9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: LADocs; klam
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0127523662a12076772b52968f1e2f9cbad72a1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-workflow-using-a-pre-built-template-or-pattern-tooget-started-quickly"></a>Configurar um fluxo de trabalho usando um modelo criado previamente ou padrão tooget iniciado rapidamente

## <a name="what-are-logic-app-templates"></a>O que são modelos de aplicativo lógico
Um modelo de lógica de aplicativo é um aplicativo de lógica predefinidos que você pode usar tooquickly começar a criar seu próprio fluxo de trabalho. 

Esses modelos é uma boa maneira toodiscover vários padrões que podem ser criados usando aplicativos lógicos. Você pode usar esses modelos como-está ou modificá-las toofit seu cenário.

## <a name="overview-of-available-templates"></a>Visão geral dos modelos disponíveis
Há muitos modelos disponíveis atualmente publicados na plataforma de aplicativo hello lógica. Algumas categorias de exemplo, bem como tipo de saudação de conectores usados, está listado abaixo.

### <a name="enterprise-cloud-templates"></a>Modelos de nuvem empresarial
Os modelos que integram o Dynamics CRM, o Salesforce, o Box, o Blob do Azure e outros conectores para suas necessidades de nuvem empresarial. Alguns exemplos do que pode ser feito com esses modelos incluem a organização dos clientes potenciais e fazer backup de dados de arquivos corporativos.

### <a name="enterprise-integration-pack-templates"></a>Modelos de pacote de integração empresarial
Configurações de VETER (validar, extrair, transformar, enriquecer, rotear) pipelines, recebendo um X12 EDI documento via AS2 e transformá-los tooXML, bem como mensagem X12 e AS2 manipulação.

### <a name="protocol-pattern-templates"></a>Modelos de padrão de protocolo
Esses modelos consistem em aplicativos lógicos que contêm os padrões de protocolo como solicitação-resposta sobre HTTP, bem como integrações por meio de FTP e SFTP. Use-os como estão ou como base para a criação de padrões mais complexos de protocolo.  

### <a name="personal-productivity-templates"></a>Modelos de produtividade pessoal
Padrões toohelp melhorar a produtividade pessoal incluem modelos que definir lembretes diárias, transformam os itens de trabalho importante em listas de tarefas e automatizam tarefas demoradas para baixo tooa etapa de aprovação de usuário único.

### <a name="consumer-cloud-templates"></a>Modelos de nuvem do consumidor
Os modelos simples que se integram com os serviços de mídia social, como o Twitter, o Slack e o email, basicamente capaz de reforçar as iniciativas de marketing de mídia social. Eles também incluem modelos como a cópia em nuvem, que podem ajudar a aumentar a produtividade, economizando o tempo gasto em tarefas tradicionalmente repetitivas. 

## <a name="how-toocreate-a-logic-app-using-a-template"></a>Como toocreate um aplicativo lógico usando um modelo
tooget iniciado usando um modelo de aplicativo de lógica, entrar no designer de saudação lógica do aplicativo. Se você estiver inserindo designer Olá abrindo um aplicativo existente da lógica, Olá lógica aplicativo carrega automaticamente no modo de exibição designer. No entanto, se você estiver criando um novo aplicativo de lógica, verá uma tela hello abaixo.  
 ![](../../includes/media/app-service-logic-templates/template7.png)  

Nessa tela, você pode escolher toostart com um aplicativo em branco lógica ou um modelo criado previamente. Se você selecionar um dos modelos de hello, são fornecidos com informações adicionais. Neste exemplo, usamos Olá *quando um novo arquivo é criado no Dropbox, copie tooOneDrive* modelo.  
 ![](../../includes/media/app-service-logic-templates/template2.png)  

Se você escolher o modelo de saudação do toouse, basta selecionar Olá *usar esse modelo* botão. Você será solicitado toosign tooyour contas com base em qual modelo de saudação conectores utiliza. Ou, se você tiver estabelecido uma conexão com esses conectores anteriormente, poderá selecionar continuar conforme mostrado abaixo.  
 ![](../../includes/media/app-service-logic-templates/template3.png)  

Depois de estabelecer conexão hello e selecionar *continuar*, Olá lógica aplicativo é aberto no designer de exibição.  
 ![](../../includes/media/app-service-logic-templates/template4.png)  

O exemplo hello acima, como Olá caso com muitos modelos, alguns dos campos de propriedade obrigatória Olá podem ser preenchido em conectores de saudação; No entanto, alguns ainda podem exigir um valor antes de poder tooproperly implantar o aplicativo de lógica de saudação. Se você tentar toodeploy sem inserir alguns Olá campos ausentes, você será notificado com uma mensagem de erro.

Se desejar que o Visualizador de modelo de toohello tooreturn, selecione Olá *modelos* botão na barra de navegação superior hello. Alternando o Visualizador do modelo toohello back, você perderá qualquer progresso não salvo. Tooswitching anterior no Visualizador de modelo, você verá uma mensagem de aviso informando sobre isso.  
 ![](../../includes/media/app-service-logic-templates/template5.png)  

## <a name="how-toodeploy-a-logic-app-created-from-a-template"></a>Como toodeploy um lógica de aplicativo criado com um modelo
Depois que você carregar o modelo e fez as alterações desejadas, selecione Olá botão Salvar no canto superior esquerdo da saudação. Isso salva e publica seu aplicativo lógico.  
 ![](../../includes/media/app-service-logic-templates/template6.png)  

Se você deseja obter mais informações sobre como tooadd mais etapas em um modelo de aplicativo lógica existente, ou fazer edições em geral, leia mais em [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).

