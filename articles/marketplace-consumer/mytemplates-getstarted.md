---
title: aaaGet iniciado com modelos privados | Microsoft Docs
description: "Adicionar, gerenciar e compartilhar seus modelos privados usando Olá portal do Azure, a saudação CLI do Azure ou o PowerShell."
services: marketplace-customer
documentationcenter: 
author: VybavaRamadoss
manager: asimm
editor: 
tags: marketplace, azure-resource-manager
keywords: 
ms.assetid: 6ec20778-b578-4885-acb5-104b0e51ea1a
ms.service: marketplace
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: vybavar
ms.openlocfilehash: 1fe2c6422f62a98f7ae9ba5c61b9639d993f0bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-private-templates-on-hello-azure-portal"></a><span data-ttu-id="c61ea-103">Introdução ao privada modelos em Olá Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c61ea-103">Get started with private Templates on hello Azure Portal</span></span>
<span data-ttu-id="c61ea-104">Um [do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) modelo é um modelo declarativo usado toodefine sua implantação.</span><span class="sxs-lookup"><span data-stu-id="c61ea-104">An [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) template is a declarative template used toodefine your deployment.</span></span> <span data-ttu-id="c61ea-105">Você pode definir Olá toodeploy de recursos para uma solução e especifique os parâmetros e variáveis que permitem valores tooinput para ambientes diferentes.</span><span class="sxs-lookup"><span data-stu-id="c61ea-105">You can define hello resources toodeploy for a solution, and specify parameters and variables that enable you tooinput values for different environments.</span></span> <span data-ttu-id="c61ea-106">Olá modelo consiste em JSON e expressões que você pode usar valores de tooconstruct para sua implantação.</span><span class="sxs-lookup"><span data-stu-id="c61ea-106">hello template consists of JSON and expressions which you can use tooconstruct values for your deployment.</span></span>

<span data-ttu-id="c61ea-107">Você pode usar o hello novo **modelos** recurso Olá [Portal do Azure](https://portal.azure.com) juntamente com hello **Microsoft.Gallery** provedor de recursos como uma extensão de saudação [ Azure Marketplace](https://azure.microsoft.com/marketplace/) tooenable toocreate de usuários, gerenciar e implantar modelos privados de uma biblioteca de pessoal.</span><span class="sxs-lookup"><span data-stu-id="c61ea-107">You can use hello new **Templates** capability in hello [Azure Portal](https://portal.azure.com) along with hello **Microsoft.Gallery** resource provider as an extension of hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) tooenable users toocreate, manage and deploy private templates from a personal library.</span></span>

<span data-ttu-id="c61ea-108">Este documento orienta você por meio de adicionar, gerenciar e compartilhar uma particular **modelo** usando Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c61ea-108">This document walks you through adding, managing and sharing a private **Template** using hello Azure Portal.</span></span>

## <a name="guidance"></a><span data-ttu-id="c61ea-109">Diretrizes</span><span class="sxs-lookup"><span data-stu-id="c61ea-109">Guidance</span></span>
<span data-ttu-id="c61ea-110">Olá sugestões a seguir ajudará você a aproveitar ao máximo **modelos** ao trabalhar com suas soluções:</span><span class="sxs-lookup"><span data-stu-id="c61ea-110">hello following suggestions will help you take full advantage of **Templates** when working with your solutions:</span></span>

* <span data-ttu-id="c61ea-111">Um **modelo** é um recurso de encapsulamento que contém um modelo do Resource Manager e metadados adicionais.</span><span class="sxs-lookup"><span data-stu-id="c61ea-111">A **Template** is an encapsulating resource that contains an Resource Manager template and additional metadata.</span></span> <span data-ttu-id="c61ea-112">Ele se comporta de maneira muito semelhante tooan item Olá Marketplace.</span><span class="sxs-lookup"><span data-stu-id="c61ea-112">It behaves very similarly tooan item in hello Marketplace.</span></span> <span data-ttu-id="c61ea-113">Olá principal diferença é que ele é um item privado como itens do Marketplace públicos toohello contrário.</span><span class="sxs-lookup"><span data-stu-id="c61ea-113">hello key difference is that it is a private item as opposed toohello public Marketplace items.</span></span>
* <span data-ttu-id="c61ea-114">Olá **modelos** biblioteca funciona bem para usuários que precisam de toocustomize suas implantações.</span><span class="sxs-lookup"><span data-stu-id="c61ea-114">hello **Templates** library works well for users who need toocustomize their deployments.</span></span>
* <span data-ttu-id="c61ea-115">**Modelos** funcionam bem com usuários que precisam de um repositório simples no Azure.</span><span class="sxs-lookup"><span data-stu-id="c61ea-115">**Templates** work well for users who need a simple repository within Azure.</span></span>
* <span data-ttu-id="c61ea-116">Comece com um modelo existente do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c61ea-116">Start with an existing Resource Manager template.</span></span> <span data-ttu-id="c61ea-117">Encontre modelos no [github](https://github.com/Azure/azure-quickstart-templates) ou [exporte o modelo](../azure-resource-manager/resource-manager-export-template.md) de um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="c61ea-117">Find templates in [github](https://github.com/Azure/azure-quickstart-templates) or [Export template](../azure-resource-manager/resource-manager-export-template.md) from an existing resource group.</span></span>
* <span data-ttu-id="c61ea-118">**Modelos de** usuário toohello associado que publica-los.</span><span class="sxs-lookup"><span data-stu-id="c61ea-118">**Templates** are tied toohello user who publishes them.</span></span> <span data-ttu-id="c61ea-119">nome do publicador Olá é visível tooeveryone que tenha acesso de leitura tooit.</span><span class="sxs-lookup"><span data-stu-id="c61ea-119">hello publisher name is visible tooeveryone who has read access tooit.</span></span>
* <span data-ttu-id="c61ea-120">**Modelos** são recursos do Resource Manager e não podem ser renomeados depois de publicados.</span><span class="sxs-lookup"><span data-stu-id="c61ea-120">**Templates** are Resource Manager resources and cannot be renamed once published.</span></span>

## <a name="add-a-template-resource"></a><span data-ttu-id="c61ea-121">Adicionar um recurso de modelo</span><span class="sxs-lookup"><span data-stu-id="c61ea-121">Add a Template resource</span></span>
<span data-ttu-id="c61ea-122">Há dois toocreate de maneiras um **modelo** recurso Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c61ea-122">There are two ways toocreate a **Template** resource in hello Azure portal.</span></span>

### <a name="method-1--create-a-new-template-resource-from-a-running-resource-group"></a><span data-ttu-id="c61ea-123">Método 1: criar um novo recurso de modelo de um grupo de recursos em execução</span><span class="sxs-lookup"><span data-stu-id="c61ea-123">Method 1 : Create a new Template resource from a running resource group</span></span>
1. <span data-ttu-id="c61ea-124">Navegue tooan grupo de recursos existente no hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c61ea-124">Navigate tooan existing resource group on hello Azure Portal.</span></span> <span data-ttu-id="c61ea-125">Selecione **Exportar modelo** em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="c61ea-125">Select **Export template** in **Settings**.</span></span>
2. <span data-ttu-id="c61ea-126">Depois que o modelo do Gerenciador de recursos de saudação é exportado, use Olá **Salvar modelo** botão toosave-toohello **modelos** repositório.</span><span class="sxs-lookup"><span data-stu-id="c61ea-126">Once hello Resource Manager template is exported, use hello **Save Template** button toosave it toohello **Templates** repository.</span></span> <span data-ttu-id="c61ea-127">Encontre todos os detalhes sobre a exportação de modelos [aqui](../azure-resource-manager/resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="c61ea-127">Find complete details for Export template [here](../azure-resource-manager/resource-manager-export-template.md).</span></span>
   <br /><br /><span data-ttu-id="c61ea-128">
   ![Exportação do grupo de recursos](media/rg-export-portal1.PNG)</span><span class="sxs-lookup"><span data-stu-id="c61ea-128">
![Resource group export](media/rg-export-portal1.PNG)</span></span>  <br />
3. <span data-ttu-id="c61ea-129">Selecione Olá **salvar tooTemplate** botão de comando.</span><span class="sxs-lookup"><span data-stu-id="c61ea-129">Select hello **Save tooTemplate** command button.</span></span>
   <br /><br />
4. <span data-ttu-id="c61ea-130">Digite hello informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="c61ea-130">Enter hello following information:</span></span>
   
   * <span data-ttu-id="c61ea-131">Nome – nome do objeto de modelo de saudação (Observação: esse é um nome com base do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c61ea-131">Name – Name of hello template object (NOTE: This is an Azure Resource Manager based name.</span></span> <span data-ttu-id="c61ea-132">Todas as restrições de nomenclatura são aplicáveis e ele não pode ser alterado depois de criado).</span><span class="sxs-lookup"><span data-stu-id="c61ea-132">All naming restrictions apply and it cannot be changed once created).</span></span>
   * <span data-ttu-id="c61ea-133">Descrição – resumo rápido sobre o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c61ea-133">Description – Quick summary about hello template.</span></span>
     
     ![Salvar Modelo](media/save-template-portal1.PNG)  <br />
5. <span data-ttu-id="c61ea-135">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="c61ea-135">Click **Save**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c61ea-136">Olá folha do modelo de exportação mostra notificações quando hello, modelo exportado do Gerenciador de recursos tem erros, mas ainda será capaz de toosave este toohello de modelo do Gerenciador de recursos modelos.</span><span class="sxs-lookup"><span data-stu-id="c61ea-136">hello Export template blade shows notifications when hello exported Resource Manager template has errors, but you will still be able toosave this Resource Manager template toohello Templates.</span></span> <span data-ttu-id="c61ea-137">Certifique-se de que você verifique e corrija qualquer Gerenciador de recursos de problemas do modelo antes de reimplantação hello exportada modelo do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="c61ea-137">Ensure that you check and fix any Resource Manager template issues before redeploying hello exported Resource Manager template.</span></span>
   > 
   > 

### <a name="method-2--add-a-new-template-resource-from-browse"></a><span data-ttu-id="c61ea-138">Método 2: adicionar um novo recurso de modelo por meio de navegação</span><span class="sxs-lookup"><span data-stu-id="c61ea-138">Method 2 : Add a new Template resource from browse</span></span>
<span data-ttu-id="c61ea-139">Você também pode adicionar um novo **modelo** do zero usando Olá + adicionar o botão de comando em **procurar > modelos**.</span><span class="sxs-lookup"><span data-stu-id="c61ea-139">You can also add a new **Template** from scratch using hello +Add command button in **Browse > Templates**.</span></span> <span data-ttu-id="c61ea-140">Você precisará tooprovide um nome, descrição e hello modelo JSON do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="c61ea-140">You will need tooprovide a Name, Description and hello Resource Manager template JSON.</span></span>

![Adicionar Modelo](media/add-template-portal1.PNG)  <br />

> [!NOTE]
> <span data-ttu-id="c61ea-142">Microsoft.Gallery é um provedor de recursos do Azure baseado em locatário.</span><span class="sxs-lookup"><span data-stu-id="c61ea-142">Microsoft.Gallery is a Tenant based Azure resource provider.</span></span> <span data-ttu-id="c61ea-143">Olá, recurso de modelo é usuário toohello associado que o criou.</span><span class="sxs-lookup"><span data-stu-id="c61ea-143">hello Template resource is tied toohello user who created it.</span></span> <span data-ttu-id="c61ea-144">Não é uma assinatura específica tooany associado.</span><span class="sxs-lookup"><span data-stu-id="c61ea-144">It is not tied tooany specific subscription.</span></span> <span data-ttu-id="c61ea-145">Uma assinatura precisa toobe escolhido somente ao implantar um modelo.</span><span class="sxs-lookup"><span data-stu-id="c61ea-145">A subscription needs toobe chosen only when deploying a Template.</span></span>
> 
> 

## <a name="view-template-resources"></a><span data-ttu-id="c61ea-146">Exibir recursos de modelo</span><span class="sxs-lookup"><span data-stu-id="c61ea-146">View Template resources</span></span>
<span data-ttu-id="c61ea-147">Todos os **modelos** tooyou disponível pode ser visto no **procurar > modelos**.</span><span class="sxs-lookup"><span data-stu-id="c61ea-147">All **Templates** available tooyou can be seen at **Browse > Templates**.</span></span> <span data-ttu-id="c61ea-148">Isso inclui **modelos** que você criou e os que foram compartilhados com você com vários níveis de permissões.</span><span class="sxs-lookup"><span data-stu-id="c61ea-148">This includes **Templates** you have created as well as ones that have been shared with you with varying levels of permissions.</span></span> <span data-ttu-id="c61ea-149">Para obter mais detalhes no hello [controle de acesso](#access-control-for-a-tenant-resource-provider) seção abaixo.</span><span class="sxs-lookup"><span data-stu-id="c61ea-149">More details in hello [access control](#access-control-for-a-tenant-resource-provider) section below.</span></span>

![Exibir Modelo](media/view-template-portal1.PNG)  <br />

<span data-ttu-id="c61ea-151">Você pode exibir detalhes de saudação de um **modelo** clicando em um item na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="c61ea-151">You can view hello details of a **Template** by clicking into an item in hello list.</span></span>

![Exibir Modelo](media/view-template-portal2c.png)  <br />

## <a name="edit-a-template-resource"></a><span data-ttu-id="c61ea-153">Editar um recurso de modelo</span><span class="sxs-lookup"><span data-stu-id="c61ea-153">Edit a Template resource</span></span>
<span data-ttu-id="c61ea-154">Você pode iniciar Olá Editar fluxo para um **modelo** por item de saudação clique direito na lista de pesquisa de saudação ou escolhendo o botão de comando de edição de saudação.</span><span class="sxs-lookup"><span data-stu-id="c61ea-154">You can initiate hello edit flow for a **Template** by right clicking hello item on hello Browse list or by choosing hello Edit command button.</span></span>

![Editar modelo](media/edit-template-portal1a.PNG)  <br />

<span data-ttu-id="c61ea-156">Você pode editar a descrição de saudação ou texto de modelo do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="c61ea-156">You can edit hello description or Resource Manager template text.</span></span> <span data-ttu-id="c61ea-157">Você não pode editar o nome de saudação porque é um nome de recurso do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="c61ea-157">You cannot edit hello name since it is an Resource Manager resource name.</span></span> <span data-ttu-id="c61ea-158">Quando você editar o modelo do Gerenciador de recursos de saudação JSON validamos tooensure que é JSON válido.</span><span class="sxs-lookup"><span data-stu-id="c61ea-158">When you edit hello Resource Manager template JSON we will validate tooensure that it is valid JSON.</span></span> <span data-ttu-id="c61ea-159">Escolha **Okey** e **salvar** toosave seu modelo atualizado.</span><span class="sxs-lookup"><span data-stu-id="c61ea-159">Choose **OK** and then **Save** toosave your updated template.</span></span>

![Editar modelo](media/edit-template-portal2a.PNG)  <br />

<span data-ttu-id="c61ea-161">Uma vez Olá **modelo** é salvo você verá uma notificação de confirmação.</span><span class="sxs-lookup"><span data-stu-id="c61ea-161">Once hello **Template** is saved you will see a confirmation notification.</span></span>

![Editar modelo](media/edit-template-portal3b.png)  <br />

## <a name="deploy-a-template-resource"></a><span data-ttu-id="c61ea-163">Implantar um recurso de modelo</span><span class="sxs-lookup"><span data-stu-id="c61ea-163">Deploy a Template resource</span></span>
<span data-ttu-id="c61ea-164">Você pode implantar qualquer **Modelo** para o qual tiver permissões de **Leitura**.</span><span class="sxs-lookup"><span data-stu-id="c61ea-164">You can deploy any **Template** that you have **Read** permissions on.</span></span> <span data-ttu-id="c61ea-165">implantação do fluxo de saudação inicia a folha de implantação de modelo do Azure standard hello.</span><span class="sxs-lookup"><span data-stu-id="c61ea-165">hello deployment flow launches hello standard Azure Template deployment blade.</span></span> <span data-ttu-id="c61ea-166">Preencha os valores hello tooproceed de parâmetros de modelo Olá Gerenciador de recursos com a implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="c61ea-166">Fill out hello values for hello Resource Manager template parameters tooproceed with hello deployment.</span></span>

![Implantar o modelo](media/deploy-template-portal1b.png)  <br />

## <a name="share-a-template-resource"></a><span data-ttu-id="c61ea-168">Compartilhar um recurso de modelo</span><span class="sxs-lookup"><span data-stu-id="c61ea-168">Share a Template resource</span></span>
<span data-ttu-id="c61ea-169">Um recurso de **modelo** pode ser compartilhados com seus colegas.</span><span class="sxs-lookup"><span data-stu-id="c61ea-169">A **Template** resource can be shared with your peers.</span></span> <span data-ttu-id="c61ea-170">Compartilhamento se comporta da mesma forma muito[atribuição de função para qualquer recurso no Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c61ea-170">Sharing behaves similarly too[role assignment for any resource on Azure](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="c61ea-171">Olá **modelo** proprietário fornece permissões tooother usuários podem interagir com um recurso de modelo.</span><span class="sxs-lookup"><span data-stu-id="c61ea-171">hello **Template** owner provides permissions tooother users who can interact with a Template resource.</span></span> <span data-ttu-id="c61ea-172">Olá pessoa ou grupo de pessoas que você compartilha Olá **modelo** com será capaz de toosee modelo de Gerenciador de recursos de saudação e suas propriedades de galeria.</span><span class="sxs-lookup"><span data-stu-id="c61ea-172">hello person or group of people you share hello **Template** with will be able toosee hello Resource Manager template and its gallery properties.</span></span>

### <a name="access-control-for-hello-microsoftgallery-resources"></a><span data-ttu-id="c61ea-173">Controle de acesso para recursos de Microsoft.Gallery Olá</span><span class="sxs-lookup"><span data-stu-id="c61ea-173">Access control for hello Microsoft.Gallery resources</span></span>
| <span data-ttu-id="c61ea-174">Função</span><span class="sxs-lookup"><span data-stu-id="c61ea-174">Role</span></span> | <span data-ttu-id="c61ea-175">Permissões</span><span class="sxs-lookup"><span data-stu-id="c61ea-175">Permissions</span></span> |
| --- | --- |
| <span data-ttu-id="c61ea-176">Proprietário</span><span class="sxs-lookup"><span data-stu-id="c61ea-176">Owner</span></span> |<span data-ttu-id="c61ea-177">Permite que o controle total sobre o recurso de modelo Olá incluindo compartilhamento</span><span class="sxs-lookup"><span data-stu-id="c61ea-177">Allows full control on hello Template resource including Share</span></span> |
| <span data-ttu-id="c61ea-178">Leitor</span><span class="sxs-lookup"><span data-stu-id="c61ea-178">Reader</span></span> |<span data-ttu-id="c61ea-179">Permite a leitura e Execute(Deploy) Olá recurso de modelo</span><span class="sxs-lookup"><span data-stu-id="c61ea-179">Allows Read and Execute(Deploy) on hello Template resource</span></span> |
| <span data-ttu-id="c61ea-180">Colaborador</span><span class="sxs-lookup"><span data-stu-id="c61ea-180">Contributor</span></span> |<span data-ttu-id="c61ea-181">Permite a permissão de edição e exclusão em Olá recurso de modelo.</span><span class="sxs-lookup"><span data-stu-id="c61ea-181">Allows Edit and Delete permission on hello Template resource.</span></span> <span data-ttu-id="c61ea-182">Usuário não pode compartilhar Olá modelo com outras pessoas</span><span class="sxs-lookup"><span data-stu-id="c61ea-182">User cannot Share hello Template with others</span></span> |

<span data-ttu-id="c61ea-183">Selecione **compartilhamento** no item de navegação Olá com um clique direito ou na folha de modo de exibição de saudação de um item específico.</span><span class="sxs-lookup"><span data-stu-id="c61ea-183">Select **Share** on hello browse item by right clicking or on hello view blade of a specific item.</span></span> <span data-ttu-id="c61ea-184">Isso inicia uma experiência de compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="c61ea-184">This launches a Share experience.</span></span>

![Compartilhar modelo](media/share-template-portal1a.png)  <br />

 <span data-ttu-id="c61ea-186">Agora você pode escolher uma função e tooa um acesso de tooprovide usuário ou grupo específico **modelo**.</span><span class="sxs-lookup"><span data-stu-id="c61ea-186">You can now choose a role and a user or group tooprovide access tooa particular **Template**.</span></span> <span data-ttu-id="c61ea-187">funções disponíveis Olá são proprietário, o leitor e o colaborador.</span><span class="sxs-lookup"><span data-stu-id="c61ea-187">hello available roles are Owner, Reader and Contributor.</span></span> <span data-ttu-id="c61ea-188">Para obter mais detalhes no hello [controle de acesso](#access-control-for-a-tenant-resource-provider) seção acima.</span><span class="sxs-lookup"><span data-stu-id="c61ea-188">More details in hello [access control](#access-control-for-a-tenant-resource-provider) section above.</span></span>

![Compartilhar modelo](media/share-template-portal2b.png)  <br />

![Compartilhar modelo](media/share-template-portal3b.png)  <br />

<span data-ttu-id="c61ea-191">Clique em **Selecionar** e em **Ok**.</span><span class="sxs-lookup"><span data-stu-id="c61ea-191">Click **Select** and **Ok**.</span></span> <span data-ttu-id="c61ea-192">Agora você pode ver Olá usuários ou grupos adicionados toohello recursos.</span><span class="sxs-lookup"><span data-stu-id="c61ea-192">You can now see hello users or groups you added toohello resource.</span></span>

![Compartilhar modelo](media/share-template-portal4b.png)  <br />

> [!NOTE]
> <span data-ttu-id="c61ea-194">Um modelo só pode ser compartilhado com usuários e grupos no hello mesmo locatário do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="c61ea-194">A Template can only be shared with users and groups in hello same Azure Active Directory tenant.</span></span> <span data-ttu-id="c61ea-195">Se você compartilhar um modelo com um endereço de email que não está em seu locatário, será enviado um convite perguntando Olá toojoin saudação do locatário usuário como convidado.</span><span class="sxs-lookup"><span data-stu-id="c61ea-195">If you share a Template with an email address that is not in your tenant, an invitation will be sent asking hello user toojoin hello tenant as a guest.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="c61ea-196">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c61ea-196">Next steps</span></span>
* <span data-ttu-id="c61ea-197">toolearn sobre como criar modelos do Gerenciador de recursos, consulte [criando modelos](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="c61ea-197">toolearn about creating Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="c61ea-198">funções de saudação toounderstand você pode usar em um modelo do Gerenciador de recursos, consulte [funções de modelo](../azure-resource-manager/resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="c61ea-198">toounderstand hello functions you can use in an Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md)</span></span>
* <span data-ttu-id="c61ea-199">Para obter diretrizes sobre como criar os modelos, confira [Práticas recomendadas para a criação de modelos do Gerenciador de Recursos do Azure](../azure-resource-manager/best-practices-resource-manager-design-templates.md)</span><span class="sxs-lookup"><span data-stu-id="c61ea-199">For guidance on designing your templates, see [Best practices for designing Azure Resource Manager templates](../azure-resource-manager/best-practices-resource-manager-design-templates.md)</span></span>

