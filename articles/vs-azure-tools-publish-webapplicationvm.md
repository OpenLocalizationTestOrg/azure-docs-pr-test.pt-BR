---
title: aaaPublish WebApplicationVM | Microsoft Docs
description: "Saiba como toodeploy uma máquina virtual de tooa de aplicativo de web. Este script cria recursos Olá necessários em sua assinatura do Azure se não existirem."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: de4cec95-f73f-44d9-babd-9f47f2633cdb
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: e4b52b620bebf44b87ddfc3b19c155bb65111814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a><span data-ttu-id="f14f4-104">Publish-WebApplicationVM (script do Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="f14f4-104">Publish-WebApplicationVM (Windows PowerShell script)</span></span>
<span data-ttu-id="f14f4-105">Implanta uma máquina virtual de tooa de aplicativo de web.</span><span class="sxs-lookup"><span data-stu-id="f14f4-105">Deploys a web application tooa virtual machine.</span></span> <span data-ttu-id="f14f4-106">script Hello cria recursos Olá necessários em sua assinatura do Azure se não existirem.</span><span class="sxs-lookup"><span data-stu-id="f14f4-106">hello script creates hello required resources in your Azure subscription if they don't exist.</span></span>

```
Publish-WebApplicationVM
–Configuration <configuration>
-SubscriptionName <subscriptionName>
-WebDeployPackage <packageName>
-VMPassword @{Name = "name"; Password = "password")
-DatabaseServerPassword @{Name = "name"; Password = "password"}
-SendHostMessagesToOutput
-Verbose
```

### <a name="configuration"></a><span data-ttu-id="f14f4-107">Configuração</span><span class="sxs-lookup"><span data-stu-id="f14f4-107">Configuration</span></span>
<span data-ttu-id="f14f4-108">Olá caminho toohello arquivo de configuração JSON que descreve os detalhes de saudação da implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="f14f4-108">hello path toohello JSON configuration file that describes hello details of hello deployment.</span></span>

| <span data-ttu-id="f14f4-109">Aliases</span><span class="sxs-lookup"><span data-stu-id="f14f4-109">Aliases</span></span> | <span data-ttu-id="f14f4-110">nenhum</span><span class="sxs-lookup"><span data-stu-id="f14f4-110">none</span></span> |
| --- | --- |
| <span data-ttu-id="f14f4-111">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="f14f4-111">Required?</span></span> |<span data-ttu-id="f14f4-112">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="f14f4-112">true</span></span> |
| <span data-ttu-id="f14f4-113">Position</span><span class="sxs-lookup"><span data-stu-id="f14f4-113">Position</span></span> |<span data-ttu-id="f14f4-114">nomeado</span><span class="sxs-lookup"><span data-stu-id="f14f4-114">named</span></span> |
| <span data-ttu-id="f14f4-115">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="f14f4-115">Default value</span></span> |<span data-ttu-id="f14f4-116">nenhum</span><span class="sxs-lookup"><span data-stu-id="f14f4-116">none</span></span> |
| <span data-ttu-id="f14f4-117">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="f14f4-117">Accept pipeline input?</span></span> |<span data-ttu-id="f14f4-118">false</span><span class="sxs-lookup"><span data-stu-id="f14f4-118">false</span></span> |
| <span data-ttu-id="f14f4-119">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="f14f4-119">Accept wildcard characters?</span></span> |<span data-ttu-id="f14f4-120">false</span><span class="sxs-lookup"><span data-stu-id="f14f4-120">false</span></span> |

### <a name="subscriptionname"></a><span data-ttu-id="f14f4-121">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="f14f4-121">SubscriptionName</span></span>
<span data-ttu-id="f14f4-122">nome de saudação do hello assinatura do Azure no qual você deseja toocreate Olá VM.</span><span class="sxs-lookup"><span data-stu-id="f14f4-122">hello name of hello Azure subscription in which you want toocreate hello virtual machine.</span></span>

| <span data-ttu-id="f14f4-123">Aliases</span><span class="sxs-lookup"><span data-stu-id="f14f4-123">Aliases</span></span> | <span data-ttu-id="f14f4-124">nenhum</span><span class="sxs-lookup"><span data-stu-id="f14f4-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="f14f4-125">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="f14f4-125">Required?</span></span> |<span data-ttu-id="f14f4-126">false</span><span class="sxs-lookup"><span data-stu-id="f14f4-126">false</span></span> |
| <span data-ttu-id="f14f4-127">Position</span><span class="sxs-lookup"><span data-stu-id="f14f4-127">Position</span></span> |<span data-ttu-id="f14f4-128">nomeado</span><span class="sxs-lookup"><span data-stu-id="f14f4-128">named</span></span> |
| <span data-ttu-id="f14f4-129">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="f14f4-129">Default value</span></span> |<span data-ttu-id="f14f4-130">Usa assinatura primeiro Olá no arquivo de assinatura de saudação</span><span class="sxs-lookup"><span data-stu-id="f14f4-130">Uses hello first subscription in hello subscription file</span></span> |
| <span data-ttu-id="f14f4-131">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="f14f4-131">Accept pipeline input?</span></span> |<span data-ttu-id="f14f4-132">false</span><span class="sxs-lookup"><span data-stu-id="f14f4-132">false</span></span> |
| <span data-ttu-id="f14f4-133">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="f14f4-133">Accept wildcard characters?</span></span> |<span data-ttu-id="f14f4-134">false</span><span class="sxs-lookup"><span data-stu-id="f14f4-134">false</span></span> |

### <a name="webdeploypackage"></a><span data-ttu-id="f14f4-135">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="f14f4-135">WebDeployPackage</span></span>
<span data-ttu-id="f14f4-136">Olá caminho toohello web implantação pacote toopublish toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f14f4-136">hello path toohello web deployment package toopublish toohello virtual machine.</span></span> <span data-ttu-id="f14f4-137">Você pode criar esse pacote usando o Assistente de publicar Web Olá no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f14f4-137">You can create this package by using hello Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="f14f4-138">Consulte [Como: criar um pacote de implantação da Web no Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="f14f4-138">See [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span>

| <span data-ttu-id="f14f4-139">Aliases</span><span class="sxs-lookup"><span data-stu-id="f14f4-139">Aliases</span></span> | <span data-ttu-id="f14f4-140">nenhum</span><span class="sxs-lookup"><span data-stu-id="f14f4-140">none</span></span> |
| --- | --- |
| <span data-ttu-id="f14f4-141">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="f14f4-141">Required?</span></span> |<span data-ttu-id="f14f4-142">false</span><span class="sxs-lookup"><span data-stu-id="f14f4-142">false</span></span> |
| <span data-ttu-id="f14f4-143">Position</span><span class="sxs-lookup"><span data-stu-id="f14f4-143">Position</span></span> |<span data-ttu-id="f14f4-144">nomeado</span><span class="sxs-lookup"><span data-stu-id="f14f4-144">named</span></span> |
| <span data-ttu-id="f14f4-145">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="f14f4-145">Default value</span></span> |<span data-ttu-id="f14f4-146">nenhum</span><span class="sxs-lookup"><span data-stu-id="f14f4-146">none</span></span> |
| <span data-ttu-id="f14f4-147">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="f14f4-147">Accept pipeline input?</span></span> |<span data-ttu-id="f14f4-148">false</span><span class="sxs-lookup"><span data-stu-id="f14f4-148">false</span></span> |
| <span data-ttu-id="f14f4-149">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="f14f4-149">Accept wildcard characters?</span></span> |<span data-ttu-id="f14f4-150">false</span><span class="sxs-lookup"><span data-stu-id="f14f4-150">false</span></span> |

### <a name="allowuntrusted"></a><span data-ttu-id="f14f4-151">AllowUntrusted</span><span class="sxs-lookup"><span data-stu-id="f14f4-151">AllowUntrusted</span></span>
<span data-ttu-id="f14f4-152">Se verdadeiro, permita o uso de saudação de certificados que não são assinados por uma autoridade raiz confiável.</span><span class="sxs-lookup"><span data-stu-id="f14f4-152">If true, allow hello use of certificates that aren't signed by a trusted root authority.</span></span>

| <span data-ttu-id="f14f4-153">Aliases</span><span class="sxs-lookup"><span data-stu-id="f14f4-153">Aliases</span></span> | <span data-ttu-id="f14f4-154">nenhum</span><span class="sxs-lookup"><span data-stu-id="f14f4-154">none</span></span> |
| --- | --- |
| <span data-ttu-id="f14f4-155">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="f14f4-155">Required?</span></span> |<span data-ttu-id="f14f4-156">false</span><span class="sxs-lookup"><span data-stu-id="f14f4-156">false</span></span> |
| <span data-ttu-id="f14f4-157">Position</span><span class="sxs-lookup"><span data-stu-id="f14f4-157">Position</span></span> |<span data-ttu-id="f14f4-158">nomeado</span><span class="sxs-lookup"><span data-stu-id="f14f4-158">named</span></span> |
| <span data-ttu-id="f14f4-159">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="f14f4-159">Default value</span></span> |<span data-ttu-id="f14f4-160">false</span><span class="sxs-lookup"><span data-stu-id="f14f4-160">false</span></span> |
| <span data-ttu-id="f14f4-161">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="f14f4-161">Accept pipeline input?</span></span> |<span data-ttu-id="f14f4-162">false</span><span class="sxs-lookup"><span data-stu-id="f14f4-162">false</span></span> |
| <span data-ttu-id="f14f4-163">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="f14f4-163">Accept wildcard characters?</span></span> |<span data-ttu-id="f14f4-164">false</span><span class="sxs-lookup"><span data-stu-id="f14f4-164">false</span></span> |

### <a name="vmpassword"></a><span data-ttu-id="f14f4-165">VMPassword</span><span class="sxs-lookup"><span data-stu-id="f14f4-165">VMPassword</span></span>
<span data-ttu-id="f14f4-166">credenciais de saudação para conta de máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="f14f4-166">hello credentials for hello virtual machine account.</span></span> <span data-ttu-id="f14f4-167">Exemplo: - VMPassword @{nome = "admin"; Senha = "password"}</span><span class="sxs-lookup"><span data-stu-id="f14f4-167">Example: -VMPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="f14f4-168">Aliases</span><span class="sxs-lookup"><span data-stu-id="f14f4-168">Aliases</span></span> | <span data-ttu-id="f14f4-169">nenhum</span><span class="sxs-lookup"><span data-stu-id="f14f4-169">none</span></span> |
| --- | --- |
| <span data-ttu-id="f14f4-170">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="f14f4-170">Required?</span></span> |<span data-ttu-id="f14f4-171">false</span><span class="sxs-lookup"><span data-stu-id="f14f4-171">false</span></span> |
| <span data-ttu-id="f14f4-172">Position</span><span class="sxs-lookup"><span data-stu-id="f14f4-172">Position</span></span> |<span data-ttu-id="f14f4-173">nomeado</span><span class="sxs-lookup"><span data-stu-id="f14f4-173">named</span></span> |
| <span data-ttu-id="f14f4-174">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="f14f4-174">Default value</span></span> |<span data-ttu-id="f14f4-175">nenhum</span><span class="sxs-lookup"><span data-stu-id="f14f4-175">none</span></span> |
| <span data-ttu-id="f14f4-176">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="f14f4-176">Accept pipeline input?</span></span> |<span data-ttu-id="f14f4-177">false</span><span class="sxs-lookup"><span data-stu-id="f14f4-177">false</span></span> |
| <span data-ttu-id="f14f4-178">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="f14f4-178">Accept wildcard characters?</span></span> |<span data-ttu-id="f14f4-179">false</span><span class="sxs-lookup"><span data-stu-id="f14f4-179">false</span></span> |

### <a name="databaseserverpassword"></a><span data-ttu-id="f14f4-180">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="f14f4-180">DatabaseServerPassword</span></span>
<span data-ttu-id="f14f4-181">credenciais Olá Olá banco de dados SQL no Azure.</span><span class="sxs-lookup"><span data-stu-id="f14f4-181">hello credentials for hello SQL database in Azure.</span></span> <span data-ttu-id="f14f4-182">Exemplo: - DatabaseServerPassword @{nome = "admin"; Senha = "password"}</span><span class="sxs-lookup"><span data-stu-id="f14f4-182">Example: -DatabaseServerPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="f14f4-183">Aliases</span><span class="sxs-lookup"><span data-stu-id="f14f4-183">Aliases</span></span> | <span data-ttu-id="f14f4-184">nenhum</span><span class="sxs-lookup"><span data-stu-id="f14f4-184">none</span></span> |
| --- | --- |
| <span data-ttu-id="f14f4-185">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="f14f4-185">Required?</span></span> |<span data-ttu-id="f14f4-186">false</span><span class="sxs-lookup"><span data-stu-id="f14f4-186">false</span></span> |
| <span data-ttu-id="f14f4-187">Position</span><span class="sxs-lookup"><span data-stu-id="f14f4-187">Position</span></span> |<span data-ttu-id="f14f4-188">nomeado</span><span class="sxs-lookup"><span data-stu-id="f14f4-188">named</span></span> |
| <span data-ttu-id="f14f4-189">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="f14f4-189">Default value</span></span> |<span data-ttu-id="f14f4-190">nenhum</span><span class="sxs-lookup"><span data-stu-id="f14f4-190">none</span></span> |
| <span data-ttu-id="f14f4-191">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="f14f4-191">Accept pipeline input?</span></span> |<span data-ttu-id="f14f4-192">false</span><span class="sxs-lookup"><span data-stu-id="f14f4-192">false</span></span> |
| <span data-ttu-id="f14f4-193">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="f14f4-193">Accept wildcard characters?</span></span> |<span data-ttu-id="f14f4-194">false</span><span class="sxs-lookup"><span data-stu-id="f14f4-194">false</span></span> |

### <a name="sendhostmessagestooutput"></a><span data-ttu-id="f14f4-195">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="f14f4-195">SendHostMessagesToOutput</span></span>
<span data-ttu-id="f14f4-196">Se true, impressão mensagens de saudação script toohello fluxo de saída.</span><span class="sxs-lookup"><span data-stu-id="f14f4-196">If true, print messages from hello script toohello output stream.</span></span>

| <span data-ttu-id="f14f4-197">Aliases</span><span class="sxs-lookup"><span data-stu-id="f14f4-197">Aliases</span></span> | <span data-ttu-id="f14f4-198">nenhum</span><span class="sxs-lookup"><span data-stu-id="f14f4-198">none</span></span> |
| --- | --- |
| <span data-ttu-id="f14f4-199">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="f14f4-199">Required?</span></span> |<span data-ttu-id="f14f4-200">false</span><span class="sxs-lookup"><span data-stu-id="f14f4-200">false</span></span> |
| <span data-ttu-id="f14f4-201">Position</span><span class="sxs-lookup"><span data-stu-id="f14f4-201">Position</span></span> |<span data-ttu-id="f14f4-202">nomeado</span><span class="sxs-lookup"><span data-stu-id="f14f4-202">named</span></span> |
| <span data-ttu-id="f14f4-203">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="f14f4-203">Default value</span></span> |<span data-ttu-id="f14f4-204">false</span><span class="sxs-lookup"><span data-stu-id="f14f4-204">false</span></span> |
| <span data-ttu-id="f14f4-205">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="f14f4-205">Accept pipeline input?</span></span> |<span data-ttu-id="f14f4-206">false</span><span class="sxs-lookup"><span data-stu-id="f14f4-206">false</span></span> |
| <span data-ttu-id="f14f4-207">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="f14f4-207">Accept wildcard characters?</span></span> |<span data-ttu-id="f14f4-208">false</span><span class="sxs-lookup"><span data-stu-id="f14f4-208">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="f14f4-209">Comentários</span><span class="sxs-lookup"><span data-stu-id="f14f4-209">Remarks</span></span>
<span data-ttu-id="f14f4-210">Para obter uma explicação completa de como toouse Olá script toocreate desenvolvimento e ambientes de teste, consulte [ambientes de teste e usando Scripts do Windows PowerShell tooPublish tooDev](vs-azure-tools-publishing-using-powershell-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="f14f4-210">For a complete explanation of how toouse hello script toocreate Dev and Test environments, see [Using Windows PowerShell Scripts tooPublish tooDev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="f14f4-211">arquivo de configuração JSON Olá Especifica detalhes de saudação do que é toobe implantado.</span><span class="sxs-lookup"><span data-stu-id="f14f4-211">hello JSON configuration file specifies hello details of what is toobe deployed.</span></span> <span data-ttu-id="f14f4-212">Ela inclui informações de saudação que você especificou quando criou o projeto hello, como nome hello, grupo de afinidade, imagem do VHD e tamanho da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="f14f4-212">It includes hello information that you specified when you created hello project, such as hello name, affinity group, VHD image, and size of hello virtual machine.</span></span> <span data-ttu-id="f14f4-213">Ele também inclui pontos de extremidade de saudação na máquina virtual de hello, Olá tooprovision de bancos de dados, se houver e parâmetros de implantação de web.</span><span class="sxs-lookup"><span data-stu-id="f14f4-213">It also includes hello endpoints on hello virtual machine, hello databases tooprovision, if any, and web deployment parameters.</span></span> <span data-ttu-id="f14f4-214">saudação de código a seguir mostra um exemplo de arquivo de configuração de JSON:</span><span class="sxs-lookup"><span data-stu-id="f14f4-214">hello following code shows an example JSON configuration file:</span></span>

```
{
    "environmentSettings": {
        "cloudService": {
            "name": "myvmname",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myvmname",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201404.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [
                    {
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [
            {
                "connectionStringName": "",
                "databaseName": "",
                "serverName": "",
                "user": "",
                "password": ""
            }
        ],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

<span data-ttu-id="f14f4-215">Você pode editar o arquivo de configuração do hello JSON toochange o que é provisionado.</span><span class="sxs-lookup"><span data-stu-id="f14f4-215">You can edit hello JSON configuration file toochange what is provisioned.</span></span> <span data-ttu-id="f14f4-216">Uma máquina virtual e um serviço de nuvem são necessários, mas Olá seção de banco de dados é opcional.</span><span class="sxs-lookup"><span data-stu-id="f14f4-216">A virtual machine and a cloud service are required, but hello database section is optional.</span></span>

