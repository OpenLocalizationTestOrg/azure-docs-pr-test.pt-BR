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
# <a name="vertically-scale-windows-vms-with-azure-automation"></a><span data-ttu-id="e63e5-103">Escalar verticalmente as VMs do Windows com a Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="e63e5-103">Vertically scale Windows VMs with Azure Automation</span></span>

<span data-ttu-id="e63e5-104">Dimensionamento vertical é o processo de saudação de aumentar ou diminuir os recursos de saudação de um computador na carga de trabalho de toohello de resposta.</span><span class="sxs-lookup"><span data-stu-id="e63e5-104">Vertical scaling is hello process of increasing or decreasing hello resources of a machine in response toohello workload.</span></span> <span data-ttu-id="e63e5-105">No Azure, isso pode ser feito alterando o tamanho de saudação do hello Máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="e63e5-105">In Azure this can be accomplished by changing hello size of hello Virtual Machine.</span></span> <span data-ttu-id="e63e5-106">Isso pode ajudar os seguintes cenários de saudação</span><span class="sxs-lookup"><span data-stu-id="e63e5-106">This can help in hello following scenarios</span></span>

* <span data-ttu-id="e63e5-107">Se Olá Máquina Virtual não está sendo usado com frequência, você pode redimensioná-la para baixo tooa menor tamanho tooreduce os custos mensais</span><span class="sxs-lookup"><span data-stu-id="e63e5-107">If hello Virtual Machine is not being used frequently, you can resize it down tooa smaller size tooreduce your monthly costs</span></span>
* <span data-ttu-id="e63e5-108">Se Olá Máquina Virtual está vendo uma carga de pico, ele pode ser redimensionada tooa maior tamanho tooincrease sua capacidade</span><span class="sxs-lookup"><span data-stu-id="e63e5-108">If hello Virtual Machine is seeing a peak load, it can be resized tooa larger size tooincrease its capacity</span></span>

<span data-ttu-id="e63e5-109">tópicos Olá Olá etapas tooaccomplish trata como abaixo</span><span class="sxs-lookup"><span data-stu-id="e63e5-109">hello outline for hello steps tooaccomplish this is as below</span></span>

1. <span data-ttu-id="e63e5-110">Instalação de automação do Azure tooaccess suas máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="e63e5-110">Setup Azure Automation tooaccess your Virtual Machines</span></span>
2. <span data-ttu-id="e63e5-111">Importar runbooks do hello escala Vertical de automação do Azure para sua assinatura</span><span class="sxs-lookup"><span data-stu-id="e63e5-111">Import hello Azure Automation Vertical Scale runbooks into your subscription</span></span>
3. <span data-ttu-id="e63e5-112">Adicionar um runbook de tooyour do webhook</span><span class="sxs-lookup"><span data-stu-id="e63e5-112">Add a webhook tooyour runbook</span></span>
4. <span data-ttu-id="e63e5-113">Adicionar um alerta tooyour Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="e63e5-113">Add an alert tooyour Virtual Machine</span></span>

> [!NOTE]
> <span data-ttu-id="e63e5-114">Devido ao tamanho de saudação do hello primeira Máquina Virtual, ele pode ser dimensionado, de tamanhos de saudação poderá ficar limitado devido a disponibilidade de toohello de saudação outros tamanhos de cluster Olá atual Máquina Virtual é implantada no.</span><span class="sxs-lookup"><span data-stu-id="e63e5-114">Because of hello size of hello first Virtual Machine, hello sizes it can be scaled to, may be limited due toohello availability of hello other sizes in hello cluster current Virtual Machine is deployed in.</span></span> <span data-ttu-id="e63e5-115">Olá publicadas runbooks de automação usados neste artigo, podemos cuidar da ocorrência e dimensionar somente dentro de saudação abaixo pares de tamanho VM.</span><span class="sxs-lookup"><span data-stu-id="e63e5-115">In hello published automation runbooks used in this article we take care of this case and only scale within hello below VM size pairs.</span></span> <span data-ttu-id="e63e5-116">Isso significa que uma máquina Virtual de Standard_D1v2 não repentinamente ser aumentadas tooStandard_G5 ou tooBasic_A0 foi reduzido.</span><span class="sxs-lookup"><span data-stu-id="e63e5-116">This means that a Standard_D1v2 Virtual Machine will not suddenly be scaled up tooStandard_G5 or scaled down tooBasic_A0.</span></span>
> 
> | <span data-ttu-id="e63e5-117">Par de dimensionamento de tamanhos de VM</span><span class="sxs-lookup"><span data-stu-id="e63e5-117">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="e63e5-118">Basic_A0</span><span class="sxs-lookup"><span data-stu-id="e63e5-118">Basic_A0</span></span> |<span data-ttu-id="e63e5-119">Basic_A4</span><span class="sxs-lookup"><span data-stu-id="e63e5-119">Basic_A4</span></span> |
> | <span data-ttu-id="e63e5-120">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="e63e5-120">Standard_A0</span></span> |<span data-ttu-id="e63e5-121">Standard_A4</span><span class="sxs-lookup"><span data-stu-id="e63e5-121">Standard_A4</span></span> |
> | <span data-ttu-id="e63e5-122">Standard_A5</span><span class="sxs-lookup"><span data-stu-id="e63e5-122">Standard_A5</span></span> |<span data-ttu-id="e63e5-123">Standard_A7</span><span class="sxs-lookup"><span data-stu-id="e63e5-123">Standard_A7</span></span> |
> | <span data-ttu-id="e63e5-124">Standard_A8</span><span class="sxs-lookup"><span data-stu-id="e63e5-124">Standard_A8</span></span> |<span data-ttu-id="e63e5-125">Standard_A9</span><span class="sxs-lookup"><span data-stu-id="e63e5-125">Standard_A9</span></span> |
> | <span data-ttu-id="e63e5-126">Standard_A10</span><span class="sxs-lookup"><span data-stu-id="e63e5-126">Standard_A10</span></span> |<span data-ttu-id="e63e5-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="e63e5-127">Standard_A11</span></span> |
> | <span data-ttu-id="e63e5-128">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="e63e5-128">Standard_D1</span></span> |<span data-ttu-id="e63e5-129">Standard_D4</span><span class="sxs-lookup"><span data-stu-id="e63e5-129">Standard_D4</span></span> |
> | <span data-ttu-id="e63e5-130">Standard_D11</span><span class="sxs-lookup"><span data-stu-id="e63e5-130">Standard_D11</span></span> |<span data-ttu-id="e63e5-131">Standard_D14</span><span class="sxs-lookup"><span data-stu-id="e63e5-131">Standard_D14</span></span> |
> | <span data-ttu-id="e63e5-132">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="e63e5-132">Standard_DS1</span></span> |<span data-ttu-id="e63e5-133">Standard_DS4</span><span class="sxs-lookup"><span data-stu-id="e63e5-133">Standard_DS4</span></span> |
> | <span data-ttu-id="e63e5-134">Standard_DS11</span><span class="sxs-lookup"><span data-stu-id="e63e5-134">Standard_DS11</span></span> |<span data-ttu-id="e63e5-135">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="e63e5-135">Standard_DS14</span></span> |
> | <span data-ttu-id="e63e5-136">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="e63e5-136">Standard_D1v2</span></span> |<span data-ttu-id="e63e5-137">Standard_D5v2</span><span class="sxs-lookup"><span data-stu-id="e63e5-137">Standard_D5v2</span></span> |
> | <span data-ttu-id="e63e5-138">Standard_D11v2</span><span class="sxs-lookup"><span data-stu-id="e63e5-138">Standard_D11v2</span></span> |<span data-ttu-id="e63e5-139">Standard_D14v2</span><span class="sxs-lookup"><span data-stu-id="e63e5-139">Standard_D14v2</span></span> |
> | <span data-ttu-id="e63e5-140">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="e63e5-140">Standard_G1</span></span> |<span data-ttu-id="e63e5-141">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="e63e5-141">Standard_G5</span></span> |
> | <span data-ttu-id="e63e5-142">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="e63e5-142">Standard_GS1</span></span> |<span data-ttu-id="e63e5-143">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="e63e5-143">Standard_GS5</span></span> |
> 
> 

## <a name="setup-azure-automation-tooaccess-your-virtual-machines"></a><span data-ttu-id="e63e5-144">Instalação de automação do Azure tooaccess suas máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="e63e5-144">Setup Azure Automation tooaccess your Virtual Machines</span></span>
<span data-ttu-id="e63e5-145">Olá primeira coisa toodo é criar uma conta de automação do Azure que hospedará Olá runbooks usado tooscale uma máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="e63e5-145">hello first thing you need toodo is create an Azure Automation account that will host hello runbooks used tooscale a Virtual Machine.</span></span> <span data-ttu-id="e63e5-146">Serviço de automação Olá introduzidos recentemente recurso "Executar como conta" hello que torna Configurando Olá entidade de serviço para execução automática Olá runbooks em nome do usuário Olá muito fácil.</span><span class="sxs-lookup"><span data-stu-id="e63e5-146">Recently hello Automation service introduced hello "Run As account" feature which makes setting up hello Service Principal for automatically running hello runbooks on hello user's behalf very easy.</span></span> <span data-ttu-id="e63e5-147">Você pode ler mais sobre isso em um artigo de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="e63e5-147">You can read more about this in hello article below:</span></span>

* [<span data-ttu-id="e63e5-148">Autenticar Runbooks com uma conta Executar como do Azure</span><span class="sxs-lookup"><span data-stu-id="e63e5-148">Authenticate Runbooks with Azure Run As account</span></span>](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-hello-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="e63e5-149">Importar runbooks do hello escala Vertical de automação do Azure para sua assinatura</span><span class="sxs-lookup"><span data-stu-id="e63e5-149">Import hello Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="e63e5-150">Olá runbooks que são necessários para escalar verticalmente sua máquina Virtual já estão publicados em Olá Galeria de Runbook de automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="e63e5-150">hello runbooks that are needed for Vertically Scaling your Virtual Machine are already published in hello Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="e63e5-151">Você precisará tooimport-los em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="e63e5-151">You will need tooimport them into your subscription.</span></span> <span data-ttu-id="e63e5-152">Você pode aprender como runbooks tooimport lendo Olá artigo a seguir.</span><span class="sxs-lookup"><span data-stu-id="e63e5-152">You can learn how tooimport runbooks by reading hello following article.</span></span>

* [<span data-ttu-id="e63e5-153">Galerias de runbook e de módulos para a Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="e63e5-153">Runbook and module galleries for Azure Automation</span></span>](../../automation/automation-runbook-gallery.md)

<span data-ttu-id="e63e5-154">Olá runbooks que precisam toobe importado são mostrados na imagem de saudação abaixo</span><span class="sxs-lookup"><span data-stu-id="e63e5-154">hello runbooks that need toobe imported are shown in hello image below</span></span>

![Importar Runbooks](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-tooyour-runbook"></a><span data-ttu-id="e63e5-156">Adicionar um runbook de tooyour do webhook</span><span class="sxs-lookup"><span data-stu-id="e63e5-156">Add a webhook tooyour runbook</span></span>
<span data-ttu-id="e63e5-157">Depois de importar runbooks Olá precisará tooadd um runbook de toohello webhook para que ele pode ser acionado por um alerta de uma máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="e63e5-157">Once you've imported hello runbooks you'll need tooadd a webhook toohello runbook so it can be triggered by an alert from a Virtual Machine.</span></span> <span data-ttu-id="e63e5-158">detalhes de saudação da criação de um webhook para seu Runbook podem ser lido aqui</span><span class="sxs-lookup"><span data-stu-id="e63e5-158">hello details of creating a webhook for your Runbook can be read here</span></span>

* [<span data-ttu-id="e63e5-159">Webhooks da Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="e63e5-159">Azure Automation webhooks</span></span>](../../automation/automation-webhooks.md)

<span data-ttu-id="e63e5-160">Certifique-se de que copiar Olá webhook antes de fechar a caixa de diálogo de webhook hello como ele será necessário na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="e63e5-160">Make sure you copy hello webhook before closing hello webhook dialog as you will need this in hello next section.</span></span>

## <a name="add-an-alert-tooyour-virtual-machine"></a><span data-ttu-id="e63e5-161">Adicionar um alerta tooyour Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="e63e5-161">Add an alert tooyour Virtual Machine</span></span>
1. <span data-ttu-id="e63e5-162">Selecione Configurações da Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="e63e5-162">Select Virtual Machine settings</span></span>
2. <span data-ttu-id="e63e5-163">Selecione “Regras de alerta”</span><span class="sxs-lookup"><span data-stu-id="e63e5-163">Select "Alert rules"</span></span>
3. <span data-ttu-id="e63e5-164">Selecione “Adicionar alerta”</span><span class="sxs-lookup"><span data-stu-id="e63e5-164">Select "Add alert"</span></span>
4. <span data-ttu-id="e63e5-165">Selecione um alerta de saudação toofire métrica em</span><span class="sxs-lookup"><span data-stu-id="e63e5-165">Select a metric toofire hello alert on</span></span>
5. <span data-ttu-id="e63e5-166">Selecione uma condição que, quando atendida será causar toofire alerta Olá</span><span class="sxs-lookup"><span data-stu-id="e63e5-166">Select a condition, which when fulfilled will cause hello alert toofire</span></span>
6. <span data-ttu-id="e63e5-167">Selecione um limite para a condição de saudação na etapa 5.</span><span class="sxs-lookup"><span data-stu-id="e63e5-167">Select a threshold for hello condition in Step 5.</span></span> <span data-ttu-id="e63e5-168">toobe atendida</span><span class="sxs-lookup"><span data-stu-id="e63e5-168">toobe fulfilled</span></span>
7. <span data-ttu-id="e63e5-169">Selecionar um período sobre quais Olá monitorando o serviço irá verificar para a condição de saudação e limite as etapas 5 e 6</span><span class="sxs-lookup"><span data-stu-id="e63e5-169">Select a period over which hello monitoring service will check for hello condition and threshold in Steps 5 & 6</span></span>
8. <span data-ttu-id="e63e5-170">Cole o webhook Olá copiada da seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="e63e5-170">Paste in hello webhook you copied from hello previous section.</span></span>

![Adicionar alerta tooVirtual máquina 1](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![Adicionar alerta tooVirtual Machine 2](./media/vertical-scaling-automation/add-alert-webhook-2.png)

