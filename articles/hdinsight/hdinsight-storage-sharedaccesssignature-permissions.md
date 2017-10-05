---
title: "Restringir o acesso usando Assinaturas de Acesso Compartilhado – HDInsight do Azure | Microsoft Docs"
description: Saiba como usar Assinaturas de Acesso Compartilhado para restringir o acesso do HDInsight a dados armazenados em blobs de armazenamento do Azure.
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
ms.openlocfilehash: 2e4b1a307fae06c0639d93b9804c6f0f703d5900
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-storage-shared-access-signatures-to-restrict-access-to-data-in-hdinsight"></a><span data-ttu-id="9321e-103">Usar Assinaturas de Acesso Compartilhado do Armazenamento do Azure para restringir o acesso a dados no HDInsight</span><span class="sxs-lookup"><span data-stu-id="9321e-103">Use Azure Storage Shared Access Signatures to restrict access to data in HDInsight</span></span>

<span data-ttu-id="9321e-104">O HDInsight tem acesso completo aos dados nas contas de Armazenamento do Azure associadas ao cluster.</span><span class="sxs-lookup"><span data-stu-id="9321e-104">HDInsight has full access to data in the Azure Storage accounts associated with the cluster.</span></span> <span data-ttu-id="9321e-105">Você pode usar Assinaturas de Acesso Compartilhado no contêiner de blob para restringir o acesso aos dados.</span><span class="sxs-lookup"><span data-stu-id="9321e-105">You can use Shared Access Signatures on the blob container to restrict access to the data.</span></span> <span data-ttu-id="9321e-106">Por exemplo, para fornecer acesso somente leitura aos dados.</span><span class="sxs-lookup"><span data-stu-id="9321e-106">For example, to provide read-only access to the data.</span></span> <span data-ttu-id="9321e-107">As Assinaturas de Acesso Compartilhado (SAS) são recursos das contas de armazenamento do Azure que permitem que você limite o acesso aos dados.</span><span class="sxs-lookup"><span data-stu-id="9321e-107">Shared Access Signatures (SAS) are a feature of Azure storage accounts that allows you to limit access to data.</span></span> <span data-ttu-id="9321e-108">Por exemplo, oferecendo acesso somente leitura aos dados.</span><span class="sxs-lookup"><span data-stu-id="9321e-108">For example, providing read-only access to data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9321e-109">Para uma solução que usa o Apache Ranger, considere usar HDInsight ingressado em domínio.</span><span class="sxs-lookup"><span data-stu-id="9321e-109">For a solution using Apache Ranger, consider using domain-joined HDInsight.</span></span> <span data-ttu-id="9321e-110">Para obter mais informações, consulte o documento [Configurar HDInsight ingressado em domínio](hdinsight-domain-joined-configure.md).</span><span class="sxs-lookup"><span data-stu-id="9321e-110">For more information, see the [Configure domain-joined HDInsight](hdinsight-domain-joined-configure.md) document.</span></span>

> [!WARNING]
> <span data-ttu-id="9321e-111">O HDInsight deve ter acesso completo ao armazenamento padrão para o cluster.</span><span class="sxs-lookup"><span data-stu-id="9321e-111">HDInsight must have full access to the default storage for the cluster.</span></span>

## <a name="requirements"></a><span data-ttu-id="9321e-112">Requisitos</span><span class="sxs-lookup"><span data-stu-id="9321e-112">Requirements</span></span>

* <span data-ttu-id="9321e-113">Uma assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="9321e-113">An Azure subscription</span></span>
* <span data-ttu-id="9321e-114">C# ou Python.</span><span class="sxs-lookup"><span data-stu-id="9321e-114">C# or Python.</span></span> <span data-ttu-id="9321e-115">O código de exemplo do C# é fornecido como uma solução do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9321e-115">C# example code is provided as a Visual Studio solution.</span></span>

  * <span data-ttu-id="9321e-116">A versão do Visual Studio deve ser a 2013, 2015 ou 2017</span><span class="sxs-lookup"><span data-stu-id="9321e-116">Visual Studio must be version 2013, 2015, or 2017</span></span>
  * <span data-ttu-id="9321e-117">A versão do Python deverá ser a 2.7 ou superior</span><span class="sxs-lookup"><span data-stu-id="9321e-117">Python must be version 2.7 or higher</span></span>

* <span data-ttu-id="9321e-118">Um cluster HDInsight baseado em Linux OU o [Azure PowerShell][powershell] ‑ Se você tiver um cluster existente baseado em Linux, poderá usar o Ambari para adicionar uma Assinatura de Acesso Compartilhado ao cluster.</span><span class="sxs-lookup"><span data-stu-id="9321e-118">A Linux-based HDInsight cluster OR [Azure PowerShell][powershell] - If you have an existing Linux-based cluster, you can use Ambari to add a Shared Access Signature to the cluster.</span></span> <span data-ttu-id="9321e-119">Caso contrário, você poderá usar o Azure PowerShell para criar um cluster e adicionar uma Assinatura de Acesso Compartilhado durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="9321e-119">If not, you can use Azure PowerShell to create a cluster and add a Shared Access Signature during cluster creation.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="9321e-120">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="9321e-120">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9321e-121">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="9321e-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="9321e-122">Os arquivos de exemplo de [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span><span class="sxs-lookup"><span data-stu-id="9321e-122">The example files from [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span></span> <span data-ttu-id="9321e-123">Esse repositório contém os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="9321e-123">This repository contains the following items:</span></span>

  * <span data-ttu-id="9321e-124">Um projeto do Visual Studio que pode criar um contêiner de armazenamento, a política armazenada e a SAS a ser usada com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="9321e-124">A Visual Studio project that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="9321e-125">Um script Python que pode criar um contêiner de armazenamento, a política armazenada e a SAS a ser usada com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="9321e-125">A Python script that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="9321e-126">Um script do PowerShell que pode criar um cluster HDInsight e configurá-lo para usar a SAS.</span><span class="sxs-lookup"><span data-stu-id="9321e-126">A PowerShell script that can create a HDInsight cluster and configure it to use the SAS.</span></span>

## <a name="shared-access-signatures"></a><span data-ttu-id="9321e-127">As Assinaturas de Acesso Compartilhado</span><span class="sxs-lookup"><span data-stu-id="9321e-127">Shared Access Signatures</span></span>

<span data-ttu-id="9321e-128">Há duas formas de Assinaturas de Acesso Compartilhado:</span><span class="sxs-lookup"><span data-stu-id="9321e-128">There are two forms of Shared Access Signatures:</span></span>

* <span data-ttu-id="9321e-129">Ad hoc: a hora de início, o tempo de expiração e as permissões para a SAS são todos especificados no URI SAS.</span><span class="sxs-lookup"><span data-stu-id="9321e-129">Ad hoc: The start time, expiry time, and permissions for the SAS are all specified on the SAS URI.</span></span>

* <span data-ttu-id="9321e-130">Política de acesso armazenada: uma política de acesso armazenada é definida em um contêiner de recurso, como um contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="9321e-130">Stored access policy: A stored access policy is defined on a resource container, such as a blob container.</span></span> <span data-ttu-id="9321e-131">Uma política pode ser usada para gerenciar as restrições de uma ou mais assinaturas de acesso compartilhado.</span><span class="sxs-lookup"><span data-stu-id="9321e-131">A policy can be used to manage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="9321e-132">Quando você associa uma SAS a uma política de acesso armazenada, a SAS herda as restrições - a hora de início, a hora de expiração e as permissões - definidas para a política de acesso armazenada.</span><span class="sxs-lookup"><span data-stu-id="9321e-132">When you associate a SAS with a stored access policy, the SAS inherits the constraints - the start time, expiry time, and permissions - defined for the stored access policy.</span></span>

<span data-ttu-id="9321e-133">A diferença entre as duas formas é importante para um cenário fundamental: revogação.</span><span class="sxs-lookup"><span data-stu-id="9321e-133">The difference between the two forms is important for one key scenario: revocation.</span></span> <span data-ttu-id="9321e-134">Uma SAS é uma URL, portanto qualquer pessoa que obtiver a SAS poderá usá-la, independentemente de quem a tiver solicitado em primeiro lugar.</span><span class="sxs-lookup"><span data-stu-id="9321e-134">A SAS is a URL, so anyone who obtains the SAS can use it, regardless of who requested it to begin with.</span></span> <span data-ttu-id="9321e-135">Se uma SAS for publicada publicamente, ela poderá ser usada por qualquer pessoa no mundo.</span><span class="sxs-lookup"><span data-stu-id="9321e-135">If a SAS is published publicly, it can be used by anyone in the world.</span></span> <span data-ttu-id="9321e-136">Uma SAS distribuída será válida até que ocorra um destes quatro fatores:</span><span class="sxs-lookup"><span data-stu-id="9321e-136">A SAS that is distributed is valid until one of four things happens:</span></span>

1. <span data-ttu-id="9321e-137">A hora de expiração especificada na SAS é atingida.</span><span class="sxs-lookup"><span data-stu-id="9321e-137">The expiry time specified on the SAS is reached.</span></span>

2. <span data-ttu-id="9321e-138">O tempo de expiração especificado na política de acesso armazenada referenciada por SAS é atingido.</span><span class="sxs-lookup"><span data-stu-id="9321e-138">The expiry time specified on the stored access policy referenced by the SAS is reached.</span></span> <span data-ttu-id="9321e-139">Os seguintes cenários fazem com que o tempo de expiração seja atingido:</span><span class="sxs-lookup"><span data-stu-id="9321e-139">The following scenarios cause the expiry time to be reached:</span></span>

    * <span data-ttu-id="9321e-140">O intervalo de tempo esgotou-se.</span><span class="sxs-lookup"><span data-stu-id="9321e-140">The time interval has elapsed.</span></span>
    * <span data-ttu-id="9321e-141">A política de acesso armazenada foi modificada para ter um tempo de expiração no passado.</span><span class="sxs-lookup"><span data-stu-id="9321e-141">The stored access policy is modified to have an expiry time in the past.</span></span> <span data-ttu-id="9321e-142">Alterar o tempo de expiração é uma maneira de revogar a SAS.</span><span class="sxs-lookup"><span data-stu-id="9321e-142">Changing the expiry time is one way to revoke the SAS.</span></span>

3. <span data-ttu-id="9321e-143">A política de acesso armazenada referenciada pelas SAS é excluída, que é uma outra maneira de revogar a SAS.</span><span class="sxs-lookup"><span data-stu-id="9321e-143">The stored access policy referenced by the SAS is deleted, which is another way to revoke the SAS.</span></span> <span data-ttu-id="9321e-144">Se você recriar a política de acesso armazenado com o mesmo nome, todos os tokens SAS para a política anterior serão válidos (se o tempo de expiração na SAS não tiver passado).</span><span class="sxs-lookup"><span data-stu-id="9321e-144">If you recreate the stored access policy with the same name, all  SAS tokens for the previous policy are valid (if the expiry time on the SAS has not passed).</span></span> <span data-ttu-id="9321e-145">Se você estiver pretendendo revogar a SAS, use um nome diferente se recriar a política de acesso com uma hora de expiração no futuro.</span><span class="sxs-lookup"><span data-stu-id="9321e-145">If you intend to revoke the SAS, be sure to use a different name if you recreate the access policy with an expiry time in the future.</span></span>

4. <span data-ttu-id="9321e-146">A chave de conta usada para criar as SAS é regenerada.</span><span class="sxs-lookup"><span data-stu-id="9321e-146">The account key that was used to create the SAS is regenerated.</span></span> <span data-ttu-id="9321e-147">A regeneração da chave faz com que todos os aplicativos que usam a chave anterior falhem na autenticação.</span><span class="sxs-lookup"><span data-stu-id="9321e-147">Regenerating the key causes all applications that use the previous key to fail authentication.</span></span> <span data-ttu-id="9321e-148">Atualize todos os componentes para a nova chave.</span><span class="sxs-lookup"><span data-stu-id="9321e-148">Update all components to the new key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9321e-149">Um URI de assinatura de acesso compartilhado é associado com a chave de conta usada para criar a assinatura e a política de acesso armazenado associada (se houver).</span><span class="sxs-lookup"><span data-stu-id="9321e-149">A shared access signature URI is associated with the account key used to create the signature, and the associated stored access policy (if any).</span></span> <span data-ttu-id="9321e-150">Se nenhuma política de acesso armazenado for especificada, a única maneira de revogar uma assinatura de acesso compartilhado é alterar a chave da conta.</span><span class="sxs-lookup"><span data-stu-id="9321e-150">If no stored access policy is specified, the only way to revoke a shared access signature is to change the account key.</span></span>

<span data-ttu-id="9321e-151">É recomendável sempre usar políticas de acesso armazenadas.</span><span class="sxs-lookup"><span data-stu-id="9321e-151">We recommend that you always use stored access policies.</span></span> <span data-ttu-id="9321e-152">Ao usar políticas armazenadas, você pode revogar assinaturas ou estender a data de expiração conforme a necessidade.</span><span class="sxs-lookup"><span data-stu-id="9321e-152">When using stored policies, you can either revoke signatures or extend the expiry date as needed.</span></span> <span data-ttu-id="9321e-153">As etapas deste documento usam políticas de acesso armazenado para gerar a SAS.</span><span class="sxs-lookup"><span data-stu-id="9321e-153">The steps in this document use stored access policies to generate SAS.</span></span>

<span data-ttu-id="9321e-154">Para saber mais sobre as Assinaturas de Acesso Compartilhado, consulte [Noções básicas sobre o modelo de SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="9321e-154">For more information on Shared Access Signatures, see [Understanding the SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

### <a name="create-a-stored-policy-and-sas-using-c"></a><span data-ttu-id="9321e-155">Criar uma política armazenada e uma SAS usando C\#</span><span class="sxs-lookup"><span data-stu-id="9321e-155">Create a stored policy and SAS using C\#</span></span>

1. <span data-ttu-id="9321e-156">Abra a solução no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9321e-156">Open the solution in Visual Studio.</span></span>

2. <span data-ttu-id="9321e-157">No Gerenciador de Soluções, clique com o botão direito do mouse no projeto **SASToken** e selecione **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="9321e-157">In Solution Explorer, right-click on the **SASToken** project and select **Properties**.</span></span>

3. <span data-ttu-id="9321e-158">Escolha **Configurações** e adicione valores às seguintes entradas:</span><span class="sxs-lookup"><span data-stu-id="9321e-158">Select **Settings** and add values for the following entries:</span></span>

   * <span data-ttu-id="9321e-159">StorageConnectionString: a cadeia de conexão da conta de armazenamento para a qual você deseja criar uma política armazenada e uma SAS.</span><span class="sxs-lookup"><span data-stu-id="9321e-159">StorageConnectionString: The connection string for the storage account that you want to create a stored policy and SAS for.</span></span> <span data-ttu-id="9321e-160">O formato deve ser `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` onde `myaccount` é o nome de sua conta de armazenamento e `mykey` é a chave da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9321e-160">The format should be `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` where `myaccount` is the name of your storage account and `mykey` is the key for the storage account.</span></span>

   * <span data-ttu-id="9321e-161">ContainerName: o contêiner na conta de armazenamento para o qual você deseja restringir o acesso.</span><span class="sxs-lookup"><span data-stu-id="9321e-161">ContainerName: The container in the storage account that you want to restrict access to.</span></span>

   * <span data-ttu-id="9321e-162">SASPolicyName: o nome a ser usado para a política armazenada que será criada.</span><span class="sxs-lookup"><span data-stu-id="9321e-162">SASPolicyName: The name to use for the stored policy to create.</span></span>

   * <span data-ttu-id="9321e-163">FileToUpload: o caminho para um arquivo que é carregado no contêiner.</span><span class="sxs-lookup"><span data-stu-id="9321e-163">FileToUpload: The path to a file that is uploaded to the container.</span></span>

4. <span data-ttu-id="9321e-164">Execute o projeto.</span><span class="sxs-lookup"><span data-stu-id="9321e-164">Run the project.</span></span> <span data-ttu-id="9321e-165">Informações semelhantes ao seguinte texto serão exibidas assim que a SAS for gerada:</span><span class="sxs-lookup"><span data-stu-id="9321e-165">Information similar to the following text is displayed once the SAS has been generated:</span></span>

        Container SAS token using stored access policy: sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="9321e-166">Salve o token da política SAS, o nome da conta de armazenamento e o nome do contêiner.</span><span class="sxs-lookup"><span data-stu-id="9321e-166">Save the SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="9321e-167">Esses valores são usados ao associar a conta de armazenamento com seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9321e-167">These values are used when associating the storage account with your HDInsight cluster.</span></span>

### <a name="create-a-stored-policy-and-sas-using-python"></a><span data-ttu-id="9321e-168">Criar uma política armazenada e uma SAS usando Python</span><span class="sxs-lookup"><span data-stu-id="9321e-168">Create a stored policy and SAS using Python</span></span>

1. <span data-ttu-id="9321e-169">Abra o arquivo SASToken.py e altere os valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="9321e-169">Open the SASToken.py file and change the following values:</span></span>

   * <span data-ttu-id="9321e-170">policy\_name: o nome a ser usado para a política armazenada que será criada.</span><span class="sxs-lookup"><span data-stu-id="9321e-170">policy\_name: The name to use for the stored policy to create.</span></span>

   * <span data-ttu-id="9321e-171">storage\_account\_name: o nome da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9321e-171">storage\_account\_name: The name of your storage account.</span></span>

   * <span data-ttu-id="9321e-172">storage\_account\_key: a chave da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9321e-172">storage\_account\_key: The key for the storage account.</span></span>

   * <span data-ttu-id="9321e-173">storage\_container\_: o contêiner na conta de armazenamento para o qual você deseja restringir o acesso.</span><span class="sxs-lookup"><span data-stu-id="9321e-173">storage\_container\_name: The container in the storage account that you want to restrict access to.</span></span>

   * <span data-ttu-id="9321e-174">example\_file\_path: o caminho para um arquivo que é carregado para o contêiner.</span><span class="sxs-lookup"><span data-stu-id="9321e-174">example\_file\_path: The path to a file that is uploaded to the container.</span></span>

2. <span data-ttu-id="9321e-175">Execute o script.</span><span class="sxs-lookup"><span data-stu-id="9321e-175">Run the script.</span></span> <span data-ttu-id="9321e-176">Isso exibirá o token SAS semelhante ao texto a seguir quando o script for concluído:</span><span class="sxs-lookup"><span data-stu-id="9321e-176">It displays the SAS token similar to the following text when the script completes:</span></span>

        sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="9321e-177">Salve o token da política SAS, o nome da conta de armazenamento e o nome do contêiner.</span><span class="sxs-lookup"><span data-stu-id="9321e-177">Save the SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="9321e-178">Esses valores são usados ao associar a conta de armazenamento com seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9321e-178">These values are used when associating the storage account with your HDInsight cluster.</span></span>

## <a name="use-the-sas-with-hdinsight"></a><span data-ttu-id="9321e-179">Usar a SAS com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="9321e-179">Use the SAS with HDInsight</span></span>

<span data-ttu-id="9321e-180">Ao criar um cluster HDInsight, você deverá especificar uma conta de armazenamento primária e, opcionalmente, poderá especificar contas de armazenamento adicionais.</span><span class="sxs-lookup"><span data-stu-id="9321e-180">When creating an HDInsight cluster, you must specify a primary storage account and you can optionally specify additional storage accounts.</span></span> <span data-ttu-id="9321e-181">Ambos os métodos de adição de armazenamento exigem acesso total às contas de armazenamento e aos contêineres usados.</span><span class="sxs-lookup"><span data-stu-id="9321e-181">Both of these methods of adding storage require full access to the storage accounts and containers that are used.</span></span>

<span data-ttu-id="9321e-182">Para usar uma Assinatura de Acesso Compartilhado para limitar o acesso a um contêiner, você deverá adicionar uma entrada personalizada para a configuração **core-site** do cluster.</span><span class="sxs-lookup"><span data-stu-id="9321e-182">To use a Shared Access Signature to limit access to a container, add a custom entry to the **core-site** configuration for the cluster.</span></span>

* <span data-ttu-id="9321e-183">Para os clusters HDInsight **baseados no Windows** ou **baseados em Linux**, você pode adicionar a entrada durante a criação do cluster usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9321e-183">For **Windows-based** or **Linux-based** HDInsight clusters, you can add the entry during cluster creation using PowerShell.</span></span>
* <span data-ttu-id="9321e-184">Para clusters HDInsight **baseados em Linux**, altere a configuração após a criação do cluster usando o Ambari.</span><span class="sxs-lookup"><span data-stu-id="9321e-184">For **Linux-based** HDInsight clusters, change the configuration after cluster creation using Ambari.</span></span>

### <a name="create-a-cluster-that-uses-the-sas"></a><span data-ttu-id="9321e-185">Criar um cluster que use a SAS</span><span class="sxs-lookup"><span data-stu-id="9321e-185">Create a cluster that uses the SAS</span></span>

<span data-ttu-id="9321e-186">Um exemplo de criação de um cluster HDInsight que use a SAS foi incluído no diretório `CreateCluster` do repositório.</span><span class="sxs-lookup"><span data-stu-id="9321e-186">An example of creating an HDInsight cluster that uses the SAS is included in the `CreateCluster` directory of the repository.</span></span> <span data-ttu-id="9321e-187">Para usá-lo, execute estas etapas:</span><span class="sxs-lookup"><span data-stu-id="9321e-187">To use it, use the following steps:</span></span>

1. <span data-ttu-id="9321e-188">Abra o arquivo `CreateCluster\HDInsightSAS.ps1` em um editor de texto e modifique os valores a seguir no início do documento.</span><span class="sxs-lookup"><span data-stu-id="9321e-188">Open the `CreateCluster\HDInsightSAS.ps1` file in a text editor and modify the following values at the beginning of the document.</span></span>

    ```powershell
    # Replace 'mycluster' with the name of the cluster to be created
    $clusterName = 'mycluster'
    # Valid values are 'Linux' and 'Windows'
    $osType = 'Linux'
    # Replace 'myresourcegroup' with the name of the group to be created
    $resourceGroupName = 'myresourcegroup'
    # Replace with the Azure data center you want to the cluster to live in
    $location = 'North Europe'
    # Replace with the name of the default storage account to be created
    $defaultStorageAccountName = 'mystorageaccount'
    # Replace with the name of the SAS container created earlier
    $SASContainerName = 'sascontainer'
    # Replace with the name of the SAS storage account created earlier
    $SASStorageAccountName = 'sasaccount'
    # Replace with the SAS token generated earlier
    $SASToken = 'sastoken'
    # Set the number of worker nodes in the cluster
    $clusterSizeInNodes = 3
    ```

    <span data-ttu-id="9321e-189">Por exemplo, altere `'mycluster'` para o nome do cluster que você deseja criar.</span><span class="sxs-lookup"><span data-stu-id="9321e-189">For example, change `'mycluster'` to the name of the cluster you want to create.</span></span> <span data-ttu-id="9321e-190">Os valores da SAS devem corresponder aos valores das etapas anteriores durante a criação de uma conta de armazenamento e de um token SAS.</span><span class="sxs-lookup"><span data-stu-id="9321e-190">The SAS values should match the values from the previous steps when creating a storage account and SAS token.</span></span>

    <span data-ttu-id="9321e-191">Depois de alterar os valores, salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="9321e-191">Once you have changed the values, save the file.</span></span>

2. <span data-ttu-id="9321e-192">Abra um novo prompt do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9321e-192">Open a new Azure PowerShell prompt.</span></span> <span data-ttu-id="9321e-193">Se você não estiver familiarizado com o Azure PowerShell ou se não o tiver instalado, consulte [Instalar e configurar o Azure PowerShell][powershell].</span><span class="sxs-lookup"><span data-stu-id="9321e-193">If you are unfamiliar with Azure PowerShell, or have not installed it, see [Install and configure Azure PowerShell][powershell].</span></span>

1. <span data-ttu-id="9321e-194">No prompt, use o seguinte comando para se autenticar em sua assinatura do Azure:</span><span class="sxs-lookup"><span data-stu-id="9321e-194">From the prompt, use the following command to authenticate to your Azure subscription:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="9321e-195">Quando solicitado, faça logon com a conta da sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="9321e-195">When prompted, log in with the account for your Azure subscription.</span></span>

    <span data-ttu-id="9321e-196">Se a conta estiver associada a várias assinaturas do Azure, talvez seja necessário utilizar `Select-AzureRmSubscription` para selecionar a assinatura que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="9321e-196">If your account is associated with multiple Azure subscriptions, you may need to use `Select-AzureRmSubscription` to select the subscription you wish to use.</span></span>

4. <span data-ttu-id="9321e-197">No prompt, altere os diretórios para o diretório `CreateCluster` que contém o arquivo HDInsightSAS.ps1.</span><span class="sxs-lookup"><span data-stu-id="9321e-197">From the prompt, change directories to the `CreateCluster` directory that contains the HDInsightSAS.ps1 file.</span></span> <span data-ttu-id="9321e-198">Em seguida, use o comando a seguir para executar o script</span><span class="sxs-lookup"><span data-stu-id="9321e-198">Then use the following command to run the script</span></span>

    ```powershell
    .\HDInsightSAS.ps1
    ```

    <span data-ttu-id="9321e-199">À medida que o script for executado, ele registrará a saída em log do prompt do PowerShell enquanto cria o grupo de recursos e as contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9321e-199">As the script runs, it logs output to the PowerShell prompt as it creates the resource group and storage accounts.</span></span> <span data-ttu-id="9321e-200">Ele solicitará que você insira o usuário HTTP para o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9321e-200">You are prompted to enter the HTTP user for the HDInsight cluster.</span></span> <span data-ttu-id="9321e-201">Essa conta é usada para proteger o acesso HTTP/s ao cluster.</span><span class="sxs-lookup"><span data-stu-id="9321e-201">This account is used to secure HTTP/s access to the cluster.</span></span>

    <span data-ttu-id="9321e-202">Se você estiver criando um cluster baseado em Linux, também será solicitado que você forneça um nome de conta de usuário SSH e uma senha.</span><span class="sxs-lookup"><span data-stu-id="9321e-202">If you are creating a Linux-based cluster, you are prompted for an SSH user account name and password.</span></span> <span data-ttu-id="9321e-203">Essa conta é usada para fazer logon remotamente no cluster.</span><span class="sxs-lookup"><span data-stu-id="9321e-203">This account is used to remotely log in to the cluster.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="9321e-204">Quando o nome de usuário ou a senha HTTP/s ou SSH forem solicitados, você deverá fornecer uma senha que atenda a estes critérios:</span><span class="sxs-lookup"><span data-stu-id="9321e-204">When prompted for the HTTP/s or SSH user name and password, you must provide a password that meets the following criteria:</span></span>
   >
   > * <span data-ttu-id="9321e-205">Deve ter pelo menos 10 caracteres de comprimento</span><span class="sxs-lookup"><span data-stu-id="9321e-205">Must be at least 10 characters in length</span></span>
   > * <span data-ttu-id="9321e-206">Deve conter pelo menos um dígito</span><span class="sxs-lookup"><span data-stu-id="9321e-206">Must contain at least one digit</span></span>
   > * <span data-ttu-id="9321e-207">Deve conter pelo menos um caractere não alfanumérico</span><span class="sxs-lookup"><span data-stu-id="9321e-207">Must contain at least one non-alphanumeric character</span></span>
   > * <span data-ttu-id="9321e-208">Deve conter pelo menos uma letra maiúscula ou minúscula</span><span class="sxs-lookup"><span data-stu-id="9321e-208">Must contain at least one upper or lower case letter</span></span>

<span data-ttu-id="9321e-209">Esse script demora um pouco para terminar, normalmente cerca de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="9321e-209">It takes a while for this script to complete, usually around 15 minutes.</span></span> <span data-ttu-id="9321e-210">Quando o script for concluído sem erros, o cluster terá sido criado.</span><span class="sxs-lookup"><span data-stu-id="9321e-210">When the script completes without any errors, the cluster has been created.</span></span>

### <a name="use-the-sas-with-an-existing-cluster"></a><span data-ttu-id="9321e-211">Usar a SAS com um cluster existente</span><span class="sxs-lookup"><span data-stu-id="9321e-211">Use the SAS with an existing cluster</span></span>

<span data-ttu-id="9321e-212">Se você tiver um cluster baseado em Linux existente, poderá adicionar a SAS à configuração **core-site** usando as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="9321e-212">If you have an existing Linux-based cluster, you can add the SAS to the **core-site** configuration by using the following steps:</span></span>

1. <span data-ttu-id="9321e-213">Abra a UI da Web do Ambari para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="9321e-213">Open the Ambari web UI for your cluster.</span></span> <span data-ttu-id="9321e-214">O endereço para essa página é https://YOURCLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="9321e-214">The address for this page is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="9321e-215">Quando solicitado, faça a autenticação no cluster usando o nome do administrador (admin) e a senha usados na criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="9321e-215">When prompted, authenticate to the cluster using the admin name (admin) and password you used when creating the cluster.</span></span>

2. <span data-ttu-id="9321e-216">No lado esquerdo da interface do usuário da Web do Ambari, escolha **HDFS** e selecione a guia **Configurações** na metade da página.</span><span class="sxs-lookup"><span data-stu-id="9321e-216">From the left side of the Ambari web UI, select **HDFS** and then select the **Configs** tab in the middle of the page.</span></span>

3. <span data-ttu-id="9321e-217">Selecione a guia **Avançado** e então role até encontrar a seção **Core-site personalizado**.</span><span class="sxs-lookup"><span data-stu-id="9321e-217">Select the **Advanced** tab, and then scroll until you find the **Custom core-site** section.</span></span>

4. <span data-ttu-id="9321e-218">Expanda a seção **Core-site personalizado**, role até o fim e escolha o link **Adicionar propriedade...**.</span><span class="sxs-lookup"><span data-stu-id="9321e-218">Expand the **Custom core-site** section, then scroll to the end and select the **Add property...** link.</span></span> <span data-ttu-id="9321e-219">Use os valores a seguir para os campos **Chave** e **Valor**:</span><span class="sxs-lookup"><span data-stu-id="9321e-219">Use the following values for the **Key** and **Value** fields:</span></span>

   * <span data-ttu-id="9321e-220">**Chave**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="9321e-220">**Key**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span></span>
   * <span data-ttu-id="9321e-221">**Valor**: a SAS retornada pelo aplicativo C# ou Python executado anteriormente</span><span class="sxs-lookup"><span data-stu-id="9321e-221">**Value**: The SAS returned by the C# or Python application you ran previously</span></span>

     <span data-ttu-id="9321e-222">Substitua **CONTAINERNAME** pelo nome do contêiner usado com o aplicativo C# ou SAS.</span><span class="sxs-lookup"><span data-stu-id="9321e-222">Replace **CONTAINERNAME** with the container name you used with the C# or SAS application.</span></span> <span data-ttu-id="9321e-223">Substitua **STORAGEACCOUNTNAME** pelo nome da conta de armazenamento usada.</span><span class="sxs-lookup"><span data-stu-id="9321e-223">Replace **STORAGEACCOUNTNAME** with the storage account name you used.</span></span>

5. <span data-ttu-id="9321e-224">Clique no botão **Adicionar** para salvar essa chave e esse valor e clique no botão **Salvar** para salvar as alterações de configuração.</span><span class="sxs-lookup"><span data-stu-id="9321e-224">Click the **Add** button to save this key and value, then click the **Save** button to save the configuration changes.</span></span> <span data-ttu-id="9321e-225">Quando solicitado, adicione uma descrição da alteração ("adicionando acesso de armazenamento SAS", por exemplo) e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="9321e-225">When prompted, add a description of the change ("adding SAS storage access" for example) and then click **Save**.</span></span>

    <span data-ttu-id="9321e-226">Clique em **OK** quando as alterações forem concluídas.</span><span class="sxs-lookup"><span data-stu-id="9321e-226">Click **OK** when the changes have been completed.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="9321e-227">Você deverá reiniciar vários serviços antes que a alteração entre em vigor.</span><span class="sxs-lookup"><span data-stu-id="9321e-227">You must restart several services before the change takes effect.</span></span>

6. <span data-ttu-id="9321e-228">Na IU da Web do Ambari, escolha **HDFS** na lista à esquerda e selecione **Reiniciar Todos** na lista suspensa **Ações de Serviço** à direita.</span><span class="sxs-lookup"><span data-stu-id="9321e-228">In the Ambari web UI, select **HDFS** from the list on the left, and then select **Restart All** from the **Service Actions** drop down list on the right.</span></span> <span data-ttu-id="9321e-229">Quando solicitado, selecione **Ativar o modo de manutenção** e selecione __Conforme Reiniciar Todos".</span><span class="sxs-lookup"><span data-stu-id="9321e-229">When prompted, select **Turn on maintenance mode** and then select __Conform Restart All".</span></span>

    <span data-ttu-id="9321e-230">Repita esse processo para MapReduce2 e YARN.</span><span class="sxs-lookup"><span data-stu-id="9321e-230">Repeat this process for MapReduce2 and YARN.</span></span>

7. <span data-ttu-id="9321e-231">Depois os serviços tiverem sido reiniciados, selecione cada uma e desabilite o modo de manutenção na lista suspensa **Ações de Serviço**.</span><span class="sxs-lookup"><span data-stu-id="9321e-231">Once the services have restarted, select each one and disable maintenance mode from the **Service Actions** drop down.</span></span>

## <a name="test-restricted-access"></a><span data-ttu-id="9321e-232">Testar o acesso restrito</span><span class="sxs-lookup"><span data-stu-id="9321e-232">Test restricted access</span></span>

<span data-ttu-id="9321e-233">Para verificar se você tem acesso restrito, use estes métodos:</span><span class="sxs-lookup"><span data-stu-id="9321e-233">To verify that you have restricted access, use the following methods:</span></span>

* <span data-ttu-id="9321e-234">Para clusters HDInsight **baseados no Windows** , use a Área de Trabalho Remota para se conectar ao cluster.</span><span class="sxs-lookup"><span data-stu-id="9321e-234">For **Windows-based** HDInsight clusters, use Remote Desktop to connect to the cluster.</span></span> <span data-ttu-id="9321e-235">Para obter mais informações, consulte [Conectar ao HDInsight usando RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="9321e-235">For more information, see [Connect to HDInsight using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

    <span data-ttu-id="9321e-236">Uma vez conectado, use o ícone **Linha de Comando do Hadoop** na área de trabalho para abrir um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="9321e-236">Once connected, use the **Hadoop Command-Line** icon on the desktop to open a command prompt.</span></span>

* <span data-ttu-id="9321e-237">Para clusters HDInsight **baseados em Linux** , use SSH para conectar-se ao cluster.</span><span class="sxs-lookup"><span data-stu-id="9321e-237">For **Linux-based** HDInsight clusters, use SSH to connect to the cluster.</span></span> <span data-ttu-id="9321e-238">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="9321e-238">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="9321e-239">Uma vez conectado ao cluster, use as etapas a seguir para verificar se você só pode ler e listar itens na conta de armazenamento SAS:</span><span class="sxs-lookup"><span data-stu-id="9321e-239">Once connected to the cluster, use the following steps to verify that you can only read and list items on the SAS storage account:</span></span>

1. <span data-ttu-id="9321e-240">Para listar o conteúdo do contêiner, use o seguinte comando no prompt:</span><span class="sxs-lookup"><span data-stu-id="9321e-240">To list the contents of the container, use the following command from the prompt:</span></span> 

    ```bash
    hdfs dfs -ls wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/
    ```

    <span data-ttu-id="9321e-241">Substitua **SASCONTAINER** pelo nome do contêiner criado para a conta de armazenamento SAS.</span><span class="sxs-lookup"><span data-stu-id="9321e-241">Replace **SASCONTAINER** with the name of the container created for the SAS storage account.</span></span> <span data-ttu-id="9321e-242">Substitua **SASACCOUNTNAME** pelo nome da conta de armazenamento usada para a SAS.</span><span class="sxs-lookup"><span data-stu-id="9321e-242">Replace **SASACCOUNTNAME** with the name of the storage account used for the SAS.</span></span>

    <span data-ttu-id="9321e-243">A lista inclui o arquivo carregado quando o contêiner e a SAS foram criados.</span><span class="sxs-lookup"><span data-stu-id="9321e-243">The list includes the file uploaded when the container and SAS were created.</span></span>

2. <span data-ttu-id="9321e-244">Use o comando a seguir para verificar se você pode ler o conteúdo do arquivo.</span><span class="sxs-lookup"><span data-stu-id="9321e-244">Use the following command to verify that you can read the contents of the file.</span></span> <span data-ttu-id="9321e-245">Substitua **SASCONTAINER** e **SASACCOUNTNAME** como na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="9321e-245">Replace the **SASCONTAINER** and **SASACCOUNTNAME** as in the previous step.</span></span> <span data-ttu-id="9321e-246">Substitua **FILENAME** pelo nome do arquivo exibido no comando anterior:</span><span class="sxs-lookup"><span data-stu-id="9321e-246">Replace **FILENAME** with the name of the file displayed in the previous command:</span></span>

    ```bash
    hdfs dfs -text wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME
    ```

    <span data-ttu-id="9321e-247">Esse comando lista o conteúdo do arquivo.</span><span class="sxs-lookup"><span data-stu-id="9321e-247">This command lists the contents of the file.</span></span>

3. <span data-ttu-id="9321e-248">Use o comando a seguir para baixar o arquivo para o sistema de arquivos local:</span><span class="sxs-lookup"><span data-stu-id="9321e-248">Use the following command to download the file to the local file system:</span></span>

    ```bash
    hdfs dfs -get wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME testfile.txt
    ```

    <span data-ttu-id="9321e-249">Esse comando baixa o arquivo para um arquivo local chamado **testfile.txt**.</span><span class="sxs-lookup"><span data-stu-id="9321e-249">This command downloads the file to a local file named **testfile.txt**.</span></span>

4. <span data-ttu-id="9321e-250">Use o comando a seguir para carregar o arquivo local para um novo arquivo chamado **testupload.txt** no armazenamento SAS:</span><span class="sxs-lookup"><span data-stu-id="9321e-250">Use the following command to upload the local file to a new file named **testupload.txt** on the SAS storage:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/testupload.txt
    ```

    <span data-ttu-id="9321e-251">Você receberá uma mensagem semelhante ao texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="9321e-251">You receive a message similar to the following text:</span></span>

        put: java.io.IOException

    <span data-ttu-id="9321e-252">Esse erro só ocorrerá porque o local do armazenamento é somente leitura+lista.</span><span class="sxs-lookup"><span data-stu-id="9321e-252">This error occurs because the storage location is read+list only.</span></span> <span data-ttu-id="9321e-253">Use o comando a para colocar os dados no armazenamento padrão do cluster, que pode ser gravável:</span><span class="sxs-lookup"><span data-stu-id="9321e-253">Use the following command to put the data on the default storage for the cluster, which is writable:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb:///testupload.txt
    ```

    <span data-ttu-id="9321e-254">Dessa vez, a operação deverá ser concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="9321e-254">This time, the operation should complete successfully.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="9321e-255">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="9321e-255">Troubleshooting</span></span>

### <a name="a-task-was-canceled"></a><span data-ttu-id="9321e-256">Uma tarefa foi cancelada</span><span class="sxs-lookup"><span data-stu-id="9321e-256">A task was canceled</span></span>

<span data-ttu-id="9321e-257">**Sintomas**: ao criar um cluster usando o script do PowerShell, talvez você receba a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="9321e-257">**Symptoms**: When creating a cluster using the PowerShell script, you may receive the following error message:</span></span>

    New-AzureRmHDInsightCluster : A task was canceled.
    At C:\Users\larryfr\Documents\GitHub\hdinsight-azure-storage-sas\CreateCluster\HDInsightSAS.ps1:62 char:5
    +     New-AzureRmHDInsightCluster `
    +     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (:) [New-AzureRmHDInsightCluster], CloudException
        + FullyQualifiedErrorId : Hyak.Common.CloudException,Microsoft.Azure.Commands.HDInsight.NewAzureHDInsightClusterCommand

<span data-ttu-id="9321e-258">**Causa**: esse erro poderá ocorrer se você usar uma senha para o usuário admin/HTTP do cluster ou, para clusters baseados em Linux, o usuário SSH.</span><span class="sxs-lookup"><span data-stu-id="9321e-258">**Cause**: This error can occur if you use a password for the admin/HTTP user for the cluster, or (for Linux-based clusters) the SSH user.</span></span>

<span data-ttu-id="9321e-259">**Resolução**: use uma senha que atenda aos seguintes critérios:</span><span class="sxs-lookup"><span data-stu-id="9321e-259">**Resolution**: Use a password that meets the following criteria:</span></span>

* <span data-ttu-id="9321e-260">Deve ter pelo menos 10 caracteres de comprimento</span><span class="sxs-lookup"><span data-stu-id="9321e-260">Must be at least 10 characters in length</span></span>
* <span data-ttu-id="9321e-261">Deve conter pelo menos um dígito</span><span class="sxs-lookup"><span data-stu-id="9321e-261">Must contain at least one digit</span></span>
* <span data-ttu-id="9321e-262">Deve conter pelo menos um caractere não alfanumérico</span><span class="sxs-lookup"><span data-stu-id="9321e-262">Must contain at least one non-alphanumeric character</span></span>
* <span data-ttu-id="9321e-263">Deve conter pelo menos uma letra maiúscula ou minúscula</span><span class="sxs-lookup"><span data-stu-id="9321e-263">Must contain at least one upper or lower case letter</span></span>

## <a name="next-steps"></a><span data-ttu-id="9321e-264">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9321e-264">Next steps</span></span>

<span data-ttu-id="9321e-265">Agora que você aprendeu a adicionar armazenamento de acesso limitado ao seu cluster HDInsight, conheça outras maneiras de trabalhar com dados no cluster:</span><span class="sxs-lookup"><span data-stu-id="9321e-265">Now that you have learned how to add limited-access storage to your HDInsight cluster, learn other ways to work with data on your cluster:</span></span>

* [<span data-ttu-id="9321e-266">Usar o Hive com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="9321e-266">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="9321e-267">Usar o Pig com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="9321e-267">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="9321e-268">Usar o MapReduce com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="9321e-268">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[powershell]: /powershell/azureps-cmdlets-docs
