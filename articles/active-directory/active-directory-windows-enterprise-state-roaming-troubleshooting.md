---
title: "Solucionando problemas de configurações do Enterprise State Roaming no Azure Active Directory | Microsoft Docs"
description: "Fornece respostas toosome perguntas aos administradores de TI podem ter sobre as configurações e sincronização de dados do aplicativo."
services: active-directory
keywords: "configurações do enterprise state roaming, nuvem do windows, perguntas frequentes sobre o enterprise state roaming"
documentationcenter: 
author: tanning
manager: swadhwa
editor: 
ms.assetid: f45d0515-99f7-42ad-94d8-307bc0d07be5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 4636d016983426e30d696459f54167b8ad2babcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
#<a name="troubleshooting-enterprise-state-roaming-settings-in-azure-active-directory"></a>Solucionando problemas de configurações do Enterprise State Roaming no Azure Active Directory

Este tópico fornece informações sobre como tootroubleshoot e diagnosticar problemas com Roaming de estado da empresa e fornece uma lista dos problemas conhecidos.

## <a name="preliminary-steps-for-troubleshooting"></a>Etapas preliminares para a solução de problemas 
Antes de iniciar a solução de problemas, verifique se dispositivo e usuário Olá foi configurados corretamente e que todos os requisitos de saudação do Roaming de estado da empresa são atendidos pelo dispositivo hello e usuário de saudação. 

1. Windows 10, com as atualizações mais recentes Olá e um mínimo versão 1511 (Build 10586 ou superior do sistema operacional) está instalado no dispositivo de saudação. 
2. dispositivo de saudação é Unido, ou domínio e registrado com o AD do Azure do AD do Azure.
3. No portal do Azure Active Directory hello, **Roaming de estado da empresa** está habilitado para diretório de saudação em **configurar** > **dispositivos**  >  **Os usuários podem sincronizar configurações e dados corporativos de aplicativo**. Todos os usuários estão selecionados ou usuário Olá é habilitado para sincronização através da opção de saudação selecionada e incluído no grupo de segurança de saudação.
4. usuário Olá tem uma assinatura do Azure Active Directory Premium atribuída toothem.  
5. Olá dispositivo foi reiniciado e Olá usuário tiver efetuado logon após a habilitação do Roaming de estado da empresa.

## <a name="information-tooinclude-when-you-need-help"></a>Informações tooinclude quando precisar de ajuda
Se você não conseguir resolver o problema com as orientações de saudação abaixo, você pode entrar em contato com nossos engenheiros de suporte. Quando você entrar em contato com eles, é recomendável Olá tooinclude informações a seguir:

- **Descrição geral do erro Olá** – há mensagens de erro vistas pelo usuário Olá? Se não houver nenhuma mensagem de erro, descreva Olá comportamento inesperado observado, em detalhes. Quais recursos estão habilitados para sincronização e o que é o usuário Olá esperando toosync? São vários recursos não está sincronizando ou é isolada de it tooone?
- **Usuários afetados** – a sincronização está funcionando/falhando para um usuário ou vários? Quantos dispositivos estão envolvidos por usuário? Nenhum deles está sincronizando ou alguns estão e outros não?
- **Informações sobre o usuário Olá** – quais identidade é usuário hello usando toolog toohello dispositivo? Como usuário hello está fazendo logon no dispositivo toohello? Eles são parte de um grupo de segurança selecionado permitido toosync? 
- **Informações sobre o dispositivo Olá** – este dispositivo associado do AD do Azure ou ingressado no domínio? O build está dispositivo Olá? Quais são as atualizações mais recentes Olá?
- **Data / hora / fuso horário** – qual era date de hello precisas e a hora você viu o erro de saudação (incluem o fuso horário de saudação)?
- A inclusão dessas informações nos ajudará a resolver seu problema o mais rápido possível.

## <a name="troubleshooting-and-diagnosing-issues"></a>Solução de problemas e diagnósticos
Esta seção fornece sugestões sobre como tootroubleshoot e diagnosticar problemas tooEnterprise relacionados a Roaming de estado.

## <a name="verify-sync-and-hello-sync-your-settings-settings-page"></a>Verifique se a sincronização e hello "Sincronizar suas configurações" página de configurações 

1. Depois de ingressar tooa seu PC com Windows 10 domínio configurado tooallow Enterprise estado de Roaming, faça logon com sua conta corporativa. Vá muito**configurações** > **contas** > **configurações de sincronização do** e verifique se as configurações individuais de sincronização e hello e esse superior de saudação do página de configurações de saudação indica que você está sincronizando com sua conta corporativa. Confirmar Olá a mesma conta também é usada como sua conta de logon em **configurações** > **contas** > **informações seu**. 
2. Verifique se a sincronização funciona em vários computadores fazendo algumas alterações no computador original hello, como mover Olá na barra de tarefas toohello lado direito ou superior da tela hello. Assista a alteração de saudação propagar toohello segunda máquina em cinco minutos. 
 - Bloqueando e desbloqueando tela hello (Win + L) pode ajudar a disparar uma sincronização.
 - Você deve estar usando Olá a mesma conta de logon em ambos os computadores para sincronização toowork – como Roaming de estado da empresa é associado toohello conta de usuário e não conta da máquina hello.

**Possível problema**: página de configurações de saudação tem alterna Olá esmaecidas e em vez de ver uma conta, você verá o texto de saudação "alguns recursos do Windows só estarão disponíveis se você estiver usando uma conta da Microsoft ou conta de trabalho". Esse problema pode ocorrer para dispositivos que foram configurados toobe ingressado no domínio e registrado tooAzure AD, mas dispositivo Olá não autenticou com êxito tooAzure AD. Uma possível causa é que deve ser aplicada a diretiva de saudação do dispositivo, mas esse aplicativo ocorre de maneira assíncrona e pode ser atrasado por algumas horas. tooverify esse problema, execute estas etapas de saudação em Verificar Olá toocheck de status de registro do dispositivo se esse for o caso de saudação.

### <a name="verify-hello-device-registration-status"></a>Verificar o status de registro de dispositivo Olá
Roaming de estado da empresa requer Olá dispositivo toobe registrado com o AD do Azure. Embora não específica tooEnterprise Roaming de estado, siga as instruções de saudação abaixo pode ajudar a confirmar que Olá cliente com Windows 10 está registrado e confirmar o status da impressão digital, URL de configurações do AD do Azure, NGC e outras informações.

1.  Prompt de comando aberta Olá o. toodo isso no Windows, abra Olá iniciador de execução (Win + R) e digite "cmd" tooopen.
2.  Uma vez aberto Olá prompt de comando, digite "*dsregcmd.exe /status*".
3.  Para a saída esperada, Olá **AzureAdJoined** valor do campo deve ser "Sim", **WamDefaultSet** valor do campo deve ser "Sim" e Olá **WamDefaultGUID** o valor do campo deve ser um GUID com "(AzureAd)" no final da saudação.

**Possível problema**: **WamDefaultSet** e **AzureAdJoined** têm "Não" no valor do campo hello, dispositivo Olá foi ingressado no domínio e registrado com o Azure AD, e dispositivo Olá não sincronizados. Se ele estiver mostrando isso, dispositivo Olá pode precisar toowait para toobe política aplicada ou Olá autenticação Olá dispositivo falhou ao se conectar tooAzure AD. usuário Olá pode ter toowait algumas horas para Olá toobe de política aplicadas. Outras etapas de solução de problemas podem incluir repetir o registro automático por iniciar ou assinatura e novamente em tarefa Olá no Agendador de tarefas. Em alguns casos, executar "*dsregcmd.exe /leave*" em uma janela de prompt de comando elevado, reinicializar e tentar se registrar novamente pode ajudar com esse problema.


**Possível problema**: campo Olá para **AzureAdSettingsUrl** está vazia e hello dispositivo não sincronização. usuário Olá pode ter registrado última no dispositivo toohello antes de Roaming de estado da empresa foi habilitada no hello Azure Active Portal de diretório. Reiniciar o dispositivo hello e ter Olá logon de usuário. Opcionalmente, no portal de hello, tente ter Olá administrador de TI desabilitar e habilitar novamente os usuários podem sincronizar configurações e dados corporativos de aplicativo. Depois de reiniciar Olá dispositivo habilitado novamente e ter Olá logon de usuário. Se isso não resolver o problema de hello, **AzureAdSettingsUrl** pode estar vazia no caso de saudação de um certificado de dispositivo inválido. Nesse caso, executar “*dsregcmd.exe /leave*” em uma janela de prompt de comandos com privilégios elevados, reinicializar e tentar se registrar novamente pode ajudar com esse problema.

## <a name="enterprise-state-roaming-and-multi-factor-authentication"></a>Enterprise State Roaming e Autenticação Multifator 
Em determinadas condições, a Roaming de estado da empresa pode falhar toosync dados se o Azure multi-Factor Authentication está configurado. Para obter detalhes adicionais sobre esses sintomas, consulte o documento de suporte de saudação [KB3193683](https://support.microsoft.com/kb/3193683). 

**Possível problema**: se o dispositivo for configurado toorequire multi-Factor Authentication no portal do Azure Active Directory Olá, você poderá falhar toosync configurações durante a assinatura no dispositivo tooa Windows 10 usando uma senha. Esse tipo de configuração de autenticação multifator é pretendido tooprotect uma conta de administrador do Azure. Usuários administrativos ainda podem ser capaz de toosync entrando tootheir Windows 10 dispositivos com o Microsoft Passport for Work PIN ou completando a autenticação multifator ao acessar outros serviços do Azure como o Office 365.

**Possível problema**: sincronização poderá falhar se Olá administrador configura a política de acesso condicional do Active Directory Federation Services multi-Factor Authentication hello e Olá token de acesso no dispositivo de saudação expira. Certifique-se de que você entrar e sair usando Olá Microsoft Passport for Work PIN ou concluir a autenticação multifator ao acessar outros serviços do Azure como o Office 365.

###<a name="event-viewer"></a>Visualizador de Eventos
Para solução de problemas avançada, o Visualizador de eventos pode ser erros específicos toofind usado. Essas situações são documentadas na tabela de saudação abaixo. Olá eventos podem ser encontrados em Visualizar eventos > Applications and Services Logs > **Microsoft** > **Windows** > **SettingSync** e para problemas relacionados à identidade com sincronização **Microsoft** > **Windows** > **AD do Azure**.


## <a name="known-issues"></a>Problemas conhecidos

### <a name="sync-does-not-work-on-devices-that-have-apps-side-loaded-using-mdm-software"></a>A sincronização não funciona em dispositivos que possuem aplicativos com sideloaded usando o software do MDM

Afeta a dispositivos que executam Olá atualização de aniversário do Windows 10 (versão 1607). No Visualizador de eventos em logs do Azure SettingSync hello, Olá 6013 de ID de evento com o erro 80070259 frequentemente é visto.

**Ação recomendada**  
Certifique-se de cliente de v1607 Olá Windows 10 tem Olá 23 de agosto de 2016 atualização cumulativa ([KB3176934](https://support.microsoft.com/kb/3176934) 14393.82 de compilação do sistema operacional). 

---

### <a name="internet-explorer-favorites-do-not-sync"></a>Os favoritos do Internet Explorer não sincronizam

Afeta a dispositivos que executam Olá atualização de novembro do Windows 10 (versão 1511).

**Ação recomendada**  
Certifique-se de cliente de v1511 Olá Windows 10 tem Olá julho de 2016 atualização cumulativa ([KB3172985](https://support.microsoft.com/kb/3172985) 10586.494 de compilação do sistema operacional).

---

### <a name="theme-is-not-syncing-as-well-as-data-protected-with-windows-information-protection"></a>O tema não está sincronizando, assim como os dados protegidos com a Proteção de Informações do Windows 

tooprevent vazamento de dados, dados que são protegidos com [Windows Information Protection](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip) não será sincronizado por meio de Roaming de estado da empresa para dispositivos usando Olá atualização de aniversário do Windows 10.



**Ação recomendada**  
Nenhuma. Atualizações futuras tooWindows pode resolver esse problema.

---

### <a name="date-time-and-region-settings-do-not-sync-on-domain-joined-device"></a>As configurações de data, hora e região não sincronizam no dispositivo associado ao domínio 
  
Dispositivos que ingressaram no domínio não terão a sincronização para Olá configuração de região de data e hora: hora automática. Usando o horário automático pode substituição Olá outras configurações de data, hora e região e fazer com que essas configurações não toosync. 

**Ação recomendada**  
Nenhuma. 

---

### <a name="uac-prompts-when-syncing-passwords"></a>O UAC é ativado ao sincronizar senhas

Dispositivos afeta executando Olá atualização de novembro Windows 10 (versão 1511) com uma placa de rede sem fio é configurado toosync senhas.

**Ação recomendada**  
Certifique-se de cliente de v1511 Olá Windows 10 tem Olá atualização cumulativa ([KB3140743](https://support.microsoft.com/kb/3140743) 10586.494 de compilação do sistema operacional).

---

### <a name="sync-does-not-work-on-devices-that-use-smart-card-for-login"></a>A sincronização não funciona em dispositivos que usam cartões inteligentes para login
Se você tentar toosign no dispositivo do Windows tooyour usando um cartão inteligente ou cartão inteligente virtual, sincronização de configurações irá parar de funcionar.     

**Ação recomendada**  
Nenhuma. Atualizações futuras tooWindows pode resolver esse problema.

---

### <a name="domain-joined-device-is-not-syncing-after-leaving-corporate-network"></a>O dispositivo associado ao domínio não está sincronizando após deixar a rede corporativa     
Dispositivos que ingressaram no domínio registrado tooAzure que AD pode apresentar falha de sincronização se o dispositivo Olá é externo por longos períodos de tempo, e não pode concluir a autenticação de domínio.

**Ação recomendada**  
Conecte-se a rede corporativa da saudação dispositivo tooa para que possa retomar a sincronização.

---

 ### <a name="azure-ad-joined-device-is-not-syncing-and-hello-user-has-a-mixed-case-user-principal-name"></a>Dispositivos de ingressados do AD do Azure não está sincronizando e usuário Olá tem um nome Principal do usuário com maiusculas.
 Se usuário Olá tem uma maiusculas e minúsculas UPN (por exemplo, nome de usuário em vez do nome de usuário) e usuário Olá estiver em um dispositivo associado do AD do Azure que foi atualizado do Windows 10 Build 10586 too14393, dispositivo saudação do usuário pode falhar toosync. 

**Ação recomendada**  
usuário Olá será necessário toounjoin e reingressar Olá dispositivo toohello nuvem. toodo isso, faça logon como usuário de Administrador Local hello e sair do dispositivo Olá indo muito**configurações** > **sistema** > **sobre** e selecione " Gerenciar ou desconectar do trabalho ou escola." Limpar arquivos de saudação abaixo e, em seguida, junção do Azure AD Olá dispositivo novamente no **configurações** > **sistema** > **sobre** e selecionando "conectar-se tooWork ou estudante". Continue toojoin Olá dispositivo tooAzure do Active Directory e o fluxo de saudação concluída.

Na etapa de limpeza hello, Olá limpeza seguintes arquivos:
- Settings.dat em `C:\Users\<Username>\AppData\Local\Packages\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy\Settings\`
- Todos os arquivos Olá Olá pasta`C:\Users\<Username>\AppData\Local\Packages\Microsoft.AAD.BrokerPlugin_cw5n1h2txyewy\AC\TokenBroker\Account`

---

### <a name="event-id-6065-80070533-this-user-cant-sign-in-because-this-account-is-currently-disabled"></a>ID de evento 6065: 80070533 Este usuário não pode fazer login porque esta conta está desabilitada no momento  
No Visualizador de eventos em logs de SettingSync/depuração hello, esse erro pode ser visto quando as credenciais do usuário Olá expiraram. Além disso, pode ocorrer quando o locatário Olá não tinha automaticamente AzureRMS provisionados. 

**Ação recomendada**  
No primeiro caso de Olá, ter a atualizar suas credenciais e o dispositivo de toohello de logon com as novas credenciais de saudação do usuário de hello. Olá toosolve AzureRMS problema, prosseguir com a saudação etapas listadas na [KB3193791](https://support.microsoft.com/kb/3193791). 

---

### <a name="event-id-1098-error-0xcaa5001c-token-broker-operation-failed"></a>ID do evento 1098: Erro: Falha na operação do agente de Token 0xCAA5001C  
No Visualizador de eventos em logs AAD/Operational hello, esse erro pode ser visto com o evento 1104: chamada de plug-in do AAD nuvem Pacífico obter token retornou o erro: 0xC000005F. Esse problema ocorre se estiverem faltando permissões ou atributos de propriedade.    

**Ação recomendada**  
Continuar com a saudação etapas listadas [KB3196528](https://support.microsoft.com/kb/3196528).  



## <a name="next-steps"></a>Próximas etapas

- Saudação de uso [Fórum de voz do usuário](https://feedback.azure.com/forums/169401-azure-active-directory/category/158658-enterprise-state-roaming) tooprovide sugestões de comentários e verifique em como o Roaming de estado tooimprove Enterprise.

- Para obter mais informações, consulte Olá [visão geral do Roaming de estado do Enterprise](active-directory-windows-enterprise-state-roaming-overview.md). 

## <a name="related-topics"></a>Tópicos relacionados
* [Visão geral do enterprise state roaming](active-directory-windows-enterprise-state-roaming-overview.md)
* [Habilitar o enterprise state roaming no Active Directory do Azure](active-directory-windows-enterprise-state-roaming-enable.md)
* [Perguntas frequentes sobre configurações e roaming de dados](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Política de grupo e as configurações do MDM para a sincronização de configurações](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Referência de configurações de roaming do Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
