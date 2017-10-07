---
title: 'Azure Active Directory Domain Services: habilitar Azure Active Directory Domain Services | Microsoft Docs'
description: "Habilitar o Azure Active Directory Domain Services usando Olá portal clássico do Azure"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c659da59-f4b5-4edd-b702-1727a8ccb36f
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 6263eb1849808a7c85e572e1046bc9039362dd9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a>Habilitar o Azure Active Directory Domain Services usando Olá portal clássico do Azure

## <a name="task-3-enable-azure-active-directory-domain-services"></a>Tarefa 3: habilitar o Azure Active Directory Domain Services
Nesta tarefa, você habilitar serviços de domínio de diretório ativo do Azure (Azure AD DS) para seu diretório fazendo Olá etapas a seguir:

1. Vá toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. No painel esquerdo do hello, selecione Olá **do Active Directory** botão.
3. Selecione o locatário do Azure Active Directory (AD do Azure) de saudação (diretório) para o qual você deseja tooenable do Azure AD DS.

    ![Selecionar um diretório do AD do Azure](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. Em Olá **directory visualização** , clique em Olá **configurar** guia.

    ![Guia Configurar do diretório](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. Em **dos serviços de domínio**, alterar Olá **habilitar serviços de domínio para este diretório** opção muito**Sim**.  
    Opções adicionais de configuração do Azure Active Directory Domain Services aparecem na página de saudação.

    ![Habilitar Serviços de Domínio](./media/active-directory-domain-services-getting-started/enable-domain-services.png)

   > [!NOTE]
   > Quando você habilita o Azure Active Directory Domain Services para seu locatário, o AD do Azure gera e armazena Olá Kerberos e NTLM hashes de credenciais que são necessários para autenticar usuários.
   >
   >
6. Especifique a saudação **nome de domínio DNS dos serviços de domínio**.

   * nome de domínio saudação padrão do diretório de saudação (com um **. c o m** sufixo) é selecionada por padrão.

   * Olá lista contém todos os domínios que foram configurados para seu diretório do AD do Azure, inclusive verificado e não verificadas domínios que você configura no hello **domínios** guia.

   * Você também pode inserir um nome de domínio personalizado. Neste exemplo, é o nome de domínio personalizado Olá *contoso100.com*.

     > [!WARNING]
     > prefixo de saudação do seu nome de domínio especificado (por exemplo, *contoso100* em Olá *contoso100.com* nome de domínio) deve conter a 15 caracteres. Você não pode criar um domínio do Azure Active Directory Domain Services com um prefixo que contenha mais de 15 caracteres.
     >
     >
7. Verifique se esse nome de domínio DNS Olá escolhido para Olá gerenciado domínio ainda não existir na rede virtual hello. Especificamente, verifique se toosee:

   * Você já tiver um domínio com hello mesmo nome de domínio DNS na rede virtual hello.

   * rede virtual que você selecionou Hello tem uma conexão VPN com a sua rede local, e você tiver um domínio com hello mesmo nome de domínio DNS na rede local.

   * Você tem um serviço de nuvem existente com esse nome na rede virtual hello.
8. Selecione uma rede virtual no qual você deseja que o Azure Active Directory Domain Services toobe disponível. Selecione Olá uma rede virtual e sub-rede dedicada que você criou no hello **domínio conectar serviços de rede virtual toothis** lista suspensa. Considere também Olá seguinte:

   * Certifique-se de que essa rede virtual Olá especificado pertence tooan região do Azure que é compatível com o Azure Active Directory Domain Services. tooascertain Olá regiões do Azure, onde o Azure Active Directory Domain Services está disponível, consulte [os serviços do Azure por região](https://azure.microsoft.com/regions/#services/).

   * Redes virtuais que pertencem a região tooa onde não há suporte para Azure Active Directory Domain Services não aparecem na lista suspensa de saudação.

   * Use uma sub-rede dedicada em rede virtual Olá para o Azure Active Directory Domain Services. Fazer *não* selecione Olá sub-rede de gateway. Confira [Considerações de rede](active-directory-ds-networking.md).

   * Da mesma forma, redes virtuais que foram criadas usando o Gerenciador de recursos do Azure não aparecem na lista suspensa de saudação. No momento, as redes virtuais baseadas no Resource Manager não têm suporte dos Azure Active Directory Domain Services.
9. tooenable do Azure Active Directory Domain Services, no painel de tarefas Olá final Olá Olá página, clique em **salvar**.
    * Enquanto o Azure Active Directory Domain Services está sendo habilitada para seu diretório, página Olá exibe um status de *pendente*.

        ![Habilitar janela de serviços de domínio](./media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)

        > [!NOTE]
        > O Azure Active Directory Domain Services fornece alta disponibilidade para seu domínio gerenciado. Depois de habilitar o Azure Active Directory Domain Services, endereços IP de saudação em qual domínio os serviços estão disponíveis na rede virtual Olá são exibidos um de cada vez. segundo endereço IP Hello é exibido pela primeira vez, logo após hello como assim serviço Olá habilita a alta disponibilidade para seu domínio. Quando a alta disponibilidade está configurada e ativo para o seu domínio, você deverá ver dois endereços IP em hello **dos serviços de domínio** seção Olá **configurar** guia.
        >
        >
    * Depois de cerca de 20 minutos de too30, Olá primeiro endereço IP no qual domínio os serviços estão disponíveis em sua rede virtual na Olá **endereço IP** campo Olá **configurar** página.

        ![Janela de serviços de domínio exibindo o primeiro IP provisionado](./media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
    * Quando a alta disponibilidade é operacional para seu domínio, dois endereços IP são exibidos na página de saudação. O domínio gerenciado está disponível em sua rede virtual selecionada nesses dois endereços IP.

10. Observe os dois endereços IP Olá para que você possa atualizar as configurações de DNS Olá para sua rede virtual. Isso permite que máquinas virtuais no domínio do hello rede virtual tooconnect toohello para operações como ingresso no domínio.

    ![Janela de serviços de domínio mostrando ambos os IPs provisionados](./media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> Dependendo do tamanho de saudação do seu locatário do AD do Azure (por exemplo, o número de saudação de usuários ou grupos), o domínio gerenciado do tooyour sincronização leva algum tempo. Esse processo de sincronização ocorre no plano de fundo de saudação. Para locatários grandes com dezenas de milhares de objetos, pode levar um ou dois dias para todos os usuários, associações de grupo e as credenciais toobe sincronizados.
>
>

## <a name="next-step"></a>Próxima etapa
[Tarefa 4: atualizar configurações de DNS Olá Olá rede virtual do Azure](active-directory-ds-getting-started-update-dns.md)
