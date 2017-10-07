---
title: "aaaHealth visão geral do monitoramento para o Gateway de aplicativo do Azure | Microsoft Docs"
description: "Saiba mais sobre Olá monitoramento de recursos no Azure Application Gateway"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7eeba328-bb2d-4d3e-bdac-7552e7900b7f
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: gwallace
ms.openlocfilehash: 5091d80394a354ff849ce7ccee8cc9d2fd0456db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-health-monitoring-overview"></a>Visão geral do monitoramento de integridade do Gateway de Aplicativo

Gateway de aplicativo do Azure por padrão monitora a integridade de saudação de todos os recursos em seu pool de back-end e automaticamente remove qualquer recurso considerado não íntegro do pool de saudação. Application Gateway continua instâncias não íntegras do toomonitor hello e os adiciona fazer toohello Íntegro pool de back-end quando estiverem disponíveis e responder toohealth testes. Gateway de aplicativo envia Olá investigações de integridade com hello mesma porta que é definida nas configurações de HTTP de back-end de saudação. Essa configuração garante que teste hello está testando Olá a mesma porta que os clientes usarão back-end do tooconnect toohello.

![exemplo de investigação de gateway de aplicativo][1]

Em adição toousing padrão investigação monitoramento de integridade, você também pode personalizar toosuit de investigação de integridade Olá requisitos do seu aplicativo. Neste artigo, serão abordadas as investigações de integridade padrão e personalizadas.

> [!NOTE]
> Se houver um NSG na sub-rede de Gateway do aplicativo, intervalos de porta 65503 65534 devem ser abertos na sub-rede de Gateway do aplicativo hello para tráfego de entrada. Essas portas são necessárias para Olá toowork de API de integridade de back-end.

## <a name="default-health-probe"></a>Investigação de integridade padrão

Um Application Gateway configura automaticamente uma investigação de integridade padrão quando você não define nenhuma configuração de investigação personalizada. Olá monitoramento de comportamento funciona fazendo que um IP de toohello de solicitação HTTP endereços configurado para o pool de back-end do hello. Para investigações de padrão se as configurações de http de back-end de saudação são configuradas para HTTPS, investigação Olá usa HTTPS como integridade bem tootest de back-ends hello.

Por exemplo: configurar o application gateway toouse servidores back-end A, B e C tooreceive HTTP tráfego de rede na porta 80. o monitoramento de integridade de padrão de saudação testa três servidores de saudação cada 30 segundos por uma resposta HTTP íntegro. Uma resposta de HTTP íntegra tem um [código de status](https://msdn.microsoft.com/library/aa287675.aspx) entre 200 e 399.

Se a verificação de investigação de padrão de saudação falhar para o servidor, o gateway de aplicativo hello remove do seu pool de back-end e interrupção do servidor toothis de fluxo de tráfego de rede. investigação de padrão de saudação ainda continua toocheck para servidor de a cada 30 segundos. Quando o servidor responde com êxito tooone solicitação de um teste de integridade padrão, ele é adicionado novamente como pool de back-end toohello íntegro e começar a tráfego fluir toohello server novamente.

### <a name="default-health-probe-settings"></a>Configurações da investigação de integridade padrão

| Propriedades da investigação | Valor | Descrição |
| --- | --- | --- |
| URL de investigação |http://127.0.0.1:\<porta\>/ |Caminho da URL |
| Intervalo |30 |Intervalo da investigação em segundos |
| Tempo limite |30 |Tempo limite da investigação em segundos |
| Limite não íntegro |3 |Contagem de repetições da investigação. servidor de back-end Hello está marcado para baixo depois contagem de falhas de investigação consecutivas Olá atinge o limite não íntegro hello. |

> [!NOTE]
> Olá porta é Olá mesma porta, como configurações de HTTP de back-end de saudação.

investigação de padrão de saudação examina somente http://127.0.0.1:\<porta\> toodetermine status de integridade. Se você precisa tooconfigure Olá integridade investigação toogo tooa URL personalizada ou modifique outras configurações, você deve usar testes personalizados conforme descrito em Olá etapas a seguir:

## <a name="custom-health-probe"></a>Investigação de integridade personalizada

Testes personalizados permitem que você toohave um controle mais granular sobre o monitoramento de integridade de saudação. Ao usar testes personalizados, você pode configurar o intervalo de sondagem Olá Olá tootest de URL e o caminho e quantos tooaccept de respostas com falha antes de marcar a instância de pool de back-end hello como não íntegro.

### <a name="custom-health-probe-settings"></a>Configurações da investigação de integridade personalizada

Olá tabela a seguir fornece definições para as propriedades de saudação de um teste de integridade personalizado.

| Propriedades da investigação | Descrição |
| --- | --- |
| Nome |Nome do teste de saudação. Esse nome é usado toorefer toohello investigação em configurações de HTTP de back-end. |
| Protocolo |Protocolo usado toosend investigação de saudação. investigação de saudação usa o protocolo de saudação definido nas configurações de HTTP de back-end de saudação |
| Host |Investigação de saudação do toosend do nome de host. Aplicável somente quando vários sites são configurados no Gateway de Aplicativo; do contrário, use '127.0.0.1'. Este valor é diferente do nome do host de VM. |
| Caminho |Caminho relativo da investigação de saudação. caminho válido Olá começa com '/'. |
| Intervalo |Intervalo de investigação em segundos. Esse valor é o intervalo de tempo de saudação entre duas investigações consecutivos. |
| Tempo limite |Tempo limite da investigação em segundos. Se uma resposta válida não for recebida dentro desse período de tempo limite, investigação hello está marcada como falha.  |
| Limite não íntegro |Contagem de repetições da investigação. servidor de back-end Hello está marcado para baixo depois contagem de falhas de investigação consecutivas Olá atinge o limite não íntegro hello. |

> [!IMPORTANT]
> Se o Gateway do aplicativo está configurado para um único site, por saudação padrão Host nome deve ser especificado como '127.0.0.1', a menos que o contrário configurada na investigação personalizada.
> Para referência uma investigação personalizada é enviada muito\<protocolo\>://\<host\>:\<porta\>\<caminho\>. Olá porta usada será Olá mesma porta, conforme definido nas configurações de HTTP de back-end de saudação.

## <a name="next-steps"></a>Próximas etapas
Depois de conhecer o monitoramento de integridade do Application Gateway, você pode configurar um [investigação de integridade personalizado](application-gateway-create-probe-portal.md) em Olá portal do Azure ou um [investigação de integridade personalizado](application-gateway-create-probe-ps.md) usando o PowerShell e hello Azure Resource Manager modelo de implantação.

[1]: ./media/application-gateway-probe-overview/appgatewayprobe.png
