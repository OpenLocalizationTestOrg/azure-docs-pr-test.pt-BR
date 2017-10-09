---
title: aaaImplement Oracle Golden Gate em uma VM do Linux do Azure | Microsoft Docs
description: Coloque rapidamente em funcionamento um Oracle Golden Gate no seu ambiente do Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: rclaus
ms.openlocfilehash: 320cafd5d23ee472f0af9f92577bc6f432f65778
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-golden-gate-on-an-azure-linux-vm"></a>Implementar Oracle Golden Gate em uma VM Linux do Azure 

Olá CLI do Azure é usado toocreate e gerenciar recursos do Azure Olá linha de comando ou em scripts. Esses detalhes de guia como toouse Olá CLI do Azure toodeploy um Oracle 12c banco de dados de imagem da Galeria hello Azure Marketplace. 

Este documento mostra passo a passo como toocreate, instalar e configurar o Oracle Golden Gate em uma VM do Azure.

Antes de começar, certifique-se que Olá que CLI do Azure foi instalado. Para obter mais informações, consulte o [Guia de instalação da CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="prepare-hello-environment"></a>Preparar o ambiente de saudação

instalação de Oracle Golden Gate do tooperform Olá, você precisa toocreate duas VMs do Azure Olá mesmo conjunto de disponibilidade. imagem do Marketplace Olá usar toocreate Olá VMs é **Oracle: Oracle-banco de dados-Ee:12.1.0.2:latest**.

Você também precisa toobe familiarizado com Unix editor vi e ter um entendimento básico de x11 (X Windows).

a seguir Olá é um resumo da configuração do ambiente de saudação:
> 
> |  | **Site primário** | **Replicar site** |
> | --- | --- | --- |
> | **Versão do Oracle** |Oracle 12c Release 2 – (12.1.0.2) |Oracle 12c Release 2 – (12.1.0.2)|
> | **Nome da máquina** |myVM1 |myVM2 |
> | **Sistema operacional** |Oracle Linux 6.x |Oracle Linux 6.x |
> | **SID do Oracle** |CDB1 |CDB1 |
> | **Esquema de replicação** |TEST|TEST |
> | **Golden Gate proprietário/replicar** |C ##GGADMIN |REPUSER |
> | **Processo de Golden Gate** |EXTORA |REPORA|


### <a name="sign-in-tooazure"></a>Entrar tooAzure 

Entrar tooyour assinatura do Azure com hello [logon az](/cli/azure/#login) comando. Em seguida, siga Olá na tela instruções.

```azurecli
az login
```

### <a name="create-a-resource-group"></a>Criar um grupo de recursos

Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando. Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e a partir do qual podem ser gerenciados. 

Olá, exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` em Olá `westus` local.

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a>Criar um conjunto de disponibilidade

Olá após a etapa é opcional, mas recomendado. Para obter mais informações, confira [Guia de conjuntos de disponibilidade do Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a>Criar uma máquina virtual

Criar uma VM com hello [criar vm az](/cli/azure/vm#create) comando. 

Olá, exemplo a seguir cria duas VMs denominadas `myVM1` e `myVM2`. Crie chaves SSH, se elas ainda não existirem em um local de chave padrão. toouse um conjunto específico de chaves, use Olá `--ssh-key-value` opção.

#### <a name="create-myvm1-primary"></a>Criar myVM1 (primário):
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

Depois de Olá que VM foi criada, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir. (Observe Olá `publicIpAddress`. Esse endereço é usado tooaccess Olá VM).

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westus",
  "macAddress": "00-0D-3A-36-2F-56",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.104.241",
  "resourceGroup": "myResourceGroup"
}
```

#### <a name="create-myvm2-replicate"></a>Criar myVM2 (replicação):
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

Anote Olá `publicIpAddress` também após ele ter sido criado.

### <a name="open-hello-tcp-port-for-connectivity"></a>Abra a porta TCP para conectividade Olá

Olá próxima etapa é tooconfigure pontos de extremidade externos, que permitem o banco de dados do Oracle tooaccess Olá remotamente. tooconfigure Olá pontos de extremidade externos, execute Olá comandos a seguir.

#### <a name="open-hello-port-for-myvm1"></a>Abra a porta Olá para myVM1:

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

Olá resultados são semelhante toohello resposta a seguir:

```bash
{
  "access": "Allow",
  "description": null,
  "destinationAddressPrefix": "*",
  "destinationPortRange": "1521",
  "direction": "Inbound",
  "etag": "W/\"bd77dcae-e5fd-4bd6-a632-26045b646414\"",
  "id": "/subscriptions/<subscription-id>/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myVmNSG/securityRules/allow-oracle",
  "name": "allow-oracle",
  "priority": 999,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sourceAddressPrefix": "*",
  "sourcePortRange": "*"
}
```

#### <a name="open-hello-port-for-myvm2"></a>Abra a porta Olá para myVM2:

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a>Conecte-se a máquina virtual de toohello

A seguir Olá Use o comando toocreate uma sessão SSH com a máquina virtual de saudação. Substitua o endereço IP de saudação com hello `publicIpAddress` de sua máquina virtual.

```bash 
ssh <publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a>Criar banco de dados de saudação myVM1 (primário)

Olá software Oracle já está instalado na imagem do Marketplace hello, portanto Olá próxima etapa é o banco de dados do tooinstall hello. 

Execute software hello como superusuário de 'oracle' hello:

```bash
sudo su - oracle
```

Crie banco de dados de saudação:

```bash
$ dbca -silent \
   -createDatabase \
   -templateName General_Purpose.dbc \
   -gdbname cdb1 \
   -sid cdb1 \
   -responseFile NO_VALUE \
   -characterSet AL32UTF8 \
   -sysPassword OraPasswd1 \
   -systemPassword OraPasswd1 \
   -createAsContainerDatabase true \
   -numberOfPDBs 1 \
   -pdbName pdb1 \
   -pdbAdminPassword OraPasswd1 \
   -databaseType MULTIPURPOSE \
   -automaticMemoryManagement false \
   -storageType FS \
   -ignorePreReqs
```
Saídas devem parecer semelhante toohello resposta a seguir:

```bash
Copying database files
1% complete
2% complete
8% complete
13% complete
19% complete
27% complete
Creating and starting Oracle instance
29% complete
32% complete
33% complete
34% complete
38% complete
42% complete
43% complete
45% complete
Completing Database Creation
48% complete
51% complete
53% complete
62% complete
70% complete
72% complete
Creating Pluggable Databases
78% complete
100% complete
Look at hello log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for more details.
```

Definir variáveis ORACLE_SID e ORACLE_HOME hello.

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=gg1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

Opcionalmente, você pode adicionar ORACLE_HOME e ORACLE_SID toohello. bashrc arquivo, para que essas configurações são salvas para futuras entradas:

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=gg1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a>Iniciar o Oracle listener
```bash
$ sudo su - oracle
$ lsnrctl start
```

### <a name="create-hello-database-on-myvm2-replicate"></a>Criar banco de dados de saudação myVM2 (replicação)

```bash
sudo su - oracle
```
Crie banco de dados de saudação:

```bash
$ dbca -silent \
   -createDatabase \
   -templateName General_Purpose.dbc \
   -gdbname cdb1 \
   -sid cdb1 \
   -responseFile NO_VALUE \
   -characterSet AL32UTF8 \
   -sysPassword OraPasswd1 \
   -systemPassword OraPasswd1 \
   -createAsContainerDatabase true \
   -numberOfPDBs 1 \
   -pdbName pdb1 \
   -pdbAdminPassword OraPasswd1 \
   -databaseType MULTIPURPOSE \
   -automaticMemoryManagement false \
   -storageType FS \
   -ignorePreReqs
```
Definir variáveis ORACLE_SID e ORACLE_HOME hello.

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

Opcionalmente, você pode ORACLE_HOME e ORACLE_SID toohello. bashrc arquivo adicionado, para que essas configurações são salvas para futuras entradas.

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a>Iniciar o Oracle listener
```bash
$ sudo su - oracle
$ lsnrctl start
```

## <a name="configure-golden-gate"></a>Configurar o Golden Gate 
tooconfigure Golden Gate etapas Olá nesta seção.

### <a name="enable-archive-log-mode-on-myvm1-primary"></a>Habilitar o modo de log de arquivo morto em myVM1 (primário)

```bash
$ sqlplus / as sysdba
SQL> SELECT log_mode FROM v$database;

LOG_MODE
------------
NOARCHIVELOG

SQL> SHUTDOWN IMMEDIATE;
SQL> STARTUP MOUNT;
SQL> ALTER DATABASE ARCHIVELOG;
SQL> ALTER DATABASE OPEN;
```
Habilite o registro em log forçado e verifique se há pelo menos um arquivo de log.

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
SQL> ALTER SYSTEM set enable_goldengate_replication=true;
SQL> ALTER PLUGGABLE DATABASE PDB1 OPEN;
SQL> ALTER SESSION SET CONTAINER=PDB1;
SQL> ALTER DATABASE ADD SUPPLEMENTAL LOG DATA;
SQL> EXIT;
```

### <a name="download-golden-gate-software"></a>Baixar o software de Golden Gate
toodownload e preparar o software Oracle Golden Gate hello, Olá concluir as etapas a seguir:

1. Baixar Olá **fbo_ggs_Linux_x64_shiphome.zip** arquivo hello [página de download do Oracle Golden Gate](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html). Em Olá baixar título **12.x.x.x do Oracle GoldenGate para Oracle Linux x86-64**, deve haver um conjunto de toodownload de arquivos. zip.

2. Depois de baixar o computador cliente do hello. zip arquivos tooyour, use o protocolo de cópia seguro (SCP) toocopy Olá arquivos tooyour VM:

  ```bash
  $ scp fbo_ggs_Linux_x64_shiphome.zip <publicIpAddress>:<folder>
  ```

3. Mover hello. zip arquivos toohello **/opt** pasta. Em seguida, altere o proprietário de saudação dos arquivos de saudação da seguinte maneira:

  ```bash
  $ sudo su -
  # mv <folder>/*.zip /opt
  ```

4. Descompacte arquivos hello (Olá instalação Linux Descompacte utilitário se ele ainda não estiver instalado):

  ```bash
  # yum install unzip
  # cd /opt
  # unzip fbo_ggs_Linux_x64_shiphome.zip
  ```

5. Alterar permissão:

  ```bash
  # chown -R oracle:oinstall /opt/fbo_ggs_Linux_x64_shiphome
  ```

### <a name="prepare-hello-client-and-vm-toorun-x11-for-windows-clients-only"></a>Preparar o cliente hello e VM toorun x11 (para clientes do Windows somente)
Esta é uma etapa opcional. Essa é uma etapa opcional, você pode ignorá-la se estiver usando um cliente do Linux ou já tiver a instalação do x11.

1. Baixe o PuTTY e Xming tooyour computador com Windows:

  * [Baixar PuTTY](http://www.putty.org/)
  * [Baixar Xming](https://xming.en.softonic.com/)

2.  Depois de instalar o PuTTY, em Olá PuTTY pasta (por exemplo, C:\Program Files\PuTTY), execute puttygen.exe (gerador de chave PuTTY).

3.  No Gerador de Chave PuTTY:

  - toogenerate uma saudação de chave, selecione **gerar** botão.
  - Copiar conteúdo de saudação da chave de saudação (**Ctrl + C**).
  - Selecione Olá **salva a chave privada** botão.
  - Ignorar aviso de saudação que aparece e, em seguida, selecione **Okey**.

    ![Captura de tela da página de gerador de chave PuTTY Olá](./media/oracle-golden-gate/puttykeygen.png)

4.  Em sua VM, execute estes comandos:

  ```bash
  # sudo su - oracle
  $ mkdir .ssh (if not already created)
  $ cd .ssh
  ```

5. Crie um arquivo chamado **authorized_keys**. Cole o conteúdo de saudação da chave Olá neste arquivo e, em seguida, salve o arquivo hello.

  > [!NOTE]
  > chave de saudação deve conter a cadeia de caracteres de saudação `ssh-rsa`. Além disso, o conteúdo de saudação da chave Olá deve ser uma única linha de texto.
  >  

6. Inicie o PuTTY. Em Olá **categoria** painel, selecione **Conexão** > **SSH** > **Auth**. Em Olá **arquivo de chave privada para autenticação** caixa, procure toohello chave gerada anteriormente.

  ![Captura de tela da página de definir a chave privada de saudação](./media/oracle-golden-gate/setprivatekey.png)

7. Em Olá **categoria** painel, selecione **Conexão** > **SSH** > **X11**. Em seguida, selecione Olá **ativar X11 encaminhamento** caixa.

  ![Captura de tela da página de habilitar X11 Olá](./media/oracle-golden-gate/enablex11.png)

8. Em Olá **categoria** painel, ir muito**sessão**. Insira as informações de host hello e, em seguida, selecione **abrir**.

  ![Captura de tela da página de sessão Olá](./media/oracle-golden-gate/puttysession.png)

### <a name="install-golden-gate-software"></a>Instalar o software de Golden Gate

tooinstall Oracle Golden Gate, Olá concluir as etapas a seguir:

1. Entre como oracle. (Você deve ser capaz de toosign em sem inserir uma senha.) Certifique-se de que Xming está em execução antes de começar a instalação de saudação.
 
  ```bash
  $ cd /opt/fbo_ggs_Linux_x64_shiphome/Disk1
  $ ./runInstaller
  ```
2. Selecione 'Oracle GoldenGate para o banco de dados Oracle 12c'. Em seguida, selecione **próximo** toocontinue.

  ![Captura de tela da página de selecione instalação do instalador Olá](./media/oracle-golden-gate/golden_gate_install_01.png)

3. Alterar o local de saudação do software. Em seguida, selecione Olá **iniciar Gerenciador** caixa e insira o local do banco de dados de saudação. Selecione **próximo** toocontinue.

  ![Captura de tela da página de instalação selecione Olá](./media/oracle-golden-gate/golden_gate_install_02.png)

4. Altere o diretório de inventário hello e, em seguida, selecione **próximo** toocontinue.

  ![Captura de tela da página de instalação selecione Olá](./media/oracle-golden-gate/golden_gate_install_03.png)

5. Em Olá **resumo** tela, selecione **instalar** toocontinue.

  ![Captura de tela da página de selecione instalação do instalador Olá](./media/oracle-golden-gate/golden_gate_install_04.png)

6. Você pode ser solicitado toorun um script como 'root'. Nesse caso, abra uma sessão separada, ssh toohello VM, sudo tooroot e, em seguida, execute o script hello. Selecione **OK** para continuar.

  ![Captura de tela da página de instalação selecione Olá](./media/oracle-golden-gate/golden_gate_install_05.png)

7. Quando a instalação Olá terminar, selecione **fechar** toocomplete processo de saudação.

  ![Captura de tela da página de instalação selecione Olá](./media/oracle-golden-gate/golden_gate_install_06.png)

### <a name="set-up-service-on-myvm1-primary"></a>Configuração de serviço no myVM1 (primário)

1. Criar ou atualizar o arquivo tnsnames.ora de saudação:

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. Crie hello Golden Gate contas de usuário e de proprietário.

  > [!NOTE]
  > conta de proprietário de Olá deve ter o prefixo de C# #.
  >

    ```bash
    $ sqlplus / as sysdba
    SQL> CREATE USER C##GGADMIN identified by ggadmin;
    SQL> EXEC dbms_goldengate_auth.grant_admin_privilege('C##GGADMIN',container=>'ALL');
    SQL> GRANT DBA tooC##GGADMIN container=all;
    SQL> connect C##GGADMIN/ggadmin
    SQL> ALTER SESSION SET CONTAINER=PDB1;
    SQL> EXIT;
    ```

3. Crie conta de usuário de teste de Golden Gate hello:

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> @demo_ora_insert
  SQL> EXIT;
  ```

4. Configure o arquivo de parâmetro de extração de saudação.

 Inicie a interface de linha de comando de portão dourada hello (ggsci):

  ```bash
  $ sudo su - oracle
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> DBLOGIN USERID test@pdb1, PASSWORD test
  Successfully logged into database  pdb1
  GGSCI>  ADD SCHEMATRANDATA pdb1.test
  2017-05-23 15:44:25  INFO    OGG-01788  SCHEMATRANDATA has been added on schema test.
  2017-05-23 15:44:25  INFO    OGG-01976  SCHEMATRANDATA for scheduling columns has been added on schema test.

  GGSCI> EDIT PARAMS EXTORA
  ```
5. Adicione Olá toohello EXTRAIA o arquivo de parâmetro a seguir (por meio de comandos vi). Pressione a tecla Esc, ': wq!' arquivo toosave. 

  ```bash
  EXTRACT EXTORA
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTRAIL ./dirdat/rt  
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT 
  LOGALLSUPCOLS
  UPDATERECORDFORMAT COMPACT
  TABLE pdb1.test.TCUSTMER;
  TABLE pdb1.test.TCUSTORD;
  ```
6. Registrar extrair – extrair integrado:

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci

  GGSCI> dblogin userid C##GGADMIN, password ggadmin
  Successfully logged into database CDB$ROOT.

  GGSCI> REGISTER EXTRACT EXTORA DATABASE CONTAINER(pdb1)

  2017-05-23 15:58:34  INFO    OGG-02003  Extract EXTORA successfully registered with database at SCN 1821260.

  GGSCI> exit
  ```
7. Configurar pontos de verificação de extração e iniciar a extração em tempo real:

  ```bash
  $ ./ggsci
  GGSCI>  ADD EXTRACT EXTORA, INTEGRATED TRANLOG, BEGIN NOW
  EXTRACT (Integrated) added.

  GGSCI>  ADD RMTTRAIL ./dirdat/rt, EXTRACT EXTORA, MEGABYTES 10
  RMTTRAIL added.

  GGSCI>  START EXTRACT EXTORA

  Sending START request tooMANAGER ...
  EXTRACT EXTORA starting

  GGSCI > info all

  Program     Status      Group       Lag at Chkpt  Time Since Chkpt

  MANAGER     RUNNING
  EXTRACT     RUNNING     EXTORA      00:00:11      00:00:04
  ```
Nesta etapa, você deve encontrar hello iniciando SCN, que será usado mais tarde, em uma seção diferente:

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> SELECT current_scn from v$database;
  CURRENT_SCN
  -----------
      1857887
  SQL> EXIT;
  ```

  ```bash
  $ ./ggsci
  GGSCI> EDIT PARAMS INITEXT
  ```

  ```bash
  EXTRACT INITEXT
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTASK REPLICAT, GROUP INITREP
  TABLE pdb1.test.*, SQLPREDICATE 'AS OF SCN 1857887'; 
  ```

  ```bash
  GGSCI> ADD EXTRACT INITEXT, SOURCEISTABLE
  ```

### <a name="set-up-service-on-myvm2-replicate"></a>Configuração de serviço no myVM2 (replicação)


1. Criar ou atualizar o arquivo tnsnames.ora de saudação:

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. Crie uma conta de replicação:

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> create user repuser identified by rep_pass container=current;
  SQL> grant dba toorepuser;
  SQL> exec dbms_goldengate_auth.grant_admin_privilege('REPUSER',container=>'PDB1');
  SQL> connect repuser/rep_pass@pdb1 
  SQL> EXIT;
  ```

3. Crie uma conta de usuário de teste Golden Gate:

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> EXIT;
  ```

4. Alterações de tooreplicate de arquivo de parâmetro de réplicas: 

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS REPORA  
  ```
  Conteúdo do arquivo de parâmetro REPORA:

  ```bash
  REPLICAT REPORA
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/repora.dsc, PURGE, MEGABYTES 100
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT
  DBOPTIONS INTEGRATEDPARAMS(parallelism 6)
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;
  ```

5. Configure um ponto de verificação de réplicas:

  ```bash
  GGSCI> ADD REPLICAT REPORA, INTEGRATED, EXTTRAIL ./dirdat/rt
  GGSCI> EDIT PARAMS INITREP

  ```

  ```bash
  REPLICAT INITREP
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/tcustmer.dsc, APPEND
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;   
  ```

  ```bash
  GGSCI> ADD REPLICAT INITREP, SPECIALRUN
  ```

### <a name="set-up-hello-replication-myvm1-and-myvm2"></a>Configurar a replicação de saudação (myVM1 e myVM2)

#### <a name="1-set-up-hello-replication-on-myvm2-replicate"></a>1. Configurar a replicação de saudação em myVM2 (replicação)

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS MGR
  ```
Atualize o arquivo de saudação com os seguintes hello:

  ```bash
  PORT 7809
  ACCESSRULE, PROG *, IPADDR *, ALLOW
  ```
Reinicie o serviço de Gerenciador de saudação:

  ```bash
  GGSCI> STOP MGR
  GGSCI> START MGR
  GGSCI> EXIT
  ```

#### <a name="2-set-up-hello-replication-on-myvm1-primary"></a>2. Configurar a replicação de saudação em myVM1 (primário)

Inicie o carregamento inicial hello e verifique se há erros:

```bash
$ cd /u01/app/oracle/product/12.1.0/oggcore_1
$ ./ggsci
GGSCI> START EXTRACT INITEXT
GGSCI> VIEW REPORT INITEXT
```
#### <a name="3-set-up-hello-replication-on-myvm2-replicate"></a>3. Configurar a replicação de saudação em myVM2 (replicação)

Alterar Olá número SCN com número de saudação obtido antes de:

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  START REPLICAT REPORA, AFTERCSN 1857887
  ```
replicação de saudação foi iniciado e você pode testá-lo pela inserção de novas tabelas tooTEST de registros.


### <a name="view-job-status-and-troubleshooting"></a>Exibir o status do trabalho e solução de problemas

#### <a name="view-reports"></a>Exibir relatórios
tooview relata myVM1, execute Olá comandos a seguir:

  ```bash
  GGSCI> VIEW REPORT EXTORA 
  ```
 
tooview relata myVM2, execute Olá comandos a seguir:

  ```bash
  GGSCI> VIEW REPORT REPORA
  ```

#### <a name="view-status-and-history"></a>Exibir o status e histórico
tooview status e o histórico no myVM1, execute Olá comandos a seguir:

  ```bash
  GGSCI> dblogin userid c##ggadmin, password ggadmin 
  GGSCI> INFO EXTRACT EXTORA, DETAIL
  ```

tooview status e o histórico no myVM2, execute Olá comandos a seguir:

  ```bash
  GGSCI> dblogin userid repuser@pdb1 password rep_pass 
  GGSCI> INFO REP REPORA, DETAIL
  ```
Isso conclui a saudação instalação e configuração de porta de Golden em Oracle linux.


## <a name="delete-hello-virtual-machine"></a>Excluir a máquina virtual de saudação

Quando ele não for mais necessário, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação, VM e recursos todos relacionados.

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Próximas etapas

[Tutorial Criar máquinas virtuais altamente disponíveis](../../linux/create-cli-complete.md)

[Explorar as amostras de CLI de implantação de VM](../../linux/cli-samples.md)
