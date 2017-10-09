---
title: "Azure AD Connect: autenticação de passagem – bloqueio inteligente | Microsoft Docs"
description: "Este artigo descreve como autenticação de passagem do Azure Active Directory (AD do Azure) protege suas contas no local contra ataques de senha de força bruta em nuvem hello."
services: active-directory
keywords: "Autenticação de Passagem do Azure AD Connect, instalar o Active Directory, componentes necessários para o Azure AD, SSO, Logon único"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: b02e315c3cc3eae00ca6408d735a416f34c2cdc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-smart-lockout"></a>Autenticação de passagem do Azure Active Directory: bloqueio inteligente

## <a name="overview"></a>Visão geral

O Azure AD protege contra ataques de senha de força bruta e impede que usuários reais sejam impedidos de acessar seus aplicativos de SaaS e do Office 365. Essa capacidade, chamada **Bloqueio Inteligente**, tem suporte quando você usa a Autenticação de Passagem como seu método de entrada. Bloqueio inteligente está habilitado por padrão para todos os locatários e está protegendo suas contas de usuário em todo o tempo de saudação; Não há nenhuma necessidade tooturn-la no.

O Bloqueio Inteligente funciona controlando tentativas de logon com falha e, depois de um determinado **Limite de bloqueio**, iniciando uma **Duração de bloqueio**. As tentativas de entrar de invasor Olá durante a duração do bloqueio de saudação são rejeitadas. Se continuar ataque hello, Olá subsequentes com falha tentativas de entrada após o término do hello duração do bloqueio resultará em mais longas de bloqueio.

>[!NOTE]
>padrão de saudação limite de bloqueio é 10 tentativas com falha e o padrão de saudação que duração do bloqueio é 60 segundos.

Bloqueio inteligente também faz distinção entre entradas de usuários originais e contra invasores e bloqueios somente out invasores Olá na maioria dos casos. Essa funcionalidade impede que invasores bloqueiem usuários reais de forma mal-intencionada. Usamos após entrar comportamento, dispositivos dos usuários & navegadores e outros toodistinguish sinais entre usuários original. Estamos aperfeiçoando constantemente nossos algoritmos.

Como a autenticação de passagem encaminha solicitações de validação de senha para o local do Active Directory (AD), é necessário tooprevent invasores bloqueio de contas de usuários do AD. Como você tem suas próprias políticas de bloqueio de conta do AD (especificamente, [ **limite de bloqueio de conta** ](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) e [ **políticas de redefinição de contador de bloqueio de conta após** ](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), é necessário que o limite de bloqueio de tooconfigure do AD do Azure e duração do bloqueio adequadamente valores toofilter ataques na nuvem de saudação antes que elas atinjam suas instalações AD.

>[!NOTE]
>Olá bloqueio inteligente recurso está livre e _em_ por padrão para todos os clientes. No entanto, modificar o limite de bloqueio e a valores de duração do bloqueio usando a API do Graph do AD do Azure precisa de sua licença do locatário toohave pelo menos um AD do Azure Premium P2. Você não precisa de uma licença Azure AD Premium P2 _por usuário_ recurso de bloqueio inteligente Olá tooget com a autenticação de passagem.

tooensure que os usuários no AD contas locais são protegidas, é necessário tooensure que:

1.  O Limite de bloqueio do Azure AD seja _menor_ que o Limite de bloqueio da Conta do AD. É recomendável que você defina os valores hello, de forma que o limite de bloqueio de conta do AD é pelo menos dois ou três vezes o limite de bloqueio do AD do Azure.
2.  A Duração de bloqueio do Azure AD (representada em segundos) seja _maior_ que o valor de Redefinir contador de bloqueios de conta após do AD (representado em minutos).

## <a name="verify-your-ad-account-lockout-policies"></a>Verifique as políticas de bloqueio de conta do AD

Use suas políticas de bloqueio de conta do AD de Olá tooverify instruções a seguir:

1.  Abra a ferramenta de gerenciamento de diretiva de grupo de saudação.
2.  Edite saudação diretiva de grupo é aplicada tooall usuários, por exemplo, Olá diretiva de domínio padrão.
3.  Navegue tooComputer configuração configurações diretivas Conta\diretiva de bloqueio.
4.  Verifique os valores de Limite de bloqueio de conta e Redefinir contador de bloqueios de conta após.

![Políticas de bloqueio de conta do AD](./media/active-directory-aadconnect-pass-through-authentication/pta5.png)

## <a name="use-hello-graph-api-toomanage-your-tenants-smart-lockout-values"></a>Use Olá Graph API toomanage valores de bloqueio inteligente do locatário

>[!IMPORTANT]
>Modificar os valores de Limite de bloqueio e de Duração de bloqueio do Azure AD usando a API do Graph é um recurso do Azure AD Premium P2. Ele também precisa toobe um Administrador Global no seu locatário.

Você pode usar [Gerenciador de gráficos](https://developer.microsoft.com/graph/graph-explorer) tooread, definir e atualizar valores de bloqueio inteligente do AD do Azure. Mas você também pode fazer essas operações de forma programática.

### <a name="read-smart-lockout-values"></a>Ler valores de Bloqueio Inteligente

Siga estas etapas tooread valores de bloqueio inteligente do locatário:

1. Entre no Explorador do Graph como um Administrador Global de seu locatário. Se solicitado, conceder acesso para Olá permissões solicitadas.
2. Clique em "Modificar permissões" e selecione a permissão de "Directory.ReadWrite.All" hello.
3. Configure a solicitação de API do Graph Olá da seguinte maneira: versão do conjunto de muito "BETA", tipo de solicitação muito "GET" e a URL muito`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.
4. Clique em "Executar consulta" toosee valores de bloqueio inteligente do locatário. Se não tiver configurado os valores de seu locatário antes, você verá um conjunto vazio.

### <a name="set-smart-lockout-values"></a>Definir valores de Bloqueio Inteligente

Siga estas etapas tooset valores de bloqueio inteligente do locatário (para Olá apenas na primeira vez):

1. Entre no Explorador do Graph como um Administrador Global de seu locatário. Se solicitado, conceder acesso para Olá permissões solicitadas.
2. Clique em "Modificar permissões" e selecione a permissão de "Directory.ReadWrite.All" hello.
3. Configure a solicitação de API do Graph Olá da seguinte maneira: versão do conjunto de muito "BETA", tipo de solicitação muito "POST" e a URL muito`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.
4. Copie e cole Olá solicitação JSON a seguir no campo de "Corpo da solicitação" hello. Alterar valores de bloqueio inteligente Olá conforme apropriado e use um GUID aleatório para `templateId`.
5. Clique em "Executar consulta" tooset valores de bloqueio inteligente do locatário.

```
{
  "templateId": "5cf42378-d67d-4f36-ba46-e8b86229381d",
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "300"
    },
    {
      "name": "LockoutThreshold",
      "value": "5"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

>[!NOTE]
>Se você não estiver usando-los, você pode deixar Olá **BannedPasswordList** e **EnableBannedPasswordCheck** valores como vazio ("") e "false" respectivamente.

Verifique se você definiu os valores do Bloqueio Inteligente de seu locatário corretamente usando [estas etapas](#read-smart-lockout-values).

### <a name="update-smart-lockout-values"></a>Atualizar valores de Bloqueio Inteligente

Siga essas etapas tooupdate valores de bloqueio inteligente do locatário (se você já tiver configurado antes):

1. Entre no Explorador do Graph como um Administrador Global de seu locatário. Se solicitado, conceder acesso para Olá permissões solicitadas.
2. Clique em "Modificar permissões" e selecione a permissão de "Directory.ReadWrite.All" hello.
3. [Siga estas etapas tooread valores de bloqueio inteligente do locatário](#read-smart-lockout-values). Saudação de cópia `id` valor (uma GUID) do item de saudação com "displayName" como "PasswordRuleSettings".
4. Configure a solicitação de API do Graph Olá da seguinte maneira: definir versão muito "BETA", tipo de solicitação muito "PATCH" e a URL muito`https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` -usar Olá GUID da etapa 3 para `<id>`.
5. Copie e cole Olá solicitação JSON a seguir no campo de "Corpo da solicitação" hello. Altere os valores de bloqueio inteligente Olá conforme apropriado.
6. Clique em "Executar consulta" tooupdate valores de bloqueio inteligente do locatário.

```
{
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "30"
    },
    {
      "name": "LockoutThreshold",
      "value": "4"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

Verifique se você atualizou os valores do Bloqueio Inteligente de seu locatário corretamente usando [estas etapas](#read-smart-lockout-values).

## <a name="next-steps"></a>Próximas etapas
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) – para registrar solicitações de novos recursos.
