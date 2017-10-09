---
title: "Olá aaaUpdate agente Linux do Azure do GitHub | Microsoft Docs"
description: "Saiba como tooupdate agente Linux do Azure para sua VM do Linux no Azure toohello a versão mais recente do GitHub"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: f1f19300-987d-4f29-9393-9aba866f049c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: mingzhan
ms.openlocfilehash: 4ce7c56efc1e6563e6415f7687573f9fb9e7b4c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-hello-azure-linux-agent-on-a-vm"></a>Como tooupdate hello Azure Linux Agent em uma máquina virtual

tooupdate seu [agente Linux do Azure](https://github.com/Azure/WALinuxAgent) em uma VM do Linux no Azure, você já deve ter:

- uma VM do Linux em execução no Azure.
- Uma conexão toothat VM Linux usando o SSH.

Você sempre deve verificar um pacote no repositório de distribuição de Linux Olá primeiro. É possível pacote de saudação disponível não pode ser versão mais recente do hello, no entanto, habilitar a atualização automática garantirá Olá agente Linux sempre obterá a atualização mais recente da saudação. Se você tiver problemas ao instalar o gerenciadores de pacotes de saudação, busque o suporte do fornecedor de distribuição de saudação.

## <a name="updating-hello-azure-linux-agent"></a>Atualizando Olá agente Linux do Azure

## <a name="ubuntu"></a>Ubuntu

#### <a name="check-your-current-package-version"></a>Verificar a versão atual do pacote

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a>Cache do pacote de atualização

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>Instalar a versão mais recente do pacote de saudação

```bash
sudo apt-get install walinuxagent
```

#### <a name="ensure-auto-update-is-enabled"></a>Verificar se a atualização automática está habilitada

Primeiro, verifique toosee se ela está habilitada:

```bash
cat /etc/waagent.conf
```

Localize 'AutoUpdate.Enabled'. Se você vir esta saída, ela estará habilitada:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable executar:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Reinicie o serviço de waagent Olá

#### <a name="restart-agent-for-1404"></a>Reinicie o agente para 14.04

```bash
initctl restart walinuxagent
```

#### <a name="restart-agent-for-1604--1704"></a>Reinicie o agente para 16.04 / 17.04

```bash
systemctl restart walinuxagent.service
```

## <a name="debian"></a>Debian

### <a name="debian-7-wheezy"></a>Debian 7 "Wheezy"

#### <a name="check-your-current-package-version"></a>Verificar a versão atual do pacote

```bash
dpkg -l | grep waagent
```

#### <a name="update-package-cache"></a>Cache do pacote de atualização

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>Instalar a versão mais recente do pacote de saudação

```bash
sudo apt-get install waagent
```

#### <a name="enable-agent-auto-update"></a>Habilitar atualização automática do agente
Esta versão do Debian não tem uma versão maior ou igual à 2.0.16, portanto, a Atualização automática não está disponível para ele. saída de saudação do hello acima comando mostrará se o pacote de saudação está atualizado.

### <a name="debian-8-jessie--debian-9-stretch"></a>Debian 8 "Jessie"/Debian 9 "Stretch"

#### <a name="check-your-current-package-version"></a>Verificar a versão atual do pacote

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a>Cache do pacote de atualização

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>Instalar a versão mais recente do pacote de saudação

```bash
sudo apt-get install waagent
```
#### <a name="ensure-auto-update-is-enabled"></a>Verificar se a atualização automática está habilitada 

Primeiro, verifique toosee se ela está habilitada:

```bash
cat /etc/waagent.conf
```

Localize 'AutoUpdate.Enabled'. Se você vir esta saída, ela estará habilitada:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable executar:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Reinicie o serviço de waagent Olá

```
sudo systemctl restart walinuxagent.service
```

## <a name="redhat--centos"></a>Redhat/CentOS

### <a name="rhelcentos-6"></a>RHEL/CentOS 6

#### <a name="check-your-current-package-version"></a>Verificar a versão atual do pacote

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a>Verificar as atualizações disponíveis

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a>Instalar a versão mais recente do pacote de saudação

```bash
sudo yum install WALinuxAgent
```

#### <a name="ensure-auto-update-is-enabled"></a>Verificar se a atualização automática está habilitada 

Primeiro, verifique toosee se ela está habilitada:

```bash
cat /etc/waagent.conf
```

Localize 'AutoUpdate.Enabled'. Se você vir esta saída, ela estará habilitada:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable executar:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Reinicie o serviço de waagent Olá

```
sudo service waagent restart
```

### <a name="rhelcentos-7"></a>RHEL/CentOS 7

#### <a name="check-your-current-package-version"></a>Verificar a versão atual do pacote

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a>Verificar as atualizações disponíveis

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a>Instalar a versão mais recente do pacote de saudação

```bash
sudo yum install WALinuxAgent  
```

#### <a name="ensure-auto-update-is-enabled"></a>Verificar se a atualização automática está habilitada 

Primeiro, verifique toosee se ela está habilitada:

```bash
cat /etc/waagent.conf
```

Localize 'AutoUpdate.Enabled'. Se você vir esta saída, ela estará habilitada:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable executar:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Reinicie o serviço de waagent Olá

```bash
sudo systemctl restart waagent.service
```

## <a name="suse-sles"></a>SUSE SLES

### <a name="suse-sles-11-sp4"></a>SUSE SLES 11 SP4

#### <a name="check-your-current-package-version"></a>Verificar a versão atual do pacote

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a>Verificar as atualizações disponíveis

Olá acima saída mostrará se o pacote de saudação é o toodate.

#### <a name="install-hello-latest-package-version"></a>Instalar a versão mais recente do pacote de saudação

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a>Verificar se a atualização automática está habilitada 

Primeiro, verifique toosee se ela está habilitada:

```bash
cat /etc/waagent.conf
```

Localize 'AutoUpdate.Enabled'. Se você vir esta saída, ela estará habilitada:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable executar:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Reinicie o serviço de waagent Olá

```bash
sudo /etc/init.d/waagent restart
```

### <a name="suse-sles-12-sp2"></a>SUSE SLES 12 SP2

#### <a name="check-your-current-package-version"></a>Verificar a versão atual do pacote

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a>Verificar as atualizações disponíveis

Na saída de saudação do hello acima, isso mostrará se o pacote de saudação está atualizada.

#### <a name="install-hello-latest-package-version"></a>Instalar a versão mais recente do pacote de saudação

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a>Verificar se a atualização automática está habilitada 

Primeiro, verifique toosee se ela está habilitada:

```bash
cat /etc/waagent.conf
```

Localize 'AutoUpdate.Enabled'. Se você vir esta saída, ela estará habilitada:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable executar:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Reinicie o serviço de waagent Olá

```bash
sudo systemctl restart waagent.service
```

## <a name="oracle-6-and-7"></a>Oracle 6 e 7

Para Oracle Linux, certifique-se de que Olá `Addons` repositório está habilitado. Escolha o arquivo de saudação tooedit `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) ou `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux) e altere a linha hello `enabled=0` muito`enabled=1` em **[ol6_addons]** ou **[ol7_addons]** Nesse arquivo.

Em seguida, tooinstall Olá versão mais recente do hello agente Linux do Azure, tipo:

```bash
sudo yum install WALinuxAgent
```

Se você não encontrar o repositório de complemento Olá você pode simplesmente adicionar essas linhas no final de saudação do arquivo .repo tooyour Oracle Linux versão de acordo com:

Para máquinas virtuais do Oracle Linux 6:

```sh
[ol6_addons]
name=Add-Ons for Oracle Linux $releasever ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/addons/x86_64
gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
gpgcheck=1
enabled=1
```

Para máquinas virtuais do Oracle Linux 7:

```sh
[ol7_addons]
name=Oracle Linux $releasever Add ons ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/addons/$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=0
```

Em seguida, digite:

```bash
sudo yum update WALinuxAgent
```

Normalmente, isso é tudo o que precisa, mas se por alguma razão, que você precisa tooinstall do https://github.com diretamente, use Olá seguindo as etapas.


## <a name="update-hello-linux-agent-when-no-agent-package-exists-for-distribution"></a>Saudação de atualização quando nenhum pacote do agente de distribuição de agentes do Linux

Instalar wget (há algumas distribuições que não instalação-lo por padrão, como Redhat, CentOS e Oracle Linux versões 6.4 e 6.5) digitando `sudo yum install wget` na linha de comando hello.

### <a name="1-download-hello-latest-version"></a>1. Baixar a versão mais recente da saudação
Abra [Olá versão do agente Linux do Azure no GitHub](https://github.com/Azure/WALinuxAgent/releases) em uma página da web e descobrir o número de versão mais recente da saudação. (Você pode localizar sua versão atual digitando `waagent --version`.)

#### <a name="for-version-22x-or-later-type"></a>Para a versão 2.2. x ou posterior, digite:
```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.x.zip
unzip v2.2.x.zip.zip
cd WALinuxAgent-2.2.x
```

Olá linha a seguir usa a versão 2.2.0 como um exemplo:

```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.14.zip
unzip v2.2.14.zip  
cd WALinuxAgent-2.2.14
```

### <a name="2-install-hello-azure-linux-agent"></a>2. Instalar Olá agente Linux do Azure

#### <a name="for-version-22x-use"></a>Para a versão 2.2. x, use:
Talvez seja necessário um pacote de saudação tooinstall `setuptools` primeiro – consulte [aqui](https://pypi.python.org/pypi/setuptools). Em seguida, execute:

```bash
sudo python setup.py install
```

#### <a name="ensure-auto-update-is-enabled"></a>Verificar se a atualização automática está habilitada

Primeiro, verifique toosee se ela está habilitada:

```bash
cat /etc/waagent.conf
```

Localize 'AutoUpdate.Enabled'. Se você vir esta saída, ela estará habilitada:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable executar:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="3-restart-hello-waagent-service"></a>3. Reinicie o serviço de waagent Olá
Para a maioria das distribuições do Linux:

```bash
sudo service waagent restart
```

Para o Ubuntu, use:

```bash
sudo service walinuxagent restart
```

Para o CoreOS, use:

```bash
sudo systemctl restart waagent
```

### <a name="4-confirm-hello-azure-linux-agent-version"></a>4. Confirmar hello Azure Linux Agent versão
    
```bash
waagent -version
```

Para CoreOS, Olá acima comando pode não funcionar.

Você verá que hello Azure Linux Agent versão tiver sido atualizada toohello nova versão.

Para obter mais informações sobre Olá agente Linux do Azure, consulte [Azure Linux Agent Leiame](https://github.com/Azure/WALinuxAgent).
