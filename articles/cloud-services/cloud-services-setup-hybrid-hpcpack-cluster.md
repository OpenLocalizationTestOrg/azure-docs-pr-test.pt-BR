---
title: "cluster de aaaSet o HPC Pack híbridos no Azure | Microsoft Docs"
description: "Saiba como toouse Microsoft HPC Pack e do Azure tooset até um pequeno, alto desempenho computação (HPC) cluster híbrido"
services: cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: hpc-pack
ms.assetid: 
ms.service: cloud-services
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: danlep
ms.openlocfilehash: 5ad30d78dcd0c6a95d2a61f25015232edab3563c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-hybrid-high-performance-computing-hpc-cluster-with-microsoft-hpc-pack-and-on-demand-azure-compute-nodes"></a>Configurar um cluster HPC (computação de alto desempenho) híbrido com nós de computação do Azure sob demanda e o Microsoft HPC Pack
Use o Microsoft HPC Pack 2012 R2 e do Azure tooset a um pequeno, híbrido computação de alto desempenho cluster (HPC). Olá mostrados neste artigo consiste em um nó de cabeçalho do HPC Pack no local e alguns computação nós sob demanda do Azure você implanta o serviço de nuvem. Em seguida, você pode executar trabalhos de computação em cluster híbrido que hello.

![Cluster híbrido de HPC][Overview] 

Este tutorial mostra uma abordagem, chamados de cluster "intermitência toohello nuvem" aplicativos de computação intensa de toorun toouse escalonáveis e sob demanda de recursos do Azure.

Este tutorial não pressupõe nenhuma experiência anterior com clusters de cálculo ou com o HPC Pack. É pretendido toohelp somente que você implantar um cluster de computação híbrido rapidamente para fins de demonstração. Para considerações e etapas toodeploy cluster híbridos HPC Pack em maior escala em um ambiente de produção ou toouse HPC Pack 2016, consulte Olá [detalhadas orientação](http://go.microsoft.com/fwlink/p/?LinkID=200493). Para ver outros cenários com o HPC Pack, incluindo a implantação de cluster automatizada nas máquinas virtuais do Azure, confira [Opções de cluster HPC com o Microsoft HPC Pack no Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="prerequisites"></a>Pré-requisitos
* **Assinatura do Azure** – Se não tiver uma, você poderá criar uma [conta gratuita](https://azure.microsoft.com/free/) em apenas alguns minutos.
* **Um computador local executando o Windows Server 2012 R2 ou o Windows Server 2012** -usar este computador como nó de cabeçalho de saudação do cluster HPC hello. Se você ainda não estiver executando o Windows Server, poderá baixar e instalar uma [versão de avaliação](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).
  
  * computador Olá deve ser tooan ingressado no domínio de Active Directory. Para fins de teste, você pode configurar o computador do nó principal hello como um controlador de domínio. tooadd Olá a função de servidor Serviços de domínio do Active Directory e promover o computador do nó principal hello como um controlador de domínio, consulte documentação Olá para o Windows Server.
  * toosupport HPC Pack, o sistema operacional de saudação deve ser instalado em um desses idiomas: inglês, japonês ou chinês (simplificado).
  * Verifique se as atualizações importantes e críticas foram instaladas.
* **HPC Pack 2012 R2** - [baixar](http://go.microsoft.com/fwlink/p/?linkid=328024) pacote de instalação de Olá para a versão mais recente da saudação livre de custos e cópia Olá arquivos toohello principal computador do nó. Escolha os arquivos de instalação Olá mesmo idioma em que a instalação do Windows Server.

    >[!NOTE]
    > Se você quiser toouse HPC Pack 2016, em vez de HPC Pack 2012 R2, a configuração adicional é necessária. Consulte Olá [detalhadas orientação](http://go.microsoft.com/fwlink/p/?LinkID=200493).
    > 
* **Conta de domínio** -essa conta deve ser configurada com permissões de administrador local no nó principal de saudação tooinstall HPC Pack.
* **Conectividade TCP na porta 443** de saudação tooAzure de nó principal.

## <a name="install-hpc-pack-on-hello-head-node"></a>Instala o HPC Pack no nó de cabeçalho Olá
Primeiro, instale o Microsoft HPC Pack em seu computador local executando o Windows Server. Este computador se torna o nó principal de saudação do cluster de saudação.

1. Faça logon no nó principal toohello usando uma conta de domínio que tenha permissões de administrador local.

2. Inicie o hello Assistente de instalação do HPC Pack executando Setup.exe Olá HPC Pack em arquivos de instalação.

3. Em Olá **instalação do HPC Pack 2012 R2** tela, clique em **nova instalação ou adicione a nova instalação existente de tooan de recursos**.

    ![Instalação do HPC Pack 2012][install_hpc1]

4. Em Olá **página Contrato de usuário do Software Microsoft**, clique em **próximo**.

5. Em Olá **Selecionar tipo de instalação** , clique em **criar um novo cluster HPC criando um nó de cabeçalho**e, em seguida, clique em **próximo**.

6. Assistente de saudação executa vários testes de pré-instalação. Clique em **próximo** em Olá **regras de instalação** página se todos os testes passarem. Caso contrário, examine Olá informações fornecidas e faça as alterações necessárias em seu ambiente. Em seguida, execute novamente os testes de saudação ou se necessário iniciar Olá Assistente de instalação novamente.
7. Em Olá **configuração de banco de dados do HPC** página, certifique-se de **nó de cabeçalho** está selecionada para todos os bancos de dados do HPC e, em seguida, clique em **próximo**. 

    ![Configuração do BD][install_hpc4]

8. Aceite as seleções de padrão nas páginas de saudação restantes do Assistente de saudação. Em Olá **instalar componentes necessários** , clique em **instalar**.
   
    ![Instalar][install_hpc6]

9. Após a conclusão da instalação Olá, desmarque **iniciar Gerenciador de Cluster de HPC** e, em seguida, clique em **concluir**. (Você iniciará o Gerenciador de Cluster de HPC em uma etapa posterior.)
   
    ![Concluir][install_hpc7]

## <a name="prepare-hello-azure-subscription"></a>Preparar Olá assinatura do Azure
Executar Olá etapas Olá [portal do Azure](https://portal.azure.com) com sua assinatura do Azure. Depois de concluir essas etapas, você pode implantar nós do Azure do nó principal do hello local. 
  
  > [!NOTE]
  > Além disso, tome nota de sua ID de assinatura do Azure, que será necessária posteriormente. Localizar a ID de saudação em **assinaturas** no portal de saudação.
  > 

### <a name="upload-hello-default-management-certificate"></a>Carregar certificado de gerenciamento saudação padrão
HPC Pack instala um certificado autoassinado no nó principal do hello, chamado de certificado de gerenciamento padrão Microsoft HPC Azure hello, que pode ser carregado como um certificado de gerenciamento do Azure. Esse certificado é fornecido para teste e conexão de saudação implantações de prova de conceito toosecure entre Olá nó principal e o Azure.

1. No computador do nó principal hello, entrar toohello [portal do Azure](https://portal.azure.com).

2. Clique em **Assinaturas** > *nome_da_assinatura*.

3. Clique em **Certificados de gerenciamento** > **Carregar**.4. Procure no nó principal Olá Olá arquivo C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer. Em seguida, clique em **Carregar**.

   
Olá **padrão do HPC Azure Management** certificado será exibido na lista de saudação de certificados de gerenciamento.

### <a name="create-an-azure-cloud-service"></a>Criar um serviço de nuvem do Azure
> [!NOTE]
> Para melhor desempenho, criar serviço de nuvem hello e conta de armazenamento da saudação (em uma etapa posterior) no hello mesma região geográfica.
> 
> 

1. No portal de saudação, clique em **(clássico) de serviços de nuvem** > **+ adicionar**.

2.  Digite um nome DNS para o serviço de saudação, escolha um grupo de recursos e um local e, em seguida, clique em **criar**.


### <a name="create-an-azure-storage-account"></a>Criar uma conta de armazenamento do Azure
1. No portal de saudação, clique em **contas de armazenamento (clássico)** > **+ adicionar**.

2. Digite um nome para a conta de saudação e selecione Olá **clássico** modelo de implantação.

3. Escolha um grupo de recursos e um local e deixe as outras configurações com os valores padrão. Em seguida, clique em **Criar**.

## <a name="configure-hello-head-node"></a>Configurar o nó principal Olá
toouse toodeploy do Gerenciador de Cluster de HPC nós do Azure e toosubmit trabalhos, primeiro executar algumas etapas de configuração de cluster necessário.

1. No nó de cabeçalho hello, inicie o Gerenciador de Cluster de HPC. Se hello **selecionar nó principal** caixa de diálogo for exibida, clique em **computador Local**. Olá **lista de tarefas de implantação** é exibida.

2. Em **Tarefas de implantação necessárias**, clique em **Configurar sua rede**.
   
    ![Configurar Rede][config_hpc2]

3. No Assistente de configuração de rede do hello, selecione **todos os nós somente em uma rede corporativa** (topologia 5). Essa configuração de rede é hello mais simples para fins de demonstração.
   
    ![Topologia 5][config_hpc3]
   
4. Clique em **próximo** tooaccept valores padrão Olá restantes páginas do Assistente de saudação. Em seguida, na Olá **revisão** , clique em **configurar** toocomplete configuração de rede de saudação.

5. Em Olá **lista de tarefas de implantação**, clique em **fornecer credenciais de instalação**.

6. Em Olá **credenciais de instalação** caixa de diálogo, digite as credenciais da conta de domínio Olá que você usou tooinstall HPC Pack hello. Em seguida, clique em **OK**. 
   
    ![Credenciais de instalação][config_hpc6]
   
7. Em Olá **lista de tarefas de implantação**, clique em **configurar Olá nomeação de novos nós**.

8. Em Olá **série de nomeação de nó especifique** caixa de diálogo caixa, aceite o padrão de saudação nomenclatura série e clique em **Okey**. Conclua esta etapa, embora hello nós do Azure que você adicionar neste tutorial são nomeadas automaticamente.
   
    ![Nomeação de nós][config_hpc8]
   
9. Em Olá **lista de tarefas de implantação**, clique em **criar um modelo de nó**. Mais tarde no tutorial hello, use cluster de toohello Olá nós modelo tooadd nós do Azure.

10. No Assistente Criar modelo de nó de hello, faça Olá a seguir:
    
    a. Em Olá **Escolher tipo de modelo de nó** , clique em **modelo de nó do Windows Azure**e, em seguida, clique em **próximo**.
    
    ![Modelo do nó][config_hpc10]
    
    b. Clique em **próximo** nome do modelo tooaccept saudação padrão.
    
    c. Em Olá **fornecem informações de assinatura** , insira sua ID de assinatura do Azure (disponível em suas informações de conta do Azure). Em seguida, em **Certificado de gerenciamento**, procure por **Gerenciamento do Azure Padrão no Microsoft HPC.** Em seguida, clique em **Próximo**.
    
    ![Modelo do nó][config_hpc12]
    
    d. Em Olá **fornecer informações sobre o serviço** página, serviço de nuvem selecione hello e conta de armazenamento Olá que você criou na etapa anterior. Em seguida, clique em **Próximo**.
    
    ![Modelo do nó][config_hpc13]
    
    e. Clique em **próximo** tooaccept valores padrão Olá restantes páginas do Assistente de saudação. Em seguida, na Olá **revisão** , clique em **criar** toocreate modelo de nó de saudação.
    
    > [!NOTE]
    > Por padrão, modelo de nó do Azure Olá inclui configurações para toostart (provisionar) e stop Olá nós manualmente, usando o Gerenciador de Cluster de HPC. Opcionalmente, você pode configurar um agendamento toostart e parar Olá nós do Azure automaticamente.
    > 
    > 

## <a name="add-azure-nodes-toohello-cluster"></a>Adicionar nós do Azure toohello cluster
Agora use o cluster de toohello Olá nós modelo tooadd nós do Azure. Adicionar o cluster do hello nós toohello armazena suas informações de configuração para que você possa iniciar (provisionar)-los a qualquer momento no serviço de nuvem hello. Sua assinatura obtém cobrada somente para nós do Azure depois Olá instâncias são executadas no serviço de nuvem hello.

Siga estas etapas tooadd dois pequeno nós.

1. No Gerenciador de Cluster HPC, clique em **Gerenciamento de Nós** (chamado de **Gerenciamento de Recursos** em versões atuais do HPC Pack) > **Adicionar Nó**.
   
    ![Adicionar Nó][add_node1]

2. Em Olá Assistente para adicionar nó, em Olá **Selecionar método de implantação** , clique em **nós do Windows Azure adicionar**e, em seguida, clique em **próximo**.
   
    ![Adicionar nó do Azure][add_node1_1]

3. Em Olá **especificar novos nós** página, o modelo de nó do Azure selecione Olá criado anteriormente (chamado por padrão **modelo AzureNode**). Em seguida, especifique **2** nós de tamanho **Pequeno** e clique em **Avançar**.
   
    ![Especificar nós][add_node2]
   
4. Em Olá **Concluindo Olá Assistente para adicionar nó** , clique em **concluir**.
    
     Dois nós do Azure, chamados **AzureCN-0001** e **AzureCN-0002**, agora são exibidos no Gerenciador de Cluster de HPC. Ambos são Olá **não implantado** estado.
   
    ![Nós adicionados][add_node3]

## <a name="start-hello-azure-nodes"></a>Iniciar Olá nós do Azure
Quando desejar que recursos de cluster toouse Olá no Azure, use o Gerenciador de Cluster de HPC toostart (provisionar) Olá nós do Azure e colocarão-los online.

1. No Gerenciador de Cluster de HPC, clique em **nó gerenciamento** (chamado **gerenciamento de recursos** nas versões atuais do HPC Pack), e selecione Olá nós do Azure.

2. Clique em **Iniciar** e clique em **OK**.
   
   ![Iniciar nós][add_node4]
   
    nós Olá transição toohello **provisionamento** estado. Saudação de exibição saudação do log tootrack progresso do provisionamento de provisionamento.
   
    ![Provisionar nós][add_node6]

3. Depois de alguns minutos, hello nós do Azure concluir o provisionamento e estão em Olá **Offline** estado. Nesse estado, instâncias de função hello estão em execução, mas ainda não podem aceitar trabalhos de cluster.

4. tooconfirm que Olá instâncias de função está em execução, no hello portal do Azure, clique em **serviços de nuvem (clássicos)** > *your_cloud_service_name*.
   
   Você deverá ver dois **HpcWorkerRole** instâncias (nós) em execução no serviço de saudação. HPC Pack automaticamente implanta dois **HpcProxy** instâncias a comunicação entre o nó principal hello e Azure toohandle (tamanho médio).

   ![Executando instâncias][view_instances1]

5. toobring Olá nós do Azure online toorun cluster trabalhos, selecione Olá nós, com o botão direito e clique **colocar Online**.
   
    ![Nós off-line][add_node7]
   
    Gerenciador de Cluster de HPC indica que nós Olá nessa Olá **Online** estado.

## <a name="run-a-command-across-hello-cluster"></a>Executar um comando de cluster Olá
instalação de saudação toocheck, use Olá HPC Pack **clusrun** comando toorun um comando ou o aplicativo em um ou mais nós de cluster. Como um exemplo simples, use **clusrun** tooget configuração de IP de saudação do hello nós do Azure.

1. No nó de cabeçalho hello, abra um prompt de comando como administrador.

2. Digite hello comando a seguir:
   
    `clusrun /nodes:azurecn* ipconfig`

3. Se solicitado, insira sua senha de administrador de cluster. Você deve ver a saída do comando a seguir toohello semelhante.
   
    ![clusrun][clusrun1]

## <a name="run-a-test-job"></a>Executar um trabalho de teste
Agora, envie um trabalho de teste é executado em um cluster híbrido que hello. Este exemplo é um trabalho simples de limpeza paramétrica (um tipo de computação intrinsecamente paralela). Este exemplo executa subtarefas que adicionar um tooitself inteiro usando Olá **set /a** comando. Todos os nós de saudação em cluster Olá contribuem toofinishing Olá subtarefas para inteiros de 1 too100.

1. No Gerenciador de Cluster HPC, clique em **Gerenciamento de Trabalho** > **Novo Trabalho de Limpeza Paramétrica**.
   
    ![Novo trabalho][test_job1]

2. Em Olá **novo trabalho de varredura paramétrica** na caixa **linha de comando**, tipo `set /a *+*` (substituindo a linha de comando do saudação padrão que é exibido). Deixe valores padrão para Olá restantes configurações e, em seguida, clique em **enviar** toosubmit trabalho de saudação.
   
    ![Limpeza paramétrica][param_sweep1]

3. Quando o trabalho de saudação é concluído, clique duas vezes em Olá **minha tarefa varredura** trabalho.

4. Clique em **exibir tarefas**e, em seguida, clique em uma saída de hello calculado tooview subtarefa dessa subtarefa.
   
    ![Resultados da tarefa][view_job361]

5. toosee qual nó executada cálculo Olá que subtarefa, clique em **alocada nós**. (Seu cluster pode mostrar um nome de nó diferente).
   
    ![Resultados da tarefa][view_job362]

## <a name="stop-hello-azure-nodes"></a>Parar Olá nós do Azure
Depois que você experimente cluster Olá, pare Olá nós do Azure tooavoid desnecessárias cobra tooyour conta. Esta etapa interrompe o serviço de nuvem hello e remove Olá instâncias de função do Azure.

1. No Gerenciador de Cluster HPC, em **Gerenciamento de Nós** (chamado de **Gerenciamento de Recursos** em versões anteriores do HPC Pack), selecione ambos os nós do Azure. Em seguida, clique em **Parar**.
   
    ![Parar os nós][stop_node1]

2. Em Olá **nós do Windows Azure parar** caixa de diálogo, clique em **parar**. 
   
3. nós Olá transição toohello **parando** estado. Depois de alguns minutos, o Gerenciador de Cluster de HPC mostra que nós Olá **não implantado**.
   
    ![Nós não implantados][stop_node4]

4. Olá de tooconfirm instâncias de função hello são não mais em execução no Azure, no portal, Azure, clique em **(clássico) de serviços de nuvem** > *your_cloud_service_name*. Não há instâncias são implantadas no ambiente de produção de hello. 
   
    Isso conclui o tutorial hello.

## <a name="next-steps"></a>Próximas etapas
* Explorar a documentação de saudação do [HPC Pack](https://technet.microsoft.com/library/cc514029).
* Consulte tooset a uma implantação de cluster de HPC Pack em maior escala, híbrida [disparar tooAzure instâncias de função de trabalho com o Microsoft HPC Pack](http://go.microsoft.com/fwlink/p/?LinkID=200493).
* Para outra maneiras toocreate um cluster de HPC Pack no Azure, incluindo modelos do Azure Resource Manager, consulte [opções de cluster HPC com Microsoft HPC Pack no Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


[Overview]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/hybrid_cluster_overview.png
[install_hpc1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc1.png
[install_hpc4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc4.png
[install_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc6.png
[install_hpc7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc7.png
[install_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc10.png
[config_hpc2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc2.png
[config_hpc3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc3.png
[config_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc6.png
[config_hpc8]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc8.png
[config_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc10.png
[config_hpc12]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc12.png
[config_hpc13]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc13.png
[add_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1.png
[add_node1_1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1_1.png
[add_node2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node2.png
[add_node3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node3.png
[add_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node4.png
[add_node6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node6.png
[add_node7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node7.png
[view_instances1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances1.png
[clusrun1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/clusrun1.png
[test_job1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/test_job1.png
[param_sweep1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/param_sweep1.png
[view_job361]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job361.png
[view_job362]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job362.png
[stop_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node1.png
[stop_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node4.png
[view_instances2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances2.png
