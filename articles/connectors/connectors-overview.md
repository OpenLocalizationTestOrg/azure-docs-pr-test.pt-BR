---
title: "aaaOverview de lógica de conectores de aplicativos | Microsoft Docs"
description: "Visão geral de conectores que podem ser usados em um aplicativo lógico"
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: ca8dab2e-9b69-4b1e-865d-1facd9f0cdac
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan
ms.openlocfilehash: dc4cac4c0dfaa2f9fd218ffc04414fa8e52a91d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-in-a-logic-app"></a>Usando conectores em um aplicativo lógico
Conectores fornecem acesso rápido tooevents, dados e ações em serviços, protocolos e plataformas.  lista completa de saudação de conectores que oferece suporte a aplicativos lógicos pode [ser encontradas aqui](apis-list.md).  Conectores pode ser usados como um disparador ou uma ação em um aplicativo lógico e pode exigir um configurado *conexão* toouse (por exemplo: Autorizar um Twitter conta tooaccess ou post em seu nome).

## <a name="basics"></a>Noções básicas
Você pode acessar como parte de um toointegrate de aplicativo lógica com outros serviços como Dynamics, Azure, a equipe de vendas, os serviços hospedados, os conectores são [e mais](apis-list.md).  Eles são implantados e gerenciados pela Microsoft para que você possa criar fluxos de trabalho de integração prestando atenção à escala, produtividade e segurança.  Você pode adicionar um aplicativo do conector tooa lógica procurando e selecionando uma ação do conector ou do gatilho em **APIs gerenciadas do Microsoft Mostrar**.

![Menu de ação para a seleção de gatilho][1]

Cada ação de conector ou gatilho terá seu conjunto de propriedades tooconfigure.  Você pode clicar em Olá informações botões toolearn mais informações sobre a ação ou sua documentação de referência [toolearn mais](apis-list.md).

Se você quiser toointegrate com um serviço ou a API que não é ainda um conector, você também pode estender a lógica de aplicativos por meio de um [conector personalizado](../logic-apps/logic-apps-create-api-app.md) ou simplesmente chamar diretamente toohello serviço por meio de um protocolo HTTP.

## <a name="triggers"></a>Gatilhos
Alguns conectores têm um gatilho, o que significa que um evento desse conector será acionar um lógica de aplicativo e passar em todos os dados como parte do disparador hello.  Um gatilho é sempre a primeira etapa Olá em um aplicativo de lógica.  Gatilhos populares incluem operações como:

* Recorrência — execução de hora em hora
* Quando uma solicitação HTTP é recebida
* Quando um item é adicionado a fila de tooa
* Quando um email é recebido

Alguns gatilhos acionarão Olá instantânea um evento ocorre por meio de um aplicativo de lógica de toohello de notificação e outros precisará de um intervalo de recorrência configurado na frequência hello aplicativo lógico verificará serviço Olá para um evento (para cima tooevery 15 segundos).  

Depois que um evento é recebido, Olá lógica aplicativo executar será acionado e ações Olá no fluxo de trabalho Olá serão iniciado.  Você também será capaz de tooaccess todos os dados de saudação disparam ao longo do fluxo de trabalho de saudação (para Olá exemplo 'em um tweet novo' gatilho passará Olá tweet em Olá executar).

## <a name="actions"></a>Ações
A maioria dos conectores têm uma ou várias ações que podem ser executadas como parte do fluxo de trabalho de saudação.  As ações são as etapas que ocorrem após a execução de saudação foi disparado de um disparador.  uma ação de tooadd clique Olá **nova etapa** botão e procure Olá conector que você deseja toouse.  Uma vez selecionado (e, depois de configurar qualquer [conexões](#connections) que podem ser necessárias) você verá o cartão de ação de saudação, você pode configurar.  Você pode selecionar dados de etapas anteriores clicando em qualquer um dos tokens de saudação para saídas ou insira em qualquer outra configuração conforme necessário.

![Configurando uma ação de conector][2]

## <a name="connections"></a>Conexões
A maioria dos conectores exigem tooconfigure um *conexão* antes de usar o conector de saudação.  Um *conexão* é qualquer logon ou a configuração de conexão necessária tooaccess conector de saudação.  Para os conectores que usar o OAuth, crie uma conexão significa entrar no serviço de saudação (como o Office 365, a equipe de vendas ou GitHub) onde o token de acesso pode ser criptografado e armazenado com segurança em um repositório de segredo do Azure.  Outros conectores (como FTP e SQL) exigem uma conexão que contenha configuração, como endereço do servidor, nome de usuário e senha.  Esses detalhes de configuração de conexão também são criptografados e armazenados com segurança.  Conexões serão tooaccess capaz de serviço Olá para desde que o serviço Olá permite.  Para conexões do Azure Active Directory OAuth (como o Office 365 e Dynamics) podem continuar token de acesso de saudação toorefresh indefinidamente.  Outros serviços podem estabelecer limites quanto ao tempo pelo qual podemos usar um token sem que ele seja atualizado.  De modo geral, determinadas ações, como mudar uma senha, invalidarão todos os tokens de acesso.  

As conexões podem ser exibidas e gerenciadas no Azure clicando em **Procurar** e selecionando **Conexões de API**.  Olá recursos de conexões de API, você pode exibir, editar, atualizar ou autorizar novamente quaisquer conexões que você criou.

## <a name="next-steps"></a>Próximas etapas
* [Criar seu primeiro aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md)
* [Veja os usos comuns e exemplos de aplicativos lógicos](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Introdução aos gatilhos e ações de integração corporativa](../logic-apps/logic-apps-enterprise-integration-overview.md)

<!--Image References -->
[1]: ./media/connectors-overview/addAction.png
[2]: ./media/connectors-overview/configureAction.png
