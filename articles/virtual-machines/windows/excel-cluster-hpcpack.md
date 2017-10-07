---
title: aaaHPC pacote de cluster para o Excel e SOA | Microsoft Docs
description: "Introdução à execução de cargas de trabalho SOA e Excel em larga escala em um cluster HPC Pack no Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: cb6a9abe-caf3-44da-b911-849a50f6cfb3
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 55b4b2c25fe65d06b75025cc23c3c13b8b764238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-running-excel-and-soa-workloads-on-an-hpc-pack-cluster-in-azure"></a>Introdução à execução de cargas de trabalho do Excel e SOA em um cluster HPC Pack no Azure
Este artigo mostra como toodeploy um Microsoft HPC Pack 2012 R2 cluster em máquinas virtuais do Azure usando um modelo de início rápido do Azure, ou, opcionalmente, um script de implantação do Azure PowerShell. cluster Olá usa toorun projetadas de imagens de VM do Azure Marketplace Microsoft Excel ou cargas de trabalho de arquitetura orientada a serviços (SOA) com o HPC Pack. Você pode usar o hello toorun de cluster HPC do Excel e serviços SOA de um computador de cliente local. serviços do Excel HPC Olá incluem descarregamento de pasta de trabalho do Excel e funções definidas pelo usuário do Excel ou UDFs.

> [!IMPORTANT] 
> Este artigo se baseia em recursos, modelos e scripts do HPC Pack 2012 R2. Atualmente, este cenário não tem suporte no HPC Pack 2016.
>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Em um nível alto, hello diagrama a seguir mostra o cluster de HPC Pack Olá que você criar.

![Cluster HPC com nós que executam cargas de trabalho do Excel][scenario]

## <a name="prerequisites"></a>Pré-requisitos
* **Computador cliente** -pode ser necessário um cliente baseado em Windows computador toosubmit exemplo do Excel e SOA trabalhos toohello cluster. Você também precisará uma saudação de toorun de computador do Windows Azure PowerShell script de implantação de cluster (se você escolher esse método de implantação).
* **Assinatura do Azure** – Se não tiver uma, você poderá criar uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.
* **Cota de núcleos** -você pode precisar de uma cota de Olá tooincrease de núcleos, especialmente se você implantar vários nós de cluster com tamanhos VM com vários núcleos. Se você estiver usando um modelo de início rápido do Azure, a cota de núcleos Olá no Gerenciador de recursos é por região do Azure. Nesse caso, você pode precisar de uma cota de saudação tooincrease em uma região específica. Consulte [Assinatura do Azure e limite de serviços, cotas e restrições](../../azure-subscription-service-limits.md). uma cota de tooincrease [abrir uma solicitação de suporte do cliente online](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) sem custo adicional.
* **Licença do Microsoft Office** – se você implantar nós de computação usando uma imagem de VM do Marketplace HPC Pack 2012 R2 com Microsoft Excel, uma versão de avaliação de 30 dias do Microsoft Excel Professional Plus 2013 será instalada. Após o período de avaliação do hello, você precisa tooprovide um válido Microsoft Office licença tooactivate Excel toocontinue toorun cargas de trabalho. Confira [Ativação do Excel](#excel-activation) mais adiante neste artigo. 

## <a name="step-1-set-up-an-hpc-pack-cluster-in-azure"></a>Etapa 1. Configurar um cluster de HPC Pack no Azure
Mostramos dois tooset opções cluster de HPC Pack 2012 R2 Olá: primeiro, usando um modelo de início rápido do Azure e Olá portal do Azure; e, segundo, usando um script de implantação do Azure PowerShell.

### <a name="option-1-use-a-quickstart-template"></a>Opção 1. Usar um modelo de início rápido
Use um tooquickly de modelo de início rápido do Azure implantar um cluster de HPC Pack em Olá portal do Azure. Quando você abre o modelo de saudação no portal de saudação, você obtém uma interface do usuário simple em que você insira configurações de saudação para seu cluster. Aqui estão as etapas de saudação. 

> [!TIP]
> Se quiser, use um [modelo do Azure Marketplace](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) que cria um cluster semelhante, especificamente para cargas de trabalho do Excel. Olá etapas um pouco diferentes do seguinte hello.
> 
> 

1. Visite Olá [página de modelo de criação de Cluster de HPC no GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster). Se você quiser, examine as informações sobre o modelo hello e código-fonte hello.
2. Clique em **implantar tooAzure** toostart uma implantação com modelo Olá Olá portal do Azure.
   
   ![Implantar o modelo tooAzure][github]
3. No portal de hello, siga esses parâmetros de saudação tooenter etapas para o modelo de cluster HPC hello.
   
   a. Em Olá **parâmetros** página, digite ou modifique os valores para parâmetros de modelo de saudação. (Clique Olá ícone próximo tooeach configuração para obter informações de Ajuda.) Valores de exemplo são mostrados no hello tela a seguir. Este exemplo cria um cluster denominado *hpc01* em Olá *hpc.local* domínio consiste em um nó de cabeçalho e de 2 nós de computação. nós de computação Olá são criados de uma imagem de VM do HPC Pack que inclui o Microsoft Excel.
   
   ![Inserir parâmetros][parameters-new-portal]
   
   > [!NOTE]
   > nó de cabeçalho Olá VM é criada automaticamente da saudação [última imagem do Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) do HPC Pack 2012 R2 no Windows Server 2012 R2. Atualmente a imagem de saudação é baseada em HPC Pack 2012 R2 Update 3.
   > 
   > VMs do nó de computação são criadas de imagem mais recente de saudação da família de nó de computação de saudação selecionada. Selecione Olá **ComputeNodeWithExcel** opção hello mais recente HPC Pack computação nó imagem que inclui uma versão de avaliação do Microsoft Excel Professional Plus 2013. toodeploy um cluster para sessões SOA gerais ou para o descarregamento de UDF do Excel, escolha Olá **ComputeNode** opção (sem o Excel instalado).
   > 
   > 
   
   b. Escolha a assinatura de saudação.
   
   c. Criar um grupo de recursos de cluster hello, como *hpc01RG*.
   
   d. Escolha um local para o grupo de recursos hello, como centro dos EUA.
   
   e. Em Olá **termos legais** , examine os termos de saudação. Se concordar, clique em **Comprar**. Em seguida, quando você terminar de definir valores de saudação para o modelo de saudação, clique em **criar**.
4. Ao concluir a implantação da saudação (normalmente demora cerca de 30 minutos), Exportar arquivo de certificado de cluster Olá Olá principal do nó de cluster. Em uma etapa posterior, você importar o certificado público no hello tooprovide saudação do servidor autenticação do computador cliente para a associação de HTTP segura.
   
   a. No portal do Azure de Olá, vá toohello painel, o nó principal do hello select e clique em **conectar** na parte superior de saudação do hello tooconnect de página usando a área de trabalho remota.
   
    <!-- ![Connect toohello head node][connect] -->
   
   b. Use procedimentos padrão no Gerenciador de certificados tooexport Olá nó principal certificado (localizado em Cert: \localmachine\my.) sem chave privada hello. Neste exemplo, exporte *CN = hpc01.eastus.cloudapp.azure.com*.
   
   ![Exportar certificado Olá][cert]

### <a name="option-2-use-hello-hpc-pack-iaas-deployment-script"></a>Opção 2. Usar script de implantação de IaaS do HPC Pack Olá
Olá script de implantação IaaS do HPC Pack fornece toodeploy de outra forma versátil um cluster de HPC Pack. Ele cria um cluster no modelo de implantação clássico Olá, enquanto o modelo de saudação usa o modelo de implantação do Azure Resource Manager hello. Além disso, o script hello é compatível com uma assinatura no hello Global do Azure ou serviço do Azure na China.

**Pré-requisitos adicionais**

* **Azure PowerShell** - [Instale e configure o Azure PowerShell](/powershell/azure/overview) (versão 0.8.10 ou posterior) no computador cliente.
* **Script de implantação IaaS do HPC Pack** - baixar e descompactar a versão mais recente de saudação do script Olá Olá [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). Verifique a versão de saudação do script hello executando `New-HPCIaaSCluster.ps1 –Version`. Este artigo se baseia na versão 4.5.0 ou posterior do script hello.

**Criar arquivo de configuração de saudação**

 Olá script de implantação IaaS do HPC Pack usa um arquivo de configuração XML como entrada que descreve a infraestrutura de saudação do cluster HPC hello. toodeploy criados a partir da imagem do nó de computação Olá que inclui o Microsoft Excel, de nós de computação de um cluster consiste em um nó principal e 18 substituir valores para o ambiente em Olá arquivo de configuração de exemplo a seguir. Para obter mais informações sobre o arquivo de configuração hello, consulte o arquivo de Manual.rtf Olá na pasta de script hello e [criar um cluster HPC com hello script de implantação IaaS do HPC Pack](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

```
<?xml version="1.0" encoding="utf-8"?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>MySubscription</SubscriptionName>
    <StorageAccount>hpc01</StorageAccount>
  </Subscription>
  <Location>West US</Location>
  <VNet>
    <VNetName>hpc-vnet01</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>HPCExcelDC01</VMName>
      <ServiceName>HPCExcelDC01</ServiceName>
      <VMSize>Medium</VMSize>
    </DomainController>
  </Domain>
   <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>HPCExcelHN01</VMName>
    <ServiceName>HPCExcelHN01</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI/>
    <EnableWebPortal/>
    <PostConfigScript>C:\tests\PostConfig.ps1</PostConfigScript>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>HPCExcelCN%00%</VMNamePattern>
    <ServiceName>HPCExcelCN01</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>18</NodeCount>
    <ImageName>HPCPack2012R2_ComputeNodeWithExcel</ImageName>
  </ComputeNodes>
</IaaSClusterConfig>
```

**Observações sobre o arquivo de configuração de saudação**

* Olá **VMName** do nó principal Olá **deve** Olá mesmo como Olá **ServiceName**, ou toorun realizá-SOA.
* Verifique se você especificar **EnableWebPortal** para que hello certificado do nó principal é gerado e exportado.
* arquivo de saudação especifica um script do PowerShell pós-configuração PostConfig.ps1 que é executado no nó principal hello. Olá script de exemplo a seguir define a cadeia de caracteres de conexão de armazenamento do Azure hello, remove a função de nó de computação de saudação do nó principal hello e coloca todos os nós online quando eles são implantados. 

```
    # add hello HPC Pack powershell cmdlets
        Add-PSSnapin Microsoft.HPC

    # set hello Azure storage connection string for hello cluster
        Set-HpcClusterProperty -AzureStorageConnectionString 'DefaultEndpointsProtocol=https;AccountName=<yourstorageaccountname>;AccountKey=<yourstorageaccountkey>'

    # remove hello compute node role for head node toomake sure hello Excel workbook won’t run on head node
        Get-HpcNode -GroupName HeadNodes | Set-HpcNodeState -State offline | Set-HpcNode -Role BrokerNode

    # total number of nodes in hello deployment including hello head node and compute nodes, which should match hello number specified in hello XML configuration file
        $TotalNumOfNodes = 19

        $ErrorActionPreference = 'SilentlyContinue'

    # bring nodes online when they are deployed until all nodes are online
        while ($true)
        {
          Get-HpcNode -State Offline | Set-HpcNodeState -State Online -Confirm:$false
          $OnlineNodes = @(Get-HpcNode -State Online)
          if ($OnlineNodes.Count -eq $TotalNumOfNodes)
          {
             break
          }
          sleep 60
        }
```

**Execute o script hello**

1. Abra o console do PowerShell de saudação no computador do cliente hello como um administrador.
2. Alterar pasta de scripts do diretório toohello (E:\IaaSClusterScript neste exemplo).
   
   ```
   cd E:\IaaSClusterScript
   ```
3. cluster de HPC Pack em Olá toodeploy, execute Olá comando a seguir. Este exemplo supõe que o arquivo de configuração hello está localizado em E:\HPCDemoConfig.xml.
   
   ```
   .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
   ```

Olá script de implantação do HPC Pack é executado por algum tempo. Um script de saudação coisa faz é tooexport e baixar o certificado de cluster hello e salvá-lo na pasta documentos saudação do usuário atual no computador do cliente de saudação. script Hello gera uma mensagem semelhante toohello a seguir. Em uma etapa seguinte, importe o certificado de saudação no repositório de certificado apropriado hello.    

    You have enabled REST API or web portal on HPC Pack head node. Please import hello following certificate in hello Trusted Root Certification Authorities certificate store on hello computer where you are submitting job or accessing hello HPC web portal:
    C:\Users\hpcuser\Documents\HPCWebComponent_HPCExcelHN004_20150707162011.cer

## <a name="step-2-offload-excel-workbooks-and-run-udfs-from-an-on-premises-client"></a>Etapa 2. Descarregaras pastas de trabalho do Excel e executar UDFs de um cliente local
### <a name="excel-activation"></a>Ativação do Excel
Ao usar o hello imagem VM ComputeNodeWithExcel para cargas de trabalho de produção, você deve tooprovide uma válido Microsoft Office licença chave tooactivate Excel em nós de computação de saudação. Caso contrário, versão de avaliação de saudação do Excel expira após 30 dias, e que executa pastas de trabalho do Excel apresentará Olá COMException (0x800AC472). 

É possível rearmar Excel por mais 30 dias de tempo de avaliação: faça logon no nó principal toohello e clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` no Excel todos os nós por meio do Gerenciador de Cluster de HPC de computação. É possível rearmar, no máximo, duas vezes. Depois disso, é necessário fornecer uma chave de licença válida do Office.

Olá Office Professional Plus 2013 instalado na imagem VM Olá é uma edição de volume com um genérico Volume licença GVLK (chave). Você pode ativá-la por meio do KMS (Serviço de Gerenciamento de Chaves)/da AD-BA (Ativação Baseada no Active Directory) ou de uma MAK (Chave de Ativação Múltipla). 

    * toouse AD/KMS-BA, usar um servidor KMS existente ou configure um novo usando Olá o pacote de licenças de Volume do Microsoft Office 2013. (Se você quiser, configurar Olá servidor no nó de cabeçalho hello.) Em seguida, ative a chave do host KMS Olá via Olá da Internet ou por telefone. Em seguida, clusrun `ospp.vbs` tooset Olá servidor KMS e a porta e ativar o Office em todos os nós de computação do Excel hello. 

    * toouse MAK, primeiro clusrun `ospp.vbs` tooinput Olá chave e, em seguida, ativar todos os nós de computação de Excel Olá via Olá da Internet ou por telefone. 

> [!NOTE]
> As chaves de produto de varejo do Office Professional Plus 2013 não podem ser usadas com essa imagem de VM. Se você tiver chaves válidas e mídia de instalação para as edições do Office ou do Excel diferentes desta edição de volume do Office Professional Plus 2013, será possível usá-las em seu lugar. Primeiro desinstale esta edição de volume e instalar a edição Olá que você possui. Olá reinstalado Excel do nó de computação pode ser capturado como uma toouse de imagem VM personalizada em uma implantação em escala.
> 
> 

### <a name="offload-excel-workbooks"></a>Descarregar pastas de trabalho do Excel
Siga essas toooffload etapas uma pasta de trabalho do Excel para que ele seja executado no cluster de HPC Pack Olá no Azure. toodo isso, você deve ter o Excel 2010 ou 2013 já instalado no computador do cliente de saudação.

1. Use uma das opções de saudação na etapa 1 toodeploy um cluster de HPC Pack com hello Excel imagem do nó de computação. Obter arquivo de certificado de cluster hello (. cer) e o nome de usuário de cluster e a senha.
2. No computador do cliente hello, importe o certificado de cluster de saudação em Cert: \CurrentUser\Root.
3. Verifique se o Excel está instalado. Criar um arquivo Excel.exe.config com hello seguindo o conteúdo no hello mesma pasta Excel.exe no computador do cliente de saudação. Essa etapa garante que Olá HPC Pack 2012 R2 Excel suplemento é carregado com êxito.
   
    ```
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
        </startup>
    </configuration>
    ```
4. Configure o cluster de HPC Pack Olá cliente toosubmit trabalhos toohello. Uma opção é completo de saudação toodownload [instalação HPC Pack 2012 R2 Update 3](http://www.microsoft.com/download/details.aspx?id=49922) e instalar o cliente do HPC Pack hello. Como alternativa, baixe e instale Olá [utilitários de cliente do HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923) e Olá apropriado Visual C++ 2010 redistributable do computador ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).
5. Neste exemplo, usamos uma pasta de trabalho do Excel de exemplo chamada ConvertiblePricing_Complete.xlsb. Você pode baixá-lo [aqui](https://www.microsoft.com/en-us/download/details.aspx?id=2939).
6. Copie a pasta de trabalho de tooa Olá Excel pasta de trabalho como D:\Excel\Run.
7. Abra a pasta de trabalho do Excel hello. Em Olá **desenvolver** de faixa de opções, clique em **suplementos COM** e confirme que Olá HPC Pack Excel suplemento é carregado com êxito.
   
   ![Suplemento do Excel para o HPC Pack][addin]
8. Editar saudação VBA macro HPCControlMacros no Excel alterando Olá comentários linhas conforme Olá script a seguir. Substitua os valores apropriados para o seu ambiente.
   
   ![Macro do Excel para o HPC Pack][macro]
   
   ```
   'Private Const HPC_ClusterScheduler = "HEADNODE_NAME"
   Private Const HPC_ClusterScheduler = "hpc01.eastus.cloudapp.azure.com"
   
   'Private Const HPC_NetworkShare = "\\PATH\TO\SHARE\DIRECTORY"
   Private Const HPC_DependFiles = "D:\Excel\Upload\ConvertiblePricing_Complete.xlsb=ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.Initialize ActiveWorkbook
   HPCExcelClient.Initialize ActiveWorkbook, HPC_DependFiles
   
   'HPCWorkbookPath = HPC_NetworkShare & Application.PathSeparator & ActiveWorkbook.name
   HPCWorkbookPath = "ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath
   HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath, UserName:="hpc\azureuser", Password:="<YourPassword>"
   ```
9. Copie o diretório de carregamento de tooan Olá Excel pasta de trabalho como D:\Excel\Upload. Esse diretório é especificado na constante de HPC_DependsFiles Olá em macro VBA hello.
10. pasta de trabalho do toorun Olá no cluster Olá no Azure, clique em Olá **Cluster** botão na planilha de saudação.

### <a name="run-excel-udfs"></a>Executar UDFs do Excel
toorun UDFs do Excel, siga etapas anteriores de saudação tooset de 1 a 3 no computador do cliente de saudação. Para UDFs do Excel, você não precisa aplicativo do Excel Olá toohave instalado em nós de computação. Portanto, ao criar o cluster de nós de computação, você pode escolher a imagem de um nó de computação normal, em vez da saudação computação imagem do nó com o Excel.

> [!NOTE]
> Há um limite de 34 caractere Olá Excel 2010 e 2013 caixa de diálogo de conector de cluster. Você usar esse cluster de Olá de toospecify caixa de diálogo que executa Olá UDFs. Se o nome completo do cluster de saudação é maior (por exemplo, hpcexcelhn01.southeastasia.cloudapp.azure.com), ele não se ajustar na caixa de diálogo de saudação. Olá solução alternativa é tooset uma variável de máquina, como *CCP_IAASHN* com valor de saudação do nome de cluster longo hello. Em seguida, insira *CCP_IAASHN %* na caixa de diálogo hello como o nome de nó principal do cluster hello. 
> 
> 

Depois que o cluster Olá é implantado com êxito, continue com Olá toorun as etapas a seguir internos exemplo UDF do Excel. Para UDFs personalizado do Excel, consulte estes [recursos](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild Olá XLLs e implantá-los no cluster de IaaS hello.

1. Abra uma nova pasta de trabalho do Excel. Em Olá **desenvolver** de faixa de opções, clique em **Add-Ins**. Em seguida, na caixa de diálogo hello, clique em **procurar**, navegar toohello %CCP_HOME%Bin\XLL32 pasta e selecione o exemplo hello ClusterUDF32.xll. Se hello ClusterUDF32 não existe na máquina do cliente hello, copie-o na pasta de %CCP_HOME%Bin\XLL32 Olá no nó de cabeçalho hello.
   
   ![Selecione Olá UDF][udf]
2. Clique em **Arquivo** > **Opções** > **Avançadas**. Em **fórmulas**, verifique **permitir toorun de funções XLL definidas pelo usuário em um cluster de computação**. Em seguida, clique em **opções** e insira o nome completo do cluster de saudação em **nome de nó principal do Cluster**. (Conforme observado anteriormente essa caixa de entrada é limitado too34 caracteres, para que um nome de cluster longo não caber. Você pode usar variáveis de todo o computador aqui para nomes de cluster longos.
   
   ![Configurar Olá UDF][options]
3. Olá toorun cálculo UDF no cluster hello, clique na célula de saudação com =XllGetComputerNameC() de valor e pressione Enter. função Hello simplesmente recupera o nome de saudação do nó de computação Olá no qual Olá UDF for executada. Para Olá executado pela primeira vez, uma caixa de diálogo de credenciais solicita Olá username e password tooconnect toohello cluster IaaS.
   
   ![Executar UDF][run]
   
   Quando há muitos toocalculate de células, pressione Ctrl-Shift-Alt + F9 cálculo de saudação de toorun em todas as células.

## <a name="step-3-run-a-soa-workload-from-an-on-premises-client"></a>Etapa 3. Executar uma carga de trabalho SOA a partir de um cliente local
aplicativos de SOA gerais toorun no cluster de HPC Pack IaaS Olá, primeiro use um dos métodos de Olá no cluster de saudação toodeploy etapa 1. Especifique a imagem de um nó de computação genérico nesse caso, porque você não precisa do Excel em nós de computação hello. Depois, siga estas etapas:

1. Depois de recuperar o certificado de cluster hello, importá-lo no computador do cliente de saudação em Cert: \CurrentUser\Root.
2. Instalar Olá [SDK do HPC Pack 2012 R2 Update 3](http://www.microsoft.com/download/details.aspx?id=49921) e [utilitários de cliente do HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923). Essas ferramentas permitem que você toodevelop e executam aplicativos de cliente SOA.
3. Baixar Olá HelloWorldR2 [código de exemplo](https://www.microsoft.com/download/details.aspx?id=41633). Abra Olá HelloWorldR2.sln no Visual Studio 2010 ou 2012. (Atualmente, este exemplo não é compatível com versões mais recentes do Visual Studio.)
4. Compilação do projeto EchoService Olá primeiro. Em seguida, implante o cluster de IaaS Olá serviço toohello em Olá mesma maneira como você implanta tooan local cluster. Para obter etapas detalhadas, consulte Olá Leiame no HelloWordR2. Modificar e criar hello HellWorldR2 e outros projetos, conforme descrito em Olá seguinte seção toogenerate saudação SOA aplicativos cliente que são executados em um cluster de IaaS do Azure.

### <a name="use-http-binding-with-azure-storage-queue"></a>Usar associação Http com fila de armazenamento do Azure
associação de Http toouse com uma fila de armazenamento do Azure, fazer algumas alterações de código de exemplo toohello.

* Atualize o nome do cluster hello.
  
    ```
  // Before
  const string headnode = "[headnode]";
  // After e.g.
  const string headnode = "hpc01.eastus.cloudapp.azure.com";
  or
  const string headnode = "hpc01.cloudapp.net";
  ```
* Opcionalmente, use o padrão de saudação TransportScheme em SessionStartInfo ou definir explicitamente tooHttp.

```
    info.TransportScheme = TransportScheme.Http;
```

* Use a associação padrão para Olá BrokerClient.
  
    ```
  // Before
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session, binding))
  // After
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session))
  ```
  
    Ou defina explicitamente usando Olá basicHttpBinding.
  
    ```
  BasicHttpBinding binding = new BasicHttpBinding(BasicHttpSecurityMode.TransportWithMessageCredential);
  binding.Security.Message.ClientCredentialType = BasicHttpMessageCredentialType.UserName;    binding.Security.Transport.ClientCredentialType = HttpClientCredentialType.None;
  ```
* Opcionalmente, defina Olá UseAzureQueue sinalizador tootrue em SessionStartInfo. Se não for definido, será definido tootrue por padrão quando o nome de cluster Olá tem sufixos de domínio do Azure e Olá TransportScheme é Http.
  
    ```
    info.UseAzureQueue = true;
  ```

### <a name="use-http-binding-without-azure-storage-queue"></a>Usar associação Http sem fila de armazenamento do Azure
associação de Http toouse sem uma fila de armazenamento do Azure, explicitamente conjunto Olá UseAzureQueue sinalizador toofalse no hello SessionStartInfo.

```
    info.UseAzureQueue = false;
```

### <a name="use-nettcp-binding"></a>Usar associação NetTcp
toouse NetTcp associação, configuração de saudação é semelhante cluster do tooconnecting tooan local. Você precisa de alguns pontos de extremidade na VM do nó principal Olá tooopen. Se você usou o cluster de Olá Olá HPC Pack IaaS implantação script toocreate, por exemplo, definir pontos de extremidade de saudação em Olá portal do Azure da seguinte maneira.

1. Pare Olá VM.
2. Adicionar as portas TCP Olá 9090, 9087, 9091, 9094 de sessão, de saudação do agente, agente de trabalho e serviços de dados, respectivamente
   
    ![Configurar pontos de extremidade][endpoint-new-portal]
3. Inicie Olá VM.

Olá aplicativo de cliente SOA não requer alterações exceto alterando o nome completo do cluster de IaaS de toohello do hello nome principal.

## <a name="next-steps"></a>Próximas etapas
* Consulte [estes recursos](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) para saber mais sobre como executar cargas de trabalho do Excel com o HPC Pack.
* Consulte [Gerenciamento de serviços SOA no Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) para saber mais sobre como implantar e gerenciar serviços SOA com HPC Pack.

<!--Image references-->
[scenario]: ./media/excel-cluster-hpcpack/scenario.png
[github]: ./media/excel-cluster-hpcpack/github.png
[template]: ./media/excel-cluster-hpcpack/template.png
[parameters]: ./media/excel-cluster-hpcpack/parameters.png
[parameters-new-portal]: ./media/excel-cluster-hpcpack/parameters-new-portal.png
[create]: ./media/excel-cluster-hpcpack/create.png
[connect]: ./media/excel-cluster-hpcpack/connect.png
[cert]: ./media/excel-cluster-hpcpack/cert.png
[addin]: ./media/excel-cluster-hpcpack/addin.png
[macro]: ./media/excel-cluster-hpcpack/macro.png
[options]: ./media/excel-cluster-hpcpack/options.png
[run]: ./media/excel-cluster-hpcpack/run.png
[endpoint]: ./media/excel-cluster-hpcpack/endpoint.png
[endpoint-new-portal]: ./media/excel-cluster-hpcpack/endpoint-new-portal.png
[udf]: ./media/excel-cluster-hpcpack/udf.png
