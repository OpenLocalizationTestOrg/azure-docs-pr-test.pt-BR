---
title: " Gerenciar um servidor de processo de escalonamento horizontal no Azure Site Recovery | Microsoft Docs"
description: "Este artigo descreve como tooset e gerenciar um servidor de processo de expansão no Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 3d72f9c2c7014a4ff2fa2af168aa55ad1452eae5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-scale-out-process-server"></a>Gerenciar um servidor de processo de escalonamento horizontal

Servidor de processo de expansão atua como um coordenador para transferir dados entre os serviços de recuperação de Site hello e sua infraestrutura local. Este artigo descreve como você pode definir, configurar e gerenciar um servidor de processo de escalonamento horizontal.

## <a name="prerequisites"></a>Pré-requisitos
Olá seguem Olá recomendados de hardware, software e rede configuração necessária tooset um servidor de processo de expansão.

> [!NOTE]
> [Planejamento de capacidade](site-recovery-capacity-planner.md) é um tooensure etapa importante que você implante Olá expansão de servidor de processo com uma configuração que conjuntos de seus requisitos de carga. Leia mais sobre [Características de dimensionamento de um servidor de processo de escalonamento horizontal](#sizing-requirements-for-a-configuration-server).

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-scale-out-process-server-software"></a>Baixar o software de servidor de processo de expansão Olá
1. Faça logon no toohello tooyour Azure portal e procurar o Cofre de serviços de recuperação.
2. Procurar muito**infra-estrutura de recuperação de Site** > **servidores de configuração** (no VMware para o & máquinas físicas).
3. Selecione seu toodrill do servidor de configuração para baixo na página de detalhes do servidor de configuração hello.
4. Clique em Olá **+ servidor de processo** botão.
5. Em Olá **do servidor em processo de adicionar** página, selecione **local do servidor de processo de implantar uma expansão** opção de saudação **escolha onde você deseja toodeploy seu servidor de processo** lista suspensa.

  ![Página Adicionar Servidores](./media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. Clique em Olá **Download Olá instalação unificado do Microsoft Azure Site Recovery** versão mais recente do link toodownload Olá da instalação do servidor de processo Olá expansão.

  > [!WARNING]
  Olá versão do seu servidor de processo de expansão deve ser igual tooor menor que a versão de servidor de configuração de saudação em execução no seu ambiente. Compatibilidade de versão de tooensure uma maneira simples é toouse Olá mesmo bits de instalador que você usou recentemente tooinstall/atualizar seu servidor de configuração.

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a>Instalar e registrar um servidor de processo de escalonamento horizontal por meio da GUI
Se você tiver tooscale sua implantação, além de 200 máquinas de origem, ou um total diário variação taxa de mais de 2 TB, você precisa o volume de tráfego de saudação do processo adicional servidores toohandle.

Verificar Olá [tamanho recomendações para servidores de processo](#size-recommendations-for-the-process-server)e, em seguida, siga tooset essas instruções backup do servidor de processo hello. Depois de configurar o servidor de saudação, migrar fonte máquinas toouse-lo.

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a>Instalar e registrar um servidor de processo de escalonamento horizontal usando a linha de comando

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a>Amostra de uso
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a>Argumentos de linha de comando do instalador do servidor de processo de escalonamento horizontal.
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a>Criar um arquivo de configuração de configurações de proxy
O parâmetro ProxySettingsFilePath utiliza um arquivo como entrada. Crie o arquivo usando Olá seguinte formato e passá-lo como parâmetro de entrada ProxySettingsFilePath.
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a>Modificando configurações de proxy do servidor de processo de escalonamento horizontal
1. Faça logon no servidor de processo de escalonamento horizontal.
2. Abra uma janela de comando do PowerShell do Administrador.
3. Olá executar comando a seguir
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. Procurar próximo diretório toohello **%PROGRAMDATA%\ASR\Agent** e o comando a seguir Olá execução
  ```
  cmd
  cdpcli.exe --registermt

  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a>Registrando novamente um servidor de processo de escalonamento horizontal
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* Em seguida, abra um prompt de comando de Administrador.
* Procurar diretório de toohello **%PROGRAMDATA%\ASR\Agent** e execute o comando Olá

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a>Atualizando um servidor de processo de escalonamento horizontal
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a>Desativando um servidor de processo de escalonamento horizontal
1. Verifique se:
  - Mostra o estado de conexão do servidor de configuração como **conectado** em Olá portal do Azure
  - Servidor de processo é ainda poderá toocommunicate com o servidor de configuração de saudação.
2. Faça logon no servidor de processo toohello como um administrador
3. Abrir o Painel de Controle > Programa > Desinstalar Programas
4. Desinstale programas Olá na sequência de saudação fornecida a seguir:
  * Servidor de processo/servidor de configuração do Microsoft Azure Site Recovery
  * Dependências de servidor de configuração do Microsoft Azure Site Recovery
  * Agente de Serviços dos Serviços de Recuperação do Microsoft Azure

Pode levar até too15 minutos de saudação do servidor em processo exclusão tooreflect no portal do Azure de saudação.

  > [!NOTE]
  Se o servidor de processo de saudação é toocommunicate não é possível com hello configuração de servidor (estado de Conexão no portal está desconectado), em seguida, você precisa toofollow Olá seguindo as etapas toopurge-lo da saudação servidor de configuração.

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a>Cancelando o registro de um servidor de processo de escalonamento horizontal desconectado de um servidor de configuração

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a>Requisitos de dimensionamento para um servidor de processo de escalonamento horizontal

| **Servidor de processo adicional** | **Tamanho do disco de cache** | **Taxa de alteração de dados** | **Computadores protegidos** |
| --- | --- | --- | --- |
|4 vCPUs (2 soquetes * 2 núcleos @ 2,5 GHz), 8 GB de memória |300 GB |250 GB ou menos |Replique 85 computadores ou menos. |
|8 vCPUs (2 soquetes * 4 núcleos @ 2,5 GHz), 12 GB de memória |600 GB |250 GB too1 TB |Replique entre 85 e 150 computadores. |
|12 vCPUs (2 soquetes * 6 núcleos @ 2,5 GHz), 24 GB de memória |1 TB |1 TB too2 TB |Replique entre 150 e 225 computadores. |
