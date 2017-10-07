---
title: "aaaHow tooretain um endereço IP virtual constante para um serviço de nuvem do Azure | Microsoft Docs"
description: "Saiba como tooensure que Olá endereço IP virtual (VIP) do seu serviço de nuvem do Azure não são alterados."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4a58e2c6-7a79-4051-8a2c-99182ff8b881
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 9e27121797ffb61517b8d2c2661ec44ff7298968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="retain-a-constant-virtual-ip-address-for-an-azure-cloud-service"></a>Reter um endereço IP virtual constante para um serviço de nuvem do Azure
Quando você atualizar um serviço de nuvem que está hospedado no Azure, talvez seja necessário tooensure endereço IP virtual (VIP) saudação do serviço de saudação não é alterado. Muitos serviços de gerenciamento de domínio usam Olá sistema de nome de domínio (DNS) para registrar nomes de domínio. DNS só funcionará se Olá VIP permanece Olá mesmo. Você pode usar o hello **Assistente de publicação** no tooensure de ferramentas do Azure que Olá VIP do seu serviço de nuvem não muda quando você atualizá-lo. Para obter mais informações sobre como toouse gerenciamento de domínio DNS para serviços de nuvem, consulte [Configurando um nome de domínio personalizado para um serviço de nuvem do Azure](cloud-services/cloud-services-custom-domain-name.md).

## <a name="publish-a-cloud-service-without-changing-its-vip"></a>Publicar um serviço de nuvem sem alterar seu VIP
Olá VIP de um serviço de nuvem é alocado quando você implanta-tooAzure em um ambiente específico, como o ambiente de produção de hello. alterações de VIP Olá somente se você excluir a implantação de saudação explicitamente ou implantação Olá é excluída implicitamente pela implantação Olá o processo de atualização. tooretain Olá VIP, você não deve excluir a implantação, e você deve assegurar-se de que o Visual Studio não exclui automaticamente sua implantação. 

Você pode especificar configurações de implantação no hello **Assistente de publicação**, que oferece suporte a várias opções de implantação. Você pode especificar uma nova implantação ou uma implantação de atualização, que pode ser incremental ou simultânea. Os dois tipos de implantação de atualização de mantém Olá VIP. Para obter definições desses tipos diferentes de implantação, consulte o [Assistente Publicar Aplicativo no Azure](vs-azure-tools-publish-azure-application-wizard.md). Além disso, você pode controlar se a implantação anterior Olá de um serviço de nuvem deve ser excluída se ocorrer um erro. Se você não definir essa opção corretamente, Olá VIP pode mudar inesperadamente.

## <a name="update-a-cloud-service-without-changing-its-vip"></a>Para atualizar um serviço de nuvem sem alterar o respectivo VIP
1. Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio. 

2. Em **Solution Explorer**, projeto de saudação do botão direito do mouse. No menu de atalho hello, selecione **publicar**.

    ![Menu Publicar](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/solution-explorer-publish-menu.png)

3. Em Olá **publicar aplicativo do Azure** caixa de diálogo, selecione Olá toowhich de assinatura do Azure você deseja toodeploy. Entre se necessário e selecione **Avançar**.

    ![Página Publicar Aplicativo do Azure – Entrar](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-signin.png)

4. Em Olá **configurações comuns** , verifique se esse nome de saudação do hello toowhich de serviço de nuvem você está implantando, hello **ambiente**, Olá **configuração de Build**e hello **Configuração do serviço** estão todos corretos.

    ![Guia Publicar aplicativo do Azure – Configurações Comuns](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-common-settings.png)

5. Em Olá **configurações avançadas** , verifique se esse Olá **rótulo de implantação** e hello **conta de armazenamento** estão corretas. Verifique se esse Olá **excluir implantação em caso de falha** caixa de seleção é desmarcada e verifique se esse Olá **atualização de implantação** caixa de seleção é marcada. Por limpar Olá **excluir implantação em caso de falha** caixa de seleção, você garantir que seu VIP não será perdida se ocorrer um erro durante a implantação. Selecionando Olá **atualização de implantação** caixa de seleção, você garantir que a implantação não é excluída e o VIP não é perdida quando você publicar novamente o aplicativo. 

    ![Guia Publicar aplicativo do Azure – Configurações Avançadas](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-advanced-settings.png)

6. toofurther especificar como você deseja Olá funções toobe atualizada, selecione **configurações** Avançar muito**atualização de implantação**. Selecione **Atualização incremental** ou **Atualização simultânea** e selecione **OK**. Escolha **atualização Incremental** tooupdate cada instância do seu aplicativo, um após o outro, para que Olá aplicativo está sempre disponível. Escolha **atualização simultânea** tooupdate todas as instâncias do seu aplicativo em Olá simultaneamente. Atualização simultânea é mais rápido, mas o serviço pode não estar disponível durante o processo de atualização de saudação. Quando tiver terminado, selecione **Avançar**.

    ![Página Publicar Aplicativo do Azure – Configurações de Implantação](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-deployment-update-settings.png)

7. Em Olá **publicar aplicativo do Azure** caixa de diálogo, selecione **próximo** até Olá **resumo** página é exibida. Verifique as configurações e, em seguida, selecione **Publicar**.
   
    ![Página Publicar Aplicativo do Azure – Resumo](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-summary.png)

## <a name="next-steps"></a>Próximas etapas
- [Usando o Visual Studio Azure Assistente para publicar aplicativo do hello](vs-azure-tools-publish-azure-application-wizard.md)

