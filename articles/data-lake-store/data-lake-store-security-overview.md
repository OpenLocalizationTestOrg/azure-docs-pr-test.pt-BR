---
title: "aaaOverview de segurança no repositório Data Lake | Microsoft Docs"
description: "Entender como o Azure Data Lake Store é um repositório de big data seguro"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ebd5b2ac-c5cc-46d4-9cfd-1a1ee70024c2
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 69e20bd046a9427202074baf59bff13f5b6a83ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="security-in-azure-data-lake-store"></a>Segurança no Armazenamento do Azure Data Lake
Muitas empresas estão tirando vantagem da análise de big data para business insights toohelp-los fazer inteligente decisões. Uma organização pode ter um ambiente regulamentado e complexo, com um número crescente de usuários diferentes. É essencial para uma toomake enterprise-se de que dados essenciais aos negócios são armazenados com mais segurança, com o nível de acesso concedido a usuários tooindividual correto hello. Repositório Azure Data Lake é projetado toohelp atender a esses requisitos de segurança. Neste artigo, saiba mais sobre os recursos de segurança de saudação do repositório Data Lake, incluindo:

* Autenticação
* Autorização
* Isolamento da rede
* Proteção de dados
* Auditoria

## <a name="authentication-and-identity-management"></a>Autenticação e gerenciamento das identidades
A autenticação é o processo de saudação pelo qual a identidade do usuário é verificada quando o usuário Olá interage com o repositório Data Lake ou com qualquer serviço que se conecta tooData Lake repositório. Para gerenciamento de identidade e autenticação, usa o repositório Data Lake [Active Directory do Azure](../active-directory/active-directory-whatis.md), uma identidade e acesso gerenciamento nuvem solução abrangente que simplifica o gerenciamento de saudação de usuários e grupos.

Toda assinatura do Azure pode ser associada a uma instância do Azure Active Directory. Somente os usuários e identidades de serviço que são definidas no serviço Active Directory do Azure podem acessar sua conta do repositório Data Lake, usando Olá portal do Azure, ferramentas de linha de comando, ou por meio de aplicativos de cliente que cria sua organização usando Olá dados do Azure Repositório Lake SDK. As principais vantagens de usar o Azure Active Directory como um mecanismo de controle de acesso centralizado são:

* Gerenciamento de ciclo de vida de identidade simplificado. identidade de saudação de um usuário ou um serviço (uma identidade de entidade de serviço) pode ser criada rapidamente e rapidamente revogada, basta excluir ou desabilitar conta Olá no diretório de saudação.
* Multi-Factor Authentication. [Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) fornece uma camada adicional de segurança para os logons e as transações dos usuários.
* A autenticação de clientes por meio de um protocolo aberto padrão, como OAuth ou OpenID.
* Federação com serviços de diretório da empresa e provedores de identidade da nuvem.

## <a name="authorization-and-access-control"></a>Autenticação e controle de acessos
Depois que o Active Directory do Azure autentica um usuário para que hello usuário possa acessar o repositório do Azure Data Lake, controles de autorização acessar permissões para o repositório Data Lake. Repositório data Lake separa a autorização para atividades relacionadas à conta e dados relacionados em Olá maneira a seguir:

* [Controle de acesso baseado em função](../active-directory/role-based-access-control-what-is.md) ) fornecido pelo Azure para gerenciamento de contas
* POSIX ACL para acesso a dados no repositório de saudação

### <a name="rbac-for-account-management"></a>RBAC para o gerenciamento da conta
Quatro funções básicas são definidas para o Data Lake Store por padrão. funções Hello permitem operações diferentes em uma conta do repositório Data Lake via Olá portal do Azure, cmdlets do PowerShell e APIs REST. Olá proprietário e funções de Colaborador podem executar uma variedade de funções de administração na conta de saudação. Você pode atribuir Olá leitor função toousers que apenas interagir com dados.

![Funções RBAC](./media/data-lake-store-security-overview/rbac-roles.png "Funções RBAC")

Observe que, embora as funções são atribuídas para gerenciamento de conta, algumas funções afetam toodata de acesso. É necessário toouse ACLs toocontrol acesso toooperations que um usuário pode executar no sistema de arquivo hello. Olá, a tabela a seguir mostra um resumo dos direitos e gerenciamento de direitos de acesso de dados para Olá funções padrão.

| Funções | Direitos de gerenciamento | Direitos de acesso a dados | Explicação |
| --- | --- | --- | --- |
| Nenhuma função atribuída |Nenhum |Controlado pela ACL |usuário de saudação não pode usar o hello Azure portal ou o Azure PowerShell cmdlets toobrowse repositório Data Lake. usuário Olá pode usar somente as ferramentas de linha de comando. |
| Proprietário |Todos |Todos |função de proprietário de saudação é um superusuário. Essa função pode gerenciar tudo e tem acesso completo toodata. |
| Leitor |Somente leitura |Controlado pela ACL |função de leitor de saudação pode exibir tudo sobre o gerenciamento de conta, como qual usuário é atribuído a função toowhich. função de leitor de saudação não pode fazer as alterações. |
| Colaborador |Tudo, exceto adicionar e remover as funções. |Controlado pela ACL |função de Colaborador Olá pode gerenciar alguns aspectos de uma conta, como implantações e criar e gerenciar alertas. função de Colaborador Olá não é possível adicionar ou remover funções. |
| Administrador de Acesso do Usuário |Adicionar e remover funções |Controlado pela ACL |função de administrador de acesso de usuário de saudação pode gerenciar tooaccounts de acesso do usuário. |

Para obter instruções, consulte [atribuir usuários ou grupos de segurança de contas do repositório de Lake tooData](data-lake-store-secure-data.md#assign-users-or-security-groups-to-azure-data-lake-store-accounts).

### <a name="using-acls-for-operations-on-file-systems"></a>Usando ACLs para as operações nos sistemas de arquivos
O Data Lake Store é um sistema de arquivos hierárquico, como o HDFS (Hadoop Distributed File System) e dá suporte a [ACLs POSIX](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_Access_Control_Lists). Ele controla leitura (r), gravação (w) e execute (tooresources de permissões para a função de proprietário de saudação para proprietários de grupo hello e para outros usuários e grupos x). Em Olá Data Lake repositório Public Preview (versão atual do hello), as ACLs podem ser habilitadas na pasta raiz de hello, subpastas e arquivos individuais. Para saber mais sobre como funcionam as ACLs no contexto do Data Lake Store, veja [Controle de acesso no Data Lake ](data-lake-store-access-control.md).

Recomendamos que você defina as ACLs para vários usuários usando [grupos de segurança](../active-directory/active-directory-accessmanagement-manage-groups.md). Adicionar grupo de segurança usuários tooa e, em seguida, atribuir Olá ACLs para um grupo de segurança de toothat do arquivo ou pasta. Isso é útil quando você desejar acesso personalizado a tooprovide, porque você está limitado tooadding um máximo de nove entradas de acesso personalizado. Para obter mais informações sobre como toobetter proteger os dados armazenados no repositório Data Lake usando grupos de segurança do Active Directory do Azure, consulte [atribuir usuários ou grupo de segurança como toohello ACLs de sistema de arquivos do repositório Azure Data Lake](data-lake-store-secure-data.md#filepermissions).

![Lista de acesso padrão e personalizado](./media/data-lake-store-security-overview/adl.acl.2.png "lista de acesso padrão e personalizado")

## <a name="network-isolation"></a>Isolamento da rede
Repositório de dados de tooyour do repositório Use Data Lake toohelp controle acesso no nível de rede hello. Você pode habilitar o firewall e definir um intervalo de endereços IP para seus clientes confiáveis. Com um intervalo de endereços IP, somente os clientes que têm um endereço IP dentro do intervalo de saudação definido podem se conectar a tooData Lake repositório.

![Configurações de firewall e acesso IP](./media/data-lake-store-security-overview/firewall-ip-access.png "Endereço IP e configurações de firewall")

## <a name="data-protection"></a>Proteção de dados
O Azure Data Lake Store protege seus dados em todo o ciclo de vida. Dados em trânsito, repositório Data Lake usa saudação padrão da indústria segurança de camada de transporte (TLS) protocol toosecure dados pela rede hello.

![Criptografia no Data Lake Store](./media/data-lake-store-security-overview/adls-encryption.png "Criptografia no Data Lake Store")

Repositório data Lake também fornece criptografia de dados que são armazenados na conta de saudação. Você pode escolher toohave seus dados criptografados ou optar por sem criptografia. Se você aceitar a criptografia, os dados armazenados no repositório Data Lake serão criptografado toostoring anterior na mídia persistente. Nesse caso, o repositório Data Lake automaticamente criptografa toopersisting anteriores de dados e descriptografa tooretrieval anteriores de dados, por isso é completamente transparente toohello cliente acessando dados saudação. Não há nenhuma alteração de código necessária nos dados do hello cliente lado tooencrypt/descriptografar.

Para gerenciamento de chaves, o repositório Data Lake oferece dois modos de gerenciar suas chaves de criptografia mestra (MEKs), que são necessários para descriptografar os dados que são armazenados no hello repositório Data Lake. Você também pode deixar repositório Data Lake gerenciar Olá MEKs para você, ou escolha tooretain apropriar MEKs hello usando sua conta do Azure Key Vault. Especifique o modo de saudação do gerenciamento de chaves enquanto durante a criação de uma conta do repositório Data Lake. Para obter mais informações sobre como tooprovide relacionadas à criptografia configuração, consulte [Introdução ao repositório Azure Data Lake usando hello Azure Portal](data-lake-store-get-started-portal.md).

## <a name="auditing-and-diagnostic-logs"></a>Logs de auditoria e diagnóstico
Você pode usar os logs de auditoria ou de diagnóstico, dependendo de estar procurando logs para atividades relacionadas ao gerenciamento ou para atividades relacionadas aos dados.

* Atividades relacionadas ao gerenciamento de usam as APIs do Gerenciador de recursos do Azure e são apresentadas em Olá portal do Azure por meio de logs de auditoria.
* As atividades relacionadas a dados usam APIs REST de WebHDFS e são apresentadas em Olá portal do Azure por meio de logs de diagnóstico.

### <a name="auditing-logs"></a>Logs de auditoria
toocomply com as normas, uma organização pode exigir as trilhas de auditoria adequada se ele precisa toodig em incidentes específicos. O Data Lake Store tem auditoria e monitoramento internos e registra todas as atividades de gerenciamento da conta.

Para trilhas de auditoria de gerenciamento de conta, exibir e escolha Olá colunas que você deseja toolog. Você também pode exportar logs de auditoria tooAzure armazenamento.

![Logs de auditoria](./media/data-lake-store-security-overview/audit-logs.png "Logs de auditoria")

### <a name="diagnostic-logs"></a>Logs de diagnóstico
Você pode definir trilhas de auditoria de acesso a dados nas Olá portal do Azure (em configurações de diagnóstico) e criar uma conta de armazenamento de BLOBs do Azure onde Olá logs são armazenados.

![Logs de diagnóstico](./media/data-lake-store-security-overview/diagnostic-logs.png "Logs de diagnóstico")

Depois de configurar as definições de diagnóstico, você pode exibir os logs de saudação em Olá **Logs de diagnóstico** guia.

Para saber mais sobre como trabalhar com logs de diagnóstico com o Azure Data Lake Store, consulte [Acessar logs de diagnóstico para o Data Lake Store](data-lake-store-diagnostic-logs.md).

## <a name="summary"></a>Resumo
Os clientes corporativos exigem uma plataforma de nuvem de análise de dados que é seguro e fácil toouse. Repositório Azure Data Lake é projetado toohelp atender a esses requisitos através de gerenciamento de identidade e autenticação por meio da integração do Active Directory do Azure, a autorização baseada em ACL, isolamento de rede, a criptografia de dados em trânsito e em repouso (Olá recebidas futuras) e auditoria.

Se você quiser toosee novos recursos do repositório Data Lake, envie seus comentários no hello [UserVoice de armazenamento do Data Lake fórum](https://feedback.azure.com/forums/327234-data-lake).

## <a name="see-also"></a>Consulte também
* [Visão geral do repositório Azure Data Lake](data-lake-store-overview.md)
* [Introdução ao Data Lake Store](data-lake-store-get-started-portal.md)
* [Proteger dados no Repositório Data Lake](data-lake-store-secure-data.md)

