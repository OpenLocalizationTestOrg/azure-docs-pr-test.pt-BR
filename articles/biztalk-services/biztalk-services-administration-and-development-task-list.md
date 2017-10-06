---
title: "aaaAdministration e lista de tarefas de desenvolvimento nos Serviços BizTalk | Microsoft Docs"
description: "Planejamento e trabalho de auxiliam na implantação dos Serviços BizTalk do Azure."
services: biztalk-services
documentationcenter: 
author: msftman
manager: erikre
editor: 
ms.assetid: 0ab70b5b-1a88-4ba5-b329-ec51b785010e
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2016
ms.author: deonhe
ms.openlocfilehash: 544c6b23fcbc2267598b713dbe1626699099d181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="administration-and-development-task-list-in-biztalk-services"></a>Lista de Tarefas de Desenvolvimento e Administração nos Serviços BizTalk   

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

## <a name="getting-started"></a>Introdução
Ao trabalhar com Serviços BizTalk do Microsoft Azure, há vários locais e tooconsider de componentes baseados em nuvem. tooget iniciado, considere Olá fluxo de processo a seguir:  

| Etapa | Quem é responsável | Tarefa | Links relacionados |
| --- | --- | --- | --- |
| 1. |Administrador |Criar hello assinatura do Microsoft Azure usando uma conta da Microsoft ou uma conta organizacional |[Portal clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885) |
| 2. |Administrador |Criar ou provisionar um Serviço BizTalk. |[Criar um Serviço BizTalk usando o Portal de clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=302280) |
| 3. |Administrador |Registrar você ou a implantação dos Serviços BizTalk da sua empresa |[Registrando e atualizando uma implantação do serviço BizTalk no hello Portal de Serviços BizTalk](https://msdn.microsoft.com/library/azure/hh689837.aspx) |
| 4. |Administrador |Se aplicará se o aplicativo hello usa o sistema de linha de negócios (LOB) do serviço de adaptador BizTalk tooconnect tooan local ou usa uma fila ou tópico de destino.  Crie hello Namespace de barramento de serviço do Azure. Dê esse namespace, o nome do emissor de barramento de serviço e o desenvolvedor de toohello de valores de chave do emissor de barramento de serviço. |[Como criar ou modificar um namespace do Barramento de Serviço](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md) e [Como obter os valores de Nome do Emissor e Chave do Emissor](biztalk-issuer-name-issuer-key.md) |
| 5. |Desenvolvedores |Instale Olá SDK e crie Olá projeto BizTalk Service no Visual Studio. |[Instalar o SDK dos Serviços BizTalk do Azure](https://msdn.microsoft.com/library/azure/hh689760.aspx) e [Criar pontos de extremidade de mensagens avançadas no Azure](https://msdn.microsoft.com/library/azure/hh689766.aspx) |
| 6. |Desenvolvedores |Implante o tooyour de projeto do BizTalk Service que BizTalk Service hospedado no Azure. |[Implantando e atualizando Olá projeto dos Serviços BizTalk](https://msdn.microsoft.com/library/azure/hh689881.aspx) |
| 7. |Administrador |Aplica-se se estiver usando o Eclipse:  Você pode adicionar parceiros e criar acordos no hello Portal de Serviços BizTalk do Microsoft Azure. Quando você cria um contrato, você pode adicionar ponte hello e/ou transformações criadas pelas configurações de contrato de toohello Olá developer. |[Configurando EDI, AS2 e EDIFACT no Portal de Serviços BizTalk](https://msdn.microsoft.com/library/azure/hh689853.aspx) |
| 8. |Administrador |Usando Olá Portal clássico do Azure, monitore a integridade de saudação do seu BizTalk Service, incluindo métricas de desempenho. |[Serviços BizTalk: guias Painel, Monitor e Escala](http://go.microsoft.com/fwlink/p/?LinkID=302281) |
| 9. |Administrador |Usando o hello Portal de Serviços BizTalk do Microsoft Azure, gerencie artefatos Olá usados por serviços BizTalk e rastrear mensagens enquanto são processadas pelos arquivos de ponte de saudação. |[Usando Olá Portal de Serviços BizTalk](https://msdn.microsoft.com/library/azure/dn874043.aspx) |
| 10. |Administrador |Crie tooback um plano de backup a saudação BizTalk Service. |[Continuidade de Negócios e Recuperação de Desastres nos Serviços BizTalk](https://msdn.microsoft.com/library/azure/dn509557.aspx) |

## <a name="next-steps"></a>Próximas etapas
[Tutoriais e Amostras](https://msdn.microsoft.com/library/azure/hh689895.aspx)

[Criar projeto Olá no Visual Studio](https://msdn.microsoft.com/library/azure/hh689811.aspx)

[Instalar o SDK dos Serviços BizTalk do Azure](https://msdn.microsoft.com/library/azure/hh689760.aspx)

## <a name="concepts"></a>Conceitos
[Criar projeto Olá no Visual Studio](https://msdn.microsoft.com/library/azure/hh689811.aspx)  
[EDI, AS2 e EDIFACT (Business tooBusiness) do sistema de mensagens](https://msdn.microsoft.com/library/azure/hh689898.aspx)  

## <a name="other-resources"></a>Outros recursos
[Adicionar pontos de extremidade de mensagens de origem, de destino e de ponte](https://msdn.microsoft.com/library/azure/hh689877.aspx)  
[Aprender e criar mapas de mensagem e transformações](https://msdn.microsoft.com/library/azure/hh689905.aspx)  
[Usando Olá serviço de adaptador do BizTalk (BAS)](https://msdn.microsoft.com/library/azure/hh689889.aspx)  
[Serviços BizTalk do Azure](http://go.microsoft.com/fwlink/p/?LinkID=303664)

