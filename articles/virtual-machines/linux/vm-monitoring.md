---
title: aaaEnable ou desabilitar o monitoramento de VM do Azure
description: Descreve como tooEnable ou desabilitar o monitoramento de VM do Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 6ce366d2-bd4c-4fef-a8f5-a3ae2374abcc
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/08/2016
ms.author: kmouss
ms.openlocfilehash: 39c2211e4e5f3ad364513b52c5acc70c00b432fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a><span data-ttu-id="64939-103">Habilitar ou desabilitar o monitoramento da VM do Azure</span><span class="sxs-lookup"><span data-stu-id="64939-103">Enable or Disable Azure VM Monitoring</span></span>

<span data-ttu-id="64939-104">Esta seção descreve como tooenable ou desabilite o monitoramento em Virtual máquinas em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="64939-104">This section describes how tooenable or disable monitoring on Virtual machines running on Azure.</span></span> <span data-ttu-id="64939-105">Você pode habilitar ou desabilitar o monitoramento usando o portal de saudação ou Interface de linha de comando do Azure para Mac, Linux e Windows (Olá CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="64939-105">You can enable or disable monitoring using hello portal or Azure Command-line Interface for Mac, Linux, and Windows (hello Azure CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="64939-106">Este documento descreve a versão 2.3 Olá extensão de diagnóstico do Linux, que foi preterido.</span><span class="sxs-lookup"><span data-stu-id="64939-106">This document describes version 2.3 of hello Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="64939-107">A versão 2.3 será suportada até 30 de junho de 2018.</span><span class="sxs-lookup"><span data-stu-id="64939-107">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="64939-108">A versão 3.0 do hello extensão de diagnóstico do Linux pode ser habilitada em vez disso.</span><span class="sxs-lookup"><span data-stu-id="64939-108">Version 3.0 of hello Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="64939-109">Para obter mais informações, consulte [Olá documentação](./diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="64939-109">For more information, see [hello documentation](./diagnostic-extension.md).</span></span>

## <a name="enable--disable-monitoring-through-hello-azure-portal"></a><span data-ttu-id="64939-110">Habilitar / desabilitar o monitoramento por meio de saudação portal do Azure</span><span class="sxs-lookup"><span data-stu-id="64939-110">Enable / Disable Monitoring through hello Azure portal</span></span>

<span data-ttu-id="64939-111">É possível habilitar o monitoramento da VM do Azure, que fornece dados sobre a sua instância em períodos de um minuto.</span><span class="sxs-lookup"><span data-stu-id="64939-111">You can enable  monitoring of your Azure VM, which provides data about your instance in 1-minute periods.</span></span> <span data-ttu-id="64939-112">(alterações de armazenamento se aplicam).</span><span class="sxs-lookup"><span data-stu-id="64939-112">(storage changes apply).</span></span> <span data-ttu-id="64939-113">Dados de diagnóstico detalhadas, em seguida, estão disponíveis para Olá VM gráficos portal hello ou por meio de saudação API.</span><span class="sxs-lookup"><span data-stu-id="64939-113">Detailed diagnostics data is then available for hello VM in hello portal graphs or through hello API.</span></span> <span data-ttu-id="64939-114">Por padrão, o portal do Azure permite o monitoramento baseado em host de um conjunto limitado de métricas.</span><span class="sxs-lookup"><span data-stu-id="64939-114">By default, Azure portal enables host-based monitoring of a limited set of metrics.</span></span> <span data-ttu-id="64939-115">Você pode habilitar o monitoramento de métricas de dentro de uma máquina virtual durante a saudação que VM está em execução ou no estado parado.</span><span class="sxs-lookup"><span data-stu-id="64939-115">You can enable monitoring of metrics from within a VM while hello VM is running or in stopped state.</span></span>

* <span data-ttu-id="64939-116">Abra hello Azure portal em [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="64939-116">Open hello Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
* <span data-ttu-id="64939-117">Na barra de navegação esquerda de Olá, clique em máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="64939-117">In hello left navigation, click Virtual machines.</span></span>
* <span data-ttu-id="64939-118">Em máquinas virtuais da saudação lista, selecione uma instância em execução ou parada.</span><span class="sxs-lookup"><span data-stu-id="64939-118">In hello list Virtual machines, select a running or stopped instance.</span></span> <span data-ttu-id="64939-119">Abre a folha de "Máquina Virtual" Hello.</span><span class="sxs-lookup"><span data-stu-id="64939-119">hello "Virtual machine" blade opens.</span></span>
* <span data-ttu-id="64939-120">Clique em Todas as configurações.</span><span class="sxs-lookup"><span data-stu-id="64939-120">Click All settings.</span></span>
* <span data-ttu-id="64939-121">Clique em Diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="64939-121">Click Diagnostics.</span></span>
* <span data-ttu-id="64939-122">Alterar status tooOn ou desativado.</span><span class="sxs-lookup"><span data-stu-id="64939-122">Change status tooOn or Off.</span></span> <span data-ttu-id="64939-123">Você também pode escolher neste nível de saudação de folha do monitoramento de detalhes que você deseja tooenable para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="64939-123">You can also pick in this blade hello level of monitoring details you would like tooenable for your virtual machine.</span></span>

![Habilitar / desabilitar o monitoramento por meio de saudação portal do Azure.][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a><span data-ttu-id="64939-125">Habilitar/desabilitar o monitoramento com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="64939-125">Enable / Disable Monitoring with Azure CLI</span></span>

<span data-ttu-id="64939-126">tooenable monitoramento para uma VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="64939-126">tooenable monitoring for an Azure VM.</span></span>

* <span data-ttu-id="64939-127">Crie um arquivo (denominado PrivateConfig.json):</span><span class="sxs-lookup"><span data-stu-id="64939-127">Create a file (named such as PrivateConfig.json):</span></span>

```json
{
        "storageAccountName":"hello storage account tooreceive data",
        "storageAccountKey":"hello key of hello account"
}
```

* <span data-ttu-id="64939-128">Habilite a extensão de saudação via CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="64939-128">Enable hello extension via Azure CLI.</span></span>

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

<span data-ttu-id="64939-129">Para obter mais informações, consulte [de usando a extensão de diagnóstico do Linux tooMonitor Linux VM dados de desempenho e diagnósticos](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="64939-129">For more information, see [Using Linux Diagnostic Extension tooMonitor Linux VM’s performance and diagnostic data](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png
