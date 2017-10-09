---
title: "aaaPreparing tooback seu ambiente backup de máquinas virtuais do Azure | Microsoft Docs"
description: "Verificar se o ambiente está preparado para fazer backup de máquinas virtuais no Azure"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonn
editor: 
keywords: backups; fazendo backup;
ms.assetid: 238ab93b-8acc-4262-81b7-ce930f76a662
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/25/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 3b914c507dd6ad703ea799115ae84ac229e27787
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-environment-tooback-up-azure-virtual-machines"></a>Preparar sua tooback ambiente backup de máquinas virtuais do Azure
> [!div class="op_single_selector"]
> * [Modelo do Gerenciador de Recursos](backup-azure-arm-vms-prepare.md)
> * [Modelo clássico](backup-azure-vms-prepare.md)
>
>

Antes de poder fazer backup de uma máquina virtual (VM) do Azure, há três condições que devem existir.

* Você precisa toocreate um cofre de backup ou identificar um cofre de backup existente *em Olá mesma região que a VM*.
* Estabelecer conectividade de rede entre hello endereços de Internet pública do Azure e Olá pontos de extremidade de armazenamento do Azure.
* Instale o agente de VM Olá em Olá VM.

Se você souber essas condições já existem em seu ambiente e, depois, toohello [backup seu artigo de VMs](backup-azure-vms.md). Caso contrário, continue lendo, este artigo orientará você Olá etapas tooprepare tooback seu ambiente a uma VM do Azure.

##<a name="supported-operating-system-for-backup"></a>Versões de sistema operacional com suporte para backup
 * **Linux**: o Backup do Azure dá suporte a [uma lista de distribuições endossadas pelo Azure](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) exceto o principal sistema operacional Linux. _Outros traga-seu-proprietário-distribuições do Linux também podem funcionar, contanto que o agente de VM hello está disponível na máquina virtual de saudação e suporte para Python existe. No entanto, não endossamos essas distribuições para backup._
 * **Windows Server**: não há suporte para versões anteriores ao Windows Server 2008 R2.


## <a name="limitations-when-backing-up-and-restoring-a-vm"></a>Limitações durante o backup e a restauração de uma VM
> [!NOTE]
> O Azure tem dois modelos de implantação para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md). Olá lista a seguir fornece as limitações de saudação ao implantar o modelo clássico hello.
>
>

* Não há suporte para o backup de máquinas virtuais com mais de 16 discos de dados.
* Não há suporte para o backup de máquinas virtuais com um endereço IP reservado e nenhum ponto de extremidade definido.
* Dados de backup não incluem tooVM de unidades conectadas montado em rede.
* Não há suporte para a substituição de uma máquina virtual existente durante a restauração. Primeiro exclua a máquina virtual existente de saudação e todos os discos associados e, em seguida, restaure os dados de saudação do backup.
* Não há suporte para backup e restauração entre regiões.
* Fazendo backup de máquinas virtuais usando o serviço de Backup do Azure Olá é suportado em todas as regiões públicas do Azure (consulte Olá [lista de verificação](https://azure.microsoft.com/regions/#services) de regiões com suporte). Se a região de saudação que você está procurando não tem suporte atualmente, ele não aparecerá na lista suspensa de saudação durante a criação do cofre.
* Fazendo backup de máquinas virtuais usando o serviço de Backup do Azure Olá só tem suporte para versões do sistema operacional select:
* A restauração de uma VM DC (controladora de domínio) que é parte de uma configuração multi-DC tem suporte somente usando o PowerShell. Leia mais sobre [como restaurar um controlador de domínio com vários DCs](backup-azure-restore-vms.md#restoring-domain-controller-vms)
* Há suporte para a restauração de máquinas virtuais que têm Olá configurações de rede especiais a seguir somente por meio do PowerShell. Máquinas virtuais que você criar usando o fluxo de trabalho de restauração Olá no hello interface do usuário não terá essas configurações de rede após a conclusão da operação de restauração de saudação. mais, consulte toolearn [Restaurando VMs com configurações de rede especial](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations).
  * Máquinas virtuais sob configuração do balanceador de carga (interno e externo)
  * Máquinas virtuais com vários endereços IP reservados
  * Máquinas virtuais com vários adaptadores de rede

## <a name="create-a-backup-vault-for-a-vm"></a>Criar um cofre de backup para uma VM
Um cofre de backup é uma entidade que armazena todos os backups de saudação e pontos de recuperação que foram criados ao longo do tempo. Cofre de backup Olá também contém políticas de backup Olá que serão aplicados toohello máquinas de virtuais está sendo feitas.

> [!IMPORTANT]
> A partir de março de 2017, você não pode usar os cofres de Backup Olá toocreate portal clássico. Ainda há suporte para os cofres de Backup existentes, e é possível muito[usam os cofres de Backup do Azure PowerShell toocreate](./backup-client-automation-classic.md#create-a-backup-vault). No entanto, a Microsoft recomenda que você cria cofres de serviços de recuperação de todas as implantações porque aperfeiçoamentos futuros aplicam tooRecovery cofres de serviços, apenas.


Esta imagem mostra relações Olá entre hello várias entidades de Backup do Azure: ![entidades de Backup do Azure e relações](./media/backup-azure-vms-prepare/vault-policy-vm.png)



## <a name="network-connectivity"></a>Conectividade de rede
Em instantâneos VM do pedido toomanage Olá, extensão de backup Olá precisa de conectividade toohello Azure endereços IP públicos. Sem conectividade de Internet certa hello, HTTP solicitações hello e tempo limite de operação de backup Olá máquina virtual falhará. Se sua implantação possui restrições de acesso em vigor (por meio de um NSG, Grupo de Segurança de Rede, por exemplo), escolha uma destas opções para fornecer um caminho livre para o tráfego de backup:

* [Intervalos IP de datacenter do Azure lista branca Olá](http://www.microsoft.com/en-us/download/details.aspx?id=41653) -consulte o artigo Olá para obter instruções sobre como toowhitelist Olá endereços IP.
* Implante um servidor de proxy HTTP para rotear o tráfego.

Ao decidir qual opção toouse, Olá compensações estão entre capacidade de gerenciamento, um controle granular e custo.

| Opção | Vantagens | Desvantagens |
| --- | --- | --- |
| Intervalos de IPs na lista de autorizados |Sem custo adicional.<br><br>Para abrir o acesso em um NSG, use Olá <i>AzureNetworkSecurityRule conjunto</i> cmdlet. |Toomanage complexo como alteração de intervalos IP hello afetado ao longo do tempo.<br><br>Fornece todo de toohello de acesso do Azure e não apenas o armazenamento. |
| Proxy HTTP |Controle granular no proxy Olá armazenamento Olá URLs permitidas. um controle granular toosetup proxy hello, https://\*.blob.core.windows.net/\* padrão de URL precisa toobe na lista de permissões. toowhitelist Olá apenas a conta de armazenamento usada pelo Olá VM, https://\<storageAccount\>.blob.core.windows.net/\* padrão de URL precisa toobe na lista de permissões. <br>TooVMs de acesso de ponto único de Internet.<br>Não sujeito a alterações de endereço IP tooAzure. |Custos adicionais para executar uma máquina virtual com o software de proxy de saudação. |

### <a name="whitelist-hello-azure-datacenter-ip-ranges"></a>Intervalos IP de datacenter do Azure lista branca Olá
intervalos de IP do toowhitelist Olá datacenter do Azure, consulte Olá [site do Azure](http://www.microsoft.com/en-us/download/details.aspx?id=41653) para obter detalhes sobre os intervalos de IP hello e instruções.

### <a name="using-an-http-proxy-for-vm-backups"></a>Usando um proxy HTTP para backups de uma VM
Ao fazer backup de uma VM, extensão de backup Olá em Olá VM envia Olá instantâneo gerenciamento comandos tooAzure armazenamento usando uma API de HTTPS. Rotear o tráfego de extensão de backup Olá por meio do proxy HTTP de saudação já que é o único componente de saudação configurado para acesso toohello Internet pública.

> [!NOTE]
> Não há nenhuma recomendação de software de proxy de saudação que deve ser usado. Certifique-se de que você escolha um proxy com persistência de saída e que é compatível com etapas de configuração de saudação abaixo. Certifique-se de softwares de terceiros não modifique as configurações de proxy Olá
>
>

imagem de exemplo Hello abaixo mostra etapas de configuração de três Olá toouse necessário um HTTP proxy:

* Rotas de VM do aplicativo vinculado a todo o tráfego HTTP Olá Internet pública por meio do Proxy de VM.
* Proxy VM permite que o tráfego de entrada de VMs na rede virtual hello.
* Olá grupo de segurança da rede (NSG) denominado NSF-bloqueio precisa de um segurança regra permitindo Internet tráfego de saída do Proxy de VM.

![Diagrama de implantação de proxy HTTP com NSG](./media/backup-azure-vms-prepare/nsg-with-http-proxy.png)

toouse um HTTP proxy toocommunicating toohello Internet pública, siga estas etapas:

#### <a name="step-1-configure-outgoing-network-connections"></a>Etapa 1. Configurar conexões de rede de saída
###### <a name="for-windows-machines"></a>Para computadores Windows
Isso definirá a configuração do servidor de proxy para a Conta do Sistema Local.

1. Baixe o [PsExec](https://technet.microsoft.com/sysinternals/bb897553)
2. Execute o seguinte comando no prompt com privilégios elevados,

     ```
     psexec -i -s "c:\Program Files\Internet Explorer\iexplore.exe"
     ```
     Isso abrirá a janela do Internet Explorer.
3. Vá tooTools -> Opções da Internet -> conexões -> configurações da LAN.
4. Verifique as configurações de proxy para a conta do Sistema. Defina o IP e a porta do proxy.
5. Feche o Internet Explorer.

Isso configurará um proxy de todo o computador e será usado para qualquer tráfego de saída HTTP/HTTPS.

Se você configurou um servidor proxy em uma conta de usuário atual (não uma conta de sistema Local), use Olá tooapply de script a segui-los tooSYSTEMACCOUNT:

```
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name DefaultConnectionSettings -Value $obj.DefaultConnectionSettings
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name SavedLegacySettings -Value $obj.SavedLegacySettings
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name ProxyEnable -Value $obj.ProxyEnable
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name Proxyserver -Value $obj.Proxyserver
```

> [!NOTE]
> Se você vir "(407) Autenticação de Proxy Necessária" no log do servidor proxy, verifique se a configuração da sua autenticação está correta.
>
>

###### <a name="for-linux-machines"></a>Para computadores Linux
Adicionar Olá toohello linha a seguir ```/etc/environment``` arquivo:

```
http_proxy=http://<proxy IP>:<proxy port>
```

Adicionar Olá toohello linhas a seguir ```/etc/waagent.conf``` arquivo:

```
HttpProxy.Host=<proxy IP>
HttpProxy.Port=<proxy port>
```

#### <a name="step-2-allow-incoming-connections-on-hello-proxy-server"></a>Etapa 2. Permita conexões de entrada no servidor de proxy hello:
1. No servidor de proxy hello, abra o Firewall do Windows. firewall do Hello mais fácil maneira tooaccess Olá é toosearch Firewall do Windows com segurança avançada.

    ![Abrir Olá Firewall](./media/backup-azure-vms-prepare/firewall-01.png)
2. Na caixa de diálogo de Firewall do Windows hello, clique com botão direito **regras de entrada** e clique em **nova regra...** .

    ![Criar uma nova regra](./media/backup-azure-vms-prepare/firewall-02.png)
3. Em Olá **novo Assistente de regra de entrada**, escolha Olá **personalizado** opção Olá **tipo de regra** e clique em **próximo**.
4. Em saudação do hello página tooselect **programa**, escolha **todos os programas** e clique em **próximo**.
5. Em Olá **protocolo e portas** página, digite Olá informações a seguir e clique em **próximo**:

    ![Criar uma nova regra](./media/backup-azure-vms-prepare/firewall-03.png)

   * para *Tipo de protocolo*, escolha *TCP*
   * para *porta Local* escolha *portas específicas*, no campo de saudação abaixo especifique Olá ```<Proxy Port>``` que foi configurado.
   * para *Porta remota*, escolha *Todas as Portas*

     Restante Olá Assistente hello, clique em todos os finais de toohello de maneira hello e dê um nome dessa regra.

#### <a name="step-3-add-an-exception-rule-toohello-nsg"></a>Etapa 3. Adicione uma regra de exceção toohello NSG:
Em um prompt de comando do PowerShell do Azure, digite Olá comando a seguir:

saudação de comando a seguir adiciona uma exceção toohello NSG. Essa exceção permite o tráfego TCP de qualquer porta 10.0.0.5 tooany endereço na Internet na porta 80 (HTTP) ou 443 (HTTPS). Se você precisar de uma porta específica no hello Internet pública, ser tooadd-se de que a porta toohello ```-DestinationPortRange``` também.

```
Get-AzureNetworkSecurityGroup -Name "NSG-lockdown" |
Set-AzureNetworkSecurityRule -Name "allow-proxy " -Action Allow -Protocol TCP -Type Outbound -Priority 200 -SourceAddressPrefix "10.0.0.5/32" -SourcePortRange "*" -DestinationAddressPrefix Internet -DestinationPortRange "80-443"
```

*Certifique-se de que você substitua nomes Olá no exemplo hello com a implantação do hello detalhes tooyour apropriado.*

## <a name="vm-agent"></a>Agente de VM
Antes de você fazer backup de saudação máquina virtual do Azure, você deve garantir que o agente de VM do Azure hello está instalado corretamente na máquina virtual de saudação. Como agente de VM Olá é um componente opcional em hora Olá Olá a máquina virtual é criado, verifique se essa caixa de seleção de saudação para agente de VM hello está selecionado antes de máquina virtual de saudação é provisionada.

### <a name="manual-installation-and-update"></a>Atualização e instalação manual
Agente de VM Olá já está presente em máquinas virtuais que são criados a partir Olá Galeria do Azure. No entanto, máquinas virtuais que são migradas de datacenters locais não teria agente de VM Olá instalado. Para essas VMs, agente de VM Olá precisa toobe instalado explicitamente. Leia mais sobre [Instalando agente VM de saudação em uma VM existente](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx).

| **Operação** | **Windows** | **Linux** |
| --- | --- | --- |
| Instalando o agente de VM Olá |<li>Baixe e instale Olá [MSI agente](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Você precisará de instalação de saudação do toocomplete de privilégios de administrador. <li>[Atualizar a propriedade VM Olá](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate que Olá agente está instalado. |<li> Instalar hello mais recente [agente Linux](https://github.com/Azure/WALinuxAgent) do GitHub. Você precisará de instalação de saudação do toocomplete de privilégios de administrador. <li> [Atualizar a propriedade VM Olá](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate que Olá agente está instalado. |
| Atualizando o agente de VM Olá |Atualizar agente VM Olá é tão simple quanto a reinstalação Olá [binários de agente VM](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). <br><br>Certifique-se de que nenhuma operação de backup está em execução enquanto o agente de VM hello está sendo atualizado. |Siga as instruções de saudação [atualização Olá agente de VM do Linux ](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). <br><br>Certifique-se de que nenhuma operação de backup está em execução enquanto o agente de VM hello está sendo atualizado. |
| Validar a instalação do agente VM Olá |<li>Navegue toohello *C:\WindowsAzure\Packages* pasta Olá VM do Azure. <li>Você deve encontrar o arquivo de WaAppAgent.exe de saudação presente.<li> Clique duas vezes o arquivo hello, ir muito**propriedades**e, em seguida, selecione Olá **detalhes** campo de versão do produto de saudação de guia deve ser 2.6.1198.718 ou superior. |N/D |

Saiba mais sobre Olá [agente de VM](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) e [como tooinstall-](https://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/).

### <a name="backup-extension"></a>Extensão de backup
tooback a máquina virtual de hello, Olá serviço Backup do Azure instala um agente VM de toohello de extensão. Olá serviço Backup do Azure diretamente atualizações e patches extensão de backup Olá sem intervenção do usuário adicional.

extensão de backup Olá será instalado se Olá VM está em execução. Uma VM em execução também fornece a possibilidade de maior Olá da obtenção de um ponto de recuperação consistentes com aplicativos. No entanto, hello Azure Backup service continuará tooback backup Olá VM – mesmo se ele está desativado e extensão de saudação não pôde ser instalado (também conhecido como off-line VM). Nesse caso, o ponto de recuperação Olá será *falha consistente* conforme descrito acima.

## <a name="questions"></a>Perguntas?
Se você tiver dúvidas ou se houver qualquer recurso que você gostaria que toosee incluído, [nos enviar comentários](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Próximas etapas
Agora que você preparou seu ambiente para fazer backup de sua VM, a próxima etapa lógica é toocreate um backup. Olá planejamento artigo fornece informações mais detalhadas sobre como fazer backup de máquinas virtuais.

* [Backup de máquinas virtuais](backup-azure-vms.md)
* [Planeje sua infraestrutura de backup da VM](backup-azure-vms-introduction.md)
* [Gerenciar backups de máquinas virtuais](backup-azure-manage-vms.md)
