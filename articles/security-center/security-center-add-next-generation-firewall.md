---
title: "aaaAdd um firewall de geração Avançar na Central de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá recomendações da Central de segurança do Azure * * adicionar uma próxima geração Firewall * * e * * tráfego de rota somente por meio de NGFW * *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 48b99015-4db8-4ce8-85e4-b544c0fa203e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 9a80f12571ba08eadf3361728c6321388c863235
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-next-generation-firewall-in-azure-security-center"></a>Adicionar um Firewall de Última Geração na Central de Segurança do Azure
Central de segurança do Azure pode recomendar que você adicionar um firewall de geração de Avançar (NGFW) de um tooincrease de parceiro da Microsoft suas proteções de segurança. Este documento orienta você por um exemplo de como toodo isso.

> [!NOTE]
> Este documento apresenta serviço hello usando um exemplo de implantação.  Ela não é um guia passo a passo.
>
>

## <a name="implement-hello-recommendation"></a>Implementar a recomendação de saudação
1. Em Olá **recomendações** folha, selecione **adicionar um Firewall de geração de Avançar**.
   ![Adicionar um Firewall de Última Geração][1]
2. Em Olá **adicionar um Firewall de geração de Avançar** folha, selecione um ponto de extremidade.
   ![Selecionar um ponto de extremidade][2]
3. Uma segunda folha **Adicionar um Firewall de Última Geração** será aberta. Você pode escolher toouse uma solução existente se estiver disponível ou você pode criar um novo. Neste exemplo não existem soluções disponíveis, por isso, criaremos um novo NGFW.
   ![Criar um novo Firewall de Última Geração][3]
4. toocreate um NGFW, selecione uma solução de lista de saudação de parceiros integrados. Neste exemplo, selecionamos **Check Point**.
   ![Selecionar uma solução de Firewall de Última Geração][4]
5. Olá **ponto de verificação** folha é aberto, fornecendo informações sobre solução de parceiro hello. Selecione **criar** na folha de informações de saudação.
   ![Folha Informações do firewall][5]
6. Olá **criar a máquina virtual** folha é aberta. Aqui você pode inserir informações necessária toospin uma máquina virtual (VM) que executa Olá NGFW. Siga as etapas de saudação e fornecer Olá NGFW informações necessárias. Selecione tooapply Okey.
   ![Criar a máquina virtual toorun NGFW][6]

## <a name="route-traffic-through-ngfw-only"></a>Rotear o tráfego apenas através do NGFW
Retornar toohello **recomendações** folha. Uma nova entrada foi gerada após a adição de um NGFW por meio da Central de Segurança, chamada **Rotear o tráfego somente por meio do NGFW**. Essa recomendação será criada somente se você tiver instalado o NGFW por meio da Central de Segurança. Se você tiver pontos de extremidade para a Internet, a Central de segurança recomenda que você configure regras de grupo de segurança de rede que forçar o tráfego de entrada tooyour VM por meio de seu NGFW.

1. Em Olá **folha recomendações**, selecione **rotear o tráfego por meio de NGFW**.
   ![Rotear o tráfego apenas através do NGFW][7]
2. Isso abre a folha de saudação **rotear o tráfego por meio de NGFW**, que lista as VMs que você pode rotear o tráfego. Selecione uma VM na lista de saudação.
   ![Selecionar uma máquina virtual][8]
3. Uma folha de saudação selecionado VM é aberta, exibindo as regras de entrada relacionadas. Uma descrição fornece a você mais informações sobre as próximas etapas possíveis. Selecione **editar regras de entrada** tooproceed com a edição de uma regra de entrada. Olá expectativa é que **fonte** não está definido muito**qualquer** para pontos de extremidade do hello voltados para Internet vinculado com hello NGFW. toolearn mais informações sobre propriedades de saudação de regra de entrada hello, consulte [regras NSG](../virtual-network/virtual-networks-nsg.md#nsg-rules).
   ![Configurar o acesso de toolimit regras][9]
   ![Editar regra de entrada][10]

## <a name="see-also"></a>Consulte também
Este documento lhe mostrou como tooimplement Olá recomendação da Central de segurança "Adicionar um Firewall de geração Avançar". toolearn mais sobre NGFWs e hello solução de parceiro do ponto de verificação, consulte o seguinte hello:

* [Firewall de Última Geração](https://en.wikipedia.org/wiki/Next-Generation_Firewall)
* [Check Point vSEC](https://azure.microsoft.com/marketplace/partners/checkpoint/check-point-r77-10/)

toolearn mais sobre o Centro de segurança, consulte o seguinte hello:

* [Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) – Saiba como tooconfigure as políticas de segurança.
* [Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.
* [Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md) – Saiba como toomonitor Olá a integridade de seus recursos do Azure.
* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como alertas de toosecurity toomanage e responder.
* [Soluções de parceiro com a Central de segurança do Azure de monitoramento](security-center-partner-solutions.md) – Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) – localizar perguntas frequentes sobre como usar o serviço de saudação.
* [Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – encontre postagens no blog sobre conformidade e segurança do Azure.

<!--Image references-->
[1]: ./media/security-center-add-next-gen-firewall/add-next-gen-firewall.png
[2]: ./media/security-center-add-next-gen-firewall/select-an-endpoint.png
[3]: ./media/security-center-add-next-gen-firewall/create-new-next-gen-firewall.png
[4]: ./media/security-center-add-next-gen-firewall/select-next-gen-firewall.png
[5]: ./media/security-center-add-next-gen-firewall/firewall-solution-info-blade.png
[6]: ./media/security-center-add-next-gen-firewall/create-virtual-machine.png
[7]: ./media/security-center-add-next-gen-firewall/route-traffic-through-ngfw.png
[8]: ./media/security-center-add-next-gen-firewall/select-vm.png
[9]: ./media/security-center-add-next-gen-firewall/configure-rules-to-limit-access.png
[10]: ./media/security-center-add-next-gen-firewall/edit-inbound-rule.png
