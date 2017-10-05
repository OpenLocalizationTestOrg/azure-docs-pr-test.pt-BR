---
title: Ferramentas para trabalhar com o Armazenamento do Azure | Microsoft Docs
description: Uma lista de ferramentas que permite exibir/interagir com os dados do Armazenamento do Azure.
services: storage
documentationcenter: 
author: dineshmurthy
manager: jahogg
editor: tysonn
ms.assetid: e4748642-98c4-437e-b0ed-4f9641c2e894
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: dineshmurthy
ms.openlocfilehash: 620efda06d8225b21b6bb9b104b79061ebb6515c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-client-tools"></a><span data-ttu-id="8afa9-103">Ferramentas de Cliente do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="8afa9-103">Azure Storage Client Tools</span></span>
<span data-ttu-id="8afa9-104">Com frequência, os usuários do Armazenamento do Azure desejam poder exibir/interagir com seus dados usando uma ferramenta de cliente do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8afa9-104">Users of Azure Storage frequently want to be able to view/interact with their data using an Azure Storage client tool.</span></span> <span data-ttu-id="8afa9-105">Nas tabelas abaixo, listamos várias ferramentas que permitem que você faça isso.</span><span class="sxs-lookup"><span data-stu-id="8afa9-105">In the tables below, we list a number of tools that allow you to do this.</span></span> <span data-ttu-id="8afa9-106">Colocamos um "X" em cada bloco caso a ferramenta forneça a capacidade de enumerar e/ou acessar a abstração de dados.</span><span class="sxs-lookup"><span data-stu-id="8afa9-106">We put an "X" in each block if it provides the ability to either enumerate and/or access the data abstraction.</span></span> <span data-ttu-id="8afa9-107">A tabela também mostra se as ferramentas são gratuitas ou não.</span><span class="sxs-lookup"><span data-stu-id="8afa9-107">The table also shows if the tools is free or not.</span></span> <span data-ttu-id="8afa9-108">"Avaliação" indica que há uma avaliação gratuita, mas o produto completo não é gratuito.</span><span class="sxs-lookup"><span data-stu-id="8afa9-108">"Trial" indicates that there is a free trial, but the full product is not free.</span></span> <span data-ttu-id="8afa9-109">"S/N" indica que uma versão está disponível gratuitamente, enquanto outra versão está disponível para compra.</span><span class="sxs-lookup"><span data-stu-id="8afa9-109">"Y/N" indicates that a version is available for free, while a different version is available for purchase.</span></span>

<span data-ttu-id="8afa9-110">Fornecemos somente um instantâneo das ferramentas de cliente do Armazenamento do Azure disponíveis.</span><span class="sxs-lookup"><span data-stu-id="8afa9-110">We've only provided a snapshot of the available Azure Storage client tools.</span></span> <span data-ttu-id="8afa9-111">Essas ferramentas poderão continuar a evoluir e expandir sua funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="8afa9-111">These tools may continue to evolve and grow in functionality.</span></span> <span data-ttu-id="8afa9-112">Se houver correções ou atualizações, deixe um comentário para nos contar.</span><span class="sxs-lookup"><span data-stu-id="8afa9-112">If there are corrections or updates, please leave a comment to let us know.</span></span> <span data-ttu-id="8afa9-113">O mesmo é verdadeiro se você conhecer ferramentas que deveriam estar aqui – ficaríamos felizes de adicioná-las.</span><span class="sxs-lookup"><span data-stu-id="8afa9-113">The same is true if you know of tools that ought to be here - we'd be happy to add them.</span></span>

<span data-ttu-id="8afa9-114">**Ferramentas de Cliente do Armazenamento do Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="8afa9-114">**Microsoft Azure Storage Client Tools**</span></span>

<table>
  <tr>
    <th rowspan="2"><span data-ttu-id="8afa9-115">Ferramenta de Cliente do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="8afa9-115">Azure Storage Client Tool</span></span></th>
    <th rowspan="2"><span data-ttu-id="8afa9-116">Blob de blocos</span><span class="sxs-lookup"><span data-stu-id="8afa9-116">Block Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="8afa9-117">Blob de páginas</span><span class="sxs-lookup"><span data-stu-id="8afa9-117">Page Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="8afa9-118">Acrescentar blob</span><span class="sxs-lookup"><span data-stu-id="8afa9-118">Append Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="8afa9-119">Tabelas</span><span class="sxs-lookup"><span data-stu-id="8afa9-119">Tables</span></span></th>
    <th rowspan="2"><span data-ttu-id="8afa9-120">Filas</span><span class="sxs-lookup"><span data-stu-id="8afa9-120">Queues</span></span></th>
    <th rowspan="2"><span data-ttu-id="8afa9-121">Arquivos</span><span class="sxs-lookup"><span data-stu-id="8afa9-121">Files</span></span></th>
    <th rowspan="2"><span data-ttu-id="8afa9-122">Grátis</span><span class="sxs-lookup"><span data-stu-id="8afa9-122">Free</span></span></th>
    <th colspan="4"><span data-ttu-id="8afa9-123">Plataforma</span><span class="sxs-lookup"><span data-stu-id="8afa9-123">Platform</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="8afa9-124">Web</span><span class="sxs-lookup"><span data-stu-id="8afa9-124">Web</span></span></td>
    <td><span data-ttu-id="8afa9-125">Windows</span><span class="sxs-lookup"><span data-stu-id="8afa9-125">Windows</span></span></td>
    <td><span data-ttu-id="8afa9-126">OSX</span><span class="sxs-lookup"><span data-stu-id="8afa9-126">OSX</span></span></td>
    <td><span data-ttu-id="8afa9-127">Linux</span><span class="sxs-lookup"><span data-stu-id="8afa9-127">Linux</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="8afa9-128"><a href="https://azure.microsoft.com/features/azure-portal/">Portal do Microsoft Azure</a></span><span class="sxs-lookup"><span data-stu-id="8afa9-128"><a href="https://azure.microsoft.com/features/azure-portal/">Microsoft Azure Portal</a></span></span></td>
    <td><span data-ttu-id="8afa9-129">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-129">X</span></span></td>
    <td><span data-ttu-id="8afa9-130">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-130">X</span></span></td>
    <td><span data-ttu-id="8afa9-131">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-131">X</span></span></td>
    <td><span data-ttu-id="8afa9-132">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-132">X</span></span></td>
    <td><span data-ttu-id="8afa9-133">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-133">X</span></span></td>
    <td><span data-ttu-id="8afa9-134">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-134">X</span></span></td>
    <td><span data-ttu-id="8afa9-135">S</span><span class="sxs-lookup"><span data-stu-id="8afa9-135">Y</span></span></td>
    <td><span data-ttu-id="8afa9-136">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-136">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="8afa9-137"><a href="http://storageexplorer.com/">Gerenciador do Armazenamento do Microsoft Azure</a></span><span class="sxs-lookup"><span data-stu-id="8afa9-137"><a href="http://storageexplorer.com/">Microsoft Azure Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="8afa9-138">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-138">X</span></span></td>
    <td><span data-ttu-id="8afa9-139">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-139">X</span></span></td>
    <td><span data-ttu-id="8afa9-140">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-140">X</span></span></td>
    <td><span data-ttu-id="8afa9-141">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-141">X</span></span></td>
    <td><span data-ttu-id="8afa9-142">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-142">X</span></span></td>
    <td><span data-ttu-id="8afa9-143">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-143">X</span></span></td>
    <td><span data-ttu-id="8afa9-144">S</span><span class="sxs-lookup"><span data-stu-id="8afa9-144">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="8afa9-145">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-145">X</span></span></td>
    <td><span data-ttu-id="8afa9-146">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-146">X</span></span></td>
    <td><span data-ttu-id="8afa9-147">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-147">X</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="8afa9-148"><a href="https://www.visualstudio.com/features/azure-tools-vs.aspx">Gerenciador de Servidores do Microsoft Visual Studio</a></span><span class="sxs-lookup"><span data-stu-id="8afa9-148"><a href="https://www.visualstudio.com/features/azure-tools-vs.aspx">Microsoft Visual Studio Server Explorer</a></span></span></td>
    <td><span data-ttu-id="8afa9-149">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-149">X</span></span></td>
    <td><span data-ttu-id="8afa9-150">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-150">X</span></span></td>
    <td><span data-ttu-id="8afa9-151">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-151">X</span></span></td>
    <td><span data-ttu-id="8afa9-152">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-152">X</span></span></td>
    <td><span data-ttu-id="8afa9-153">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-153">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="8afa9-154">S</span><span class="sxs-lookup"><span data-stu-id="8afa9-154">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="8afa9-155">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-155">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
</table>

<span data-ttu-id="8afa9-156">**Ferramentas de Cliente de terceiros do Armazenamento do Azure**</span><span class="sxs-lookup"><span data-stu-id="8afa9-156">**Third-Party Azure Storage Client Tools**</span></span>

<span data-ttu-id="8afa9-157">Nós não verificamos a funcionalidade nem a qualidade declarada pelas ferramentas de terceiros indicadas a seguir e sua listagem não implica o endosso da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8afa9-157">We have not verified the functionality or quality claimed by the following third-party tools and their listing does not imply an endorsement by Microsoft.</span></span>

<table>
  <tr>
    <th rowspan="2"><span data-ttu-id="8afa9-158">Ferramenta de Cliente do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="8afa9-158">Azure Storage Client Tool</span></span></th>
    <th rowspan="2"><span data-ttu-id="8afa9-159">Blob de blocos</span><span class="sxs-lookup"><span data-stu-id="8afa9-159">Block Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="8afa9-160">Blob de páginas</span><span class="sxs-lookup"><span data-stu-id="8afa9-160">Page Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="8afa9-161">Acrescentar blob</span><span class="sxs-lookup"><span data-stu-id="8afa9-161">Append Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="8afa9-162">Tabelas</span><span class="sxs-lookup"><span data-stu-id="8afa9-162">Tables</span></span></th>
    <th rowspan="2"><span data-ttu-id="8afa9-163">Filas</span><span class="sxs-lookup"><span data-stu-id="8afa9-163">Queues</span></span></th>
    <th rowspan="2"><span data-ttu-id="8afa9-164">Arquivos</span><span class="sxs-lookup"><span data-stu-id="8afa9-164">Files</span></span></th>
    <th rowspan="2"><span data-ttu-id="8afa9-165">Grátis</span><span class="sxs-lookup"><span data-stu-id="8afa9-165">Free</span></span></th>
    <th colspan="4"><span data-ttu-id="8afa9-166">Plataforma</span><span class="sxs-lookup"><span data-stu-id="8afa9-166">Platform</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="8afa9-167">Web</span><span class="sxs-lookup"><span data-stu-id="8afa9-167">Web</span></span></td>
    <td><span data-ttu-id="8afa9-168">Windows</span><span class="sxs-lookup"><span data-stu-id="8afa9-168">Windows</span></span></td>
    <td><span data-ttu-id="8afa9-169">OSX</span><span class="sxs-lookup"><span data-stu-id="8afa9-169">OSX</span></span></td>
    <td><span data-ttu-id="8afa9-170">Linux</span><span class="sxs-lookup"><span data-stu-id="8afa9-170">Linux</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="8afa9-171"><a href="http://www.cloudportam.com/">Cloud Portam</a></span><span class="sxs-lookup"><span data-stu-id="8afa9-171"><a href="http://www.cloudportam.com/">Cloud Portam</a></span></span></td>
    <td><span data-ttu-id="8afa9-172">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-172">X</span></span></td>
    <td><span data-ttu-id="8afa9-173">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-173">X</span></span></td>
    <td><span data-ttu-id="8afa9-174">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-174">X</span></span></td>
    <td><span data-ttu-id="8afa9-175">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-175">X</span></span></td>
    <td><span data-ttu-id="8afa9-176">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-176">X</span></span></td>
    <td><span data-ttu-id="8afa9-177">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-177">X</span></span></td>
    <td><span data-ttu-id="8afa9-178">Avaliação</span><span class="sxs-lookup"><span data-stu-id="8afa9-178">Trial</span></span></td>
    <td><span data-ttu-id="8afa9-179">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-179">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="8afa9-180"><a href="http://www.cerebrata.com/products/azure-management-studio/introduction">Cerabrata: Azure Management Studio</a></span><span class="sxs-lookup"><span data-stu-id="8afa9-180"><a href="http://www.cerebrata.com/products/azure-management-studio/introduction">Cerabrata: Azure Management Studio</a></span></span></td>
    <td><span data-ttu-id="8afa9-181">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-181">X</span></span></td>
    <td><span data-ttu-id="8afa9-182">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-182">X</span></span></td>
    <td><span data-ttu-id="8afa9-183">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-183">X</span></span></td>
    <td><span data-ttu-id="8afa9-184">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-184">X</span></span></td>
    <td><span data-ttu-id="8afa9-185">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-185">X</span></span></td>
    <td><span data-ttu-id="8afa9-186">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-186">X</span></span></td>
    <td><span data-ttu-id="8afa9-187">Avaliação</span><span class="sxs-lookup"><span data-stu-id="8afa9-187">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="8afa9-188">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-188">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="8afa9-189"><a href="http://www.cerebrata.com/products/azure-explorer/introduction">Cerabrata: Explorador do Azure</a></span><span class="sxs-lookup"><span data-stu-id="8afa9-189"><a href="http://www.cerebrata.com/products/azure-explorer/introduction">Cerabrata: Azure Explorer</a></span></span></td>
    <td><span data-ttu-id="8afa9-190">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-190">X</span></span></td>
    <td><span data-ttu-id="8afa9-191">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-191">X</span></span></td>
    <td><span data-ttu-id="8afa9-192">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-192">X</span></span></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="8afa9-193">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-193">X</span></span></td>
    <td><span data-ttu-id="8afa9-194">S</span><span class="sxs-lookup"><span data-stu-id="8afa9-194">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="8afa9-195">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-195">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="8afa9-196"><a href="https://github.com/sebagomez/azurestorageexplorer">Gerenciador de Armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="8afa9-196"><a href="https://github.com/sebagomez/azurestorageexplorer">Azure Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="8afa9-197">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-197">X</span></span></td>
    <td><span data-ttu-id="8afa9-198">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-198">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="8afa9-199">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-199">X</span></span></td>
    <td><span data-ttu-id="8afa9-200">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-200">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="8afa9-201">S</span><span class="sxs-lookup"><span data-stu-id="8afa9-201">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="8afa9-202">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-202">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="8afa9-203"><a href="http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx">CloudBerry Explorer</a></span><span class="sxs-lookup"><span data-stu-id="8afa9-203"><a href="http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx">CloudBerry Explorer</a></span></span></td>
    <td><span data-ttu-id="8afa9-204">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-204">X</span></span></td>
    <td><span data-ttu-id="8afa9-205">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-205">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="8afa9-206">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-206">X</span></span></td>
    <td><span data-ttu-id="8afa9-207">S/N</span><span class="sxs-lookup"><span data-stu-id="8afa9-207">Y/N</span></span></td>
    <td></td>
    <td><span data-ttu-id="8afa9-208">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-208">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="8afa9-209"><a href="http://www.gapotchenko.com/cloudcombine">Cloud Combine</a></span><span class="sxs-lookup"><span data-stu-id="8afa9-209"><a href="http://www.gapotchenko.com/cloudcombine">Cloud Combine</a></span></span></td>
    <td><span data-ttu-id="8afa9-210">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-210">X</span></span></td>
    <td><span data-ttu-id="8afa9-211">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-211">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="8afa9-212">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-212">X</span></span></td>
    <td><span data-ttu-id="8afa9-213">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-213">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="8afa9-214">Avaliação</span><span class="sxs-lookup"><span data-stu-id="8afa9-214">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="8afa9-215">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-215">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="8afa9-216"><a href="http://clumsyleaf.com">ClumsyLeaf: AzureXplorer, CloudXplorer, TableXplorer</a></span><span class="sxs-lookup"><span data-stu-id="8afa9-216"><a href="http://clumsyleaf.com">ClumsyLeaf: AzureXplorer, CloudXplorer, TableXplorer</a></span></span></td>
    <td><span data-ttu-id="8afa9-217">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-217">X</span></span></td>
    <td><span data-ttu-id="8afa9-218">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-218">X</span></span></td>
    <td><span data-ttu-id="8afa9-219">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-219">X</span></span></td>
    <td><span data-ttu-id="8afa9-220">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-220">X</span></span></td>
    <td><span data-ttu-id="8afa9-221">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-221">X</span></span></td>
    <td><span data-ttu-id="8afa9-222">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-222">X</span></span></td>
    <td><span data-ttu-id="8afa9-223">S</span><span class="sxs-lookup"><span data-stu-id="8afa9-223">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="8afa9-224">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-224">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="8afa9-225"><a href="http://www.gladinet.com/Azure-Storage/index.htm">Gladinet Cloud</a></span><span class="sxs-lookup"><span data-stu-id="8afa9-225"><a href="http://www.gladinet.com/Azure-Storage/index.htm">Gladinet Cloud</a></span></span></td>
    <td><span data-ttu-id="8afa9-226">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-226">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="8afa9-227">Avaliação</span><span class="sxs-lookup"><span data-stu-id="8afa9-227">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="8afa9-228">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-228">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="8afa9-229"><a href="http://storageexplorer.codeplex.com/">Navegador do Armazenamento da Web do Azure</a></span><span class="sxs-lookup"><span data-stu-id="8afa9-229"><a href="http://storageexplorer.codeplex.com/">Azure Web Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="8afa9-230">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-230">X</span></span></td>
    <td><span data-ttu-id="8afa9-231">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-231">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="8afa9-232">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-232">X</span></span></td>
    <td><span data-ttu-id="8afa9-233">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-233">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="8afa9-234">S</span><span class="sxs-lookup"><span data-stu-id="8afa9-234">Y</span></span></td>
    <td><span data-ttu-id="8afa9-235">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-235">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="8afa9-236"><a href="https://zudio.co/">Zudio</a></span><span class="sxs-lookup"><span data-stu-id="8afa9-236"><a href="https://zudio.co/">Zudio</a></span></span></td>
    <td><span data-ttu-id="8afa9-237">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-237">X</span></span></td>
    <td><span data-ttu-id="8afa9-238">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-238">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="8afa9-239">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-239">X</span></span></td>
    <td><span data-ttu-id="8afa9-240">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-240">X</span></span></td>
    <td><span data-ttu-id="8afa9-241">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-241">X</span></span></td>
    <td><span data-ttu-id="8afa9-242">Avaliação</span><span class="sxs-lookup"><span data-stu-id="8afa9-242">Trial</span></span></td>
    <td><span data-ttu-id="8afa9-243">X</span><span class="sxs-lookup"><span data-stu-id="8afa9-243">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</table>
