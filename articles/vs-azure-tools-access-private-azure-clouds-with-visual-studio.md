---
title: nuvens privadas do Azure de aaaAccessing com o Visual Studio | Microsoft Docs
description: Saiba como privada tooaccess recursos de nuvem usando o Visual Studio.
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
ms.openlocfilehash: 5cfd6439afdcf98c6f7d7f29ab6c4256ed02533a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-private-azure-clouds-with-visual-studio"></a><span data-ttu-id="e8166-103">Acessando nuvens privadas do Azure com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e8166-103">Accessing private Azure clouds with Visual Studio</span></span>
<span data-ttu-id="e8166-104">Por padrão, o Visual Studio dá suporte a pontos de extremidade REST de nuvem pública do Azure.</span><span class="sxs-lookup"><span data-stu-id="e8166-104">By default, Visual Studio supports public Azure cloud REST endpoints.</span></span> <span data-ttu-id="e8166-105">Neste tópico, você aprenderá como toouse sua nuvem privada do certificado tooaccess - e interagir com - Olá nuvem privada do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e8166-105">In this topic, you learn how toouse your private cloud's certificate tooaccess - and interact with - hello private cloud from Visual Studio.</span></span>

## <a name="tooaccess-a-private-azure-cloud-in-visual-studio"></a><span data-ttu-id="e8166-106">tooaccess um Azure privado de nuvem no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e8166-106">tooaccess a private Azure cloud in Visual Studio</span></span>
1. <span data-ttu-id="e8166-107">Em Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885) para nuvem privada do hello, baixe o arquivo de configurações de publicação ou contate o administrador para um arquivo de configurações de publicação.</span><span class="sxs-lookup"><span data-stu-id="e8166-107">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) for hello private cloud, download your publish-settings file, or contact your administrator for a publish-settings file.</span></span> <span data-ttu-id="e8166-108">Na versão pública de saudação do Azure, Olá toodownload link trata [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/).</span><span class="sxs-lookup"><span data-stu-id="e8166-108">On hello public version of Azure, hello link toodownload this is [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/).</span></span> <span data-ttu-id="e8166-109">(o arquivo baixado Olá deve ter uma extensão de `.publishsettings`)</span><span class="sxs-lookup"><span data-stu-id="e8166-109">(hello downloaded file should have an extension of `.publishsettings`)</span></span>

1. <span data-ttu-id="e8166-110">Abra o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e8166-110">Open Visual Studio</span></span>

1. <span data-ttu-id="e8166-111">Em **Server Explorer**, Olá do botão direito do mouse **Azure** nó e, no menu de contexto hello, selecione **gerenciar e assinaturas de filtro**.</span><span class="sxs-lookup"><span data-stu-id="e8166-111">In **Server Explorer**, right-click hello **Azure** node and, from hello context menu, select **Manage and Filter Subscriptions**.</span></span>
   
    ![Comando Gerenciar assinaturas](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790778.png)

1. <span data-ttu-id="e8166-113">Em Olá **gerenciar assinaturas do Microsoft Azure** caixa de diálogo, selecione Olá **certificados** guia e, em seguida, selecione **importação**.</span><span class="sxs-lookup"><span data-stu-id="e8166-113">In hello **Manage Microsoft Azure Subscriptions** dialog, select hello **Certificates** tab, and then select **Import**.</span></span>
   
    ![Importação de certificados do Azure](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790779.png)

1. <span data-ttu-id="e8166-115">Em Olá **importação assinatura do Microsoft Azure** caixa de diálogo, selecione **procurar**.</span><span class="sxs-lookup"><span data-stu-id="e8166-115">In hello **Import Microsoft Azure Subscriptions** dialog, select **Browse**.</span></span>

    ![Botão na caixa de diálogo de importação assinatura do Microsoft Azure Olá procurar](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/browse-button.png)

1. <span data-ttu-id="e8166-117">Em Olá **abrir** caixa de diálogo, procurar toohello diretório onde você Olá salvo-arquivo configurações de publicação, selecione Olá arquivo e, em seguida, selecione **abrir**.</span><span class="sxs-lookup"><span data-stu-id="e8166-117">In hello **Open** dialog, browse toohello directory where you saved hello publish-settings file, select hello file, and then select **Open**.</span></span>

    ![Selecione o arquivo de configurações de publicação Olá](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/select-publish-settings-file.png)

1. <span data-ttu-id="e8166-119">Quando retornado toohello **importação assinatura do Microsoft Azure** caixa de diálogo, selecione **importação**.</span><span class="sxs-lookup"><span data-stu-id="e8166-119">When returned toohello **Import Microsoft Azure Subscriptions** dialog, select **Import**.</span></span>

    ![Importar arquivo de configurações de publicação Olá](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790780.png)

    <span data-ttu-id="e8166-121">certificados Olá são importados do arquivo de configurações de publicação Olá para Visual Studio, e você agora pode interagir com seus recursos de nuvem privada.</span><span class="sxs-lookup"><span data-stu-id="e8166-121">hello certificates are imported from hello publish-settings file into Visual Studio, and you can now interact with your private cloud resources.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="e8166-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e8166-122">Next steps</span></span>
- [<span data-ttu-id="e8166-123">Publicação tooan serviço de nuvem do Azure do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e8166-123">Publishing tooan Azure Cloud Service from Visual Studio</span></span>](https://msdn.microsoft.com/library/azure/ee460772.aspx)
- <span data-ttu-id="e8166-124">[Como baixar e importar informações de assinatura e configurações de publicação](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)</span><span class="sxs-lookup"><span data-stu-id="e8166-124">[How to: Download and Import Publish Settings and Subscription Information](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)</span></span>
