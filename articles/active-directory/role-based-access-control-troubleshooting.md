---
title: Solucionar problemas de RBAC do Azure | Microsoft Docs
description: "Obtenha ajuda para problemas ou dúvidas sobre recursos do Controle de Acesso Baseado em Função."
services: azure-portal
documentationcenter: na
author: andredm7
manager: femila
ms.assetid: df42cca2-02d6-4f3c-9d56-260e1eb7dc44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 407c030ea159915d4d7ac21760a3d17ec2204372
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="role-based-access-control-troubleshooting"></a><span data-ttu-id="c924b-103">Solução de problemas de Controle de Acesso baseado em função</span><span class="sxs-lookup"><span data-stu-id="c924b-103">Role-Based Access Control troubleshooting</span></span>

<span data-ttu-id="c924b-104">Este artigo responde a perguntas comuns sobre os direitos de acesso específicos concedidos com as funções, para que você saiba o que esperar ao usar as funções no portal do Azure e possa solucionar problemas de acesso.</span><span class="sxs-lookup"><span data-stu-id="c924b-104">This document article answers common questions about the specific access rights that are granted with roles, so that you know what to expect when using the roles in the Azure portal and can troubleshoot access problems.</span></span> <span data-ttu-id="c924b-105">Estas três funções abrangem todos os tipos de recurso:</span><span class="sxs-lookup"><span data-stu-id="c924b-105">These three roles cover all resource types:</span></span>

* <span data-ttu-id="c924b-106">Proprietário</span><span class="sxs-lookup"><span data-stu-id="c924b-106">Owner</span></span>  
* <span data-ttu-id="c924b-107">Colaborador</span><span class="sxs-lookup"><span data-stu-id="c924b-107">Contributor</span></span>  
* <span data-ttu-id="c924b-108">Leitor</span><span class="sxs-lookup"><span data-stu-id="c924b-108">Reader</span></span>  

<span data-ttu-id="c924b-109">Os proprietários e colaboradores têm acesso completo a experiência de gerenciamento, mas um colaborador não pode conceder acesso aos outros usuário ou grupos.</span><span class="sxs-lookup"><span data-stu-id="c924b-109">Owners and contributors both have full access to the management experience, but a contributor can’t give access to other users or groups.</span></span> <span data-ttu-id="c924b-110">As coisas ficam um pouco mais interessantes com a função de leitor e é para ela que vamos dedicar algum tempo.</span><span class="sxs-lookup"><span data-stu-id="c924b-110">Things get a little more interesting with the reader role, so that’s where we'll spend some time.</span></span> <span data-ttu-id="c924b-111">Consulte o [Artigo de introdução ao Controle de Acesso Baseado em Função](role-based-access-control-configure.md) para obter detalhes sobre como conceder acesso.</span><span class="sxs-lookup"><span data-stu-id="c924b-111">See the [Role-Based Access Control get-started article](role-based-access-control-configure.md) for details on how to grant access.</span></span>

## <a name="app-service-workloads"></a><span data-ttu-id="c924b-112">Cargas de trabalho do serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="c924b-112">App service workloads</span></span>
### <a name="write-access-capabilities"></a><span data-ttu-id="c924b-113">Recursos do acesso de gravação</span><span class="sxs-lookup"><span data-stu-id="c924b-113">Write access capabilities</span></span>
<span data-ttu-id="c924b-114">Se você conceder a um usuário o acesso somente leitura a um aplicativo Web, para sua surpresa, alguns recursos estarão desabilitados.</span><span class="sxs-lookup"><span data-stu-id="c924b-114">If you grant a user read-only access to a single web app, some features are disabled that you might not expect.</span></span> <span data-ttu-id="c924b-115">As funcionalidades de gerenciamento a seguir exigem o acesso de **gravação** para um aplicativo Web (Colaborador ou Proprietário) e não estarão disponíveis em um cenário somente leitura.</span><span class="sxs-lookup"><span data-stu-id="c924b-115">The following management capabilities require **write** access to a web app (either Contributor or Owner), and aren’t available in any read-only scenario.</span></span>

* <span data-ttu-id="c924b-116">Comandos (como iniciar, parar, etc.)</span><span class="sxs-lookup"><span data-stu-id="c924b-116">Commands (like start, stop, etc.)</span></span>
* <span data-ttu-id="c924b-117">Alterar configurações como configuração geral, configurações de escala, configurações de backup e configurações de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="c924b-117">Changing settings like general configuration, scale settings, backup settings, and monitoring settings</span></span>
* <span data-ttu-id="c924b-118">Acessar credenciais de publicação e outros segredos como configurações de aplicativos e cadeias de conexão.</span><span class="sxs-lookup"><span data-stu-id="c924b-118">Accessing publishing credentials and other secrets like app settings and connection strings</span></span>
* <span data-ttu-id="c924b-119">Logs de streaming</span><span class="sxs-lookup"><span data-stu-id="c924b-119">Streaming logs</span></span>
* <span data-ttu-id="c924b-120">Configuração dos logs de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="c924b-120">Diagnostic logs configuration</span></span>
* <span data-ttu-id="c924b-121">Console (prompt de comando)</span><span class="sxs-lookup"><span data-stu-id="c924b-121">Console (command prompt)</span></span>
* <span data-ttu-id="c924b-122">Ativo e implantações recentes (para a implantação contínua do git local)</span><span class="sxs-lookup"><span data-stu-id="c924b-122">Active and recent deployments (for local git continuous deployment)</span></span>
* <span data-ttu-id="c924b-123">Gasto estimado</span><span class="sxs-lookup"><span data-stu-id="c924b-123">Estimated spend</span></span>
* <span data-ttu-id="c924b-124">Testes da Web</span><span class="sxs-lookup"><span data-stu-id="c924b-124">Web tests</span></span>
* <span data-ttu-id="c924b-125">Rede virtual (somente visível para um leitor se uma rede virtual foi anteriormente configurada por um usuário com acesso para gravação).</span><span class="sxs-lookup"><span data-stu-id="c924b-125">Virtual network (only visible to a reader if a virtual network has previously been configured by a user with write access).</span></span>

<span data-ttu-id="c924b-126">Se você não conseguir acessar nenhum desses blocos, precisará solicitar ao administrador o acesso de Colaborador ao aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="c924b-126">If you can't access any of these tiles, you need to ask your administrator for Contributor access to the web app.</span></span>

### <a name="dealing-with-related-resources"></a><span data-ttu-id="c924b-127">Lidando com recursos relacionados</span><span class="sxs-lookup"><span data-stu-id="c924b-127">Dealing with related resources</span></span>
<span data-ttu-id="c924b-128">Os aplicativos Web são complicados pela presença de alguns recursos diferentes que interagem.</span><span class="sxs-lookup"><span data-stu-id="c924b-128">Web apps are complicated by the presence of a few different resources that interplay.</span></span> <span data-ttu-id="c924b-129">Aqui encontra-se um grupo de recursos típico com alguns sites:</span><span class="sxs-lookup"><span data-stu-id="c924b-129">Here is a typical resource group with a couple websites:</span></span>

![Grupo de recursos do aplicativo Web](./media/role-based-access-control-troubleshooting/website-resource-model.png)

<span data-ttu-id="c924b-131">Como resultado, se você conceder a alguém o acesso somente ao aplicativo Web, muitas das funcionalidades na folha do site no portal do Azure estarão desabilitadas.</span><span class="sxs-lookup"><span data-stu-id="c924b-131">As a result, if you grant someone access to just the web app, much of the functionality on the website blade in the Azure portal is disabled.</span></span>

<span data-ttu-id="c924b-132">Estes itens exigem acesso para **gravação** no **Plano do Serviço de Aplicativo** que corresponde ao seu site:</span><span class="sxs-lookup"><span data-stu-id="c924b-132">These items require **write** access to the **App Service plan** that corresponds to your website:</span></span>  

* <span data-ttu-id="c924b-133">Exibindo o tipo de preço do aplicativo Web (Grátis ou Standard)</span><span class="sxs-lookup"><span data-stu-id="c924b-133">Viewing the web app’s pricing tier (Free or Standard)</span></span>  
* <span data-ttu-id="c924b-134">Configuração de escala (número instâncias, tamanho da máquina virtual, configurações de escalonamento automático)</span><span class="sxs-lookup"><span data-stu-id="c924b-134">Scale configuration (number of instances, virtual machine size, autoscale settings)</span></span>  
* <span data-ttu-id="c924b-135">Cotas (armazenamento, largura de banda, CPU)</span><span class="sxs-lookup"><span data-stu-id="c924b-135">Quotas (storage, bandwidth, CPU)</span></span>  

<span data-ttu-id="c924b-136">Estes itens exigem acesso para **gravação** no **Grupo de recursos** inteiro que contém o seu site:</span><span class="sxs-lookup"><span data-stu-id="c924b-136">These items require **write** access to the whole **Resource group** that contains your website:</span></span>  

* <span data-ttu-id="c924b-137">Associações e Certificados SSL (os certificados SSL podem ser compartilhados entre sites no mesmo grupo de recursos e localização geográfica)</span><span class="sxs-lookup"><span data-stu-id="c924b-137">SSL Certificates and bindings (SSL certificates can be shared between sites in the same resource group and geo-location)</span></span>  
* <span data-ttu-id="c924b-138">Regras de alerta</span><span class="sxs-lookup"><span data-stu-id="c924b-138">Alert rules</span></span>  
* <span data-ttu-id="c924b-139">Configurações de autoescala</span><span class="sxs-lookup"><span data-stu-id="c924b-139">Autoscale settings</span></span>  
* <span data-ttu-id="c924b-140">Componentes do Application insights</span><span class="sxs-lookup"><span data-stu-id="c924b-140">Application insights components</span></span>  
* <span data-ttu-id="c924b-141">Testes da Web</span><span class="sxs-lookup"><span data-stu-id="c924b-141">Web tests</span></span>  

## <a name="virtual-machine-workloads"></a><span data-ttu-id="c924b-142">Cargas de trabalho da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c924b-142">Virtual machine workloads</span></span>
<span data-ttu-id="c924b-143">Como muitos aplicativos Web, alguns recursos na folha da máquina virtual requerem o acesso de gravação para a máquina virtual ou a outros recursos no grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c924b-143">Much like with web apps, some features on the virtual machine blade require write access to the virtual machine, or to other resources in the resource group.</span></span>

<span data-ttu-id="c924b-144">As máquinas virtuais são relacionadas a nomes de domínio, redes virtuais, contas de armazenamento e regras de alerta.</span><span class="sxs-lookup"><span data-stu-id="c924b-144">Virtual machines are related to Domain names, virtual networks, storage accounts, and alert rules.</span></span>

<span data-ttu-id="c924b-145">Estes itens exigem acesso para **gravação** na **Máquina virtual**:</span><span class="sxs-lookup"><span data-stu-id="c924b-145">These items require **write** access to the **Virtual machine**:</span></span>

* <span data-ttu-id="c924b-146">Pontos de extremidade</span><span class="sxs-lookup"><span data-stu-id="c924b-146">Endpoints</span></span>  
* <span data-ttu-id="c924b-147">Endereços IP</span><span class="sxs-lookup"><span data-stu-id="c924b-147">IP addresses</span></span>  
* <span data-ttu-id="c924b-148">Discos</span><span class="sxs-lookup"><span data-stu-id="c924b-148">Disks</span></span>  
* <span data-ttu-id="c924b-149">Extensões</span><span class="sxs-lookup"><span data-stu-id="c924b-149">Extensions</span></span>  

<span data-ttu-id="c924b-150">Estes exigem acesso para **gravação** tanto na **Máquina virtual** quanto no **Grupo de recursos** (juntamente com o Nome de domínio) encontrados em:</span><span class="sxs-lookup"><span data-stu-id="c924b-150">These require **write** access to both the **Virtual machine**, and the **Resource group** (along with the Domain name) that it is in:</span></span>  

* <span data-ttu-id="c924b-151">Conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="c924b-151">Availability set</span></span>  
* <span data-ttu-id="c924b-152">Conjunto de balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="c924b-152">Load balanced set</span></span>  
* <span data-ttu-id="c924b-153">Regras de alerta</span><span class="sxs-lookup"><span data-stu-id="c924b-153">Alert rules</span></span>  

<span data-ttu-id="c924b-154">Se você não conseguir acessar nenhum desses blocos, solicite ao administrador o acesso de Colaborador ao Grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c924b-154">If you can't access any of these tiles, ask your administrator for Contributor access to the Resource group.</span></span>

## <a name="see-more"></a><span data-ttu-id="c924b-155">Veja mais</span><span class="sxs-lookup"><span data-stu-id="c924b-155">See more</span></span>
* <span data-ttu-id="c924b-156">[Controle de Acesso Baseado em Função](role-based-access-control-configure.md): introdução ao RBAC no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c924b-156">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in the Azure portal.</span></span>
* <span data-ttu-id="c924b-157">[Funções internas](role-based-access-built-in-roles.md): obter detalhes sobre as funções que são incluídas por padrão no RBAC.</span><span class="sxs-lookup"><span data-stu-id="c924b-157">[Built-in roles](role-based-access-built-in-roles.md): Get details about the roles that come standard in RBAC.</span></span>
* <span data-ttu-id="c924b-158">[Funções personalizadas no Azure RBAC](role-based-access-control-custom-roles.md): aprenda a criar funções personalizadas para atender às suas necessidades de acesso.</span><span class="sxs-lookup"><span data-stu-id="c924b-158">[Custom roles in Azure RBAC](role-based-access-control-custom-roles.md): Learn how to create custom roles to fit your access needs.</span></span>
* <span data-ttu-id="c924b-159">[Criar um relatório de histórico de alterações de acesso](role-based-access-control-access-change-history-report.md): mantenha o controle das alterações de atribuições de função no RBAC.</span><span class="sxs-lookup"><span data-stu-id="c924b-159">[Create an access change history report](role-based-access-control-access-change-history-report.md): Keep track of changing role assignments in RBAC.</span></span>

