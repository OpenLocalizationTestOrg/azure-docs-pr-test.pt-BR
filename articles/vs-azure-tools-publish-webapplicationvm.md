---
title: Publicar WebApplicationVM | Microsoft Docs
description: "Saiba como implantar um aplicativo Web para uma máquina virtual. Se os recursos necessários não existirem, este script criará tais recursos em sua assinatura do Azure."
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
ms.openlocfilehash: 2738fc1dff50a177a227ae2c7719bd9a192d82ad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a><span data-ttu-id="0aaa1-104">Publish-WebApplicationVM (script do Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="0aaa1-104">Publish-WebApplicationVM (Windows PowerShell script)</span></span>
<span data-ttu-id="0aaa1-105">Implanta um aplicativo Web em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0aaa1-105">Deploys a web application to a virtual machine.</span></span> <span data-ttu-id="0aaa1-106">Se os recursos necessários não existirem, o script criará tais recursos em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="0aaa1-106">The script creates the required resources in your Azure subscription if they don't exist.</span></span>

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

### <a name="configuration"></a><span data-ttu-id="0aaa1-107">Configuração</span><span class="sxs-lookup"><span data-stu-id="0aaa1-107">Configuration</span></span>
<span data-ttu-id="0aaa1-108">O caminho para o arquivo de configuração de JSON que descreve os detalhes da implantação.</span><span class="sxs-lookup"><span data-stu-id="0aaa1-108">The path to the JSON configuration file that describes the details of the deployment.</span></span>

| <span data-ttu-id="0aaa1-109">Aliases</span><span class="sxs-lookup"><span data-stu-id="0aaa1-109">Aliases</span></span> | <span data-ttu-id="0aaa1-110">nenhum</span><span class="sxs-lookup"><span data-stu-id="0aaa1-110">none</span></span> |
| --- | --- |
| <span data-ttu-id="0aaa1-111">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="0aaa1-111">Required?</span></span> |<span data-ttu-id="0aaa1-112">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="0aaa1-112">true</span></span> |
| <span data-ttu-id="0aaa1-113">Position</span><span class="sxs-lookup"><span data-stu-id="0aaa1-113">Position</span></span> |<span data-ttu-id="0aaa1-114">nomeado</span><span class="sxs-lookup"><span data-stu-id="0aaa1-114">named</span></span> |
| <span data-ttu-id="0aaa1-115">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="0aaa1-115">Default value</span></span> |<span data-ttu-id="0aaa1-116">nenhum</span><span class="sxs-lookup"><span data-stu-id="0aaa1-116">none</span></span> |
| <span data-ttu-id="0aaa1-117">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="0aaa1-117">Accept pipeline input?</span></span> |<span data-ttu-id="0aaa1-118">false</span><span class="sxs-lookup"><span data-stu-id="0aaa1-118">false</span></span> |
| <span data-ttu-id="0aaa1-119">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="0aaa1-119">Accept wildcard characters?</span></span> |<span data-ttu-id="0aaa1-120">false</span><span class="sxs-lookup"><span data-stu-id="0aaa1-120">false</span></span> |

### <a name="subscriptionname"></a><span data-ttu-id="0aaa1-121">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="0aaa1-121">SubscriptionName</span></span>
<span data-ttu-id="0aaa1-122">O nome da assinatura do Azure no qual você deseja criar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0aaa1-122">The name of the Azure subscription in which you want to create the virtual machine.</span></span>

| <span data-ttu-id="0aaa1-123">Aliases</span><span class="sxs-lookup"><span data-stu-id="0aaa1-123">Aliases</span></span> | <span data-ttu-id="0aaa1-124">nenhum</span><span class="sxs-lookup"><span data-stu-id="0aaa1-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="0aaa1-125">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="0aaa1-125">Required?</span></span> |<span data-ttu-id="0aaa1-126">false</span><span class="sxs-lookup"><span data-stu-id="0aaa1-126">false</span></span> |
| <span data-ttu-id="0aaa1-127">Position</span><span class="sxs-lookup"><span data-stu-id="0aaa1-127">Position</span></span> |<span data-ttu-id="0aaa1-128">nomeado</span><span class="sxs-lookup"><span data-stu-id="0aaa1-128">named</span></span> |
| <span data-ttu-id="0aaa1-129">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="0aaa1-129">Default value</span></span> |<span data-ttu-id="0aaa1-130">Usa a primeira assinatura no arquivo de assinatura</span><span class="sxs-lookup"><span data-stu-id="0aaa1-130">Uses the first subscription in the subscription file</span></span> |
| <span data-ttu-id="0aaa1-131">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="0aaa1-131">Accept pipeline input?</span></span> |<span data-ttu-id="0aaa1-132">false</span><span class="sxs-lookup"><span data-stu-id="0aaa1-132">false</span></span> |
| <span data-ttu-id="0aaa1-133">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="0aaa1-133">Accept wildcard characters?</span></span> |<span data-ttu-id="0aaa1-134">false</span><span class="sxs-lookup"><span data-stu-id="0aaa1-134">false</span></span> |

### <a name="webdeploypackage"></a><span data-ttu-id="0aaa1-135">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="0aaa1-135">WebDeployPackage</span></span>
<span data-ttu-id="0aaa1-136">O caminho para o pacote de implantação da web para publicar na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0aaa1-136">The path to the web deployment package to publish to the virtual machine.</span></span> <span data-ttu-id="0aaa1-137">Você pode criar este pacote usando o assistente Publicar Web no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0aaa1-137">You can create this package by using the Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="0aaa1-138">Consulte [Como: criar um pacote de implantação da Web no Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="0aaa1-138">See [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span>

| <span data-ttu-id="0aaa1-139">Aliases</span><span class="sxs-lookup"><span data-stu-id="0aaa1-139">Aliases</span></span> | <span data-ttu-id="0aaa1-140">nenhum</span><span class="sxs-lookup"><span data-stu-id="0aaa1-140">none</span></span> |
| --- | --- |
| <span data-ttu-id="0aaa1-141">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="0aaa1-141">Required?</span></span> |<span data-ttu-id="0aaa1-142">false</span><span class="sxs-lookup"><span data-stu-id="0aaa1-142">false</span></span> |
| <span data-ttu-id="0aaa1-143">Position</span><span class="sxs-lookup"><span data-stu-id="0aaa1-143">Position</span></span> |<span data-ttu-id="0aaa1-144">nomeado</span><span class="sxs-lookup"><span data-stu-id="0aaa1-144">named</span></span> |
| <span data-ttu-id="0aaa1-145">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="0aaa1-145">Default value</span></span> |<span data-ttu-id="0aaa1-146">nenhum</span><span class="sxs-lookup"><span data-stu-id="0aaa1-146">none</span></span> |
| <span data-ttu-id="0aaa1-147">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="0aaa1-147">Accept pipeline input?</span></span> |<span data-ttu-id="0aaa1-148">false</span><span class="sxs-lookup"><span data-stu-id="0aaa1-148">false</span></span> |
| <span data-ttu-id="0aaa1-149">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="0aaa1-149">Accept wildcard characters?</span></span> |<span data-ttu-id="0aaa1-150">false</span><span class="sxs-lookup"><span data-stu-id="0aaa1-150">false</span></span> |

### <a name="allowuntrusted"></a><span data-ttu-id="0aaa1-151">AllowUntrusted</span><span class="sxs-lookup"><span data-stu-id="0aaa1-151">AllowUntrusted</span></span>
<span data-ttu-id="0aaa1-152">Se for verdadeiro, permite o uso de certificados que não está assinado por uma autoridade raiz confiável.</span><span class="sxs-lookup"><span data-stu-id="0aaa1-152">If true, allow the use of certificates that aren't signed by a trusted root authority.</span></span>

| <span data-ttu-id="0aaa1-153">Aliases</span><span class="sxs-lookup"><span data-stu-id="0aaa1-153">Aliases</span></span> | <span data-ttu-id="0aaa1-154">nenhum</span><span class="sxs-lookup"><span data-stu-id="0aaa1-154">none</span></span> |
| --- | --- |
| <span data-ttu-id="0aaa1-155">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="0aaa1-155">Required?</span></span> |<span data-ttu-id="0aaa1-156">false</span><span class="sxs-lookup"><span data-stu-id="0aaa1-156">false</span></span> |
| <span data-ttu-id="0aaa1-157">Position</span><span class="sxs-lookup"><span data-stu-id="0aaa1-157">Position</span></span> |<span data-ttu-id="0aaa1-158">nomeado</span><span class="sxs-lookup"><span data-stu-id="0aaa1-158">named</span></span> |
| <span data-ttu-id="0aaa1-159">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="0aaa1-159">Default value</span></span> |<span data-ttu-id="0aaa1-160">false</span><span class="sxs-lookup"><span data-stu-id="0aaa1-160">false</span></span> |
| <span data-ttu-id="0aaa1-161">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="0aaa1-161">Accept pipeline input?</span></span> |<span data-ttu-id="0aaa1-162">false</span><span class="sxs-lookup"><span data-stu-id="0aaa1-162">false</span></span> |
| <span data-ttu-id="0aaa1-163">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="0aaa1-163">Accept wildcard characters?</span></span> |<span data-ttu-id="0aaa1-164">false</span><span class="sxs-lookup"><span data-stu-id="0aaa1-164">false</span></span> |

### <a name="vmpassword"></a><span data-ttu-id="0aaa1-165">VMPassword</span><span class="sxs-lookup"><span data-stu-id="0aaa1-165">VMPassword</span></span>
<span data-ttu-id="0aaa1-166">As credenciais da conta de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0aaa1-166">The credentials for the virtual machine account.</span></span> <span data-ttu-id="0aaa1-167">Exemplo: - VMPassword @{nome = "admin"; Senha = "password"}</span><span class="sxs-lookup"><span data-stu-id="0aaa1-167">Example: -VMPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="0aaa1-168">Aliases</span><span class="sxs-lookup"><span data-stu-id="0aaa1-168">Aliases</span></span> | <span data-ttu-id="0aaa1-169">nenhum</span><span class="sxs-lookup"><span data-stu-id="0aaa1-169">none</span></span> |
| --- | --- |
| <span data-ttu-id="0aaa1-170">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="0aaa1-170">Required?</span></span> |<span data-ttu-id="0aaa1-171">false</span><span class="sxs-lookup"><span data-stu-id="0aaa1-171">false</span></span> |
| <span data-ttu-id="0aaa1-172">Position</span><span class="sxs-lookup"><span data-stu-id="0aaa1-172">Position</span></span> |<span data-ttu-id="0aaa1-173">nomeado</span><span class="sxs-lookup"><span data-stu-id="0aaa1-173">named</span></span> |
| <span data-ttu-id="0aaa1-174">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="0aaa1-174">Default value</span></span> |<span data-ttu-id="0aaa1-175">nenhum</span><span class="sxs-lookup"><span data-stu-id="0aaa1-175">none</span></span> |
| <span data-ttu-id="0aaa1-176">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="0aaa1-176">Accept pipeline input?</span></span> |<span data-ttu-id="0aaa1-177">false</span><span class="sxs-lookup"><span data-stu-id="0aaa1-177">false</span></span> |
| <span data-ttu-id="0aaa1-178">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="0aaa1-178">Accept wildcard characters?</span></span> |<span data-ttu-id="0aaa1-179">false</span><span class="sxs-lookup"><span data-stu-id="0aaa1-179">false</span></span> |

### <a name="databaseserverpassword"></a><span data-ttu-id="0aaa1-180">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="0aaa1-180">DatabaseServerPassword</span></span>
<span data-ttu-id="0aaa1-181">As credenciais do banco de dados SQL no Azure.</span><span class="sxs-lookup"><span data-stu-id="0aaa1-181">The credentials for the SQL database in Azure.</span></span> <span data-ttu-id="0aaa1-182">Exemplo: - DatabaseServerPassword @{nome = "admin"; Senha = "password"}</span><span class="sxs-lookup"><span data-stu-id="0aaa1-182">Example: -DatabaseServerPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="0aaa1-183">Aliases</span><span class="sxs-lookup"><span data-stu-id="0aaa1-183">Aliases</span></span> | <span data-ttu-id="0aaa1-184">nenhum</span><span class="sxs-lookup"><span data-stu-id="0aaa1-184">none</span></span> |
| --- | --- |
| <span data-ttu-id="0aaa1-185">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="0aaa1-185">Required?</span></span> |<span data-ttu-id="0aaa1-186">false</span><span class="sxs-lookup"><span data-stu-id="0aaa1-186">false</span></span> |
| <span data-ttu-id="0aaa1-187">Position</span><span class="sxs-lookup"><span data-stu-id="0aaa1-187">Position</span></span> |<span data-ttu-id="0aaa1-188">nomeado</span><span class="sxs-lookup"><span data-stu-id="0aaa1-188">named</span></span> |
| <span data-ttu-id="0aaa1-189">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="0aaa1-189">Default value</span></span> |<span data-ttu-id="0aaa1-190">nenhum</span><span class="sxs-lookup"><span data-stu-id="0aaa1-190">none</span></span> |
| <span data-ttu-id="0aaa1-191">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="0aaa1-191">Accept pipeline input?</span></span> |<span data-ttu-id="0aaa1-192">false</span><span class="sxs-lookup"><span data-stu-id="0aaa1-192">false</span></span> |
| <span data-ttu-id="0aaa1-193">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="0aaa1-193">Accept wildcard characters?</span></span> |<span data-ttu-id="0aaa1-194">false</span><span class="sxs-lookup"><span data-stu-id="0aaa1-194">false</span></span> |

### <a name="sendhostmessagestooutput"></a><span data-ttu-id="0aaa1-195">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="0aaa1-195">SendHostMessagesToOutput</span></span>
<span data-ttu-id="0aaa1-196">Se seu valor for true, imprimir mensagens do script para o fluxo de saída.</span><span class="sxs-lookup"><span data-stu-id="0aaa1-196">If true, print messages from the script to the output stream.</span></span>

| <span data-ttu-id="0aaa1-197">Aliases</span><span class="sxs-lookup"><span data-stu-id="0aaa1-197">Aliases</span></span> | <span data-ttu-id="0aaa1-198">nenhum</span><span class="sxs-lookup"><span data-stu-id="0aaa1-198">none</span></span> |
| --- | --- |
| <span data-ttu-id="0aaa1-199">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="0aaa1-199">Required?</span></span> |<span data-ttu-id="0aaa1-200">false</span><span class="sxs-lookup"><span data-stu-id="0aaa1-200">false</span></span> |
| <span data-ttu-id="0aaa1-201">Position</span><span class="sxs-lookup"><span data-stu-id="0aaa1-201">Position</span></span> |<span data-ttu-id="0aaa1-202">nomeado</span><span class="sxs-lookup"><span data-stu-id="0aaa1-202">named</span></span> |
| <span data-ttu-id="0aaa1-203">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="0aaa1-203">Default value</span></span> |<span data-ttu-id="0aaa1-204">false</span><span class="sxs-lookup"><span data-stu-id="0aaa1-204">false</span></span> |
| <span data-ttu-id="0aaa1-205">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="0aaa1-205">Accept pipeline input?</span></span> |<span data-ttu-id="0aaa1-206">false</span><span class="sxs-lookup"><span data-stu-id="0aaa1-206">false</span></span> |
| <span data-ttu-id="0aaa1-207">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="0aaa1-207">Accept wildcard characters?</span></span> |<span data-ttu-id="0aaa1-208">false</span><span class="sxs-lookup"><span data-stu-id="0aaa1-208">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="0aaa1-209">Comentários</span><span class="sxs-lookup"><span data-stu-id="0aaa1-209">Remarks</span></span>
<span data-ttu-id="0aaa1-210">Para obter uma explicação completa de como usar o script para criar ambientes de desenvolvimento e teste, consulte [Usando scripts do Windows PowerShell para publicar para ambientes de desenvolvimento e teste](vs-azure-tools-publishing-using-powershell-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="0aaa1-210">For a complete explanation of how to use the script to create Dev and Test environments, see [Using Windows PowerShell Scripts to Publish to Dev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="0aaa1-211">O arquivo de configuração JSON especifica os detalhes daquilo que está para ser implantado.</span><span class="sxs-lookup"><span data-stu-id="0aaa1-211">The JSON configuration file specifies the details of what is to be deployed.</span></span> <span data-ttu-id="0aaa1-212">Ele inclui as informações que você especificou quando criou o projeto, como o nome, grupo de afinidades, imagem de VHD e tamanho da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0aaa1-212">It includes the information that you specified when you created the project, such as the name, affinity group, VHD image, and size of the virtual machine.</span></span> <span data-ttu-id="0aaa1-213">Também inclui os pontos de extremidade na máquina virtual, os bancos de dados a provisionar, se houver, e os parâmetros de implantação de web.</span><span class="sxs-lookup"><span data-stu-id="0aaa1-213">It also includes the endpoints on the virtual machine, the databases to provision, if any, and web deployment parameters.</span></span> <span data-ttu-id="0aaa1-214">O código a seguir mostra um exemplo de arquivo de configuração JSON:</span><span class="sxs-lookup"><span data-stu-id="0aaa1-214">The following code shows an example JSON configuration file:</span></span>

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

<span data-ttu-id="0aaa1-215">Você pode editar o arquivo de configuração do JSON para alterar o que é provisionado.</span><span class="sxs-lookup"><span data-stu-id="0aaa1-215">You can edit the JSON configuration file to change what is provisioned.</span></span> <span data-ttu-id="0aaa1-216">Uma máquina virtual e um serviço de nuvem são necessários, mas a seção de banco de dados é opcional.</span><span class="sxs-lookup"><span data-stu-id="0aaa1-216">A virtual machine and a cloud service are required, but the database section is optional.</span></span>

