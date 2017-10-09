---
title: "aaaAzure considerações de design do Active Directory híbrida identidade - definir a estratégia de proteção de dados | Microsoft Docs"
description: "Você definirá a estratégia de proteção de dados de saudação para seu híbrida identidade solução toomeet Olá requisitos de negócios que você definiu."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: e76fd1f4-340a-492a-84d9-e05f3b7cc396
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 8fd7ab364a09de3b60293a4a1cbb6e0fa4a3295d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="define-data-protection-strategy-for-your-hybrid-identity-solution"></a>Definir estratégia de proteção de dados para sua solução de identidade híbrida
Nesta tarefa, você definirá a estratégia de proteção de dados de saudação para seu híbrida identidade solução toomeet Olá requisitos de negócios que você definiu no:

* [Determinar os requisitos para proteção de dados](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md)
* [Determinar requisitos de gerenciamento de conteúdo](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)
* [Determinar requisitos de controle de acesso](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)
* [Determinar requisitos de resposta a incidentes](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="define-data-protection-options"></a>Definir opções de proteção de dados
Como foi explicado em [Determinar requisitos de sincronização de diretório](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md), o AD do Microsoft Azure pode ser sincronizado com o AD DS (Serviços de Domínio do Active Directory) local. Essa integração permite que as organizações tooleverage AD do Azure tooverify as credenciais de usuário quando ele estão tentando recursos corporativos tooaccess. Isso pode ser feito para os dois cenários: dados em rest no local e na nuvem hello.  Toodata de acesso no AD do Azure requer autenticação de usuário por meio de um serviço de token de segurança (STS).

Quando autenticado, Olá UPN (UPN) é lido do token de autenticação hello e Olá duplicado partição e correspondente de contêiner é determinado domínio toohello do usuário. Obter informações sobre a existência do usuário hello, estado habilitado e função são usadas por toodetermine de sistema de autorização de saudação se locatário de destino em toohello Olá acesso solicitado está autorizado para este usuário nesta sessão. Determinadas ações autorizadas (especificamente, criar usuários, redefinição de senha) criar uma trilha de auditoria que pode ser usada por um locatário os esforços de conformidade do administrador toomanage ou investigações.

Movimentação de dados de seu datacenter local no armazenamento do Azure em uma conexão de Internet pode não ser viável devido toodata volume, a disponibilidade de largura de banda ou outras considerações. Olá [serviço de importação/exportação do armazenamento do Azure](../storage/common/storage-import-export-service.md) fornece uma opção com base em hardware para colocar/recuperar grandes volumes de dados no armazenamento de blob. Ele permite toosend [criptografados pelo BitLocker](https://technet.microsoft.com/library/dn306081#BKMK_BL2012R2) diretamente tooan datacenter do Azure onde os operadores de nuvem carregará a conta de armazenamento Olá conteúdo tooyour ou eles podem baixar seu tooyour de dados do Azure unidades tooreturn de unidades de disco rígido tooyou. Apenas discos criptografados são aceitas para esse processo (usando uma chave do BitLocker gerada pelo serviço Olá próprio durante a instalação do trabalho de saudação). chave do BitLocker Olá é fornecida tooAzure separadamente, proporcionando fora da banda chave compartilhamento.

Como os dados em trânsito podem ocorrer em diferentes cenários, também é tooknow relevante que o Microsoft Azure usa [a rede virtual](https://azure.microsoft.com/documentation/services/virtual-network/) tráfego tooisolate locatários uns dos outros, empregar medidas como host e convidado-nível firewalls, filtragem de pacotes IP, porta de bloqueio e pontos de extremidade HTTPS. No entanto, a maioria das comunicações internas do Azure, incluindo infraestrutura para infraestrutura e infraestrutura para cliente (local), também é criptografada. Outro cenário importante é a comunicação de saudação em datacenters do Azure; A Microsoft gerencia tooassure redes que nenhuma VM pode representar ou interceptar no endereço IP de saudação do outro. O TLS/SSL é usado ao acessar o armazenamento do Azure ou bancos de dados SQL ou ao se conectar a serviços tooCloud. Nesse caso, administrador de saudação do cliente é responsável por obter um certificado TLS/SSL e implantá-la tootheir infra-estrutura de locatário. Tráfego de dados movendo entre máquinas virtuais Olá mesma implantação em ou entre locatários em uma única implantação via rede Virtual do Microsoft Azure podem ser protegidos por meio de protocolos de comunicação criptografados, como HTTPS, SSL/TLS ou outras pessoas.

Dependendo de como você respondeu perguntas Olá [determinar requisitos de proteção de dados](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md), você deve ser capaz de toodetermine como você deseja que os dados tooprotect e solução de identidade híbrida Olá irá ajudá-lo em que. tabela Olá mostra as opções de saudação com suporte do Azure que estão disponíveis para cada cenário de proteção de dados.

| Opções de proteção de dados | Em repouso na nuvem Olá | Em repouso no local | Em trânsito |
| --- | --- | --- | --- |
| Criptografia de Unidade BitLocker |X |X | |
| Bancos de dados do SQL Server tooencrypt |X |X | |
| Criptografia de VM para VM | | |X |
| SSL/TLS | | |X |
| VPN | | |X |

> [!NOTE]
> Leitura [conformidade por recurso](https://azure.microsoft.com/support/trust-center/services/) em [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/) tooknow mais sobre as certificações de saudação que cada serviço do Azure é compatível com.
> Como as opções de saudação de proteção de dados usam uma abordagem de várias camada, a comparação entre essas opções não são aplicáveis para esta tarefa. Certifique-se de que estão utilizando todas as opções disponíveis para cada estado que dados hello serão.
>
>

## <a name="define-content-management-options"></a>Definir opções de gerenciamento de conteúdo
Uma vantagem de usar o AD do Azure toomanage uma infraestrutura de identidade híbrida é que o processo de saudação é completamente transparente da perspectiva de saudação do usuário. usuário Olá tentará tooaccess um recurso compartilhado, Olá recurso requer autenticação, usuário Olá terá toosend tooAzure uma solicitação de autenticação AD em ordem tooobtain Olá token e acessar recursos de saudação. Todo esse processo ocorre em segundo plano, sem interação do usuário. Também é possível toogrant permissão tooa [grupo](active-directory-manage-groups.md#getting-started-with-access-management) de usuários em ordem tooallow-los tooperform determinadas ações comuns.

As organizações que se preocupam com a privacidade dos dados normalmente exigem a classificação de dados para sua solução. Se sua infraestrutura local atual já estiver usando a classificação de dados, é possível tooleverage AD do Azure como repositório de saudação principal para a identidade do usuário. Uma ferramenta comum que é usada no local para a classificação de dados é denominada [Kit de Ferramentas de Classificação de Dados](https://msdn.microsoft.com/library/Hh204743.aspx) para Windows Server 2012 R2. Essa ferramenta pode ajudar a tooidentify, classificar e proteger dados em servidores de arquivos em sua nuvem privada. Também é possível tooleverage Olá [classificação automática de arquivos](https://technet.microsoft.com/library/hh831672.aspx) no Windows Server 2012 tooaccomplish isso.

Se sua organização não tiver a classificação de dados no local, mas precisa tooprotect os arquivos confidenciais sem adicionar novos servidores no local, eles podem usar o Microsoft [Azure Rights Management Service](https://technet.microsoft.com/library/JJ585026.aspx).  O Azure RMS usa criptografia, identidade e autorização políticas toohelp proteger seus arquivos e emails, e funciona em vários dispositivos — PCs, tablets e telefones. Como o Azure RMS é um serviço de nuvem, não é necessário tooexplicitly configurar relações de confiança com outras organizações antes de você pode compartilhar conteúdo protegido com elas. Se elas já tiverem um Office 365 ou um diretório do AD do Azure, isso significa que há suporte automático para a colaboração entre organizações. Você também pode sincronizar apenas Olá atributos do diretório que o Azure RMS precisa toosupport uma identidade comum para suas contas do Active Directory local, usando o Azure Active Directory Synchronization Services (AAD Sync) ou do Azure AD Connect.

Uma parte essencial do gerenciamento de conteúdo é toounderstand quem está acessando quais recursos, portanto um recurso de registro em log avançado é importante para a solução de gerenciamento de identidade de saudação. O AD do Azure fornece log por 30 dias, incluindo:

* Alterações na associação de função (ex: usuário adicionou a função de administrador de tooGlobal)
* Atualizações de credencial (por exemplo: alterações de senha)
* Gerenciamento de domínio (por exemplo: verificar um domínio personalizado, remover um domínio)
* Adicionando ou removendo aplicativos
* Gerenciamento de usuários (por exemplo: adição, remoção, atualização de um usuário)
* Adicionando ou removendo licenças

> [!NOTE]
> Leitura [gerenciamento de logs de auditoria e segurança do Microsoft Azure](http://download.microsoft.com/download/B/6/C/B6C0A98B-D34A-417C-826E-3EA28CDFC9DD/AzureSecurityandAuditLogManagement_11132014.pdf) tooknow mais sobre os recursos de registro em log no Azure.
> Dependendo de como você respondeu perguntas Olá [determinar os requisitos de gerenciamento de conteúdo](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md), você deve ser capaz de toodetermine como você deseja Olá toobe conteúdo gerenciado em sua solução de identidade híbrida. Enquanto todas as opções expostas na tabela 6 são capazes de integração com o AD do Azure, é importante toodefine que é mais adequado às suas necessidades de negócios.
>
>

| Opções de gerenciamento de conteúdo | Vantagens | Desvantagens |
| --- | --- | --- |
| Centralizado no local (servidor do Active Directory Rights Management) |Controle total sobre a infraestrutura de servidor de saudação responsável para classificar dados saudação <br> Recurso interno no Windows Server, não é necessária nenhuma licença nem assinatura adicional <br> Pode ser integrado ao AD do Azure em um cenário híbrido <br> Oferece suporte a recursos de IRM (Gerenciamento de Direitos de Informação) no Microsoft Online Services, como o Exchange Online e o SharePoint Online, bem como o Office 365 <br> Oferece suporte aos produtos de servidor Microsoft no local, como Exchange Server, SharePoint Server e servidores de arquivos que executam o Windows Server e a FCI (Infraestrutura de Classificação de Arquivos). |Manutenção mais alta, (manter backup com atualizações, configuração e possíveis atualizações), desde IT possui Olá Server <br> Requer uma infraestrutura de servidor local<br> Não aproveita originalmente os recursos do Azure |
| Centralizado na nuvem hello (Azure RMS) |Toohello mais fácil de toomanage comparado solução local <br> Pode ser integrado ao AD DS em um cenário híbrido <br>  Totalmente integrado ao AD do Azure <br> Não requer um servidor local no serviço de saudação do pedido toodeploy <br> Oferece suporte aos produtos de servidor Microsoft no local, como Exchange Server, SharePoint Server e servidores de arquivos que executam o Windows Server e a FCI (Infraestrutura de Classificação de Arquivos) <br> A TI pode ter controle total da chave de seus locatários com o recurso BYOK. |Sua organização deve ter uma assinatura de nuvem que ofereça suporte ao RMS  <br> Sua organização deve ter uma autenticação de usuário do AD do Azure diretório toosupport para RMS |
| Híbrido (Azure RMS integrado ao servidor do Active Directory Rights Management local) |Este cenário acumula vantagens hello, centralizado no local e na nuvem hello. |Sua organização deve ter uma assinatura de nuvem que ofereça suporte ao RMS  <br> Sua organização deve ter uma autenticação de usuário do AD do Azure diretório toosupport para RMS, <br> Exige uma conexão entre o serviço de nuvem do Azure e a infraestrutura local |

## <a name="define-access-control-options"></a>Definir opções de controle de acesso
Ao utilizar autenticação hello, autorização de controle de acesso recursos disponíveis no AD do Azure, você será capaz de tooenable toouse sua empresa um repositório central de identidade enquanto permite que os usuários e parceiros toouse-logon único (SSO) conforme mostrado no Olá Figura abaixo:

![](./media/hybrid-id-design-considerations/centralized-management.png)

Gerenciamento centralizado e integração completa a outros diretórios

Active Directory do Azure fornece toothousands de logon único de aplicativos SaaS e aplicativos da web local. Leia Olá [lista de compatibilidade de Federação do Active Directory do Azure: logon único de provedores de identidade de terceiros que podem ser usado tooimplement](https://msdn.microsoft.com/library/azure/jj679342.aspx) artigo para obter mais detalhes sobre Olá SSO terceiros que foram testados por Microsoft. Esse recurso permite que a organização tooimplement uma variedade de cenários B2B, mantendo o controle de gerenciamento de identidade e acesso hello. No entanto, durante a saudação B2B criação de processo é o método de autenticação de saudação do toounderstand importantes que será usado pelo parceiro hello e valida se esse método tem suporte pelo Azure. Atualmente, estes são os métodos com suporte do AD do Azure:

* SAML (Security Assertion Markup Language)
* OAuth
* Kerberos
* Tokens
* Certificados

> [!NOTE]
> ler [protocolos de autenticação do Azure Active Directory](https://msdn.microsoft.com/library/azure/dn151124.aspx) tooknow mais detalhes sobre cada protocolo e seus recursos no Azure.
>
>

Usando o suporte de saudação do AD do Azure, negócios móveis, os aplicativos podem usar Olá mesmo fácil serviços móveis autenticação experiência tooallow funcionários toosign em seus aplicativos móveis com suas credenciais corporativas do Active Directory. Com esse recurso, o AD do Azure tem suporte como um provedor de identidade nos serviços móveis junto com hello outros provedores de identidade que já têm suporte (que incluem Accounts da Microsoft, Facebook ID, ID do Google e Twitter ID). Se Olá aplicativos usa Olá credencial do usuário localizada em AD DS da empresa Olá no local, o acesso de saudação de parceiros e usuários provenientes da nuvem de saudação deve ser transparente. Gerenciar do usuário aplicativos de web de too(cloud-based) de controle de acesso condicional, API da web, Microsoft serviços de nuvem, 3ª aplicativos SaaS de terceiros e aplicativos cliente (móvel) nativo e ter benefícios de saudação de segurança, auditoria, relatórios em um local. No entanto, é recomendável toovalidate isso em um ambiente de não produção ou com uma quantidade limitada de usuários.

> [!TIP]
> é importante toomention que AD do Azure não tem diretiva de grupo como o AD DS do tem. Na política de tooenforce ordem para dispositivos você precisará uma solução de gerenciamento de dispositivos móveis, como [Microsoft Intune](https://technet.microsoft.com/library/jj676587.aspx).
>
>

Depois que o usuário Olá é autenticado usando o Azure AD, é importante tooevaluate nível de saudação de acesso Olá usuário tê-lo. Olá nível de acesso que Olá usuário terá sobre um recurso pode variar, enquanto o AD do Azure pode adicionar uma camada adicional de segurança, controlando toosome de acessar recursos, você deve também Lembre-se que o próprio recurso de saudação também pode ter sua própria lista de controle de acesso separadamente, como controle de acesso de saudação de arquivos localizados em um servidor de arquivos. Figura Olá a seguir resume os níveis de saudação do controle de acesso que você pode ter em um cenário híbrido:

![](./media/hybrid-id-design-considerations/accesscontrol.png)

Cada interação no diagrama Olá mostrada na Figura X representa um cenário de controle de acesso que pode ser coberto pelo AD do Azure. Abaixo, você tem uma descrição de cada cenário:

1. Tooapplications de acesso condicional que estão hospedados no local: você pode usar dispositivos registrados com políticas de acesso para aplicativos que são configurados toouse do AD FS com o Windows Server 2012 R2. Para obter mais informações sobre como configurar o acesso condicional para local, consulte [Configurando o acesso condicional local usando o registro do dispositivo do Active Directory do Azure](active-directory-conditional-access.md).

2. Controle de acesso toohello portal do Azure: Azure também permite que você portal de toohello de acesso de controle usando o controle de acesso baseado em função (RBAC)). Esse método permite que o valor de saudação do hello empresa toorestrict de operações que um indivíduo pode fazer no portal do Azure de saudação. Usando o portal de toohello RBAC toocontrol acesso, os administradores de TI pode delegar acesso usando Olá abordagens de gerenciamento de acesso a seguir:

* Atribuição de função com base em grupo: você pode atribuir acesso tooAzure AD grupos que podem ser sincronizados do seu Active Directory local. Isso permite que você tooleverage Olá investimentos existentes que sua organização tornou-se em ferramentas e processos para gerenciar os grupos. Você também pode usar o recurso de gerenciamento de grupo delegado de saudação do Azure AD Premium.
* Aproveite criado em funções no Azure: você pode usar três funções — tooensure proprietário e colaborador leitor, usuários e grupos têm permissão toodo somente Olá tarefas precisam toodo seus trabalhos.
* Acesso granular tooresources: você pode atribuir funções toousers e grupos para uma assinatura específica, grupo de recursos ou um recurso individual do Azure como um site ou o banco de dados. Dessa forma, você pode garantir que os usuários tenham acesso tooall Olá os recursos necessários e nenhum tooresources de acesso que eles não precisam de toomanage.

> [!NOTE]
> Se você estiver criando aplicativos e deseja controle de acesso de saudação toocustomize para eles, também é possível toouse funções de aplicativo do AD do Azure para autorização. Examine esse [WebApp-RoleClaims-DotNet exemplo](https://github.com/AzureADSamples/WebApp-RoleClaims-DotNet) sobre como toobuild toouse seu aplicativo esse recurso.
>
>

3. Acesso condicional para aplicativos do Office 365 com o Microsoft Intune: os administradores de TI podem provisionar o acesso condicional dispositivo políticas toosecure recursos corporativos, enquanto a saudação mesmo momento permitindo que operadores de informações Olá de tooaccess de dispositivos compatíveis serviços. Para mais informações, consulte [Políticas de dispositivo de acesso condicional para serviços do Office 365](active-directory-conditional-access-device-policies.md).

4. Acesso condicional para aplicativos Saas: [esse recurso](http://blogs.technet.com/b/ad/archive/2015/06/25/azure-ad-conditional-access-preview-update-more-apps-and-blocking-access-for-users-not-at-work.aspx) permite regras de acesso de autenticação multifator por aplicativo tooconfigure e Olá capacidade tooblock acesso a usuários não em uma rede confiável. Você pode aplicar Olá autenticação multifator regras tooall os usuários que recebem o aplicativo toohello ou apenas para os usuários especificados grupos de segurança. Os usuários podem ser excluídos do requisito de autenticação multifator Olá se eles estiverem acessando aplicativo hello de um endereço IP que interna em Olá rede da organização.

Como opções de saudação para controle de acesso usam uma abordagem de várias camada, a comparação entre essas opções não são aplicáveis para esta tarefa. Certifique-se de que estão utilizando todas as opções disponíveis para cada cenário que requer que você tooyour toocontrol acessar os recursos.

## <a name="define-incident-response-options"></a>Definir opções de resposta a incidentes
O AD do Azure pode ajudar IT tooidentity possível riscos de segurança no ambiente de saudação pelo monitoramento de atividade do usuário, o departamento de TI pode aproveitam o acesso do AD do Azure e relatórios de uso do recurso toogain visibilidade Olá integridade e segurança do diretório da sua organização. Com essas informações, um administrador de TI pode determinar melhor onde possíveis riscos de segurança pode para que possa planejar toomitigate adequadamente esses riscos.  [Assinatura do Azure AD Premium](active-directory-get-started-premium.md) tem um conjunto de relatórios de segurança que pode permitir a IT tooobtain essas informações. [relatórios do AD do Azure](active-directory-view-access-usage-reports.md) são categorizados como mostrado abaixo:

* **Relatórios de anomalias**: contém eventos que encontramos toobe anormais de conexão. Nosso objetivo é toomake você ciente de tais atividades e permitem que você toobe capaz de toomake uma decisão sobre se um evento é suspeito.
* **Relatórios de aplicativos integrados**: fornecem um panorama de como os aplicativos em nuvem estão sendo usados na sua organização. O Active Directory do Azure oferece integração com milhares de aplicativos em nuvem.
* **Relatórios de erros**: indicar erros que podem ocorrer durante o provisionamento de aplicativos de tooexternal de contas.
* **Relatórios específicos do usuário**: exibem dados de atividade de entrada/dispositivo de um usuário específico.
* **Logs de atividade**: contém um registro de todos os eventos auditados em Olá últimas 24 horas, últimos 7 dias ou últimos 30 dias, bem como alterações do grupo de atividade e atividade de registro e redefinição de senha.

> [!TIP]
> Outro relatório que também pode ajudar a equipe de resposta a incidentes trabalhando em um caso de Olá é hello [usuário com credenciais vazadas](http://blogs.technet.com/b/ad/archive/2015/06/15/azure-active-directory-premium-reporting-now-detects-leaked-credentials.aspx) relatório.  Esse relatório revela as correspondências entre essa lista de credenciais vazadas e seu locatário.
>
>

Outros relatórios internos importantes no AD do Azure que podem ser usados durante uma investigação de resposta a incidentes são:

* **Atividade de redefinição de senha**: fornecer ideias sobre como ativamente a redefinição de senha está sendo usada na organização Olá Olá administrador.
* **Atividade de registro de redefinição de senha**: fornece informações sobre quais usuários registraram seus métodos para redefinição de senha e quais métodos eles selecionaram.
* **Atividade de grupo**: fornece um histórico de alterações toohello grupo (ex: os usuários adicionados ou removidos) que foram iniciadas no painel de acesso de saudação.

Além disso toohello reporting multi-core disponível no Azure AD Premium que também pode ser aproveitado durante um processo de investigação de resposta a incidentes, a TI pode aproveitar informações do relatório de auditoria tooobtain como:

* Alterações na associação de função (ex: usuário adicionou a função de administrador de tooGlobal)
* Atualizações de credencial (por exemplo: alterações de senha)
* Gerenciamento de domínio (por exemplo: verificar um domínio personalizado, remover um domínio)
* Adicionando ou removendo aplicativos
* Gerenciamento de usuários (por exemplo: adição, remoção, atualização de um usuário)
* Adicionando ou removendo licenças

Como opções de saudação de resposta a incidentes usam uma abordagem de várias camada, a comparação entre essas opções não são aplicáveis para esta tarefa. Certifique-se de que você está aproveitando todas as opções disponíveis para cada cenário que requer que você toouse funcionalidade de relatório do Azure AD como parte do processo de resposta a incidentes da sua empresa.

## <a name="next-steps"></a>Próximas etapas
[Determinar tarefas de gerenciamento de identidade híbrida](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)

## <a name="see-also"></a>Consulte também
[Visão geral sobre as considerações de design](active-directory-hybrid-identity-design-considerations-overview.md)
