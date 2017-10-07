---
title: "falhas de extensão de VM do Windows aaaTroubleshooting | Microsoft Docs"
description: "Saiba mais sobre como solucionar falhas da extensão de VM do Windows no Azure"
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: 878ab9b6-c3e6-40be-82d4-d77fecd5030f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: d24544743d9e0cb1a68ec9ab7718716f918054f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-windows-vm-extension-failures"></a><span data-ttu-id="6316f-103">Solucionando problemas de falhas da extensão da VM do Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="6316f-103">Troubleshooting Azure Windows VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="6316f-104">Exibindo o status da extensão</span><span class="sxs-lookup"><span data-stu-id="6316f-104">Viewing extension status</span></span>
<span data-ttu-id="6316f-105">Os modelos do Azure Resource Manager podem ser executados no Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6316f-105">Azure Resource Manager templates can be executed from Azure PowerShell.</span></span> <span data-ttu-id="6316f-106">Depois Olá modelo é executado, o status da extensão de saudação podem ser exibidos de ferramentas de linha de comando do Gerenciador de recursos do Azure ou hello.</span><span class="sxs-lookup"><span data-stu-id="6316f-106">Once hello template is executed, hello extension status can be viewed from Azure Resource Explorer or hello command line tools.</span></span>

<span data-ttu-id="6316f-107">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="6316f-107">Here is an example:</span></span>

<span data-ttu-id="6316f-108">PowerShell do Azure:</span><span class="sxs-lookup"><span data-stu-id="6316f-108">Azure PowerShell:</span></span>

      Get-AzureRmVM -ResourceGroupName $RGName -Name $vmName -Status

<span data-ttu-id="6316f-109">Aqui está a saída de exemplo hello:</span><span class="sxs-lookup"><span data-stu-id="6316f-109">Here is hello sample output:</span></span>

      Extensions:  {
      "ExtensionType": "Microsoft.Compute.CustomScriptExtension",
      "Name": "myCustomScriptExtension",
      "SubStatuses": [
        {
          "Code": "ComponentStatus/StdOut/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "    Directory: C:\\temp\\n\\n\\nMode                LastWriteTime     Length Name
              \\n----                -------------     ------ ----                              \\n-a---          9/1/2015   2:03 AM         11
              test.txt                          \\n\\n",
                      "Time": null
          },
        {
          "Code": "ComponentStatus/StdErr/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "",
          "Time": null
        }
    }
  <span data-ttu-id="6316f-110">]</span><span class="sxs-lookup"><span data-stu-id="6316f-110">]</span></span>

## <a name="troubleshooting-extension-failures"></a><span data-ttu-id="6316f-111">Solução de problemas de falhas da extensão</span><span class="sxs-lookup"><span data-stu-id="6316f-111">Troubleshooting extension failures</span></span>
### <a name="re-running-hello-extension-on-hello-vm"></a><span data-ttu-id="6316f-112">Executar novamente a extensão de saudação em Olá VM</span><span class="sxs-lookup"><span data-stu-id="6316f-112">Re-running hello extension on hello VM</span></span>
<span data-ttu-id="6316f-113">Se você estiver executando os scripts em Olá VM usando a extensão de Script personalizado, você pode executar, às vezes, um erro onde a VM foi criada com êxito mas script hello falhou.</span><span class="sxs-lookup"><span data-stu-id="6316f-113">If you are running scripts on hello VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but hello script has failed.</span></span> <span data-ttu-id="6316f-114">Sob essas conditons hello recomendado maneira toorecover desse erro é tooremove Olá extensão e novamente o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="6316f-114">Under these conditons, hello recommended way toorecover from this error is tooremove hello extension and rerun hello template again.</span></span>
<span data-ttu-id="6316f-115">Observação: No futuro, essa funcionalidade seria tooremove avançado Olá necessidade para desinstalar a extensão de saudação.</span><span class="sxs-lookup"><span data-stu-id="6316f-115">Note: In future, this functionality would be enhanced tooremove hello need for uninstalling hello extension.</span></span>

#### <a name="remove-hello-extension-from-azure-powershell"></a><span data-ttu-id="6316f-116">Remover extensão de saudação do PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="6316f-116">Remove hello extension from Azure PowerShell</span></span>
    Remove-AzureRmVMExtension -ResourceGroupName $RGName -VMName $vmName -Name "myCustomScriptExtension"

<span data-ttu-id="6316f-117">Quando Olá extensão foi removida, o modelo de Olá pode ser executado novamente toorun Olá scripts Olá VM.</span><span class="sxs-lookup"><span data-stu-id="6316f-117">Once hello extension has been removed, hello template can be re-executed toorun hello scripts on hello VM.</span></span>

