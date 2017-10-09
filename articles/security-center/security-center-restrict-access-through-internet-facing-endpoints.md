---
title: "aaaRestrict acesso por meio de pontos de extremidade da Internet na Central de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá recomendação da Central de segurança do Azure * * restringir o acesso por meio da Internet voltada para o ponto de extremidade * *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 727d88c9-163b-4ea0-a4ce-3be43686599f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: ee72497088618d4db29b5ae4183f4fe77b498423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-access-through-internet-facing-endpoints-in-azure-security-center"></a>Restringir o acesso por meio de pontos de extremidade para a Internet na Central de Segurança do Azure
A Central de Segurança do Azure recomendará que você restrinja o acesso por meio de pontos de extremidade para a Internet se qualquer um dos seus grupos de segurança de rede (NSGs) tiver uma ou mais regras de entrada que permitam acesso de "qualquer" endereço IP de origem. Abertura de acesso muito "qualquer" pode permitir que os invasores tooaccess seus recursos. Central de segurança recomende que você editar endereços IP essas regras de entrada toorestrict acesso toosource que realmente precisam de acesso.

Essa recomendação é gerada para qualquer porta que não seja da Web que tenha "qualquer" como fonte.

> [!NOTE]
> Este documento apresenta serviço hello usando um exemplo de implantação. Ela não é um guia passo a passo.
>
>

## <a name="implement-hello-recommendation"></a>Implementar a recomendação de saudação
1. Em Olá **folha recomendações**, selecione **restringir o acesso por meio do ponto de extremidade da Internet**.

   ![Restringir o acesso por meio de ponto de extremidade para a Internet][1]
2. Isso abre a folha de saudação **restringir o acesso por meio do ponto de extremidade da Internet**. Esta folha lista Olá as máquinas virtuais (VMs) com as regras de entrada que cria um problema de segurança potencial. Selecionar uma máquina virtual.

   ![Selecionar uma máquina virtual][2]
3. Olá **NSG** folha exibe informações de grupo de segurança de rede, as regras de entrada relacionadas, e Olá associados a VM. Selecione **editar regras de entrada** tooproceed com a edição de uma regra de entrada.

   ![Folha Grupo de Segurança de Rede][3]
4. Em Olá **regras de segurança de entrada** selecione folha Olá tooedit de regra de entrada. Neste exemplo, vamos selecionar **AllowWeb**.

   ![Regras de segurança de entrada][4]

   Observe que você também pode selecionar **padrão regras** toosee conjunto de saudação de regras padrão por todos os NSGs. as regras de saudação padrão não podem ser excluídas, mas, porque eles recebem uma prioridade mais baixa, elas podem ser substituídas pelas regras de saudação que você criar. Saiba mais sobre [regras padrão](../virtual-network/virtual-networks-nsg.md#default-rules).

   ![Regras padrão][5]
5. Em Olá **AllowWeb** folha, editar propriedades de saudação da regra de entrada hello para que Olá **origem** é um endereço IP ou o bloco de endereços IP. toolearn mais informações sobre propriedades de saudação de regra de entrada hello, consulte [regras NSG](../virtual-network/virtual-networks-nsg.md#nsg-rules).

   ![Editar regra de entrada][6]

## <a name="see-also"></a>Consulte também
Este artigo lhe mostrou como tooimplement Olá Central de segurança recomendação "restringir o acesso por meio do ponto de extremidade da Internet." toolearn mais sobre como habilitar os NSGs e regras, consulte o seguinte hello:

* [O que é um NSG (grupo de segurança de rede)?](../virtual-network/virtual-networks-nsg.md)
* [Como toomanage NSGs usando Olá portal do Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

toolearn mais sobre o Centro de segurança, consulte o seguinte hello:

* [Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md)– Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.
* [Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md): saiba como as recomendações ajudam a proteger os recursos do Azure.
* [Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md)– Saiba como toomonitor Olá a integridade de seus recursos do Azure.
* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md)– Saiba como alertas de toosecurity toomanage e responder.
* [Soluções de parceiro com a Central de segurança do Azure de monitoramento](security-center-partner-solutions.md) – Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md)– localizar perguntas frequentes sobre como usar o serviço de saudação.
* [Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/)– obter notícias mais recentes de segurança do Azure hello e informações.

<!--Image references-->
[1]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/restrict-access-thru-internet-facing-endpoint.png
[2]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/select-a-vm.png
[3]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/network-security-group-blade.png
[4]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/inbound-security-rules.png
[5]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/default-rules.png
[6]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/edit-inbound-rule.png
