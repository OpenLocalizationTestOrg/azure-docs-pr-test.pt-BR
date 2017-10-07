---
title: "toovertically de automação do Azure aaaUse escala de máquinas virtuais do Windows | Microsoft Docs"
description: "Expandir verticalmente uma máquina Virtual do Windows em alertas de toomonitoring de resposta na automação do Azure"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4f964713-fb67-4bcc-8246-3431452ddf7d
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/29/2016
ms.author: kasing
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 24d07f3e2e217668f18676e6d6873be4f9770349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="vertically-scale-windows-vms-with-azure-automation"></a>Escalar verticalmente as VMs do Windows com a Automação do Azure

Dimensionamento vertical é o processo de saudação de aumentar ou diminuir os recursos de saudação de um computador na carga de trabalho de toohello de resposta. No Azure, isso pode ser feito alterando o tamanho de saudação do hello Máquina Virtual. Isso pode ajudar os seguintes cenários de saudação

* Se Olá Máquina Virtual não está sendo usado com frequência, você pode redimensioná-la para baixo tooa menor tamanho tooreduce os custos mensais
* Se Olá Máquina Virtual está vendo uma carga de pico, ele pode ser redimensionada tooa maior tamanho tooincrease sua capacidade

tópicos Olá Olá etapas tooaccomplish trata como abaixo

1. Instalação de automação do Azure tooaccess suas máquinas virtuais
2. Importar runbooks do hello escala Vertical de automação do Azure para sua assinatura
3. Adicionar um runbook de tooyour do webhook
4. Adicionar um alerta tooyour Máquina Virtual

> [!NOTE]
> Devido ao tamanho de saudação do hello primeira Máquina Virtual, ele pode ser dimensionado, de tamanhos de saudação poderá ficar limitado devido a disponibilidade de toohello de saudação outros tamanhos de cluster Olá atual Máquina Virtual é implantada no. Olá publicadas runbooks de automação usados neste artigo, podemos cuidar da ocorrência e dimensionar somente dentro de saudação abaixo pares de tamanho VM. Isso significa que uma máquina Virtual de Standard_D1v2 não repentinamente ser aumentadas tooStandard_G5 ou tooBasic_A0 foi reduzido.
> 
> | Par de dimensionamento de tamanhos de VM |  |
> | --- | --- |
> | Basic_A0 |Basic_A4 |
> | Standard_A0 |Standard_A4 |
> | Standard_A5 |Standard_A7 |
> | Standard_A8 |Standard_A9 |
> | Standard_A10 |Standard_A11 |
> | Standard_D1 |Standard_D4 |
> | Standard_D11 |Standard_D14 |
> | Standard_DS1 |Standard_DS4 |
> | Standard_DS11 |Standard_DS14 |
> | Standard_D1v2 |Standard_D5v2 |
> | Standard_D11v2 |Standard_D14v2 |
> | Standard_G1 |Standard_G5 |
> | Standard_GS1 |Standard_GS5 |
> 
> 

## <a name="setup-azure-automation-tooaccess-your-virtual-machines"></a>Instalação de automação do Azure tooaccess suas máquinas virtuais
Olá primeira coisa toodo é criar uma conta de automação do Azure que hospedará Olá runbooks usado tooscale uma máquina Virtual. Serviço de automação Olá introduzidos recentemente recurso "Executar como conta" hello que torna Configurando Olá entidade de serviço para execução automática Olá runbooks em nome do usuário Olá muito fácil. Você pode ler mais sobre isso em um artigo de saudação abaixo:

* [Autenticar Runbooks com uma conta Executar como do Azure](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-hello-azure-automation-vertical-scale-runbooks-into-your-subscription"></a>Importar runbooks do hello escala Vertical de automação do Azure para sua assinatura
Olá runbooks que são necessários para escalar verticalmente sua máquina Virtual já estão publicados em Olá Galeria de Runbook de automação do Azure. Você precisará tooimport-los em sua assinatura. Você pode aprender como runbooks tooimport lendo Olá artigo a seguir.

* [Galerias de runbook e de módulos para a Automação do Azure](../../automation/automation-runbook-gallery.md)

Olá runbooks que precisam toobe importado são mostrados na imagem de saudação abaixo

![Importar Runbooks](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-tooyour-runbook"></a>Adicionar um runbook de tooyour do webhook
Depois de importar runbooks Olá precisará tooadd um runbook de toohello webhook para que ele pode ser acionado por um alerta de uma máquina Virtual. detalhes de saudação da criação de um webhook para seu Runbook podem ser lido aqui

* [Webhooks da Automação do Azure](../../automation/automation-webhooks.md)

Certifique-se de que copiar Olá webhook antes de fechar a caixa de diálogo de webhook hello como ele será necessário na próxima seção, Olá.

## <a name="add-an-alert-tooyour-virtual-machine"></a>Adicionar um alerta tooyour Máquina Virtual
1. Selecione Configurações da Máquina Virtual
2. Selecione “Regras de alerta”
3. Selecione “Adicionar alerta”
4. Selecione um alerta de saudação toofire métrica em
5. Selecione uma condição que, quando atendida será causar toofire alerta Olá
6. Selecione um limite para a condição de saudação na etapa 5. toobe atendida
7. Selecionar um período sobre quais Olá monitorando o serviço irá verificar para a condição de saudação e limite as etapas 5 e 6
8. Cole o webhook Olá copiada da seção anterior hello.

![Adicionar alerta tooVirtual máquina 1](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![Adicionar alerta tooVirtual Machine 2](./media/vertical-scaling-automation/add-alert-webhook-2.png)

