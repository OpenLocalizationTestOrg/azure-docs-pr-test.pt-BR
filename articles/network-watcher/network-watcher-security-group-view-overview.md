---
title: "exibição de grupo de toosecurity aaaIntroduction no Inspetor de rede do Azure | Microsoft Docs"
description: "Esta página fornece uma visão geral da saudação recurso de exibição de segurança do observador de rede"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: ad27ab85-9d84-4759-b2b9-e861ef8ea8d8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: c2f6dbbffd0aedbb9db4b69d1758f2e66dd7abb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonetwork-security-group-view-in-azure-network-watcher"></a>Exibição de grupo de segurança Introdução toonetwork no Inspetor de rede do Azure

Os grupos Segurança da Rede podem ser associados no nível da sub-rede ou no nível da NIC. Quando associado em um nível de sub-rede, ele se aplica a instâncias de VM Olá tooall na sub-rede hello. Exibição de grupo de segurança de rede retorna todos os NSGs Olá configurado e regras associadas em um nível NIC e de sub-rede para uma máquina virtual fornece ideias sobre configuração de saudação. Além disso, as regras de segurança efetiva de saudação são retornadas para cada uma das NICs de saudação em uma VM. Usando a exibição Grupo de Segurança da Rede, você pode avaliar uma VM quanto às vulnerabilidades da rede, como as portas abertas. Você também pode validar se o grupo de segurança de rede está funcionando conforme o esperado com base em um [comparação entre hello configurado e Olá regras de segurança efetiva](network-watcher-nsg-auditing-powershell.md).

Um caso de uso mais estendido está em conformidade com a segurança e auditoria. Você pode definir um conjunto prescritivo de regras de segurança como um modelo de controle da segurança em sua organização. Uma auditoria periódica de conformidade pode ser implementada de forma programática, comparando regras de prescritivas Olá com regras efetivo Olá para cada uma das VMs de saudação em sua rede.

Em Olá portais regras são divididas por efetiva, sub-rede, Interface de rede e padrão. Isso fornece uma exibição simple na máquina virtual do hello regras aplicadas tooa. Um botão de download é fornecido tooeasily baixar todas as regras de segurança de hello, independentemente do guia de saudação em um arquivo CSV.

![exibição do grupo de segurança][1]

As regras podem ser selecionadas e prefixos de grupo de segurança de rede e de origem e de destino de saudação tooshow abre uma nova folha. Desta folha você pode navegar toohello recurso de grupo de segurança de rede diretamente.

![busca detalhada][2]

### <a name="next-steps"></a>Próximas etapas

Saiba como tooaudit a segurança da rede agrupar configurações visitando [configurações de grupo de segurança de rede de auditoria com o PowerShell](network-watcher-nsg-auditing-powershell.md)

[1]: ./media/network-watcher-security-group-view-overview/securitygroupview.png
[2]: ./media/network-watcher-security-group-view-overview/figure1.png









