---
title: "aaaUsing SAP em máquinas virtuais do Windows | Microsoft Docs"
description: "Saiba como usar o SAP em VMs (máquinas virtuais) do Windows no Microsoft Azure"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: MSSedusch
manager: timlt
editor: 
tags: azure-service-management
keywords: 
ms.assetid: 1b455be4-c02f-43e3-8d39-c2d5f216e646
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: campaign-page
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 10/04/2016
ms.author: sedusch
ms.openlocfilehash: 6c4d8a066a4a8805668e78e67fd2110f2000ee75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-sap-on-windows-virtual-machines-in-azure"></a>Usando o SAP em máquinas virtuais do Windows
Computação em nuvem é um termo amplamente usado que está adquirindo cada vez mais importância no hello setor de TI de empresas de pequenas porte a empresas toolarge e multinacional. Microsoft Azure é hello plataforma de serviços de nuvem da Microsoft que oferece uma ampla variedade de novas possibilidades. Agora, os clientes estão toorapidly capaz de provisionar e provisionamento de aplicativos como serviços de nuvem, para que eles não são limitado tootechnical ou restrições de orçamentos. Em vez de investir tempo e dinheiro na infraestrutura de hardware, as empresas podem concentrar no aplicativo hello, processos de negócios e seus benefícios para os clientes e usuários.

Com as máquinas virtuais do Microsoft Azure, a Microsoft oferece uma plataforma abrangente de IaaS (Infraestrutura como Serviço). Os aplicativos baseados no SAP NetWeaver têm suporte em Máquinas Virtuais do Azure (IaaS). Olá white papers abaixo descrevem como tooplan e implementar SAP NetWeaver com base em aplicativos em máquinas virtuais do Windows no Azure. Você também pode implementar aplicativos baseados no SAP NetWeaver em [máquinas virtuais do Linux](../../linux/classic/sap-get-started.md).

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure---ha"></a>SAP NetWeaver no Azure - HA
título: aaaSAP NetWeaver no Azure – Clustering SAP ASCS/SCS instâncias usando o Cluster de Failover do Windows Server no Azure com SIOS DataKeeper

Resumo: ' Este documento descreve como toouse SIOS DataKeeper tooset uma configuração altamente disponível do SAP ASCS/SCS no Azure. O SAP protege seus componentes de ponto único de falha, como o SAP ASCS/SCS ou o Enqueue Replication Services, com configurações de Cluster de Failover do Windows Server que exigem discos compartilhados. Esses componentes SAP são essenciais para a funcionalidade de saudação de um sistema SAP. Portanto, necessidades de funcionalidade de alta disponibilidade toobe colocar em colocar toomake-se de que os componentes possam sustentar uma falha de um servidor ou em uma VM como feito com configurações de Cluster do Windows para ambientes de Hyper-V e bare-metal. A partir de agosto de 2015 próprio Azure não pode fornecer discos compartilhados que seriam necessários para o Windows hello com base em configurações de alta disponibilidade necessárias para esses componentes essenciais do SAP. No entanto com a Ajuda de saudação do produto Olá DataKeeper por SIOS, as configurações conforme necessário para SAP ASCS/SCS do Cluster de Failover do Windows Server podem ser criadas na plataforma do Azure IaaS hello. Este documento descreve uma abordagem passo a passo como tooinstall uma configuração de Cluster de Failover do Windows Server com disco compartilhado fornecido pelo SIOS Datakeeper no Azure. Olá artigo explica detalhes em configurações no lado hello Azure, Windows e SAP que torna a configuração de alta disponibilidade Olá funcionam de forma ideal. Olá papel complementa Olá documentação de instalação do SAP e observações sobre o SAP que representam os recursos principais de saudação para instalações e implantações de software SAP em fornecidos plataformas.

Atualização: agosto de 2015

[Baixar este guia agora](http://go.microsoft.com/fwlink/?LinkId=613056)

