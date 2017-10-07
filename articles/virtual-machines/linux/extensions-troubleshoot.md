---
title: "aaaTroubleshooting VM Linux falhas de extensão | Microsoft Docs"
description: "Saiba mais sobre como solucionar falhas da extensão de VM do Linux no Azure"
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: f05d93f3-42fc-4a09-9798-d92f7929c417
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 29a0ca34207421e0014380000a313d3c44e7e594
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-linux-vm-extension-failures"></a><span data-ttu-id="fc98f-103">Solucionando problemas de falhas de extensões de VM do Linux</span><span class="sxs-lookup"><span data-stu-id="fc98f-103">Troubleshooting Azure Linux VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="fc98f-104">Exibindo o status da extensão</span><span class="sxs-lookup"><span data-stu-id="fc98f-104">Viewing extension status</span></span>
<span data-ttu-id="fc98f-105">Modelos do Gerenciador de recursos do Azure podem ser executados de saudação CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc98f-105">Azure Resource Manager templates can be executed from hello  Azure CLI.</span></span> <span data-ttu-id="fc98f-106">Depois Olá modelo é executado, o status da extensão de saudação podem ser exibidos de ferramentas de linha de comando do Gerenciador de recursos do Azure ou hello.</span><span class="sxs-lookup"><span data-stu-id="fc98f-106">Once hello template is executed, hello extension status can be viewed from Azure Resource Explorer or hello command line tools.</span></span>

<span data-ttu-id="fc98f-107">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="fc98f-107">Here is an example:</span></span>

<span data-ttu-id="fc98f-108">CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="fc98f-108">Azure CLI:</span></span>

      azure vm get-instance-view


<span data-ttu-id="fc98f-109">Aqui está a saída de exemplo hello:</span><span class="sxs-lookup"><span data-stu-id="fc98f-109">Here is hello sample output:</span></span>

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
  <span data-ttu-id="fc98f-110">]</span><span class="sxs-lookup"><span data-stu-id="fc98f-110">]</span></span>

## <a name="troubleshooting-extenson-failures"></a><span data-ttu-id="fc98f-111">Solucionando falhas de Extensão:</span><span class="sxs-lookup"><span data-stu-id="fc98f-111">Troubleshooting Extenson failures:</span></span>
### <a name="re-running-hello-extension-on-hello-vm"></a><span data-ttu-id="fc98f-112">Executar novamente a extensão de saudação em Olá VM</span><span class="sxs-lookup"><span data-stu-id="fc98f-112">Re-running hello extension on hello VM</span></span>
<span data-ttu-id="fc98f-113">Se você estiver executando os scripts em Olá VM usando a extensão de Script personalizado, você pode executar, às vezes, um erro onde a VM foi criada com êxito mas script hello falhou.</span><span class="sxs-lookup"><span data-stu-id="fc98f-113">If you are running scripts on hello VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but hello script has failed.</span></span> <span data-ttu-id="fc98f-114">Sob essas conditons hello recomendado maneira toorecover desse erro é tooremove Olá extensão e novamente o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc98f-114">Under these conditons, hello recommended way toorecover from this error is tooremove hello extension and rerun hello template again.</span></span>
<span data-ttu-id="fc98f-115">Observação: No futuro, essa funcionalidade seria tooremove avançado Olá necessidade para desinstalar a extensão de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc98f-115">Note: In future, this functionality would be enhanced tooremove hello need for uninstalling hello extension.</span></span>

#### <a name="remove-hello-extension-from-azure-cli"></a><span data-ttu-id="fc98f-116">Remover extensão de saudação da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="fc98f-116">Remove hello extension from Azure CLI</span></span>
      azure vm extension set --resource-group "KPRG1" --vm-name "kundanapdemo" --publisher-name "Microsoft.Compute.CustomScriptExtension" --name "myCustomScriptExtension" --version 1.4 --uninstall

<span data-ttu-id="fc98f-117">Onde "nome do Publisher" corresponde a tipo de extensão toohello da saída de saudação da "máquina virtual do azure get-instância-exibição" e nome é o nome de saudação do recurso de extensão de saudação do modelo Olá</span><span class="sxs-lookup"><span data-stu-id="fc98f-117">Where "publsher-name" corresponds toohello extension type from hello output of "azure vm get-instance-view" and name is hello name of hello extension resource from hello template</span></span>

<span data-ttu-id="fc98f-118">Quando Olá extensão foi removida, o modelo de Olá pode ser executado novamente toorun Olá scripts Olá VM.</span><span class="sxs-lookup"><span data-stu-id="fc98f-118">Once hello extension has been removed, hello template can be re-executed toorun hello scripts on hello VM.</span></span>

