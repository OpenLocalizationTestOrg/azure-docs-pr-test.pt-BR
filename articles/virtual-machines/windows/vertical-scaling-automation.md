---
title: "Usar a Automação do Azure para escalar verticalmente as máquinas virtuais do Windows | Microsoft Docs"
description: "Escalar verticalmente uma máquina virtual do Windows em resposta aos alertas de monitoramento com a Automação do Azure"
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
ms.openlocfilehash: ea5169c1a95f00e78ae3f5f177812466eb7a0deb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="vertically-scale-windows-vms-with-azure-automation"></a><span data-ttu-id="d9e0d-103">Escalar verticalmente as VMs do Windows com a Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="d9e0d-103">Vertically scale Windows VMs with Azure Automation</span></span>

<span data-ttu-id="d9e0d-104">A escala vertical é o processo de aumentar ou diminuir os recursos de um computador em resposta à carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d9e0d-104">Vertical scaling is the process of increasing or decreasing the resources of a machine in response to the workload.</span></span> <span data-ttu-id="d9e0d-105">No Azure, isso pode ser feito alterando o tamanho da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d9e0d-105">In Azure this can be accomplished by changing the size of the Virtual Machine.</span></span> <span data-ttu-id="d9e0d-106">Isso pode ajudar nos cenários a seguir</span><span class="sxs-lookup"><span data-stu-id="d9e0d-106">This can help in the following scenarios</span></span>

* <span data-ttu-id="d9e0d-107">Se a máquina virtual não está sendo usado com frequência, você pode redimensioná-la para um tamanho menor, a fim de reduzir os custos mensais</span><span class="sxs-lookup"><span data-stu-id="d9e0d-107">If the Virtual Machine is not being used frequently, you can resize it down to a smaller size to reduce your monthly costs</span></span>
* <span data-ttu-id="d9e0d-108">Se a máquina virtual está enfrentando um pico de carga, ela pode ser redimensionada para um tamanho maior, a fim de aumentar sua capacidade</span><span class="sxs-lookup"><span data-stu-id="d9e0d-108">If the Virtual Machine is seeing a peak load, it can be resized to a larger size to increase its capacity</span></span>

<span data-ttu-id="d9e0d-109">Veja abaixo a descrição das etapas para fazer isso</span><span class="sxs-lookup"><span data-stu-id="d9e0d-109">The outline for the steps to accomplish this is as below</span></span>

1. <span data-ttu-id="d9e0d-110">Configurar a Automação do Azure para acessar suas máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="d9e0d-110">Setup Azure Automation to access your Virtual Machines</span></span>
2. <span data-ttu-id="d9e0d-111">Importar os runbooks de Escala Vertical da Automação do Azure para sua assinatura</span><span class="sxs-lookup"><span data-stu-id="d9e0d-111">Import the Azure Automation Vertical Scale runbooks into your subscription</span></span>
3. <span data-ttu-id="d9e0d-112">Adicionar um webhook ao seu Runbook</span><span class="sxs-lookup"><span data-stu-id="d9e0d-112">Add a webhook to your runbook</span></span>
4. <span data-ttu-id="d9e0d-113">Adicionar um alerta à sua máquina virtual</span><span class="sxs-lookup"><span data-stu-id="d9e0d-113">Add an alert to your Virtual Machine</span></span>

> [!NOTE]
> <span data-ttu-id="d9e0d-114">Devido ao tamanho da primeira máquina virtual, os tamanhos para expansão podem ser limitados devido à disponibilidade de outros tamanhos no cluster em que a máquina virtual atual está implantada.</span><span class="sxs-lookup"><span data-stu-id="d9e0d-114">Because of the size of the first Virtual Machine, the sizes it can be scaled to, may be limited due to the availability of the other sizes in the cluster current Virtual Machine is deployed in.</span></span> <span data-ttu-id="d9e0d-115">Nos Runbooks de automação publicados usados neste artigo, levamos isso em conta e dimensionamos apenas dentro dos pares de tamanhos da VM abaixo.</span><span class="sxs-lookup"><span data-stu-id="d9e0d-115">In the published automation runbooks used in this article we take care of this case and only scale within the below VM size pairs.</span></span> <span data-ttu-id="d9e0d-116">Isso significa que uma máquina virtual Standard_D1v2 não será expandida repentinamente para Standard_G5 ou reduzida para Basic_A0.</span><span class="sxs-lookup"><span data-stu-id="d9e0d-116">This means that a Standard_D1v2 Virtual Machine will not suddenly be scaled up to Standard_G5 or scaled down to Basic_A0.</span></span>
> 
> | <span data-ttu-id="d9e0d-117">Par de dimensionamento de tamanhos de VM</span><span class="sxs-lookup"><span data-stu-id="d9e0d-117">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="d9e0d-118">Basic_A0</span><span class="sxs-lookup"><span data-stu-id="d9e0d-118">Basic_A0</span></span> |<span data-ttu-id="d9e0d-119">Basic_A4</span><span class="sxs-lookup"><span data-stu-id="d9e0d-119">Basic_A4</span></span> |
> | <span data-ttu-id="d9e0d-120">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="d9e0d-120">Standard_A0</span></span> |<span data-ttu-id="d9e0d-121">Standard_A4</span><span class="sxs-lookup"><span data-stu-id="d9e0d-121">Standard_A4</span></span> |
> | <span data-ttu-id="d9e0d-122">Standard_A5</span><span class="sxs-lookup"><span data-stu-id="d9e0d-122">Standard_A5</span></span> |<span data-ttu-id="d9e0d-123">Standard_A7</span><span class="sxs-lookup"><span data-stu-id="d9e0d-123">Standard_A7</span></span> |
> | <span data-ttu-id="d9e0d-124">Standard_A8</span><span class="sxs-lookup"><span data-stu-id="d9e0d-124">Standard_A8</span></span> |<span data-ttu-id="d9e0d-125">Standard_A9</span><span class="sxs-lookup"><span data-stu-id="d9e0d-125">Standard_A9</span></span> |
> | <span data-ttu-id="d9e0d-126">Standard_A10</span><span class="sxs-lookup"><span data-stu-id="d9e0d-126">Standard_A10</span></span> |<span data-ttu-id="d9e0d-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="d9e0d-127">Standard_A11</span></span> |
> | <span data-ttu-id="d9e0d-128">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="d9e0d-128">Standard_D1</span></span> |<span data-ttu-id="d9e0d-129">Standard_D4</span><span class="sxs-lookup"><span data-stu-id="d9e0d-129">Standard_D4</span></span> |
> | <span data-ttu-id="d9e0d-130">Standard_D11</span><span class="sxs-lookup"><span data-stu-id="d9e0d-130">Standard_D11</span></span> |<span data-ttu-id="d9e0d-131">Standard_D14</span><span class="sxs-lookup"><span data-stu-id="d9e0d-131">Standard_D14</span></span> |
> | <span data-ttu-id="d9e0d-132">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="d9e0d-132">Standard_DS1</span></span> |<span data-ttu-id="d9e0d-133">Standard_DS4</span><span class="sxs-lookup"><span data-stu-id="d9e0d-133">Standard_DS4</span></span> |
> | <span data-ttu-id="d9e0d-134">Standard_DS11</span><span class="sxs-lookup"><span data-stu-id="d9e0d-134">Standard_DS11</span></span> |<span data-ttu-id="d9e0d-135">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="d9e0d-135">Standard_DS14</span></span> |
> | <span data-ttu-id="d9e0d-136">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="d9e0d-136">Standard_D1v2</span></span> |<span data-ttu-id="d9e0d-137">Standard_D5v2</span><span class="sxs-lookup"><span data-stu-id="d9e0d-137">Standard_D5v2</span></span> |
> | <span data-ttu-id="d9e0d-138">Standard_D11v2</span><span class="sxs-lookup"><span data-stu-id="d9e0d-138">Standard_D11v2</span></span> |<span data-ttu-id="d9e0d-139">Standard_D14v2</span><span class="sxs-lookup"><span data-stu-id="d9e0d-139">Standard_D14v2</span></span> |
> | <span data-ttu-id="d9e0d-140">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="d9e0d-140">Standard_G1</span></span> |<span data-ttu-id="d9e0d-141">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="d9e0d-141">Standard_G5</span></span> |
> | <span data-ttu-id="d9e0d-142">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="d9e0d-142">Standard_GS1</span></span> |<span data-ttu-id="d9e0d-143">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="d9e0d-143">Standard_GS5</span></span> |
> 
> 

## <a name="setup-azure-automation-to-access-your-virtual-machines"></a><span data-ttu-id="d9e0d-144">Configurar a Automação do Azure para acessar suas máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="d9e0d-144">Setup Azure Automation to access your Virtual Machines</span></span>
<span data-ttu-id="d9e0d-145">A primeira coisa que você precisa fazer é criar uma conta de Automação do Azure que hospedará os runbooks usados para dimensionar uma Máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="d9e0d-145">The first thing you need to do is create an Azure Automation account that will host the runbooks used to scale a Virtual Machine.</span></span> <span data-ttu-id="d9e0d-146">O serviço de Automação introduziu recentemente o recurso "Executar como conta" que facilita a configuração da Entidade de Serviço para execução automática de Runbooks em nome do usuário.</span><span class="sxs-lookup"><span data-stu-id="d9e0d-146">Recently the Automation service introduced the "Run As account" feature which makes setting up the Service Principal for automatically running the runbooks on the user's behalf very easy.</span></span> <span data-ttu-id="d9e0d-147">Leia mais sobre isso no artigo abaixo:</span><span class="sxs-lookup"><span data-stu-id="d9e0d-147">You can read more about this in the article below:</span></span>

* [<span data-ttu-id="d9e0d-148">Autenticar runbooks com uma conta Executar como do Azure</span><span class="sxs-lookup"><span data-stu-id="d9e0d-148">Authenticate Runbooks with Azure Run As account</span></span>](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-the-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="d9e0d-149">Importar os runbooks de Escala Vertical da Automação do Azure para sua assinatura</span><span class="sxs-lookup"><span data-stu-id="d9e0d-149">Import the Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="d9e0d-150">Os Runbooks necessários para dimensionar verticalmente a sua máquina virtual já estão publicados na Galeria de Runbook da Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="d9e0d-150">The runbooks that are needed for Vertically Scaling your Virtual Machine are already published in the Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="d9e0d-151">Você precisará importá-los para sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="d9e0d-151">You will need to import them into your subscription.</span></span> <span data-ttu-id="d9e0d-152">Saiba como importar Runbooks lendo o seguinte artigo:</span><span class="sxs-lookup"><span data-stu-id="d9e0d-152">You can learn how to import runbooks by reading the following article.</span></span>

* [<span data-ttu-id="d9e0d-153">Galerias de runbook e de módulos para a Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="d9e0d-153">Runbook and module galleries for Azure Automation</span></span>](../../automation/automation-runbook-gallery.md)

<span data-ttu-id="d9e0d-154">Os Runbooks que precisam ser importados são mostrados na imagem abaixo</span><span class="sxs-lookup"><span data-stu-id="d9e0d-154">The runbooks that need to be imported are shown in the image below</span></span>

![Importar Runbooks](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-to-your-runbook"></a><span data-ttu-id="d9e0d-156">Adicionar um webhook ao seu Runbook</span><span class="sxs-lookup"><span data-stu-id="d9e0d-156">Add a webhook to your runbook</span></span>
<span data-ttu-id="d9e0d-157">Depois de ter importado os Runbooks, você precisará adicionar um webhook ao Runbook para que ele possa ser disparado por um alerta de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d9e0d-157">Once you've imported the runbooks you'll need to add a webhook to the runbook so it can be triggered by an alert from a Virtual Machine.</span></span> <span data-ttu-id="d9e0d-158">Os detalhes da criação de um webhook para seu Runbook podem ser lidos aqui</span><span class="sxs-lookup"><span data-stu-id="d9e0d-158">The details of creating a webhook for your Runbook can be read here</span></span>

* [<span data-ttu-id="d9e0d-159">Webhooks da Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="d9e0d-159">Azure Automation webhooks</span></span>](../../automation/automation-webhooks.md)

<span data-ttu-id="d9e0d-160">Copie o webhook antes de fechar a caixa de diálogo do webhook, pois você precisará disso na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="d9e0d-160">Make sure you copy the webhook before closing the webhook dialog as you will need this in the next section.</span></span>

## <a name="add-an-alert-to-your-virtual-machine"></a><span data-ttu-id="d9e0d-161">Adicionar um alerta à sua máquina virtual</span><span class="sxs-lookup"><span data-stu-id="d9e0d-161">Add an alert to your Virtual Machine</span></span>
1. <span data-ttu-id="d9e0d-162">Selecione Configurações da Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="d9e0d-162">Select Virtual Machine settings</span></span>
2. <span data-ttu-id="d9e0d-163">Selecione “Regras de alerta”</span><span class="sxs-lookup"><span data-stu-id="d9e0d-163">Select "Alert rules"</span></span>
3. <span data-ttu-id="d9e0d-164">Selecione “Adicionar alerta”</span><span class="sxs-lookup"><span data-stu-id="d9e0d-164">Select "Add alert"</span></span>
4. <span data-ttu-id="d9e0d-165">Selecione uma métrica na qual acionar o alerta</span><span class="sxs-lookup"><span data-stu-id="d9e0d-165">Select a metric to fire the alert on</span></span>
5. <span data-ttu-id="d9e0d-166">Selecione uma condição que, quando cumprida, fará com que o alerta seja acionado</span><span class="sxs-lookup"><span data-stu-id="d9e0d-166">Select a condition, which when fulfilled will cause the alert to fire</span></span>
6. <span data-ttu-id="d9e0d-167">Selecione um limite para a condição na Etapa 5.</span><span class="sxs-lookup"><span data-stu-id="d9e0d-167">Select a threshold for the condition in Step 5.</span></span> <span data-ttu-id="d9e0d-168">a ser cumprida</span><span class="sxs-lookup"><span data-stu-id="d9e0d-168">to be fulfilled</span></span>
7. <span data-ttu-id="d9e0d-169">Selecione um período no qual o serviço de monitoramento verificará a condição e o limite nas Etapas 5 e 6</span><span class="sxs-lookup"><span data-stu-id="d9e0d-169">Select a period over which the monitoring service will check for the condition and threshold in Steps 5 & 6</span></span>
8. <span data-ttu-id="d9e0d-170">Cole o webhook que você copiou da seção anterior.</span><span class="sxs-lookup"><span data-stu-id="d9e0d-170">Paste in the webhook you copied from the previous section.</span></span>

![Adicionar alerta à máquina virtual 1](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![Adicionar alerta à máquina virtual 2](./media/vertical-scaling-automation/add-alert-webhook-2.png)

