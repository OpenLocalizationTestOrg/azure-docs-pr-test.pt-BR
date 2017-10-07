---
title: "Instalação de tempo de execução de funções de aaaAzure | Microsoft Docs"
description: "Como tooInstall Olá tempo de execução de funções do Azure"
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 67c6d10b5c0ac43e880d29cff0ae7b099f82bdb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-functions-runtime-preview"></a>Instalar Olá visualização de tempo de execução de funções do Azure

Se você quiser visualizar de tempo de execução de funções do Azure Olá tooinstall, você deve seguir estas etapas:

1. Certifique-se de que sua máquina passa os requisitos mínimos de saudação
1. Baixar Olá [instalador de visualização do Azure funções em tempo de execução](https://aka.ms/azafr). 
1. Instalar visualização de tempo de execução de funções do Azure Olá
1. Configuração de saudação completa de visualização de tempo de execução de funções do Azure Olá

## <a name="prerequisites"></a>Pré-requisitos

Antes de instalar a visualização de tempo de execução de funções do Azure hello, você deve ter o seguinte hello:

1. Um computador executando o Microsoft Windows Server 2016 ou a Atualização do Microsoft Windows 10 para Criadores (Professional ou Enterprise Edition).
1. Uma instância do SQL Server em execução em sua rede.  O requisito mínimo de edição é o SQL Server Express.

## <a name="install-hello-azure-functions-runtime-preview"></a>Instalar Olá visualização de tempo de execução de funções do Azure

instalador de visualização de tempo de execução de funções do Azure Olá orientará você durante a instalação de saudação de visualização de tempo de execução de funções do Azure Olá gerenciamento e funções de trabalho.  É possível tooinstall Olá gerenciamento e função de trabalho no hello mesma máquina.  No entanto, à medida que você adiciona mais funções, você deve implantar mais funções de trabalho em máquinas adicionais toobe capaz de tooscale funções em vários trabalhadores.

## <a name="install-hello-management-and-worker-role-on-hello-same-machine"></a>Instalar hello gerenciamento e a função de trabalho em Olá mesmo computador

1. Execute Olá instalador de visualização do Azure funções em tempo de execução.

    ![Instalador da visualização do Azure Functions Runtime][1]

1. **Clique em Avançar** ampliar após o primeiro estágio de saudação do instalador de saudação
1. Depois que você leu termos Olá Olá **EULA**, **Olá caixa de seleção** termos de saudação tooaccept e **clique em Avançar** tooadvance.
1. Agora selecione Olá funções você deseja tooinstall nesta máquina **funções de gerenciamento de função** e/ou **funções de função de trabalho** e **clique em Avançar**

    ![Instalador da visualização do Azure Functions Runtime - Seleção de função][3]

    > [!NOTE]
    > Você pode instalar Olá **funções de função de trabalho** em muitos outros toodo máquinas assim, siga estas instruções e selecionar apenas **função de trabalho de funções** no instalador hello.

1. **Clique em Avançar** toohave Olá **instalador de tempo de execução de funções do Azure** instalar em seu computador.
1. Depois que o instalador completo Olá iniciará Olá **ferramenta de configuração de tempo de execução de funções do Azure**.

    ![Instalador da visualização do Azure Functions Runtime concluída][5]

    > [!NOTE]
    > Se você estiver instalando em **Windows 10** e hello **contêiner** recurso não foi previamente habilitado, hello **tempo de execução de funções do Azure** instalador solicita que você tooreboot saudação de toocomplete sua máquina instalar.

## <a name="configure-hello-azure-functions-runtime"></a>Configurar Olá tempo de execução de funções do Azure

Olá toocomplete instalação de tempo de execução de funções do Azure, você deve concluir a configuração de saudação.

1. Olá **ferramenta de configuração de tempo de execução de funções do Azure** mostra quais funções estão instaladas em seu computador.

    ![Ferramenta de configuração da visualização do Azure Functions Runtime][6]

1. Clique em Olá **banco de dados** , insira Olá **detalhes de conexão para sua instância do SQL Server** e **clique em aplicar**.  Isso é necessário em ordem toohello toocreate de tempo de execução de funções do Azure uma saudação toosupport do banco de dados em tempo de execução.
    
    ![Configuração de banco de dados da visualização do Azure Functions Runtime][7]

1. Clique em Olá **credenciais** guia.  Nessa tela, você deve criar duas credenciais novas para uso com um compartilhamento de arquivos para hospedagem de todas as suas Azure Functions.  **Especifique o nome de usuário e senha** combinações para Olá **proprietário do compartilhamento de arquivo** e Olá **usuário do compartilhamento de arquivo** e clique em **aplicar**.

    ![Credenciais da visualização do Azure Functions Runtime][8]

1. Clique em Olá **compartilhamento de arquivos** guia.  Nessa tela, você deve especificar os detalhes de saudação do hello **local de compartilhamento de arquivo**.  Isso pode ser criado para você, ou você pode usar um Compartilhamento de Arquivo existente e clicar em **Aplicar**.  Se você selecionar um novo local de compartilhamento de arquivos, você deve especificar um diretório para uso por Olá tempo de execução de funções do Azure.
    
    ![Compartilhamento de arquivo da visualização do Azure Functions Runtime][9]

1. Clique em Olá **IIS** guia.  Essa guia mostra detalhes de saudação de Olá sites no IIS que Olá instalação de tempo de execução de funções do Azure criará.  **Clique em aplicar** toocomplete.

    ![IIS da visualização do Azure Functions Runtime][10]

1. Clique em Olá **serviços** guia.  Essa guia mostra o status de saudação dos serviços de saudação na instalação do tempo de execução de funções do Azure.  Se, depois de saudação da configuração inicial **serviço de ativação de Host de funções do Azure** não está sendo executado clique **iniciar serviço**

    ![Configuração da visualização do Azure Functions Runtime completa][11]

1. Por fim, navegue toohello **Portal de tempo de execução de funções** como`https://<machinename>/`

    ![Portal de visualização do Azure Functions Runtime][12]


<!--Image references-->
[1]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer1.png
[2]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer2-EULA.png
[3]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer3-ChooseRoles.png
[4]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer4-Install.png
[5]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer5-InstallComplete.png
[6]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration1.png
[7]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration2_SQL.png
[8]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration3_Credentials.png
[9]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration4_Fileshare.png
[10]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration5_IIS.png
[11]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration6_Services.png
[12]: ./media/functions-runtime-install/AzureFunctionsRuntime_Portal.png