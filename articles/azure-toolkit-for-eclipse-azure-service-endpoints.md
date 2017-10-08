---
title: "aaaAzure pontos de extremidade de serviço"
description: "Descreve as configurações de ponto de extremidade de serviço do Azure Olá no hello Kit de ferramentas do Azure para Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9c6125ec-7278-461e-b69c-ed56e844f742
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 357aa56409a894719077f2c8f302575c8ebb6883
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-endpoints"></a>Pontos de extremidade do Azure
Pontos de extremidade de serviço do Azure determinam que se o aplicativo é implantado tooand gerenciado pela plataforma global do Azure da saudação, Azure operado pela 21Vianet na China ou uma particular plataforma Windows Azure. Olá **pontos de extremidade de serviço** caixa de diálogo permite toospecify que você deseja toouse de pontos de extremidade de serviço. Olá tooopen **pontos de extremidade de serviço** caixa de diálogo, no Eclipse, clique em **janela**, clique em **preferências**, expanda **Azure**e, em seguida, clique em **Pontos de extremidade de serviço**. Saudação de configuração **conjunto ativo** campo determina qual serviço do Azure, pontos de extremidade serão usados para hello Azure projetos no seu espaço de trabalho atual.

Veja a seguir de Olá Olá **pontos de extremidade de serviço** caixa de diálogo.

![][ic719493]

## <a name="tooset-hello-service-endpoints"></a>pontos de extremidade do serviço tooset Olá
Em Olá **pontos de extremidade de serviço** caixa de diálogo, execute uma das seguintes ações de saudação:

* Se você quiser toouse Olá plataforma global do Azure, de saudação **conjunto ativo** lista suspensa, selecione **windowsazure.com** e clique em **Okey**.

* Se você quiser que o Azure operado pela 21Vianet na China, de saudação do toouse **conjunto ativo** lista suspensa, selecione **windowsazure.cn (China)** e clique em **Okey**.

* Se você desejar toouse uma plataforma privada do Azure:

  1. Clique em **Editar**.

  2. Abre uma caixa de diálogo, informando que Olá **pontos de extremidade de serviço** caixa de diálogo será fechada e o arquivo de definições de preferência Olá será aberto. Clique em **OK**.

  3. No arquivo do hello preferencesets.xml, crie um novo `preferenceset` elemento. Para esse novo elemento, criar `name`, `blob`, `management`, `portalURL` e `publishsettings` atributos e adicionar valores para eles que correspondam a plataforma do tooyour privada do Azure. Você pode usar valores hello fornecidos Olá existentes `preferenceset` elementos como modelos. **Observação**: Olá valor usado para Olá `blob` atributo deve conter o texto de saudação "blob" na URL de saudação.

  4. Salve e feche preferencesets.xml.

  5. Reabra Olá **pontos de extremidade de serviço** caixa de diálogo.

  6. De saudação **conjunto ativo** lista suspensa, selecione Olá ativo definido que você criou e clique em **Okey**.

  7. Depois de criar sua plataforma privada do Azure `preferenceset` elemento, você pode alterar Olá valores atribuídos tooit clicando Olá **editar** botão Olá **ponto de extremidade de serviços** caixa de diálogo. Se desejar, você também pode criar vários elementos `preferenceset` de plataformas privadas do Azure.

## <a name="see-also"></a>Consulte também
[Kit de Ferramentas do Azure para Eclipse][Azure Toolkit for Eclipse]

[Saudação de instalar o Kit de ferramentas do Azure para Eclipse][Installing hello Azure Toolkit for Eclipse] 

[Criar um aplicativo Hello World para Azure no Eclipse][Creating a Hello World Application for Azure in Eclipse]

Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
