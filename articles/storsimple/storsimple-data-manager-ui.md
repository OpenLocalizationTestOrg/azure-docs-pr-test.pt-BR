---
title: "Interface do usuário do Gerenciador de Dados do Microsoft Azure StorSimple | Microsoft Docs"
description: "Descreve como usar a interface do usuário do serviço Gerenciador de Dados do StorSimple (visualização privada)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: 53a8599df2c647613122cd791b680e2e658586b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-using-the-storsimple-data-manager-service-ui-private-preview"></a><span data-ttu-id="726d0-103">Gerenciar usando a interface do usuário do serviço Gerenciador de Dados do StorSimple (visualização privada)</span><span class="sxs-lookup"><span data-stu-id="726d0-103">Manage using the StorSimple Data Manager service UI (Private Preview)</span></span>

<span data-ttu-id="726d0-104">Este artigo explica como você pode usar a interface do usuário do Gerenciador de Dados do StorSimple para executar a transformação em dados que residem em dispositivos das séries StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="726d0-104">This article explains how you can use the StorSimple Data Manager UI to perform data transformation on data residing on the StorSimple 8000 series devices.</span></span> <span data-ttu-id="726d0-105">Os dados transformados podem ser consumidos por outros serviços do Azure, como os Serviços de Mídia do Azure, Azure HDInsight, Azure Machine Learning e Azure Search.</span><span class="sxs-lookup"><span data-stu-id="726d0-105">The transformed data can then be consumed by other Azure services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search.</span></span> 


## <a name="use-storsimple-data-transformation"></a><span data-ttu-id="726d0-106">Usar a transformação de dados do StorSimple</span><span class="sxs-lookup"><span data-stu-id="726d0-106">Use StorSimple Data Transformation</span></span>

<span data-ttu-id="726d0-107">O Gerenciador de Dados do StorSimple é um recurso em que a Transformação de Dados pode ser instanciada.</span><span class="sxs-lookup"><span data-stu-id="726d0-107">The StorSimple Data Manager is the resource within which Data Transformation can be instantiated.</span></span> <span data-ttu-id="726d0-108">O serviço Transformação de Dados permite mover dados do dispositivo StorSimple local para blobs no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="726d0-108">The Data Transformation service lets you move data from your StorSimple on-premises device to blobs in Azure storage.</span></span> <span data-ttu-id="726d0-109">Portanto, no fluxo de trabalho, você precisa especificar os detalhes sobre seu dispositivo StorSimple e os dados de interesse que você deseja mover para a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="726d0-109">Hence, in workflow you need to specify the details about your StorSimple device and the data of interest that you want to move to the storage account.</span></span>

### <a name="create-a-storsimple-data-manager-service"></a><span data-ttu-id="726d0-110">Criar um serviço Gerenciador de Dados do StorSimple</span><span class="sxs-lookup"><span data-stu-id="726d0-110">Create a StorSimple Data Manager service</span></span>

<span data-ttu-id="726d0-111">Execute as etapas a seguir para criar um serviço Gerenciador de Dados do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="726d0-111">Perform the following steps to create a StorSimple Data Manager service.</span></span>

1. <span data-ttu-id="726d0-112">Para criar um serviço Gerenciador de Dados do StorSimple Manager, vá para [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)</span><span class="sxs-lookup"><span data-stu-id="726d0-112">To create a StorSimple Data Manager service, go to [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)</span></span>

2. <span data-ttu-id="726d0-113">Clique no ícone **+** e procure o Gerenciador de Dados do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="726d0-113">Click the **+** icon and search for StorSimple Data Manager.</span></span> <span data-ttu-id="726d0-114">Clique em seu serviço Gerenciador de Dados do StorSimple e então clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="726d0-114">Click your StorSimple Data Manager service and then click **Create**.</span></span>

3. <span data-ttu-id="726d0-115">Se sua assinatura está habilitada para a criação desse serviço, você verá a folha a seguir.</span><span class="sxs-lookup"><span data-stu-id="726d0-115">If your subscription is enabled for creating this service, you see the following blade.</span></span>

    ![Criar um recurso Gerenciadores de Dados do StorSimple](./media/storsimple-data-manager-ui/create-new-data-manager-service.png)

4. <span data-ttu-id="726d0-117">Insira as entradas e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="726d0-117">Enter the inputs and click **Create**.</span></span> <span data-ttu-id="726d0-118">O local especificado deve ser aquele que hospeda suas contas de armazenamento e seu serviço StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="726d0-118">The specified location should be the one that houses your storage accounts and your StorSimple Manager service.</span></span> <span data-ttu-id="726d0-119">Atualmente, há suporte somente para as regiões Oeste dos EUA e Europa Ocidental.</span><span class="sxs-lookup"><span data-stu-id="726d0-119">Currently, only West US and West Europe regions are supported.</span></span> <span data-ttu-id="726d0-120">Portanto, seu serviço StorSimple Manager, o serviço Gerenciador de Dados e a conta de armazenamento devem estar na região com suporte anterior.</span><span class="sxs-lookup"><span data-stu-id="726d0-120">Hence, your StorSimple Manager service, Data Manager service, and the associated storage account should all be in the preceding supported regions.</span></span> <span data-ttu-id="726d0-121">Demora cerca de um minuto para criar o serviço.</span><span class="sxs-lookup"><span data-stu-id="726d0-121">It takes about a minute to create the service.</span></span>

### <a name="create-a-data-transformation-job-definition"></a><span data-ttu-id="726d0-122">Criar uma definição de trabalho de transformação de dados</span><span class="sxs-lookup"><span data-stu-id="726d0-122">Create a data transformation job definition</span></span>

<span data-ttu-id="726d0-123">Em um serviço Gerenciador de Dados do StorSimple, você precisa criar uma definição de trabalho de transformação de dados.</span><span class="sxs-lookup"><span data-stu-id="726d0-123">Within a StorSimple Data Manager service, you need to create a data transformation job definition.</span></span> <span data-ttu-id="726d0-124">Uma definição de trabalho especifica os detalhes dos dados que você está interessado em mudar para uma conta de armazenamento no formato nativo.</span><span class="sxs-lookup"><span data-stu-id="726d0-124">A job definition specifies details of the data that you are interested in moving into a storage account in the native format.</span></span> 

<span data-ttu-id="726d0-125">Execute as seguintes etapas para criar uma nova definição de trabalho de transformação de dados.</span><span class="sxs-lookup"><span data-stu-id="726d0-125">Perform the following steps to create a new data transformation job definition.</span></span>

1.  <span data-ttu-id="726d0-126">Navegue até o serviço que você criou.</span><span class="sxs-lookup"><span data-stu-id="726d0-126">Navigate to the service that you created.</span></span> <span data-ttu-id="726d0-127">Clique em **+ Definição de Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="726d0-127">Click **+ Job Definition**.</span></span>

    ![Clique em +Definição de Trabalho](./media/storsimple-data-manager-ui/click-add-job-definition.png)

2. <span data-ttu-id="726d0-129">A folha da nova definição de trabalho é aberta.</span><span class="sxs-lookup"><span data-stu-id="726d0-129">The new job definition blade opens up.</span></span> <span data-ttu-id="726d0-130">Dê um nome à sua definição de trabalho e clique em **Origem**.</span><span class="sxs-lookup"><span data-stu-id="726d0-130">Give your job definition a name and click **Source**.</span></span> <span data-ttu-id="726d0-131">Na folha **Configurar fonte de dados**, especifique os detalhes do seu dispositivo StorSimple e os dados de interesse.</span><span class="sxs-lookup"><span data-stu-id="726d0-131">In the **Configure data source** blade, specify the details of your StorSimple device and the data of interest.</span></span>

    ![Criar definição de trabalho](./media/storsimple-data-manager-ui//create-new-job-deifnition.png)

3. <span data-ttu-id="726d0-133">Como esse é um novo serviço Gerenciador de Dados, não há nenhum repositório de dados configurado.</span><span class="sxs-lookup"><span data-stu-id="726d0-133">Since this is a new Data Manager service, no data repositories are configured.</span></span> <span data-ttu-id="726d0-134">Para adicionar o StorSimple Manager como um repositório de dados, clique em **Adicionar novo** na lista suspensa do repositório de dados e clique em **Adicionar Repositório de Dados**.</span><span class="sxs-lookup"><span data-stu-id="726d0-134">To add your StorSimple Manager as a data repository, click **Add new** in the data repository dropdown and then click **Add Data Repository**.</span></span>

4. <span data-ttu-id="726d0-135">Escolha **StorSimple série 8000 Manager** como o tipo de repositório e insira as propriedades de seu **StorSimple Manager**.</span><span class="sxs-lookup"><span data-stu-id="726d0-135">Choose **StorSimple 8000 series Manager** as the repository type and enter the properties of your **StorSimple Manager**.</span></span> <span data-ttu-id="726d0-136">Para o campo **Id de Recurso**, você precisa inserir o número antes do **:** na chave do registro do seu gerenciador do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="726d0-136">For the **Resource Id** field, you need to enter the number before the **:** in the registration key of your StorSimple manager.</span></span>

    ![Criar a fonte de dados](./media/storsimple-data-manager-ui/create-new-data-source.png)

5.  <span data-ttu-id="726d0-138">Toque em **OK** quando terminar.</span><span class="sxs-lookup"><span data-stu-id="726d0-138">Click **OK** when done.</span></span> <span data-ttu-id="726d0-139">Isso salva seu repositório de dados e o StorSimple Manager pode ser reutilizado em outras definições de trabalho sem a inserção desses parâmetros novamente.</span><span class="sxs-lookup"><span data-stu-id="726d0-139">This saves your data repository and this StorSimple Manager can be reused in other job definitions without entering these parameters again.</span></span> <span data-ttu-id="726d0-140">Demora alguns segundos depois de clicar em **OK** para que o StorSimple Manager apareça na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="726d0-140">It takes a few seconds after you click **OK** for the StorSimple Manager to show up in the dropdown.</span></span>

6.  <span data-ttu-id="726d0-141">Na folha **Configurar fonte de dados**, insira o nome do dispositivo e o nome do volume que possui os dados de interesse.</span><span class="sxs-lookup"><span data-stu-id="726d0-141">In the **Configure data source** blade, enter the device name and the volume name that has your data of interest.</span></span>

7.  <span data-ttu-id="726d0-142">Na subseção **Filtro**, insira o diretório raiz que contém os dados de interesse (esse campo deve começar com um `\`).</span><span class="sxs-lookup"><span data-stu-id="726d0-142">In the **Filter** subsection, enter the root directory that contains your data of interest (this field should start with a `\`).</span></span> <span data-ttu-id="726d0-143">Você também pode adicionar qualquer filtro de arquivo aqui.</span><span class="sxs-lookup"><span data-stu-id="726d0-143">You can also add any file filters here.</span></span>

8.  <span data-ttu-id="726d0-144">O serviço de transformação de dados funciona nos dados que são passados para o Azure por meio de instantâneos.</span><span class="sxs-lookup"><span data-stu-id="726d0-144">The data transformation service works on the data that is pushed up to the Azure via snapshots.</span></span> <span data-ttu-id="726d0-145">Ao executar esse trabalho, você pode optar por fazer um backup sempre que esse trabalho for executado (para trabalhar em dados mais recentes) ou usar o último backup existente na nuvem (se você estiver trabalhando em alguns dados arquivados).</span><span class="sxs-lookup"><span data-stu-id="726d0-145">When running this job, you can choose to take a backup every time this job is run (to work on latest data) or to use the last existing backup in the cloud (if you are working on some archived data).</span></span>

    ![Novos detalhes da fonte de dados](./media/storsimple-data-manager-ui/new-data-source-details.png)

9. <span data-ttu-id="726d0-147">Em seguida, as configurações de destino precisarão ser configuradas.</span><span class="sxs-lookup"><span data-stu-id="726d0-147">Next, the Target settings need to be configured.</span></span> <span data-ttu-id="726d0-148">Há dois tipos de destinos com suporte – contas do Armazenamento do Azure e dos Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="726d0-148">There are 2 types of supported targets – Azure Storage accounts and Azure Media Services accounts.</span></span> <span data-ttu-id="726d0-149">Escolha contas de armazenamento para colocar arquivos em blobs na conta.</span><span class="sxs-lookup"><span data-stu-id="726d0-149">Choose storage accounts to put files into blobs in that account.</span></span> <span data-ttu-id="726d0-150">Escolha a conta dos serviços de mídia para colocar os arquivos nos ativos dessa conta.</span><span class="sxs-lookup"><span data-stu-id="726d0-150">Choose media services account to put files into assets in that account.</span></span> <span data-ttu-id="726d0-151">Novamente, precisamos adicionar um repositório.</span><span class="sxs-lookup"><span data-stu-id="726d0-151">Again, we need to add a repository.</span></span> <span data-ttu-id="726d0-152">No menu suspenso, selecione **Adicionar novo** e **Definir configurações**.</span><span class="sxs-lookup"><span data-stu-id="726d0-152">In the dropdown, select **Add new** and then **Configure settings**.</span></span>

    ![Criar coletor de dados](./media/storsimple-data-manager-ui/create-new-data-sink.png)

10. <span data-ttu-id="726d0-154">Aqui, você pode selecionar o tipo de repositório que deseja adicionar e os outros parâmetros associados ao repositório.</span><span class="sxs-lookup"><span data-stu-id="726d0-154">Here, you can select the type of repository you want to add and the other parameters associated with the repository.</span></span> <span data-ttu-id="726d0-155">Em ambos os casos, uma fila de armazenamento é criada quando o trabalho é executado.</span><span class="sxs-lookup"><span data-stu-id="726d0-155">In both cases, a storage queue is created when the job runs.</span></span> <span data-ttu-id="726d0-156">Essa fila é populada com mensagens sobre blobs transformados à medida que elas estejam prontas.</span><span class="sxs-lookup"><span data-stu-id="726d0-156">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="726d0-157">O nome dessa fila é igual ao nome da definição do trabalho.</span><span class="sxs-lookup"><span data-stu-id="726d0-157">The name of this queue is the same as the name of the job definition.</span></span> <span data-ttu-id="726d0-158">Se você selecionar **Serviços de Mídia** como o tipo de repositório, também poderá inserir credenciais da conta de armazenamento onde a fila é criada.</span><span class="sxs-lookup"><span data-stu-id="726d0-158">If you select **Media Services** as the repo type, then you can also enter storage account credentials where the queue is created.</span></span>

    ![Novos detalhes do coletor de dados](./media/storsimple-data-manager-ui/new-data-sink-details.png)

11. <span data-ttu-id="726d0-160">Depois de adicionar o repositório de dados (que leva alguns segundos), você encontrará o repositório na lista suspensa no **Nome da conta de destino**.</span><span class="sxs-lookup"><span data-stu-id="726d0-160">After adding the data repository (which takes a few seconds), you will find the repo in the dropdown in the **Target account name**.</span></span>  <span data-ttu-id="726d0-161">Escolha o destino de que você precisa.</span><span class="sxs-lookup"><span data-stu-id="726d0-161">Choose the target that you need.</span></span>

12. <span data-ttu-id="726d0-162">Clique em **OK** para criar a definição de trabalho.</span><span class="sxs-lookup"><span data-stu-id="726d0-162">Click **OK** to create the job definition.</span></span> <span data-ttu-id="726d0-163">A definição de trabalho está configurada.</span><span class="sxs-lookup"><span data-stu-id="726d0-163">Your job definition is now set up.</span></span> <span data-ttu-id="726d0-164">Você pode usar essa definição de trabalho várias vezes por meio da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="726d0-164">You can use this job definition multiple times via the UI.</span></span>

    ![Adicionar nova definição de trabalho](./media/storsimple-data-manager-ui/add-new-job-definition.png)

### <a name="run-the-job-definition"></a><span data-ttu-id="726d0-166">Executar definição de trabalho</span><span class="sxs-lookup"><span data-stu-id="726d0-166">Run the job definition</span></span>

<span data-ttu-id="726d0-167">Sempre que você precisar mover dados do StorSimple para a conta de armazenamento especificada na definição de trabalho, será necessário invocá-los.</span><span class="sxs-lookup"><span data-stu-id="726d0-167">Whenever you need to move data from StorSimple to the storage account that you have specified in the job definition, you will need to invoke it.</span></span> <span data-ttu-id="726d0-168">Há alguma flexibilidade na alteração dos parâmetros sempre que você invoca o trabalho.</span><span class="sxs-lookup"><span data-stu-id="726d0-168">There is some flexibility in changing the parameters every time you invoke the job.</span></span> <span data-ttu-id="726d0-169">As etapas são as seguintes:</span><span class="sxs-lookup"><span data-stu-id="726d0-169">The steps are as follows:</span></span>

1. <span data-ttu-id="726d0-170">Selecione o serviço Gerenciador de Dados do StorSimple e vá para **Monitoramento**.</span><span class="sxs-lookup"><span data-stu-id="726d0-170">Select your StorSimple Data Manager service and go to **Monitoring**.</span></span> <span data-ttu-id="726d0-171">Clique em **Executar Agora**.</span><span class="sxs-lookup"><span data-stu-id="726d0-171">Click **Run Now**.</span></span>

    ![Definição de trabalho de gatilho](./media/storsimple-data-manager-ui/run-now.png)

2. <span data-ttu-id="726d0-173">Escolha a definição de trabalho que você deseja executar.</span><span class="sxs-lookup"><span data-stu-id="726d0-173">Choose the job definition that you want to run.</span></span> <span data-ttu-id="726d0-174">Clique em **Configurações de execução** para modificar as configurações que você talvez queira alterar para esta execução do trabalho.</span><span class="sxs-lookup"><span data-stu-id="726d0-174">Click **Run settings** to modify any settings that you might want to change for this job run.</span></span>

    ![Executar configurações do trabalho](./media/storsimple-data-manager-ui/run-settings.png)

3. <span data-ttu-id="726d0-176">Clique em **OK** e, em seguida, clique em **Executar** para iniciar seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="726d0-176">Click **OK** and then click **Run** to launch your job.</span></span> <span data-ttu-id="726d0-177">Para monitorar esse trabalho, vá para a página **Trabalhos** em seu Gerenciador de Dados do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="726d0-177">To monitor this job, go to the **Jobs** page in your StorSimple Data Manager.</span></span>

    ![Status e a lista de trabalhos](./media/storsimple-data-manager-ui/jobs-list-and-status.png)

4. <span data-ttu-id="726d0-179">Além do monitoramento na folha **Trabalhos**, você também pode escutar a fila de armazenamento para onde uma mensagem é adicionada toda vez que um arquivo é movido do StorSimple para a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="726d0-179">In addition to monitoring in the **Jobs** blade, you can also listen on the storage queue where a message is added every time a file is moved from StorSimple to the storage account.</span></span>


## <a name="next-steps"></a><span data-ttu-id="726d0-180">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="726d0-180">Next steps</span></span>

<span data-ttu-id="726d0-181">[Usar o SDK do .NET para iniciar trabalhos do Gerenciador de Dados do StorSimple](storsimple-data-manager-dotnet-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="726d0-181">[Use .NET SDK to launch StorSimple Data Manager jobs](storsimple-data-manager-dotnet-jobs.md).</span></span>