---
title: "Instalação do Azure Functions Runtime | Microsoft Docs"
description: Como Instalar o Azure Functions Runtime
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
ms.openlocfilehash: 1e4188313a87d07f396e5f8edc8969dd5da2c436
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="install-the-azure-functions-runtime-preview"></a><span data-ttu-id="a98b5-103">Instalar a visualização do Azure Functions Runtime</span><span class="sxs-lookup"><span data-stu-id="a98b5-103">Install the Azure Functions Runtime Preview</span></span>

<span data-ttu-id="a98b5-104">Se você quiser instalar a visualização do Azure Functions Runtime, execute estas etapas:</span><span class="sxs-lookup"><span data-stu-id="a98b5-104">If you would like to install the Azure Functions Runtime preview, you must follow these steps:</span></span>

1. <span data-ttu-id="a98b5-105">Certifique-se de que sua máquina atenda aos requisitos mínimos</span><span class="sxs-lookup"><span data-stu-id="a98b5-105">Ensure your machine passes the minimum requirements</span></span>
1. <span data-ttu-id="a98b5-106">Baixe o [Instalador da visualização do Azure Functions Runtime](https://aka.ms/azafr).</span><span class="sxs-lookup"><span data-stu-id="a98b5-106">Download the [Azure Functions Runtime Preview Installer](https://aka.ms/azafr).</span></span> 
1. <span data-ttu-id="a98b5-107">Instalar a visualização do Azure Functions Runtime</span><span class="sxs-lookup"><span data-stu-id="a98b5-107">Install the Azure Functions Runtime preview</span></span>
1. <span data-ttu-id="a98b5-108">Concluir a configuração da visualização do Azure Functions Runtime</span><span class="sxs-lookup"><span data-stu-id="a98b5-108">Complete the configuration of the Azure Functions Runtime preview</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a98b5-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a98b5-109">Prerequisites</span></span>

<span data-ttu-id="a98b5-110">Antes de instalar a visualização do Azure Functions Runtime, você deve ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a98b5-110">Before you install the Azure Functions Runtime preview, you must have the following:</span></span>

1. <span data-ttu-id="a98b5-111">Um computador executando o Microsoft Windows Server 2016 ou a Atualização do Microsoft Windows 10 para Criadores (Professional ou Enterprise Edition).</span><span class="sxs-lookup"><span data-stu-id="a98b5-111">A machine running Microsoft Windows Server 2016 or Microsoft Windows 10 Creators Update (Professional or Enterprise Edition).</span></span>
1. <span data-ttu-id="a98b5-112">Uma instância do SQL Server em execução em sua rede.</span><span class="sxs-lookup"><span data-stu-id="a98b5-112">A SQL Server instance running within your network.</span></span>  <span data-ttu-id="a98b5-113">O requisito mínimo de edição é o SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="a98b5-113">Minimum edition requirement is SQL Server Express.</span></span>

## <a name="install-the-azure-functions-runtime-preview"></a><span data-ttu-id="a98b5-114">Instalar a visualização do Azure Functions Runtime</span><span class="sxs-lookup"><span data-stu-id="a98b5-114">Install the Azure Functions Runtime Preview</span></span>

<span data-ttu-id="a98b5-115">O instalador da versão prévia do Azure Functions Runtime orienta você durante a instalação das Funções de Gerenciamento e de Trabalho da versão prévia do Azure Functions Runtime.</span><span class="sxs-lookup"><span data-stu-id="a98b5-115">The Azure Functions Runtime preview installer guides you through the installation of the Azure Functions Runtime preview Management and Worker Roles.</span></span>  <span data-ttu-id="a98b5-116">É possível instalar as Funções de Gerenciamento e de Trabalho no mesmo computador.</span><span class="sxs-lookup"><span data-stu-id="a98b5-116">It is possible to install the Management and Worker role on the same machine.</span></span>  <span data-ttu-id="a98b5-117">No entanto, à medida que você adiciona mais funções, é necessário implantar mais funções de trabalho em computadores adicionais para poder escalar suas funções para vários trabalhadores.</span><span class="sxs-lookup"><span data-stu-id="a98b5-117">However, as you add more Functions, you must deploy more worker roles on additional machines to be able to scale your functions onto multiple workers.</span></span>

## <a name="install-the-management-and-worker-role-on-the-same-machine"></a><span data-ttu-id="a98b5-118">Instalar as Funções de Gerenciamento e de Trabalho no mesmo computador</span><span class="sxs-lookup"><span data-stu-id="a98b5-118">Install the Management and Worker Role on the same machine</span></span>

1. <span data-ttu-id="a98b5-119">Execute o Instalador da visualização do Azure Functions Runtime.</span><span class="sxs-lookup"><span data-stu-id="a98b5-119">Run the Azure Functions Runtime Preview Installer.</span></span>

    ![Instalador da visualização do Azure Functions Runtime][1]

1. <span data-ttu-id="a98b5-121">**Clique em Avançar** para passar para o primeiro estágio do instalador</span><span class="sxs-lookup"><span data-stu-id="a98b5-121">**Click Next** advance past the first stage of the installer</span></span>
1. <span data-ttu-id="a98b5-122">Depois de ler os termos do **EULA**, **marque a caixa** para aceitar os termos e **clique em Avançar** para avançar.</span><span class="sxs-lookup"><span data-stu-id="a98b5-122">Once you have read the terms of the **EULA**, **check the box** to accept the terms and **click Next** to advance.</span></span>
1. <span data-ttu-id="a98b5-123">Agora, selecione as funções que você deseja instalar neste computador **Função de Gerenciamento do Functions** e/ou **Função de Trabalho do Functions** e **clique em Avançar**</span><span class="sxs-lookup"><span data-stu-id="a98b5-123">Now select the roles you want to install on this machine **Functions Management Role** and/or **Functions Worker Role** and **Click Next**</span></span>

    ![Instalador da visualização do Azure Functions Runtime - Seleção de função][3]

    > [!NOTE]
    > <span data-ttu-id="a98b5-125">Você pode instalar a **Função de Trabalho do Functions** em muitas outras máquinas. Para fazer isso, siga estas instruções e selecione somente a **Função de Trabalho do Functions** no instalador.</span><span class="sxs-lookup"><span data-stu-id="a98b5-125">You can install the **Functions Worker Role** on many other machines to do so, follow these instructions, and only select **Functions Worker Role** in the installer.</span></span>

1. <span data-ttu-id="a98b5-126">**Clique em Avançar** para instalar o **Instalador do Azure Functions Runtime** em seu computador.</span><span class="sxs-lookup"><span data-stu-id="a98b5-126">**Click Next** to have the **Azure Functions Runtime Installer** install on your machine.</span></span>
1. <span data-ttu-id="a98b5-127">Após a conclusão, o instalador iniciará a **ferramenta de Configuração do Azure Functions Runtime**.</span><span class="sxs-lookup"><span data-stu-id="a98b5-127">Once complete the installer will launch the **Azure Functions Runtime Configuration tool**.</span></span>

    ![Instalador da visualização do Azure Functions Runtime concluída][5]

    > [!NOTE]
    > <span data-ttu-id="a98b5-129">Se você estiver instalando no **Windows 10** e o recurso **Contêiner** não tiver sido habilitado, o instalador do **Azure Functions Runtime** solicitará a reinicialização do computador para concluir a instalação.</span><span class="sxs-lookup"><span data-stu-id="a98b5-129">If you are installing on **Windows 10** and the **Container** feature has not been previously enabled, the **Azure Functions Runtime** Installer prompts you to reboot your machine to complete the install.</span></span>

## <a name="configure-the-azure-functions-runtime"></a><span data-ttu-id="a98b5-130">Configurar o Azure Functions Runtime</span><span class="sxs-lookup"><span data-stu-id="a98b5-130">Configure the Azure Functions Runtime</span></span>

<span data-ttu-id="a98b5-131">Para concluir a instalação do Azure Functions Runtime, você deverá concluir a configuração.</span><span class="sxs-lookup"><span data-stu-id="a98b5-131">To complete the Azure Functions Runtime installation you must complete the configuration.</span></span>

1. <span data-ttu-id="a98b5-132">A **ferramenta de Configuração do Azure Functions Runtime** mostra quais funções estão instaladas em seu computador.</span><span class="sxs-lookup"><span data-stu-id="a98b5-132">The **Azure Functions Runtime Configuration Tool** shows which roles are installed on your machine.</span></span>

    ![Ferramenta de configuração da visualização do Azure Functions Runtime][6]

1. <span data-ttu-id="a98b5-134">Clique na guia **Banco de Dados**, insira os **detalhes da conexão de sua instância do SQL Server** e **clique em Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="a98b5-134">Click the **Database** tab, enter the **connection details for your SQL Server Instance** and **click Apply**.</span></span>  <span data-ttu-id="a98b5-135">Isso é necessário para que o Azure Functions Runtime crie um banco de dados para dar suporte ao Runtime.</span><span class="sxs-lookup"><span data-stu-id="a98b5-135">This is required in order to the Azure Functions Runtime to create a database to support the Runtime.</span></span>
    
    ![Configuração de banco de dados da visualização do Azure Functions Runtime][7]

1. <span data-ttu-id="a98b5-137">Clique na guia **Credenciais**.</span><span class="sxs-lookup"><span data-stu-id="a98b5-137">Click the **Credentials** tab.</span></span>  <span data-ttu-id="a98b5-138">Nessa tela, você deve criar duas credenciais novas para uso com um compartilhamento de arquivos para hospedagem de todas as suas Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="a98b5-138">On this screen you must create two new credentials for use with a FileShare for hosting all your Azure Functions.</span></span>  <span data-ttu-id="a98b5-139">**Especifique combinações de nome de usuário e senha** para o **Proprietário do Compartilhamento de Arquivo** e para o **Usuário do Compartilhamento de Arquivo** e clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="a98b5-139">**Specify Username and Password** combinations for the **File Share Owner** and for the **File Share User** and click **Apply**.</span></span>

    ![Credenciais da visualização do Azure Functions Runtime][8]

1. <span data-ttu-id="a98b5-141">Clique na guia **Compartilhamento de Arquivos**.</span><span class="sxs-lookup"><span data-stu-id="a98b5-141">Click the **File Share** tab.</span></span>  <span data-ttu-id="a98b5-142">Nessa tela, você deve especificar os detalhes do **Local do Compartilhamento de Arquivo**.</span><span class="sxs-lookup"><span data-stu-id="a98b5-142">In this screen you must specify the details of the **File Share location**.</span></span>  <span data-ttu-id="a98b5-143">Isso pode ser criado para você, ou você pode usar um Compartilhamento de Arquivo existente e clicar em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="a98b5-143">This can be created for you or you can use an existing File Share and click **Apply**.</span></span>  <span data-ttu-id="a98b5-144">Se você selecionar um novo local de Compartilhamento de Arquivos, especifique um diretório para ser usado pelo Azure Functions Runtime.</span><span class="sxs-lookup"><span data-stu-id="a98b5-144">If you select a new File Share location, you must specify a directory for use by the Azure Functions Runtime.</span></span>
    
    ![Compartilhamento de arquivo da visualização do Azure Functions Runtime][9]

1. <span data-ttu-id="a98b5-146">Clique na guia **IIS**.</span><span class="sxs-lookup"><span data-stu-id="a98b5-146">Click the **IIS** tab.</span></span>  <span data-ttu-id="a98b5-147">Essa guia mostra os detalhes dos sites no IIS que serão criados pela instalação do Azure Functions Runtime.</span><span class="sxs-lookup"><span data-stu-id="a98b5-147">This tab shows the details of the websites in IIS that the Azure Functions Runtime Installation will create.</span></span>  <span data-ttu-id="a98b5-148">**Clique em Aplicar** para concluir.</span><span class="sxs-lookup"><span data-stu-id="a98b5-148">**Click Apply** to complete.</span></span>

    ![IIS da visualização do Azure Functions Runtime][10]

1. <span data-ttu-id="a98b5-150">Clique na guia **Serviços**.</span><span class="sxs-lookup"><span data-stu-id="a98b5-150">Click the **Services** tab.</span></span>  <span data-ttu-id="a98b5-151">Essa guia mostra o status dos serviços em sua instalação do Azure Functions Runtime.</span><span class="sxs-lookup"><span data-stu-id="a98b5-151">This tab shows the status of the services in your Azure Functions Runtime installation.</span></span>  <span data-ttu-id="a98b5-152">Se, após a configuração inicial, o **Serviço de Ativação de Host do Azure Functions** não estiver em execução, clique em **Iniciar Serviço**</span><span class="sxs-lookup"><span data-stu-id="a98b5-152">If after initial configuration the **Azure Functions Host Activation Service** is not running click **Start Service**</span></span>

    ![Configuração da visualização do Azure Functions Runtime completa][11]

1. <span data-ttu-id="a98b5-154">Por fim, navegue até o **Portal do Azure Functions Runtime** como`https://<machinename>/`</span><span class="sxs-lookup"><span data-stu-id="a98b5-154">Finally browse to the **Azure Functions Runtime Portal** as `https://<machinename>/`</span></span>

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