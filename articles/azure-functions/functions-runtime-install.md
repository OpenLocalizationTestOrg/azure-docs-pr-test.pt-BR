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
# <a name="install-hello-azure-functions-runtime-preview"></a><span data-ttu-id="0105d-103">Instalar Olá visualização de tempo de execução de funções do Azure</span><span class="sxs-lookup"><span data-stu-id="0105d-103">Install hello Azure Functions Runtime Preview</span></span>

<span data-ttu-id="0105d-104">Se você quiser visualizar de tempo de execução de funções do Azure Olá tooinstall, você deve seguir estas etapas:</span><span class="sxs-lookup"><span data-stu-id="0105d-104">If you would like tooinstall hello Azure Functions Runtime preview, you must follow these steps:</span></span>

1. <span data-ttu-id="0105d-105">Certifique-se de que sua máquina passa os requisitos mínimos de saudação</span><span class="sxs-lookup"><span data-stu-id="0105d-105">Ensure your machine passes hello minimum requirements</span></span>
1. <span data-ttu-id="0105d-106">Baixar Olá [instalador de visualização do Azure funções em tempo de execução](https://aka.ms/azafr).</span><span class="sxs-lookup"><span data-stu-id="0105d-106">Download hello [Azure Functions Runtime Preview Installer](https://aka.ms/azafr).</span></span> 
1. <span data-ttu-id="0105d-107">Instalar visualização de tempo de execução de funções do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="0105d-107">Install hello Azure Functions Runtime preview</span></span>
1. <span data-ttu-id="0105d-108">Configuração de saudação completa de visualização de tempo de execução de funções do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="0105d-108">Complete hello configuration of hello Azure Functions Runtime preview</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0105d-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0105d-109">Prerequisites</span></span>

<span data-ttu-id="0105d-110">Antes de instalar a visualização de tempo de execução de funções do Azure hello, você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="0105d-110">Before you install hello Azure Functions Runtime preview, you must have hello following:</span></span>

1. <span data-ttu-id="0105d-111">Um computador executando o Microsoft Windows Server 2016 ou a Atualização do Microsoft Windows 10 para Criadores (Professional ou Enterprise Edition).</span><span class="sxs-lookup"><span data-stu-id="0105d-111">A machine running Microsoft Windows Server 2016 or Microsoft Windows 10 Creators Update (Professional or Enterprise Edition).</span></span>
1. <span data-ttu-id="0105d-112">Uma instância do SQL Server em execução em sua rede.</span><span class="sxs-lookup"><span data-stu-id="0105d-112">A SQL Server instance running within your network.</span></span>  <span data-ttu-id="0105d-113">O requisito mínimo de edição é o SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="0105d-113">Minimum edition requirement is SQL Server Express.</span></span>

## <a name="install-hello-azure-functions-runtime-preview"></a><span data-ttu-id="0105d-114">Instalar Olá visualização de tempo de execução de funções do Azure</span><span class="sxs-lookup"><span data-stu-id="0105d-114">Install hello Azure Functions Runtime Preview</span></span>

<span data-ttu-id="0105d-115">instalador de visualização de tempo de execução de funções do Azure Olá orientará você durante a instalação de saudação de visualização de tempo de execução de funções do Azure Olá gerenciamento e funções de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0105d-115">hello Azure Functions Runtime preview installer guides you through hello installation of hello Azure Functions Runtime preview Management and Worker Roles.</span></span>  <span data-ttu-id="0105d-116">É possível tooinstall Olá gerenciamento e função de trabalho no hello mesma máquina.</span><span class="sxs-lookup"><span data-stu-id="0105d-116">It is possible tooinstall hello Management and Worker role on hello same machine.</span></span>  <span data-ttu-id="0105d-117">No entanto, à medida que você adiciona mais funções, você deve implantar mais funções de trabalho em máquinas adicionais toobe capaz de tooscale funções em vários trabalhadores.</span><span class="sxs-lookup"><span data-stu-id="0105d-117">However, as you add more Functions, you must deploy more worker roles on additional machines toobe able tooscale your functions onto multiple workers.</span></span>

## <a name="install-hello-management-and-worker-role-on-hello-same-machine"></a><span data-ttu-id="0105d-118">Instalar hello gerenciamento e a função de trabalho em Olá mesmo computador</span><span class="sxs-lookup"><span data-stu-id="0105d-118">Install hello Management and Worker Role on hello same machine</span></span>

1. <span data-ttu-id="0105d-119">Execute Olá instalador de visualização do Azure funções em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="0105d-119">Run hello Azure Functions Runtime Preview Installer.</span></span>

    ![Instalador da visualização do Azure Functions Runtime][1]

1. <span data-ttu-id="0105d-121">**Clique em Avançar** ampliar após o primeiro estágio de saudação do instalador de saudação</span><span class="sxs-lookup"><span data-stu-id="0105d-121">**Click Next** advance past hello first stage of hello installer</span></span>
1. <span data-ttu-id="0105d-122">Depois que você leu termos Olá Olá **EULA**, **Olá caixa de seleção** termos de saudação tooaccept e **clique em Avançar** tooadvance.</span><span class="sxs-lookup"><span data-stu-id="0105d-122">Once you have read hello terms of hello **EULA**, **check hello box** tooaccept hello terms and **click Next** tooadvance.</span></span>
1. <span data-ttu-id="0105d-123">Agora selecione Olá funções você deseja tooinstall nesta máquina **funções de gerenciamento de função** e/ou **funções de função de trabalho** e **clique em Avançar**</span><span class="sxs-lookup"><span data-stu-id="0105d-123">Now select hello roles you want tooinstall on this machine **Functions Management Role** and/or **Functions Worker Role** and **Click Next**</span></span>

    ![Instalador da visualização do Azure Functions Runtime - Seleção de função][3]

    > [!NOTE]
    > <span data-ttu-id="0105d-125">Você pode instalar Olá **funções de função de trabalho** em muitos outros toodo máquinas assim, siga estas instruções e selecionar apenas **função de trabalho de funções** no instalador hello.</span><span class="sxs-lookup"><span data-stu-id="0105d-125">You can install hello **Functions Worker Role** on many other machines toodo so, follow these instructions, and only select **Functions Worker Role** in hello installer.</span></span>

1. <span data-ttu-id="0105d-126">**Clique em Avançar** toohave Olá **instalador de tempo de execução de funções do Azure** instalar em seu computador.</span><span class="sxs-lookup"><span data-stu-id="0105d-126">**Click Next** toohave hello **Azure Functions Runtime Installer** install on your machine.</span></span>
1. <span data-ttu-id="0105d-127">Depois que o instalador completo Olá iniciará Olá **ferramenta de configuração de tempo de execução de funções do Azure**.</span><span class="sxs-lookup"><span data-stu-id="0105d-127">Once complete hello installer will launch hello **Azure Functions Runtime Configuration tool**.</span></span>

    ![Instalador da visualização do Azure Functions Runtime concluída][5]

    > [!NOTE]
    > <span data-ttu-id="0105d-129">Se você estiver instalando em **Windows 10** e hello **contêiner** recurso não foi previamente habilitado, hello **tempo de execução de funções do Azure** instalador solicita que você tooreboot saudação de toocomplete sua máquina instalar.</span><span class="sxs-lookup"><span data-stu-id="0105d-129">If you are installing on **Windows 10** and hello **Container** feature has not been previously enabled, hello **Azure Functions Runtime** Installer prompts you tooreboot your machine toocomplete hello install.</span></span>

## <a name="configure-hello-azure-functions-runtime"></a><span data-ttu-id="0105d-130">Configurar Olá tempo de execução de funções do Azure</span><span class="sxs-lookup"><span data-stu-id="0105d-130">Configure hello Azure Functions Runtime</span></span>

<span data-ttu-id="0105d-131">Olá toocomplete instalação de tempo de execução de funções do Azure, você deve concluir a configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="0105d-131">toocomplete hello Azure Functions Runtime installation you must complete hello configuration.</span></span>

1. <span data-ttu-id="0105d-132">Olá **ferramenta de configuração de tempo de execução de funções do Azure** mostra quais funções estão instaladas em seu computador.</span><span class="sxs-lookup"><span data-stu-id="0105d-132">hello **Azure Functions Runtime Configuration Tool** shows which roles are installed on your machine.</span></span>

    ![Ferramenta de configuração da visualização do Azure Functions Runtime][6]

1. <span data-ttu-id="0105d-134">Clique em Olá **banco de dados** , insira Olá **detalhes de conexão para sua instância do SQL Server** e **clique em aplicar**.</span><span class="sxs-lookup"><span data-stu-id="0105d-134">Click hello **Database** tab, enter hello **connection details for your SQL Server Instance** and **click Apply**.</span></span>  <span data-ttu-id="0105d-135">Isso é necessário em ordem toohello toocreate de tempo de execução de funções do Azure uma saudação toosupport do banco de dados em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="0105d-135">This is required in order toohello Azure Functions Runtime toocreate a database toosupport hello Runtime.</span></span>
    
    ![Configuração de banco de dados da visualização do Azure Functions Runtime][7]

1. <span data-ttu-id="0105d-137">Clique em Olá **credenciais** guia.  Nessa tela, você deve criar duas credenciais novas para uso com um compartilhamento de arquivos para hospedagem de todas as suas Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="0105d-137">Click hello **Credentials** tab.  On this screen you must create two new credentials for use with a FileShare for hosting all your Azure Functions.</span></span>  <span data-ttu-id="0105d-138">**Especifique o nome de usuário e senha** combinações para Olá **proprietário do compartilhamento de arquivo** e Olá **usuário do compartilhamento de arquivo** e clique em **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="0105d-138">**Specify Username and Password** combinations for hello **File Share Owner** and for hello **File Share User** and click **Apply**.</span></span>

    ![Credenciais da visualização do Azure Functions Runtime][8]

1. <span data-ttu-id="0105d-140">Clique em Olá **compartilhamento de arquivos** guia.  Nessa tela, você deve especificar os detalhes de saudação do hello **local de compartilhamento de arquivo**.</span><span class="sxs-lookup"><span data-stu-id="0105d-140">Click hello **File Share** tab.  In this screen you must specify hello details of hello **File Share location**.</span></span>  <span data-ttu-id="0105d-141">Isso pode ser criado para você, ou você pode usar um Compartilhamento de Arquivo existente e clicar em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="0105d-141">This can be created for you or you can use an existing File Share and click **Apply**.</span></span>  <span data-ttu-id="0105d-142">Se você selecionar um novo local de compartilhamento de arquivos, você deve especificar um diretório para uso por Olá tempo de execução de funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="0105d-142">If you select a new File Share location, you must specify a directory for use by hello Azure Functions Runtime.</span></span>
    
    ![Compartilhamento de arquivo da visualização do Azure Functions Runtime][9]

1. <span data-ttu-id="0105d-144">Clique em Olá **IIS** guia.  Essa guia mostra detalhes de saudação de Olá sites no IIS que Olá instalação de tempo de execução de funções do Azure criará.</span><span class="sxs-lookup"><span data-stu-id="0105d-144">Click hello **IIS** tab.  This tab shows hello details of hello websites in IIS that hello Azure Functions Runtime Installation will create.</span></span>  <span data-ttu-id="0105d-145">**Clique em aplicar** toocomplete.</span><span class="sxs-lookup"><span data-stu-id="0105d-145">**Click Apply** toocomplete.</span></span>

    ![IIS da visualização do Azure Functions Runtime][10]

1. <span data-ttu-id="0105d-147">Clique em Olá **serviços** guia.  Essa guia mostra o status de saudação dos serviços de saudação na instalação do tempo de execução de funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="0105d-147">Click hello **Services** tab.  This tab shows hello status of hello services in your Azure Functions Runtime installation.</span></span>  <span data-ttu-id="0105d-148">Se, depois de saudação da configuração inicial **serviço de ativação de Host de funções do Azure** não está sendo executado clique **iniciar serviço**</span><span class="sxs-lookup"><span data-stu-id="0105d-148">If after initial configuration hello **Azure Functions Host Activation Service** is not running click **Start Service**</span></span>

    ![Configuração da visualização do Azure Functions Runtime completa][11]

1. <span data-ttu-id="0105d-150">Por fim, navegue toohello **Portal de tempo de execução de funções** como`https://<machinename>/`</span><span class="sxs-lookup"><span data-stu-id="0105d-150">Finally browse toohello **Azure Functions Runtime Portal** as `https://<machinename>/`</span></span>

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