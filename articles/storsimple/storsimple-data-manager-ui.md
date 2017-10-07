---
title: aaaMicrosoft Azure StorSimple Data Manager UI | Microsoft Docs
description: "Descreve como toouse serviço StorSimple Manager de dados da interface do usuário (visualização particular)"
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
ms.openlocfilehash: b0ee12b3e495400b54e48eb1a98c68b1af2e5f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-using-hello-storsimple-data-manager-service-ui-private-preview"></a><span data-ttu-id="370bf-103">Gerenciar usando o serviço de Gerenciador de dados StorSimple Olá da interface do usuário (visualização particular)</span><span class="sxs-lookup"><span data-stu-id="370bf-103">Manage using hello StorSimple Data Manager service UI (Private Preview)</span></span>

<span data-ttu-id="370bf-104">Este artigo explica como você pode usar o hello transformação de dados do Gerenciador de dados StorSimple UI tooperform nos dados que residem em dispositivos da série StorSimple 8000 hello.</span><span class="sxs-lookup"><span data-stu-id="370bf-104">This article explains how you can use hello StorSimple Data Manager UI tooperform data transformation on data residing on hello StorSimple 8000 series devices.</span></span> <span data-ttu-id="370bf-105">Olá dados transformados podem ser consumidos por outros serviços do Azure, como os serviços de mídia do Azure, HDInsight do Azure, aprendizado de máquina do Azure e pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="370bf-105">hello transformed data can then be consumed by other Azure services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search.</span></span> 


## <a name="use-storsimple-data-transformation"></a><span data-ttu-id="370bf-106">Usar a transformação de dados do StorSimple</span><span class="sxs-lookup"><span data-stu-id="370bf-106">Use StorSimple Data Transformation</span></span>

<span data-ttu-id="370bf-107">Olá StorSimple Data Manager é o recurso de saudação dentro do qual a transformação de dados pode ser instanciada.</span><span class="sxs-lookup"><span data-stu-id="370bf-107">hello StorSimple Data Manager is hello resource within which Data Transformation can be instantiated.</span></span> <span data-ttu-id="370bf-108">Olá Data Transformation Services permite mover dados de sua tooblobs de dispositivo StorSimple local no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="370bf-108">hello Data Transformation service lets you move data from your StorSimple on-premises device tooblobs in Azure storage.</span></span> <span data-ttu-id="370bf-109">Portanto, no fluxo de trabalho precisar toospecify Olá detalhes sobre os dados de dispositivo e hello StorSimple de interesse que deseja que a conta de armazenamento do toomove toohello.</span><span class="sxs-lookup"><span data-stu-id="370bf-109">Hence, in workflow you need toospecify hello details about your StorSimple device and hello data of interest that you want toomove toohello storage account.</span></span>

### <a name="create-a-storsimple-data-manager-service"></a><span data-ttu-id="370bf-110">Criar um serviço Gerenciador de Dados do StorSimple</span><span class="sxs-lookup"><span data-stu-id="370bf-110">Create a StorSimple Data Manager service</span></span>

<span data-ttu-id="370bf-111">Execute Olá etapas toocreate um serviço StorSimple Manager de dados a seguir.</span><span class="sxs-lookup"><span data-stu-id="370bf-111">Perform hello following steps toocreate a StorSimple Data Manager service.</span></span>

1. <span data-ttu-id="370bf-112">toocreate um serviço StorSimple Manager de dados, vá muito[https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)</span><span class="sxs-lookup"><span data-stu-id="370bf-112">toocreate a StorSimple Data Manager service, go too[https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)</span></span>

2. <span data-ttu-id="370bf-113">Clique em Olá  **+**  ícone e pesquisa para o Gerenciador de dados do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="370bf-113">Click hello **+** icon and search for StorSimple Data Manager.</span></span> <span data-ttu-id="370bf-114">Clique em seu serviço Gerenciador de Dados do StorSimple e então clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="370bf-114">Click your StorSimple Data Manager service and then click **Create**.</span></span>

3. <span data-ttu-id="370bf-115">Se sua assinatura está habilitada para a criação desse serviço, você verá Olá folha a seguir.</span><span class="sxs-lookup"><span data-stu-id="370bf-115">If your subscription is enabled for creating this service, you see hello following blade.</span></span>

    ![Criar um recurso Gerenciadores de Dados do StorSimple](./media/storsimple-data-manager-ui/create-new-data-manager-service.png)

4. <span data-ttu-id="370bf-117">Insira entradas hello e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="370bf-117">Enter hello inputs and click **Create**.</span></span> <span data-ttu-id="370bf-118">Olá especificado local deve ser Olá que hospeda suas contas de armazenamento e o serviço StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="370bf-118">hello specified location should be hello one that houses your storage accounts and your StorSimple Manager service.</span></span> <span data-ttu-id="370bf-119">Atualmente, há suporte somente para as regiões Oeste dos EUA e Europa Ocidental.</span><span class="sxs-lookup"><span data-stu-id="370bf-119">Currently, only West US and West Europe regions are supported.</span></span> <span data-ttu-id="370bf-120">Portanto, seu serviço StorSimple Manager, o serviço de Gerenciador de dados e a saudação conta de armazenamento associada deve ser em regiões de saudação anterior com suporte.</span><span class="sxs-lookup"><span data-stu-id="370bf-120">Hence, your StorSimple Manager service, Data Manager service, and hello associated storage account should all be in hello preceding supported regions.</span></span> <span data-ttu-id="370bf-121">Demora cerca de um serviço de saudação toocreate minutos.</span><span class="sxs-lookup"><span data-stu-id="370bf-121">It takes about a minute toocreate hello service.</span></span>

### <a name="create-a-data-transformation-job-definition"></a><span data-ttu-id="370bf-122">Criar uma definição de trabalho de transformação de dados</span><span class="sxs-lookup"><span data-stu-id="370bf-122">Create a data transformation job definition</span></span>

<span data-ttu-id="370bf-123">Em um serviço de Gerenciador de dados de StorSimple, você precisa toocreate uma definição de trabalho de transformação de dados.</span><span class="sxs-lookup"><span data-stu-id="370bf-123">Within a StorSimple Data Manager service, you need toocreate a data transformation job definition.</span></span> <span data-ttu-id="370bf-124">Uma definição de trabalho Especifica detalhes dos dados de saudação que você está interessado em movimentação em uma conta de armazenamento em formato nativo hello.</span><span class="sxs-lookup"><span data-stu-id="370bf-124">A job definition specifies details of hello data that you are interested in moving into a storage account in hello native format.</span></span> 

<span data-ttu-id="370bf-125">Execute Olá seguindo as etapas toocreate uma nova definição de trabalho de transformação de dados.</span><span class="sxs-lookup"><span data-stu-id="370bf-125">Perform hello following steps toocreate a new data transformation job definition.</span></span>

1.  <span data-ttu-id="370bf-126">Navegue serviço toohello que você criou.</span><span class="sxs-lookup"><span data-stu-id="370bf-126">Navigate toohello service that you created.</span></span> <span data-ttu-id="370bf-127">Clique em **+ Definição de Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="370bf-127">Click **+ Job Definition**.</span></span>

    ![Clique em +Definição de Trabalho](./media/storsimple-data-manager-ui/click-add-job-definition.png)

2. <span data-ttu-id="370bf-129">nova folha de definição de trabalho Olá abre.</span><span class="sxs-lookup"><span data-stu-id="370bf-129">hello new job definition blade opens up.</span></span> <span data-ttu-id="370bf-130">Dê um nome à sua definição de trabalho e clique em **Origem**.</span><span class="sxs-lookup"><span data-stu-id="370bf-130">Give your job definition a name and click **Source**.</span></span> <span data-ttu-id="370bf-131">Em Olá **configurar fonte de dados** folha, especifique os detalhes de saudação do seu dispositivo StorSimple e Olá dados de interesse.</span><span class="sxs-lookup"><span data-stu-id="370bf-131">In hello **Configure data source** blade, specify hello details of your StorSimple device and hello data of interest.</span></span>

    ![Criar definição de trabalho](./media/storsimple-data-manager-ui//create-new-job-deifnition.png)

3. <span data-ttu-id="370bf-133">Como esse é um novo serviço Gerenciador de Dados, não há nenhum repositório de dados configurado.</span><span class="sxs-lookup"><span data-stu-id="370bf-133">Since this is a new Data Manager service, no data repositories are configured.</span></span> <span data-ttu-id="370bf-134">tooadd seu StorSimple Manager como um repositório de dados, clique em **adicionar novo** em Olá suspensa de repositório de dados e, em seguida, clique em **Adicionar repositório de dados**.</span><span class="sxs-lookup"><span data-stu-id="370bf-134">tooadd your StorSimple Manager as a data repository, click **Add new** in hello data repository dropdown and then click **Add Data Repository**.</span></span>

4. <span data-ttu-id="370bf-135">Escolha **StorSimple série 8000 Manager** como repositório de saudação tipo e insira as propriedades de saudação do seu **StorSimple Manager**.</span><span class="sxs-lookup"><span data-stu-id="370bf-135">Choose **StorSimple 8000 series Manager** as hello repository type and enter hello properties of your **StorSimple Manager**.</span></span> <span data-ttu-id="370bf-136">Para Olá **Id de recurso** campo, você precisa tooenter Olá número antes Olá **:** na chave de registro de saudação do seu StorSimple manager.</span><span class="sxs-lookup"><span data-stu-id="370bf-136">For hello **Resource Id** field, you need tooenter hello number before hello **:** in hello registration key of your StorSimple manager.</span></span>

    ![Criar a fonte de dados](./media/storsimple-data-manager-ui/create-new-data-source.png)

5.  <span data-ttu-id="370bf-138">Toque em **OK** quando terminar.</span><span class="sxs-lookup"><span data-stu-id="370bf-138">Click **OK** when done.</span></span> <span data-ttu-id="370bf-139">Isso salva seu repositório de dados e o StorSimple Manager pode ser reutilizado em outras definições de trabalho sem a inserção desses parâmetros novamente.</span><span class="sxs-lookup"><span data-stu-id="370bf-139">This saves your data repository and this StorSimple Manager can be reused in other job definitions without entering these parameters again.</span></span> <span data-ttu-id="370bf-140">Levará alguns segundos depois de clicar em **Okey** para Olá tooshow StorSimple Manager para cima na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="370bf-140">It takes a few seconds after you click **OK** for hello StorSimple Manager tooshow up in hello dropdown.</span></span>

6.  <span data-ttu-id="370bf-141">Em Olá **configurar fonte de dados** folha, insira o nome do dispositivo hello e Olá nome do volume que tenha seus dados de interesse.</span><span class="sxs-lookup"><span data-stu-id="370bf-141">In hello **Configure data source** blade, enter hello device name and hello volume name that has your data of interest.</span></span>

7.  <span data-ttu-id="370bf-142">Em Olá **filtro** subseção, insira o diretório raiz de saudação que contém os dados de interesse (este campo deve começar com um `\`).</span><span class="sxs-lookup"><span data-stu-id="370bf-142">In hello **Filter** subsection, enter hello root directory that contains your data of interest (this field should start with a `\`).</span></span> <span data-ttu-id="370bf-143">Você também pode adicionar qualquer filtro de arquivo aqui.</span><span class="sxs-lookup"><span data-stu-id="370bf-143">You can also add any file filters here.</span></span>

8.  <span data-ttu-id="370bf-144">serviço de transformação de dados Olá funciona em dados de saudação toohello do Azure são passados por meio de instantâneos.</span><span class="sxs-lookup"><span data-stu-id="370bf-144">hello data transformation service works on hello data that is pushed up toohello Azure via snapshots.</span></span> <span data-ttu-id="370bf-145">Ao executar este trabalho, você pode escolher tootake um backup sempre que esse trabalho é executado (toowork nos dados mais recentes) ou toouse Olá último backup existente na nuvem hello (se você estiver trabalhando em alguns dados arquivados).</span><span class="sxs-lookup"><span data-stu-id="370bf-145">When running this job, you can choose tootake a backup every time this job is run (toowork on latest data) or toouse hello last existing backup in hello cloud (if you are working on some archived data).</span></span>

    ![Novos detalhes da fonte de dados](./media/storsimple-data-manager-ui/new-data-source-details.png)

9. <span data-ttu-id="370bf-147">Em seguida, as configurações de destino Olá necessário toobe configurado.</span><span class="sxs-lookup"><span data-stu-id="370bf-147">Next, hello Target settings need toobe configured.</span></span> <span data-ttu-id="370bf-148">Há dois tipos de destinos com suporte – contas do Armazenamento do Azure e dos Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="370bf-148">There are 2 types of supported targets – Azure Storage accounts and Azure Media Services accounts.</span></span> <span data-ttu-id="370bf-149">Escolha contas de armazenamento tooput arquivos em blobs na conta.</span><span class="sxs-lookup"><span data-stu-id="370bf-149">Choose storage accounts tooput files into blobs in that account.</span></span> <span data-ttu-id="370bf-150">Escolha a conta do media services tooput arquivos em recursos nessa conta.</span><span class="sxs-lookup"><span data-stu-id="370bf-150">Choose media services account tooput files into assets in that account.</span></span> <span data-ttu-id="370bf-151">Novamente, é preciso tooadd um repositório.</span><span class="sxs-lookup"><span data-stu-id="370bf-151">Again, we need tooadd a repository.</span></span> <span data-ttu-id="370bf-152">No menu suspenso hello, selecione **adicionar novo** e **configurar**.</span><span class="sxs-lookup"><span data-stu-id="370bf-152">In hello dropdown, select **Add new** and then **Configure settings**.</span></span>

    ![Criar coletor de dados](./media/storsimple-data-manager-ui/create-new-data-sink.png)

10. <span data-ttu-id="370bf-154">Aqui, você pode selecionar o tipo de saudação do repositório que você deseja tooadd e hello outros parâmetros associados a repositório hello.</span><span class="sxs-lookup"><span data-stu-id="370bf-154">Here, you can select hello type of repository you want tooadd and hello other parameters associated with hello repository.</span></span> <span data-ttu-id="370bf-155">Em ambos os casos, uma fila de armazenamento é criada quando Olá trabalho é executado.</span><span class="sxs-lookup"><span data-stu-id="370bf-155">In both cases, a storage queue is created when hello job runs.</span></span> <span data-ttu-id="370bf-156">Essa fila é populada com mensagens sobre blobs transformados à medida que elas estejam prontas.</span><span class="sxs-lookup"><span data-stu-id="370bf-156">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="370bf-157">nome da saudação dessa fila é Olá igual ao nome de Olá Olá da definição do trabalho.</span><span class="sxs-lookup"><span data-stu-id="370bf-157">hello name of this queue is hello same as hello name of hello job definition.</span></span> <span data-ttu-id="370bf-158">Se você selecionar **os serviços de mídia** como tipo de repositório Olá, em seguida, você também pode inserir credenciais da conta de armazenamento em que a fila de saudação é criada.</span><span class="sxs-lookup"><span data-stu-id="370bf-158">If you select **Media Services** as hello repo type, then you can also enter storage account credentials where hello queue is created.</span></span>

    ![Novos detalhes do coletor de dados](./media/storsimple-data-manager-ui/new-data-sink-details.png)

11. <span data-ttu-id="370bf-160">Depois de adicionar um repositório de dados de saudação (o que levará alguns segundos), você encontrará o repositório Olá na lista suspensa de saudação em Olá **nome da conta de destino**.</span><span class="sxs-lookup"><span data-stu-id="370bf-160">After adding hello data repository (which takes a few seconds), you will find hello repo in hello dropdown in hello **Target account name**.</span></span>  <span data-ttu-id="370bf-161">Escolha o destino de saudação que você precisa.</span><span class="sxs-lookup"><span data-stu-id="370bf-161">Choose hello target that you need.</span></span>

12. <span data-ttu-id="370bf-162">Clique em **Okey** toocreate definição de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="370bf-162">Click **OK** toocreate hello job definition.</span></span> <span data-ttu-id="370bf-163">A definição de trabalho está configurada.</span><span class="sxs-lookup"><span data-stu-id="370bf-163">Your job definition is now set up.</span></span> <span data-ttu-id="370bf-164">Você pode usar esta definição de trabalho várias vezes por meio de saudação da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="370bf-164">You can use this job definition multiple times via hello UI.</span></span>

    ![Adicionar nova definição de trabalho](./media/storsimple-data-manager-ui/add-new-job-definition.png)

### <a name="run-hello-job-definition"></a><span data-ttu-id="370bf-166">Executar definição de trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="370bf-166">Run hello job definition</span></span>

<span data-ttu-id="370bf-167">Sempre que você precisar toomove dados da conta de armazenamento do StorSimple toohello especificado na definição de trabalho hello, será necessário tooinvoke-lo.</span><span class="sxs-lookup"><span data-stu-id="370bf-167">Whenever you need toomove data from StorSimple toohello storage account that you have specified in hello job definition, you will need tooinvoke it.</span></span> <span data-ttu-id="370bf-168">Há alguma flexibilidade na alterando os parâmetros de saudação toda vez que você chama trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="370bf-168">There is some flexibility in changing hello parameters every time you invoke hello job.</span></span> <span data-ttu-id="370bf-169">etapas de saudação são da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="370bf-169">hello steps are as follows:</span></span>

1. <span data-ttu-id="370bf-170">Selecione o serviço StorSimple Manager de dados e vá muito**monitoramento**.</span><span class="sxs-lookup"><span data-stu-id="370bf-170">Select your StorSimple Data Manager service and go too**Monitoring**.</span></span> <span data-ttu-id="370bf-171">Clique em **Executar Agora**.</span><span class="sxs-lookup"><span data-stu-id="370bf-171">Click **Run Now**.</span></span>

    ![Definição de trabalho de gatilho](./media/storsimple-data-manager-ui/run-now.png)

2. <span data-ttu-id="370bf-173">Escolha a definição de trabalho Olá que você deseja toorun.</span><span class="sxs-lookup"><span data-stu-id="370bf-173">Choose hello job definition that you want toorun.</span></span> <span data-ttu-id="370bf-174">Clique em **as configurações de execução** toomodify todas as configurações que você poderá toochange para esta execução do trabalho.</span><span class="sxs-lookup"><span data-stu-id="370bf-174">Click **Run settings** toomodify any settings that you might want toochange for this job run.</span></span>

    ![Executar configurações do trabalho](./media/storsimple-data-manager-ui/run-settings.png)

3. <span data-ttu-id="370bf-176">Clique em **Okey** e, em seguida, clique em **executar** toolaunch seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="370bf-176">Click **OK** and then click **Run** toolaunch your job.</span></span> <span data-ttu-id="370bf-177">toomonitor esse trabalho, vá toohello **trabalhos** página no Gerenciador de dados de seu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="370bf-177">toomonitor this job, go toohello **Jobs** page in your StorSimple Data Manager.</span></span>

    ![Status e a lista de trabalhos](./media/storsimple-data-manager-ui/jobs-list-and-status.png)

4. <span data-ttu-id="370bf-179">Em adição toomonitoring em Olá **trabalhos** folha, você também pode ouvir na fila de armazenamento de saudação em que uma mensagem é adicionada toda vez que um arquivo é movido da conta de armazenamento do StorSimple toohello.</span><span class="sxs-lookup"><span data-stu-id="370bf-179">In addition toomonitoring in hello **Jobs** blade, you can also listen on hello storage queue where a message is added every time a file is moved from StorSimple toohello storage account.</span></span>


## <a name="next-steps"></a><span data-ttu-id="370bf-180">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="370bf-180">Next steps</span></span>

<span data-ttu-id="370bf-181">[Usar trabalhos do SDK do .NET toolaunch StorSimple Data Manager](storsimple-data-manager-dotnet-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="370bf-181">[Use .NET SDK toolaunch StorSimple Data Manager jobs](storsimple-data-manager-dotnet-jobs.md).</span></span>
