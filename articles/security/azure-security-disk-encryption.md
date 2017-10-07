---
title: aaaAzure criptografia de disco para o Windows e Linux VMs de IaaS | Microsoft Docs
description: "Este artigo fornece uma visão geral do Microsoft Azure Disk Encryption para VMs IaaS do Windows e Linux."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: d3fac8bb-4829-405e-8701-fa7229fb1725
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: kakhan
ms.openlocfilehash: b685abdcc908e66d2352ec5ac2d9996aa75af1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a>Azure Disk Encryption para VMs IaaS Windows e Linux
Microsoft Azure está fortemente comprometido tooensuring a privacidade dos dados, Soberania de dados e permite que você toocontrol hospedado do Azure dados por meio de uma variedade de tecnologias avançadas tooencrypt, controlar e gerenciar chaves de criptografia, auditoria e controle de acesso de dados. Isso oferece aos clientes do Azure Olá flexibilidade toochoose Olá solução melhor atende às suas necessidades de negócios. Neste documento, apresentaremos você tooa nova solução de tecnologia "Criptografia de disco do Azure para Windows e de Linux IaaS VM" toohelp proteger e proteger seu dados toomeet seus compromissos de segurança e conformidade organizacionais. papel Olá oferece orientação detalhada sobre como recursos de criptografia do disco do Azure Olá toouse incluindo Olá suporte para cenários e as experiências do usuário Olá.

> [!NOTE]
> Determinadas recomendações podem aumentar o uso de recursos de dados, rede ou computação, resultando em custos adicionais de licença ou inscrição.

## <a name="overview"></a>Visão geral
o Azure Disk Encryption é um novo recurso que ajuda a criptografar os discos de suas máquinas virtuais IaaS Windows e Linux. Criptografia de disco do Azure utiliza o padrão da indústria Olá [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) recurso do Windows e hello [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) recurso de criptografia de volume tooprovide Linux para hello SO e discos de dados de saudação. Olá solução é integrada com [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) toohelp controlar e gerenciar chaves de criptografia de disco hello e segredos em sua assinatura do Cofre de chaves. solução de saudação também garante que todos os dados em discos de máquina virtual Olá sejam criptografados em repouso no armazenamento do Azure.

O Azure Disk Encryption para VMs IaaS do Windows e Linux agora está em **Disponibilidade Geral** em todas as regiões públicas do Azure e AzureGov para VMs Standard e VMs com armazenamento premium.

### <a name="encryption-scenarios"></a>Cenários de criptografia
Olá solução de criptografia de disco do Azure dá suporte a saudação os seguintes cenários de cliente:

* Habilitar a criptografia em novas VMs IaaS criadas com base em VHD pré-criptografado e chaves de criptografia
* Habilitar a criptografia em novas VMs de IaaS criado a partir de imagens de galeria do Azure Olá com suporte
* Habilitar a criptografia em VMs IaaS existentes em execução no Azure
* Desabilitar a criptografia em VMs IaaS do Windows
* Desabilitar a criptografia em unidades de dados para VMs IaaS do Linux
* Ativar criptografia de VMs de disco gerenciado
* Atualizar configurações de criptografia de uma VM de armazenamento não premium criptografada existente
* Backup e restauração de VMs criptografadas, criptografadas com chave de critografia de chave

solução de saudação dá suporte à saudação os seguintes cenários para VMs de IaaS quando eles estão habilitados no Microsoft Azure:

* Integração com o Cofre da Chave do Azure
* VMs de camada padrão: [ A, D, DS, G, GS, F e VMs IaaS ](https://azure.microsoft.com/pricing/details/virtual-machines/)
* Habilitar a criptografia em Windows e VMs de IaaS Linux e máquinas virtuais de disco gerenciado de saudação suporte para imagens da Galeria do Azure
* Desativar criptografia no SO e nas unidades de dados para VMs da IaaS do Windows e VMs de disco gerenciado
* Desativar criptografia em unidades de dados para Linux Iaas VMs e VMs de disco gerenciado
* Habilitar a criptografia em VMs IaaS executando o sistema operacional Windows Client
* Habilitar a criptografia em volumes com caminhos de montagem
* Habilitar criptografia em VMs do Linux configuradas com disk striping (RAID) usando mdadm
* Habilitar criptografia no Linux VMs utilizando LVM para discos de dados
* Habilitar a criptografia em VMs do Windows configuradas com os Espaços de Armazenamento
* Atualizar configurações de criptografia de uma VM de armazenamento não premium criptografada existente
* Para todas as regiões do Público do Azure e AzureGov há suporte

solução de saudação não oferece suporte a saudação cenários, recursos e tecnologias a seguir:

* VMs IaaS da camada Básica
* Como desabilitar a criptografia em unidades do sistema operacional para VMs IaaS do Linux
* Desabilitar a criptografia em uma unidade de dados se Olá unidade do sistema operacional for criptografada para VMs de Iaas Linux
* VMs de IaaS que são criadas usando o método de criação de VM clássico Olá
* Habilitar criptografia em imagens personalizadas do cliente de VMs de IaaS do Linux e Windows NÃO tem suporte. Habilitar criptografia no disco do SO do LVM do Linux, atualmente não tem suporte. Este suporte será disponibilizado em breve.
* Integração com o Serviço de Gerenciamento de Chaves no local
* Arquivos do Azure (sistema de arquivos compartilhados), NFS (Network File System), volumes dinâmicos e VMs do Windows configuradas com Sistemas RAID baseados em software
* Backup e restauração de VMs criptografadas, criptografadas com chave de criptografia de chave.
* Atualize configurações de criptografia de um armazenamento VM existente criptografado premium.

> [!NOTE]
> Backup e restauração de VMs criptografadas com suporte apenas para VMs que são criptografados com a configuração de KEK hello. Não há suporte em VMs que são criptografados sem KEK. KEK é um parâmetro opcional que habilita a criptografia de VM. Esse suporte será oferecido em breve.
> Atualizar configurações de criptografia de uma VM de armazenamento não premium criptografada existente. Esse suporte será oferecido em breve.

### <a name="encryption-features"></a>Recursos de criptografia
Quando você habilita e implanta a criptografia de disco do Azure para VMs de IaaS do Azure, hello seguintes recursos estão habilitados, dependendo da configuração de saudação fornecida:

* Criptografia de volume de inicialização de Olá Olá SO volume tooprotect em repouso no armazenamento
* Criptografia de dados volumes tooprotect Olá os volumes de dados em repouso no armazenamento
* Desabilitar a criptografia em hello sistema operacional e dados unidades para as VMs de IaaS do Windows
* Desabilitar a criptografia em dados Olá unidades para as VMs de IaaS Linux (somente se o sistema operacional da unidade não é criptografado)
* Protegendo chaves de criptografia de saudação e segredos em sua assinatura do Cofre de chaves
* Relatar o status de criptografia de saudação do hello criptografado IaaS VM
* Remoção de configurações de criptografia de disco da máquina de virtual IaaS Olá
* Backup e restauração de VMs criptografadas usando o serviço de Backup do Azure Olá

> [!NOTE]
> Backup e restauração de VMs criptografadas com suporte apenas para VMs que são criptografados com a configuração de KEK hello. Não há suporte em VMs que são criptografados sem KEK. KEK é um parâmetro opcional que habilita a criptografia de VM.

o Azure Disk Encryption para VMS IaaS para a solução Windows e Linux inclui:

* extensão de criptografia de disco Olá para Windows.
* extensão de criptografia de disco Olá para Linux.
* Olá cmdlets do PowerShell de criptografia de disco.
* Olá cmdlets de interface de linha de comando (CLI) do Azure de criptografia de disco.
* Olá modelos do Gerenciador de recursos do Azure de criptografia de disco.

Olá solução de criptografia de disco do Azure tem suporte em VMs de IaaS que estejam executando o SO Windows ou Linux. Para obter mais informações sobre sistemas operacionais de saudação com suporte, consulte hello "pré-requisitos" seção.

> [!NOTE]
> Não são cobradas taxas adicionais para a criptografia de discos de VM com o Azure Disk Encryption.

### <a name="value-proposition"></a>Proposta de valor
Quando você aplica solução Olá gerenciamento de criptografia de disco do Azure, você pode atender Olá necessidades de negócios a seguir:

* As VMs de IaaS são protegidas no restante, porque você pode usar a criptografia padrão da indústria tecnologia tooaddress segurança e conformidade requisitos organizacionais.
* As VMs IaaS são inicializadas por meio de políticas e chaves controladas pelo cliente, e você pode auditar seu uso no cofre de chaves.

### <a name="encryption-workflow"></a>Fluxo de trabalho de criptografia
criptografia de disco tooenable para Windows e VMs do Linux, Olá a seguir:

1. Escolha um cenário de criptografia entre Olá anterior cenários de criptografia.
2. Ativar criptografia de disco tooenabling por meio do modelo do Gerenciador de recursos de criptografia de disco do Azure hello, cmdlets do PowerShell ou comando CLI e especificar a configuração de criptografia de saudação.

   * Para cenário VHD criptografado cliente hello, carregar conta de armazenamento Olá criptografado VHD tooyour e cofre da chave Olá criptografia tooyour material de chave. Em seguida, fornece Olá criptografia configuração tooenable criptografia em uma nova VM IaaS.
   * Para novas VMs que são criados a partir Olá Marketplace e VMs existentes que já estão em execução no Azure, fornecem criptografia de tooenable de configuração de criptografia Olá sobre Olá IaaS VM.

3. Conceder acesso toohello plataforma Windows Azure tooread Olá chave de criptografia material (chaves de criptografia do BitLocker para os sistemas Windows) e a frase secreta para Linux da criptografia de tooenable seu Cofre de chaves em Olá IaaS VM.

4. Fornece hello Azure Active Directory (AD do Azure) aplicativo identidade toowrite Olá criptografia tooyour material de chave Cofre de chaves. Isso habilita a criptografia em hello IaaS VM para cenários de saudação mencionado na etapa 2.

5. Azure atualiza o modelo de serviço VM Olá com criptografia e a configuração do Cofre de chaves de Olá e define sua VM criptografado.

 ![Microsoft Antimalware no Azure](./media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a>Fluxo de trabalho de descriptografia
criptografia de disco toodisable para VMs de IaaS, Olá completo seguindo as etapas de alto nível:

1. Escolha toodisable criptografia (decodificação) em uma VM IaaS em execução no Azure por meio do modelo do Gerenciador de recursos de criptografia de disco do Azure hello ou cmdlets do PowerShell e especificar a configuração de descriptografia hello.

 Esta etapa desabilitará a criptografia do volume de dados de sistema operacional ou Olá Olá ou ambos em Olá executando Windows IaaS VM. No entanto, como mencionado na seção anterior hello, desabilitando a criptografia de disco do sistema operacional para Linux não há suporte. etapa de descriptografia Olá só é permitida para unidades de dados em VMs do Linux desde que o disco do sistema operacional Olá não está criptografado.
2. Atualizações do Azure Olá modelo de serviço VM e Olá IaaS VM está marcado como descriptografada. conteúdo de saudação do hello VM não é criptografado em repouso.

> [!NOTE]
> operação de criptografia desabilitar Olá não exclui o cofre e hello criptografia chave material de chave (chaves de criptografia do BitLocker para os sistemas Windows) ou a senha para Linux.
 > Não há suporte para desativação de criptografia de disco de OS para Linux. etapa de descriptografia Olá só é permitida para unidades de dados em VMs do Linux.
Não há suporte para a desabilitação da criptografia de disco de dados para Linux se Olá unidade do sistema operacional está criptografado.

## <a name="prerequisites"></a>Pré-requisitos
Antes de habilitar a criptografia de disco do Azure em VMs de IaaS do Azure para cenários de saudação suporte discutidas Olá seção "Visão geral", consulte Olá pré-requisitos a seguir:

* Você deve ter um recurso de toocreate válido de assinatura ativa do Azure no Azure em regiões Olá com suporte.
* Criptografia de disco do Azure tem suporte em Olá seguintes versões do Windows Server: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 e Windows Server 2016.
* Criptografia de disco do Azure tem suporte em Olá versões cliente do Windows a seguir: cliente Windows 8 e Windows 10.

> [!NOTE]
> Para o Windows Server 2008 R2, você deve ter o .NET Framework 4.5 instalado antes de habilitar a criptografia no Azure. Você pode instalá-lo a partir do Windows Update pela instalação de atualização opcional de saudação Microsoft .NET Framework 4.5.2 para sistemas baseados em x64 do Windows Server 2008 R2 ([KB2901983](https://support.microsoft.com/kb/2901983)).

* Há suporte para criptografia de disco do Azure em Olá seguindo a Galeria do Azure com base em versões e distribuições do Linux server:

| Distribuição Linux | Versão | Tipo de Volume com Suporte para Criptografia|
| --- | --- |--- |
| Ubuntu | 16.04-LTS-DIÁRIO | SO e Disco de Dados |
| Ubuntu | 14.04.5-LTS-DIÁRIO | SO e Disco de Dados |
| Ubuntu | 12.10 | Disco de dados |
| Ubuntu | 12.04 | Disco de dados |
| RHEL | 7.3 | SO e Disco de Dados |
| RHEL | 7,2 | SO e Disco de Dados |
| RHEL | 6,8 | SO e Disco de Dados |
| RHEL | 6.7 | Disco de dados |
| CentOS | 7.3 | SO e Disco de Dados |
| CentOS | 7.2n | SO e Disco de Dados |
| CentOS | 6,8 | SO e Disco de Dados |
| CentOS | 7.1 | Disco de dados |
| CentOS | 7.0 | Disco de dados |
| CentOS | 6.7 | Disco de dados |
| CentOS | 6.6 | Disco de dados |
| CentOS | 6.5 | Disco de dados |
| openSUSE | 13.2 | Disco de dados |
| SLES | 12 SP1 | Disco de dados |
| SLES | 12-SP1 (Premium) | Disco de dados |
| SLES | HPC 12 | Disco de dados |
| SLES | 11-SP4 (Premium) | Disco de dados |
| SLES | 11 SP4 | Disco de dados |

* Criptografia de disco do Azure requer que seu Cofre de chaves e VMs residam em Olá mesma região do Azure e assinatura.

> [!NOTE]
> Configurando recursos de saudação em regiões separadas faz com que uma falha na habilitação do recurso de criptografia de disco do Azure hello.

* tooset backup e configurar o Cofre de chaves de criptografia de disco do Azure, consulte a seção **definir e configurar o Cofre de chaves de criptografia de disco do Azure** em Olá *pré-requisitos* deste artigo.
* tooset backup e configurar o aplicativo do AD do Azure no Azure Active directory para criptografia de disco do Azure, consulte a seção **configurar o aplicativo hello AD do Azure no Azure Active Directory** em Olá *pré-requisitos* seção deste artigo.
* tooset backup e configurar política de acesso do Cofre de chaves Olá para o aplicativo hello AD do Azure, consulte a seção **configurar política de acesso do Cofre de chaves Olá para o aplicativo hello AD do Azure** em Olá *pré-requisitos* seção Este artigo.
* tooprepare um VHD do Windows previamente criptografado, consulte a seção **preparar um VHD do Windows previamente criptografado** em Olá *apêndice*.
* tooprepare um VHD Linux previamente criptografado, consulte a seção **preparar um VHD Linux pré-criptografado** em Olá *apêndice*.
* Olá plataforma Windows Azure precisa de chaves de criptografia do acesso toohello ou segredos em seu Cofre de chaves toomake-los disponíveis toohello máquina de virtual quando ele é inicializado e descriptografa o volume do sistema operacional da máquina virtual de saudação. plataforma de tooAzure permissões toogrant, Olá conjunto **EnabledForDiskEncryption** propriedade no cofre de chaves hello. Para obter mais informações, consulte **definir e configurar o Cofre de chaves de criptografia de disco do Azure** em Olá apêndice.
* O segredo do cofre de chaves e as URLs KEK devem ter controle de versão. O Azure impõe essa restrição de controle de versão. Para um segredo válido e KEK URLs, consulte Olá exemplos a seguir:

  * Exemplo de URL de segredo válida: *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*
  * Exemplo de URL KEK válida: *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*

* o Azure Disk Encryption não dá suporte à especificação de números de portas como parte de segredos do cofre de chaves e URLs KEK. Para obter exemplos de URLs de Cofre de chaves com suporte e sem suporte, consulte o seguinte hello:

  * URL do cofre de chaves inaceitável *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*
  * URL do cofre de chaves aceitável: *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*

* recurso de criptografia de disco do Azure do tooenable hello, Olá VMs de IaaS deve atender aos Olá seguindo os requisitos de configuração de ponto de extremidade de rede:
  * tooget um cofre de chaves token tooconnect tooyour, Olá IaaS VM deve ser capaz de tooconnect tooan Active Directory do Azure ponto de extremidade \[login.microsoftonline.com\].
  * toowrite Olá criptografia chaves tooyour Cofre de chaves, Olá IaaS VM deve ser o ponto de extremidade de Cofre de chaves de toohello tooconnect possível.
  * Olá IaaS VM deve ser capaz de tooconnect tooan armazenamento do Azure ponto de extremidade que hosts Olá repositório de extensão do Azure e uma conta de armazenamento do Azure que hospeda Olá arquivos VHD.

  > [!NOTE]
  > Se a política de segurança limita o acesso de VMs do Azure toohello da Internet, poderá resolver Olá precede o URI e configurar toohello de conectividade de saída de tooallow uma regra específica IPs.
  >
  >tooconfigure e acessar o Cofre de chaves do Azure atrás de um firewall (https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)

* Use a versão mais recente de saudação do SDK do Azure PowerShell versão tooconfigure criptografia de disco do Azure. Baixar a versão mais recente de saudação do [versão do PowerShell do Azure](https://github.com/Azure/azure-powershell/releases)

 > [!NOTE]
  > Não há suporte para o Azure Disk Encryption no [SDK do Azure PowerShell versão 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016). Se você estiver recebendo um erro relacionado toousing Azure PowerShell 1.1.0, consulte [tooAzure relacionados para erro de criptografia do disco do Azure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).

* toorun qualquer comando CLI do Azure e associá-lo a sua assinatura do Azure, você deve primeiro instalar a CLI do Azure:
  * tooinstall CLI do Azure e associá-lo a sua assinatura do Azure, consulte [como tooinstall e configurar a CLI do Azure](../cli-install-nodejs.md).
  * toouse CLI do Azure para Mac, Linux e Windows com o Azure Resource Manager, consulte [comandos de CLI do Azure no Gerenciador de recursos de modo](../virtual-machines/azure-cli-arm-commands.md).

* Ao criptografar um disco gerenciado, é obrigatório tootake pré-requisito um instantâneo do disco Olá gerenciado ou um backup de disco Olá fora de criptografia de tooenabling anterior de criptografia de disco do Azure.  Sem um backup em vigor, qualquer falha inesperada durante a criptografia pode renderizar disco hello e VM inacessível sem uma opção de recuperação.  Conjunto AzureRmVMDiskEncryptionExtension atualmente não fazer backup de discos gerenciados e gerarão um erro se usado em um disco gerenciado, a menos que Olá - skipVmBackup parâmetro foi especificado.  Esse parâmetro é toouse unsafe, a menos que um backup já foi feito fora de criptografia de disco do Azure.   Quando Olá - skipVmBackup parâmetro for especificado, Olá cmdlet não fará um backup de tooencryption anterior de disco Olá gerenciado.  Por esse motivo, é considerada um toomake pré-requisito obrigatório se um backup de disco gerenciado de saudação que VM está em vigor anterior tooenabling criptografia de disco do Azure no caso de recuperação é posterior é necessária.  
> [!NOTE]
 > parâmetro de skipVmBackup - Olá nunca deve ser usado, a menos que um instantâneo ou backup já foram feito fora de criptografia de disco do Azure. 

* Olá solução de criptografia de disco do Azure usa o protetor de chave externo Olá BitLocker para VMs de IaaS do Windows. Para VMs ingressadas no domínio, NÃO envie nenhuma política de grupo que imponha protetores de TPM. Para obter informações sobre a política de grupo hello "Permitir BitLocker sem um TPM compatível", consulte [referência de política de grupo do BitLocker](https://technet.microsoft.com/library/ee706521).
* Política do BitLocker em máquinas virtuais de domínio associado com a política de grupo personalizado deve incluir Olá configuração a seguir: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key` criptografia de disco do Azure falhará quando as configurações de diretiva de grupo personalizado para o Bitlocker são incompatíveis. Em computadores que não tinham Olá a configuração de política correta, aplicar a nova política de hello, forçando Olá de nova política tooupdate (gpupdate.exe /force) e, em seguida, reiniciar pode ser necessária.  
* toocreate um aplicativo do AD do Azure, criar um cofre de chaves, ou configurar um cofre de chave existente e habilitar a criptografia, consulte Olá [script do PowerShell pré-requisito de criptografia de disco do Azure](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).
* os pré-requisitos de criptografia de disco tooconfigure usando Olá CLI do Azure, consulte [esse script Bash](https://github.com/ejarvi/ade-cli-getting-started).
* toouse hello Azure Backup service tooback backup e restauração criptografada VMs, quando a criptografia está habilitada com a criptografia de disco do Azure, criptografam suas VMs usando configuração de chave de criptografia de disco do Azure hello. saudação de serviço de Backup oferece suporte a máquinas virtuais que são criptografadas usando apenas a configuração de KEK. Consulte [como tooback backup e restauração criptografada máquinas virtuais com criptografia de Backup do Azure](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).

* Ao criptografar um volume do sistema operacional Linux, observe que uma reinicialização VM é necessária no final de saudação do processo de saudação no momento. Isso pode ser feito por meio do portal de hello, powershell ou CLI.   progresso de saudação tootrack de criptografia, sondar periodicamente a mensagem de saudação do status retornada por Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.  Após a conclusão da criptografia, a mensagem de status de Olá Olá retornada por este comando indicará isso.  Por exemplo, "ProgressMessage: disco do sistema operacional criptografado com êxito, reinicialize Olá VM" no hello ponto de VM pode ser reiniciada e usada.  

* Criptografia de disco do Azure para Linux requer dados discos toohave um sistema de arquivos montados em tooencryption anterior do Linux

* Recursivamente discos de dados montados não são suportados pelo Olá criptografia de disco do Azure para Linux. Por exemplo, se hello sistema de destino foi montado em um disco em /foo/bar e, em seguida, outro na /foo/bar/baz, criptografia de saudação do /foo/bar/baz terá êxito, mas a criptografia da barra/foo/falhará. 

* Imagens da Galeria do Azure com suporte que atendem aos pré-requisitos mencionados acima Olá somente há suporte para criptografia de disco do Azure. Não há suporte para imagens personalizadas do cliente devido toocustom esquemas de partição e comportamentos de processo que podem existir nessas imagens. Além disso, até mesmo VMs baseadas em imagem de galeria que inicialmente atendiam aos pré-requisitos, mas que foram modificadas após a criação, podem ser incompatíveis.  Para que motivo, Olá sugerido procedimento usado para criptografar uma VM do Linux é toostart de uma imagem da Galeria limpa, criptografar Olá VM e, em seguida, adicionar software personalizado ou dados toohello VM conforme necessário.  

> [!NOTE]
> Backup e restauração de VMs criptografadas com suporte apenas para VMs que são criptografados com a configuração de KEK hello. Não há suporte em VMs que são criptografados sem KEK. KEK é um parâmetro opcional que permite VM.

#### <a name="set-up-hello-azure-ad-application-in-azure-active-directory"></a>Configurar Olá aplicativo AD do Azure no Azure Active Directory
Quando você precisar toobe criptografia habilitada em uma VM em execução no Azure, a criptografia de disco do Azure gera e grava o Cofre de chaves do hello criptografia chaves tooyour. O gerenciamento de chaves de criptografia no cofre de chaves requer a autenticação do Azure AD.

Para essa finalidade, crie um aplicativo Azure AD. Você pode encontrar etapas detalhadas para registrar um aplicativo na seção de "Obter uma identidade Olá aplicativo" hello de postagem de blog Olá [Cofre de chaves do Azure - passo](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx). Esta postagem também contém vários exemplos úteis para configurar o cofre de chaves. Para fins de autenticação, você pode usar a autenticação baseada em segredo do cliente ou a autenticação Azure AD baseada em certificado do cliente.

#### <a name="client-secret-based-authentication-for-azure-ad"></a>Autenticação do Azure AD baseada em segredo do cliente
seções Olá a seguir podem ajudá-lo a configurar uma autenticação com base em segredo do cliente do AD do Azure.

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a>Criar um aplicativo Azure AD usando o Azure PowerShell
Use Olá toocreate de cmdlet do PowerShell um aplicativo do AD do Azure a seguir:

    $aadClientSecret = "yourSecret"
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> $azureAdApplication.ApplicationId é hello ClientID do AD do Azure e $aadClientSecret é o segredo do cliente Olá que você deve usar tooenable posterior a criptografia de disco do Azure. Proteger adequadamente o segredo do cliente de saudação do AD do Azure.

##### <a name="setting-up-hello-azure-ad-client-id-and-secret-from-hello-azure-classic-portal"></a>Configuração de ID de cliente de saudação do AD do Azure e o segredo de saudação portal clássico do Azure
Você também pode configurar sua ID de cliente do AD do Azure e o segredo usando Olá [portal clássico do Azure]( https://manage.windowsazure.com). tooperform task, Olá a seguir:

1. Clique em Olá **do Active Directory** guia.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. Clique em **Adicionar aplicativo**e, em seguida, tipo hello nome do aplicativo.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. Clique o botão de seta hello e, em seguida, configurar propriedades do aplicativo hello.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. Clique em marca de seleção Olá Olá toofinish de canto esquerdo inferior. página de configuração de aplicativo Hello aparece e ID de cliente do AD do Azure Olá é exibida na parte inferior da saudação da página de saudação.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. Salve o segredo do cliente de saudação do AD do Azure clicando em Olá **salvar** botão. Observe o segredo do cliente de saudação do AD do Azure na caixa de texto Olá chaves. Proteja-o adequadamente.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > Não há suporte para Olá anterior fluxo Olá portal clássico do Azure.

##### <a name="use-an-existing-application"></a>Usar um aplicativo existente
tooexecute Olá comandos a seguir, obtenha e use Olá [módulo PowerShell do AD do Azure](https://technet.microsoft.com/library/jj151815.aspx).

> [!NOTE]
> Olá comandos a seguir devem ser executados de uma nova janela do PowerShell. Não use o Azure PowerShell ou comandos Olá tooexecute da janela de saudação do Azure Resource Manager. Recomendamos essa abordagem porque esses cmdlets no módulo de MSOnline de saudação ou o PowerShell do Azure AD.

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a>Autenticação baseada em certificado do Azure AD
> [!NOTE]
> No momento, não há suporte para a autenticação baseada em certificado do Azure AD em VMs do Linux.

Olá seções a seguir mostram como tooconfigure uma autenticação baseada em certificado do AD do Azure.

##### <a name="create-an-azure-ad-application"></a>Criar um aplicativo Azure AD
toocreate um aplicativo do AD do Azure, execute Olá cmdlets do PowerShell a seguir:

> [!NOTE]
> Substitua o seguinte Olá `yourpassword` cadeia de caracteres com sua senha segura e a senha de saudação de proteção.

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

Depois de concluir esta etapa, carregar um cofre de chaves de tooyour do arquivo PFX e habilitar Olá acesso política necessária toodeploy tooa esse certificado VM.

##### <a name="use-an-existing-azure-ad-application"></a>Usar um aplicativo existente do Azure AD
Se você estiver configurando a autenticação baseada em certificado para um aplicativo existente, use cmdlets do PowerShell Olá mostrado aqui. Ser tooexecute-se de uma nova janela do PowerShell.

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

Depois de concluir esta etapa, carregue um cofre de chaves de tooyour do arquivo PFX e habilitar política de acesso de saudação que é necessário toodeploy Olá certificado tooa VM.

##### <a name="upload-a-pfx-file-tooyour-key-vault"></a>Carregar um cofre de chaves de tooyour do arquivo PFX
Para obter uma explicação detalhada desse processo, consulte [Olá oficial Blog da equipe do Azure Key Vault](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx). No entanto, Olá cmdlets do PowerShell a seguir é tudo o que precisa para tarefa de saudação. Ser tooexecute se-las no console do PowerShell do Azure.

> [!NOTE]
> Substitua o seguinte Olá `yourpassword` cadeia de caracteres com sua senha segura e a senha de saudação de proteção.

    $certLocalPath = 'C:\certs\myaadapp.pfx'
    $certPassword = "yourpassword"
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’

    $fileContentBytes = get-content $certLocalPath -Encoding Byte
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

    $jsonObject = @"
    {
    "data": "$filecontentencoded",
    "dataType" :"pfx",
    "password": "$certPassword"
    }
    "@

    $jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
    $jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

    Switch-AzureMode -Name AzureResourceManager
    $secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
    Set-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName -SecretValue $secret
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ResourceGroupName $resourceGroupName –EnabledForDeployment

##### <a name="deploy-a-certificate-in-your-key-vault-tooan-existing-vm"></a>Implante um certificado em seu tooan de Cofre de chaves existente VM
Depois de terminar de carregar Olá PFX, implante um certificado no hello tooan de Cofre de chaves existente VM com os seguintes hello:
 ```
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’
    $vmName = ‘yourVMName’
    $certUrl = (Get-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName).Id
    $sourceVaultId = (Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $resourceGroupName).ResourceId
    $vm = Get-AzureRmVM -ResourceGroupName $resourceGroupName -Name $vmName
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore "My" -CertificateUrl $certUrl
    Update-AzureRmVM -VM $vm  -ResourceGroupName $resourceGroupName
 ```

#### <a name="set-up-hello-key-vault-access-policy-for-hello-azure-ad-application"></a>Definir a política de acesso do Cofre de chaves Olá para o aplicativo hello AD do Azure
Seu aplicativo do AD do Azure precisa de direitos tooaccess Olá as chaves ou os segredos no cofre hello. Saudação de uso [ `Set-AzureKeyVaultAccessPolicy` ](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet toogrant permissões toohello aplicativo usando a ID do cliente hello (que foi gerado quando o aplicativo hello foi registrado) como Olá _– ServicePrincipalName_ valor do parâmetro. toolearn mais, consulte Olá postagem de blog [Cofre de chaves do Azure - passo](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx). Aqui está um exemplo de como tooperform essa tarefa por meio do PowerShell:

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> Criptografia de disco do Azure requer Olá tooconfigure após o aplicativo de cliente de tooyour AD do Azure de políticas de acesso: _WrapKey_ e _definir_ permissões.

## <a name="terminology"></a>Terminologia
toounderstand alguns dos termos comuns Olá usados por esta tecnologia, use Olá terminologia a tabela a seguir:

| Terminologia | Definição |
| --- | --- |
| AD do Azure | Azure AD significa [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/). Uma conta do Azure AD é um pré-requisito para autenticar, armazenar e recuperar segredos do cofre de chaves. |
| Cofre da Chave do Azure | O Key Vault é um serviço de gerenciamento de chaves criptográfico baseado em módulos de segurança de hardware validados pelo FIPS (Federal Information Processing Standards), que ajuda a proteger as chaves criptográficas e os segredos confidenciais. Para obter mais informações, confira a documentação do [Key Vault](https://azure.microsoft.com/services/key-vault/). |
| ARM | Gerenciador de Recursos do Azure |
| BitLocker |[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) é uma reconhecido Windows volume tecnologia de criptografia que foi usada criptografia de disco tooenable em VMs de IaaS do Windows. |
| BEK | Chaves de criptografia do BitLocker são volume de inicialização Olá SO tooencrypt usados e os volumes de dados. chaves do BitLocker Olá são protegidas em um cofre de chaves como segredos. |
| CLI | Confira [Interface de linha de comando do Azure](../cli-install-nodejs.md). |
| DM-Crypt |[DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) é subsistema de criptografia transparente de disco com base em Linux Olá que usou a criptografia de disco tooenable em VMs de IaaS do Linux. |
| KEK | Chave de criptografia de chave é Olá chave assimétrica (RSA de 2048) que você pode usar tooprotect ou encapsular segredo hello. Você pode fornecer uma chave protegida por HSM (módulos de segurança de hardware) ou uma chave protegida por software. Para obter mais detalhes, confira a [documentação do Azure Key Vault](https://azure.microsoft.com/services/key-vault/). |
| Cmdlets de DNS | Confira [Cmdlets do Azure PowerShell](/powershell/azure/overview). |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a>Instalar e configurar o cofre de chaves de Azure Disk Encryption
Criptografia de disco do Azure ajuda a proteger chaves de criptografia de disco de hello e segredos no cofre de chaves. tooset o seu Cofre de chaves de criptografia de disco do Azure, Olá concluído as etapas em cada uma das seguintes seções de saudação.

#### <a name="create-a-key-vault"></a>Criar um cofre de chave
toocreate um cofre de chaves, use um dos Olá as opções a seguir:

* [Modelo "101-Key-Vault-Create" do Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* [Cmdlets do cofre de chaves do Azure PowerShell](/powershell/module/azurerm.keyvault/#key_vault)
* Gerenciador de Recursos do Azure
* Como muito[proteger seu Cofre de chaves](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)

> [!NOTE]
> Se você já tiver configurado um cofre de chaves para sua assinatura, ignore toohello próxima seção.

![Cofre da Chave do Azure](./media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a>Configurar uma chave de criptografia de chave (opcional)
Se você quiser toouse uma KEK para uma camada adicional de segurança para chaves de criptografia do BitLocker Olá, adicione um cofre de chaves do KEK tooyour. Saudação de uso [ `Add-AzureKeyVaultKey` ](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) toocreate cmdlet uma chave de criptografia de chave no cofre de chave hello. Você também pode importar a KEK do HSM do gerenciamento de chaves local. Para obter mais detalhes, confira a [Documentação do Key Vault](https://azure.microsoft.com/documentation/services/key-vault/).

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

Você pode adicionar Olá KEK indo tooAzure Gerenciador de recursos ou usando a interface do Cofre de chaves.

![Cofre da Chave do Azure](./media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a>Definir permissões de cofre de chaves
Olá plataforma Windows Azure precisa de chaves de criptografia do acesso toohello ou segredos em seu Cofre de chaves toomake-los disponível toohello VM para inicializar e descriptografia de volumes de saudação. toogrant permissões toohello plataforma Windows Azure, Olá conjunto **EnabledForDiskEncryption** propriedade na chave Olá cofre usando o cmdlet do PowerShell Olá Cofre de chaves:

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

Você também pode definir Olá **EnabledForDiskEncryption** propriedade visitando Olá [Gerenciador de recursos do Azure](https://resources.azure.com).

Como mencionado anteriormente, você deve definir Olá **EnabledForDiskEncryption** propriedade em seu Cofre de chaves. Caso contrário, ocorrerá falha na implantação de saudação.

Você pode configurar políticas de acesso para seu aplicativo do AD do Azure na interface do Cofre de chaves hello, conforme mostrado aqui:

![Cofre da Chave do Azure](./media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![Cofre da Chave do Azure](./media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

Em Olá **políticas de acesso avançados** guia, certifique-se de que seu Cofre de chaves está habilitado para criptografia de disco do Azure:

![Cofre de chaves do Azure](./media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a>Cenários de implantação de criptografia de disco e experiências de usuário
Você pode habilitar muitos cenários de criptografia de disco e etapas de saudação podem variar de acordo cenário de toohello. Olá, seções a seguir abordam os cenários hello mais detalhadamente.

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-hello-marketplace"></a>Habilitar a criptografia em novas VMs de IaaS que são criados a partir Olá Marketplace
Você pode habilitar a criptografia de disco em nova VM do Windows IaaS de saudação Marketplace no Azure usando Olá [modelo do Gerenciador de recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).

1. No modelo de saudação de início rápido do Azure, clique em **implantar tooAzure**, insira a configuração de criptografia de saudação em Olá **parâmetros** folha e depois clique em **Okey**.

2. Selecione a assinatura hello, grupo de recursos, local do grupo de recursos, os termos legais e contrato e, em seguida, clique em **criar** tooenable criptografia em uma nova VM IaaS.

> [!NOTE]
> Este modelo cria uma nova VM criptografado do Windows que usa a imagem da Galeria Olá Windows Server 2012.

Você pode habilitar a criptografia de disco em uma nova VM IaaS do RedHat Linux 7.2 com uma matriz RAID 0 de 200 GB usando esse [modelo do Gerenciador de Recursos](https://aka.ms/fde-rhel). Depois de implantar o modelo hello, verificar o status de criptografia de VM de saudação usando Olá `Get-AzureRmVmDiskEncryptionStatus` cmdlet, conforme descrito em [SO com criptografia de unidade em uma VM do Linux em execução](#encrypting-os-drive-on-a-running-linux-vm). Quando a máquina Olá retorna um status de _VMRestartPending_, reinicie Olá VM.

Olá tabela a seguir lista parâmetros de modelo do Gerenciador de recursos de saudação para novas VMs do cenário do Marketplace hello usando uma ID de cliente do AD do Azure:

| Parâmetro | Descrição |
| --- | --- |
| adminUserName | Nome de usuário de administrador para a máquina virtual de saudação. |
| adminPassword | Senha do usuário administrador da máquina virtual de saudação. |
| newStorageAccountName | Nome do toostore de conta de armazenamento Olá SO e VHDs de dados. |
| vmSize | Tamanho da VM de saudação. Atualmente, há suporte somente para séries Standard A, D e G. |
| virtualNetworkName | Nome de rede virtual que Olá NIC de VM do hello deve pertencer ao. |
| subnetName | Nome da sub-rede Olá Olá VNet que Olá NIC de VM deve pertencer ao. |
| AADClientID | ID do cliente do aplicativo de saudação do AD do Azure que tenha permissões toowrite segredos tooyour chave de cofre. |
| AADClientSecret | Segredo do cliente do aplicativo de saudação do AD do Azure que tenha permissões toowrite segredos tooyour chave de cofre. |
| keyVaultURL | URL da chave Olá cofre que Olá BitLocker chave deve ser carregada. Você pode obtê-lo usando o cmdlet Olá `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`. |
| keyEncryptionKeyURL | URL da chave de criptografia de chave de saudação que é usado tooencrypt hello gerada chave do BitLocker (opcional). |
| keyVaultResourceGroup | Grupo de recursos do Cofre de chaves hello. |
| vmName | Nome da saudação VM Olá a operação de criptografia é toobe executada em. |

> [!NOTE]
> _KeyEncryptionKeyURL_ é um parâmetro opcional. Você pode colocar sua própria chave de dados criptografia do KEK toofurther proteção hello (senha secreta) em seu Cofre de chaves.

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a>Habilite a criptografia na nova VM IaaS criada usando VHD criptografado pelo cliente e chaves de criptografia
Nesse cenário, você pode habilitar a criptografia usando o modelo do Gerenciador de recursos de hello, cmdlets do PowerShell ou CLI comandos. Olá seções a seguir explicam em modelo de Gerenciador de recursos do maior detalhe hello e comandos CLI.

Siga as instruções de saudação de uma dessas seções para preparar imagens previamente criptografadas que podem ser usadas no Azure. Após a criação de imagem Olá, você pode usar etapas Olá Olá toocreate próximo da seção uma VM do Azure criptografados.

* [Preparar um VHD do Windows previamente criptografado](#preparing-a-pre-encrypted-windows-vhd)
* [Preparar um VHD Linux previamente criptografado](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-hello-resource-manager-template"></a>Usando o modelo do Gerenciador de recursos de saudação
Você pode habilitar a criptografia de disco em seu VHD criptografado usando Olá [modelo do Gerenciador de recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).

1. No modelo de saudação de início rápido do Azure, clique em **implantar tooAzure**, insira a configuração de criptografia de saudação em Olá **parâmetros** folha e depois clique em **Okey**.

2. Selecione a assinatura hello, grupo de recursos, local do grupo de recursos, os termos legais e contrato e, em seguida, clique em **criar** tooenable criptografia em Olá nova VM IaaS.

Olá tabela a seguir lista parâmetros de modelo do Gerenciador de recursos de saudação para seu VHD criptografado:

| Parâmetro | Descrição |
| --- | --- |
| newStorageAccountName | Nome do Olá Olá de toostore de conta de armazenamento criptografado VHD do sistema operacional. Esta conta de armazenamento deve já ter sido criada no hello mesmo grupo de recursos e no mesmo local que Olá VM. |
| osVhdUri | URI da saudação VHD do sistema operacional da conta de armazenamento hello. |
| osType | Tipo de produto do sistema operacional (Windows/Linux). |
| virtualNetworkName | Nome de rede virtual que Olá NIC de VM do hello deve pertencer ao. Olá nome deve já ter sido criado no hello mesmo grupo de recursos e no mesmo local que Olá VM. |
| subnetName | Nome da sub-rede Olá Olá VNet que Olá NIC de VM deve pertencer ao. |
| vmSize | Tamanho da VM de saudação. Atualmente, há suporte somente para séries Standard A, D e G. |
| keyVaultResourceID | Olá ResourceID que identifica o recurso de Cofre de chaves Olá no Gerenciador de recursos do Azure. Você pode obtê-lo usando o cmdlet do PowerShell Olá `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`. |
| keyVaultSecretUrl | URL da chave de criptografia de disco Olá configurado no cofre de chaves hello. |
| keyVaultKekUrl | URL Olá chave da chave de criptografia para criptografar a chave de criptografia de disco Olá gerado. |
| vmName | Nome da saudação IaaS VM. |

#### <a name="using-powershell-cmdlets"></a>Usando os cmdlets do PowerShell
Você pode habilitar a criptografia de disco em seu VHD criptografado usando o cmdlet do PowerShell Olá [ `Set-AzureRmVMOSDisk` ](/powershell/module/azurerm.compute/set-azurermvmosdisk).  

#### <a name="using-cli-commands"></a>Usando comandos da CLI
criptografia de disco tooenable para este cenário, usando os comandos CLI, Olá a seguir:

1. Definir políticas de acesso no cofre de chaves:

   * Saudação de conjunto **EnabledForDiskEncryption** sinalizador:

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * Conjunto de permissões tooAzure AD aplicativo toowrite segredos tooyour Cofre de chaves:

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. criptografia tooenable em uma VM existente ou em execução, tipo:

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. Obtenha o status de criptografia:

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. criptografia de tooenable em uma nova VM em seu VHD criptografado, Olá use parâmetros com hello a seguir `azure vm create` comando:

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a>Habilitar a criptografia na VM IaaS do Windows existente ou em execução no Azure
Nesse cenário, você pode habilitar a criptografia usando o modelo do Gerenciador de recursos de hello, cmdlets do PowerShell ou CLI comandos. Olá seções a seguir explicam mais detalhadamente como tooenable usando Olá modelo do Gerenciador de recursos e comandos CLI.

#### <a name="using-hello-resource-manager-template"></a>Usando o modelo do Gerenciador de recursos de saudação
Você pode habilitar a criptografia de disco existente ou VMs de IaaS do Windows em execução no Azure usando Olá [modelo do Gerenciador de recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).

1. No modelo de saudação de início rápido do Azure, clique em **implantar tooAzure**, insira a configuração de criptografia de saudação em Olá **parâmetros** folha e depois clique em **Okey**.

2. Selecione a assinatura hello, grupo de recursos, local do grupo de recursos, os termos legais e contrato e, em seguida, clique em **criar** tooenable criptografia Olá existente ou executando o IaaS VM.

Hello tabela a seguir lista os parâmetros de modelo do Gerenciador de recursos Olá para existente ou a execução de máquinas virtuais que usam uma ID de cliente do AD do Azure:

| Parâmetro | Descrição |
| --- | --- |
| AADClientID | ID do cliente do aplicativo de saudação do AD do Azure que tenha permissões toowrite segredos toohello chave de cofre. |
| AADClientSecret | Segredo do cliente do aplicativo de saudação do AD do Azure que tenha permissões toowrite segredos toohello chave de cofre. |
| keyVaultName | Nome da chave de saudação cofre que Olá BitLocker chave deve ser carregada. Você pode obtê-lo usando o cmdlet Olá `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`. |
|  keyEncryptionKeyURL | URL da chave de criptografia de chave de saudação que é usado tooencrypt hello gerada chave do BitLocker. Esse parâmetro é opcional se você selecionar **nokek** na lista de saudação UseExistingKek lista suspensa. Se você selecionar **kek** na lista de saudação UseExistingKek lista suspensa, você deve inserir Olá _keyEncryptionKeyURL_ valor. |
| volumeType | Tipo de volume Olá criptografia operação é executada. Os valores válidos são _OS_, _Data_ e _All_. |
| sequenceVersion | Versão da sequência de saudação operação do BitLocker. Aumentar esse número de versão toda vez que uma operação de criptografia de disco é executada em Olá mesma VM. |
| vmName | Nome da saudação VM Olá a operação de criptografia é toobe executada em. |

> [!NOTE]
> _KeyEncryptionKeyURL_ é um parâmetro opcional. Você pode trazer sua própria chave de dados criptografia do KEK toofurther proteção hello (secreta de criptografia do BitLocker) no cofre de chaves hello.

#### <a name="using-powershell-cmdlets"></a>Usando os cmdlets do PowerShell
Para obter informações sobre como habilitar a criptografia com criptografia de disco do Azure usando cmdlets do PowerShell, consulte as postagens de blog de saudação [explorar criptografia de disco do Azure com o Azure PowerShell - parte 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) e [explorar criptografia de disco do Azure com o Azure PowerShell - parte 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).

#### <a name="using-cli-commands"></a>Usando comandos da CLI
criptografia tooenable existente ou executando o IaaS VM do Windows no Azure usando comandos CLI, Olá a seguir:

1. políticas de acesso tooset no cofre de chaves hello:
   * Saudação de conjunto **EnabledForDiskEncryption** sinalizador:

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * Conjunto de permissões tooAzure AD aplicativo toowrite segredos tooyour Cofre de chaves:

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. criptografia tooenable em uma VM existente ou em execução:

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. status da criptografia tooget:

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. criptografia de tooenable em uma nova VM em seu VHD criptografado, Olá use parâmetros com hello a seguir `azure vm create` comando:

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a>Habilitar a criptografia em uma VM IaaS do Linux existente ou em execução no Azure
Você pode habilitar a criptografia de disco em uma VM do Linux de IaaS existentes ou em execução no Azure usando Olá [modelo do Gerenciador de recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).

1. Clique em **implantar tooAzure** no modelo Olá início rápido do Azure, insira configuração de criptografia Olá nas Olá **parâmetros** folha e depois clique em **Okey**.

2. Selecione a assinatura hello, grupo de recursos, local do grupo de recursos, os termos legais e contrato e, em seguida, clique em **criar** tooenable criptografia Olá existente ou executando o IaaS VM.

Olá, a tabela a seguir lista os parâmetros de modelo do Gerenciador de recursos para existente ou a execução de máquinas virtuais que usam uma ID de cliente do AD do Azure:

| Parâmetro | Descrição |
| --- | --- |
| AADClientID | ID do cliente do aplicativo de saudação do AD do Azure que tenha permissões toowrite segredos toohello chave de cofre. |
| AADClientSecret | Segredo do cliente do aplicativo de saudação do AD do Azure que tenha permissões toowrite segredos tooyour chave de cofre. |
| keyVaultName | Nome da chave de saudação cofre que Olá BitLocker chave deve ser carregada. Você pode obtê-lo usando o cmdlet Olá `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`. |
|  keyEncryptionKeyURL | URL da chave de criptografia de chave de saudação que é usado tooencrypt hello gerada chave do BitLocker. Esse parâmetro é opcional se você selecionar **nokek** na lista de saudação UseExistingKek lista suspensa. Se você selecionar **kek** na lista de saudação UseExistingKek lista suspensa, você deve inserir Olá _keyEncryptionKeyURL_ valor. |
| volumeType | Tipo de volume Olá criptografia operação é executada. Os valores válidos com suporte são _OS_ ou _Todos_ (para RHEL 7.2, CentOS 7.2 e Ubuntu 16.04) e _Dados_ (para todas as outras distribuições). |
| sequenceVersion | Versão da sequência de saudação operação do BitLocker. Aumentar esse número de versão toda vez que uma operação de criptografia de disco é executada em Olá mesma VM. |
| vmName | Nome da saudação VM Olá a operação de criptografia é toobe executada em. |
| Senha | Digite uma senha forte como chave de criptografia de dados de saudação. |

> [!NOTE]
> _KeyEncryptionKeyURL_ é um parâmetro opcional. Você pode colocar sua própria chave de dados criptografia do KEK toofurther proteção hello (senha secreta) em seu Cofre de chaves.

#### <a name="cli-commands"></a>Comandos de CLI
Você pode habilitar a criptografia de disco em seu VHD criptografado instalando e usando Olá [comando CLI](../cli-install-nodejs.md). criptografia tooenable existente ou IaaS Linux VMs em execução no Azure usando comandos CLI, Olá a seguir:

1. Definir políticas de acesso no cofre de chaves hello:

 * Saudação de conjunto **EnabledForDiskEncryption** sinalizador:

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * Conjunto de permissões tooAzure AD aplicativo toowrite segredos tooyour Cofre de chaves:

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. criptografia tooenable em uma VM existente ou em execução:

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. Obtenha o status de criptografia:

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. criptografia de tooenable em uma nova VM em seu VHD criptografado, Olá use parâmetros com hello a seguir `azure vm create` comando:
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-hello-encryption-status-of-an-encrypted-iaas-vm"></a>Obter status de criptografia de saudação de uma VM IaaS criptografado
Você pode obter o status da criptografia hello usando o Gerenciador de recursos do Azure, [cmdlets do PowerShell](/powershell/azure/overview), ou comandos CLI. Olá seções a seguir explica como Olá toouse portal clássico do Azure e CLI comandos tooget Olá status de criptografia.

#### <a name="get-hello-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a>Obter status de criptografia de saudação de uma VM do Windows criptografado usando o Gerenciador de recursos do Azure
Você pode obter o status de criptografia de saudação do hello IaaS VM do Gerenciador de recursos do Azure fazendo Olá seguinte:

1. Entrar toohello [portal clássico do Azure](https://portal.azure.com/)e, em seguida, clique em **máquinas virtuais** no painel esquerdo de saudação toosee uma exibição resumida de máquinas virtuais de saudação em sua assinatura. Você pode filtrar a exibição de máquinas virtuais de hello, selecionando o nome da assinatura Olá no hello **assinatura** lista suspensa.

2. Na parte superior de saudação do hello **máquinas virtuais** , clique em **colunas**.

3. Em Olá **coluna escolha** folha, selecione **criptografia de disco**e, em seguida, clique em **atualização**. Você deve ver o estado de criptografia de Olá Olá criptografia de disco coluna mostrando _habilitado_ ou _não habilitada_ para cada VM, conforme mostrado na figura a seguir de saudação:

 ![Microsoft Antimalware no Azure](./media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-hello-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-hello-disk-encryption-powershell-cmdlet"></a>Obter status de criptografia de saudação de uma VM de IaaS (Windows/Linux) criptografado usando o cmdlet do PowerShell de criptografia de disco Olá
Você pode obter o status de criptografia de saudação do hello IaaS VM do cmdlet do PowerShell de criptografia de disco Olá `Get-AzureRmVMDiskEncryptionStatus`. configurações de criptografia tooget Olá para sua VM, digite seguinte hello:

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

Você pode inspecionar a saída de saudação do _AzureRmVMDiskEncryptionStatus Get_ para criptografia de chave URLs.

    C:\> $status = Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName
    e $VMName -ExtensionName $ExtensionName
    C:\> $status.OsVolumeEncryptionSettings

    DiskEncryptionKey                                                 KeyEncryptionKey                                               Enabled
    -----------------                                                 ----------------                                               -------
    Microsoft.Azure.Management.Compute.Models.KeyVaultSecretReference Microsoft.Azure.Management.Compute.Models.KeyVaultKeyReference    True


    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey.SecretUrl
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a
    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey

    SecretUrl                                                                                                               SourceVault
    ---------                                                                                                               -----------
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a Microsoft.Azure.Management....

Olá OSVolumeEncrypted e valores de configurações de DataVolumesEncrypted são definidos too_Encrypted_, que mostra que ambos os volumes são criptografados usando a criptografia de disco do Azure. Para obter informações sobre como habilitar a criptografia com criptografia de disco do Azure usando cmdlets do PowerShell, consulte as postagens de blog de saudação [explorar criptografia de disco do Azure com o Azure PowerShell - parte 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) e [explorar criptografia de disco do Azure com o Azure PowerShell - parte 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).

> [!NOTE]
> Em VMs do Linux, leva três minutos toofour para Olá `Get-AzureRmVMDiskEncryptionStatus` status de criptografia do cmdlet tooreport hello.

#### <a name="get-hello-encryption-status-of-hello-iaas-vm-from-hello-disk-encryption-cli-command"></a>Obter status de criptografia de saudação de Olá IaaS VM do comando CLI Olá criptografia de disco
Você pode obter o status de criptografia de saudação do hello IaaS VM usando o comando CLI de criptografia de disco Olá `azure vm show-disk-encryption-status`. configurações de criptografia tooget Olá para sua VM, insira sua sessão de CLI do Azure:

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a>Desabilitar a criptografia em VMs IaaS do Windows em execução
Você pode desabilitar a criptografia em um VM de IaaS Linux ou do Windows em execução por meio do modelo do Gerenciador de recursos de criptografia de disco do Azure hello ou cmdlets do PowerShell e especificar a configuração de descriptografia hello.

##### <a name="windows-vm"></a>VM Windows
etapa de desabilitar a criptografia Olá desabilita a criptografia de Olá SO, volume de dados hello ou ambos em Olá executando Windows IaaS VM. Você não pode desabilitar o volume do sistema operacional hello e deixe o volume de dados Olá criptografado. Quando Olá desabilitar criptografia etapa será executada, modelo de implantação clássico do Azure Olá atualiza o modelo de serviço VM Olá e Olá VM de IaaS do Windows está marcado como descriptografado. conteúdo de saudação do hello VM não é criptografado em repouso. descriptografia Olá não excluir o cofre e hello criptografia chave material de chave (chaves de criptografia do BitLocker para Windows e senha para Linux).

##### <a name="linux-vm"></a>VM Linux
etapa de desabilitar a criptografia Olá desabilita a criptografia do volume de dados Olá Olá executando Linux IaaS VM. Esta etapa só funciona se o disco do sistema operacional Olá não está criptografado.

> [!NOTE]
> A desabilitação da criptografia no disco do sistema operacional Olá não é permitida em VMs do Linux.

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a>Desabilitar a criptografia em uma VM IaaS existente ou em execução
Você pode desabilitar a criptografia de disco em executando as VMs de IaaS do Windows usando Olá [modelo do Gerenciador de recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).

1. No modelo de saudação de início rápido do Azure, clique em **implantar tooAzure**, insira a configuração de descriptografia de saudação em Olá **parâmetros** folha e depois clique em **Okey**.

2. Selecione a assinatura hello, grupo de recursos, local do grupo de recursos, os termos legais e contrato e, em seguida, clique em **criar** tooenable criptografia em uma nova VM IaaS.

Para VMs do Linux, você pode desabilitar a criptografia usando Olá [desabilitar a criptografia em uma VM do Linux em execução](https://aka.ms/decrypt-linuxvm) modelo.

Hello tabela a seguir lista os parâmetros de modelo do Gerenciador de recursos para desabilitar a criptografia em um IaaS VM em execução:

| Parâmetro | Descrição |
| --- | --- |
| vmName | Nome da saudação VM Olá a operação de criptografia é toobe executada em.
| volumeType | Tipo de volume em que uma operação de descriptografia é executada. Os valores válidos são _OS_, _Data_ e _All_. Você não pode desabilitar a criptografia em execução o volume de inicialização/sistema operacional Windows IaaS VM sem a desabilitação da criptografia no hello _dados_ volume. Observe também que a desabilitação da criptografia no disco do sistema operacional Olá não é permitida em VMs do Linux. |
| sequenceVersion | Versão da sequência de saudação operação do BitLocker. Aumentar esse número de versão toda vez que uma operação de descriptografia de disco é executada em Olá mesma VM. |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a>Desabilitar a criptografia em uma VM IaaS existente ou em execução
criptografia toodisable em uma VM IaaS existente ou em execução usando o cmdlet do PowerShell hello, consulte [ `Disable-AzureRmVMDiskEncryption` ](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption). Esse cmdlet dá suporte a VMs do Linux e do Windows. criptografia toodisable, ele instala uma extensão na máquina virtual de saudação. Se hello _nome_ parâmetro não for especificado, uma extensão com o nome padrão Olá _AzureDiskEncryption para VMs do Windows_ é criado.

Em VMs do Linux, Olá AzureDiskEncryptionForLinux extensão é usado.

> [!NOTE]
> Esse cmdlet reinicia a máquina virtual de saudação.

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a>Habilitar criptografia na VM da IaaS criptografada previamente com o Azure Managed Disk
Use Olá BRAÇO do disco do Azure gerenciados modelo toocreate uma VM criptografada em um VHD previamente criptografado usando o modelo do ARM Olá localizada em   
[Criar um novo disco gerenciado criptografado a partir de um blob de armazenamento/VHD criptografado] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a>Habilitar criptografia em uma nova VM de IaaS Linux com o Azure Managed Disk
Use Olá BRAÇO do disco do Azure gerenciados modelo toocreate criptografado uma nova VM de IaaS Linux usando o modelo do ARM Olá localizado em   
[Implantação do RHEL 7.2 com criptografia de disco completo] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a>Habilitar criptografia em uma nova VM de IaaS do Windows com o Azure Managed Disk
 Use Olá BRAÇO do disco do Azure gerenciados modelo toocreate criptografado uma nova VM de IaaS Linux usando o modelo do ARM Olá localizado em   
 [Criar uma nova VM do Disco Gerenciado de IaaS do Windows a partir da imagem da galeria] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)

  > [!NOTE]
  >É obrigatório toosnapshot e/ou backup um disco gerenciado com base instância VM fora do e tooenabling anterior a criptografia de disco do Azure.  Um instantâneo do disco gerenciado Olá pode ser executado no portal de saudação ou Backup do Azure pode ser usado.  Backups Certifique-se de que uma opção de recuperação é possível no caso de saudação de qualquer falha inesperada durante a criptografia.  Depois que um backup é realizado, Olá conjunto AzureRmVMDiskEncryptionExtension cmdlet pode ser usado tooencrypt gerenciado discos especificando o parâmetro - skipVmBackup de hello.  Este comando falhará em VMs baseadas em disco gerenciado até que um backup tenha sido feito e esse parâmetro tenha sido especificado.    
 
### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a>Atualizar configurações de criptografia de uma VM de armazenamento não premium criptografada existente
  Use Olá disco Azure criptografia tem suportada interfaces existentes para executar a VM [cmdlets do PS, modelos CLI ou ARM] tooupdate configurações de criptografia de saudação que o cliente AAD ID/segredo, chave de criptografia [KEK], chave de criptografia do BitLocker para a máquina virtual do Windows ou a senha para Configuração de criptografia de atualização de Olá etc. de VM do Linux tem suporte apenas para VMs com o apoio de armazenamento não premium. Não oferece suporte para VMs com suporte de armazenamento premium.

## <a name="appendix"></a>Apêndice
### <a name="connect-tooyour-subscription"></a>Conecte-se a assinatura de tooyour
Antes de prosseguir, verifique Olá *pré-requisitos* seção neste artigo. Depois de garantir que todos os pré-requisitos foram atendidos, conecte-se tooyour assinatura fazendo Olá seguinte:

1. Iniciar uma sessão do PowerShell do Azure e entrar tooyour conta do Azure com hello comando a seguir:

    `Login-AzureRmAccount`

2. Se você tiver várias assinaturas e deseja um toouse toospecify, digite Olá assinaturas de saudação toosee para sua conta a seguir:

    `Get-AzureRmSubscription`

3. assinatura de saudação toospecify deseja toouse, tipo:

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. tooverify que a assinatura de saudação configurada está correta, digite:

    `Get-AzureRmSubscription`

5. Olá tooconfirm criptografia de disco de Azure cmdlets são instalados, tipo:

    `Get-command *diskencryption*`

6. Olá saída a seguir confirma a instalação do PowerShell de criptografia de disco do Azure hello:

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a>Preparar um VHD do Windows previamente criptografado
seções Olá a seguir são necessária tooprepare um VHD do Windows previamente criptografado para implantação como um VHD criptografado no IaaS do Azure. Use Olá informações tooprepare e inicializar uma nova VM (VHD do Windows) no Azure Site Recovery ou no Azure.

#### <a name="update-group-policy-tooallow-non-tpm-for-os-protection"></a>Atualizar grupo política tooallow não-TPM para a proteção do sistema operacional
Configurar a política de grupo do BitLocker Olá **a criptografia de unidade de disco BitLocker**, que você encontrará em **política de computador Local** > **deconfiguraçãodocomputador**  >  **Modelos administrativos** > **componentes do Windows**. Alterar essa configuração muito**unidades do sistema operacional** > **exigir autenticação adicional na inicialização** > **Permitir BitLocker sem um TPM compatível**, conforme mostrado na figura a seguir de saudação:

![Microsoft Antimalware no Azure](./media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a>Instalar componentes de recursos do BitLocker
Para o Windows Server 2012 e posterior, use Olá comando a seguir:

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

Para Windows Server 2008 R2, use Olá comando a seguir:

    ServerManagerCmd -install BitLockers

#### <a name="prepare-hello-os-volume-for-bitlocker-by-using-bdehdcfg"></a>Preparar o volume do sistema operacional de saudação do BitLocker usando`bdehdcfg`
toocompress Olá partição do sistema operacional e preparar o computador de saudação do BitLocker, executar Olá comando a seguir:

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-hello-os-volume-by-using-bitlocker"></a>Proteger o volume do sistema operacional hello usando o BitLocker
Saudação de uso [ `manage-bde` ](https://technet.microsoft.com/library/ff829849.aspx) criptografia do comando tooenable no volume de inicialização hello usando um protetor de chave externo. Também coloca chave de externo de saudação (arquivo .bek) na unidade externa hello ou volume. Criptografia está habilitada no volume de inicialização do sistema Olá após a próxima reinicialização do hello.

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> Prepare Olá VM com um data separado/recurso VHD para obtenção de chave externa hello usando o BitLocker.

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a>Criptografando uma unidade do sistema operacional em uma VM do Linux em execução
Criptografia de unidade do sistema operacional em uma VM do Linux em execução é compatível com hello distribuições a seguir:

* RHEL 7.2
* CentOS 7.2
* Ubuntu 16.04

##### <a name="prerequisites-for-os-disk-encryption"></a>Pré-requisitos para a criptografia de disco do sistema operacional

* Olá VM deve ser criada da imagem do Marketplace Olá no Gerenciador de recursos do Azure.
* VM do Azure com, no mínimo, 4 GB de RAM (o tamanho recomendável é de 7 GB).
* (Para RHEL e CentOS) Desabilite o SELinux. toodisable SELinux, consulte "4.4.2. Desabilitar o SELinux"hello [guia do administrador e usuário SELinux](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) em Olá VM.
* Depois de desabilitar SELinux, reinicialize Olá VM pelo menos uma vez.

##### <a name="steps"></a>Etapas
1. Crie uma máquina virtual usando uma das distribuições de saudação especificadas anteriormente.

 Para o CentOS 7.2, há suporte para a criptografia de disco do sistema operacional por meio de uma imagem especial. toouse imagem, especifique "7.2n" como Olá SKU quando você cria Olá VM:
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. Configure as necessidades de acordo tooyour Olá VM. Se você for tooencrypt todas as unidades de saudação (sistema operacional + dados), unidades de dados Olá necessário toobe especificado e pode ser montado em /etc/fstab.

 > [!NOTE]
 > Use o UUID =... toospecify unidades de dados/etc/fstab em vez de especificar o nome de dispositivo de bloco hello (por exemplo, /dev/sdb1). Durante a criptografia, Olá ordem das alterações de unidades em Olá VM. Se sua VM se baseia em uma ordem específica de dispositivos de bloco, ele falhará toomount-las após a criptografia.

3. Saia de sessões SSH de saudação.

4. Olá tooencrypt OS, especifique volumeType como **todos os** ou **OS** quando você [habilitar a criptografia](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).

 > [!NOTE]
 > Todos os processos de espaço de usuário que não estão sendo executados como serviços `systemd` deverão ser encerrados com um `SIGKILL`. Reinicialize Olá VM. Ao habilitar a criptografia de disco do sistema operacional em uma VM em execução, planeje o tempo de inatividade da VM.

5. Periodicamente monitorar o progresso de saudação de criptografia usando instruções Olá Olá [próxima seção](#monitoring-os-encryption-progress).

6. Depois de Get-AzureRmVmDiskEncryptionStatus mostra "VMRestartPending", reinicie a VM entrando no tooit ou usando o portal de hello, PowerShell ou CLI.
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot hello VM
    ```
Antes de reinicializar, recomendamos que você salve [diagnósticos de inicialização](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) de saudação VM.

#### <a name="monitoring-os-encryption-progress"></a>Monitorando o progresso da criptografia do sistema operacional
Você pode monitorar o progresso de criptografia do sistema operacional de três maneiras:

* Saudação de uso `Get-AzureRmVmDiskEncryptionStatus` cmdlet e inspecione o campo de ProgressMessage hello:
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 Depois de saudação VM atinge "Criptografia iniciada em disco do SO", que leva cerca de 40 minutos too50 em um armazenamento Premium feito VM.

 Devido ao [problema 388](https://github.com/Azure/WALinuxAgent/issues/388) no WALinuxAgent, `OsVolumeEncrypted` e `DataVolumesEncrypted` são mostrados como `Unknown` em algumas distribuições. Com a versão 2.1.5 WALinuxAgent e posterior, esse problema é corrigido automaticamente. Se você vir `Unknown` na saída de hello, você pode verificar o status de criptografia de disco usando Olá Gerenciador de recursos do Azure.

 Vá muito[Gerenciador de recursos do Azure](https://resources.azure.com/)e, em seguida, expanda essa hierarquia no painel de seleção Olá esquerda:

 ~~~~
 |-- subscriptions
     |-- [Your subscription]
          |-- resourceGroups
               |-- [Your resource group]
                    |-- providers
                         |-- Microsoft.Compute
                              |-- virtualMachines
                                   |-- [Your virtual machine]
                                        |-- InstanceView
~~~~                

 No hello InstanceView, role para baixo de status da criptografia Olá toosee de suas unidades.

 ![Exibição de instância VM](./media/azure-security-disk-encryption/vm-instanceview.png)

* Examine o [diagnóstico de inicialização](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/). Mensagens de saudação extensão ADE devem ser prefixadas com `[AzureDiskEncryption]`.

* Entrar toohello VM por meio do SSH e obter o log de extensão de saudação do:

    /var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux

 É recomendável que você não entrar no toohello VM enquanto a criptografia de sistema operacional está em andamento. Copie os logs de saudação apenas quando hello outros dois métodos falharem.

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a>Preparar um VHD Linux previamente criptografado
##### <a name="ubuntu-16"></a>Ubuntu 16
Configure a criptografia durante a instalação de distribuição Olá Olá seguinte:

1. Selecione **configurar volumes criptografados** quando você particionar os discos de saudação.

 ![Instalação do Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. Crie uma unidade de inicialização separada que não deverá ser criptografada. Criptografe a unidade de inicialização.

 ![Instalação do Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. Forneça uma frase secreta. Isso é Olá que você carregue toohello Cofre de chaves.

 ![Instalação do Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. Conclua o particionamento.

 ![Instalação do Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. Ao inicializar Olá VM e será solicitado para uma frase secreta, use Olá senha fornecida na etapa 3.

 ![Instalação do Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. Preparar Olá VM para carregar no Azure usando [estas instruções](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/). Ainda não executado última etapa do hello (Olá desprovisionamento VM).

Configure criptografia toowork com o Azure fazendo Olá seguinte:

1. Crie um arquivo em /usr/local/sbin/azure_crypt_key.sh, com conteúdo Olá Olá script a seguir. Preste atenção toohello KeyFileName, porque ele é o nome do arquivo de senha Olá usado pelo Azure.

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint
    modprobe vfat >/dev/null 2>&1
    modprobe ntfs >/dev/null 2>&1
    sleep 2
    OPENED=0
    cd /sys/block
    for DEV in sd*; do

        echo "> Trying device: $DEV ..." >&2
        mount -t vfat -r /dev/${DEV}1 $MountPoint >/dev/null||
        mount -t ntfs -r /dev/${DEV}1 $MountPoint >/dev/null
        if [ -f $MountPoint/$KeyFileName ]; then
                cat $MountPoint/$KeyFileName
                umount $MountPoint 2>/dev/null
                OPENED=1
                break
        fi
        umount $MountPoint 2>/dev/null
    done

      if [ $OPENED -eq 0 ]; then
        echo "FAILED toofind suitable passphrase file ..." >&2
        echo -n "Try tooenter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. Altere Olá crypt configuração em */etc/crypttab*. O resultado deve ser assim:
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. Se você estiver editando *azure_crypt_key.sh* no Windows e você copiou tooLinux, execute `dos2unix /usr/local/sbin/azure_crypt_key.sh`.

4. Adicione permissões executável toohello script:
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. Edite */etc/initramfs-tools/modules* acrescentando linha:
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. Executar `update-initramfs -u -k all` tooupdate Olá initramfs toomake Olá `keyscript` entrem em vigor.

7. Agora você pode cancelar o provisionamento Olá VM.

 ![Instalação do Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. Continuar toohello próxima etapa e [carregar o VHD](#upload-encrypted-vhd-to-an-azure-storage-account) no Azure.

##### <a name="opensuse-132"></a>openSUSE 13.2
criptografia tooconfigure durante a instalação de distribuição hello, Olá a seguir:
1. Ao particionar discos hello, selecione **criptografar o grupo de volumes**e, em seguida, digite uma senha. Esta é Olá senha que você fará o upload tooyour Cofre de chaves.

 ![Instalação do openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. Saudação de inicialização VM usando sua senha.

 ![Instalação do openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. Preparar Olá VM para carregar tooAzure, seguindo as instruções de saudação do [preparar uma máquina virtual SLES ou openSUSE para o Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131). Ainda não executado última etapa do hello (Olá desprovisionamento VM).

tooconfigure toowork de criptografia com o Azure, Olá a seguir:
1. Editar saudação /etc/dracut.conf e, em seguida, adicione Olá seguinte linha:
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. Comente essas linhas final Olá Olá /usr/lib/dracut/modules.d/90crypt/module-setup.sh do arquivo:
 ```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
 ```

3. Acrescente Olá a seguinte linha no início de saudação do hello arquivo /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:
 ```
    DRACUT_SYSTEMD=0
 ```
E altere todas as ocorrências de:
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
para:
```
    if [ 1 ]; then
```
4. Editar /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh e acrescente muito "dispositivo de abrir LUKS #":

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```
5. Executar `/usr/sbin/dracut -f -v` tooupdate Olá initrd.

6. Agora você pode cancelar o provisionamento Olá VM e [carregar o VHD](#upload-encrypted-vhd-to-an-azure-storage-account) no Azure.

##### <a name="centos-7"></a>CentOS 7
criptografia tooconfigure durante a instalação de distribuição hello, Olá a seguir:
1. Selecione **Criptografar meus dados** ao particionar os discos.

 ![Instalação do CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. Verifique se a opção **Criptografar** está selecionada para a partição raiz.

 ![Instalação do CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. Forneça uma frase secreta. Isso é Olá que você fará o upload tooyour Cofre de chaves.

 ![Instalação do CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. Ao inicializar Olá VM e será solicitado para uma frase secreta, use Olá senha fornecida na etapa 3.

 ![Instalação do CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. Preparar Olá VM para carregar no Azure usando instruções "CentOS 7.0 +" hello [preparar uma máquina virtual com base em CentOS Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70). Ainda não executado última etapa do hello (Olá desprovisionamento VM).

6. Agora você pode cancelar o provisionamento Olá VM e [carregar o VHD](#upload-encrypted-vhd-to-an-azure-storage-account) no Azure.

tooconfigure toowork de criptografia com o Azure, Olá a seguir:

1. Editar saudação /etc/dracut.conf e, em seguida, adicione Olá seguinte linha:
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. Comente essas linhas final Olá Olá /usr/lib/dracut/modules.d/90crypt/module-setup.sh do arquivo:
```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
```

3. Acrescente Olá a seguinte linha no início de saudação do hello arquivo /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:
```
    DRACUT_SYSTEMD=0
```
E altere todas as ocorrências de:
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
para
```
    if [ 1 ]; then
```
4. Edite /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh e anexá-lo após hello "dispositivo de abrir LUKS #":
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```    
5. Executar hello "/ /sbin/Service/usr/dracut - f - v" tooupdate Olá initrd.

![Instalação do CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-tooan-azure-storage-account"></a>Carregar conta de armazenamento do Azure de tooan VHD criptografadas
Depois de DM Crypt ou a criptografia do BitLocker é habilitado, Olá local criptografado conta de armazenamento do VHD necessidades toobe carregado tooyour.

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-hello-disk-encryption-secret-for-hello-pre-encrypted-vm-tooyour-key-vault"></a>Carregar secreta de criptografia de disco Olá para Olá previamente criptografado VM tooyour Cofre de chaves
segredo de criptografia de disco Olá que você obteve anteriormente deve ser carregado como um segredo no cofre de chaves. Cofre de chaves Olá precisa de criptografia de disco toohave e permissões habilitadas para o cliente do AD do Azure.

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a>Segredo de criptografia de disco não criptografado com uma KEK
tooset o segredo de saudação em seu Cofre de chaves, use [AzureKeyVaultSecret conjunto](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret). Se você tiver uma máquina virtual do Windows, o arquivo de bek de saudação é codificado como uma cadeia de caracteres base64 e, em seguida, carregado tooyour Cofre de chaves usando Olá `Set-AzureKeyVaultSecret` cmdlet. Para o Linux, Olá senha é codificada como uma cadeia de caracteres base64 e carregados toohello Cofre de chaves. Além disso, certifique-se que Olá marcas a seguir são definidos quando você cria o segredo Olá no cofre de chaves hello.

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

Saudação de uso `$secretUrl` na próxima etapa Olá para [anexando disco Olá SO sem usar KEK](#without-using-a-kek).

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a>Segredo de criptografia de disco criptografado com uma KEK
Antes de carregar o cofre da chave secreta toohello hello, você pode opcionalmente criptografá-lo usando uma chave de criptografia de chave. Quebra automática de saudação do uso [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst criptografar segredo hello usando a chave de criptografia de chave de saudação. Olá, a saída dessa operação wrap é uma cadeia de URL codificada em base64, que, em seguida, você pode carregar como um segredo usando Olá [ `Set-AzureKeyVaultSecret` ](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    Add-AzureKeyVaultKey -VaultName $KeyVaultName -Name "keyencryptionkey" -Destination Software
    $KeyEncryptionKey = Get-AzureKeyVaultKey -VaultName $KeyVault.OriginalVault.Name -Name "keyencryptionkey"

    $apiversion = "2015-06-01"

    ##############################
    # Get Auth URI
    ##############################

    $uri = $KeyVault.VaultUri + "/keys"
    $headers = @{}

    $response = try { Invoke-RestMethod -Method GET -Uri $uri -Headers $headers } catch { $_.Exception.Response }

    $authHeader = $response.Headers["www-authenticate"]
    $authUri = [regex]::match($authHeader, 'authorization="(.*?)"').Groups[1].Value

    Write-Host "Got Auth URI successfully"

    ##############################
    # Get Auth Token
    ##############################

    $uri = $authUri + "/oauth2/token"
    $body = "grant_type=client_credentials"
    $body += "&client_id=" + $AadClientId
    $body += "&client_secret=" + [Uri]::EscapeDataString($AadClientSecret)
    $body += "&resource=" + [Uri]::EscapeDataString("https://vault.azure.net")
    $headers = @{}

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $access_token = $response.access_token

    Write-Host "Got Auth Token successfully"

    ##############################
    # Get KEK info
    ##############################

    $uri = $KeyEncryptionKey.Id + "?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token}

    $response = Invoke-RestMethod -Method GET -Uri $uri -Headers $headers

    $keyid = $response.key.kid

    Write-Host "Got KEK info successfully"

    ##############################
    # Encrypt passphrase using KEK
    ##############################

    $passphraseB64 = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($Passphrase))
    $uri = $keyid + "/encrypt?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"alg" = "RSA-OAEP"; "value" = $passphraseB64}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $wrappedSecret = $response.value

    Write-Host "Encrypted passphrase successfully"

    ##############################
    # Store secret
    ##############################

    $secretName = [guid]::NewGuid().ToString()
    $uri = $KeyVault.VaultUri + "/secrets/" + $secretName + "?api-version=" + $apiversion
    $secretAttributes = @{"enabled" = $true}
    $secretTags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"value" = $wrappedSecret; "attributes" = $secretAttributes; "tags" = $secretTags}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method PUT -Uri $uri -Headers $headers -Body $body

    Write-Host "Stored secret successfully"

    $secretUrl = $response.id

Use `$KeyEncryptionKey` e `$secretUrl` na próxima etapa Olá para [anexando disco Olá SO usando KEK](#using-a-kek).

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a>Especificar uma URL secreta ao anexar um disco do sistema operacional
#### <a name="without-using-a-kek"></a>Sem usar uma KEK
Enquanto você está anexando disco Olá sistema operacional, você precisa toopass `$secretUrl`. Olá URL foi gerado na seção de "secreta de criptografia de disco não criptografada com uma KEK" hello.

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a>Usando uma KEK
Quando você anexa um disco Olá SO, passar `$KeyEncryptionKey` e `$secretUrl`. Olá URL foi gerado na seção de "secreta de criptografia de disco não criptografada com uma KEK" hello.

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $CopiedTemplateBlobUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl `
            -KeyEncryptionKeyVaultId $KeyVault.ResourceId `
            -KeyEncryptionKeyURL $KeyEncryptionKey.Id

## <a name="download-this-guide"></a>Baixar este guia
Você pode baixar este guia do hello [Galeria do TechNet](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).

## <a name="for-more-information"></a>Para obter mais informações
[Explorar a Azure Disk Encryption com o Azure PowerShell - Parte 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0)  
[Explorar a Azure Disk Encryption com o Azure PowerShell - Parte 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)
