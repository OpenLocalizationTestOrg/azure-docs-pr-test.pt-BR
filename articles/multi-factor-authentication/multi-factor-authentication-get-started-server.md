---
title: aaaGetting Iniciar servidor Azure multi-Factor Authentication | Microsoft Docs
description: "Esta é hello Azure multi-factor authentication página que descreve como tooget iniciada com o servidor Azure MFA."
services: multi-factor-authentication
keywords: "servidor de autenticação, página de ativação de aplicativo de autenticação multifator do azure, download de servidor de autenticação"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: e94120e4-ed77-44b8-84e4-1c5f7e186a6b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 92a6a586eb96375e92a9455ad64e67221001db81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-multi-factor-authentication-server"></a>Guia de Introdução com hello servidor Azure multi-Factor Authentication

<center>![MFA local](./media/multi-factor-authentication-get-started-server/server2.png)</center>

Agora que determinamos toouse servidor multi-Factor Authentication local, vamos começar. Esta página aborda uma nova instalação do servidor de saudação e configurá-lo com o Active Directory no local. Se você já Olá MFA server está instalado e estiver buscando tooupgrade, consulte [toohello de atualização mais recente do Azure multi-Factor Authentication Server](multi-factor-authentication-server-upgrade.md). Se você estiver procurando informações sobre como instalar apenas o Olá web serviço, consulte [Olá implantar aplicativo da Web serviço do Azure multi-Factor Authentication Server Mobile](multi-factor-authentication-get-started-server-webservice.md).

## <a name="plan-your-deployment"></a>Planejar sua implantação

Antes de baixar Olá servidor Azure multi-Factor Authentication, considere quais são seus requisitos de alta disponibilidade e carga. Use este toodecide informações sobre como e onde toodeploy.

Uma boa diretriz para a quantidade de saudação de memória necessária é o número de saudação de usuários esperado tooauthenticate regularmente.

| Usuários | RAM |
| ----- | --- |
| 1-10,000 | 4 GB |
| 10,001-50,000 | 8 GB |
| 50,001-100,000 | 12 GB |
| 100,000-200,001 | 16 GB |
| 200,001+ | 32 GB |

Você precisa tooset backup de vários servidores para alta disponibilidade ou o balanceamento de carga? Há uma série de maneiras tooset esta configuração com o servidor Azure MFA. Quando você instala seu primeiro servidor MFA do Azure, ele se torna mestre hello. Quaisquer servidores adicionais se tornam subordinadas e sincronizam automaticamente os usuários e a configuração com o mestre de saudação. Em seguida, você pode configurar um servidor primário e fazer com que o restante da saudação atuar como backup, ou você pode configurar o balanceamento de carga entre todos os servidores de saudação.

Quando um servidor Azure MFA mestre fica offline, os servidores subordinados Olá ainda podem processar solicitações de verificação em duas etapas. No entanto, você não pode adicionar novos usuários e os usuários existentes não podem atualizar suas configurações até que o mestre de saudação está novamente online ou subordinada é promovida.

### <a name="prepare-your-environment"></a>Prepare o seu ambiente

Verifique se servidor de saudação que você está usando para o Azure multi-Factor Authentication atende Olá requisitos a seguir:

| Requisitos do Servidor de Autenticação Multifator do Azure | Descrição |
|:--- |:--- |
| Hardware |<li>200 MB de espaço em disco rígido</li><li>processador compatível com x32 ou x64</li><li>1 GB ou mais de RAM</li> |
| Software |<li>Windows Server 2008 ou superior se o host de saudação é um servidor de sistema operacional</li><li>Windows 7 ou superior se o host de saudação é um sistema operacional cliente</li><li>Microsoft .NET 4.0 Framework</li><li>IIS 7.0 ou superior se instalando Olá usuário portal ou serviço web SDK</li> |

### <a name="azure-mfa-server-components"></a>Componentes do servidor MFA do Azure

Há três componentes Web que perfazem o servidor MFA do Azure:

* SDK - permite comunicação com hello outros componentes e é instalado no servidor de aplicativos do Azure MFA de saudação do serviço Web
* Portal do usuário - um site do IIS que permite que os usuários tooenroll no Azure multi-Factor Authentication (MFA) e mantenham suas contas.
* Serviço de aplicativo Web móvel - permite usar um aplicativo móvel como o aplicativo do Microsoft Authenticator Olá para verificação em duas etapas.

Todos os três componentes podem ser instalados em Olá mesmo servidor, se o servidor de saudação é voltado para a internet. Se dividir componentes Olá, Olá SDK do serviço Web está instalado no servidor de aplicativos do Azure MFA hello e hello Portal do usuário e o serviço Web aplicativos móveis são instalados em um servidor da internet.

### <a name="azure-multi-factor-authentication-server-firewall-requirements"></a>Requisitos de firewall do Servidor de Autenticação Multifator do Azure

Cada servidor MFA deve ser capaz de toocommunicate na porta 443 toohello saída endereços a seguir:

* https://pfd.phonefactor.net
* https://pfd2.phonefactor.net
* https://css.phonefactor.net

Se os firewalls de saída estiverem restritos na porta 443, abra Olá intervalos de endereços IP a seguir:

| Subrede de IP | Máscara de rede | Intervalo IP |
|:---: |:---: |:---: |
| 134.170.116.0/25 |255.255.255.128 |134.170.116.1 – 134.170.116.126 |
| 134.170.165.0/25 |255.255.255.128 |134.170.165.1 – 134.170.165.126 |
| 70.37.154.128/25 |255.255.255.128 |70.37.154.129 – 70.37.154.254 |

Se você não estiver usando o recurso de confirmação de eventos hello e seus usuários não estão usando aplicativos móveis tooverify de dispositivos na rede corporativa Olá, basta Olá intervalos a seguir:

| Subrede de IP | Máscara de rede | Intervalo IP |
|:---: |:---: |:---: |
| 134.170.116.72/29 |255.255.255.248 |134.170.116.72 – 134.170.116.79 |
| 134.170.165.72/29 |255.255.255.248 |134.170.165.72 – 134.170.165.79 |
| 70.37.154.200/29 |255.255.255.248 |70.37.154.201 – 70.37.154.206 |

## <a name="download-hello-azure-multi-factor-authentication-server"></a>Baixar Olá servidor Azure multi-Factor Authentication

1. Entrar toohello [portal do Azure](https://portal.azure.com) como um administrador.
2. Olá esquerda, selecione **do Active Directory**
3. Clique em **Usuários e grupos**
4. Clique em **Todos os usuários**
5. Clique em **Autenticação Multifator**
6. Na seção **autenticação multifator**, selecione **configurações de serviço**

   ![Página de configurações do serviço](./media/multi-factor-authentication-get-started-server/servicesettings.png)

6. Na página de configurações de serviços hello, na parte inferior da saudação da tela hello clique **Go toohello portal**. Uma nova página é aberta.
7. Clique em **Downloads**.
8. Clique em Olá **baixar** link e salve o instalador de saudação.

   ![Baixar o Servidor MFA](./media/multi-factor-authentication-get-started-server/download4.png)

9. Mantenha essa página aberta, pois chamaremos tooit depois de instalador de saudação em execução.

## <a name="install-and-configure-hello-azure-multi-factor-authentication-server"></a>Instalar e configurar o servidor Azure multi-Factor Authentication da saudação

Agora que você baixou o servidor de saudação, você pode instalar e configurá-lo. Certifique-se de que você está instalando-o no servidor Olá atende aos requisitos listados na seção de planejamento de saudação.

1. Clique duas vezes em Olá executável.
2. Na tela Selecionar pasta de instalação de hello, certifique-se de pasta hello está correta e clique em **próximo**.
3. Após a conclusão da instalação de saudação, clique em **concluir**.  Inicia o Assistente de configuração de saudação.
4. Na tela Bem-vindo do hello configuração assistente, verifique **ignorar usando Olá Assistente de configuração de autenticação** e clique em **próximo**.  Olá Assistente fecha e Olá server é iniciado.

   ![Nuvem](./media/multi-factor-authentication-get-started-server/skip2.png)

5. Volta na página de saudação que baixamos o servidor de saudação do, clique Olá **gerar credenciais de ativação** botão. Copiar essas informações em Olá servidor Azure MFA nas caixas Olá fornecido e clique em **ativar**.

## <a name="send-users-an-email"></a>Enviar um email aos usuários

distribuição de tooease, permitir que o servidor MFA toocommunicate com seus usuários. Servidor MFA pode enviar um email tooinform-los se eles foram registrados para verificação em duas etapas.

email Olá que enviar deve ser determinado por como você pode configurar seus usuários para a verificação em duas etapas. Por exemplo, se você estiver tooimport capaz de números de telefone do diretório de empresa hello, email Olá deve incluir números de telefone saudação padrão para que os usuários saibam que tooexpect. Se você não importar números de telefone, ou os usuários vão aplicativo móvel do toouse Olá, eles enviar um email que direciona toocomplete o registro da conta. Inclua um toohello de hiperlink Portal do usuário do Azure multi-Factor Authentication no email de saudação.

conteúdo de saudação do email Olá também varia dependendo método hello de verificação que foi definida para o usuário hello (chamada telefônica, SMS ou aplicativo móvel).  Por exemplo, se usuário Olá toouse necessário um PIN ao autenticar, email Olá informando o que o PIN inicial foi definido como.  Os usuários é necessária toochange o PIN durante a sua primeira verificação.

### <a name="configure-email-and-email-templates"></a>Configurar o email e os modelos de email

Clique em Olá email ícone tooset esquerdo de saudação configurações hello para enviar emails. Esta página é onde você pode inserir informações de saudação SMTP de seu email de servidor e envio de email, verificando Olá **enviar emails toousers** caixa de seleção.

![Configuração de email do Servidor MFA](./media/multi-factor-authentication-get-started-server/email1.png)

Na guia conteúdo de Email do hello, você pode ver modelos de email de saudação são toochoose disponível do. Dependendo de como você configurou sua verificação de duas etapas tooperform usuários, escolha o modelo de hello mais adequada para você.

![Modelos de email do Servidor MFA](./media/multi-factor-authentication-get-started-server/email2.png)

## <a name="import-users-from-active-directory"></a>Importar usuários do Active Directory

Agora está instalado nesse servidor de saudação deseja tooadd usuários. Você pode escolher toocreate-los manualmente, importar usuários do Active Directory ou configurar a sincronização automática com o Active Directory.

### <a name="manual-import-from-active-directory"></a>Importar do Active Directory manualmente

1. No hello servidor Azure MFA, Olá esquerda, selecione **usuários**.
2. Na parte inferior do hello, selecione **importar do Active Directory**.
3. Agora você pode ou procurar para usuários individuais ou Olá pesquisa diretório AD UOs com usuários neles.  Nesse caso, podemos especificar usuários Olá UO.
4. Realce todos os usuários Olá Olá à direita e clique em **importação**.  Você deve receber uma mensagem informando que obteve êxito.  Janela de importação Olá fechar.

   ![Importação de usuários do Servidor MFA](./media/multi-factor-authentication-get-started-server/import2.png)

### <a name="automated-synchronization-with-active-directory"></a>Sincronização automática com o Active Directory

1. No hello servidor Azure MFA, Olá esquerda, selecione **integração de diretórios**.
2. Navegue toohello **sincronização** guia.
3. Na parte inferior da saudação, escolha **adicionar**
4. Em Olá **Adicionar Item de sincronização** caixa que aparece escolha Olá domínio, OU **ou** grupo de segurança, configurações, padrões de método e idioma padrão para a sincronização de tarefas e clique em **Adicionar**.
5. Olá caixa **habilitar a sincronização com o Active Directory** e escolha um **intervalo de sincronização** entre um minuto e 24 horas.

## <a name="how-hello-azure-multi-factor-authentication-server-handles-user-data"></a>Como o hello servidor Azure multi-Factor Authentication lida com dados de usuário

Quando você usar Olá servidor multi-Factor Authentication (MFA) local, dados de um usuário são armazenados em servidores de locais de saudação. Nenhum dado de usuário persistente é armazenado na nuvem hello. Quando o usuário Olá executa uma verificação em duas etapas, Olá servidor MFA envia dados toohello verificação de saudação do Azure MFA nuvem serviço tooperform. Quando essas solicitações de autenticação são enviadas toohello serviço de nuvem, hello campos a seguir são enviados em logs e solicitação Olá para que fiquem disponíveis nos relatórios de uso/autenticação do cliente hello. Alguns dos campos de saudação são opcionais para que eles podem ser habilitados ou desabilitados no hello servidor multi-Factor Authentication. comunicação de saudação do hello serviço de nuvem do servidor MFA toohello MFA usa SSL/TLS pela porta 443 de saída. Esses campos são:

* ID exclusiva: nome de usuário ou ID interna do servidor MFA
* Nome e sobrenome (opcional)
* Endereço de email (opcional)
* Número de telefone - ao fazer uma chamada de voz ou SMS de autenticação
* Token de dispositivo: ao fazer autenticação de aplicativos móveis
* Modo de autenticação
* Resultado da autenticação
* Nome do servidor MFA
* Servidor IP MFA
* Cliente IP: se disponível

Além disso toohello campos acima, resultados de verificação da saudação (êxito/negação) e o motivo para qualquer recusa também é armazenado com os dados de autenticação hello e disponível por meio de relatórios de uso/autenticação hello.

## <a name="back-up-and-restore-azure-mfa-server"></a>Fazer backup e restaurar o Servidor MFA do Azure

Certificando-se de que você tenha um bom backup é tootake uma etapa importante com qualquer sistema.

tooback o servidor Azure MFA, certifique-se de que você tenha uma cópia da saudação **C:\Program programas\Servidor multi-Factor Authentication Server\Dados.** pasta incluindo Olá **PhoneFactor.pfdata** arquivo. 

No caso de uma restauração, é necessário Olá concluída após etapas:

1. Reinstale o Servidor MFA do Azure em um novo servidor.
2. Ativar Olá novo servidor do Azure MFA.
3. Saudação de parada **MultiFactorAuth** service.
4. Substituir saudação **PhoneFactor.pfdata** com hello backup de cópia.
5. Iniciar Olá **MultiFactorAuth** service.

novo servidor de saudação está agora em execução Olá dados originais de configuração e do usuário do backup.

## <a name="next-steps"></a>Próximas etapas

- Instalar e configurar o hello [Portal do usuário](multi-factor-authentication-get-started-portal.md) para autoatendimento de usuário.
- Instalar e configurar o hello servidor Azure MFA com [o serviço de Federação do Active Directory](multi-factor-authentication-get-started-adfs.md), [autenticação RADIUS](multi-factor-authentication-get-started-server-radius.md), ou [autenticação LDAP](multi-factor-authentication-get-started-server-ldap.md).
- Instale e configure o [Gateway de Área de Trabalho Remota e o Servidor de Autenticação Multifator do Azure usando RADIUS](multi-factor-authentication-get-started-server-rdg.md).
- [Implantar Olá aplicativo Web serviço do Azure multi-Factor Authentication Server Mobile](multi-factor-authentication-get-started-server-webservice.md).
- [Cenários avançados com a Autenticação Multifator do Azure e VPNs de terceiros](multi-factor-authentication-advanced-vpn-configurations.md).
