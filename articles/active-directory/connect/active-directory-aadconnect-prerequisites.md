---
title: "Azure AD Connect: pré-requisitos e hardware | Microsoft Docs"
description: "Este tópico descreve os pré-requisitos de saudação e requisitos de hardware de saudação do Azure AD Connect"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 91b88fda-bca6-49a8-898f-8d906a661f07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2ec8b5da9440c92e8f9d6702d5e5e20de952b588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-for-azure-ad-connect"></a>Pré-requisitos do Azure AD Connect
Este tópico descreve os pré-requisitos de saudação e requisitos de hardware de saudação do Azure AD Connect.

## <a name="before-you-install-azure-ad-connect"></a>Antes de instalar o Azure AD Connect
Antes de instalar o Azure AD Connect, aqui estão algumas coisas de que você precisará.

### <a name="azure-ad"></a>AD do Azure
* Uma assinatura do Azure ou uma [Assinatura de avaliação do Azure](https://azure.microsoft.com/pricing/free-trial/). Esta assinatura só é necessária para acessar o portal do Azure de saudação e não para o uso do Azure AD Connect. Se você estiver usando o PowerShell ou o Office 365, você não precisa toouse uma assinatura do Azure AD Connect do Azure. Se você tiver uma licença do Office 365, você também pode usar o portal de saudação Office 365. Com uma licença paga do Office 365, você também pode obter em Olá portal do Azure do portal do Office 365 de saudação.
  * Você também pode usar o hello [portal do Azure](https://portal.azure.com). Esse portal não requer uma licença do Azure AD.
* [Adicionar e verificar o domínio Olá](../active-directory-domains-add-azure-portal.md) planejar toouse no AD do Azure. Por exemplo, se você planejar toouse contoso.com para seus usuários, certifique-se este domínio foi verificado e você não estiver usando apenas domínio do hello contoso.onmicrosoft.com padrão.
* Um locatário do Azure AD pode ter, por padrão, 50 mil objetos. Quando você verificar seu domínio, o limite de Olá é too300k maior de objetos. Se você precisar de mais objetos no AD do Azure, você precisa tooopen um limite de saudação do suporte toohave caso ainda maior. Se você precisar de mais de 500 mil objetos, precisará de uma licença, como Office 365, Azure AD Básico, Azure AD Premium ou Enterprise Mobility and Security.

### <a name="prepare-your-on-premises-data"></a>Preparar seus dados locais
* Use [IdFix](https://support.office.com/article/Install-and-run-the-Office-365-IdFix-tool-f4bd2439-3e41-4169-99f6-3fabdfa326ac) tooidentify erros como duplicatas e problemas de formatação em seu diretório antes de sincronizar tooAzure AD e Office 365.
* Consulte os [recursos de sincronização opcionais que você pode habilitar no Azure AD](active-directory-aadconnectsyncservice-features.md) e avalie quais recursos você deve habilitar.

### <a name="on-premises-active-directory"></a>Active Directory local
* Olá AD esquema versão e a floresta nível funcional deve ser Windows Server 2003 ou posterior. controladores de domínio Olá podem executar qualquer versão como Olá esquema e floresta níveis requisitos sejam atendidos.
* Se desejar que o recurso de saudação toouse **write-back de senha**, Olá controladores de domínio deve ser no Windows Server 2008 (com o SP mais recente) ou posterior. Se os controladores de domínio estiverem no 2008 (pré-R2), você também deverá aplicar o [hotfix KB2386717](http://support.microsoft.com/kb/2386717).
* controlador de domínio de saudação usado pelo AD do Azure deve ser gravável. É **não tem suporte** toouse um RODC (controlador de domínio somente leitura) e o Azure AD Connect não segue qualquer redirecionamentos de gravação.
* É **não tem suporte** toouse florestas/domínios usando coloque (domínios de rótulo único) local.
* É **não tem suporte** toouse florestas/domínios usando "pontilhado" local (nome contém um ponto ".") Nomes de NetBios.
* Recomenda-se muito[habilitar a Lixeira do Active Directory de saudação](active-directory-aadconnectsync-recycle-bin.md).

### <a name="azure-ad-connect-server"></a>Servidor do Azure AD Connect
* O Azure AD Connect não pode ser instalado no Small Business Server ou no Windows Server Essentials. servidor de saudação deve estar usando o Windows Server standard ou superior.
* servidor de conectar de saudação do AD do Azure deve ter uma GUI completa instalada. É **não tem suporte** tooinstall no server core.
* O Azure AD Connect deve ser instalado no Windows Server 2008 ou posterior. Esse servidor pode ser um controlador de domínio ou um servidor membro ao usar as configurações expressas. Se você usar configurações personalizadas, o servidor de saudação também pode ser autônoma e não tem toobe tooa ingressado no domínio.
* Se você instalar o Azure Connect AD no Windows Server 2008 ou Windows Server 2008 R2, em seguida, verifique se tooapply Olá últimos hotfixes do Windows Update. instalação de saudação não é capaz de toostart com um servidor sem patch.
* Se desejar que o recurso de saudação toouse **a sincronização de senha**, deverá ser o servidor de conectar-se de saudação do AD do Azure no Windows Server 2008 R2 SP1 ou posterior.
* Se você planejar toouse um **conta de serviço gerenciado de grupo**, deverá ser o servidor de conectar-se de saudação do AD do Azure no Windows Server 2012 ou posterior.
* Olá AD do Azure Connect servidor deve ter [do .NET Framework 4.5.1](#component-prerequisites) ou posterior e [Microsoft PowerShell 3.0](#component-prerequisites) ou posterior instalado.
* servidor do Azure AD Connect Olá não deve ter a política de grupo de transcrição do PowerShell habilitada.
* Se os serviços de Federação do Active Directory está sendo implantado servidores Olá onde estão instalados do AD FS ou o Proxy de aplicativo Web devem ser Windows Server 2012 R2 ou posterior. [O gerenciamento remoto do Windows](#windows-remote-management) deve estar habilitado nesses servidores para instalação remota.
* Se o Serviços de Federação do Active Directory estiver sendo implantado, você precisará dos [Certificados SSL](#ssl-certificate-requirements).
* Se os serviços de Federação do Active Directory está sendo implantado, você precisará tooconfigure [a resolução de nome](#name-resolution-for-federation-servers).
* Se os administradores globais têm MFA habilitada, em seguida, Olá URL **https://secure.aadcdn.microsoftonline-p.com** devem estar na lista de sites confiáveis hello. Você está tooadd solicitada esta lista de sites confiáveis toohello do site quando você for solicitado um desafio MFA e ele não tenha adicionado antes. Você pode usar o Internet Explorer tooadd-tooyour confiável de sites.

### <a name="sql-server-used-by-azure-ad-connect"></a>SQL Server usado pelo Azure AD Connect
* Conexão do AD do Azure requer um dados de identidade de toostore de banco de dados do SQL Server. Por padrão, um SQL Server 2012 Express LocalDB (uma versão leve do SQL Server Express) é instalado. SQL Server Express tem um limite de tamanho de 10GB que permite a você toomanage aproximadamente 100.000 objetos. Se você precisar toomanage um maior volume de objetos de diretório, você precisa toopoint Olá instalação Assistente tooa instalação diferente do SQL Server.
* Se você usar um SQL Server separado, esses requisitos se aplicam:
  * Conexão do AD do Azure oferece suporte a todas as versões do Microsoft SQL Server do SQL Server 2008 (com o Service Pack mais recente) tooSQL Server 2016 SP1. O Banco de Dados SQL do Microsoft Azure **não tem suporte** como banco de dados.
  * Deve usar uma colação de SQL que não diferencia maiúsculas de minúsculas Esses agrupamentos são identificados com um \_CI_ no nome. É **não tem suporte** toouse um agrupamento diferencia maiusculas de minúsculas, identificado por \_CS _ em seu nome.
  * Você só pode ter um mecanismo de sincronização por instância do SQL. É **não tem suporte** tooshare um SQL da instância com a sincronização do FIM/MIM, DirSync ou do Azure AD Sync.

### <a name="accounts"></a>Contas
* Uma conta de Administrador Global do AD do Azure para o locatário de saudação do AD do Azure que você deseja toointegrate com. Essa conta deve ser uma **conta corporativa ou de estudante** e não pode ser uma **conta da Microsoft**.
* Se você usar as configurações ou a atualização expressa do DirSync, então deverá ter uma conta de Administrador Corporativo para seu Active Directory local.
* [Contas no Active Directory](active-directory-aadconnect-accounts-permissions.md) se você usar o caminho de instalação de configurações personalizadas de saudação.

### <a name="connectivity"></a>Conectividade
* Olá AD do Azure Connect servidor precisa resolução DNS da intranet e internet. Olá servidor DNS deve ser capaz de tooresolve nomes tooyour locais do Active Directory e hello pontos de extremidade do AD do Azure.
* Se você tiver firewalls em sua Intranet, e você precisar tooopen portas entre servidores de conectar-se de saudação do AD do Azure e os controladores de domínio, consulte [portas de conexão do Azure AD](active-directory-aadconnect-ports.md) para obter mais informações.
* Se o seu limite de proxy ou firewall que podem ser acessadas URLs, em seguida, Olá URLs documentados em [intervalos de endereços IP e URLs do Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) deve ser aberta.
  * Se você estiver usando Olá Microsoft Cloud na Alemanha ou na nuvem do Microsoft Azure Government de saudação, em seguida, consulte [considerações de instâncias do serviço de sincronização do Azure AD Connect](active-directory-aadconnect-instances.md) para URLs.
* Conexão do AD do Azure é por padrão usando o TLS 1.0 toocommunicate com o Azure AD. Você pode alterar esse tooTLS 1.2, seguindo as etapas de saudação em [habilitar o protocolo TLS 1.2 para o Azure AD Connect](#enable-tls-12-for-azure-ad-connect).
* Se você estiver usando um proxy de saída para conectar-se à Internet de toohello, Olá após a configuração no hello **C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config** arquivo deve ser adicionado para o Assistente de instalação Olá e do Azure AD Connect sincronização toobe capaz de tooconnect toohello da Internet e o AD do Azure. Esse texto deve ser inserido na parte inferior de saudação do arquivo hello. Nesse código, &lt;PROXYADRESS&gt; representa Olá nome de host ou endereço IP de proxy real.

```
    <system.net>
        <defaultProxy>
            <proxy
            usesystemdefault="true"
            proxyaddress="http://<PROXYADDRESS>:<PROXYPORT>"
            bypassonlocal="true"
            />
        </defaultProxy>
    </system.net>
```

* Se o servidor proxy requer autenticação, Olá [conta de serviço](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) devem estar localizados no hello domínio e você deve usar toospecify de caminho de instalação de configurações Olá personalizado um [conta de serviço personalizado](active-directory-aadconnect-get-started-custom.md#install-required-components). Também é necessário um toomachine.config alteração diferente. Com essa alteração em Machine. config, o mecanismo de assistente e sincronização de instalação de saudação responder tooauthentication solicitações do servidor de proxy de saudação. Em todas as páginas do Assistente de instalação, excluindo Olá **configurar** página saudação usuário conectado são usadas as credenciais. Em Olá **configurar** página final Olá Olá do Assistente de instalação, o contexto de saudação é comutada toohello [conta de serviço](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) que foi criado por você. seção de Machine. config Olá deve ter esta aparência.

```
    <system.net>
        <defaultProxy enabled="true" useDefaultCredentials="true">
            <proxy
            usesystemdefault="true"
            proxyaddress="http://<PROXYADDRESS>:<PROXYPORT>"
            bypassonlocal="true"
            />
        </defaultProxy>
    </system.net>
```

* Quando a conexão do AD do Azure envia uma solicitação de web tooAzure AD como parte da sincronização de diretórios, o AD do Azure pode demorar até too5 minutos toorespond. É comum para a configuração de tempo limite de ociosidade de conexão do proxy servidores toohave. Certifique-se de que a configuração de saudação é definida tooat menos de 6 minutos ou mais.

Para obter mais informações, consulte o MSDN sobre Olá [padrão proxy elemento](https://msdn.microsoft.com/library/kd3cf2ex.aspx).  
Para obter mais informações quando você tiver problemas de conectividade, consulte [Solucionar problemas de conectividade](active-directory-aadconnect-troubleshoot-connectivity.md).

### <a name="other"></a>outro
* Opcional: Uma teste usuário tooverify sincronização da conta.

## <a name="component-prerequisites"></a>Pré-requisitos do componente
### <a name="powershell-and-net-framework"></a>PowerShell e .Net Framework
O Azure AD Connect depende do Microsoft PowerShell e do .NET Framework 4.5.1. Você precisa desta versão ou de uma versão posterior instalada no seu servidor. Dependendo de sua versão do Windows Server, Olá a seguir:

* Windows Server 2012R2
  * O Microsoft PowerShell é instalado por padrão. Nenhuma ação é necessária.
  * .NET Framework 4.5.1 e versões posteriores são oferecidas pelo Windows Update. Certifique-se de que ter instalado tooWindows de atualizações mais recentes de saudação servidor Olá painel de controle.
* Windows Server 2008R2 e Windows Server 2012
  * Olá a versão mais recente do PowerShell do Microsoft está disponível em **Windows Management Framework 4.0**, disponível em [Microsoft Download Center](http://www.microsoft.com/downloads).
  * O .NET Framework 4.5.1 e versões posteriores estão disponíveis no [Centro de Download da Microsoft](http://www.microsoft.com/downloads).
* Windows Server 2008
  * a versão mais recente com suporte de saudação do PowerShell está disponível em **Windows Management Framework 3.0**, disponível em [Microsoft Download Center](http://www.microsoft.com/downloads).
  * O .NET Framework 4.5.1 e versões posteriores estão disponíveis no [Centro de Download da Microsoft](http://www.microsoft.com/downloads).

### <a name="enable-tls-12-for-azure-ad-connect"></a>Habilitar TLS 1.2 no Azure Connect AD
Conexão do AD do Azure está usando o TLS 1.0 por padrão para criptografar a comunicação entre o servidor de saudação do mecanismo de sincronização e o Azure AD hello. Você pode alterar isso ao configurar os aplicativos .net da toouse TLS 1.2 por padrão no servidor de saudação. Saiba mais sobre o TLS 1.2 em [Microsoft Security Advisory 2960358 ](https://technet.microsoft.com/security/advisory/2960358).

1. O TLS 1.2 não pode ser habilitado no Windows Server 2008. Você precisa do Windows Server 2008 R2 ou posterior. Verifique se você tem Olá .net 4.5.1 hotfix instalado em seu sistema operacional, consulte [Microsoft Security Advisory 2960358](https://technet.microsoft.com/security/advisory/2960358). É possível ter esse hotfix ou uma versão posterior já instalada no servidor.
2. Se você usar o Windows Server 2008 R2, verifique se o TLS 1.2 está habilitado. No servidor Windows Server 2012 e em versões posteriores, o TLS 1.2 já deve estar habilitado.
   ```
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2]
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client] "DisabledByDefault"=dword:00000000 "Enabled"=dword:00000001
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server] "DisabledByDefault"=dword:00000000 "Enabled"=dword:00000001
   ```
3. Para todos os sistemas operacionais, defina essa chave do registro e reinicie o servidor de saudação.
   ```
   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319
   "SchUseStrongCrypto"=dword:00000001
   ```
4. Se você também deseja tooenable TLS 1.2 entre o servidor do mecanismo de sincronização hello e um servidor SQL remoto, verifique se você tiver versões Olá necessário instaladas para [suporte a TLS 1.2 para o Microsoft SQL Server](https://support.microsoft.com/kb/3135244).

## <a name="prerequisites-for-federation-installation-and-configuration"></a>Pré-requisitos para a configuração e instalação de federação
### <a name="windows-remote-management"></a>O gerenciamento remoto do Windows
Ao usar o Azure AD Connect toodeploy os serviços de Federação do Active Directory ou hello Proxy de aplicativo Web, verifique estes requisitos:

* Se o servidor de destino de saudação ingressado no domínio, em seguida, verifique se gerenciados remotos do Windows está habilitado
  * Em uma janela Comando de PSH com privilégio elevado, use o comando `Enable-PSRemoting –force`
* Se o servidor de destino Olá é não domínio Unido máquina WAP, há alguns requisitos adicionais
  * No computador de destino da saudação (computador WAP):
    * Certifique-se de saudação winrm (gerenciamento remoto do Windows / WS-Management) serviço está em execução por meio do snap-in de serviços de saudação
    * Em uma janela Comando de PSH com privilégio elevado, use o comando `Enable-PSRemoting –force`
  * Na máquina de saudação em qual Olá o assistente está sendo executado (se o computador de destino de saudação é domínio associado ou não confiável de fora do domínio):
    * Em uma janela de comando com privilégios elevados PSH, use o comando Olá`Set-Item WSMan:\localhost\Client\TrustedHosts –Value <DMZServerFQDN> -Force –Concatenate`
    * No Gerenciador de Servidores:
      * Adicionar pool de toomachine host DMZ WAP (Gerenciador do servidor -> Gerenciar -> Adicionar servidores... use a guia DNS)
      * Guia de todos os servidores do Gerenciador de servidores: servidor WAP clique com botão direito e selecione Gerenciar como..., digite credenciais local (não de domínio) para a máquina WAP Olá
      * toovalidate PSH a conectividade remota, na guia todos os servidores do Gerenciador do servidor de saudação: servidor WAP clique com botão direito e escolha o Windows PowerShell. Abra uma sessão remota do PSH tooensure remotas sessões do PowerShell podem ser estabelecidas.

### <a name="ssl-certificate-requirements"></a>Requisitos de Certificado SSL
* É altamente recomendável toouse Olá mesmo certificado SSL em todos os nós do farm do AD FS e todos os servidores de proxy de aplicativo Web.
* saudação do certificado deve ser X509 certificado.
* Você pode usar um certificado autoassinado nos servidores da federação em um ambiente de laboratório de teste. No entanto, para um ambiente de produção, recomendamos que você obtenha o certificado de saudação de uma CA pública.
  * Se usar um certificado que não é confiável publicamente, certifique-se de certificado Olá instalado em cada servidor de Proxy de aplicativo Web é confiável no servidor de local ambos hello e em todos os servidores de Federação
* identidade de saudação do certificado de saudação deve corresponder o nome de serviço de Federação do hello (por exemplo, sts.contoso.com).
  * identidade de saudação é uma extensão de SAN (nome alternativo) de entidade do tipo dNSName ou, se não houver nenhuma entrada de SAN, o nome da entidade de saudação especificado como um nome comum.  
  * Várias entradas SAN podem estar presentes no certificado hello, desde que um deles corresponde ao nome de serviço de federação de saudação.
  * Se você estiver planejando toouse ingresso no local, um SAN adicional é necessário com o valor de saudação **enterpriseregistration.** seguido pelo sufixo de nome Principal do usuário (UPN) de saudação da sua organização, por exemplo, **enterpriseregistration.contoso.com**.
* Não há suporte para certificados com base em chaves CNG (CryptoAPI de próxima geração) e provedores de armazenamento de chaves. Isso significa que você deve usar um certificado baseado em um CSP (provedor de serviços de criptografia) e não um KSP (provedor de armazenamento de chaves).
* Há suporte para certificados curinga.

### <a name="name-resolution-for-federation-servers"></a>Resolução de nome para servidores de federação
* Configure os registros DNS para Olá nome de serviço de Federação do AD FS (por exemplo, sts.contoso.com) para intranet hello (o servidor DNS interno) e Olá extranet (DNS público por meio de seu registrador de domínio). Registro de DNS de intranet hello, certifique-se de que você use um registros e não os registros CNAME. Isso é necessário para windows autenticação toowork corretamente a partir de seu computador ingressado no domínio.
* Se você estiver implantando a mais de um servidor AD FS ou servidor de Proxy de aplicativo Web, certifique-se de que você tenha configurado o balanceador de carga e registros DNS Olá Olá AD FS federation service name (por exemplo, sts.contoso.com) ponto toohello balanceador de carga.
* Para toowork de autenticação integrada do windows para aplicativos de navegador usando o Internet Explorer em sua intranet, certifique-se de que o nome de serviço de Federação do AD FS (por exemplo, sts.contoso.com) Olá é adicionado toohello zona de intranet no Internet Explorer. Isso pode ser controlado por meio da diretiva de grupo e tooall implantado em computadores ingressados seu domínio.

## <a name="azure-ad-connect-supporting-components"></a>Componentes de suporte do Azure AD Connect
a seguir Olá é uma lista dos componentes do Azure AD Connect instalados no servidor de saudação onde o Azure AD Connect está instalado. Esta lista é para uma instalação básica do Express. Se você escolher toouse um SQL Server diferente em Olá instale a página de serviços de sincronização, em seguida, SQL Express LocalDB não está instalado localmente.

* Azure AD Connect Health
* Assistente de Conexão do Microsoft Online Services para Profissionais de TI (instalado, mas sem dependência)
* Utilitários de linha de comando do Microsoft SQL Server 2012
* LocalDB do Microsoft SQL Server 2012 Express
* Microsoft SQL Server 2012 Native Client
* Pacote de redistribuição de Microsoft Visual C++ 2013

## <a name="hardware-requirements-for-azure-ad-connect"></a>Requisitos de hardware para o Azure AD Connect
Olá tabela a seguir mostra os requisitos mínimos de Olá para o computador de sincronização de saudação do Azure AD Connect.

| Número de objetos no Active Directory | CPU | Memória | Tamanho do disco rígido |
| --- | --- | --- | --- |
| Menos de 10.000 |1,6 GHz |4 GB |70 GB |
| 10.000–50.000 |1,6 GHz |4 GB |70 GB |
| 50.000–100.000 |1,6 GHz |16 GB |100 GB |
| Para 100.000 ou mais objetos versão completa de saudação do SQL Server é necessário | | | |
| 100.000–300.000 |1,6 GHz |32 GB |300 GB |
| 300.000–600.000 |1,6 GHz |32 GB |450 GB |
| Mais de 600.000 |1,6 GHz |32 GB |500 GB |

Olá requisitos mínimos para computadores que executam o AD FS ou servidores de aplicativos Web é a seguinte hello:

* CPU: Dual-core de 1,6 GHz ou superior
* MEMÓRIA: 2 GB ou superior
* VM do Azure: Configuração A2 ou superior

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).
