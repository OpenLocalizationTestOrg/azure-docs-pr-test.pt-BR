---
title: aaaHow tooinstall um servidor de destino mestre Linux para o failover de local de tooon do Azure | Microsoft Docs
description: "Antes de proteger novamente uma máquina virtual Linux, você precisa de um servidor de destino mestre do Linux. Saiba como tooinstall um."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: d7c55d115712b9862414979f89efb1f177c5f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-linux-master-target-server"></a>Instalar o servidor de destino mestre do Linux
Depois de executar o failover suas máquinas virtuais, você pode falhar Olá back máquinas virtuais toohello no site local. toofail novamente, você precisa tooreprotect Olá VM do Azure toohello no site local. Para esse processo, é necessário um tráfego de saudação de tooreceive do servidor de destino mestre local. 

Se sua máquina virtual protegida for uma máquina virtual do Windows, será necessário um destino mestre do Windows. Para uma máquina virtual Linux, é necessário um destino mestre do Linux. As etapas a seguir de saudação de leitura toolearn como toocreate e instale um Linux mestre de destino.

> [!IMPORTANT]
> A partir da versão do servidor de destino mestre Olá 9.10.0, servidor de destino mestre hello mais recente pode ser instalado de apenas em um servidor do Ubuntu 16.04. Novas instalações não são permitidas em servidores CentOS6.6. No entanto, você pode continuar tooupgrade seus servidores de destino mestre antiga usando Olá 9.10.0 versão.

## <a name="overview"></a>Visão geral
Este artigo fornece instruções sobre como a tooinstall um Linux de destino mestre.

Poste comentários ou perguntas no final da saudação deste artigo ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="prerequisites"></a>Pré-requisitos

* host de saudação toochoose qual destino mestre do hello de toodeploy, determinar se o failback Olá será toobe tooan existente na máquina virtual ou local tooa nova máquina de virtual. 
    * Para uma máquina virtual existente, host de saudação do destino mestre Olá deve ter acesso toohello repositórios de dados da máquina virtual de saudação.
    * Se a máquina virtual no local, Olá não existir, Olá failback VM é criado no hello mesmo host como um destino mestre hello. Você pode escolher qualquer host ESXi destino mestre do tooinstall hello.
* destino mestre Olá deve estar em uma rede que pode se comunicar com o servidor de processo hello e o servidor de configuração de saudação.
* versão de saudação do destino mestre Olá deve ser igual tooor anteriores a versões de saudação do servidor de processo hello e o servidor de configuração de saudação. Por exemplo, se a versão Olá saudação do servidor de configuração for 9.4, versão de saudação do destino mestre Olá pode ser 9.4 ou 9.3 mas não 9,5.
* destino mestre Olá só pode ser uma máquina virtual VMware e não um servidor físico.

## <a name="create-hello-master-target-according-toohello-sizing-guidelines"></a>Criar destino mestre hello, de acordo com toohello diretrizes de dimensionamento

Crie destino mestre de saudação conforme Olá cumprimento das diretrizes de dimensionamento:
- **RAM**: 6 GB ou mais
- **Tamanho de disco do sistema operacional**: 100 GB ou mais (tooinstall CentOS6.6)
- **Tamanho de disco adicional para a unidade de retenção**: 1 TB
- **Núcleos de CPU**: 4 núcleos ou mais

a seguir Olá suporte para Ubuntu kernels têm suporte.


|Série de Kernel  |Suporte a backup muito |
|---------|---------|
|4.4      |4.4.0-81-generic         |
|4.8      |4.8.0-56-generic         |
|4.10     |4.10.0-24-generic        |


## <a name="deploy-hello-master-target-server"></a>Implantar o servidor de destino mestre Olá

### <a name="install-ubuntu-16042-minimal"></a>Instalar o Ubuntu 16.04.2 Minimal

Levar Olá Olá etapas tooinstall Olá Ubuntu 16.04.2 64-bit operacional sistema a seguir.

**Etapa 1:** vá toohello [link de download](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) e escolha espelho mais próximo de saudação do qual baixar um ISO de 64 bits Ubuntu 16.04.2 mínimo.

Manter um ISO de 64 bits Ubuntu 16.04.2 mínimo na unidade de DVD do hello e iniciar o sistema hello.

**Etapa 2:** selecione **Inglês** como o seu Idioma de preferência e selecione **Enter**.

![Selecionar um idioma](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image1.png)

**Etapa 3:** selecione **Instalar Servidor Ubuntu** e pressione **Enter**.

![Selecionar Instalar Ubuntu Server](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image2.png)

**Etapa 4:** selecione **Inglês** como o idioma de preferência e selecione **Enter**.

![Selecionar Inglês como seu idioma preferencial](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image3.png)

**Etapa 5:** selecione Olá opção apropriada da saudação **fuso horário** lista de opções e, em seguida, selecione **Enter**.

![Selecione o fuso horário correto de saudação](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image4.png)

**Etapa 6:** selecione **não** (hello a opção padrão) e, em seguida, selecione **Enter**.


![Configurar o teclado Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image5.png)

**Etapa 7:** selecione **inglês (EUA)** como Olá país de origem para teclado hello e, em seguida, selecione **Enter**.

![Selecione EUA como país Olá de origem](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image6.png)

**Etapa 8:** selecione **inglês (EUA)** como o layout do teclado hello e selecione **Enter**.

![Selecione inglês (EUA) como o layout do teclado Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image7.png)

**Etapa 9:** insira o nome do host Olá para o servidor de saudação **Hostname** caixa e, em seguida, selecione **continuar**.

![Digite o nome de host de saudação do servidor](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image8.png)

**Etapa 10:** toocreate uma conta de usuário, insira o nome de usuário hello e, em seguida, selecione **continuar**.

![Criar uma conta do usuário](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image9.png)

**Etapa 11:** Insira senha Olá Olá nova conta de usuário e, em seguida, selecione **continuar**.

![Insira a senha de saudação](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image10.png)

**Etapa 12:** Confirmar senha Olá Olá novo usuário e, em seguida, selecione **continuar**.

![Confirmar senhas Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image11.png)

**Etapa 13:** selecione **não** (hello a opção padrão) e, em seguida, selecione **Enter**.

![Configurar usuários e senhas](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image12.png)

**Etapa 14:** se Olá fuso horário é exibido está correto, selecione **Sim** (hello a opção padrão) e, em seguida, selecione **Enter**.

tooreconfigure seu fuso horário, selecione **não**.

![Configure o relógio Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image13.png)

**Etapa 15:** Olá opções do método de particionamento, selecione **interativa - usar o disco inteiro**e, em seguida, selecione **Enter**.

![Selecione Olá opção método de particionamento](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image14.png)

**Etapa 16:** selecione Olá disco adequado de saudação **Selecionar disco toopartition** opções e, em seguida, selecione **Enter**.


![Selecione o disco Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image15.png)

**Etapa 17:** selecione **Sim** toowrite Olá toodisk de alterações e, em seguida, selecione **Enter**.

![Gravar saudação alterações toodisk](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image16.png)

**Etapa 18:** selecione a opção padrão de saudação, selecione **continuar**e, em seguida, selecione **Enter**.

![Selecione a opção padrão de saudação](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image17.png)

**Etapa 19:** selecione a opção apropriada Olá para gerenciar atualizações em seu sistema e, em seguida, selecione **Enter**.

![Selecione como as atualizações toomanage](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image18.png)

> [!WARNING]
> Porque o servidor de destino mestre do Azure Site Recovery Olá requer uma versão muito específica de saudação Ubuntu, é necessário tooensure que kernel Olá atualizações estão desabilitadas para a máquina virtual de saudação. Se eles estiverem habilitados, todas as atualizações regulares causam Olá toomalfunction de servidor de destino mestre. Verifique se você selecionou Olá **não existem atualizações automáticas** opção.


**Etapa 20:** selecione as opções padrão. Se você desejar openSSH para conexão SSH, selecione Olá **OpenSSH servidor** opção e, em seguida, selecione **continuar**.

![Selecionar o software](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image19.png)

**Etapa 21:** selecione **Sim**e selecione **Enter**.

![Carregador de inicialização GRUB instalação Olá](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image20.png)

**Etapa 22:** selecione Olá dispositivo apropriado para a instalação do carregador de inicialização hello (preferencialmente **/desenvolvimento/sda**) e, em seguida, selecione **Enter**.

![Selecionar um dispositivo para a instalação do carregador de inicialização](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image21.png)

**Etapa 23:** selecione **continuar**e, em seguida, selecione **Enter** toofinish instalação de saudação.

![Concluir a instalação de saudação](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image22.png)

Após instalação hello, entre toohello VM com novas credenciais de usuário hello. (Consulte muito**etapa 10** para obter mais informações.)

Etapas Olá Olá Olá tooset de captura de tela raiz a seguir descritas senha do usuário. Faça logon como usuário raiz.

![Senha de usuário do conjunto Olá raiz](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image23.png)


### <a name="prepare-hello-machine-for-configuration-as-a-master-target-server"></a>Preparar o computador de saudação para a configuração como um servidor de destino mestre
Em seguida, prepare o computador de saudação para a configuração como um servidor de destino mestre.

tooget Olá ID para cada disco SCSI em uma máquina virtual Linux, habilitar Olá **em disco. EnableUUID = TRUE** parâmetro.

tooenable esse parâmetro, Olá take seguindo as etapas:

1. Desligue sua máquina virtual.

2. Entrada Olá para a máquina virtual de saudação no painel esquerdo do hello e, em seguida, selecione **editar configurações de**.

3. Selecione Olá **opções** guia.

4. No painel esquerdo do hello, selecione **avançado** > **geral**e, em seguida, selecione Olá **parâmetros de configuração** botão na parte inferior direita Olá tela hello.

    ![Guia Opções](./media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    Olá **parâmetros de configuração** opção não está disponível quando a saudação máquina está em execução. toomake este guia ativa, desligar máquina virtual de saudação.

5. Verifique se já existe uma linha com **disk.EnableUUID**.

    - Se o valor de saudação existe e está definido muito**False**, altere o valor de saudação muito**True**. (os valores hello não diferenciam maiusculas de minúsculas).

    - Se o valor de saudação existe e está definido muito**True**, selecione **Cancelar**.

    - Se o valor de saudação não existir, selecione **Adicionar linha**.

    - Na coluna de nome hello, adicionar **em disco. EnableUUID**e, em seguida, defina o valor de saudação muito**TRUE**.

    ![Verificação se disk.EnableUUID já existe](./media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="disable-kernel-upgrades"></a>Desabilitar atualizações de kernel

Servidor de destino mestre do Azure Site Recovery requer uma versão muito específica de saudação Ubuntu, verifique se as atualizações de kernel Olá estão desabilitadas para a máquina virtual de saudação.

Se as atualizações de kernel estiverem habilitadas, todas as atualizações regulares causam Olá toomalfunction de servidor de destino mestre.

#### <a name="download-and-install-additional-packages"></a>Baixar e instalar pacotes adicionais

> [!NOTE]
> Certifique-se de que você tenha toodownload de conectividade de Internet e instala outros pacotes. Se você não tiver conectividade com a Internet, será necessário toomanually localizar esses pacotes RPM e instalá-los.

```
apt-get install -y multipath-tools lsscsi python-pyasn1 lvm2 kpartx
```

### <a name="get-hello-installer-for-setup"></a>Obter o instalador Olá para instalação

Se o destino mestre tem conectividade com a Internet, você pode usar o hello instalador de saudação do toodownload as etapas a seguir. Caso contrário, você pode copiar o instalador Olá saudação do servidor de processo e instalá-lo.

#### <a name="download-hello-master-target-installation-packages"></a>Baixe os pacotes de instalação de destino mestre Olá

[Fazer o download de bits de instalação de destino mestre do hello mais recentes Linux](https://aka.ms/latestlinuxmobsvc).

toodownload usando o Linux, tipo:

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

Certifique-se de que você baixe e descompacte o instalador de saudação em seu diretório base. Se você descompactar muito**usr/Local**, Olá instalação falhará.


#### <a name="access-hello-installer-from-hello-process-server"></a>Instalador de saudação do acesso saudação do servidor de processo

1. No servidor de processo hello, ir muito**C:\Program Files (x86) \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.

2. Copie o arquivo de instalador necessário de saudação saudação do servidor de processo e salve-o como **latestlinuxmobsvc.tar.gz** em seu diretório base.


### <a name="apply-custom-configuration-changes"></a>Aplicar alterações de configuração personalizadas

alterações de configuração personalizada tooapply, Olá use as etapas a seguir:


1. Execute Olá binário de saudação do comando toountar a seguir.
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![Captura de tela da saudação comando toorun](./media/site-recovery-how-to-install-linux-master-target/image16.png)

2. Execute Olá toogive permissão a seguir.
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. Olá executar script do comando toorun Olá a seguir.
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> Execute o script de saudação apenas uma vez no servidor de saudação. Desligar o servidor de saudação. Reinicie o servidor de saudação, em seguida, depois de adicionar um disco, conforme descrito na próxima seção, Olá.

### <a name="add-a-retention-disk-toohello-linux-master-target-virtual-machine"></a>Adicionar uma máquina virtual retenção disco toohello Linux destino mestre

Use Olá etapas toocreate um disco de retenção a seguir:

1. Anexar uma novo disco de 1 TB toohello Linux mestre máquina virtual de destino e, em seguida, inicie a máquina de saudação.

2. Saudação de uso **multipath -ll** toolearn Olá multipath ID do disco de retenção de saudação do comando.

    ```
    multipath -ll
    ```
    ![Olá ID de vários caminhos de disco de retenção Olá](./media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. Formatar a unidade hello e, em seguida, criar um sistema de arquivos na unidade de novo hello.

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![Criando um sistema de arquivos na unidade de saudação](./media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. Depois de criar o sistema de arquivos hello, monte o disco de retenção de saudação.
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```
    ![Disco de retenção de saudação de montagem](./media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. Criar hello **fstab** entrada toomount Olá unidade de retenção sempre Olá sistema é iniciado.
    ```
    vi /etc/fstab
    ```
    Selecione **inserir** toobegin editando o arquivo hello. Criar uma nova linha e insira Olá texto a seguir. Edite ID vários caminhos do disco Olá com base na ID de vários caminhos Olá realçado do comando anterior hello.

    **/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**

    Selecione **Esc**e, em seguida, digite **: wq** (gravação e sair) tooclose janela do editor de saudação.

### <a name="install-hello-master-target"></a>Instalar o destino mestre Olá

> [!IMPORTANT]
> versão de Olá Olá mestre do servidor de destino deve ser igual tooor anteriores a versões de saudação do servidor de processo hello e o servidor de configuração de saudação. Se essa condição não for atendida, o proteger novamente terá êxito, mas a replicação falhará.


> [!NOTE]
> Antes de instalar o servidor de destino mestre hello, verifique que Olá **/etc/hosts** arquivo na máquina virtual de saudação contém entradas que mapeiam Olá nome do host local toohello endereços IP associados a todos os adaptadores de rede.

1. Copiar senha de saudação do **C:\ProgramData\Microsoft do Azure Site Recovery\private\connection.passphrase** no servidor de configuração de saudação. Em seguida, salve-o como **passphrase.txt** em Olá mesmo diretório local executando Olá comando a seguir:

    ```
    echo <passphrase> >passphrase.txt
    ```
    Exemplo: 
    
    ```
    echo itUx70I47uxDuUVY >passphrase.txt
    ```

2. Observe o endereço IP do servidor de configuração de saudação. Ele é necessário na próxima etapa do hello.

3. Executar Olá após o servidor de destino mestre do comando tooinstall hello e registre o servidor de saudação com o servidor de configuração de saudação.

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```

    Exemplo: 
    
    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

    Aguarde até que o script hello termina. Se o destino mestre Olá registra com êxito, destino mestre hello está listado no hello **infra-estrutura de recuperação de Site** página do portal de saudação.


#### <a name="install-hello-master-target-by-using-interactive-installation"></a>Instalar o destino mestre hello usando a instalação interativa

1. Execute Olá destino mestre do comando tooinstall Olá a seguir. Para função de agente hello, escolha **destino mestre**.

    ```
    ./install
    ```

2. Escolha saudação padrão local para a instalação e, em seguida, selecione **Enter** toocontinue.

    ![Escolher um local padrão para a instalação de destino mestre](./media/site-recovery-how-to-install-linux-master-target/image17.png)

Após instalação hello, registre o servidor de configuração de saudação usando a linha de comando hello.

1. Anote o endereço IP de saudação saudação do servidor de configuração. Ele é necessário na próxima etapa do hello.

2. Executar Olá após o servidor de destino mestre do comando tooinstall hello e registre o servidor de saudação com o servidor de configuração de saudação.

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```
    Exemplo: 

    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

   Aguarde até que o script hello termina. Se o destino mestre Olá é com êxito registrado, destino mestre hello está listado no hello **infra-estrutura de recuperação de Site** página do portal de saudação.


### <a name="upgrade-hello-master-target"></a>Atualizar o destino mestre Olá

Execute o instalador de saudação. Detecta automaticamente que o agente hello está instalado no destino mestre hello. tooupgrade, selecione **Y**.  Olá após a instalação for concluída, verifique a versão de saudação do destino mestre hello, instalado usando o comando a seguir de saudação.

    ```
    cat /usr/local/.vx_version
    ```

Você pode ver que Olá **versão** campo retorna o número de versão de saudação do destino mestre hello.

### <a name="install-vmware-tools-on-hello-master-target-server"></a>Instalar as ferramentas do VMware no servidor de destino mestre Olá

É necessário tooinstall as ferramentas do VMware no destino mestre Olá para que ele possa descobrir Olá armazenamentos de dados. Se as ferramentas de saudação não são instaladas, tela de nova proteção hello não está listada na Olá armazenamentos de dados. Após a instalação das ferramentas do VMware Olá, é necessário toorestart.

## <a name="next-steps"></a>Próximas etapas
Instalação hello e o registro do destino mestre Olá finsihed, após você pode ver destino mestre Olá em Olá **destino mestre** seção **infra-estrutura de recuperação de Site**, sob Olá Visão geral de servidor de configuração.

Você pode prosseguir com a [nova proteção](site-recovery-how-to-reprotect.md), seguida pelo failback.

## <a name="common-issues"></a>Problemas comuns

* Não ative Storage vMotion em quaisquer componentes de gerenciamento como um destino mestre. Se o destino mestre Olá move após uma nova proteção bem-sucedida, os discos da máquina virtual hello (VMDKs) não podem ser desanexados. Nesse caso, o failback falhará.

* destino mestre Olá não deve ter todos os instantâneos na máquina virtual de saudação. Se houver instantâneos, o failback falhará.

* Devido a toosome configurações de NIC personalizadas em alguns clientes, Olá a interface de rede está desabilitada durante a inicialização e não é possível inicializar o agente de destino mestre Olá. Certifique-se de que Olá propriedades a seguir estão definidas corretamente. Verificar essas propriedades no hello Ethernet /etc/sysconfig/network-scripts/ifcfg do arquivo de cartão-eth *.
    * BOOTPROTO=dhcp
    * ONBOOT=yes
