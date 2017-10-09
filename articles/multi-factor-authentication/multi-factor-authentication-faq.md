---
title: "aaaAzure perguntas Frequentes de autenticação multifator | Microsoft Docs"
description: "Perguntas frequentes e respostas relacionadas tooAzure multi-Factor Authentication. O Multi-Factor Authentication é um método de verificar a identidade de um usuário que exige mais do que um nome de usuário e uma senha. Ele fornece uma camada adicional de segurança toouser entrar e transações."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 50bb8ac3-5559-4d8b-a96a-799a74978b14
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c8305cf4c41bf8e9802df192fecdb7e463eff9eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-multi-factor-authentication"></a>Perguntas frequentes sobre a Autenticação Multifator do Azure
Perguntas Frequentes respostas a perguntas comuns sobre o Azure multi-Factor Authentication e usando o serviço de autenticação multifator hello. Ele é dividido em perguntas sobre o serviço de saudação em geral, modelos, as experiências do usuário, de cobrança e solução de problemas.

## <a name="general"></a>Geral
**P: Como o Servidor Azure Multi-Factor Authentication lida com os dados do usuário?**

Com o servidor de autenticação multifator, dados de usuário são armazenados apenas em servidores de locais de saudação. Nenhum dado de usuário persistente é armazenado na nuvem hello. Quando o usuário Olá executa a verificação em duas etapas, o servidor multi-Factor Authentication envia dados toohello serviço de nuvem do Azure multi-Factor Authentication para autenticação. Comunicação entre o servidor multi-Factor Authentication e hello serviço de nuvem multi-Factor Authentication usa o protocolo (SSL) ou segurança de camada de transporte (TLS) pela porta 443 de saída.

Quando as solicitações de autenticação são enviadas toohello serviço de nuvem, os dados são coletados para autenticação e o uso de relatórios. Os campos de dados incluídos em logs de verificação em duas etapas são:

* **ID Exclusiva** (ou o nome de usuário, ou a ID do Servidor Multi-Factor Authentication local)
* **Nome e Sobrenome** (opcional)
* **Endereço de Email** (opcional)
* **Número de Telefone** (ao usar uma chamada de voz ou autenticação SMS)
* **Token de Dispositivo** (ao usar a autenticação de aplicativos móveis)
* **Modo de autenticação**
* **Resultado da autenticação**
* **Nome do Servidor Multi-Factor Authentication**
* **IP do Servidor Multi-Factor Authentication**
* **IP do Cliente** (se disponível)

os campos opcionais Olá podem ser configurados no servidor multi-Factor Authentication.

Olá resultados de verificação (sucesso ou negação) e hello motivo se ele foi negado, é armazenado com dados de autenticação de saudação. Esses dados estão disponíveis em relatórios de uso e de autenticação.

## <a name="billing"></a>Cobrança
A maioria das questões de cobrança podem ser respondidas referindo Olá tooeither [página de preços de autenticação multifator](https://azure.microsoft.com/pricing/details/multi-factor-authentication/) ou Olá documentação sobre [como tooget Azure multi-Factor Authentication](multi-factor-authentication-versions-plans.md).

**P: há minha organização cobrada para enviar chamadas hello e mensagens de texto que são usadas para autenticação?**

Não, você não seja cobrado por chamadas individuais colocadas ou mensagens de texto enviadas toousers por meio do Azure multi-Factor Authentication. Se você usar um provedor MFA por autenticação, você será cobrado para cada autenticação, mas não para o método hello usado.

Os usuários podem cobrados Olá telefonemas ou mensagens de texto recebem, serviço de telefone pessoal tootheir acordo.

**P: modelo de cobrança Olá por usuário cobrar me habilitados todos os usuários ou Olá apenas aqueles que executou a verificação em duas etapas?**

Cobrança baseia-se no número de saudação de usuários configurados toouse multi-Factor Authentication, independentemente se eles executaram a verificação em duas etapas naquele mês.

**P: Como funciona a cobrança do Multi-Factor Authentication?**

Quando você cria um provedor MFA por usuário ou por autenticação, a assinatura do Azure da sua organização é cobrada mensalmente com base no uso. Esse modelo de cobrança é semelhante toohow Azure cobra por uso de máquinas virtuais e sites.

Quando você compra uma assinatura do Azure multi-Factor Authentication, sua organização só pagará taxa de licença anual Olá para cada usuário. Licenças MFA e Office 365, Azure AD Premium ou os pacotes Enterprise Mobility + Security são cobrados dessa maneira. 

Saiba mais sobre suas opções em [como tooget Azure multi-Factor Authentication](multi-factor-authentication-versions-plans.md).

**P: Existe uma versão gratuita da Autenticação Multifator do Azure?**

Em alguns casos, sim.

Multi-Factor Authentication para administradores Azure oferece um subconjunto de recursos do Azure MFA, sem nenhum custo para acessar serviços online da tooMicrosoft, incluindo os portais de administrador do Azure e o Office 365 hello. Esta oferta só se aplica a administradores tooglobal em instâncias do Active Directory do Azure que não tem a versão completa saudação do Azure MFA por meio de uma licença MFA, um pacote ou um provedor de baseado em consumo autônomo. Se seus administradores de usam a versão gratuita hello e, em seguida, você pode comprar uma versão completa do Azure MFA, todos os administradores globais são elevado toohello paga versão automaticamente.

Autenticação multifator para usuários do Office 365 oferece um subconjunto de recursos do Azure MFA, sem nenhum custo para acessar serviços de 365 tooOffice, incluindo o Exchange Online e o SharePoint Online. Esta oferta aplica toousers que tenham uma licença do Office 365 atribuída, quando a instância correspondente saudação do Active Directory do Azure não tem a versão completa saudação do Azure MFA por meio de uma licença MFA, um pacote ou um provedor de baseado em consumo autônomo.

**P: Minha organização pode alternar entre os modelos de cobrança de consumo por usuário e por autenticação a qualquer momento?**

Se sua organização adquirir o MFA como um serviço autônomo de cobrança com base em consumo, escolha um modelo de cobrança ao criar um provedor MFA. Você não pode alterar o modelo de cobrança Olá após a criação de um provedor de MFA. No entanto, você pode excluir o provedor MFA de saudação e, em seguida, criar uma com um modelo de cobrança diferente.

Quando é criado um provedor MFA, pode ser vinculado tooan do Active Directory do Azure (também conhecido como "locatário do AD do Azure"). Se hello provedor MFA atual é vinculado tooan AD do Azure locatário, com segurança poderá excluir o provedor MFA de saudação e criar um locatário toohello vinculado mesmo Azure AD. Como alternativa, se você adquiriu suficiente MFA, o Azure AD Premium, ou o Enterprise Mobility + a segurança (EMS) licenças toocover todos os usuários que estão habilitados para MFA, você pode excluir provedor MFA de saudação completamente.

Se seu provedor MFA *não* tooan vinculado do Azure AD locatário ou vincular Olá novo MFA provedor tooa diferente do AD do Azure locatário, as configurações de usuário e opções de configuração não são transferidas. Além disso, servidores do Azure MFA existentes necessário toobe reativado usando credenciais de ativação gerados por meio de Olá novo provedor de MFA. Reativando Olá servidores MFA toolink-los toohello novo provedor de MFA não afeta a chamada telefônica e autenticação de mensagem de texto, mas o aplicativo móvel notificações irá parar de funcionar para todos os usuários até que eles reativarem o aplicativo móvel hello.

Saiba mais sobre provedores MFA em [Introdução a um provedor de Autenticação Multifator do Azure](multi-factor-authentication-get-started-auth-provider.md).

**P: Minha organização pode trocar alternar entre a cobrança baseada no consumo e assinaturas (um modelo baseado em licenças) a qualquer momento?**

Em alguns casos, sim.

Se o diretório tiver um provedor de Autenticação Multifator do Azure *por usuário*, você pode adicionar licenças do MFA. Os usuários com licenças não são contados cobrança baseado em consumo do hello por usuário. Os usuários sem licenças ainda podem ser habilitados para MFA por meio do provedor MFA de saudação. Se você comprar e atribuir licenças para todos os seus usuários configurada toouse multi-Factor Authentication, você pode excluir o provedor de autenticação multifator do Azure hello. Você sempre pode criar outro provedor MFA por usuário se você tiver mais usuários do que licenças em Olá futuras.

Se o diretório tiver um *por autenticação* provedor de autenticação multifator do Azure, você sempre é cobrados para cada autenticação, como provedor MFA de saudação é vinculado tooyour assinatura. Você pode atribuir MFA licenças toousers, mas você será ainda cobrado para cada solicitação de verificação em duas etapas, se ele é originário de uma pessoa com uma licença MFA atribuída ou não.

**P: minha organização tem toouse e sincronizar toouse identidades do Azure multi-Factor Authentication?**

Se a sua organização usa um modelo de cobrança baseado em consumo, o Azure Active Directory é opcional, mas não é necessário. Se seu provedor MFA não estiver vinculado tooan locatário do AD do Azure, você pode implantar apenas o servidor Azure multi-Factor Authentication ou Olá SDK do Azure multi-Factor Authentication local.

Active Directory do Azure é necessário para o modelo de licença Olá porque licenças são adicionadas toohello locatário de AD do Azure quando você comprar e atribuí-los toousers no diretório de saudação.

## <a name="manage-and-support-user-accounts"></a>Gerenciar e dar suporte a contas de usuário

**P: o que devo dizer aos meus toodo meus usuários se eles não recebem uma resposta em seu telefone, ou não tem seu telefone com eles?**

Espero que todos os usuários configuraram mais de um método de verificação. Diga tootry entrar novamente, mas selecione um método de verificação diferente na página de entrada hello.

Você pode apontar seu toohello usuários [guia de solução de problemas do usuário final](./end-user/multi-factor-authentication-end-user-troubleshoot.md).


**P: o que devo fazer se um dos meus usuários não é possível obter tootheir conta?**

Você pode redefinir conta saudação do usuário, tornando-os toogo pelo processo de registro de saudação novamente. Saiba mais sobre [Gerenciando as configurações de usuário e dispositivo com o Azure multi-Factor Authentication na nuvem Olá](multi-factor-authentication-manage-users-and-devices.md).

**P: o que devo fazer se um dos meus usuários perder um telefone que está usando senhas de aplicativo?**

tooprevent acesso não autorizado, excluir senhas de aplicativo do usuário Olá todos. Após o usuário Olá tem um dispositivo de substituição, eles podem recriar senhas hello. Saiba mais sobre [Gerenciando as configurações de usuário e dispositivo com o Azure multi-Factor Authentication na nuvem Olá](multi-factor-authentication-manage-users-and-devices.md).

**P: se um usuário não pode entrar em aplicativos de navegador toonon?**

Se sua organização ainda usa os clientes herdados e você [permitido o uso de saudação de senhas de aplicativo](multi-factor-authentication-whats-next.md#app-passwords), em seguida, os usuários não podem entrar em clientes herdados de toothese com seu nome de usuário e senha. Em vez disso, eles precisam muito[configurar senhas de aplicativo](./end-user/multi-factor-authentication-end-user-app-passwords.md). Os usuários devem limpar (excluir) suas informações de logon, reiniciar o aplicativo hello e entre com seu nome de usuário e *senha de aplicativo* em vez de regulares de senha.

Se sua organização não tiver clientes herdados, você não deve permitir aos usuários toocreate senhas de aplicativo.

> [!NOTE]
> Autenticação moderna para clientes do Office 2013
>
> Senhas de aplicativo são necessárias apenas para aplicativos que não suportam autenticação moderna. Clientes do Office 2013 oferece suporte aos protocolos de autenticação moderna, mas precisam toobe configurado. Os clientes do Office mais recentes automaticamente dão suporte a protocolos de autenticação moderna. Para obter mais informações, consulte Olá [comunicado de visualização pública de autenticação moderna do Office 2013](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).

**P: meu usuários dizem que, às vezes, eles não receberem a mensagem de texto de saudação ou responder a mensagens de texto de forma tootwo mas tempo limite da verificação de saudação.**

Entrega de mensagens de texto e o recebimento de respostas do SMS bidirecional não têm garantia porque há incontroláveis fatores que podem afetar a confiabilidade de saudação do serviço de saudação. Esses fatores incluem país de destino hello, operadora de celular hello e sinal hello.

Se os usuários geralmente têm problemas com confiável receber mensagens de texto, informe toouse móvel chamada telefônica ou aplicativo método hello em vez disso. aplicativo móvel Olá pode receber notificações tanto sobre conexões Wi-Fi e de celular. Além disso, o aplicativo móvel Olá pode gerar códigos de verificação mesmo quando o dispositivo de saudação não tem nenhum sinal em todos os. Olá Microsoft Authenticator aplicativo está disponível para [Android](http://go.microsoft.com/fwlink/?Linkid=825072), [IOS](http://go.microsoft.com/fwlink/?Linkid=825073), e [do Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071).

Se você precisa usar mensagens de texto, é recomendável usar SMS unidirecional em vez de SMS bidirecional, quando possível. SMS unidirecional é mais confiável e impede que os usuários incorrer em encargos SMS internacionais de mensagem de texto tooa respondem que foi enviada de outro país.

**P: posso alterar quantidade Olá que meus usuários têm o código de verificação de saudação tooenter de uma mensagem de texto antes do sistema Olá tempo limite de tempo?**

Em alguns casos, Sim. 

Para o SMS unidirecional versão 7.0 do servidor Azure MFA ou superior, você pode configurar tempo limite de saudação configuração definindo uma chave do registro. Após Olá serviço de nuvem MFA envia a mensagem de texto de saudação, o código de verificação de hello (ou a senha de uso único) é retornada toohello servidor MFA. Olá servidor MFA armazena o código de saudação na memória para 300 segundos por padrão. Se o usuário Olá não insira o código de saudação antes de saudação 300 segundos, a autenticação é negada. Use essas etapas toochange Olá tempo limite padrão de configuração:

1. Vá tooHKLM\Software\Wow6432Node\Positive Networks\PhoneFactor.
2. Criar uma chave de Registro DWORD chamada **pfsvc_pendingSmsTimeoutSeconds** e defina o tempo de saudação em segundos que você deseja que senhas de uso únicas Olá servidor Azure MFA toostore.

>[!TIP] 
>Se você tiver vários servidores de MFA, somente Olá aquele processado a solicitação de autenticação original Olá sabe código de verificação de saudação enviada toohello usuário. Quando o usuário Olá insere o código de hello, Olá toovalidate de solicitação de autenticação devem ser enviada toohello mesmo servidor. Se a validação de código Olá for enviada tooa outro servidor, autenticação de saudação é negada. 

Para o SMS bidirecional com o servidor Azure MFA, você pode definir a configuração de tempo limite de Olá no Portal de gerenciamento de MFA de saudação. Se os usuários não responder toohello SMS dentro do período de tempo limite definido do hello, a autenticação será negada. 

Para o SMS unidirecional com o Azure MFA na nuvem hello (incluindo Olá extensão de servidor de políticas de rede de adaptador ou hello do AD FS), você não pode configurar a configuração de tempo limite de saudação. AD do Azure armazena o código de verificação de saudação de 180 segundos. 

**P: Posso usar tokens de hardware com o Servidor Multi-Factor Authentication?**

Se estiver usando o Servidor de Autenticação Multifator, você poderá importar tokens de terceiros com TOTP (senha de uso único) baseados no tempo OATH (Autenticação Aberta) e usá-los com a verificação em duas etapas.

Você pode usar os tokens de ActiveIdentity que são tokens de OATH TOTP, se você colocar a chave secreta Olá em um arquivo CSV e importar tooAzure servidor multi-Factor Authentication. Você pode usar tokens OATH com serviços de Federação do Active Directory (ADFS), autenticação baseada em formulários de servidor de informações da Internet (IIS) e remoto Authentication Dial-In RADIUS (User Service) como sistema de saudação do cliente pode aceitar a entrada do usuário hello.

Você pode importar tokens OATH TOTP de terceiros com hello formatos a seguir:  

- PSKC (Contêiner Portátil de Chave Simétrica)  
- Se o arquivo hello contém um número de série, uma chave de segredo no formato Base 32 e um intervalo de tempo CSV  

**P: posso usar os serviços de Terminal do servidor Azure multi-Factor Authentication toosecure?**

Sim, mas se você estiver usando o Windows Server 2012 R2 ou posterior apenas você pode proteger os serviços de Terminal usando a área de trabalho remota (Gateway RD).

Alterações de segurança no Windows Server 2012 R2 alterado como o servidor Azure multi-Factor Authentication se conecta toohello pacote de segurança autoridade de segurança Local (LSA) no Windows Server 2012 e versões anteriores. Para versões dos Serviços de Terminal no Windows Server 2012 ou anteriores, você pode [proteger um aplicativo com a Autenticação do Windows](multi-factor-authentication-get-started-server-windows.md#to-secure-an-application-with-windows-authentication-use-the-following-procedure). Se estiver usando o Windows Server 2012 R2, você precisará do RD Gateway.

**P: Eu configurei um ID do Chamador no Servidor MFA, mas os usuários ainda recebem chamadas de Autenticação Multifator de um chamador anônimo.**

Quando as chamadas de autenticação multifator são colocadas por meio da rede de telefonia pública hello, às vezes, são roteadas por meio de uma operadora que não oferece suporte a identificação do chamador. Por isso, ID de chamadas não é garantida, embora Olá sistema de autenticação multifator sempre envia.

**P: por que meus usuários sendo solicitado tooregister suas informações de segurança?**
Há vários motivos que os usuários podem ser solicitada tooregister suas informações de segurança:

- usuário de saudação foi habilitado para MFA pelo administrador no AD do Azure, mas não tem informações de segurança ainda registradas para sua conta.
- Olá usuário foi habilitado para autoatendimento redefinição de senha no AD do Azure. informações de segurança Olá ajudá-lo a redefinir sua senha no futuro de saudação se ele esquecerem.
- usuário de saudação acessou um aplicativo que tem uma política de acesso condicional toorequire MFA e não foi registrado anteriormente para MFA.
- usuário de saudação está registrando um dispositivo com o Azure AD (incluindo a junção do Azure AD) e sua organização exigir MFA para registro do dispositivo, mas usuário Olá não foi registrado anteriormente para MFA.
- usuário Hello está gerando o Windows Hello para empresas no Windows 10 (que exige MFA) e não foi registrado anteriormente para MFA.
- organização de saudação criou e habilitado uma política de MFA de registro que tenha sido aplicado toohello usuário.
- usuário Olá anteriormente registrado para MFA, mas escolher um método de verificação que um administrador como desabilitado. usuário Hello, portanto, deve passar pelo registro MFA tooselect novamente um novo método de verificação padrão.


## <a name="errors"></a>Errors
**P: o que os usuários deverão fazer se receberem uma mensagem de erro "A solicitação de autenticação não é para uma conta ativada" ao usar notificações de aplicativo móvel?**

Diga toofollow tooremove esse procedimento sua conta do aplicativo móvel do hello, em seguida, adicioná-lo novamente:

1. Vá muito[seu perfil no portal do Azure](https://account.activedirectory.windowsazure.com/profile/) e entre com sua conta organizacional.
2. Escolha **Verificação de Segurança Adicional**.
3. Remova conta existente de saudação do aplicativo móvel hello.
4. Clique em **configurar**e, em seguida, siga o aplicativo móvel do Olá Olá instruções tooreconfigure.

**P: o que os usuários devem fazer se eles veem uma mensagem de erro 0x800434D4L ao entrar no aplicativo de navegador não tooa?**

Olá 0x800434D4L ocorre quando você tentar toosign no aplicativo de navegador não tooa, instalado em um computador local, o que não funciona com contas que requerem a verificação em duas etapas.

Uma solução alternativa para esse erro é toohave separado contas de usuário relacionadas à administração e operações não administrativas. Posteriormente, você pode vincular caixas de correio entre sua conta de administrador e a conta não administrativa para que você pode entrar no tooOutlook usando sua conta não administrativa. Para obter mais detalhes sobre esta solução, Aprenda como muito[dar um Olá administrador capacidade tooopen e exibição Olá conteúdo da caixa de correio do usuário](http://help.outlook.com/141/gg709759.aspx?sl=1).

## <a name="next-steps"></a>Próximas etapas
Se sua pergunta não é respondida aqui, deixe-nos comentários Olá final Olá Olá página. Ou então, aqui estão algumas opções adicionais para obter ajuda:

* Saudação de pesquisa [Base de dados de Conhecimento Microsoft](https://www.microsoft.com/en-us/Search/result.aspx?form=mssupport&q=phonefactor&form=mssupport) para problemas técnicos de toocommon de soluções.
* Procurar e navegue perguntas e respostas de comunidade Olá técnicas ou fazer sua pergunta em Olá [fóruns do Active Directory do Azure](https://social.msdn.microsoft.com/Forums/azure/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).
* Se você é um cliente herdado do PhoneFactor e você tiver dúvidas ou precisa de ajuda para redefinir uma senha, use Olá [de redefinição de senha](mailto:phonefactorsupport@microsoft.com) link tooopen um caso de suporte.
* Entre em contato com um profissional de suporte por meio do [suporte do Servidor de Autenticação Multifator do Azure (PhoneFactor)](https://support.microsoft.com/oas/default.aspx?prid=14947). Ao entrar em contato conosco, é útil incluir o máximo possível de informações sobre o problema. Você pode fornecer as informações incluem página Olá onde você viu o erro hello, código de erro específico do hello, ID de sessão específica de saudação e ID de saudação do usuário de saudação que viu o erro de saudação.
