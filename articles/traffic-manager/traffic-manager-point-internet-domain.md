---
title: "aaaPoint um nome de domínio da empresa Internet domínio tooa Traffic Manager | Microsoft Docs"
description: "Este artigo o ajudará a apontar seu nome de domínio da empresa domínio nome tooa Gerenciador de tráfego."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 29822946-2d45-4434-ba47-fc180a445cc3
ms.service: traffic-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: kumud
ms.openlocfilehash: 84c428f60a1dc70452bf957d98a68c95e0b51715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="point-a-company-internet-domain-tooan-azure-traffic-manager-domain"></a>Apontar um domínio de Gerenciador de tráfego do Azure da empresa Internet domínio tooan

Quando você cria um perfil do Gerenciador de tráfego, o Azure atribui automaticamente um nome DNS ao perfil. toouse um nome de zona DNS, crie um registro de DNS CNAME que mapeia o nome de domínio toohello do seu perfil do Gerenciador de tráfego. Você pode encontrar o nome de domínio do Traffic Manager Olá no hello **geral** seção na página de configuração Olá Olá perfil do Traffic Manager.

Por exemplo, toopoint nome www.contoso.com toohello contoso.trafficmanager.net de nome DNS do Traffic Manager, você deve criar Olá registro de recurso DNS a seguir:

    www.contoso.com IN CNAME contoso.trafficmanager.net

Todo o tráfego de solicitações muito*www.contoso.com* obter direcionado muito*contoso.trafficmanager.net*.

> [!IMPORTANT]
> Você não pode apontar um domínio de segundo nível, como *contoso.com*, domínio do Traffic Manager toohello. Os padrões de protocolo DNS não permitem registros CNAME para nomes de domínio de segundo nível.

## <a name="next-steps"></a>Próximas etapas

* [Métodos de roteamento do Gerenciador de Tráfego](traffic-manager-routing-methods.md)
* [Gerenciador de Tráfego - Desabilitar, habilitar ou excluir um perfil](disable-enable-or-delete-a-profile.md)
* [Gerenciador de Tráfego - Desabilitar ou habilitar um ponto de extremidade](disable-or-enable-an-endpoint.md)
