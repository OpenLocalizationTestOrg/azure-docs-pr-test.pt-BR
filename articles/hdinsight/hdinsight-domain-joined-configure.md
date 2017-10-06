---
title: "clusters de HDInsight domínio aaaConfigure - Azure | Microsoft Docs"
description: "Saiba como tooset e configurar clusters HDInsight ingressado no domínio"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 0cbb49cc-0de1-4a1a-b658-99897caf827c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/02/2016
ms.author: saurinsh
ms.openlocfilehash: 8c4b3d269a7662d27a49b839e5cd05a3e24f7023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-domain-joined-hdinsight-clusters-preview"></a>Configurar clusters HDInsight ingressados no domínio (Preview)

Saiba como tooset backup um Azure HDInsight cluster com o Azure Active Directory (AD do Azure) e [Apache Ranger](http://hortonworks.com/apache/ranger/) tootake proveito das políticas RBAC (controle) de acesso baseado em função avançado e autenticação forte.  O HDInsight ingressado em domínio só pode ser configurado em clusters baseados em Linux. Para obter mais informações, consulte [Introduzir clusters HDInsight ingressados no domínio](hdinsight-domain-joined-introduction.md).

> [!IMPORTANT]
> O Oozie não está habilitado no HDInsight ingressado no domínio.

Este artigo é o primeiro tutorial saudação de uma série:

* Crie um tooAzure de cluster conectado HDInsight AD (por meio do recurso de serviços de domínio do diretório do Azure Olá) com Apache Ranger habilitado.
* Criar e aplicar políticas de Hive por meio do Apache Ranger e permitir que os usuários (por exemplo, os cientistas de dados) tooHive tooconnect usando ferramentas baseadas em ODBC, por exemplo, Excel, Tableau etc. A Microsoft está trabalhando na adição de outras cargas de trabalho, como HBase, Spark e tempestade, unidas tooDomain HDInsight em breve.

Um exemplo de topologia de saudação final será semelhante ao seguinte:

![Topologia de HDInsight ingressado no domínio](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-topology.png)

Já que o Azure AD dá suporte atualmente apenas a VNets (redes virtuais) clássicas e os clusters HDInsight baseados em Linux dão suporte apenas a VNets com base no Azure Resource Manager, a integração do Azure AD do HDInsight requer duas VNets e um emparelhamento entre elas. Para informações de comparação de saudação entre modelos de implantação de saudação dois, consulte [do Azure Resource Manager versus implantação clássica: entender os modelos de implantação e Olá estado de seus recursos](../azure-resource-manager/resource-manager-deployment-model.md). Olá duas VNets deve estar no hello mesma região hello Azure AD DS.

Nomes de serviço do Azure devem ser globalmente exclusivos. Olá nomes a seguir é usada neste tutorial. Contoso é um nome fictício. Você deve substituir *contoso* com um nome diferente ao percorrer o tutorial hello. 

**Nomes:**

| Propriedade | Valor |
| --- | --- |
| VNet do Azure AD |contosoaadvnet |
| Grupo de recursos de VNet do Azure AD |contosoaadrg |
| Diretório do AD do Azure |contosoaaddirectory |
| Nome de domínio do Azure AD |contoso (contoso.onmicrosoft.com) |
| VNet HDInsight |contosohdivnet |
| Grupo de recursos de VNet HDInsight |contosohdirg |
| Cluster HDInsight |contosohdicluster |

Este tutorial fornece as etapas de saudação para configurar um cluster HDInsight ingressado no domínio. Cada seção tem artigos de tooother links com mais informações em segundo plano.

## <a name="prerequisite"></a>Pré-requisito:
* Familiarize-se com o [Azure AD Domain Services](https://azure.microsoft.com/services/active-directory-ds/) e sua estrutura de [preços](https://azure.microsoft.com/pricing/details/active-directory-ds/).
* Certifique-se de que sua assinatura está na lista de permissões para essa visualização pública. Você pode fazer isso enviando um email toohdipreview@microsoft.com com sua ID de assinatura.
* Um certificado SSL assinado por uma autoridade de autenticação para seu domínio. Olá certificado é necessário ao configurar o LDAP seguro. Os certificados autoassinados não podem ser usados.

## <a name="procedures"></a>Procedimentos
1. Crie uma VNet clássica do Azure para o Azure AD.  
2. Crie e configure o Azure AD e o Azure AD DS.
3. Crie uma VNet de HDInsight no modo de gerenciamento de recursos do Azure hello.
4. Par Olá duas VNets.
5. Crie um cluster HDInsight.

> [!NOTE]
> Este tutorial presume que você não tenha um Azure AD. Se você tiver um, você pode ignorar a parte Olá na etapa 2.
> 
> 

Há um script do PowerShell que automatiza as etapas 3 a 7.  Para obter mais informações, consulte [Configurar clusters HDInsight ingressados em domínio usando o Azure PowerShell](hdinsight-domain-joined-configure-use-powershell.md).

## <a name="create-an-azure-virtual-network-classic"></a>Criar uma rede virtual (clássica) do Azure
Nesta seção, você deve criar uma rede virtual (clássica) usando Olá portal do Azure. Na próxima seção, Olá, você habilita hello Azure AD DS para AD do Azure na rede virtual hello. Para obter mais informações sobre Olá seguindo o procedimento e usando outros métodos de criação de rede virtual, consulte [criar uma rede virtual (clássico) usando o portal do Azure de saudação](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).

**toocreate uma rede virtual clássica**

1. Logon toohello [portal do Azure](https://portal.azure.com). 
2. Clique em **Nova** > **Rede** > **Rede Virtual**.
3. Em **Selecionar um modelo de implantação**, selecione **Clássico** e, em seguida, clique em **Criar**.
4. Insira ou selecione Olá valores a seguir:
   
   * **Nome**: contosoaadvnet
   * **Espaço de endereço**: 10.1.0.0/16
   * **Nome da sub-rede**: Subnet1
   * **Intervalo de endereços da sub-rede**: 10.1.0.0/24
   * **Assinatura**: (Selecione uma assinatura usada para criar esta VNet.)
   * **ResourceGroup**: contosoaadrg
   * **Localização**: (Selecione uma região para seu cluster HDInsight.)
     
     > [!IMPORTANT]
     > Você deve escolher uma localização que dê suporte ao Azure AD DS. Para obter mais informações, veja [Produtos disponíveis por região](https://azure.microsoft.com/en-us/regions/services/). 
     > 
     > Ambos Olá VNet clássico e hello VNet do grupo de recursos deve estar no hello mesma região hello Azure AD DS.
     > 
     > 
5. Clique em **criar** toocreate Olá VNet.

## <a name="create-and-configure-azure-ad-ds-for-your-azure-ad"></a>Criar e configurar o Azure AD DS para o Azure AD
Nesta seção, você irá:

1. Criar um Azure AD.
2. Criar usuários do Azure AD. Esses usuários são usuários do domínio. Use o primeiro usuário de saudação para configurar o cluster do HDInsight Olá com hello AD do Azure.  Olá outros dois usuários são opcionais para este tutorial. Eles serão usados em [Configurar políticas Hive para clusters HDInsight ingressados no domínio](hdinsight-domain-joined-run-hive.md), quando você configurar políticas do Apache Ranger.
3. Criar grupo de administradores de controlador de domínio do AAD hello e adicionar grupo de toohello de usuários de AD do Azure hello. Você usar essa unidade organizacional do usuário toocreate hello.
4. Habilite serviços de domínio do Azure AD (Azure AD DS) para Olá AD do Azure.
5. Configure LDAPS para Olá AD do Azure. Olá LDAP Lightweight Directory Access Protocol () é usado tooread de e escrever tooAzure AD.

Se você preferir toouse um existente do AD do Azure, você pode ignorar as etapas 1 e 2.

**toocreate um AD do Azure**

1. De saudação [portal clássico do Azure](https://manage.windowsazure.com), clique em **novo** > **serviços de aplicativos** > **do Active Directory**  >  **Diretório** > **criação personalizada**. 
2. Insira ou selecione Olá valores a seguir:
   
   * **Nome**: contosoaaddirectory
   * **Nome de domínio**: contoso.  Esse nome deve ser globalmente exclusivo.
   * **País ou região**: selecione seu país ou região.
3. Clique em **Concluído**.

**Criar um usuário do Azure AD**

1. De saudação [portal clássico do Azure](https://manage.windowsazure.com), clique em **do Active Directory** -> **contosoaaddirectory**. 
2. Clique em **usuários** no menu superior hello.
3. Clique em **Adicionar Usuário**.
4. Insira o **Nome de Usuário** e, em seguida, clique em **Próximo**. 
5. Configure o perfil do usuário; em **Função**, selecione **Administrador Global** e, em seguida, clique em **Próximo**.  função de Administrador Global de saudação é unidades organizacionais toocreate necessários.
6. Clique em **criar** tooget uma senha temporária.
7. Faça uma cópia da senha hello e, em seguida, clique em **concluir**. Posteriormente neste tutorial, você usará este cluster do HDInsight administrador global usuário toocreate hello.

Siga Olá dois usuários mais toocreate do mesmo procedimento com hello **usuário** função, hiveuser1 e hiveuser2. Olá usuários a seguir serão usados na [Hive configurar políticas para clusters de HDInsight domínio](hdinsight-domain-joined-run-hive.md).

**toocreate Olá grupo Administradores de DC AAD e adicionar um usuário do AD do Azure**

1. De saudação [portal clássico do Azure](https://manage.windowsazure.com), clique em **do Active Directory** > **contosoaaddirectory**. 
2. Clique em **grupos** no menu superior hello.
3. Clique em **Adicionar um Grupo** ou **Adicionar Grupo**.
4. Insira ou selecione Olá valores a seguir:
   
   * **Nome**: Administradores do AAD DC.  Não altere o nome do grupo de saudação.
   * **Tipo de Grupo**: segurança.
5. Clique em **Concluído**.
6. Clique em **AAD DC administradores** tooopen grupo de saudação.
7. Clique em **Adicionar Membros**.
8. Selecione primeiro usuário de saudação criado na etapa anterior hello e, em seguida, clique em **concluir**.
9. Olá repetição mesmo toocreate de etapas outro grupo chamado **HiveUsers**, e adicione Olá dois Hive usuários toohello grupo.

Para obter mais informações, consulte [serviços de domínio do AD do Azure (visualização) - criar hello 'Administradores de controlador de domínio do AAD' grupo](../active-directory-domain-services/active-directory-ds-getting-started.md).

**tooenable do Azure AD DS para AD do Azure**

1. De saudação [portal clássico do Azure](https://manage.windowsazure.com), clique em **do Active Directory** > **contosoaaddirectory**. 
2. Clique em **configurar** no menu superior hello.
3. Role para baixo demais**dos serviços de domínio**, e a saudação do conjunto de valores a seguir:
   
   * **Habilitar os serviços de domínio para este diretório**: sim.
   * **Nome de domínio DNS dos serviços de domínio**: isso mostra o nome DNS de padrão de saudação do hello directory do Azure. Por exemplo, contoso.onmicrosoft.com.
   * **Conectar a rede virtual do domínio serviços toothis**: selecione Olá clássico rede virtual que você criou anteriormente, ou seja, **contosoaadvnet**.
4. Clique em **salvar** Olá página de baixo hello. Você verá **pendentes...**  Avançar muito**habilitar serviços de domínio para este diretório**.  
5. Aguarde até que **Pendente...** desapareça e o campo **Endereço IP** seja populado. Dois endereços IP serão populados. Esses são endereços IP Olá Olá de controladores de domínio provisionados pelos serviços de domínio. Cada endereço IP será visível depois que o controlador de domínio correspondente Olá é provisionada e pronta. Anote os dois endereços IP hello. Você precisará delas mais tarde.

Para obter mais informações, veja [Azure AD Domain Services (Preview) – Habilitar o Azure AD Domain Services](../active-directory-domain-services/active-directory-ds-getting-started-enableaadds.md).

**senha toosynchronize**

Se você usar seu próprio domínio, senha de saudação do toosynchronize é necessária. Consulte [habilitar serviços de domínio de tooAzure AD de sincronização de senha para um Azure somente em nuvem diretório AD](../active-directory-domain-services/active-directory-ds-getting-started-password-sync.md).

**tooconfigure LDAPS para Olá AD do Azure**

1. Obtenha um certificado SSL assinado por uma autoridade de autenticação para seu domínio. Se você quiser toouse um certificado autoassinado, entre em contato toohdipreview@microsoft.com para uma exceção.
2. De saudação [portal clássico do Azure](https://manage.windowsazure.com), clique em **do Active Directory** > **contosoaaddirectory**. 
3. Clique em **configurar** no menu superior hello.
4. Role muito**dos serviços de domínio**.
5. Clique em **Configurar certificado**.
6. Execute o arquivo de certificado do hello instrução toospecify hello e a senha de saudação. Você verá **pendentes...**  Avançar muito**habilitar serviços de domínio para este diretório**.  
7. Aguarde até que **Pendente...** desapareça e que **Certificado LDAP Seguro** seja populado.  Isso pode levar 10 minutos ou mais.

> [!NOTE]
> Se algumas tarefas em segundo plano estão sendo executadas em hello Azure AD DS, você verá um erro ao carregar certificado - <i>há uma operação que está sendo executada para este locatário. Tente novamente mais tarde</i>.  Caso esse erro ocorra, tente novamente após algum tempo. Olá que segundo IP do controlador de domínio pode levar até too3 horas toobe provisionado.
> 
> 

Para obter mais informações, veja [Configurar o LDAPS (LDAP Seguro) para um domínio gerenciado do Azure AD Domain Services](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md).

## <a name="create-a-resource-manager-vnet-for-hdinsight-cluster"></a>Criar uma VNet do Resource Manager para o cluster HDInsight
Nesta seção, você criará uma VNet Gerenciador de recursos do Azure que será usado para o cluster do HDInsight hello. Para obter mais informações sobre como criar VNET do Azure usando outros métodos, veja [Criar uma rede virtual](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)

Depois de criar hello VNet, você irá configurar Olá toouse do Gerenciador de recursos de VNet Olá mesmo servidores DNS como Olá rede virtual do Azure AD. Se você seguiu as etapas neste tutorial toocreate Olá Olá clássico VNet e hello AD do Azure, os servidores DNS Olá são 10.1.0.4 e 10.1.0.5.

**toocreate VNet um Gerenciador de recursos**

1. Logon toohello [portal do Azure](https://portal.azure.com).
2. Clique em **Nova**, **Rede**, **Rede virtual**. 
3. Em **Selecionar um modelo de implantação**, selecione **Resource Manager** e clique em **Criar**.
4. Digite ou selecione Olá valores a seguir:
   
   * **Nome**: contosohdivnet
   * **Espaço de endereço**: 10.2.0.0/16. Verifique se o intervalo de endereços de saudação não pode se sobrepor com intervalo de endereços IP de saudação do hello VNet clássico.
   * **Nome da sub-rede**: Subnet1
   * **Intervalo de endereços da sub-rede**: 10.2.0.0/24
   * **Assinatura**: (Selecione sua assinatura do Azure.)
   * **Grupo de recursos**: contosohdirg
   * **Local**: (selecione Olá mesmo local como Olá rede virtual do Azure AD, ou seja, contosoaadvnet.)
5. Clique em **Criar**.

**tooconfigure DNS para Olá Gerenciador de recursos de VNet**

1. De saudação [portal do Azure](https://portal.azure.com), clique em **mais serviços** -> **redes virtuais**. Certifique-se de não tooclick **redes virtuais (clássico)**.
2. Clique em **contosohdivnet**.
3. Clique em **servidores DNS** de saudação lado esquerdo da folha nova hello.
4. Clique em **personalizado**e, em seguida, digite Olá valores a seguir:
   
   * 10.1.0.4
   * 10.1.0.5
     
     Esses endereços IP do servidor DNS devem corresponder toohello servidores DNS Olá rede virtual do AD do Azure (VNet clássico).
5. Clique em **Salvar**.

## <a name="peer-hello-azure-ad-vnet-and-hello-hdinsight-vnet"></a>Par Olá rede virtual do Azure AD e Olá HDInsight VNet
**toopeer Olá duas redes**

1. Logon toohello [portal do Azure](https://portal.azure.com).
2. Clique em **mais serviços** no menu esquerdo hello.
3. Clique em **Redes Virtuais**. Não clique em **Redes virtuais (clássicas)**.
4. Clique em **contosohdivnet**.  Isso é hello HDInsight VNet.
5. Clique em **emparelhamentos** no menu esquerdo de saudação da folha de saudação.
6. Clique em **adicionar** no menu superior hello. Ele abre Olá **adicionar emparelhamento** folha.
7. Em Olá **adicionar emparelhamento** folha, Olá definido ou selecione os valores a seguir:
   
   * **Nome**: ContosoAADHDIVNetPeering
   * **Modelo de implantação de rede virtual**: clássico
   * **Assinatura**: selecione o nome da sua assinatura usada para a rede virtual do hello clássico (do Azure AD).
   * **Rede virtual**: contosoaadvnet.
   * **Permitir acesso à rede virtual**: (Marcar)
   * **Permitir tráfego encaminhado**: (Marcar). Deixar Olá outras duas caixas de seleção está desmarcada.
8. Clique em **OK**.

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
     * **Versão**: HDI 3.6. Somente a versão 3.6 do cluster HDInsight dá suporte ao HDInsight ingressado no domínio.
     * **Tipo de cluster**: PREMIUM
       
       Clique em **selecione** toosave alterações de saudação.
   * **Credenciais**: configurar credenciais Olá Olá cluster e de usuário usuário SSH hello.
   * **Fonte de dados**: criar uma nova conta de armazenamento ou usar uma conta de armazenamento existente como Olá conta de armazenamento padrão para o cluster do HDInsight hello. local de saudação deve Olá mesmas Olá duas VNets.  Olá local é também saudação do cluster do HDInsight hello.
   * **Preços**: selecione Olá número de nós de trabalho do cluster.
   * **Configurações avançadas**: 
     
     * **Ingresso no domínio e Sub-rede/VNet**: 
       
       * **Configurações de domínio**: 
         
         * **Nome de domínio**: contoso.onmicrosoft.com
         * **Nome de usuário de domínio**: insira um nome de usuário de domínio. Esse domínio deve ter Olá seguintes privilégios: ingressar máquinas toohello domínio e colocá-los na unidade de organização Olá especificar durante a criação do cluster. Criar entidades de serviço na unidade de organização Olá que especificar durante a criação do cluster. Crie entradas de DNS reverso. Este usuário de domínio se tornará administrador Olá desse cluster HDInsight ingressado no domínio.
         * **Senha do domínio**: insira a senha de usuário de domínio hello.
         * **Unidade de organização**: digite nome distinto de saudação do hello UO que você deseja toouse com o cluster HDInsight. Por exemplo: OU=HDInsightOU,DC=contoso,DC=onmicrosoft,DC=com. Se essa UO não existir, o cluster HDInsight tentará toocreate essa UO. Certifique-se de saudação OU já está presente ou conta de domínio Olá tem permissões toocreate um novo. Se você usar a conta de domínio de saudação que faz parte dos administradores AADDC, ele terá as permissões necessárias toocreate Olá UO.
         * **URL LDAPS**: ldaps://contoso.onmicrosoft.com:636
         * **Grupo de usuários de acesso**: especifique o grupo de segurança de saudação cujos usuários toosync toohello pelo cluster. Por exemplo, HiveUsers.
           
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
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-domain-joined-hdinsight-cluster.json" target="_blank"><img src="./media/hdinsight-domain-joined-configure/deploy-to-azure.png" alt="Deploy tooAzure"></a>
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
   * **DNs do grupo de usuários do cluster**: [\"HiveUsers\"]
   * **LDAPUrls**: ["ldaps://contoso.onmicrosoft.com:636"]
   * **DomainAdminUserName**: (nome de usuário do Enter Olá domínio admin)
   * **DomainAdminPassword**: (Insira a senha de usuário do administrador de domínio Olá)
   * **Eu concordo toohello termos e condições acima**: (Verificar)
   * **PIN toodashboard**: (Verificar)
3. Clique em **Comprar**. Você verá um novo bloco intitulado **Implantando a implantação de modelo**. Demora cerca de aproximadamente 20 minutos toocreate um cluster. Depois de criar o cluster hello, você pode clicar em folha de cluster Olá em tooopen portal Olá-lo.

Depois de concluir o tutorial hello, talvez você queira toodelete cluster de saudação. Com o HDInsight, seus dados são armazenados no Armazenamento do Azure, assim você poderá excluir, com segurança, um cluster quando ele não estiver em uso. Você também é cobrado por um cluster HDInsight, mesmo quando ele não está em uso. Como encargos Olá para cluster Olá são muitas vezes mais do que encargos Olá para armazenamento, faz sentido, financeiramente falando toodelete clusters quando eles não estiverem em uso. Para obter instruções de saudação da exclusão de um cluster, consulte [clusters gerenciar Hadoop em HDInsight usando Olá portal do Azure](hdinsight-administer-use-management-portal.md#delete-clusters).

## <a name="next-steps"></a>Próximas etapas
* Para configurar políticas do Hive e executar consultas do Hive, confira [Configurar políticas do Hive para clusters HDInsight associados ao domínio](hdinsight-domain-joined-run-hive.md).
* Para usar clusters de HDInsight tooDomain associado do SSH tooconnect, consulte [usar SSH com baseados em Linux Hadoop no HDInsight do Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).

