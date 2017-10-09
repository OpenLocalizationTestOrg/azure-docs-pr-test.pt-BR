---
title: "funções de saudação aaaConfigure para um Azure serviço com o Visual Studio em nuvem | Microsoft Docs"
description: "Saiba como tooset e configurar funções para serviços de nuvem do Azure usando o Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: d397ef87-64e5-401a-aad5-7f83f1022e16
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: d3c62eb57040ebe987787e73b17b468bb82122bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-cloud-service-roles-with-visual-studio"></a><span data-ttu-id="e07a6-103">Configurar funções de serviço de nuvem do Azure com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e07a6-103">Configure Azure cloud service roles with Visual Studio</span></span>
<span data-ttu-id="e07a6-104">Um serviço de nuvem do Azure pode ter uma ou mais funções web ou de trabalho.</span><span class="sxs-lookup"><span data-stu-id="e07a6-104">An Azure cloud service can have one or more worker or web roles.</span></span> <span data-ttu-id="e07a6-105">Para cada função, você precisa toodefine como essa função é configurada e também configurar como essa função é executado.</span><span class="sxs-lookup"><span data-stu-id="e07a6-105">For each role, you need toodefine how that role is set up and also configure how that role runs.</span></span> <span data-ttu-id="e07a6-106">toolearn mais informações sobre funções em serviços de nuvem, consulte o vídeo Olá [tooAzure Introdução serviços de nuvem](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services).</span><span class="sxs-lookup"><span data-stu-id="e07a6-106">toolearn more about roles in cloud services, see hello video [Introduction tooAzure Cloud Services](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services).</span></span> 

<span data-ttu-id="e07a6-107">informações de saudação para seu serviço de nuvem são armazenadas no hello seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="e07a6-107">hello information for your cloud service is stored in hello following files:</span></span>

- <span data-ttu-id="e07a6-108">**Servicedefinition. Csdef** -arquivo de definição de serviço Olá define configurações de tempo de execução de saudação para seu serviço de nuvem, incluindo as funções que são necessárias, os pontos de extremidade e tamanho da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e07a6-108">**ServiceDefinition.csdef** - hello service definition file defines hello runtime settings for your cloud service including what roles are required, endpoints, and virtual machine size.</span></span> <span data-ttu-id="e07a6-109">Nenhum dos dados Olá armazenados em `ServiceDefinition.csdef` pode ser alterado quando a função está em execução.</span><span class="sxs-lookup"><span data-stu-id="e07a6-109">None of hello data stored in `ServiceDefinition.csdef` can be changed when your role is running.</span></span>
- <span data-ttu-id="e07a6-110">**ServiceConfiguration. cscfg** - arquivo de configuração de serviço Olá configura quantas instâncias de uma função são executadas e valores hello configurações de saudação definidos para uma função.</span><span class="sxs-lookup"><span data-stu-id="e07a6-110">**ServiceConfiguration.cscfg** - hello service configuration file configures how many instances of a role are run and hello values of hello settings defined for a role.</span></span> <span data-ttu-id="e07a6-111">Olá dados armazenados em `ServiceConfiguration.cscfg` pode ser alterado enquanto a função está em execução.</span><span class="sxs-lookup"><span data-stu-id="e07a6-111">hello data stored in `ServiceConfiguration.cscfg` can be changed while your role is running.</span></span>

<span data-ttu-id="e07a6-112">toostore diferente valores para configurações de saudação que controlam como uma função é executada, você pode definir várias configurações de serviço.</span><span class="sxs-lookup"><span data-stu-id="e07a6-112">toostore different values for hello settings that control how a role runs, you can define multiple service configurations.</span></span> <span data-ttu-id="e07a6-113">Você pode usar uma configuração de serviço diferente para cada ambiente de implantação.</span><span class="sxs-lookup"><span data-stu-id="e07a6-113">You can use a different service configuration for each deployment environment.</span></span> <span data-ttu-id="e07a6-114">Por exemplo, você pode definir o emulador de armazenamento do Azure local armazenamento conta conexão cadeia de caracteres toouse Olá em uma configuração de serviço local e criar outro toouse de configuração do serviço armazenamento do Azure na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="e07a6-114">For example, you can set your storage account connection string toouse hello local Azure storage emulator in a local service configuration and create another service configuration toouse Azure storage in hello cloud.</span></span>

<span data-ttu-id="e07a6-115">Quando você cria um serviço de nuvem do Azure no Visual Studio, duas configurações de serviço são criadas automaticamente e adicionado tooyour projeto do Azure:</span><span class="sxs-lookup"><span data-stu-id="e07a6-115">When you create an Azure cloud service in Visual Studio, two service configurations are automatically created and added tooyour Azure project:</span></span>

- `ServiceConfiguration.Cloud.cscfg`
- `ServiceConfiguration.Local.cscfg`

## <a name="configure-an-azure-cloud-service"></a><span data-ttu-id="e07a6-116">Configurar um serviço de nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="e07a6-116">Configure an Azure cloud service</span></span>
<span data-ttu-id="e07a6-117">Você pode configurar um serviço de nuvem do Azure no Gerenciador de soluções no Visual Studio, conforme mostrado no hello etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e07a6-117">You can configure an Azure cloud service from Solution Explorer in Visual Studio, as shown in hello following steps:</span></span>

1. <span data-ttu-id="e07a6-118">Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e07a6-118">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="e07a6-119">Em **Solution Explorer**, clique com botão direito Olá e, no menu de contexto hello, selecione **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="e07a6-119">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>
   
    ![Menu de contexto do projeto do Gerenciador de Soluções](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-project-context-menu.png)

1. <span data-ttu-id="e07a6-121">Na página de propriedades do projeto hello, selecione Olá **desenvolvimento** guia.</span><span class="sxs-lookup"><span data-stu-id="e07a6-121">In hello project's properties page, select hello **Development** tab.</span></span> 

    ![Página de propriedades do projeto — guia Desenvolvimento](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-development-tab.png)

1. <span data-ttu-id="e07a6-123">Em Olá **configuração do serviço** lista, o nome de saudação select da configuração de serviço Olá que você deseja tooedit.</span><span class="sxs-lookup"><span data-stu-id="e07a6-123">In hello **Service Configuration** list, select hello name of hello service configuration that you want tooedit.</span></span> <span data-ttu-id="e07a6-124">(Se você desejar toomake altera configurações de serviço tooall Olá para esta função, selecione **todas as configurações**.)</span><span class="sxs-lookup"><span data-stu-id="e07a6-124">(If you want toomake changes tooall hello service configurations for this role, select **All Configurations**.)</span></span>
   
    > [!IMPORTANT]
    > <span data-ttu-id="e07a6-125">Se você escolher uma configuração de serviço específica, algumas propriedades ficarão desabilitadas porque elas só podem ser definidas para todas as configurações.</span><span class="sxs-lookup"><span data-stu-id="e07a6-125">If you choose a specific service configuration, some properties are disabled because they can only be set for all configurations.</span></span> <span data-ttu-id="e07a6-126">tooedit essas propriedades, você deve selecionar **todas as configurações de**.</span><span class="sxs-lookup"><span data-stu-id="e07a6-126">tooedit these properties, you must select **All Configurations**.</span></span>
    > 
    > 
   
    ![Lista Configuração de Serviço para um serviço de nuvem do Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/cloud-service-service-configuration-property.png)

## <a name="change-hello-number-of-role-instances"></a><span data-ttu-id="e07a6-128">Saudação de alterar número de instâncias de função</span><span class="sxs-lookup"><span data-stu-id="e07a6-128">Change hello number of role instances</span></span>
<span data-ttu-id="e07a6-129">desempenho de saudação do tooimprove de seu serviço de nuvem, você pode alterar o número de saudação de instâncias de uma função em execução, com base no número de saudação de usuários ou carga Olá esperado para uma função específica.</span><span class="sxs-lookup"><span data-stu-id="e07a6-129">tooimprove hello performance of your cloud service, you can change hello number of instances of a role that are running, based on hello number of users or hello load expected for a particular role.</span></span> <span data-ttu-id="e07a6-130">Uma outra máquina virtual é criada para cada instância de uma função quando o serviço de nuvem Olá é executado no Azure.</span><span class="sxs-lookup"><span data-stu-id="e07a6-130">A separate virtual machine is created for each instance of a role when hello cloud service runs in Azure.</span></span> <span data-ttu-id="e07a6-131">Isso afeta a cobrança Olá para implantação de saudação deste serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="e07a6-131">This affects hello billing for hello deployment of this cloud service.</span></span> <span data-ttu-id="e07a6-132">Para obter mais informações sobre a fatura, veja [Entenda sua fatura do Microsoft Azure](billing/billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="e07a6-132">For more information about billing, see [Understand your bill for Microsoft Azure](billing/billing-understand-your-bill.md).</span></span>

1. <span data-ttu-id="e07a6-133">Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e07a6-133">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="e07a6-134">Em **Solution Explorer**, expanda o nó do projeto hello.</span><span class="sxs-lookup"><span data-stu-id="e07a6-134">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="e07a6-135">Em Olá **funções** nó, uma função de saudação atalho deseja tooupdate e, no menu de contexto hello, selecione **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="e07a6-135">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Menu de contexto da função do Azure no Gerenciador de Soluções](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="e07a6-137">Selecione Olá **configuração** guia.</span><span class="sxs-lookup"><span data-stu-id="e07a6-137">Select hello **Configuration** tab.</span></span>

    ![Guia Configuração](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page.png)

1. <span data-ttu-id="e07a6-139">Em Olá **configuração do serviço** lista, a configuração do serviço Olá selecione que você deseja tooupdate.</span><span class="sxs-lookup"><span data-stu-id="e07a6-139">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>
   
    ![Lista Configuração de Serviço](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-select-configuration.png)

1. <span data-ttu-id="e07a6-141">Em Olá **a contagem de instâncias** texto, digite o número de saudação de instâncias que você deseja toostart para essa função.</span><span class="sxs-lookup"><span data-stu-id="e07a6-141">In hello **Instance count** text box, enter hello number of instances that you want toostart for this role.</span></span> <span data-ttu-id="e07a6-142">Cada instância é executada em uma máquina virtual separada quando você publica Olá tooAzure de serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="e07a6-142">Each instance runs on a separate virtual machine when you publish hello cloud service tooAzure.</span></span>

    ![Atualizando Olá contagem de instâncias](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-instance-count.png)

1. <span data-ttu-id="e07a6-144">De saudação Visual Studio, ferramentas, selecione **salvar**.</span><span class="sxs-lookup"><span data-stu-id="e07a6-144">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="manage-connection-strings-for-storage-accounts"></a><span data-ttu-id="e07a6-145">Gerenciar cadeias de conexão para contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="e07a6-145">Manage connection strings for storage accounts</span></span>
<span data-ttu-id="e07a6-146">Você pode adicionar, remover ou modificar cadeias de conexão para suas configurações de serviço.</span><span class="sxs-lookup"><span data-stu-id="e07a6-146">You can add, remove, or modify connection strings for your service configurations.</span></span> <span data-ttu-id="e07a6-147">Por exemplo, você pode querer uma cadeia de conexão local para uma configuração de serviço local que tem um valor de `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="e07a6-147">For example, you might want a local connection string for a local service configuration that has a value of `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="e07a6-148">Você também poderá tooconfigure uma configuração de serviço de nuvem que usa uma conta de armazenamento no Azure.</span><span class="sxs-lookup"><span data-stu-id="e07a6-148">You might also want tooconfigure a cloud service configuration that uses a storage account in Azure.</span></span>

> [!WARNING]
> <span data-ttu-id="e07a6-149">Quando você insere informações chave de conta do armazenamento do Azure de Olá para uma cadeia de conexão da conta de armazenamento, essas informações são armazenadas localmente no arquivo de configuração do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="e07a6-149">When you enter hello Azure storage account key information for a storage account connection string, this information is stored locally in hello service configuration file.</span></span> <span data-ttu-id="e07a6-150">No entanto, atualmente essas informações não são armazenadas como texto criptografado.</span><span class="sxs-lookup"><span data-stu-id="e07a6-150">However, this information is currently not stored as encrypted text.</span></span>
> 
> 

<span data-ttu-id="e07a6-151">Usando um valor diferente para cada configuração de serviço, você não tem cadeias de caracteres de conexão diferentes toouse em seu serviço de nuvem ou modificar seu código, quando você publica seu tooAzure de serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="e07a6-151">By using a different value for each service configuration, you do not have toouse different connection strings in your cloud service or modify your code when you publish your cloud service tooAzure.</span></span> <span data-ttu-id="e07a6-152">Você pode usar o hello mesmo nome para a cadeia de caracteres de conexão de saudação em seu valor de código e hello é diferente, com base na configuração de serviço Olá selecionado quando você compila seu serviço de nuvem ou quando você publicá-la.</span><span class="sxs-lookup"><span data-stu-id="e07a6-152">You can use hello same name for hello connection string in your code and hello value is different, based on hello service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="e07a6-153">Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e07a6-153">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="e07a6-154">Em **Solution Explorer**, expanda o nó do projeto hello.</span><span class="sxs-lookup"><span data-stu-id="e07a6-154">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="e07a6-155">Em Olá **funções** nó, uma função de saudação atalho deseja tooupdate e, no menu de contexto hello, selecione **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="e07a6-155">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Menu de contexto da função do Azure no Gerenciador de Soluções](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="e07a6-157">Selecione Olá **configurações** guia.</span><span class="sxs-lookup"><span data-stu-id="e07a6-157">Select hello **Settings** tab.</span></span>

    ![Guia Configurações](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="e07a6-159">Em Olá **configuração do serviço** lista, a configuração do serviço Olá selecione que você deseja tooupdate.</span><span class="sxs-lookup"><span data-stu-id="e07a6-159">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>

    ![Configuração de Serviço](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="e07a6-161">tooadd uma cadeia de caracteres de conexão, selecione **Adicionar configuração**.</span><span class="sxs-lookup"><span data-stu-id="e07a6-161">tooadd a connection string, select **Add Setting**.</span></span>

    ![Adicionar cadeia de conexão](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="e07a6-163">Depois que a nova configuração de saudação adicionou toohello lista, atualize a linha de saudação na lista de saudação com informações necessárias hello.</span><span class="sxs-lookup"><span data-stu-id="e07a6-163">Once hello new setting has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![Nova cadeia de conexão](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="e07a6-165">**Nome** -insira Olá nome que você deseja toouse para cadeia de caracteres de conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="e07a6-165">**Name** - Enter hello name that you want toouse for hello connection string.</span></span>
    - <span data-ttu-id="e07a6-166">**Tipo** - selecione **cadeia de caracteres de Conexão** da lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="e07a6-166">**Type** - Select **Connection String** from hello drop-down list.</span></span>
    - <span data-ttu-id="e07a6-167">**Valor** -você pode inserir cadeia de caracteres de conexão Olá diretamente em Olá **valor** célula ou selecione Olá toowork de reticências (...) no hello **criar cadeia de Conexão de armazenamento** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e07a6-167">**Value** - You can either enter hello connection string directly into hello **Value** cell, or select hello ellipsis (...) toowork in hello **Create Storage Connection String** dialog.</span></span>  

1. <span data-ttu-id="e07a6-168">Em Olá **criar cadeia de Conexão de armazenamento** caixa de diálogo, selecione uma opção para **se conectar usando**.</span><span class="sxs-lookup"><span data-stu-id="e07a6-168">In hello **Create Storage Connection String** dialog, select an option for **Connect using**.</span></span> <span data-ttu-id="e07a6-169">Siga as instruções de saudação para opção Olá selecionada:</span><span class="sxs-lookup"><span data-stu-id="e07a6-169">Then follow hello instructions for hello option you select:</span></span>

    - <span data-ttu-id="e07a6-170">**Emulador de armazenamento do Microsoft Azure** -se você selecionar essa opção, configurações de saudação restantes na caixa de diálogo de saudação estão desabilitadas porque se aplicam somente tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e07a6-170">**Microsoft Azure storage emulator** - If you select this option, hello remaining settings on hello dialog are disabled as they apply only tooAzure.</span></span> <span data-ttu-id="e07a6-171">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="e07a6-171">Select **OK**.</span></span>
    - <span data-ttu-id="e07a6-172">**Sua assinatura** : se você selecionar essa opção, use Olá suspensa lista tooeither, selecione e logon em uma conta da Microsoft, ou adicionar uma conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e07a6-172">**Your subscription** - If you select this option, use hello dropdown list tooeither select and sign into a Microsoft account, or add a Microsoft account.</span></span> <span data-ttu-id="e07a6-173">Selecione uma assinatura do Azure e a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e07a6-173">Select an Azure subscription and storage account.</span></span> <span data-ttu-id="e07a6-174">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="e07a6-174">Select **OK**.</span></span>
    - <span data-ttu-id="e07a6-175">**Credenciais inseridas manualmente** - insira o nome de conta de armazenamento hello e o hello chave primária ou segundo.</span><span class="sxs-lookup"><span data-stu-id="e07a6-175">**Manually entered credentials** - Enter hello storage account name, and either hello primary or second key.</span></span> <span data-ttu-id="e07a6-176">Selecione uma opção para **Conexão** (HTTPS é recomendado na maioria dos cenários). Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="e07a6-176">Select an option for **Connection** (HTTPS is recommended for most scenarios.) Select **OK**.</span></span>

1. <span data-ttu-id="e07a6-177">toodelete uma cadeia de caracteres de conexão, selecione a cadeia de caracteres de conexão hello e, em seguida, selecione **remover configuração**.</span><span class="sxs-lookup"><span data-stu-id="e07a6-177">toodelete a connection string, select hello connection string, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="e07a6-178">De saudação Visual Studio, ferramentas, selecione **salvar**.</span><span class="sxs-lookup"><span data-stu-id="e07a6-178">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-connection-string"></a><span data-ttu-id="e07a6-179">Acessar uma cadeia de conexão de modo programático</span><span class="sxs-lookup"><span data-stu-id="e07a6-179">Programmatically access a connection string</span></span>

<span data-ttu-id="e07a6-180">Olá etapas a seguir mostram como tooprogrammatically acessar uma cadeia de caracteres de conexão usando o c#.</span><span class="sxs-lookup"><span data-stu-id="e07a6-180">hello following steps show how tooprogrammatically access a connection string using C#.</span></span>

1. <span data-ttu-id="e07a6-181">Adicione o seguinte Olá usando diretivas tooa c# arquivo onde você vai toouse configuração de saudação:</span><span class="sxs-lookup"><span data-stu-id="e07a6-181">Add hello following using directives tooa C# file where you are going toouse hello setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="e07a6-182">Olá, código a seguir ilustra um exemplo de como tooaccess uma cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="e07a6-182">hello following code illustrates an example of how tooaccess a connection string.</span></span> <span data-ttu-id="e07a6-183">Substituir saudação &lt;ConnectionStringName > espaço reservado com o valor apropriado de saudação.</span><span class="sxs-lookup"><span data-stu-id="e07a6-183">Replace hello &lt;ConnectionStringName> placeholder with hello appropriate value.</span></span> 

    ```csharp
    // Setup hello connection tooAzure Storage
    var storageAccount = CloudStorageAccount.Parse(RoleEnvironment.GetConfigurationSettingValue("<ConnectionStringName>"));
    ```

## <a name="add-custom-settings-toouse-in-your-azure-cloud-service"></a><span data-ttu-id="e07a6-184">Adicionar configurações personalizadas toouse em seu serviço de nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="e07a6-184">Add custom settings toouse in your Azure cloud service</span></span>
<span data-ttu-id="e07a6-185">As configurações personalizadas no arquivo de configuração de serviço Olá permitem adicionar um nome e valor para uma cadeia de caracteres para uma configuração de serviço específico.</span><span class="sxs-lookup"><span data-stu-id="e07a6-185">Custom settings in hello service configuration file let you add a name and value for a string for a specific service configuration.</span></span> <span data-ttu-id="e07a6-186">Você pode escolher toouse tooconfigure essa configuração que um recurso em seu serviço de nuvem lendo valor Olá Olá definindo e usando essa lógica de saudação do valor toocontrol no seu código.</span><span class="sxs-lookup"><span data-stu-id="e07a6-186">You might choose toouse this setting tooconfigure a feature in your cloud service by reading hello value of hello setting and using this value toocontrol hello logic in your code.</span></span> <span data-ttu-id="e07a6-187">Você pode alterar esses valores de configuração de serviço sem ter que toorebuild seu pacote de serviço ou quando o serviço de nuvem está em execução.</span><span class="sxs-lookup"><span data-stu-id="e07a6-187">You can change these service configuration values without having toorebuild your service package or when your cloud service is running.</span></span> <span data-ttu-id="e07a6-188">Seu código pode verificar se há notificações de quando uma configuração é alterada.</span><span class="sxs-lookup"><span data-stu-id="e07a6-188">Your code can check for notifications of when a setting changes.</span></span> <span data-ttu-id="e07a6-189">Consulte [Evento RoleEnvironment.Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).</span><span class="sxs-lookup"><span data-stu-id="e07a6-189">See [RoleEnvironment.Changing Event](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).</span></span>

<span data-ttu-id="e07a6-190">Você pode adicionar, remover ou modificar configurações personalizadas para suas configurações de serviço.</span><span class="sxs-lookup"><span data-stu-id="e07a6-190">You can add, remove, or modify custom settings for your service configurations.</span></span> <span data-ttu-id="e07a6-191">Talvez você queira valores diferentes para essas cadeias de caracteres para configurações de serviço diferentes.</span><span class="sxs-lookup"><span data-stu-id="e07a6-191">You might want different values for these strings for different service configurations.</span></span>

<span data-ttu-id="e07a6-192">Usando um valor diferente para cada configuração de serviço, você não tiver toouse cadeias de caracteres diferentes em seu serviço de nuvem ou modificar seu código, quando você publica seu tooAzure de serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="e07a6-192">By using a different value for each service configuration, you do not have toouse different strings in your cloud service or modify your code when you publish your cloud service tooAzure.</span></span> <span data-ttu-id="e07a6-193">Você pode usar o hello mesmo nome para a cadeia de caracteres de saudação em seu valor de código e hello é diferente, com base na configuração de serviço Olá selecionado quando você compila seu serviço de nuvem ou quando você publicá-la.</span><span class="sxs-lookup"><span data-stu-id="e07a6-193">You can use hello same name for hello string in your code and hello value is different, based on hello service configuration that you select when you build your cloud service or when you publish it.</span></span>

1. <span data-ttu-id="e07a6-194">Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e07a6-194">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="e07a6-195">Em **Solution Explorer**, expanda o nó do projeto hello.</span><span class="sxs-lookup"><span data-stu-id="e07a6-195">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="e07a6-196">Em Olá **funções** nó, uma função de saudação atalho deseja tooupdate e, no menu de contexto hello, selecione **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="e07a6-196">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Menu de contexto da função do Azure no Gerenciador de Soluções](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="e07a6-198">Selecione Olá **configurações** guia.</span><span class="sxs-lookup"><span data-stu-id="e07a6-198">Select hello **Settings** tab.</span></span>

    ![Guia Configurações](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. <span data-ttu-id="e07a6-200">Em Olá **configuração do serviço** lista, a configuração do serviço Olá selecione que você deseja tooupdate.</span><span class="sxs-lookup"><span data-stu-id="e07a6-200">In hello **Service Configuration** list, select hello service configuration that you want tooupdate.</span></span>

    ![Lista Configuração de Serviço](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. <span data-ttu-id="e07a6-202">tooadd uma configuração personalizada, selecione **Adicionar configuração**.</span><span class="sxs-lookup"><span data-stu-id="e07a6-202">tooadd a custom setting, select **Add Setting**.</span></span>

    ![Adicionar configuração personalizada](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. <span data-ttu-id="e07a6-204">Depois que a nova configuração de saudação adicionou toohello lista, atualize a linha de saudação na lista de saudação com informações necessárias hello.</span><span class="sxs-lookup"><span data-stu-id="e07a6-204">Once hello new setting has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![Nova configuração personalizada](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - <span data-ttu-id="e07a6-206">**Nome** -insira Olá nome da configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="e07a6-206">**Name** - Enter hello name of hello setting.</span></span>
    - <span data-ttu-id="e07a6-207">**Tipo** - selecione **cadeia de caracteres** da lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="e07a6-207">**Type** - Select **String** from hello drop-down list.</span></span>
    - <span data-ttu-id="e07a6-208">**Valor** -insira Olá valor de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="e07a6-208">**Value** - Enter hello value of hello setting.</span></span> <span data-ttu-id="e07a6-209">Você pode digitar o valor de saudação diretamente em Olá **valor** célula ou selecione Olá reticências (...) tooenter Olá valor em Olá **Editar cadeia de caracteres** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e07a6-209">You can either enter hello value directly into hello **Value** cell, or select hello ellipsis (...) tooenter hello value in hello **Edit String** dialog.</span></span>  

1. <span data-ttu-id="e07a6-210">toodelete uma configuração personalizada, selecione configuração de saudação e, em seguida, selecione **remover configuração**.</span><span class="sxs-lookup"><span data-stu-id="e07a6-210">toodelete a custom setting, select hello setting, and then select **Remove Setting**.</span></span>

1. <span data-ttu-id="e07a6-211">De saudação Visual Studio, ferramentas, selecione **salvar**.</span><span class="sxs-lookup"><span data-stu-id="e07a6-211">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-access-a-custom-settings-value"></a><span data-ttu-id="e07a6-212">Acessar o valor de uma configuração personalizada de modo programático</span><span class="sxs-lookup"><span data-stu-id="e07a6-212">Programmatically access a custom setting's value</span></span>
 
<span data-ttu-id="e07a6-213">Olá etapas a seguir mostram como tooprogrammatically acessar uma configuração personalizada usando c#.</span><span class="sxs-lookup"><span data-stu-id="e07a6-213">hello following steps show how tooprogrammatically access a custom setting using C#.</span></span>

1. <span data-ttu-id="e07a6-214">Adicione o seguinte Olá usando diretivas tooa c# arquivo onde você vai toouse configuração de saudação:</span><span class="sxs-lookup"><span data-stu-id="e07a6-214">Add hello following using directives tooa C# file where you are going toouse hello setting:</span></span>

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. <span data-ttu-id="e07a6-215">Olá, código a seguir ilustra um exemplo de como tooaccess uma configuração personalizada.</span><span class="sxs-lookup"><span data-stu-id="e07a6-215">hello following code illustrates an example of how tooaccess a custom setting.</span></span> <span data-ttu-id="e07a6-216">Substituir saudação &lt;SettingName > espaço reservado com o valor apropriado de saudação.</span><span class="sxs-lookup"><span data-stu-id="e07a6-216">Replace hello &lt;SettingName> placeholder with hello appropriate value.</span></span> 
    
    ```csharp
    var settingValue = RoleEnvironment.GetConfigurationSettingValue("<SettingName>");
    ```

## <a name="manage-local-storage-for-each-role-instance"></a><span data-ttu-id="e07a6-217">Gerenciar o armazenamento local para cada instância de função</span><span class="sxs-lookup"><span data-stu-id="e07a6-217">Manage local storage for each role instance</span></span>
<span data-ttu-id="e07a6-218">Você pode adicionar o armazenamento do sistema de arquivos local para cada instância de uma função.</span><span class="sxs-lookup"><span data-stu-id="e07a6-218">You can add local file system storage for each instance of a role.</span></span> <span data-ttu-id="e07a6-219">Olá dados armazenados no armazenamento não está acessível por outras instâncias de função Olá para qual Olá dados são armazenados, ou por outras funções.</span><span class="sxs-lookup"><span data-stu-id="e07a6-219">hello data stored in that storage is not accessible by other instances of hello role for which hello data is stored, or by other roles.</span></span>  

1. <span data-ttu-id="e07a6-220">Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e07a6-220">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="e07a6-221">Em **Solution Explorer**, expanda o nó do projeto hello.</span><span class="sxs-lookup"><span data-stu-id="e07a6-221">In **Solution Explorer**, expand hello project node.</span></span> <span data-ttu-id="e07a6-222">Em Olá **funções** nó, uma função de saudação atalho deseja tooupdate e, no menu de contexto hello, selecione **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="e07a6-222">Under hello **Roles** node, right-click hello role you want tooupdate, and, from hello context menu, select **Properties**.</span></span>

    ![Menu de contexto da função do Azure no Gerenciador de Soluções](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. <span data-ttu-id="e07a6-224">Selecione Olá **armazenamento Local** guia.</span><span class="sxs-lookup"><span data-stu-id="e07a6-224">Select hello **Local Storage** tab.</span></span>

    ![Guia Armazenamento local](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab.png)

1. <span data-ttu-id="e07a6-226">Em Olá **configuração do serviço** lista, verifique se **todas as configurações de** está selecionado como configurações de armazenamento local Olá aplicam configurações de serviço tooall.</span><span class="sxs-lookup"><span data-stu-id="e07a6-226">In hello **Service Configuration** list, ensure that **All Configurations** is selected as hello local storage settings apply tooall service configurations.</span></span> <span data-ttu-id="e07a6-227">Qualquer outro valor resulta em todos os campos de entrada hello na página hello está sendo desativado.</span><span class="sxs-lookup"><span data-stu-id="e07a6-227">Any other value results in all hello input fields on hello page being disabled.</span></span> 

    ![Lista Configuração de Serviço](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-service-configuration.png)

1. <span data-ttu-id="e07a6-229">tooadd uma entrada de armazenamento local, selecione **adicionar armazenamento Local**.</span><span class="sxs-lookup"><span data-stu-id="e07a6-229">tooadd a local storage entry, select **Add Local Storage**.</span></span>

    ![Adicionar armazenamento local](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-add-local-storage.png)

1. <span data-ttu-id="e07a6-231">Depois que a nova entrada de armazenamento local Olá adicionou toohello lista, atualize a linha de saudação na lista de saudação com informações necessárias hello.</span><span class="sxs-lookup"><span data-stu-id="e07a6-231">Once hello new local storage entry has been added toohello list, update hello row in hello list with hello necessary information.</span></span>

    ![Nova entrada de armazenamento local](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-new-local-storage.png)

    - <span data-ttu-id="e07a6-233">**Nome** -insira Olá nome que você deseja toouse para armazenamento local do novo hello.</span><span class="sxs-lookup"><span data-stu-id="e07a6-233">**Name** - Enter hello name that you want toouse for hello new local storage.</span></span>
    - <span data-ttu-id="e07a6-234">**Tamanho (MB)** -insira o tamanho de saudação em MB que é necessário para o armazenamento local do novo hello.</span><span class="sxs-lookup"><span data-stu-id="e07a6-234">**Size (MB)** - Enter hello size in MB that you need for hello new local storage.</span></span>
    - <span data-ttu-id="e07a6-235">**Limpeza na reciclagem da função** -selecione dados opção tooremove Olá no armazenamento local do novo hello quando a máquina virtual de saudação para função hello é reciclada.</span><span class="sxs-lookup"><span data-stu-id="e07a6-235">**Clean on role recycle** - Select this option tooremove hello data in hello new local storage when hello virtual machine for hello role is recycled.</span></span>

1. <span data-ttu-id="e07a6-236">toodelete uma entrada de armazenamento local, selecione entrada hello e, em seguida, selecione **remover armazenamento Local**.</span><span class="sxs-lookup"><span data-stu-id="e07a6-236">toodelete a local storage entry, select hello entry, and then select **Remove Local Storage**.</span></span>

1. <span data-ttu-id="e07a6-237">De saudação Visual Studio, ferramentas, selecione **salvar**.</span><span class="sxs-lookup"><span data-stu-id="e07a6-237">From hello Visual Studio, toolbar, select **Save**.</span></span>

## <a name="programmatically-accessing-local-storage"></a><span data-ttu-id="e07a6-238">Acessar o armazenamento local de modo programático</span><span class="sxs-lookup"><span data-stu-id="e07a6-238">Programmatically accessing local storage</span></span>

<span data-ttu-id="e07a6-239">Esta seção ilustra como tooprogrammatically acessar o armazenamento local usando c#, escrevendo um arquivo de texto de teste `MyLocalStorageTest.txt`.</span><span class="sxs-lookup"><span data-stu-id="e07a6-239">This section illustrates how tooprogrammatically access local storage using C# by writing a test text file `MyLocalStorageTest.txt`.</span></span>  

### <a name="write-a-text-file-toolocal-storage"></a><span data-ttu-id="e07a6-240">Gravar um armazenamento de toolocal do arquivo de texto</span><span class="sxs-lookup"><span data-stu-id="e07a6-240">Write a text file toolocal storage</span></span>

<span data-ttu-id="e07a6-241">saudação de código a seguir mostra um exemplo de como o armazenamento de toolocal de arquivo toowrite um texto.</span><span class="sxs-lookup"><span data-stu-id="e07a6-241">hello following code shows an example of how toowrite a text file toolocal storage.</span></span> <span data-ttu-id="e07a6-242">Substituir saudação &lt;LocalStorageName > espaço reservado com o valor apropriado de saudação.</span><span class="sxs-lookup"><span data-stu-id="e07a6-242">Replace hello &lt;LocalStorageName> placeholder with hello appropriate value.</span></span> 

    ```csharp
    // Retrieve an object that points toohello local storage resource
    LocalResource localResource = RoleEnvironment.GetLocalResource("<LocalStorageName>");
    
    //Define hello file name and path
    string[] paths = { localResource.RootPath, "MyLocalStorageTest.txt" };
    String filePath = Path.Combine(paths);
    
    using (FileStream writeStream = File.Create(filePath))
    {
        Byte[] textToWrite = new UTF8Encoding(true).GetBytes("Testing Web role storage");
        writeStream.Write(textToWrite, 0, textToWrite.Length);
    }

    ```

### <a name="find-a-file-written-toolocal-storage"></a><span data-ttu-id="e07a6-243">Localizar um arquivo gravado toolocal armazenamento</span><span class="sxs-lookup"><span data-stu-id="e07a6-243">Find a file written toolocal storage</span></span>

<span data-ttu-id="e07a6-244">arquivo de saudação tooview criado pelo código de saudação na seção anterior do hello, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="e07a6-244">tooview hello file created by hello code in hello previous section, follow these steps:</span></span>
    
1.  <span data-ttu-id="e07a6-245">Em Olá área de notificação do Windows, Olá ícone do Azure e, no menu de contexto hello, selecione **Mostrar UI do emulador de computação**.</span><span class="sxs-lookup"><span data-stu-id="e07a6-245">In hello Windows notification area, right-click hello Azure icon, and, from hello context menu, select **Show Compute Emulator UI**.</span></span> 

    ![Mostrar emulador de computação do Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/show-compute-emulator.png)

1. <span data-ttu-id="e07a6-247">Selecione a função da web de saudação.</span><span class="sxs-lookup"><span data-stu-id="e07a6-247">Select hello web role.</span></span>

    ![Emulador de computação do Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator.png)

1. <span data-ttu-id="e07a6-249">Em Olá **emulador de computação do Microsoft Azure** menu, selecione **ferramentas** > **abrir repositório local**.</span><span class="sxs-lookup"><span data-stu-id="e07a6-249">On hello **Microsoft Azure Compute Emulator** menu, select **Tools** > **Open local store**.</span></span>

    ![Item de menu Abrir repositório local](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator-open-local-store-menu.png)

1. <span data-ttu-id="e07a6-251">Quando a janela do Explorer do Windows hello for aberta, digite ' MyLocalStorageTest.txt ' em Olá **pesquisa** caixa de texto e selecione **Enter** toostart pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="e07a6-251">When hello Windows Explorer window opens, enter `MyLocalStorageTest.txt`\` into hello **Search** text box, and select **Enter** toostart hello search.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e07a6-252">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e07a6-252">Next steps</span></span>
<span data-ttu-id="e07a6-253">Saiba mais sobre projetos do Azure no Visual Studio, lendo [Configurando um projeto do Azure](vs-azure-tools-configuring-an-azure-project.md).</span><span class="sxs-lookup"><span data-stu-id="e07a6-253">Learn more about Azure projects in Visual Studio by reading [Configuring an Azure Project](vs-azure-tools-configuring-an-azure-project.md).</span></span> <span data-ttu-id="e07a6-254">Saiba mais sobre o esquema do serviço de nuvem Olá lendo [referência de esquema](https://msdn.microsoft.com/library/azure/dd179398).</span><span class="sxs-lookup"><span data-stu-id="e07a6-254">Learn more about hello cloud service schema by reading [Schema Reference](https://msdn.microsoft.com/library/azure/dd179398).</span></span>

