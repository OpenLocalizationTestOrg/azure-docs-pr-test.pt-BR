---
title: aaaCreate um banco de dados Oracle em uma VM do Azure | Microsoft Docs
description: Coloque rapidamente em funcionamento um banco de dados Oracle Database 12c no ambiente do Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/17/2017
ms.author: rclaus
ms.openlocfilehash: 83205154c3275d5f57b46c8acfb0cb4e5c68a412
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-oracle-database-in-an-azure-vm"></a>Criar um Banco de Dados Oracle em uma VM do Azure

Esses detalhes de guia usando Olá CLI do Azure toodeploy uma máquina virtual do Azure de saudação [imagem da Galeria marketplace Oracle](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) em ordem toocreate um banco de dados Oracle 12c. Depois que o servidor de saudação for implantado, você se conecta por meio do SSH no banco de dados da Oracle Olá ordem tooconfigure. 

Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este guia de início rápido requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Criar um grupo de recursos

Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando. Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados. 

Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```
## <a name="create-virtual-machine"></a>Criar máquina virtual

toocreate uma máquina virtual (VM), use Olá [criar vm az](/cli/azure/vm#create) comando. 

Olá, exemplo a seguir cria uma VM denominada `myVM`. Ele também criará chaves SSH, se elas ainda não existirem em um local de chave padrão. toouse um conjunto específico de chaves, use Olá `--ssh-key-value` opção.  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --admin-username azureuser \
    --generate-ssh-keys
```

Depois de criar hello VM, CLI do Azure exibe informações toohello semelhante exemplo a seguir. Observe o valor de saudação para `publicIpAddress`. Usar o hello de tooaccess esse endereço VM.

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/{snip}/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westus",
  "macAddress": "00-0D-3A-36-2F-56",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.104.241",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="connect-toohello-vm"></a>Conecte-se toohello VM

toocreate uma sessão SSH com hello VM, use Olá comando a seguir. Substitua o endereço IP de saudação com hello `publicIpAddress` valor para a VM.

```bash 
ssh <publicIpAddress>
```

## <a name="create-hello-database"></a>Criar banco de dados de saudação

Olá software Oracle já está instalado na imagem do Marketplace hello. Crie um banco de dados de exemplo da seguinte maneira. 

1.  Alternar toohello *oracle* superusuário, em seguida, inicializar o ouvinte de saudação para registro em log:

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    ```

    saída de Hello é a seguir toohello semelhante:

    ```bash
    Copyright (c) 1991, 2014, Oracle.  All rights reserved.

    Starting /u01/app/oracle/product/12.1.0/dbhome_1/bin/tnslsnr: please wait...

    TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Log messages written too/u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))

    Connecting too(ADDRESS=(PROTOCOL=tcp)(HOST=)(PORT=1521))
    STATUS of hello LISTENER
    ------------------------
    Alias                     LISTENER
    Version                   TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Start Date                23-MAR-2017 15:32:08
    Uptime                    0 days 0 hr. 0 min. 0 sec
    Trace Level               off
    Security                  ON: Local OS Authentication
    SNMP                      OFF
    Listener Log File         /u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening Endpoints Summary...
    (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))
    hello listener supports no services
    hello command completed successfully
    ```

2.  Crie banco de dados de saudação:

    ```bash
    dbca -silent \
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

    Ele usa o banco de dados Olá toocreate de alguns minutos.

3. Definir variáveis do Oracle

Antes de você se conectar, você precisa tooset duas variáveis de ambiente: *ORACLE_HOME* e *ORACLE_SID*.

```bash
ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
ORACLE_SID=cdb1; export ORACLE_SID
```
Você também pode adicionar ORACLE_HOME e ORACLE_SID arquivo de. bashrc toohello de variáveis. Isso salvará as variáveis de ambiente Olá para futuras entradas. Confirme a seguir Olá instruções foram adicionadas toohello `~/.bashrc` arquivo usando o editor de sua escolha.

```bash
# Add ORACLE_HOME. 
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1 
# Add ORACLE_SID. 
export ORACLE_SID=cdb1 
```

## <a name="oracle-em-express-connectivity"></a>Conectividade com o Oracle EM Express

Para uma ferramenta de gerenciamento de GUI que você pode usar o banco de dados do tooexplore hello, configure o Oracle EM Express. tooconnect tooOracle EM Express, você deve primeiro configurar porta Olá no Oracle. 

1. Conecte o banco de dados de tooyour usando sqlplus:

    ```bash
    sqlplus / as sysdba
    ```

2. Uma vez conectado, defina a porta de saudação 5502 para Express EM

    ```bash
    exec DBMS_XDB_CONFIG.SETHTTPSPORT(5502);
    ```

3. Contêiner Olá abrir PDB1 se não já aberto, mas primeiro verificar o status de saudação:

    ```bash
    select con_id, name, open_mode from v$pdbs;
    ```

    saída de Hello é a seguir toohello semelhante:

    ```bash
      CON_ID NAME                           OPEN_MODE 
      ----------- ------------------------- ---------- 
      2           PDB$SEED                  READ ONLY 
      3           PDB1                      MOUNT
    ```

4. Se Olá OPEN_MODE para `PDB1` não é leitura-gravação, em seguida, execute Olá seguinte comandos tooopen PDB1:

   ```bash
    alter session set container=pdb1;
    alter database open;
   ```

Você precisa tootype `quit` tooend Olá sqlplus sessão e o tipo `exit` toologout saudação do usuário do oracle.

## <a name="automate-database-startup-and-shutdown"></a>Automatizar a inicialização e o desligamento do banco de dados

banco de dados do Oracle Olá por padrão não for iniciado automaticamente quando você reiniciar Olá VM. tooset backup toostart de banco de dados Oracle Olá automaticamente, primeiro entrar como raiz. Em seguida, crie e atualize alguns arquivos do sistema.

1. Conectar-se como raiz
    ```bash
    sudo su -
    ```

2.  Usando seu editor favorito, edite o arquivo hello `/etc/oratab` e alterar o padrão de saudação `N` muito`Y`:

    ```bash
    cdb1:/u01/app/oracle/product/12.1.0/dbhome_1:Y
    ```

3.  Crie um arquivo chamado `/etc/init.d/dbora` e colar Olá conteúdo a seguir:

    ```
    #!/bin/sh
    # chkconfig: 345 99 10
    # Description: Oracle auto start-stop script.
    #
    # Set ORA_HOME toobe equivalent too$ORACLE_HOME.
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle

    case "$1" in
    'start')
        # Start hello Oracle databases:
        # hello following command assumes that hello Oracle sign-in
        # will not prompt hello user for any values.
        # Remove "&" if you don't want startup as a background process.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" &
        touch /var/lock/subsys/dbora
        ;;

    'stop')
        # Stop hello Oracle databases:
        # hello following command assumes that hello Oracle sign-in
        # will not prompt hello user for any values.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" &
        rm -f /var/lock/subsys/dbora
        ;;
    esac
    ```

4.  Altere as permissões nos arquivos com *chmod* da seguinte maneira:

    ```bash
    chgrp dba /etc/init.d/dbora
    chmod 750 /etc/init.d/dbora
    ```

5.  Crie links simbólicos para inicialização e desligamento, da seguinte maneira:

    ```bash
    ln -s /etc/init.d/dbora /etc/rc.d/rc0.d/K01dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc3.d/S99dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc5.d/S99dbora
    ```

6.  tootest as alterações, reinicie Olá VM:

    ```bash
    reboot
    ```

## <a name="open-ports-for-connectivity"></a>Abrir as portas para conectividade

tarefa final Olá é tooconfigure alguns pontos de extremidade externos. tooset backup Olá grupo de segurança de rede do Azure que protege Olá VM, primeiro a sair de sua sessão de SSH no hello VM (deve ter sido iniciada sem SSH ao reinicializar na etapa anterior). 

1.  ponto de extremidade de saudação do tooopen que você use o banco de dados do Oracle tooaccess Olá remotamente, crie uma regra de grupo de segurança de rede com [criar regra de nsg rede az](/cli/azure/network/nsg/rule#create) da seguinte maneira: 

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup\
        --nsg-name myVmNSG \
        --name allow-oracle \
        --protocol tcp \
        --priority 1001 \
        --destination-port-range 1521
    ```

2.  ponto de extremidade de saudação do tooopen que você use tooaccess Oracle EM Express remotamente, crie uma regra de grupo de segurança de rede com [criar regra de nsg rede az](/cli/azure/network/nsg/rule#create) da seguinte maneira:

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup \
        --nsg-name myVmNSG \
        --name allow-oracle-EM \
        --protocol tcp \
        --priority 1002 \
        --destination-port-range 5502
    ```

3. Se necessário, obtenha o endereço IP público de saudação da VM novamente com [az rede ip público exibir](/cli/azure/network/public-ip#show) da seguinte maneira:

    ```azurecli-interactive
    az network public-ip show \
        --resource-group myResourceGroup \
        --name myVMPublicIP \
        --query [ipAddress] \
        --output tsv
    ```

4.  Conecte-se ao EM Express pelo navegador. Verifique se o seu navegador é compatível com EM Express (é necessário ter Flash instalado): 

    ```
    https://<VM ip address or hostname>:5502/em
    ```

Você pode fazer logon usando Olá **SYS** conta e verificar Olá **como sysdba** caixa de seleção. Usar a senha de saudação **OraPasswd1** que podem ser definidas durante a instalação. 

![Captura de tela da página de logon Oracle OEM Express Olá](./media/oracle-quick-start/oracle_oem_express_login.png)

## <a name="clean-up-resources"></a>Limpar recursos

Depois de terminar de explorar seu primeiro banco de dados Oracle no Azure e hello VM não é mais necessário, você pode usar o hello [excluir grupo de az](/cli/azure/group#delete) tooremove grupo de recursos de saudação, a VM e relacionados com todos os recursos de comando.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre outras [Soluções Oracle no Azure](oracle-considerations.md). 

Tente Olá [instalando e configurando o Oracle Automated Storage Management](configure-oracle-asm.md) tutorial.
