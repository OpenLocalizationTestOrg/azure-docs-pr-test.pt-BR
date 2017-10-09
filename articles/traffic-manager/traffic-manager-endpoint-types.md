---
title: Tipos de ponto de extremidade do Gerenciador de aaaTraffic | Microsoft Docs
description: "Este artigo explica os diferentes tipos de pontos de extremidade que podem ser usados com o Gerenciador de Tráfego do Azure"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 4e506986-f78d-41d1-becf-56c8516e4d21
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/29/2017
ms.author: kumud
ms.openlocfilehash: 787412ac6207f76791bf3ff753d1df2767b1a964
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-endpoints"></a>Pontos de extremidade do Gerenciador de Tráfego
Microsoft Azure Traffic Manager permite toocontrol como o tráfego de rede é distribuída tooapplication implantações em execução em datacenters diferentes. Você configurar cada implantação de aplicativo como um “ponto de extremidade” no Gerenciador de Tráfego. Quando o Traffic Manager recebe uma solicitação DNS, ele escolhe tooreturn um ponto de extremidade disponíveis no hello resposta DNS. Gerenciador de tráfego baseia escolha Olá no status atual de ponto de extremidade hello e método de roteamento de tráfego hello. Para obter mais informações, consulte [Como o Gerenciador de Tráfego Funciona](traffic-manager-how-traffic-manager-works.md).

Há três tipos de ponto de extremidade suportados pelo Gerenciador de Tráfego:
* **pontos de extremidade do Azure** são usados para os serviços hospedados no Azure.
* **pontos de extremidade externos** são usados para os serviços hospedados fora do Azure, no local ou com um provedor de hospedagem diferente.
* **Aninhados pontos de extremidade** é toocreate de perfis do Gerenciador de tráfego toocombine usado mais flexível roteamento de tráfego esquemas toosupport Olá necessidades de implantações maiores e mais complexas.

Não há nenhuma restrição sobre como os pontos de extremidade de diferentes tipos são combinados em um único perfil do Gerenciador de Tráfego. Cada perfil pode conter qualquer combinação de tipos de ponto de extremidade.

Olá seções a seguir descreve cada tipo de ponto de extremidade em mais detalhes.

## <a name="azure-endpoints"></a>pontos de extremidade do Azure

Os pontos de extremidade do Azure são usados para serviços baseados no Azure no Gerenciador de Tráfego. Olá seguintes tipos de recursos do Azure têm suporte:

* VMs IaaS “Clássicas” e serviços de nuvem PaaS.
* Aplicativos Web
* Recursos de PublicIPAddress (que podem ser tooVMs conectado diretamente ou por meio de um balanceador de carga do Azure). Olá publicIpAddress deve ter um nome DNS atribuído toobe usada em um perfil do Gerenciador de tráfego.

Os recursos de PublicIPAddress são recursos do Azure Resource Manager. Eles não existem no modelo de implantação clássico hello. Assim, eles têm suporte apenas em experiências do Azure Resource Manager do Gerenciador de Tráfego. Olá outros tipos de ponto de extremidade têm suporte por meio do Gerenciador de recursos e hello modelo de implantação clássico.

Ao usar os pontos de extremidade do Azure, o Gerenciador de Tráfego detecta quando uma VM IaaS “Clássica”, serviço de nuvem ou Aplicativo Web é interrompido e iniciado. Esse status é refletido no status do ponto de extremidade de saudação. Consulte detalhes em [Monitoramento do ponto de extremidade do Gerenciador de Tráfego](traffic-manager-monitoring.md#endpoint-and-profile-status). Quando Olá serviço subjacente é interrompido, Gerenciador de tráfego não executa verificações de integridade do ponto de extremidade ou ponto de extremidade de toohello de tráfego direto. Nenhum Gerenciador de tráfego de cobrança eventos ocorrem para Olá interrompeu a instância. Quando o serviço Olá for reiniciado, cobrança currículos e ponto de extremidade de saudação é elegível tooreceive tráfego. Essa detecção não se aplica a pontos de extremidade de tooPublicIpAddress.

## <a name="external-endpoints"></a>pontos de extremidade externos

Pontos de extremidade externos são usados para serviços fora do Azure. Por exemplo, um serviço hospedado localmente ou com um provedor diferente. Pontos de extremidade externos podem ser usados individualmente ou combinados com pontos de extremidade do Azure em Olá mesmo perfil do Gerenciador de tráfego. Combinar pontos de extremidade do Azure com pontos de extremidade Externos permite vários cenários:

* Em um modelo de failover ativo-ativo ou ativo-passivo, use o Azure tooprovide aumentado redundância para um aplicativo local existente.
* tooreduce latência do aplicativo para usuários em todo o mundo hello, estender uma existente no local aplicativo tooadditional localizações geográficas no Azure. Para obter mais informações, consulte [Roteamento de tráfego por “Desempenho” do Gerenciador de Tráfego](traffic-manager-routing-methods.md#performance).
* Use a capacidade adicional tooprovide do Azure para um aplicativo local existente, continuamente ou como um toomeet 'Expandir para nuvem' solução um aumento na demanda.

Em alguns casos, é útil toouse tooreference de pontos de extremidade externos do Azure services (para obter exemplos, consulte Olá [perguntas frequentes sobre](traffic-manager-faqs.md#traffic-manager-endpoints)). Nesse caso, verificações de integridade são cobradas na taxa de pontos de extremidade do Azure hello, taxa de pontos de extremidade externos Olá não. No entanto, ao contrário de pontos de extremidade do Azure, se você interromper ou excluir Olá subjacente de serviço, verificação de integridade cobrança continua até que você desabilitar ou excluir o ponto de extremidade Olá no Gerenciador de tráfego.

## <a name="nested-endpoints"></a>pontos de extremidade aninhados

Pontos de extremidade aninhados combinam vários Traffic Manager perfis toocreate flexível roteamento de tráfego esquemas e dar suporte às necessidades de saudação de implantações maiores e complexas. Com pontos de extremidade aninhadas, um perfil de 'child' é adicionado como um perfil do ponto de extremidade tooa 'parent'. Ambos os perfis de pai e filho Olá podem conter outros pontos de extremidade de qualquer tipo, incluindo outros perfis aninhados. Para obter mais informações, consulte [perfis aninhados do Gerenciador de Tráfego](traffic-manager-nested-profiles.md).

## <a name="web-apps-as-endpoints"></a>Aplicativos Web como pontos de extremidade

Algumas considerações adicionais se aplicam ao configurar os Aplicativos Web como pontos de extremidade no Gerenciador de Tráfego:

1. Somente os aplicativos Web hello SKU 'Padrão' ou acima são elegíveis para uso com o Gerenciador de tráfego. Tentativas de tooadd um aplicativo Web de uma falha SKU inferior. Fazendo downgrade Olá SKU de um aplicativo Web existente resulta no Gerenciador de tráfego não enviar tráfego toothat aplicativo Web.
2. Quando um ponto de extremidade recebe uma solicitação HTTP, ele usa Olá 'host' Cabeçalho Olá solicitação toodetermine qual aplicativo Web deve solicitar saudação do serviço. cabeçalho de host Olá contém Olá DNS nome usado tooinitiate Olá solicitação, por exemplo 'contosoapp.azurewebsites.net'. toouse um nome DNS diferente com o aplicativo Web, o nome DNS de saudação deve ser registrado como um nome de domínio personalizado para Olá aplicativo. Ao adicionar um ponto de extremidade do aplicativo Web como um ponto de extremidade do Azure, o nome DNS de perfil do Gerenciador de tráfego Olá é registrado automaticamente para Olá aplicativo. Esse registro é removido automaticamente quando o ponto de extremidade de saudação é excluído.
3. Cada perfil do Gerenciador de Tráfego pode ter, no máximo, um ponto de extremidade do aplicativo Web de cada região do Azure. toowork ao redor para que essa restrição, você pode configurar um aplicativo Web como um ponto de extremidade externo. Para obter mais informações, consulte Olá [perguntas frequentes sobre](traffic-manager-faqs.md#traffic-manager-endpoints).

## <a name="enabling-and-disabling-endpoints"></a>Habilitando e desabilitando os pontos de extremidade

Desabilitar um ponto de extremidade no Traffic Manager pode ser útil tootemporarily remover tráfego de um ponto de extremidade que esteja no modo de manutenção ou que esteja sendo reimplantado. Ponto de extremidade de saudação é executado novamente, ele poderá ser habilitado novamente.

Pontos de extremidade podem ser habilitados e desabilitados por meio do portal de Gerenciador de tráfego hello, PowerShell, CLI ou API REST, que têm suporte no Gerenciador de recursos e o modelo de implantação clássico hello.

> [!NOTE]
> Desabilitar um ponto de extremidade do Azure não tem nada toodo com seu estado de implantação no Azure. Um Azure serviço (como uma VM ou um aplicativo Web permanece em execução e é capaz de tráfego de tooreceive, mesmo quando desabilitado no Traffic Manager. Tráfego pode ser resolvido diretamente toohello instância do serviço em vez de por meio de saudação do Traffic Manager nome DNS do perfil. Para obter mais informações, consulte [como o Gerenciador de Tráfego funciona](traffic-manager-how-traffic-manager-works.md).

qualificação atual de saudação do tráfego de tooreceive cada ponto de extremidade depende Olá fatores a seguir:

* status do perfil Hello (ativado/desativado)
* status de ponto de extremidade da saudação (ativado/desativado)
* resultados de Olá Olá de verificações de integridade para esse ponto de extremidade

Para obter detalhes, consulte [Monitoramento do ponto de extremidade do Gerenciador de Tráfego](traffic-manager-monitoring.md#endpoint-and-profile-status).

> [!NOTE]
> Como o Traffic Manager funciona no nível DNS de saudação, é endpoint de tooany conexões existentes tooinfluence não é possível. Quando um ponto de extremidade não estiver disponível, o Traffic Manager direciona novas conexões tooanother ponto de extremidade disponível. No entanto, o host Olá atrás Olá desabilitado ou ponto de extremidade Íntegro pode continuar tooreceive tráfego por meio de conexões existentes até essas sessões são encerradas. Aplicativos limite Olá sessão duração tooallow tráfego toodrain de conexões existentes.

Se todos os pontos de extremidade em um perfil são desabilitados ou se o próprio perfil de saudação é desabilitado, o Traffic Manager envia uma 'NXDOMAIN' resposta tooa nova consulta DNS.


## <a name="next-steps"></a>Próximas etapas

* Saiba [como funciona o Gerenciador de Tráfego](traffic-manager-how-traffic-manager-works.md).
* Saiba mais sobre [o monitoramento de ponto de extremidade e failover automático](traffic-manager-monitoring.md)do Gerenciador de Tráfego.
* Saiba mais sobre os [métodos de roteamento de tráfego](traffic-manager-routing-methods.md)do Gerenciador de Tráfego.
