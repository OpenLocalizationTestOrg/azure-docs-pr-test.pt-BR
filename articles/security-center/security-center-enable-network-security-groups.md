---
title: "Habilitar Grupos de Segurança de Rede na Central de Segurança do Azure | Microsoft Docs"
description: "Este documento mostra como implementar a recomendação da Central de Segurança do Azure para **Habilitar Grupos de Segurança de Rede**."
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
ms.openlocfilehash: 1e034d59d8847f237fa0d4c772344d45cd618576
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-network-security-groups-in-azure-security-center"></a>Habilitar Grupos de Segurança de Rede na Central de Segurança do Azure
A Central de Segurança do Azure recomenda que você habilite um NSG (grupo de segurança de rede), se já não estiver habilitado. Os NSGs contêm uma lista de regras de ACL (Lista de Controle de Acesso) que permitem ou negam o tráfego de rede para suas instâncias de VM em uma Rede Virtual. Os NSGs podem ser associados a sub-redes ou instâncias de VM individuais dentro dessa sub-rede. Quando um NSG é associado a uma sub-rede, as regras de ACL se aplicam a todas as instâncias de VM na sub-rede. Além disso, o tráfego para uma VM individual pode ser restrito ainda mais por meio da associação de um NSG diretamente à VM. Para saber mais, confira [O que é um NSG (Grupo de Segurança de Rede)?](../virtual-network/virtual-networks-nsg.md)

Se você não tiver NSGs habilitados, a Central de Segurança apresentará duas recomendações: Habilitar Grupos de Segurança de Rede em sub-redes e Habilitar Grupos de Segurança de Rede em máquinas virtuais. Você escolhe a qual nível, sub-rede ou VM aplicar NSGs.

> [!NOTE]
> Este documento apresenta o serviço usando uma implantação de exemplo.  Ela não é um guia passo a passo.
>
>

## <a name="implement-the-recommendation"></a>Implementar a recomendação
1. Na folha **Recomendações**, selecione **Habilitar Grupos de Segurança de Rede** em sub-redes ou em máquinas virtuais.
   ![Habilitar Grupos de segurança de rede][1]
2. Isso abrirá a folha **Configurar Grupos de Segurança de Rede Ausentes** para sub-redes ou para máquinas virtuais, dependendo da recomendação que você selecionou. Selecione uma sub-rede ou máquina virtual para configurar um NSG.

   ![Configurar NSG para sub-rede][2]

   ![Configurar NSG para VM][3]
3. Na folha **Escolher grupo de segurança de rede**, selecione um NSG existente ou selecione para **Criar novo** para criar um novo NSG.

   ![Escolher grupo de segurança de rede][4]

Se você criar um novo NSG, siga as etapas em [Como gerenciar NSGs usando o portal do Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) para criar um NSG e definir regras de segurança.

## <a name="see-also"></a>Consulte também
Este artigo mostrou como implementar a recomendação da Central de Segurança "Habilitar Grupos de Segurança de Rede" para máquinas virtuais ou sub-redes. Para saber mais sobre como habilitar NSGs, confira o seguinte:

* [O que é um NSG (grupo de segurança de rede)?](../virtual-network/virtual-networks-nsg.md)
* [Como gerenciar NSGs usando o portal do Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

Para saber mais sobre a Central de Segurança, confira o seguinte:

* [Configurando políticas de segurança na Central de Segurança do Azure](security-center-policies.md) – saiba como configurar políticas de segurança para suas assinaturas e grupos de recursos do Azure.
* [Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.
* [Monitoramento de integridade de segurança na Central de Segurança do Azure](security-center-monitoring.md) : saiba como monitorar a integridade dos recursos do Azure.
* [Gerenciando e respondendo a alertas de segurança na Central de Segurança do Azure](security-center-managing-and-responding-alerts.md) : aprenda a gerenciar e a responder a alertas de segurança.
* [Monitoramento de soluções de parceiros com a Central de Segurança do Azure](security-center-partner-solutions.md) – saiba como monitorar o status de integridade de suas soluções de parceiro.
* [Perguntas frequentes sobre a Central de Segurança do Azure](security-center-faq.md) : encontre as perguntas frequentes sobre como usar o serviço de localização.
* [Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) : obtenha as últimas notícias de segurança e informações do Azure.

<!--Image references-->
[1]: ./media/security-center-enable-nsg/enable-nsg.png
[2]:./media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: ./media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: ./media/security-center-enable-nsg/choose-nsg.png
