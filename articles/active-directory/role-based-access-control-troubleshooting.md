---
title: aaaTroubleshoot RBAC do Azure | Microsoft Docs
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
ms.openlocfilehash: 15feced32d8459d90c4c246d335932f90e1fc91f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-troubleshooting"></a><span data-ttu-id="5cf80-103">Solução de problemas de Controle de Acesso baseado em função</span><span class="sxs-lookup"><span data-stu-id="5cf80-103">Role-Based Access Control troubleshooting</span></span>

<span data-ttu-id="5cf80-104">Este artigo de documento respostas a perguntas comuns sobre direitos de acesso específicos de saudação que são concedidas com funções, para que você saiba quais tooexpect quando usando Olá funções hello portal do Azure e pode solucionar problemas de acesso.</span><span class="sxs-lookup"><span data-stu-id="5cf80-104">This document article answers common questions about hello specific access rights that are granted with roles, so that you know what tooexpect when using hello roles in hello Azure portal and can troubleshoot access problems.</span></span> <span data-ttu-id="5cf80-105">Estas três funções abrangem todos os tipos de recurso:</span><span class="sxs-lookup"><span data-stu-id="5cf80-105">These three roles cover all resource types:</span></span>

* <span data-ttu-id="5cf80-106">Proprietário</span><span class="sxs-lookup"><span data-stu-id="5cf80-106">Owner</span></span>  
* <span data-ttu-id="5cf80-107">Colaborador</span><span class="sxs-lookup"><span data-stu-id="5cf80-107">Contributor</span></span>  
* <span data-ttu-id="5cf80-108">Leitor</span><span class="sxs-lookup"><span data-stu-id="5cf80-108">Reader</span></span>  

<span data-ttu-id="5cf80-109">Os proprietários e os fatores que contribuem com o gerenciamento de toohello acesso completo a experiência, mas um Colaborador não pode conceder acesso tooother usuários ou grupos.</span><span class="sxs-lookup"><span data-stu-id="5cf80-109">Owners and contributors both have full access toohello management experience, but a contributor can’t give access tooother users or groups.</span></span> <span data-ttu-id="5cf80-110">As coisas são um pouco mais interessantes com a função de leitor de hello, que é onde vamos gastar algum tempo.</span><span class="sxs-lookup"><span data-stu-id="5cf80-110">Things get a little more interesting with hello reader role, so that’s where we'll spend some time.</span></span> <span data-ttu-id="5cf80-111">Consulte Olá [artigo iniciada por get do controle de acesso baseado em função](role-based-access-control-configure.md) para obter detalhes sobre como acessar toogrant.</span><span class="sxs-lookup"><span data-stu-id="5cf80-111">See hello [Role-Based Access Control get-started article](role-based-access-control-configure.md) for details on how toogrant access.</span></span>

## <a name="app-service-workloads"></a><span data-ttu-id="5cf80-112">Cargas de trabalho do serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="5cf80-112">App service workloads</span></span>
### <a name="write-access-capabilities"></a><span data-ttu-id="5cf80-113">Recursos do acesso de gravação</span><span class="sxs-lookup"><span data-stu-id="5cf80-113">Write access capabilities</span></span>
<span data-ttu-id="5cf80-114">Se você conceder a um usuário acesso somente leitura tooa web único aplicativo, alguns recursos são desabilitados se você não esperava.</span><span class="sxs-lookup"><span data-stu-id="5cf80-114">If you grant a user read-only access tooa single web app, some features are disabled that you might not expect.</span></span> <span data-ttu-id="5cf80-115">Olá, recursos de gerenciamento a seguir exige **gravar** acessar tooa web app (colaborador ou proprietário) e não estão disponíveis em qualquer cenário de somente leitura.</span><span class="sxs-lookup"><span data-stu-id="5cf80-115">hello following management capabilities require **write** access tooa web app (either Contributor or Owner), and aren’t available in any read-only scenario.</span></span>

* <span data-ttu-id="5cf80-116">Comandos (como iniciar, parar, etc.)</span><span class="sxs-lookup"><span data-stu-id="5cf80-116">Commands (like start, stop, etc.)</span></span>
* <span data-ttu-id="5cf80-117">Alterar configurações como configuração geral, configurações de escala, configurações de backup e configurações de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="5cf80-117">Changing settings like general configuration, scale settings, backup settings, and monitoring settings</span></span>
* <span data-ttu-id="5cf80-118">Acessar credenciais de publicação e outros segredos como configurações de aplicativos e cadeias de conexão.</span><span class="sxs-lookup"><span data-stu-id="5cf80-118">Accessing publishing credentials and other secrets like app settings and connection strings</span></span>
* <span data-ttu-id="5cf80-119">Logs de streaming</span><span class="sxs-lookup"><span data-stu-id="5cf80-119">Streaming logs</span></span>
* <span data-ttu-id="5cf80-120">Configuração dos logs de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="5cf80-120">Diagnostic logs configuration</span></span>
* <span data-ttu-id="5cf80-121">Console (prompt de comando)</span><span class="sxs-lookup"><span data-stu-id="5cf80-121">Console (command prompt)</span></span>
* <span data-ttu-id="5cf80-122">Ativo e implantações recentes (para a implantação contínua do git local)</span><span class="sxs-lookup"><span data-stu-id="5cf80-122">Active and recent deployments (for local git continuous deployment)</span></span>
* <span data-ttu-id="5cf80-123">Gasto estimado</span><span class="sxs-lookup"><span data-stu-id="5cf80-123">Estimated spend</span></span>
* <span data-ttu-id="5cf80-124">Testes da Web</span><span class="sxs-lookup"><span data-stu-id="5cf80-124">Web tests</span></span>
* <span data-ttu-id="5cf80-125">Rede virtual (somente o tooa visível leitor se uma rede virtual tiver sido configurada anteriormente por um usuário com acesso de gravação).</span><span class="sxs-lookup"><span data-stu-id="5cf80-125">Virtual network (only visible tooa reader if a virtual network has previously been configured by a user with write access).</span></span>

<span data-ttu-id="5cf80-126">Se você não pode acessar qualquer um desses blocos, será necessário tooask o administrador do aplicativo web do Colaborador acesso toohello.</span><span class="sxs-lookup"><span data-stu-id="5cf80-126">If you can't access any of these tiles, you need tooask your administrator for Contributor access toohello web app.</span></span>

### <a name="dealing-with-related-resources"></a><span data-ttu-id="5cf80-127">Lidando com recursos relacionados</span><span class="sxs-lookup"><span data-stu-id="5cf80-127">Dealing with related resources</span></span>
<span data-ttu-id="5cf80-128">Os aplicativos Web são complicados pela presença de saudação de alguns recursos diferentes que interação.</span><span class="sxs-lookup"><span data-stu-id="5cf80-128">Web apps are complicated by hello presence of a few different resources that interplay.</span></span> <span data-ttu-id="5cf80-129">Aqui encontra-se um grupo de recursos típico com alguns sites:</span><span class="sxs-lookup"><span data-stu-id="5cf80-129">Here is a typical resource group with a couple websites:</span></span>

![Grupo de recursos do aplicativo Web](./media/role-based-access-control-troubleshooting/website-resource-model.png)

<span data-ttu-id="5cf80-131">Como resultado, se você conceder a pessoa acesso toojust Olá web app, grande parte da funcionalidade de saudação na folha de site Olá no hello portal do Azure está desabilitado.</span><span class="sxs-lookup"><span data-stu-id="5cf80-131">As a result, if you grant someone access toojust hello web app, much of hello functionality on hello website blade in hello Azure portal is disabled.</span></span>

<span data-ttu-id="5cf80-132">Esses itens requerem **gravar** acessar toohello **plano de serviço de aplicativo** que corresponde a tooyour site:</span><span class="sxs-lookup"><span data-stu-id="5cf80-132">These items require **write** access toohello **App Service plan** that corresponds tooyour website:</span></span>  

* <span data-ttu-id="5cf80-133">Exibindo Olá web app do preço (gratuito ou padrão)</span><span class="sxs-lookup"><span data-stu-id="5cf80-133">Viewing hello web app’s pricing tier (Free or Standard)</span></span>  
* <span data-ttu-id="5cf80-134">Configuração de escala (número instâncias, tamanho da máquina virtual, configurações de escalonamento automático)</span><span class="sxs-lookup"><span data-stu-id="5cf80-134">Scale configuration (number of instances, virtual machine size, autoscale settings)</span></span>  
* <span data-ttu-id="5cf80-135">Cotas (armazenamento, largura de banda, CPU)</span><span class="sxs-lookup"><span data-stu-id="5cf80-135">Quotas (storage, bandwidth, CPU)</span></span>  

<span data-ttu-id="5cf80-136">Esses itens requerem **gravar** toohello de acesso toda **grupo de recursos** que contém seu site:</span><span class="sxs-lookup"><span data-stu-id="5cf80-136">These items require **write** access toohello whole **Resource group** that contains your website:</span></span>  

* <span data-ttu-id="5cf80-137">Certificados SSL e associações (certificados SSL podem ser compartilhados entre sites em Olá mesmo grupo de recursos e a localização geográfica)</span><span class="sxs-lookup"><span data-stu-id="5cf80-137">SSL Certificates and bindings (SSL certificates can be shared between sites in hello same resource group and geo-location)</span></span>  
* <span data-ttu-id="5cf80-138">Regras de alerta</span><span class="sxs-lookup"><span data-stu-id="5cf80-138">Alert rules</span></span>  
* <span data-ttu-id="5cf80-139">Configurações de autoescala</span><span class="sxs-lookup"><span data-stu-id="5cf80-139">Autoscale settings</span></span>  
* <span data-ttu-id="5cf80-140">Componentes do Application insights</span><span class="sxs-lookup"><span data-stu-id="5cf80-140">Application insights components</span></span>  
* <span data-ttu-id="5cf80-141">Testes da Web</span><span class="sxs-lookup"><span data-stu-id="5cf80-141">Web tests</span></span>  

## <a name="virtual-machine-workloads"></a><span data-ttu-id="5cf80-142">Cargas de trabalho da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="5cf80-142">Virtual machine workloads</span></span>
<span data-ttu-id="5cf80-143">Muito como com aplicativos da web, alguns recursos na folha de máquina virtual Olá exigem acesso de gravação toohello VM ou tooother recursos no grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="5cf80-143">Much like with web apps, some features on hello virtual machine blade require write access toohello virtual machine, or tooother resources in hello resource group.</span></span>

<span data-ttu-id="5cf80-144">Máquinas virtuais são nomes tooDomain relacionados, redes virtuais, contas de armazenamento e regras de alerta.</span><span class="sxs-lookup"><span data-stu-id="5cf80-144">Virtual machines are related tooDomain names, virtual networks, storage accounts, and alert rules.</span></span>

<span data-ttu-id="5cf80-145">Esses itens requerem **gravar** acessar toohello **Máquina Virtual**:</span><span class="sxs-lookup"><span data-stu-id="5cf80-145">These items require **write** access toohello **Virtual machine**:</span></span>

* <span data-ttu-id="5cf80-146">Pontos de extremidade</span><span class="sxs-lookup"><span data-stu-id="5cf80-146">Endpoints</span></span>  
* <span data-ttu-id="5cf80-147">Endereços IP</span><span class="sxs-lookup"><span data-stu-id="5cf80-147">IP addresses</span></span>  
* <span data-ttu-id="5cf80-148">Discos</span><span class="sxs-lookup"><span data-stu-id="5cf80-148">Disks</span></span>  
* <span data-ttu-id="5cf80-149">Extensões</span><span class="sxs-lookup"><span data-stu-id="5cf80-149">Extensions</span></span>  

<span data-ttu-id="5cf80-150">Essas tarefas exigem **gravar** saudação do acesso tooboth **Máquina Virtual**e hello **grupo de recursos** (junto com o nome de domínio Olá) que ele está em:</span><span class="sxs-lookup"><span data-stu-id="5cf80-150">These require **write** access tooboth hello **Virtual machine**, and hello **Resource group** (along with hello Domain name) that it is in:</span></span>  

* <span data-ttu-id="5cf80-151">Conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="5cf80-151">Availability set</span></span>  
* <span data-ttu-id="5cf80-152">Conjunto de balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="5cf80-152">Load balanced set</span></span>  
* <span data-ttu-id="5cf80-153">Regras de alerta</span><span class="sxs-lookup"><span data-stu-id="5cf80-153">Alert rules</span></span>  

<span data-ttu-id="5cf80-154">Se você não pode acessar qualquer um desses blocos, peça ao administrador para o grupo de recursos de toohello de acesso de Colaborador.</span><span class="sxs-lookup"><span data-stu-id="5cf80-154">If you can't access any of these tiles, ask your administrator for Contributor access toohello Resource group.</span></span>

## <a name="see-more"></a><span data-ttu-id="5cf80-155">Veja mais</span><span class="sxs-lookup"><span data-stu-id="5cf80-155">See more</span></span>
* <span data-ttu-id="5cf80-156">[Controle de acesso baseado em função](role-based-access-control-configure.md): Introdução ao RBAC em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5cf80-156">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in hello Azure portal.</span></span>
* <span data-ttu-id="5cf80-157">[Funções internas](role-based-access-built-in-roles.md): obter detalhes sobre as funções hello incluídos por padrão em RBAC.</span><span class="sxs-lookup"><span data-stu-id="5cf80-157">[Built-in roles](role-based-access-built-in-roles.md): Get details about hello roles that come standard in RBAC.</span></span>
* <span data-ttu-id="5cf80-158">[Funções personalizadas no Azure RBAC](role-based-access-control-custom-roles.md): Saiba como toocreate funções personalizadas toofit sua necessidades de acesso.</span><span class="sxs-lookup"><span data-stu-id="5cf80-158">[Custom roles in Azure RBAC](role-based-access-control-custom-roles.md): Learn how toocreate custom roles toofit your access needs.</span></span>
* <span data-ttu-id="5cf80-159">[Criar um relatório de histórico de alterações de acesso](role-based-access-control-access-change-history-report.md): mantenha o controle das alterações de atribuições de função no RBAC.</span><span class="sxs-lookup"><span data-stu-id="5cf80-159">[Create an access change history report](role-based-access-control-access-change-history-report.md): Keep track of changing role assignments in RBAC.</span></span>

