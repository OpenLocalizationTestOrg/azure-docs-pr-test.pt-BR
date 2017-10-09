---
title: "práticas recomendadas de segurança do banco de dados aaaAzure | Microsoft Docs"
description: "Este artigo fornece um conjunto de melhores práticas de segurança do banco de dados do Azure."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: tomsh
ms.openlocfilehash: 78984291e8f74879c7f738e2ce3176c4be18d154
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-security-best-practices"></a>Melhores práticas de segurança do banco de dados do Azure

A segurança é uma das principais preocupações durante o gerenciamento de bancos de dados e sempre foi uma prioridade para o Banco de Dados SQL do Azure. Os bancos de dados podem ser totalmente protegido toohelp atender mais normas ou requisitos de segurança, como HIPAA, ISO 27001/27002 e PCI DSS nível 1, entre outros. Uma lista atual das certificações de conformidade de segurança está disponível em Olá [site Microsoft Trust Center](http://azure.microsoft.com/support/trust-center/services/). Você também pode escolher tooplace seus bancos de dados em datacenters do Azure específico com base em requisitos regulamentares.

Neste artigo, veremos uma coleção de melhores práticas de segurança de banco de dados do Azure. Essas práticas recomendadas são derivadas da nossa experiência com segurança de banco de dados do Azure e experiências de saudação de clientes, como por conta própria.

Para cada prática recomendada, vamos explicar:

-   A prática recomendada que Olá é
-   Por que você deseja tooenable essa prática recomendada
-   O que pode ser resultado de saudação se você não a prática recomendada de saudação tooenable
-   Como você pode aprender a prática recomendada de saudação tooenable

Este artigo de práticas recomendadas de segurança de banco de dados do Azure baseia-se em uma opinião consenso e recursos de plataforma do Azure e conjuntos de recursos que existem em tempo de saudação que este artigo foi escrito. Tecnologias e opiniões alterar ao longo do tempo e este artigo será atualizado em um tooreflect regularmente essas alterações.

As melhores práticas de segurança de banco de dados do Azure discutidas neste artigo incluem:

-   Use o acesso de banco de dados de toorestrict de regras de firewall
-   Habilitar a autenticação de banco de dados
-   Proteger seus dados usando criptografia
-   Proteger dados em trânsito
-   Habilitar a auditoria do banco de dados
-   Habilitar detecção de ameaças ao banco de dados


## <a name="use-firewall-rules-toorestrict-database-access"></a>Use o acesso de banco de dados de toorestrict de regras de firewall

O Banco de Dados SQL do Microsoft Azure fornece um serviço de banco de dados relacional para o Azure e outros aplicativos baseados na Internet. tooprovide segurança de acesso, banco de dados SQL controla o acesso com regras de firewall limitando conectividade por endereço IP, os mecanismos de autenticação que requerem usuários tooprove sua identidade e mecanismos de autorização, limitando os usuários toospecific ações e dados. Firewalls impedir que todos os servidores de banco de dados do access tooyour até que você especifique quais computadores têm permissão. firewall de saudação concede acesso toodatabases com base em Olá endereços IP de cada solicitação de origem.

![Regras de firewall](./media/azure-database-security-best-practices/azure-database-security-best-practices-Fig1.png)

Olá serviço de banco de dados SQL está disponível somente pela porta TCP 1433. tooaccess um banco de dados SQL do seu computador, verifique se o firewall do computador cliente permite a comunicação TCP de saída na porta TCP 1433. Se não for necessário a outros aplicativos, bloqueie as conexões de entrada na porta TCP 1433 usando regras de firewall.

Como parte do processo de conexão de hello, conexões de máquinas virtuais do Azure são tooa redirecionado a outro endereço IP e porta exclusiva para cada função de trabalho. número da porta Hello está no intervalo de saudação do too11999 11000. Para obter mais informações sobre portas TCP, consulte [Portas além da 1433 para o ADO.NET 4.5 e o Banco de Dados SQL 2](https://docs.microsoft.com/azure/sql-database/sql-database-develop-direct-route-ports-adonet-v12).

> [!Note]
> Para obter mais informações sobre as regras de firewall no Banco de Dados SQL, confira [Regras de firewall de Banco de Dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

## <a name="enable-database-authentication"></a>Habilitar a autenticação de banco de dados
O Banco de Dados SQL dá suporte a dois tipos de autenticação: a autenticação do SQL e a autenticação do Azure AD (Autenticação do Azure Active Directory).

A **Autenticação do SQL** é recomendável nos seguintes casos:

-   Ele permite que os ambientes do SQL Azure toosupport com sistemas operacionais mistos, onde todos os usuários não são autenticados por um domínio do Windows.
-   Permite que aplicativos mais antigos do SQL Azure toosupport e aplicativos fornecidos por terceiros que exigem a autenticação do SQL Server.
-   Permite que os usuários tooconnect de domínios desconhecidos ou não confiáveis. Por exemplo, um aplicativo em que os clientes estabelecidos se conectam com logons do SQL Server tooreceive Olá status atribuído das suas ordens.
-   Permite que o SQL Azure toosupport aplicativos baseados na Web onde os usuários criam suas próprias identidades.
-   Permite que o software toodistribute desenvolvedores seus aplicativos por meio de uma hierarquia de permissões complexa com base no conhecido, predefinição logons do SQL Server.

> [!Note]
> No entanto, a autenticação do SQL Server não pode usar o protocolo de segurança Kerberos.

Se você usa a **autenticação SQL**, deve:

-   Gerencie credenciais fortes hello.
-   Protege credenciais Olá na cadeia de caracteres de conexão de saudação.
-   (Possivelmente) protege credenciais Olá passadas pela rede de saudação do Olá Web server toohello banco de dados. Para obter mais informações, consulte [como: conectar-se tooSQL Server usando a autenticação do SQL no ASP.NET 2.0](https://msdn.microsoft.com/library/ms998300.aspx).

**Autenticação do Active Directory do Azure** é um mecanismo de conexão tooMicrosoft banco de dados do SQL Azure e [SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-what-is) usando as identidades no Azure Active Directory (AD do Azure). Com a autenticação do AD do Azure, você pode gerenciar centralmente as identidades de saudação de usuários de banco de dados e outros serviços da Microsoft em um local central. Central de gerenciamento de ID fornece um único local toomanage usuários de banco de dados e simplifica o gerenciamento de permissões. Os benefícios incluem o seguinte hello:

-   Ele fornece uma autenticação de servidor tooSQL alternativo.
-   Ajuda a parar a proliferação de saudação de identidades de usuário entre os servidores de banco de dados.
-   Permite o rodízio de senhas em um único lugar.
-   Os clientes podem gerenciar permissões de banco de dados usando grupos (AAD) externos.
-   Pode eliminar o armazenamento de senhas, permitindo a autenticação integrada do Windows e outras formas de autenticação às quais o Active Directory do Azure dá suporte.
-   Autenticação do Azure AD usa identidades de tooauthenticate de usuários de banco de dados independente em nível de banco de dados de saudação.
-   O AD do Azure dá suporte à autenticação baseada em token para aplicativos que se conectam tooSQL banco de dados.
-   A autenticação do Azure AD dá suporte ao ADFS (federação de domínio) ou à autenticação nativa de senha/usuário para um local do Azure Active Directory sem a sincronização de domínio.
-   O Azure AD dá suporte a conexões do SQL Server Management Studio que usam a Autenticação Universal do Active Directory, que inclui o MFA (Autenticação Multifator). A MFA inclui autenticação eficiente com uma variedade de opções de verificação fáceis como chamada telefônica, mensagem de texto, cartões inteligentes com PIN ou notificação por aplicativos móveis. Para saber mais, confira [Suporte do SSMS para MFA do Azure AD com o Banco de Dados SQL e o SQL Data Warehouse](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication).

etapas de configuração de saudação incluem hello tooconfigure procedimentos a seguir e usam a autenticação do Active Directory do Azure.

-   Criar e popular o Azure AD.
-   Opcional: Associar ou alterar Olá active directory que está associado a sua assinatura do Azure.
-   Crie um administrador do Azure Active Directory para o Azure SQL Server ou o [SQL Data Warehouse do Azure](https://azure.microsoft.com/services/sql-data-warehouse/).
- Configure os computadores cliente.
-   Crie usuários de banco de dados independente em seu banco de dados mapeado tooAzure identidades do AD.
-   Conecte o banco de dados de tooyour usando identidades do AD do Azure.

Você pode encontrar informações detalhadas [aqui](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).

## <a name="protect-your-data-using-encryption"></a>Proteger seus dados usando criptografia

[Criptografia de dados transparente de banco de dados SQL do Azure (TDE)](https://msdn.microsoft.com/library/dn948096.aspx) ajuda a proteger contra a ameaça de saudação de atividades mal-intencionadas executando criptografia em tempo real e a descriptografia do banco de dados de hello, backups associados, e arquivos de log de transações em repouso sem necessidade de alterações toohello aplicativo. Ela criptografa o armazenamento de saudação de um banco de dados inteiro usando uma chave de criptografia de banco de dados de saudação de chamada de chave simétrica.

Mesmo quando o armazenamento inteiro Olá é criptografado, é muito importante tooalso criptografar seu próprio banco de dados. Esta é uma implementação de defesa Olá abordagem em camadas para a proteção de dados. Se você estiver usando o banco de dados do SQL Azure e deseja que os dados confidenciais, como números de previdência social ou de cartão de crédito tooprotect, você pode criptografar os bancos de dados com a criptografia AES de 256 bits de 140-2 validados de FIPS que atende aos requisitos de saudação de muitos padrões do setor (por exemplo, HIPAA, PCI).

É importante toounderstand arquivos relacionados muito[buffer pool BPE (extensão)](https://docs.microsoft.com/sql/database-engine/configure-windows/buffer-pool-extension) não são criptografados quando um banco de dados é criptografado usando TDE. Você deve usar ferramentas de criptografia no nível do sistema de arquivos como [BitLocker](https://technet.microsoft.com/library/cc732774) ou hello [Encrypting File System (EFS)](https://technet.microsoft.com/library/cc700811.aspx) para BPE arquivos relacionados.

Desde que um usuário autorizado, como um administrador de segurança ou um administrador de banco de dados pode acessar dados hello, mesmo se o banco de dados de saudação é criptografado com TDE, você também deve seguir as recomendações de saudação abaixo:

-   Habilite a autenticação do SQL no nível de banco de dados de saudação.
-   Use a autenticação do Azure AD com [funções RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is).
-   Os usuários e aplicativos devem usar tooauthenticate contas separadas. Dessa forma, você pode limitar as permissões de saudação concedidas toousers e aplicativos e reduzir os riscos de saudação de atividade mal-intencionada.
-   Implementar segurança em nível de banco de dados usando as funções de banco de dados fixa (como db_datareader ou db_datawriter), ou você pode criar funções personalizadas para seu aplicativo toogrant objetos de banco de dados de tooselected permissões explícitas.

Para outra maneiras tooencrypt seus dados, considere:

-   [Criptografia em nível de célula](https://msdn.microsoft.com/library/ms179331.aspx) tooencrypt colunas específicas ou mesmo células de dados com diferentes chaves de criptografia.
-   Criptografia em uso usando o sempre criptografado: [sempre criptografado](https://msdn.microsoft.com/library/mt163865.aspx) permite que os clientes tooencrypt os dados confidenciais em aplicativos de cliente e nunca revelem toohello chaves de criptografia Olá mecanismo de banco de dados (banco de dados SQL ou SQL Server). Como resultado, sempre criptografado fornece uma separação entre aqueles que possuem dados saudação (e podem exibi-lo) e aqueles que gerenciam dados de saudação (mas não devem ter acesso).
-   Usando a segurança de nível de linha: segurança de nível de linha permite que os clientes toocontrol acesso toorows em uma tabela de banco de dados com base em características de saudação do usuário Olá executando uma consulta (por exemplo, grupo associação ou contexto de execução). Para saber mais, confira [Segurança em nível de linha](https://msdn.microsoft.com/library/dn765131).

## <a name="protect-data-in-transit"></a>Proteger dados em trânsito
A proteção dos dados em trânsito deve ser parte essencial de sua estratégia de proteção de dados. Desde que os dados serão movendo alternadas em vários locais, a recomendação geral Olá é sempre usar dados de tooexchange protocolos SSL/TLS em diferentes locais. Em algumas circunstâncias, talvez seja o canal de comunicação inteira Olá tooisolate entre seu local e nuvem infraestrutura usando uma rede virtual privada (VPN).

Para dados que se movem entre sua infraestrutura local e o Azure, você deve considerar proteções adequadas, como HTTPS ou VPN.

Para organizações que precisam de acesso toosecure de vários tooAzure localizado no local de estações de trabalho, use [VPN site a site do Azure](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-site-to-site-create).

Para organizações que precisam de toosecure o acesso de estações de trabalho individuais localizados no local ou externamente tooAzure, considere o uso de [ponto a Site VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-point-to-site-create).

Conjuntos de dados maiores podem ser movidos em um link WAN de alta velocidade dedicado, como o [ExpressRoute](https://azure.microsoft.com/services/expressroute/). Se você escolher toouse rota expressa, você também pode criptografar dados Olá no nível do aplicativo, Olá usando [SSL/TLS](https://support.microsoft.com/kb/257591) ou outros protocolos para proteção adicional.

Se você estiver interagindo com o armazenamento do Azure por meio de saudação Portal do Azure, todas as transações ocorrem por meio de HTTPS. [API de REST do armazenamento](https://msdn.microsoft.com/library/azure/dd179355.aspx) via HTTPS também pode ser o toointeract usado com [armazenamento do Azure](https://azure.microsoft.com/services/storage/) e [banco de dados do SQL Azure](https://azure.microsoft.com/services/sql-database/).

As organizações que não tooprotect dados em trânsito são mais suscetíveis para [ataques man-in-the-middle](https://technet.microsoft.com/library/gg195821.aspx), [espionagem](https://technet.microsoft.com/library/gg195641.aspx) e sequestro de sessão. Esses ataques podem ser a primeira etapa Olá na obtenção de dados do access tooconfidential.

mais informações sobre a opção de VPN do Azure ao ler o artigo de saudação do toolearn [de planejamento e design para o Gateway de VPN](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-plan-design).

## <a name="enable-database-auditing"></a>Habilitar a auditoria do banco de dados
Auditoria de uma instância de saudação mecanismo de banco de dados do SQL Server ou um banco de dados individual envolve o acompanhamento e log de eventos que ocorrem no hello mecanismo de banco de dados. A auditoria do SQL Server permite criar auditorias de servidor, que podem conter especificações de auditoria de servidor para eventos no nível do servidor e especificações de auditoria de banco de dados para eventos no nível do banco de dados. Os eventos auditados podem ser gravados os logs de eventos de toohello ou tooaudit arquivos.

Há vários níveis de auditoria do SQL Server, dependendo dos requisitos padrão ou governamentais de sua instalação. Auditoria do SQL Server fornece ferramentas de saudação e os processos que você deve ter tooenable, armazenamento e exibir auditorias em vários objetos de servidor e banco de dados.

[Auditoria de banco de dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-auditing) rastreia eventos de banco de dados e grava o log de auditoria tooan em sua conta de armazenamento do Azure.

A auditoria pode ajudar você a manter uma conformidade regulatória, a entender a atividade do banco de dados e a obter informações sobre discrepâncias e anomalias que poderiam indicar preocupações de negócios ou suspeitas de violações de segurança.

A auditoria permite e facilita a padrões de toocompliance aderência mas não garante conformidade.

toolearn mais sobre a auditoria de banco de dados e como tooenable, leia o artigo de saudação [ativar a detecção de ameaças e auditoria em servidores SQL na Central de segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-enable-auditing-on-sql-servers).

## <a name="enable-database-threat-detection"></a>Habilitar detecção de ameaças ao banco de dados
Detecção de ameaças SQL permite toodetect e responder a ameaças de toopotential conforme elas ocorrem, fornecendo alertas de segurança em atividades anormais. Você receberá um alerta em caso de atividades suspeitas em bancos de dados, possíveis vulnerabilidades e ataques de injeção de SQL, bem como padrões anômalos de acesso ao banco de dados. Alertas de detecção de ameaças SQL fornecer detalhes de atividade suspeita e recomendarão a ação sobre como tooinvestigate e atenuar a ameaça de saudação.

Por exemplo, injeção de SQL é um Olá Web aplicativo problemas de segurança comuns em Olá Internet, os aplicativos usados tooattack controladas por dados. Os invasores tirar proveito de aplicativo vulnerabilidades tooinject de instruções SQL mal-intencionadas nos campos de entrada do aplicativo, serem violados ou modificar dados no banco de dados de saudação.

toolearn sobre como tooset a detecção de ameaças do banco de dados em hello Azure portal, consulte [detecção de ameaças do banco de dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection).

Além disso, a Detecção de Ameaças do SQL integra seus alertas à [Central de Segurança do Azure](https://azure.microsoft.com/services/security-center/). Você está convidado tootry-lo por 60 dias para liberar.

toolearn mais sobre a detecção de ameaças do banco de dados e como tooenable, leia o artigo de saudação [ativar a detecção de ameaças e auditoria em servidores SQL na Central de segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-enable-auditing-on-sql-servers).

## <a name="conclusion"></a>Conclusão
O Banco de Dados do Azure é uma plataforma robusta de banco de dados, com uma gama completa de recursos de segurança que atendem aos vários requisitos de conformidade organizacional e regulamentar. Você pode ajudar a proteger dados, controlar dados de tooyour saudação acesso físico e, em seguida, usando uma variedade de opções de segurança de dados no arquivo hello-, coluna ou nível de linha com a criptografia transparente de dados, a criptografia no nível da célula ou a segurança em nível de linha. Sempre criptografado também permite que as operações em relação aos dados criptografados, simplificando o processo de saudação de atualizações de aplicativo. Por sua vez, tooauditing acesso os logs de atividade de banco de dados SQL fornece informações de saudação for necessário, permitindo que você tooknow como e quando os dados são acessados.

## <a name="next-steps"></a>Próximas etapas
- toolearn mais informações sobre regras de firewall, consulte [as regras de Firewall](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).
- toolearn sobre usuários e logons, consulte [gerenciar logons](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins).
- Para obter um tutorial, consulte [Proteger o Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-security-tutorial).
