---
title: Perguntas frequentes sobre o DNS de aaaAzure | Microsoft Docs
description: Perguntas frequentes sobre o DNS do Azure
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: jonatul
ms.openlocfilehash: 55006e9d8b311f1e94678eb9d35ce3448b936488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-faq"></a>Perguntas frequentes do DNS do Azure

## <a name="about-azure-dns"></a>Sobre o DNS do Azure

### <a name="what-is-azure-dns"></a>O que é o DNS do Azure?

Olá, sistema de nomes de domínio ou DNS, é responsável pela conversão (ou seja, resolver) um site ou serviço name tooits endereço IP. O DNS do Azure é um serviço de hospedagem para domínios DNS, fornecendo resolução de nomes usando a infraestrutura do Microsoft Azure. Ao hospedar seus domínios no Azure, você pode gerenciar seu DNS registros usando Olá mesmo credenciais, APIs, ferramentas e cobrança como outros serviços do Azure.

Domínios DNS no DNS do Azure são hospedados na rede global do Azure de servidores de nomes DNS. Usamos a difusão de rede para que cada consulta DNS for atendida, o servidor DNS mais próximo disponível para o hello. Isso fornece desempenho rápido e alta disponibilidade para seu domínio.

Olá serviço DNS do Azure é baseada no Gerenciador de recursos do Azure. Sendo assim, ele aproveita recursos do Resource Manager, como o controle de acesso baseado em função, os logs de auditoria e o bloqueio de recursos. Seus domínios e registros podem ser gerenciados por meio de saudação portal do Azure, cmdlets do PowerShell do Azure, em Olá CLI do Azure de plataforma cruzada. Aplicativos que exigem o gerenciamento automático de DNS podem integrar saudação do serviço por meio de saudação API REST e SDKs.

### <a name="how-much-does-azure-dns-cost"></a>Quanto custa o DNS do Azure?

modelo de cobrança de DNS do Azure Olá é com base no número de saudação de zonas DNS hospedadas no DNS do Azure e o número de saudação de recebem as consultas DNS. Descontos são fornecidos com base no uso.

Para obter mais informações, consulte Olá [DNS do Azure página de preços](https://azure.microsoft.com/pricing/details/dns/).

### <a name="what-is-hello-sla-for-azure-dns"></a>O que é o SLA de saudação do DNS do Azure?

Podemos garantir que as solicitações de DNS válidas receberá uma resposta pelo menos um servidor de nome DNS do Azure pelo menos 99,99% de tempo de saudação.

Para obter mais informações, consulte Olá [página de SLA do Azure DNS](https://azure.microsoft.com/support/legal/sla/dns).

### <a name="what-is-a-dns-zone-is-it-hello-same-as-a-dns-domain"></a>O que é uma 'zona DNS'? É-Olá mesmo como um domínio DNS? 

Um domínio é um nome exclusivo no sistema de nomes de domínio hello, por exemplo 'contoso.com'.

Uma zona DNS é usado toohost Olá registros DNS para um domínio específico. Por exemplo, domínio Olá 'contoso.com' pode conter vários registros DNS, como mail.contoso.com (para um servidor de email) e www.contoso.com (para um site da web). Esses seriam hospedados na zona DNS hello "contoso.com".

Um nome de domínio é *apenas um nome de*, enquanto uma zona DNS é um recurso de dados que contém os registros DNS Olá para um nome de domínio. DNS do Azure permite que você toohost uma zona DNS e gerenciar registros DNS Olá para um domínio no Azure. Ele também fornece servidores de nome DNS tooanswer as consultas DNS de saudação à Internet.

### <a name="do-i-need-toopurchase-a-dns-domain-name-toouse-azure-dns"></a>É necessário toopurchase um toouse de nome de domínio DNS do Azure DNS? 

Não necessariamente.

Não é necessário toopurchase toohost um domínio uma zona DNS no DNS do Azure. Você pode criar uma zona DNS a qualquer momento sem possui o nome de domínio de saudação. Consultas DNS para esta zona serão resolvido somente se eles são direcionados a servidores de nome DNS do Azure toohello atribuído toohello zona.

É necessário nome de domínio Olá toopurchase se você quiser toolink a zona DNS para a hierarquia de DNS global hello – Isso permite que o DNS a consultas de qualquer lugar no hello world toofind a zona DNS e respondido com seus registros DNS.

## <a name="azure-dns-features"></a>Recursos do DNS do Azure

### <a name="does-azure-dns-support-dns-based-traffic-routing-or-endpoint-failover"></a>O DNS do Azure dá suporte a roteamento de tráfego com base em DNS ou failover de ponto de extremidade?

O roteamento de tráfego com base em DNS e o failover de ponto de extremidade são fornecidos pelo Gerenciador de Tráfego do Azure. Isso é um serviço do Azure separado que pode ser usado junto com o DNS do Azure. Para obter mais informações, consulte Olá [visão geral do Gerenciador de tráfego](../traffic-manager/traffic-manager-overview.md).

DNS do Azure oferece suporte somente à hospedagem 'static' domínios DNS, onde cada consulta DNS para um determinado registro DNS sempre recebe a saudação mesma resposta DNS.

### <a name="does-azure-dns-support-domain-name-registration"></a>O DNS do Azure dá suporte ao registro de nome de domínio?

Não. O DNS do Azure não dá suporte a compra de nomes de domínio. Se você quiser toopurchase domínios, é necessário toouse um registrador de nomes de domínio de terceiro. registrador Olá normalmente cobra uma pequena taxa anual. domínios Olá, em seguida, podem ser hospedados no Azure DNS para o gerenciamento de registros de DNS. Consulte [delegar tooAzure um domínio DNS](dns-domain-delegation.md) para obter detalhes.

Esse é um recurso que estamos acompanhando em nossa lista de pendências. Você pode usar nosso site de feedback muito[registrar seu suporte para esse recurso](https://feedback.azure.com/forums/217313-networking/suggestions/4996615-azure-should-be-its-own-domain-registrar).

### <a name="does-azure-dns-support-private-domains"></a>O DNS do Azure oferece suporte a domínios 'privados'?

Não. O DNS do Azure no momento apenas oferece suporte a domínios da Internet.

Esse é um recurso que estamos acompanhando em nossa lista de pendências. Você pode usar nosso site de feedback muito[registrar seu suporte para esse recurso](https://feedback.azure.com/forums/217313-networking/suggestions/10737696-enable-split-dns-for-providing-both-public-and-int).

Para saber mais sobre opções de DNS internas no Azure, veja [Resolução de nomes de máquinas virtuais e instâncias de função](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

### <a name="does-azure-dns-support-dnssec"></a>O DNS do Azure oferece suporte a DNSSEC?

Não. Atualmente não há suporte para DNSSEC no DNS do Azure.

Esse é um recurso que estamos acompanhando em nossa lista de pendências. Você pode usar nosso site de feedback muito[registrar seu suporte para esse recurso](https://feedback.azure.com/forums/217313-networking/suggestions/13284393-azure-dns-needs-dnssec-support).

### <a name="does-azure-dns-support-zone-transfers-axfrixfr"></a>O DNS do Azure dá suporte para transferências de zona (AXFR/IXFR)?

Não. Atualmente não há suporte para transferências de zona. As zonas DNS podem ser [importado para o DNS do Azure usando Olá CLI do Azure](dns-import-export.md). Os registros de DNS podem ser gerenciados por meio de saudação [portal de gerenciamento do DNS do Azure](dns-operations-recordsets-portal.md), nosso [API REST](https://docs.microsoft.com/powershell/module/azurerm.dns), [SDK](dns-sdk.md), [cmdlets do PowerShell](dns-operations-recordsets.md), ou [ Ferramenta CLI](dns-operations-recordsets-cli.md).

Esse é um recurso que estamos acompanhando em nossa lista de pendências. Você pode usar nosso site de feedback muito[registrar seu suporte para esse recurso](https://feedback.azure.com/forums/217313-networking/suggestions/12925503-extend-azure-dns-to-support-zone-transfers-so-it-c).

### <a name="does-azure-dns-support-url-redirects"></a>O DNS do Azure oferece suporte a redirecionamentos de URL?

Não. Serviços de redirecionamento de URL não são, na verdade, um serviço DNS - funcionam no nível HTTP hello, em vez de nível DNS hello. Alguns provedores DNS toobundle um serviço de redirecionamento de URL como parte da sua oferta geral. Atualmente, isso não tem o suporte do DNS do Azure.

Esse recurso é acompanhado em nossa lista de pendências. Você pode usar nosso site de feedback muito[registrar seu suporte para esse recurso](https://feedback.azure.com/forums/217313-networking/suggestions/10109736-provide-a-301-permanent-redirect-service-for-ape).

## <a name="using-azure-dns"></a>Usando o DNS do Azure

### <a name="can-i-co-host-a-domain-using-azure-dns-and-another-dns-provider"></a>É possível co-hospedar um domínio usando o DNS do Azure e outro provedor de DNS?

Sim. O DNS do Azure oferece suporte a domínios de co-hospedagem com outros serviços de DNS.

toodo assim, você precisa de registros de saudação NS toomodify para domínio hello (que controlam quais provedores recebem DNS consultas para o domínio de saudação) toopoint toohello servidores de nome de ambos os provedores. Esses registros NS necessário toobe modificado em 3 locais: no DNS do Azure, em Olá outro provedor e na zona pai de saudação (normalmente é configurado por meio do registrador de nome de domínio de saudação). Para saber mais sobre delegação de DNS, veja [Delegação de domínio de DNS](dns-domain-delegation.md).

Além disso, você precisa tooensure que os registros DNS Olá para domínio Olá são sincronizados entre os dois provedores DNS. Atualmente não há suporte para transferências de zona DNS. Você precisa toosynchronize registros DNS usando o hello [portal de gerenciamento do DNS do Azure](dns-operations-recordsets-portal.md), nosso [API REST](https://docs.microsoft.com/powershell/module/azurerm.dns), [SDK](dns-sdk.md), [cmdlets do PowerShell](dns-operations-recordsets.md) , ou [ferramenta CLI](dns-operations-recordsets-cli.md).

### <a name="do-i-have-toodelegate-my-domain-tooall-4-azure-dns-name-servers"></a>É necessário toodelegate meus servidores de nome DNS do Azure domínio tooall 4?

Sim. DNS do Azure atribui 4 servidores de nome tooeach zona DNS, para o isolamento de falhas e aumentar a resiliência. tooqualify para Olá SLA de DNS do Azure, você precisa toodelegate seus servidores de nome do domínio tooall 4.

### <a name="what-are-hello-usage-limits-for-azure-dns"></a>Quais são os limites de uso de saudação do DNS do Azure?

Olá limites padrão a seguir se aplicam ao usar o DNS do Azure:

[!INCLUDE [dns-limits](../../includes/dns-limits.md)]

### <a name="can-i-move-an-azure-dns-zone-between-resource-groups-or-between-subscriptions"></a>Posso mover uma zona DNS do Azure entre grupos de recursos ou entre assinaturas?

Sim. As zonas DNS podem ser movidas entre grupos de recursos ou entre assinaturas.

Não há nenhum impacto nas consultas de DNS ao mover uma zona DNS. servidores de nome de saudação atribuídos toohello zona permanecem Olá que mesmo e consultas DNS são processadas como normal em todo.

Para obter mais informações e instruções sobre como toomove zonas DNS, consulte [mover recursos tooa novo grupo de recursos ou assinatura](../azure-resource-manager/resource-group-move-resources.md).

### <a name="how-long-does-it-take-for-dns-changes-tootake-effect"></a>Quanto tempo leva para efeito de tootake de alterações DNS?

Novas zonas DNS e registros de DNS são normalmente refletidos nos servidores de nome DNS do Azure Olá rapidamente, em alguns segundos.

Os registros DNS tooexisting alterações podem demorar um pouco mais, mas ainda devem ser refletidos em servidores de nome DNS do Azure hello dentro de 60 segundos. Nesse caso, a cache de DNS fora do DNS do Azure (por clientes e resolvedores do DNS recursivo) também pode afetar Olá tempo para um toobe de alteração do DNS efetivo. A duração do cache pode ser controlada usando a propriedade de tempo de vida (TTL) de saudação de cada conjunto de registros.

### <a name="how-can-i-protect-my-dns-zones-against-accidental-deletion"></a>Como posso proteger minhas zonas DNS contra exclusão acidental?

DNS do Azure é gerenciado com o Gerenciador de recursos do Azure e benefícios da saudação acessar recursos de controle que o Gerenciador de recursos do Azure fornece. Controle de acesso baseado em função pode ser usado toocontrol quais usuários têm acesso de leitura ou gravação zonas de tooDNS e conjuntos de registros. Bloqueios de recursos podem ser aplicada tooprevent a modificação acidental ou exclusão de zonas DNS e conjuntos de registros.

Para saber mais, veja [Proteção de zonas e registros DNS](dns-protect-zones-recordsets.md).

### <a name="how-do-i-set-up-spf-records-in-azure-dns"></a>Como posso configurar registros de SPF no DNS do Azure?

[!INCLUDE [dns-spf-include](../../includes/dns-spf-include.md)]

### <a name="how-do-i-set-up-an-international-domain-name-idn-in-azure-dns"></a>Como posso configurar um nome de domínio internacional (IDN) no DNS do Azure?

Nomes de domínios internacionais (IDNs) funcionam por codificação de cada nome de DNS usando '[punycode](https://en.wikipedia.org/wiki/Punycode)'. As consultas de DNS são feitas usando esses nomes codificados para punycode.

Você pode configurar os nomes de domínio internacionais (IDNs) no DNS do Azure pelo primeiro nome de zona Olá converter ou toopunycode do nome do conjunto de registros. Atualmente não há suporte para conversão interna de/para punycode no DNS do Azure.

## <a name="next-steps"></a>Próximas etapas

[Saiba mais sobre DNS do Azure](dns-overview.md)
<br>
[Saiba mais sobre zonas e registros DNS](dns-zones-records.md)
<br>
[Introdução ao DNS do Azure](dns-getstarted-portal.md)

