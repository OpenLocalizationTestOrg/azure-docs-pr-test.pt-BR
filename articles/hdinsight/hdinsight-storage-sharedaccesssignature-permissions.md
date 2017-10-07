---
title: acesso de aaaRestrict usando assinaturas de acesso compartilhado - HDInsight do Azure | Microsoft Docs
description: Saiba como toouse assinaturas de acesso compartilhado toorestrict HDInsight acessar toodata armazenado em blobs de armazenamento do Azure.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 7bcad2dd-edea-467c-9130-44cffc005ff3
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: a34a2f8e52e47a15b09f09bc1fc67fc6159ec75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-shared-access-signatures-toorestrict-access-toodata-in-hdinsight"></a><span data-ttu-id="2dec6-103">Usar assinaturas de acesso compartilhado do Azure Storage toorestrict acesso toodata no HDInsight</span><span class="sxs-lookup"><span data-stu-id="2dec6-103">Use Azure Storage Shared Access Signatures toorestrict access toodata in HDInsight</span></span>

<span data-ttu-id="2dec6-104">HDInsight tem acesso completo toodata nas contas de armazenamento do Azure Olá associadas Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="2dec6-104">HDInsight has full access toodata in hello Azure Storage accounts associated with hello cluster.</span></span> <span data-ttu-id="2dec6-105">Você pode usar assinaturas de acesso compartilhado em dados de toohello Olá blob contêiner toorestrict acesso.</span><span class="sxs-lookup"><span data-stu-id="2dec6-105">You can use Shared Access Signatures on hello blob container toorestrict access toohello data.</span></span> <span data-ttu-id="2dec6-106">Por exemplo, tooprovide acesso somente leitura toohello dados.</span><span class="sxs-lookup"><span data-stu-id="2dec6-106">For example, tooprovide read-only access toohello data.</span></span> <span data-ttu-id="2dec6-107">Assinaturas de acesso compartilhado (SAS) são um recurso de contas de armazenamento do Azure que permite que você toolimit toodata de acesso.</span><span class="sxs-lookup"><span data-stu-id="2dec6-107">Shared Access Signatures (SAS) are a feature of Azure storage accounts that allows you toolimit access toodata.</span></span> <span data-ttu-id="2dec6-108">Por exemplo, fornecendo acesso somente leitura toodata.</span><span class="sxs-lookup"><span data-stu-id="2dec6-108">For example, providing read-only access toodata.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2dec6-109">Para uma solução que usa o Apache Ranger, considere usar HDInsight ingressado em domínio.</span><span class="sxs-lookup"><span data-stu-id="2dec6-109">For a solution using Apache Ranger, consider using domain-joined HDInsight.</span></span> <span data-ttu-id="2dec6-110">Para obter mais informações, consulte Olá [configurar domínio HDInsight](hdinsight-domain-joined-configure.md) documento.</span><span class="sxs-lookup"><span data-stu-id="2dec6-110">For more information, see hello [Configure domain-joined HDInsight](hdinsight-domain-joined-configure.md) document.</span></span>

> [!WARNING]
> <span data-ttu-id="2dec6-111">HDInsight deve ter acesso completo toohello padrão armazenamento Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="2dec6-111">HDInsight must have full access toohello default storage for hello cluster.</span></span>

## <a name="requirements"></a><span data-ttu-id="2dec6-112">Requisitos</span><span class="sxs-lookup"><span data-stu-id="2dec6-112">Requirements</span></span>

* <span data-ttu-id="2dec6-113">Uma assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="2dec6-113">An Azure subscription</span></span>
* <span data-ttu-id="2dec6-114">C# ou Python.</span><span class="sxs-lookup"><span data-stu-id="2dec6-114">C# or Python.</span></span> <span data-ttu-id="2dec6-115">O código de exemplo do C# é fornecido como uma solução do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2dec6-115">C# example code is provided as a Visual Studio solution.</span></span>

  * <span data-ttu-id="2dec6-116">A versão do Visual Studio deve ser a 2013, 2015 ou 2017</span><span class="sxs-lookup"><span data-stu-id="2dec6-116">Visual Studio must be version 2013, 2015, or 2017</span></span>
  * <span data-ttu-id="2dec6-117">A versão do Python deverá ser a 2.7 ou superior</span><span class="sxs-lookup"><span data-stu-id="2dec6-117">Python must be version 2.7 or higher</span></span>

* <span data-ttu-id="2dec6-118">Um cluster HDInsight baseados em Linux ou [Azure PowerShell] [ powershell] -se você tiver um cluster existente com base em Linux, você pode usar o Ambari tooadd um cluster de toohello de assinatura de acesso compartilhado.</span><span class="sxs-lookup"><span data-stu-id="2dec6-118">A Linux-based HDInsight cluster OR [Azure PowerShell][powershell] - If you have an existing Linux-based cluster, you can use Ambari tooadd a Shared Access Signature toohello cluster.</span></span> <span data-ttu-id="2dec6-119">Caso contrário, você pode usar o Azure PowerShell toocreate um cluster e adicionar uma assinatura de acesso compartilhado durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="2dec6-119">If not, you can use Azure PowerShell toocreate a cluster and add a Shared Access Signature during cluster creation.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="2dec6-120">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="2dec6-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2dec6-121">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="2dec6-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="2dec6-122">Olá arquivos de exemplo do [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span><span class="sxs-lookup"><span data-stu-id="2dec6-122">hello example files from [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span></span> <span data-ttu-id="2dec6-123">Esse repositório contém Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="2dec6-123">This repository contains hello following items:</span></span>

  * <span data-ttu-id="2dec6-124">Um projeto do Visual Studio que pode criar um contêiner de armazenamento, a política armazenada e a SAS a ser usada com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="2dec6-124">A Visual Studio project that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="2dec6-125">Um script Python que pode criar um contêiner de armazenamento, a política armazenada e a SAS a ser usada com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="2dec6-125">A Python script that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="2dec6-126">Um script do PowerShell que pode criar um HDInsight de cluster e configurá-lo toouse Olá SAS.</span><span class="sxs-lookup"><span data-stu-id="2dec6-126">A PowerShell script that can create a HDInsight cluster and configure it toouse hello SAS.</span></span>

## <a name="shared-access-signatures"></a><span data-ttu-id="2dec6-127">As Assinaturas de Acesso Compartilhado</span><span class="sxs-lookup"><span data-stu-id="2dec6-127">Shared Access Signatures</span></span>

<span data-ttu-id="2dec6-128">Há duas formas de Assinaturas de Acesso Compartilhado:</span><span class="sxs-lookup"><span data-stu-id="2dec6-128">There are two forms of Shared Access Signatures:</span></span>

* <span data-ttu-id="2dec6-129">Ad hoc: Olá hora de início, hora de expiração e as permissões para Olá SAS são especificados no URI SAS de saudação.</span><span class="sxs-lookup"><span data-stu-id="2dec6-129">Ad hoc: hello start time, expiry time, and permissions for hello SAS are all specified on hello SAS URI.</span></span>

* <span data-ttu-id="2dec6-130">Política de acesso armazenada: uma política de acesso armazenada é definida em um contêiner de recurso, como um contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="2dec6-130">Stored access policy: A stored access policy is defined on a resource container, such as a blob container.</span></span> <span data-ttu-id="2dec6-131">Uma política pode ser usado toomanage restrições para uma ou mais assinaturas de acesso compartilhado.</span><span class="sxs-lookup"><span data-stu-id="2dec6-131">A policy can be used toomanage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="2dec6-132">Quando você associa uma SAS com uma política de acesso armazenada, Olá SAS herda restrições Olá - Olá hora de início, hora de expiração e permissões - definidas para a política de acesso Olá armazenado.</span><span class="sxs-lookup"><span data-stu-id="2dec6-132">When you associate a SAS with a stored access policy, hello SAS inherits hello constraints - hello start time, expiry time, and permissions - defined for hello stored access policy.</span></span>

<span data-ttu-id="2dec6-133">Olá diferença entre formulários Olá dois é importante para um cenário de chave: revogação.</span><span class="sxs-lookup"><span data-stu-id="2dec6-133">hello difference between hello two forms is important for one key scenario: revocation.</span></span> <span data-ttu-id="2dec6-134">Uma SAS é uma URL, portanto qualquer pessoa que obtém Olá SAS pode usá-lo, independentemente de quem solicitou toobegin com.</span><span class="sxs-lookup"><span data-stu-id="2dec6-134">A SAS is a URL, so anyone who obtains hello SAS can use it, regardless of who requested it toobegin with.</span></span> <span data-ttu-id="2dec6-135">Se uma SAS é publicada publicamente, ele pode ser usado por qualquer pessoa no Olá, mundo.</span><span class="sxs-lookup"><span data-stu-id="2dec6-135">If a SAS is published publicly, it can be used by anyone in hello world.</span></span> <span data-ttu-id="2dec6-136">Uma SAS distribuída será válida até que ocorra um destes quatro fatores:</span><span class="sxs-lookup"><span data-stu-id="2dec6-136">A SAS that is distributed is valid until one of four things happens:</span></span>

1. <span data-ttu-id="2dec6-137">tempo de expiração de saudação especificado em Olá que SAS é atingido.</span><span class="sxs-lookup"><span data-stu-id="2dec6-137">hello expiry time specified on hello SAS is reached.</span></span>

2. <span data-ttu-id="2dec6-138">tempo de expiração de saudação especificado na política de acesso Olá armazenado referenciada por Olá que SAS é atingido.</span><span class="sxs-lookup"><span data-stu-id="2dec6-138">hello expiry time specified on hello stored access policy referenced by hello SAS is reached.</span></span> <span data-ttu-id="2dec6-139">cenários a seguir Hello causam um tempo de expiração Olá toobe atingido:</span><span class="sxs-lookup"><span data-stu-id="2dec6-139">hello following scenarios cause hello expiry time toobe reached:</span></span>

    * <span data-ttu-id="2dec6-140">intervalo de tempo de saudação expirou.</span><span class="sxs-lookup"><span data-stu-id="2dec6-140">hello time interval has elapsed.</span></span>
    * <span data-ttu-id="2dec6-141">política de acesso de saudação armazenada é modificado toohave um tempo de expiração em Olá anterior.</span><span class="sxs-lookup"><span data-stu-id="2dec6-141">hello stored access policy is modified toohave an expiry time in hello past.</span></span> <span data-ttu-id="2dec6-142">Alterar o tempo de expiração de saudação é uma maneira toorevoke Olá SAS.</span><span class="sxs-lookup"><span data-stu-id="2dec6-142">Changing hello expiry time is one way toorevoke hello SAS.</span></span>

3. <span data-ttu-id="2dec6-143">Olá armazenado referenciada por Olá que SAS é excluído, que é Olá toorevoke de outra maneira SAS de política de acesso.</span><span class="sxs-lookup"><span data-stu-id="2dec6-143">hello stored access policy referenced by hello SAS is deleted, which is another way toorevoke hello SAS.</span></span> <span data-ttu-id="2dec6-144">Se você recriar a política de acesso de saudação armazenada com hello mesmo nome, todos os tokens SAS para diretiva anterior Olá são válidas (se o tempo de expiração saudação em Olá SAS não passou).</span><span class="sxs-lookup"><span data-stu-id="2dec6-144">If you recreate hello stored access policy with hello same name, all  SAS tokens for hello previous policy are valid (if hello expiry time on hello SAS has not passed).</span></span> <span data-ttu-id="2dec6-145">Se você pretende toorevoke Olá SAS, ser toouse se um nome diferente se você recriar a política de acesso de saudação com um tempo de expiração em Olá futuras.</span><span class="sxs-lookup"><span data-stu-id="2dec6-145">If you intend toorevoke hello SAS, be sure toouse a different name if you recreate hello access policy with an expiry time in hello future.</span></span>

4. <span data-ttu-id="2dec6-146">Olá a chave de conta que foi usado toocreate Olá SAS é regenerada.</span><span class="sxs-lookup"><span data-stu-id="2dec6-146">hello account key that was used toocreate hello SAS is regenerated.</span></span> <span data-ttu-id="2dec6-147">Regenerando chave Olá faz com que todos os aplicativos que usam a autenticação de chave toofail anterior hello.</span><span class="sxs-lookup"><span data-stu-id="2dec6-147">Regenerating hello key causes all applications that use hello previous key toofail authentication.</span></span> <span data-ttu-id="2dec6-148">Atualize todos os componentes toohello nova chave.</span><span class="sxs-lookup"><span data-stu-id="2dec6-148">Update all components toohello new key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2dec6-149">Um URI de assinatura de acesso compartilhado é associado à assinatura de Olá Olá conta chave toocreate usado e Olá associados a política de acesso armazenada (se houver).</span><span class="sxs-lookup"><span data-stu-id="2dec6-149">A shared access signature URI is associated with hello account key used toocreate hello signature, and hello associated stored access policy (if any).</span></span> <span data-ttu-id="2dec6-150">Se nenhuma política de acesso armazenada for especificada, hello toorevoke de maneira somente uma assinatura de acesso compartilhado é toochange Olá conta chave.</span><span class="sxs-lookup"><span data-stu-id="2dec6-150">If no stored access policy is specified, hello only way toorevoke a shared access signature is toochange hello account key.</span></span>

<span data-ttu-id="2dec6-151">É recomendável sempre usar políticas de acesso armazenadas.</span><span class="sxs-lookup"><span data-stu-id="2dec6-151">We recommend that you always use stored access policies.</span></span> <span data-ttu-id="2dec6-152">Ao usar as diretivas armazenadas, você pode revogar assinaturas ou estender a data de expiração de saudação conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="2dec6-152">When using stored policies, you can either revoke signatures or extend hello expiry date as needed.</span></span> <span data-ttu-id="2dec6-153">Olá etapas deste documento usam políticas de acesso armazenada toogenerate SAS.</span><span class="sxs-lookup"><span data-stu-id="2dec6-153">hello steps in this document use stored access policies toogenerate SAS.</span></span>

<span data-ttu-id="2dec6-154">Para obter mais informações sobre assinaturas de acesso compartilhado, consulte [modelo SAS Olá Noções básicas sobre](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="2dec6-154">For more information on Shared Access Signatures, see [Understanding hello SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

### <a name="create-a-stored-policy-and-sas-using-c"></a><span data-ttu-id="2dec6-155">Criar uma política armazenada e uma SAS usando C\#</span><span class="sxs-lookup"><span data-stu-id="2dec6-155">Create a stored policy and SAS using C\#</span></span>

1. <span data-ttu-id="2dec6-156">Abra a solução de saudação no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2dec6-156">Open hello solution in Visual Studio.</span></span>

2. <span data-ttu-id="2dec6-157">No Gerenciador de soluções, clique com botão direito em Olá **SASToken** do projeto e selecione **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="2dec6-157">In Solution Explorer, right-click on hello **SASToken** project and select **Properties**.</span></span>

3. <span data-ttu-id="2dec6-158">Selecione **configurações** e adicionar valores para Olá entradas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2dec6-158">Select **Settings** and add values for hello following entries:</span></span>

   * <span data-ttu-id="2dec6-159">StorageConnectionString: conexão Olá string hello conta de armazenamento que você deseja toocreate uma política armazenada e a SAS para.</span><span class="sxs-lookup"><span data-stu-id="2dec6-159">StorageConnectionString: hello connection string for hello storage account that you want toocreate a stored policy and SAS for.</span></span> <span data-ttu-id="2dec6-160">saudação de formato deve ser `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` onde `myaccount` é o nome da saudação da sua conta de armazenamento e `mykey` é chave Olá Olá conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2dec6-160">hello format should be `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` where `myaccount` is hello name of your storage account and `mykey` is hello key for hello storage account.</span></span>

   * <span data-ttu-id="2dec6-161">ContainerName: contêiner de saudação na conta de armazenamento de saudação que você deseja toorestrict access.</span><span class="sxs-lookup"><span data-stu-id="2dec6-161">ContainerName: hello container in hello storage account that you want toorestrict access to.</span></span>

   * <span data-ttu-id="2dec6-162">SASPolicyName: Olá nome toouse para Olá armazenados toocreate de política.</span><span class="sxs-lookup"><span data-stu-id="2dec6-162">SASPolicyName: hello name toouse for hello stored policy toocreate.</span></span>

   * <span data-ttu-id="2dec6-163">FileToUpload: Olá caminho tooa arquivo que é carregado toohello contêiner.</span><span class="sxs-lookup"><span data-stu-id="2dec6-163">FileToUpload: hello path tooa file that is uploaded toohello container.</span></span>

4. <span data-ttu-id="2dec6-164">Execute projeto hello.</span><span class="sxs-lookup"><span data-stu-id="2dec6-164">Run hello project.</span></span> <span data-ttu-id="2dec6-165">Informações toohello semelhante texto a seguir é exibida depois Olá SAS foi gerada:</span><span class="sxs-lookup"><span data-stu-id="2dec6-165">Information similar toohello following text is displayed once hello SAS has been generated:</span></span>

        Container SAS token using stored access policy: sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="2dec6-166">Salve o token de política SAS Olá, nome da conta de armazenamento e nome do contêiner.</span><span class="sxs-lookup"><span data-stu-id="2dec6-166">Save hello SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="2dec6-167">Esses valores são usados ao associar a conta de armazenamento Olá seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2dec6-167">These values are used when associating hello storage account with your HDInsight cluster.</span></span>

### <a name="create-a-stored-policy-and-sas-using-python"></a><span data-ttu-id="2dec6-168">Criar uma política armazenada e uma SAS usando Python</span><span class="sxs-lookup"><span data-stu-id="2dec6-168">Create a stored policy and SAS using Python</span></span>

1. <span data-ttu-id="2dec6-169">Abrir o arquivo de SASToken.py hello e alterar Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="2dec6-169">Open hello SASToken.py file and change hello following values:</span></span>

   * <span data-ttu-id="2dec6-170">diretiva\_nome: Olá nome toouse para Olá armazenados toocreate de política.</span><span class="sxs-lookup"><span data-stu-id="2dec6-170">policy\_name: hello name toouse for hello stored policy toocreate.</span></span>

   * <span data-ttu-id="2dec6-171">armazenamento\_conta\_name: nome de saudação da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2dec6-171">storage\_account\_name: hello name of your storage account.</span></span>

   * <span data-ttu-id="2dec6-172">armazenamento\_conta\_chave: Olá chave Olá conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2dec6-172">storage\_account\_key: hello key for hello storage account.</span></span>

   * <span data-ttu-id="2dec6-173">armazenamento\_contêiner\_nome: contêiner de saudação na conta de armazenamento de saudação que você deseja toorestrict access.</span><span class="sxs-lookup"><span data-stu-id="2dec6-173">storage\_container\_name: hello container in hello storage account that you want toorestrict access to.</span></span>

   * <span data-ttu-id="2dec6-174">exemplo\_arquivo\_caminho: Olá caminho tooa arquivo contêiner toohello carregado.</span><span class="sxs-lookup"><span data-stu-id="2dec6-174">example\_file\_path: hello path tooa file that is uploaded toohello container.</span></span>

2. <span data-ttu-id="2dec6-175">Execute o script hello.</span><span class="sxs-lookup"><span data-stu-id="2dec6-175">Run hello script.</span></span> <span data-ttu-id="2dec6-176">Ele exibe o saudação SAS token semelhante toohello texto a seguir quando Olá script é concluído:</span><span class="sxs-lookup"><span data-stu-id="2dec6-176">It displays hello SAS token similar toohello following text when hello script completes:</span></span>

        sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="2dec6-177">Salve o token de política SAS Olá, nome da conta de armazenamento e nome do contêiner.</span><span class="sxs-lookup"><span data-stu-id="2dec6-177">Save hello SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="2dec6-178">Esses valores são usados ao associar a conta de armazenamento Olá seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2dec6-178">These values are used when associating hello storage account with your HDInsight cluster.</span></span>

## <a name="use-hello-sas-with-hdinsight"></a><span data-ttu-id="2dec6-179">Usar Olá SAS com HDInsight</span><span class="sxs-lookup"><span data-stu-id="2dec6-179">Use hello SAS with HDInsight</span></span>

<span data-ttu-id="2dec6-180">Ao criar um cluster HDInsight, você deverá especificar uma conta de armazenamento primária e, opcionalmente, poderá especificar contas de armazenamento adicionais.</span><span class="sxs-lookup"><span data-stu-id="2dec6-180">When creating an HDInsight cluster, you must specify a primary storage account and you can optionally specify additional storage accounts.</span></span> <span data-ttu-id="2dec6-181">Ambos os métodos de adição de armazenamento exigem contas de armazenamento toohello acesso completo e contêineres que são usados.</span><span class="sxs-lookup"><span data-stu-id="2dec6-181">Both of these methods of adding storage require full access toohello storage accounts and containers that are used.</span></span>

<span data-ttu-id="2dec6-182">toouse um contêiner de tooa de acesso de toolimit de assinatura de acesso compartilhado, adicione uma entrada personalizada toohello **site principal** configuração de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="2dec6-182">toouse a Shared Access Signature toolimit access tooa container, add a custom entry toohello **core-site** configuration for hello cluster.</span></span>

* <span data-ttu-id="2dec6-183">Para **baseados no Windows** ou **baseados em Linux** clusters de HDInsight, você pode adicionar a entrada de saudação durante a criação de cluster usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2dec6-183">For **Windows-based** or **Linux-based** HDInsight clusters, you can add hello entry during cluster creation using PowerShell.</span></span>
* <span data-ttu-id="2dec6-184">Para **baseados em Linux** clusters de HDInsight, alterar a configuração de saudação após a criação de cluster usando o Ambari.</span><span class="sxs-lookup"><span data-stu-id="2dec6-184">For **Linux-based** HDInsight clusters, change hello configuration after cluster creation using Ambari.</span></span>

### <a name="create-a-cluster-that-uses-hello-sas"></a><span data-ttu-id="2dec6-185">Criar um cluster que usa Olá SAS</span><span class="sxs-lookup"><span data-stu-id="2dec6-185">Create a cluster that uses hello SAS</span></span>

<span data-ttu-id="2dec6-186">Um exemplo de como criar um cluster HDInsight que Olá usa SAS está incluído no hello `CreateCluster` diretório de repositório de saudação.</span><span class="sxs-lookup"><span data-stu-id="2dec6-186">An example of creating an HDInsight cluster that uses hello SAS is included in hello `CreateCluster` directory of hello repository.</span></span> <span data-ttu-id="2dec6-187">toouse-lo, use Olá seguindo as etapas:</span><span class="sxs-lookup"><span data-stu-id="2dec6-187">toouse it, use hello following steps:</span></span>

1. <span data-ttu-id="2dec6-188">Olá abrir `CreateCluster\HDInsightSAS.ps1` do arquivo em um editor de texto e modifique Olá valores no início de saudação do documento de saudação a seguir.</span><span class="sxs-lookup"><span data-stu-id="2dec6-188">Open hello `CreateCluster\HDInsightSAS.ps1` file in a text editor and modify hello following values at hello beginning of hello document.</span></span>

    ```powershell
    # Replace 'mycluster' with hello name of hello cluster toobe created
    $clusterName = 'mycluster'
    # Valid values are 'Linux' and 'Windows'
    $osType = 'Linux'
    # Replace 'myresourcegroup' with hello name of hello group toobe created
    $resourceGroupName = 'myresourcegroup'
    # Replace with hello Azure data center you want toohello cluster toolive in
    $location = 'North Europe'
    # Replace with hello name of hello default storage account toobe created
    $defaultStorageAccountName = 'mystorageaccount'
    # Replace with hello name of hello SAS container created earlier
    $SASContainerName = 'sascontainer'
    # Replace with hello name of hello SAS storage account created earlier
    $SASStorageAccountName = 'sasaccount'
    # Replace with hello SAS token generated earlier
    $SASToken = 'sastoken'
    # Set hello number of worker nodes in hello cluster
    $clusterSizeInNodes = 3
    ```

    <span data-ttu-id="2dec6-189">Por exemplo, alterar `'mycluster'` toohello nome de cluster Olá você deseja toocreate.</span><span class="sxs-lookup"><span data-stu-id="2dec6-189">For example, change `'mycluster'` toohello name of hello cluster you want toocreate.</span></span> <span data-ttu-id="2dec6-190">valores SAS Olá devem corresponder valores hello de etapas anteriores Olá ao criar uma conta de armazenamento e o token SAS.</span><span class="sxs-lookup"><span data-stu-id="2dec6-190">hello SAS values should match hello values from hello previous steps when creating a storage account and SAS token.</span></span>

    <span data-ttu-id="2dec6-191">Depois que você tiver alterado os valores hello, salve arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="2dec6-191">Once you have changed hello values, save hello file.</span></span>

2. <span data-ttu-id="2dec6-192">Abra um novo prompt do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2dec6-192">Open a new Azure PowerShell prompt.</span></span> <span data-ttu-id="2dec6-193">Se você não estiver familiarizado com o Azure PowerShell ou se não o tiver instalado, consulte [Instalar e configurar o Azure PowerShell][powershell].</span><span class="sxs-lookup"><span data-stu-id="2dec6-193">If you are unfamiliar with Azure PowerShell, or have not installed it, see [Install and configure Azure PowerShell][powershell].</span></span>

1. <span data-ttu-id="2dec6-194">No prompt de hello, use Olá comando tooauthenticate tooyour assinatura do Azure a seguir:</span><span class="sxs-lookup"><span data-stu-id="2dec6-194">From hello prompt, use hello following command tooauthenticate tooyour Azure subscription:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="2dec6-195">Quando solicitado, faça logon com a conta Olá para sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="2dec6-195">When prompted, log in with hello account for your Azure subscription.</span></span>

    <span data-ttu-id="2dec6-196">Se sua conta estiver associada a várias assinaturas do Azure, talvez seja necessário toouse `Select-AzureRmSubscription` tooselect assinatura de saudação desejar toouse.</span><span class="sxs-lookup"><span data-stu-id="2dec6-196">If your account is associated with multiple Azure subscriptions, you may need toouse `Select-AzureRmSubscription` tooselect hello subscription you wish toouse.</span></span>

4. <span data-ttu-id="2dec6-197">No prompt de hello, altere diretórios toohello `CreateCluster` diretório que contém o arquivo de HDInsightSAS.ps1 hello.</span><span class="sxs-lookup"><span data-stu-id="2dec6-197">From hello prompt, change directories toohello `CreateCluster` directory that contains hello HDInsightSAS.ps1 file.</span></span> <span data-ttu-id="2dec6-198">Em seguida, usar Olá após o script do comando toorun Olá</span><span class="sxs-lookup"><span data-stu-id="2dec6-198">Then use hello following command toorun hello script</span></span>

    ```powershell
    .\HDInsightSAS.ps1
    ```

    <span data-ttu-id="2dec6-199">Como Olá script é executado, ele registra prompt do PowerShell toohello saída enquanto cria recursos Olá contas de grupo e de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2dec6-199">As hello script runs, it logs output toohello PowerShell prompt as it creates hello resource group and storage accounts.</span></span> <span data-ttu-id="2dec6-200">Você está tooenter solicitada ao usuário Olá HTTP Olá cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2dec6-200">You are prompted tooenter hello HTTP user for hello HDInsight cluster.</span></span> <span data-ttu-id="2dec6-201">Essa conta é usada toosecure cluster de toohello de acesso HTTP/s.</span><span class="sxs-lookup"><span data-stu-id="2dec6-201">This account is used toosecure HTTP/s access toohello cluster.</span></span>

    <span data-ttu-id="2dec6-202">Se você estiver criando um cluster baseado em Linux, também será solicitado que você forneça um nome de conta de usuário SSH e uma senha.</span><span class="sxs-lookup"><span data-stu-id="2dec6-202">If you are creating a Linux-based cluster, you are prompted for an SSH user account name and password.</span></span> <span data-ttu-id="2dec6-203">Essa conta é usado tooremotely login toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="2dec6-203">This account is used tooremotely log in toohello cluster.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="2dec6-204">Quando solicitado Olá HTTP/s ou SSH nome de usuário e senha, você deve fornecer uma senha que atenda a saudação critérios a seguir:</span><span class="sxs-lookup"><span data-stu-id="2dec6-204">When prompted for hello HTTP/s or SSH user name and password, you must provide a password that meets hello following criteria:</span></span>
   >
   > * <span data-ttu-id="2dec6-205">Deve ter pelo menos 10 caracteres de comprimento</span><span class="sxs-lookup"><span data-stu-id="2dec6-205">Must be at least 10 characters in length</span></span>
   > * <span data-ttu-id="2dec6-206">Deve conter pelo menos um dígito</span><span class="sxs-lookup"><span data-stu-id="2dec6-206">Must contain at least one digit</span></span>
   > * <span data-ttu-id="2dec6-207">Deve conter pelo menos um caractere não alfanumérico</span><span class="sxs-lookup"><span data-stu-id="2dec6-207">Must contain at least one non-alphanumeric character</span></span>
   > * <span data-ttu-id="2dec6-208">Deve conter pelo menos uma letra maiúscula ou minúscula</span><span class="sxs-lookup"><span data-stu-id="2dec6-208">Must contain at least one upper or lower case letter</span></span>

<span data-ttu-id="2dec6-209">Leva algum tempo para esse script toocomplete, normalmente em torno de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="2dec6-209">It takes a while for this script toocomplete, usually around 15 minutes.</span></span> <span data-ttu-id="2dec6-210">Quando o script de saudação é concluído sem erros, Olá cluster foi criado.</span><span class="sxs-lookup"><span data-stu-id="2dec6-210">When hello script completes without any errors, hello cluster has been created.</span></span>

### <a name="use-hello-sas-with-an-existing-cluster"></a><span data-ttu-id="2dec6-211">Usar Olá SAS com um cluster existente</span><span class="sxs-lookup"><span data-stu-id="2dec6-211">Use hello SAS with an existing cluster</span></span>

<span data-ttu-id="2dec6-212">Se você tiver um cluster existente com base em Linux, você pode adicionar Olá SAS toohello **site principal** configuração usando Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2dec6-212">If you have an existing Linux-based cluster, you can add hello SAS toohello **core-site** configuration by using hello following steps:</span></span>

1. <span data-ttu-id="2dec6-213">Abra Olá Ambari web da interface do usuário para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="2dec6-213">Open hello Ambari web UI for your cluster.</span></span> <span data-ttu-id="2dec6-214">endereço de saudação para essa página é https://YOURCLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="2dec6-214">hello address for this page is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="2dec6-215">Quando solicitado, autentique toohello cluster usando o nome do administrador de saudação (administrador) e senha que você usou quando criar o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="2dec6-215">When prompted, authenticate toohello cluster using hello admin name (admin) and password you used when creating hello cluster.</span></span>

2. <span data-ttu-id="2dec6-216">Olá lado esquerdo da interface da web hello Ambari, selecione **HDFS** e, em seguida, selecione Olá **configurações** guia no meio de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="2dec6-216">From hello left side of hello Ambari web UI, select **HDFS** and then select hello **Configs** tab in hello middle of hello page.</span></span>

3. <span data-ttu-id="2dec6-217">Selecione Olá **avançado** guia e, em seguida, role até encontrar hello **site personalizado core** seção.</span><span class="sxs-lookup"><span data-stu-id="2dec6-217">Select hello **Advanced** tab, and then scroll until you find hello **Custom core-site** section.</span></span>

4. <span data-ttu-id="2dec6-218">Expanda Olá **site personalizado core** seção, em seguida, final de toohello de rolagem e selecione Olá **adicionar propriedade...**  link.</span><span class="sxs-lookup"><span data-stu-id="2dec6-218">Expand hello **Custom core-site** section, then scroll toohello end and select hello **Add property...** link.</span></span> <span data-ttu-id="2dec6-219">A seguir Olá Use valores de saudação **chave** e **valor** campos:</span><span class="sxs-lookup"><span data-stu-id="2dec6-219">Use hello following values for hello **Key** and **Value** fields:</span></span>

   * <span data-ttu-id="2dec6-220">**Chave**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="2dec6-220">**Key**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span></span>
   * <span data-ttu-id="2dec6-221">**Valor**: Olá SAS retornado por Olá aplicativo c# ou Python que você executou anteriormente</span><span class="sxs-lookup"><span data-stu-id="2dec6-221">**Value**: hello SAS returned by hello C# or Python application you ran previously</span></span>

     <span data-ttu-id="2dec6-222">Substituir **CONTAINERNAME** com o nome do contêiner de saudação usada com o aplicativo hello de c# ou SAS.</span><span class="sxs-lookup"><span data-stu-id="2dec6-222">Replace **CONTAINERNAME** with hello container name you used with hello C# or SAS application.</span></span> <span data-ttu-id="2dec6-223">Substituir **STORAGEACCOUNTNAME** com o nome de conta de armazenamento Olá usado.</span><span class="sxs-lookup"><span data-stu-id="2dec6-223">Replace **STORAGEACCOUNTNAME** with hello storage account name you used.</span></span>

5. <span data-ttu-id="2dec6-224">Clique em Olá **adicionar** toosave nesse chave e valor e clique em Olá **salvar** botão toosave alterações de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="2dec6-224">Click hello **Add** button toosave this key and value, then click hello **Save** button toosave hello configuration changes.</span></span> <span data-ttu-id="2dec6-225">Quando solicitado, adicione uma descrição da alteração da saudação ("adicionar acesso de armazenamento SAS" por exemplo) e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="2dec6-225">When prompted, add a description of hello change ("adding SAS storage access" for example) and then click **Save**.</span></span>

    <span data-ttu-id="2dec6-226">Clique em **Okey** quando Olá alterações foram concluídas.</span><span class="sxs-lookup"><span data-stu-id="2dec6-226">Click **OK** when hello changes have been completed.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="2dec6-227">Você deve reiniciar vários serviços para que Olá alteração entra em vigor.</span><span class="sxs-lookup"><span data-stu-id="2dec6-227">You must restart several services before hello change takes effect.</span></span>

6. <span data-ttu-id="2dec6-228">No Olá Ambari web da interface do usuário, selecione **HDFS** na lista Olá Olá à esquerda e, em seguida, selecione **reiniciar todos os** de saudação **ações de serviço** suspensa lista saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="2dec6-228">In hello Ambari web UI, select **HDFS** from hello list on hello left, and then select **Restart All** from hello **Service Actions** drop down list on hello right.</span></span> <span data-ttu-id="2dec6-229">Quando solicitado, selecione **Ativar o modo de manutenção** e selecione __Conforme Reiniciar Todos".</span><span class="sxs-lookup"><span data-stu-id="2dec6-229">When prompted, select **Turn on maintenance mode** and then select __Conform Restart All".</span></span>

    <span data-ttu-id="2dec6-230">Repita esse processo para MapReduce2 e YARN.</span><span class="sxs-lookup"><span data-stu-id="2dec6-230">Repeat this process for MapReduce2 and YARN.</span></span>

7. <span data-ttu-id="2dec6-231">Depois de reiniciar serviços hello, selecione cada uma e desabilitar o modo de manutenção de saudação **ações de serviço** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="2dec6-231">Once hello services have restarted, select each one and disable maintenance mode from hello **Service Actions** drop down.</span></span>

## <a name="test-restricted-access"></a><span data-ttu-id="2dec6-232">Testar o acesso restrito</span><span class="sxs-lookup"><span data-stu-id="2dec6-232">Test restricted access</span></span>

<span data-ttu-id="2dec6-233">tooverify restringir o acesso, use Olá métodos a seguir:</span><span class="sxs-lookup"><span data-stu-id="2dec6-233">tooverify that you have restricted access, use hello following methods:</span></span>

* <span data-ttu-id="2dec6-234">Para **baseados no Windows** clusters de HDInsight, use o cluster de toohello tooconnect área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="2dec6-234">For **Windows-based** HDInsight clusters, use Remote Desktop tooconnect toohello cluster.</span></span> <span data-ttu-id="2dec6-235">Para obter mais informações, consulte [se conectar usando o RDP de tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="2dec6-235">For more information, see [Connect tooHDInsight using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

    <span data-ttu-id="2dec6-236">Uma vez conectado, use Olá **Hadoop de linha de comando** ícone Olá desktop tooopen um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="2dec6-236">Once connected, use hello **Hadoop Command-Line** icon on hello desktop tooopen a command prompt.</span></span>

* <span data-ttu-id="2dec6-237">Para **baseados em Linux** clusters de HDInsight, usar SSH tooconnect toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="2dec6-237">For **Linux-based** HDInsight clusters, use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="2dec6-238">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="2dec6-238">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="2dec6-239">Uma vez conectado toohello cluster, use Olá tooverify etapas que você pode somente leitura e a lista de itens na conta de armazenamento SAS Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="2dec6-239">Once connected toohello cluster, use hello following steps tooverify that you can only read and list items on hello SAS storage account:</span></span>

1. <span data-ttu-id="2dec6-240">conteúdo de saudação toolist do contêiner hello, use Olá comando a seguir no prompt de saudação de:</span><span class="sxs-lookup"><span data-stu-id="2dec6-240">toolist hello contents of hello container, use hello following command from hello prompt:</span></span> 

    ```bash
    hdfs dfs -ls wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/
    ```

    <span data-ttu-id="2dec6-241">Substituir **SASCONTAINER** com o nome de saudação do contêiner Olá criado para conta de armazenamento SAS de saudação.</span><span class="sxs-lookup"><span data-stu-id="2dec6-241">Replace **SASCONTAINER** with hello name of hello container created for hello SAS storage account.</span></span> <span data-ttu-id="2dec6-242">Substituir **SASACCOUNTNAME** com nome Olá Olá da conta de armazenamento usada para Olá SAS.</span><span class="sxs-lookup"><span data-stu-id="2dec6-242">Replace **SASACCOUNTNAME** with hello name of hello storage account used for hello SAS.</span></span>

    <span data-ttu-id="2dec6-243">lista de saudação inclui arquivo hello carregado quando o contêiner de saudação e a SAS foram criados.</span><span class="sxs-lookup"><span data-stu-id="2dec6-243">hello list includes hello file uploaded when hello container and SAS were created.</span></span>

2. <span data-ttu-id="2dec6-244">Use Olá tooverify de comando que você pode ler o conteúdo de saudação do arquivo hello a seguir.</span><span class="sxs-lookup"><span data-stu-id="2dec6-244">Use hello following command tooverify that you can read hello contents of hello file.</span></span> <span data-ttu-id="2dec6-245">Substituir saudação **SASCONTAINER** e **SASACCOUNTNAME** como na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="2dec6-245">Replace hello **SASCONTAINER** and **SASACCOUNTNAME** as in hello previous step.</span></span> <span data-ttu-id="2dec6-246">Substituir **FILENAME** pelo nome de saudação do arquivo de saudação exibido no comando anterior hello:</span><span class="sxs-lookup"><span data-stu-id="2dec6-246">Replace **FILENAME** with hello name of hello file displayed in hello previous command:</span></span>

    ```bash
    hdfs dfs -text wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME
    ```

    <span data-ttu-id="2dec6-247">Esse comando lista os conteúdos de saudação do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="2dec6-247">This command lists hello contents of hello file.</span></span>

3. <span data-ttu-id="2dec6-248">Saudação de usar o sistema de arquivos local do comando toodownload Olá arquivo toohello a seguir:</span><span class="sxs-lookup"><span data-stu-id="2dec6-248">Use hello following command toodownload hello file toohello local file system:</span></span>

    ```bash
    hdfs dfs -get wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME testfile.txt
    ```

    <span data-ttu-id="2dec6-249">Este comando downloads Olá tooa local arquivo denominado **Testfile**.</span><span class="sxs-lookup"><span data-stu-id="2dec6-249">This command downloads hello file tooa local file named **testfile.txt**.</span></span>

4. <span data-ttu-id="2dec6-250">A seguir use Olá comando tooupload Olá arquivo local tooa novo arquivo denominado **testupload.txt** em Olá armazenamento SAS:</span><span class="sxs-lookup"><span data-stu-id="2dec6-250">Use hello following command tooupload hello local file tooa new file named **testupload.txt** on hello SAS storage:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/testupload.txt
    ```

    <span data-ttu-id="2dec6-251">Você receberá um toohello semelhante mensagem texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="2dec6-251">You receive a message similar toohello following text:</span></span>

        put: java.io.IOException

    <span data-ttu-id="2dec6-252">Esse erro ocorre porque o local de armazenamento de saudação é leitura + lista.</span><span class="sxs-lookup"><span data-stu-id="2dec6-252">This error occurs because hello storage location is read+list only.</span></span> <span data-ttu-id="2dec6-253">Use Olá seguindo os dados de saudação do comando tooput no armazenamento padrão da saudação para cluster hello, que é gravável:</span><span class="sxs-lookup"><span data-stu-id="2dec6-253">Use hello following command tooput hello data on hello default storage for hello cluster, which is writable:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb:///testupload.txt
    ```

    <span data-ttu-id="2dec6-254">Neste momento, Olá operação deve ser concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="2dec6-254">This time, hello operation should complete successfully.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="2dec6-255">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="2dec6-255">Troubleshooting</span></span>

### <a name="a-task-was-canceled"></a><span data-ttu-id="2dec6-256">Uma tarefa foi cancelada</span><span class="sxs-lookup"><span data-stu-id="2dec6-256">A task was canceled</span></span>

<span data-ttu-id="2dec6-257">**Sintomas**: ao criar um cluster usando o script do PowerShell hello, você pode receber Olá a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="2dec6-257">**Symptoms**: When creating a cluster using hello PowerShell script, you may receive hello following error message:</span></span>

    New-AzureRmHDInsightCluster : A task was canceled.
    At C:\Users\larryfr\Documents\GitHub\hdinsight-azure-storage-sas\CreateCluster\HDInsightSAS.ps1:62 char:5
    +     New-AzureRmHDInsightCluster `
    +     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (:) [New-AzureRmHDInsightCluster], CloudException
        + FullyQualifiedErrorId : Hyak.Common.CloudException,Microsoft.Azure.Commands.HDInsight.NewAzureHDInsightClusterCommand

<span data-ttu-id="2dec6-258">**Causa**: este erro pode ocorrer se você usar uma senha de usuário de administração/HTTP Olá para cluster hello, ou (para clusters baseados em Linux) usuário SSH hello.</span><span class="sxs-lookup"><span data-stu-id="2dec6-258">**Cause**: This error can occur if you use a password for hello admin/HTTP user for hello cluster, or (for Linux-based clusters) hello SSH user.</span></span>

<span data-ttu-id="2dec6-259">**Resolução**: Use uma senha que atenda a saudação critérios a seguir:</span><span class="sxs-lookup"><span data-stu-id="2dec6-259">**Resolution**: Use a password that meets hello following criteria:</span></span>

* <span data-ttu-id="2dec6-260">Deve ter pelo menos 10 caracteres de comprimento</span><span class="sxs-lookup"><span data-stu-id="2dec6-260">Must be at least 10 characters in length</span></span>
* <span data-ttu-id="2dec6-261">Deve conter pelo menos um dígito</span><span class="sxs-lookup"><span data-stu-id="2dec6-261">Must contain at least one digit</span></span>
* <span data-ttu-id="2dec6-262">Deve conter pelo menos um caractere não alfanumérico</span><span class="sxs-lookup"><span data-stu-id="2dec6-262">Must contain at least one non-alphanumeric character</span></span>
* <span data-ttu-id="2dec6-263">Deve conter pelo menos uma letra maiúscula ou minúscula</span><span class="sxs-lookup"><span data-stu-id="2dec6-263">Must contain at least one upper or lower case letter</span></span>

## <a name="next-steps"></a><span data-ttu-id="2dec6-264">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2dec6-264">Next steps</span></span>

<span data-ttu-id="2dec6-265">Agora que você aprendeu como tooadd acesso limitado armazenamento tooyour cluster HDInsight, aprender toowork outras maneiras com dados em seu cluster:</span><span class="sxs-lookup"><span data-stu-id="2dec6-265">Now that you have learned how tooadd limited-access storage tooyour HDInsight cluster, learn other ways toowork with data on your cluster:</span></span>

* [<span data-ttu-id="2dec6-266">Usar o Hive com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="2dec6-266">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="2dec6-267">Usar o Pig com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="2dec6-267">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="2dec6-268">Usar o MapReduce com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="2dec6-268">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[powershell]: /powershell/azureps-cmdlets-docs
