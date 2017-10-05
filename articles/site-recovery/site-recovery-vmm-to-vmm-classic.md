---
title: "Replicar VMs do Hyper-V no VMM para um site secundário (Azure clássico) | Microsoft Docs"
description: "Este artigo descreve como replicar máquinas virtuais Hyper-V em nuvens do VMM para um site secundário do VMM com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: a63acba3-8fb3-4926-aa29-b1e64a765681
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: raynew
ms.openlocfilehash: 6814f62f73bad272229205f4768dcce5947117d1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-a-secondary-vmm-site"></a>Replicar máquinas virtuais do Hyper-V em nuvens de VMM para um site de VMM secundário
> [!div class="op_single_selector"]
> * [Portal do Azure](site-recovery-vmm-to-vmm.md)
> * [Portal clássico](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell – Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

O Azure Site Recovery contribui para sua estratégia de BCDR (continuidade de negócios e recuperação de desastre) administrando a replicação, o failover e a recuperação de máquinas virtuais e servidores físicos. As máquinas podem ser replicadas no Azure ou em um datacenter local secundário. Para ter uma breve visão geral, leia [O que é Azure Site Recovery?](site-recovery-overview.md)

## <a name="overview"></a>Visão geral
Este artigo descreve como replicar máquinas virtuais de Hyper-V em servidores de host Hyper-V gerenciados em nuvens do VMM para site secundário do VMM usando o Azure Site Recovery.

O artigo inclui os pré-requisitos, mostra como configurar um cofre do Site Recovery, instalar o Provedor do Azure Site Recovery nos servidores do VMM de origem e destino, registrar os servidores no cofre, definir as configurações de proteção para nuvens VMM e, em seguida, habilitar a proteção para VMs do Hyper-V. Conclua testando o failover para verificar se tudo está funcionando conforme o esperado.

Publique eventuais comentários ou perguntas no final deste artigo ou no [Fórum dos Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="architecture"></a>Arquitetura
A figura abaixo mostra os canais de comunicação e as portas diferentes usados pelo Azure Site Recovery para coordenação e a replicação

![Topologia E2E](./media/site-recovery-vmm-to-vmm-classic/e2e-topology.png)

## <a name="before-you-start"></a>Antes de começar
Verifique se estes pré-requisitos estão em vigor:

| **Pré-requisitos** | **Detalhes** |
| --- | --- |
| **As tabelas** |Você precisa de uma conta do [Microsoft Azure](https://azure.microsoft.com/) . Você pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/). [Saiba mais](https://azure.microsoft.com/pricing/details/site-recovery/) sobre os preços da Recuperação de Site. |
| **VMM** |Você precisará de pelo menos um servidor do VMM.<br/><br/>O servidor VMM deve estar executando pelo menos o System Center 2012 SP1 com as últimas atualizações cumulativas.<br/><br/>Se quiser configurar a proteção com um único servidor VMM, você precisará de pelo menos duas nuvens configuradas no servidor.<br/><br/>Se você desejar implantar a proteção com dois servidores VMM, cada servidor deverá ter pelo menos uma nuvem configurada no servidor VMM primário que você deseja proteger e uma nuvem configurada no servidor VMM secundário que você deseja usar para proteção e recuperação<br/><br/>Todas as nuvens VMM devem ter o perfil de capacidade do Hyper-V definido.<br/><br/>A nuvem de origem que você deseja proteger deve conter um ou mais grupos de host VMM. |
| **Hyper-V** |Você precisará de um ou mais servidores de host do Hyper-V nos grupos de hosts do VMM primários e secundários e de uma ou mais máquinas virtuais em cada servidor de host do Hyper-V.<br/><br/>Os servidores Hyper-V host e de destino devem estar executando pelo menos o Windows Server 2012 com a função Hyper-V e ter as últimas atualizações instaladas.<br/><br/>Qualquer servidor Hyper-V que contenha as VMs que deseja proteger deve estar localizado em uma nuvem VMM.<br/><br/>Se você estiver executando o Hyper-V em um cluster, observe que o agente de cluster não será criado automaticamente caso tenha um cluster baseado em endereços IP estáticos. Você precisará configurar o agente de cluster manualmente. [Saiba mais](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters) na entrada do blog de Aidan Finn. |
| **Mapeamento de rede** |Você pode definir o mapeamento de rede para assegurar que as máquinas virtuais de réplica sejam colocadas da melhor forma possível em servidores host Hyper-V secundários após o failover e que possam se conectar às redes VM apropriadas. Se você não configurar a réplica de mapeamento de rede, as VMs não serão conectadas a nenhuma rede após o failover.<br/><br/>Para configurar o mapeamento de rede durante a implantação, certifique-se de que as máquinas virtuais no servidor host Hyper-V de origem estejam conectadas a uma rede de VM do VMM. Essa rede deve estar vinculada a uma rede lógica associada à nuvem.<br/<br/>A nuvem de destino no servidor VMM secundário que você usar para recuperação deverá ter uma rede VM correspondente configurada, que, por sua vez, deverá estar vinculada a uma rede lógica correspondente associada à nuvem de destino. |
| **Mapeamento de armazenamento** |Por padrão, quando você replica uma máquina virtual em um servidor host Hyper-V de origem para um servidor host Hyper-V de destino, os dados replicados são armazenados no local padrão indicado para o host Hyper-V de destino no Gerenciador Hyper-V. Para obter mais controle sobre onde os dados replicados são armazenados, você pode configurar o mapeamento do armazenamento<br/><br/> Para configurar o mapeamento do armazenamento, precisa configurar as classificações de armazenamento nos servidores do VMM de origem e de destino antes de começar a implantação. |

## <a name="step-1-create-a-site-recovery-vault"></a>Etapa 1: criar um cofre de Recuperação de Site
1. Entre no [Portal de Gerenciamento](https://portal.azure.com) do servidor VMM que você deseja registrar.
2. Expanda **Serviços de Dados** > **Serviços de Recuperação** e clique em **Cofre do Site Recovery**.
3. Clique em **Criar Novo** > **Criação Rápida**.
4. Em **Nome**, digite um nome amigável para identificar o cofre.
5. Em **Região** , selecione a região geográfica para o cofre. Para verificar as regiões com suporte, consulte a Disponibilidade Geográfica nos [Detalhes dos Preços do Azure Site Recovery](http://go.microsoft.com/fwlink/?LinkId=389880).
6. Clique em **Criar cofre**.

    ![Criar cofre](./media/site-recovery-vmm-to-vmm-classic/create-vault.png)

Na barra de status, verifique se o cofre foi criado. O cofre será listado como **Ativo** na página de Serviços de Recuperação.

## <a name="step-2-generate-a-vault-registration-key"></a>Etapa 2: gerar uma chave de registro do cofre
Gere uma chave de registro no cofre. Após baixar o Provedor do Azure Site Recovery e instalá-lo no servidor VMM, você usará essa chave para registrar o servidor VMM no cofre.

1. Na página **Serviços de Recuperação** , clique no cofre para abrir na página de Início Rápido. O Início Rápido pode também ser aberto a qualquer tempo usando o ícone.

    ![Ícone de Inicialização Rápida](./media/site-recovery-vmm-to-vmm-classic/quick-start-icon.png)
2. Na lista suspensa, escolha **Entre dois sites de VMM locais**.
3. Em **Preparar Servidores VMM**, clique em **Gerar arquivo de chave de registro**. O arquivo de chave é gerado automaticamente e é válido por cinco dias após ter sido gerado. Se não estiver acessando o Portal do Azure por meio do servidor VMM, você precisará copiar esse arquivo para o servidor.

    ![Chave de Registro](./media/site-recovery-vmm-to-vmm-classic/register-key.png)

## <a name="step-3-install-the-azure-site-recovery-provider"></a>Etapa 3: instalar o Provedor do Azure Site Recovery
1. Na página **Início Rápido**, em **Preparar servidores VMM**, clique **Baixar o Provedor do Microsoft Azure Site Recovery para instalação nos servidores VMM** para obter a versão mais recente do arquivo de instalação do Provedor.
2. Execute esse arquivo no servidor VMM de origem.

   > [!NOTE]
   > Se o VMM for implantado em um cluster e você estiver instalando o Provedor pela primeira vez, instale-o em um nó ativo e conclua a instalação para registrar o servidor VMM no cofre. Em seguida, instale o Provedor nos outros nós. Observe que, se estiver atualizando o Provedor, você precisará fazer a atualização em todos os nós porque todos eles devem estar executando a mesma versão do Provedor.
   >
   >
3. O Instalador faz algumas **Verificações de Pré-requisitos** e solicita permissão para interromper o serviço VMM para iniciar a instalação do Provedor. O Serviço VMM será reiniciado automaticamente quando a instalação for finalizada. Se estiver instalando em um cluster do VMM, você deverá parar a função de Cluster.
4. No **Microsoft Update** você pode optar por atualizações. Com esta configuração de Provedor habilitada, a atualização será instalada de acordo com a política do Microsoft Update.

    ![Atualizações da Microsoft](./media/site-recovery-vmm-to-vmm-classic/ms-update.png)
5. O local de instalação é definido como **<SystemDrive>\Arquivos de Programas\Microsoft System Center 2012 R2\Virtual Machine Manager\bin**. Clique no botão Instalar para iniciar a instalação do Provedor.

    ![InstallLocation](./media/site-recovery-vmm-to-vmm-classic/install-location.png)
6. Após a instalação do Provedor, clique em **Registrar** para registrar o servidor no cofre.

    ![InstallComplete](./media/site-recovery-vmm-to-vmm-classic/install-complete.png)
7. Em **Nome do cofre**, verifique o nome do cofre para o qual o servidor será registrado. Clique em *Próximo*.

    ![Registros do servidor](./media/site-recovery-vmm-to-vmm-classic/vaultcred.PNG)
8. Em **Conexão de Internet** , especifique como o Provedor em execução no servidor VMM se conecta à Internet. Selecione **Conectar-se com as configurações de proxy existentes** para usar as configurações de conexão com a Internet padrão definidas no servidor.

    ![Configurações da Internet](./media/site-recovery-vmm-to-vmm-classic/proxydetails.PNG)

   * Se quiser usar um proxy personalizado, você deverá configurá-lo antes de instalar o provedor. Quando você definir as configurações personalizadas de proxy, será executado um teste para verificar a conexão proxy.
   * Se usar um proxy personalizado ou se seu proxy padrão exigir autenticação, você precisará inserir os detalhes do proxy, incluindo a porta e o endereço do proxy.
   * As URLs a seguir devem estar acessíveis no servidor do VMM e nos hosts Hyper-V
     * *.hypervrecoverymanager.windowsazure.com
     * *.accesscontrol.windows.net
     * *.backup.windowsazure.com
     * *.blob.core.windows.net
     * *.store.core.windows.net
   * Permita os endereços IP descritos em [Intervalos de IP do armazenamento de dados do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) e o protocolo HTTPS (443). Você teria que fazer uma lista de intervalos IP válidos da região do Azure que você planeja usar e do oeste dos EUA.
   * Se você usar um proxy personalizado, uma conta RunAs VMM (DRAProxyAccount) será criada automaticamente usando as credenciais de proxy especificadas. Configure o servidor proxy para que essa conta possa ser autenticada com êxito. As configurações da conta RunAs VMM podem ser modificadas no console do VMM. Para fazer isso, abra o espaço de trabalho **Configurações**, expanda **Segurança**, clique em **Contas Executar como** e modifique a senha de DRAProxyAccount. Você precisará reiniciar o serviço VMM para que essa configuração entre em vigor.
9. Em **Chave de Registro**, selecione a chave que você baixou no Azure Site Recovery e copiou para o servidor VMM.
10. A configuração de criptografia é usada somente quando você estiver replicando VMs do Hyper-V em nuvens do VMM no Azure. Se estiver replicando para um site secundário, ela não é usada.
11. Em **Nome do servidor**, especifique um nome amigável para identificar o servidor VMM no cofre. Em uma configuração de cluster, especifique o nome de função de cluster do VMM.
12. Em **Sincronizar metadados de nuvem** , selecione se você deseja sincronizar os metadados para todas as nuvens no servidor do VMM com o cofre. Esta ação só precisa acontecer uma vez em cada servidor. Se você não quiser sincronizar todas as nuvens, você pode deixar essa configuração desmarcada e sincronizar cada nuvem individualmente nas propriedades da nuvem no console VMM.
13. Clique em **Avançar** para concluir o processo. Após o registro, os metadados do servidor VMM é recuperado pela Recuperação de Site do Azure. O servidor é exibido em **Servidores VMM** > **Servidores** no cofre.

    ![Servidores](./media/site-recovery-vmm-to-vmm-classic/provider13.PNG)

### <a name="command-line-installation"></a>Instalação de linha de comando
O Provedor do Azure Site Recovery também pode ser instalado da linha de comando. Esse método pode ser usado para instalar o provedor em um Server CORE para o Windows Server 2012 R2.

1. Baixar o arquivo de instalação do provedor e a chave de registro em uma pasta. Por exemplo, C:\ASR.
2. Parar o Serviço System Center Virtual Machine Manager
3. Extraia o instalador do Provedor executando estes comandos de um prompt de comando com privilégios de **Administrador** :

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. Instale o provedor executando:

        C:\ASR> setupdr.exe /i
5. Registrar o provedor executando:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of the server> /Credentials <path of the credentials file> /EncryptionEnabled <full file name to save the encryption certificate>     

Em que os parâmetros são:

* **/Credentials**: parâmetro obrigatório que especifica o local no qual o arquivo da chave de registro está localizado  
* **/FriendlyName**: parâmetro obrigatório para o nome do servidor do host Hyper-V que aparece no Portal do Azure Site Recovery.
* **/EncryptionEnabled**: parâmetro opcional que você precisará usar apenas no Cenário VMM para Azure se precisar da criptografia de suas máquinas virtuais em repouso no Azure. Certifique-se de que o nome do arquivo que você fornecer tem uma extensão **. pfx** .
* **/proxyAddress**: parâmetro opcional que especifica o endereço do servidor proxy.
* **/proxyport**: parâmetro opcional que especifica a porta do servidor proxy.
* **/proxyUsername**: parâmetro opcional que especifica o nome de usuário de Proxy (se o proxy exige autenticação).
* **/proxyPassword**: parâmetro opcional que especificará a senha para autenticação com o servidor proxy (se o proxy exigir autenticação).  

## <a name="step-4-configure-cloud-protection-settings"></a>Etapa 4: definir as configurações da proteção de nuvem
Depois que os servidores VMM são registrados, você pode definir as configurações de proteção de nuvem. Se você tiver habilitado a opção **Sincronizar dados de nuvem com o cofre** ao instalar o Provedor, todas as nuvens no servidor VMM serão mostradas na guia **Itens Protegidos** no cofre. Se não a tiver habilitado, você poderá sincronizar uma nuvem específica com o Azure Site Recovery na guia **Geral** da página de propriedades de nuvem no console do VMM.

![Publicar uma nuvem](./media/site-recovery-vmm-to-vmm-classic/clouds-list.png)

1. Na página de Início Rápido, clique em **Configurar a proteção para nuvens VMM**.
2. Na guia **Nuvens VMM**, selecione a nuvem que você deseja configurar e vá para a guia **Configuração**.
3. Em **Destino**, selecione **VMM**.
4. Em **Local de destino**, selecione o servidor VMM local que gerencia a nuvem que você deseja usar para a recuperação.
5. Em **Nuvem de Destino**, selecione a nuvem de destino que você deseja usar para failover de máquinas virtuais na nuvem de origem. Observe que:

   * É recomendável selecionar uma nuvem de destino que atende aos requisitos de recuperação para máquinas virtuais que você protegerá.
   * Uma nuvem só pode pertencer a um par único de nuvem - como uma nuvem primária ou de destino.
6. Em **Frequência de cópia**, especifique com que frequência os dados devem ser sincronizados entre os locais de origem e de destino. Observe que essa configuração só é relevante quando o host Hyper-V está executando o Windows Server 2012 R2. Para outros servidores, é usada uma configuração padrão de cinco minutos.
7. Em **Pontos de recuperação adicionais**, especifique se você deseja criar pontos adicionais. O valor padrão de zero indica que apenas o ponto de recuperação mais recente para uma máquina virtual primária é armazenado em um servidor de host de réplica. Observe que a habilitação de vários pontos de recuperação exige armazenamento adicional para os instantâneos que são armazenados em cada ponto de recuperação. Por padrão, os pontos de recuperação são criados a cada hora, assim, cada ponto de recuperação contém dados válidos equivalentes a uma hora. O valor de ponto de recuperação que você atribui à máquina virtual no console do VMM não deve ser menor do que o valor atribuído no console do Azure Site Recovery.
8. Em **Frequência dos instantâneos consistentes por aplicativo**, especifique com que frequência criar instantâneos consistentes com aplicativos. O Hyper-V usa dois tipos de instantâneos: um instantâneo padrão, que fornece um instantâneo incremental de toda a máquina virtual, e um instantâneo consistente com aplicativos, que cria um instantâneo pontual dos dados do aplicativo na máquina virtual. Os instantâneos consistentes com aplicativos usam o Serviço de VSS (Cópias de Sombra de Volume) para garantir que os aplicativos estejam em um estado consistente quando o instantâneo for obtido. Observe que, se você habilitar instantâneos consistentes com aplicativos, isso afetará o desempenho de aplicativos executados em máquinas virtuais de origem. Verifique se o valor definido é menor do que o número de pontos de recuperação adicionais que você configurar.

    ![Definir configurações de proteção](./media/site-recovery-vmm-to-vmm-classic/cloud-settings.png)
9. Em **Compactação da transferência de dados**, especifique se os dados replicados transferidos devem ser compactados.
10. Em **Autenticação**, especifique como o tráfego é autenticado entre os servidores de host do Hyper-V primário e de recuperação. Selecione HTTPS, a menos que você tenha um ambiente Kerberos configurado em funcionamento. A Recuperação de Site do Azure configurará automaticamente os certificados para autenticação HTTPS. Nenhuma configuração manual é necessária. Se você selecionar Kerberos, um tíquete Kerberos será usado para autenticação mútua dos servidores host. Por padrão, as portas 8083 e 8084 (para certificados) serão abertas no Firewall do Windows nos servidores host Hyper-V. Observe que esta configuração só é relevante para servidores de host Hyper-V no Windows Server 2012 R2.
11. Em **Porta**, modifique o número da porta em que os computadores host de origem e de destino ouvem o tráfego de replicação. Por exemplo, você poderá modificar a configuração se desejar aplicar a limitação de largura de banda de rede de QoS (Qualidade de Serviço) ao tráfego de replicação. Verifique se a porta não é usada por outro aplicativo e se ela está aberta nas configurações do firewall.
12. Em **Método de replicação**, especifique como a replicação inicial de dados de locais de origem para destino será tratada, antes de iniciar a replicação normal:

    * **Pela rede**- Copiando dados pela rede pode ser demorado e consumir muitos recursos. É recomendável usar essa opção se a nuvem contiver máquinas virtuais com discos rígidos virtuais relativamente pequenos e se o site primário estiver conectado ao site secundário por uma conexão com largura de banda ampla. Você pode especificar que a cópia deve iniciar imediatamente ou selecionar uma hora. Se você usar a replicação de rede, recomendamos que você agende fora dos horários de pico.
    * **Offline**- Esse método especifica que a replicação inicial será executada usando mídia externa. É útil se você deseja evitar a degradação no desempenho da rede ou para locais geograficamente remotos. Para usar esse método, você especifica o local de exportação na nuvem de origem e o local de importação na nuvem de destino. Ao ativar a proteção de uma máquina virtual, o disco rígido virtual é copiado para o local de exportação especificado. Você envia para o local de destino e copia para o local de importação. O sistema copia as informações importadas para as máquinas virtuais de réplica.
13. Selecione **Excluir Máquina Virtual de Réplica** para especificar que a máquina virtual de réplica deve ser excluída se você parar de proteger a máquina virtual ao selecionar a opção **Excluir proteção para a máquina virtual** na guia Máquinas Virtuais das propriedades da nuvem. Com esta configuração habilitada, quando você desabilita a proteção, a máquina virtual é removida da Recuperação de Site do Azure, as configurações da Recuperação de Site para a máquina virtual são removidas no console VMM, e a réplica é excluída.

    ![Definir configurações de proteção](./media/site-recovery-vmm-to-vmm-classic/cloud-settings-replica.png)

Depois de salvar as configurações, um trabalho será criado e poderá ser monitorado pela guia **Trabalhos** . Todos os servidores do host Hyper-V na nuvem de origem do VMM serão configurados para replicação. As configurações de nuvem podem ser modificadas na guia **Configurar** . Se você deseja modificar a nuvem de destino local ou destino, você deve remover a configuração de nuvem e, em seguida, reconfigurar a nuvem.

### <a name="prepare-for-offline-initial-replication"></a>Preparar a replicação inicial offline
Você precisará executar as seguintes ações para preparar a replicação inicial offline:

* No servidor de origem, você especificará um local do caminho do qual será realizada a exportação de dados. Atribua Controle Total para permissões de NTFS e de Compartilhamento ao serviço VMM no caminho de exportação. No servidor de destino, você especificará um local do caminho do qual será feita a importação de dados. Atribua as mesmas permissões nesse caminho de importação.
* Se o caminho de importação ou de exportação for compartilhado, atribua a associação de grupo de Administrador, Usuário Avançado, Operador de Impressão ou Operador de Servidor à conta de serviço VMM no computador remoto no qual o caminho compartilhado está localizado.
* Se você estiver usando contas Executar como para adicionar hosts, nos caminhos de importação e de exportação, atribua permissões de leitura e gravação às contas Executar como no VMM.
* Os compartilhamentos de importação e de exportação não devem estar localizados em um computador usado como um servidor host Hyper-V porque o Hyper-V não dá suporte à configuração de loopback.
* No Active Directory, em cada servidor host Hyper-V que contém máquinas virtuais que deseja proteger, habilite e configure a delegação restrita para confiar nos computadores remotos nos quais os caminhos de importação e de exportação estão localizados, da seguinte maneira:
  1. No controlador de domínio, abra **Usuários e Computadores do Active Directory**.
  2. Na árvore de console, clique em **DomainName** > **Computadores**.
  3. Clique com o botão direito do mouse no nome do servidor host Hyper-V > **Propriedades**.
  4. Na guia **Delegação**, clique em **Confiar no computador para delegação apenas a serviços especificados**.
  5. Clique em **Usar qualquer protocolo de autenticação**.
  6. Clique em **Adicionar** > **Usuários e Computadores**.
  7. Digite o nome do computador que hospeda o caminho de exportação > **OK**. Na lista de serviços disponíveis, mantenha pressionada a tecla CTRL e clique em **cifs** > **OK**. Repita o procedimento para o nome do computador que hospeda o caminho de importação. Repita conforme necessário para servidores host Hyper-V adicionais.

## <a name="step-5-configure-network-mapping"></a>Etapa 5: configurar o mapeamento de rede
1. Na página Início Rápido, clique em **Mapear redes**.
2. Selecione o servidor VMM de origem do qual você deseja mapear redes e o servidor VMM de destino para o qual as redes serão mapeadas. A lista de redes de origem e suas redes de destino associadas é exibida. Um valor vazio é mostrado para redes que não estão mapeadas no momento.
3. Selecione uma rede em **Rede na origem** > **Mapear**. O serviço detecta as redes VM no servidor de destino e as exibe. Clique no ícone de informações ao lado dos nomes de rede de origem e de destino para exibir as sub-redes de cada rede.

    ![Configurar o mapeamento de rede](./media/site-recovery-vmm-to-vmm-classic/network-mapping1.png)
4. Na caixa de diálogo, selecione uma das redes VM do servidor VMM de destino.

    ![Selecionar uma rede de destino](./media/site-recovery-vmm-to-vmm-classic/network-mapping2.png)
5. Quando você seleciona uma rede de destino, as nuvens protegidas que usam a rede de origem são exibidas. As redes de destino disponíveis que estão associados às nuvens usadas para proteção também são exibidas. Recomendamos que você selecione uma rede de destino disponível para todas as nuvens que você está usando para proteção. Ou você também pode ir para o Servidor VMM e modificar as propriedades da nuvem para adicionar a rede lógica correspondente à rede da vm que deseja escolher.
6. Clique na marca de seleção para concluir o processo de mapeamento. Um trabalho é iniciado para rastrear o progresso do mapeamento. Você pode exibi-lo na Guia **Trabalhos** .

## <a name="step-6-configure-storage-mapping"></a>Etapa 6: configurar mapeamento de armazenamento
Por padrão, quando você replica uma máquina virtual em um servidor host Hyper-V de origem para um servidor host Hyper-V de destino, os dados replicados são armazenados no local padrão indicado para o host Hyper-V de destino no Gerenciador Hyper-V. Para obter mais controle sobre onde os dados replicados são armazenados, você pode configurar mapeamentos de armazenamento da seguinte maneira:

1. Defina classificações de armazenamento nos servidores VMM de origem e de destino. [Saiba mais](https://technet.microsoft.com/library/gg610685.aspx). As classificações devem estar disponíveis para os servidores host Hyper-V nas nuvens de origem e de destino. As classificações não precisam ter o mesmo tipo de armazenamento. Por exemplo, você pode mapear uma classificação de origem que contenha compartilhamentos SMB para uma classificação de destino que contenha CSVs.
2. Depois que classificações estiverem em vigor, você poderá criar mapeamentos. Para fazer isso, acesse a página **Início Rápido** > **Mapear armazenamento**.
3. Clique na guia **Armazenamento** > **Mapear classificações de armazenamento**.
4. Na guia **Mapear classificações de armazenamento** , selecione as classificações nos servidores VMM de origem e de destino. Salve suas configurações.

    ![Selecionar uma rede de destino](./media/site-recovery-vmm-to-vmm-classic/storage-mapping.png)

## <a name="step-7-enable-virtual-machine-protection"></a>Etapa 7: habilitar proteção da máquina virtual
Depois de redes, servidores e nuvens estarem configurados corretamente, você pode ativar a proteção para máquinas virtuais na nuvem.

1. Na guia **Máquinas Virtuais**, na nuvem em que a máquina virtual está localizada, clique em **Habilitar proteção** > **Adicionar máquinas virtuais**.
2. Na lista de máquinas virtuais na nuvem, selecione uma que você quer proteger.

    ![Habilitar a proteção da máquina virtual](./media/site-recovery-vmm-to-vmm-classic/enable-protection.png)
3. Acompanhe o progresso da ação Habilitar Proteção na guia **Trabalhos** , incluindo a replicação inicial. Após o trabalho de Finalizar Proteção ser executado, a máquina virtual está pronta para failover. Após a proteção estar habilitada e as máquinas virtuais serem replicadas, você será capaz de visualizá-los no Azure.

    ![Trabalho de proteção da máquina virtual](./media/site-recovery-vmm-to-vmm-classic/vm-jobs.png)

> [!NOTE]
> Também é possível habilitar a proteção para máquinas virtuais no console do VMM. Clique em **Habilitar Proteção** na barra de ferramentas na guia do **Azure Site Recovery** nas propriedades da máquina virtual.
>
>

### <a name="on-board-existing-virtual-machines"></a>Integrar máquinas virtuais existentes
Se tiver máquinas virtuais existentes no VMM que são replicadas usando a Réplica do Hyper-V, você precisará integrá-las para a proteção do Azure Site Recovery, da seguinte maneira:

1. Verifique se que você tem nuvens primárias e secundárias. Verifique se o servidor Hyper-V que hospeda a máquina virtual existente está localizado em nuvem primária e o servidor Hyper-V que hospeda a máquina virtual de réplica está localizado na nuvem secundária. Verifique se você definiu as configurações de proteção para as nuvens. As configurações devem corresponder àquelas atualmente definidas para a Réplica do Hyper-V. Caso contrário, a replicação de máquina virtual poderá não funcionar conforme o esperado.
2. Em seguida, habilite a proteção para a máquina virtual primária. O Azure Site Recovery e o VMM garantirão que o mesmo host de réplica e a mesma máquina virtual sejam detectados, e o Azure Site Recovery reutilizará e restabelecerá a replicação usando as configurações definidas durante a configuração de nuvem.

## <a name="test-your-deployment"></a>Testar a implantação
Para testar sua implantação, você pode executar um failover de teste para uma única máquina virtual, ou criar um plano de recuperação consistente de várias máquinas virtuais e executar um failover de teste para o plano.  O failover de teste simula o mecanismo de failover e recuperação em uma rede isolada.

### <a name="create-a-recovery-plan"></a>Criar um plano de recuperação
1. Na guia **Planos de Recuperação**, clique em **Criar Plano de Recuperação**.
2. Especifique um nome para o plano de recuperação e servidores do VMM de origem e destino. O servidor de origem deve ter máquinas virtuais que são habilitadas para failover e recuperação. Selecione **Hyper-V** para exibir somente as nuvens que estão configuradas para replicação do Hyper-V.

    ![Criar Plano de Recuperação](./media/site-recovery-vmm-to-vmm-classic/recovery-plan1.png)
3. Em **Selecionar Máquina Virtual**, selecione os grupos de replicação. Todas as máquinas virtuais associadas ao grupo de replicação serão selecionadas e adicionadas ao plano de recuperação. Essas máquinas virtuais são adicionadas ao grupo padrão do plano de recuperação — Grupo 1. Você pode adicionar mais grupos se necessário. Observe que, depois da replicação, as máquinas virtuais serão inicializadas de acordo com a ordem dos grupos de plano de recuperação.

    ![Adicionar máquinas virtuais](./media/site-recovery-vmm-to-vmm-classic/recovery-plan2.png)

Depois que um plano de recuperação tiver sido criado, ele aparecerá na lista da guia **Planos de Recuperação** .

### <a name="run-a-test-failover"></a>Execute um teste de failover
1. Na guia **Planos de Recuperação**, selecione o plano e clique em **Failover de Teste**.
2. Na página **Confirmar Failover de Teste** selecione **Nenhum**. Observe que com essa opção habilitada a falha em máquinas virtuais de réplica não será conectada a nenhuma rede. Isso irá testar se a máquina virtual falha conforme o esperado, mas não testa seu ambiente de rede de replicação. Veja como [executar um failover de teste](site-recovery-failover.md) para obter mais detalhes sobre como usar diferentes opções de rede.
3. A máquina virtual de teste será criada no mesmo host como o host em que a máquina virtual de réplica existe. Ela não é adicionada à mesma nuvem na qual a máquina virtual de réplica está localizada.

### <a name="run-a-recovery-plan"></a>Executar um plano de recuperação
Depois da replicação, a máquina virtual de réplica não poderá ter um endereço IP que seja igual ao endereço IP da máquina virtual primária. As máquinas virtuais atualizarão o servidor DNS que estiverem usando depois que forem iniciadas. Você também pode adicionar um script para atualizar o servidor DNS a fim de garantir uma atualização em tempo hábil.

#### <a name="script-to-retrieve-the-ip-address"></a>Script para recuperar o endereço IP
Execute este script de exemplo para recuperar o endereço IP.

        $vm = Get-SCVirtualMachine -Name <VM_NAME>
        $na = $vm[0].VirtualNetworkAdapters>
        $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
        $ip.address  

#### <a name="script-to-update-dns"></a>Script para atualizar o DNS
Execute este script de exemplo para atualizar o DNS especificando o endereço IP recuperado usando o script de exemplo anterior.

        string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord



## <a name="privacy-information-for-site-recovery"></a>Informações de privacidade para Site Recovery
Esta seção fornece informações adicionais de privacidade para o serviço Microsoft Azure Site Recovery ("Serviço"). Para exibir a política de privacidade dos serviços do Microsoft Azure, confira a [Política de Privacidade do Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=324899)

**Recurso: Registro**

* **O que ele faz**: registra o servidor no serviço para que as máquinas virtuais possam ser protegidas
* **Informações coletadas**: após o registro, o Serviço coleta, processa e transmite as informações de certificado de gerenciamento do servidor VMM designado para fornecer recuperação de desastres usando o nome do Serviço do servidor VMM e o nome de nuvens de máquinas virtuais no servidor VMM.
* **Uso das informações**:

  * Certificado de gerenciamento: usado para ajudar a identificar e autenticar o servidor VMM registrado para acessar o Serviço. O Serviço usa a parte da chave pública do certificado para proteger um token que somente o servidor VMM registrado pode acessar. O servidor precisa usar esse token para obter acesso aos recursos do Serviço.
  * Nome do servidor VMM: o nome do servidor VMM é necessário para identificar e se comunicar com o servidor VMM apropriado no qual as nuvens estão localizadas.
  * Nomes de nuvem do servidor VMM: o nome de nuvem é necessário ao se usar o recurso de emparelhamento/desemparelhamento da nuvem do Serviço descrito abaixo. Quando você decide emparelhar sua nuvem de um data center primário com outra nuvem no data center de recuperação, os nomes de todas as nuvens do data center de recuperação são apresentados.
* **Escolha**: essas informações são uma parte essencial do processo de registro do Serviço porque ajuda você e o Serviço a identificar o servidor VMM para o qual você deseja fornecer a proteção do Azure Site Recovery, além de identificar o servidor VMM registrado correto. Se você não quiser enviar essas informações ao Serviço, não use esse Serviço. Se registrar seu servidor e, mais tarde, quiser cancelar o registro, você poderá fazer isso excluindo as informações do servidor VMM do portal do Serviço (que é o portal do Azure).

**Recurso: Habilitar a proteção do Azure Site Recovery**

* **O que ele faz**: o Provedor do Azure Site Recovery instalado no servidor VMM é o canal de comunicação com o Serviço. O Provedor é uma DLL (biblioteca de vínculo dinâmico) hospedada no processo do VMM. Depois que o Provedor é instalado, o recurso "Recuperação do Data Center" é habilitado no console do administrador do VMM. Máquinas virtuais novas ou existentes em uma nuvem podem habilitar uma propriedade chamada "Recuperação do Data Center" para ajudar a proteger a máquina virtual. Quando essa propriedade é definida, o Provedor envia o nome e a ID da máquina virtual ao Serviço. A proteção virtual é habilitada pela tecnologia de replicação do Hyper-V do Windows Server 2012 ou Windows Server 2012 R2. Os dados da máquina virtual são replicados de um host Hyper-V para outro (normalmente localizado em um data center de "recuperação" diferente).
* **Informações coletadas**: o Serviço coleta, processa e transmite metadados para a máquina virtual, que inclui o nome, a ID, a rede virtual e o nome da nuvem à qual ele pertence.
* **Uso das informações**: o Serviço usa as informações acima para popular as informações da máquina virtual no portal do Serviço.
* **Escolha**: essa é uma parte essencial do serviço e não pode ser desativada. Se não quiser que essas informações sejam enviadas ao serviço, não habilite a proteção do Azure Site Recovery para máquinas virtuais. Observe que todos os dados enviados pelo Provedor ao Serviço são enviados via HTTPS.

**Recurso: Plano de recuperação**

* **O que ele faz**: esse recurso ajuda você a criar um plano de orquestração para o datacenter de “recuperação”. Você pode definir a ordem na qual as máquinas virtuais ou um grupo de máquinas virtuais devem ser iniciados no local de recuperação. Você também pode especificar scripts automatizados para execução ou qualquer ação manual a ser executada no momento da recuperação para cada máquina virtual. O failover (abordado na próxima seção) costuma ser disparado no nível do Plano de Recuperação para a recuperação coordenada.
* **Informações coletadas**: o Serviço coleta, processa e transmite metadados para o plano de recuperação, incluindo metadados de máquina virtual e metadados de scripts de automação e anotações de ações manuais.
* **Uso das informações**: os metadados descritos acima são usados para criar o plano de recuperação no portal do Serviço.
* **Escolha**: essa é uma parte essencial do serviço e não pode ser desativada. Se não quiser que essas informações sejam enviadas ao serviço, não crie Planos de Recuperação nesse Serviço.

**Recurso: Mapeamento de rede**

* **O que ele faz**: esse recurso permite mapear as informações de rede do datacenter principal para o datacenter de recuperação. Quando as máquinas virtuais são recuperadas no site de recuperação, esse mapeamento ajuda a estabelecer a conectividade de rede para elas.
* **Informações coletadas**: como parte do recurso de mapeamento de rede, o Serviço coleta, processa e transmite os metadados das redes lógicas para cada site (primário e datacenter).
* **Uso de informações**: o Serviço usa os metadados para popular o portal do Serviço, em que você pode mapear as informações de rede.
* **Escolha**: essa é uma parte essencial do Serviço e não pode ser desativada. Se não quiser que essas informações sejam enviadas ao Serviço, não use o recurso de mapeamento de rede.

**Recurso: Failover — planejado, não planejado, teste**

* **O que ele faz**: esse recurso ajuda o failover de uma máquina virtual de um datacenter gerenciado por VMM para outro datacenter gerenciado por VMM. A ação de failover é disparada pelo usuário em seu portal do Serviço. As possíveis razões para um failover incluem um evento não planejado (por exemplo, no caso de desastre natural); um evento planejado (por exemplo, o balanceamento de carga do data center); um failover de teste (por exemplo, um ensaio de plano de recuperação).

O Provedor no servidor VMM é notificado do evento pelo Serviço e executa uma ação de failover no host Hyper-V por meio das interfaces do VMM. O failover real da máquina virtual de um host Hyper-V para outro (normalmente em execução em um data center de "recuperação" diferente) é tratado pela tecnologia de replicação do Hyper-V do Windows Server 2012 ou Windows Server 2012 R2. Depois que o failover for concluído, o Provedor instalado no servidor VMM do data center de "recuperação" enviará as informações de êxito ao serviço.

* **Informações coletadas**: o Serviço usa as informações acima para popular o status das informações de ação de failover no portal do Serviço.
* **Uso de informações**: o Serviço usa as informações acima do modo descrito a seguir:

  * Certificado de gerenciamento: usado para ajudar a identificar e autenticar o servidor VMM registrado para acessar o Serviço. O Serviço usa a parte da chave pública do certificado para proteger um token que somente o servidor VMM registrado pode acessar. O servidor precisa usar esse token para obter acesso aos recursos do Serviço.
  * Nome do servidor VMM: o nome do servidor VMM é necessário para identificar e se comunicar com o servidor VMM apropriado no qual as nuvens estão localizadas.
  * Nomes de nuvem do servidor VMM: o nome de nuvem é necessário ao se usar o recurso de emparelhamento/desemparelhamento da nuvem do Serviço descrito abaixo. Quando você decide emparelhar sua nuvem de um data center primário com outra nuvem no data center de recuperação, os nomes de todas as nuvens do data center de recuperação são apresentados.
* **Escolha**: essa é uma parte essencial do serviço e não pode ser desativada. Se não quiser que essas informações sejam enviadas ao Serviço, não use esse Serviço.

## <a name="next-steps"></a>Próximas etapas
Depois de executar um failover de teste para verificar se o seu ambiente está funcionando conforme o esperado, [saiba mais sobre](site-recovery-failover.md) os diferentes tipos de failover.
