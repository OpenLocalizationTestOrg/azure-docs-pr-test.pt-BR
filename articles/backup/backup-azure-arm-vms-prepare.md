---
title: "O Backup do Azure: Preparar tooback backup de máquinas virtuais | Microsoft Docs"
description: "Assegure-se de que o ambiente esteja preparado para fazer backup de máquinas virtuais no Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: backups; fazendo backup;
ms.assetid: e87e8db2-b4d9-40e1-a481-1aa560c03395
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 5c3a41b5d3bd56e62ca5f207442867913aa99816
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-environment-tooback-up-resource-manager-deployed-virtual-machines"></a>Preparar sua tooback ambiente backup de máquinas de virtuais implantadas pelo Gerenciador de recursos
> [!div class="op_single_selector"]
> * [Modelo do Gerenciador de Recursos](backup-azure-arm-vms-prepare.md)
> * [Modelo clássico](backup-azure-vms-prepare.md)
>
>

Este artigo fornece etapas Olá para preparar seu tooback ambiente uma máquina virtual implantada para o Gerenciador de recursos (VM). Olá, etapas mostradas nos procedimentos de saudação usam Olá portal do Azure.  

saudação de serviço de Backup do Azure tem dois tipos de cofres (backup cofres e cofres de serviços de recuperação) para proteger suas VMs. Um cofre de backup protege as VMs implantadas usando o modelo de implantação clássico hello. Um cofre dos serviços de recuperação protege **tanto as VMs implantadas com o modelo de implantação Clássico quanto aquelas implantadas com o Resource Manager**. Você deve usar um cofre de serviços de recuperação tooprotect uma VM implantada para o Gerenciador de recursos.

> [!NOTE]
> O Azure tem dois modelos de implantação para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md). Consulte [preparar seu tooback ambiente backup de máquinas virtuais do Azure](backup-azure-vms-prepare.md) para obter detalhes sobre como trabalhar com implantação clássico VMs de modelo.
>
>

Antes de proteger ou fazer backup de uma VM (máquina virtual) implantada com o Gerenciador de Recursos, verifique se esses pré-requisitos foram cumpridos:

* Crie um cofre de serviços de recuperação (ou identificar um cofre de serviços de recuperação existente) *em Olá mesmo local que sua VM*.
* Selecionar um cenário, definir a política de backup hello e definir tooprotect de itens.
* Verifique a instalação de saudação do agente de VM na máquina virtual.
* Verificar a conectividade de rede
* Para VMs do Linux, caso você deseje toocustomize seu ambiente de backup para backups consistentes com aplicativo siga Olá [tooconfigure etapas previamente de instantâneo e os scripts de instantâneo após](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent)

Se você souber essas condições já existem em seu ambiente e, depois, toohello [backup seu artigo de VMs](backup-azure-vms.md). Se você precisa tooset backup ou verificar, qualquer um dos pré-requisitos, este artigo o orienta Olá etapas tooprepare esse pré-requisito.

##<a name="supported-operating-system-for-backup"></a>Versões de sistema operacional com suporte para backup
 * **Linux**: o Backup do Azure dá suporte a [uma lista de distribuições endossadas pelo Azure](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) exceto o principal sistema operacional Linux. _Outros traga-seu-proprietário-distribuições do Linux também podem funcionar, contanto que o agente de VM hello está disponível na máquina virtual de saudação e suporte para Python existe. No entanto, não endossamos essas distribuições para backup._
 * **Windows Server**: não há suporte para versões anteriores ao Windows Server 2008 R2.

## <a name="limitations-when-backing-up-and-restoring-a-vm"></a>Limitações durante o backup e a restauração de uma VM
Antes de preparar seu ambiente, entenda as limitações de saudação.

* Não há suporte para o backup de máquinas virtuais com mais de 16 discos de dados.
* Não há suporte para o backup de máquinas virtuais com tamanhos de discos de dados maiores que 1.023 GB.
* Não há suporte para o backup de máquinas virtuais com um endereço IP reservado e nenhum ponto de extremidade definido.
* Não há suporte para backup de VMs criptografadas usando apenas BEK. Não há suporte para backup de VMs Linux criptografadas usando criptografia LUKS.
* O backup de VMs na configuração do Servidor de Arquivos de Escalabilidade Horizontal não é recomendado.
* Dados de backup não incluem tooVM de unidades conectadas montado em rede.
* Não há suporte para a substituição de uma máquina virtual existente durante a restauração. Se você tentar toorestore Olá VM quando Olá VM existe, a operação de restauração de saudação falhará.
* Não há suporte para backup e restauração entre regiões.
* Você pode fazer backup de máquinas virtuais em todas as regiões públicas do Azure (consulte Olá [lista de verificação](https://azure.microsoft.com/regions/#services) de regiões com suporte). Se a região de saudação que você está procurando não tem suporte atualmente, ele não aparecerá na lista suspensa de saudação durante a criação do cofre.
* A restauração de uma VM DC (controladora de domínio) que é parte de uma configuração multi-DC tem suporte somente usando o PowerShell. Leia mais sobre [como restaurar um controlador de domínio com vários DCs](backup-azure-restore-vms.md#restoring-domain-controller-vms)
* Há suporte para a restauração de máquinas virtuais que têm Olá configurações de rede especiais a seguir somente por meio do PowerShell. Máquinas virtuais criadas usando o fluxo de trabalho de restauração Olá Olá interface do usuário não terá essas configurações de rede após a conclusão da operação de restauração de saudação. mais, consulte toolearn [Restaurando VMs com configurações de rede especial](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations).
  * Máquinas virtuais sob configuração do balanceador de carga (interno e externo)
  * Máquinas virtuais com vários endereços IP reservados
  * Máquinas virtuais com vários adaptadores de rede

## <a name="create-a-recovery-services-vault-for-a-vm"></a>Criar um cofre de Serviços de Recuperação para uma VM
Um cofre de serviços de recuperação é uma entidade que armazena os backups hello e pontos de recuperação que foram criados ao longo do tempo. Cofre de serviços de recuperação de saudação também contém políticas de backup Olá associadas com as máquinas virtuais de saudação protegida.

Cofre de serviços de toocreate uma recuperação:

1. Entrar toohello [portal do Azure](https://portal.azure.com/).
2. No menu de Hub hello, clique em **procurar** e, na lista de saudação de recursos, digite **dos serviços de recuperação**. Como começar a digitar, lista Olá filtra com base em sua entrada. Clique em **Cofre dos Serviços de Recuperação**.

    ![Clique o botão de procura hello e digite dos serviços de recuperação. Quando você vir os serviços de recuperação de saudação cofre opção, clique em tooopen Olá dos serviços de recuperação cofre folha.](./media/backup-azure-arm-vms-prepare/browse-to-rs-vaults-updated.png) <br/>

    saudação de lista de cofres de serviços de recuperação é exibida.
3. Em Olá **os cofres de serviços de recuperação** menu, clique em **adicionar**.

    ![Criar Cofre de Serviços de Recuperação - etapa 2](./media/backup-azure-arm-vms-prepare/rs-vault-menu.png)

    Serviços de recuperação de saudação cofre abre a folha, solicitando que você tooprovide uma **nome**, **assinatura**, **grupo de recursos**, e **local**.

    ![Criar Cofre de Serviços de Recuperação - etapa 5](./media/backup-azure-arm-vms-prepare/rs-vault-attributes.png)
4. Para **nome**, insira um cofre de saudação tooidentify nome amigável. nome da saudação precisa toobe exclusivo Olá assinatura do Azure. Digite um nome que contenha de 2 a 50 caracteres. Ele deve começar com uma letra e pode conter apenas letras, números e hifens.
5. Clique em **assinatura** toosee Olá lista de assinaturas. Se você não tiver certeza de qual toouse de assinatura, use saudação padrão (ou sugerido) assinatura. Haverá várias opções somente se sua conta organizacional estiver associada a várias assinaturas do Azure.
6. Clique em **grupo de recursos** toosee Olá a lista de grupos de recursos disponíveis, ou clique em **novo** toocreate um novo grupo de recursos. Para obter informações completas sobre Grupos de recursos, confira [Visão geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)
7. Clique em **local** tooselect Olá região para o cofre hello. cofre Olá **deve** em Olá Olá de máquinas virtuais que você deseja tooprotect mesma região.

   > [!IMPORTANT]
   > Se você tiver certeza da saudação localização na qual sua VM, feche fora da caixa de diálogo de criação de cofre hello e vá toohello a lista de máquinas virtuais no portal de saudação. Se você tiver máquinas virtuais em várias regiões, você precisará toocreate um cofre de serviços de recuperação de cada região. Crie cofre Olá no primeiro local de saudação antes de ir toohello próximo local. Há contas de armazenamento sem necessidade toospecify toostore Olá os dados de backup – Olá Cofre de serviços de recuperação e hello Azure Backup service lidar com isso automaticamente.
   >
   >

8. Clique em **Criar**. Pode levar algum tempo para Olá toobe criado de Cofre de serviços de recuperação. Monitorar as notificações de status de saudação na área superior direito de saudação no portal de saudação. Depois de criar seu cofre, ele aparece na lista de saudação de cofres de serviços de recuperação. Se você não encontrar seu cofre, clique em **Atualizar** para

    ![Lista de cofres de backup](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

    Agora que você criou seu cofre, saiba como tooset Olá replicação de armazenamento.

## <a name="set-storage-replication"></a>Definir replicação de armazenamento
opção de replicação de armazenamento Olá permite toochoose entre o armazenamento com redundância geográfica e o armazenamento redundante localmente. Por padrão, seu cofre tem armazenamento com redundância geográfica. Deixe Olá opção set toogeo redundantes armazenamento se esta for sua principal de backup. Escolha o armazenamento com redundância local se quiser uma opção mais barata que não seja tão durável.

configuração de replicação de armazenamento de saudação tooedit:

1. Em Olá **os cofres de serviços de recuperação** folha, selecione o cofre.
    Quando você clica em seu cofre, Olá folha de configurações (*que tem o nome de saudação do cofre Olá na parte superior da saudação*) e os detalhes de cofre Olá abre folha.

    ![Escolha seu cofre Olá lista de cofres de backup](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)

2. Em Olá **configurações** folha, use Olá slider vertical tooscroll para baixo toohello **gerenciar** seção. Clique em **Backup infraestrutura** tooopen sua folha. Em Olá **geral** seção clique **configuração de Backup** tooopen sua folha. Em Olá **configuração de Backup** folha, escolha a opção de replicação de armazenamento Olá para seu cofre. Por padrão, seu cofre tem armazenamento com redundância geográfica. Se você alterar o tipo de replicação de armazenamento hello, clique em **salvar**.

    ![Lista de cofres de backup](./media/backup-azure-arm-vms-prepare/full-blade.png)

     Se você estiver usando o Azure como um ponto de extremidade de armazenamento de backup principal, continue usando o armazenamento com redundância geográfica. Se você estiver usando o Azure como um ponto de extremidade de armazenamento de backup não primário, considere a escolha do armazenamento com redundância local. Leia mais sobre [georredundante](../storage/common/storage-redundancy.md#geo-redundant-storage) e [localmente redundante](../storage/common/storage-redundancy.md#locally-redundant-storage) opções de armazenamento no hello [visão geral de replicação de armazenamento do Azure](../storage/common/storage-redundancy.md).
    Depois de escolher a opção de armazenamento de saudação para seu cofre, você está pronto tooassociate Olá VM com o cofre hello. associação de saudação toobegin, você deve descobrir e registrar Olá máquinas virtuais do Azure.

## <a name="select-a-backup-goal-set-policy-and-define-items-tooprotect"></a>Selecione uma meta de backup, defina a política e definir tooprotect itens
Antes de registrar uma VM com um cofre, execute Olá tooensure de processo de descoberta que quaisquer novas máquinas virtuais que foram adicionadas toohello assinatura são identificadas. Olá processar consultas do Azure para obter lista de saudação de máquinas virtuais na assinatura hello, juntamente com informações adicionais, como nome de serviço de nuvem hello e região Olá. Olá portal do Azure, o cenário refere-se toowhat serão tooput no cofre de serviços de recuperação de saudação. A diretiva é agenda Olá para frequência e quando os pontos de recuperação são feitos. Política também inclui o período de retenção Olá Olá pontos de recuperação.

1. Se você já tiver um cofre de serviços de recuperação aberta, vá toostep 2. Se você não tiver um cofre de serviços de recuperação aberto, abra Olá [portal do Azure](https://portal.azure.com/) e no menu de Hub hello, clique em **mais serviços**.

   * Na lista de saudação de recursos, digite **dos serviços de recuperação**.
   * Como começar a digitar, lista Olá filtra com base em sua entrada. Quando vir a opção **Cofres de Serviços de Recuperação**, clique nela.

     ![Criar Cofre de Serviços de Recuperação - etapa 1](./media/backup-azure-arm-vms-prepare/browse-to-rs-vaults-updated.png) <br/>

     saudação de lista de cofres de serviços de recuperação é exibida. Se não houver nenhum cofre em sua assinatura, essa lista estará vazia.

    ![Lista de cofres de modo de exibição de saudação dos serviços de recuperação](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

   * Na lista de saudação de cofres de serviços de recuperação, selecione um cofre tooopen seu painel.

     folha de configurações de saudação e hello cofre painel Cofre Olá escolhida, é aberta.

     ![Abrir a folha do cofre](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)
2. No menu do painel Cofre Olá clique **Backup** tooopen folha de Backup de saudação.

    ![Abrir a folha Backup](./media/backup-azure-arm-vms-prepare/backup-button.png)

    folhas de Backup e Backup meta Olá abrir.

    ![Abrir a folha Cenário](./media/backup-azure-arm-vms-prepare/select-backup-goal-1.png)

3. Na folha de meta de Backup hello, defina **onde sua carga de trabalho está executando** tooAzure e **o que fazer você deseja toobackup** tooVirtual máquina e, em seguida, clique em **Okey**.

    Isso registra Olá extensão de VM com o cofre hello. Olá meta Backup folha fecha e hello **política de Backup** folha é aberta.

    ![Abrir a folha Cenário](./media/backup-azure-arm-vms-prepare/select-backup-goal-2.png)
4. Na folha de política de Backup hello, selecione política de backup Olá deseja tooapply toohello cofre.

    ![Selecionar a política de backup](./media/backup-azure-arm-vms-prepare/setting-rs-backup-policy-new.png)

    detalhes de saudação da política de padrão de saudação são listados sob o menu suspenso de saudação. Se você desejar toocreate uma nova política, selecione **criar novo** do menu suspenso de saudação. Para obter instruções sobre como definir uma política de backup, confira [Definindo uma política de backup](backup-azure-vms-first-look-arm.md#defining-a-backup-policy).
    Clique em **Okey** tooassociate política de backup Olá cofre hello.

    Olá fecha de folha de política de Backup e hello **selecionar máquinas virtuais** folha é aberta.
5. Em Olá **selecionar máquinas virtuais** folha, escolha Olá tooassociate de máquinas virtuais com hello especificado política e clique em **Okey**.

    ![Selecionar carga de trabalho](./media/backup-azure-arm-vms-prepare/select-vms-to-backup.png)

    máquina virtual de saudação selecionada é validada. Se você não vir as máquinas virtuais de saudação esperado toosee, verifique se eles existem no hello mesmo local do Azure Olá Cofre de serviços de recuperação e não ainda estão protegido no cofre de outro. local de saudação de saudação que Cofre de serviços de recuperação é mostrado no painel do cofre hello.

6. Agora que você definiu todas as configurações para o cofre hello, no hello folha Backup clique **habilitar Backup**. Isso implanta Olá política toohello do cofre e Olá VMs. Isso não cria o ponto de recuperação inicial de saudação para a máquina virtual de saudação.

    ![Habilitar Backup](./media/backup-azure-arm-vms-prepare/vm-validated-click-enable.png)

Depois de habilitar o backup de saudação com êxito, sua política de backup será executado na agenda. Se você quiser toogenerate tooback um trabalho de backup sob demanda backup de máquinas virtuais de saudação agora, consulte [trabalho de Backup Olá Triggering](./backup-azure-arm-vms.md#triggering-the-backup-job).

Se você tiver problemas ao registrar a máquina virtual de hello, consulte Olá seguintes informações sobre como instalar Olá agente de VM e conectividade de rede. Você provavelmente não precisará Olá informações a seguir se você estiver protegendo máquinas virtuais criadas no Azure. No entanto se você migrou máquinas virtuais no Azure, em seguida, certifique-se que você tiver instalado o agente de VM hello e se sua máquina virtual pode se comunicar com a rede virtual Olá corretamente.

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a>Instalar Olá agente de VM na máquina virtual de saudação
Hello Azure VM Agent deve ser instalado em Olá máquina virtual do Azure para Olá toowork de extensão de Backup. Se sua VM foi criada de saudação Galeria do Azure, Olá VM Agent já está presente na máquina virtual de saudação. Essas informações são fornecidas para Olá situações nas quais é *não* usando uma VM criada a partir Olá Galeria do Azure - por exemplo você migrou uma máquina virtual de um datacenter local. Nesse caso, Olá agente de VM precisa toobe instalado na máquina virtual do pedido tooprotect hello. Saiba mais sobre Olá [agente de VM](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux).

Se você tiver problemas ao fazer backup Olá VM do Azure, verifique se hello Azure VM Agent está instalado corretamente na máquina virtual de saudação (consulte a tabela de saudação abaixo). Olá, a tabela a seguir fornece informações adicionais sobre Olá VM Agent para Windows e VMs do Linux.

| **Operação** | **Windows** | **Linux** |
| --- | --- | --- |
| Olá instalar agente de VM |Baixe e instale Olá [MSI agente](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Você precisará de instalação de saudação do toocomplete de privilégios de administrador. |<li> Instalar hello mais recente [agente Linux](../virtual-machines/linux/agent-user-guide.md). Você precisará de instalação de saudação do toocomplete de privilégios de administrador. É recomendável instalar o agente do seu repositório de distribuição. **Não é recomendável** instalar o agente de VM Linux diretamente do GitHub.  |
| Atualizando Olá agente de VM |Olá atualizar agente de VM é tão simple quanto a reinstalação Olá [binários de agente de VM](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). <br>Certifique-se de que nenhuma operação de backup está em execução enquanto o agente de VM hello está sendo atualizado. |Siga as instruções de saudação [atualização Olá agente de VM do Linux](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). É recomendável atualizar o agente do seu repositório de distribuição. **Não é recomendável** atualizar o agente de VM Linux diretamente do GitHub.<br>Certifique-se de que nenhuma operação de backup está em execução durante a saudação que VM Agent está sendo atualizado. |
| Validar a instalação do agente de VM Olá |<li>Navegue toohello *C:\WindowsAzure\Packages* pasta Olá VM do Azure. <li>Você deve encontrar o arquivo de WaAppAgent.exe de saudação presente.<li> Clique duas vezes o arquivo hello, ir muito**propriedades**e, em seguida, selecione Olá **detalhes** campo de versão do produto de saudação de guia deve ser 2.6.1198.718 ou superior. |N/D |

### <a name="backup-extension"></a>Extensão de backup
Uma vez Olá que VM Agent está instalado na máquina virtual de hello, Olá serviço Backup do Azure instala Olá extensão backup toohello agente de VM. Olá serviço Backup do Azure diretamente atualizações e patches extensão backup hello.

extensão de backup Olá é instalado pelo serviço de Backup Olá Olá VM está em execução ou não. Uma VM em execução fornece a possibilidade maior Olá da obtenção de um ponto de recuperação consistentes com aplicativos. No entanto, Olá serviço Backup do Azure continua tooback backup Olá VM mesmo se ele está desativado e não foi possível instalar a extensão de saudação. Isso é conhecido como VM Offline. Nesse caso, o ponto de recuperação Olá será *falha consistente*.

## <a name="network-connectivity"></a>Conectividade de rede
Em instantâneos VM do pedido toomanage Olá, extensão de backup Olá precisa de conectividade toohello Azure endereços IP públicos. Sem conectividade de Internet certa hello, HTTP solicitações hello e tempo limite de operação de backup Olá máquina virtual falhará. Se sua implantação possui restrições de acesso em vigor (por meio de um NSG, Grupo de Segurança de Rede, por exemplo), escolha uma destas opções para fornecer um caminho livre para o tráfego de backup:

* [Intervalos IP de datacenter do Azure lista branca Olá](http://www.microsoft.com/en-us/download/details.aspx?id=41653) -consulte o artigo Olá para obter instruções sobre como toowhitelist Olá endereços IP.
* Implante um servidor de proxy HTTP para rotear o tráfego.

Ao decidir qual opção toouse, Olá compensações estão entre capacidade de gerenciamento, um controle granular e custo.

| Opção | Vantagens | Desvantagens |
| --- | --- | --- |
| Intervalos de IPs na lista de autorizados |Sem custo adicional.<br><br>Para abrir o acesso em um NSG, use Olá <i>AzureNetworkSecurityRule conjunto</i> cmdlet. |Toomanage complexo como alteração de intervalos IP hello afetado ao longo do tempo.<br><br>Fornece todo de toohello de acesso do Azure e não apenas o armazenamento. |
| Proxy HTTP |Controle granular no proxy Olá armazenamento Olá URLs permitidas.<br>TooVMs de acesso de ponto único de Internet.<br>Não sujeito a alterações de endereço IP tooAzure. |Custos adicionais para executar uma máquina virtual com o software de proxy de saudação. |

### <a name="whitelist-hello-azure-datacenter-ip-ranges"></a>Intervalos IP de datacenter do Azure lista branca Olá
intervalos de IP do toowhitelist Olá datacenter do Azure, consulte Olá [site do Azure](http://www.microsoft.com/en-us/download/details.aspx?id=41653) para obter detalhes sobre os intervalos de IP hello e instruções.

### <a name="using-an-http-proxy-for-vm-backups"></a>Usando um proxy HTTP para backups de uma VM
Ao fazer backup de uma VM, extensão de backup Olá em Olá VM envia Olá instantâneo gerenciamento comandos tooAzure armazenamento usando uma API de HTTPS. Rotear o tráfego de extensão de backup Olá por meio do proxy HTTP de saudação já que é o único componente de saudação configurado para acesso toohello Internet pública.

> [!NOTE]
> Não há nenhuma recomendação de software de proxy de saudação que deve ser usado. Certifique-se de que você escolha um proxy que é compatível com etapas de configuração de saudação abaixo.
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
> Se você receber "(407) Autenticação de Proxy Necessária" no log do servidor proxy, verifique se a configuração da sua autenticação está correta.
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


*Essas etapas usam valores e nomes específicos para esse exemplo. Use Olá nomes e valores para sua implantação ao inserir, ou recortar e colar os detalhes em seu código.*

Agora que você sabe que há conectividade de rede, você está pronto tooback a sua máquina virtual. Confira [Back up Resource Manager-deployed VMs](backup-azure-arm-vms.md)(Fazer backup das máquinas virtuais implantadas com o Gerenciador de Recursos).

## <a name="questions"></a>Perguntas?
Se você tiver dúvidas ou se houver qualquer recurso que você gostaria que toosee incluído, [nos enviar comentários](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Próximas etapas
Agora que você preparou seu ambiente para fazer backup de sua VM, a próxima etapa lógica é toocreate um backup. Olá planejamento artigo fornece informações mais detalhadas sobre como fazer backup de máquinas virtuais.

* [Backup de máquinas virtuais](backup-azure-vms.md)
* [Planeje sua infraestrutura de backup da VM](backup-azure-vms-introduction.md)
* [Gerenciar backups de máquinas virtuais](backup-azure-manage-vms.md)
