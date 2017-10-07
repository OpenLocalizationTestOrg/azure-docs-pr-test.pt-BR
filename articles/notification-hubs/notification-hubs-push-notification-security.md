---
title: "aaaSecurity Hubs de notificação"
description: "Este tópico explica a segurança para hubs de notificação do Azure."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: 6506177c-e25c-4af7-8508-a3ddca9dc07c
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: f59ad4594c2c0a2e2b22ab0b6d6bad53825a4dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="security"></a>Segurança
## <a name="overview"></a>Visão geral
Este tópico descreve o modelo de segurança de saudação de Hubs de notificação do Azure. Como os Hubs de notificação são uma entidade de barramento de serviço, eles implementam Olá mesmo modelo de segurança de barramento de serviço. Para obter mais informações, consulte Olá [autenticação do barramento de serviço](https://msdn.microsoft.com/library/azure/dn155925.aspx) tópicos.

## <a name="shared-access-signature-security-sas"></a>Segurança de assinatura de acesso compartilhado (SAS)
Os hubs de notificação implementam um esquema de segurança de nível de entidade chamado SAS (assinatura de acesso compartilhado). Esse esquema permite que mensagens toodeclare de entidades, as regras de autorização too12 nas suas descrições que concedem direitos naquela entidade.

Cada regra contém um nome, um valor de chave (segredo compartilhado) e um conjunto de direitos, conforme explicado na seção hello "Declarações de segurança". Ao criar um Hub de notificação, duas regras são automaticamente criadas: uma com direitos de escuta (que Olá usos de aplicativo do cliente) e outra com todos os direitos (que Olá usos de back-end do aplicativo).

Ao executar o gerenciamento de registros dos aplicativos cliente, se as informações de saudação enviadas por meio de notificações não for confidencial (por exemplo, atualizações de clima), um tooaccess de maneira comum um Hub de notificação é o valor da chave toogive Olá de saudação regra acesso de somente escuta toohello aplicativo cliente e valor da chave toogive Olá de saudação regra acesso completo toohello aplicativo back-end.

Não é recomendável que você inserir o valor de chave de saudação em aplicativos de cliente da Windows Store. Um tooavoid de maneira inserindo o valor de chave de saudação é toohave Olá cliente aplicativo recuperá-la de back-end de aplicativo hello na inicialização.

É importante toounderstand que Olá chave com acesso de escuta permite que um cliente tooregister do aplicativo de qualquer marca. Se seu aplicativo deve restringir os clientes do registros toospecific marcas toospecific (por exemplo, quando as marcas representam IDs de usuário), o back-end do aplicativo deve executar registros hello. Para mais informações, consulte a seção Gerenciamento de registro. Observe que dessa maneira, Olá aplicativo cliente não terá acesso direto tooNotification Hubs.

## <a name="security-claims"></a>Declarações de segurança
Entidades tooother semelhante, operações de Hub de notificação são permitidas para três declarações de segurança: escutar, enviar e gerenciar.

| Declaração | Descrição | Operações permitidas |
| --- | --- | --- |
| Escutar |Criar/atualizar, ler e excluir registros simples |Criar/Atualizar o registro<br><br>Ler registro<br><br>Ler todos os registros para um identificador<br><br>Excluir registro |
| Enviar |Enviar o hub de notificação de toohello de mensagens |Enviar mensagem |
| Gerenciar |CRUDs nos Hubs de notificação (incluindo atualização de credenciais PNS e chaves de segurança) e ler registros baseados em marcas |Criar/Atualizar/Ler/Excluir hubs de notificação<br><br>Ler registros por marca |

Hubs de notificação aceitam declarações concedidas pelos tokens de controle de acesso do Microsoft Azure e por tokens de assinatura gerados com chaves compartilhadas configuradas diretamente no Hub de notificação de saudação.

