---
title: "aaaProvision uma máquina Virtual do SQL Server | Microsoft Docs"
description: "Criar e conectar-se a máquina de virtual tooa do SQL Server no Azure usando o Portal de saudação. Este tutorial usa o modo de Gerenciador de recursos de saudação."
services: virtual-machines-windows
documentationcenter: na
author: rothja
editor: 
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 1aff691f-a40a-4de2-b6a0-def1384e086e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: jroth
experimental_id: a641df96-f27d-40
ms.openlocfilehash: aaad422d6ed47f5ca00b1ef484ac270a58e24f99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-in-hello-azure-portal"></a>Provisionar uma máquina de virtual do SQL Server no hello Portal do Azure
> [!div class="op_single_selector"]
> * [Portal](virtual-machines-windows-portal-sql-server-provision.md)
> * [PowerShell](virtual-machines-windows-ps-sql-create.md)
> 
> 

Este tutorial de ponta a ponta mostra como toouse hello Azure Portal tooprovision uma máquina virtual executando o SQL Server.

Galeria de máquina virtual do Azure (VM) Olá inclui várias imagens que contêm o Microsoft SQL Server. Com alguns cliques, você pode selecionar uma saudação que SQL VM imagens da Galeria de saudação e provisioná-la no seu ambiente do Azure.

Neste tutorial, você irá:

* [Selecione uma imagem de VM do SQL na Galeria de saudação](#select-a-sql-vm-image-from-the-gallery)
* [Configurar e criar hello VM](#configure-the-vm)
* [Abra Olá VM com área de trabalho remota](#open-the-vm-with-remote-desktop)
* [Conecte-se tooSQL servidor remotamente](#connect-to-sql-server-remotely)

## <a name="select-a-sql-vm-image-from-hello-gallery"></a>Selecione uma imagem de VM do SQL na Galeria de saudação
1. Faça logon no toohello [portal do Azure](https://portal.azure.com) usando sua conta.

   > [!NOTE]
   > Se você não tiver uma conta do Azure, visite [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).

2. No portal do Azure de Olá, clique em **novo**. portal de saudação abre Olá **novo** folha. há recursos de VM do SQL Server de Olá Olá **de computação** grupo da saudação Marketplace.
3. Em Olá **novo** folha, clique em **de computação** e, em seguida, clique em **ver todos os**.
4. Em Olá **filtro** texto caixa tipo de SQL Server e pressione a tecla ENTER de saudação.

   ![Folha Máquinas Virtuais do Azure](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-blade2.png)

5. Examine as imagens Olá disponíveis do SQL Server. Cada imagem identifica uma versão do SQL Server e um sistema operacional. 
6. Selecione a imagem de saudação para desenvolvedor do SQL Server 2016 SP1 no Windows Server 2016.

   > [!TIP]
   > edição de desenvolvedor Olá é usada neste tutorial, porque é uma edição completa do SQL Server que está livre para fins de teste de desenvolvimento. Você paga apenas para o custo de saudação da execução Olá VM.

   > [!NOTE]
   > Imagens de VM do SQL incluem os custos de licenciamento Olá para o SQL Server em Olá por minuto preços de saudação VM criar (exceto Olá Developer e Express editions). O SQL Server Developer é gratuito para desenvolvimento/teste (não para produção) e o SQL Express é gratuito para cargas de trabalho leves (menores que 1 GB de memória e menores que 10 GB de armazenamento).
   > Há outra opção toobring-seu-proprietário-licença (BYOL) e pagamento somente para Olá VM. Os nomes de imagem têm o prefixo {BYOL}. Para obter mais informações sobre essas opções, consulte [Diretrizes para os preço das VMs do Azure do SQL Server](virtual-machines-windows-sql-server-pricing-guidance.md).

7. Em **Selecionar um modelo de implantação**, verifique se **Resource Manager** está selecionado. Gerenciador de recursos é hello recomendado o modelo de implantação de novas máquinas virtuais. Clique em **Criar**.

    ![Criar VM do SQL com o Resource Manager](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-sql-deployment-model.png)

## <a name="configure-hello-vm"></a>Configurar Olá VM
Há cinco folhas para configuração de uma máquina virtual do SQL Server.

| Etapa | Descrição |
| --- | --- |
| **Noções básicas** |[Definir as configurações básicas](#1-configure-basic-settings) |
| **Tamanho** |[Escolher o tamanho da máquina virtual](#2-choose-virtual-machine-size) |
| **Configurações** |[Configurar os recursos opcionais](#3-configure-optional-features) |
| **Configurações do SQL Server** |[Definir as configurações do SQL Server](#4-configure-sql-server-settings) |
| **Resumo** |[Resumo de saudação de revisão](#5-review-the-summary) |

## <a name="1-configure-basic-settings"></a>1. Definir as configurações básicas
Em Olá **Noções básicas sobre** folha, fornecer Olá informações a seguir:

* Digite um **Nome**exclusivo da máquina virtual.
* Especifique um **nome de usuário** Olá conta de administrador local no hello VM. Essa conta também é adicionada toohello do SQL Server **sysadmin** função de servidor fixa.
* Forneça uma **Senha**forte.
* Se você tiver várias assinaturas, confirme se a assinatura de saudação está correta para Olá nova VM.
* Em Olá **grupo de recursos** , digite um nome para um novo grupo de recursos. Como alternativa, o clique de um grupo de recursos existente em toouse **usar existente**. Um grupo de recursos é uma coleção de recursos relacionados no Azure (máquinas virtuais, contas de armazenamento, redes virtuais etc.).
  
  > [!NOTE]
  > O uso de um novo grupo de recursos é útil se você estiver apenas testando ou aprendendo sobre implantações do SQL Server no Azure. Após concluir o teste, exclua Olá Olá recurso grupo tooautomatically excluir VM e todos os recursos associados a esse grupo de recursos. Para saber mais sobre os grupos de recursos, confira [Visão geral do Azure Resource Manager](../../../azure-resource-manager/resource-group-overview.md).
  > 
  > 
* Selecione um **Local** para essa implantação.
* Clique em **Okey** toosave configurações de saudação.
  
    ![Folha de Noções Básicas do SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-basic.png)

## <a name="2-choose-virtual-machine-size"></a>2. Escolher o tamanho da máquina virtual
Em Olá **tamanho** etapa, escolha um tamanho de máquina virtual em Olá **escolher um tamanho** folha. folha de saudação inicialmente exibe os tamanhos de recomendado de máquina com base em imagem Olá selecionada.

> [!IMPORTANT]
> Olá estimado custo mensal, exibido em Olá **escolher um tamanho** folha não inclui os custos de licenciamento do SQL Server. Esse custo mensal estimado é o custo de saudação do hello VM autônoma. Para edições Olá de Express e Developer do SQL Server, esse é o custo estimado total hello. Para outras edições, consulte Olá [página de preços máquinas virtuais do Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) e selecione a edição de destino do SQL Server. Consulte também Olá [preços orientação para VMs do Azure SQL Server](virtual-machines-windows-sql-server-pricing-guidance.md).

![Opções de tamanho de VM do SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-choose-a-size.png)

Para as cargas de trabalho de produção, recomendamos escolher um tamanho de máquina virtual que dê suporte ao [Armazenamento Premium](../../../storage/storage-premium-storage.md). Se você não precisar desse nível de desempenho, use Olá **exibir todos os** botão, que mostra todas as opções de tamanho de máquina. Por exemplo, você pode usar um tamanho de máquina menor para um ambiente de teste ou desenvolvimento.

> [!NOTE]
> Para obter mais informações sobre tamanhos de máquinas virtuais, consulte [Tamanhos de máquinas virtuais](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Para ver as considerações sobre os tamanhos de VM do SQL Server, consulte as [Práticas recomendadas de desempenho para o SQL Server nas Máquinas Virtuais do Azure](virtual-machines-windows-sql-performance.md).

Escolha o tamanho da máquina e clique em **Selecionar**.

## <a name="3-configure-optional-features"></a>3. Configurar os recursos opcionais
Em Olá **configurações** folha, configurar o armazenamento do Azure, rede e monitoramento para a máquina virtual de saudação.

* Em **Armazenamento**, especifique um **Tipo de disco** Standard ou Premium (SSD). Armazenamento Premium é recomendado para cargas de trabalho de produção.

> [!NOTE]
> Se você selecionar Premium (SSD) para um tamanho de máquina que não dá suporte a armazenamento Premium, o tamanho da máquina será alterado automaticamente.  
> 
> 

* Em **conta de armazenamento**, você pode aceitar o nome de conta de armazenamento provisionado automaticamente hello. Você também pode clicar em **conta de armazenamento** toochoose existente da conta e configurar o tipo de conta de armazenamento hello. Por padrão, o Azure cria uma nova conta de armazenamento com o armazenamento com redundância local. Para saber mais sobre as opções de armazenamento, consulte [Replicação do Armazenamento do Azure](../../../storage/storage-redundancy.md).
* Em **rede**, você pode aceitar valores hello preenchida automaticamente. Você também pode clicar em cada recurso toomanually configurar Olá **rede Virtual**, **sub-rede**, **endereço IP público**, e **degrupodesegurançaderede**. Para fins de saudação deste tutorial, mantenha valores padrão de saudação.
* Habilita Azure **monitoramento** por padrão com hello a mesma conta de armazenamento designada para Olá VM. Você pode alterar essas configurações aqui.
* Em **Conjunto de disponibilidades**, especifique um conjunto de disponibilidades. Para fins de saudação deste tutorial, você pode selecionar **nenhum**. Se você planejar tooset grupos de disponibilidade de AlwaysOn do SQL, configure Olá disponibilidade tooavoid recriando Olá VM.  Para obter mais informações, consulte [gerenciar Olá disponibilidade das máquinas virtuais](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Ao concluir as configurações, clique em **OK**.

## <a name="4-configure-sql-server-settings"></a>4. Definir as configurações do SQL Server
Em Olá **configurações do SQL Server** folha, definir configurações específicas e otimizações para o SQL Server. configurações de saudação que você pode configurar para o SQL Server incluem hello configurações a seguir.

| Configuração |
| --- |
| [Conectividade](#connectivity) |
| [Autenticação](#authentication) |
| [Configuração de armazenamento](#storage-configuration) |
| [Aplicação de patch automatizada](#automated-patching) |
| [Backup Automatizado](#automated-backup) |
| [Integração do Cofre da Chave do Azure](#azure-key-vault-integration) |
| [R Services](#r-services) |

### <a name="connectivity"></a>Conectividade
Em **conectividade SQL**, especifique o tipo de saudação de acesso que você deseja toohello instância do SQL Server essa VM. Para fins de saudação deste tutorial, selecione **pública (internet)** tooallow conexões tooSQL servidor de serviços ou máquinas Olá da internet. Com esta opção selecionada, o Azure configura automaticamente firewall hello e tráfego de tooallow do grupo de segurança de rede de saudação na porta 1433.  

![Opções de conectividade do SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-connectivity-alt.png)

tooconnect tooSQL Server por meio de saudação à internet, você também deve habilitar a autenticação do SQL Server, que é descrito na próxima seção, Olá.

> [!NOTE]
> Ele é possível tooadd mais restrições tooyour comunicações de rede Olá VM do SQL Server. Você pode adicionar mais restrições por grupo de segurança de rede de edição Olá depois Olá VM é criada. Para obter mais informações, consulte [O que é um NSG (Grupo de Segurança de Rede)?](../../../virtual-network/virtual-networks-nsg.md)
> 
> 

Se você preferir toonot habilitar conexões toohello mecanismo de banco de dados por meio de Olá internet, escolha uma saudação as opções a seguir:

* **Local (dentro da VM)** tooallow conexões tooSQL servidor somente de dentro de saudação VM.
* **Privada (dentro de uma rede Virtual)** tooallow conexões tooSQL servidor de máquinas ou serviços em Olá mesma rede virtual.

> [!NOTE]
> imagem da máquina virtual Olá para o SQL Server Express edition não habilita automaticamente protocolo hello TCP/IP. Isso é verdadeiro mesmo para Olá conectividade públicas e privadas opções. Para a edição Express, você deve usar SQL Server Configuration Manager muito[habilitar manualmente o protocolo TCP/IP de saudação](#configure-sql-server-to-listen-on-the-tcp-protocol) depois de criar hello VM.
> 
> 

Em geral, melhore a segurança, escolhendo hello mais restritiva conectividade de seu cenário. Mas todas as opções de saudação são protegidas por meio de regras de grupo de segurança de rede e a autenticação do Windows do SQL.

**Porta** padrões too1433. Você pode especificar um número de porta diferente.
Para obter mais informações, consulte [conectar tooa Máquina Virtual do SQL Server (Gerenciador de recursos) | Microsoft Azure](virtual-machines-windows-sql-connect.md).

### <a name="authentication"></a>Autenticação
Se você precisar da Autenticação do SQL Server, clique em **Habilitar** under **Autenticação do SQL**.

![Autenticação do SQL Server](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-authentication.png)

> [!NOTE]
> Se você planejar tooaccess do SQL Server sobre Olá da internet (ou seja, Olá opções de conectividade pública), você deve habilitar a autenticação do SQL aqui. Toohello de acesso público do SQL Server requer o uso de saudação da autenticação do SQL.
> 
> 

Se você habilitar a Autenticação do SQL Server, especifique um **Nome de logon** e **Senha**. Este nome de usuário é configurado como um logon de autenticação do SQL Server e membro da saudação **sysadmin** função de servidor fixa. Para saber mais sobre os Modos de autenticação, consulte [Escolher um modo de autenticação](http://msdn.microsoft.com/library/ms144284.aspx).

Se você não habilitar a autenticação do SQL Server, você pode usar a conta de administrador local Olá na instância do SQL Server do hello VM tooconnect toohello.

### <a name="storage-configuration"></a>Configuração de armazenamento
Clique em **configuração de armazenamento** toospecify requisitos de armazenamento de saudação.

![Configuração do armazenamento do SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-storage.png)

> [!NOTE]
> Se você selecionar o armazenamento Standard, essa opção não estará disponível. A otimização de armazenamento automático está disponível apenas para o Armazenamento Premium.
> 
> 

Você pode especificar os requisitos como operações IOPs (entrada/saída por segundo), taxa de transferência em MB/s e tamanho total de armazenamento. Configure esses valores usando Olá deslizante escalas. portal de saudação automaticamente calcula o número de saudação de discos com base nesses requisitos.

Por padrão, o Azure otimiza o armazenamento de saudação para 5000 IOPs, 200 MB e 1 TB de espaço de armazenamento. Você pode alterar essas configurações de armazenamento com base na carga de trabalho. Em **armazenamento otimizado para**, selecione uma saudação as opções a seguir:

* **Geral** é a configuração padrão de saudação e dá suporte à maioria das cargas de trabalho.
* **Transacional** processamento otimiza o armazenamento de saudação para cargas de trabalho OLTP de banco de dados tradicional.
* **Data warehouse** otimiza o armazenamento de saudação para cargas de trabalho de análise e emissão de relatórios.

> [!NOTE]
> limites superiores de saudação em controles deslizantes de saudação variam dependendo o tamanho da máquina virtual selecionada.
> 
> 

### <a name="automated-patching"></a>Aplicação de patch automatizada
**Automated patching** está habilitada por padrão. Aplicação de patch automatizada permite que o sistema operacional do Azure tooautomatically patch do SQL Server e hello. Especifique um dia da semana hello, hora e duração de uma janela de manutenção. O Azure realiza a aplicação de patch na janela de manutenção. agendamento de janela de manutenção Olá usa a localidade VM de saudação por tempo. Se você não quiser tooautomatically Azure patch do SQL Server e saudação do sistema operacional, clique em **desabilitar**.  

![Aplicação de patch automatizada do SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-patching.png)

Para saber mais, consulte [Aplicação de Patch Automatizada para SQL Server nas Máquinas Virtuais do Azure](virtual-machines-windows-sql-automated-patching.md).

### <a name="automated-backup"></a>Backup Automatizado
Habilite backups automáticos do banco de dados para todos os bancos de dados em **Backup automatizado**. O backup automatizado está desabilitado por padrão.

Quando você habilita o backup automatizado do SQL, você pode configurar Olá configurações a seguir:

* Período de retenção (dias) para backups
* Toouse de conta de armazenamento de backups
* Opção de criptografia e senha para backups
* Bancos de dados do sistema de backup
* Configurar agendamento de backup

Clique em fazer backup, de saudação tooencrypt **habilitar**. Em seguida, especifique Olá **senha**. O Azure cria um certificado de backups de saudação tooencrypt e Olá usa especificado tooprotect senha esse certificado.

![Backup Automatizado do SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-autobackup2.png)

 Para obter mais informações, veja [Backup Automatizado para o SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-automated-backup.md).

### <a name="azure-key-vault-integration"></a>Integração do Cofre da Chave do Azure
segredos de segurança toostore no Azure para criptografia, clique em **integração do Cofre de chaves do Azure** e clique em **habilitar**.

![Integração do Cofre da Chave do SQL Azure](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-akv.png)

Olá tabela a seguir lista Olá de parâmetros necessários tooconfigure integração do cofre da chave do Azure.

| PARÂMETRO | Descrição | EXEMPLO |
| --- | --- | --- |
| **URL do cofre da chave** |local de saudação do Cofre de chaves hello. |https://contosokeyvault.vault.azure.net/ |
| **Nome de entidade** |Nome de entidade de serviço do Active Directory do Azure Esse nome também é chamado tooas Olá ID do cliente. |fde2b411-33d5-4e11-af04eb07b669ccf2 |
| **Segredo da entidade** |Segredo da entidade de serviço do Azure Active Directory. Esse segredo também é chamado tooas Olá segredo do cliente. |9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM= |
| **Nome da credencial** |**Nome da credencial**: integração AKV cria uma credencial do SQL Server, permitindo que o cofre da chave de toohello Olá VM toohave acesso. Escolha um nome para essa credencial. |mycred1 |

Para saber mais, consulte [Configurar a Integração do Cofre de Chaves do Azure para o SQL nas VMs do Azure](virtual-machines-windows-ps-sql-keyvault.md).

Ao concluir as configurações do SQL Server, clique em **OK**.

### <a name="r-services"></a>R Services
Você pode habilitar os [serviços de R do SQL Server](https://msdn.microsoft.com/library/mt604845.aspx). SQL Server R Services permite que você toouse advanced analytics com o SQL Server 2016. Clique em **habilitar** em Olá **configurações do SQL Server** folha.

![Habilitar os serviços de R do SQL Server](./media/virtual-machines-windows-portal-sql-server-provision/azure-vm-sql-server-r-services.png)


## <a name="5-review-hello-summary"></a>5. Resumo de saudação de revisão
Em Olá **resumo** folha, examine Olá resumo e clique em **Okey** toocreate do SQL Server, o grupo de recursos e recursos especificados para essa VM.

Você pode monitorar a implantação de saudação do portal de saudação do azure. Olá **notificações** botão na parte superior de saudação da tela hello mostra o status básico de implantação de saudação.

> [!NOTE]
> tooprovide com uma ideia na implantação tempos, eu implantei uma região do Leste dos EUA de toohello VM do SQL com as configurações padrão. Esta implantação de teste levou um total de minutos 26 toocomplete. Mas sua implantação pode ser rápida ou mais lenta de acordo com sua região e com as configurações selecionadas.
> 
> 

## <a name="open-hello-vm-with-remote-desktop"></a>Abra Olá VM com área de trabalho remota
Use Olá seguindo as etapas tooconnect toohello virtual machine com área de trabalho remota:

1. Depois de saudação que baseia-se a VM do Azure, o ícone Olá Olá VM aparece no painel do Azure. Você também pode encontrá-lo navegando por suas máquinas virtuais existentes. Clique na nova máquina virtual do SQL. Uma folha da **Máquina virtual** exibe os detalhes de sua máquina virtual.
2. Na parte superior de saudação do hello **Máquina Virtual** folha, clique em **conectar**.
3. navegador de saudação baixa um arquivo RDP para Olá VM. Arquivo RDP Olá aberto.
    ![TooSQL de área de trabalho remota VM](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-remote-desktop.png)
4. saudação de Conexão de área de trabalho remota notifica que Olá Editor desta conexão remota não pode ser identificado. Clique em **conectar** toocontinue.
5. Em Olá **a segurança do Windows** caixa de diálogo, clique em **usar outra conta**.
6. Para **nome de usuário** tipo  **\<nome de usuário >**, onde <user name> é Olá nome de usuário que você especificou quando configurou Olá VM. Você tem uma barra invertida inicial antes do nome de saudação tooadd.
7. Saudação de tipo **senha** configurados anteriormente para essa VM e, em seguida, clique em **Okey** tooconnect.
8. Se houver outro **Conexão de área de trabalho remota** caixa de diálogo solicita se tooconnect, clique em **Sim**.

Depois que você se conectar a máquina de virtual toohello do SQL Server, você pode iniciar o SQL Server Management Studio e conectar-se com a autenticação do Windows usando suas credenciais de administrador local. Se você habilitou a autenticação do SQL Server, você também pode se conectar com a autenticação do SQL usando o logon do SQL hello e senha configurados durante o provisionamento.

Acessar o computador toohello permite que você toodirectly alteração máquina e configurações do SQL Server com base nos seus requisitos. Por exemplo, você pode definir configurações de firewall de saudação ou alterar definições de configuração do SQL Server.

## <a name="connect-toosql-server-remotely"></a>Conecte-se tooSQL servidor remotamente
Neste tutorial, selecionamos **pública** acesso para a máquina virtual de saudação e **autenticação do SQL Server**. Essas conexões configurações Olá configurada automaticamente máquina virtual tooallow do SQL Server de qualquer cliente sobre Olá internet (supondo que tiverem o logon SQL correto Olá).

> [!NOTE]
> Se você não selecionou público durante o provisionamento, etapas adicionais serão necessárias tooaccess sua instância do SQL Server sobre Olá da internet. Para obter mais informações, consulte [conectar tooa Máquina Virtual do SQL Server](virtual-machines-windows-sql-connect.md).
> 
> 

Olá seções a seguir mostra como tooconnect tooyour a instância do SQL Server na sua VM em um computador diferente em Olá da internet.

> [!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]
> 
> 

## <a name="next-steps"></a>Próximas etapas
Para obter outras informações sobre como usar o SQL Server no Azure, consulte [do SQL Server em máquinas virtuais Azure](virtual-machines-windows-sql-server-iaas-overview.md) e hello [Frequently Asked Questions](virtual-machines-windows-sql-server-iaas-faq.md).

Para uma visão geral em vídeo do SQL Server em máquinas virtuais do Azure, inspecionar [VM do Azure é a melhor plataforma Olá para o SQL Server 2016](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016).

[Explorar Olá aprendizado](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) para o SQL Server em máquinas virtuais do Azure.

