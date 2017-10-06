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
# <a name="installing-elastic-database-jobs-overview"></a>Visão geral de Instalando trabalhos de Banco de Dados Elástico
[**Trabalhos do banco de dados Elásticos** ](sql-database-elastic-jobs-overview.md) pode ser instalado por meio do PowerShell ou por meio de saudação Portal.You clássico do Azure podem obter acesso toocreate e gerenciar trabalhos usando Olá API PowerShell somente se você instalar o pacote do PowerShell hello. Além disso, Olá APIs do PowerShell fornecem funcionalidade significativamente mais que o portal de saudação neste momento.

Se você já tiver instalado **trabalhos do banco de dados Elástico** por meio de saudação Portal de uma já existente **pool Elástico**, visualização mais recente do Powershell de saudação inclui scripts tooupgrade sua instalação existente. É altamente recomendável tooupgrade toohello sua instalação mais recente **trabalhos do banco de dados Elástico** Olá de componentes em vantagens de tootake de ordem da nova funcionalidade exposta por meio de APIs do PowerShell.

## <a name="prerequisites"></a>Pré-requisitos
* Uma assinatura do Azure. Para obter uma avaliação gratuita, veja [Avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).
* PowerShell do Azure. Instalar a versão mais recente de hello usando Olá [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376). Para obter informações detalhadas, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).
* [O utilitário de linha de comando do NuGet](https://nuget.org/nuget.exe) é usado tooinstall Olá banco de dados Elástico trabalhos pacote. Para obter mais informações, consulte http://docs.nuget.org/docs/start-here/installing-nuget.

## <a name="download-and-import-hello-elastic-database-jobs-powershell-package"></a>Baixe e importe o pacote de PowerShell de trabalhos de banco de dados Elástico Olá
1. Inicie a janela de comando do Microsoft Azure PowerShell e navegue toohello diretório onde você baixou o utilitário de linha de comando do NuGet (nuget.exe).
2. Baixar e importar **trabalhos do banco de dados Elástico** pacote no diretório atual de saudação com hello comando a seguir:
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    Olá **trabalhos do banco de dados Elástico** os arquivos são colocados no diretório local de saudação em uma pasta chamada **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** onde *x.x.xxxx.x* reflete o número de versão de saudação. cmdlets do PowerShell Hello (incluindo DLLs de cliente necessárias) estão localizados em Olá **tools\ElasticDatabaseJobs** subdiretório e hello tooinstall de scripts do PowerShell, atualizar e desinstalar também residem em Olá  **ferramentas** subdiretório.
3. Navegue toohello ferramentas subdiretório na pasta de Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x Olá digitando cd ferramentas, por exemplo:
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. Execute o diretório do hello.\InstallElasticDatabaseJobsCmdlets.ps1 scripts toocopy Olá ElasticDatabaseJobs em $home\documents\windowspowershell\modules.. Isso também importará automaticamente módulo Olá para uso, por exemplo:
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-hello-elastic-database-jobs-components-using-powershell"></a>Instalar componentes de trabalhos do banco de dados Elástico hello usando o PowerShell
1. Inicie uma janela de comando do Microsoft Azure PowerShell e navegue toohello \tools subdiretório na pasta de Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x Olá: digite cd \tools
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. Executar script do PowerShell.\InstallElasticDatabaseJobs.ps1 hello e forneça valores para as variáveis de solicitada. Esse script cria componentes Olá descritos [banco de dados Elástico trabalhos componentes e preços](sql-database-elastic-jobs-overview.md#components-and-pricing) bem Configurando Olá serviço de nuvem do Azure tooappropriately usam os componentes dependentes hello.

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

Ao executar este comando, uma janela é aberta solicitando um **nome de usuário** e **senha**. Isso não é suas credenciais do Azure, insira o nome de usuário de saudação e a senha que serão as credenciais de administrador de saudação desejar toocreate para novo servidor de saudação.

parâmetros de saudação fornecidos nessa invocação de exemplo podem ser modificados para as configurações desejadas. seguir Olá fornece mais informações sobre o comportamento de saudação de cada parâmetro:

<table style="width:100%">
  <tr>
    <th>Parâmetro</th>
    <th>Descrição</th>
  </tr>

<tr>
    <td>ResourceGroupName</td>
    <td>Fornece o nome do grupo de recursos do Azure Olá criado Olá toocontain recém-criada em componentes do Azure. Padrão desse parâmetro é muito "__ElasticDatabaseJob". Não é recomendável toochange esse valor.</td>
    </tr>

</tr>

    <tr>
    <td>ResourceGroupLocation</td>
    <td>Fornece Olá local do Azure toobe usado para Olá recém-criada em componentes do Azure. O padrão desse parâmetro é toohello local de centro dos EUA.</td>
</tr>

<tr>
    <td>ServiceWorkerCount</td>
    <td>Fornece o número de saudação do tooinstall de trabalhadores de serviço. O padrão desse parâmetro é too1. Um número maior de trabalhadores pode ser usado tooscale out Olá tooprovide e serviço de alta disponibilidade. É recomendável toouse "2" para implantações que exigem alta disponibilidade do serviço de saudação.</td>
    </tr>

</tr>
    <tr>
    <td>ServiceVmSize</td>
    <td>Fornece o tamanho da VM Olá para uso em Olá serviço de nuvem. O padrão desse parâmetro é tooA0. Valores de parâmetros de A0/A1/A2/A3 são aceitos que fazer com que o trabalho de saudação função toouse um tamanho muito pequeno/pequeno/médio/grande, respectivamente. Para obter mais informações sobre tamanhos de função de trabalho, consulte [Elastic Database jobs components and pricing (Preço e componentes de trabalhos do Banco de Dados Elástico)](sql-database-elastic-jobs-overview.md#components-and-pricing).</td>
</tr>

</tr>
    <tr>
    <td>SqlServerDatabaseSlo</td>
    <td>Fornece o objetivo de nível de serviço Olá para uma edição Standard. O padrão desse parâmetro é tooS0. Valores de parâmetro de S0/S1/S2/S3 são aceitas que provocam hello Azure SQL Database toouse Olá SLO do respectivo. Para obter mais informações sobre SLOs do Banco de Dados SQL, consulte [Elastic Database jobs components and pricing (Preço e componentes de trabalhos do Banco de Dados Elástico)](sql-database-elastic-jobs-overview.md#components-and-pricing).</td>
</tr>

</tr>
    <tr>
    <td>SqlServerAdministratorUserName</td>
    <td>Fornece o nome de usuário de administrador Olá para Olá criado recentemente o servidor de banco de dados SQL. Quando não especificado, será aberta uma janela de credenciais do PowerShell tooprompt credenciais hello.</td>
</tr>

</tr>
    <tr>
    <td>SqlServerAdministratorPassword</td>
    <td>Fornece senha do administrador Olá para Olá criado recentemente o servidor de banco de dados SQL. Quando não fornecido, será aberta uma janela de credenciais do PowerShell tooprompt credenciais hello.</td>
</tr>
</table>

Para sistemas com grandes números de trabalhos em execução em paralelo em relação a um grande número de bancos de dados de destino, é recomendável toospecify parâmetros, como: ServiceWorkerCount - 2 - ServiceVmSize A2 - SqlServerDatabaseSlo S2.

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a>Atualizar uma instalação existente de componentes do trabalhos de Banco de Dados Elástico usando o PowerShell
**trabalhos de Banco de Dados Elástico** podem ser atualizados em uma instalação existente em relação à escala e à alta disponibilidade. Esse processo permite que as atualizações futuras do código de serviço sem ter que toodrop e recriar o banco de dados de controle de saudação. Esse processo também pode ser usado dentro de saudação mesmo versão toomodify Olá serviço tamanho ou hello servidor worker contagem de VM.

tamanho da VM tooupdate saudação de uma instalação, Olá executar script com os parâmetros a seguir toohello valores atualizados de sua escolha.

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th>Parâmetro</th>
  <th>Descrição</th>
</tr>

  <tr>
    <td>ResourceGroupName</td>
    <td>Identifica o nome do grupo de recursos do Azure Olá usado quando componentes de trabalho de banco de dados Elástico Olá inicialmente foram instalados. Padrão desse parâmetro é muito "__ElasticDatabaseJob". Já que não é recomendado toochange esse valor, você não deve ter toospecify esse parâmetro.</td>
    </tr>
</tr>

</tr>

  <tr>
    <td>ServiceWorkerCount</td>
    <td>Fornece o número de saudação do tooinstall de trabalhadores de serviço.  O padrão desse parâmetro é too1.  Um número maior de trabalhadores pode ser usado tooscale out Olá tooprovide e serviço de alta disponibilidade.  É recomendável toouse "2" para implantações que exigem alta disponibilidade do serviço de saudação.</td>
</tr>

</tr>

    <tr>
    <td>ServiceVmSize</td>
    <td>Fornece o tamanho da VM Olá para uso em Olá serviço de nuvem. O padrão desse parâmetro é tooA0. Valores de parâmetros de A0/A1/A2/A3 são aceitos que fazer com que o trabalho de saudação função toouse um tamanho muito pequeno/pequeno/médio/grande, respectivamente. Para obter mais informações sobre tamanhos de função de trabalho, consulte [Elastic Database jobs components and pricing (Preço e componentes de trabalhos do Banco de Dados Elástico)](sql-database-elastic-jobs-overview.md#components-and-pricing).</td>
</tr>

</table>

## <a name="install-hello-elastic-database-jobs-components-using-hello-portal"></a>Instalar componentes de trabalhos do banco de dados Elástico hello usando Olá Portal
Uma vez que [criado um pool Elástico](sql-database-elastic-pool-manage-portal.md), você pode instalar **trabalhos do banco de dados Elástico** a execução de tarefas administrativas em cada banco de dados no pool Elástico Olá tooenable componentes. Diferentemente de quando usar Olá **trabalhos do banco de dados Elástico** APIs do PowerShell, a interface de portal Olá é tooonly restrita atualmente em execução em um pool existente.

**Estimado tempo toocomplete:** 10 minutos.

1. Na exibição de painel de saudação do pool Elástico de saudação via Olá [Portal do Azure](https://portal.azure.com/#) , clique em **criar trabalho**.
2. Se você estiver criando um trabalho para Olá a primeira vez, você deve instalar **trabalhos do banco de dados Elástico** clicando **termos de visualização**.
3. Aceite termos de saudação clicando Olá a caixa de seleção.
4. Na exibição de hello "serviços de instalação", clique em **CREDENCIAIS de trabalho**.
   
    ![Instalando serviços Olá][1]
5. Digite um nome de usuário e uma senha para um administrador de banco de dados. Como parte da instalação do hello, um novo servidor de banco de dados SQL é criado. Dentro desse novo servidor, um novo banco de dados, conhecido como banco de dados de controle Olá, é criado e usado metadados de saudação toocontain para trabalhos do banco de dados Elástico. Olá nome e senha criados aqui são usados para fins de saudação de registro em log no banco de dados de controle de toohello. Uma credencial separada é usada para execução do script em bancos de dados de saudação em pool hello.
   
    ![Criar nome de usuário e senha][2]
6. Botão Olá Okey. componentes de saudação são criadas para você em poucos minutos em uma nova [grupo de recursos](../azure-resource-manager/resource-group-overview.md). novo grupo de recursos Olá é fixado toohello iniciar quadro, conforme mostrado abaixo. Trabalhos do banco de dados após a criação, Elástico (serviço de nuvem, banco de dados SQL, barramento de serviço e armazenamento) são criados no grupo de saudação.
   
    ![grupo de recursos na tela inicial][3]
7. Se você tentar toocreate ou gerenciar um trabalho, enquanto os trabalhos de banco de dados Elástico é instalada, fornecendo **credenciais** você verá a seguinte mensagem de saudação.
   
    ![Implantação ainda em andamento][4]

Se a desinstalação é necessária, exclua o grupo de recursos de saudação. Consulte [como toouninstall Olá banco de dados Elástico trabalho componentes](sql-database-elastic-jobs-uninstall.md).

## <a name="next-steps"></a>Próximas etapas
Certifique-se de uma credencial com direitos apropriados Olá para execução do script é criada em cada banco de dados no grupo de hello, para obter mais informações, consulte [proteger seu banco de dados do SQL](sql-database-manage-logins.md).
Consulte [criando e gerenciando um banco de dados Elástico trabalhos](sql-database-elastic-jobs-create-and-manage.md) tooget iniciado.

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: ./media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: ./media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: ./media/sql-database-elastic-jobs-service-installation/not-done.png
