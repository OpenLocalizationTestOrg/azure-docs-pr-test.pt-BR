---
title: "aaaEnable grupos de segurança de rede na Central de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá recomendação da Central de segurança do Azure * * habilitar rede segurança grupos * *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: f53ed853-ffaf-4530-a019-1906ba6f341b
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 2f70fe432aa452f833a5c322d13102ebbd6dbb69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-network-security-groups-in-azure-security-center"></a>Habilitar Grupos de Segurança de Rede na Central de Segurança do Azure
A Central de Segurança do Azure recomenda que você habilite um NSG (grupo de segurança de rede), se já não estiver habilitado. Os NSGs contém uma lista de regras de lista de controle de acesso (ACL) que permitem ou negam o tráfego de rede tooyour instâncias VM em uma rede Virtual. Os NSGs podem ser associados a sub-redes ou instâncias de VM individuais dentro dessa sub-rede. Quando um NSG está associado uma sub-rede, regras de ACL de saudação se aplicam a instâncias de VM Olá tooall nessa sub-rede. Além disso, o tráfego tooan VM individual pode ser restrito adicional associando um NSG toothat VM diretamente. toolearn mais ver [o que é um grupo de segurança de rede (NSG)?](../virtual-network/virtual-networks-nsg.md)

Se você não tiver os NSGs habilitados, a Central de segurança apresenta dois tooyou de recomendações: habilitar os grupos de segurança de rede em sub-redes e habilitar os grupos de segurança de rede em máquinas virtuais. Você escolhe qual nível, a sub-rede ou a VM, tooapply NSGs.

> [!NOTE]
> Este documento apresenta serviço hello usando um exemplo de implantação.  Ela não é um guia passo a passo.
>
>

## <a name="implement-hello-recommendation"></a>Implementar a recomendação de saudação
1. Em Olá **recomendações** folha, selecione **habilitar grupos de segurança de rede** em sub-redes ou em máquinas virtuais.
   ![Habilitar Grupos de segurança de rede][1]
2. Isso abre a folha de saudação **configurar grupos de segurança de rede ausente** para sub-redes ou para máquinas virtuais, dependendo de recomendação de saudação que você selecionou. Selecione uma sub-rede ou uma máquina virtual de tooconfigure um NSG.

   ![Configurar NSG para sub-rede][2]

   ![Configurar NSG para VM][3]
3. Em Olá **o grupo de segurança de rede escolha** folha, selecione um NSG existente ou selecione **criar novo** toocreate um NSG.

   ![Escolher grupo de segurança de rede][4]

Se você criar um NSG, siga as etapas de saudação em [como toomanage NSGs usando Olá portal do Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) toocreate um NSG e defina as regras de segurança.

## <a name="see-also"></a>Consulte também
Este artigo mostrou como tooimplement Olá Central de segurança recomendação "habilitar grupos de segurança rede" em sub-redes ou máquinas virtuais. toolearn mais sobre como habilitar os NSGs, consulte o seguinte hello:

* [O que é um NSG (grupo de segurança de rede)?](../virtual-network/virtual-networks-nsg.md)
* [Como toomanage NSGs usando Olá portal do Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

toolearn mais sobre o Centro de segurança, consulte o seguinte hello:

* [Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) – Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.
* [Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.
* [Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md) – Saiba como toomonitor Olá a integridade de seus recursos do Azure.
* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como alertas de toosecurity toomanage e responder.
* [Soluções de parceiro com a Central de segurança do Azure de monitoramento](security-center-partner-solutions.md) – Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) – localizar perguntas frequentes sobre como usar o serviço de saudação.
* [Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – obter notícias mais recentes de segurança do Azure hello e informações.

<!--Image references-->
[1]: ./media/security-center-enable-nsg/enable-nsg.png
[2]:./media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: ./media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: ./media/security-center-enable-nsg/choose-nsg.png
