---
title: "alertas de segurança aaaHandling na Central de segurança do Azure | Microsoft Docs"
description: "Este documento ajudará a incidentes de segurança de toohandle de recursos do toouse Central de segurança do Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: e8feb669-8f30-49eb-ba38-046edf3f9656
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: edb911c298a2ce93cd0ea5b22ce002005040090f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="handling-security-incidents-in-azure-security-center"></a>Manipulação de Incidentes de Segurança na Central de Segurança do Azure
Separação e investigando os alertas de segurança podem levar muito tempo para que os analistas de segurança mais capacitados Olá mesmo e para muitos é tooeven difícil saber onde toobegin. Usando [análise](security-center-detection-capabilities.md) tooconnect informações de saudação entre distintos [alertas de segurança](security-center-managing-and-responding-alerts.md), Central de segurança pode fornecer uma única exibição de uma campanha de ataque e todos Olá relacionados alertas – você pode Compreenda rapidamente o invasor de saudação ações levou e os recursos que foram afetados.

Este documento aborda como toouse alerta de segurança do recurso na Central de segurança tooassist você lidar com incidentes de segurança.

## <a name="what-is-a-security-incident"></a>O que é um incidente de segurança?
Na Central de Segurança, um incidente de segurança é uma agregação de todos os alertas de um recurso que se alinham com os padrões da [cadeia de desativações](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) . Incidentes aparecem na Olá [alertas de segurança](security-center-managing-and-responding-alerts.md) lado a lado e folha. Um incidente revelará a lista de saudação de alertas relacionados, que permite que você tooobtain obter mais informações sobre cada ocorrência.

## <a name="managing-security-incidents"></a>Gerenciamento de incidentes de segurança
Você pode examinar seus incidentes de segurança atual examinando Olá bloco de alertas de segurança. Acesso Olá Portal do Azure e siga as etapas de saudação abaixo toosee mais detalhes sobre cada incidente de segurança:

1. No painel de Central de segurança hello, você verá Olá **alertas de segurança** lado a lado.

    ![Bloco Alertas de segurança na Central de Segurança](./media/security-center-incident/security-center-incident-fig1.png)

2. Clique em tooexpand esse bloco-lo e se um incidente de segurança é detectado, ele será exibido no gráfico de alertas de segurança Olá conforme mostrado abaixo:

    ![Incidente de segurança](./media/security-center-incident/security-center-incident-fig2.png)

3. Observe que a descrição do incidente de segurança Olá tem um ícone diferente em comparação com tooother alertas. Clique nela tooview mais detalhes sobre este incidente.

    ![Incidente de segurança](./media/security-center-incident/security-center-incident-fig3.png)

4. Em Olá **incidente** folha, você verá mais detalhes sobre este incidente de segurança, que inclui a descrição completa, sua severidade (que nesse caso é alta), seu estado atual (nesse caso ele ainda é *ativo*, o que implica que o usuário Olá não tiver feito tooit uma ação - isso pode ser feito pelo clique com o botão direito no incidente Olá no hello **alertas de segurança** folha), Olá atacados recurso (neste caso *VM1*), Olá etapas de correção de incidente hello e no painel inferior de saudação você tem alertas de saudação que foram incluídos neste incidente. Se você quiser obter mais informações sobre cada alerta tooobtain, basta clicar nele e outra folha será aberta, conforme mostrado abaixo:

    ![Incidente de segurança](./media/security-center-incident/security-center-incident-fig4.png)

informações de saudação nesta folha variam de alerta de toohello de acordo. Leitura [toosecurity está respondendo e gerenciamento de alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) para obter mais informações sobre como toomanage esses alertas. Algumas considerações importantes sobre esse recurso:

* Um novo filtro permite que você toocustomize que tooincident sua exibição alertas somente, apenas, ou ambos.
* Olá mesmo alerta pode existir como parte de um incidente (se aplicável), bem como toobe visível como um alerta autônomo.

## <a name="see-also"></a>Consulte também
Neste documento, você aprendeu como toouse Olá do recurso incidente de segurança na Central de segurança. toolearn mais sobre o Centro de segurança, consulte o seguinte hello:

* [Gerenciando e responder a alertas toosecurity na Central de segurança do Azure](security-center-managing-and-responding-alerts.md)
* [Recursos de detecção da Central de Segurança do Azure](security-center-detection-capabilities.md)
* [Guia de planejamento e operações da Central de Segurança do Azure](security-center-planning-and-operations-guide.md)
* [Gerenciando e responder a alertas toosecurity na Central de segurança do Azure](security-center-managing-and-responding-alerts.md)
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md)– localizar perguntas frequentes sobre como usar o serviço de saudação.
* [Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/): encontre postagens no blog sobre a conformidade e a segurança do Azure.
