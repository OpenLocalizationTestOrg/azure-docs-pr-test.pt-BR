---
title: aaaSettings e perguntas Frequentes de roaming de dados | Microsoft Docs
description: "Fornece respostas toosome perguntas aos administradores de TI podem ter sobre as configurações e sincronização de dados do aplicativo."
services: active-directory
keywords: "configurações do enterprise state roaming, nuvem do windows, perguntas frequentes sobre o enterprise state roaming"
documentationcenter: 
author: tanning
manager: swadhwa
editor: curtand
ms.assetid: c0824f5c-129b-4240-969f-921f6a64eae7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 4d6d6619b3a5fbd1d274603808d89b73ed942cd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="settings-and-data-roaming-faq"></a>Configurações e perguntas frequentes sobre o roaming de dados
Este tópico responde a algumas dúvidas que os administradores de TI podem ter sobre as configurações e a sincronização de dados do aplicativo.

## <a name="what-data-roams"></a>Quais dados são movidos?
**Configurações do Windows**: Olá configurações do PC que são integradas ao sistema de operacional do Windows hello. Em geral, essas são as configurações que personalizem seu PC e incluem hello amplas categorias a seguir:

* *Tema*, que inclui recursos como configurações de tema e barra de tarefas da área de trabalho.
* *Configurações do Internet Explorer*, incluindo guias abertas recentemente e favoritos.
* *Configurações do navegador Edge*, como favoritos e lista de leitura.
* *Senhas*, incluindo senhas da Internet, perfis de Wi-Fi e outros.
* *Preferências de idioma*, que inclui configurações de layouts de teclado, idioma do sistema, data e hora e outros.
* *Recursos de facilidade de acesso*, como tema de alto contraste, Narrador e Lupa.
* *Outras configurações do Windows*, como configurações do prompt de comando e lista de aplicativos.

**Dados de aplicativo**: aplicativos universais do Windows podem gravar configurações dados tooa roaming pasta e todos os dados gravados toothis pasta serão automaticamente sincronizados. É o toodesign de desenvolvedor de aplicativos individuais toohello uma vantagem de tootake aplicativo desse recurso. Para obter mais detalhes sobre como toodevelop um aplicativo Universal do Windows que usa móveis, consulte Olá [API de armazenamento appdata](https://msdn.microsoft.com/library/windows/apps/mt299098.aspx) e hello [appdata do Windows 8 roaming blog do desenvolvedor](http://blogs.msdn.com/b/windowsappdev/archive/2012/07/17/roaming-your-app-data.aspx).

## <a name="what-account-is-used-for-settings-sync"></a>Qual conta é usada para a sincronização de configurações?
No Windows 8 e no Windows 8.1, a sincronização de configurações sempre usou as contas de consumidor da Microsoft. Usuários corporativos tinham Olá capacidade tooconnect um tootheir de conta Microsoft sincronização de toosettings acesso do toogain de conta de domínio do Active Directory. No Windows 10, essa funcionalidade de conta da Microsoft conectada está sendo substituída por uma estrutura de conta principal/secundária.

conta primária Olá é definida como Olá conta usada toosign tooWindows. Ela pode ser uma conta da Microsoft, uma conta do Azure AD (Azure Active Directory), uma conta do Active Directory local ou uma conta local. Em adição toohello primário da conta, os usuários do Windows 10 podem adicionar um ou mais dispositivos de tootheir contas de nuvem secundária. Uma conta secundária geralmente é uma conta da Microsoft, uma conta do Azure AD ou outra conta, como do Gmail ou do Facebook. Essas contas secundárias fornecem acesso tooadditional serviços como o logon único e hello da Windows Store, mas eles não são capazes de habilitação de sincronização de configurações.

No Windows 10, apenas Olá principal conta para dispositivo Olá pode ser usada para sincronização de configurações (consulte [como atualizar a partir de sincronização de configurações de conta da Microsoft na sincronização de configurações do Windows 8 tooAzure AD no Windows 10?](active-directory-windows-enterprise-state-roaming-faqs.md#how-do-i-upgrade-from-microsoft-account-settings-sync-in-windows-8-to-azure-ad-settings-sync-in-windows-10)).

Dados nunca é misto entre Olá diferentes contas de usuário no dispositivo de saudação. Há duas regras para a sincronização de configurações:

* Configurações do Windows sempre serão movido com conta primária hello.
* Dados de aplicativo serão marcados com hello conta usada tooacquire Olá aplicativo. Somente aplicativos marcados com conta primária Olá serão sincronizado. Marcação de propriedade do aplicativo é determinada quando um aplicativo é carregado no lado por meio de armazenamento do Windows hello ou gerenciamento de dispositivo móvel (MDM).

Se o proprietário do aplicativo não pode ser identificado, ele será movido com conta primária hello. Se um dispositivo é atualizado do Windows 8 ou Windows 8.1 tooWindows 10, todos os aplicativos hello serão marcados como adquirida por conta da Microsoft hello. Isso ocorre porque a maioria dos usuários adquirir aplicativos por meio de saudação da Windows Store, e não sem suporte da Windows Store para tooWindows anteriores do AD do Azure contas 10. Se um aplicativo é instalado por meio de uma licença offline, aplicativo hello será marcado usando conta primária Olá Olá dispositivo.

> [!NOTE]
> Dispositivos Windows 10 corporativos e são conectado tooAzure AD não podem se conectar a sua conta de domínio Microsoft tooa de contas. Olá capacidade tooconnect uma conta de domínio de tooa de conta Microsoft e têm a sincronização de dados do usuário Olá todos os toohello conta da Microsoft (ou seja, Olá Microsoft conta móvel por meio da conta da Microsoft hello conectado e a funcionalidade do Active Directory) é removido do Dispositivos Windows 10 que estão unida tooa conectado do Active Directory ou o ambiente do AD do Azure.
>
>

## <a name="how-do-i-upgrade-from-microsoft-account-settings-sync-in-windows-8-tooazure-ad-settings-sync-in-windows-10"></a>Como atualizar de sincronização de configurações de conta da Microsoft na sincronização de configurações do Windows 8 tooAzure AD no Windows 10?
Se você estiver toohello ingressado no domínio de Active Directory executando o Windows 8 ou Windows 8.1 com uma conta da Microsoft conectada, você sincronizará as configurações por meio de sua conta da Microsoft. Após a atualização tooWindows 10, você continuará toosync as configurações do usuário por meio da conta da Microsoft, desde que você é um usuário de domínio e domínio do Active Directory Olá não se conecta com o Azure AD.

Se Olá local domínio do Active Directory se conectar com o AD do Azure, o dispositivo tentará toosync configurações usando a conta do AD do Azure Olá conectado. Se administrador Olá AD do Azure não habilitar Enterprise Roaming de estado, o conectado conta do Azure AD irá parar a sincronização de configurações. Se você for um usuário do Windows 10 e entrar com uma identidade do Azure AD, você começará a sincronizar as configurações do Windows assim que o administrador permitir a sincronização de configurações por meio do Azure AD.

Se você armazenou os dados pessoais em seu dispositivo corporativo, você deve estar ciente de que dados de aplicativo e sistema operacional Windows começará sincronizando tooAzure AD. Isso tem Olá implicações a seguir:

* As configurações de conta pessoais do Microsoft serão descompasso além de configurações de saudação em seu trabalho ou escola contas do AD do Azure. Isso ocorre porque a conta da Microsoft hello e configurações do AD do Azure sincronizar agora estão usando contas separadas.
* Dados pessoais, como senhas de Wi-Fi, credenciais da Web e favoritos do Internet Explorer que eram sincronizados anteriormente por meio de uma conta da Microsoft conectada serão sincronizados por meio do Azure AD.

## <a name="how-do-microsoft-account-and-azure-ad-enterprise-state-roaming-interoperability-work"></a>Como funciona a conta da Microsoft e a interoperabilidade do Enterprise State Roaming do Azure AD?
No hello novembro de 2015 ou versões posteriores do Windows 10, Roaming de estado da empresa tem somente suporte para uma única conta por vez. Se você entrar no tooWindows usando um trabalho ou escola conta AD do Azure, todos os dados serão sincronizado por meio do AD do Azure. Se você entrar no tooWindows usando uma conta pessoal da Microsoft, todos os dados serão sincronizado por meio de saudação conta da Microsoft. Appdata universal será móvel usando somente Olá entrar conta primária no dispositivo hello e transitará somente se a licença do aplicativo hello pertence a conta primária hello. Appdata universal para aplicativos Olá pertencentes a todas as contas secundárias não será sincronizado.

## <a name="do-settings-sync-for-azure-ad-accounts-from-multiple-tenants"></a>As configurações das contas do AD do Azure de vários locatários são sincronizadas?
Quando o AD do Azure várias contas de diferentes locatários do AD do Azure estão Olá mesmo dispositivo, você deve atualizar toocommunicate de registro do dispositivo Olá com o Azure Rights Management (Azure RMS) para cada locatário do AD do Azure.  

1. Localize Olá GUID para cada locatário do AD do Azure. Abra Olá portal clássico do Azure e selecione um locatário do AD do Azure. Olá GUID para o locatário Olá é Olá URL na barra de endereços de saudação do seu navegador. Por exemplo: `https://manage.windowsazure.com/YourAccount.onmicrosoft.com#Workspaces/ActiveDirectoryExtension/Directory/Tenant GUID/directoryQuickStart`
2. Depois de ter Olá GUID, você precisará de chave de registro de saudação tooadd **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\SettingSync\WinMSIPC\<GUID da ID de locatário >**.
   De saudação **GUID da ID de locatário** chave, crie uma nova cadeia de caracteres múltipla value (REG-MULTI-SZ) chamada **AllowedRMSServerUrls**. Para seus dados, especifica Olá licenciamento URLs de ponto de distribuição de saudação outros locatários do Azure que Olá acessos de dispositivo.
3. Você pode encontrar hello licenciamento URLs de ponto de distribuição executando Olá **Get-AadrmConfiguration** cmdlet. Se valores Olá Olá **LicensingIntranetDistributionPointUrl** e **LicensingExtranetDistributionPointUrl** forem diferentes, especifique os dois valores. Se Olá são valores hello mesmo, especifique o valor de saudação apenas uma vez.

## <a name="what-are-hello-roaming-settings-options-for-existing-windows-desktop-applications"></a>Quais são as opções de configurações de roaming Olá para aplicativos de área de trabalho do Windows existentes?
O roaming só funciona para aplicativos Universais do Windows. Há duas opções para habilitar o roaming em um aplicativo da área de trabalho existente do Windows:

* Olá [ponte de área de trabalho](http://aka.ms/desktopbridge) ajuda você a trazer seu toohello de aplicativos de desktop do Windows existente plataforma Universal do Windows. Aqui, as alterações mínimas de código necessária tootake aproveitar roaming de dados de aplicativo do AD do Azure. Olá ponte de área de trabalho fornece seus aplicativos com uma identidade de aplicativo, que é necessário tooenable dados de aplicativo móvel para aplicativos de área de trabalho existentes.
* [UE-V (User Experience Virtualization)](https://technet.microsoft.com/library/dn458947.aspx) ajuda você a criar um modelo de configurações personalizado para aplicativos da área de trabalho existentes do Windows e habilitar o roaming para aplicativos do Win32. Essa opção não requer código de toochange de desenvolvedor de aplicativo de saudação do aplicativo hello. UE-V é limitado tooon local do Active Directory móvel para clientes que compraram Olá Microsoft Desktop Optimization Pack.

Os administradores podem configurar dados de aplicativo de área de trabalho do Windows do UE-V tooroam alterando o roaming de configurações do sistema operacional Windows e dados de aplicativo Universal por meio de [políticas de grupo do UE-V](https://technet.microsoft.com/itpro/mdop/uev-v2/configuring-ue-v-2x-with-group-policy-objects-both-uevv2), incluindo:

* Política de grupo Roaming de configurações do Windows
* Política de grupo Não sincronizar aplicativos do Windows
* Roaming na seção de aplicativos de saudação do Internet Explorer

Em Olá futuras, Microsoft pode investigar maneiras toomake QUE UE-V profundamente integrado ao Windows e estender as configurações de tooroam UE-V por meio de saudação nuvem do Azure AD.

## <a name="can-i-store-synced-settings-and-data-on-premises"></a>Posso armazenar configurações e dados sincronizados localmente?
Roaming de estado da empresa armazena todos os dados sincronizados em Olá nuvem do Azure. O UE-V oferece uma solução de roaming local.

## <a name="who-owns-hello-data-thats-being-roamed"></a>Quem possui os dados de saudação que estão sendo movidos?
as empresas de saudação próprias hello dados movidos por meio de Roaming de estado da empresa. Os dados são armazenados em um datacenter do Azure. Todos os dados de usuário são criptografados em trânsito e em repouso na nuvem hello usando o Azure RMS. Essa é uma melhoria em comparação comparada tooMicrosoft configurações baseadas na conta de sincronização, que criptografa apenas determinados dados confidenciais, como as credenciais do usuário antes de sair do dispositivo de saudação.

A Microsoft está comprometida toosafeguarding os dados do cliente. Os dados de configurações do usuário de uma empresa são automaticamente criptografados pelo Azure RMS antes de deixar um dispositivo Windows 10, para que outro usuário não possa lê-los. Se sua organização tiver uma assinatura paga do Azure RMS, você pode usar outros recursos do Azure RMS, como rastrear e revogar documentos automaticamente proteger emails que contêm informações confidenciais e gerenciar suas próprias chaves (Olá solução "Traga sua própria chave", também conhecida como BYOK). Para saber mais sobre esses recursos e sobre o funcionamento do Azure RMS, confira [O que é o Azure Rights Management](https://technet.microsoft.com/jj585026.aspx).

## <a name="can-i-manage-sync-for-a-specific-app-or-setting"></a>Posso gerenciar a sincronização para um aplicativo ou uma configuração específica?
No Windows 10, não há nenhuma configuração de MDM ou a política de grupo toodisable roaming para um aplicativo individual. Os administradores de locatários podem desabilitar a sincronização de dados de aplicativos para todos os aplicativos em um dispositivo gerenciado, mas não há controles mais refinados por aplicativo ou ao nível do aplicativo.

## <a name="how-can-i-enable-or-disable-roaming"></a>Como habilitar ou desabilitar o roaming?
Em Olá **configurações** aplicativo, vá muito**contas** > **sincronizar suas configurações**. Nessa página, você pode ver qual conta está sendo usado tooroam configurações, e você pode habilitar ou desabilitar os grupos individuais de configurações toobe movidos.

## <a name="what-is-microsofts-recommendation-for-enabling-roaming-in-windows-10"></a>Qual é a recomendação da Microsoft para habilitar o roaming no Windows 10?
A Microsoft tem algumas soluções de roaming de configurações diferentes disponíveis, incluindo Perfis de Usuário de Roaming, UE-V e Enterprise State Roaming.  A Microsoft está comprometida toomaking um investimento em estado de empresa móvel em futuras versões do Windows. Se sua organização não está pronto ou está confortável com toohello movimentação de dados na nuvem, é recomendável que você use o UE-V como a principal tecnologia móvel. Se sua organização requer suporte para aplicativos de área de trabalho do Windows existentes de roaming, mas é adiantada toomove toohello nuvem, é recomendável que você use o Roaming de estado do Enterprise e UE-V. Embora a UE-V e o Roaming de Estado da Empresa sejam tecnologias muito semelhantes, eles não são mutuamente exclusivos. Elas se complementam toohelp Certifique-se de que sua organização fornece Olá serviços que os usuários precisam de roaming.  

Ao usar o Roaming de estado da empresa e o UE-V, Olá regras a seguir se aplicam:

* Roaming de estado da empresa é o agente de roaming primário do hello no dispositivo de saudação. UE-V está sendo usado toosupplement hello "Lacuna de Win32".
* Roaming de configurações do Windows e os dados de aplicativo UWP modernos UE-V deve ser desabilitado quando usando grupo Olá UE-V políticas. Eles já estão cobertos pelo Roaming de Estado de Empresa.

## <a name="how-does-enterprise-state-roaming-support-virtual-desktop-infrastructure-vdi"></a>Como o Roaming de Estado de Empresa dá suporte ao VDI (Virtual Desktop Infrastructure)?
O Roaming de Estado de Empresa tem suporte em SKUs de cliente do Windows 10, mas não em SKUs de servidor. Se um cliente VM estiver hospedado em um computador de hipervisor e entre remotamente na máquina virtual de toohello, seus dados serão movido. Se vários usuários compartilharem Olá mesmo sistema operacional e os usuários entram remotamente no servidor tooa para uma experiência de área de trabalho completa, o roaming pode não funcionar. cenário de baseadas em sessão de Olá último não é oficialmente suportado.

## <a name="what-happens-when-my-organization-purchases-azure-rms-after-using-roaming"></a>O que acontece quando minha organização adquire o Azure RMS depois de usar o roaming?
Se sua organização já estiver usando roaming no Windows 10 com hello assinatura gratuita do Azure RMS uso limitado, comprar uma assinatura paga do Azure RMS não terá nenhum impacto sobre a funcionalidade de saudação do recurso de roaming Olá, e nenhuma alteração de configuração será exigido por seu administrador de TI.

## <a name="known-issues"></a>Problemas conhecidos
Consulte a documentação de saudação em Olá [de solução de problemas](active-directory-windows-enterprise-state-roaming-troubleshooting.md) seção para obter uma lista dos problemas conhecidos. 

## <a name="related-topics"></a>Tópicos relacionados
* [Visão geral do enterprise state roaming](active-directory-windows-enterprise-state-roaming-overview.md)
* [Habilitar o enterprise state roaming no Active Directory do Azure](active-directory-windows-enterprise-state-roaming-enable.md)
* [Política de grupo e as configurações do MDM para a sincronização de configurações](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Referência de configurações de roaming do Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [Solução de problemas](active-directory-windows-enterprise-state-roaming-troubleshooting.md)
