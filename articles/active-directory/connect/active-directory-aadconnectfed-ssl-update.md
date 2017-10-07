---
title: "Do Azure AD Connect: Certificado SSL de saudação atualização para um farm de serviços de Federação do Active Directory (AD FS) | Microsoft Docs"
description: "Este documento detalhes Olá etapas tooupdate Olá certificado SSL de um farm do AD FS usando o Azure AD Connect."
services: active-directory
keywords: "azure ad connect, atualizar ssl do adfs, atualização do certificado do adfs, alterar certificado do adfs, novo certificado do adfs, certificado do adfs, atualizar certificado ssl do adfs, atualizar adfs do certificado ssl, configurar certificado ssl do adfs, adfs, ssl, certificado, certificado de comunicação do serviço adfs, atualizar federação, configurar federação, aad connect"
authors: anandyadavmsft
manager: femila
editor: billmath
ms.assetid: 7c781f61-848a-48ad-9863-eb29da78f53c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: anandy
ms.openlocfilehash: bce7f75aab83b6abacb8472a6895054d137e10e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="update-hello-ssl-certificate-for-an-active-directory-federation-services-ad-fs-farm"></a>Atualizar o certificado SSL de saudação para um farm de serviços de Federação do Active Directory (AD FS)

## <a name="overview"></a>Visão geral
Este artigo descreve como você pode usar o certificado SSL do Azure AD Connect tooupdate Olá para um farm de serviços de Federação do Active Directory (AD FS). Você pode usar o certificado SSL Olá AD do Azure Connect ferramenta tooeasily atualização Olá para o farm do hello AD FS mesmo se o usuário entrar método hello selecionado não é do AD FS.

Você pode executar a operação de inteiro de saudação de atualizar o certificado SSL para o farm do hello AD FS em todos os servidores de Proxy de aplicativo da Web (WAP) em três etapas simples e federação:

![Três etapas](./media/active-directory-aadconnectfed-ssl-update/threesteps.png)


>[!NOTE]
>toolearn mais sobre os certificados usados pelo AD FS, consulte [Noções básicas sobre os certificados usados pelo AD FS](https://technet.microsoft.com/library/cc730660.aspx).

## <a name="prerequisites"></a>Pré-requisitos

* **Farm do AD FS**: certifique-se de que seu farm do AD FS seja baseado no Windows Server 2012 R2 ou posterior.
* **Azure AD Connect**: Certifique-se de que Olá versão do Azure AD Connect é 1.1.443.0 ou posterior. Você usará a tarefa Olá **atualização AD certificado SSL FS**.

![Atualizar a tarefa SSL](./media/active-directory-aadconnectfed-ssl-update/updatessltask.png)

## <a name="step-1-provide-ad-fs-farm-information"></a>Etapa 1: fornecer informações do farm do AD FS

Azure AD Connect tentativas tooobtain informações sobre o farm do hello AD FS automaticamente pelo:
1. Consultando informações de saudação do farm do AD FS (Windows Server 2016 ou posterior).
2. Informações de referência Olá de execuções anteriores, que são armazenados localmente com o Azure AD Connect.

Você pode modificar a lista de saudação de servidores que são exibidas adicionando ou removendo Olá Olá servidores tooreflect atual configuração de farm do hello AD FS. Assim como informações de saudação do servidor for fornecidas, o Azure AD Connect exibe conectividade hello e o status atual do certificado SSL.

![Informações do servidor AD FS](./media/active-directory-aadconnectfed-ssl-update/adfsserverinfo.png)

Se a lista de saudação contém um servidor que não faz parte do farm do hello AD FS, clique em **remover** toodelete servidor de saudação da lista de saudação de servidores no farm do AD FS.

![Servidor offline na lista](./media/active-directory-aadconnectfed-ssl-update/offlineserverlist.png)

>[!NOTE]
> Removendo um servidor na lista de saudação de servidores para um AD FS farm no Azure AD Connect é uma operação de local e atualizações Olá informações para Olá farm do AD FS que mantém a conexão do AD do Azure localmente. Azure AD Connect não modifica a configuração de Olá no AD FS tooreflect Olá alteração.    

## <a name="step-2-provide-a-new-ssl-certificate"></a>Etapa 2: Fornecer um novo certificado SSL

Após ter confirmado informações Olá sobre servidores do farm do AD FS, o Azure AD Connect solicita novo certificado SSL Olá. Forneça uma instalação do hello toocontinue do certificado, protegido por senha PFX.

![Certificado SSL](./media/active-directory-aadconnectfed-ssl-update/certificate.png)

Depois que você fornecer um certificado hello, Azure AD Connect passa por uma série de pré-requisitos. Verifique se Olá certificado tooensure que Olá certificado está correta para o farm de saudação do AD FS:

-   Olá nome de entidade de nome/alternativo de assunto para o certificado de saudação é Olá mesmo como o nome do serviço de Federação hello, ou é um certificado curinga.
-   certificado de saudação é válido por mais de 30 dias.
-   cadeia de confiança de certificado Olá é válida.
-   certificado de saudação é protegido por senha.

## <a name="step-3-select-servers-for-hello-update"></a>Etapa 3: Selecionar servidores para atualização Olá

Na próxima etapa de hello, selecione servidores de saudação que precisam de certificado SSL Olá toohave atualizado. Servidores que estejam offline não podem ser selecionados para atualização de saudação.

![Selecione os servidores tooupdate](./media/active-directory-aadconnectfed-ssl-update/selectservers.png)

Depois de concluir a configuração de hello, Azure AD Connect exibe a mensagem de saudação que indica o status de saudação da atualização de saudação e fornece uma opção tooverify saudação do AD FS entrar.

![Configuração concluída](./media/active-directory-aadconnectfed-ssl-update/configurecomplete.png)   

## <a name="faqs"></a>Perguntas frequentes

* **O que deve ser o nome da entidade do certificado de saudação Olá para o novo certificado de SSL do AD FS Olá?**

    Azure AD Connect verifica se Olá entidade alternativa de nome/nome da entidade Olá certificado contém nome de serviço de Federação hello. Por exemplo, se o nome do seu serviço de Federação for fs.contoso.com, o nome de entidade alternativo/nome da entidade de Olá deve ser fs.contoso.com.  Certificados curinga também são aceitos.

* **Por que estou, precisará fornecer as credenciais novamente na página de servidor WAP Olá?**

    Se credenciais Olá fornecidas para conectar tooAD FS servidores também não tem servidores WAP Olá privilégio toomanage hello, Azure AD Connect solicita credenciais que tenham privilégios administrativos nos servidores WAP hello.

* **servidor de saudação é mostrado como offline. O que devo fazer?**

    Azure AD Connect não pode executar qualquer operação se Olá servidor estiver offline. Se o servidor de saudação fizer parte de saudação farm do AD FS, em seguida, verifique o servidor de toohello de conectividade de saudação. Depois que você resolveu o problema de hello, pressione status de Olá Olá atualização ícone tooupdate no Assistente de saudação. Se o servidor de saudação fazia parte da saudação farm anteriormente, mas agora não existe mais, clique em **remover** toodelete da lista de saudação de servidores do Azure AD Connect mantém. Remover servidor de saudação da lista de saudação no Azure AD Connect não altera Olá configuração do AD FS em si. Se você estiver usando o AD FS no Windows Server 2016 ou posterior, Olá servidor permanece nas definições de configuração de saudação e será exibido novamente hello próxima vez hello tarefa é executada.

* **Pode atualizar um subconjunto dos meus servidores do farm com o novo certificado SSL Olá?**

    Sim. Você também pode executar a tarefa de saudação **certificado de SSL da atualização** novamente Olá tooupdate restantes servidores. Em Olá **atualização de certificados de servidores selecionados para SSL** página, você pode classificar a lista Olá de servidores **data de expiração de SSL** tooeasily acessar Olá servidores que ainda não estão atualizados.

* **Eu removi servidor Olá no hello anterior executar, mas ainda está sendo mostrado como offline e listados na página do hello AD FS servidores. Por que é servidor offline Olá ainda existe mesmo depois que removê-lo?**

    Remover servidor de saudação da lista de saudação no Azure AD Connect não removê-lo no hello configuração do AD FS. Conexão do AD do Azure faz referência para todas as informações sobre o farm de saudação do AD FS (Windows Server 2016 ou superior). Se o servidor de saudação ainda está presente no hello configuração do AD FS, ele será listado em lista hello.  

## <a name="next-steps"></a>Próximas etapas

- [Azure AD Connect e federação](active-directory-aadconnectfed-whatis.md)
- [Gerenciamento e personalização dos Serviços de Federação do Active Directory (AD FS) com o Azure AD Connect](active-directory-aadconnect-federation-management.md)
