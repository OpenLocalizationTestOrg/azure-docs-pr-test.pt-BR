---
title: "aaaOverview de multilocatário back termina com o Gateway de aplicativo do Azure | Microsoft Docs"
description: "Esta página fornece uma visão geral do suporte do Application Gateway Olá para vários locatários back-ends."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: b7da8c9c68e34bd83ad2b828fab62c00caea354a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-support-for-multi-tenant-back-ends"></a>O Gateway de Aplicativo dá suporte a back-ends com vários locatários

O Gateway de Aplicativo do Azure dá suporte a conjuntos de dimensionamento de máquina virtual, adaptadores de rede, IPs públicos/privados ou FQDN (nomes de domínio totalmente qualificados) como parte de seus pools de back-end. Por padrão, gateway do aplicativo não altera cabeçalho de host HTTP entrado hello de cliente hello e envia Olá back-end toohello inalterado de cabeçalho. Há muitos serviços como [aplicativos Web do Azure](../app-service-web/app-service-web-overview.md) e [gerenciamento de API](../api-management/api-management-key-concepts.md) que são multilocatário por natureza e contam com um cabeçalho de host específico ou SNI extensão tooresolve toohello ponto de extremidade correto. Application Gateway agora oferece suporte a capacidade de saudação para usuários toooverwrite Olá entrado cabeçalho de host HTTP com base nas configurações de back-end HTTP hello. Esse recurso habilita o suporte a Aplicativos Web do Azure e ao Gerenciamento de APIs com back-ends com vários locatários. Esse recurso está disponível para o saudação padrão e WAF SKU. Multilocatário back-end suporte também funciona com cenários SSL de tooend de encerramento e de término SSL.

![cenário de aplicativo Web](./media/application-gateway-web-app-overview/scenario.png)

Olá capacidade toospecify uma substituição de host está definida no hello configurações HTTP e pode ser aplicado tooany volta terminar pool durante a criação da regra. Multilocatário volta termina Olá suporte a dois modos de substituição de cabeçalho de host e extensão SNI a seguir.

1. Olá capacidade tooset Olá host nome tooa fixa valor Olá configurações de HTTP. Esse recurso garante que esse cabeçalho de host Olá é substituído toothis valor para todo pool de back-end do toohello tráfego em que são aplicadas as configurações de saudação HTTP. Ao usar final tooend SSL, esse nome de host substituído é usado em Olá extensão SNI. Esse recurso habilita cenários onde um farm de pool de back-end espera um cabeçalho de host que é diferente do cabeçalho de host de cliente de entrada hello.

2. Olá capacidade tooderive Olá nome do host da saudação IP ou FQDN de membros do pool de back-end de saudação. Configurações HTTP também fornecem um nome de host opção toopick Olá do FQDN de um membro pool de back-end se configurado com o nome de host do hello opção tooderive de um membro do pool de back-end individuais. Ao usar final tooend SSL, esse nome de host é derivado do hello FQDN e é usado em Olá extensão SNI. Esse recurso permite cenários em que um pool de back-end pode ter dois ou mais serviços de PaaS multilocatários como aplicativos web do Azure e membro de tooeach de cabeçalho de host da solicitação Olá contém o nome do host de saudação derivado de seu FQDN.

> [!NOTE]
> Em ambos Olá anterior casos Olá só afetam comportamento de tráfego ao vivo hello e não Olá comportamento de investigação de integridade. Personalizado já testes suporte Olá capacidade toospecify um cabeçalho de host na configuração de investigação de saudação. Testes personalizados também dão suporte a saudação capacidade tooderive Olá host cabeçalho comportamento das configurações de HTTP de saudação configurada no momento. Essa configuração pode ser especificada usando Olá `PickHostNameFromback endAddress` parâmetro na configuração de investigação de saudação. Para final tooend funcionalidade toowork, investigação hello e configurações de HTTP Olá devem ser configuração correta de saudação tooreflect modificado.

Com essa funcionalidade, os clientes especificar opções Olá nas configurações de HTTP hello e personalizadas sondas de configuração apropriado toohello. Essa configuração está ligada, em seguida, tooa ouvinte e um back end pool, usando uma regra.

## <a name="next-steps"></a>Próximas etapas

Saiba como tooset a um gateway de aplicativo com um aplicativo da web como um back end membro do pool visitando: [aplicativos da web de configurar o serviço de aplicativo com o Application Gateway](application-gateway-web-app-powershell.md)
