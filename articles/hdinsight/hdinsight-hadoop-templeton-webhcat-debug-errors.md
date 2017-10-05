---
title: "Entenda e resolva erros do WebHCat no HDInsight – Azure | Microsoft Docs"
description: "Saiba sobre erros comuns retornados pelo WebHCat no HDInsight e como resolvê-los."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1b3d94b1-207d-4550-aece-21dc45485549
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 6d8162e0d64ec9fc42690392b7c822593c0c2767
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a><span data-ttu-id="dbd3b-103">Entenda e resolva erros recebidos do WebHCat no HDInsight</span><span class="sxs-lookup"><span data-stu-id="dbd3b-103">Understand and resolve errors received from WebHCat on HDInsight</span></span>

<span data-ttu-id="dbd3b-104">Saiba mais sobre erros recebidos ao usar o WebHCat com HDInsight e como resolvê-los.</span><span class="sxs-lookup"><span data-stu-id="dbd3b-104">Learn about errors received when using WebHCat with HDInsight, and how to resolve them.</span></span> <span data-ttu-id="dbd3b-105">WebHCat é usado internamente por ferramentas de cliente como o Azure PowerShell e as Ferramentas do Data Lake para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dbd3b-105">WebHCat is used internally by client-side tools such as Azure PowerShell and the Data Lake Tools for Visual Studio.</span></span>

## <a name="what-is-webhcat"></a><span data-ttu-id="dbd3b-106">O que é o WebHCat</span><span class="sxs-lookup"><span data-stu-id="dbd3b-106">What is WebHCat</span></span>

<span data-ttu-id="dbd3b-107">O [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) é uma API REST para o [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), uma camada de gerenciamento de armazenamento e tabela para Hadoop.</span><span class="sxs-lookup"><span data-stu-id="dbd3b-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) is a REST API for [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), a table, and storage management layer for Hadoop.</span></span> <span data-ttu-id="dbd3b-108">O WebHCat é habilitado por padrão em clusters do HDInsight e é usado por várias ferramentas para enviar trabalhos, obter o status do trabalho etc. sem logon no cluster.</span><span class="sxs-lookup"><span data-stu-id="dbd3b-108">WebHCat is enabled by default on HDInsight clusters, and is used by various tools to submit jobs, get job status, etc. without logging in to the cluster.</span></span>

## <a name="modifying-configuration"></a><span data-ttu-id="dbd3b-109">Modificando a configuração</span><span class="sxs-lookup"><span data-stu-id="dbd3b-109">Modifying configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dbd3b-110">Vários dos erros listados neste documento ocorrerem porque um máximo configurado foi excedido.</span><span class="sxs-lookup"><span data-stu-id="dbd3b-110">Several of the errors listed in this document occur because a configured maximum has been exceeded.</span></span> <span data-ttu-id="dbd3b-111">Quando a etapa de solução menciona que você pode alterar um valor, use um dos seguintes para realizar a alteração:</span><span class="sxs-lookup"><span data-stu-id="dbd3b-111">When the resolution step mentions that you can change a value, you must use one of the following to perform the change:</span></span>

* <span data-ttu-id="dbd3b-112">Para clusters do **Windows** : use uma ação de script para configurar o valor durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="dbd3b-112">For **Windows** clusters: Use a script action to configure the value during cluster creation.</span></span> <span data-ttu-id="dbd3b-113">Para obter mais informações, consulte [Desenvolver ações de script](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="dbd3b-113">For more information, see [Develop script actions](hdinsight-hadoop-script-actions.md).</span></span>

* <span data-ttu-id="dbd3b-114">Para clusters do **Linux** : use o Ambari (API REST ou Web) para modificar o valor.</span><span class="sxs-lookup"><span data-stu-id="dbd3b-114">For **Linux** clusters: Use Ambari (web or REST API) to modify the value.</span></span> <span data-ttu-id="dbd3b-115">Para obter mais informações, consulte [Gerenciar o HDInsight usando o Ambari](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="dbd3b-115">For more information, see [Manage HDInsight using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dbd3b-116">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="dbd3b-116">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="dbd3b-117">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="dbd3b-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="default-configuration"></a><span data-ttu-id="dbd3b-118">Configuração padrão</span><span class="sxs-lookup"><span data-stu-id="dbd3b-118">Default configuration</span></span>

<span data-ttu-id="dbd3b-119">Se os seguintes valores padrão forem excedidos, isso poderá prejudicar o desempenho do WebHCat ou causar erros:</span><span class="sxs-lookup"><span data-stu-id="dbd3b-119">If the following default values are exceeded, it can degrade WebHCat performance or cause errors:</span></span>

| <span data-ttu-id="dbd3b-120">Configuração</span><span class="sxs-lookup"><span data-stu-id="dbd3b-120">Setting</span></span> | <span data-ttu-id="dbd3b-121">O que faz</span><span class="sxs-lookup"><span data-stu-id="dbd3b-121">What it does</span></span> | <span data-ttu-id="dbd3b-122">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="dbd3b-122">Default value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dbd3b-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span><span class="sxs-lookup"><span data-stu-id="dbd3b-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span></span> |<span data-ttu-id="dbd3b-124">O número máximo de trabalhos que podem estar ativos ao mesmo tempo (em execução ou pendentes)</span><span class="sxs-lookup"><span data-stu-id="dbd3b-124">The maximum number of jobs that can be active concurrently (pending or running)</span></span> |<span data-ttu-id="dbd3b-125">10.000</span><span class="sxs-lookup"><span data-stu-id="dbd3b-125">10,000</span></span> |
| <span data-ttu-id="dbd3b-126">[templeton.exec.max-procs][max-procs]</span><span class="sxs-lookup"><span data-stu-id="dbd3b-126">[templeton.exec.max-procs][max-procs]</span></span> |<span data-ttu-id="dbd3b-127">O número máximo de solicitações que podem ser atendidas simultaneamente</span><span class="sxs-lookup"><span data-stu-id="dbd3b-127">The maximum number of requests that can be served concurrently</span></span> |<span data-ttu-id="dbd3b-128">20</span><span class="sxs-lookup"><span data-stu-id="dbd3b-128">20</span></span> |
| <span data-ttu-id="dbd3b-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span><span class="sxs-lookup"><span data-stu-id="dbd3b-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span></span> |<span data-ttu-id="dbd3b-130">O número de dias pelos quais o histórico de trabalhos é mantido</span><span class="sxs-lookup"><span data-stu-id="dbd3b-130">The number of days that job history are retained</span></span> |<span data-ttu-id="dbd3b-131">7 dias</span><span class="sxs-lookup"><span data-stu-id="dbd3b-131">7 days</span></span> |

## <a name="too-many-requests"></a><span data-ttu-id="dbd3b-132">Número excessivo de solicitações</span><span class="sxs-lookup"><span data-stu-id="dbd3b-132">Too many requests</span></span>

<span data-ttu-id="dbd3b-133">**Código de status HTTP**: 429</span><span class="sxs-lookup"><span data-stu-id="dbd3b-133">**HTTP Status code**: 429</span></span>

| <span data-ttu-id="dbd3b-134">Causa</span><span class="sxs-lookup"><span data-stu-id="dbd3b-134">Cause</span></span> | <span data-ttu-id="dbd3b-135">Resolução</span><span class="sxs-lookup"><span data-stu-id="dbd3b-135">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="dbd3b-136">Você excedeu o máximo de solicitações simultâneas atendidas pelo WebHCat por minuto (padrão de 20)</span><span class="sxs-lookup"><span data-stu-id="dbd3b-136">You have exceeded the maximum concurrent requests served by WebHCat per minute (default 20)</span></span> |<span data-ttu-id="dbd3b-137">Reduza a carga de trabalho para garantir que não sejam enviadas mais do que o número máximo de solicitações simultâneas ou aumente o limite de solicitações simultâneas modificando `templeton.exec.max-procs`.</span><span class="sxs-lookup"><span data-stu-id="dbd3b-137">Reduce your workload to ensure that you do not submit more than the maximum number of concurrent requests or increase the concurrent request limit by modifying `templeton.exec.max-procs`.</span></span> <span data-ttu-id="dbd3b-138">Para obter mais informações, consulte [Modificar a configuração](#modifying-configuration)</span><span class="sxs-lookup"><span data-stu-id="dbd3b-138">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |

## <a name="server-unavailable"></a><span data-ttu-id="dbd3b-139">Servidor indisponível</span><span class="sxs-lookup"><span data-stu-id="dbd3b-139">Server unavailable</span></span>

<span data-ttu-id="dbd3b-140">**Código de status HTTP**: 503</span><span class="sxs-lookup"><span data-stu-id="dbd3b-140">**HTTP Status code**: 503</span></span>

| <span data-ttu-id="dbd3b-141">Causa</span><span class="sxs-lookup"><span data-stu-id="dbd3b-141">Cause</span></span> | <span data-ttu-id="dbd3b-142">Resolução</span><span class="sxs-lookup"><span data-stu-id="dbd3b-142">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="dbd3b-143">Esse código de status geralmente ocorre durante o failover entre o nó de cabeçalho primário e secundário para o cluster</span><span class="sxs-lookup"><span data-stu-id="dbd3b-143">This status code usually occurs during failover between the primary and secondary HeadNode for the cluster</span></span> |<span data-ttu-id="dbd3b-144">Aguarde dois minutos e repita a operação</span><span class="sxs-lookup"><span data-stu-id="dbd3b-144">Wait two minutes, then retry the operation</span></span> |

## <a name="bad-request-content-could-not-find-job"></a><span data-ttu-id="dbd3b-145">Conteúdo de solicitação incorreto: não foi possível encontrar o trabalho</span><span class="sxs-lookup"><span data-stu-id="dbd3b-145">Bad request Content: Could not find job</span></span>

<span data-ttu-id="dbd3b-146">**Código de status HTTP**: 400</span><span class="sxs-lookup"><span data-stu-id="dbd3b-146">**HTTP Status code**: 400</span></span>

| <span data-ttu-id="dbd3b-147">Causa</span><span class="sxs-lookup"><span data-stu-id="dbd3b-147">Cause</span></span> | <span data-ttu-id="dbd3b-148">Resolução</span><span class="sxs-lookup"><span data-stu-id="dbd3b-148">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="dbd3b-149">Os detalhes do trabalho foram apagados pelo limpador de histórico de trabalhos</span><span class="sxs-lookup"><span data-stu-id="dbd3b-149">Job details have been cleaned up by the job history cleaner</span></span> |<span data-ttu-id="dbd3b-150">O período de retenção padrão do histórico de trabalhos é de 7 dias.</span><span class="sxs-lookup"><span data-stu-id="dbd3b-150">The default retention period for job history is 7 days.</span></span> <span data-ttu-id="dbd3b-151">O período de retenção padrão pode ser alterado modificando `mapreduce.jobhistory.max-age-ms`.</span><span class="sxs-lookup"><span data-stu-id="dbd3b-151">The default retention period can be changed by modifying `mapreduce.jobhistory.max-age-ms`.</span></span> <span data-ttu-id="dbd3b-152">Para obter mais informações, consulte [Modificar a configuração](#modifying-configuration)</span><span class="sxs-lookup"><span data-stu-id="dbd3b-152">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |
| <span data-ttu-id="dbd3b-153">O trabalho foi encerrado devido a um failover</span><span class="sxs-lookup"><span data-stu-id="dbd3b-153">Job has been killed due to a failover</span></span> |<span data-ttu-id="dbd3b-154">Repita o envio do trabalho em até dois minutos</span><span class="sxs-lookup"><span data-stu-id="dbd3b-154">Retry job submission for up to two minutes</span></span> |
| <span data-ttu-id="dbd3b-155">Foi usada uma ID de trabalho inválida</span><span class="sxs-lookup"><span data-stu-id="dbd3b-155">An Invalid job id was used</span></span> |<span data-ttu-id="dbd3b-156">Verifique se a ID de trabalho está correta</span><span class="sxs-lookup"><span data-stu-id="dbd3b-156">Check if the job id is correct</span></span> |

## <a name="bad-gateway"></a><span data-ttu-id="dbd3b-157">Gateway inválido</span><span class="sxs-lookup"><span data-stu-id="dbd3b-157">Bad gateway</span></span>

<span data-ttu-id="dbd3b-158">**Código de status HTTP**: 502</span><span class="sxs-lookup"><span data-stu-id="dbd3b-158">**HTTP Status code**: 502</span></span>

| <span data-ttu-id="dbd3b-159">Causa</span><span class="sxs-lookup"><span data-stu-id="dbd3b-159">Cause</span></span> | <span data-ttu-id="dbd3b-160">Resolução</span><span class="sxs-lookup"><span data-stu-id="dbd3b-160">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="dbd3b-161">A coleta de lixo interna está ocorrendo no processo do WebHCat</span><span class="sxs-lookup"><span data-stu-id="dbd3b-161">Internal garbage collection is occurring within the WebHCat process</span></span> |<span data-ttu-id="dbd3b-162">Aguarde até que a coleta de lixo seja concluída ou reinicie o serviço do WebHCat</span><span class="sxs-lookup"><span data-stu-id="dbd3b-162">Wait for garbage collection to finish or restart the WebHCat service</span></span> |
| <span data-ttu-id="dbd3b-163">Tempo limite atingido ao aguardar uma resposta do serviço ResourceManager.</span><span class="sxs-lookup"><span data-stu-id="dbd3b-163">Time out waiting on a response from the ResourceManager service.</span></span> <span data-ttu-id="dbd3b-164">Esse erro pode ocorrer quando o número de aplicativos ativos atinge o máximo configurado (padrão de 10.000)</span><span class="sxs-lookup"><span data-stu-id="dbd3b-164">This error can occur when the number of active applications goes the configured maximum (default 10,000)</span></span> |<span data-ttu-id="dbd3b-165">Aguarde até que os trabalhos em execução no momento sejam concluídos ou aumente o limite de trabalhos simultâneos modificando `yarn.scheduler.capacity.maximum-applications`.</span><span class="sxs-lookup"><span data-stu-id="dbd3b-165">Wait for currently running jobs to complete or increase the concurrent job limit by modifying `yarn.scheduler.capacity.maximum-applications`.</span></span> <span data-ttu-id="dbd3b-166">Para obter mais informações, consulte a seção [Modificar a configuração](#modifying-configuration).</span><span class="sxs-lookup"><span data-stu-id="dbd3b-166">For more information, see the [Modifying configuration](#modifying-configuration) section.</span></span> |
| <span data-ttu-id="dbd3b-167">Tentar recuperar todos os trabalhos por meio da chamada [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) quando `Fields` está definido como `*`</span><span class="sxs-lookup"><span data-stu-id="dbd3b-167">Attempting to retrieve all jobs through the [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) call while `Fields` is set to `*`</span></span> |<span data-ttu-id="dbd3b-168">Não recupere *todos* os detalhes do trabalho.</span><span class="sxs-lookup"><span data-stu-id="dbd3b-168">Do not retrieve *all* job details.</span></span> <span data-ttu-id="dbd3b-169">Em vez disso, use `jobid` para recuperar detalhes somente de trabalhos maiores que determinada ID de trabalho.</span><span class="sxs-lookup"><span data-stu-id="dbd3b-169">Instead use `jobid` to retrieve details for jobs only greater than certain job id.</span></span> <span data-ttu-id="dbd3b-170">Ou não use `Fields`</span><span class="sxs-lookup"><span data-stu-id="dbd3b-170">Or, do not use `Fields`</span></span> |
| <span data-ttu-id="dbd3b-171">O serviço do WebHCat está inativo durante o failover do HeadNode</span><span class="sxs-lookup"><span data-stu-id="dbd3b-171">The WebHCat service is down during HeadNode failover</span></span> |<span data-ttu-id="dbd3b-172">Aguarde dois minutos e repita a operação</span><span class="sxs-lookup"><span data-stu-id="dbd3b-172">Wait for two minutes and retry the operation</span></span> |
| <span data-ttu-id="dbd3b-173">Há mais de 500 trabalhos pendentes enviados por meio do WebHCat</span><span class="sxs-lookup"><span data-stu-id="dbd3b-173">There are more than 500 pending jobs submitted through WebHCat</span></span> |<span data-ttu-id="dbd3b-174">Aguarde até que os trabalhos pendentes no momento sejam concluídos antes de enviar mais trabalhos</span><span class="sxs-lookup"><span data-stu-id="dbd3b-174">Wait until currently pending jobs have completed before submitting more jobs</span></span> |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml
