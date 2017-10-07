---
title: "aaaUsing DNS do Azure com outros serviços do Azure | Microsoft Docs"
description: "Noções básicas sobre como nome de toouse tooresolve de DNS do Azure para outros serviços do Azure"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure dns
ms.assetid: e9b5eb94-7984-4640-9930-564bb9e82b78
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 09/21/2016
ms.author: gwallace
ms.openlocfilehash: 791f93d6aff2c638c08518e9f1e8ab89ac8de3f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-dns-works-with-other-azure-services"></a>Como o Azure DNS funciona com outros serviços do Azure

O DNS do Azure é um serviço hospedado de gerenciamento de DNS e resolução de nomes. Isso permite que você toocreate públicos nomes DNS Olá outros aplicativos e serviços que você implantou no Azure. Criar um nome para um serviço do Azure no seu domínio personalizado é tão simple quanto adicionar um registro de tipo de saudação correto para seu serviço.

* Endereços IP alocados dinamicamente, você deve criar um registro de DNS CNAME esse nome DNS de toohello mapas Azure criado para o serviço. Padrões DNS impedem que você usar um registro CNAME para ápice da zona de saudação.
* Endereços IP alocados estaticamente, você pode criar um registro de DNS A usar qualquer nome, incluindo um *domínio naked* nome no ápice da zona de saudação.

Olá seguir saudação de estruturas de tabela suporte para tipos de registro que podem ser usados para diversos serviços do Azure. Como você pode ver nessa tabela, o DNS do Azure dá suporte apenas a registros DNS para recursos de rede voltados para a Internet. O DNS do Azure não pode ser usado para a resolução de nome de endereços internos, privadas.

| Serviço do Azure | Interface de rede | Descrição |
| --- | --- | --- |
| Gateway de Aplicativo |[IP público de front-end](dns-custom-domain.md#public-ip-address) |Você pode criar um registro CNAME ou DNS A. |
| Balanceador de carga |[IP público de front-end](dns-custom-domain.md#public-ip-address)  |Você pode criar um registro CNAME ou DNS A. O Balanceador de Carga pode ter um endereço IP público do IPv6 que é atribuído dinamicamente. Portanto, você deve criar um registro CNAME para um endereço IPv6. |
| Gerenciador de Tráfego |Nome público |Você só pode criar um CNAME que mapeia toohello trafficmanager.net nome atribuído tooyour perfil do Traffic Manager. Para saber mais, confira [Como o Gerenciador de Tráfego funciona](../traffic-manager/traffic-manager-overview.md#traffic-manager-example). |
| Serviço de Nuvem |[IP público](dns-custom-domain.md#public-ip-address) |Para endereços IP alocados estaticamente, você pode criar um registro DNS A. Endereços IP alocados dinamicamente, você deve criar um registro CNAME que mapeia toohello *cloudapp.net* nome. Essa regra se aplica a tooVMs criado no portal clássico do hello porque eles são implantados como um serviço de nuvem. Para saber mais, confira [Configurar um nome de domínio personalizado nos Serviços de Nuvem](../cloud-services/cloud-services-custom-domain-name-portal.md). |
| Serviço de Aplicativo | [IP externo](dns-custom-domain.md#app-service-web-apps) |Para endereços IP externos, você pode criar um registro DNS A. Caso contrário, você deve criar um registro CNAME que mapeia o nome de toohello azurewebsites.net. Para obter mais informações, consulte [mapear um nome de domínio personalizado tooan aplicativo do Azure](../app-service-web/web-sites-custom-domain-name.md) |
| VMs do Resource Manager |[IP público](dns-custom-domain.md#public-ip-address) |As VMs do Gerenciador de Recursos pode ter endereços IP públicos. Uma VM com um endereço IP público também pode estar por trás de um balanceador de carga. Você pode criar um registro DNS A ou CNAME para Olá endereço público. Esse nome personalizado pode ser usado toobypass Olá VIP no balanceador de carga de saudação. |
| VMs clássicas |[IP público](dns-custom-domain.md#public-ip-address) |VMs clássicas criadas usando o PowerShell ou a CLI podem ser configuradas com um endereço virtual (reservado) dinâmico ou estático. Você pode criar um registro DNS CNAME ou A, respectivamente. |
