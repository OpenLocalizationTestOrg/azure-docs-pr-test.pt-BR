---
title: "Instalando trabalhos de banco de dados elástico | Microsoft Docs"
description: "Percorra a instalação do recurso de trabalho elástico."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: cbe0aa2b-17e3-4b6f-a16f-6ebc1f5a66af
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: e7a2d6dbcefbb31d76257eaf96ccc235d7a29416
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="installing-elastic-database-jobs-overview"></a><span data-ttu-id="95b98-103">Visão geral de Instalando trabalhos de Banco de Dados Elástico</span><span class="sxs-lookup"><span data-stu-id="95b98-103">Installing Elastic Database jobs overview</span></span>
<span data-ttu-id="95b98-104">Os [**trabalhos de Banco de Dados Elástico**](sql-database-elastic-jobs-overview.md) podem ser instalados por meio do PowerShell ou pelo portal clássico do Azure. Será possível obter acesso para criar e gerenciar trabalhos usando a API do PowerShell apenas se você instalar o pacote do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="95b98-104">[**Elastic Database jobs**](sql-database-elastic-jobs-overview.md) can be installed via PowerShell or through the Azure Classic Portal.You can gain access to create and manage jobs using the PowerShell API only if you install the PowerShell package.</span></span> <span data-ttu-id="95b98-105">Além disso, as APIs do PowerShell fornecem muito mais funcionalidade do que o portal neste momento.</span><span class="sxs-lookup"><span data-stu-id="95b98-105">Additionally, the PowerShell APIs provide significantly more functionality than the portal at this point in time.</span></span>

<span data-ttu-id="95b98-106">Se você já tiver instalado os **trabalhos de Banco de Dados Elástico** por meio do Portal usando um **pool elástico** existente, a versão prévia mais recente do Powershell incluirá scripts para atualizar sua instalação existente.</span><span class="sxs-lookup"><span data-stu-id="95b98-106">If you have already installed **Elastic Database jobs** through the Portal from an existing **elastic pool**, the latest Powershell preview includes scripts to upgrade your existing installation.</span></span> <span data-ttu-id="95b98-107">É altamente recomendável atualizar sua instalação para a versão mais recente dos componentes dos **trabalhos de Banco de Dados Elástico** para aproveitar a nova funcionalidade exposta por meio das APIs do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="95b98-107">It is highly recommended to upgrade your installation to the latest **Elastic Database jobs** components in order to take advantage of new functionality exposed via the PowerShell APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95b98-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="95b98-108">Prerequisites</span></span>
* <span data-ttu-id="95b98-109">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="95b98-109">An Azure subscription.</span></span> <span data-ttu-id="95b98-110">Para obter uma avaliação gratuita, veja [Avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="95b98-110">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="95b98-111">PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="95b98-111">Azure PowerShell.</span></span> <span data-ttu-id="95b98-112">Instale a versão mais recente usando o [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376).</span><span class="sxs-lookup"><span data-stu-id="95b98-112">Install the latest version using the [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376).</span></span> <span data-ttu-id="95b98-113">Para obter informações detalhadas, confira [Como instalar e configurar o PowerShell do Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="95b98-113">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="95b98-114">[Utilitário de Linha de Comando do NuGet](https://nuget.org/nuget.exe) é usado para instalar o pacote de trabalhos de Banco de Dados Elástico.</span><span class="sxs-lookup"><span data-stu-id="95b98-114">[NuGet Command-line Utility](https://nuget.org/nuget.exe) is used to install the Elastic Database jobs package.</span></span> <span data-ttu-id="95b98-115">Para obter mais informações, consulte http://docs.nuget.org/docs/start-here/installing-nuget.</span><span class="sxs-lookup"><span data-stu-id="95b98-115">For more information, see http://docs.nuget.org/docs/start-here/installing-nuget.</span></span>

## <a name="download-and-import-the-elastic-database-jobs-powershell-package"></a><span data-ttu-id="95b98-116">Baixar e importar o pacote do PowerShell de trabalhos de Banco de Dados Elástico</span><span class="sxs-lookup"><span data-stu-id="95b98-116">Download and import the Elastic Database jobs PowerShell package</span></span>
1. <span data-ttu-id="95b98-117">Inicie a janela de comando do Microsoft Azure PowerShell e navegue até o diretório onde você baixou o utilitário de linha de comando do NuGet (nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="95b98-117">Launch Microsoft Azure PowerShell command window and navigate to the directory where you downloaded NuGet Command-line Utility (nuget.exe).</span></span>
2. <span data-ttu-id="95b98-118">Baixar e importar o pacote **trabalhos de Banco de Dados Elástico** para o diretório atual com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="95b98-118">Download and import **Elastic Database jobs** package into the current directory with the following command:</span></span>
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    <span data-ttu-id="95b98-119">Os arquivos de **trabalhos de Banco de Dados Elástico** são colocados no diretório local em uma pasta chamada **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x**, em que *x.x.xxxx.x* reflete o número de versão.</span><span class="sxs-lookup"><span data-stu-id="95b98-119">The **Elastic Database jobs** files are placed in the local directory in a folder named **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** where *x.x.xxxx.x* reflects the version number.</span></span> <span data-ttu-id="95b98-120">Os cmdlets do PowerShell (incluindo .dlls de cliente necessárias) estão localizados no subdiretório **tools\ElasticDatabaseJobs** e os scripts do PowerShell a serem instalados, atualizados e desinstalados também residem no subdiretório **tools**.</span><span class="sxs-lookup"><span data-stu-id="95b98-120">The PowerShell cmdlets (including required client .dlls) are located in the **tools\ElasticDatabaseJobs** sub-directory and the PowerShell scripts to install, upgrade and uninstall also reside in the **tools** sub-directory.</span></span>
3. <span data-ttu-id="95b98-121">Navegue até o subdiretório Ferramentas, na pasta Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x, digitando cd ferramentas, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="95b98-121">Navigate to the tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder by typing cd tools, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. <span data-ttu-id="95b98-122">Execute o script .\InstallElasticDatabaseJobsCmdlets.ps1 para copiar o diretório ElasticDatabaseJobs para $home\Documents\WindowsPowerShell\Modules.</span><span class="sxs-lookup"><span data-stu-id="95b98-122">Execute the .\InstallElasticDatabaseJobsCmdlets.ps1 script to copy the ElasticDatabaseJobs directory into $home\Documents\WindowsPowerShell\Modules.</span></span> <span data-ttu-id="95b98-123">Isso também importará automaticamente o módulo a ser usado, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="95b98-123">This will also automatically import the module for use, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-the-elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="95b98-124">Instalar componentes de trabalhos de Banco de Dados Elástico usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="95b98-124">Install the Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="95b98-125">Inicie uma janela de comando do Microsoft Azure PowerShell e navegue até o subdiretório \ferramentas, na pasta Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x: digite cd \ferramentas</span><span class="sxs-lookup"><span data-stu-id="95b98-125">Launch a Microsoft Azure PowerShell command window and navigate to the \tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder: Type cd \tools</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. <span data-ttu-id="95b98-126">Execute o script do PowerShell .\InstallElasticDatabaseJobs.ps1 e forneça valores para as variáveis solicitadas.</span><span class="sxs-lookup"><span data-stu-id="95b98-126">Execute the .\InstallElasticDatabaseJobs.ps1 PowerShell script and supply values for its requested variables.</span></span> <span data-ttu-id="95b98-127">Esse script cria os componentes descritos em [Preços e componentes de trabalhos de Banco de Dados Elástico](sql-database-elastic-jobs-overview.md#components-and-pricing) , juntamente com a configuração do Serviço de Nuvem do Azure para usar os componentes dependentes.</span><span class="sxs-lookup"><span data-stu-id="95b98-127">This script will create the components described in [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing) along with configuring the Azure Cloud Service to appropriately use the dependent components.</span></span>

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

<span data-ttu-id="95b98-128">Ao executar este comando, uma janela é aberta solicitando um **nome de usuário** e **senha**.</span><span class="sxs-lookup"><span data-stu-id="95b98-128">When you run this command a window opens asking for a **user name** and **password**.</span></span> <span data-ttu-id="95b98-129">Essas não são suas credenciais do Azure, insira o nome de usuário e a senha que serão as credenciais de administrador que você deseja criar para o novo servidor.</span><span class="sxs-lookup"><span data-stu-id="95b98-129">This is not your Azure credentials, enter the user name and password that will be the administrator credentials you want to create for the new server.</span></span>

<span data-ttu-id="95b98-130">Os parâmetros fornecidos nesta chamada de exemplo podem ser modificados para as configurações desejadas.</span><span class="sxs-lookup"><span data-stu-id="95b98-130">The parameters provided on this sample invocation can be modified for your desired settings.</span></span> <span data-ttu-id="95b98-131">O exemplo a seguir fornece mais informações sobre o comportamento de cada parâmetro:</span><span class="sxs-lookup"><span data-stu-id="95b98-131">The following provides more information on the behavior of each parameter:</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="95b98-132">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="95b98-132">Parameter</span></span></th>
    <th><span data-ttu-id="95b98-133">Descrição</span><span class="sxs-lookup"><span data-stu-id="95b98-133">Description</span></span></th>
  </tr>

<tr>
    <td><span data-ttu-id="95b98-134">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="95b98-134">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="95b98-135">Fornece o nome do grupo de recursos do Azure criado para conter os componentes recém-criados do Azure.</span><span class="sxs-lookup"><span data-stu-id="95b98-135">Provides the Azure resource group name created to contain the newly created Azure components.</span></span> <span data-ttu-id="95b98-136">Esse parâmetro usa "__ElasticDatabaseJob" como padrão.</span><span class="sxs-lookup"><span data-stu-id="95b98-136">This parameter defaults to “__ElasticDatabaseJob”.</span></span> <span data-ttu-id="95b98-137">Não é recomendável alterar esse valor.</span><span class="sxs-lookup"><span data-stu-id="95b98-137">It is not recommended to change this value.</span></span></td>
    </tr>

</tr>

    <tr>
    <td><span data-ttu-id="95b98-138">ResourceGroupLocation</span><span class="sxs-lookup"><span data-stu-id="95b98-138">ResourceGroupLocation</span></span></td>
    <td><span data-ttu-id="95b98-139">Fornece o local do Azure a ser usado para os componentes recém-criados do Azure.</span><span class="sxs-lookup"><span data-stu-id="95b98-139">Provides the Azure location to be used for the newly created Azure components.</span></span> <span data-ttu-id="95b98-140">O padrão desse parâmetro é o local Central dos Estados Unidos.</span><span class="sxs-lookup"><span data-stu-id="95b98-140">This parameter defaults to the Central US location.</span></span></td>
</tr>

<tr>
    <td><span data-ttu-id="95b98-141">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="95b98-141">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="95b98-142">Fornece o número de trabalhadores de serviço para instalar.</span><span class="sxs-lookup"><span data-stu-id="95b98-142">Provides the number of service workers to install.</span></span> <span data-ttu-id="95b98-143">O padrão desse parâmetro é 1.</span><span class="sxs-lookup"><span data-stu-id="95b98-143">This parameter defaults to 1.</span></span> <span data-ttu-id="95b98-144">Um número maior de trabalhadores pode ser usado para escalar horizontalmente o serviço e fornecer alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="95b98-144">A higher number of workers can be used to scale out the service and to provide high availability.</span></span> <span data-ttu-id="95b98-145">É recomendável usar "2" para implantações que exigem alta disponibilidade do serviço.</span><span class="sxs-lookup"><span data-stu-id="95b98-145">It is recommended to use “2” for deployments that require high availability of the service.</span></span></td>
    </tr>

</tr>
    <tr>
    <td><span data-ttu-id="95b98-146">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="95b98-146">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="95b98-147">Fornece o tamanho da VM para uso no Serviço de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="95b98-147">Provides the VM size for usage within the Cloud Service.</span></span> <span data-ttu-id="95b98-148">O padrão desse parâmetro é A0.</span><span class="sxs-lookup"><span data-stu-id="95b98-148">This parameter defaults to A0.</span></span> <span data-ttu-id="95b98-149">Os valores de parâmetros de A0/A1/A2/A3 são aceitos, o que faz com que a função de trabalho use um tamanho Extra pequeno/Pequeno/Médio/Grande, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="95b98-149">Parameters values of A0/A1/A2/A3 are accepted which cause the worker role to use an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="95b98-150">Para obter mais informações sobre tamanhos de função de trabalho, consulte [Elastic Database jobs components and pricing (Preço e componentes de trabalhos do Banco de Dados Elástico)](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="95b98-150">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="95b98-151">SqlServerDatabaseSlo</span><span class="sxs-lookup"><span data-stu-id="95b98-151">SqlServerDatabaseSlo</span></span></td>
    <td><span data-ttu-id="95b98-152">Fornece o objetivo de nível de serviço para uma edição Standard.</span><span class="sxs-lookup"><span data-stu-id="95b98-152">Provides the service level objective for a Standard edition.</span></span> <span data-ttu-id="95b98-153">O padrão desse parâmetro é S0.</span><span class="sxs-lookup"><span data-stu-id="95b98-153">This parameter defaults to S0.</span></span> <span data-ttu-id="95b98-154">Valores de parâmetro de S0/S1/S2/S3 são aceitos, o que faz com que o Banco de Dados SQL do Azure use o respectivo SLO.</span><span class="sxs-lookup"><span data-stu-id="95b98-154">Parameter values of S0/S1/S2/S3 are accepted which cause the Azure SQL Database to use the respective SLO.</span></span> <span data-ttu-id="95b98-155">Para obter mais informações sobre SLOs do Banco de Dados SQL, consulte [Elastic Database jobs components and pricing (Preço e componentes de trabalhos do Banco de Dados Elástico)](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="95b98-155">For more information on SQL Database SLOs, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="95b98-156">SqlServerAdministratorUserName</span><span class="sxs-lookup"><span data-stu-id="95b98-156">SqlServerAdministratorUserName</span></span></td>
    <td><span data-ttu-id="95b98-157">Fornece o nome de usuário do administrador para o servidor de Banco de Dados SQL recém-criado.</span><span class="sxs-lookup"><span data-stu-id="95b98-157">Provides the admin user name for the newly created Azure SQL Database server.</span></span> <span data-ttu-id="95b98-158">Quando as credenciais não forem especificadas, será exibida uma janela de credenciais do PowerShell solicitando-as.</span><span class="sxs-lookup"><span data-stu-id="95b98-158">When not specified, a PowerShell credentials window will open to prompt for the credentials.</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="95b98-159">SqlServerAdministratorPassword</span><span class="sxs-lookup"><span data-stu-id="95b98-159">SqlServerAdministratorPassword</span></span></td>
    <td><span data-ttu-id="95b98-160">Fornece a senha do administrador para o servidor de Banco de Dados SQL recém-criado.</span><span class="sxs-lookup"><span data-stu-id="95b98-160">Provides the admin password for the newly created Azure SQL Database server.</span></span> <span data-ttu-id="95b98-161">Quando as credenciais não forem fornecidas, será exibida uma janela de credenciais do PowerShell solicitando-as.</span><span class="sxs-lookup"><span data-stu-id="95b98-161">When not provided, a PowerShell credentials window will open to prompt for the credentials.</span></span></td>
</tr>
</table>

<span data-ttu-id="95b98-162">Para sistemas com grandes números de trabalhos sendo executados em paralelo em um grande número de bancos de dados de destino, é recomendável especificar parâmetros como: -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2.</span><span class="sxs-lookup"><span data-stu-id="95b98-162">For systems that target having large numbers of jobs running in parallel against a large number of databases, it is recommended to specify parameters such as: -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a><span data-ttu-id="95b98-163">Atualizar uma instalação existente de componentes do trabalhos de Banco de Dados Elástico usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="95b98-163">Update an existing Elastic Database jobs components installation using PowerShell</span></span>
<span data-ttu-id="95b98-164">**trabalhos de Banco de Dados Elástico** podem ser atualizados em uma instalação existente em relação à escala e à alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="95b98-164">**Elastic Database jobs** can be updated within an existing installation for scale and high-availability.</span></span> <span data-ttu-id="95b98-165">Esse processo permite atualizações futuras do código de serviço sem precisar remover e recriar o banco de dados de controle.</span><span class="sxs-lookup"><span data-stu-id="95b98-165">This process allows for future upgrades of service code without having to drop and recreate the control database.</span></span> <span data-ttu-id="95b98-166">Esse processo também pode ser usado dentro da mesma versão para modificar o tamanho da VM de serviço ou a contagem de trabalho do servidor.</span><span class="sxs-lookup"><span data-stu-id="95b98-166">This process can also be used within the same version to modify the service VM size or the server worker count.</span></span>

<span data-ttu-id="95b98-167">Para atualizar o tamanho da VM de uma instalação, execute o script a seguir com parâmetros atualizados para os valores de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="95b98-167">To update the VM size of an installation, run the following script with parameters updated to the values of your choice.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th><span data-ttu-id="95b98-168">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="95b98-168">Parameter</span></span></th>
  <th><span data-ttu-id="95b98-169">Descrição</span><span class="sxs-lookup"><span data-stu-id="95b98-169">Description</span></span></th>
</tr>

  <tr>
    <td><span data-ttu-id="95b98-170">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="95b98-170">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="95b98-171">Identifica o nome do grupo de recursos do Azure usado quando os componentes de trabalho de Banco de Dados Elástico foram inicialmente instalados.</span><span class="sxs-lookup"><span data-stu-id="95b98-171">Identifies the Azure resource group name used when the Elastic Database job components were initially installed.</span></span> <span data-ttu-id="95b98-172">Esse parâmetro usa "__ElasticDatabaseJob" como padrão.</span><span class="sxs-lookup"><span data-stu-id="95b98-172">This parameter defaults to “__ElasticDatabaseJob”.</span></span> <span data-ttu-id="95b98-173">Uma vez que não é recomendável alterar esse valor, você não deve ter que especificar este parâmetro.</span><span class="sxs-lookup"><span data-stu-id="95b98-173">Since it is not recommended to change this value, you shouldn't have to specify this parameter.</span></span></td>
    </tr>
</tr>

</tr>

  <tr>
    <td><span data-ttu-id="95b98-174">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="95b98-174">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="95b98-175">Fornece o número de trabalhadores de serviço para instalar.</span><span class="sxs-lookup"><span data-stu-id="95b98-175">Provides the number of service workers to install.</span></span>  <span data-ttu-id="95b98-176">O padrão desse parâmetro é 1.</span><span class="sxs-lookup"><span data-stu-id="95b98-176">This parameter defaults to 1.</span></span>  <span data-ttu-id="95b98-177">Um número maior de trabalhadores pode ser usado para escalar horizontalmente o serviço e fornecer alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="95b98-177">A higher number of workers can be used to scale out the service and to provide high availability.</span></span>  <span data-ttu-id="95b98-178">É recomendável usar "2" para implantações que exigem alta disponibilidade do serviço.</span><span class="sxs-lookup"><span data-stu-id="95b98-178">It is recommended to use “2” for deployments that require high availability of the service.</span></span></td>
</tr>

</tr>

    <tr>
    <td><span data-ttu-id="95b98-179">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="95b98-179">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="95b98-180">Fornece o tamanho da VM para uso no Serviço de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="95b98-180">Provides the VM size for usage within the Cloud Service.</span></span> <span data-ttu-id="95b98-181">O padrão desse parâmetro é A0.</span><span class="sxs-lookup"><span data-stu-id="95b98-181">This parameter defaults to A0.</span></span> <span data-ttu-id="95b98-182">Os valores de parâmetros de A0/A1/A2/A3 são aceitos, o que faz com que a função de trabalho use um tamanho Extra pequeno/Pequeno/Médio/Grande, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="95b98-182">Parameters values of A0/A1/A2/A3 are accepted which cause the worker role to use an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="95b98-183">Para obter mais informações sobre tamanhos de função de trabalho, consulte [Elastic Database jobs components and pricing (Preço e componentes de trabalhos do Banco de Dados Elástico)](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="95b98-183">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</table>

## <a name="install-the-elastic-database-jobs-components-using-the-portal"></a><span data-ttu-id="95b98-184">Instalar os componentes de trabalhos de Banco de Dados Elástico usando o Portal</span><span class="sxs-lookup"><span data-stu-id="95b98-184">Install the Elastic Database jobs components using the Portal</span></span>
<span data-ttu-id="95b98-185">Após a [criação de um pool elástico](sql-database-elastic-pool-manage-portal.md), você pode instalar componentes dos **trabalhos de Banco de Dados Elástico** para habilitar a execução de tarefas administrativas em cada banco de dados no pool elástico.</span><span class="sxs-lookup"><span data-stu-id="95b98-185">Once you have [created an elastic pool](sql-database-elastic-pool-manage-portal.md), you can install **Elastic Database jobs** components to enable execution of administrative tasks against each database in the elastic pool.</span></span> <span data-ttu-id="95b98-186">Ao contrário do que ocorre quando as APIs do PowerShell de **trabalhos de Banco de Dados Elástico** são usadas, a interface do portal está atualmente restrita à execução exclusivamente em um pool existente.</span><span class="sxs-lookup"><span data-stu-id="95b98-186">Unlike when using the **Elastic Database jobs** PowerShell APIs, the portal interface is currently restricted to only executing against an existing pool.</span></span>

<span data-ttu-id="95b98-187">**Tempo estimado para conclusão:** 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="95b98-187">**Estimated time to complete:** 10 minutes.</span></span>

1. <span data-ttu-id="95b98-188">Na exibição de painel do pool elástico, por meio do [Portal do Azure](https://portal.azure.com/#), clique em **Criar trabalho**.</span><span class="sxs-lookup"><span data-stu-id="95b98-188">From the dashboard view of the elastic pool via the [Azure Portal](https://portal.azure.com/#) , click **Create job**.</span></span>
2. <span data-ttu-id="95b98-189">Se estiver criando um trabalho pela primeira vez, será necessário instalar os **trabalhos de Banco de Dados Elástico** clicando em **VISUALIZAR TERMOS**.</span><span class="sxs-lookup"><span data-stu-id="95b98-189">If you are creating a job for the first time, you must install **Elastic Database jobs** by clicking **PREVIEW TERMS**.</span></span>
3. <span data-ttu-id="95b98-190">Aceite os termos clicando na caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="95b98-190">Accept the terms by clicking the checkbox.</span></span>
4. <span data-ttu-id="95b98-191">No modo de exibição "Instalar serviços", clique em **CREDENCIAIS DO TRABALHO**.</span><span class="sxs-lookup"><span data-stu-id="95b98-191">In the "Install services" view, click **JOB CREDENTIALS**.</span></span>
   
    ![Instalando os serviços][1]
5. <span data-ttu-id="95b98-193">Digite um nome de usuário e uma senha para um administrador de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="95b98-193">Type a user name and password for a database admin.</span></span> <span data-ttu-id="95b98-194">Como parte da instalação, um novo servidor de Banco de Dados SQL é criado.</span><span class="sxs-lookup"><span data-stu-id="95b98-194">As part of the installation, a new Azure SQL Database server is created.</span></span> <span data-ttu-id="95b98-195">Dentro desse novo servidor, um novo banco de dados, conhecido como banco de dados de controle, é criado e usado para conter os metadados para trabalhos de Banco de Dados Elástico.</span><span class="sxs-lookup"><span data-stu-id="95b98-195">Within this new server, a new database, known as the control database, is created and used to contain the meta data for Elastic Database jobs.</span></span> <span data-ttu-id="95b98-196">O nome de usuário e senha criados aqui são usados para fins de logon no banco de dados do controle.</span><span class="sxs-lookup"><span data-stu-id="95b98-196">The user name and password created here are used for the purpose of logging in to the control database.</span></span> <span data-ttu-id="95b98-197">Uma credencial separada é usada para execução de scripts nos bancos de dados dentro do pool.</span><span class="sxs-lookup"><span data-stu-id="95b98-197">A separate credential is used for script execution against the databases within the pool.</span></span>
   
    ![Criar nome de usuário e senha][2]
6. <span data-ttu-id="95b98-199">Clique no botão OK.</span><span class="sxs-lookup"><span data-stu-id="95b98-199">Click the OK button.</span></span> <span data-ttu-id="95b98-200">Os componentes são criados para você em questão de minutos em um novo [Grupo de recursos](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="95b98-200">The components are created for you in a few minutes in a new [Resource group](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="95b98-201">O novo grupo de recursos é fixado à tela inicial, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="95b98-201">The new resource group is pinned to the start board, as shown below.</span></span> <span data-ttu-id="95b98-202">Depois de criados, os trabalhos de banco de dados elástico (Serviço de Nuvem, Banco de Dados SQL, Barramento de Serviço e Armazenamento) são criados no grupo.</span><span class="sxs-lookup"><span data-stu-id="95b98-202">Once created, elastic database jobs (Cloud Service, SQL Database, Service Bus, and Storage) are all created in the group.</span></span>
   
    ![grupo de recursos na tela inicial][3]
7. <span data-ttu-id="95b98-204">Se você tentar criar ou gerenciar um trabalho durante instalação dos trabalhos de banco de dados elástico, ao fornecer as **Credenciais** , verá a mensagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="95b98-204">If you attempt to create or manage a job while elastic database jobs is installing, when providing **Credentials** you will see the following message.</span></span>
   
    ![Implantação ainda em andamento][4]

<span data-ttu-id="95b98-206">Se a desinstalação for necessária, exclua o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="95b98-206">If uninstallation is required, delete the resource group.</span></span> <span data-ttu-id="95b98-207">Veja [Como desinstalar os componentes de trabalho de Banco de Dados Elástico](sql-database-elastic-jobs-uninstall.md).</span><span class="sxs-lookup"><span data-stu-id="95b98-207">See [How to uninstall the Elastic Database job components](sql-database-elastic-jobs-uninstall.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="95b98-208">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="95b98-208">Next steps</span></span>
<span data-ttu-id="95b98-209">Certifique-se de que uma credencial com os direitos apropriados para a execução do script é criada em cada banco de dados no grupo; para obter mais informações, veja [Protegendo seu Banco de Dados SQL](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="95b98-209">Ensure a credential with the appropriate rights for script execution is created on each database in the group, for more information see [Securing your SQL Database](sql-database-manage-logins.md).</span></span>
<span data-ttu-id="95b98-210">Veja [Criando e gerenciando trabalhos de Banco de Dados Elástico](sql-database-elastic-jobs-create-and-manage.md) para começar.</span><span class="sxs-lookup"><span data-stu-id="95b98-210">See [Creating and managing an Elastic Database jobs](sql-database-elastic-jobs-create-and-manage.md) to get started.</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: ./media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: ./media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: ./media/sql-database-elastic-jobs-service-installation/not-done.png
