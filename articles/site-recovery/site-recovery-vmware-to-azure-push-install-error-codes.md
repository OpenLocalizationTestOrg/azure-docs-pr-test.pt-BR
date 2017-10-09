---
title: "aaaAzure Solucionando problemas de recuperação de Site do VMware tooAzure | Microsoft Docs"
description: "Solução de erros durante a replicação de máquinas virtuais do Azure"
services: site-recovery
documentationcenter: 
author: asgang
manager: srinathv
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/24/2017
ms.author: asgang
ms.openlocfilehash: 912097c8892540dd798ba025e0b10374ca51d664
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-mobility-service-push-install-issues"></a>Solução de problemas de instalação por push do Serviço de Mobilidade

Este artigo fornece detalhes sobre problemas comuns de saudação enfrentados durante a tentativa de saudação tooinstall serviço de mobilidade no servidor de toosource para habilitar a proteção.

## <a name="error-code-95107-protection-could-not-be-enabled"></a>(Código de erro 95107) Não foi possível habilitar a proteção.
**Código de erro** | **Possíveis causas:** | **Recomendações específicas ao erro**
--- | --- | ---
95107 </br>***Mensagem -*** instalação por Push do computador de origem toohello do serviço de mobilidade Olá falhou com código de erro ***EP0858***. <br> O que credenciais Olá fornecida tooinstall serviço de mobilidade está incorreta ou Olá conta de usuário tem privilégios insuficientes | As credenciais do usuário fornecida tooinstall serviço de mobilidade no computador de origem está incorreto | Verifique as credenciais do usuário Olá fornecidas Olá computador de origem no servidor de configuração estão corretas. <br> as credenciais do usuário tooadd/editar: vá tooconfiguration server > Cspsconfigtool ícone > Gerenciar conta. </br> Além disso, certifique-se abaixo os pré-requisitos são toosuccessfully check concluir instalação.

## <a name="error-code-95015-protection-could-not-be-enabled"></a>(Código de erro 95015) Não foi possível habilitar a proteção.
**Código de erro** | **Possíveis causas:** | **Recomendações específicas ao erro**
--- | --- | ---
95105 </br>***Mensagem -*** instalação por Push do computador de origem toohello do serviço de mobilidade Olá falhou com código de erro ***EP0856***. <br> O "Compartilhamento de arquivos e impressoras" não permitida no computador de origem hello, ou há problemas de conectividade de rede entre o servidor de processo hello e o computador de origem de saudação| O compartilhamento de arquivos e impressoras não está habilitado | Permitir "E impressora compartilhamento de arquivos" no computador de origem de saudação em Olá Firewall do Windows, vá toohello da máquina de origem > em Firewall do Windows > "Permitir que um aplicativo ou recurso pelo Firewall" > Selecionar "Compartilhamento de arquivos e impressora para todos os perfis". </br> Além disso, certifique-se abaixo os pré-requisitos são toosuccessfully check concluir instalação.

## <a name="error-code-95117-protection-could-not-be-enabled"></a>(Código de erro 95117) Não foi possível habilitar a proteção.
**Código de erro** | **Possíveis causas:** | **Recomendações específicas ao erro**
--- | --- | ---
95117 </br>***Mensagem -*** instalação por Push do computador de origem toohello do serviço de mobilidade Olá falhou com código de erro ***EP0865***. <br> O computador de origem Olá não está em execução ou há problemas de conectividade de rede entre o servidor de processo hello e o computador de origem de saudação | Conectividade de rede entre o servidor em processo e o servidor de origem | Verifique a conectividade entre o servidor em processo e o servidor de origem. </br> Além disso, certifique-se abaixo os pré-requisitos são toosuccessfully check concluir instalação.

## <a name="error-code-95103-protection-could-not-be-enabled"></a>(Código de erro 95103) Não foi possível habilitar a proteção.
**Código de erro** | **Possíveis causas:** | **Recomendações específicas ao erro**
--- | --- | ---
95103 </br>***Mensagem -*** instalação por Push do computador de origem toohello do serviço de mobilidade Olá falhou com código de erro ***EP0854***. <br> O "Windows Management Instrumentation (WMI)" não é permitida no computador de origem hello, ou há problemas de conectividade de rede entre o servidor de processo hello e o computador de origem de saudação| Windows Management Instrumentation (WMI) bloqueado Olá Firewall do Windows | Permitir o Windows Management Instrumentation (WMI) no hello Firewall do Windows. Em configurações do Firewall do Windows > “Permitir um aplicativo ou recurso pelo Firewall” > “selecionar o WMI para todos os perfis”. </br> Além disso, certifique-se abaixo os pré-requisitos são toosuccessfully check concluir instalação.

## <a name="check-push-install-logs-for-errors"></a>Verificar se há erros nos Logs de Instalação por Push

No servidor de processo de configuração/hello, navegar toofile 'PushinstallService' localizado em <Microsoft Azure Site Recovery Install Location>\home\svsystems\pushinstallsvc\ origem de saudação toounderstand do problema hello e use abaixo problema de saudação tooresolve etapas de solução de problemas.</br>
![pushiinstalllogs](./media/site-recovery-protection-common-errors/pushinstalllogs.png)

## <a name="push-install-pre-requisites-for-windows"></a>Pré-requisitos da Instalação por Push para o Windows
### <a name="ensure-file-and-printer-sharing-is-enabled"></a>Verificar se a opção “Compartilhamento de Arquivos e Impressoras” está habilitada
Permitir que o "Compartilhamento de arquivos e impressoras" e "Windows Management Instrumentation" no computador de origem de saudação em Olá Firewall do Windows </br>
#### <a name="if-source-machine-is-domain-joined-br"></a>Se o computador de origem for ingressado no domínio: </br>
Defina as configurações de firewall usando o GPMC (Console de Gerenciamento de Política de Grupo).
1. Domínio de login do diretório tooActive do computador como administrador e abra o Console de gerenciamento de diretiva de grupo (GPMC. MSC, executar a partir de uma inicialização > execute).</br>
3. Se o GPMC não estiver instalado, siga o link de saudação muito[Olá instalar o GPMC](https://technet.microsoft.com/library/cc725932.aspx) </br>
4. Na árvore de console do GPMC hello, clique duas vezes em objetos de política de grupo no domínio e floresta hello e navegue muito "Política de domínio padrão". </br>
![gpmc1](./media/site-recovery-protection-common-errors/gpmc1.png) </br>
</br>
5. Clique com o botão direito do mouse em “Política de Domínio Padrão” > Editar > uma nova janela “Editor de Gerenciamento de Política de Grupo” será aberta. </br>
![gpmc2](./media/site-recovery-protection-common-errors/gpmc2.png) </br>
</br>
6. No hello Editor de gerenciamento de diretiva de grupo, navegue tooComputer Configuração > Políticas > modelos administrativos > rede > conexões de rede > Firewall do Windows. </br>
![gpmc3](./media/site-recovery-protection-common-errors/gpmc3.png) </br>
</br>
7. Habilitar Olá seguindo as configurações de perfil do domínio e perfil padrão </br>
a) Clique duas vezes na exceção “Firewall do Windows: permitir exceção de compartilhamento de arquivos e impressoras de entrada”. Selecione Habilitado e clique em OK. </br>
b) Clique duas vezes na exceção “Firewall do Windows: permitir exceção de administração remota de entrada”. Selecione Habilitado e clique em OK. </br>
![gpmc4](./media/site-recovery-protection-common-errors/gpmc4.png) </br>
</br>

###### <a name="if-source-machine-is-not-domain-joined-and-part-of-workgroup-br"></a>Se o computador de origem não estiver ingressado no domínio e fizer parte de um grupo de trabalho </br>
Defina as configurações de firewall no computador remoto (para o grupo de trabalho):
1. Acesse o computador de origem toohello,</br>
2. Em configurações do Firewall do Windows > “Permitir um aplicativo ou recurso pelo Firewall” > selecione “Compartilhamento de Arquivos e Impressoras para todos os perfis”. </br>
3. Em configurações do Firewall do Windows > “Permitir um aplicativo ou recurso pelo Firewall” > “selecionar o WMI para todos os perfis”. </br>

#### <a name="disable-remote-user-account-control-uac"></a>Desabilitar o UAC (Controle de Conta de Usuário)
Desabilite o UAC usando o serviço de mobilidade de saudação de toopush chave do registro.
1. Clique em Iniciar > Executar > digite regedit > ENTER
2. Localize e, em seguida, clique em Olá seguinte subchave do registro: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System
3. Se não existir Olá entrada do registro LocalAccountTokenFilterPolicy, execute estas etapas:
4. No menu de editar hello > Novo > clique em valor DWORD.
5. Digite LocalAccountTokenFilterPolicy e, em seguida, pressione ENTER.
6. Clique com o botão direito do mouse em LocalAccountTokenFilterPolicy e, em seguida, clique em Modificar.
7. Na caixa de dados do valor hello, digite 1 e, em seguida, clique em Okey.
8. Saia do Editor do Registro.


## <a name="push-install-pre-requisites-for-linux"></a>Pré-requisitos da Instalação por Push para o Linux:

1. Crie um usuário raiz no servidor do hello origem Linux. (Use esta conta somente para atualizações e a instalação por push Olá)</br>
2. Verifique o arquivo /etc/hosts Olá na fonte Olá Linux server tem entradas que mapeiam Olá nome do host local tooIP endereços associados a todos os adaptadores de rede. </br>
3. Certifique-se de hello mais recente openssh, servidor openssh e openssl os pacotes são instalados no servidor Linux de origem. </br>
Verifique se a porta 22 SSH está habilitada e em execução. </br>
4. Verifique se as entradas obsoletas de agentes já estão presentes no servidor de origem hello, desinstalar os agentes de mais antigos de saudação e reinicializar o servidor de saudação, reinstale o agente. </br>

#### <a name="enable-sftp-subsystem-and-password-authentication-in-hello-sshdconfig-file"></a>Habilitar a autenticação de SFTP subsistema e a senha no arquivo de sshd_config Olá
1. No servidor de origem, entre como raiz. </br>
2. No arquivo de /etc/ssh/sshd_config de saudação,</br> Localize a linha de saudação que começa com PasswordAuthentication. </br>
3. d.   Descomente a linha hello e altere o valor de saudação de "não" muito "Sim". </br>
![Linux1](./media/site-recovery-protection-common-errors/linux1.png)
4. Localizar a linha de saudação que começa com "Subsistema" e remova os comentários de linha de saudação. </br>
![Linux2](./media/site-recovery-protection-common-errors/linux2.png)
5. Salvar alterações de saudação e reinicie o serviço de sshd hello. </br>

## <a name="push-installation-checks-on-configurationprocess-server"></a>A Instalação por Push verifica o servidor de Configuração/em Processo.
#### <a name="validate-credentials-for-discovery-and-installation"></a>Validar as credenciais para descoberta e instalação

1. No Servidor de Configuração, inicie Cspsconfigtool</br>
![WMItestConnect5](./media/site-recovery-protection-common-errors/wmitestconnect5.png) </br>

2. Certifique-se de que a conta Olá usada para proteção tem direitos de administrador no computador de origem de saudação. </br>

#### <a name="check-connectivity-between-process-server-and-source-server"></a>Verificar a conectividade entre o servidor em processo e o servidor de origem
1. Verifique se o Servidor em Processo tem conexão com a Internet.
2. Verifique a conexão do WMI usando wbemtest.exe. </br>
No servidor de processo hello, clique em Iniciar > Executar > wbemtest.exe > Testador de instrumentação de gerenciamento do Windows a janela será aberta como mostrado.</br>
   ![WMItestConnect1](./media/site-recovery-protection-common-errors/wmitestconnect1.png) </br>
   </br>
Clique em conectar > Insira Olá IP do servidor de origem em nome de usuário de entrada de Namespace hello e senha (se o computador de origem está associado a um domínio, fornecer nome de domínio de saudação junto com o nome de usuário como "NomeDeDomínio \ nomedeusuário". Se o computador de origem estiver em workgroup, forneça apenas o nome de usuário hello.) Selecione o nível de autenticação hello como privacidade do pacote. </br>
![WMItestConnect2](./media/site-recovery-protection-common-errors/wmitestconnect2.png) </br>
   </br>
   Clique em Conectar. Agora conexão de WMI Olá deve ser bem-sucedida com hello fornecida dados e deve ser exibida a janela do Testador de instrumentação de gerenciamento do Windows hello conforme mostrado abaixo: </br>
   ![WMItestConnect3](./media/site-recovery-protection-common-errors/wmitestconnect3.png) </br>
</br>
   Se a conexão do WMI não for bem-sucedida, um pop-up de mensagem de erro será exibido. Olá captura de tela abaixo mostra uma tentativa malsucedida se WMI/Remote Administration não está habilitada no firewall do Windows permitido aplicativo. </br>
   ![WMItestConnect4](./media/site-recovery-protection-common-errors/wmitestconnect4.png) </br>
</br>

3. Verifique o status do WMI Olá e conectividade.</br>
No servidor de processo de configuração/Olá, </br>
Clique em Iniciar > Executar > wmimgmt.msc > Ações > mais ações > conectar computador tooanother (computador de origem). </br>
Insira as credenciais de saudação da conta Olá usado para proteção e verifique se a conectividade é bom. </br>

#### <a name="verify-network-shared-folders-of-source-machine-is-accessible-from-process-server-ps-remotely-using-specified-credentials"></a>Verificar se a pastas compartilhadas de rede do computador de origem são acessíveis no PS (Servidor em Processo) remotamente usando as credenciais especificadas.
  1. Máquina de servidor (PS) tooProcess logon, o Explorador de arquivos abertos > no tipo de barra de endereço hello > "\\\source-machine-ip\C$" > clique em Enter. </br>
  ![Fileshare1](./media/site-recovery-protection-common-errors/fileshare1.png) </br>
  2. O Explorador de Arquivos solicitará as credenciais. Digite hello username e password > clique Okey.</br>
   Se o computador de origem está associado a um domínio, forneça o nome de domínio de saudação junto com o nome de usuário como "NomeDeDomínio \ nomedeusuário".</br>
   Se o computador de origem estiver em workgroup, forneça apenas hello "username". </br>
  ![Fileshare2](./media/site-recovery-protection-common-errors/fileshare2.png) </br>
  3. Se a conexão for bem-sucedida, você pode exibir pastas de saudação da máquina de origem remotamente do processo de servidor (PS) </br>
  ![Fileshare3](./media/site-recovery-protection-common-errors/fileshare3.png) </br>

> [!NOTE] 
> Se a conexão não for bem-sucedida, verifique se todos os pré-requisitos foram atendidos.
>

Se você não quiser tooopen "Windows Management Instrumentation", você também pode instalar o serviço de mobilidade manualmente no computador de origem de saudação.</br> [Instalar o Serviço de Mobilidade manualmente por meio da GUI](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) </br>
[Diretrizes de instalação por meio do Configuration Manager](site-recovery-install-mobility-service-using-sccm.md) </br>

## <a name="next-steps"></a>Próximas etapas
- [Habilitar a replicação em máquinas virtuais do VMware](vmware-walkthrough-enable-replication.md)
