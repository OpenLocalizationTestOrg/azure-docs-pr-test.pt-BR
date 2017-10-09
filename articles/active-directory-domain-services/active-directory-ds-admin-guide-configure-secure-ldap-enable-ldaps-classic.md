---
title: "aaaConfigure seguro LDAP (LDAPS) nos serviços de domínio do AD do Azure | Microsoft Docs"
description: "Configurar o LDAP Seguro (LDAPS) para um domínio gerenciado dos Serviços de Domínio do Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9d563c45-9578-410d-96c8-355af64feae8
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: a0d6e2faf474b1f0cbe157fb4ae2754b1d521ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Configurar o LDAPS (LDAP Seguro) para um domínio gerenciado do Azure AD Domain Services

## <a name="before-you-begin"></a>Antes de começar
Certifique-se de que você acabou de [tarefa 2 - Olá exportação tooa de certificado segura LDAP. Arquivo PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).

Escolha se toouse Olá visualização experiência do portal do Azure ou Olá toocomplete de portal clássico do Azure essa tarefa.
> [!div class="op_single_selector"]
> * **Portal do Azure (visualização)**: [habilitar secure LDAP usando Olá portal do Azure](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
> * **Portal clássico do Azure**: [habilitar seguro usando o portal do Azure clássico de saudação do LDAP](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-classic-azure-portal"></a>Tarefa 3 - habilitar LDAP seguro para Olá domínio gerenciado usando o portal do Azure clássico de saudação
tooenable LDAP seguro, execute Olá etapas de configuração a seguir:

1. Navegue toohello  **[portal clássico do Azure](https://manage.windowsazure.com)**.
2. Selecione Olá **do Active Directory** nó no painel esquerdo da saudação.
3. Selecione o diretório de saudação do AD do Azure (também chamado tooas 'locatário'), para o qual você habilitou os serviços de domínio do AD do Azure.

    ![Selecionar um diretório do AD do Azure](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. Clique em Olá **configurar** guia.

    ![Guia Configurar do diretório](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. Role para baixo toohello seção **dos serviços de domínio**. Você verá uma opção chamada **LDAP seguro (LDAPS)** conforme Olá captura de tela a seguir:

    ![Seção Configuração dos Serviços de Domínio](./media/active-directory-domain-services-admin-guide/secure-ldap-start.png)
6. Clique em Olá **configurar certificado...**  toobring botão backup Olá **Configure o certificado para LDAP seguro** caixa de diálogo.

    ![Configurar Certificado para LDAP Seguro](./media/active-directory-domain-services-admin-guide/secure-ldap-configure-cert-page.png)
7. Clique em seguinte de ícone de pasta Olá **arquivo com o certificado de PFX** toospecify Olá arquivo PFX que contém o certificado de saudação desejar toouse para toohello de acesso LDAP seguro gerenciados domínio. Também Inserir senha Olá especificados ao exportar o arquivo PFX do hello certificado toohello. Clique em Olá feito botão na parte inferior da saudação.

    ![Especificar arquivo PFX e senha de LDAP seguro](./media/active-directory-domain-services-admin-guide/secure-ldap-specify-pfx.png)
8. Olá **dos serviços de domínio** seção Olá **configurar** guia deve obter esmaecida e estiver em Olá **pendentes...**  estado por alguns minutos. Durante esse período, o certificado LDAPS Olá é verificado quanto à precisão e LDAP seguro está configurado para o domínio gerenciado.

    ![LDAP Seguro - estado pendente](./media/active-directory-domain-services-admin-guide/secure-ldap-pending-state.png)

   > [!NOTE]
   > Leva aproximadamente 10 minutos too15 tooenable LDAP seguro para seu domínio gerenciado. Se Olá fornecida seguro de certificados LDAP não coincide com hello necessário critérios, LDAP seguro não está habilitado para seu diretório e você verá uma falha. Por exemplo, nome de domínio hello está incorreta, certificado Olá já expirou ou expirará em breve.
   >
   >

9. Quando o LDAP seguro estiver habilitado com êxito para o domínio gerenciado, Olá **pendentes...**  mensagem deverá desaparecer. Você deve ver a impressão digital de saudação do certificado Olá exibido.

    ![LDAP Seguro habilitado](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled.png)

<br>

## <a name="task-4---enable-secure-ldap-access-over-hello-internet"></a>Tarefa 4 - habilitar acesso LDAP seguro sobre Olá internet
**Tarefas opcionais** - se você não planeja tooaccess Olá domínio usando LDAPS Olá da internet, para ignorar esta tarefa de configuração.

Antes de começar essa tarefa, certifique-se de concluir Olá etapas descritas em [tarefa 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).

1. Você verá uma opção muito**Olá permitem proteger LDAP acesso pela INTERNET** em Olá **dos serviços de domínio** seção Olá **configurar** página. Essa opção for definida muito**não** por padrão como toohello de acesso de internet gerenciado domínio sobre LDAP seguro é desabilitado por padrão.

    ![LDAP Seguro habilitado](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled2.png)
2. Ativar/desativar **Olá permitem proteger LDAP acesso pela INTERNET** muito**Sim**. Clique em Olá **salvar** botão no painel inferior de saudação.
    ![LDAP Seguro habilitado](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)
3. Olá **dos serviços de domínio** seção Olá **configurar** guia deve obter esmaecida e estiver em Olá **pendentes...**  estado por alguns minutos. Após algum tempo, é habilitado para internet acesso tooyour domínio gerenciados através de LDAP seguro.

    ![LDAP Seguro - estado pendente](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access-pending-state.png)

   > [!NOTE]
   > Ele leva cerca de 10 minutos tooenable acesso à internet através de LDAP seguro para seu domínio gerenciado.
   >
   >
4. Quando tooyour de acesso LDAP seguro gerenciados domínio pela Olá internet foi habilitado com êxito, Olá **pendentes...**  mensagem deverá desaparecer. Você deve ver o IP externo de saudação de endereços que podem ser usados tooaccess seu diretório over LDAPS no campo Olá **endereço de IP externo para acesso de LDAPS**.

    ![LDAP Seguro habilitado](./media/active-directory-domain-services-admin-guide/secure-ldap-internet-access-enabled.png)

<br>

## <a name="task-5---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a>Tarefa 5 - configurar DNS tooaccess Olá domínio gerenciado de saudação à internet
**Tarefas opcionais** - se você não planeja tooaccess Olá domínio usando LDAPS Olá da internet, para ignorar esta tarefa de configuração.

Antes de começar essa tarefa, certifique-se de concluir Olá etapas descritas em [tarefa 4](#task-4---enable-secure-ldap-access-over-the-internet).

Depois que você tiver habilitado o acesso LDAP seguro através da internet de Olá para seu domínio gerenciado, você precisa tooupdate DNS para que os computadores cliente possam encontrar este domínio gerenciado. Final de saudação de tarefa 4, um endereço IP externo é exibido na Olá **configurar** guia **endereço de IP externo para acesso de LDAPS**.

Configure seu provedor DNS externo para que o nome DNS Olá de saudação gerenciado endereço IP externo de pontos toothis domínio (por exemplo, ' ldaps.contoso100.com'). Em nosso exemplo, precisamos Olá toocreate entrada DNS a seguir:

    ldaps.contoso100.com  -> 52.165.38.113

É isso – agora você está pronto tooconnect toohello gerenciado Olá de domínio usando o LDAP seguro através da internet.

> [!WARNING]
> Lembre-se de que os computadores cliente devem confiar emissor Olá Olá LDAPS certificado toobe capaz de tooconnect com êxito toohello gerenciados usando LDAPS do domínio. Se você estiver usando uma autoridade de certificação corporativa ou de uma autoridade de certificação publicamente confiável, você não precisa toodo nada desde que essas emissores de certificado de confiança de computadores cliente. Se você estiver usando um certificado autoassinado, você precisa parte pública do tooinstall saudação do certificado autoassinado Olá no repositório de certificados confiáveis de saudação no computador do cliente de saudação.
>
>


## <a name="lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a>Bloqueio LDAPS acessar o domínio gerenciado tooyour pela Olá internet
> [!NOTE]
> **Tarefas opcionais** - se você não tiver habilitado o LDAPS domínio gerenciado do acesso toohello Olá da internet, para ignorar esta tarefa de configuração.
>
>

Antes de começar essa tarefa, certifique-se de concluir Olá etapas descritas em [tarefa 4](#task-4---enable-secure-ldap-access-over-the-internet).

Expondo o domínio gerenciado para acesso LDAPS sobre Olá internet representa uma ameaça à segurança. Olá domínio gerenciado é acessível a partir do hello internet na porta Olá usada para LDAP seguro (ou seja, porta 636). Portanto, você pode escolher toorestrict acesso toohello gerenciado domínio toospecific conhecido endereços IP. Para maior segurança, crie um grupo de segurança de rede (NSG) e associá-lo a sub-rede Olá onde você habilitou os serviços de domínio do AD do Azure.

Olá, tabela a seguir ilustra um exemplo NSG que você pode configurar, toolock para acesso LDAP seguro através de saudação à internet. Olá NSG contém um conjunto de regras que permitam o acesso LDAPS entrada pela porta TCP 636 somente de um conjunto especificado de endereços IP. Olá padrão 'DenyAll' regra se aplica tooall outro tráfego de entrada de saudação à internet. Olá NSG regra tooallow LDAPS o acesso por Olá internet de endereços IP especificados tem uma prioridade mais alta que Olá regra DenyAll NSG.

![Acesso ao exemplo NSG toosecure LDAPS por Olá da internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

**Mais informações** - [Grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md).

<br>

## <a name="related-content"></a>Conteúdo relacionado
* [Serviços de Domínio do Azure AD - guia de Introdução](active-directory-ds-getting-started.md)
* [Administrar um domínio gerenciado dos Serviços de Domínio do Azure AD](active-directory-ds-admin-guide-administer-domain.md)
* [Administrar a política de grupo em um domínio gerenciado do Azure AD Domain Services](active-directory-ds-admin-guide-administer-group-policy.md)
* [Grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md)
* [Criar um Grupo de Segurança de Rede](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
