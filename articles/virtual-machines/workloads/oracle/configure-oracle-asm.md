---
title: "aaaSet backup Oracle ASM em uma máquina virtual de Linux do Azure | Microsoft Docs"
description: Coloque o Oracle ASM em funcionamento rapidamente no ambiente do Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/19/2017
ms.author: rclaus
ms.openlocfilehash: d6a7046638e919876477d46943faabcb1872acac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-oracle-asm-on-an-azure-linux-virtual-machine"></a>Configurar o Oracle ASM em uma máquina virtual Linux do Azure  

Máquinas virtuais do Azure fornecem um ambiente de computação totalmente configurável e flexível. Este tutorial aborda a implantação básica da máquina virtual do Azure combinada com a instalação de saudação e a configuração do Oracle Automated Storage Management (ASM).  Você aprenderá como:

> [!div class="checklist"]
> * Criar e conectar tooan VM de banco de dados Oracle
> * Instalar e configurar o Oracle Automated Storage Management
> * Instalar e configurar a infraestrutura Oracle Grid
> * Inicializar uma instalação do Oracle ASM
> * Criar um Oracle DB gerenciado por ASM


[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="prepare-hello-environment"></a>Preparar o ambiente de saudação

### <a name="create-a-resource-group"></a>Criar um grupo de recursos

toocreate um grupo de recursos, use Olá [criar grupo az](/cli/azure/group#create) comando. Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados. Neste exemplo, um grupo de recursos denominado *myResourceGroup* em Olá *eastus* região.

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

### <a name="create-a-vm"></a>Criar uma máquina virtual

toocreate uma máquina virtual com base na imagem do banco de dados Oracle hello e configurá-lo toouse Oracle ASM, use Olá [criar vm az](/cli/azure/vm#create) comando. 

Olá, exemplo a seguir cria uma VM denominada myVM que é um tamanho de Standard_DS2_v2 com quatro discos de dados anexado de 50 GB. Se eles ainda não existir no local de chave saudação padrão, ele também cria chaves SSH.  toouse um conjunto específico de chaves, use Olá `--ssh-key-value` opção.  

   ```azurecli-interactive
   az vm create --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50 50 50 50
   ```

Depois de criar hello VM, CLI do Azure exibe informações toohello semelhante exemplo a seguir. Observe o valor de saudação para `publicIpAddress`. Usar o hello de tooaccess esse endereço VM.

   ```azurecli
   {
     "fqdns": "",
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
     "location": "eastus",
     "macAddress": "00-0D-3A-36-2F-56",
     "powerState": "VM running",
     "privateIpAddress": "10.0.0.4",
     "publicIpAddress": "13.64.104.241",
     "resourceGroup": "myResourceGroup"
   }
   ```

### <a name="connect-toohello-vm"></a>Conecte-se toohello VM

toocreate uma sessão SSH com hello VM e definir configurações adicionais, use Olá comando a seguir. Substitua o endereço IP de saudação com hello `publicIpAddress` valor para a VM.

```bash 
ssh <publicIpAddress>
```

## <a name="install-oracle-asm"></a>Instalar o Oracle ASM

tooinstall Oracle ASM Olá concluir as etapas a seguir. 

Para saber mais sobre como instalar o ASM do Oracle, confira [Downloads do Oracle ASMLib para Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html).  

1. É necessário toologin como raiz em ordem toocontinue com instalação ASM:

   ```bash
   sudo su -
   ```
   
2. Execute esses comandos adicionais componentes do Oracle ASM tooinstall:

   ```bash
    yum list | grep oracleasm 
    yum -y install kmod-oracleasm.x86_64 
    yum -y install oracleasm-support.x86_64 
    wget http://download.oracle.com/otn_software/asmlib/oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    yum -y install oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    rm -f oracleasmlib-2.0.12-1.el6.x86_64.rpm
   ```

3. Verifique se o Oracle ASM está instalado:

   ```bash
   rpm -qa |grep oracleasm
   ```

    saída de Hello desse comando deve listar Olá componentes a seguir:

    ```bash
   oracleasm-support-2.1.10-4.el6.x86_64
   kmod-oracleasm-2.0.8-15.el6_9.x86_64
   oracleasmlib-2.0.12-1.el6.x86_64
    ```

4. ASM requer usuários e funções na ordem toofunction corretamente. Olá comandos a seguir cria grupos e contas de usuário de pré-requisito hello: 

   ```bash
    groupadd -g 54345 asmadmin 
    groupadd -g 54346 asmdba 
    groupadd -g 54347 asmoper 
    useradd -u 3000 -g oinstall -G dba,asmadmin,asmdba,asmoper grid 
    usermod -g oinstall -G dba,asmdba,asmadmin oracle
   ```

5. Verifique se os usuários e grupos foram criados corretamente:

   ```bash
   id grid
   ```

    Olá saída desse comando deve listar seguinte Olá usuários e grupos:

    ```bash
    uid=3000(grid) gid=54321(oinstall) groups=54321(oinstall),54322(dba),54345(asmadmin),54346(asmdba),54347(asmoper)
    ```
 
6. Crie uma pasta para o usuário *grade* e alterar o proprietário de saudação:

   ```bash
   mkdir /u01/app/grid 
   chown grid:oinstall /u01/app/grid
   ```

## <a name="set-up-oracle-asm"></a>Configurar o Oracle ASM

Para este tutorial, o usuário de padrão de saudação é *grade* e saudação padrão grupo é *asmadmin*. Certifique-se de que Olá *oracle* usuário faz parte do grupo de asmadmin hello. tooset a instalação com a Oracle ASM, Olá concluir as etapas a seguir:

1. Configurando o driver de biblioteca do Oracle ASM Olá envolve a definição de usuário padrão de saudação (grade) e o grupo padrão (asmadmin), bem como configurar Olá unidade toostart na inicialização (escolha y) e tooscan para discos de inicialização (escolha y). É necessário tooanswer Olá prompts de saudação comando a seguir:

   ```bash
   /usr/sbin/oracleasm configure -i
   ```

   saída de Hello desse comando deve ter toohello semelhante a seguir, parando com toobe prompts respondida.

    ```bash
   Configuring hello Oracle ASM library driver.

   This will configure hello on-boot properties of hello Oracle ASM library
   driver. hello following questions will determine whether hello driver is
   loaded on boot and what permissions it will have. hello current values
   will be shown in brackets ('[]'). Hitting <ENTER> without typing an
   answer will keep that current value. Ctrl-C will abort.

   Default user tooown hello driver interface []: grid
   Default group tooown hello driver interface []: asmadmin
   Start Oracle ASM library driver on boot (y/n) [n]: y
   Scan for Oracle ASM disks on boot (y/n) [y]: y
   Writing Oracle ASM library driver configuration: done
   ```

2. Exibir a configuração de disco hello:
   ```bash
   cat /proc/partitions
   ```

   saída de Hello desse comando deve ser semelhante toohello seguir a lista de discos disponíveis

   ```bash
   8       16   14680064 sdb
   8       17   14678976 sdb1
   8        0   52428800 sda
   8        1     512000 sda1
   8        2   51915776 sda2
   8       48   52428800 sdd
   8       64   52428800 sde
   8       80   52428800 sdf
   8       32   52428800 sdc
   11       0       1152 sr0
   ```

3. Formatar o disco */desenvolvimento/sdc* executando Olá comando a seguir e responder Olá prompts com:
   - *n* para a nova partição
   - *p* para a partição primária
   - *1* primeira partição do tooselect Olá
   - Pressione `enter` para primeiro cilindro do saudação padrão
   - Pressione `enter` para último cilindro do saudação padrão
   - Pressione *w* tabela de partição toowrite Olá alterações toohello  

   ```bash
   fdisk /dev/sdc
   ```
   
   Saída Olá para o comando de fdisk hello usando respostas Olá fornecidas acima, deverá parecer como Olá a seguir:

   ```bash
   Device contains not a valid DOS partition table, or Sun, SGI or OSF disklabel
   Building a new DOS disklabel with disk identifier 0xf865c6ca.
   Changes will remain in memory only, until you decide toowrite them.
   After that, of course, hello previous content won't be recoverable.

   Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

   hello device presents a logical sector size that is smaller than
   hello physical sector size. Aligning tooa physical sector (or optimal
   I/O) size boundary is recommended, or performance may be impacted.

   WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
           switch off hello mode (command 'c') and change display units to
           sectors (command 'u').

   Command (m for help): n
   Command action
     e   extended
     p   primary partition (1-4)
   p
   Partition number (1-4): 1
   First cylinder (1-6527, default 1):
   Using default value 1
   Last cylinder, +cylinders or +size{K,M,G} (1-6527, default 6527):
   Using default value 6527

   Command (m for help): w
   hello partition table has been altered!

   Calling ioctl() toore-read partition table.
   Syncing disks.
   ```

4. Repita Olá precede o comando fdisk para `/dev/sdd`, `/dev/sde`, e `/dev/sdf`.

5. Verifique a configuração de disco hello:

   ```bash
   cat /proc/partitions
   ```

   saída de saudação do comando Olá deve ter aparência Olá a seguir:

   ```bash
   major minor  #blocks  name

     8       16   14680064 sdb
     8       17   14678976 sdb1
     8       32   52428800 sdc
     8       33   52428096 sdc1
     8       48   52428800 sdd
     8       49   52428096 sdd1
     8       64   52428800 sde
     8       65   52428096 sde1
     8       80   52428800 sdf
     8       81   52428096 sdf1
     8        0   52428800 sda
     8        1     512000 sda1
     8        2   51915776 sda2
     11       0    1048575 sr0
   ```

6. Verificar status do serviço Oracle ASM hello e iniciar o serviço do Oracle ASM hello:

   ```bash
   service oracleasm status 
   service oracleasm start
   ```

   saída de saudação do comando Olá deve ter aparência Olá a seguir:
   
   ```bash
   Checking if ASM is loaded: no
   Checking if /dev/oracleasm is mounted: no
   Initializing hello Oracle ASMLib driver:                     [  OK  ]
   Scanning hello system for Oracle ASMLib disks:               [  OK  ]
   ```

7. Crie discos do Oracle ASM:

   ```bash
   service oracleasm createdisk ASMSP /dev/sdc1 
   service oracleasm createdisk DATA /dev/sdd1 
   service oracleasm createdisk DATA1 /dev/sde1 
   service oracleasm createdisk FRA /dev/sdf1
   ```    

   saída de saudação do comando Olá deve ter aparência Olá a seguir:

   ```bash
   Marking disk "ASMSP" as an ASM disk:                       [  OK  ]
   Marking disk "DATA" as an ASM disk:                        [  OK  ]
   Marking disk "DATA1" as an ASM disk:                       [  OK  ]
   Marking disk "FRA" as an ASM disk:                         [  OK  ]
   ```

8. Liste os discos do Oracle ASM:

   ```bash
   service oracleasm listdisks
   ```   

   saída de saudação do comando Olá deve listar off Olá seguintes discos Oracle ASM:

   ```bash
    ASMSP
    DATA
    DATA1
    FRA
   ```

9. Alterar as senhas de saudação para usuários de raiz, oracle e grade hello. **Anote essas novas senhas** como eles serão usados posteriormente, durante a instalação de saudação.

   ```bash
   passwd oracle 
   passwd grid 
   passwd root
   ```

10. Alterar permissões de pasta hello:

   ```bash
   chmod -R 775 /opt 
   chown grid:oinstall /opt 
   chown oracle:oinstall /dev/sdc1 
   chown oracle:oinstall /dev/sdd1 
   chown oracle:oinstall /dev/sde1 
   chown oracle:oinstall /dev/sdf1 
   chmod 600 /dev/sdc1 
   chmod 600 /dev/sdd1 
   chmod 600 /dev/sde1 
   chmod 600 /dev/sdf1
   ```

## <a name="download-and-prepare-oracle-grid-infrastructure"></a>Baixe e prepare a infraestrutura em grade do Oracle

toodownload e preparar o software de infraestrutura de grade Oracle hello, Olá concluir as etapas a seguir:

1. Fazer o download de infraestrutura de grade Oracle Olá [página de download do Oracle ASM](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html). 

   Em download de saudação intitulada **banco de dados Oracle 12c versão 1 grade infraestrutura (12.1.0.2.0) para Linux x86-64**, baixar arquivos. zip de saudação dois.

2. Depois de baixar o computador cliente do hello. zip arquivos tooyour, você pode usar o protocolo de cópia seguro (SCP) toocopy Olá arquivos tooyour VM:

   ```bash
   scp *.zip <publicIpAddress>:.
   ```

3. SSH volta para sua VM Oracle no Azure em arquivos do pedido toomove hello. zip em Olá / Escolher pasta. Em seguida, altere o proprietário de saudação do arquivos hello:

   ```bash
   ssh <publicIPAddress>
   sudo mv ./*.zip /opt
   cd /opt
   sudo chown grid:oinstall linuxamd64_12102_grid_1of2.zip
   sudo chown grid:oinstall linuxamd64_12102_grid_2of2.zip
   ```

4. Descompacte arquivos de saudação. (Instalação Olá Linux Descompacte ferramenta se ele ainda não estiver instalado.)
   
   ```bash
   sudo yum install unzip
   sudo unzip linuxamd64_12102_grid_1of2.zip
   sudo unzip linuxamd64_12102_grid_2of2.zip
   ```

5. Alterar permissão:
   
   ```bash
   sudo chown -R grid:oinstall /opt/grid
   ```

6. Atualize o espaço de troca configurado. Componentes de grade Oracle necessário pelo menos 6,8 GB de espaço de permuta tooinstall grade. tamanho de arquivo de permuta Olá padrão para as imagens da Oracle Linux no Azure é apenas 2048MB. Você precisa tooincrease `ResourceDisk.SwapSizeMB` em Olá `/etc/waagent.conf` de arquivo e reiniciar serviço de WALinuxAgent Olá Olá atualizado configurações tootake efeito. Como é um arquivo somente leitura, é necessário o acesso de gravação do toochange arquivo permissões tooenable.

   ```bash
   sudo chmod 777 /etc/waagent.conf  
   vi /etc/waagent.conf
   ```
   
   Procurar `ResourceDisk.SwapSizeMB` e altere o valor de saudação muito**8192**. Você precisará toopress `insert` tooenter no modo de inserção, tipo de valor de saudação do **8192** e, em seguida, pressione `esc` tooreturn toocommand modo. alterações de saudação toowrite e arquivo hello quit, digite `:wq` e pressione `enter`.
   
   > [!NOTE]
   > É altamente recomendável que você sempre use `WALinuxAgent` tooconfigure espaço de permuta para que ele é sempre criado no hello efêmera disco local (disco temporário) para melhor desempenho. Para obter mais informações, consulte [como tooadd uma permuta de arquivo em máquinas virtuais do Linux Azure](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).

## <a name="prepare-your-local-client-and-vm-toorun-x11"></a>Preparar seu cliente local e a VM toorun x11
Configurar o Oracle ASM requer uma interface gráfica toocomplete Olá instalação e configuração. Estamos usando Olá x11 protocolo toofacilitate esta instalação. Se você estiver usando um sistema de cliente (Mac ou Linux) que já tenha X11 recursos habilitada e configurada - você pode ignorar essa configuração e instalação máquinas tooWindows exclusivo. 

1. [Baixar o PuTTY](http://www.putty.org/) e [baixar Xming](https://xming.en.softonic.com/) tooyour computador com Windows. Você precisará toocomplete instalação de saudação de ambos os aplicativos com os valores padrão de saudação antes de continuar.

2. Depois de instalar o PuTTY, abra um prompt de comando, altere para Olá PuTTY pasta (por exemplo, C:\Program Files\PuTTY) e execute `puttygen.exe` em ordem toogenerate uma chave.

3. No Gerador de Chave PuTTY:
   
   1. Gerar uma chave selecionando Olá `Generate` botão.
   2. Copie o conteúdo de saudação da chave de saudação (Ctrl + C).
   3. Selecione Olá `Save private key` botão.
   4. Ignorar aviso Olá sobre como proteger a chave de saudação com uma senha e, em seguida, selecione `OK`.

   ![Captura de tela do Gerador de Chaves PuTTY](./media/oracle-asm/puttykeygen.png)

4. Em sua VM, execute estes comandos:

   ```bash
   sudo su - grid
   mkdir .ssh 
   cd .ssh
   ```

5. Crie um arquivo chamado `authorized_keys`. Cole o conteúdo de saudação da chave Olá neste arquivo e, em seguida, salve o arquivo hello.

   > [!NOTE]
   > chave de saudação deve conter a cadeia de caracteres de saudação `ssh-rsa`. Além disso, o conteúdo de saudação da chave Olá deve ser uma única linha de texto.
   >  

6. No sistema cliente, inicie o PuTTY. Em Olá **categoria** painel, ir muito**Conexão** > **SSH** > **Auth**. Em Olá **arquivo de chave privada para autenticação** caixa, procure toohello chave gerada anteriormente.

   ![Captura de tela de opções de autenticação SSH Olá](./media/oracle-asm/setprivatekey.png)

7. Em Olá **categoria** painel, ir muito**Conexão** > **SSH** > **X11**. Selecione Olá **ativar X11 encaminhamento** caixa de seleção.

   ![Captura de tela da saudação SSH X11 opções de encaminhamento](./media/oracle-asm/enablex11.png)

8. Em Olá **categoria** painel, ir muito**sessão**. Insira sua VM do Oracle ASM `<publicIPaddress>` na caixa de diálogo de nome de host hello, preencha um novo `Saved Session` nome e, em seguida, clique em `Save`.  Uma vez salvo, clique em `open` tooconnect tooyour Oracle ASM VM.  Olá primeira vez que você se conectar será avisado não armazenado em cache no registro do sistema remoto hello. Clique em `yes` tooadd-lo e continuar.

   ![Captura de tela de opções de sessão PuTTY Olá](./media/oracle-asm/puttysession.png)

## <a name="install-oracle-grid-infrastructure"></a>Instalar a infraestrutura em grade do Oracle

tooinstall infra-estrutura de grade da Oracle, Olá concluir as etapas a seguir:

1. Entre como **grade**. (Você deve ser capaz de toosign em sem inserir uma senha.) 

   > [!NOTE]
   > Se você estiver executando o Windows, verifique se que você iniciou Xming antes de começar a instalação de saudação.

   ```bash
   cd /opt/grid
   ./runInstaller
   ```

   O instalador da Infraestrutura em grade do Oracle 12c versão 1 é aberto. (Ele pode levar alguns minutos para Olá instalador toostart).

2. Em Olá **Selecionar opção de instalação** , selecione **instalar e configurar a infraestrutura de grade Oracle para um servidor autônomo**.

   ![Captura de tela da página de selecionar a opção de instalação do instalador Olá](./media/oracle-asm/install01.png)

3. Em Olá **selecionar idiomas de produto** página, certifique-se de **inglês** ou idioma Olá desejado está selecionado.  Clique em `next`.

4. Em Olá **criar grupo de discos do ASM** página:
   - Insira um nome para o grupo de discos de saudação.
   - Em **Redundância**, selecione **Externa**.
   - Em **Tamanho da Unidade de Alocação**, selecione **4**.
   - Em **Adicionar Discos**, selecione **ORCLASMSP**.
   - Clique em `next`.

5. Em Olá **especificar ASM senha** página, selecione Olá **usar as mesmas senhas para essas contas** opção e digite uma senha.

   ![Captura de tela de página de especificar senha de ASM do instalador de saudação](./media/oracle-asm/install04.png)

6. Em Olá **especificar opções de gerenciamento** página, ter Olá opção tooconfigure EM controle de nuvem. Vamos ignorar essa opção - clique `next` toocontinue. 

7. Em Olá **grupos privilegiados do sistema operacional** página, use as configurações padrão de saudação. Clique em `next` toocontinue.

8. Em Olá **especificar local de instalação** página, use as configurações padrão de saudação. Clique em `next` toocontinue.

9. Em Olá **Criar inventário** página, altere Olá Directory inventário muito`/u01/app/grid/oraInventory`. Clique em `next` toocontinue.

   ![Captura da página de criar inventário do instalador Olá](./media/oracle-asm/install08.png)

10. Em Olá **configuração de execução de script raiz** página, selecione Olá **automaticamente executar scripts de configuração** caixa de seleção. Em seguida, selecione Olá **usar credenciais de usuário "raiz"** opção e digite a senha do usuário raiz hello.

    ![Captura de tela da página de configuração de execução de script do instalador Olá raiz](./media/oracle-asm/install09.png)

11. Em Olá **executar verificações de pré-requisito** página, a instalação atual do hello falhará com erros. Este é um comportamento esperado. Selecione `Fix & Check Again`.

12. Em Olá **Script de correção** caixa de diálogo, clique em `OK`.

13. Em Olá **resumo** página, examine as configurações selecionadas e, em seguida, clique em `Install`.

    ![Captura de tela da página de resumo do instalador Olá](./media/oracle-asm/install12.png)

14. Uma caixa de diálogo de aviso será exibida informando os scripts de configuração precisa toobe executar como um usuário com privilégios. Clique em `Yes` toocontinue.

15. Em Olá **concluir** , clique em `Close` toofinish instalação de saudação.

## <a name="set-up-your-oracle-asm-installation"></a>Configurar a sua instalação do Oracle ASM

tooset a instalação com a Oracle ASM, Olá concluir as etapas a seguir:

1. Verifique se você ainda está conectado como **grade**, da sua sessão X11. Talvez seja necessário toohit `enter` toorevive Olá terminal. Em seguida, inicie Olá Oracle Automated Storage Management Assistente de configuração:

   ```bash
   cd /u01/app/grid/product/12.1.0/grid/bin
   ./asmca
   ```

   O assistente de configuração do Oracle ASM é aberto.

2. Em Olá **configurar ASM: grupos de discos** caixa de diálogo, clique em Olá `Create` botão e, em seguida, clique em `Show Advanced Options`.

3. Em Olá **criar grupo de discos** caixa de diálogo:

   - Inserir nome do grupo de disco Olá **dados**.
   - Em **Selecionar discos membros**, selecione **ORCL_DATA** e **ORCL_DATA1**.
   - Em **Tamanho da Unidade de Alocação**, selecione **4**.
   - Clique em `ok` toocreate grupo de discos de saudação.
   - Clique em `ok` tooclose janela de confirmação de saudação.

   ![Captura de tela da caixa de diálogo Criar grupo de discos Olá](./media/oracle-asm/asm02.png)

4. Em Olá **configurar ASM: grupos de discos** caixa de diálogo, clique em Olá `Create` botão e, em seguida, clique em `Show Advanced Options`.

5. Em Olá **criar grupo de discos** caixa de diálogo:

   - Inserir nome do grupo de disco Olá **FRA**.
   - Em **Redundância**, selecione **Externa (nenhuma)**.
   - Em **Selecionar discos membros**, selecione **ORCL_FRA**.
   - Em **Tamanho da Unidade de Alocação**, selecione **4**.
   - Clique em `ok` toocreate grupo de discos de saudação.
   - Clique em `ok` tooclose janela de confirmação de saudação.

   ![Captura de tela da caixa de diálogo Criar grupo de discos Olá](./media/oracle-asm/asm04.png)

6. Selecione **Exit** tooclose o Assistente de configuração do ASM.

   ![Captura de tela de Olá configurar ASM: caixa de diálogo de grupos de discos com o botão de saída](./media/oracle-asm/asm05.png)

## <a name="create-hello-database"></a>Criar banco de dados de saudação

Olá software de banco de dados Oracle já está instalado na imagem do hello Azure Marketplace. toocreate um banco de dados, Olá concluir as etapas a seguir:

1. Alternar superusuário do usuários toohello Oracle e, em seguida, inicializar o ouvinte de saudação para registro em log:

   ```bash
   su - oracle
   cd /u01/app/oracle/product/12.1.0/dbhome_1/bin
   ./dbca
   ```
   O assistente de configuração do banco de dados é aberto.

2. Em Olá **operação de banco de dados** , clique em `Create Database`.

3. Em Olá **modo de criação de** página:

   - Insira um nome para o banco de dados de saudação.
   - Para **Tipo de armazenamento**, verifique se **ASM (Automatic Storage Management )** está selecionado.
   - Para **local dos arquivos de banco de dados**, use o padrão de saudação ASM sugerido local.
   - Para **área de recuperação rápida**, use o padrão de saudação ASM sugerido local.
   - digite uma **Senha administrativa** e **confirme a senha**.
   - certifique-se de que `create as container database` esteja selecionado.
   - digite um valor `pluggable database name`.

4. Em Olá **resumo** página, examine as configurações selecionadas e, em seguida, clique em `Finish` o banco de dados do toocreate hello.

   ![Captura de tela da página de resumo de saudação](./media/oracle-asm/createdb03.png)

5. Olá banco de dados foi criado. Em Olá **concluir** página, você tem Olá opção toounlock contas adicionais toouse esse banco de dados e alterar senhas de saudação. Se você desejar toodo isso, selecione **gerenciamento de senha** -caso contrário, clique em `close`.

## <a name="delete-hello-vm"></a>Excluir Olá VM

Você configurou com êxito o Oracle Automated Storage Management na imagem de banco de dados Oracle de saudação do hello Azure Marketplace.  Quando você não precisa mais essa VM, você pode usar o hello grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir:

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Próximas etapas

[Tutorial: configurar o Oracle DataGuard](configure-oracle-dataguard.md)

[Tutorial: configurar o Oracle GoldenGate](Configure-oracle-golden-gate.md)

Examine [Projetar um Oracle DB](oracle-design.md)
