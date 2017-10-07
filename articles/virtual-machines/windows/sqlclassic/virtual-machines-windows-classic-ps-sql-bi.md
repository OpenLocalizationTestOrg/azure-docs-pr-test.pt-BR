---
title: aaaSQL Server Business Intelligence | Microsoft Docs
description: "Este tópico usa recursos criados com o modelo de implantação clássico hello e descreve os recursos de Business Intelligence (BI) do hello disponíveis do SQL Server em execução em máquinas virtuais do Azure (VMs)."
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: c681e7a7-eeda-48aa-bc35-6277f4828244
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/30/2017
ms.author: asaxton
ms.openlocfilehash: e3288f0835d6c4a19baeeea5f6b65fec16cd751f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-business-intelligence-in-azure-virtual-machines"></a>Business Intelligence do SQL Server em máquinas virtuais do Azure
> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.

Galeria de máquina Virtual do Microsoft Azure Olá inclui imagens que contêm instalações do SQL Server. Olá, as edições com suporte nas imagens da Galeria de saudação do SQL Server Olá mesmos arquivos de instalação, você pode instalar computadores tooon locais e máquinas virtuais. Este tópico resume Olá SQL Server Business Intelligence (BI) recursos instalados nas imagens hello e etapas de configuração necessárias depois que uma máquina virtual é provisionada. Este tópico também descreve as topologias de implantação com suporte para recursos de BI e as práticas recomendadas.

## <a name="license-considerations"></a>Considerações sobre licenças
Há duas maneiras toolicense do SQL Server em máquinas virtuais do Microsoft Azure:

1. Benefícios de mobilidade da licença que fazem parte do Software Assurance. Para saber mais, consulte [Mobilidade de licenças por meio do Software Assurance no Azure](https://azure.microsoft.com/pricing/license-mobility/).
2. Taxa de pagamento por hora de Máquinas Virtuais do Azure com o SQL Server instalado. Consulte Olá a seção "SQL Server" em [preços das máquinas virtuais](https://azure.microsoft.com/pricing/details/virtual-machines/#Sql).

Para saber mais sobre licenciamento e taxas atuais, consulte [Perguntas frequentes sobre licenciamento de máquinas virtuais](https://azure.microsoft.com/pricing/licensing-faq/%20/).

## <a name="sql-server-images-available-in-azure-virtual-machine-gallery"></a>Imagens do SQL Server disponíveis na galeria de Máquinas Virtuais do Azure
Galeria de máquina Virtual do Microsoft Azure Olá inclui várias imagens que contêm o Microsoft SQL Server. software Olá instalado nas imagens de máquina virtual Olá varia de acordo com hello versão do sistema operacional de saudação e saudação do SQL Server. lista de saudação de imagens disponíveis na Galeria de máquina virtual do Azure Olá alterados com frequência.

<!--![SQL image in azure VM gallery](./media/virtual-machines-windows-classic-ps-sql-bi/IC741367.png)-->
![Imagem do SQL na Galeria da VM do Azure](./media/virtual-machines-windows-classic-ps-sql-bi/vm-sql-images.png)

![PowerShell](./media/virtual-machines-windows-classic-ps-sql-bi/IC660119.gif) Olá, seguinte script do PowerShell retorna Olá lista de imagens do Azure que contêm "SQL Server" hello ImageName:

    # assumes you have already uploaded a management certificate tooyour Microsoft Azure Subscription. View hello thumbprint value from hello "Subscriptions" menu in Azure portal.

    $subscriptionID = ""    # REQUIRED: Provide your subscription ID.
    $subscriptionName = "" # REQUIRED: Provide your subscription name.
    $thumbPrint = "" # REQUIRED: Provide your certificate thumbprint.
    $certificate = Get-Item cert:\currentuser\my\$thumbPrint # REQUIRED: If your certificate is in a different store, provide it here.-Ser  store is hello one specified with hello -ss parameter on MakeCert

    Set-AzureSubscription -SubscriptionName $subscriptionName -Certificate $certificate -SubscriptionID $subscriptionID

    Write-Host -foregroundcolor green "List of available gallery images where imagename contains 2016"
    Write-Host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
    get-azurevmimage | where {$_.ImageName -Like "*SQL-Server-2016*"} | select imagename,category, location, label, description

    Write-Host -foregroundcolor green "List of available gallery images where imagename contains 2014"
    Write-Host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
    get-azurevmimage | where {$_.ImageName -Like "*SQL-Server-2014*"} | select imagename,category, location, label, description

Para obter mais informações sobre as edições e os recursos com suporte do SQL Server, consulte o seguinte hello:

* [Edições do SQL Server](https://www.microsoft.com/server-cloud/products/sql-server-editions/#fbid=Zae0-E6r5oh)
* [Recursos suportados por Olá edições do SQL Server 2016](https://msdn.microsoft.com/library/cc645993.aspx)

### <a name="bi-features-installed-on-hello-sql-server-virtual-machine-gallery-images"></a>Recursos de BI instalados em Olá imagens da Galeria de máquina Virtual do SQL Server
Olá, tabela a seguir resume recursos de Business Intelligence de Olá instalados nas imagens comuns da Galeria de máquina Virtual do Microsoft Azure Olá para o SQL Server:

* SQL Server 2016 SP1 Enterprise
* SQL Server 2016 SP1 Standard
* SQL Server 2014 SP2 Enterprise
* SQL Server 2014 SP2 Standard
* SQL Server 2012 SP3 Enterprise
* SQL Server 2012 SP3 Standard

| Recurso de BI do SQL Server | Instalado na imagem da Galeria Olá | Observações |
| --- | --- | --- |
| **Modo nativo do Reporting Services** |Sim |Instalado, mas requer configuração, incluindo a URL do Gerenciador de relatórios hello. Consulte a seção Olá [configurar o Reporting Services](#configure-reporting-services). |
| **Modo SharePoint do Reporting Services** |Não |Olá imagem da Galeria da máquina Virtual do Microsoft Azure não inclui o SharePoint ou do SharePoint arquivos de instalação. <sup>1</sup> |
| **Multidimensional e mineração de dados do Analysis Services (OLAP)** |Sim |Instância do Analysis Services instalado e configurado como saudação padrão |
| **Tabela do Analysis Services** |Não |Com suporte em imagens do SQL Server 2012, 2014 e 2016, mas não está instalado por padrão. Instale outra instância do Analysis Services. Consulte a seção Olá instalar outros serviços do SQL Server e recursos neste tópico. |
| **Power Pivot do Analysis Services para SharePoint** |Não |Olá imagem da Galeria da máquina Virtual do Microsoft Azure não inclui o SharePoint ou do SharePoint arquivos de instalação. <sup>1</sup> |

<sup>1</sup> Para saber mais sobre o SharePoint e as máquinas virtuais do Azure, consulte Arquiteturas do [Microsoft Azure](https://technet.microsoft.com/library/dn635309.aspx) para SharePoint 2013 e Implantação do [SharePoint em máquinas virtuais do Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=34598).

![PowerShell](./media/virtual-machines-windows-classic-ps-sql-bi/IC660119.gif) Execute Olá tooget de comando do PowerShell a seguir uma lista de serviços instalados que contêm "SQL" no nome do serviço de saudação.

    get-service | Where-Object{ $_.DisplayName -like '*SQL*' } | Select DisplayName, status, servicetype, dependentservices | format-Table -AutoSize

## <a name="general-recommendations-and-best-practices"></a>Recomendações gerais e práticas recomendadas
* Olá mínimo tamanho recomendado para uma máquina virtual é **A3** ao usar o SQL Server Enterprise Edition. Olá **A4** tamanho da máquina virtual é recomendado para implantações de BI do SQL Server Analysis Services e Reporting Services.
  
    Para obter informações sobre tamanhos VM atuais hello, consulte [tamanhos de máquina Virtual para o Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Uma prática recomendada para o gerenciamento de disco é diferente de toostore dados, log e arquivos de backup em unidades **C**: e **D**:. Por exemplo, crie discos de dados **E**: e **F**:.
  
  * unidade de saudação política de cache da unidade padrão de saudação **C**: não é ideal para trabalhar com dados.
  * Olá **D**: unidade é uma unidade temporária que é usada principalmente para o arquivo de paginação de saudação. Olá **D**: não é persistente e não é salva no armazenamento de blob. Tarefas de gerenciamento, como um tamanho de máquina virtual toohello alteração redefinir Olá **D**: unidade. Recomenda-se muito**não** usar Olá **D**: disco para arquivos de banco de dados, incluindo tempdb.
    
    Para obter mais informações sobre como criar e anexar discos, consulte [como tooAttach uma máquina Virtual de tooa do disco de dados](../classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
* Interrompa ou desinstale os serviços que você não planeja toouse. Por exemplo se a máquina virtual de saudação é usada somente para o Reporting Services, parar ou desinstalar o Analysis Services e SQL Server Integration Services. Olá imagem a seguir é um exemplo dos serviços de saudação que são iniciados por padrão.
  
    ![Serviços do SQL Server](./media/virtual-machines-windows-classic-ps-sql-bi/IC650107.gif)
  
  > [!NOTE]
  > mecanismo de banco de dados do SQL Server Olá é necessário em cenários de BI de saudação com suporte. Em uma topologia VM de servidor único, o mecanismo de banco de dados de saudação é necessário toobe em execução no hello mesma VM.
  
    Para obter mais informações, consulte o seguinte Olá: [desinstalar o Reporting Services](https://msdn.microsoft.com/library/hh479745.aspx) e [desinstalar uma instância do Analysis Services](https://msdn.microsoft.com/library/ms143687.aspx).
* Verifique se há novas ‘Atualizações importantes’ no **Windows Update** . imagens de máquina Virtual do Microsoft Azure Olá são atualizadas com frequência; No entanto atualizações importantes podem se tornar disponíveis do **Windows Update** depois que a imagem da VM Olá foi atualizada pela última vez.

## <a name="example-deployment-topologies"></a>Exemplo de topologias de implantação
Olá seguem as implantações de exemplo que usam máquinas virtuais do Microsoft Azure. topologias de saudação nesses diagramas são apenas algumas das topologias possíveis hello, que você pode usar os recursos de BI do SQL Server e máquinas virtuais do Microsoft Azure.

### <a name="single-virtual-machine"></a>Máquina Virtual individual
Analysis Services, Reporting Services, Mecanismo de Banco de Dados SQL Server e fontes de dados em uma única máquina virtual.

![cenário bi iaas com uma máquina virtual](./media/virtual-machines-windows-classic-ps-sql-bi/IC650108.gif)

### <a name="two-virtual-machines"></a>Duas Máquinas Virtuais
* Analysis Services, Reporting Services e Olá mecanismo de banco de dados do SQL Server em uma única máquina virtual. Essa implantação inclui bancos de dados de servidor de relatório hello.
* Fontes de dados em uma segunda VM. Olá segunda VM inclui o mecanismo de banco de dados do SQL Server como uma fonte de dados.

![cenário bi iaas com duas máquinas virtuais](./media/virtual-machines-windows-classic-ps-sql-bi/IC650109.gif)

### <a name="mixed-azure--data-on-azure-sql-database"></a>Azure combinado – dados no banco de dados SQL do Azure
* Analysis Services, Reporting Services e Olá mecanismo de banco de dados do SQL Server em uma única máquina virtual. Essa implantação inclui bancos de dados de servidor de relatório hello.
* A fonte de dados é o banco de dados SQL do Azure.

![cenários bi iaas com vm e AzureSQL como fonte de dados](./media/virtual-machines-windows-classic-ps-sql-bi/IC650110.gif)

### <a name="hybrid-data-on-premises"></a>Híbrido – dados locais
* Este exemplo de implantação do Analysis Services, Reporting Services e Olá mecanismo de banco de dados do SQL Server executado em uma única máquina virtual. hosts de máquina virtual Olá Olá bancos de dados de servidor de relatório. máquina virtual de saudação é tooan ingressado no domínio local por meio da rede Virtual do Azure, ou alguns outros VPN solução de encapsulamento.
* A fonte de dados é local.

![fontes de dados locais e da vm de cenários iaas de bi](./media/virtual-machines-windows-classic-ps-sql-bi/IC654384.gif)

## <a name="reporting-services-native-mode-configuration"></a>Configuração do modo Nativo do Reporting Services
imagem da Galeria Olá máquina virtual para o SQL Server inclui o modo nativo do Reporting Services instalado, no entanto, o servidor de relatório Olá não está configurado. etapas de Olá nesta seção configuram o servidor de relatório do Reporting Services Olá. Para obter informações mais detalhadas sobre como configurar o modo Nativo do Reporting Services, consulte [Instalar o servidor de relatório no modo nativo do Reporting Services (SSRS)](https://msdn.microsoft.com/library/ms143711.aspx).

> [!NOTE]
> Para obter conteúdo semelhante que usa o servidor de relatório do Windows PowerShell scripts tooconfigure hello, consulte [tooCreate de usar o PowerShell um Azure VM com um modo de servidor de relatório nativo](../classic/ps-sql-report.md).

### <a name="connect-toohello-virtual-machine-and-start-hello-reporting-services-configuration-manager"></a>Conecte-se toohello Máquina Virtual e iniciar Olá Gerenciador de configuração do Reporting Services
Há dois fluxos de trabalho comuns para conexão tooan Máquina Virtual do Azure:

* tooconnect em hello, clique Olá nome da máquina virtual de saudação e, em seguida, clique em **conectar**. Abre uma conexão de área de trabalho remota e o nome do computador Olá é preenchida automaticamente.
  
    ![Conecte-se a máquina virtual de tooazure](./media/virtual-machines-windows-classic-ps-sql-bi/IC650112.gif)
* Conecte a máquina virtual de toohello com Conexão de área de trabalho remota do Windows. Na interface do usuário da área de trabalho remota Olá Olá:
  
  1. Saudação de tipo **nome do serviço de nuvem** como nome do computador hello.
  2. Digite dois-pontos (:) e Olá número da porta pública configurado para o ponto de extremidade Olá TCP remoto da área de trabalho.
     
      Myservice.cloudapp.net:63133
     
      Para obter mais informações, consulte [O que é um serviço de nuvem?](https://azure.microsoft.com/manage/services/cloud-services/what-is-a-cloud-service/).


**Inicie o Gerenciador de Configurações do Reporting Services**

No **Windows Server 2012/2016**:

1. De saudação **iniciar** tela, digite **Reporting Services** toosee uma lista de aplicativos.
2. Clique com o botão direito do mouse no **Gerenciador de Configuração do Reporting Services** e clique em **Executar como Administrador**.

No **Windows Server 2008 R2**:

1. Clique em **Iniciar** e em **TODOS os Programas**.
2. Clique em **Microsoft SQL Server 2016**.
3. Clique em **Ferramentas de Configuração**.
4. Clique com o botão direito do mouse no **Gerenciador de Configuração do Reporting Services** e clique em **Executar como Administrador**.

Ou:

1. Clique em **Iniciar**.
2. Em Olá **pesquisar programas e arquivos** tipo de caixa de diálogo **reporting services**. Se Olá VM estiver executando o Windows Server 2012, digite **reporting services** na tela inicial do Windows Server 2012 do hello.
3. Clique com o botão direito do mouse no **Gerenciador de Configuração do Reporting Services** e clique em **Executar como Administrador**.
   
    ![pesquisar gerenciador de configuração do ssrs](./media/virtual-machines-windows-classic-ps-sql-bi/IC650113.gif)

### <a name="configure-reporting-services"></a>Configurar o Reporting Services
**Conta de serviço e URL do serviço Web:**

1. Verifique se Olá **nome do servidor** é o nome do servidor local hello e clique em **conectar**.
2. Saudação de anotação em branco **nome de banco de dados do servidor de relatório**. banco de dados de saudação é criado quando Olá configuração for concluída.
3. Verifique se Olá **Status do servidor de relatório** é **iniciado**. Se você deseja tooverify Olá serviço no Windows Server Manager, o serviço de saudação é Olá **SQL Server Reporting Services** serviço do Windows.
4. Clique em **conta de serviço** e altere a conta de saudação conforme necessário. Se a máquina virtual de saudação é usada em um ambiente Unido fora do domínio, Olá interno **ReportServer** conta é suficiente. Para obter mais informações sobre a conta de serviço hello, consulte [conta de serviço](https://msdn.microsoft.com/library/ms189964.aspx).
5. Clique em **URL do serviço Web** no painel esquerdo da saudação.
6. Clique em **aplicar** valores do tooconfigure saudação padrão.
7. Saudação de Observação **URLs de serviço Web do Report Server**. Observe que a porta padrão TCP Olá 80 e faz parte da URL de saudação. Em uma etapa posterior, você deve criar um ponto de extremidade de máquina Virtual do Microsoft Azure para a porta de saudação.
8. Em Olá **resultados** painel, verifique se ações de saudação foi concluídas com êxito.

**Banco de dados:**

1. Clique em **banco de dados** no painel esquerdo da saudação.
2. Clique em **Alterar Banco de Dados**.
3. Verifique se **Criar um novo banco de dados do servidor de relatório** está selecionada e clique em Avançar.
4. Verifique o **Nome do Servidor** e clique em **Testar Conexão**.
5. Se o resultado de saudação é **Testar conexão bem-sucedida**, clique em **Okey** e, em seguida, clique em **próximo**.
6. Nome do banco de dados de anotação Olá é **ReportServer** e hello **modo de servidor de relatório** é **nativo** , em seguida, clique em **próximo**.
7. Clique em **próximo** em Olá **credenciais** página.
8. Clique em **próximo** em Olá **resumo** página.
9. Clique em **próximo** em Olá **progresso e conclusão** página.

**URL do Portal da Web ou URL do Gerenciador de Relatórios para as versões 2012 e 2014:**

1. Clique em **URL do Portal Web**, ou **URL do Report Manager** 2014 e 2012, no painel esquerdo da saudação.
2. Clique em **Aplicar**.
3. Em Olá **resultados** painel, verifique se ações de saudação foi concluídas com êxito.
4. Clique em **Sair**.

Para saber mais sobre permissões do servidor de relatório, consulte [Concedendo permissões em um Servidor de Relatório em Modo Nativo](https://msdn.microsoft.com/library/ms156014.aspx).

### <a name="browse-toohello-local-report-manager"></a>Procurar toohello Gerenciador de relatórios local
configuração de saudação tooverify, procurar tooreport gerente Olá VM.

1. Em Olá VM, inicie o Internet Explorer com privilégios de administrador.
2. Procure toohttp://localhost/reports em Olá VM.

### <a name="tooconnect-tooremote-web-portal-or-report-manager-for-2014-and-2012"></a>o portal da web tooConnect tooRemote ou Gerenciador de relatórios para 2014 e 2012
Se você quiser o portal da web tooconnect toohello ou Gerenciador de relatórios para 2014 e 2012, na máquina virtual de saudação de um computador remoto, crie uma nova máquina virtual ponto de extremidade TCP. Por padrão, o servidor de relatório Olá escuta solicitações HTTP na **a porta 80**. Se você configurar Olá relatório servidor URLs toouse uma porta diferente, você deve especificar esse número de porta no hello instruções a seguir.

1. Crie um ponto de extremidade para Olá Máquina Virtual do TCP Port 80. Para obter mais informações, consulte Olá [pontos de extremidade de máquina Virtual e as portas de Firewall](#virtual-machine-endpoints-and-firewall-ports) seção neste documento.
2. Abra a porta 80 no firewall da máquina de virtual hello.
3. Navegar no portal da web de toohello ou Gerenciador de relatórios, usando a máquina Virtual do Azure **nome DNS** como nome do servidor Olá Olá URL. Por exemplo:
   
    **Servidor de relatório**: http://uebi.cloudapp.net/reportserver **Portal da Web**: http://uebi.cloudapp.net/reports
   
    [Configurar um firewall para acesso ao servidor de relatório](https://msdn.microsoft.com/library/bb934283.aspx)

### <a name="toocreate-and-publish-reports-toohello-azure-virtual-machine"></a>tooCreate e publicar relatórios toohello Máquina Virtual do Azure
Olá tabela a seguir resume alguns dos relatórios existentes do hello opções toopublish disponíveis de um servidor de relatório local computador toohello hospedado em Olá Máquina Virtual do Microsoft Azure:

* **Construtor de relatórios**: máquina virtual de saudação inclui Olá clique-uma vez a versão do construtor de relatórios do Microsoft SQL Server para SQL 2014 e 2012. saudação de construtor relatório toostart primeira vez em máquina virtual Olá SQL 2016:
  
  1. Inicie o navegador com privilégios administrativos.
  2. Procurar portal web toohello na máquina virtual de Olá e selecione Olá **baixar** ícone no canto superior direito de saudação.
  3. Selecione **Construtor de Relatórios**.
     
     Para saber mais, veja [Iniciar o Construtor de Relatórios](https://msdn.microsoft.com/library/ms159221.aspx).
* **SQL Server Data Tools**: VM: SQL Server Data Tools está instalado na máquina virtual de saudação e pode ser usado toocreate **projetos do servidor de relatório** e relatórios na máquina virtual de saudação. SQL Server Data Tools pode publicar o servidor de relatório de toohello Olá relatórios na máquina virtual de saudação.
* **SQL Server Data Tools: Remoto**: no computador local, crie um projeto do Reporting Services no SQL Server Data Tools que contenha os relatórios do Reporting Services. Configure projeto Olá toohello tooconnect URL do serviço web.
  
    ![propriedades de projeto ssdt para projeto SSRS](./media/virtual-machines-windows-classic-ps-sql-bi/IC650114.gif)
* Criar um. Disco rígido VHD que contém relatórios e, em seguida, carregue e anexe a unidade de saudação.
  
  1. Crie um disco rígido .VHD no computador local com seus relatórios.
  2. Crie e instale um certificado de gerenciamento.
  3. Carregar Olá tooAzure de arquivo VHD usando o cmdlet Add-AzureVHD do hello [criar e carregar um VHD do Windows Server tooAzure](../classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
  4. Anexe a máquina virtual do hello disco toohello.

## <a name="install-other-sql-server-services-and-features"></a>Instalar outros serviços e recursos do SQL Server
tooinstall adicionais do SQL Server dos serviços, como o Analysis Services no modo de tabela, execute o Assistente de instalação do hello SQL server. arquivos de instalação de saudação estão no disco local da máquina de virtual hello.

1. Clique em **Iniciar** e em **Todos os Programas**.
2. Clique em **Microsoft SQL Server 2016**, em **Microsoft SQL Server 2014** ou em **Microsoft SQL Server 2012** e clique em **Ferramentas de Configuração**.
3. Clique em **Central de Instalação do SQL Server**.

Ou execute C:\SQLServer_13.0_full\setup.exe, C:\SQLServer_12.0_full\setup.exe ou C:\SQLServer_11.0_full\setup.exe

> [!NOTE]
> Olá primeira vez que você executar a instalação do SQL Server, instalação de mais arquivos podem ser baixados e requerem a reinicialização da máquina virtual de saudação e a reinicialização da instalação do SQL Server.
> 
> Se você precisar toorepeatedly personalizar Olá imagem selecionada de saudação Máquina Virtual do Microsoft Azure, considere criar sua própria imagem do SQL Server. A funcionalidade SysPrep do Analysis Services foi habilitada com o SQL Server 2012 SP1 CU2. Para saber mais, consulte [Considerações sobre a instalação do SQL Server usando SysPrep](https://msdn.microsoft.com/library/ee210754.aspx) e [Suporte do Sysprep para funções de servidor](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).
> 
> 

### <a name="tooinstall-analysis-services-tabular-mode"></a>tooInstall modo Tabular do Analysis Services
Olá as etapas nesta seção **resumir** Olá a instalação do modo de tabela do Analysis Services. Para obter mais informações, consulte o seguinte hello:

* [Instalar o Analysis Services em Modo de Tabela](https://msdn.microsoft.com/library/hh231722.aspx)
* [Modelagem de tabela (tutorial da Adventure Works)](https://msdn.microsoft.com/library/140d0b43-9455-4907-9827-16564a904268)

**tooInstall modo Tabular do Analysis Services:**

1. No Assistente de instalação do SQL Server hello, clique em **instalação** em Olá painel esquerdo e, em seguida, clique em **instalação autônoma do novo SQL server ou adicionar recursos tooan existente instalação**.
   
   * Se você vir Olá **Procurar pasta**, procurar tooc:\SQLServer_13.0_full, c:\SQLServer_12.0_full ou c:\SQLServer_11.0_full e, em seguida, clique em **Okey**.
2. Clique em **próximo** na página de atualizações de produto hello.
3. Em Olá **tipo de instalação** página, selecione **executar uma nova instalação do SQL Server** e clique em **próximo**.
4. Em Olá **função de instalação** , clique em **instalação de recursos do SQL Server**.
5. Em Olá **seleção de recursos** , clique em **Analysis Services**.
6. Em Olá **configuração da instância** página, digite um nome descritivo, como **Tabular** em **instância nomeada** e **Id de instância** texto caixas.
7. Em Olá **configuração do Analysis Services** página, selecione **modo de tabela**. Adicione lista de permissões administrativas para Olá atual usuário toohello.
8. Conclua e feche o Assistente de instalação do SQL Server hello.

## <a name="analysis-services-configuration"></a>Configuração do Analysis Services
### <a name="remote-access-tooanalysis-services-server"></a>TooAnalysis de acesso remoto dos serviços de servidor
O servidor do Analysis Services dá suporte apenas à autenticação do Windows . tooaccess Analysis Services remotamente a partir de aplicativos cliente, como o SQL Server Management Studio ou o SQL Server Data Tools, precisa de máquina virtual de saudação toobe tooyour ingressado no domínio local, usando a rede Virtual do Azure. Para saber mais, consulte [Rede Virtual do Azure](../../../virtual-network/virtual-networks-overview.md).

Uma **instância padrão** do Analysis Services escuta na porta TCP **2383**. Abra a porta de saudação no firewall de máquinas virtuais de saudação. Uma instância nomeada em cluster do Analysis Services também escuta na porta **2383**.

Para uma **instância nomeada** do Analysis Services, Olá serviço navegador do SQL Server é necessário acesso de porta toomanage. configuração de padrão de navegador do SQL Server Olá é a porta **2382**.

Abrir a porta no firewall de máquinas virtuais hello, **2382** e criar um Analysis Services estático porta de instância nomeada.

1. tooverify portas que já estão em usar Olá VM e qual processo está usando portas hello, execute Olá comando com privilégios administrativos a seguir:
   
        netstat /ao
2. Porta de instância nomeada Use SQL Server Management Studio toocreate um estático do Analysis Services, atualizando 'Porta' valor na tabela AS propriedades gerais da instância. Para obter mais informações, consulte hello "Usar uma porta fixa para um padrão ou instância nomeada" em [configurar o Firewall do Windows de saudação tooAllow acesso ao Analysis Services](https://msdn.microsoft.com/library/ms174937.aspx#bkmk_fixed).
3. Reinicie instância de tabela de saudação do hello serviço Analysis Services.

Para obter mais informações, consulte Olá **pontos de extremidade de máquina Virtual e as portas de Firewall** seção neste documento.

## <a name="virtual-machine-endpoints-and-firewall-ports"></a>Pontos de extremidade de máquina virtual e portas de firewall
Esta seção resume os pontos de extremidade de máquina Virtual do Microsoft Azure tooopen de toocreate e portas nos firewalls da máquina virtual de saudação. Olá, tabela a seguir resume Olá **TCP** portas toocreate pontos de extremidade e Olá tooopen de portas no firewall de máquinas virtuais de saudação.

* Se você estiver usando uma única VM e hello dois itens a seguir forem verdadeiras, você não precisa de pontos de extremidade VM toocreate e você não precisa de portas de saudação tooopen no firewall Olá Olá VM.
  
  * Você não se conectar remotamente toohello recursos do SQL Server na VM de saudação. Estabelecer uma conexão de área de trabalho remota de toohello VM e acessar recursos do SQL Server Olá localmente no hello VM não é considerada uma conexão remota toohello do SQL Server de recursos.
  * Não é necessário unir domínio do hello VM tooan local por meio de rede Virtual do Azure ou outra solução de túnel VPN.
* Se a máquina virtual de saudação não é tooa ingressado no domínio, mas você deseja tooremotely conectar toohello recursos do SQL Server na máquina virtual:
  
  * Abrir as portas de saudação no firewall Olá Olá VM.
  * Criar pontos de extremidade de máquina virtual para Olá observado portas (*).
* Se a máquina virtual de saudação é tooa ingressado no domínio usando um túnel VPN, como a rede Virtual do Azure, pontos de extremidade de saudação não são necessários. No entanto abra portas de saudação no firewall Olá Olá VM.
  
  | Porta | Tipo | Descrição |
  | --- | --- | --- |
  | **80** |TCP |Acesso remoto ao servidor de relatório (*). |
  | **1433** |TCP |SQL Server Management Studio (*). |
  | **1434** |UDP |SQL Server Browser. Isso é necessário quando Olá VM tooa ingressado no domínio. |
  | **2382** |TCP |SQL Server Browser. |
  | **2383** |TCP |Instância padrão do SQL Server Analysis Services e instâncias nomeadas em cluster. |
  | **Definido pelo usuário** |TCP |Crie um Analysis Services estático chamado de porta de instância para um número de porta que você escolher e desbloquear o número da porta Olá no firewall hello. |

Para obter mais informações sobre a criação de pontos de extremidade, consulte o seguinte hello:

* Criar pontos de extremidade:[como pontos de extremidade de tooSet tooa Máquina Virtual](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
* SQL Server: Consulte a seção "Concluir a configuração etapas tooconnect toohello máquina virtual usando o SQL Server Management Studio" hello [provisionar uma máquina Virtual do SQL Server no Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).

Olá diagrama a seguir ilustra Olá portas tooopen em Olá VM firewall tooallow acesso remoto toofeatures e componentes no hello VM.

![portas tooopen aplicativos de bi em máquinas virtuais do Azure](./media/virtual-machines-windows-classic-ps-sql-bi/IC654385.gif)

## <a name="resources"></a>Recursos
* Examine a política de suporte de saudação do software de servidor da Microsoft usado no ambiente de máquina Virtual do Azure hello. Olá tópico a seguir resume o suporte para recursos como BitLocker, Clustering de Failover e balanceamento de carga de rede. [Suporte de software a servidores da Microsoft para máquinas virtuais do Azure](http://support.microsoft.com/kb/2721672)
* [Visão geral do SQL Server em máquinas virtuais do Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md)
* [Máquinas virtuais](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Provisionando uma máquina virtual do SQL Server no Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md)
* [Como tooAttach uma máquina Virtual de tooa do disco de dados](../classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Migrando um banco de dados tooSQL Server em uma VM do Azure](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json)
* [Determinar Olá modo de servidor de uma instância do Analysis Services](https://msdn.microsoft.com/library/gg471594.aspx)
* [Modelagem multidimensional (tutorial da Adventure Works)](https://technet.microsoft.com/library/ms170208.aspx)
* [Centro de Documentação do Azure](https://azure.microsoft.com/documentation/)
* [Usando o Power BI em um ambiente híbrido](https://msdn.microsoft.com/library/dn798994.aspx)

> [!NOTE]
> [Enviar comentários e informações de contato pelo Microsoft SQL Server Connect](https://connect.microsoft.com/SQLServer/Feedback)

### <a name="community-content"></a>Conteúdo da comunidade
* [Gerenciamento de banco de dados SQL do Azure com o PowerShell](http://blogs.msdn.com/b/windowsazure/archive/2013/02/07/windows-azure-sql-database-management-with-powershell.aspx)

