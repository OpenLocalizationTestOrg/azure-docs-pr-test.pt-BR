---
title: Gerenciar conjuntos de registros DNS e registros com o DNS do Azure | Microsoft Docs
description: "O DNS do Azure fornece a capacidade de gerenciar registros e conjuntos de registros de DNS ao hospedar seu domínio."
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
ms.openlocfilehash: 001b80ccba43beab44f6a598f820df65a85a345f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-dns-records-and-record-sets-by-using-the-azure-portal"></a><span data-ttu-id="8aeab-103">Gerenciar registros e conjuntos de registros DNS usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8aeab-103">Manage DNS records and record sets by using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8aeab-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8aeab-104">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="8aeab-105">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="8aeab-105">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="8aeab-106">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="8aeab-106">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="8aeab-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8aeab-107">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="8aeab-108">Este artigo mostra como gerenciar registros e conjuntos de registros da zona DNS usando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8aeab-108">This article shows you how to manage record sets and records for your DNS zone by using the Azure portal.</span></span>

<span data-ttu-id="8aeab-109">É importante compreender a diferença entre os conjuntos de registros DNS e registros DNS individuais.</span><span class="sxs-lookup"><span data-stu-id="8aeab-109">It's important to understand the difference between DNS record sets and individual DNS records.</span></span> <span data-ttu-id="8aeab-110">Um conjunto de registros é uma coleção de registros em uma zona que tem o mesmo nome e o mesmo tipo.</span><span class="sxs-lookup"><span data-stu-id="8aeab-110">A record set is a collection of records in a zone that have the same name and are the same type.</span></span> <span data-ttu-id="8aeab-111">Para obter mais informações, veja [Criar registros e conjuntos de registros DNS usando o portal do Azure](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8aeab-111">For more information, see [Create DNS record sets and records by using the Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="create-a-new-record-set-and-record"></a><span data-ttu-id="8aeab-112">Criar registro e um novo conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="8aeab-112">Create a new record set and record</span></span>

<span data-ttu-id="8aeab-113">Para criar um conjunto de registros no portal do Azure, veja [Create DNS records using the Azure portal](dns-getstarted-create-recordset-portal.md)(Criar registros DNS usando o Portal do Azure).</span><span class="sxs-lookup"><span data-stu-id="8aeab-113">To create a record set in the Azure portal, see [Create DNS records by using the Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="view-a-record-set"></a><span data-ttu-id="8aeab-114">Exibir um conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="8aeab-114">View a record set</span></span>

1. <span data-ttu-id="8aeab-115">No portal do Azure, vá para a folha **Zona DNS** .</span><span class="sxs-lookup"><span data-stu-id="8aeab-115">In the Azure portal, go to the **DNS zone** blade.</span></span>
2. <span data-ttu-id="8aeab-116">Procure o conjunto de registros e selecione-o.</span><span class="sxs-lookup"><span data-stu-id="8aeab-116">Search for the record set and select it.</span></span> <span data-ttu-id="8aeab-117">Isso abrirá as propriedades do conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="8aeab-117">This opens the record set properties.</span></span>

    ![Pesquisar um conjunto de registros](./media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-to-a-record-set"></a><span data-ttu-id="8aeab-119">Adicionar um novo registro a um conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="8aeab-119">Add a new record to a record set</span></span>

<span data-ttu-id="8aeab-120">Você pode adicionar até 20 registros em qualquer conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="8aeab-120">You can add up to 20 records to any record set.</span></span> <span data-ttu-id="8aeab-121">Um conjunto de registros não pode conter dois registros idênticos.</span><span class="sxs-lookup"><span data-stu-id="8aeab-121">A record set cannot contain two identical records.</span></span> <span data-ttu-id="8aeab-122">Conjuntos de registros vazios (sem nenhum registro) podem ser criados, mas não aparecem nos servidores de nome DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="8aeab-122">Empty record sets (with zero records) can be created, but do not appear on the Azure DNS name servers.</span></span> <span data-ttu-id="8aeab-123">Os conjuntos de registros do tipo CNAME podem conter, no máximo, um registro.</span><span class="sxs-lookup"><span data-stu-id="8aeab-123">Record sets of type CNAME can contain one record at most.</span></span>

1. <span data-ttu-id="8aeab-124">Na folha **Propriedades do conjunto de registros** da zona DNS, clique no conjunto de registros ao qual você quer adicionar um registro.</span><span class="sxs-lookup"><span data-stu-id="8aeab-124">On the **Record set properties** blade for your DNS zone, click the record set that you want to add a record to.</span></span>

    ![Selecionar um conjunto de registros](./media/dns-operations-recordsets-portal/selectset500.png)

2. <span data-ttu-id="8aeab-126">Especifique as configurações do conjunto de registros preenchendo os campos.</span><span class="sxs-lookup"><span data-stu-id="8aeab-126">Specify the record set properties by filling in the fields.</span></span>

    ![Adicionar um registro](./media/dns-operations-recordsets-portal/addrecord500.png)

3. <span data-ttu-id="8aeab-128">Clique em **Salvar** na parte superior da folha para salvar as configurações.</span><span class="sxs-lookup"><span data-stu-id="8aeab-128">Click **Save** at the top of the blade to save your settings.</span></span> <span data-ttu-id="8aeab-129">Em seguida, feche a folha.</span><span class="sxs-lookup"><span data-stu-id="8aeab-129">Then close the blade.</span></span>
4. <span data-ttu-id="8aeab-130">No canto, você verá que o registro está sendo salvo.</span><span class="sxs-lookup"><span data-stu-id="8aeab-130">In the corner, you will see that the record is saving.</span></span>

    ![Salvando o conjunto de registros](./media/dns-operations-recordsets-portal/saving150.png)

<span data-ttu-id="8aeab-132">Assim que o registro for salvo, os valores da folha **Zona DNS** refletirão o novo registro.</span><span class="sxs-lookup"><span data-stu-id="8aeab-132">After the record has been saved, the values on the **DNS zone** blade will reflect the new record.</span></span>

## <a name="update-a-record"></a><span data-ttu-id="8aeab-133">Atualizar um registro</span><span class="sxs-lookup"><span data-stu-id="8aeab-133">Update a record</span></span>

<span data-ttu-id="8aeab-134">Ao atualizar um registro em um conjunto de registros existente, os campos disponíveis que poderão ser atualizados dependem do tipo de registro com o qual você está trabalhando.</span><span class="sxs-lookup"><span data-stu-id="8aeab-134">When you update a record in an existing record set, the fields you can update depend on the type of record you're working with.</span></span>

1. <span data-ttu-id="8aeab-135">Na folha **Propriedades do conjunto de registros** do conjunto de registros, procure o registro.</span><span class="sxs-lookup"><span data-stu-id="8aeab-135">On the **Record set properties** blade for your record set, search for the record.</span></span>
2. <span data-ttu-id="8aeab-136">Modifique o registro.</span><span class="sxs-lookup"><span data-stu-id="8aeab-136">Modify the record.</span></span> <span data-ttu-id="8aeab-137">Quando você modifica um registro, é possível alterar suas configurações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="8aeab-137">When you modify a record, you can change the available settings for the record.</span></span> <span data-ttu-id="8aeab-138">No exemplo a seguir, o campo **endereço IP** é selecionado e o endereço IP está sendo modificado.</span><span class="sxs-lookup"><span data-stu-id="8aeab-138">In the following example, the **IP address** field is selected, and the IP address is in the process of being modified.</span></span>

    ![Modificar um registro](./media/dns-operations-recordsets-portal/modifyrecord500.png)

3. <span data-ttu-id="8aeab-140">Clique em **Salvar** na parte superior da folha para salvar as configurações.</span><span class="sxs-lookup"><span data-stu-id="8aeab-140">Click **Save** at the top of the blade to save your settings.</span></span> <span data-ttu-id="8aeab-141">No canto superior direito, você verá a notificação informando que o registro foi salvo.</span><span class="sxs-lookup"><span data-stu-id="8aeab-141">In the upper right corner, you'll see the notification that the record has been saved.</span></span>

    ![Conjunto de registros salvo](./media/dns-operations-recordsets-portal/saved150.png)

<span data-ttu-id="8aeab-143">Assim que o registro for salvo, os valores do conjunto de registros na folha **Zona DNS** refletirão o registro atualizado.</span><span class="sxs-lookup"><span data-stu-id="8aeab-143">After the record has been saved, the values for the record set on the **DNS zone** blade will reflect the updated record.</span></span>

## <a name="remove-a-record-from-a-record-set"></a><span data-ttu-id="8aeab-144">Remover um registro de um conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="8aeab-144">Remove a record from a record set</span></span>

<span data-ttu-id="8aeab-145">Você pode usar o Portal do Azure para remover registros de um conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="8aeab-145">You can use the Azure portal to remove records from a record set.</span></span> <span data-ttu-id="8aeab-146">Observe que remover o último registro de um conjunto de registros não exclui o conjunto.</span><span class="sxs-lookup"><span data-stu-id="8aeab-146">Note that removing the last record from a record set does not delete the record set.</span></span>

1. <span data-ttu-id="8aeab-147">Na folha **Propriedades do conjunto de registros** do conjunto de registros, procure o registro.</span><span class="sxs-lookup"><span data-stu-id="8aeab-147">On the **Record set properties** blade for your record set, search for the record.</span></span>
2. <span data-ttu-id="8aeab-148">Clique no registro que você quer remover.</span><span class="sxs-lookup"><span data-stu-id="8aeab-148">Click the record that you want to remove.</span></span> <span data-ttu-id="8aeab-149">Em seguida, selecione **Remover**.</span><span class="sxs-lookup"><span data-stu-id="8aeab-149">Then select **Remove**.</span></span>

    ![Remover um registro](./media/dns-operations-recordsets-portal/removerecord500.png)

3. <span data-ttu-id="8aeab-151">Clique em **Salvar** na parte superior da folha para salvar as configurações.</span><span class="sxs-lookup"><span data-stu-id="8aeab-151">Click **Save** at the top of the blade to save your settings.</span></span>
4. <span data-ttu-id="8aeab-152">Assim que o registro for removido, os valores do registro na folha **Zona DNS** refletirão a remoção.</span><span class="sxs-lookup"><span data-stu-id="8aeab-152">After the record has been removed, the values for the record on the **DNS zone** blade will reflect the removal.</span></span>

## <span data-ttu-id="8aeab-153"><a name="delete"></a>Excluir um conjunto de registros</span><span class="sxs-lookup"><span data-stu-id="8aeab-153"><a name="delete"></a>Delete a record set</span></span>

1. <span data-ttu-id="8aeab-154">Na folha **Propriedades do conjunto de registros**do conjunto de registros, clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="8aeab-154">On the **Record set properties** blade for your record set, click **Delete**.</span></span>

    ![Excluir um conjunto de registros](./media/dns-operations-recordsets-portal/deleterecordset500.png)

2. <span data-ttu-id="8aeab-156">Será exibida uma mensagem perguntando se você deseja excluir o conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="8aeab-156">A message appears asking if you want to delete the record set.</span></span>
3. <span data-ttu-id="8aeab-157">Verifique se o nome corresponde ao conjunto de registros que você quer excluir e clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="8aeab-157">Verify that the name matches the record set that you want to delete, and then click **Yes**.</span></span>
4. <span data-ttu-id="8aeab-158">Na folha **Zona DNS** , você poderá verificar que o conjunto de registros não está mais visível.</span><span class="sxs-lookup"><span data-stu-id="8aeab-158">On the **DNS zone** blade, verify that the record set is no longer visible.</span></span>

## <a name="work-with-ns-and-soa-records"></a><span data-ttu-id="8aeab-159">Trabalhar com registros NS e SOA</span><span class="sxs-lookup"><span data-stu-id="8aeab-159">Work with NS and SOA records</span></span>

<span data-ttu-id="8aeab-160">Os registros NS e SOA que são criados automaticamente são gerenciados de modo diferente de outros tipos de registro.</span><span class="sxs-lookup"><span data-stu-id="8aeab-160">NS and SOA records that are automatically created are managed differently from other record types.</span></span>

### <a name="modify-soa-records"></a><span data-ttu-id="8aeab-161">Modificar registros SOA</span><span class="sxs-lookup"><span data-stu-id="8aeab-161">Modify SOA records</span></span>

<span data-ttu-id="8aeab-162">Não é possível adicionar nem remover registros no conjunto de registros SOA criados automaticamente no apex da zona (nome = "@").</span><span class="sxs-lookup"><span data-stu-id="8aeab-162">You cannot add or remove records from the automatically created SOA record set at the zone apex (name = "@").</span></span> <span data-ttu-id="8aeab-163">No entanto, é possível modificar qualquer um dos parâmetros no registro SOA (exceto o “Host”) e o TTL do conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="8aeab-163">However, you can modify any of the parameters within the SOA record (except "Host") and the record set TTL.</span></span>

### <a name="modify-ns-records-at-the-zone-apex"></a><span data-ttu-id="8aeab-164">Modificar registros NS no apex da zona</span><span class="sxs-lookup"><span data-stu-id="8aeab-164">Modify NS records at the zone apex</span></span>

<span data-ttu-id="8aeab-165">O registro NS definido no apex da zona é criado automaticamente com cada zona DNS.</span><span class="sxs-lookup"><span data-stu-id="8aeab-165">The NS record set at the zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="8aeab-166">Ele contém os nomes dos servidores de nome DNS do Azure atribuídos à zona.</span><span class="sxs-lookup"><span data-stu-id="8aeab-166">It contains the names of the Azure DNS name servers assigned to the zone.</span></span>

<span data-ttu-id="8aeab-167">Você pode adicionar servidores de nome adicionais a esse conjunto de registros NS para dar suporte à co-hospedagem de domínios com mais de um provedor DNS.</span><span class="sxs-lookup"><span data-stu-id="8aeab-167">You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="8aeab-168">Você também pode modificar o TTL e os metadados para esse conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="8aeab-168">You can also modify the TTL and metadata for this record set.</span></span> <span data-ttu-id="8aeab-169">No entanto, você não pode remover nem modificar os servidores de nome DNS do Azure previamente populados.</span><span class="sxs-lookup"><span data-stu-id="8aeab-169">However, you cannot remove or modify the pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="8aeab-170">Observe que isso se aplica somente ao conjunto de registros NS definido no apex da zona.</span><span class="sxs-lookup"><span data-stu-id="8aeab-170">Note that this applies only to the NS record set at the zone apex.</span></span> <span data-ttu-id="8aeab-171">Outros conjuntos de registros NS na sua zona (conforme utilizados para delegar zonas filho) podem ser modificados sem restrição.</span><span class="sxs-lookup"><span data-stu-id="8aeab-171">Other NS record sets in your zone (as used to delegate child zones) can be modified without constraint.</span></span>

### <a name="delete-soa-or-ns-record-sets"></a><span data-ttu-id="8aeab-172">Excluir conjuntos de registros SOA ou NS</span><span class="sxs-lookup"><span data-stu-id="8aeab-172">Delete SOA or NS record sets</span></span>

<span data-ttu-id="8aeab-173">Não é possível excluir os conjuntos de registros SOA e NS no apex da zona (nome = "@") criados automaticamente quando a zona é criada.</span><span class="sxs-lookup"><span data-stu-id="8aeab-173">You cannot delete the SOA and NS record sets at the zone apex (name = "@") that are created automatically when the zone is created.</span></span> <span data-ttu-id="8aeab-174">Eles são excluídos automaticamente ao excluir a zona.</span><span class="sxs-lookup"><span data-stu-id="8aeab-174">They are deleted automatically when you delete the zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8aeab-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8aeab-175">Next steps</span></span>

* <span data-ttu-id="8aeab-176">Para obter mais informações sobre o DNS do Azure, confira [Visão geral do DNS do Azure](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8aeab-176">For more information about Azure DNS, see the [Azure DNS overview](dns-overview.md).</span></span>
* <span data-ttu-id="8aeab-177">Para obter mais informações sobre como automatizar o DNS, confira [Criando zonas DNS e conjuntos de registros usando o SDK do .NET](dns-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="8aeab-177">For more information about automating DNS, see [Creating DNS zones and record sets using the .NET SDK](dns-sdk.md).</span></span>
* <span data-ttu-id="8aeab-178">Para saber mais sobre os registros DNS reversos, veja [Visão geral de DNS reverso e suporte no Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8aeab-178">For more information about reverse DNS records, see [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>
