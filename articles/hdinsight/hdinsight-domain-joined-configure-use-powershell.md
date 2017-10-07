---
title: "aaaConfigure clusters de HDInsight ingressado no domínio usando o PowerShell - Azure | Microsoft Docs"
description: "Saiba como tooset e configurar os clusters de HDInsight ingressado no domínio usando o PowerShell do Azure"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: a13b2f7a-612d-4800-bc92-7fc0524f3e89
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/02/2016
ms.author: saurinsh
ms.openlocfilehash: 49da3439513d1e51171f0f7f7f9c3d967d55cb7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-domain-joined-hdinsight-clusters-preview-using-azure-powershell"></a>Configurar clusters HDInsight ingressados no domínio (visualização) usando o Azure PowerShell
Saiba como tooset backup um Azure HDInsight cluster com o Azure Active Directory (AD do Azure) e [Apache Ranger](http://hortonworks.com/apache/ranger/) usando o PowerShell do Azure. Um script do PowerShell do Azure é fornecido a configuração de saudação toomake mais rápida e menos propenso a erros. O HDInsight ingressado em domínio só pode ser configurado em clusters baseados em Linux. Para obter mais informações, consulte [Introduzir clusters HDInsight ingressados no domínio](hdinsight-domain-joined-introduction.md).

> [!IMPORTANT]
> O Oozie não está habilitado no HDInsight ingressado no domínio.

Uma configuração típica de cluster HDInsight domínio envolve Olá etapas a seguir:

1. Crie uma VNet clássica do Azure para o Azure AD.  
2. Crie e configure o Azure AD e o Azure AD DS.
3. Adicionar uma VM toohello clássico VNet para criar a unidade organizacional. 
4. Crie uma unidade organizacional para o Azure AD DS.
5. Crie uma VNet de HDInsight no modo de gerenciamento de recursos do Azure hello.
6. Configure zonas de DNS reverso de saudação do Azure AD DS.
7. Par Olá duas VNets.
8. Crie um cluster HDInsight.

Olá script do PowerShell fornecido executa as etapas 3 a 7. Você deve percorrer as etapas 1 e 2 manualmente.  Se você preferir não toouse PowerShell do Azure, consulte [clusters HDInsight configurar domínio](hdinsight-domain-joined-configure.md). 

Um exemplo de topologia de saudação final será semelhante ao seguinte:

![Topologia de HDInsight ingressado no domínio](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-topology.png)

Já que o Azure AD dá suporte atualmente apenas a VNets (redes virtuais) clássicas e os clusters HDInsight baseados em Linux dão suporte apenas a VNets com base no Azure Resource Manager, a integração do Azure AD do HDInsight requer duas VNets e um emparelhamento entre elas. Para informações de comparação de saudação entre modelos de implantação de saudação dois, consulte [do Azure Resource Manager versus implantação clássica: entender os modelos de implantação e Olá estado de seus recursos](../azure-resource-manager/resource-manager-deployment-model.md). Olá duas VNets deve estar no hello mesma região hello Azure AD DS.

> [!NOTE]
> Este tutorial presume que você não tenha um Azure AD. Se você tiver um, você pode ignorar a parte Olá na etapa 2.
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
Você deve ter Olá toogo itens com este tutorial a seguir:

* Familiarize-se com o [Azure AD Domain Services](https://azure.microsoft.com/services/active-directory-ds/) e sua estrutura de [preços](https://azure.microsoft.com/pricing/details/active-directory-ds/).
* Certifique-se de que sua assinatura está na lista de permissões para essa visualização pública. Você pode fazer isso enviando um email toohdipreview@microsoft.com com sua ID de assinatura.
* Um certificado SSL assinado por uma autoridade de autenticação para seu domínio. Olá certificado é necessário ao configurar o LDAP seguro. Os certificados autoassinados não podem ser usados.
* PowerShell do Azure.  Confira [Instalar e configurar o Azure PowerShell](/powershell/azure/overview).

## <a name="create-an-azure-classic-vnet-for-your-azure-ad"></a>Crie uma VNet clássica do Azure para o Azure AD.
Para obter instruções hello, consulte [aqui](hdinsight-domain-joined-configure.md#create-an-azure-virtual-network-classic).

## <a name="create-and-configure-azure-ad-and-azure-ad-ds"></a>Crie e configure o Azure AD e o Azure AD DS.
Para obter instruções hello, consulte [aqui](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).

## <a name="run-hello-powershell-script"></a>Executar script do PowerShell Olá
saudação de script do PowerShell pode ser baixada do [GitHub](https://github.com/hdinsight/DomainJoinedHDInsight). Extrair o arquivo zip de saudação e salvar arquivos Olá localmente.

**Olá tooedit script do PowerShell**

1. Abra run.ps1 usando o ISE do Windows PowerShell ou outro editor de texto.
2. Preencha valores Olá Olá variáveis a seguir:
   
   * **$SubscriptionName** – hello nome da saudação assinatura do Azure onde deseja toocreate seu cluster HDInsight. Você já criou uma rede virtual clássica nesta assinatura e criará uma rede virtual do Gerenciador de recursos do Azure para cluster de HDInsight Olá na assinatura.
   * **$ClassicVNetName** -Olá clássico rede virtual que contém a saudação do Azure AD DS. Esta rede virtual deve estar no hello mesma assinatura que é fornecida acima. Esta rede virtual deve ser criada usando Olá portal do Azure e não usando o portal clássico. Se você seguir as instruções de saudação da [clusters de HDInsight configurar domínio (visualização)](hdinsight-domain-joined-configure.md#create-an-azure-virtual-network-classic), Olá padrão é contosoaadvnet.
   * **$ClassicResourceGroupName** – nome do grupo de Gerenciador de recursos de saudação para Olá clássico rede virtual que é mencionado acima. Por exemplo, contosoaadrg. 
   * **$ArmResourceGroupName** – nome do grupo de recursos hello dentro da qual, toocreate Olá pelo cluster HDInsight. Você pode usar o hello mesmo grupo de recursos $ArmResourceGroupName.  Se o grupo de recursos de saudação não existir, o script de Olá cria o grupo de recursos hello.
   * **$ArmVNetName** -nome de rede virtual do Gerenciador de recursos hello dentro da qual você deseja que o cluster de HDInsight toocreate hello. Essa rede virtual será colocada em $ArmResourceGroupName.  Se não existir Olá VNet, Olá script do PowerShell o criará. Se ele existir, ele deve ser parte saudação do grupo de recursos que você fornecer acima.
   * **$AddressVnetAddressSpace** – hello espaço de endereço de rede virtual do Gerenciador de recursos de saudação de rede. Verifique se esse espaço de endereço está disponível. Este espaço de endereço não pode sobrepor o espaço de endereço Olá clássico da rede virtual. Por exemplo, “10.1.0.0/16”
   * **$ArmVnetSubnetName** -nome da sub-rede Olá Gerenciador de recursos rede virtual dentro da qual você deseja que o cluster do HDInsight tooplace Olá VMs. Se não existir, sub-rede Olá Olá script do PowerShell criará. Se ele existir, ele deve ser parte da saudação rede virtual que você fornecer acima.
   * **$AddressSubnetAddressSpace** – hello intervalo de endereços de sub-rede da rede virtual Olá Gerenciador de recursos de rede. Olá cluster HDInsight endereços IP da VM será desse intervalo de endereço de sub-rede. Por exemplo, “10.1.0.0/24”.
   * **$ActiveDirectoryDomainName** – nome de domínio de saudação do AD do Azure que você deseja toojoin Olá HDInsight as VMs do cluster. Por exemplo, “contoso.onmicrosoft.com”
   * **$ClusterUsersGroups** – nome comum de Olá Olá de grupos de segurança do AD do que você deseja que o cluster do HDInsight toohello toosync. usuários Hello dentro deste grupo de segurança será capaz de toolog no painel de controle do cluster toohello usando suas credenciais de domínio do active directory. Esses grupos de segurança devem existir no active directory de saudação. Por exemplo, "hiveusers" ou "clusteroperatorusers".
   * **$OrganizationalUnitName** -a unidade organizacional Olá no domínio hello, dentro do qual você deseja cluster do HDInsight tooplace Olá VMs e Olá entidades de serviço usadas pelo cluster hello. saudação de script do PowerShell criará essa UO se ele não existe. Por exemplo, "HDInsightOU".
3. Salve alterações de saudação.

**script de saudação toorun**

1. Execute o **Windows PowerShell** como Administrador.
2. Procure pasta toohello de run.ps1. 
3. Execute o script hello digitando o nome do arquivo hello e pressione **ENTER**.  Três diálogos de entrada aparecem:
   
   1. **Entrar no portal clássico tooAzure** – Insira suas credenciais que você usar toosign no portal clássico do tooAzure. Você deve ter criado Olá AD do Azure e o Azure AD DS usando essas credenciais.
   2. **Entrar no portal do Gerenciador de recursos de tooAzure** – Insira suas credenciais que você usar toosign no portal do Gerenciador de recursos de tooAzure.
   3. **Nome de usuário de domínio** – insira credenciais Olá Olá domínio do nome de usuário que você deseja toobe um administrador no cluster do HDInsight hello. Se você criou um Azure AD do zero, deve ter criado o usuário com esta documentação. 
      
      > [!IMPORTANT]
      > Insira o nome de usuário de saudação neste formato: 
      > 
      > Nomededomínio\nomedeusuário (por exemplo, contoso.onmicrosoft.com\clusteradmin)
      > 
      > 
      
      Esse usuário deve ter privilégios de 3: toojoin máquinas toohello fornecido o domínio do Active Directory; entidades de serviço toocreate e objetos de computador no hello fornecida uma unidade organizacional. e regras de proxy DNS reversas tooadd.

Ao criar zonas DNS reversas, script hello solicitará que você tooenter uma identificação de rede. Essa ID de rede deve ser um prefixo de endereço da rede virtual Gerenciador de recursos hello. Por exemplo, se seu espaço de endereço de sub-rede de rede virtual do Gerenciador de recursos for 10.2.0.0/24, insira 10.2.0.0/24 quando a ferramenta Olá solicita Olá ID de rede. 

## <a name="create-hdinsight-cluster"></a>Criar cluster HDInsight
Nesta seção, criar um cluster baseado em Linux Hadoop no HDInsight usando o portal do Azure Olá ou [modelo do Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). Para outros métodos de criação de cluster e Noções básicas sobre configurações de hello, consulte [HDInsight criar clusters](hdinsight-hadoop-provision-linux-clusters.md). Para obter mais informações sobre como usar o Gerenciador de recursos modelo toocreate Hadoop clusters de HDInsight, consulte [Hadoop criar clusters de HDInsight usando modelos do Gerenciador de recursos](hdinsight-hadoop-create-windows-clusters-arm-templates.md)

**toocreate um cluster HDInsight ingressado no domínio usando Olá portal do Azure**

1. Logon toohello [portal do Azure](https://portal.azure.com).
2. Clique em **Novo**, **Inteligência + análise** e então em **HDInsight**.
3. De saudação **cluster HDInsight novo** folha, insira ou selecione Olá valores a seguir:
   
   * **Nome do cluster**: digite um novo nome de cluster para cluster de HDInsight domínio hello.
   * **Assinatura**: selecione uma assinatura do Azure usada para criar esse cluster.
   * **Configuração do cluster**:
     
     * **Tipo de cluster**: Hadoop. Atualmente, apenas clusters Hadoop dão suporte ao HDInsight ingressado no domínio.
     * **Sistema Operacional**: Linux.  Apenas clusters HDInsight baseados em Linux dão suporte ao HDInsight ingressado no domínio.
     * **Versão**: Hadoop 2.7.3 (HDI 3.5). Somente a versão 3.5 de cluster HDInsight dá suporte ao HDInsight ingressado no domínio.
     * **Tipo de cluster**: PREMIUM
       
       Clique em **selecione** toosave alterações de saudação.
   * **Credenciais**: configurar credenciais Olá Olá cluster e de usuário usuário SSH hello.
   * **Fonte de dados**: criar uma nova conta de armazenamento ou usar uma conta de armazenamento existente como Olá conta de armazenamento padrão para o cluster do HDInsight hello. local de saudação deve Olá mesmas Olá duas VNets.  Olá local é também saudação do cluster do HDInsight hello.
   * **Preços**: selecione Olá número de nós de trabalho do cluster.
   * **Configurações avançadas**: 
     
     * **Ingresso no domínio e Sub-rede/VNet**: 
       
       * **Configurações de domínio**: 
         
         * **Nome de domínio**: contoso.onmicrosoft.com
         * **Nome de usuário de domínio**: insira um nome de usuário de domínio. Esse domínio deve ter Olá seguintes privilégios: ingressar máquinas toohello domínio e colocá-los na unidade de organização Olá configurados anteriormente; Criar entidades de serviço na unidade de organização Olá configurados anteriormente; Crie entradas de DNS reverso. Este usuário de domínio se tornará administrador Olá desse cluster HDInsight ingressado no domínio.
         * **Senha do domínio**: insira a senha de usuário de domínio hello.
         * **Unidade de organização**: digite nome distinto de saudação do hello UO que você configurou anteriormente. Por exemplo: OU=HDInsightOU,DC=contoso,DC=onmicrosoft,DC=com
         * **URL LDAPS**: ldaps://contoso.onmicrosoft.com:636
         * **Grupo de usuários de acesso**: especifique o grupo de segurança de saudação cujos usuários que você quer toosync toohello cluster. Por exemplo, HiveUsers.
           
           Clique em **selecione** toosave alterações de saudação.
           
           ![Configuração de domínio para configurar o portal do HDInsight ingressado no domínio](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-portal-domain-setting.png)
       * **Rede virtual**: contosohdivnet
       * **Subrede**: Subnet1
         
         Clique em **selecione** toosave alterações de saudação.        
         Clique em **selecione** toosave alterações de saudação.
   * **Grupo de recursos**: grupo de recursos de saudação selecione usado para Olá HDInsight VNet (contosohdirg).
4. Clique em **Criar**.  

Outra opção para criar o cluster HDInsight ingressado no domínio é toouse modelo de gerenciamento de recursos do Azure. Olá procedimento a seguir mostra como:

**toocreate um cluster HDInsight ingressado no domínio usando um modelo de gerenciamento de recursos**

1. Clique em Olá imagem tooopen um modelo do Gerenciador de recursos no portal do Azure de saudação a seguir. modelo do Gerenciador de recursos de saudação está localizado em um contêiner de blob público. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-domain-joined-hdinsight-cluster.json" target="_blank"><img src="./media/hdinsight-domain-joined-configure-use-powershell/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. De saudação **parâmetros** folha, digite Olá valores a seguir:
   
   * **Assinatura**: (Selecione sua assinatura do Azure).
   * **Grupo de recursos**: clique em **usar existente**e especifique Olá mesmo grupo de recursos que você usou.  Por exemplo, contosohdirg. 
   * **Localização**: especifique uma localização para o grupo de recursos.
   * **Nome do cluster**: insira um nome para o cluster de Hadoop Olá que você criará. Por exemplo, contosohdicluster.
   * **Tipo de Cluster**: selecione um tipo de cluster.  valor padrão de saudação é **hadoop**.
   * **Local**: selecione um local para o cluster de saudação.  conta de armazenamento de padrão de saudação usa Olá mesmo local.
   * **Contagem de nós de trabalho de cluster**: selecione Olá número de nós de trabalho.
   * **Nome de logon e senha do cluster**: nome de logon padrão Olá é **admin**.
   * **SSH username e password**: nome de usuário saudação padrão é **sshuser**.  Você pode renomeá-lo. 
   * **ID da Rede Virtual**: /subscriptions/&lt;SubscriptionID>/resourceGroups/&lt;ResourceGroupName>/providers/Microsoft.Network/virtualNetworks/&lt;VNetName>
   * **Sub-rede da Rede Virtual**: /subscriptions/&lt;SubscriptionID>/resourceGroups/&lt;ResourceGroupName>/providers/Microsoft.Network/virtualNetworks/&lt;VNetName>/subnets/Subnet1
   * **Nome de Domínio**: contoso.onmicrosoft.com
   * **DN da Unidade Organizacional**: OU=HDInsightOU,DC=contoso,DC=onmicrosoft,DC=com
   * **DNs do Grupo de Usuários do Cluster**: "\"CN=HiveUsers,OU=AADDC Users,DC=<DomainName>,DC=onmicrosoft,DC=com\""
   * **LDAPUrls**: ["ldaps://contoso.onmicrosoft.com:636"]
   * **DomainAdminUserName**: (nome de usuário do Enter Olá domínio admin)
   * **DomainAdminPassword**: (Insira a senha de usuário do administrador de domínio Olá)
   * **Eu concordo toohello termos e condições acima**: (Verificar)
   * **PIN toodashboard**: (Verificar)
3. Clique em **Comprar**. Você verá um novo bloco intitulado **Implantando a implantação de modelo**. Demora cerca de aproximadamente 20 minutos toocreate um cluster. Depois de criar o cluster hello, você pode clicar em folha de cluster Olá em tooopen portal Olá-lo.

Depois de concluir o tutorial hello, talvez você queira toodelete cluster de saudação. Com o HDInsight, seus dados são armazenados no Armazenamento do Azure, assim você poderá excluir, com segurança, um cluster quando ele não estiver em uso. Você também é cobrado por um cluster HDInsight, mesmo quando ele não está em uso. Como encargos Olá para cluster Olá são muitas vezes mais do que encargos Olá para armazenamento, faz sentido, financeiramente falando toodelete clusters quando eles não estiverem em uso. Para obter instruções de saudação da exclusão de um cluster, consulte [clusters gerenciar Hadoop em HDInsight usando Olá portal do Azure](hdinsight-administer-use-management-portal.md#delete-clusters).

## <a name="next-steps"></a>Próximas etapas

* Para configurar políticas do Hive e executar consultas do Hive, confira [Configurar políticas do Hive para clusters HDInsight associados ao domínio](hdinsight-domain-joined-run-hive.md).
* Para usar clusters de HDInsight tooDomain associado do SSH tooconnect, consulte [usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).

