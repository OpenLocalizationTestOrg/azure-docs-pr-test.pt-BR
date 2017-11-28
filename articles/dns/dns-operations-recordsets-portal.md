---
title: aaaManage DNS registram conjuntos e registros de DNS do Azure | Microsoft Docs
description: "DNS do Azure fornece o registro DNS do hello recurso toomanage define e registra ao hospedar seu domínio."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ed44a1-7bfe-454f-964e-922ad978264a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 2e62d017341589eaf8d1f8df2fe5db4b973381d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-record-sets-by-using-hello-azure-portal"></a><span data-ttu-id="ecbf4-103">Gerenciar registros de DNS e conjuntos de registros usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ecbf4-103">Manage DNS records and record sets by using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ecbf4-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ecbf4-104">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="ecbf4-105">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="ecbf4-105">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="ecbf4-106">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="ecbf4-106">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="ecbf4-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ecbf4-107">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="ecbf4-108">Este artigo mostra como toomanage conjuntos de registros e os registros para a zona DNS usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-108">This article shows you how toomanage record sets and records for your DNS zone by using hello Azure portal.</span></span>

<span data-ttu-id="ecbf4-109">É importante toounderstand diferença de saudação entre conjuntos de registros de DNS e registros DNS individuais.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-109">It's important toounderstand hello difference between DNS record sets and individual DNS records.</span></span> <span data-ttu-id="ecbf4-110">Um conjunto de registros é uma coleção de registros em uma zona ter Olá mesmo nome e são Olá mesmo tipo.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-110">A record set is a collection of records in a zone that have hello same name and are hello same type.</span></span> <span data-ttu-id="ecbf4-111">Para obter mais informações, consulte [registros usando e conjuntos de registros de DNS criar hello portal do Azure](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ecbf4-111">For more information, see [Create DNS record sets and records by using hello Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="create-a-new-record-set-and-record"></a><span data-ttu-id="ecbf4-112">Criar registro e um novo conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="ecbf4-112">Create a new record set and record</span></span>

<span data-ttu-id="ecbf4-113">toocreate um conjunto de registros em Olá portal do Azure, consulte [Olá de registros de DNS criar usando o portal do Azure](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ecbf4-113">toocreate a record set in hello Azure portal, see [Create DNS records by using hello Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="view-a-record-set"></a><span data-ttu-id="ecbf4-114">Exibir um conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="ecbf4-114">View a record set</span></span>

1. <span data-ttu-id="ecbf4-115">No portal do Azure de Olá, vá toohello **zona DNS** folha.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-115">In hello Azure portal, go toohello **DNS zone** blade.</span></span>
2. <span data-ttu-id="ecbf4-116">Pesquisar o conjunto de registros hello e selecioná-lo.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-116">Search for hello record set and select it.</span></span> <span data-ttu-id="ecbf4-117">Isso abre as propriedades de conjunto de registros de saudação.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-117">This opens hello record set properties.</span></span>

    ![Pesquisar um conjunto de registros](./media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-tooa-record-set"></a><span data-ttu-id="ecbf4-119">Adicionar um novo conjunto de registros de registro tooa</span><span class="sxs-lookup"><span data-stu-id="ecbf4-119">Add a new record tooa record set</span></span>

<span data-ttu-id="ecbf4-120">Você pode adicionar o conjunto de registros too20 registros tooany.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-120">You can add up too20 records tooany record set.</span></span> <span data-ttu-id="ecbf4-121">Um conjunto de registros não pode conter dois registros idênticos.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-121">A record set cannot contain two identical records.</span></span> <span data-ttu-id="ecbf4-122">Conjuntos de registros vazios (com zero registros) podem ser criados, mas não aparecem nos servidores de nome DNS do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-122">Empty record sets (with zero records) can be created, but do not appear on hello Azure DNS name servers.</span></span> <span data-ttu-id="ecbf4-123">Os conjuntos de registros do tipo CNAME podem conter, no máximo, um registro.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-123">Record sets of type CNAME can contain one record at most.</span></span>

1. <span data-ttu-id="ecbf4-124">Em Olá **propriedades de conjunto de registros** folha para a zona DNS, clique em registro Olá definido que deseja tooadd um registro.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-124">On hello **Record set properties** blade for your DNS zone, click hello record set that you want tooadd a record to.</span></span>

    ![Selecionar um conjunto de registros](./media/dns-operations-recordsets-portal/selectset500.png)

2. <span data-ttu-id="ecbf4-126">Especifica propriedades de conjunto de registros de saudação preenchendo os campos de saudação.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-126">Specify hello record set properties by filling in hello fields.</span></span>

    ![Adicionar um registro](./media/dns-operations-recordsets-portal/addrecord500.png)

3. <span data-ttu-id="ecbf4-128">Clique em **salvar** em Olá superior da saudação folha toosave suas configurações.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-128">Click **Save** at hello top of hello blade toosave your settings.</span></span> <span data-ttu-id="ecbf4-129">Em seguida, feche a folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-129">Then close hello blade.</span></span>
4. <span data-ttu-id="ecbf4-130">Canto hello, você verá que está salvando o registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-130">In hello corner, you will see that hello record is saving.</span></span>

    ![Salvando o conjunto de registros](./media/dns-operations-recordsets-portal/saving150.png)

<span data-ttu-id="ecbf4-132">Depois que o registro Olá foi salvo, Olá valores hello **zona DNS** folha refletirá o novo registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-132">After hello record has been saved, hello values on hello **DNS zone** blade will reflect hello new record.</span></span>

## <a name="update-a-record"></a><span data-ttu-id="ecbf4-133">Atualizar um registro</span><span class="sxs-lookup"><span data-stu-id="ecbf4-133">Update a record</span></span>

<span data-ttu-id="ecbf4-134">Quando você atualiza um registro em um conjunto de registros existente, campos de saudação, que você pode atualizar dependem do tipo de saudação do registro que o estiver trabalhando com.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-134">When you update a record in an existing record set, hello fields you can update depend on hello type of record you're working with.</span></span>

1. <span data-ttu-id="ecbf4-135">Em Olá **propriedades de conjunto de registros** folha para seu conjunto de registros, pesquise o registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-135">On hello **Record set properties** blade for your record set, search for hello record.</span></span>
2. <span data-ttu-id="ecbf4-136">Modificar o registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-136">Modify hello record.</span></span> <span data-ttu-id="ecbf4-137">Quando você modifica um registro, você pode alterar configurações disponíveis de saudação para registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-137">When you modify a record, you can change hello available settings for hello record.</span></span> <span data-ttu-id="ecbf4-138">Em Olá exemplo a seguir, Olá **endereço IP** campo é selecionado, e o endereço IP de saudação está no processo de saudação do que está sendo modificado.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-138">In hello following example, hello **IP address** field is selected, and hello IP address is in hello process of being modified.</span></span>

    ![Modificar um registro](./media/dns-operations-recordsets-portal/modifyrecord500.png)

3. <span data-ttu-id="ecbf4-140">Clique em **salvar** em Olá superior da saudação folha toosave suas configurações.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-140">Click **Save** at hello top of hello blade toosave your settings.</span></span> <span data-ttu-id="ecbf4-141">Olá no canto superior direito, você verá a notificação de Olá Olá registro foi salvo.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-141">In hello upper right corner, you'll see hello notification that hello record has been saved.</span></span>

    ![Conjunto de registros salvo](./media/dns-operations-recordsets-portal/saved150.png)

<span data-ttu-id="ecbf4-143">Olá registro foi salvo, os valores de saudação para registro de saudação definidos em Olá **zona DNS** folha refletirá registro Olá atualizado.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-143">After hello record has been saved, hello values for hello record set on hello **DNS zone** blade will reflect hello updated record.</span></span>

## <a name="remove-a-record-from-a-record-set"></a><span data-ttu-id="ecbf4-144">Remover um registro de um conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="ecbf4-144">Remove a record from a record set</span></span>

<span data-ttu-id="ecbf4-145">Você pode usar os registros Olá tooremove portal do Azure de um conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-145">You can use hello Azure portal tooremove records from a record set.</span></span> <span data-ttu-id="ecbf4-146">Observe que a remover o último registro de saudação de um conjunto de registros não exclui o conjunto de registros de saudação.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-146">Note that removing hello last record from a record set does not delete hello record set.</span></span>

1. <span data-ttu-id="ecbf4-147">Em Olá **propriedades de conjunto de registros** folha para seu conjunto de registros, pesquise o registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-147">On hello **Record set properties** blade for your record set, search for hello record.</span></span>
2. <span data-ttu-id="ecbf4-148">Clique em registro Olá que você deseja tooremove.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-148">Click hello record that you want tooremove.</span></span> <span data-ttu-id="ecbf4-149">Em seguida, selecione **Remover**.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-149">Then select **Remove**.</span></span>

    ![Remover um registro](./media/dns-operations-recordsets-portal/removerecord500.png)

3. <span data-ttu-id="ecbf4-151">Clique em **salvar** em Olá superior da saudação folha toosave suas configurações.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-151">Click **Save** at hello top of hello blade toosave your settings.</span></span>
4. <span data-ttu-id="ecbf4-152">Após a remoção do registro hello, Olá valores de registro de saudação em Olá **zona DNS** folha refletirá a remoção de saudação.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-152">After hello record has been removed, hello values for hello record on hello **DNS zone** blade will reflect hello removal.</span></span>

## <span data-ttu-id="ecbf4-153"><a name="delete"></a>Excluir um conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="ecbf4-153"><a name="delete"></a>Delete a record set</span></span>

1. <span data-ttu-id="ecbf4-154">Em Olá **propriedades de conjunto de registros** folha para seu conjunto de registros, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-154">On hello **Record set properties** blade for your record set, click **Delete**.</span></span>

    ![Excluir um conjunto de registros](./media/dns-operations-recordsets-portal/deleterecordset500.png)

2. <span data-ttu-id="ecbf4-156">Uma mensagem aparece perguntando se você quiser que o conjunto de registros toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-156">A message appears asking if you want toodelete hello record set.</span></span>
3. <span data-ttu-id="ecbf4-157">Verifique se o conjunto de registros de Olá Olá nome corresponde ao que você deseja toodelete e, em seguida, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-157">Verify that hello name matches hello record set that you want toodelete, and then click **Yes**.</span></span>
4. <span data-ttu-id="ecbf4-158">Em Olá **zona DNS** folha, verifique se que o conjunto de registros Olá não está mais visível.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-158">On hello **DNS zone** blade, verify that hello record set is no longer visible.</span></span>

## <a name="work-with-ns-and-soa-records"></a><span data-ttu-id="ecbf4-159">Trabalhar com registros NS e SOA</span><span class="sxs-lookup"><span data-stu-id="ecbf4-159">Work with NS and SOA records</span></span>

<span data-ttu-id="ecbf4-160">Os registros NS e SOA que são criados automaticamente são gerenciados de modo diferente de outros tipos de registro.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-160">NS and SOA records that are automatically created are managed differently from other record types.</span></span>

### <a name="modify-soa-records"></a><span data-ttu-id="ecbf4-161">Modificar registros SOA</span><span class="sxs-lookup"><span data-stu-id="ecbf4-161">Modify SOA records</span></span>

<span data-ttu-id="ecbf4-162">Você não pode adicionar ou remover registros da saudação criado automaticamente o registro SOA definido no ápice da zona de saudação (nome = "@").</span><span class="sxs-lookup"><span data-stu-id="ecbf4-162">You cannot add or remove records from hello automatically created SOA record set at hello zone apex (name = "@").</span></span> <span data-ttu-id="ecbf4-163">No entanto, você pode modificar qualquer um dos parâmetros de saudação em Olá registro SOA (exceto "Host") e registro Olá definir o TTL.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-163">However, you can modify any of hello parameters within hello SOA record (except "Host") and hello record set TTL.</span></span>

### <a name="modify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="ecbf4-164">Modificar os registros no ápice da zona de saudação NS</span><span class="sxs-lookup"><span data-stu-id="ecbf4-164">Modify NS records at hello zone apex</span></span>

<span data-ttu-id="ecbf4-165">registro de NS Olá definido no ápice da zona de saudação é criado automaticamente com cada zona DNS.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-165">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="ecbf4-166">Ela contém nomes de saudação da zona do hello Azure DNS nome servidores toohello atribuído.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-166">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="ecbf4-167">Você pode adicionar nome adicionais servidores toothis NS conjunto de registros, toosupport co-hospedagem domínios com mais de um provedor DNS.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-167">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="ecbf4-168">Você também pode modificar hello TTL e metadados para esse conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-168">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="ecbf4-169">No entanto, você não pode remover ou modificar servidores de nome DNS do Azure preenchidos previamente hello.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-169">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="ecbf4-170">Observe que isso se aplica apenas toohello NS conjunto de registros no ápice da zona de saudação.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-170">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="ecbf4-171">Outros conjuntos de registros NS na zona (como zonas de filho usado toodelegate) podem ser modificados sem restrição.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-171">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

### <a name="delete-soa-or-ns-record-sets"></a><span data-ttu-id="ecbf4-172">Excluir conjuntos de registros SOA ou NS</span><span class="sxs-lookup"><span data-stu-id="ecbf4-172">Delete SOA or NS record sets</span></span>

<span data-ttu-id="ecbf4-173">Você não pode excluir Olá SOA e NS conjuntos de registros no ápice da zona de saudação (nome = "@") que são criadas automaticamente quando a zona de saudação é criada.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-173">You cannot delete hello SOA and NS record sets at hello zone apex (name = "@") that are created automatically when hello zone is created.</span></span> <span data-ttu-id="ecbf4-174">Eles são excluídos automaticamente quando você excluir a zona de saudação.</span><span class="sxs-lookup"><span data-stu-id="ecbf4-174">They are deleted automatically when you delete hello zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ecbf4-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ecbf4-175">Next steps</span></span>

* <span data-ttu-id="ecbf4-176">Para obter mais informações sobre DNS do Azure, consulte Olá [visão geral do DNS do Azure](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ecbf4-176">For more information about Azure DNS, see hello [Azure DNS overview](dns-overview.md).</span></span>
* <span data-ttu-id="ecbf4-177">Para obter mais informações sobre como automatizar o DNS, consulte [zonas DNS criando e usando conjuntos de registros Olá .NET SDK](dns-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="ecbf4-177">For more information about automating DNS, see [Creating DNS zones and record sets using hello .NET SDK](dns-sdk.md).</span></span>
* <span data-ttu-id="ecbf4-178">Para saber mais sobre os registros DNS reversos, veja [Visão geral de DNS reverso e suporte no Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ecbf4-178">For more information about reverse DNS records, see [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>
