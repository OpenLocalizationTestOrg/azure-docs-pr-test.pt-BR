---
title: "aaaUsing área de trabalho remota com funções do Azure | Microsoft Docs"
description: "Usando a Área de Trabalho Remota com as funções do Azure"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f5727ebe-9f57-4d7d-aff1-58761e8de8c1
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d35fd421cde8be9e3caa474db95974a54e528bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-with-azure-roles"></a><span data-ttu-id="e29e0-103">Usando a Área de Trabalho Remota com as funções do Azure</span><span class="sxs-lookup"><span data-stu-id="e29e0-103">Using Remote Desktop with Azure Roles</span></span>
<span data-ttu-id="e29e0-104">Por meio de saudação do SDK do Azure e os serviços de área de trabalho remota, você pode acessar as funções do Azure e máquinas virtuais que são hospedadas pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="e29e0-104">By using hello Azure SDK and Remote Desktop Services, you can access Azure roles and virtual machines that are hosted by Azure.</span></span> <span data-ttu-id="e29e0-105">No Visual Studio, você pode configurar os Serviços de Área de Trabalho Remota por meio de um projeto de serviço de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="e29e0-105">In Visual Studio, you can configure Remote Desktop Services from an Azure cloud service project.</span></span> <span data-ttu-id="e29e0-106">tooenable de serviços de área de trabalho remota, você deve criar um projeto de trabalho que contém uma ou mais funções e, em seguida, publicá-lo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e29e0-106">tooenable Remote Desktop Services, you must create a working project that contains one or more roles and then publish it tooAzure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e29e0-107">Você deve acessar uma função do Azure apenas para desenvolvimento ou solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="e29e0-107">You should access an Azure role for troubleshooting or development only.</span></span> <span data-ttu-id="e29e0-108">Olá a finalidade de cada máquina virtual é toorun uma função específica em seu aplicativo do Azure, não toorun outros aplicativos cliente.</span><span class="sxs-lookup"><span data-stu-id="e29e0-108">hello purpose of each virtual machine is toorun a specific role in your Azure application, not toorun other client applications.</span></span> <span data-ttu-id="e29e0-109">Se você quiser toouse Azure toohost uma máquina virtual que você pode usar para qualquer finalidade, consulte Acessando máquinas virtuais do Azure do Gerenciador de servidores.</span><span class="sxs-lookup"><span data-stu-id="e29e0-109">If you want toouse Azure toohost a virtual machine that you can use for any purpose, see Accessing Azure Virtual Machines from Server Explorer.</span></span>
> 
> 

## <a name="tooenable-and-use-remote-desktop-for-an-azure-role"></a><span data-ttu-id="e29e0-110">tooenable e use a área de trabalho remota para uma função do Azure</span><span class="sxs-lookup"><span data-stu-id="e29e0-110">tooenable and use Remote Desktop for an Azure Role</span></span>
1. <span data-ttu-id="e29e0-111">No Gerenciador de soluções, abrir o menu de atalho de saudação para seu projeto de serviço de nuvem e, em seguida, escolha **publicar**.</span><span class="sxs-lookup"><span data-stu-id="e29e0-111">In Solution Explorer, open hello shortcut menu for your cloud service project, and then choose **Publish**.</span></span>
   
    <span data-ttu-id="e29e0-112">Olá **publicar aplicativo do Azure** assistente é exibido.</span><span class="sxs-lookup"><span data-stu-id="e29e0-112">hello **Publish Azure Application** wizard appears.</span></span>
   
    ![Publicar o comando para um projeto de Serviço de Nuvem](./media/vs-azure-tools-remote-desktop-roles/IC799161.png)
2. <span data-ttu-id="e29e0-114">Na parte inferior de saudação do **configurações de publicação do Microsoft Azure** página do Assistente de saudação, selecione Olá **habilitar área de trabalho remota** todas as funções caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="e29e0-114">At hello bottom of **Microsoft Azure Publish Settings** page of hello wizard, select hello **Enable Remote Desktop** for all roles check box.</span></span> 
   
    <span data-ttu-id="e29e0-115">Olá **configuração da área de trabalho remota** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="e29e0-115">hello **Remote Desktop Configuration** dialog box appears.</span></span>
3. <span data-ttu-id="e29e0-116">Na parte inferior de saudação do hello **configuração da área de trabalho remota** caixa de diálogo caixa, escolha Olá **mais opções** botão.</span><span class="sxs-lookup"><span data-stu-id="e29e0-116">At hello bottom of hello **Remote Desktop Configuration** dialog box, choose hello **More Options** button.</span></span> 
   
    <span data-ttu-id="e29e0-117">Isso exibe uma caixa de listagem suspensa que permite que você crie ou escolha um certificado para que você possa criptografar informações de credenciais ao conectar-se via área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="e29e0-117">This displays a dropdown list box that lets you create or choose a certificate so that you can encrypt credentials information when connecting via remote desktop.</span></span>
4. <span data-ttu-id="e29e0-118">Na lista suspensa de saudação, escolha  **&lt;criar >**, ou escolha um existente na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="e29e0-118">In hello dropdown list, choose **&lt;Create>**, or choose an existing one from hello list.</span></span> 
   
    <span data-ttu-id="e29e0-119">Se você escolher um certificado existente, ignore Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="e29e0-119">If you choose an existing certificate, skip hello following steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e29e0-120">certificados de saudação que é necessário para uma conexão de área de trabalho remota são diferentes dos certificados de saudação que você usa para outras operações do Azure.</span><span class="sxs-lookup"><span data-stu-id="e29e0-120">hello certificates that you need for a remote desktop connection are different from hello certificates that you use for other Azure operations.</span></span> <span data-ttu-id="e29e0-121">certificado de acesso remoto Olá deve ter uma chave privada.</span><span class="sxs-lookup"><span data-stu-id="e29e0-121">hello remote access certificate must have a private key.</span></span>
   > 
   > 
   
    <span data-ttu-id="e29e0-122">Olá **Create Certificate** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="e29e0-122">hello **Create Certificate** dialog box appears.</span></span>
   
   1. <span data-ttu-id="e29e0-123">Forneça um nome amigável para o novo certificado de saudação e escolha Olá **Okey** botão.</span><span class="sxs-lookup"><span data-stu-id="e29e0-123">Provide a friendly name for hello new certificate, and then choose hello **OK** button.</span></span> <span data-ttu-id="e29e0-124">novo certificado de saudação aparece na caixa de listagem suspensa hello.</span><span class="sxs-lookup"><span data-stu-id="e29e0-124">hello new certificate appears in hello dropdown list box.</span></span>
   2. <span data-ttu-id="e29e0-125">Em Olá **configuração da área de trabalho remota** caixa de diálogo caixa, forneça um nome de usuário e uma senha.</span><span class="sxs-lookup"><span data-stu-id="e29e0-125">In hello **Remote Desktop Configuration** dialog box, provide a user name and a password.</span></span>
      
       <span data-ttu-id="e29e0-126">Você não pode usar uma conta existente.</span><span class="sxs-lookup"><span data-stu-id="e29e0-126">You can’t use an existing account.</span></span> <span data-ttu-id="e29e0-127">Não especifique um administrador como nome de usuário de Olá para a nova conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="e29e0-127">Don’t specify Administrator as hello user name for hello new account.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="e29e0-128">Se a senha de saudação não atende aos requisitos de complexidade de saudação, um ícone vermelho aparece próxima caixa de texto de senha toohello.</span><span class="sxs-lookup"><span data-stu-id="e29e0-128">If hello password doesn’t meet hello complexity requirements, a red icon appears next toohello password text box.</span></span> <span data-ttu-id="e29e0-129">senha de saudação deve incluir letras maiusculas, letras minúsculas e números ou símbolos.</span><span class="sxs-lookup"><span data-stu-id="e29e0-129">hello password must include capital letters, lowercase letters, and numbers or symbols.</span></span>
      > 
      > 
   3. <span data-ttu-id="e29e0-130">Escolha uma data na qual conta Olá irá expirar e depois quais conexões de área de trabalho remotas serão bloqueados.</span><span class="sxs-lookup"><span data-stu-id="e29e0-130">Choose a date on which hello account will expire and after which remote desktop connections will be blocked.</span></span>
   4. <span data-ttu-id="e29e0-131">Depois de ter fornecido todas as informações necessárias de hello, escolha Olá **Okey** botão.</span><span class="sxs-lookup"><span data-stu-id="e29e0-131">After you've provided all hello required information, choose hello **OK** button.</span></span>
      
       <span data-ttu-id="e29e0-132">Várias configurações que permitem que os serviços de acesso remoto são adicionadas toohello. cscfg e. csdef arquivos.</span><span class="sxs-lookup"><span data-stu-id="e29e0-132">Several settings that enable Remote Access Services are added toohello .cscfg and .csdef files.</span></span>
5. <span data-ttu-id="e29e0-133">Em Olá **configurações de publicação do Microsoft Azure** assistente, escolha Olá **Okey** botão quando estiver pronto toopublish seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="e29e0-133">In hello **Microsoft Azure Publish Settings** wizard, choose hello **OK** button when you’re ready toopublish your cloud service.</span></span>
   
    <span data-ttu-id="e29e0-134">Se você não tiver toopublish pronto, escolha Olá **Cancelar** botão.</span><span class="sxs-lookup"><span data-stu-id="e29e0-134">If you're not ready toopublish, choose hello **Cancel** button.</span></span> <span data-ttu-id="e29e0-135">Olá configurações são salvas, e você pode publicar seu serviço de nuvem mais tarde.</span><span class="sxs-lookup"><span data-stu-id="e29e0-135">hello configuration settings are saved, and you can publish your cloud service later.</span></span>

## <a name="connect-tooan-azure-role-by-using-remote-desktop"></a><span data-ttu-id="e29e0-136">Conecte-se tooan função do Azure usando a área de trabalho remota</span><span class="sxs-lookup"><span data-stu-id="e29e0-136">Connect tooan Azure Role by using Remote Desktop</span></span>
<span data-ttu-id="e29e0-137">Depois de publicar seu serviço de nuvem no Azure, você pode usar toolog do Gerenciador de servidores em máquinas virtuais Olá que hospeda do Azure.</span><span class="sxs-lookup"><span data-stu-id="e29e0-137">After you publish your cloud service on Azure, you can use Server Explorer toolog into hello virtual machines that Azure hosts.</span></span> 

1. <span data-ttu-id="e29e0-138">No Gerenciador de servidores, expanda Olá **Azure** nó e, em seguida, expanda o nó de saudação de um serviço de nuvem e uma das sua funções toodisplay uma lista de instâncias.</span><span class="sxs-lookup"><span data-stu-id="e29e0-138">In Server Explorer, expand hello **Azure** node, and then expand hello node for a cloud service and one of its roles toodisplay a list of instances.</span></span>
2. <span data-ttu-id="e29e0-139">Abrir menu de atalho Olá para um nó da instância e, em seguida, escolha **se conectar usando área de trabalho remota**.</span><span class="sxs-lookup"><span data-stu-id="e29e0-139">Open hello shortcut menu for an instance node, and then choose **Connect Using Remote Desktop**.</span></span>
   
    ![Conectando-se via área de trabalho remota](./media/vs-azure-tools-remote-desktop-roles/IC799162.png)
3. <span data-ttu-id="e29e0-141">Insira o nome de usuário de saudação e a senha que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e29e0-141">Enter hello user name and password that you created previously.</span></span> <span data-ttu-id="e29e0-142">Agora você está conectado na sessão remota.</span><span class="sxs-lookup"><span data-stu-id="e29e0-142">You are now logged into your remote session.</span></span>

