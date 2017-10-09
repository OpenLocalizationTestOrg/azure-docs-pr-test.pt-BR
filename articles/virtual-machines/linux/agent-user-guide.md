---
title: "aaaAzure visão geral de agente de VM do Linux | Microsoft Docs"
description: "Saiba como tooinstall e configurar o agente do Linux (waagent) toomanage interação da sua máquina virtual com o controlador de malha do Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: e41de979-6d56-40b0-8916-895bf215ded6
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: szark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4e08c84d9205f4db7aae6fd1568ec1f15fba395c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-and-using-hello-azure-linux-agent"></a>Entendendo e usando Olá agente Linux do Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a>Introdução
Olá Microsoft Azure Linux Agent (waagent) gerencia Linux e FreeBSD provisionamento e interação de VM com hello controlador de malha do Azure. Ele fornece Olá funcionalidade para implantações do Linux e FreeBSD IaaS a seguir:

> [!NOTE]
> Consulte hello Azure Linux agent [Leiame](https://github.com/Azure/WALinuxAgent/blob/master/README.md) para obter detalhes adicionais.
> 
> 

* **Provisionamento de imagem**
  
  * Criação de uma conta de usuário
  * Configurando os tipos de autenticação do SSH
  * Implantação de chaves públicas do SSH e pares de chaves
  * Nome de host da saudação de configuração
  * Publicação Olá nome toohello plataforma de host DNS
  * SSH host impressão digital da chave toohello plataforma de relatórios
  * Gerenciamento de recursos de disco
  * Formatação e montar o disco de recurso Olá
  * Configurando o espaço de permuta
* **Rede**
  
  * Gerencia rotas tooimprove compatibilidade com servidores DHCP de plataforma
  * Garante a estabilidade de saudação do nome de interface de rede Olá
* **Kernel**
  
  * Configura NUMA virtual (desabilitar para kernel < 2.6.37)
  * Consome entropia de Hyper-V para /dev/random
  * Configura o tempo limite de SCSI para dispositivo de raiz da saudação (que poderia ser remoto)
* **Diagnostics**
  
  * Redirecionamento de console toohello porta serial
* **Implantações SCVMM**
  
  * Detecta e inicializa o agente do VMM Olá para Linux, quando executado em um ambiente do System Center Virtual Machine Manager 2012 R2
* **Extensão de VM**
  
  * Inserir componente criada pela Microsoft e de parceiros para a automação de software e configuração de VM do Linux (IaaS) tooenable
  * Implementação de referência de extensão de VM em [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)

## <a name="communication"></a>Comunicação
fluxo de informações de saudação do agente de toohello plataforma Olá ocorre por meio de dois canais:

* Um DVD anexado ao tempo de inicialização para as implementações de IaaS. DVD inclui um arquivo de configuração compatível com OVF que inclui todas as informações de provisionamento diferente Olá real pares de chaves SSH.
* Um ponto de extremidade TCP expor uma API REST usado tooobtain implantação e configuração de topologia.

## <a name="requirements"></a>Requisitos
Hello sistemas a seguir foram testados e que são conhecidos toowork com hello agente Linux do Azure:

> [!NOTE]
> Essa lista pode ser diferente da lista oficial de saudação de sistemas em Olá plataforma Microsoft Azure, conforme descrito aqui: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)
> 
> 

* CoreOS
* CentOS 6.3+
* Red Hat Enterprise Linux 6.7+
* Debian 7.0+
* Ubuntu 12.04+
* openSUSE 12.3+
* SLES 11 SP3+
* Oracle Linux 6.4+

Outros sistemas com suporte:

* FreeBSD 10+ (Agente Linux do Azure v2.0.10+)

agente do Linux Olá depende de alguns pacotes de sistema na ordem toofunction corretamente:

* Python 2.6+
* OpenSSL 1.0+
* OpenSSH 5.3+
* Utilitários de sistema de arquivos: sfdisk, fdisk, mkfs, parted
* Ferramentas de senha: chpasswd, sudo
* Ferramentas de processamento de texto: sed, grep
* Ferramentas de rede: roteamento ip
* Suporte a kernel para montar sistemas de arquivos UDF.

## <a name="installation"></a>Instalação
Instalação usando um RPM ou um pacote de DEB do repositório de pacotes de distribuição é o método preferido de saudação instalando e atualizando Olá agente Linux do Azure. Saudação de todos os [aprovados provedores distribuição](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrar o pacote de saudação do agente Linux do Azure em suas imagens e repositórios.

Consulte a documentação do toohello em Olá [repositório de agente Linux do Azure no GitHub](https://github.com/Azure/WALinuxAgent) para opções de instalação avançada, como instalação de locais de origem ou toocustom ou prefixos.

## <a name="command-line-options"></a>Opções de linha de comando
### <a name="flags"></a>Sinalizadores
* verbose: aumentar o nível de detalhes do comando especificado
* forçar: Ignorar confirmação interativa para alguns comandos

### <a name="commands"></a>Comandos
* Ajuda: lista de sinalizadores e comandos de saudação com suporte.
* desprovisionamento: tentativa de sistema de saudação tooclean e torná-lo adequado para provisionamento novamente. Esta operação excluídos seguinte hello:
  
  * Todas as chaves de host do SSH (se Provisioning.RegenerateSshHostKeyPair for 'y' no arquivo de configuração de saudação)
  * Configuração de servidor de nomes em /etc/resolv.conf
  * Senha de raiz de /etc/shadow (se Provisioning.DeleteRootPassword for 'y' no arquivo de configuração de saudação)
  * Concessões de cliente DHCP em cache
  * Redefine toolocalhost.localdomain de nome de host

> [!WARNING]
> Desprovisionamento não garante que essa imagem Olá é limpo de todas as informações confidenciais e adequada para redistribuição.
> 
> 

* desprovisionamento + user: executa tudo sob - desprovisionamento (acima) e também exclui a conta de usuário provisionado última hello (obtida /var/lib/waagent) e dados associados. Este parâmetro é quando a desconfiguração de uma imagem que foi anteriormente provisionamento no Azure para podem ser capturada e usada novamente.
* versão: exibe a versão de saudação do waagent
* serialconsole: configura GRUB toomark ttyS0 (Olá a primeira porta serial) como o console de inicialização de saudação. Isso garante que os logs de inicialização do kernel são enviadas de porta serial toothe e disponibilizados para depuração.
* o daemon: executar waagent como uma interação de toomanage daemon com a plataforma de saudação. Esse argumento é toowaagent especificado no script de inicialização de waagent hello.
* Iniciar: executar waagent como um processo em segundo plano

## <a name="configuration"></a>Configuração
Um arquivo de configuração (/ etc/waagent.conf) controles Olá ações de waagent. Uma amostra do arquivo de configuração é mostrada abaixo:

    Provisioning.Enabled=y
    Provisioning.DeleteRootPassword=n
    Provisioning.RegenerateSshHostKeyPair=y
    Provisioning.SshHostKeyPairType=rsa
    Provisioning.MonitorHostName=y
    Provisioning.DecodeCustomData=n
    Provisioning.ExecuteCustomData=n
    Provisioning.PasswordCryptId=6
    Provisioning.PasswordCryptSaltLength=10
    ResourceDisk.Format=y
    ResourceDisk.Filesystem=ext4
    ResourceDisk.MountPoint=/mnt/resource
    ResourceDisk.MountOptions=None
    ResourceDisk.EnableSwap=n
    ResourceDisk.SwapSizeMB=0
    LBProbeResponder=y
    Logs.Verbose=n
    OS.RootDeviceScsiTimeout=300
    OS.OpensslPath=None
    HttpProxy.Host=None
    HttpProxy.Port=None

Olá que várias opções de configuração são descritas em detalhes abaixo. Há três tipos opções de configuração: Booliano, String ou Integer. Opções de configuração booliano Olá podem ser especificadas como "y" ou "n". Olá palavra-chave especial "None" pode ser usado para entradas de configuração de tipo alguma cadeia de caracteres conforme detalhado abaixo.

**Provisioning.Enabled:**  
Tipo: booliano  
Padrão: y

Isso permite Olá usuário tooenable ou desabilitar Olá funcionalidade no agente de saudação de provisionamento. Os valores válidos são "y" ou "n". Se o provisionamento é desabilitado, as chaves de host e o usuário SSH na imagem de saudação são preservadas e todas as configurações especificadas no hello API de provisionamento do Azure será ignorada.

> [!NOTE]
> Olá `Provisioning.Enabled` muito "n" no Ubuntu imagens de nuvem que usam init de nuvem para o provisionamento de padrões de parâmetro.
> 
> 

**Provisioning.DeleteRootPassword:**  
Tipo: booliano  
Padrão: n

Se o conjunto de senha de raiz Olá no arquivo hello/etc/sombra é apagado durante Olá o processo de provisionamento.

**Provisioning.RegenerateSshHostKeyPair:**  
Tipo: booliano  
Padrão: y

Se o conjunto, todos os SSH host pares de chave (ecdsa, dsa e rsa) é excluído durante a saudação processo de /etc/hosts ssh/de provisionamento. E um único par de chave novo é gerado.

tipo de criptografia Olá para o par de chaves novo Olá é configurável por Olá Provisioning.SshHostKeyPairType entrada. Observe que algumas distribuições recriará pares de chaves de SSH para quaisquer tipos de criptografia ausente quando o daemon do SSH Olá é reiniciado (por exemplo, após uma reinicialização).

**Provisioning.SshHostKeyPairType:**  
Tipo: String  
Padrão: rsa

Isso pode ser definido tooan tipo de algoritmo de criptografia que é compatível com o daemon do SSH Olá na máquina virtual de saudação. valores Hello normalmente existe suportada são "rsa", "dsa" e "ecdsa". Observe que "putty.exe" no Windows não oferece suporte a "ecdsa". Portanto, se você pretende toouse putty.exe em Windows tooconnect tooa implantação do Linux, use "rsa" ou "dsa".

**Provisioning.MonitorHostName:**  
Tipo: booliano  
Padrão: y

Se definido, waagent irá monitorar Olá máquina de virtual do Linux para que as alterações de nome de host (como retornado pelo comando de "nome do host" hello) e atualizar automaticamente a configuração de rede Olá na alteração de Olá Olá imagem tooreflect. No nome da ordem toopush Olá alterar toohello os servidores DNS, rede será reiniciada na máquina virtual de saudação. Isso resultará em resumo perda de conectividade com a Internet.

**Provisioning.DecodeCustomData**  
Tipo: booliano  
Padrão: n

Se definido, o waagent decodificará o CustomData da Base64.

**Provisioning.ExecuteCustomData**  
Tipo: booliano  
Padrão: n

Se definido, o waagent executará o CustomData após o provisionamento.

**Provisioning.PasswordCryptId**  
Tipo: Sequência  
Padrão: 6

Algoritmo usado pelo Crypt ao gerar o hash de senha.  
 1 - MD5  
 2a - Blowfish  
 5 - SHA-256  
 6 - SHA-512  

**Provisioning.PasswordCryptSaltLength**  
Tipo: Sequência  
Padrão: 10

Comprimento de sal aleatório usado ao gerar o hash de senha.

**ResourceDisk.Format:**  
Tipo: booliano  
Padrão: y

Se definido, disco de recurso Olá fornecido pela plataforma Olá será formatado e montado pelo waagent se o tipo de sistema de arquivos de saudação solicitado pelo usuário "ResourceDisk.Filesystem" hello é algo diferente de "ntfs". Uma única partição do tipo Linux (83) estará disponível em disco hello. Observe que essa partição não será formatada se ele pode ser montado com êxito.

**ResourceDisk.Filesystem:**  
Tipo: String  
Padrão: ext4

Isso especifica o tipo de sistema de arquivos de Olá do disco de recurso de saudação. Valores aceitos variam de acordo com a distribuição do Linux. Se X, em seguida, mkfs cadeia de caracteres de saudação. X deve estar presente na imagem do Linux hello. Imagens de 11 SLES geralmente devem utilizar 'ext3'. FreeBSD imagens devem usar 'ufs2' aqui.

**ResourceDisk.MountPoint:**  
Tipo: String  
Padrão: recurso /dev/emcpowera1 

Isso especifica o caminho de saudação em que o disco de recurso hello está montado. Observe que esse disco de recurso Olá é um *temporário* disco e pode ser esvaziada quando Olá VM for desprovisionada.

**ResourceDisk.MountOptions**  
Tipo: String  
Padrão: nenhum

Especifica opções de montagem disco toobe passado toohello mount -o comando. Trata-se de uma lista de valores separados por vírgulas, por exemplo, 'nodev, nosuid'. Consulte montagem(8) para obter detalhes.

**ResourceDisk.EnableSwap:**  
Tipo: booliano  
Padrão: n

Se definido, um arquivo de permuta (/ arquivo de permuta) é criado no disco de recurso hello e adicionado toohello espaço de permuta de sistema.

**ResourceDisk.SwapSizeMB:**  
Tipo: inteiro  
Padrão: 0

tamanho de Olá Olá do arquivo de permuta em megabytes.

**Logs.Verbose:**  
Tipo: booliano  
Padrão: n

Se definido, a verbosidade do log é aumentado. Waagent registros too/var/log/waagent.log e aproveita Olá sistema logrotate funcionalidade toorotate logs.

**OS.EnableRDMA**  
Tipo: booliano  
Padrão: n

Se definido, agente Olá irá tentar tooinstall e, em seguida, carregar um driver de kernel RDMA que corresponde à versão de saudação do firmware Olá Olá hardware subjacente.

**OS.RootDeviceScsiTimeout:**  
Tipo: inteiro  
Padrão: 300

Isso configura o tempo limite de SCSI Olá em segundos em unidades de disco e dados Olá sistema operacional. Se não for definido, o sistema Olá padrões são usados.

**OS.OpensslPath:**  
Tipo: String  
Padrão: nenhum

Isso pode ser usado toospecify um caminho alternativo para Olá openssl binário toouse para operações criptográficas.

**HttpProxy.Host, HttpProxy.Port**  
Tipo: String  
Padrão: nenhum

Se definido, Olá agente usará esse proxy server tooaccess Olá da internet. 

## <a name="ubuntu-cloud-images"></a>Imagens de nuvem do Ubuntu
Observe que utilizam o Ubuntu nuvem imagens [init nuvem](https://launchpad.net/ubuntu/+source/cloud-init) tooperform Olá de várias tarefas de configuração, caso contrário, deve ser gerenciadas pelo agente Linux do Azure.  Observação Olá diferenças a seguir:

* **Provisioning.Enabled** padrões muito "n" no Ubuntu imagens de nuvem que usam tooperform nuvem init tarefas de provisionamento.
* Olá, parâmetros de configuração a seguir não têm nenhum efeito no Ubuntu imagens de nuvem que usam init nuvem toomanage Olá recurso disco e troca de espaço:
  
  * **ResourceDisk.Format**
  * **ResourceDisk.Filesystem**
  * **ResourceDisk.MountPoint**
  * **ResourceDisk.EnableSwap**
  * **ResourceDisk.SwapSizeMB**
* Consulte Olá após o ponto de montagem do disco de recurso do recursos tooconfigure hello e trocar o espaço no Ubuntu nuvem imagens durante o provisionamento:
  
  * [Wiki do Ubuntu: configurar partições de troca](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [Injetando dados personalizados em uma Máquina Virtual do Azure](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

