---
title: aaaEnable Roaming de estado da empresa no Active Directory do Azure | Microsoft Docs
description: "Perguntas frequentes sobre as configurações do Enterprise State Roaming em dispositivos do Windows. Roaming de estado da empresa fornece aos usuários uma experiência unificada em seus dispositivos Windows e reduz o tempo de saudação necessário para configurar um novo dispositivo."
services: active-directory
keywords: "estado de empresa móvel, na nuvem do windows, como tooenable roaming de estado da empresa"
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: f71d66fd-7f9e-45eb-9cfe-5d989870f8a4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: c69a9cfa8055f418a3b81c62939885d5bec8a6f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-enterprise-state-roaming-in-azure-active-directory"></a>Habilitar o Enterprise State Roaming no Active Directory do Azure
Roaming de estado da empresa está disponível tooany organização com uma assinatura Premium do Azure Active Directory (AD do Azure). Para obter mais detalhes sobre como tooget uma assinatura do AD do Azure, consulte Olá [página de produto do AD do Azure](https://azure.microsoft.com/services/active-directory).

Quando você habilita o Roaming de estado da empresa, sua organização será automaticamente concedida licenças para uma assinatura gratuita de uso limitado de tooAzure Rights Management. Essa assinatura gratuita é limitada tooencrypting e descriptografia de configurações da empresa e dados de aplicativo sincronizados pela Olá Enterprise Roaming de estado do serviço; Você deve ter uma assinatura paga toouse Olá todos os recursos do Azure Rights Management.

Depois de obter uma assinatura Premium do AD do Azure, siga essas tooenable etapas Roaming de estado da empresa:

1. Logon toohello portal clássico do Azure.
2. Olá esquerda, selecione **do ACTIVE DIRECTORY**e, em seguida, selecione o diretório de saudação para o qual você deseja tooenable Roaming de estado da empresa.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming.png)
3. Vá toohello **configurar** guia na parte superior da saudação.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-configure.png)
4. Role para baixo a página hello e selecione **os usuários podem sincronizar configurações e dados corporativos de aplicativo**e, em seguida, clique em **salvar**.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-select-all-sync-settings.png)

Um Windows 10 tooroam para configurações para dispositivos com hello serviço Roaming de estado da empresa, o dispositivo Olá deve autenticar usando uma identidade do AD do Azure. Para dispositivos que estão unida tooAzure AD, Olá primário logon de usuário é identidade de saudação do AD do Azure, portanto, nenhuma configuração adicional é necessária. Para dispositivos que usam um tradicional no Active Directory local, Olá administrador de TI deve [conectar Olá dispositivos que ingressaram no domínio tooAzure AD para experiências do Windows 10](active-directory-azureadjoin-devices-group-policy.md).

## <a name="sync-data-storage"></a>Sincronizar armazenamento de dados
Dados de Roaming de estado da empresa estão hospedados em um ou mais [regiões do Azure](https://azure.microsoft.com/regions/) que melhor se alinha com o valor de país/região do hello definido na instância do Active Directory do Azure hello. Os dados do Enterprise State Roaming são particionados com base em três regiões geográficas principais: América do Norte, EMEA e APAC. Dados Roaming de estado da empresa para o locatário hello estão localizados localmente com a região geográfica hello e não serão replicados entre regiões.  Por exemplo, os clientes que têm sua tooone de conjunto de valor de país/região de países EMEA como "França" ou "Zâmbia" terá seus dados hospedados em um ou de saudação regiões do Azure na Europa.  Os clientes que definir seu valor de país/região no AD do Azure tooone de países da América do Norte, como "EUA" ou "Canadá" terá seus dados hospedados em um ou mais Olá regiões do Azure dentro de saudação dos EUA.  Os clientes que definir seu valor de país/região no AD do Azure tooone de países APAC como "Austrália" ou "Nova Zelândia" terá seus dados hospedados em um ou mais Olá regiões do Azure na Ásia.  Países América do Sul e dados Antártida serão hospedados em um ou mais regiões do Azure dentro de saudação dos EUA.  valor de país/região Olá é definido como parte do processo de criação de diretório do AD do Azure de saudação e não pode ser modificada posteriormente. 

Se você precisar de mais detalhes sobre o local de armazenamento de dados, crie um tíquete no [suporte do Azure](https://azure.microsoft.com/support/options/).

## <a name="manage-enterprise-state-roaming"></a>Gerenciar o Enterprise State Roaming
Administradores globais do Azure AD podem habilitar e desabilitar o Roaming de estado da empresa em Olá portal clássico do Azure.
![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-manage.png)

Os administradores globais podem limitar os grupos de segurança de toospecific de sincronização de configurações.

Os administradores globais também podem exibir um relatório de status de sincronização de dispositivo por usuário, selecionando um usuário específico na instância do Active Directory Olá **usuários** lista e clicando em **dispositivos** guia e selecionar Exibir **Dispositivos sincronizar configurações e dados corporativos de aplicativo**.
![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-device-sync-settings.png)

## <a name="data-retention"></a>Retenção de dados
TooAzure dados sincronizados por meio de Roaming de estado da empresa será retido indefinidamente, a menos que uma operação de exclusão manual é executada ou dados de saudação em questão são determinado toobe obsoletos. 

**Exclusão explícita:** dados saudação são excluídos quando um administrador do Azure exclui um usuário ou um diretório ou um administrador solicita explicitamente que dados sejam toobe excluído.

* **Exclusão de usuário**: quando um usuário é excluído do AD do Azure, conta de usuário de saudação roaming de dados será marcada para exclusão e será excluída entre 90 dias too180. 
* **Exclusão de diretório**: a exclusão de um diretório inteiro no Azure AD é uma operação imediata. Todos os dados de configurações de saudação associados com esse diretório será marcado para exclusão e será excluído entre 90 dias too180. 
* **Na exclusão de solicitação**: se Olá AD do Azure administrador quer toomanually excluir dados ou dados de configurações de um usuário específico, Olá administrador pode emitir um ticket com [suporte do Azure](https://azure.microsoft.com/support/). 

**Obsoleto exclusão de dados**: dados que não foram acessados para um ano ("período de retenção de hello") será tratado como obsoleto e poderá ser excluído do Azure. período de retenção de saudação é toochange de assunto, mas não serão menos de 90 dias. dados obsoletos Olá podem ser um conjunto específico de configurações do aplicativo do Windows ou todas as configurações para um usuário. Por exemplo:

* Se nenhum dispositivo acessar uma coleção de configurações específico (por exemplo, um aplicativo é removido do dispositivo hello, ou um grupo de configurações, como "Tema" está desabilitado para todos os dispositivos do usuário), essa coleção se tornarão obsoleta após o período de retenção hello e pode ser excluído. 
* Se um usuário desativou a sincronização de configurações em todos os seus dispositivos, em seguida, nenhum dos dados de configurações de saudação será acessado e todos os dados de configurações de Olá para o usuário se tornará obsoletos e poderão ser excluídos após o período de retenção hello. 
* Se Olá administrador de diretório do AD do Azure desliga Roaming de estado da empresa para o diretório inteiro hello, em seguida, todos os usuários nesse diretório interromperá a sincronização de configurações e todos os dados de configurações para todos os usuários se tornarão obsoletos e podem ser excluídos após o período de retenção hello. 

**A recuperação de dados excluídos**: política de retenção de dados de saudação não é configurável. Quando dados saudação foi excluídos permanentemente, não serão recuperável. No entanto, é importante toonote que Olá dados de configurações só será excluída do Azure, o dispositivo de usuário final do hello. Se qualquer dispositivo posterior se reconectar toohello serviço de Roaming de estado da empresa, configurações de saudação novamente serão sincronizadas e armazenadas no Azure.

## <a name="related-topics"></a>Tópicos relacionados
* [Visão geral do Enterprise State Roaming](active-directory-windows-enterprise-state-roaming-overview.md)
* [Perguntas frequentes sobre configurações e roaming de dados](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Política de grupo e as configurações do MDM para a sincronização de configurações](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Referência de configurações de roaming do Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [Solução de problemas](active-directory-windows-enterprise-state-roaming-troubleshooting.md)
