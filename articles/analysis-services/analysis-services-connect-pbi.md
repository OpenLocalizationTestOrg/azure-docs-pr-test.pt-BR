---
title: aaaConnect tooAzure Analysis Services com o Power BI | Microsoft Docs
description: Saiba como tooconnect tooan Azure Analysis Services server usando o Power BI.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: f6c4cdec6edb92900ad2e552e23a4d9172ba9b84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-power-bi"></a><span data-ttu-id="aca87-103">Conectar com Power BI</span><span class="sxs-lookup"><span data-stu-id="aca87-103">Connect with Power BI</span></span>

<span data-ttu-id="aca87-104">Depois que você criou um servidor no Azure e implantou um modelo de tabela tooit, os usuários em sua organização são tooconnect pronto e começam a explorar os dados.</span><span class="sxs-lookup"><span data-stu-id="aca87-104">Once you've created a server in Azure, and deployed a tabular model tooit, users in your organization are ready tooconnect and begin exploring data.</span></span> 

> [!TIP]
> <span data-ttu-id="aca87-105">Ter a versão mais recente do se Olá de toouse de [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="aca87-105">Be sure toouse hello latest version of [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span></span>
> 
> 
  
## <a name="connect-in-power-bi-desktop"></a><span data-ttu-id="aca87-106">Conexão no Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="aca87-106">Connect in Power BI Desktop</span></span>

1. <span data-ttu-id="aca87-107">No Power BI Desktop, clique em **Obter Dados** > **Azure** > **Banco de dados do Azure Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="aca87-107">In Power BI Desktop, click **Get Data** > **Azure** > **Azure Analysis Services database**.</span></span>

2. <span data-ttu-id="aca87-108">Em **servidor**, digite o nome do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="aca87-108">In **Server**, enter hello server name.</span></span> 
    
    <span data-ttu-id="aca87-109">Ser se tooinclude Olá a URL completa.</span><span class="sxs-lookup"><span data-stu-id="aca87-109">Be sure tooinclude hello full URL.</span></span> <span data-ttu-id="aca87-110">Por exemplo, asazure://westcentralus.asazure.windows.net/advworks.</span><span class="sxs-lookup"><span data-stu-id="aca87-110">For example, asazure://westcentralus.asazure.windows.net/advworks.</span></span>

3. <span data-ttu-id="aca87-111">Em **banco de dados**, se você souber o nome de saudação do banco de dados de modelo de tabela Olá ou perspectiva que você deseja tooconnect para, cole-o aqui.</span><span class="sxs-lookup"><span data-stu-id="aca87-111">In **Database**, if you know hello name of hello tabular model database or perspective you want tooconnect to, paste it here.</span></span> <span data-ttu-id="aca87-112">Caso contrário, você pode deixar esse campo em branco e selecionar um banco de dados ou perspectiva posteriormente.</span><span class="sxs-lookup"><span data-stu-id="aca87-112">Otherwise, you can leave this field blank and select a database or perspective later.</span></span>

4. <span data-ttu-id="aca87-113">Deixe o padrão de saudação **conectar-se ao vivo** opção e, em seguida, pressione **conectar**.</span><span class="sxs-lookup"><span data-stu-id="aca87-113">Leave hello default **Connect live** option, then press **Connect**.</span></span> 

5. <span data-ttu-id="aca87-114">Se solicitado, insira suas credenciais de logon.</span><span class="sxs-lookup"><span data-stu-id="aca87-114">If prompted, enter your login credentials.</span></span> 

6. <span data-ttu-id="aca87-115">Em **navegador**, expanda o servidor de saudação e selecione o modelo hello ou perspectiva que você deseja tooconnect para, em seguida, clique em **conectar**.</span><span class="sxs-lookup"><span data-stu-id="aca87-115">In **Navigator**, expand hello server, then select hello model or perspective you want tooconnect to, then click **Connect**.</span></span> <span data-ttu-id="aca87-116">Clique em um modelo ou perspectiva tooshow todos os objetos de saudação para esse modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="aca87-116">Click  a model or perspective tooshow all hello objects for that view.</span></span>

    <span data-ttu-id="aca87-117">modelo de saudação é aberto no Power BI Desktop com um relatório em branco na exibição de relatório.</span><span class="sxs-lookup"><span data-stu-id="aca87-117">hello model opens in Power BI Desktop with a blank report in Report view.</span></span> <span data-ttu-id="aca87-118">lista de campos de saudação exibe todos os objetos de modelo não ocultos.</span><span class="sxs-lookup"><span data-stu-id="aca87-118">hello Fields list displays all non-hidden model objects.</span></span> <span data-ttu-id="aca87-119">Status da Conexão é exibido no canto inferior direito de saudação.</span><span class="sxs-lookup"><span data-stu-id="aca87-119">Connection status is displayed in hello lower-right corner.</span></span>

## <a name="connect-in-power-bi-service"></a><span data-ttu-id="aca87-120">Conectar-se no Power BI (serviço)</span><span class="sxs-lookup"><span data-stu-id="aca87-120">Connect in Power BI (service)</span></span>

1. <span data-ttu-id="aca87-121">Crie um arquivo de área de trabalho do Power BI com um modelo de tooyour de conexão ao vivo em seu servidor.</span><span class="sxs-lookup"><span data-stu-id="aca87-121">Create a Power BI Desktop file that has a live connection tooyour model on your server.</span></span>
2. <span data-ttu-id="aca87-122">No [Power BI](https://powerbi.microsoft.com), clique em **Obter Dados** > **Arquivos**.</span><span class="sxs-lookup"><span data-stu-id="aca87-122">In [Power BI](https://powerbi.microsoft.com), click **Get Data** > **Files**.</span></span> <span data-ttu-id="aca87-123">Localize e selecione o arquivo.</span><span class="sxs-lookup"><span data-stu-id="aca87-123">Locate and select your file.</span></span>



## <a name="see-also"></a><span data-ttu-id="aca87-124">Consulte também</span><span class="sxs-lookup"><span data-stu-id="aca87-124">See also</span></span>
<span data-ttu-id="aca87-125">[Conecte-se tooAzure Analysis Services](analysis-services-connect.md) </span><span class="sxs-lookup"><span data-stu-id="aca87-125">[Connect tooAzure Analysis Services](analysis-services-connect.md) </span></span>  
[<span data-ttu-id="aca87-126">Bibliotecas de cliente</span><span class="sxs-lookup"><span data-stu-id="aca87-126">Client libraries</span></span>](analysis-services-data-providers.md)

