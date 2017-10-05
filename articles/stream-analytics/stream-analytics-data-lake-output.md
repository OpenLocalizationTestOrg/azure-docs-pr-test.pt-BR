---
title: "Saída do Data Lake Store no Stream Analytics | Microsoft Docs"
description: "Configuração de autenticação e autorização de um Repositório Azure Data Lake em um trabalho do Stream Analytics"
keywords: 
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: ea5baafa-0054-4c70-973a-6a3a8c6eaffc
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 3d867df3ef875d5cc41de418c3d1d269ff751fda
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="stream-analytics-data-lake-store-output"></a><span data-ttu-id="0de59-103">Saída do Repositório Data Lake do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="0de59-103">Stream Analytics Data Lake Store output</span></span>
<span data-ttu-id="0de59-104">Trabalhos do Stream Analytics dão suporte a vários métodos de saída, sendo um deles um [Repositório Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/).</span><span class="sxs-lookup"><span data-stu-id="0de59-104">Stream Analytics jobs support several output methods, one being an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span></span> <span data-ttu-id="0de59-105">O Repositório Azure Data Lake é um repositório em hiper-escala corporativo para cargas de trabalho de análise de big data.</span><span class="sxs-lookup"><span data-stu-id="0de59-105">Azure Data Lake Store is an enterprise-wide hyper-scale repository for big data analytic workloads.</span></span> <span data-ttu-id="0de59-106">O Repositório Data Lake permite que você armazene dados de qualquer tamanho, tipo e velocidade de ingestão para análises operacionais e exploratórias.</span><span class="sxs-lookup"><span data-stu-id="0de59-106">Data Lake Store enables you to store data of any size, type and ingestion speed for operational and exploratory analytics.</span></span>

## <a name="authorize-a-data-lake-store-account"></a><span data-ttu-id="0de59-107">Autorizar uma conta do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="0de59-107">Authorize a Data Lake Store account</span></span>
1. <span data-ttu-id="0de59-108">Quando o Data Lake Store é selecionado como uma saída no portal do Azure, você deve autorizar o uso de seu Data Lake Store existente ou solicitar o acesso ao Data Lake Store por meio do Portal Clássico.</span><span class="sxs-lookup"><span data-stu-id="0de59-108">When Data Lake Store is selected as an output in the Azure portal, you will be prompted to authorize use of your existing Data Lake Store or to request access to the Data Lake Store via the Classic Portal.</span></span>
   
   ![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-authorization.png)  
   
2. <span data-ttu-id="0de59-109">Se você já tiver acesso ao Data Lake Store, clique em "Autorizar agora" e, por um curto período, uma página será exibida indicando "Redirecionando para autorização".</span><span class="sxs-lookup"><span data-stu-id="0de59-109">If you already have access to Data Lake Store, click “Authorize Now” and for a brief time a page will pop up indicating “Redirecting to authorization”.</span></span> <span data-ttu-id="0de59-110">A página será fechada automaticamente e você verá a página que permite configurar a saída do Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="0de59-110">The page will automatically close and you will be presented with the page that would allow you to configure the Data Lake Store output.</span></span>

<span data-ttu-id="0de59-111">Se não tiver feito a inscrição no Data Lake Store, você poderá seguir o link “Inscrever-se agora” para iniciar a solicitação ou seguir as [instruções de introdução](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0de59-111">If you have not signed up for Data Lake Store, you can follow the “Sign up now” link to initiate the request, or follow the [get started instructions](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="configure-the-data-lake-store-output-properties"></a><span data-ttu-id="0de59-112">Configurar as propriedades de saída do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="0de59-112">Configure the Data Lake Store output properties</span></span>
<span data-ttu-id="0de59-113">Uma vez que a conta do Repositório Data Lake foi autenticada, você pode configurar as propriedades de saída do Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="0de59-113">Once you have the Data Lake Store account authenticated, you can configure the properties for your Data Lake Store output.</span></span> <span data-ttu-id="0de59-114">A tabela a seguir é a lista de nomes de propriedade e sua descrição para configurar a saída do Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="0de59-114">The table below is the list of property names and their description to configure your Data Lake Store output.</span></span>

<table>
<tbody>
<tr>
<td><span data-ttu-id="0de59-115"><B>NOME DA PROPRIEDADE</B></span><span class="sxs-lookup"><span data-stu-id="0de59-115"><B>PROPERTY NAME</B></span></span></td>
<td><span data-ttu-id="0de59-116"><B>DESCRIÇÃO</B></span><span class="sxs-lookup"><span data-stu-id="0de59-116"><B>DESCRIPTION</B></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0de59-117">Alias de saída</span><span class="sxs-lookup"><span data-stu-id="0de59-117">Output Alias</span></span></td>
<td><span data-ttu-id="0de59-118">Esse é um nome amigável utilizado em consultas para direcionar a saída da consulta para esse Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="0de59-118">This is a friendly name used in queries to direct the query output to this Data Lake Store.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0de59-119">Conta do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="0de59-119">Data Lake Store Account</span></span></td>
<td><span data-ttu-id="0de59-120">O nome da conta de armazenamento para o qual você está enviando a saída</span><span class="sxs-lookup"><span data-stu-id="0de59-120">The name of the storage account where you are sending your output.</span></span> <span data-ttu-id="0de59-121">Você verá uma lista de contas do Data Lake Store que do usuário conectado tem acesso ao.</span><span class="sxs-lookup"><span data-stu-id="0de59-121">You will be presented with a list of Data Lake Store accounts  the logged in user has access to.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0de59-122">Padrão de prefixo do caminho [<I>opcional</I>]</span><span class="sxs-lookup"><span data-stu-id="0de59-122">Path Prefix Pattern [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="0de59-123">O caminho do arquivo usado para gravar seus arquivos na Conta do Repositório Data Lake especificada.</span><span class="sxs-lookup"><span data-stu-id="0de59-123">The file path used to write your files within the specified Data Lake Store Account.</span></span> <BR><span data-ttu-id="0de59-124">{data}, {hora}</span><span class="sxs-lookup"><span data-stu-id="0de59-124">{date}, {time}</span></span><BR><span data-ttu-id="0de59-125">Exemplo 1: pasta1/logs/{data}/{hora}</span><span class="sxs-lookup"><span data-stu-id="0de59-125">Example 1: folder1/logs/{date}/{time}</span></span><BR><span data-ttu-id="0de59-126">Exemplo 2: pasta1/logs/{data}</span><span class="sxs-lookup"><span data-stu-id="0de59-126">Example 2: folder1/logs/{date}</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0de59-127">Formato de data [<I>opcional</I>]</span><span class="sxs-lookup"><span data-stu-id="0de59-127">Date Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="0de59-128">Se o token de data for usado no caminho do prefixo, você pode selecionar o formato de data na qual os arquivos são organizados.</span><span class="sxs-lookup"><span data-stu-id="0de59-128">If the date token is used in the prefix path, you can select the date format in which your files are organized.</span></span> <span data-ttu-id="0de59-129">Exemplo: AAAA/MM/DD</span><span class="sxs-lookup"><span data-stu-id="0de59-129">Example: YYYY/MM/DD</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0de59-130">Formato de hora [<I>opcional</I>]</span><span class="sxs-lookup"><span data-stu-id="0de59-130">Time Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="0de59-131">Se o token de hora for usado no caminho do prefixo, você pode selecionar o formato de hora na qual os arquivos são organizados.</span><span class="sxs-lookup"><span data-stu-id="0de59-131">If the time token is used in the prefix path, specify the time format in which your files are organized.</span></span> <span data-ttu-id="0de59-132">Atualmente, o único valor aceito é HH.</span><span class="sxs-lookup"><span data-stu-id="0de59-132">Currently the only supported value is HH.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0de59-133">Formato de serialização do evento</span><span class="sxs-lookup"><span data-stu-id="0de59-133">Event Serialization Format</span></span></td>
<td><span data-ttu-id="0de59-134">Formato de serialização para dados de saída.</span><span class="sxs-lookup"><span data-stu-id="0de59-134">Serialization format for output data.</span></span> <span data-ttu-id="0de59-135">Há suporte para JSON, CSV e Avro.</span><span class="sxs-lookup"><span data-stu-id="0de59-135">JSON, CSV, and Avro are supported.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0de59-136">Codificação</span><span class="sxs-lookup"><span data-stu-id="0de59-136">Encoding</span></span></td>
<td><span data-ttu-id="0de59-137">Se o formato for CSV ou JSON, uma codificação deve ser especificada.</span><span class="sxs-lookup"><span data-stu-id="0de59-137">If CSV or JSON format, an encoding must be specified.</span></span> <span data-ttu-id="0de59-138">UTF-8 é o único formato de codificação com suporte no momento.</span><span class="sxs-lookup"><span data-stu-id="0de59-138">UTF-8 is the only supported encoding format at this time.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0de59-139">Delimitador</span><span class="sxs-lookup"><span data-stu-id="0de59-139">Delimiter</span></span></td>
<td><span data-ttu-id="0de59-140">Aplicável somente à serialização de CSV.</span><span class="sxs-lookup"><span data-stu-id="0de59-140">Only applicable for CSV serialization.</span></span> <span data-ttu-id="0de59-141">O Stream Analytics é compatível com vários delimitadores comuns para serialização de dados CSV.</span><span class="sxs-lookup"><span data-stu-id="0de59-141">Stream Analytics supports a number of common delimiters for serializing CSV data.</span></span> <span data-ttu-id="0de59-142">Os valores suportados são vírgula, ponto e vírgula, espaço, tab e barra vertical.</span><span class="sxs-lookup"><span data-stu-id="0de59-142">Supported values are comma, semicolon, space, tab and vertical bar.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="0de59-143">Formatar</span><span class="sxs-lookup"><span data-stu-id="0de59-143">Format</span></span></td>
<td><span data-ttu-id="0de59-144">Aplicável somente para serialização JSON.</span><span class="sxs-lookup"><span data-stu-id="0de59-144">Only applicable for JSON serialization.</span></span> <span data-ttu-id="0de59-145">Uma linha separada especifica que a saída será formatada com cada objeto JSON separado por uma nova linha.</span><span class="sxs-lookup"><span data-stu-id="0de59-145">Line separated specifies that the output will be formatted by having each JSON object separated by a new line.</span></span> <span data-ttu-id="0de59-146">Matriz especifica que a saída será formatada como uma matriz de objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="0de59-146">Array specifies that the output will be formatted as an array of JSON objects.</span></span></td>
</tr>
</tbody>
</table>

## <a name="renew-data-lake-store-authorization"></a><span data-ttu-id="0de59-147">Renovar autorização do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="0de59-147">Renew Data Lake Store Authorization</span></span>
<span data-ttu-id="0de59-148">Atualmente, há uma limitação em que o token de autenticação deve ser atualizado manualmente a cada 90 dias para todos os trabalhos com saída do Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="0de59-148">Currently, there is a limitation where the authentication token needs to be manually refreshed every 90 days for all jobs with Data Lake Store output.</span></span> <span data-ttu-id="0de59-149">Você também precisará autenticar novamente sua conta do Repositório Data Lake caso sua senha tenha sido alterada depois de seu trabalho ter sido criado ou autenticado pela última vez.</span><span class="sxs-lookup"><span data-stu-id="0de59-149">You will also need to re-authenticate your Data Lake Store account if you have changed your password since your job was created or last authenticated.</span></span> <span data-ttu-id="0de59-150">Um sintoma desse problema é nenhuma saída de trabalho e um erro nos Logs de Operação indicando a necessidade de uma nova autorização.</span><span class="sxs-lookup"><span data-stu-id="0de59-150">A symptom of this issue is no job output and an error in the Operation Logs indicating need for re-authorization.</span></span>

<span data-ttu-id="0de59-151">Para resolver esse problema, pare seu trabalho em execução e vá para a saída do Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="0de59-151">To resolve this issue, stop your running job and go to your Data Lake Store output.</span></span> <span data-ttu-id="0de59-152">Clique no link "Renovar autorização" e por um curto período uma página será exibida indicando "Redirecionando para autorização...".</span><span class="sxs-lookup"><span data-stu-id="0de59-152">Click the “Renew authorization” link, and for a brief time a page will pop up indicating “Redirecting to authorization..”.</span></span> <span data-ttu-id="0de59-153">A página será fechada automaticamente e, se for bem-sucedida, indicará "A autorização foi renovada com êxito".</span><span class="sxs-lookup"><span data-stu-id="0de59-153">The page will automatically close and if successful, will indicate “Authorization has been successfully renewed”.</span></span> <span data-ttu-id="0de59-154">Em seguida, você precisa clicar em "Salvar" na parte inferior da página e poderá continuar reiniciando seu trabalho da última vez em que foi interrompido para evitar perda de dados.</span><span class="sxs-lookup"><span data-stu-id="0de59-154">You then need to click “Save” at the bottom of the page, and can proceed by restarting your job from the Last Stopped Time to avoid data loss.</span></span>

![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-renew-authorization.png)

