---
title: aaaIntroduction tooAzure Application Gateway | Microsoft Docs
description: "Esta página fornece uma visão geral do serviço do Application Gateway Olá para balanceamento de carga de camada 7, incluindo os tamanhos de gateway, a afinidade de sessão baseado em cookie, balanceamento de carga de HTTP e descarregamento de SSL."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: b37a2473-4f0e-496b-95e7-c0594e96f83e
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: c40c9dba64ab03d9f6f81b3cb8f26c6562ac26c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-application-gateway"></a>Visão geral do Gateway de Aplicativo

O Gateway de Aplicativo do Microsoft Azure é uma solução de virtualização dedicada que fornece um ADC (controlador de entrega de aplicativos) como um serviço. Ele oferece vários recursos de balanceamento de carga de camada 7 ao seu aplicativo. Ele permite que os clientes produtividade de farm da web toooptimize descarregando CPU intensa SSL encerramento toohello gateway de aplicativo. Ele também fornece outros recursos de roteamento de camada 7 incluindo rodízio distribuição de tráfego de entrada, a afinidade de sessão baseada em cookie, roteamento baseado no caminho de URL e Olá capacidade toohost vários sites por trás de um único Gateway de aplicativo. Um firewall do aplicativo web (WAF) também é fornecido como parte do gateway de aplicativo hello WAF SKU. Ele oferece proteção tooweb aplicativos comuns de vulnerabilidades de web e explorações. O Gateway de Aplicativo pode ser configurado como um gateway voltado para a Internet, um gateway apenas interno ou uma combinação de ambos. 

![cenário](./media/application-gateway-introduction/scenario.png)

## <a name="features"></a>Recursos

Application Gateway fornece atualmente Olá recursos a seguir:


* **[Firewall do aplicativo Web](application-gateway-webapplicationfirewall-overview.md)**  -firewall do aplicativo web hello (WAF) no Gateway de aplicativo do Azure protege os aplicativos da web comuns ataques baseados na web como injeção de SQL, ataques de script entre sites e sequestros de sessão.
* **Balanceamento de carga HTTP** - o Gateway de Aplicativo fornece balanceamento de carga round robin. O balanceamento de carga é feito na camada 7 e é usado somente para o tráfego HTTP(S).
* **Afinidade de sessão baseada em cookie** -recurso de afinidade de sessão baseada em cookie Olá é útil quando você deseja tookeep uma sessão de usuário em Olá mesmo back-end. Gerenciado pelo gateway cookies, Olá Application Gateway é toodirect capaz de tráfego de subsequentes de um toohello de sessão de usuário mesmo back-end para processamento. Esse recurso é importante em casos onde o estado da sessão é salvo localmente no servidor de back-end Olá para uma sessão de usuário.
* **[Descarregamento de SSL (Sockets Layer) segura](application-gateway-ssl-arm.md)**  -esse recurso se a tarefa cara Olá de descriptografar o tráfego HTTPS longe dos seus servidores web. Por Olá Finalizando a conexão SSL no hello Application Gateway e Olá solicitação toohello servidor descriptografado de encaminhamento, servidor de web hello é unburdened por descriptografia.  Application Gateway criptografa novamente resposta Olá antes de enviá-lo voltar toohello cliente. Esse recurso é útil em cenários onde Olá back-end está localizado em Olá mesmo protegidos rede virtual como Olá Application Gateway no Azure.
* **[Encerrar tooEnd SSL](application-gateway-backend-ssl.md)**  -suporta Application Gateway terminar tooend criptografia de tráfego. Application Gateway faz isso encerrando a conexão de SSL Olá no gateway do aplicativo hello. gateway de Hello, em seguida, aplica regras de roteamento de saudação toohello tráfego, criptografa novamente o pacote de saudação e encaminha Olá pacote toohello apropriado back-end com base nas regras de roteamento Olá definidas. Qualquer resposta do servidor de web hello atravessa Olá mesmo processo toohello back end usuário.
* **[Roteamento de conteúdo baseado em URL](application-gateway-url-route-overview.md)**  -esse recurso fornece a capacidade de saudação toouse diferentes servidores de back-end para o tráfego diferente. O tráfego para uma pasta no servidor de web hello, ou para uma CDN pode ser roteado tooa diferentes back-end. Esse recurso reduz a carga desnecessária em back-ends que não atende a um conteúdo específico.
* **[Roteamento de múltiplos sites](application-gateway-multi-site-overview.md)**  -Application gateway permite que você tooconsolidate backup too20 sites em um gateway de aplicativo único.
* **[Suporte para WebSocket](application-gateway-websocket.md)**  -outro grande recurso do Application Gateway é o suporte nativo a saudação Websocket.
* **[Monitoramento de integridade](application-gateway-probe-overview.md)**  -Application gateway fornece sondas de integridade padrão personalizada e monitoramento de recursos de back-end toomonitor para cenários mais específicos.
* **[Política de SSL e codificações](application-gateway-ssl-policy-overview.md)**  - esse recurso fornece a capacidade de saudação as versões do protocolo SSL toolimit hello e Olá codificações pacotes que têm suporte e Olá a ordem na qual eles são processados.
* **[Solicitação de redirecionamento](application-gateway-redirect-overview.md)**  -este recurso fornece um ouvinte HTTPS de tooan Olá recurso tooredirect HTTP solicitações.
* **[Suporte de back-end multilocatário](application-gateway-web-app-overview.md)** - O gateway de aplicativo dá suporte à configuração de serviços de back-end multilocatários, como Aplicativos Web do Azure e Gateway de API, como membros do pool de back-ends. 
* **[Diagnóstico avançado](application-gateway-diagnostics.md)** – o Gateway de Aplicativo fornece logs de diagnóstico e acesso completos. Logs do firewall estão disponíveis para recursos de gateway de aplicativo que têm o WAF habilitado.

## <a name="benefits"></a>Benefícios

O Gateway de Aplicativo é útil para:

* Aplicativos que necessitam de solicitações de saudação mesmo tooreach de sessão de usuário/cliente Olá mesma máquina virtual de back-end. Exemplos desses aplicativos são os aplicativos de carrinho de compras e servidores de email na Web.
* Remoção da sobrecarga de terminação SSL para farms de servidores Web.
* Aplicativos, como uma rede de fornecimento de conteúdo, que requer várias solicitações HTTP na Olá mesmo toobe de conexão TCP de longa execução roteadas ou servidores de back-end toodifferent com balanceamento de carga.
* Aplicativos que oferecem suporte a tráfego websocket
* Proteger aplicativos Web contra ataques comuns baseados na Web, como injeção SQL, ataques de script entre sites e sequestros de sessão.
* Distribuição lógica de tráfego com base em critérios de roteamentos diferentes como caminho de url ou cabeçalhos de domínio.

O Gateway de Aplicativo é totalmente gerenciado pelo Azure, escalonável e altamente disponível. Ele fornece um conjunto avançado de recursos de log e diagnósticos para melhor capacidade de gerenciamento. Quando você cria um gateway de aplicativo, um ponto de extremidade (VIP público ou IP ILB interno) é usado e associado para tráfego de rede de entrada. Este VIP ou ILB IP é fornecido pelo Balanceador de carga do Azure, trabalhando no nível de transporte da saudação (TCP/UDP) e ter todos os tráfego de rede que está sendo carga toohello balanceada application gateway instâncias de trabalho. Olá gateway de aplicativo e rotas Olá tráfego HTTP/HTTPS baseado em sua configuração se ela é uma máquina virtual, serviço de nuvem, interno ou um endereço IP externo.

Application Gateway balanceamento de carga como um serviço gerenciado do Azure permite Olá provisionamento de um balanceador de carga de camada 7 por trás do balanceador de carga de software do Azure hello. Gerenciador de tráfego pode ser usado toocomplete cenário de saudação visto Olá após a imagem, onde o Traffic Manager fornece redirecionamento e a disponibilidade de tráfego toomultiple recursos de gateway de aplicativos em regiões diferentes, enquanto o gateway do aplicativo fornece entre o balanceamento de carga de camada 7 da região. Um exemplo desse cenário pode ser encontrado em: [serviços em nuvem do Azure de saudação de balanceamento de carga de uso](../traffic-manager/traffic-manager-load-balancing-azure.md)

![cenário do Gerenciador de Tráfego e do Gateway de Aplicativo](./media/application-gateway-introduction/tm-lb-ag-scenario.png)

[!INCLUDE [load-balancer-compare-tm-ag-lb-include.md](../../includes/load-balancer-compare-tm-ag-lb-include.md)]

## <a name="gateway-sizes-and-instances"></a>Instâncias e tamanhos de gateway

O Gateway de Aplicativo atualmente é oferecido em três tamanhos: **Pequeno**, **Médio** e **Grande**. Os tamanhos de instância pequenos são destinados a cenários de desenvolvimento e teste.

Você pode criar até too50 application gateways por assinatura, e cada gateway do aplicativo pode ter até too10 instâncias. Cada gateway de aplicativo pode consistir em 20 ouvintes http. Para obter uma lista completa de limites do gateway de aplicativo, consulte [Limites de serviço do Gateway de Aplicativo](../azure-subscription-service-limits.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#application-gateway-limits).

Olá, a tabela a seguir mostra uma taxa de transferência de desempenho médio para cada instância de gateway do aplicativo com o descarregamento SSL habilitado:

| Resposta de página de back-end | Pequena | Média | Grande |
| --- | --- | --- | --- |
| 6 mil |7,5 Mbps |13 Mbps |50 Mbps |
| 100K |35 Mbps |100 Mbps |200 Mbps |

> [!NOTE]
> Esses valores são valores aproximados para uma produtividade do Gateway de Aplicativo. taxa de transferência real Olá depende de diversos detalhes de ambiente, como tamanho de página média de instâncias de back-end e tooserve de tempo de processamento de uma página. Para obter números de desempenho exatos, você deve executar seus próprios testes. Esses valores são fornecidos apenas para a orientação do planejamento de capacidade.

## <a name="health-monitoring"></a>Monitoramento da integridade

Gateway de aplicativo do Azure automaticamente monitora a integridade de saudação de instâncias de back-end Olá por meio de investigações de integridade básica ou personalizada. Usando testes de integridade, garante que hospeda apenas íntegra responde tootraffic. Para saber mais, consulte a [Visão geral do monitoramento de integridade do Gateway de Aplicativo](application-gateway-probe-overview.md).

## <a name="configuring-and-managing"></a>Configurando e gerenciando

Para seu ponto de extremidade, o gateway de aplicativo pode ter um IP público, um IP privado ou ambos, quando é configurado. O Gateway de Aplicativo é configurado em uma rede virtual na sua própria sub-rede. sub-rede Olá criados ou usados para o application gateway não pode conter todos os tipos de recursos, Olá somente os recursos que são permitidos na sub-rede Olá são os gateways de outros aplicativos. toosecure seus recursos de back-end, servidores de back-end Olá podem estar contidos em uma sub-rede diferente no hello mesma rede virtual que o gateway de aplicativo hello. Esta sub-rede, que ele não é necessário para aplicativos de back-end de saudação. Como gateway de aplicativo hello pode alcançar o endereço de ip hello, gateway do aplicativo é tooprovide capaz de recursos de ADC para servidores de back-end de saudação. 

É possível criar e gerenciar um gateway de aplicativo usando as APIs REST, os cmdlets do PowerShell, a CLI do Azure ou o [portal do Azure](https://portal.azure.com/). Para outras perguntas no Application gateway visite [perguntas frequentes sobre o Application Gateway](application-gateway-faq.md) perguntas frequentes sobre o tooview uma lista de comuns.

## <a name="pricing"></a>Preços

Preço tem base nos encargos por hora da instância do gateway e nos encargos de processamento de dados. Por hora são diferente de encargos de SKU padrão gateway preços para Olá WAF SKU. Encontre essas informações sobre preços em [Detalhes de preço do Gateway de Aplicativo](https://azure.microsoft.com/pricing/details/application-gateway/). Processamento de dados permaneçam encargos Olá mesmo.

## <a name="faq"></a>Perguntas frequentes

Para perguntas frequentes sobre o Gateway de Aplicativo, consulte [Perguntas frequentes do Gateway de Aplicativo](application-gateway-faq.md).

## <a name="next-steps"></a>Próximas etapas

Depois de aprendizado sobre o gateway de aplicativo, você pode [criar um application gateway](application-gateway-create-gateway-portal.md) ou você pode [criar um application gateway descarregamento de SSL](application-gateway-ssl-arm.md) conexões HTTPS de saldo de tooload.

toolearn como toocreate um application gateway usando a URL de roteamento baseado em conteúdo, vá muito[criar um gateway de aplicativo usando roteamento baseado em URL](application-gateway-create-url-route-arm-ps.md) para obter mais informações.

toolearn sobre alguns dos Olá outra chave de rede de recursos do Azure, consulte [rede Azure](../networking/networking-overview.md).
