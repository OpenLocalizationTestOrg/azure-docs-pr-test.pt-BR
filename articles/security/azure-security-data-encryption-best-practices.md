---
title: "aaaData segurança e práticas recomendadas de criptografia | Microsoft Docs"
description: "Este artigo fornece um conjunto de práticas recomendadas de segurança de dados e criptografia usando recursos internos do Azure."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 17ba67ad-e5cd-4a8f-b435-5218df753ca4
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/09/2017
ms.author: yurid
ms.openlocfilehash: 5057c85ed3107921462a40045e716675ea41e4bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-security-and-encryption-best-practices"></a>Práticas Recomendadas de Segurança de Dados e Criptografia do Azure
Uma proteção de toodata Olá chaves na nuvem Olá é responsável por possíveis estados Olá na qual os dados podem ocorrer e quais controles estão disponíveis para esse estado. Para fins de saudação de práticas recomendadas de segurança e criptografia de dados do Azure recomendações Olá será em torno de saudação estados dos dados a seguir:

* Em repouso: isso inclui todos os objetos de armazenamento, contêineres e tipos de informações que existem estaticamente em mídia física, seja ela magnética ou disco óptico.
* Em trânsito: Quando dados estão sendo transferidos entre componentes, locais ou programas, como rede hello, através de um barramento de serviço (de toocloud local e vice-versa, incluindo conexões híbridas como rota expressa), ou durante uma entrada/saída processo, ele é considerado como sendo em movimento.

Neste artigo, veremos uma coleção de práticas de recomendadas de segurança de dados e criptografia do Azure. Essas práticas recomendadas são derivadas da nossa experiência com segurança de dados do Azure e criptografia e hello experiências de clientes.

Para cada prática recomendada, vamos explicar:

* A prática recomendada que Olá é
* Por que você deseja tooenable essa prática recomendada
* O que pode ser resultado de saudação se você não a prática recomendada de saudação tooenable
* Prática recomendada de toohello possíveis alternativas
* Como você pode aprender a prática recomendada de saudação tooenable

Este artigo de práticas recomendadas de criptografia e de segurança de dados do Azure baseia-se em uma opinião consenso e recursos da plataforma Azure e conjuntos de recursos, que existem em tempo de saudação que este artigo foi escrito. Tecnologias e opiniões alterar ao longo do tempo e este artigo será atualizado em um tooreflect regularmente essas alterações.

As práticas recomendadas de segurança de dados e criptografia do Azure debatidas neste artigo incluem:

* Impor autenticação multifator
* Usar RBAC (controle de acesso baseado em função)
* Criptografar máquinas virtuais do Azure
* Usar modelos de segurança de hardware
* Gerenciar com Estações de Trabalho Protegidas
* Habilitar a criptografia de dados SQL
* Proteger dados em trânsito
* Impor criptografia de dados no nível do arquivo

## <a name="enforce-multi-factor-authentication"></a>Impor Autenticação Multifator
Olá primeira etapa no acesso a dados e o controle no Microsoft Azure são o usuário de saudação do tooauthenticate. A [Azure MFA (Autenticação Multifator)](../multi-factor-authentication/multi-factor-authentication.md) é um método de verificação da identidade do usuário que utiliza outro método além do nome de usuário e senha. Esse método de autenticação ajuda a proteger acesso toodata e aplicativos atendendo a demanda do usuário para um processo de logon simple.

Ativando o Azure MFA para os usuários, você está adicionando uma segunda camada de segurança toouser entradas e transações. Nesse caso, uma transação pode ser o acesso a um documento localizado em um servidor de arquivos ou no SharePoint Online. MFA do Azure também ajuda a probabilidade de saudação do IT tooreduce que uma credencial comprometida terá dados do access tooorganization.

Por exemplo: se você impor o MFA do Azure para seus usuários e configurá-lo toouse uma chamada telefônica ou mensagem de texto como uma verificação, se a credencial do usuário Olá estiver comprometido, o invasor Olá não ser capaz de tooaccess qualquer recurso porque ele não terá telefone do acesso toouser. As organizações que não adicionar essa camada extra de proteção de identidade são mais suscetíveis de ataque de roubo de credenciais, que pode causar o comprometimento de toodata.

Uma alternativa para organizações que desejam tookeep Olá autenticação controle local foi toouse [servidor Azure multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-server.md), também chamado de MFA no local. Usando esse método ainda será tooenforce capaz de autenticação de vários fatores, mantendo Olá MFA server local.

Para obter mais informações sobre o Azure MFA, leia o artigo Olá [guia de Introdução ao Azure multi-Factor Authentication na nuvem Olá](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).

## <a name="use-role-based-access-control-rbac"></a>Usar RBAC (Controle de Acesso Baseado em Função)
Restringir o acesso com base em Olá [necessário tooknow](https://en.wikipedia.org/wiki/Need_to_know) e [privilégio mínimo](https://en.wikipedia.org/wiki/Principle_of_least_privilege) princípios de segurança. Isso é essencial para as organizações que desejam tooenforce políticas de segurança para acesso a dados. Controle de acesso do Azure baseado em função (RBAC) pode ser usado tooassign permissões toousers, grupos e aplicativos em um determinado escopo. escopo de saudação de uma atribuição de função pode ser uma assinatura, um grupo de recursos ou um único recurso.

Você pode aproveitar [funções internas de RBAC](../active-directory/role-based-access-built-in-roles.md) no Azure tooassign privilégios toousers. Considere o uso de *colaborador da conta de armazenamento* para operadores de nuvem que precisam de contas de armazenamento toomanage e *Colaborador clássico de conta de armazenamento* contas de armazenamento clássicas toomanage de função. Operadores de nuvem que precisa toomanage VMs e conta de armazenamento, considere a possibilidade de adicioná-los muito*colaborador da máquina Virtual* função.

As organizações que não impõem o controle de acesso de dados utilizando recursos como o RBAC podem estar dando mais privilégios do que o necessário para seus usuários. Isso pode levar comprometimento toodata fazendo com que alguns usuários que têm toodata de acesso que eles não deveriam ter em primeiro lugar de saudação.

Você pode aprender mais sobre o RBAC do Azure ao ler o artigo Olá [o controle de acesso](../active-directory/role-based-access-control-configure.md).

## <a name="encrypt-azure-virtual-machines"></a>Criptografar Máquinas Virtuais do Azure
Para muitas organizações, a [criptografia de dados em repouso](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) é uma etapa obrigatória no sentido de garantir a soberania, a privacidade e a conformidade dos dados. Criptografia de disco do Azure permite que os administradores IT tooencrypt Windows e discos de Linux IaaS VM (Máquina Virtual). Criptografia de disco do Azure utiliza Olá setor padrão BitLocker recursos do Windows e Olá DM Crypt Linux tooprovide da criptografia do volume para Olá SO e discos de dados de saudação.

Você pode aproveitar a criptografia de disco do Azure toohelp proteger e proteger seu dados toomeet seus requisitos de segurança e conformidade organizacionais. As organizações também devem considerar o uso criptografia toohelp reduzir riscos relacionados toounauthorized acesso a dados. Também é recomendável que você criptografe unidades toowriting anterior dados confidenciais toothem.

Verifique se tooencrypt volumes de dados da VM e o volume de inicialização dados de pedidos tooprotect em repouso em sua conta de armazenamento do Azure. Proteger segredos e chaves de criptografia Olá aproveitando [Azure Key Vault](../key-vault/key-vault-whatis.md).

Para servidores Windows local, considere Olá seguir as práticas recomendadas de criptografia:

* Usar [BitLocker](https://technet.microsoft.com/library/dn306081.aspx) para criptografia de dados
* Armazene informações de recuperação no AD DS.
* Se houver qualquer problema que as chaves de BitLocker foi comprometidas, é recomendável formatar ou Olá unidade tooremove todas as instâncias de metadados de BitLocker Olá de unidade de saudação ou descriptografar e criptografar a unidade inteira Olá novamente.

As organizações que não impõem criptografia de dados são mais provável toodata de toobe exposto problemas de integridade, como usuários mal-intencionados ou invasores roubo de dados e comprometido contas que tenham acesso não autorizado toodata em formato criptografado. Além desses riscos, as empresas que têm toocomply com regulamentos do setor, deve provar que são cuidadoso e estiver usando a segurança de dados do hello segurança correto controles tooenhance.

Você pode aprender mais sobre a criptografia de disco do Azure ao ler o artigo Olá [Azure criptografia de disco do Windows e VMs de IaaS Linux](azure-security-disk-encryption.md).

## <a name="use-hardware-security-modules"></a>Usar Módulos de Segurança de Hardware
Soluções de criptografia do setor usam dados de tooencrypt chaves secretas. Portanto, é importante que essas chaves sejam armazenadas com segurança. Gerenciamento de chaves se torna parte integrante da proteção de dados, desde que ela será utilizado toostore chaves secretas que são usadas tooencrypt dados.

Criptografia de disco do Azure usa [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) toohelp controlar e gerenciar chaves de criptografia de disco e segredos em sua assinatura do Cofre de chaves, garantindo que todos os dados em discos da máquina virtual Olá sejam criptografados em repouso do Azure armazenamento. Você deve usar as chaves do Azure Key Vault tooaudit e uso de política.

Há muitos toonot relacionados riscos inerentes com controles de segurança apropriadas no local tooprotect Olá chaves secretas que foram usado tooencrypt seus dados. Se os invasores têm acesso toohello as chaves secretas, eles serão ser capaz de toodecrypt Olá dados e potencialmente têm acesso tooconfidential informações.

Você pode aprender mais sobre as recomendações gerais para o gerenciamento de certificados no Azure lendo o artigo Olá [gerenciamento de certificado no Azure: regras](https://blogs.msdn.microsoft.com/azuresecurity/2015/07/13/certificate-management-in-azure-dos-and-donts/).

Para saber mais sobre o Cofre de Chaves do Azure, leia [Introdução ao Cofre de Chaves do Azure](../key-vault/key-vault-get-started.md).

## <a name="manage-with-secure-workstations"></a>Gerenciar com Estações de Trabalho Protegidas
Desde a grande maioria de usuário final do hello ataques destino Olá Olá, o ponto de extremidade de saudação se torna um dos principais pontos Olá de ataque. Se um invasor comprometer o ponto de extremidade hello, ele pode aproveitar os dados do tooorganization do acesso toogain as credenciais do usuário hello. A maioria dos ataques de ponto de extremidade são tootake capaz de aproveitar fatos Olá que os usuários finais são administradores em suas estações de trabalho locais.

Você pode reduzir esses riscos usando uma estação de trabalho de gerenciamento segura. Recomendamos que você use um [estações de trabalho de acesso privilegiado (PATA)](https://technet.microsoft.com/library/mt634654.aspx) tooreduce superfície de ataque de saudação em estações de trabalho. Essas estações de trabalho de gerenciamento seguras podem ajudar a atenuar alguns desses ataques e a garantir que seus dados ficarão mais seguros. Verifique se toouse PAW tooharden e bloqueio para baixo de sua estação de trabalho. Essa é uma garantia de segurança alta tooprovide etapa importante para contas confidenciais, tarefas e proteção de dados.

Falta de proteção de ponto de extremidade pode colocar seus dados em risco, verifique se tooenforce políticas de segurança em todos os dispositivos que são dados tooconsume usado, independentemente do local de dados da saudação (nuvem ou local).

Você pode aprender mais sobre privilégios de acesso estação de trabalho ao ler o artigo Olá [proteção de acesso privilegiado](https://technet.microsoft.com/library/mt631194.aspx).

## <a name="enable-sql-data-encryption"></a>Habilitar a criptografia de dados SQL
[Criptografia de dados transparente de banco de dados SQL do Azure](https://msdn.microsoft.com/library/dn948096.aspx) (TDE) ajuda a proteger contra a ameaça de saudação de atividades mal-intencionadas executando criptografia em tempo real e a descriptografia do banco de dados de hello, backups associados, e arquivos de log de transações em repouso sem necessidade de alterações toohello aplicativo.  Ela criptografa o armazenamento de saudação de um banco de dados inteiro usando uma chave de criptografia de banco de dados de saudação de chamada de chave simétrica.

Mesmo quando o armazenamento inteiro Olá é criptografado, é muito importante tooalso criptografar seu próprio banco de dados. Esta é uma implementação de defesa Olá abordagem em camadas para a proteção de dados. Se você estiver usando [banco de dados do SQL Azure](https://msdn.microsoft.com/library/0bf7e8ff-1416-4923-9c4c-49341e208c62.aspx) e desejar tooprotect os dados confidenciais, como o cartão de crédito ou números de previdência social, você pode criptografar bancos de dados com o FIPS 140-2 criptografia de AES de 256 bits validado que atende aos requisitos de saudação de muitos padrões do setor (por exemplo, HIPAA, PCI).

É importante toounderstand que arquivos relacionados muito[extensão do pool de buffers](https://msdn.microsoft.com/library/dn133176.aspx) (BPE) não são criptografados quando um banco de dados é criptografado usando TDE. Você deve usar ferramentas de criptografia no nível do sistema de arquivos como BitLocker ou Olá [Encrypting File System](https://technet.microsoft.com/library/cc700811.aspx) (EFS) para BPE arquivos relacionados.

Desde que um usuário autorizado, como um administrador de segurança ou um administrador de banco de dados pode acessar dados hello, mesmo se o banco de dados de saudação é criptografado com TDE, você também deve seguir as recomendações de saudação abaixo:

* Autenticação no nível de banco de dados de saudação do SQL
* Autenticação do Azure AD usando funções RBAC
* Os usuários e aplicativos devem usar tooauthenticate contas separadas. Dessa forma, você pode limitar as permissões de saudação concedidas toousers e aplicativos e reduzir os riscos de saudação de atividade mal-intencionada
* Implementar segurança em nível de banco de dados usando as funções de banco de dados fixa (como db_datareader ou db_datawriter), ou você pode criar funções personalizadas para seu aplicativo toogrant objetos de banco de dados de tooselected permissões explícitas

As organizações que não estiverem usando criptografia no nível do banco de dados estarão mais suscetíveis a ataques que podem comprometer os dados localizados em bancos de dados SQL.

Você pode aprender mais sobre a criptografia SQL TDE lendo o artigo Olá [Transparent Data Encryption com o banco de dados do Azure SQL](https://msdn.microsoft.com/library/0bf7e8ff-1416-4923-9c4c-49341e208c62.aspx).

## <a name="protect-data-in-transit"></a>Proteger dados em trânsito
A proteção dos dados em trânsito deve ser parte essencial de sua estratégia de proteção de dados. Desde que os dados serão movendo alternadas em vários locais, a recomendação geral Olá é sempre usar dados de tooexchange protocolos SSL/TLS em diferentes locais. Em algumas circunstâncias, talvez seja o canal de comunicação inteira Olá tooisolate entre seu local e nuvem infraestrutura usando uma rede virtual privada (VPN).

Para dados que se movem entre sua infraestrutura local e o Azure, você deve considerar proteções adequadas, como HTTPS ou VPN.

Para organizações que precisam de acesso toosecure de vários tooAzure localizado no local de estações de trabalho, use [VPN site a site do Azure](../vpn-gateway/vpn-gateway-site-to-site-create.md).

Para organizações que precisam de acesso toosecure de uma estação de trabalho localizado no local tooAzure, use [ponto a Site VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md).

Conjuntos de dados maiores podem ser movidos em um link WAN de alta velocidade dedicado, como o [ExpressRoute](https://azure.microsoft.com/services/expressroute/). Se você escolher toouse rota expressa, você também pode criptografar dados Olá no nível do aplicativo, Olá usando [SSL/TLS](https://support.microsoft.com/kb/257591) ou outros protocolos para proteção adicional.

Se você estiver interagindo com o armazenamento do Azure por meio de saudação Portal do Azure, todas as transações ocorrem por meio de HTTPS. [API de REST do armazenamento](https://msdn.microsoft.com/library/azure/dd179355.aspx) via HTTPS também pode ser o toointeract usado com [armazenamento do Azure](https://azure.microsoft.com/services/storage/) e [banco de dados do SQL Azure](https://azure.microsoft.com/services/sql-database/).

As organizações que não tooprotect dados em trânsito são mais suscetíveis para [ataques man-in-the-middle](https://technet.microsoft.com/library/gg195821.aspx), [espionagem](https://technet.microsoft.com/library/gg195641.aspx) e sequestro de sessão. Esses ataques podem ser a primeira etapa Olá na obtenção de dados do access tooconfidential.

Você pode aprender mais sobre a opção de VPN do Azure lendo o artigo Olá [de planejamento e design para o Gateway de VPN](../vpn-gateway/vpn-gateway-plan-design.md).

## <a name="enforce-file-level-data-encryption"></a>Impor criptografia de dados no nível do arquivo
Outra camada de proteção que pode aumentar o nível de saudação de segurança para seus dados é criptografar arquivo hello, independentemente do local do arquivo hello.

[O Azure RMS](https://technet.microsoft.com/library/jj585026.aspx) toohelp de políticas de criptografia, identidade e autorização usa proteger seus arquivos e email. O Azure RMS funciona em vários dispositivos, como telefones, tablets e PCs, protegendo-os dentro e fora da sua organização. Esse recurso é possível porque o Azure RMS adiciona um nível de proteção permanece com dados hello, mesmo quando ele sai dos limites da organização.

Quando você usa o Azure RMS tooprotect seus arquivos, você está usando criptografia padrão do setor com suporte total a [FIPS 140-2](http://csrc.nist.gov/groups/STM/cmvp/standards.html). Quando você utilizar o Azure RMS para proteção de dados, terá garantia Olá que Olá permanece com arquivo hello, mesmo se ele for copiado toostorage que não está sob controle de saudação de TI, como um serviço de armazenamento de nuvem. Olá mesmo ocorre para os arquivos compartilhados por email, Olá arquivo é protegido como uma mensagem de email do anexo tooan, com instruções como tooopen Olá protegido anexo.

Ao planejar para a adoção do Azure RMS, é recomendável seguir hello:

* Instalar Olá [aplicativo RMS sharing](https://technet.microsoft.com/library/dn339006.aspx). Esse aplicativo se integra a aplicativos do Office, instalando um suplemento do Office para que os usuários possam proteger seus arquivos de forma direta e fácil.
* Configurar aplicativos e serviços toosupport Azure RMS
* Crie [modelos personalizados](https://technet.microsoft.com/library/dn642472.aspx) que reflitam as necessidades dos negócios. Por exemplo: um modelo de dados secretos que deve ser aplicado a todos os emails secretos relacionados.

As organizações que são fracas em [classificação de dados](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) e proteção de arquivo pode ser mais suscetível vazamento de toodata. Sem proteção adequadas de arquivo, as organizações não ser capaz de tooobtain ideias de negócios, monitorar abuso e impedir o acesso mal-intencionado toofiles.

Você pode aprender mais sobre o Azure RMS ao ler o artigo Olá [guia de Introdução ao Azure Rights Management](https://technet.microsoft.com/library/jj585016.aspx).
