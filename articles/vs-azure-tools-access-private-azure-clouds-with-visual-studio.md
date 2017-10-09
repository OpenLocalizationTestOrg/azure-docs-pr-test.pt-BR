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
# <a name="accessing-private-azure-clouds-with-visual-studio"></a>Acessando nuvens privadas do Azure com o Visual Studio
Por padrão, o Visual Studio dá suporte a pontos de extremidade REST de nuvem pública do Azure. Neste tópico, você aprenderá como toouse sua nuvem privada do certificado tooaccess - e interagir com - Olá nuvem privada do Visual Studio.

## <a name="tooaccess-a-private-azure-cloud-in-visual-studio"></a>tooaccess um Azure privado de nuvem no Visual Studio
1. Em Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885) para nuvem privada do hello, baixe o arquivo de configurações de publicação ou contate o administrador para um arquivo de configurações de publicação. Na versão pública de saudação do Azure, Olá toodownload link trata [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/). (o arquivo baixado Olá deve ter uma extensão de `.publishsettings`)

1. Abra o Visual Studio

1. Em **Server Explorer**, Olá do botão direito do mouse **Azure** nó e, no menu de contexto hello, selecione **gerenciar e assinaturas de filtro**.
   
    ![Comando Gerenciar assinaturas](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790778.png)

1. Em Olá **gerenciar assinaturas do Microsoft Azure** caixa de diálogo, selecione Olá **certificados** guia e, em seguida, selecione **importação**.
   
    ![Importação de certificados do Azure](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790779.png)

1. Em Olá **importação assinatura do Microsoft Azure** caixa de diálogo, selecione **procurar**.

    ![Botão na caixa de diálogo de importação assinatura do Microsoft Azure Olá procurar](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/browse-button.png)

1. Em Olá **abrir** caixa de diálogo, procurar toohello diretório onde você Olá salvo-arquivo configurações de publicação, selecione Olá arquivo e, em seguida, selecione **abrir**.

    ![Selecione o arquivo de configurações de publicação Olá](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/select-publish-settings-file.png)

1. Quando retornado toohello **importação assinatura do Microsoft Azure** caixa de diálogo, selecione **importação**.

    ![Importar arquivo de configurações de publicação Olá](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790780.png)

    certificados Olá são importados do arquivo de configurações de publicação Olá para Visual Studio, e você agora pode interagir com seus recursos de nuvem privada.
   
## <a name="next-steps"></a>Próximas etapas
- [Publicação tooan serviço de nuvem do Azure do Visual Studio](https://msdn.microsoft.com/library/azure/ee460772.aspx)
- [Como baixar e importar informações de assinatura e configurações de publicação](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)
