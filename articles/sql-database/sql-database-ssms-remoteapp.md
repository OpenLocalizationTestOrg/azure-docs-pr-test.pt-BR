---
title: Conectar Banco de Dados SQL usando o SQL Server Management Studio no Azure RemoteApp | Microsoft Docs
description: "Use este tutorial para aprender a usar o SQL Server Management Studio no Azure RemoteApp para segurança e desempenho ao se conectar ao Banco de Dados SQL"
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
ms.openlocfilehash: ae1f2fa38d38fe6c10bc7960fddb07ae330d1eeb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-to-connect-to-sql-database"></a><span data-ttu-id="319cf-103">Usar o SQL Server Management Studio no Azure RemoteApp para conectar-se ao Banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="319cf-103">Use SQL Server Management Studio in Azure RemoteApp to connect to SQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="319cf-104">O RemoteApp do Azure está sendo descontinuado.</span><span class="sxs-lookup"><span data-stu-id="319cf-104">Azure RemoteApp is being discontinued.</span></span> <span data-ttu-id="319cf-105">Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="319cf-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
>

## <a name="introduction"></a><span data-ttu-id="319cf-106">Introdução</span><span class="sxs-lookup"><span data-stu-id="319cf-106">Introduction</span></span>
<span data-ttu-id="319cf-107">Este tutorial mostra como usar o SQL Server Management Studio (SSMS) no RemoteApp do Azure para conectar-se ao Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="319cf-107">This tutorial shows you how to use SQL Server Management Studio (SSMS) in Azure RemoteApp to connect to SQL Database.</span></span> <span data-ttu-id="319cf-108">Ele fornece uma orientação pelo processo de configuração do SQL Server Management Studio no Azure RemoteApp, explica os benefícios e mostra os recursos de segurança que podem ser usados no Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="319cf-108">It walks you through the process of setting up SQL Server Management Studio in Azure RemoteApp, explains the benefits, and shows security features that you can use in Azure Active Directory.</span></span>

<span data-ttu-id="319cf-109">**Tempo estimado para conclusão:** 45 minutos</span><span class="sxs-lookup"><span data-stu-id="319cf-109">**Estimated time to complete:** 45 minutes</span></span>

## <a name="ssms-in-azure-remoteapp"></a><span data-ttu-id="319cf-110">SSMS no Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="319cf-110">SSMS in Azure RemoteApp</span></span>
<span data-ttu-id="319cf-111">O Azure RemoteApp é um serviço RDS no Azure que fornece aplicativos.</span><span class="sxs-lookup"><span data-stu-id="319cf-111">Azure RemoteApp is an RDS service in Azure that delivers applications.</span></span> <span data-ttu-id="319cf-112">Saiba mais sobre ele aqui: [O que é o RemoteApp?](../remoteapp/remoteapp-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="319cf-112">You can learn more about it here: [What is RemoteApp?](../remoteapp/remoteapp-whatis.md)</span></span>

<span data-ttu-id="319cf-113">O SSMS em execução no Azure RemoteApp fornece a mesma experiência que a execução local do SSMS.</span><span class="sxs-lookup"><span data-stu-id="319cf-113">SSMS running in Azure RemoteApp gives you the same experience as running SSMS locally.</span></span>

![Captura de tela mostrando o SSMS em execução no Azure RemoteApp][1]

## <a name="benefits"></a><span data-ttu-id="319cf-115">Benefícios</span><span class="sxs-lookup"><span data-stu-id="319cf-115">Benefits</span></span>
<span data-ttu-id="319cf-116">Há muitos benefícios no uso do SSMS no Azure RemoteApp, incluindo:</span><span class="sxs-lookup"><span data-stu-id="319cf-116">There are many benefits to using SSMS in Azure RemoteApp, including:</span></span>

* <span data-ttu-id="319cf-117">A porta 1433 no Azure SQL Server não precisa ser exposta externamente (fora do Azure).</span><span class="sxs-lookup"><span data-stu-id="319cf-117">Port 1433 on Azure SQL server does not have to be exposed externally (outside of Azure).</span></span>
* <span data-ttu-id="319cf-118">Não há necessidade de continuar a adicionar e remover endereços IP no firewall do Azure SQL Server.</span><span class="sxs-lookup"><span data-stu-id="319cf-118">No need to keep adding and removing IP addresses in the Azure SQL server firewall.</span></span>
* <span data-ttu-id="319cf-119">Todas as conexões do Azure RemoteApp ocorrem por HTTPS na porta 443 usando o protocolo de Área de Trabalho Remota</span><span class="sxs-lookup"><span data-stu-id="319cf-119">All Azure RemoteApp connections occur over HTTPS on port 443 using encrypted Remote Desktop protocol</span></span>
* <span data-ttu-id="319cf-120">Ele é multiusuário e pode ser dimensionado.</span><span class="sxs-lookup"><span data-stu-id="319cf-120">It is multi-user and can scale.</span></span>
* <span data-ttu-id="319cf-121">Há um ganho de desempenho por ter o SSMS na mesma região que o Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="319cf-121">There is a performance gain from having SSMS in the same region as the SQL Database.</span></span>
* <span data-ttu-id="319cf-122">Você pode auditar o uso do Azure RemoteApp com o Active Directory do Azure Premium Edition, que tem relatórios de atividade do usuário.</span><span class="sxs-lookup"><span data-stu-id="319cf-122">You can audit use of Azure RemoteApp with the Premium edition of Azure Active Directory which has user activity reports.</span></span>
* <span data-ttu-id="319cf-123">Você pode habilitar a MFA (Multi-Factor Authentication).</span><span class="sxs-lookup"><span data-stu-id="319cf-123">You can enable multi-factor authentication (MFA).</span></span>
* <span data-ttu-id="319cf-124">Acesse o SSMS em qualquer lugar ao usar qualquer um dos clientes com suporte do Azure RemoteApp, entre eles iOS, Android, Mac, Windows Phone e PCs com Windows.</span><span class="sxs-lookup"><span data-stu-id="319cf-124">Access SSMS anywhere when using any of the supported Azure RemoteApp clients which includes iOS, Android, Mac, Windows Phone, and Windows PC’s.</span></span>

## <a name="create-the-azure-remoteapp-collection"></a><span data-ttu-id="319cf-125">Criar a coleção do Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="319cf-125">Create the Azure RemoteApp collection</span></span>
<span data-ttu-id="319cf-126">Veja a seguir as etapas para criar sua coleção do Azure RemoteApp com o SSMS:</span><span class="sxs-lookup"><span data-stu-id="319cf-126">Here are the steps to create your Azure RemoteApp collection with SSMS:</span></span>

### <a name="1-create-a-new-windows-vm-from-image"></a><span data-ttu-id="319cf-127">1. Criar uma nova VM do Windows a partir da Imagem</span><span class="sxs-lookup"><span data-stu-id="319cf-127">1. Create a new Windows VM from Image</span></span>
<span data-ttu-id="319cf-128">Use a imagem "Windows Server Remote Desktop Session Host Windows Server 2012 R2" da Galeria para criar sua nova VM.</span><span class="sxs-lookup"><span data-stu-id="319cf-128">Use the "Windows Server Remote Desktop Session Host Windows Server 2012 R2" Image from the Gallery to make your new VM.</span></span>

### <a name="2-install-ssms-from-sql-express"></a><span data-ttu-id="319cf-129">2. Instalar o SSMS do SQL Express</span><span class="sxs-lookup"><span data-stu-id="319cf-129">2. Install SSMS from SQL Express</span></span>
<span data-ttu-id="319cf-130">Acesse a nova VM e navegue até essa página de download: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span><span class="sxs-lookup"><span data-stu-id="319cf-130">Go onto the new VM and navigate to this download page: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span></span>

<span data-ttu-id="319cf-131">Há uma opção para baixar somente o SSMS.</span><span class="sxs-lookup"><span data-stu-id="319cf-131">There is an option to only download SSMS.</span></span> <span data-ttu-id="319cf-132">Após o download, vá até o diretório de instalação e execute a Instalação para instalar o SSMS.</span><span class="sxs-lookup"><span data-stu-id="319cf-132">After download, go into the install directory and run Setup to install SSMS.</span></span>

<span data-ttu-id="319cf-133">Também é necessário instalar o SQL Server 2014 Service Pack 1.</span><span class="sxs-lookup"><span data-stu-id="319cf-133">You also need to install SQL Server 2014 Service Pack 1.</span></span> <span data-ttu-id="319cf-134">Você pode baixá-lo aqui: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span><span class="sxs-lookup"><span data-stu-id="319cf-134">You can download it here: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span></span>

<span data-ttu-id="319cf-135">O SQL Server 2014 Service Pack 1 inclui uma funcionalidade essencial para trabalhar com o Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="319cf-135">SQL Server 2014 Service Pack 1 includes essential functionality for working with Azure SQL Database.</span></span>

### <a name="3-run-validate-script-and-sysprep"></a><span data-ttu-id="319cf-136">3. Executar o script Validate e o Sysprep</span><span class="sxs-lookup"><span data-stu-id="319cf-136">3. Run Validate script and Sysprep</span></span>
<span data-ttu-id="319cf-137">Na área de trabalho da VM há um script do PowerShell chamado Validate.</span><span class="sxs-lookup"><span data-stu-id="319cf-137">On the desktop of the VM is a PowerShell script called Validate.</span></span> <span data-ttu-id="319cf-138">Execute-o clicando duas vezes nele.</span><span class="sxs-lookup"><span data-stu-id="319cf-138">Run this by double-clicking.</span></span> <span data-ttu-id="319cf-139">Ele verificará se a VM está pronta para ser usada para hospedagem remota de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="319cf-139">It will verify that the VM is ready to be used for remote hosting of applications.</span></span> <span data-ttu-id="319cf-140">Quando a verificação estiver concluída, você receberá uma solicitação para executar o sysprep. Escolha executá-lo.</span><span class="sxs-lookup"><span data-stu-id="319cf-140">When verification is complete, it will ask to run sysprep - choose to run it.</span></span>

<span data-ttu-id="319cf-141">Após a conclusão do sysprep, ele desligará a VM.</span><span class="sxs-lookup"><span data-stu-id="319cf-141">When sysprep completes, it will shut down the VM.</span></span>

<span data-ttu-id="319cf-142">Para saber mais sobre como criar uma imagem do Azure RemoteApp, confira: [Como criar uma imagem de modelo do RemoteApp no Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="319cf-142">To learn more about creating a Azure RemoteApp image, see: [How to create a RemoteApp template image in Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span></span>

### <a name="4-capture-image"></a><span data-ttu-id="319cf-143">4. Capturar a imagem</span><span class="sxs-lookup"><span data-stu-id="319cf-143">4. Capture image</span></span>
<span data-ttu-id="319cf-144">Após a interrupção da execução da VM, encontre-a no portal atual e capture-a.</span><span class="sxs-lookup"><span data-stu-id="319cf-144">When the VM has stopped running, find it in the current portal and capture it.</span></span>

<span data-ttu-id="319cf-145">Para saber mais sobre como capturar uma imagem, consulte [Capturar uma imagem de uma máquina virtual Windows do Azure criada com o modelo de implantação clássico](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="319cf-145">To learn more about capturing an image, see [Capture an image of an Azure Windows virtual machine created with the classic deployment model](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

### <a name="5-add-to-azure-remoteapp-template-images"></a><span data-ttu-id="319cf-146">5. Adicionar a imagens de modelo do Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="319cf-146">5. Add to Azure RemoteApp Template images</span></span>
<span data-ttu-id="319cf-147">Na seção Azure RemoteApp do portal atual, acesse a guia Imagens de Modelo e clique em Adicionar.</span><span class="sxs-lookup"><span data-stu-id="319cf-147">In the Azure RemoteApp section of the current portal, go to the Template Images tab and click Add.</span></span> <span data-ttu-id="319cf-148">Na caixa pop-up, selecione "Importar uma imagem da biblioteca Máquinas Virtuais" e, em seguida, escolha a imagem que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="319cf-148">In the pop-up box, select "Import an image from your Virtual Machines library" and then choose the Image that you just created.</span></span>

### <a name="6-create-cloud-collection"></a><span data-ttu-id="319cf-149">6. Criar uma coleção na nuvem</span><span class="sxs-lookup"><span data-stu-id="319cf-149">6. Create cloud collection</span></span>
<span data-ttu-id="319cf-150">No portal atual, crie uma nova Coleção na Nuvem do Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="319cf-150">In the current portal, create a new Azure RemoteApp Cloud Collection.</span></span> <span data-ttu-id="319cf-151">Escolha a Imagem de Modelo que você acabou de importar com o SSMS instalado.</span><span class="sxs-lookup"><span data-stu-id="319cf-151">Choose the Template Image that you just imported with SSMS installed on it.</span></span>

![Criar uma nova coleção na nuvem][2]

### <a name="7-publish-ssms"></a><span data-ttu-id="319cf-153">7. Publicar o SSMS</span><span class="sxs-lookup"><span data-stu-id="319cf-153">7. Publish SSMS</span></span>
<span data-ttu-id="319cf-154">Na guia Publicação de sua nova coleção na nuvem, selecione Publicar um aplicativo no Menu Iniciar e, em seguida, escolha o SSMS na lista.</span><span class="sxs-lookup"><span data-stu-id="319cf-154">On the Publishing tab of your new cloud collection, select Publish an application from the Start Menu and then choose SSMS from the list.</span></span>

![Publicar aplicativo][5]

### <a name="8-add-users"></a><span data-ttu-id="319cf-156">8. Adicionar usuários</span><span class="sxs-lookup"><span data-stu-id="319cf-156">8. Add users</span></span>
<span data-ttu-id="319cf-157">Na guia Acesso de Usuário, você pode selecionar os usuários que terão acesso a esta coleção do Azure RemoteApp que inclui somente o SSMS.</span><span class="sxs-lookup"><span data-stu-id="319cf-157">On the User Access tab you can select the users that will have access to this Azure RemoteApp collection which only includes SSMS.</span></span>

![Adicionar usuário][6]

### <a name="9-install-the-azure-remoteapp-client-application"></a><span data-ttu-id="319cf-159">9. Instalar o aplicativo cliente do Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="319cf-159">9. Install the Azure RemoteApp client application</span></span>
<span data-ttu-id="319cf-160">Você pode baixar e instalar um cliente do Azure RemoteApp aqui: [Baixar | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span><span class="sxs-lookup"><span data-stu-id="319cf-160">You can download and install a Azure RemoteApp client here: [Download | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span></span>

## <a name="configure-azure-sql-server"></a><span data-ttu-id="319cf-161">Configurar o Azure SQL Server</span><span class="sxs-lookup"><span data-stu-id="319cf-161">Configure Azure SQL server</span></span>
<span data-ttu-id="319cf-162">A única configuração necessária é garantir que os Serviços do Azure estejam habilitados para o firewall.</span><span class="sxs-lookup"><span data-stu-id="319cf-162">The only configuration needed is to ensure that Azure Services is enabled for the firewall.</span></span> <span data-ttu-id="319cf-163">Se você usar essa solução, não será necessário adicionar endereços IP para abrir o firewall.</span><span class="sxs-lookup"><span data-stu-id="319cf-163">If you use this solution, then you do not need to add any IP addresses to open the firewall.</span></span> <span data-ttu-id="319cf-164">O tráfego de rede permitido para o SQL Server é de outros serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="319cf-164">The network traffic that is allowed to the SQL Server is from other Azure services.</span></span>

![Permissão do Azure][4]

## <a name="multi-factor-authentication-mfa"></a><span data-ttu-id="319cf-166">Multi-Factor Authentication (MFA)</span><span class="sxs-lookup"><span data-stu-id="319cf-166">Multi-Factor Authentication (MFA)</span></span>
<span data-ttu-id="319cf-167">A MFA pode ser habilitada especificamente para esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="319cf-167">MFA can be enabled for this application specifically.</span></span> <span data-ttu-id="319cf-168">Acesse a guia Aplicativos do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="319cf-168">Go to the Applications tab of your Azure Active Directory.</span></span> <span data-ttu-id="319cf-169">Você encontrará uma entrada para o Microsoft Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="319cf-169">You will find an entry for Microsoft Azure RemoteApp.</span></span> <span data-ttu-id="319cf-170">Se você clicar nesse aplicativo e configurá-lo, verá a página abaixo de onde você pode habilitar a MFA para este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="319cf-170">If you click that application and then configure, you will see the page below where you can enable MFA for this application.</span></span>

![Habilitar MFA][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a><span data-ttu-id="319cf-172">Auditar a atividade do usuário com o Active Directory Premium do Azure</span><span class="sxs-lookup"><span data-stu-id="319cf-172">Audit user activity with Azure Active Directory Premium</span></span>
<span data-ttu-id="319cf-173">Se você não tiver o Azure AD Premium, será necessário ativá-lo na seção Licenças do diretório.</span><span class="sxs-lookup"><span data-stu-id="319cf-173">If you do not have Azure AD Premium, then you have to turn it on in the Licenses section of your directory.</span></span> <span data-ttu-id="319cf-174">Com o Premium ativado, você poderá atribuir usuários para o nível Premium.</span><span class="sxs-lookup"><span data-stu-id="319cf-174">With Premium enabled, you can assign users to the Premium level.</span></span>

<span data-ttu-id="319cf-175">Quando você acessa um usuário no Active Directory do Azure, é possível acessar a guia Atividade para ver informações de logon para o Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="319cf-175">When you go to a user in your Azure Active Directory, you can then go to the Activity tab to see login information to Azure RemoteApp.</span></span>

## <a name="next-steps"></a><span data-ttu-id="319cf-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="319cf-176">Next steps</span></span>
<span data-ttu-id="319cf-177">Depois de concluir todas as etapas acima, você será capaz de executar o cliente do Azure RemoteApp e fazer logon com um usuário atribuído.</span><span class="sxs-lookup"><span data-stu-id="319cf-177">After completing all the above steps, you will be able to run the Azure RemoteApp client and log-in with an assigned user.</span></span> <span data-ttu-id="319cf-178">Você receberá o SSMS como um de seus aplicativos e poderá executá-lo da mesma forma que se estivesse instalado em seu computador com acesso ao Azure SQL Server.</span><span class="sxs-lookup"><span data-stu-id="319cf-178">You will be presented with SSMS as one of your applications, and you can run it as you would if it were installed on your computer with access to Azure SQL server.</span></span>

<span data-ttu-id="319cf-179">Para saber mais sobre como fazer a conexão com o Banco de Dados SQL, confira [Conectar-se ao Banco de Dados SQL com o SQL Server Management Studio e executar uma consulta T-SQL de exemplo](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="319cf-179">For more information on how to make the connection to SQL Database, see [Connect to SQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>

<span data-ttu-id="319cf-180">Isso é tudo por enquanto.</span><span class="sxs-lookup"><span data-stu-id="319cf-180">That's everything for now.</span></span> <span data-ttu-id="319cf-181">Aproveite!</span><span class="sxs-lookup"><span data-stu-id="319cf-181">Enjoy!</span></span>

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png