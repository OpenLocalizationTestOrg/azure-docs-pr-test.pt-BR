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
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-storage-client-tools"></a><span data-ttu-id="66d33-103">Ferramentas de Cliente do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="66d33-103">Azure Storage Client Tools</span></span>
<span data-ttu-id="66d33-104">Com frequência, os usuários do Armazenamento do Azure desejam poder exibir/interagir com seus dados usando uma ferramenta de cliente do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="66d33-104">Users of Azure Storage frequently want to be able to view/interact with their data using an Azure Storage client tool.</span></span> <span data-ttu-id="66d33-105">Nas tabelas abaixo, listamos várias ferramentas que permitem que você faça isso.</span><span class="sxs-lookup"><span data-stu-id="66d33-105">In the tables below, we list a number of tools that allow you to do this.</span></span> <span data-ttu-id="66d33-106">Colocamos um "X" em cada bloco caso a ferramenta forneça a capacidade de enumerar e/ou acessar a abstração de dados.</span><span class="sxs-lookup"><span data-stu-id="66d33-106">We put an "X" in each block if it provides the ability to either enumerate and/or access the data abstraction.</span></span> <span data-ttu-id="66d33-107">A tabela também mostra se as ferramentas são gratuitas ou não.</span><span class="sxs-lookup"><span data-stu-id="66d33-107">The table also shows if the tools is free or not.</span></span> <span data-ttu-id="66d33-108">"Avaliação" indica que há uma avaliação gratuita, mas o produto completo não é gratuito.</span><span class="sxs-lookup"><span data-stu-id="66d33-108">"Trial" indicates that there is a free trial, but the full product is not free.</span></span> <span data-ttu-id="66d33-109">"S/N" indica que uma versão está disponível gratuitamente, enquanto outra versão está disponível para compra.</span><span class="sxs-lookup"><span data-stu-id="66d33-109">"Y/N" indicates that a version is available for free, while a different version is available for purchase.</span></span>

<span data-ttu-id="66d33-110">Fornecemos somente um instantâneo das ferramentas de cliente do Armazenamento do Azure disponíveis.</span><span class="sxs-lookup"><span data-stu-id="66d33-110">We've only provided a snapshot of the available Azure Storage client tools.</span></span> <span data-ttu-id="66d33-111">Essas ferramentas poderão continuar a evoluir e expandir sua funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="66d33-111">These tools may continue to evolve and grow in functionality.</span></span> <span data-ttu-id="66d33-112">Se houver correções ou atualizações, deixe um comentário para nos contar.</span><span class="sxs-lookup"><span data-stu-id="66d33-112">If there are corrections or updates, please leave a comment to let us know.</span></span> <span data-ttu-id="66d33-113">O mesmo é verdadeiro se você conhecer ferramentas que deveriam estar aqui – ficaríamos felizes de adicioná-las.</span><span class="sxs-lookup"><span data-stu-id="66d33-113">The same is true if you know of tools that ought to be here - we'd be happy to add them.</span></span>

<span data-ttu-id="66d33-114">**Ferramentas de Cliente do Armazenamento do Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="66d33-114">**Microsoft Azure Storage Client Tools**</span></span>

<table>
  <tr>
    <th rowspan="2"><span data-ttu-id="66d33-115">Ferramenta de Cliente do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="66d33-115">Azure Storage Client Tool</span></span></th>
    <th rowspan="2"><span data-ttu-id="66d33-116">Blob de blocos</span><span class="sxs-lookup"><span data-stu-id="66d33-116">Block Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="66d33-117">Blob de páginas</span><span class="sxs-lookup"><span data-stu-id="66d33-117">Page Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="66d33-118">Acrescentar blob</span><span class="sxs-lookup"><span data-stu-id="66d33-118">Append Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="66d33-119">Tabelas</span><span class="sxs-lookup"><span data-stu-id="66d33-119">Tables</span></span></th>
    <th rowspan="2"><span data-ttu-id="66d33-120">Filas</span><span class="sxs-lookup"><span data-stu-id="66d33-120">Queues</span></span></th>
    <th rowspan="2"><span data-ttu-id="66d33-121">Arquivos</span><span class="sxs-lookup"><span data-stu-id="66d33-121">Files</span></span></th>
    <th rowspan="2"><span data-ttu-id="66d33-122">Grátis</span><span class="sxs-lookup"><span data-stu-id="66d33-122">Free</span></span></th>
    <th colspan="4"><span data-ttu-id="66d33-123">Plataforma</span><span class="sxs-lookup"><span data-stu-id="66d33-123">Platform</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="66d33-124">Web</span><span class="sxs-lookup"><span data-stu-id="66d33-124">Web</span></span></td>
    <td><span data-ttu-id="66d33-125">Windows</span><span class="sxs-lookup"><span data-stu-id="66d33-125">Windows</span></span></td>
    <td><span data-ttu-id="66d33-126">OSX</span><span class="sxs-lookup"><span data-stu-id="66d33-126">OSX</span></span></td>
    <td><span data-ttu-id="66d33-127">Linux</span><span class="sxs-lookup"><span data-stu-id="66d33-127">Linux</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="66d33-128"><a href="https://azure.microsoft.com/features/azure-portal/">Portal do Microsoft Azure</a></span><span class="sxs-lookup"><span data-stu-id="66d33-128"><a href="https://azure.microsoft.com/features/azure-portal/">Microsoft Azure Portal</a></span></span></td>
    <td><span data-ttu-id="66d33-129">X</span><span class="sxs-lookup"><span data-stu-id="66d33-129">X</span></span></td>
    <td><span data-ttu-id="66d33-130">X</span><span class="sxs-lookup"><span data-stu-id="66d33-130">X</span></span></td>
    <td><span data-ttu-id="66d33-131">X</span><span class="sxs-lookup"><span data-stu-id="66d33-131">X</span></span></td>
    <td><span data-ttu-id="66d33-132">X</span><span class="sxs-lookup"><span data-stu-id="66d33-132">X</span></span></td>
    <td><span data-ttu-id="66d33-133">X</span><span class="sxs-lookup"><span data-stu-id="66d33-133">X</span></span></td>
    <td><span data-ttu-id="66d33-134">X</span><span class="sxs-lookup"><span data-stu-id="66d33-134">X</span></span></td>
    <td><span data-ttu-id="66d33-135">S</span><span class="sxs-lookup"><span data-stu-id="66d33-135">Y</span></span></td>
    <td><span data-ttu-id="66d33-136">X</span><span class="sxs-lookup"><span data-stu-id="66d33-136">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="66d33-137"><a href="http://storageexplorer.com/">Gerenciador do Armazenamento do Microsoft Azure</a></span><span class="sxs-lookup"><span data-stu-id="66d33-137"><a href="http://storageexplorer.com/">Microsoft Azure Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="66d33-138">X</span><span class="sxs-lookup"><span data-stu-id="66d33-138">X</span></span></td>
    <td><span data-ttu-id="66d33-139">X</span><span class="sxs-lookup"><span data-stu-id="66d33-139">X</span></span></td>
    <td><span data-ttu-id="66d33-140">X</span><span class="sxs-lookup"><span data-stu-id="66d33-140">X</span></span></td>
    <td><span data-ttu-id="66d33-141">X</span><span class="sxs-lookup"><span data-stu-id="66d33-141">X</span></span></td>
    <td><span data-ttu-id="66d33-142">X</span><span class="sxs-lookup"><span data-stu-id="66d33-142">X</span></span></td>
    <td><span data-ttu-id="66d33-143">X</span><span class="sxs-lookup"><span data-stu-id="66d33-143">X</span></span></td>
    <td><span data-ttu-id="66d33-144">S</span><span class="sxs-lookup"><span data-stu-id="66d33-144">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="66d33-145">X</span><span class="sxs-lookup"><span data-stu-id="66d33-145">X</span></span></td>
    <td><span data-ttu-id="66d33-146">X</span><span class="sxs-lookup"><span data-stu-id="66d33-146">X</span></span></td>
    <td><span data-ttu-id="66d33-147">X</span><span class="sxs-lookup"><span data-stu-id="66d33-147">X</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="66d33-148"><a href="https://www.visualstudio.com/features/azure-tools-vs.aspx">Gerenciador de Servidores do Microsoft Visual Studio</a></span><span class="sxs-lookup"><span data-stu-id="66d33-148"><a href="https://www.visualstudio.com/features/azure-tools-vs.aspx">Microsoft Visual Studio Server Explorer</a></span></span></td>
    <td><span data-ttu-id="66d33-149">X</span><span class="sxs-lookup"><span data-stu-id="66d33-149">X</span></span></td>
    <td><span data-ttu-id="66d33-150">X</span><span class="sxs-lookup"><span data-stu-id="66d33-150">X</span></span></td>
    <td><span data-ttu-id="66d33-151">X</span><span class="sxs-lookup"><span data-stu-id="66d33-151">X</span></span></td>
    <td><span data-ttu-id="66d33-152">X</span><span class="sxs-lookup"><span data-stu-id="66d33-152">X</span></span></td>
    <td><span data-ttu-id="66d33-153">X</span><span class="sxs-lookup"><span data-stu-id="66d33-153">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="66d33-154">S</span><span class="sxs-lookup"><span data-stu-id="66d33-154">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="66d33-155">X</span><span class="sxs-lookup"><span data-stu-id="66d33-155">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
</table>

<span data-ttu-id="66d33-156">**Ferramentas de Cliente de terceiros do Armazenamento do Azure**</span><span class="sxs-lookup"><span data-stu-id="66d33-156">**Third-Party Azure Storage Client Tools**</span></span>

<span data-ttu-id="66d33-157">Nós não verificamos a funcionalidade nem a qualidade declarada pelas ferramentas de terceiros indicadas a seguir e sua listagem não implica o endosso da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="66d33-157">We have not verified the functionality or quality claimed by the following third-party tools and their listing does not imply an endorsement by Microsoft.</span></span>

<table>
  <tr>
    <th rowspan="2"><span data-ttu-id="66d33-158">Ferramenta de Cliente do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="66d33-158">Azure Storage Client Tool</span></span></th>
    <th rowspan="2"><span data-ttu-id="66d33-159">Blob de blocos</span><span class="sxs-lookup"><span data-stu-id="66d33-159">Block Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="66d33-160">Blob de páginas</span><span class="sxs-lookup"><span data-stu-id="66d33-160">Page Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="66d33-161">Acrescentar blob</span><span class="sxs-lookup"><span data-stu-id="66d33-161">Append Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="66d33-162">Tabelas</span><span class="sxs-lookup"><span data-stu-id="66d33-162">Tables</span></span></th>
    <th rowspan="2"><span data-ttu-id="66d33-163">Filas</span><span class="sxs-lookup"><span data-stu-id="66d33-163">Queues</span></span></th>
    <th rowspan="2"><span data-ttu-id="66d33-164">Arquivos</span><span class="sxs-lookup"><span data-stu-id="66d33-164">Files</span></span></th>
    <th rowspan="2"><span data-ttu-id="66d33-165">Grátis</span><span class="sxs-lookup"><span data-stu-id="66d33-165">Free</span></span></th>
    <th colspan="4"><span data-ttu-id="66d33-166">Plataforma</span><span class="sxs-lookup"><span data-stu-id="66d33-166">Platform</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="66d33-167">Web</span><span class="sxs-lookup"><span data-stu-id="66d33-167">Web</span></span></td>
    <td><span data-ttu-id="66d33-168">Windows</span><span class="sxs-lookup"><span data-stu-id="66d33-168">Windows</span></span></td>
    <td><span data-ttu-id="66d33-169">OSX</span><span class="sxs-lookup"><span data-stu-id="66d33-169">OSX</span></span></td>
    <td><span data-ttu-id="66d33-170">Linux</span><span class="sxs-lookup"><span data-stu-id="66d33-170">Linux</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="66d33-171"><a href="http://www.cloudportam.com/">Cloud Portam</a></span><span class="sxs-lookup"><span data-stu-id="66d33-171"><a href="http://www.cloudportam.com/">Cloud Portam</a></span></span></td>
    <td><span data-ttu-id="66d33-172">X</span><span class="sxs-lookup"><span data-stu-id="66d33-172">X</span></span></td>
    <td><span data-ttu-id="66d33-173">X</span><span class="sxs-lookup"><span data-stu-id="66d33-173">X</span></span></td>
    <td><span data-ttu-id="66d33-174">X</span><span class="sxs-lookup"><span data-stu-id="66d33-174">X</span></span></td>
    <td><span data-ttu-id="66d33-175">X</span><span class="sxs-lookup"><span data-stu-id="66d33-175">X</span></span></td>
    <td><span data-ttu-id="66d33-176">X</span><span class="sxs-lookup"><span data-stu-id="66d33-176">X</span></span></td>
    <td><span data-ttu-id="66d33-177">X</span><span class="sxs-lookup"><span data-stu-id="66d33-177">X</span></span></td>
    <td><span data-ttu-id="66d33-178">Avaliação</span><span class="sxs-lookup"><span data-stu-id="66d33-178">Trial</span></span></td>
    <td><span data-ttu-id="66d33-179">X</span><span class="sxs-lookup"><span data-stu-id="66d33-179">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="66d33-180"><a href="http://www.cerebrata.com/products/azure-management-studio/introduction">Cerabrata: Azure Management Studio</a></span><span class="sxs-lookup"><span data-stu-id="66d33-180"><a href="http://www.cerebrata.com/products/azure-management-studio/introduction">Cerabrata: Azure Management Studio</a></span></span></td>
    <td><span data-ttu-id="66d33-181">X</span><span class="sxs-lookup"><span data-stu-id="66d33-181">X</span></span></td>
    <td><span data-ttu-id="66d33-182">X</span><span class="sxs-lookup"><span data-stu-id="66d33-182">X</span></span></td>
    <td><span data-ttu-id="66d33-183">X</span><span class="sxs-lookup"><span data-stu-id="66d33-183">X</span></span></td>
    <td><span data-ttu-id="66d33-184">X</span><span class="sxs-lookup"><span data-stu-id="66d33-184">X</span></span></td>
    <td><span data-ttu-id="66d33-185">X</span><span class="sxs-lookup"><span data-stu-id="66d33-185">X</span></span></td>
    <td><span data-ttu-id="66d33-186">X</span><span class="sxs-lookup"><span data-stu-id="66d33-186">X</span></span></td>
    <td><span data-ttu-id="66d33-187">Avaliação</span><span class="sxs-lookup"><span data-stu-id="66d33-187">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="66d33-188">X</span><span class="sxs-lookup"><span data-stu-id="66d33-188">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="66d33-189"><a href="http://www.cerebrata.com/products/azure-explorer/introduction">Cerabrata: Explorador do Azure</a></span><span class="sxs-lookup"><span data-stu-id="66d33-189"><a href="http://www.cerebrata.com/products/azure-explorer/introduction">Cerabrata: Azure Explorer</a></span></span></td>
    <td><span data-ttu-id="66d33-190">X</span><span class="sxs-lookup"><span data-stu-id="66d33-190">X</span></span></td>
    <td><span data-ttu-id="66d33-191">X</span><span class="sxs-lookup"><span data-stu-id="66d33-191">X</span></span></td>
    <td><span data-ttu-id="66d33-192">X</span><span class="sxs-lookup"><span data-stu-id="66d33-192">X</span></span></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="66d33-193">X</span><span class="sxs-lookup"><span data-stu-id="66d33-193">X</span></span></td>
    <td><span data-ttu-id="66d33-194">S</span><span class="sxs-lookup"><span data-stu-id="66d33-194">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="66d33-195">X</span><span class="sxs-lookup"><span data-stu-id="66d33-195">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="66d33-196"><a href="https://github.com/sebagomez/azurestorageexplorer">Gerenciador de Armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="66d33-196"><a href="https://github.com/sebagomez/azurestorageexplorer">Azure Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="66d33-197">X</span><span class="sxs-lookup"><span data-stu-id="66d33-197">X</span></span></td>
    <td><span data-ttu-id="66d33-198">X</span><span class="sxs-lookup"><span data-stu-id="66d33-198">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="66d33-199">X</span><span class="sxs-lookup"><span data-stu-id="66d33-199">X</span></span></td>
    <td><span data-ttu-id="66d33-200">X</span><span class="sxs-lookup"><span data-stu-id="66d33-200">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="66d33-201">S</span><span class="sxs-lookup"><span data-stu-id="66d33-201">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="66d33-202">X</span><span class="sxs-lookup"><span data-stu-id="66d33-202">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="66d33-203"><a href="http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx">CloudBerry Explorer</a></span><span class="sxs-lookup"><span data-stu-id="66d33-203"><a href="http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx">CloudBerry Explorer</a></span></span></td>
    <td><span data-ttu-id="66d33-204">X</span><span class="sxs-lookup"><span data-stu-id="66d33-204">X</span></span></td>
    <td><span data-ttu-id="66d33-205">X</span><span class="sxs-lookup"><span data-stu-id="66d33-205">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="66d33-206">X</span><span class="sxs-lookup"><span data-stu-id="66d33-206">X</span></span></td>
    <td><span data-ttu-id="66d33-207">S/N</span><span class="sxs-lookup"><span data-stu-id="66d33-207">Y/N</span></span></td>
    <td></td>
    <td><span data-ttu-id="66d33-208">X</span><span class="sxs-lookup"><span data-stu-id="66d33-208">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="66d33-209"><a href="http://www.gapotchenko.com/cloudcombine">Cloud Combine</a></span><span class="sxs-lookup"><span data-stu-id="66d33-209"><a href="http://www.gapotchenko.com/cloudcombine">Cloud Combine</a></span></span></td>
    <td><span data-ttu-id="66d33-210">X</span><span class="sxs-lookup"><span data-stu-id="66d33-210">X</span></span></td>
    <td><span data-ttu-id="66d33-211">X</span><span class="sxs-lookup"><span data-stu-id="66d33-211">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="66d33-212">X</span><span class="sxs-lookup"><span data-stu-id="66d33-212">X</span></span></td>
    <td><span data-ttu-id="66d33-213">X</span><span class="sxs-lookup"><span data-stu-id="66d33-213">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="66d33-214">Avaliação</span><span class="sxs-lookup"><span data-stu-id="66d33-214">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="66d33-215">X</span><span class="sxs-lookup"><span data-stu-id="66d33-215">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="66d33-216"><a href="http://clumsyleaf.com">ClumsyLeaf: AzureXplorer, CloudXplorer, TableXplorer</a></span><span class="sxs-lookup"><span data-stu-id="66d33-216"><a href="http://clumsyleaf.com">ClumsyLeaf: AzureXplorer, CloudXplorer, TableXplorer</a></span></span></td>
    <td><span data-ttu-id="66d33-217">X</span><span class="sxs-lookup"><span data-stu-id="66d33-217">X</span></span></td>
    <td><span data-ttu-id="66d33-218">X</span><span class="sxs-lookup"><span data-stu-id="66d33-218">X</span></span></td>
    <td><span data-ttu-id="66d33-219">X</span><span class="sxs-lookup"><span data-stu-id="66d33-219">X</span></span></td>
    <td><span data-ttu-id="66d33-220">X</span><span class="sxs-lookup"><span data-stu-id="66d33-220">X</span></span></td>
    <td><span data-ttu-id="66d33-221">X</span><span class="sxs-lookup"><span data-stu-id="66d33-221">X</span></span></td>
    <td><span data-ttu-id="66d33-222">X</span><span class="sxs-lookup"><span data-stu-id="66d33-222">X</span></span></td>
    <td><span data-ttu-id="66d33-223">S</span><span class="sxs-lookup"><span data-stu-id="66d33-223">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="66d33-224">X</span><span class="sxs-lookup"><span data-stu-id="66d33-224">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="66d33-225"><a href="http://www.gladinet.com/Azure-Storage/index.htm">Gladinet Cloud</a></span><span class="sxs-lookup"><span data-stu-id="66d33-225"><a href="http://www.gladinet.com/Azure-Storage/index.htm">Gladinet Cloud</a></span></span></td>
    <td><span data-ttu-id="66d33-226">X</span><span class="sxs-lookup"><span data-stu-id="66d33-226">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="66d33-227">Avaliação</span><span class="sxs-lookup"><span data-stu-id="66d33-227">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="66d33-228">X</span><span class="sxs-lookup"><span data-stu-id="66d33-228">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="66d33-229"><a href="http://storageexplorer.codeplex.com/">Navegador do Armazenamento da Web do Azure</a></span><span class="sxs-lookup"><span data-stu-id="66d33-229"><a href="http://storageexplorer.codeplex.com/">Azure Web Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="66d33-230">X</span><span class="sxs-lookup"><span data-stu-id="66d33-230">X</span></span></td>
    <td><span data-ttu-id="66d33-231">X</span><span class="sxs-lookup"><span data-stu-id="66d33-231">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="66d33-232">X</span><span class="sxs-lookup"><span data-stu-id="66d33-232">X</span></span></td>
    <td><span data-ttu-id="66d33-233">X</span><span class="sxs-lookup"><span data-stu-id="66d33-233">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="66d33-234">S</span><span class="sxs-lookup"><span data-stu-id="66d33-234">Y</span></span></td>
    <td><span data-ttu-id="66d33-235">X</span><span class="sxs-lookup"><span data-stu-id="66d33-235">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="66d33-236"><a href="https://zudio.co/">Zudio</a></span><span class="sxs-lookup"><span data-stu-id="66d33-236"><a href="https://zudio.co/">Zudio</a></span></span></td>
    <td><span data-ttu-id="66d33-237">X</span><span class="sxs-lookup"><span data-stu-id="66d33-237">X</span></span></td>
    <td><span data-ttu-id="66d33-238">X</span><span class="sxs-lookup"><span data-stu-id="66d33-238">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="66d33-239">X</span><span class="sxs-lookup"><span data-stu-id="66d33-239">X</span></span></td>
    <td><span data-ttu-id="66d33-240">X</span><span class="sxs-lookup"><span data-stu-id="66d33-240">X</span></span></td>
    <td><span data-ttu-id="66d33-241">X</span><span class="sxs-lookup"><span data-stu-id="66d33-241">X</span></span></td>
    <td><span data-ttu-id="66d33-242">Avaliação</span><span class="sxs-lookup"><span data-stu-id="66d33-242">Trial</span></span></td>
    <td><span data-ttu-id="66d33-243">X</span><span class="sxs-lookup"><span data-stu-id="66d33-243">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</table>
