---
title: aaaUnderstand e resolver erros de WebHCat no HDInsight - Azure | Microsoft Docs
description: Saiba como erros comuns tooabout retornado por WebHCat no HDInsight e tooresolve-los.
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
ms.openlocfilehash: 0071a1e9ed448ae146b93c8f4f518e31b95d27c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a><span data-ttu-id="49b76-103">Entenda e resolva erros recebidos do WebHCat no HDInsight</span><span class="sxs-lookup"><span data-stu-id="49b76-103">Understand and resolve errors received from WebHCat on HDInsight</span></span>

<span data-ttu-id="49b76-104">Saiba mais sobre erros recebidos ao usar WebHCat com HDInsight e como tooresolve-los.</span><span class="sxs-lookup"><span data-stu-id="49b76-104">Learn about errors received when using WebHCat with HDInsight, and how tooresolve them.</span></span> <span data-ttu-id="49b76-105">WebHCat é usado internamente por ferramentas de cliente como o PowerShell do Azure e hello Data Lake Tools para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="49b76-105">WebHCat is used internally by client-side tools such as Azure PowerShell and hello Data Lake Tools for Visual Studio.</span></span>

## <a name="what-is-webhcat"></a><span data-ttu-id="49b76-106">O que é o WebHCat</span><span class="sxs-lookup"><span data-stu-id="49b76-106">What is WebHCat</span></span>

<span data-ttu-id="49b76-107">O [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) é uma API REST para o [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), uma camada de gerenciamento de armazenamento e tabela para Hadoop.</span><span class="sxs-lookup"><span data-stu-id="49b76-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) is a REST API for [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), a table, and storage management layer for Hadoop.</span></span> <span data-ttu-id="49b76-108">WebHCat está habilitado por padrão em clusters de HDInsight e é usada por vários trabalhos de toosubmit de ferramentas, obter o status do trabalho, etc. sem efetuar login no cluster toohello.</span><span class="sxs-lookup"><span data-stu-id="49b76-108">WebHCat is enabled by default on HDInsight clusters, and is used by various tools toosubmit jobs, get job status, etc. without logging in toohello cluster.</span></span>

## <a name="modifying-configuration"></a><span data-ttu-id="49b76-109">Modificando a configuração</span><span class="sxs-lookup"><span data-stu-id="49b76-109">Modifying configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="49b76-110">Vários erros de saudação listados neste documento ocorrerem porque um máximo configurado foi excedido.</span><span class="sxs-lookup"><span data-stu-id="49b76-110">Several of hello errors listed in this document occur because a configured maximum has been exceeded.</span></span> <span data-ttu-id="49b76-111">Quando a etapa de solução de saudação menciona que você pode alterar um valor, você deve usar uma saudação após tooperform Olá alteração:</span><span class="sxs-lookup"><span data-stu-id="49b76-111">When hello resolution step mentions that you can change a value, you must use one of hello following tooperform hello change:</span></span>

* <span data-ttu-id="49b76-112">Para **Windows** clusters: Use um valor de saudação do script ação tooconfigure durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="49b76-112">For **Windows** clusters: Use a script action tooconfigure hello value during cluster creation.</span></span> <span data-ttu-id="49b76-113">Para obter mais informações, consulte [Desenvolver ações de script](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="49b76-113">For more information, see [Develop script actions](hdinsight-hadoop-script-actions.md).</span></span>

* <span data-ttu-id="49b76-114">Para **Linux** clusters: valor de saudação toomodify Ambari de uso (web ou a API REST).</span><span class="sxs-lookup"><span data-stu-id="49b76-114">For **Linux** clusters: Use Ambari (web or REST API) toomodify hello value.</span></span> <span data-ttu-id="49b76-115">Para obter mais informações, consulte [Gerenciar o HDInsight usando o Ambari](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="49b76-115">For more information, see [Manage HDInsight using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="49b76-116">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="49b76-116">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="49b76-117">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="49b76-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="default-configuration"></a><span data-ttu-id="49b76-118">Configuração padrão</span><span class="sxs-lookup"><span data-stu-id="49b76-118">Default configuration</span></span>

<span data-ttu-id="49b76-119">Se Olá valores padrão a seguir é excedido, ela pode prejudicar o desempenho do WebHCat ou provocar erros:</span><span class="sxs-lookup"><span data-stu-id="49b76-119">If hello following default values are exceeded, it can degrade WebHCat performance or cause errors:</span></span>

| <span data-ttu-id="49b76-120">Configuração</span><span class="sxs-lookup"><span data-stu-id="49b76-120">Setting</span></span> | <span data-ttu-id="49b76-121">O que faz</span><span class="sxs-lookup"><span data-stu-id="49b76-121">What it does</span></span> | <span data-ttu-id="49b76-122">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="49b76-122">Default value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="49b76-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span><span class="sxs-lookup"><span data-stu-id="49b76-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span></span> |<span data-ttu-id="49b76-124">Olá número máximo de trabalhos que podem estar ativas simultaneamente (em execução ou pendente)</span><span class="sxs-lookup"><span data-stu-id="49b76-124">hello maximum number of jobs that can be active concurrently (pending or running)</span></span> |<span data-ttu-id="49b76-125">10.000</span><span class="sxs-lookup"><span data-stu-id="49b76-125">10,000</span></span> |
| <span data-ttu-id="49b76-126">[templeton.exec.max-procs][max-procs]</span><span class="sxs-lookup"><span data-stu-id="49b76-126">[templeton.exec.max-procs][max-procs]</span></span> |<span data-ttu-id="49b76-127">número máximo de saudação de solicitações que podem ser usadas simultaneamente</span><span class="sxs-lookup"><span data-stu-id="49b76-127">hello maximum number of requests that can be served concurrently</span></span> |<span data-ttu-id="49b76-128">20</span><span class="sxs-lookup"><span data-stu-id="49b76-128">20</span></span> |
| <span data-ttu-id="49b76-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span><span class="sxs-lookup"><span data-stu-id="49b76-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span></span> |<span data-ttu-id="49b76-130">saudação de número de dias que o histórico de trabalho será retida</span><span class="sxs-lookup"><span data-stu-id="49b76-130">hello number of days that job history are retained</span></span> |<span data-ttu-id="49b76-131">7 dias</span><span class="sxs-lookup"><span data-stu-id="49b76-131">7 days</span></span> |

## <a name="too-many-requests"></a><span data-ttu-id="49b76-132">Número excessivo de solicitações</span><span class="sxs-lookup"><span data-stu-id="49b76-132">Too many requests</span></span>

<span data-ttu-id="49b76-133">**Código de status HTTP**: 429</span><span class="sxs-lookup"><span data-stu-id="49b76-133">**HTTP Status code**: 429</span></span>

| <span data-ttu-id="49b76-134">Causa</span><span class="sxs-lookup"><span data-stu-id="49b76-134">Cause</span></span> | <span data-ttu-id="49b76-135">Resolução</span><span class="sxs-lookup"><span data-stu-id="49b76-135">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="49b76-136">Você excedeu solicitações simultâneas máximas Olá servidas por WebHCat por minuto (padrão de 20)</span><span class="sxs-lookup"><span data-stu-id="49b76-136">You have exceeded hello maximum concurrent requests served by WebHCat per minute (default 20)</span></span> |<span data-ttu-id="49b76-137">Reduzir tooensure sua carga de trabalho que você não enviar mais de Olá número máximo de solicitações simultâneas ou aumentar o limite de solicitações simultâneas Olá modificando `templeton.exec.max-procs`.</span><span class="sxs-lookup"><span data-stu-id="49b76-137">Reduce your workload tooensure that you do not submit more than hello maximum number of concurrent requests or increase hello concurrent request limit by modifying `templeton.exec.max-procs`.</span></span> <span data-ttu-id="49b76-138">Para obter mais informações, consulte [Modificar a configuração](#modifying-configuration)</span><span class="sxs-lookup"><span data-stu-id="49b76-138">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |

## <a name="server-unavailable"></a><span data-ttu-id="49b76-139">Servidor indisponível</span><span class="sxs-lookup"><span data-stu-id="49b76-139">Server unavailable</span></span>

<span data-ttu-id="49b76-140">**Código de status HTTP**: 503</span><span class="sxs-lookup"><span data-stu-id="49b76-140">**HTTP Status code**: 503</span></span>

| <span data-ttu-id="49b76-141">Causa</span><span class="sxs-lookup"><span data-stu-id="49b76-141">Cause</span></span> | <span data-ttu-id="49b76-142">Resolução</span><span class="sxs-lookup"><span data-stu-id="49b76-142">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="49b76-143">Esse código de status geralmente ocorre durante o failover entre Olá primário e secundário um nó principal para o cluster de saudação</span><span class="sxs-lookup"><span data-stu-id="49b76-143">This status code usually occurs during failover between hello primary and secondary HeadNode for hello cluster</span></span> |<span data-ttu-id="49b76-144">Aguarde dois minutos e repita a operação de saudação</span><span class="sxs-lookup"><span data-stu-id="49b76-144">Wait two minutes, then retry hello operation</span></span> |

## <a name="bad-request-content-could-not-find-job"></a><span data-ttu-id="49b76-145">Conteúdo de solicitação incorreto: não foi possível encontrar o trabalho</span><span class="sxs-lookup"><span data-stu-id="49b76-145">Bad request Content: Could not find job</span></span>

<span data-ttu-id="49b76-146">**Código de status HTTP**: 400</span><span class="sxs-lookup"><span data-stu-id="49b76-146">**HTTP Status code**: 400</span></span>

| <span data-ttu-id="49b76-147">Causa</span><span class="sxs-lookup"><span data-stu-id="49b76-147">Cause</span></span> | <span data-ttu-id="49b76-148">Resolução</span><span class="sxs-lookup"><span data-stu-id="49b76-148">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="49b76-149">Detalhes do trabalho foram limpos pelo histórico do trabalho Olá Limpador</span><span class="sxs-lookup"><span data-stu-id="49b76-149">Job details have been cleaned up by hello job history cleaner</span></span> |<span data-ttu-id="49b76-150">período de retenção padrão Olá para o histórico de trabalho é 7 dias.</span><span class="sxs-lookup"><span data-stu-id="49b76-150">hello default retention period for job history is 7 days.</span></span> <span data-ttu-id="49b76-151">período de retenção saudação padrão pode ser alterado modificando `mapreduce.jobhistory.max-age-ms`.</span><span class="sxs-lookup"><span data-stu-id="49b76-151">hello default retention period can be changed by modifying `mapreduce.jobhistory.max-age-ms`.</span></span> <span data-ttu-id="49b76-152">Para obter mais informações, consulte [Modificar a configuração](#modifying-configuration)</span><span class="sxs-lookup"><span data-stu-id="49b76-152">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |
| <span data-ttu-id="49b76-153">Trabalho foi encerrado devido a failover tooa</span><span class="sxs-lookup"><span data-stu-id="49b76-153">Job has been killed due tooa failover</span></span> |<span data-ttu-id="49b76-154">Repita o envio de trabalho de backup tootwo minutos</span><span class="sxs-lookup"><span data-stu-id="49b76-154">Retry job submission for up tootwo minutes</span></span> |
| <span data-ttu-id="49b76-155">Foi usada uma ID de trabalho inválida</span><span class="sxs-lookup"><span data-stu-id="49b76-155">An Invalid job id was used</span></span> |<span data-ttu-id="49b76-156">Verifique se a id do trabalho hello está correto</span><span class="sxs-lookup"><span data-stu-id="49b76-156">Check if hello job id is correct</span></span> |

## <a name="bad-gateway"></a><span data-ttu-id="49b76-157">Gateway inválido</span><span class="sxs-lookup"><span data-stu-id="49b76-157">Bad gateway</span></span>

<span data-ttu-id="49b76-158">**Código de status HTTP**: 502</span><span class="sxs-lookup"><span data-stu-id="49b76-158">**HTTP Status code**: 502</span></span>

| <span data-ttu-id="49b76-159">Causa</span><span class="sxs-lookup"><span data-stu-id="49b76-159">Cause</span></span> | <span data-ttu-id="49b76-160">Resolução</span><span class="sxs-lookup"><span data-stu-id="49b76-160">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="49b76-161">Coleta de lixo interno está ocorrendo em Olá WebHCat processo</span><span class="sxs-lookup"><span data-stu-id="49b76-161">Internal garbage collection is occurring within hello WebHCat process</span></span> |<span data-ttu-id="49b76-162">Espere toofinish de coleta de lixo ou reinicie o serviço WebHCat de saudação</span><span class="sxs-lookup"><span data-stu-id="49b76-162">Wait for garbage collection toofinish or restart hello WebHCat service</span></span> |
| <span data-ttu-id="49b76-163">Tempo limite aguardando uma resposta do hello serviço ResourceManager.</span><span class="sxs-lookup"><span data-stu-id="49b76-163">Time out waiting on a response from hello ResourceManager service.</span></span> <span data-ttu-id="49b76-164">Esse erro pode ocorrer quando o número de saudação de aplicativos ativos vai máximo configurado de saudação (padrão de 10.000)</span><span class="sxs-lookup"><span data-stu-id="49b76-164">This error can occur when hello number of active applications goes hello configured maximum (default 10,000)</span></span> |<span data-ttu-id="49b76-165">Aguarde executando trabalhos toocomplete ou aumentar o limite de trabalho simultâneas de saudação modificando `yarn.scheduler.capacity.maximum-applications`.</span><span class="sxs-lookup"><span data-stu-id="49b76-165">Wait for currently running jobs toocomplete or increase hello concurrent job limit by modifying `yarn.scheduler.capacity.maximum-applications`.</span></span> <span data-ttu-id="49b76-166">Para obter mais informações, consulte Olá [configuração modificando](#modifying-configuration) seção.</span><span class="sxs-lookup"><span data-stu-id="49b76-166">For more information, see hello [Modifying configuration](#modifying-configuration) section.</span></span> |
| <span data-ttu-id="49b76-167">Tentativa de tooretrieve todos os trabalhos por meio de saudação [/jobs. GET](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) chamada ao `Fields` está definido muito`*`</span><span class="sxs-lookup"><span data-stu-id="49b76-167">Attempting tooretrieve all jobs through hello [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) call while `Fields` is set too`*`</span></span> |<span data-ttu-id="49b76-168">Não recupere *todos* os detalhes do trabalho.</span><span class="sxs-lookup"><span data-stu-id="49b76-168">Do not retrieve *all* job details.</span></span> <span data-ttu-id="49b76-169">Em vez disso, use `jobid` tooretrieve detalhes para trabalhos de maiores somente a certo id do trabalho. Ou não use `Fields`</span><span class="sxs-lookup"><span data-stu-id="49b76-169">Instead use `jobid` tooretrieve details for jobs only greater than certain job id. Or, do not use `Fields`</span></span> |
| <span data-ttu-id="49b76-170">Olá serviço WebHCat está inativo durante o failover de nó principal</span><span class="sxs-lookup"><span data-stu-id="49b76-170">hello WebHCat service is down during HeadNode failover</span></span> |<span data-ttu-id="49b76-171">Aguarde até dois minutos e repita a operação de saudação</span><span class="sxs-lookup"><span data-stu-id="49b76-171">Wait for two minutes and retry hello operation</span></span> |
| <span data-ttu-id="49b76-172">Há mais de 500 trabalhos pendentes enviados por meio do WebHCat</span><span class="sxs-lookup"><span data-stu-id="49b76-172">There are more than 500 pending jobs submitted through WebHCat</span></span> |<span data-ttu-id="49b76-173">Aguarde até que os trabalhos pendentes no momento sejam concluídos antes de enviar mais trabalhos</span><span class="sxs-lookup"><span data-stu-id="49b76-173">Wait until currently pending jobs have completed before submitting more jobs</span></span> |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml
