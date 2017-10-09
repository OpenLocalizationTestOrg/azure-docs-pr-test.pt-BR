---
title: "alertas de segurança aaaManage na Central de segurança do Azure | Microsoft Docs"
description: "Este documento ajuda você toouse Central de segurança do Azure recursos toomanage e responde a alertas de toosecurity."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b88a8df7-6979-479b-8039-04da1b8737a7
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: f1cb7e4770776827b75ed15893914678c1f44216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-and-responding-toosecurity-alerts-in-azure-security-center"></a>Gerenciando e responder a alertas toosecurity na Central de segurança do Azure
Este documento ajuda você a usar a Central de segurança do Azure toomanage e responder a alertas toosecurity.

> [!NOTE]
> detecções de tooenable avançado, atualização tooAzure Central de segurança padrão. Há uma avaliação gratuita de 60 dias disponível. tooupgrade, selecione preço no hello [política de segurança](security-center-policies.md). Consulte [Central de segurança do Azure preços](security-center-pricing.md) toolearn mais.
>
>

## <a name="what-are-security-alerts"></a>O que são alertas de segurança?
Central de segurança automaticamente coleta, analisa e integra dados de log de seus recursos do Azure, rede Olá e conectados soluções de parceiros, como soluções de proteção de firewall e de ponto de extremidade, ameaças reais toodetect e reduzir os falsos positivos. É mostrada uma lista de alertas de segurança priorizados na Central de segurança junto com hello informações que você precisa tooquickly investigar o problema hello e recomendações sobre como tooremediate um ataque.


> [!NOTE]
> Para saber mais sobre como funciona os recursos de detecção da Central de Segurança, leia [Recursos de detecção da Central de Segurança do Azure](security-center-detection-capabilities.md).
>
>

## <a name="managing-security-alerts"></a>Configurando alertas de segurança
Você pode examinar os alertas atuais examinando Olá **alertas de segurança** lado a lado. Abra o Portal do Azure e siga as etapas de saudação abaixo toosee mais detalhes sobre cada alerta:

1. No painel de Central de segurança hello, você verá Olá **alertas de segurança** lado a lado.

    ![Bloco Alertas de segurança na Central de Segurança](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig1-ga.png)

2. Clique em Olá bloco tooopen Olá **alertas de segurança** folha que contém mais detalhes sobre Olá alertas conforme mostrado abaixo.

   ![folha de alertas de segurança Olá na Central de segurança](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig2-ga.png)

Na parte inferior Olá esta folha são os detalhes de saudação para cada alerta. toosort, clique em coluna Olá que você deseja toosort por. definição de saudação para cada coluna é indicada abaixo:

* **Descrição**: uma breve explicação de alerta de saudação.
* **Contagem**: uma lista de todos os alertas desse tipo específico que foram detectados em um dia específico.
* **Detectado pelo**: Olá serviço que foi responsável para disparar o alerta de saudação.
* **Data**: Olá data que o evento Olá ocorreu.
* **Estado**: Olá estado atual para o alerta. Há dois tipos de estado:
  * **Active**: alerta de segurança Olá foi detectada.
* **Severidade**: nível de severidade hello, que pode ser alta, média ou baixa.

### <a name="filtering-alerts"></a>Filtragem de alertas
Você pode filtrar com base na data, no estado e na gravidade dos alertas. Filtragem de alertas pode ser útil para cenários em que você precisa que o escopo de saudação toonarrow de apresentação de alertas de segurança. Por exemplo, você pode desejar tooaddress alertas de segurança que ocorreram em Olá últimas 24 horas, porque você está investigando uma possível falha no sistema de saudação.

1. Clique em **filtro** em Olá **alertas de segurança** folha. Olá **filtro** folha é aberto e você selecionar valores de data, o estado e a gravidade de saudação desejar toosee.

    ![Filtragem de alertas na Central de Segurança](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig3-2017.png)

### <a name="respond-toosecurity-alerts"></a>Responder a alertas de toosecurity
Selecione um toolearn de alerta de segurança mais sobre o evento Olá que disparou o alerta hello e, se houver, etapas que você precisam tootake tooremediate um ataque. Os alertas de segurança são agrupados por tipo e data. Clicando em um alerta de segurança, você abrirá uma folha que contém uma lista de alertas de saudação agrupada.

![Responder a alertas toosecurity na Central de segurança do Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig5-ga.png)

Nesse caso, os alertas de saudação que foram acionados consulte toosuspicious atividade do protocolo de área de trabalho remota (RDP). Olá primeira coluna mostra quais recursos foram atacados; Olá segundo mostra quantas vezes recurso Olá atacado; Olá terceiro mostra o tempo de saudação de ataque de saudação. Olá quarto mostra o estado de alerta de saudação; e Olá quinto mostra a gravidade de saudação do ataque de saudação. Depois de revisar essas informações, clique em recursos de saudação que foi atacado e abrirá uma nova folha.

![Sugestões para quais toodo sobre a segurança de alertas na Central de segurança do Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig6-ga.png)

Em Olá **descrição** campo desta folha você encontrará mais detalhes sobre esse evento. Esses detalhes adicionais oferecem informações sobre quais Olá disparada segurança alerta, Olá recurso de destino, quando aplicável Olá fonte de endereço IP e recomendações sobre como tooremediate.  Em alguns casos, o endereço IP de origem Olá ser esvaziará (não disponível) porque nem todos os logs de eventos de segurança do Windows incluem o endereço IP de saudação.

correção Olá sugerida pela Central de segurança variam de acordo alerta de segurança toohello. Em alguns casos, você pode ter toouse tooimplement outros recursos do Azure Olá recomendado correção. Olá, por exemplo, a correção para esse ataque é o endereço IP do tooblacklist Olá que está gerando esse ataque usando um [ACL de rede](../virtual-network/virtual-networks-acl.md) ou um [grupo de segurança de rede](../virtual-network/virtual-networks-nsg.md) regra.

> [!NOTE]
> Para obter mais informações sobre tipos diferentes de saudação de alertas, leia [alertas de segurança por tipo na Central de segurança do Azure](security-center-alerts-type.md).
>
>

## <a name="see-also"></a>Consulte também
Neste documento, você aprendeu como tooconfigure políticas de segurança na Central de segurança. toolearn mais sobre o Centro de segurança, consulte o seguinte hello:

* [Manipulação de incidente de segurança na Central de Segurança do Azure](security-center-incident.md)
* [Recursos de detecção da Central de Segurança do Azure](security-center-detection-capabilities.md)
* [Guia de planejamento e operações da Central de Segurança do Azure](security-center-planning-and-operations-guide.md)
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) — localizar perguntas frequentes sobre como usar o serviço de saudação.
* [Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) : encontre postagens no blog sobre conformidade e segurança do Azure.
