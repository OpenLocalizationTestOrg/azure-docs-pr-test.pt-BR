---
title: aaaConnect tooAzure Analysis Services com o Excel | Microsoft Docs
description: Saiba como tooconnect tooan Azure Analysis Services server usando o Excel.
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
ms.openlocfilehash: 175b83e7d936716a626aa4b3bf22b5598bb983d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-excel"></a><span data-ttu-id="08896-103">Conectar com o Excel</span><span class="sxs-lookup"><span data-stu-id="08896-103">Connect with Excel</span></span>

<span data-ttu-id="08896-104">Depois que você criou um servidor no Azure e implantou um modelo de tabela tooit, você está pronto tooconnect e começar a explorar os dados.</span><span class="sxs-lookup"><span data-stu-id="08896-104">Once you've created a server in Azure, and deployed a tabular model tooit, you're ready tooconnect and begin exploring data.</span></span>


## <a name="connect-in-excel"></a><span data-ttu-id="08896-105">Conectar-se no Excel</span><span class="sxs-lookup"><span data-stu-id="08896-105">Connect in Excel</span></span>

<span data-ttu-id="08896-106">Há suporte para a conexão de servidor tooa no Excel usando obter dados no Excel 2016.</span><span class="sxs-lookup"><span data-stu-id="08896-106">Connecting tooa server in Excel is supported by using Get Data in Excel 2016.</span></span> <span data-ttu-id="08896-107">Não há suporte para a conexão usando Olá Assistente de importação de tabela no Power Pivot.</span><span class="sxs-lookup"><span data-stu-id="08896-107">Connecting by using hello Import Table Wizard in Power Pivot is not supported.</span></span> 

<span data-ttu-id="08896-108">**tooconnect no Excel 2016**</span><span class="sxs-lookup"><span data-stu-id="08896-108">**tooconnect in Excel 2016**</span></span>

1. <span data-ttu-id="08896-109">No Excel 2016, Olá **dados** de faixa de opções, clique em **obter dados externos** > **de outras fontes** > **do Analysis Services** .</span><span class="sxs-lookup"><span data-stu-id="08896-109">In Excel 2016, on hello **Data** ribbon, click **Get External Data** > **From Other Sources** > **From Analysis Services**.</span></span>

2. <span data-ttu-id="08896-110">Em Olá Assistente de Conexão de dados, em **nome do servidor**, digite nome do servidor de saudação incluindo protocolo e URI.</span><span class="sxs-lookup"><span data-stu-id="08896-110">In hello Data Connection Wizard, in **Server name**, enter hello server name including protocol and URI.</span></span> <span data-ttu-id="08896-111">Em seguida, em **credenciais de Logon**, selecione **Olá usar nome de usuário e senha a seguir**e digite o nome de usuário da organização hello, por exemplo nancy@adventureworks.come a senha.</span><span class="sxs-lookup"><span data-stu-id="08896-111">Then, in **Logon credentials**, select **Use hello following User Name and Password**, and then type hello organizational user name, for example nancy@adventureworks.com, and password.</span></span>

    ![Conectar a partir do logon do Excel](./media/analysis-services-connect-excel/aas-connect-excel-logon.png)

3. <span data-ttu-id="08896-113">Em **Selecionar banco de dados e tabela**, selecione o banco de dados de saudação e o modelo ou perspectiva e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="08896-113">In **Select Database and Table**, select hello database and model or perspective, and then click **Finish**.</span></span>
   
    ![Conectar a partir do modelo de seleção do Excel](./media/analysis-services-connect-excel/aas-connect-excel-select.png)


## <a name="see-also"></a><span data-ttu-id="08896-115">Consulte também</span><span class="sxs-lookup"><span data-stu-id="08896-115">See also</span></span>
<span data-ttu-id="08896-116">[Bibliotecas do cliente](analysis-services-data-providers.md) </span><span class="sxs-lookup"><span data-stu-id="08896-116">[Client libraries](analysis-services-data-providers.md) </span></span>  
[<span data-ttu-id="08896-117">Gerenciar seu serviço</span><span class="sxs-lookup"><span data-stu-id="08896-117">Manage your server</span></span>](analysis-services-manage.md)     


