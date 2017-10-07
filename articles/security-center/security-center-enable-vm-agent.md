---
title: "aaaEnable agente de VM na Central de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá recomendação da Central de segurança do Azure * * habilitar o VM Agent * *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 5b431c25-4241-45b7-9556-cf2a1956f3da
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 9bd71e638b020780537da25fd4cf7baf34d3e11a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-vm-agent-in-azure-security-center"></a>Habilitar o Agente de VM na Central de Segurança do Azure
Olá VM Agent deve ser instalado em máquinas virtuais (VMs) na ordem muito[habilitar coleta de dados](security-center-enable-data-collection.md).  Habilita a Central de segurança do Azure você toosee que exigem VMs Olá agente de VM e recomendará que você habilite Olá agente de VM nessas VMs.

Olá agente VM é instalado por padrão para VMs que são implantados de saudação do Azure Marketplace. artigo Olá [agente de VM e extensões – parte 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) fornece informações sobre como tooinstall Olá agente de VM.

> [!NOTE]
> Este documento apresenta serviço hello usando um exemplo de implantação. Ela não é um guia passo a passo.
>
>

## <a name="implement-hello-recommendation"></a>Implementar a recomendação de saudação
1. Em Olá **folha recomendações**, selecione **habilitar o agente de VM**.
   ![Habilitar o Agente de VM][1]
2. Isso abre a folha de saudação **VM Agent está ausente ou não respondendo**. Esta folha lista Olá máquinas virtuais que exigem Olá agente de VM. Siga as instruções de saudação no agente de VM Olá folha tooinstall hello.
   ![O Agente de VM está ausente][2]

## <a name="see-also"></a>Consulte também
toolearn mais sobre o Centro de segurança, consulte o seguinte hello:

* [Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md)– Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.
* [Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md): saiba como as recomendações ajudam a proteger os recursos do Azure.
* [Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md)– Saiba como toomonitor Olá a integridade de seus recursos do Azure.
* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md)– Saiba como alertas de toosecurity toomanage e responder.
* [Soluções de parceiro com a Central de segurança do Azure de monitoramento](security-center-partner-solutions.md) – Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md)– localizar perguntas frequentes sobre como usar o serviço de saudação.
* [Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/)– obter notícias mais recentes de segurança do Azure hello e informações.

<!--Image references-->
[1]: ./media/security-center-enable-vm-agent/enable-vm-agent.png
[2]: ./media/security-center-enable-vm-agent/vm-agent-is-missing.png
