---
title: "Olá de aaaManaging dispositivos usando o portal do Azure - visualização | Microsoft Docs"
description: "Saiba como toouse Olá dispositivos toomanage portal do Azure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: a39d14e4ce8bb79f0223a9de40d5f1259a869927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-devices-using-hello-azure-portal---preview"></a>Gerenciamento de dispositivos usando Olá portal do Azure - visualização

>[!NOTE]
>Atualmente, essa capacidade está em visualização pública. Prepare-se toorevert ou remova as alterações. recurso de saudação está disponível em qualquer assinatura do Azure Active Directory (AD do Azure) durante a visualização pública. No entanto, quando o recurso de saudação se torna disponível, alguns aspectos do recurso de saudação podem exigir uma assinatura premium do Active Directory do Azure.


Com o gerenciamento de dispositivos no Azure AD (Azure Active Directory), você pode garantir que os usuários acessem recursos usando dispositivos que atendam aos padrões de segurança e conformidade. 

Este tópico:

- Pressupõe que você esteja familiarizado com hello [gerenciamento de toodevice de Introdução no Active Directory do Azure](device-management-introduction.md)

- Fornece informações sobre como gerenciar dispositivos usando Olá portal do Azure


dispositivos toomanage Olá portal do Azure, você precisa tooclick **dispositivos** em Olá **gerenciar** seção Olá Olá **Active Directory do Azure** folha.

![Gerenciar um dispositivo do Intune](./media/device-management-azure-portal/11.png)




## <a name="configure-device-settings"></a>Definir configurações do dispositivo

toomanage seus dispositivos usando Olá portal do Azure, que precisam toobe registrado ou ingressou tooAzure AD. Como administrador, você pode ajustar o processo de saudação de registro e ingresso de dispositivos, definindo configurações de dispositivo de saudação.

![Gerenciar um dispositivo do Intune](./media/device-management-azure-portal/22.png)


folha de configurações de dispositivo Olá permite tooconfigure:

- **Os usuários podem ingressar seus dispositivos tooAzure AD** – essa configurações permite que usuários Olá tooselect podem unir dispositivos tooAzure AD. saudação padrão é **todos os**.

- **Outros administradores locais no AD do Azure associado dispositivos** -você pode selecionar os usuários de saudação são concedidos direitos de administrador local em um dispositivo. Os usuários adicionados aqui são adicionados toohello *administradores do dispositivo* função no AD do Azure. Os administradores globais no Azure AD e os proprietários do dispositivo recebem direitos de administrador local por padrão. Essa opção é um recurso de edição premium disponível por meio de produtos como o Azure AD Premium Olá Enterprise Mobility Suite (EMS). 

- **Os usuários podem registrar seus dispositivos com o Azure AD** -você precisa tooconfigure toobe de dispositivos de tooallow essa configuração registrado com o AD do Azure. Se você selecionar **nenhum**, dispositivos não são permitidos tooregister quando eles não são parte do AD do Azure ou híbrido do AD do Azure associado. O registro com o Microsoft Intune ou o MDM (Gerenciamento de Dispositivo Móvel) para o Office 365 exige registro. Se você tiver configurado qualquer um desses serviços, a opção **TODOS** estará selecionada e **NENHUM** não estará disponível.

- **Exigir que os dispositivos do multi-Factor Auth toojoin** -você pode escolher se os usuários são necessária tooprovide uma autenticação de segundo fator toojoin tooAzure seu dispositivo AD. saudação padrão é **não**. É recomendável exigir a autenticação multifator ao registrar um dispositivo. Antes de habilitar a autenticação multifator para este serviço, você deve garantir que a autenticação multifator está configurada para usuários de saudação que registrem seus dispositivos. Para saber mais sobre os diferentes serviços de autenticação multifator do Azure, consulte [Introdução à autenticação multifator do Azure](../multi-factor-authentication/multi-factor-authentication-get-started.md). 

- **Número máximo de dispositivos** -essa configuração permite que você tooselect Olá alto número de dispositivos que um usuário pode ter no AD do Azure. Se um usuário atingir essa cota, eles não são ser dispositivos adicionais tooadd capaz de até que um ou mais dos dispositivos existentes Olá são removidos. aspas de dispositivo de saudação é contada para todos os dispositivos que estão unidas do AD do Azure ou AD do Azure registrado atualmente. valor padrão de saudação é **20**.

- **Os usuários podem sincronizar configurações e dados de aplicativo em dispositivos** -por padrão, essa configuração é definida muito**NONE**. Selecionar usuários específicos ou grupos ou todos os permite do usuário Olá configurações e toosync de dados de aplicativo em seus dispositivos Windows 10. Saiba mais sobre como a sincronização funciona no Windows 10.
Essa opção é um recurso premium disponível por meio de produtos como o Azure AD Premium Olá Enterprise Mobility Suite (EMS).
 
    ![Gerenciar um dispositivo do Intune](./media/device-management-azure-portal/21.png)




## <a name="locate-devices"></a>Localizar dispositivos

Como administrador, Olá portal do Azure, você tem duas opções toolocate registraram e uniram dispositivos:

- **Todos os dispositivos** em Olá **gerenciar** seção Olá **dispositivos** folha  

    ![Todos os dispositivos](./media/device-management-azure-portal/41.png)


- **Dispositivos** em Olá **gerenciar** seção um **usuário** folha
 
    ![Todos os dispositivos](./media/device-management-azure-portal/43.png)



Com ambas as opções, você pode ver tooa que:


- Permite que você toosearch para dispositivos usando o nome de exibição hello como filtro.

- Fornece visão geral detalhada de dispositivos registrados e associados

- Permite que você tooperform tarefas comuns de gerenciamento de dispositivo
   

![Todos os dispositivos](./media/device-management-azure-portal/51.png)


## <a name="device-management-tasks"></a>Tarefas de gerenciamento de dispositivos

Como administrador, você pode gerenciar Olá registrado ou dispositivos ingressados no. Esta seção fornece informações sobre tarefas comuns de gerenciamento de dispositivo.


**Gerenciar um dispositivo do Intune** – se você for um administrador do Intune, será possível gerenciar dispositivos marcados como **Microsoft Intune**. Um administrador pode ver dispositivos adicionais 

![Gerenciar um dispositivo do Intune](./media/device-management-azure-portal/31.png)


**Habilitar/desabilitar um dispositivo do Azure AD**

tooenable ou desativar um dispositivo, você precisa toobe um administrador global no AD do Azure. Desabilitar um dispositivo impede que um dispositivo acesse seus recursos do Azure AD.  dispositivo de saudação toodisable, você pode clicar em *...* Clique em dispositivo Olá para obter detalhes adicionais.

 
![Gerenciar um dispositivo do Intune](./media/device-management-azure-portal/33.png)

Desativar um dispositivo altera o estado de saudação em Olá **habilitado** coluna muito**não**.

![Desabilitar um dispositivo](./media/device-management-azure-portal/32.png)


**Excluir um dispositivo do AD do Azure** -toodelete um dispositivo, você precisa toobe um administrador global no AD do Azure.  
Excluindo um dispositivo:
 
- Impede que um dispositivo acesse seus recursos do Azure AD 

- Remove todos os detalhes de dispositivo anexado toohello, por exemplo, chaves do BitLocker para dispositivos Windows  

- Representa uma atividade não recuperável e não é recomendável a menos que necessário

Se um dispositivo for gerenciado por outra autoridade de gerenciamento (por exemplo, o Microsoft Intune), verifique se esse dispositivo Olá tem foi apagado / desativado antes de excluir o dispositivo Olá no AD do Azure.

Você pode selecionar “…” dispositivo de saudação toodelete ou clique no dispositivo Olá para obter detalhes adicionais
 
![Excluir um dispositivo](./media/device-management-azure-portal/34.png)


**Exibir ou copiar a ID do dispositivo** -você pode usar o dispositivo ID tooverify Olá ID detalhes do dispositivo no dispositivo de saudação ou usando o PowerShell durante a solução de problemas. tooaccess Olá cópia, clique em dispositivo hello.

![Exibir uma ID do dispositivo](./media/device-management-azure-portal/35.png)
  

**Exibir ou copiar as chaves do BitLocker** -se você for um administrador, você pode exibir hello cópia BitLocker chaves e toohelp usuários toorecover sua unidade criptografada. Essas chaves só estão disponíveis para dispositivos Windows que são criptografados e têm suas chaves armazenadas no Azure AD. Você pode copiar essas chaves ao acessar detalhes do dispositivo hello.
 
![Exibir chaves do BitLocker](./media/device-management-azure-portal/36.png)



## <a name="audit-logs"></a>Logs de auditoria


atividades de dispositivo Olá estão disponíveis por meio de registros de atividade de saudação. Isso inclui atividades disparadas pelo serviço de registro de dispositivo de saudação ou por usuário hello:

- Criação de dispositivo e adicionar usuários/proprietários do dispositivo Olá

- Altera as configurações de toodevice

- Operações de dispositivo como excluir ou atualizar um dispositivo
 
O toohello de ponto de entrada dados de auditoria é **logs de auditoria** em Olá **atividade** seção hello **dispositivos* folha.

![Logs de auditoria](./media/device-management-azure-portal/61.png)


Um log de auditoria tem um modo de exibição de lista padrão que mostra:

- Data de saudação e a hora da ocorrência da saudação

- destinos de saudação

- Olá iniciador / ator (que) de uma atividade

- atividade de saudação (o que)

![Logs de auditoria](./media/device-management-azure-portal/63.png)

Você pode personalizar o modo de exibição de lista Olá clicando **colunas** na barra de ferramentas de saudação.
 
![Logs de auditoria](./media/device-management-azure-portal/64.png)


toonarrow inativo saudação relatados nível tooa de dados que funciona para você, você pode filtrar os dados de auditoria hello usando Olá campos a seguir:

- Categoria
- Tipo de recurso de atividade
- Atividade
- Intervalo de datas
- Destino
- Iniciado por (ator)

Além disso toohello filtros, você pode procurar itens específicos.

![Logs de auditoria](./media/device-management-azure-portal/65.png)

## <a name="next-steps"></a>Próximas etapas

* [Gerenciamento de toodevice de Introdução no Active Directory do Azure](device-management-introduction.md)



