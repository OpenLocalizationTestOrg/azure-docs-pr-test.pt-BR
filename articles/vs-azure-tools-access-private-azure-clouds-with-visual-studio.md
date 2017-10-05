---
title: Acesso a nuvens privadas do Azure com o Visual Studio | Microsoft Docs
description: Saiba como acessar recursos de nuvem privada usando o Visual Studio.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 9d733c8d-703b-44e7-a210-bb75874c45c8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/19/2017
ms.author: kraigb
ms.openlocfilehash: b2578c837732ab05d538e9b896ed3a3035075a70
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="accessing-private-azure-clouds-with-visual-studio"></a><span data-ttu-id="ac580-103">Acessando nuvens privadas do Azure com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ac580-103">Accessing private Azure clouds with Visual Studio</span></span>
<span data-ttu-id="ac580-104">Por padrão, o Visual Studio dá suporte a pontos de extremidade REST de nuvem pública do Azure.</span><span class="sxs-lookup"><span data-stu-id="ac580-104">By default, Visual Studio supports public Azure cloud REST endpoints.</span></span> <span data-ttu-id="ac580-105">Neste tópico, você aprende a usar o certificado da nuvem privada para acessar – e interagir – com a nuvem privada no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ac580-105">In this topic, you learn how to use your private cloud's certificate to access - and interact with - the private cloud from Visual Studio.</span></span>

## <a name="to-access-a-private-azure-cloud-in-visual-studio"></a><span data-ttu-id="ac580-106">Para acessar uma nuvem privada do Azure no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ac580-106">To access a private Azure cloud in Visual Studio</span></span>
1. <span data-ttu-id="ac580-107">No [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885) da nuvem privada, baixe o arquivo de configurações de publicação ou contate o administrador para obter um arquivo de configurações de publicação.</span><span class="sxs-lookup"><span data-stu-id="ac580-107">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) for the private cloud, download your publish-settings file, or contact your administrator for a publish-settings file.</span></span> <span data-ttu-id="ac580-108">Na versão pública do Azure, o link para baixá-lo é [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/).</span><span class="sxs-lookup"><span data-stu-id="ac580-108">On the public version of Azure, the link to download this is [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/).</span></span> <span data-ttu-id="ac580-109">(O arquivo baixado deve ter uma extensão `.publishsettings`)</span><span class="sxs-lookup"><span data-stu-id="ac580-109">(The downloaded file should have an extension of `.publishsettings`)</span></span>

1. <span data-ttu-id="ac580-110">Abra o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ac580-110">Open Visual Studio</span></span>

1. <span data-ttu-id="ac580-111">No **Gerenciador de Servidores**, clique com o botão direito do mouse no nó **Azure** e, no menu de contexto, selecione **Gerenciar e Filtrar Assinaturas**.</span><span class="sxs-lookup"><span data-stu-id="ac580-111">In **Server Explorer**, right-click the **Azure** node and, from the context menu, select **Manage and Filter Subscriptions**.</span></span>
   
    ![Comando Gerenciar assinaturas](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790778.png)

1. <span data-ttu-id="ac580-113">Na caixa de diálogo **Gerenciar Assinaturas do Microsoft Azure**, selecione a guia **Certificados** e, em seguida, **Importar**.</span><span class="sxs-lookup"><span data-stu-id="ac580-113">In the **Manage Microsoft Azure Subscriptions** dialog, select the **Certificates** tab, and then select **Import**.</span></span>
   
    ![Importação de certificados do Azure](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790779.png)

1. <span data-ttu-id="ac580-115">Na caixa de diálogo **Importar Assinaturas do Microsoft Azure**, selecione **Procurar**.</span><span class="sxs-lookup"><span data-stu-id="ac580-115">In the **Import Microsoft Azure Subscriptions** dialog, select **Browse**.</span></span>

    ![Botão Procurar na caixa de diálogo Importar Assinaturas do Microsoft Azure](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/browse-button.png)

1. <span data-ttu-id="ac580-117">Na caixa de diálogo **Abrir**, procure o diretório em que você salvou o arquivo de configurações de publicação, selecione o arquivo e, em seguida, selecione **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="ac580-117">In the **Open** dialog, browse to the directory where you saved the publish-settings file, select the file, and then select **Open**.</span></span>

    ![Selecionar o arquivo de configurações de publicação](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/select-publish-settings-file.png)

1. <span data-ttu-id="ac580-119">Ao retornar para a caixa de diálogo **Importar Assinaturas do Microsoft Azure**, selecione **Importar**.</span><span class="sxs-lookup"><span data-stu-id="ac580-119">When returned to the **Import Microsoft Azure Subscriptions** dialog, select **Import**.</span></span>

    ![Importar o arquivo de configurações de publicação](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790780.png)

    <span data-ttu-id="ac580-121">Os certificados são importados do arquivo de configurações de publicação para o Visual Studio, e agora é possível interagir com os recursos de nuvem privada.</span><span class="sxs-lookup"><span data-stu-id="ac580-121">The certificates are imported from the publish-settings file into Visual Studio, and you can now interact with your private cloud resources.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="ac580-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ac580-122">Next steps</span></span>
- [<span data-ttu-id="ac580-123">Publicando em um Serviço de Nuvem do Azure do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ac580-123">Publishing to an Azure Cloud Service from Visual Studio</span></span>](https://msdn.microsoft.com/library/azure/ee460772.aspx)
- <span data-ttu-id="ac580-124">[Como baixar e importar informações de assinatura e configurações de publicação](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)</span><span class="sxs-lookup"><span data-stu-id="ac580-124">[How to: Download and Import Publish Settings and Subscription Information](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)</span></span>
