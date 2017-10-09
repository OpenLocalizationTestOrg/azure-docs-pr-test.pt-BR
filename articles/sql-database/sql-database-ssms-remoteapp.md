---
title: aaaConnect tooSQL banco de dados usando o SQL Server Management Studio no Azure RemoteApp | Microsoft Docs
description: "Use este tutorial toolearn como toouse SQL Server Management Studio no Azure RemoteApp para segurança e desempenho ao se conectar tooSQL banco de dados"
services: sql-database
documentationcenter: 
author: adhurwit
manager: jhubbard
ms.assetid: 1052c83c-e7f5-4736-922f-216194d8874b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: adhurwit
ms.openlocfilehash: 73994f9a1eb3e48efa5d7c4f976b00cfcbc88d75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-tooconnect-toosql-database"></a><span data-ttu-id="b58c2-103">Use o SQL Server Management Studio no Azure RemoteApp tooconnect tooSQL banco de dados</span><span class="sxs-lookup"><span data-stu-id="b58c2-103">Use SQL Server Management Studio in Azure RemoteApp tooconnect tooSQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b58c2-104">O RemoteApp do Azure está sendo descontinuado.</span><span class="sxs-lookup"><span data-stu-id="b58c2-104">Azure RemoteApp is being discontinued.</span></span> <span data-ttu-id="b58c2-105">Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="b58c2-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
>

## <a name="introduction"></a><span data-ttu-id="b58c2-106">Introdução</span><span class="sxs-lookup"><span data-stu-id="b58c2-106">Introduction</span></span>
<span data-ttu-id="b58c2-107">Este tutorial mostra como toouse SQL Server Management Studio (SSMS) no Azure RemoteApp tooconnect tooSQL banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b58c2-107">This tutorial shows you how toouse SQL Server Management Studio (SSMS) in Azure RemoteApp tooconnect tooSQL Database.</span></span> <span data-ttu-id="b58c2-108">Ele orienta você pelo processo de saudação de configurar o SQL Server Management Studio no Azure RemoteApp, explica os benefícios de saudação e mostra os recursos de segurança que você pode usar no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b58c2-108">It walks you through hello process of setting up SQL Server Management Studio in Azure RemoteApp, explains hello benefits, and shows security features that you can use in Azure Active Directory.</span></span>

<span data-ttu-id="b58c2-109">**Estimado tempo toocomplete:** 45 minutos</span><span class="sxs-lookup"><span data-stu-id="b58c2-109">**Estimated time toocomplete:** 45 minutes</span></span>

## <a name="ssms-in-azure-remoteapp"></a><span data-ttu-id="b58c2-110">SSMS no Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="b58c2-110">SSMS in Azure RemoteApp</span></span>
<span data-ttu-id="b58c2-111">O Azure RemoteApp é um serviço RDS no Azure que fornece aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b58c2-111">Azure RemoteApp is an RDS service in Azure that delivers applications.</span></span> <span data-ttu-id="b58c2-112">Saiba mais sobre ele aqui: [O que é o RemoteApp?](../remoteapp/remoteapp-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="b58c2-112">You can learn more about it here: [What is RemoteApp?](../remoteapp/remoteapp-whatis.md)</span></span>

<span data-ttu-id="b58c2-113">SSMS em execução no Azure RemoteApp permite você Olá mesma experiência como executando o SSMS localmente.</span><span class="sxs-lookup"><span data-stu-id="b58c2-113">SSMS running in Azure RemoteApp gives you hello same experience as running SSMS locally.</span></span>

![Captura de tela mostrando o SSMS em execução no Azure RemoteApp][1]

## <a name="benefits"></a><span data-ttu-id="b58c2-115">Benefícios</span><span class="sxs-lookup"><span data-stu-id="b58c2-115">Benefits</span></span>
<span data-ttu-id="b58c2-116">Há muitos benefícios toousing SSMS no Azure RemoteApp, incluindo:</span><span class="sxs-lookup"><span data-stu-id="b58c2-116">There are many benefits toousing SSMS in Azure RemoteApp, including:</span></span>

* <span data-ttu-id="b58c2-117">A porta 1433 no Azure SQL server não tem toobe exposta externamente (fora do Azure).</span><span class="sxs-lookup"><span data-stu-id="b58c2-117">Port 1433 on Azure SQL server does not have toobe exposed externally (outside of Azure).</span></span>
* <span data-ttu-id="b58c2-118">Nenhum tookeep necessidade, adicionando e removendo endereços IP no firewall de servidor do SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b58c2-118">No need tookeep adding and removing IP addresses in hello Azure SQL server firewall.</span></span>
* <span data-ttu-id="b58c2-119">Todas as conexões do Azure RemoteApp ocorrem por HTTPS na porta 443 usando o protocolo de Área de Trabalho Remota</span><span class="sxs-lookup"><span data-stu-id="b58c2-119">All Azure RemoteApp connections occur over HTTPS on port 443 using encrypted Remote Desktop protocol</span></span>
* <span data-ttu-id="b58c2-120">Ele é multiusuário e pode ser dimensionado.</span><span class="sxs-lookup"><span data-stu-id="b58c2-120">It is multi-user and can scale.</span></span>
* <span data-ttu-id="b58c2-121">Há um ganho de desempenho de se ter o SSMS em Olá mesma região Olá banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="b58c2-121">There is a performance gain from having SSMS in hello same region as hello SQL Database.</span></span>
* <span data-ttu-id="b58c2-122">Você pode auditar o uso do Azure RemoteApp com a edição Premium Olá do Active Directory do Azure que tem relatórios de atividade do usuário.</span><span class="sxs-lookup"><span data-stu-id="b58c2-122">You can audit use of Azure RemoteApp with hello Premium edition of Azure Active Directory which has user activity reports.</span></span>
* <span data-ttu-id="b58c2-123">Você pode habilitar a MFA (Multi-Factor Authentication).</span><span class="sxs-lookup"><span data-stu-id="b58c2-123">You can enable multi-factor authentication (MFA).</span></span>
* <span data-ttu-id="b58c2-124">Acesso SSMS em qualquer lugar ao usar qualquer um dos Olá clientes com suporte do Azure RemoteApp que inclui o iOS, Android, Mac, Windows Phone e Windows PC.</span><span class="sxs-lookup"><span data-stu-id="b58c2-124">Access SSMS anywhere when using any of hello supported Azure RemoteApp clients which includes iOS, Android, Mac, Windows Phone, and Windows PC’s.</span></span>

## <a name="create-hello-azure-remoteapp-collection"></a><span data-ttu-id="b58c2-125">Criar coleção do Azure RemoteApp Olá</span><span class="sxs-lookup"><span data-stu-id="b58c2-125">Create hello Azure RemoteApp collection</span></span>
<span data-ttu-id="b58c2-126">Aqui está Olá etapas toocreate sua coleção do RemoteApp do Azure com o SSMS:</span><span class="sxs-lookup"><span data-stu-id="b58c2-126">Here are hello steps toocreate your Azure RemoteApp collection with SSMS:</span></span>

### <a name="1-create-a-new-windows-vm-from-image"></a><span data-ttu-id="b58c2-127">1. Criar uma nova VM do Windows a partir da Imagem</span><span class="sxs-lookup"><span data-stu-id="b58c2-127">1. Create a new Windows VM from Image</span></span>
<span data-ttu-id="b58c2-128">Use hello "Windows Server Remote Desktop sessão hosts Windows Server 2012 R2" imagem da saudação Galeria toomake sua nova VM.</span><span class="sxs-lookup"><span data-stu-id="b58c2-128">Use hello "Windows Server Remote Desktop Session Host Windows Server 2012 R2" Image from hello Gallery toomake your new VM.</span></span>

### <a name="2-install-ssms-from-sql-express"></a><span data-ttu-id="b58c2-129">2. Instalar o SSMS do SQL Express</span><span class="sxs-lookup"><span data-stu-id="b58c2-129">2. Install SSMS from SQL Express</span></span>
<span data-ttu-id="b58c2-130">Vá para Olá nova VM e navegar a página de download do toothis: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span><span class="sxs-lookup"><span data-stu-id="b58c2-130">Go onto hello new VM and navigate toothis download page: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span></span>

<span data-ttu-id="b58c2-131">Há um download de tooonly opção SSMS.</span><span class="sxs-lookup"><span data-stu-id="b58c2-131">There is an option tooonly download SSMS.</span></span> <span data-ttu-id="b58c2-132">Após o download, vá para o diretório de instalação do hello e execute a instalação tooinstall SSMS.</span><span class="sxs-lookup"><span data-stu-id="b58c2-132">After download, go into hello install directory and run Setup tooinstall SSMS.</span></span>

<span data-ttu-id="b58c2-133">Você também precisa tooinstall SQL Server 2014 Service Pack 1.</span><span class="sxs-lookup"><span data-stu-id="b58c2-133">You also need tooinstall SQL Server 2014 Service Pack 1.</span></span> <span data-ttu-id="b58c2-134">Você pode baixá-lo aqui: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span><span class="sxs-lookup"><span data-stu-id="b58c2-134">You can download it here: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span></span>

<span data-ttu-id="b58c2-135">O SQL Server 2014 Service Pack 1 inclui uma funcionalidade essencial para trabalhar com o Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="b58c2-135">SQL Server 2014 Service Pack 1 includes essential functionality for working with Azure SQL Database.</span></span>

### <a name="3-run-validate-script-and-sysprep"></a><span data-ttu-id="b58c2-136">3. Executar o script Validate e o Sysprep</span><span class="sxs-lookup"><span data-stu-id="b58c2-136">3. Run Validate script and Sysprep</span></span>
<span data-ttu-id="b58c2-137">Em Olá a área de trabalho do hello VM é um script PowerShell chamado validar.</span><span class="sxs-lookup"><span data-stu-id="b58c2-137">On hello desktop of hello VM is a PowerShell script called Validate.</span></span> <span data-ttu-id="b58c2-138">Execute-o clicando duas vezes nele.</span><span class="sxs-lookup"><span data-stu-id="b58c2-138">Run this by double-clicking.</span></span> <span data-ttu-id="b58c2-139">Ele verificará que Olá VM está pronto toobe usado para hospedar remoto de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b58c2-139">It will verify that hello VM is ready toobe used for remote hosting of applications.</span></span> <span data-ttu-id="b58c2-140">Quando a verificação for concluída, ela solicitará toorun sysprep - escolha toorun-lo.</span><span class="sxs-lookup"><span data-stu-id="b58c2-140">When verification is complete, it will ask toorun sysprep - choose toorun it.</span></span>

<span data-ttu-id="b58c2-141">Quando o sysprep for concluído, ele será encerrado Olá VM.</span><span class="sxs-lookup"><span data-stu-id="b58c2-141">When sysprep completes, it will shut down hello VM.</span></span>

<span data-ttu-id="b58c2-142">toolearn mais sobre como criar uma imagem do RemoteApp do Azure, consulte: [como toocreate um modelo do RemoteApp da imagem no Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="b58c2-142">toolearn more about creating a Azure RemoteApp image, see: [How toocreate a RemoteApp template image in Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span></span>

### <a name="4-capture-image"></a><span data-ttu-id="b58c2-143">4. Capturar a imagem</span><span class="sxs-lookup"><span data-stu-id="b58c2-143">4. Capture image</span></span>
<span data-ttu-id="b58c2-144">Quando a saudação VM parou de funcionar, encontrá-lo no portal atual do hello e capturá-lo.</span><span class="sxs-lookup"><span data-stu-id="b58c2-144">When hello VM has stopped running, find it in hello current portal and capture it.</span></span>

<span data-ttu-id="b58c2-145">toolearn mais sobre como capturar uma imagem, consulte [capturar uma imagem de uma máquina virtual do Windows Azure criada com o modelo de implantação clássico Olá](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="b58c2-145">toolearn more about capturing an image, see [Capture an image of an Azure Windows virtual machine created with hello classic deployment model](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

### <a name="5-add-tooazure-remoteapp-template-images"></a><span data-ttu-id="b58c2-146">5. Adicionar imagens de modelo do RemoteApp tooAzure</span><span class="sxs-lookup"><span data-stu-id="b58c2-146">5. Add tooAzure RemoteApp Template images</span></span>
<span data-ttu-id="b58c2-147">Em hello Azure RemoteApp seção portal atual do hello, vá toohello guia de imagens de modelo e clique em Adicionar.</span><span class="sxs-lookup"><span data-stu-id="b58c2-147">In hello Azure RemoteApp section of hello current portal, go toohello Template Images tab and click Add.</span></span> <span data-ttu-id="b58c2-148">Na caixa de pop-up hello, selecione "Importar uma imagem de sua biblioteca de máquinas virtuais" e, em seguida, escolha Olá imagem que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="b58c2-148">In hello pop-up box, select "Import an image from your Virtual Machines library" and then choose hello Image that you just created.</span></span>

### <a name="6-create-cloud-collection"></a><span data-ttu-id="b58c2-149">6. Criar uma coleção na nuvem</span><span class="sxs-lookup"><span data-stu-id="b58c2-149">6. Create cloud collection</span></span>
<span data-ttu-id="b58c2-150">No portal atual do hello, crie uma nova coleção de nuvem do RemoteApp do Azure.</span><span class="sxs-lookup"><span data-stu-id="b58c2-150">In hello current portal, create a new Azure RemoteApp Cloud Collection.</span></span> <span data-ttu-id="b58c2-151">Escolha Olá imagem de modelo que você acabou de importar com o SSMS instalado nele.</span><span class="sxs-lookup"><span data-stu-id="b58c2-151">Choose hello Template Image that you just imported with SSMS installed on it.</span></span>

![Criar uma nova coleção na nuvem][2]

### <a name="7-publish-ssms"></a><span data-ttu-id="b58c2-153">7. Publicar o SSMS</span><span class="sxs-lookup"><span data-stu-id="b58c2-153">7. Publish SSMS</span></span>
<span data-ttu-id="b58c2-154">Em Olá publicando guia da sua nova coleção de nuvem, selecione publicar um aplicativo do hello Menu Iniciar e escolha SSMS da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="b58c2-154">On hello Publishing tab of your new cloud collection, select Publish an application from hello Start Menu and then choose SSMS from hello list.</span></span>

![Publicar aplicativo][5]

### <a name="8-add-users"></a><span data-ttu-id="b58c2-156">8. Adicionar usuários</span><span class="sxs-lookup"><span data-stu-id="b58c2-156">8. Add users</span></span>
<span data-ttu-id="b58c2-157">Na guia de acesso do usuário hello, você pode selecionar usuários Olá que terão acesso toothis Azure RemoteApp coleção que inclui apenas o SSMS.</span><span class="sxs-lookup"><span data-stu-id="b58c2-157">On hello User Access tab you can select hello users that will have access toothis Azure RemoteApp collection which only includes SSMS.</span></span>

![Adicionar usuário][6]

### <a name="9-install-hello-azure-remoteapp-client-application"></a><span data-ttu-id="b58c2-159">9. Instalar o aplicativo de cliente hello Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="b58c2-159">9. Install hello Azure RemoteApp client application</span></span>
<span data-ttu-id="b58c2-160">Você pode baixar e instalar um cliente do Azure RemoteApp aqui: [Baixar | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span><span class="sxs-lookup"><span data-stu-id="b58c2-160">You can download and install a Azure RemoteApp client here: [Download | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span></span>

## <a name="configure-azure-sql-server"></a><span data-ttu-id="b58c2-161">Configurar o Azure SQL Server</span><span class="sxs-lookup"><span data-stu-id="b58c2-161">Configure Azure SQL server</span></span>
<span data-ttu-id="b58c2-162">Olá somente a configuração necessária é tooensure serviços do Azure está habilitada para o firewall hello.</span><span class="sxs-lookup"><span data-stu-id="b58c2-162">hello only configuration needed is tooensure that Azure Services is enabled for hello firewall.</span></span> <span data-ttu-id="b58c2-163">Se você usar essa solução, em seguida, você não precisa tooadd qualquer firewall de saudação do tooopen de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="b58c2-163">If you use this solution, then you do not need tooadd any IP addresses tooopen hello firewall.</span></span> <span data-ttu-id="b58c2-164">tráfego de rede de saudação é permitido toohello do SQL Server é de outros serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="b58c2-164">hello network traffic that is allowed toohello SQL Server is from other Azure services.</span></span>

![Permissão do Azure][4]

## <a name="multi-factor-authentication-mfa"></a><span data-ttu-id="b58c2-166">Multi-Factor Authentication (MFA)</span><span class="sxs-lookup"><span data-stu-id="b58c2-166">Multi-Factor Authentication (MFA)</span></span>
<span data-ttu-id="b58c2-167">A MFA pode ser habilitada especificamente para esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b58c2-167">MFA can be enabled for this application specifically.</span></span> <span data-ttu-id="b58c2-168">Vá toohello guia de aplicativos do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="b58c2-168">Go toohello Applications tab of your Azure Active Directory.</span></span> <span data-ttu-id="b58c2-169">Você encontrará uma entrada para o Microsoft Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="b58c2-169">You will find an entry for Microsoft Azure RemoteApp.</span></span> <span data-ttu-id="b58c2-170">Se você clicar nesse aplicativo e, em seguida, configurar, você verá a página de saudação abaixo onde você pode habilitar a MFA para este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b58c2-170">If you click that application and then configure, you will see hello page below where you can enable MFA for this application.</span></span>

![Habilitar MFA][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a><span data-ttu-id="b58c2-172">Auditar a atividade do usuário com o Active Directory Premium do Azure</span><span class="sxs-lookup"><span data-stu-id="b58c2-172">Audit user activity with Azure Active Directory Premium</span></span>
<span data-ttu-id="b58c2-173">Se você não tiver Azure AD Premium, você terá que tooturn-lo no hello seção licenças do seu diretório.</span><span class="sxs-lookup"><span data-stu-id="b58c2-173">If you do not have Azure AD Premium, then you have tooturn it on in hello Licenses section of your directory.</span></span> <span data-ttu-id="b58c2-174">Com o Premium ativado, você pode atribuir usuários toohello nível de Premium.</span><span class="sxs-lookup"><span data-stu-id="b58c2-174">With Premium enabled, you can assign users toohello Premium level.</span></span>

<span data-ttu-id="b58c2-175">Quando você for um usuário tooa no Active Directory do Azure, em seguida, você pode ir toohello atividade guia toosee logon informações tooAzure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="b58c2-175">When you go tooa user in your Azure Active Directory, you can then go toohello Activity tab toosee login information tooAzure RemoteApp.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b58c2-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b58c2-176">Next steps</span></span>
<span data-ttu-id="b58c2-177">Depois de concluir todas as Olá acima etapas, você será capaz de toorun hello Azure RemoteApp cliente e log com um usuário atribuído.</span><span class="sxs-lookup"><span data-stu-id="b58c2-177">After completing all hello above steps, you will be able toorun hello Azure RemoteApp client and log-in with an assigned user.</span></span> <span data-ttu-id="b58c2-178">Você verá SSMS como um de seus aplicativos e execute-o como você faria se estivesse instalado em seu computador com tooAzure acessar o SQL server.</span><span class="sxs-lookup"><span data-stu-id="b58c2-178">You will be presented with SSMS as one of your applications, and you can run it as you would if it were installed on your computer with access tooAzure SQL server.</span></span>

<span data-ttu-id="b58c2-179">Para obter mais informações sobre como toomake Olá conexão tooSQL banco de dados, consulte [conectar tooSQL banco de dados com o SQL Server Management Studio e executar um exemplo de consulta T-SQL](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="b58c2-179">For more information on how toomake hello connection tooSQL Database, see [Connect tooSQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>

<span data-ttu-id="b58c2-180">Isso é tudo por enquanto.</span><span class="sxs-lookup"><span data-stu-id="b58c2-180">That's everything for now.</span></span> <span data-ttu-id="b58c2-181">Aproveite!</span><span class="sxs-lookup"><span data-stu-id="b58c2-181">Enjoy!</span></span>

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png