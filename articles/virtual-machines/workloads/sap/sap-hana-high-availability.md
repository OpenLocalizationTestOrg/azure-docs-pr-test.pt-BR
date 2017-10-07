---
title: "aaaHigh disponibilidade do SAP HANA em máquinas virtuais do Azure (VMs) | Microsoft Docs"
description: "Estabeleça alta disponibilidade do SAP HANA em VMs (máquinas virtuais) do Azure."
services: virtual-machines-linux
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: sedusch
ms.openlocfilehash: dcb9bb70594f9d97f8a888cec76300bcbe0bf1ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-sap-hana-on-azure-virtual-machines-vms"></a>Alta disponibilidade do SAP HANA em VMs (máquinas virtuais) do Azure

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

[2205917]:https://launchpad.support.sap.com/#/notes/2205917
[1944799]:https://launchpad.support.sap.com/#/notes/1944799
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351

[hana-ha-guide-replication]:sap-hana-high-availability.md#14c19f65-b5aa-4856-9594-b81c7e4df73d
[hana-ha-guide-shared-storage]:sap-hana-high-availability.md#498de331-fa04-490b-997c-b078de457c9d

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[sap-swcenter]:https://launchpad.support.sap.com/#/softwarecenter
[template-multisid-db]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged%2Fazuredeploy.json

No local, você pode usar a replicação de sistema HANA ou usar o armazenamento compartilhado tooestablish alta disponibilidade para o SAP HANA.
Atualmente, damos suporte apenas à configuração da Replicação do Sistema HANA no Azure. A Replicação do Sistema HANA consiste em um nó mestre e, pelo menos, um nó subordinado. Alterações toohello dados no nó mestre Olá são replicados nós de subordinado toohello forma síncrona ou assíncrona.

Este artigo descreve como máquinas virtuais do toodeploy Olá, configurar máquinas virtuais de hello, instalar o framework de cluster hello, instalar e configurar a replicação de sistema do SAP HANA.
Em configurações de exemplo hello, número da instância etc. 03 de comandos de instalação e HANA HDB de ID de sistema é usado.

Saudação de leitura a seguir observações sobre o SAP e documentos primeiro

* A Nota SAP [1928533], que tem:
  * Lista de tamanhos de VM do Azure que têm suporte para implantação de saudação do software SAP
  * Informações importantes sobre capacidade para tamanhos de VM do Azure
  * Software SAP e combinações de SO (sistema operacional) e banco de dados com suporte
  * A versão do kernel do SAP necessária para Windows e para Linux no Microsoft Azure
* A Nota SAP [2015553] lista pré-requisitos para implantações de software SAP com suporte do SAP no Azure.
* A Nota SAP [2205917] tem configurações de SO recomendadas para SUSE Linux Enterprise Server para aplicativos SAP
* A Nota SAP [1944799] tem Diretrizes SAP HANA para SUSE Linux Enterprise Server para aplicativos SAP
* A Nota SAP [2178632] contém informações detalhadas sobre todas as métricas de monitoramentos relatadas para o SAP no Azure.
* Nota da SAP [2191498] Olá exigiu versão SAP Host Agent para Linux no Azure.
* A Nota SAP [2243692] tem informações sobre o licenciamento do SAP no Linux no Azure.
* A Nota SAP [1984787] tem informações gerais sobre o SUSE Linux Enterprise Server 12.
* Nota da SAP [1999351] tem informações adicionais de solução de problemas para hello Azure extensão de monitoramento aprimorada para SAP.
* [WIKI da comunidade do SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) tem todas as Notas SAP necessárias para Linux.
* [Planejamento e implementação de Máquinas Virtuais do Azure para SAP no Linux][planning-guide]
* [Implantação de máquinas virtuais do Azure para SAP no Linux (este artigo)][deployment-guide]
* [Implantação de Máquinas Virtuais do Azure do DBMS para SAP no Linux][dbms-guide]
* [Cenário de otimização de desempenho do SAP HANA SR] [ suse-hana-ha-guide] guia Olá contém tooset de todas as informações necessárias a replicação de sistema do SAP HANA local. Use este guia como uma linha de base.

## <a name="deploying-linux"></a>Implantação do Linux

Agente de recurso Olá para o SAP HANA está incluído no SUSE Linux Enterprise Server para aplicativos SAP.
Hello Azure Marketplace contém uma imagem para SUSE Linux Enterprise Server para 12 de aplicativos SAP com BYOS (Traga sua própria assinatura) que você pode usar máquinas virtuais da nova toodeploy.

### <a name="manual-deployment"></a>Implantação manual

1. Criar um grupo de recursos
1. Criar uma rede virtual
1. Crie duas Contas de Armazenamento
1. Crie um Conjunto de Disponibilidade  
   Defina o máximo de domínio de atualização
1. Crie um Balanceador de Carga (interno)  
   Selecione a VNET da etapa acima
1. Crie a Máquina Virtual 1  
   https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1  
   SLES For SAP Applications 12 SP1 (BYOS)  
   Escolha a Conta de Armazenamento 1  
   Escolha o Conjunto de Disponibilidade  
1. Crie a Máquina Virtual 2  
   https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1  
   SLES For SAP Applications 12 SP1 (BYOS)  
   Escolha a Conta de Armazenamento 2   
   Escolha o Conjunto de Disponibilidade  
1. Adicione Discos de Dados
1. Configure o balanceador de carga Olá
    1. Crie um pool de IPs de front-end
        1. Abra o balanceador de carga hello, selecione o pool IP de front-end e clique em Adicionar
        1. Digite nome Olá Olá novo front-end do pool de IP (por exemplo hana-front-end)
       1. Clique em OK
        1. Depois que o novo pool IP de front-end Olá é criado, anote o endereço IP
    1. Crie um pool de back-end
        1. Abra o balanceador de carga hello, selecione os pools de back-end e clique em Adicionar
        1. Insira nome de saudação do pool de back-end novo hello (por exemplo hana-back-end)
        1. Clique em Adicionar uma máquina virtual
        1. Selecione Olá criado anteriormente do conjunto de disponibilidade
        1. Selecione as máquinas virtuais de saudação do cluster do SAP HANA Olá
        1. Clique em OK
    1. Criar uma investigação de integridade
       1. Abra o balanceador de carga hello, selecione investigações de integridade e clique em Adicionar
        1. Insira o nome de saudação do teste de integridade novo hello (por exemplo, hana-hp)
        1. Escolha TCP como protocolo, porta 625**03**, mantenha o Intervalo como 5 e o Limite de não integridade como 2
        1. Clique em OK
    1. Criar regras de balanceamento de carga
        1. Abra o balanceador de carga hello, selecione as regras de balanceamento de carga e clique em Adicionar
        1. Insira nome de saudação da nova regra de Balanceador de carga hello (por exemplo hana-lb-3**03**15)
        1. Endereço IP de front-end Select hello, pool de back-end e integridade teste que você criou anteriormente (por exemplo hana-front-end)
        1. Mantenha o protocolo TCP, insira a porta 3**03**15
        1. Aumentar o tempo limite de ociosidade too30 minutos
       1. **Certifique-se de que tooenable IP flutuante**
        1. Clique em OK
        1. Repita as etapas de saudação acima para a porta 3**03**17

### <a name="deploy-with-template"></a>Implantar com modelo
Você pode usar um dos modelos de início rápido de saudação no github toodeploy todos os recursos necessários. modelo de saudação implanta máquinas virtuais de saudação, o balanceador de carga hello, disponibilidade definida etc. Siga o modelo de saudação de toodeploy essas etapas:

1. Olá abrir [modelo de banco de dados] [ template-multisid-db] ou hello [convergido modelo] [ template-converged] em Olá Portal de modelo de banco de dados de saudação só cria Olá regras de balanceamento de carga para um banco de dados enquanto também cria um modelo convergida Olá Olá regras de balanceamento de carga para um ASCS/SCS e uma instância de ES (Linux). Se você planejar tooinstall um sistema baseados no SAP NetWeaver e deseja também tooinstall Olá ASCS/SCS de instância em Olá mesmo máquinas, use Olá [convergido modelo][template-converged].
1. Digite hello parâmetros a seguir
    1. ID do sistema SAP  
       Insira o sistema SAP de hello, Id de saudação sistema SAP que você deseja tooinstall. Olá Id será usado como um prefixo para recursos de saudação que são implantados.
    1. Tipo de pilha (aplicável somente se você usar o modelo convergida Olá)  
       Selecione o tipo de pilha do SAP NetWeaver Olá
    1. Tipo de sistema operacional  
       Selecione uma saudação distribuições do Linux. Para este exemplo, selecione SLES 12 BYOS
    1. Tipo de banco de dados  
       Selecionar HANA
    1. Tamanho do sistema SAP  
       quantidade de saudação do sistema novo do SAPS Olá fornecerá. Se não tiver certeza do sistema de saudação SAPS quantos exigirá, peça ao seu parceiro de tecnologia do SAP ou o integrador de sistema
    1. Disponibilidade do sistema  
       Selecione HA
    1. Nome de Usuário de Administrador e Senha do Administrador  
       Um novo usuário é criado que pode ser usado toolog toohello máquina.
    1. Sub-rede Nova ou Existente  
       Determina se uma nova rede virtual e sub-rede devem ser criadas ou se uma sub-rede existente deve ser usada. Se você já tiver uma rede virtual que é a rede de local tooyour conectado, selecione existente.
    1. ID da Sub-rede  
    Olá ID das máquinas virtuais do hello sub-rede toowhich Olá deve ser conectado ao. Selecione a sub-rede de saudação de sua VPN ou rota expressa rede virtual tooconnect Olá máquina virtual tooyour na rede local. Olá ID geralmente parece com /subscriptions/`<subscription id`> /resourceGroups/`<resource group name`> /providers/Microsoft.Network/virtualNetworks/`<virtual network name`> /subnets/`<subnet name`>

## <a name="setting-up-linux-ha"></a>Configuração de HA do Linux

Olá itens a seguir é prefixado com um [A] - nós tooall aplicável, [1] toonode aplicável somente - aplicável apenas toonode [2] ou 1 - 2.

1. [A] SLES para SAP BYOS somente - repositórios de saudação do SLES registrar toobe toouse capaz
1. [A] Apenas SLES for SAP BYOS – adicione o módulo de nuvem pública
1. [A] Atualize o SLES
    ```bash
    sudo zypper update

    ```

1. [1] Habilite o acesso ssh
    ```bash
    sudo ssh-keygen -tdsa
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key
    sudo cat /root/.ssh/id_dsa.pub
    ```

2. [2] Habilite o acesso ssh
    ```bash
    sudo ssh-keygen -tdsa

    # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
    sudo vi /root/.ssh/authorized_keys
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key    
    sudo cat /root/.ssh/id_dsa.pub
    ```

1. [1] Habilite o acesso ssh
    ```bash
    # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
    sudo vi /root/.ssh/authorized_keys
    
    ```

1. [A] Instale a extensão HA
    ```bash
    sudo zypper install sle-ha-release fence-agents
    
    ```

1. [A] Configure o layout do disco
    1. LVM  
    Geralmente, é recomendável toouse LVM para volumes que armazenam dados e arquivos de log. Olá exemplo a seguir supõe que máquinas virtuais de saudação tiver quatro discos de dados anexados que devem ser usado toocreate dois volumes.
        * Crie volumes físicos de todos os discos que você deseja toouse.
    <pre><code>
    sudo pvcreate /dev/sdc
    sudo pvcreate /dev/sdd
    sudo pvcreate /dev/sde
    sudo pvcreate /dev/sdf
    </code></pre>
        * Criar um grupo de volumes para arquivos de dados hello, um grupo de volumes para arquivos de log hello e um diretório compartilhado de saudação do SAP HANA
    <pre><code>
    sudo vgcreate vg_hana_data /dev/sdc /dev/sdd
    sudo vgcreate vg_hana_log /dev/sde
    sudo vgcreate vg_hana_shared /dev/sdf
    </code></pre>
        * Criar hello volumes lógicos
    <pre><code>
    sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
    sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
    sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
    sudo mkfs.xfs /dev/vg_hana_data/hana_data
    sudo mkfs.xfs /dev/vg_hana_log/hana_log
    sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
    </code></pre>
        * Criar diretórios de montagem hello e copie Olá UUID de todos os volumes lógicos
    <pre><code>
    sudo mkdir -p /hana/data
    sudo mkdir -p /hana/log
    sudo mkdir -p /hana/shared
    # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
    sudo blkid
    </code></pre>
        * Crie entradas de fstab para Olá três volumes lógicos
    <pre><code>
    sudo vi /etc/fstab
    </code></pre>
    Inserir essa linha muito/etc/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b> /hana/data xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b> /hana/log xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b> /hana/shared xfs  defaults,nofail  0  2
    </code></pre>
        * Montar Olá novos volumes
    <pre><code>
    sudo mount -a
    </code></pre>
    1. Discos simples  
       Para sistemas pequenos ou de demonstração, você pode colocar os arquivos de log e dados do HANA em um disco. Olá comandos a seguir criar uma partição em /dev/sdc e formate-o com xfs.
    ```bash
    sudo fdisk /dev/sdc
    sudo mkfs.xfs /dev/sdc1
    
    # <a name="write-down-hello-id-of-devsdc1"></a>Anote a id de saudação do /dev/sdc1
    sudo /sbin/blkid  sudo vi /etc/fstab
    ```

    Insert this line too/etc/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID&gt;</b> /hana xfs  defaults,nofail  0  2
    </code></pre>

    Create hello target directory and mount hello disk.

    ```bash
    sudo mkdir /hana
    sudo mount -a
    ```

1. [A] Configure a resolução de nome do host para todos os hosts  
    Você pode usar um servidor DNS ou modificar /etc/hosts Olá em todos os nós. Este exemplo mostra como toouse Olá arquivo /etc/hosts.
   Substituir endereço IP de saudação e nome de host Olá no hello comandos a seguir
    ```bash
    sudo vi /etc/hosts
    ```
    Inserir saudação linhas muito/etc/hosts a seguir. Alterar o ambiente de saudação IP toomatch de endereço e o nome do host    
    
    <pre><code>
    <b>&lt;IP address of host 1&gt; &lt;hostname of host 1&gt;</b>
    <b>&lt;IP address of host 2&gt; &lt;hostname of host 2&gt;</b>
    </code></pre>

1. [1] Instale o Cluster
    ```bash
    sudo ha-cluster-init
    
    # Do you want toocontinue anyway? [y/N] -> y
    # Network address toobind too(e.g.: 192.168.1.0) [10.79.227.0] -> ENTER
    # Multicast address (e.g.: 239.x.x.x) [239.174.218.125] -> ENTER
    # Multicast port [5405] -> ENTER
    # Do you wish toouse SBD? [y/N] -> N
    # Do you wish tooconfigure an administration IP? [y/N] -> N
    ```
        
1. [2] adicionar nó toocluster
    ```bash
    sudo ha-cluster-join
        
    # WARNING: NTP is not configured toostart at system boot.
    # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
    # Do you want toocontinue anyway? [y/N] -> y
    # IP address or hostname of existing node (e.g.: 192.168.1.1) [] -> IP address of node 1 e.g. 10.0.0.5
    # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
    ```

1. [A] alteração hacluster senha toohello mesma senha
    ```bash
    sudo passwd hacluster
    
    ```

1. [A] configurar corosync toouse outro transporte e adicionar nodelist. Caso contrário, o cluster não funcionará.
    ```bash
    sudo vi /etc/corosync/corosync.conf    
    
    ```

    Adicione Olá negrito toohello conteúdo de arquivo a seguir.
    
    <pre><code> 
    [...]
      interface { 
          [...] 
      }
      <b>transport:      udpu</b>
    } 
    <b>nodelist {
      node {
        ring0_addr:     < ip address of node 1 >
      }
      node {
        ring0_addr:     < ip address of node 2 > 
      } 
    }</b>
    logging {
      [...]
    </code></pre>

    Em seguida, reinicie o serviço de corosync Olá

    ```bash
    sudo service corosync restart
    
    ```

1. [A] Instale os pacotes HANA HA  
    ```bash
    sudo zypper install SAPHanaSR
    
    ```

## <a name="installing-sap-hana"></a>Instalando o SAP HANA

Siga o capítulo 4 de saudação [guia de cenário de otimização de desempenho do SAP HANA SR] [ suse-hana-ha-guide] tooinstall replicação de sistema do SAP HANA.

1. [A] executar hdblcm Olá HANA DVD
    * Escolha instalação -> 1
    * Selecione os componentes adicionais para instalação -> 1
    * Insira o caminho de instalação [/hana/shared]: -> ENTER
    * Insira o Nome do Host Local [..]: -> ENTER
    * Você deseja que o sistema de toohello tooadd hosts adicionais? (s/n) [n]: -> ENTER
    * Insira a ID do Sistema SAP HANA: <SID of HANA e.g. HDB>
    * Insira o Número da Instância [00]:   
  Número da instância do HANA. Use 03 se usado Olá modelo do Azure ou seguido exemplo hello acima
    * Selecione Modo de Banco de Dados/Inserir Índice [1]: -> ENTER
    * Selecione o Uso do Sistema/Inserir Índice [4]:  
  Selecione o sistema de saudação uso
    * Informe o Local dos Volumes de Dados [/data/hana/HDB]: -> ENTER
    * Informe o Local dos Volumes de Log [/hana/log/HDB]: -> ENTER
    * Restringir a alocação máxima de memória? [n]: -> ENTER
    * Insira o nome de Host do certificado para o Host '...' [...]: -> ENTER
    * Insira a Senha de Usuário do Agente do Host SAP (sapadm):
    * Confirme a Senha de Usuário do Agente do Host SAP (sapadm):
    * Insira a Senha do Administrador de Sistema (hdbadm):
    * Confirme a Senha do Administrador de Sistema (hdbadm):
    * Insira o Diretório Base do Administrador de Sistema [/usr/sap/HDB/home]: -> ENTER
    * Insira o Shell de Logon do Administrador de Sistema [/bin/sh]: -> ENTER
    * Insira a ID de Usuário do Administrador de Sistema [1001]: -> ENTER
    * Insira a ID do Grupo de Usuários (sapsys) [79]: -> ENTER
    * Insira a Senha de Usuário do Banco de Dados (SYSTEM):
    * Confirme a Senha de Usuário do Banco de Dados (SYSTEM):
    * Reiniciar o sistema após a reinicialização do computador? [n]: -> ENTER
    * Você deseja toocontinue? (s/n):  
  Validar Olá resumo e digite y toocontinue
1. [A] Atualize o Agente do Host do SAP  
  Baixe o arquivo de SAP Host Agent mais recente de saudação do hello [SAP Softwarecenter] [ sap-swcenter] e execução hello comando tooupgrade Olá agente a seguir. Substitua saudação caminho toohello toopoint toohello arquivo baixado.
    ```bash
    sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <path tooSAP Host Agent SAR>
    ```

1. [1] Crie uma replicação HANA (como raiz)  
    Execute Olá comando a seguir. Verifique se tooreplace negrito cadeias de caracteres (HANA HDB de ID de sistema e instância número 03) com valores de saudação da instalação do SAP HANA.
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
    hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
    hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
    </code></pre>

1. [A] Criar entrada de repositório de chaves (como raiz)
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>passwd</b>
    </code></pre>
1. [1] Faça o backup do banco de dados backup (como raiz)
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
    </code></pre>
1. [1] alterne toohello sapsid usuário (por exemplo, hdbadm) e criar o site primário hello.
    <pre><code>
    su - <b>hdb</b>adm
    hdbnsutil -sr_enable –-name=<b>SITE1</b>
    </code></pre>
1. [2] alterne toohello sapsid usuário (por exemplo, hdbadm) e criar site secundário hello.
    <pre><code>
    su - <b>hdb</b>adm
    sapcontrol -nr <b>03</b> -function StopWait 600 10
    hdbnsutil -sr_register --remoteHost=<b>saphanavm1</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
    </code></pre>

## <a name="configure-cluster-framework"></a>Configurar a estrutura do cluster

Alterar as configurações padrão de saudação

<pre>
sudo vi crm-defaults.txt
# enter hello following toocrm-defaults.txt
<code>
property $id="cib-bootstrap-options" \
  no-quorum-policy="ignore" \
  stonith-enabled="true" \
  stonith-action="reboot" \
  stonith-timeout="150s"
rsc_defaults $id="rsc-options" \
  resource-stickiness="1000" \
  migration-threshold="5000"
op_defaults $id="op-options" \
  timeout="600"
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>Agora podemos carregar o cluster de toohello arquivo hello
sudo crm configure load update crm-defaults.txt
</pre>

### <a name="create-stonith-device"></a>Criar dispositivo STONITH

dispositivo STONITH Olá usa tooauthorize uma entidade de serviço no Microsoft Azure. Siga essas etapas toocreate uma entidade de serviço.

1. Vá muito<https://portal.azure.com>
1. Folha de Active Directory do Azure Olá aberto  
   Vá tooProperties e anote Olá ID de diretório. Isso é hello **id de locatário**.
1. Clique em Registros do Aplicativo
1. Clique em Adicionar
1. Digite um Nome, selecione Tipo de Aplicativo "Aplicativo Web/API", insira uma URL de logon (por exemplo, http://localhost) e clique em Criar
1. URL de entrada Hello não é usado e pode ser qualquer URL válido
1. Selecione Olá novo aplicativo e clique em chaves no guia de configurações de saudação
1. Insira uma descrição para uma nova chave, selecione "Nunca expira" e clique em Salvar
1. Anote o valor de saudação. Ele é usado como Olá **senha** para Olá entidade de serviço
1. Anote a saudação ID do aplicativo. Ele é usado como Olá username (**id de logon** nas etapas de saudação abaixo) de saudação entidade de serviço

Olá entidade de serviço não tem permissões tooaccess seus recursos do Azure por padrão. Você precisa toogive toostart de permissões de entidade de serviço de saudação e parar (desalocar) todas as máquinas virtuais do cluster hello.

1. Vá toohttps://portal.azure.com
1. Abrir Olá folha de todos os recursos
1. Selecione a máquina virtual de saudação
1. Clique em Controle de acesso (IAM)
1. Clique em Adicionar
1. Selecione a função hello proprietário
1. Insira nome de saudação do aplicativo hello criado acima
1. Clique em OK

Depois de editar permissões Olá para máquinas virtuais de hello, você pode configurar dispositivos STONITH de saudação em cluster hello.

<pre>
sudo vi crm-fencing.txt
# enter hello following toocrm-fencing.txt
# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password
<code>
primitive rsc_st_azure_1 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

primitive rsc_st_azure_2 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>Agora podemos carregar o cluster de toohello arquivo hello
sudo crm configure load update crm-fencing.txt
</pre>

### <a name="create-sap-hana-resources"></a>Criar recursos do SAP HANA

<pre>
sudo vi crm-saphanatop.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number and HANA system id
<code>
primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHanaTopology \
    operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
    op monitor interval="10" timeout="600" \
    op start interval="0" timeout="600" \
    op stop interval="0" timeout="300" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"

clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>Agora podemos carregar o cluster de toohello arquivo hello
sudo crm configure load update crm-saphanatop.txt
</pre>

<pre>
sudo vi crm-saphana.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
<code>
primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
    operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
    op start interval="0" timeout="3600" \
    op stop interval="0" timeout="3600" \
    op promote interval="0" timeout="3600" \
    op monitor interval="60" role="Master" timeout="700" \
    op monitor interval="61" role="Slave" timeout="700" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
    DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"

ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
    target-role="Started" interleave="true"

primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
    meta target-role="Started" is-managed="true" \ 
    operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
    op monitor interval="10s" timeout="20s" \ 
    params ip="<b>10.0.0.21</b>" 
primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
    params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
    op monitor timeout=20s interval=10 depth=0 
group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
 
colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  
order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>Agora podemos carregar o cluster de toohello arquivo hello
sudo crm configure load update crm-saphana.txt
</pre>

### <a name="test-cluster-setup"></a>Testar configuração do cluster
Olá capítulo a seguir descreve como você pode testar sua instalação. Cada teste pressupõe que são raiz e o mestre do SAP HANA hello está sendo executado no hello saphanavm1 de máquina virtual.

#### <a name="fencing-test"></a>Teste de isolamento

Você pode testar a instalação do agente de isolamento de saudação Olá desabilitando a interface de rede de saudação no nó saphanavm1.

<pre><code>
sudo ifdown eth0
</code></pre>

máquina virtual de saudação agora deve obter reiniciada ou interrompida, dependendo da configuração do cluster.
Se você definir Olá stonith ação toooff, máquina virtual de saudação será interrompida e recursos de saudação são migrado toohello máquina virtual em execução.

Assim que você iniciar a máquina virtual de saudação novamente, Olá recursos SAP HANA falhará toostart como secundário se você definir AUTOMATED_REGISTER = "false". Nesse caso, você precisa tooconfigure Olá HANA instância secundária executando Olá comando a seguir:

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b>

# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-manual-failover"></a>Teste de um failover manual

Você pode testar um failover manual, interrompendo o serviço de pacemaker de saudação no nó saphanavm1.
<pre><code>
service pacemaker stop
</code></pre>

Após o failover hello, você pode iniciar o serviço de saudação novamente. Olá recursos SAP HANA em saphanavm1 falhará toostart como secundário se você definir AUTOMATED_REGISTER = "false". Nesse caso, você precisa tooconfigure Olá HANA instância secundária executando Olá comando a seguir:

<pre><code>
service pacemaker start
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 


# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-migration"></a>Teste de uma migração

Você pode migrar o nó principal do SAP HANA Olá executando o comando a seguir de saudação
<pre><code>
crm resource migrate msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
crm resource migrate g_ip_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
</code></pre>

Isso deve migrar o nó mestre do SAP HANA hello e grupo Olá que contém toosaphanavm2 de endereço IP virtual hello.
Olá recursos SAP HANA em saphanavm1 falhará toostart como secundário se você definir AUTOMATED_REGISTER = "false". Nesse caso, você precisa tooconfigure Olá HANA instância secundária executando Olá comando a seguir:

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 
</code></pre>

migração de saudação cria restrições de local que precisam toobe excluída novamente.

<pre><code>
crm configure edited

# delete location contraints that are named like hello following contraint. You should have two contraints, one for hello SAP HANA resource and one for hello IP address group.
location cli-prefer-g_ip_<b>HDB</b>_HDB<b>03</b> g_ip_<b>HDB</b>_HDB<b>03</b> role=Started inf: <b>saphanavm2</b>
</code></pre>

Você também precisa toocleanup estado de saudação do recurso de nó secundário Olá

<pre><code>
# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

## <a name="next-steps"></a>Próximas etapas
* [Planejamento e implementação de Máquinas Virtuais do Azure para SAP][planning-guide]
* [Implantação de Máquinas Virtuais do Azure para SAP][deployment-guide]
* [Implantação DBMS de Máquinas Virtuais do Azure para SAP][dbms-guide]
* toolearn como tooestablish alta disponibilidade e o plano de recuperação de desastres do HANA SAP no Azure (instâncias grandes), consulte [SAP HANA (instâncias grandes) alta disponibilidade e recuperação de desastres no Azure](hana-overview-high-availability-disaster-recovery.md). 
