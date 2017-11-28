---
title: aaaPublish-WebApplicationWebSite (script do Windows PowerShell) | Microsoft Docs
description: "Saiba como toopublish uma web projeto tooan site do Azure. Este script cria recursos Olá necessários em sua assinatura do Azure se não existirem."
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
ms.openlocfilehash: d46904e30e3c2e040e57888fa31543e8e366527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a><span data-ttu-id="d4b53-104">Publish-WebApplicationWebSite (script do Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="d4b53-104">Publish-WebApplicationWebSite (Windows PowerShell script)</span></span>
## <a name="syntax"></a><span data-ttu-id="d4b53-105">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="d4b53-105">Syntax</span></span>
<span data-ttu-id="d4b53-106">Publica um tooan do projeto web site do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4b53-106">Publishes a web project tooan Azure website.</span></span> <span data-ttu-id="d4b53-107">script Hello cria recursos Olá necessários em sua assinatura do Azure se não existirem.</span><span class="sxs-lookup"><span data-stu-id="d4b53-107">hello script creates hello required resources in your Azure subscription if they don't exist.</span></span>

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a><span data-ttu-id="d4b53-108">Configuração</span><span class="sxs-lookup"><span data-stu-id="d4b53-108">Configuration</span></span>
<span data-ttu-id="d4b53-109">Olá caminho toohello arquivo de configuração JSON que descreve os detalhes de saudação da implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="d4b53-109">hello path toohello JSON configuration file that describes hello details of hello deployment.</span></span>

| <span data-ttu-id="d4b53-110">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d4b53-110">Parameter</span></span> | <span data-ttu-id="d4b53-111">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="d4b53-111">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="d4b53-112">Aliases</span><span class="sxs-lookup"><span data-stu-id="d4b53-112">Aliases</span></span> |<span data-ttu-id="d4b53-113">nenhum</span><span class="sxs-lookup"><span data-stu-id="d4b53-113">none</span></span> |
| <span data-ttu-id="d4b53-114">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="d4b53-114">Required?</span></span> |<span data-ttu-id="d4b53-115">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="d4b53-115">true</span></span> |
| <span data-ttu-id="d4b53-116">Position</span><span class="sxs-lookup"><span data-stu-id="d4b53-116">Position</span></span> |<span data-ttu-id="d4b53-117">nomeado</span><span class="sxs-lookup"><span data-stu-id="d4b53-117">named</span></span> |
| <span data-ttu-id="d4b53-118">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="d4b53-118">Default value</span></span> |<span data-ttu-id="d4b53-119">nenhum</span><span class="sxs-lookup"><span data-stu-id="d4b53-119">none</span></span> |
| <span data-ttu-id="d4b53-120">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="d4b53-120">Accept pipeline input?</span></span> |<span data-ttu-id="d4b53-121">false</span><span class="sxs-lookup"><span data-stu-id="d4b53-121">false</span></span> |
| <span data-ttu-id="d4b53-122">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="d4b53-122">Accept wildcard characters?</span></span> |<span data-ttu-id="d4b53-123">false</span><span class="sxs-lookup"><span data-stu-id="d4b53-123">false</span></span> |

## <a name="subscriptionname"></a><span data-ttu-id="d4b53-124">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="d4b53-124">SubscriptionName</span></span>
<span data-ttu-id="d4b53-125">nome de saudação do hello assinatura do Azure que você quiser que toocreate Olá site no.</span><span class="sxs-lookup"><span data-stu-id="d4b53-125">hello name of hello Azure subscription that you want toocreate hello website in.</span></span>

| <span data-ttu-id="d4b53-126">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d4b53-126">Parameter</span></span> | <span data-ttu-id="d4b53-127">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="d4b53-127">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="d4b53-128">Aliases</span><span class="sxs-lookup"><span data-stu-id="d4b53-128">Aliases</span></span> |<span data-ttu-id="d4b53-129">nenhum</span><span class="sxs-lookup"><span data-stu-id="d4b53-129">none</span></span> |
| <span data-ttu-id="d4b53-130">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="d4b53-130">Required?</span></span> |<span data-ttu-id="d4b53-131">false</span><span class="sxs-lookup"><span data-stu-id="d4b53-131">false</span></span> |
| <span data-ttu-id="d4b53-132">Position</span><span class="sxs-lookup"><span data-stu-id="d4b53-132">Position</span></span> |<span data-ttu-id="d4b53-133">nomeado</span><span class="sxs-lookup"><span data-stu-id="d4b53-133">named</span></span> |
| <span data-ttu-id="d4b53-134">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="d4b53-134">Default value</span></span> |<span data-ttu-id="d4b53-135">nenhum</span><span class="sxs-lookup"><span data-stu-id="d4b53-135">none</span></span> |
| <span data-ttu-id="d4b53-136">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="d4b53-136">Accept pipeline input?</span></span> |<span data-ttu-id="d4b53-137">false</span><span class="sxs-lookup"><span data-stu-id="d4b53-137">false</span></span> |
| <span data-ttu-id="d4b53-138">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="d4b53-138">Accept wildcard characters?</span></span> |<span data-ttu-id="d4b53-139">false</span><span class="sxs-lookup"><span data-stu-id="d4b53-139">false</span></span> |

## <a name="webdeploypackage"></a><span data-ttu-id="d4b53-140">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="d4b53-140">WebDeployPackage</span></span>
<span data-ttu-id="d4b53-141">Olá caminho toohello web pacote toopublish toohello site de implantação.</span><span class="sxs-lookup"><span data-stu-id="d4b53-141">hello path toohello web deployment package toopublish toohello website.</span></span> <span data-ttu-id="d4b53-142">Você pode criar esse pacote usando o Assistente de publicar Web Olá no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d4b53-142">You can create this package by using hello Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="d4b53-143">Para obter mais informações, consulte [Introdução aos serviços de nuvem do Azure e ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span><span class="sxs-lookup"><span data-stu-id="d4b53-143">For more information, see [Get started with Azure Cloud Services and ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span></span>

| <span data-ttu-id="d4b53-144">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d4b53-144">Parameter</span></span> | <span data-ttu-id="d4b53-145">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="d4b53-145">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="d4b53-146">Aliases</span><span class="sxs-lookup"><span data-stu-id="d4b53-146">Aliases</span></span> |<span data-ttu-id="d4b53-147">nenhum</span><span class="sxs-lookup"><span data-stu-id="d4b53-147">none</span></span> |
| <span data-ttu-id="d4b53-148">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="d4b53-148">Required?</span></span> |<span data-ttu-id="d4b53-149">false</span><span class="sxs-lookup"><span data-stu-id="d4b53-149">false</span></span> |
| <span data-ttu-id="d4b53-150">Position</span><span class="sxs-lookup"><span data-stu-id="d4b53-150">Position</span></span> |<span data-ttu-id="d4b53-151">nomeado</span><span class="sxs-lookup"><span data-stu-id="d4b53-151">named</span></span> |
| <span data-ttu-id="d4b53-152">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="d4b53-152">Default value</span></span> |<span data-ttu-id="d4b53-153">nenhum</span><span class="sxs-lookup"><span data-stu-id="d4b53-153">none</span></span> |
| <span data-ttu-id="d4b53-154">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="d4b53-154">Accept pipeline input?</span></span> |<span data-ttu-id="d4b53-155">false</span><span class="sxs-lookup"><span data-stu-id="d4b53-155">false</span></span> |
| <span data-ttu-id="d4b53-156">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="d4b53-156">Accept wildcard characters?</span></span> |<span data-ttu-id="d4b53-157">false</span><span class="sxs-lookup"><span data-stu-id="d4b53-157">false</span></span> |

## <a name="databaseserverpassword"></a><span data-ttu-id="d4b53-158">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="d4b53-158">DatabaseServerPassword</span></span>
<span data-ttu-id="d4b53-159">saudação de nome de usuário e senha Olá banco de dados SQL no Azure.</span><span class="sxs-lookup"><span data-stu-id="d4b53-159">hello username and password for hello SQL database in Azure.</span></span>

| <span data-ttu-id="d4b53-160">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d4b53-160">Parameter</span></span> | <span data-ttu-id="d4b53-161">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="d4b53-161">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="d4b53-162">Aliases</span><span class="sxs-lookup"><span data-stu-id="d4b53-162">Aliases</span></span> |<span data-ttu-id="d4b53-163">nenhum</span><span class="sxs-lookup"><span data-stu-id="d4b53-163">none</span></span> |
| <span data-ttu-id="d4b53-164">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="d4b53-164">Required?</span></span> |<span data-ttu-id="d4b53-165">false</span><span class="sxs-lookup"><span data-stu-id="d4b53-165">false</span></span> |
| <span data-ttu-id="d4b53-166">Position</span><span class="sxs-lookup"><span data-stu-id="d4b53-166">Position</span></span> |<span data-ttu-id="d4b53-167">nomeado</span><span class="sxs-lookup"><span data-stu-id="d4b53-167">named</span></span> |
| <span data-ttu-id="d4b53-168">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="d4b53-168">Default value</span></span> |<span data-ttu-id="d4b53-169">nenhum</span><span class="sxs-lookup"><span data-stu-id="d4b53-169">none</span></span> |
| <span data-ttu-id="d4b53-170">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="d4b53-170">Accept pipeline input?</span></span> |<span data-ttu-id="d4b53-171">false</span><span class="sxs-lookup"><span data-stu-id="d4b53-171">false</span></span> |
| <span data-ttu-id="d4b53-172">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="d4b53-172">Accept wildcard characters?</span></span> |<span data-ttu-id="d4b53-173">false</span><span class="sxs-lookup"><span data-stu-id="d4b53-173">false</span></span> |

## <a name="sendhostmessagestooutput"></a><span data-ttu-id="d4b53-174">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="d4b53-174">SendHostMessagesToOutput</span></span>
<span data-ttu-id="d4b53-175">Se true, impressão mensagens de saudação script toohello fluxo de saída.</span><span class="sxs-lookup"><span data-stu-id="d4b53-175">If true, print messages from hello script toohello output stream.</span></span>

| <span data-ttu-id="d4b53-176">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="d4b53-176">Parameter</span></span> | <span data-ttu-id="d4b53-177">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="d4b53-177">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="d4b53-178">Aliases</span><span class="sxs-lookup"><span data-stu-id="d4b53-178">Aliases</span></span> |<span data-ttu-id="d4b53-179">nenhum</span><span class="sxs-lookup"><span data-stu-id="d4b53-179">none</span></span> |
| <span data-ttu-id="d4b53-180">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="d4b53-180">Required?</span></span> |<span data-ttu-id="d4b53-181">false</span><span class="sxs-lookup"><span data-stu-id="d4b53-181">false</span></span> |
| <span data-ttu-id="d4b53-182">Position</span><span class="sxs-lookup"><span data-stu-id="d4b53-182">Position</span></span> |<span data-ttu-id="d4b53-183">nomeado</span><span class="sxs-lookup"><span data-stu-id="d4b53-183">named</span></span> |
| <span data-ttu-id="d4b53-184">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="d4b53-184">Default value</span></span> |<span data-ttu-id="d4b53-185">false</span><span class="sxs-lookup"><span data-stu-id="d4b53-185">false</span></span> |
| <span data-ttu-id="d4b53-186">Aceitar entrada do Pipeline?</span><span class="sxs-lookup"><span data-stu-id="d4b53-186">Accept pipeline input?</span></span> |<span data-ttu-id="d4b53-187">false</span><span class="sxs-lookup"><span data-stu-id="d4b53-187">false</span></span> |
| <span data-ttu-id="d4b53-188">Aceitar caracteres curinga?</span><span class="sxs-lookup"><span data-stu-id="d4b53-188">Accept wildcard characters?</span></span> |<span data-ttu-id="d4b53-189">false</span><span class="sxs-lookup"><span data-stu-id="d4b53-189">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="d4b53-190">Comentários</span><span class="sxs-lookup"><span data-stu-id="d4b53-190">Remarks</span></span>
<span data-ttu-id="d4b53-191">Para obter uma explicação completa de como toouse Olá script toocreate desenvolvimento e ambientes de teste, consulte [ambientes de teste e usando Scripts do Windows PowerShell tooPublish tooDev](vs-azure-tools-publishing-using-powershell-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="d4b53-191">For a complete explanation of how toouse hello script toocreate Dev and Test environments, see [Using Windows PowerShell Scripts tooPublish tooDev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="d4b53-192">arquivo de configuração JSON Olá Especifica detalhes de saudação do que é toobe implantado.</span><span class="sxs-lookup"><span data-stu-id="d4b53-192">hello JSON configuration file specifies hello details of what is toobe deployed.</span></span> <span data-ttu-id="d4b53-193">Ela inclui informações de saudação que você especificou quando criou o projeto hello, como nome de saudação e o nome de usuário para o site de saudação.</span><span class="sxs-lookup"><span data-stu-id="d4b53-193">It includes hello information that you specified when you created hello project, such as hello name and username for hello website.</span></span> <span data-ttu-id="d4b53-194">Ele também inclui Olá tooprovision do banco de dados, se houver.</span><span class="sxs-lookup"><span data-stu-id="d4b53-194">It also includes hello database tooprovision, if any.</span></span> <span data-ttu-id="d4b53-195">saudação de código a seguir mostra um exemplo de arquivo de configuração de JSON:</span><span class="sxs-lookup"><span data-stu-id="d4b53-195">hello following code shows an example JSON configuration file:</span></span>

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

<span data-ttu-id="d4b53-196">Você pode editar o arquivo de configuração do hello JSON toochange o que foi implantado.</span><span class="sxs-lookup"><span data-stu-id="d4b53-196">You can edit hello JSON configuration file toochange what is deployed.</span></span> <span data-ttu-id="d4b53-197">Uma seção do site é necessária, mas a seção de banco de dados de saudação é opcional.</span><span class="sxs-lookup"><span data-stu-id="d4b53-197">A webSite section is required, but hello database section is optional.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4b53-198">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d4b53-198">Next steps</span></span>
<span data-ttu-id="d4b53-199">Para obter mais informações, consulte [WebApplicationVM de publicação (script do Windows PowerShell)](vs-azure-tools-publish-webapplicationvm.md)</span><span class="sxs-lookup"><span data-stu-id="d4b53-199">For more information, see [Publish-WebApplicationVM (Windows PowerShell script)](vs-azure-tools-publish-webapplicationvm.md)</span></span>

