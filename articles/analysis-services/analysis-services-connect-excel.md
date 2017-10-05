---
title: Conectar-se ao Azure Analysis Services com Excel | Microsoft Docs
description: Saiba como se conectar a um servidor Azure Analysis Services usando Excel.
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
ms.openlocfilehash: d51b6980120f1cf9bc8d053d463a73ac600b915f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-with-excel"></a><span data-ttu-id="e2273-103">Conectar com o Excel</span><span class="sxs-lookup"><span data-stu-id="e2273-103">Connect with Excel</span></span>

<span data-ttu-id="e2273-104">Depois de criar um servidor no Azure e implantar um modelo tabular, você estará pronto para se conectar e começar a explorar os dados.</span><span class="sxs-lookup"><span data-stu-id="e2273-104">Once you've created a server in Azure, and deployed a tabular model to it, you're ready to connect and begin exploring data.</span></span>


## <a name="connect-in-excel"></a><span data-ttu-id="e2273-105">Conectar-se no Excel</span><span class="sxs-lookup"><span data-stu-id="e2273-105">Connect in Excel</span></span>

<span data-ttu-id="e2273-106">Há suporte para a conexão com um servidor no Excel usando Obter Dados no Excel 2016.</span><span class="sxs-lookup"><span data-stu-id="e2273-106">Connecting to a server in Excel is supported by using Get Data in Excel 2016.</span></span> <span data-ttu-id="e2273-107">Não há suporte para a conexão usando o Assistente para Importar tabela no Power Pivot.</span><span class="sxs-lookup"><span data-stu-id="e2273-107">Connecting by using the Import Table Wizard in Power Pivot is not supported.</span></span> 

<span data-ttu-id="e2273-108">**Para se conectar no Excel 2016**</span><span class="sxs-lookup"><span data-stu-id="e2273-108">**To connect in Excel 2016**</span></span>

1. <span data-ttu-id="e2273-109">No Excel 2016, na faixa de opções **Dados**, clique em **Obter Dados Externos** > **De Outras Fontes** > **Do Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="e2273-109">In Excel 2016, on the **Data** ribbon, click **Get External Data** > **From Other Sources** > **From Analysis Services**.</span></span>

2. <span data-ttu-id="e2273-110">No Assistente de Conexão de Dados, em **Nome do servidor**, insira o nome do servidor, incluindo protocolo e URI.</span><span class="sxs-lookup"><span data-stu-id="e2273-110">In the Data Connection Wizard, in **Server name**, enter the server name including protocol and URI.</span></span> <span data-ttu-id="e2273-111">Em seguida, em **Credenciais de logon**, selecione **Usar o seguinte Nome de Usuário e Senha** e digite o nome de usuário da organização, por exemplo nancy@adventureworks.com, e a senha.</span><span class="sxs-lookup"><span data-stu-id="e2273-111">Then, in **Logon credentials**, select **Use the following User Name and Password**, and then type the organizational user name, for example nancy@adventureworks.com, and password.</span></span>

    ![Conectar a partir do logon do Excel](./media/analysis-services-connect-excel/aas-connect-excel-logon.png)

3. <span data-ttu-id="e2273-113">Em **Selecionar Banco de Dados e Tabela**, selecione o banco de dados e um modelo ou perspectiva e, em seguida, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="e2273-113">In **Select Database and Table**, select the database and model or perspective, and then click **Finish**.</span></span>
   
    ![Conectar a partir do modelo de seleção do Excel](./media/analysis-services-connect-excel/aas-connect-excel-select.png)


## <a name="see-also"></a><span data-ttu-id="e2273-115">Consulte também</span><span class="sxs-lookup"><span data-stu-id="e2273-115">See also</span></span>
<span data-ttu-id="e2273-116">[Bibliotecas do cliente](analysis-services-data-providers.md) </span><span class="sxs-lookup"><span data-stu-id="e2273-116">[Client libraries](analysis-services-data-providers.md) </span></span>  
[<span data-ttu-id="e2273-117">Gerenciar seu serviço</span><span class="sxs-lookup"><span data-stu-id="e2273-117">Manage your server</span></span>](analysis-services-manage.md)     


