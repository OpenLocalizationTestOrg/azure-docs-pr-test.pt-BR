---
title: "Visão geral da criptografia aaaAzure | Microsoft Docs"
description: "Saiba mais sobre as várias opções de criptografia no Azure"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 08/18/2017
ms.author: barclayn
ms.openlocfilehash: ef9ab46de32b857e99e8fe628a61386b95cf197f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-overview"></a>Visão geral da criptografia do Azure

Este artigo fornece uma visão geral de como a criptografia é usada no Microsoft Azure. Ele aborda as áreas principais Olá de criptografia, incluindo criptografia em repouso, criptografia em trânsito e gerenciamento de chaves com cofre da chave. Cada seção inclui links para informações mais detalhadas.

## <a name="encryption-of-data-at-rest"></a>Criptografia de dados em repouso

Os dados em repouso incluem informações que residem no armazenamento persistente da mídia física, em qualquer formato digital. Isso inclui arquivos em mídia magnética ou óptica, dados arquivados e backups de dados. Microsoft Azure oferece uma variedade de toomeet de soluções de armazenamento de dados diferentes necessidades, incluindo o arquivo, blob, tabela de armazenamento e disco. A Microsoft também fornece criptografia tooprotect [banco de dados do SQL Azure](../sql-database/sql-database-technical-overview.md), [CosmosDB](../cosmos-db/introduction.md)e o Azure Data Lake.

Criptografia de dados em repouso está disponível para serviços em hello Azure Software-como um serviço (SaaS), plataforma como um-serviço (PaaS) e modelos de nuvem de infraestrutura-como-um-serviço (IaaS). Este documento resume e fornece recursos toohelp usar opções de criptografia do Azure.

Para obter mais discussão de como os dados em repouso são criptografados no Azure, consulte o documento hello [dados do Azure com criptografia em repouso](azure-security-encryption-atrest.md)

## <a name="azure-encryption-models"></a>Modelos de criptografia do Azure

O Azure dá suporte a vários modelos de criptografia, incluindo criptografia no servidor usando chaves gerenciadas pelo serviço, chaves gerenciadas pelo cliente no Azure Key Vault ou chaves gerenciadas pelo cliente no hardware controlado pelo cliente. Criptografia do lado do cliente permite que você toomanage e o repositório de chaves local ou em outro local seguro.

### <a name="client-side-encryption"></a>Criptografia do cliente

A criptografia no cliente é realizada fora do Azure. A criptografia no cliente inclui:

- Dados criptografados por um aplicativo que está em execução no Centro de dados do cliente hello ou por um aplicativo de serviço
- Dados já criptografados quando recebidos pelo Azure.

Com a criptografia do lado do cliente provedor de serviços de nuvem Olá não tem chaves de criptografia de toohello de acesso e não pode descriptografar esses dados. Manter o controle total das chaves de saudação.

### <a name="server-side-encryption"></a>Criptografia no servidor

três modelos de criptografia do servidor de saudação oferecem características diferentes de gerenciamento de chaves, que podem ser escolhidas por seus requisitos.

- **Chaves gerenciadas pelo serviço**: fornecem uma combinação de controle e conveniência com baixa sobrecarga

- **Chaves gerenciados pelo cliente** oferecem controle sobre chaves hello, incluindo Olá capacidade toobring suas próprias chaves (BYOK) ou toogenerate novos.

- **Chaves de serviço gerenciado no ccustomer controlledhardware** permite chaves toomanage em seu repositório de propriedade que está fora do controle da Microsoft. Isso é chamado de HYOK (hospede sua própria chave). No entanto, a configuração é complexa e a maioria dos serviços do Azure não dá suporte a esse modelo.

### <a name="azure-disk-encryption"></a>Azure Disk Encryption

Máquinas virtuais Windows e Linux podem ser protegidas usando [criptografia de disco do Azure](azure-security-disk-encryption.md), que usa Olá [Windows BitLocker](https://technet.microsoft.com/library/cc766295(v=ws.10).aspx) tecnologia e Linux [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) tooprotect discos do sistema operacional e discos de dados com a criptografia de volume completo.

As chaves de criptografia e os segredos são protegidos na sua assinatura do [Azure Key Vault](../key-vault/key-vault-whatis.md). Você pode fazer backup e restaurar criptografados VMs que são criptografados com a configuração de KEK hello usando o serviço de Backup do Azure hello.

### <a name="azure-storage-service-encryption"></a>Criptografia do serviço de Armazenamento do Microsoft Azure

Os dados em repouso no Armazenamento do Microsoft Azure (Blobs e Arquivos) podem ser criptografados em cenários do servidor e do cliente.

[Criptografia do serviço de armazenamento do Azure](../storage/storage-service-encryption.md) (SSE) automaticamente pode criptografar os dados antes que ele é armazenado e descriptografa automaticamente quando você recupera-lo, tornando Olá processar usuários completamente transparentes. Criptografia do serviço de armazenamento usa 256 bits [criptografia AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), que é uma saudação codificações em bloco mais segura disponíveis e lida com a criptografia, descriptografia e gerenciamento de chaves de forma transparente.

### <a name="client-side-encryption-of-azure-blobs"></a>Criptografia de blobs do Azure no cliente

A criptografia de blobs do Azure no cliente pode ser realizada de maneiras diferentes.

Você pode usar o hello biblioteca de cliente de armazenamento do Azure para dados de tooencrypt de pacote do NuGet do .NET na sua toouploading anteriores de aplicativos de cliente-tooAzure armazenamento.

toolearn mais sobre e download Olá biblioteca de cliente de armazenamento do Azure para o pacote do NuGet do .NET, consulte o documento hello [8.3.0 de armazenamento do Windows Azure](https://www.nuget.org/packages/WindowsAzure.Storage)

Quando você usar a criptografia do lado do cliente com o Cofre de chaves do Azure, seus dados são criptografados usando uma única simétrica conteúdo criptografia de chave (CEK) que é gerada pelo SDK do cliente de armazenamento do Azure hello. Olá CEK é criptografada usando uma chave de criptografia de chave (KEK), que pode ser uma chave simétrica ou um par de chaves assimétricas. Você pode gerenciá-la localmente ou armazená-la no Azure Key Vault. Olá os dados criptografados são, em seguida, carregar o serviço de armazenamento tooAzure.

toolearn mais sobre a criptografia de cliente com o Cofre de chaves do Azure e começar com tooinstructions como, consulte o documento hello [Tutorial: criptografar e descriptografar os blobs no armazenamento do Microsoft Azure usando o Cofre de chaves do Azure](../storage/storage-encrypt-decrypt-blobs-key-vault.md)

Por fim, você também pode usar o hello biblioteca de cliente de armazenamento do Azure para criptografia de cliente Java tooperform antes de carregar tooAzure armazenamento e toodecrypt Olá dados durante o download de toohello cliente. Essa biblioteca também dá suporte à integração ao [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) para gerenciamento de chaves da conta de armazenamento.

### <a name="encryption-of-data-at-rest-with-azure-sql-database"></a>Criptografia de dados em repouso com o banco de dados SQL do Azure

O [Banco de Dados SQL do Azure](../sql-database/sql-database-technical-overview.md)é um serviço de banco de dados relacional de uso geral no Microsoft Azure que dá suporte a estruturas como XML, JSON, espacial e dados relacionais. SQL Azure oferece suporte à criptografia do lado do servidor por meio do recurso de criptografia de dados transparente (TDE) hello e criptografia do lado do cliente por meio do recurso sempre criptografado do hello.

#### <a name="transparent-data-encryption"></a>Transparent Data Encryption

[Criptografia de dados transparente TDE](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-tde) é usado tooencrypt [do SQL Server](https://www.microsoft.com/sql-server/sql-server-2016), [banco de dados do SQL Azure](../sql-database/sql-database-technical-overview.md), e [Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) arquivos de dados em tempo real, usando uma chave de criptografia de banco de dados (DEK), que é armazenada no registro de inicialização do banco de dados Olá para disponibilidade durante a recuperação.

A TDE protege dados e arquivos de log usando os algoritmos de criptografia AES e 3DES. Criptografia de arquivo de banco de dados de saudação é executada no nível de página Olá; páginas de saudação em um banco de dados criptografado são criptografadas antes de serem gravadas toodisk e são descriptografadas quando lidas na memória. A TDE agora é habilitada por padrão em bancos de dados SQL do Azure recentemente criados.

#### <a name="always-encrypted"></a>Always Encrypted

Olá [sempre criptografado](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-database-engine) recurso no SQL Azure permite que você tooencrypt dados em aplicativos de cliente toostoring anterior no banco de dados do SQL Azure e permite a delegação de tooenable de toothird de administração de banco de dados local partes e manter a separação entre aqueles que possuem e pode exibir dados de saudação e aqueles que gerenciá-lo, mas não deve ter acesso tooit.

#### <a name="cellcolumn-level-encryption"></a>Criptografia no nível de célula/coluna

Banco de dados SQL do Azure permite que você tooapply coluna de tooa de criptografia simétrica de dados usando o Transact-SQL. Isso é chamado de [criptografia de nível de coluna ou de criptografia no nível da célula](https://docs.microsoft.com/sql/relational-databases/security/encryption/encrypt-a-column-of-data) (CLE), porque você pode usá-lo colunas específicas de tooencrypt ou até mesmo células de dados com diferentes chaves de criptografia. Isso proporciona recurso de criptografia mais granular que a TDE, que criptografa dados em páginas.

CLE tem funções internas que você pode usar dados tooencrypt usando chaves simétricas ou assimétricas, com a chave pública de saudação de um certificado ou com uma senha usando 3DES.

### <a name="cosmos-db-database-encryption"></a>Criptografia de banco de dados do Cosmos DB

O [Azure Cosmos DB](../cosmos-db/database-encryption-at-rest.md) é o banco de dados multimodelo globalmente distribuído da Microsoft. Dados de usuário armazenados no banco de dados do Cosmos no armazenamento não volátil (unidades de estado sólido) são criptografados por padrão. Não há nenhum tooturn controles-ativado ou desativado. A criptografia em repouso é implementada usando várias tecnologias de segurança, incluindo sistemas seguros de armazenamento de chaves, redes criptografadas e APIs criptográficas. As chaves de criptografia são gerenciadas pela Microsoft e alternadas por diretrizes internas da Microsoft.

### <a name="at-rest-encryption-in-azure-data-lake"></a>Criptografia em repouso no Azure Data Lake

[Azure Data Lake](../data-lake-store/data-lake-store-encryption.md) é um repositório de toda a empresa de cada tipo de dados coletados em uma definição formal de tooany anterior único local de requisitos ou esquema. Dá suporte ao repositório Azure Data Lake "em por padrão," criptografia transparente de dados em repouso, que é configurado durante a criação de saudação da sua conta. Por padrão, o repositório Data Lake gerencia chaves Olá para você, mas tem Olá opção toomanage-las por conta própria.

Três tipos de chaves são usados na criptografia e descriptografia de dados: Olá a chave de criptografia mestra (MEK), a chave de criptografia de dados (DEK) e a chave de criptografia de bloco (BEK). Olá MEK é usado tooencrypt Olá DEK, que é armazenada na mídia persistente, e Olá BEK é derivado do hello DEK e bloco de dados de saudação. Se você estiver gerenciando suas próprias chaves, você pode girar Olá MEK.

## <a name="encryption-of-data-in-transit"></a>Criptografia de dados em trânsito

O Azure oferece vários mecanismos para manter os dados privados conforme avança da tooanother de um local.

### <a name="tlsssl-encryption-in-azure"></a>Criptografia TLS/SSL no Azure

A Microsoft usa Olá [Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) protocol tooprotect dados quando ele está viajando entre clientes e serviços de nuvem hello. Data centers da Microsoft negociam uma conexão TLS com sistemas de cliente que se conectam tooAzure serviços. O TLS fornece autenticação forte, privacidade de mensagem e integridade (habilitando a detecção de violação, interceptação e falsificação de mensagens), interoperabilidade, flexibilidade de algoritmo, facilidade de implantação e uso.

O PFS ([Perfect Forward Secrecy](https://en.wikipedia.org/wiki/Forward_secrecy)) protege conexões entre sistemas cliente dos clientes e serviços em nuvem da Microsoft por chaves exclusivas. As conexões também usam comprimentos de chave de criptografia de 2.048 bits baseados em RSA. Essa combinação torna difícil para alguém toointercept e acessar dados que está em trânsito.

### <a name="azure-storage-transactions"></a>Transações do Armazenamento do Microsoft Azure

Quando você interage com o armazenamento do Azure por meio de saudação portal do Azure, todas as transações ocorrem em HTTPS. Você também pode usar o hello API REST do armazenamento em toointeract HTTPS com o armazenamento do Azure. Você pode impor o uso de saudação de HTTPS ao chamar objetos de tooaccess de APIs REST Olá nas contas de armazenamento, permitindo que a transferência segura necessária para a conta de armazenamento hello.

Assinaturas de acesso compartilhado ([SAS](../storage/storage-dotnet-shared-access-signature-part-1.md)), que pode ser usado toodelegate acessar objetos de armazenamento tooAzure, incluem uma opção toospecify que Olá somente pode ser usado o protocolo HTTPS ao usar assinaturas de acesso compartilhado. Isso garante que qualquer pessoa enviando links com tokens SAS usa o protocolo apropriado de saudação.

[SMB 3.0](https://technet.microsoft.com/library/dn551363(v=ws.11).aspx#BKMK_SMBEncryption) tooaccess usado compartilhamentos de arquivos do Azure oferece suporte à criptografia, e está disponível no Windows Server 2012 R2, Windows 8, Windows 8.1 e Windows 10, permitindo o acesso entre regiões e até mesmo acessar na área de trabalho de saudação.

Criptografia de cliente criptografa os dados de saudação antes que esta foi enviada tooAzure armazenamento, para que ele é criptografado como ele viaja pela rede de saudação.

### <a name="smb-encryption-over-azure-virtual-networks"></a>Criptografia SMB pelas Redes Virtuais do Azure 

[SMB 3.0](https://support.microsoft.com/help/2709568/new-smb-3-0-features-in-the-windows-server-2012-file-server) em VMs do Azure executando o Windows Server 2012 e superior oferece Olá dados toomake de capacidade transferências seguro, criptografando dados em trânsito em redes virtuais do Azure, ataques tooprotect contra violação e espionagem. Os administradores podem habilitar a criptografia SMB para todo o servidor hello, ou ações específicas.

Por padrão, depois que a criptografia SMB está ativada para um compartilhamento ou servidor, somente os clientes SMB 3 são permitidos tooaccess Olá criptografado compartilhamentos.

## <a name="in-transit-encryption-in-azure-virtual-machines"></a>Criptografia em trânsito nas Máquinas Virtuais do Azure

Dados em trânsito para, de e entre máquinas virtuais do Azure que executam o Windows são criptografados de várias maneiras, dependendo da natureza de saudação da conexão hello.

### <a name="rdp-sessions"></a>Sessões RDP

Você pode se conectar e fazer logon tooan VM do Azure usando Olá [Remote Desktop Protocol](https://msdn.microsoft.com/library/aa383015(v=vs.85).aspx) (RDP) a partir de um computador cliente com Windows ou um Mac com um cliente RDP instalado. Dados em trânsito pela rede Olá em sessões RDP podem ser protegidos por TLS.

Você também pode usar a área de trabalho remota tooconnect tooa VM do Linux no Azure.

### <a name="secure-access-toolinux-vms-with-ssh"></a>Proteger o acesso tooLinux VMs com SSH

Você pode usar [Secure Shell](../virtual-machines/linux/ssh-from-windows.md) (SSH) tooconnect tooLinux VMs em execução no Azure para gerenciamento remoto. O SSH é um protocolo de conexão criptografada que permite logons seguros por conexões não protegidas. É o protocolo de conexão padrão Olá para VMs do Linux hospedado no Azure. Usando as chaves de SSH para autenticação, você eliminar necessidade de saudação de senhas toolog em. O SSH usa um par de chaves pública/privada (criptografia assimétrica) para autenticação.

## <a name="azure-vpn-encryption"></a>Criptografia de VPN do Azure

Você pode conectar tooAzure por meio de uma rede virtual privada que cria de privacidade de saudação tooprotect encapsulamento seguro de dados de saudação que são enviados pela rede hello.

### <a name="azure-vpn-gateway"></a>Gateway de VPN do Azure

[Gateway VPN do Azure](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md) pode ser usado toosend criptografado tráfego entre sua rede virtual e sua localização no local em uma conexão pública ou toosend o tráfego entre redes virtuais.

A VPN site a site usa [IPsec](https://en.wikipedia.org/wiki/IPsec) para criptografia de transporte. Os gateways de VPN do Azure usam um conjunto de propostas padrão. Você pode configurar uma política personalizada do IPsec/IKE de toouse de gateways de VPN do Azure com algoritmos criptográficos específicos e restrições de chave, em vez de Olá conjuntos de política padrão do Azure.

### <a name="point-to-site-vpn"></a>VPN ponto a site

VPNs ponto a Site permitem que clientes individuais computadores acessar tooan rede Virtual do Azure. [Olá Secure Socket Tunneling Protocol](https://technet.microsoft.com/library/2007.06.cableguy.aspx) (SSTP) é o encapsulamento VPN Olá toocreate usado e pode atravessar firewalls (túnel Olá aparece como uma conexão HTTPS). Você pode usar sua própria AC raiz de PKI interna para conectividade ponto a site.

Você pode configurar uma ponto a site VPN conexão tooa rede virtual usando Olá portal do Azure com autenticação de certificado ou o PowerShell.

toolearn mais sobre tooAzure conexões de VPN ponto a site VNets, consulte: [configurar uma conexão de ponto para Site tooa VNet usando a autenticação de certificação: portal do Azure](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md) e

[Configurar uma conexão de ponto para Site tooa VNet usando a autenticação de certificado: PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

### <a name="site-to-site-vpn"></a>VPN site a site 

Uma conexão de gateway VPN Site a Site é usado tooconnect seu local de rede tooan rede virtual do Azure por um túnel VPN IPsec/IKE (IKEv1 ou IKEv2). Esse tipo de conexão exige um VPN de dispositivos localizado localmente que tenha uma tooit de endereço atribuído de IP público externamente.

Você pode configurar uma site a site VPN conexão tooa rede virtual usando Olá portal do Azure, o PowerShell ou hello Azure Interface de linha de comando (CLI).

Leia estes artigos para saber mais:

[Criar uma conexão Site a Site no portal do Azure de saudação](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

[Criar uma conexão site a site](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

[Criar uma rede virtual com uma conexão VPN site a site usando a CLI](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="in-transit-encryption-in-azure-data-lake"></a>Criptografia em trânsito no Azure Data Lake

Dados em trânsito (também conhecidos como dados em movimento) também são sempre criptografados no Data Lake Store. Além disso mídia toopersistent do tooencrypting dados toostoring anterior, Olá dados são sempre protegidos em trânsito usando HTTPS. HTTPS é Olá único protocolo com suporte para Olá que interfaces Data Lake repositório REST.

toolearn mais informações sobre criptografia de dados em trânsito no Azure Data Lake, consulte o documento hello [criptografia de dados no repositório Azure Data Lake.](../data-lake-store/data-lake-store-encryption.md)

## <a name="key-management-with-azure-key-vault"></a>Gerenciamento de chaves com o Azure Key Vault

Sem proteção adequada e gerenciamento de chaves hello, a criptografia será renderizada como inútil. Cofre de chaves do Azure é a solução recomendada da Microsoft para gerenciar e controlar as chaves de tooencryption acesso usadas pelos serviços de nuvem. Chaves de tooaccess permissões podem ser atribuídas tooservices ou toousers por meio de contas do Active Directory do Azure.

Cofre de chaves do Azure poupa organizações de saudação necessidade tooconfigure, patch e manter módulos de segurança de Hardware (HSM) e o software de gerenciamento de chaves. Com o Cofre de chaves do Azure, Microsoft nunca vê as chaves e aplicativos não têm acesso direto toothem; Manter o controle. Você também pode importar ou gerar chaves em HSMs.

## <a name="next-steps"></a>Próximas etapas

- [Visão geral de segurança do Azure](security-get-started-overview.md)
- [Visão geral da segurança de rede do Azure](security-network-overview.md)
- [Visão geral de segurança do banco de dados do Azure](azure-database-security-overview.md)
- [Visão geral de segurança de máquinas virtuais do Azure](security-virtual-machines-overview.md)
- [Criptografia de dados em repouso](azure-security-encryption-atrest.md)
- [Práticas recomendadas de segurança e criptografia de dados](azure-security-data-encryption-best-practices.md)
