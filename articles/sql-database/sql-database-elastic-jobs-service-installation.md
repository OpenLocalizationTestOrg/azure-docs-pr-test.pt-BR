---
title: "trabalhos do banco de dados Elástico aaaInstalling | Microsoft Docs"
description: "Passar pela instalação do recurso de trabalho Elástico hello."
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
ms.openlocfilehash: 0349f66a4428f81d00d43681d7f2177f273ec032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="installing-elastic-database-jobs-overview"></a><span data-ttu-id="ba292-103">Visão geral de Instalando trabalhos de Banco de Dados Elástico</span><span class="sxs-lookup"><span data-stu-id="ba292-103">Installing Elastic Database jobs overview</span></span>
<span data-ttu-id="ba292-104">[**Trabalhos do banco de dados Elásticos** ](sql-database-elastic-jobs-overview.md) pode ser instalado por meio do PowerShell ou por meio de saudação Portal.You clássico do Azure podem obter acesso toocreate e gerenciar trabalhos usando Olá API PowerShell somente se você instalar o pacote do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="ba292-104">[**Elastic Database jobs**](sql-database-elastic-jobs-overview.md) can be installed via PowerShell or through hello Azure Classic Portal.You can gain access toocreate and manage jobs using hello PowerShell API only if you install hello PowerShell package.</span></span> <span data-ttu-id="ba292-105">Além disso, Olá APIs do PowerShell fornecem funcionalidade significativamente mais que o portal de saudação neste momento.</span><span class="sxs-lookup"><span data-stu-id="ba292-105">Additionally, hello PowerShell APIs provide significantly more functionality than hello portal at this point in time.</span></span>

<span data-ttu-id="ba292-106">Se você já tiver instalado **trabalhos do banco de dados Elástico** por meio de saudação Portal de uma já existente **pool Elástico**, visualização mais recente do Powershell de saudação inclui scripts tooupgrade sua instalação existente.</span><span class="sxs-lookup"><span data-stu-id="ba292-106">If you have already installed **Elastic Database jobs** through hello Portal from an existing **elastic pool**, hello latest Powershell preview includes scripts tooupgrade your existing installation.</span></span> <span data-ttu-id="ba292-107">É altamente recomendável tooupgrade toohello sua instalação mais recente **trabalhos do banco de dados Elástico** Olá de componentes em vantagens de tootake de ordem da nova funcionalidade exposta por meio de APIs do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ba292-107">It is highly recommended tooupgrade your installation toohello latest **Elastic Database jobs** components in order tootake advantage of new functionality exposed via hello PowerShell APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba292-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ba292-108">Prerequisites</span></span>
* <span data-ttu-id="ba292-109">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba292-109">An Azure subscription.</span></span> <span data-ttu-id="ba292-110">Para obter uma avaliação gratuita, veja [Avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ba292-110">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ba292-111">PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba292-111">Azure PowerShell.</span></span> <span data-ttu-id="ba292-112">Instalar a versão mais recente de hello usando Olá [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376).</span><span class="sxs-lookup"><span data-stu-id="ba292-112">Install hello latest version using hello [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376).</span></span> <span data-ttu-id="ba292-113">Para obter informações detalhadas, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ba292-113">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="ba292-114">[O utilitário de linha de comando do NuGet](https://nuget.org/nuget.exe) é usado tooinstall Olá banco de dados Elástico trabalhos pacote.</span><span class="sxs-lookup"><span data-stu-id="ba292-114">[NuGet Command-line Utility](https://nuget.org/nuget.exe) is used tooinstall hello Elastic Database jobs package.</span></span> <span data-ttu-id="ba292-115">Para obter mais informações, consulte http://docs.nuget.org/docs/start-here/installing-nuget.</span><span class="sxs-lookup"><span data-stu-id="ba292-115">For more information, see http://docs.nuget.org/docs/start-here/installing-nuget.</span></span>

## <a name="download-and-import-hello-elastic-database-jobs-powershell-package"></a><span data-ttu-id="ba292-116">Baixe e importe o pacote de PowerShell de trabalhos de banco de dados Elástico Olá</span><span class="sxs-lookup"><span data-stu-id="ba292-116">Download and import hello Elastic Database jobs PowerShell package</span></span>
1. <span data-ttu-id="ba292-117">Inicie a janela de comando do Microsoft Azure PowerShell e navegue toohello diretório onde você baixou o utilitário de linha de comando do NuGet (nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="ba292-117">Launch Microsoft Azure PowerShell command window and navigate toohello directory where you downloaded NuGet Command-line Utility (nuget.exe).</span></span>
2. <span data-ttu-id="ba292-118">Baixar e importar **trabalhos do banco de dados Elástico** pacote no diretório atual de saudação com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="ba292-118">Download and import **Elastic Database jobs** package into hello current directory with hello following command:</span></span>
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    <span data-ttu-id="ba292-119">Olá **trabalhos do banco de dados Elástico** os arquivos são colocados no diretório local de saudação em uma pasta chamada **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** onde *x.x.xxxx.x* reflete o número de versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="ba292-119">hello **Elastic Database jobs** files are placed in hello local directory in a folder named **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** where *x.x.xxxx.x* reflects hello version number.</span></span> <span data-ttu-id="ba292-120">cmdlets do PowerShell Hello (incluindo DLLs de cliente necessárias) estão localizados em Olá **tools\ElasticDatabaseJobs** subdiretório e hello tooinstall de scripts do PowerShell, atualizar e desinstalar também residem em Olá  **ferramentas** subdiretório.</span><span class="sxs-lookup"><span data-stu-id="ba292-120">hello PowerShell cmdlets (including required client .dlls) are located in hello **tools\ElasticDatabaseJobs** sub-directory and hello PowerShell scripts tooinstall, upgrade and uninstall also reside in hello **tools** sub-directory.</span></span>
3. <span data-ttu-id="ba292-121">Navegue toohello ferramentas subdiretório na pasta de Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x Olá digitando cd ferramentas, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ba292-121">Navigate toohello tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder by typing cd tools, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. <span data-ttu-id="ba292-122">Execute o diretório do hello.\InstallElasticDatabaseJobsCmdlets.ps1 scripts toocopy Olá ElasticDatabaseJobs em $home\documents\windowspowershell\modules..</span><span class="sxs-lookup"><span data-stu-id="ba292-122">Execute hello .\InstallElasticDatabaseJobsCmdlets.ps1 script toocopy hello ElasticDatabaseJobs directory into $home\Documents\WindowsPowerShell\Modules.</span></span> <span data-ttu-id="ba292-123">Isso também importará automaticamente módulo Olá para uso, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ba292-123">This will also automatically import hello module for use, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-hello-elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="ba292-124">Instalar componentes de trabalhos do banco de dados Elástico hello usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba292-124">Install hello Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="ba292-125">Inicie uma janela de comando do Microsoft Azure PowerShell e navegue toohello \tools subdiretório na pasta de Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x Olá: digite cd \tools</span><span class="sxs-lookup"><span data-stu-id="ba292-125">Launch a Microsoft Azure PowerShell command window and navigate toohello \tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder: Type cd \tools</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. <span data-ttu-id="ba292-126">Executar script do PowerShell.\InstallElasticDatabaseJobs.ps1 hello e forneça valores para as variáveis de solicitada.</span><span class="sxs-lookup"><span data-stu-id="ba292-126">Execute hello .\InstallElasticDatabaseJobs.ps1 PowerShell script and supply values for its requested variables.</span></span> <span data-ttu-id="ba292-127">Esse script cria componentes Olá descritos [banco de dados Elástico trabalhos componentes e preços](sql-database-elastic-jobs-overview.md#components-and-pricing) bem Configurando Olá serviço de nuvem do Azure tooappropriately usam os componentes dependentes hello.</span><span class="sxs-lookup"><span data-stu-id="ba292-127">This script will create hello components described in [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing) along with configuring hello Azure Cloud Service tooappropriately use hello dependent components.</span></span>

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

<span data-ttu-id="ba292-128">Ao executar este comando, uma janela é aberta solicitando um **nome de usuário** e **senha**.</span><span class="sxs-lookup"><span data-stu-id="ba292-128">When you run this command a window opens asking for a **user name** and **password**.</span></span> <span data-ttu-id="ba292-129">Isso não é suas credenciais do Azure, insira o nome de usuário de saudação e a senha que serão as credenciais de administrador de saudação desejar toocreate para novo servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="ba292-129">This is not your Azure credentials, enter hello user name and password that will be hello administrator credentials you want toocreate for hello new server.</span></span>

<span data-ttu-id="ba292-130">parâmetros de saudação fornecidos nessa invocação de exemplo podem ser modificados para as configurações desejadas.</span><span class="sxs-lookup"><span data-stu-id="ba292-130">hello parameters provided on this sample invocation can be modified for your desired settings.</span></span> <span data-ttu-id="ba292-131">seguir Olá fornece mais informações sobre o comportamento de saudação de cada parâmetro:</span><span class="sxs-lookup"><span data-stu-id="ba292-131">hello following provides more information on hello behavior of each parameter:</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="ba292-132">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="ba292-132">Parameter</span></span></th>
    <th><span data-ttu-id="ba292-133">Descrição</span><span class="sxs-lookup"><span data-stu-id="ba292-133">Description</span></span></th>
  </tr>

<tr>
    <td><span data-ttu-id="ba292-134">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="ba292-134">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="ba292-135">Fornece o nome do grupo de recursos do Azure Olá criado Olá toocontain recém-criada em componentes do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba292-135">Provides hello Azure resource group name created toocontain hello newly created Azure components.</span></span> <span data-ttu-id="ba292-136">Padrão desse parâmetro é muito "__ElasticDatabaseJob".</span><span class="sxs-lookup"><span data-stu-id="ba292-136">This parameter defaults too“__ElasticDatabaseJob”.</span></span> <span data-ttu-id="ba292-137">Não é recomendável toochange esse valor.</span><span class="sxs-lookup"><span data-stu-id="ba292-137">It is not recommended toochange this value.</span></span></td>
    </tr>

</tr>

    <tr>
    <td><span data-ttu-id="ba292-138">ResourceGroupLocation</span><span class="sxs-lookup"><span data-stu-id="ba292-138">ResourceGroupLocation</span></span></td>
    <td><span data-ttu-id="ba292-139">Fornece Olá local do Azure toobe usado para Olá recém-criada em componentes do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba292-139">Provides hello Azure location toobe used for hello newly created Azure components.</span></span> <span data-ttu-id="ba292-140">O padrão desse parâmetro é toohello local de centro dos EUA.</span><span class="sxs-lookup"><span data-stu-id="ba292-140">This parameter defaults toohello Central US location.</span></span></td>
</tr>

<tr>
    <td><span data-ttu-id="ba292-141">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="ba292-141">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="ba292-142">Fornece o número de saudação do tooinstall de trabalhadores de serviço.</span><span class="sxs-lookup"><span data-stu-id="ba292-142">Provides hello number of service workers tooinstall.</span></span> <span data-ttu-id="ba292-143">O padrão desse parâmetro é too1.</span><span class="sxs-lookup"><span data-stu-id="ba292-143">This parameter defaults too1.</span></span> <span data-ttu-id="ba292-144">Um número maior de trabalhadores pode ser usado tooscale out Olá tooprovide e serviço de alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="ba292-144">A higher number of workers can be used tooscale out hello service and tooprovide high availability.</span></span> <span data-ttu-id="ba292-145">É recomendável toouse "2" para implantações que exigem alta disponibilidade do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="ba292-145">It is recommended toouse “2” for deployments that require high availability of hello service.</span></span></td>
    </tr>

</tr>
    <tr>
    <td><span data-ttu-id="ba292-146">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="ba292-146">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="ba292-147">Fornece o tamanho da VM Olá para uso em Olá serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="ba292-147">Provides hello VM size for usage within hello Cloud Service.</span></span> <span data-ttu-id="ba292-148">O padrão desse parâmetro é tooA0.</span><span class="sxs-lookup"><span data-stu-id="ba292-148">This parameter defaults tooA0.</span></span> <span data-ttu-id="ba292-149">Valores de parâmetros de A0/A1/A2/A3 são aceitos que fazer com que o trabalho de saudação função toouse um tamanho muito pequeno/pequeno/médio/grande, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="ba292-149">Parameters values of A0/A1/A2/A3 are accepted which cause hello worker role toouse an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="ba292-150">Para obter mais informações sobre tamanhos de função de trabalho, consulte [Elastic Database jobs components and pricing (Preço e componentes de trabalhos do Banco de Dados Elástico)](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="ba292-150">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="ba292-151">SqlServerDatabaseSlo</span><span class="sxs-lookup"><span data-stu-id="ba292-151">SqlServerDatabaseSlo</span></span></td>
    <td><span data-ttu-id="ba292-152">Fornece o objetivo de nível de serviço Olá para uma edição Standard.</span><span class="sxs-lookup"><span data-stu-id="ba292-152">Provides hello service level objective for a Standard edition.</span></span> <span data-ttu-id="ba292-153">O padrão desse parâmetro é tooS0.</span><span class="sxs-lookup"><span data-stu-id="ba292-153">This parameter defaults tooS0.</span></span> <span data-ttu-id="ba292-154">Valores de parâmetro de S0/S1/S2/S3 são aceitas que provocam hello Azure SQL Database toouse Olá SLO do respectivo.</span><span class="sxs-lookup"><span data-stu-id="ba292-154">Parameter values of S0/S1/S2/S3 are accepted which cause hello Azure SQL Database toouse hello respective SLO.</span></span> <span data-ttu-id="ba292-155">Para obter mais informações sobre SLOs do Banco de Dados SQL, consulte [Elastic Database jobs components and pricing (Preço e componentes de trabalhos do Banco de Dados Elástico)](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="ba292-155">For more information on SQL Database SLOs, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="ba292-156">SqlServerAdministratorUserName</span><span class="sxs-lookup"><span data-stu-id="ba292-156">SqlServerAdministratorUserName</span></span></td>
    <td><span data-ttu-id="ba292-157">Fornece o nome de usuário de administrador Olá para Olá criado recentemente o servidor de banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="ba292-157">Provides hello admin user name for hello newly created Azure SQL Database server.</span></span> <span data-ttu-id="ba292-158">Quando não especificado, será aberta uma janela de credenciais do PowerShell tooprompt credenciais hello.</span><span class="sxs-lookup"><span data-stu-id="ba292-158">When not specified, a PowerShell credentials window will open tooprompt for hello credentials.</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="ba292-159">SqlServerAdministratorPassword</span><span class="sxs-lookup"><span data-stu-id="ba292-159">SqlServerAdministratorPassword</span></span></td>
    <td><span data-ttu-id="ba292-160">Fornece senha do administrador Olá para Olá criado recentemente o servidor de banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="ba292-160">Provides hello admin password for hello newly created Azure SQL Database server.</span></span> <span data-ttu-id="ba292-161">Quando não fornecido, será aberta uma janela de credenciais do PowerShell tooprompt credenciais hello.</span><span class="sxs-lookup"><span data-stu-id="ba292-161">When not provided, a PowerShell credentials window will open tooprompt for hello credentials.</span></span></td>
</tr>
</table>

<span data-ttu-id="ba292-162">Para sistemas com grandes números de trabalhos em execução em paralelo em relação a um grande número de bancos de dados de destino, é recomendável toospecify parâmetros, como: ServiceWorkerCount - 2 - ServiceVmSize A2 - SqlServerDatabaseSlo S2.</span><span class="sxs-lookup"><span data-stu-id="ba292-162">For systems that target having large numbers of jobs running in parallel against a large number of databases, it is recommended toospecify parameters such as: -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a><span data-ttu-id="ba292-163">Atualizar uma instalação existente de componentes do trabalhos de Banco de Dados Elástico usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba292-163">Update an existing Elastic Database jobs components installation using PowerShell</span></span>
<span data-ttu-id="ba292-164">**trabalhos de Banco de Dados Elástico** podem ser atualizados em uma instalação existente em relação à escala e à alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="ba292-164">**Elastic Database jobs** can be updated within an existing installation for scale and high-availability.</span></span> <span data-ttu-id="ba292-165">Esse processo permite que as atualizações futuras do código de serviço sem ter que toodrop e recriar o banco de dados de controle de saudação.</span><span class="sxs-lookup"><span data-stu-id="ba292-165">This process allows for future upgrades of service code without having toodrop and recreate hello control database.</span></span> <span data-ttu-id="ba292-166">Esse processo também pode ser usado dentro de saudação mesmo versão toomodify Olá serviço tamanho ou hello servidor worker contagem de VM.</span><span class="sxs-lookup"><span data-stu-id="ba292-166">This process can also be used within hello same version toomodify hello service VM size or hello server worker count.</span></span>

<span data-ttu-id="ba292-167">tamanho da VM tooupdate saudação de uma instalação, Olá executar script com os parâmetros a seguir toohello valores atualizados de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="ba292-167">tooupdate hello VM size of an installation, run hello following script with parameters updated toohello values of your choice.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th><span data-ttu-id="ba292-168">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="ba292-168">Parameter</span></span></th>
  <th><span data-ttu-id="ba292-169">Descrição</span><span class="sxs-lookup"><span data-stu-id="ba292-169">Description</span></span></th>
</tr>

  <tr>
    <td><span data-ttu-id="ba292-170">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="ba292-170">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="ba292-171">Identifica o nome do grupo de recursos do Azure Olá usado quando componentes de trabalho de banco de dados Elástico Olá inicialmente foram instalados.</span><span class="sxs-lookup"><span data-stu-id="ba292-171">Identifies hello Azure resource group name used when hello Elastic Database job components were initially installed.</span></span> <span data-ttu-id="ba292-172">Padrão desse parâmetro é muito "__ElasticDatabaseJob".</span><span class="sxs-lookup"><span data-stu-id="ba292-172">This parameter defaults too“__ElasticDatabaseJob”.</span></span> <span data-ttu-id="ba292-173">Já que não é recomendado toochange esse valor, você não deve ter toospecify esse parâmetro.</span><span class="sxs-lookup"><span data-stu-id="ba292-173">Since it is not recommended toochange this value, you shouldn't have toospecify this parameter.</span></span></td>
    </tr>
</tr>

</tr>

  <tr>
    <td><span data-ttu-id="ba292-174">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="ba292-174">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="ba292-175">Fornece o número de saudação do tooinstall de trabalhadores de serviço.</span><span class="sxs-lookup"><span data-stu-id="ba292-175">Provides hello number of service workers tooinstall.</span></span>  <span data-ttu-id="ba292-176">O padrão desse parâmetro é too1.</span><span class="sxs-lookup"><span data-stu-id="ba292-176">This parameter defaults too1.</span></span>  <span data-ttu-id="ba292-177">Um número maior de trabalhadores pode ser usado tooscale out Olá tooprovide e serviço de alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="ba292-177">A higher number of workers can be used tooscale out hello service and tooprovide high availability.</span></span>  <span data-ttu-id="ba292-178">É recomendável toouse "2" para implantações que exigem alta disponibilidade do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="ba292-178">It is recommended toouse “2” for deployments that require high availability of hello service.</span></span></td>
</tr>

</tr>

    <tr>
    <td><span data-ttu-id="ba292-179">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="ba292-179">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="ba292-180">Fornece o tamanho da VM Olá para uso em Olá serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="ba292-180">Provides hello VM size for usage within hello Cloud Service.</span></span> <span data-ttu-id="ba292-181">O padrão desse parâmetro é tooA0.</span><span class="sxs-lookup"><span data-stu-id="ba292-181">This parameter defaults tooA0.</span></span> <span data-ttu-id="ba292-182">Valores de parâmetros de A0/A1/A2/A3 são aceitos que fazer com que o trabalho de saudação função toouse um tamanho muito pequeno/pequeno/médio/grande, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="ba292-182">Parameters values of A0/A1/A2/A3 are accepted which cause hello worker role toouse an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="ba292-183">Para obter mais informações sobre tamanhos de função de trabalho, consulte [Elastic Database jobs components and pricing (Preço e componentes de trabalhos do Banco de Dados Elástico)](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="ba292-183">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</table>

## <a name="install-hello-elastic-database-jobs-components-using-hello-portal"></a><span data-ttu-id="ba292-184">Instalar componentes de trabalhos do banco de dados Elástico hello usando Olá Portal</span><span class="sxs-lookup"><span data-stu-id="ba292-184">Install hello Elastic Database jobs components using hello Portal</span></span>
<span data-ttu-id="ba292-185">Uma vez que [criado um pool Elástico](sql-database-elastic-pool-manage-portal.md), você pode instalar **trabalhos do banco de dados Elástico** a execução de tarefas administrativas em cada banco de dados no pool Elástico Olá tooenable componentes.</span><span class="sxs-lookup"><span data-stu-id="ba292-185">Once you have [created an elastic pool](sql-database-elastic-pool-manage-portal.md), you can install **Elastic Database jobs** components tooenable execution of administrative tasks against each database in hello elastic pool.</span></span> <span data-ttu-id="ba292-186">Diferentemente de quando usar Olá **trabalhos do banco de dados Elástico** APIs do PowerShell, a interface de portal Olá é tooonly restrita atualmente em execução em um pool existente.</span><span class="sxs-lookup"><span data-stu-id="ba292-186">Unlike when using hello **Elastic Database jobs** PowerShell APIs, hello portal interface is currently restricted tooonly executing against an existing pool.</span></span>

<span data-ttu-id="ba292-187">**Estimado tempo toocomplete:** 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="ba292-187">**Estimated time toocomplete:** 10 minutes.</span></span>

1. <span data-ttu-id="ba292-188">Na exibição de painel de saudação do pool Elástico de saudação via Olá [Portal do Azure](https://portal.azure.com/#) , clique em **criar trabalho**.</span><span class="sxs-lookup"><span data-stu-id="ba292-188">From hello dashboard view of hello elastic pool via hello [Azure Portal](https://portal.azure.com/#) , click **Create job**.</span></span>
2. <span data-ttu-id="ba292-189">Se você estiver criando um trabalho para Olá a primeira vez, você deve instalar **trabalhos do banco de dados Elástico** clicando **termos de visualização**.</span><span class="sxs-lookup"><span data-stu-id="ba292-189">If you are creating a job for hello first time, you must install **Elastic Database jobs** by clicking **PREVIEW TERMS**.</span></span>
3. <span data-ttu-id="ba292-190">Aceite termos de saudação clicando Olá a caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="ba292-190">Accept hello terms by clicking hello checkbox.</span></span>
4. <span data-ttu-id="ba292-191">Na exibição de hello "serviços de instalação", clique em **CREDENCIAIS de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="ba292-191">In hello "Install services" view, click **JOB CREDENTIALS**.</span></span>
   
    ![Instalando serviços Olá][1]
5. <span data-ttu-id="ba292-193">Digite um nome de usuário e uma senha para um administrador de banco de dados. Como parte da instalação do hello, um novo servidor de banco de dados SQL é criado.</span><span class="sxs-lookup"><span data-stu-id="ba292-193">Type a user name and password for a database admin. As part of hello installation, a new Azure SQL Database server is created.</span></span> <span data-ttu-id="ba292-194">Dentro desse novo servidor, um novo banco de dados, conhecido como banco de dados de controle Olá, é criado e usado metadados de saudação toocontain para trabalhos do banco de dados Elástico.</span><span class="sxs-lookup"><span data-stu-id="ba292-194">Within this new server, a new database, known as hello control database, is created and used toocontain hello meta data for Elastic Database jobs.</span></span> <span data-ttu-id="ba292-195">Olá nome e senha criados aqui são usados para fins de saudação de registro em log no banco de dados de controle de toohello.</span><span class="sxs-lookup"><span data-stu-id="ba292-195">hello user name and password created here are used for hello purpose of logging in toohello control database.</span></span> <span data-ttu-id="ba292-196">Uma credencial separada é usada para execução do script em bancos de dados de saudação em pool hello.</span><span class="sxs-lookup"><span data-stu-id="ba292-196">A separate credential is used for script execution against hello databases within hello pool.</span></span>
   
    ![Criar nome de usuário e senha][2]
6. <span data-ttu-id="ba292-198">Botão Olá Okey.</span><span class="sxs-lookup"><span data-stu-id="ba292-198">Click hello OK button.</span></span> <span data-ttu-id="ba292-199">componentes de saudação são criadas para você em poucos minutos em uma nova [grupo de recursos](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ba292-199">hello components are created for you in a few minutes in a new [Resource group](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="ba292-200">novo grupo de recursos Olá é fixado toohello iniciar quadro, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="ba292-200">hello new resource group is pinned toohello start board, as shown below.</span></span> <span data-ttu-id="ba292-201">Trabalhos do banco de dados após a criação, Elástico (serviço de nuvem, banco de dados SQL, barramento de serviço e armazenamento) são criados no grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ba292-201">Once created, elastic database jobs (Cloud Service, SQL Database, Service Bus, and Storage) are all created in hello group.</span></span>
   
    ![grupo de recursos na tela inicial][3]
7. <span data-ttu-id="ba292-203">Se você tentar toocreate ou gerenciar um trabalho, enquanto os trabalhos de banco de dados Elástico é instalada, fornecendo **credenciais** você verá a seguinte mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="ba292-203">If you attempt toocreate or manage a job while elastic database jobs is installing, when providing **Credentials** you will see hello following message.</span></span>
   
    ![Implantação ainda em andamento][4]

<span data-ttu-id="ba292-205">Se a desinstalação é necessária, exclua o grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="ba292-205">If uninstallation is required, delete hello resource group.</span></span> <span data-ttu-id="ba292-206">Consulte [como toouninstall Olá banco de dados Elástico trabalho componentes](sql-database-elastic-jobs-uninstall.md).</span><span class="sxs-lookup"><span data-stu-id="ba292-206">See [How toouninstall hello Elastic Database job components](sql-database-elastic-jobs-uninstall.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba292-207">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ba292-207">Next steps</span></span>
<span data-ttu-id="ba292-208">Certifique-se de uma credencial com direitos apropriados Olá para execução do script é criada em cada banco de dados no grupo de hello, para obter mais informações, consulte [proteger seu banco de dados do SQL](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="ba292-208">Ensure a credential with hello appropriate rights for script execution is created on each database in hello group, for more information see [Securing your SQL Database](sql-database-manage-logins.md).</span></span>
<span data-ttu-id="ba292-209">Consulte [criando e gerenciando um banco de dados Elástico trabalhos](sql-database-elastic-jobs-create-and-manage.md) tooget iniciado.</span><span class="sxs-lookup"><span data-stu-id="ba292-209">See [Creating and managing an Elastic Database jobs](sql-database-elastic-jobs-create-and-manage.md) tooget started.</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: ./media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: ./media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: ./media/sql-database-elastic-jobs-service-installation/not-done.png
