---
title: "aaaStream análise Data Lake repositório saída | Microsoft Docs"
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
ms.openlocfilehash: 183cf51edb2e49ac3e42257e67a8077b95777258
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-data-lake-store-output"></a><span data-ttu-id="462ac-103">Saída do Repositório Data Lake do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="462ac-103">Stream Analytics Data Lake Store output</span></span>
<span data-ttu-id="462ac-104">Trabalhos do Stream Analytics dão suporte a vários métodos de saída, sendo um deles um [Repositório Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/).</span><span class="sxs-lookup"><span data-stu-id="462ac-104">Stream Analytics jobs support several output methods, one being an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span></span> <span data-ttu-id="462ac-105">O Repositório Azure Data Lake é um repositório em hiper-escala corporativo para cargas de trabalho de análise de big data.</span><span class="sxs-lookup"><span data-stu-id="462ac-105">Azure Data Lake Store is an enterprise-wide hyper-scale repository for big data analytic workloads.</span></span> <span data-ttu-id="462ac-106">Repositório data Lake permite toostore dados de qualquer velocidade de tamanho, tipo e inclusão para análise operacional e exploratória.</span><span class="sxs-lookup"><span data-stu-id="462ac-106">Data Lake Store enables you toostore data of any size, type and ingestion speed for operational and exploratory analytics.</span></span>

## <a name="authorize-a-data-lake-store-account"></a><span data-ttu-id="462ac-107">Autorizar uma conta do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="462ac-107">Authorize a Data Lake Store account</span></span>
1. <span data-ttu-id="462ac-108">Quando o repositório Data Lake é selecionado como uma saída de hello portal do Azure, você será solicitado tooauthorize uso do repositório existente do Data Lake ou toorequest acessar o repositório toohello Data Lake via Olá Portal clássico.</span><span class="sxs-lookup"><span data-stu-id="462ac-108">When Data Lake Store is selected as an output in hello Azure portal, you will be prompted tooauthorize use of your existing Data Lake Store or toorequest access toohello Data Lake Store via hello Classic Portal.</span></span>
   
   ![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-authorization.png)  
   
2. <span data-ttu-id="462ac-109">Se você já tiver acessar o repositório de Lake tooData, clique em 'Autorizar agora' e por um curto período uma página será exibida indicando "Redirecionando tooauthorization".</span><span class="sxs-lookup"><span data-stu-id="462ac-109">If you already have access tooData Lake Store, click “Authorize Now” and for a brief time a page will pop up indicating “Redirecting tooauthorization”.</span></span> <span data-ttu-id="462ac-110">página Olá automaticamente será fechado e você verá página Olá que lhe permitiria tooconfigure Olá repositório Data Lake saída.</span><span class="sxs-lookup"><span data-stu-id="462ac-110">hello page will automatically close and you will be presented with hello page that would allow you tooconfigure hello Data Lake Store output.</span></span>

<span data-ttu-id="462ac-111">Se você não estiver inscrito para repositório Data Lake, siga hello "Inscrever-se agora" link tooinitiate Olá solicitação ou siga Olá [obter instruções iniciadas](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="462ac-111">If you have not signed up for Data Lake Store, you can follow hello “Sign up now” link tooinitiate hello request, or follow hello [get started instructions](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="configure-hello-data-lake-store-output-properties"></a><span data-ttu-id="462ac-112">Configurar propriedades de saída do repositório Data Lake Olá</span><span class="sxs-lookup"><span data-stu-id="462ac-112">Configure hello Data Lake Store output properties</span></span>
<span data-ttu-id="462ac-113">Uma vez que a conta do repositório Data Lake Olá autenticado, você pode configurar propriedades de saudação para a saída do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="462ac-113">Once you have hello Data Lake Store account authenticated, you can configure hello properties for your Data Lake Store output.</span></span> <span data-ttu-id="462ac-114">tabela de saudação abaixo é a lista de saudação de nomes de propriedade e seu tooconfigure descrição que seu repositório Data Lake de saída.</span><span class="sxs-lookup"><span data-stu-id="462ac-114">hello table below is hello list of property names and their description tooconfigure your Data Lake Store output.</span></span>

<table>
<tbody>
<tr>
<td><span data-ttu-id="462ac-115"><B>NOME DA PROPRIEDADE</B></span><span class="sxs-lookup"><span data-stu-id="462ac-115"><B>PROPERTY NAME</B></span></span></td>
<td><span data-ttu-id="462ac-116"><B>DESCRIÇÃO</B></span><span class="sxs-lookup"><span data-stu-id="462ac-116"><B>DESCRIPTION</B></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="462ac-117">Alias de saída</span><span class="sxs-lookup"><span data-stu-id="462ac-117">Output Alias</span></span></td>
<td><span data-ttu-id="462ac-118">Este é um nome amigável usado em consultas toodirect Olá consulta saída toothis repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="462ac-118">This is a friendly name used in queries toodirect hello query output toothis Data Lake Store.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="462ac-119">Conta do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="462ac-119">Data Lake Store Account</span></span></td>
<td><span data-ttu-id="462ac-120">nome de Olá Olá da conta de armazenamento em que você está enviando a saída.</span><span class="sxs-lookup"><span data-stu-id="462ac-120">hello name of hello storage account where you are sending your output.</span></span> <span data-ttu-id="462ac-121">Você verá uma lista de contas do repositório Data Lake Olá registrada no usuário tem acesso ao.</span><span class="sxs-lookup"><span data-stu-id="462ac-121">You will be presented with a list of Data Lake Store accounts  hello logged in user has access to.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="462ac-122">Padrão de prefixo do caminho [<I>opcional</I>]</span><span class="sxs-lookup"><span data-stu-id="462ac-122">Path Prefix Pattern [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="462ac-123">Olá arquivo caminho usado toowrite seus arquivos no hello especificado conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="462ac-123">hello file path used toowrite your files within hello specified Data Lake Store Account.</span></span> <BR><span data-ttu-id="462ac-124">{data}, {hora}</span><span class="sxs-lookup"><span data-stu-id="462ac-124">{date}, {time}</span></span><BR><span data-ttu-id="462ac-125">Exemplo 1: pasta1/logs/{data}/{hora}</span><span class="sxs-lookup"><span data-stu-id="462ac-125">Example 1: folder1/logs/{date}/{time}</span></span><BR><span data-ttu-id="462ac-126">Exemplo 2: pasta1/logs/{data}</span><span class="sxs-lookup"><span data-stu-id="462ac-126">Example 2: folder1/logs/{date}</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="462ac-127">Formato de data [<I>opcional</I>]</span><span class="sxs-lookup"><span data-stu-id="462ac-127">Date Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="462ac-128">Se o token de data de saudação é usado no caminho de prefixo hello, você pode selecionar o formato de data de saudação na qual os arquivos são organizados.</span><span class="sxs-lookup"><span data-stu-id="462ac-128">If hello date token is used in hello prefix path, you can select hello date format in which your files are organized.</span></span> <span data-ttu-id="462ac-129">Exemplo: AAAA/MM/DD</span><span class="sxs-lookup"><span data-stu-id="462ac-129">Example: YYYY/MM/DD</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="462ac-130">Formato de hora [<I>opcional</I>]</span><span class="sxs-lookup"><span data-stu-id="462ac-130">Time Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="462ac-131">Se o token de tempo de saudação é usado no caminho de prefixo Olá, especifique o formato de tempo de saudação na qual os arquivos são organizados.</span><span class="sxs-lookup"><span data-stu-id="462ac-131">If hello time token is used in hello prefix path, specify hello time format in which your files are organized.</span></span> <span data-ttu-id="462ac-132">Atualmente, o valor de saudação só tem suportada é HH.</span><span class="sxs-lookup"><span data-stu-id="462ac-132">Currently hello only supported value is HH.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="462ac-133">Formato de serialização do evento</span><span class="sxs-lookup"><span data-stu-id="462ac-133">Event Serialization Format</span></span></td>
<td><span data-ttu-id="462ac-134">Formato de serialização para dados de saída.</span><span class="sxs-lookup"><span data-stu-id="462ac-134">Serialization format for output data.</span></span> <span data-ttu-id="462ac-135">Há suporte para JSON, CSV e Avro.</span><span class="sxs-lookup"><span data-stu-id="462ac-135">JSON, CSV, and Avro are supported.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="462ac-136">Codificação</span><span class="sxs-lookup"><span data-stu-id="462ac-136">Encoding</span></span></td>
<td><span data-ttu-id="462ac-137">Se o formato for CSV ou JSON, uma codificação deve ser especificada.</span><span class="sxs-lookup"><span data-stu-id="462ac-137">If CSV or JSON format, an encoding must be specified.</span></span> <span data-ttu-id="462ac-138">UTF-8 é Olá somente suporte para formato de codificação no momento.</span><span class="sxs-lookup"><span data-stu-id="462ac-138">UTF-8 is hello only supported encoding format at this time.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="462ac-139">Delimitador</span><span class="sxs-lookup"><span data-stu-id="462ac-139">Delimiter</span></span></td>
<td><span data-ttu-id="462ac-140">Aplicável somente à serialização de CSV.</span><span class="sxs-lookup"><span data-stu-id="462ac-140">Only applicable for CSV serialization.</span></span> <span data-ttu-id="462ac-141">O Stream Analytics é compatível com vários delimitadores comuns para serialização de dados CSV.</span><span class="sxs-lookup"><span data-stu-id="462ac-141">Stream Analytics supports a number of common delimiters for serializing CSV data.</span></span> <span data-ttu-id="462ac-142">Os valores suportados são vírgula, ponto e vírgula, espaço, tab e barra vertical.</span><span class="sxs-lookup"><span data-stu-id="462ac-142">Supported values are comma, semicolon, space, tab and vertical bar.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="462ac-143">Formatar</span><span class="sxs-lookup"><span data-stu-id="462ac-143">Format</span></span></td>
<td><span data-ttu-id="462ac-144">Aplicável somente para serialização JSON.</span><span class="sxs-lookup"><span data-stu-id="462ac-144">Only applicable for JSON serialization.</span></span> <span data-ttu-id="462ac-145">Linha separada Especifica que a saída de hello será formatada tendo cada objeto JSON separado por uma nova linha.</span><span class="sxs-lookup"><span data-stu-id="462ac-145">Line separated specifies that hello output will be formatted by having each JSON object separated by a new line.</span></span> <span data-ttu-id="462ac-146">Matriz Especifica que Olá saída será formatada como uma matriz de objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="462ac-146">Array specifies that hello output will be formatted as an array of JSON objects.</span></span></td>
</tr>
</tbody>
</table>

## <a name="renew-data-lake-store-authorization"></a><span data-ttu-id="462ac-147">Renovar autorização do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="462ac-147">Renew Data Lake Store Authorization</span></span>
<span data-ttu-id="462ac-148">Atualmente, há uma limitação de onde o token de autenticação Olá precisa toobe atualizada manualmente a cada 90 dias para todos os trabalhos com a saída do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="462ac-148">Currently, there is a limitation where hello authentication token needs toobe manually refreshed every 90 days for all jobs with Data Lake Store output.</span></span> <span data-ttu-id="462ac-149">Você também precisará toore-autenticar sua conta do repositório Data Lake se você alterou sua senha desde que o trabalho foi criado ou última autenticado.</span><span class="sxs-lookup"><span data-stu-id="462ac-149">You will also need toore-authenticate your Data Lake Store account if you have changed your password since your job was created or last authenticated.</span></span> <span data-ttu-id="462ac-150">Um sintoma desse problema é nenhuma saída de trabalho e um erro nos Logs de operação Olá indicando a necessidade de autorização novamente.</span><span class="sxs-lookup"><span data-stu-id="462ac-150">A symptom of this issue is no job output and an error in hello Operation Logs indicating need for re-authorization.</span></span>

<span data-ttu-id="462ac-151">tooresolve esse problema, interromper seu trabalho em execução e vá repositório tooyour Data Lake de saída.</span><span class="sxs-lookup"><span data-stu-id="462ac-151">tooresolve this issue, stop your running job and go tooyour Data Lake Store output.</span></span> <span data-ttu-id="462ac-152">Clique o link de "Renovar autorização" Olá e por um curto período uma página será exibida indicando "Redirecionando tooauthorization...".</span><span class="sxs-lookup"><span data-stu-id="462ac-152">Click hello “Renew authorization” link, and for a brief time a page will pop up indicating “Redirecting tooauthorization..”.</span></span> <span data-ttu-id="462ac-153">página de saudação será fechada automaticamente e se for bem-sucedido, a indicação "Autorização foi renovada com êxito".</span><span class="sxs-lookup"><span data-stu-id="462ac-153">hello page will automatically close and if successful, will indicate “Authorization has been successfully renewed”.</span></span> <span data-ttu-id="462ac-154">Você precisa tooclick "Salvar" final Olá Olá página e pode continuar, reiniciar o trabalho de saudação perda de dados tooavoid hora da última interrupção.</span><span class="sxs-lookup"><span data-stu-id="462ac-154">You then need tooclick “Save” at hello bottom of hello page, and can proceed by restarting your job from hello Last Stopped Time tooavoid data loss.</span></span>

![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-renew-authorization.png)

