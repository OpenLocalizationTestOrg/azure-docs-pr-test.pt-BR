---
title: " Gerenciar um Servidor de Configuração no Azure Site Recovery | Microsoft Docs"
description: "Este artigo descreve como tooset e gerenciar um servidor de configuração."
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
ms.openlocfilehash: 2852bcd25409121be46a1ebf135ebfcdce6e5de5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-configuration-server"></a>Gerenciar um Servidor de Configuração

Servidor de configuração atua como um coordenador entre serviços de recuperação de Site hello e sua infraestrutura local. Este artigo descreve como você pode configurar, configurar e gerenciar Olá servidor de configuração.

## <a name="prerequisites"></a>Pré-requisitos
Olá seguem mínimos de hardware hello, software e rede configuração necessária tooset um servidor de configuração.

> [!NOTE]
> [Planejamento de capacidade](site-recovery-capacity-planner.md) é um tooensure etapa importante que você implante Olá servidor de configuração com uma configuração que conjuntos de seus requisitos de carga. Leia mais sobre [requisitos para um servidor de configuração de dimensionamento](#sizing-requirements-for-a-configuration-server).

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-configuration-server-software"></a>Baixar o software de servidor de configuração de saudação
1. Faça logon no toohello tooyour Azure portal e procurar o Cofre de serviços de recuperação.
2. Procurar muito**infra-estrutura de recuperação de Site** > **servidores de configuração** (no VMware para o & máquinas físicas).

  ![Página Adicionar Servidores](./media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. Clique em Olá **+ servidores** botão.
4. Em Olá **Adicionar servidor** , clique em chave de registro de Olá Olá Download botão toodownload. Você precisa essa chave durante a saudação tooregister de instalação de servidor de configuração com o serviço do Azure Site Recovery.
5. Clique em Olá **Download Olá instalação unificado do Microsoft Azure Site Recovery** versão mais recente do link toodownload Olá de saudação servidor de configuração.

  ![Página Download](./media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  Versão mais recente do hello servidor de configuração pode ser baixado diretamente do [página de download da Microsoft Download Center](http://aka.ms/unifiedsetup)

## <a name="installing-and-registering-a-configuration-server-from-gui"></a>Instalar e registrar um servidor de configuração da GUI
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a>Instalar e registrar um servidor de configuração usando a linha de comando

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
  ```

### <a name="sample-usage"></a>Exemplo de uso
  ```
  MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
  cd C:\Temp\Extracted
  UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "CS" /InstallLocation "D:\" /MySQLCredsFilePath "C:\Temp\MySQLCredentialsfile.txt" /VaultCredsFilePath "C:\Temp\MyVault.vaultcredentials" /EnvType "VMWare"
  ```


### <a name="configuration-server-installer-command-line-arguments"></a>Argumentos de linha de comando do instalador do servidor de configuração.
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-mysql-credentials-file"></a>Criar um arquivo de credenciais do MySql
Parâmetro MySQLCredsFilePath utiliza um arquivo como entrada. Crie arquivo de saudação usando Olá seguinte formato e passá-lo como parâmetro de entrada MySQLCredsFilePath.
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a>Criar um arquivo de configuração de configurações de proxy
O parâmetro ProxySettingsFilePath utiliza um arquivo como entrada. Crie arquivo de saudação usando Olá seguinte formato e passá-lo como parâmetro de entrada ProxySettingsFilePath.

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a>Modificando configurações de proxy de servidor de configuração
1. Logon tooyour servidor de configuração.
2. Iniciar cspsconfigtool.exe hello usando o atalho de saudação em seu.
3. Clique em Olá **registro do cofre** guia.
4. Download de um novo arquivo de registro do cofre no portal de saudação e fornecê-la como ferramenta de toohello de entrada.

  ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. Fornecer novos detalhes do servidor Proxy hello e clique em Olá **registrar** botão.
6. Abra uma janela de comando do PowerShell do Administrador.
7. Olá executar comando a seguir
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  Se você tiver servidores de processo de expansão anexado toothis servidor de configuração, é necessário muito[corrigir as configurações de proxy de saudação em todos os servidores de processo de expansão Olá](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) em sua implantação.

## <a name="re-register-a-configuration-server-with-hello-same-recovery-services-vault"></a>Registrar novamente um servidor de configuração com hello mesmo Cofre de serviços de recuperação
  1. Logon tooyour servidor de configuração.
  2. Inicie cspsconfigtool.exe hello usando o atalho de saudação na área de trabalho.
  3. Clique em Olá **registro do cofre** guia.
  4. Baixe um novo arquivo de registro do portal hello e fornecê-la como ferramenta de toohello de entrada.
        ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
  5. Fornecer detalhes de servidor Proxy hello e clique em Olá **registrar** botão.  
  6. Abra uma janela de comando do PowerShell do Administrador.
  7. Olá executar comando a seguir

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  Se você tiver servidores de processo de expansão anexado toothis servidor de configuração, é necessário muito[registrar novamente todos os servidores de processo de expansão Olá](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) em sua implantação.

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a>Registrar um servidor de configuração com um cofre de serviços de recuperação diferente.
1. Logon tooyour servidor de configuração.
2. em um prompt de comando do administrador, execute o comando de saudação

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. Iniciar cspsconfigtool.exe hello usando o atalho de saudação em seu.
4. Clique em Olá **registro do cofre** guia.
5. Baixe um novo arquivo de registro do portal hello e fornecê-la como ferramenta de toohello de entrada.

    ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. Fornecer detalhes de servidor Proxy hello e clique em Olá **registrar** botão.  
7. Abra uma janela de comando do PowerShell do Administrador.
8. Olá executar comando a seguir
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a>Encerramento de um Servidor de Configuração
Certifique-se de seguir Olá antes de iniciar o encerramento de seu servidor de configuração.
1. Desabilite a proteção para todas as máquinas virtuais por este servidor de configuração.
2. Desassocie todas as políticas de replicação de saudação servidor de configuração.
3. Exclua todos os hosts de servidores/vSphere vCenters que estão associado toohello servidor de configuração.

### <a name="delete-hello-configuration-server-from-azure-portal"></a>Excluir Olá servidor de configuração do portal do Azure
1. No portal do Azure, procurar muito**infra-estrutura de recuperação de Site** > **servidores de configuração** no menu de cofre hello.
2. Clique em Olá servidor de configuração que você deseja toodecommission.
3. Na página de detalhes do servidor de configuração hello, clique botão de exclusão de saudação.

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.PNG)
4. Clique em **Sim** tooconfirm exclusão de saudação do servidor de saudação.

  >[!WARNING]
  Se você tiver máquinas virtuais, políticas de replicação ou hosts de servidores/vSphere vCenter associados a este servidor de configuração, você não pode excluir o servidor de saudação. Exclua essas entidades antes de tentar toodelete Cofre de saudação.

### <a name="uninstall-hello-configuration-server-software-and-its-dependencies"></a>Desinstalar o software de servidor de configuração de saudação e suas dependências
  > [!TIP]
  Se planejar Olá tooreuse servidor de configuração com o Azure Site Recovery novamente, em seguida, você poderá ignorar toostep 4 diretamente

1. Faça logon no toohello servidor de configuração como um administrador.
2. Abrir o Painel de Controle > Programa > Desinstalar Programas
3. Desinstale programas Olá Olá sequência a seguir:
  * Agente de Serviços dos Serviços de Recuperação do Microsoft Azure
  * Servidor de destino do Microsoft Azure Site Recovery mobilidade mestra do serviço
  * Provedor do Microsoft Azure Site Recovery
  * Servidor de processo/servidor de configuração do Microsoft Azure Site Recovery
  * Dependências de servidor de configuração do Microsoft Azure Site Recovery
  * MySQL Server 5.5
4. Execute hello comando a seguir e o prompt de comando do administrador.
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a>Renovar certificados de configuração de servidor Secure Socket Layer(SSL)
Olá, servidor de configuração tem uma servidor Web embutida, que coordena as atividades de saudação do hello serviço de mobilidade, servidores de processo, e servidores de destino mestre conectado toohello servidor de configuração. servidor da Web do servidor de configuração Olá usa um tooauthenticate de certificado SSL seus clientes. Este certificado tem uma expiração de três anos e poderá ser renovado a qualquer momento usando Olá método a seguir:

> [!WARNING]
Expiração do certificado pode ser executada somente na versão 9.4.XXXX. X ou superior. Atualizar todos os componentes hello Azure Site Recovery (servidor de configuração, servidor de processo, o servidor de destino mestre, serviço de mobilidade) antes de iniciar o fluxo de trabalho do hello renovar certificados.

1. Olá portal do Azure, procurar tooyour cofre > infraestrutura de recuperação do Site > Configuração do servidor.
2. Clique em servidor de configuração de saudação para as quais você precisa toorenew Olá certificado SSL para.
3. Em Olá integridade do servidor de configuração, você poderá ver a data de expiração de saudação para Olá certificado SSL.
4. Renovar certificado de saudação clicando Olá **renovar certificados** ação conforme Olá a imagem a seguir:

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.png)

### <a name="secure-socket-layer-certificate-expiry-warning"></a>Aviso de expiração de certificado SSL

> [!NOTE]
Olá a validade do certificado SSL para todas as instalações que ocorreram antes de maio de 2016 foi definida tooone ano. você iniciou vendo notificações de expiração do certificado aparecendo no hello portal do Azure.

1. Se certificado SSL do servidor de configuração Olá tooexpire em Olá próximos dois meses, o serviço de saudação inicia notificar os usuários por meio de saudação portal do Azure & email (necessário notificações de recuperação de Site tooAzure toobe assinado). Você começar a ver uma faixa de notificação na página de recursos de saudação do cofre.

  ![certificate-notification](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. Clique em detalhes adicionais do hello faixa tooget na expiração do certificado hello.

  ![certificate-details](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  Se em vez de um botão **Renovar Agora** você vir um botão **Atualizar Agora**. Isso significa que há alguns componentes em seu ambiente que ainda não foram atualizados too9.4.xxxx.x ou versões posteriores.

## <a name="sizing-requirements-for-a-configuration-server"></a>Requisitos de dimensionamento para um servidor de configuração

| **CPU** | **Memória** | **Tamanho do disco de cache** | **Taxa de alteração de dados** | **Computadores protegidos** |
| --- | --- | --- | --- | --- |
| 8 vCPUs (2 soquetes * 4 núcleos @ 2,5 GHz) |16 GB |300 GB |500 GB ou menos |Replicar máquinas menos de 100. |
| 12 vCPUs (2 soquetes * 6 núcleos @ 2,5 GHz) |18 GB |600 GB |500 GB too1 TB |Replique entre 100 e 150 computadores. |
| 16 vCPUs (2 soquetes * 8 núcleos @ 2,5 GHz) |32 GB |1 TB |1 TB too2 TB |Replique entre 150 e 200 computadores. |

  >[!TIP]
  Se a rotatividade de dados diariamente excede 2 TB, ou planejar tooreplicate mais de 200 máquinas virtuais, é recomendável tráfego de replicação toodeploy processo adicional servidores tooload saldo hello. Saiba mais sobre como os servidores de toodeploy o processo de expansão.


## <a name="common-issues"></a>Problemas comuns
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]
