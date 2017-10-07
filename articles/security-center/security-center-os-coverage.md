---
title: "plataformas aaaSupported na Central de segurança do Azure | Microsoft Docs"
description: "Este documento fornece uma lista de sistemas operacionais Windows e Linux com suporte na Central de Segurança do Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: f73e04970749271fc9d75836f4f468b0a4953f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="supported-platforms-in-azure-security-center"></a>Plataformas com suporte na Central de Segurança do Azure
Monitoramento de estado de segurança e as recomendações estão disponíveis para máquinas virtuais (VMs) criadas usando Olá clássico e modelos de implantação do Gerenciador de recursos.

> [!NOTE]
> Saiba mais sobre Olá [clássico e modelos de implantação do Gerenciador de recursos](../azure-classic-rm.md) para recursos do Azure.
>
>

## <a name="supported-platforms-for-windows-vms"></a>Plataformas com suporte para VMs do Windows
Sistemas operacionais Windows com suporte:

* Windows Server 2008
* Windows Server 2008 R2
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

> [!NOTE]
>
* Avaliações de vulnerabilidade do sistema operacional ainda não estão disponíveis para o Windows Server 2016.
* Detecções de análise de falha só têm suporte no Windows Server 2012 e Windows Server 2012 R2.
>
>

## <a name="supported-platforms-for-linux-vms"></a>Plataformas com suporte para VMs Linux
Sistemas operacionais Linux com suporte:

* Ubuntu versões 12.04, 14.04, 16.04, 16.10
* Debian versões 7, 8
* CentOS versões 6.\*, 7.*
* Red Hat Enterprise Linux (RHEL) versões 6.\*, 7.*
* SUSE Linux Enterprise Server (SLES) versões 11.SP4+, 12.*
* Oracle Linux versões 6.\*, 7. *

> [!NOTE]
> A análise de comportamento de máquina virtual ainda não está disponível para sistemas operacionais Linux.
>
>

## <a name="vms-and-cloud-services"></a>VMs e Serviços de Nuvem
Também há suporte para VMs em execução em um serviço de nuvem. Apenas serviços de nuvem da Web e funções de trabalho em execução em slots de produção são monitorados. toolearn mais sobre o serviço de nuvem, consulte [visão geral dos serviços de nuvem](../cloud-services/cloud-services-choose-me.md).

## <a name="next-steps"></a>Próximas etapas

- [Planejamento da Central de segurança do Azure e guia de operações](security-center-planning-and-operations-guide.md) — Saiba como tooplan e entender a Central de segurança do hello design considerações tooadopt do Azure
- [Alertas de segurança por tipo na Central de segurança do Azure](https://docs.microsoft.com/en-us/azure/security-center/security-center-alerts-type.md#virtual-machine-behavioral-analysis) – Saiba mais sobre a análise comportamental da máquina virtual e análise de memória de despejo de memória na Central de Segurança
- [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) — localizar perguntas frequentes sobre como usar o serviço de saudação
- [Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – encontre postagens no blog sobre conformidade e segurança do Azure
