---
title: Publish-WebApplicationWebSite (script do Windows PowerShell) | Microsoft Docs
description: "Saiba como publicar um projeto Web em um site do Azure. Se os recursos necessários não existirem, este script criará tais recursos em sua assinatura do Azure."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 63cfaa2d-f04d-40dc-8677-345385c278d5
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 07d21b7ce6cd8aee1cff704d316e7a2ca8c00437
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a><span data-ttu-id="d055f-104">Publish-WebApplicationWebSite (script do Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="d055f-104">Publish-WebApplicationWebSite (Windows PowerShell script)</span></span>
## <a name="syntax"></a><span data-ttu-id="d055f-105">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="d055f-105">Syntax</span></span>
<span data-ttu-id="d055f-106">Publica um projeto Web em um site do Azure.</span><span class="sxs-lookup"><span data-stu-id="d055f-106">Publishes a web project to an Azure website.</span></span> <span data-ttu-id="d055f-107">Se os recursos necessários não existirem, o script criará tais recursos em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="d055f-107">The script creates the required resources in your Azure subscription if they don't exist.</span></span>

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a><span data-ttu-id="d055f-108">Configuração</span><span class="sxs-lookup"><span data-stu-id="d055f-108">Configuration</span></span>
<span data-ttu-id="d055f-109">O caminho para o arquivo de configuração de JSON que descreve os detalhes da implantação.</span><span class="sxs-lookup"><span data-stu-id="d055f-109">The path to the JSON configuration file that describes the details of the deployment.</span></span>

| <span data-ttu-id="d055f-110">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d055f-110">Parameter</span></span> | <span data-ttu-id="d055f-111">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="d055f-111">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="d055f-112">Aliases</span><span class="sxs-lookup"><span data-stu-id="d055f-112">Aliases</span></span> |<span data-ttu-id="d055f-113">nenhum</span><span class="sxs-lookup"><span data-stu-id="d055f-113">none</span></span> |
| <span data-ttu-id="d055f-114">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="d055f-114">Required?</span></span> |<span data-ttu-id="d055f-115">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="d055f-115">true</span></span> |
| <span data-ttu-id="d055f-116">Position</span><span class="sxs-lookup"><span data-stu-id="d055f-116">Position</span></span> |<span data-ttu-id="d055f-117">nomeado</span><span class="sxs-lookup"><span data-stu-id="d055f-117">named</span></span> |
| <span data-ttu-id="d055f-118">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="d055f-118">Default value</span></span> |<span data-ttu-id="d055f-119">nenhum</span><span class="sxs-lookup"><span data-stu-id="d055f-119">none</span></span> |
| <span data-ttu-id="d055f-120">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="d055f-120">Accept pipeline input?</span></span> |<span data-ttu-id="d055f-121">false</span><span class="sxs-lookup"><span data-stu-id="d055f-121">false</span></span> |
| <span data-ttu-id="d055f-122">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="d055f-122">Accept wildcard characters?</span></span> |<span data-ttu-id="d055f-123">false</span><span class="sxs-lookup"><span data-stu-id="d055f-123">false</span></span> |

## <a name="subscriptionname"></a><span data-ttu-id="d055f-124">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="d055f-124">SubscriptionName</span></span>
<span data-ttu-id="d055f-125">O nome da assinatura do Azure na qual você deseja criar o site.</span><span class="sxs-lookup"><span data-stu-id="d055f-125">The name of the Azure subscription that you want to create the website in.</span></span>

| <span data-ttu-id="d055f-126">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d055f-126">Parameter</span></span> | <span data-ttu-id="d055f-127">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="d055f-127">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="d055f-128">Aliases</span><span class="sxs-lookup"><span data-stu-id="d055f-128">Aliases</span></span> |<span data-ttu-id="d055f-129">nenhum</span><span class="sxs-lookup"><span data-stu-id="d055f-129">none</span></span> |
| <span data-ttu-id="d055f-130">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="d055f-130">Required?</span></span> |<span data-ttu-id="d055f-131">false</span><span class="sxs-lookup"><span data-stu-id="d055f-131">false</span></span> |
| <span data-ttu-id="d055f-132">Position</span><span class="sxs-lookup"><span data-stu-id="d055f-132">Position</span></span> |<span data-ttu-id="d055f-133">nomeado</span><span class="sxs-lookup"><span data-stu-id="d055f-133">named</span></span> |
| <span data-ttu-id="d055f-134">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="d055f-134">Default value</span></span> |<span data-ttu-id="d055f-135">nenhum</span><span class="sxs-lookup"><span data-stu-id="d055f-135">none</span></span> |
| <span data-ttu-id="d055f-136">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="d055f-136">Accept pipeline input?</span></span> |<span data-ttu-id="d055f-137">false</span><span class="sxs-lookup"><span data-stu-id="d055f-137">false</span></span> |
| <span data-ttu-id="d055f-138">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="d055f-138">Accept wildcard characters?</span></span> |<span data-ttu-id="d055f-139">false</span><span class="sxs-lookup"><span data-stu-id="d055f-139">false</span></span> |

## <a name="webdeploypackage"></a><span data-ttu-id="d055f-140">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="d055f-140">WebDeployPackage</span></span>
<span data-ttu-id="d055f-141">O caminho para o pacote de implantação Web a publicar no site.</span><span class="sxs-lookup"><span data-stu-id="d055f-141">The path to the web deployment package to publish to the website.</span></span> <span data-ttu-id="d055f-142">Você pode criar este pacote usando o assistente Publicar Web no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d055f-142">You can create this package by using the Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="d055f-143">Para obter mais informações, consulte [Introdução aos serviços de nuvem do Azure e ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span><span class="sxs-lookup"><span data-stu-id="d055f-143">For more information, see [Get started with Azure Cloud Services and ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span></span>

| <span data-ttu-id="d055f-144">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d055f-144">Parameter</span></span> | <span data-ttu-id="d055f-145">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="d055f-145">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="d055f-146">Aliases</span><span class="sxs-lookup"><span data-stu-id="d055f-146">Aliases</span></span> |<span data-ttu-id="d055f-147">nenhum</span><span class="sxs-lookup"><span data-stu-id="d055f-147">none</span></span> |
| <span data-ttu-id="d055f-148">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="d055f-148">Required?</span></span> |<span data-ttu-id="d055f-149">false</span><span class="sxs-lookup"><span data-stu-id="d055f-149">false</span></span> |
| <span data-ttu-id="d055f-150">Position</span><span class="sxs-lookup"><span data-stu-id="d055f-150">Position</span></span> |<span data-ttu-id="d055f-151">nomeado</span><span class="sxs-lookup"><span data-stu-id="d055f-151">named</span></span> |
| <span data-ttu-id="d055f-152">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="d055f-152">Default value</span></span> |<span data-ttu-id="d055f-153">nenhum</span><span class="sxs-lookup"><span data-stu-id="d055f-153">none</span></span> |
| <span data-ttu-id="d055f-154">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="d055f-154">Accept pipeline input?</span></span> |<span data-ttu-id="d055f-155">false</span><span class="sxs-lookup"><span data-stu-id="d055f-155">false</span></span> |
| <span data-ttu-id="d055f-156">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="d055f-156">Accept wildcard characters?</span></span> |<span data-ttu-id="d055f-157">false</span><span class="sxs-lookup"><span data-stu-id="d055f-157">false</span></span> |

## <a name="databaseserverpassword"></a><span data-ttu-id="d055f-158">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="d055f-158">DatabaseServerPassword</span></span>
<span data-ttu-id="d055f-159">O nome do administrador e a senha do Banco de Dados SQL no Azure.</span><span class="sxs-lookup"><span data-stu-id="d055f-159">The username and password for the SQL database in Azure.</span></span>

| <span data-ttu-id="d055f-160">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d055f-160">Parameter</span></span> | <span data-ttu-id="d055f-161">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="d055f-161">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="d055f-162">Aliases</span><span class="sxs-lookup"><span data-stu-id="d055f-162">Aliases</span></span> |<span data-ttu-id="d055f-163">nenhum</span><span class="sxs-lookup"><span data-stu-id="d055f-163">none</span></span> |
| <span data-ttu-id="d055f-164">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="d055f-164">Required?</span></span> |<span data-ttu-id="d055f-165">false</span><span class="sxs-lookup"><span data-stu-id="d055f-165">false</span></span> |
| <span data-ttu-id="d055f-166">Position</span><span class="sxs-lookup"><span data-stu-id="d055f-166">Position</span></span> |<span data-ttu-id="d055f-167">nomeado</span><span class="sxs-lookup"><span data-stu-id="d055f-167">named</span></span> |
| <span data-ttu-id="d055f-168">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="d055f-168">Default value</span></span> |<span data-ttu-id="d055f-169">nenhum</span><span class="sxs-lookup"><span data-stu-id="d055f-169">none</span></span> |
| <span data-ttu-id="d055f-170">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="d055f-170">Accept pipeline input?</span></span> |<span data-ttu-id="d055f-171">false</span><span class="sxs-lookup"><span data-stu-id="d055f-171">false</span></span> |
| <span data-ttu-id="d055f-172">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="d055f-172">Accept wildcard characters?</span></span> |<span data-ttu-id="d055f-173">false</span><span class="sxs-lookup"><span data-stu-id="d055f-173">false</span></span> |

## <a name="sendhostmessagestooutput"></a><span data-ttu-id="d055f-174">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="d055f-174">SendHostMessagesToOutput</span></span>
<span data-ttu-id="d055f-175">Se seu valor for true, imprimir mensagens do script para o fluxo de saída.</span><span class="sxs-lookup"><span data-stu-id="d055f-175">If true, print messages from the script to the output stream.</span></span>

| <span data-ttu-id="d055f-176">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d055f-176">Parameter</span></span> | <span data-ttu-id="d055f-177">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="d055f-177">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="d055f-178">Aliases</span><span class="sxs-lookup"><span data-stu-id="d055f-178">Aliases</span></span> |<span data-ttu-id="d055f-179">nenhum</span><span class="sxs-lookup"><span data-stu-id="d055f-179">none</span></span> |
| <span data-ttu-id="d055f-180">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="d055f-180">Required?</span></span> |<span data-ttu-id="d055f-181">false</span><span class="sxs-lookup"><span data-stu-id="d055f-181">false</span></span> |
| <span data-ttu-id="d055f-182">Position</span><span class="sxs-lookup"><span data-stu-id="d055f-182">Position</span></span> |<span data-ttu-id="d055f-183">nomeado</span><span class="sxs-lookup"><span data-stu-id="d055f-183">named</span></span> |
| <span data-ttu-id="d055f-184">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="d055f-184">Default value</span></span> |<span data-ttu-id="d055f-185">false</span><span class="sxs-lookup"><span data-stu-id="d055f-185">false</span></span> |
| <span data-ttu-id="d055f-186">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="d055f-186">Accept pipeline input?</span></span> |<span data-ttu-id="d055f-187">false</span><span class="sxs-lookup"><span data-stu-id="d055f-187">false</span></span> |
| <span data-ttu-id="d055f-188">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="d055f-188">Accept wildcard characters?</span></span> |<span data-ttu-id="d055f-189">false</span><span class="sxs-lookup"><span data-stu-id="d055f-189">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="d055f-190">Comentários</span><span class="sxs-lookup"><span data-stu-id="d055f-190">Remarks</span></span>
<span data-ttu-id="d055f-191">Para obter uma explicação completa de como usar o script para criar ambientes de desenvolvimento e teste, consulte [Usando scripts do Windows PowerShell para publicar para ambientes de desenvolvimento e teste](vs-azure-tools-publishing-using-powershell-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="d055f-191">For a complete explanation of how to use the script to create Dev and Test environments, see [Using Windows PowerShell Scripts to Publish to Dev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="d055f-192">O arquivo de configuração JSON especifica os detalhes daquilo que está para ser implantado.</span><span class="sxs-lookup"><span data-stu-id="d055f-192">The JSON configuration file specifies the details of what is to be deployed.</span></span> <span data-ttu-id="d055f-193">Ele inclui as informações que você especificou quando criou o projeto, como o nome e também o nome de usuário para o site.</span><span class="sxs-lookup"><span data-stu-id="d055f-193">It includes the information that you specified when you created the project, such as the name and username for the website.</span></span> <span data-ttu-id="d055f-194">Ele também inclui o banco de dados a provisionar, se houver.</span><span class="sxs-lookup"><span data-stu-id="d055f-194">It also includes the database to provision, if any.</span></span> <span data-ttu-id="d055f-195">O código a seguir mostra um exemplo de arquivo de configuração JSON:</span><span class="sxs-lookup"><span data-stu-id="d055f-195">The following code shows an example JSON configuration file:</span></span>

    {
        "environmentSettings": {
            "webSite": {
                "name": "WebApplication10554",
                "location": "West US"
            },
            "databases": [
                {
                    "connectionStringName": "DefaultConnection",
                    "databaseName": "WebApplication10554_db",
                    "serverName": "iss00brc88",
                    "user": "sqluser2",
                    "password": "",
                    "edition": "",
                    "size": "",
                    "collation": "",
                    "location": "West US"
                }
            ]
        }
    }

<span data-ttu-id="d055f-196">Você pode editar o arquivo de configuração JSON para alterar o que é implantado.</span><span class="sxs-lookup"><span data-stu-id="d055f-196">You can edit the JSON configuration file to change what is deployed.</span></span> <span data-ttu-id="d055f-197">Uma seção de site é obrigatória, mas a seção de banco de dados é opcional.</span><span class="sxs-lookup"><span data-stu-id="d055f-197">A webSite section is required, but the database section is optional.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d055f-198">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d055f-198">Next steps</span></span>
<span data-ttu-id="d055f-199">Para obter mais informações, consulte [WebApplicationVM de publicação (script do Windows PowerShell)](vs-azure-tools-publish-webapplicationvm.md)</span><span class="sxs-lookup"><span data-stu-id="d055f-199">For more information, see [Publish-WebApplicationVM (Windows PowerShell script)](vs-azure-tools-publish-webapplicationvm.md)</span></span>

