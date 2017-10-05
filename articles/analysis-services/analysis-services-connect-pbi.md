---
title: Conectar-se ao Azure Analysis Services com Power BI | Microsoft Docs
description: Saiba como se conectar a um servidor Azure Analysis Services usando Power BI.
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
ms.openlocfilehash: 3a2af043feddb4a1d6d63f50e838c8a39035449f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-with-power-bi"></a><span data-ttu-id="9e53c-103">Conectar com Power BI</span><span class="sxs-lookup"><span data-stu-id="9e53c-103">Connect with Power BI</span></span>

<span data-ttu-id="9e53c-104">Depois de criar um servidor no Azure e implantar um modelo tabular nele, os usuários em sua organização estarão prontos para se conectar e começar a explorar os dados.</span><span class="sxs-lookup"><span data-stu-id="9e53c-104">Once you've created a server in Azure, and deployed a tabular model to it, users in your organization are ready to connect and begin exploring data.</span></span> 

> [!TIP]
> <span data-ttu-id="9e53c-105">Certifique-se de usar a versão mais recente do [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="9e53c-105">Be sure to use the latest version of [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span></span>
> 
> 
  
## <a name="connect-in-power-bi-desktop"></a><span data-ttu-id="9e53c-106">Conexão no Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="9e53c-106">Connect in Power BI Desktop</span></span>

1. <span data-ttu-id="9e53c-107">No Power BI Desktop, clique em **Obter Dados** > **Azure** > **Banco de dados do Azure Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="9e53c-107">In Power BI Desktop, click **Get Data** > **Azure** > **Azure Analysis Services database**.</span></span>

2. <span data-ttu-id="9e53c-108">Em **Servidor**, insira o nome do servidor.</span><span class="sxs-lookup"><span data-stu-id="9e53c-108">In **Server**, enter the server name.</span></span> 
    
    <span data-ttu-id="9e53c-109">Certifique-se de incluir a URL completa.</span><span class="sxs-lookup"><span data-stu-id="9e53c-109">Be sure to include the full URL.</span></span> <span data-ttu-id="9e53c-110">Por exemplo, asazure://westcentralus.asazure.windows.net/advworks.</span><span class="sxs-lookup"><span data-stu-id="9e53c-110">For example, asazure://westcentralus.asazure.windows.net/advworks.</span></span>

3. <span data-ttu-id="9e53c-111">Em **Banco de Dados**, se você souber o nome do banco de dados de modelo de tabela ou da perspectiva a qual você deseja se conectar, cole-o aqui.</span><span class="sxs-lookup"><span data-stu-id="9e53c-111">In **Database**, if you know the name of the tabular model database or perspective you want to connect to, paste it here.</span></span> <span data-ttu-id="9e53c-112">Caso contrário, você pode deixar esse campo em branco e selecionar um banco de dados ou perspectiva posteriormente.</span><span class="sxs-lookup"><span data-stu-id="9e53c-112">Otherwise, you can leave this field blank and select a database or perspective later.</span></span>

4. <span data-ttu-id="9e53c-113">Deixe a opção **Conectar em tempo real** padrão selecionada e, em seguida, pressione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="9e53c-113">Leave the default **Connect live** option, then press **Connect**.</span></span> 

5. <span data-ttu-id="9e53c-114">Se solicitado, insira suas credenciais de logon.</span><span class="sxs-lookup"><span data-stu-id="9e53c-114">If prompted, enter your login credentials.</span></span> 

6. <span data-ttu-id="9e53c-115">Em **Navegador**, expanda o servidor e selecione o modelo ou a perspectiva que você deseja se conectar e clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="9e53c-115">In **Navigator**, expand the server, then select the model or perspective you want to connect to, then click **Connect**.</span></span> <span data-ttu-id="9e53c-116">Clique em um modelo ou perspectiva para exibir todos os objetos dessa visualização.</span><span class="sxs-lookup"><span data-stu-id="9e53c-116">Click  a model or perspective to show all the objects for that view.</span></span>

    <span data-ttu-id="9e53c-117">O modelo é aberto no Power BI Desktop com um relatório em branco na exibição de Relatório.</span><span class="sxs-lookup"><span data-stu-id="9e53c-117">The model opens in Power BI Desktop with a blank report in Report view.</span></span> <span data-ttu-id="9e53c-118">A lista de Campos exibe todos os objetos modelo não ocultos.</span><span class="sxs-lookup"><span data-stu-id="9e53c-118">The Fields list displays all non-hidden model objects.</span></span> <span data-ttu-id="9e53c-119">O status de conexão é exibido no canto inferior direito.</span><span class="sxs-lookup"><span data-stu-id="9e53c-119">Connection status is displayed in the lower-right corner.</span></span>

## <a name="connect-in-power-bi-service"></a><span data-ttu-id="9e53c-120">Conectar-se no Power BI (serviço)</span><span class="sxs-lookup"><span data-stu-id="9e53c-120">Connect in Power BI (service)</span></span>

1. <span data-ttu-id="9e53c-121">Crie um arquivo do Power BI Desktop que tenha uma conexão ativa com seu modelo no servidor.</span><span class="sxs-lookup"><span data-stu-id="9e53c-121">Create a Power BI Desktop file that has a live connection to your model on your server.</span></span>
2. <span data-ttu-id="9e53c-122">No [Power BI](https://powerbi.microsoft.com), clique em **Obter Dados** > **Arquivos**.</span><span class="sxs-lookup"><span data-stu-id="9e53c-122">In [Power BI](https://powerbi.microsoft.com), click **Get Data** > **Files**.</span></span> <span data-ttu-id="9e53c-123">Localize e selecione o arquivo.</span><span class="sxs-lookup"><span data-stu-id="9e53c-123">Locate and select your file.</span></span>



## <a name="see-also"></a><span data-ttu-id="9e53c-124">Consulte também</span><span class="sxs-lookup"><span data-stu-id="9e53c-124">See also</span></span>
<span data-ttu-id="9e53c-125">[Conectar-se ao Azure Analysis Services](analysis-services-connect.md) </span><span class="sxs-lookup"><span data-stu-id="9e53c-125">[Connect to Azure Analysis Services](analysis-services-connect.md) </span></span>  
[<span data-ttu-id="9e53c-126">Bibliotecas de cliente</span><span class="sxs-lookup"><span data-stu-id="9e53c-126">Client libraries</span></span>](analysis-services-data-providers.md)

