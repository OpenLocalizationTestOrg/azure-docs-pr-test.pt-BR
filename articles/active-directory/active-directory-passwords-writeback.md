---
title: SSPR do Azure AD com write-back de senha | Microsoft Docs
description: Usando o AD do Azure e o Azure AD directory do Connect toowriteback senhas tooon local
services: active-directory
keywords: "Gerenciamento de senha do Active Directory, gerenciamento de senha, autoatendimento de redefinição de senha do Azure AD"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 6a1dd964a51b4f3b5b0be303b722ab6deb4a6110
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="password-writeback-overview"></a>Visão geral de write-back de senha

Write-back de senha permite que você tooconfigure AD do Azure toowrite senhas fazer tooyou do Active Directory local. Ele remove Olá necessidade tooset backup e gerenciar uma solução de redefinição de senha de autoatendimento complicadas no local, e ele fornece uma maneira conveniente de baseado em nuvem para seu usuários tooreset suas senhas no local onde quer que eles estejam. O write-back de senha é um componente do [Azure Active Directory Connect](./connect/active-directory-aadconnect.md) que pode ser habilitado e usado pelos assinantes atuais das [Edições do Azure Active Directory](active-directory-editions.md) Premium.

Write-back de senha fornece Olá recursos a seguir

* **Comentários sem atraso** – o write-back de senha é uma operação síncrona. Os usuários são notificados imediatamente se sua senha não atendeu à política ou foi toobe não é possível redefinir ou alterado por qualquer motivo.
* **Dá suporte à redefinição de senhas de usuários usando AD FS ou outras tecnologias da federação** -com write-back de senha, como hello contas de usuários federados são sincronizadas no seu locatário do AD do Azure, eles são toomanage capaz de seu AD local senhas da nuvem de saudação.
* **Dá suporte à redefinição de senhas de usuários usando [sincronização de hash de senha](./connect/active-directory-aadconnectsync-implement-password-synchronization.md)**  - quando o serviço de redefinição de senha Olá detecta que uma conta de usuário sincronizada está habilitada para sincronização de hash de senha, redefinimos ambos esta conta local e a senha de nuvem simultaneamente.
* **Oferece suporte à alteração de senhas de saudação acessar o painel e o Office 365** - quando federado ou senha sincronizada usuários vêm toochange suas senhas expiradas ou não expiradas, escrevemos o ambiente de tooyour back AD local essas senhas.
* **Oferece suporte à gravação de senhas quando um administrador redefini-las de Olá portal do Azure** - sempre que um administrador redefine uma senha de usuário no hello [portal do Azure](https://portal.azure.com), se esse usuário for federado ou sincronizados com senha, vamos definir Olá senha Olá administrador seleciona no AD local, também. Isso não é suportado atualmente no Portal de administração do Office de hello.
* **Impõe seu local políticas de senha AD** - quando um usuário redefine sua senha, certificamos de que ele atende aos seus locais política antes de confirmá-la toothat diretório do AD. Isso inclui histórico, complexidade, tempo, filtros de senha e qualquer outra restrição de senha que você tenha definido no AD local.
* **Não requer quaisquer regras de firewall de entrada** -write-back de senha usa um relé do barramento de serviço do Azure como um canal de comunicação subjacente, que significa que você não tem tooopen portas de entrada no firewall para esse recurso toowork.
* **Sem suporte em contas de usuário existentes em grupos protegidos no Active Directory local** – para obter mais informações sobre grupos protegidos, consulte [Contas e grupos protegidos no Active Directory](https://technet.microsoft.com/library/dn535499.aspx).

## <a name="how-password-writeback-works"></a>Como funciona o write-back de senha

Quando um hash de senha ou federado sincronizada usuário vem tooreset ou alterar sua senha na nuvem Olá, Olá seguinte acontece:

1. Verificamos toosee tem o tipo de usuário de saudação de senha.
    * Quando virmos que a senha de saudação é gerenciada no local
        * Verificamos se hello serviço de write-back está ativo e em execução, se estiver, permitimos que usuário Olá continuar
        * Se o serviço de write-back de saudação não estiver disponível, informamos usuário Olá sua senha não pode ser redefinida agora
2. Em seguida, usuário Olá passa portões de autenticação apropriado hello e atinge a tela do hello redefinição de senha.
3. usuário Olá seleciona uma nova senha e confirma isso.
4. Após clicar em enviar, podemos criptografar a senha de texto sem formatação Olá com uma chave simétrica que foi criada durante o processo de instalação de write-back de saudação.
5. Após criptografar a senha hello, podemos incluí-la em uma carga que seja enviada por uma retransmissão de barramento de serviço específico do locatário HTTPS canal tooyour (que também configuramos para você durante o processo de instalação de write-back de saudação). Esta retransmissão é protegida por uma senha gerada aleatoriamente que somente a sua instalação local sabe.
6. Depois que a mensagem de saudação atinge o barramento de serviço, hello ponto de extremidade de redefinição de senha automaticamente reativado e vê que tem uma solicitação de redefinição pendente.
7. Olá serviço procurará usuário Olá em questão usando o atributo de âncora de nuvem hello. Para este toosucceed de pesquisa:

    * o objeto de usuário Olá deve existir no hello espaço do conector AD
    * o objeto de usuário Olá deve ser objeto MV correspondente de toohello vinculado
    * objeto de usuário de saudação deve ser vinculado toohello objeto do conector AAD correspondente.
    * Hello link de tooMV de objeto de conector AD deve ter regras de sincronização de saudação `Microsoft.InfromADUserAccountEnabled.xxx` no link de saudação. <br> <br>
    Quando chamada hello vem da nuvem Olá, usos de mecanismo de sincronização de saudação Olá toolook do atributo cloudAnchor o objeto de espaço do conector Olá AAD, segue o objeto de MV Olá link toohello voltar e segue toohello back AD objeto do link de saudação. Como pode haver vários objetos AD (várias florestas) para Olá depende do mesmo usuário, o mecanismo de sincronização Olá Olá `Microsoft.InfromADUserAccountEnabled.xxx` saudação do link toopick corrija uma.

    > [!Note]
    > Como resultado, essa lógica do Azure AD Connect deve ser capaz de toocommunicate com hello emulador PDC para toowork de write-back de senha. Se você precisar tooenable nesse manualmente, você pode se conectar do Azure AD Connect toohello emulador PDC clicando em Olá **propriedades** do conector de sincronização do Active Directory hello, selecionando **configurar partições de diretório**. A partir daí, procure Olá **configurações de conexão do controlador de domínio** seção e marque a caixa de saudação intitulada **usam somente controladores de domínio preferencial**. Mesmo se Olá preferencial que DC não é um emulador de PDC, o Azure AD Connect tentará tooconnect toohello PDC para write-back de senha.

8. Depois que a conta de usuário de saudação for encontrada, tentarmos senha de saudação tooreset diretamente na floresta do AD apropriada hello.
9. Se a operação de definição de senha Olá for bem-sucedida, informamos usuário Olá que sua senha foi alterada.
    > [!NOTE]
    > No caso de Olá quando Olá a senha de usuário é sincronizada tooAzure AD usando a sincronização de senha, há uma possibilidade de que a política de senha de local de saudação é mais fraca que a política de senha de nuvem hello. Nesse caso, estamos ainda impor qualquer política de local de saudação é e, em vez disso, Permitir senha hash de saudação de toosynchronize de sincronização de hash de senha. Isso garante que a diretiva local é imposta em nuvem hello, não importa se você usar tooprovide de Federação ou sincronização de senha logon único.

10. Se senha Olá definido haverá falha na operação, podemos retornar Olá erro toohello usuário e deixaremos que ele tente novamente.
    * Olá operação pode falhar devido à seguinte Olá
        * Olá serviço foi desativado
        * senha de saudação selecionadas não atendeu as políticas da organização
        * Não foi possível encontrar usuário Olá no hello AD local

    Temos uma determinada mensagem para muitos desses casos e informar o usuário de saudação eles podem fazer tooresolve problema de saudação.

## <a name="configuring-password-writeback"></a>Configurando o write-back de senha

É recomendável que você use o recurso de atualização automática de saudação do [do Azure AD Connect](./connect/active-directory-aadconnect-get-started-express.md) se você quiser que o write-back de senha toouse.

DirSync e Azure AD Sync não estão mais meio com suporte da habilitação do artigo de saudação do Write-back de senha [atualizar do DirSync e Azure AD Sync](connect/active-directory-aadconnect-dirsync-deprecated.md) tem mais toohelp de informações com a transição.

Olá passos abaixo supõem que você já tenha configurado o Azure AD Connect em seu ambiente usando Olá [Express](./connect/active-directory-aadconnect-get-started-express.md) ou [personalizado](./connect/active-directory-aadconnect-get-started-custom.md) configurações.

1. tooconfigure e habilitar write-back de senha faça logon no servidor do tooyour do Azure AD Connect e inicie Olá **do Azure AD Connect** Assistente de configuração.
2. Na tela de boas-vindas Olá clique **configurar**.
3. Em Olá adicionais tarefas tela clique **personalizar opções de sincronização** e, em seguida, escolha **próximo**.
4. Na tela de tooAzure AD Connect hello, insira uma credencial de Administrador Global e escolha **próximo**.
5. Em Olá conectar seus diretórios e o domínio e UO filtragem telas que você pode escolher **próximo**.
6. Na tela de recursos opcionais de saudação caixa de seleção Olá Avançar muito**write-back de senha** e clique em **próximo**.
   ![Habilitar write-back de senha no Azure AD Connect][Writeback]
7. Na tela de tooconfigure pronto do hello clique **configurar** e aguarde Olá processo toocomplete.
8. Ao visualizar Configuração concluída, clique em **Sair**

## <a name="licensing-requirements-for-password-writeback"></a>Requisitos de licenciamento do write-back de senha

Para obter informações sobre licenciamento, consulte o tópico de saudação [licenças necessárias para write-back de senha](active-directory-passwords-licensing.md#licenses-required-for-password-writeback) ou Olá sites a seguir

* [Site de Preços do Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/)
* [Enterprise Mobility + Security](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [Secure Productive Enterprise](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

### <a name="on-premises-authentication-modes-supported-for-password-writeback"></a>Modos de autenticação locais com suporte para write-back de senha

Write-back de senha funciona para Olá seguintes tipos de senha do usuário:

* **Usuários somente de nuvem**: o write-back de senha não se aplica nesse caso, pois não há uma senha local
* **Usuários sincronizados com senha**: write-back de senha com suporte
* **Usuários federados**: suporte para write-back de senha
* **Usuários de autenticação de passagem**: suporte para write-back de senha

### <a name="user-and-admin-operations-supported-for-password-writeback"></a>Operações de administrador e usuário com suporte para write-back de senha

As senhas são gravadas no hello todas as situações a seguir:

* **Operações do usuário final com suporte**
  * Qualquer operação de alteração de senha voluntária de autoatendimento do usuário final
  * Qualquer operação para forçar o autoatendimento de alteração de senha do usuário final (por exemplo, expiração de senha)
  * Qualquer senha de autoatendimento do usuário final redefinir provenientes de saudação [Portal de redefinição de senha](https://passwordreset.microsoftonline.com)
* **Operações do administrador com suporte**
  * Qualquer operação de alteração de senha voluntária de autoatendimento do administrador
  * Qualquer operação para forçar o autoatendimento de alteração de senha do administrador (por exemplo, expiração de senha)
  * Provenientes de saudação de redefinição de senha de autoatendimento qualquer administrador [Portal de redefinição de senha](https://passwordreset.microsoftonline.com)
  * Qualquer iniciadas pelo administrador do usuário final redefinição de senha do hello [portal clássico do Azure](https://manage.windowsazure.com)
  * Qualquer iniciadas pelo administrador do usuário final redefinição de senha do hello [portal do Azure](https://portal.azure.com)

### <a name="user-and-admin-operations-not-supported-for-password-writeback"></a>Operações de administrador e usuário sem suporte para write-back de senha

As senhas são **não** escrito em qualquer uma das seguintes situações de saudação:

* **Operações do usuário final sem suporte**
  * Qualquer usuário final redefinir suas próprias senhas usando o PowerShell v1, v2 ou hello Azure AD Graph API
* **Operações do administrador sem suporte**
  * Qualquer iniciadas pelo administrador do usuário final redefinição de senha do hello [portal de gerenciamento do Office](https://portal.office.com)
  * Qualquer iniciadas pelo administrador do usuário final redefinição de senha do PowerShell v1, v2 ou hello Azure AD Graph API

Enquanto estamos trabalhando tooremove essas limitações, não temos um cronograma específico que compartilhar ainda.

## <a name="password-writeback-security-model"></a>Modelo de segurança de write-back de senha

O write-back de senha é um serviço altamente seguro.  tooensure que suas informações estejam protegidas, habilitamos um modelo de segurança de 4 camadas que é descrito abaixo.

* **Retransmissão do barramento de serviço específica ao locatário**
  * Quando você configura o serviço de hello, configuramos uma retransmissão de barramento de serviço específico do locatário que é protegida por uma senha forte gerada aleatoriamente que Microsoft nunca tem acesso.
* **Chave de criptografia de senha criptograficamente forte e bloqueada**
  * Após a criação de retransmissão de barramento de serviço hello, criamos uma chave simétrica forte, use tooencrypt Olá senha durante a transmissão de saudação. Essa chave reside somente no armazenamento secreto da sua empresa na nuvem hello, que é extremamente bloqueada e auditado, assim como qualquer senha no diretório de saudação.
* **TLS padrão da indústria**
  1. Quando uma senha redefinir ou alterar operação ocorre na nuvem hello, podemos levar a senha de texto sem formatação hello e criptografá-la com sua chave pública.
  2. Em seguida, colocamos que em uma mensagem HTTPS, que é enviada por um canal criptografado usando a retransmissão de barramento de serviço do Microsoft SSL certificados tooyour.
  3. Após a mensagem de saudação chega no barramento de serviço, o agente local é ativado para cima e autentica usando o barramento tooService Olá senha forte gerada anteriormente.
  4. Agente local pega a mensagem de saudação criptografada, descriptografa usando a chave privada de saudação gerada.
  5. Agente de local, em seguida, tente tooset senha Olá Olá API do AD DS SetPassword.
     * Esta etapa é o que permite tooenforce seu AD local (complexidade, idade, histórico, filtros, etc.) de diretiva de senha na nuvem hello.
* **Políticas de expiração de mensagem** 
  * Se a mensagem de saudação se encontra no barramento de serviço porque o serviço no local está inativo, ele perderá a validade e ser removido após vários minutos tooincrease ainda mais a segurança.

### <a name="password-writeback-encryption-details"></a>Detalhes de criptografia de write-back de senha

etapas de criptografia Olá passa de uma solicitação de redefinição de senha por depois que um usuário envia, antes de chegar no seu ambiente local, de tooensure serviço máximo confiabilidade e segurança são descritas abaixo.

* **Etapa 1: criptografia de senha com a chave RSA de 2048 bits** - uma vez que um usuário envia um toobe senha gravado tooon, primeiro, Olá enviado senha local em si é criptografado com uma chave RSA de 2048 bits.
* **Etapa 2 - criptografia de nível de pacote com AES-GCM** - então Olá todo o pacote (senha + metadados necessários) é criptografado usando AES-GCM. Isso impede que qualquer pessoa com o canal de barramento de serviço subjacente do acesso direto toohello exibindo/violação com conteúdo hello.
* **Etapa 3 - toda a comunicação ocorre por TLS / SSL** -todas as comunicações de saudação com barramento de serviço ocorre em um canal SSL/TLS. Isso protege o conteúdo de saudação do 3º autorizadas.
* **Substituição da chave automática a cada seis meses** - automaticamente a cada 6 meses, ou sempre que o write-back de senha está desabilitada ou habilitada novamente no Azure AD Connect, podemos substituição todas essas chaves de segurança de serviço máximo de tooensure e segurança.

### <a name="password-writeback-bandwidth-usage"></a>Uso de largura de banda de write-back de senha

Write-back de senha é um serviço de baixa largura de banda que envia solicitações de agente de local toohello somente sob Olá circunstâncias a seguir para trás:

1. Duas mensagens enviadas ao ativar ou desativar o recurso de saudação por meio do Azure AD Connect.
2. Uma mensagem é enviada uma vez a cada cinco minutos como uma pulsação de serviço para como Olá serviço está em execução.
3. Duas mensagens são enviadas sempre que uma nova senha é enviada
    * Primeira mensagem, como uma operação de saudação do tooperform de solicitação
    * Segunda mensagem, que contém o resultado de saudação da operação de saudação e é enviada em Olá circunstâncias a seguir:
        * Sempre que uma nova senha é enviada durante uma redefinição de senha de autoatendimento do usuário.
        * Sempre que uma nova senha é enviada durante uma operação de alteração de senha do usuário.
        * Cada vez que uma nova senha é enviada durante uma usuário iniciada pelo administrador de redefinição de senha (do portais do Azure admin do hello somente).

#### <a name="message-size-and-bandwidth-considerations"></a>Considerações sobre a largura de banda e o tamanho da mensagem

Olá tamanho de cada mensagem de saudação descrita acima normalmente é em 1 kb, mesmo sob cargas extremas, serviço de write-back de senha Olá em si está consumindo alguns quilobits por segundo de largura de banda. Como cada mensagem é enviada em tempo real, somente quando necessário por uma operação de atualização de senha e como o tamanho da mensagem de saudação é tão pequeno, uso de largura de banda de saudação do recurso de write-back de saudação efetivamente é muito pequeno toohave qualquer impacto mensurável real.

## <a name="next-steps"></a>Próximas etapas

Olá links a seguir fornece informações adicionais sobre a redefinição de senha usando o AD do Azure

* [**Início Rápido**](active-directory-passwords-getting-started.md): comece agora mesmo a usar o gerenciamento de autoatendimento de senhas do Azure AD 
* [**Licenciamento** ](active-directory-passwords-licensing.md) - Configuração do licenciamento do Azure AD
* [**Dados** ](active-directory-passwords-data.md) - entender dados Olá necessários e como ele é usado para gerenciamento de senha
* [**Distribuição** ](active-directory-passwords-best-practices.md) -planejar e implantar os usuários de tooyour SSPR usando Olá diretrizes encontradas aqui
* [**Personalizar** ](active-directory-passwords-customize.md) -personalizar Olá aparência de saudação SSPR experiência para sua empresa.
* [**Política** ](active-directory-passwords-policy.md) - Como entender e definir políticas de senha do Azure AD
* [**Relatórios**](active-directory-passwords-reporting.md): descubra se, quando e onde os usuários estão acessando a funcionalidade SSPR
* [**Mergulho profundo técnica** ](active-directory-passwords-how-it-works.md) -vá atrás Olá cortina toounderstand como ele funciona
* [**Perguntas frequentes**](active-directory-passwords-faq.md): como? Por quê? O quê? Onde? Quem? Quando? -Respostas tooquestions você sempre quis tooask
* [**Solucionar problemas de** ](active-directory-passwords-troubleshoot.md) -Saiba como problemas comuns de tooresolve que vemos com SSPR

[Writeback]: ./media/active-directory-passwords-writeback/enablepasswordwriteback.png "Habilitar write-back de senha no Azure AD Connect"
