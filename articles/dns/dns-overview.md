---
title: aaaOverview do DNS do Azure | Microsoft Docs
description: "Visão geral do Serviço de hospedagem de DNS no Microsoft Azure. Hospede seu domínio no Microsoft Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 68747a0d-b358-4b8e-b5e2-e2570745ec3f
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: gwallace
ms.openlocfilehash: a10f87c488356469e9c04aabde31129049563891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-overview"></a>Visão geral do DNS do Azure

Olá, sistema de nomes de domínio ou DNS, é responsável pela conversão (ou seja, resolver) um site ou serviço name tooits endereço IP. O DNS do Azure é um serviço de hospedagem para domínios DNS, fornecendo resolução de nomes usando a infraestrutura do Microsoft Azure. Ao hospedar seus domínios no Azure, você pode gerenciar seu DNS registros usando Olá mesmo credenciais, APIs, ferramentas e cobrança como outros serviços do Azure.

![Visão geral de DNS](./media/dns-overview/scenario.png)

## <a name="features"></a>Recursos

* **Confiabilidade e desempenho** - domínios DNS no DNS do Azure são hospedados na rede global do Azure de servidores de nomes DNS. Usamos a difusão de rede para que cada consulta DNS for atendida, o servidor DNS mais próximo disponível para o hello. Isso fornece desempenho rápido e alta disponibilidade para seu domínio.

* **Integração perfeita** -serviço de DNS do Azure Olá pode ser usado toomanage registros de DNS para os serviços do Azure e pode ser usado tooprovide DNS para os recursos externos, bem. DNS do Azure é integrado no hello portal do Azure e usa Olá as mesmas credenciais, cobrança e contrato de suporte como os outros serviços do Azure.

* **Segurança** -Olá serviço DNS do Azure baseia-se no Gerenciador de recursos do Azure. Sendo assim, ele aproveita recursos do Resource Manager, como o controle de acesso baseado em função, os logs de auditoria e o bloqueio de recursos. Seus domínios e registros podem ser gerenciados por meio de saudação portal do Azure, cmdlets do PowerShell do Azure, em Olá CLI do Azure de plataforma cruzada. Aplicativos que exigem o gerenciamento automático de DNS podem integrar saudação do serviço por meio de saudação API REST e SDKs.

O DNS do Azure não dá suporte a compra de nomes de domínio. Se você quiser toopurchase domínios, é necessário toouse um registrador de nomes de domínio de terceiro. registrador Olá normalmente cobra uma pequena taxa anual. domínios Olá, em seguida, podem ser hospedados no Azure DNS para o gerenciamento de registros de DNS. Consulte [delegar tooAzure um domínio DNS](dns-domain-delegation.md) para obter detalhes.

## <a name="pricing"></a>Preços

Cobrança do DNS é com base no número de saudação de zonas DNS hospedadas no Azure e pelo número de saudação de consultas DNS. toolearn mais sobre preços visite [de preços do Azure DNS](https://azure.microsoft.com/pricing/details/dns/).

## <a name="faq"></a>Perguntas frequentes

Para perguntas frequentes sobre o DNS do Azure, consulte Olá [perguntas Frequentes do Azure DNS](dns-faq.md).

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre as zonas e registros DNS visitando: [Visão geral de zonas e registros DNS](dns-zones-records.md).

Saiba como muito[criar uma zona DNS](./dns-getstarted-create-dnszone-portal.md) no DNS do Azure.

Saiba mais sobre alguns dos Olá outra chave [recursos de rede](../networking/networking-overview.md) do Azure.

