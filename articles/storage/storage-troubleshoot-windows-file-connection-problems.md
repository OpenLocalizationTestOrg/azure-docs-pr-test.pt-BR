---
title: problemas de armazenamento de arquivo do Azure aaaTroubleshoot no Windows | Microsoft Docs
description: "Solução de problemas de Armazenamento de Arquivos do Azure File no Windows"
services: storage
documentationcenter: 
author: genlin
manager: willchen
editor: na
tags: storage
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: genli
ms.openlocfilehash: ba0315d1add76a27fec93a9aee3aa99ccb7fa164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a>Solução de problemas de Armazenamento de Arquivos do Azure File no Windows

Este artigo lista os problemas comuns que estão relacionada tooMicrosoft armazenamento de arquivo do Azure durante a conexão de clientes do Windows. Também fornece as possíveis causas e resoluções para esses problemas. Além de solução de problemas de toohello as etapas neste artigo, você também pode usar [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) para garantir que Windows hello o ambiente do cliente tem pré-requisitos corretos. AzFileDiagnostics automatiza a detecção da maioria dos sintomas Olá mencionados neste artigo e ajuda a configurar o desempenho ideal do ambiente tooget. Você também pode encontrar essas informações no hello [solução de problemas de compartilhamentos de arquivos do Azure](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) que fornece etapas tooassist com problemas de compartilhamentos de arquivos do Azure conectando/mapeamento/montagem.


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a>Erro 53, Erro 67 ou Erro 87 ao montar ou desmontar um compartilhamento de arquivos do Azure

Quando você tenta toomount um compartilhamento de arquivos do local ou de um datacenter diferente, você poderá receber Olá os erros a seguir:

- Ocorreu um erro de sistema 53. caminho de rede Olá não foi encontrado.
- Ocorreu um erro de sistema 67. nome da rede Olá não pode ser encontrado.
- Ocorreu um erro de sistema 87. Olá parâmetro está incorreto.

### <a name="cause-1-unencrypted-communication-channel"></a>Causa 1: Canal de comunicação não criptografado

Por motivos de segurança, conexões tooAzure compartilhamentos de arquivos estão bloqueados se o canal de comunicação Olá não é criptografado e tentativa de conexão de saudação não é feita de Olá mesmo datacenter onde residem os compartilhamentos de arquivos do Azure de saudação. Criptografia de canal de comunicação é fornecida apenas se o sistema operacional do cliente do usuário Olá dá suporte a criptografia SMB.

O Windows 8, o Windows Server 2012 e versões posteriores de cada solicitação de negociação de sistema que inclua o SMB 3.0, que dá suporte à criptografia.

### <a name="solution-for-cause-1"></a>Solução para a causa 1

Conecte-se de um cliente que executa um dos seguintes hello:

- Atende aos requisitos de saudação do Windows 8 e Windows Server 2012 ou versões posteriores
- Conecta-se em uma máquina virtual no hello mesmo datacenter como Olá conta de armazenamento do Azure que é usada para compartilhamento de arquivos do Azure Olá

### <a name="cause-2-port-445-is-blocked"></a>Causa 2: A porta 445 está bloqueada

Erro de sistema 53 ou sistema 67 pode ocorrer se a porta 445 comunicação de saída tooan arquivo do Azure storage datacenter está bloqueada. Resumo de saudação toosee de provedores que permitir ou impedir o acesso de porta 445, ir muito[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).

toounderstand se essa é a razão de saudação atrás de mensagem de "Erro de sistema 53" Olá, você pode usar o ponto de extremidade do Portqry tooquery Olá TCP:445. Se o ponto de extremidade do hello TCP:445 é exibido como filtrado, Olá a porta TCP será bloqueado. Veja um exemplo de consulta:

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

Se a porta TCP 445 está bloqueada por uma regra de caminho de rede hello, você verá Olá saída a seguir:

  `TCP port 445 (microsoft-ds service): FILTERED`

Para obter mais informações sobre como toouse Portqry, consulte [descrição do utilitário de linha de comando do hello Portqry.exe](https://support.microsoft.com/help/310099).

### <a name="solution-for-cause-2"></a>Solução para a causa 2

Trabalhar com a porta de tooopen do departamento de IT 445 saída muito[intervalos de IP do Azure](https://www.microsoft.com/download/details.aspx?id=41653).

### <a name="cause-3-ntlmv1-is-enabled"></a>Causa 3: NTLMv1 está habilitado

Erro de sistema 53 ou sistema 87 pode ocorrer se a comunicação NTLMv1 está habilitada no cliente de saudação. O Armazenamento de Arquivos do Azure dá suporte apenas à autenticação NTLMv2. Ter NTLMv1 habilitado faz com que o cliente esteja menos seguro. Portanto, a comunicação será bloqueada para o Armazenamento de Arquivos do Azure. 

toodetermine se esta é a causa Olá Olá erro, verifique se esse Olá seguinte subchave do registro está definida tooa valor de 3:

**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**

Para obter mais informações, consulte Olá [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) tópico no TechNet.

### <a name="solution-for-cause-3"></a>Solução para a causa 3

Reverter Olá **LmCompatibilityLevel** toohello valor padrão 3 na seguinte subchave do registro de saudação do valor:

  **HKLM\SYSTEM\CurrentControlSet\Control\Lsa**

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-tooprocess-this-command-when-you-copy-tooan-azure-file-share"></a>Erro 1816 "não há cota suficiente está disponível tooprocess este comando" quando você copia tooan compartilhamento de arquivos do Azure

### <a name="cause"></a>Causa

Erro 1816 ocorre quando você atingir o limite superior de saudação de identificadores abertos simultâneos permitidas para um arquivo no computador de saudação em que o compartilhamento de arquivo hello está sendo montado.

### <a name="solution"></a>Solução

Reduzir o número de saudação de identificadores abertos simultâneos fechando alguns identificadores e, em seguida, tente novamente. Para obter mais informações, consulte [Lista de verificação de desempenho e escalabilidade do Armazenamento do Microsoft Azure](storage-performance-checklist.md).

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-windows"></a>Arquivos lenta copiando tooand do armazenamento de arquivo do Azure no Windows

Você pode ver o desempenho lento ao tentar tootransfer arquivos toohello serviço arquivo do Azure.

- Se você não tiver um requisito de tamanho de e/s mínimo específico, é recomendável que você use 1 MB como Olá tamanho de e/s para o desempenho ideal.
-   Se você souber o tamanho final de saudação de um arquivo que você estiver estendendo com grava e o software não tem problemas de compatibilidade quando final não gravada no arquivo hello hello contém zeros, em seguida, conjunto Olá tamanho do arquivo com antecedência, em vez de fazer cada gravação uma gravação estendendo.
-   Use o método de cópia de direito de saudação:
    -   Use o [AzCopy](storage-use-azcopy.md#file-copy) para todas as transferências entre dois compartilhamentos de arquivo.
    -   Use o [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) entre um compartilhamento de arquivos e um computador local.

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a>Considerações para Windows 8.1 ou Windows Server 2012 R2

Para clientes que executam o Windows 8.1 ou Windows Server 2012 R2, certifique-se de que Olá [KB3114025](https://support.microsoft.com/help/3114025) hotfix foi instalado. Este hotfix melhora o desempenho de saudação de criar e fechar identificadores.

Você pode executar Olá toocheck de script a seguir se Olá hotfix foi instalado:

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

Se o hotfix foi instalado, hello seguinte saída é exibida:

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> As imagens do Windows Server 2012 R2 no Azure Marketplace têm o hotfix KB3114025 instalado por padrão desde dezembro de 2015.

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a>Nenhuma pasta com uma letra de unidade em **Meu Computador**

Se você mapear um compartilhamento de arquivos do Azure como administrador por meio do uso de rede, o compartilhamento de saudação aparece toobe ausente.

### <a name="cause"></a>Causa

Por padrão, o Explorador de Arquivos do Windows não é executado como administrador. Se você executar o uso de rede em um prompt de comando administrativo, Mapear unidade de rede hello como um administrador. Como unidades mapeadas são centrado no usuário, conta de usuário de saudação que está conectada não exibe Olá unidades se eles estão montados em uma conta de usuário diferente.

### <a name="solution"></a>Solução
Compartilhamento de saudação montagem de uma linha de comando não administrador. Como alternativa, você pode seguir [neste tópico TechNet](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure Olá **EnableLinkedConnections** o valor do registro.

<a id="netuse"></a>
## <a name="net-use-command-fails-if-hello-storage-account-contains-a-forward-slash"></a>Comando NET use falhará se a conta de armazenamento Olá contém uma barra invertida

### <a name="cause"></a>Causa

comando net use de saudação interpreta uma barra invertida (/) como uma opção de linha de comando. Se o nome da sua conta de usuário começa com uma barra invertida, o mapeamento de unidade Olá falhará.

### <a name="solution"></a>Solução

Você pode usar o hello etapas toowork problema Olá a seguir:

- Execute Olá comando PowerShell a seguir:

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  De um arquivo em lotes, você pode executar o comando de saudação desta forma:

  `Echo new-smbMapping ... | powershell -command –`

- Coloque aspas duplas em torno de saudação toowork de chave alternativa para esse problema – a menos que a barra de saudação é Olá primeiro caractere. Se for, usar o modo interativo hello e insira sua senha separadamente ou regenerar sua chaves tooget uma chave que não começa com uma barra invertida.

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a>O aplicativo ou serviço não pode acessar a unidade montada dos Arquivos do Azure

### <a name="cause"></a>Causa

As unidades são montadas por usuário. Se seu aplicativo ou serviço estiver em execução sob uma conta de usuário diferente de saudação que Olá unidade montada, o aplicativo hello não verá unidade hello.

### <a name="solution"></a>Solução

Use uma saudação soluções a seguir:

-   Montar a unidade de saudação do hello mesma conta de usuário que contém o aplicativo hello. Você pode usar uma ferramenta como o PsExec.
- Passe o nome de conta de armazenamento hello e a chave nos parâmetros de nome e senha de usuário de saudação do comando net use de saudação.

Depois de seguir estas instruções, você poderá receber Olá a seguinte mensagem de erro quando você executa o uso de rede para a conta de serviço de rede do sistema Olá: "Erro de sistema 1312 ocorreu. Uma sessão de logon especificada não existe. Talvez ela já tenha sido finalizada.” Se isso ocorrer, verifique se esse nome de usuário de saudação que é passado toonet uso inclui informações de domínio (por exemplo: "[nome de conta de armazenamento]. file.core.windows .net").

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-tooa-destination-that-does-not-support-encryption"></a>Erro "Você está copiando um arquivo de destino de tooa que não dá suporte à criptografia"

Quando um arquivo é copiado pela rede hello, arquivo hello é descriptografado no computador de origem hello, transmitidas em texto não criptografado e criptografados novamente no destino hello. No entanto, você poderá ver o erro a seguir quando estiver tentando toocopy um arquivo criptografado de saudação: "Você está copiando destino Olá de tooa de arquivo que não dá suporte à criptografia".

### <a name="cause"></a>Causa
Esse problema pode ocorrer se você estiver usando o sistema de arquivos com criptografia (EFS). Arquivos criptografados pelo BitLocker podem ser copiados tooAzure o armazenamento de arquivos. No entanto, o Armazenamento de Arquivos do Azure não dá suporte a EFS NTFS.

### <a name="workaround"></a>Solução alternativa
toocopy um arquivo pela rede hello, você deve primeiro descriptografá-lo. Use um dos métodos a seguir de saudação:

- Saudação de uso **copiar /d** comando. Olá criptografado permite que arquivos toobe salvo como arquivos descriptografados no destino hello.
- Saudação de conjunto de chave do registro a seguir:
  - Caminho = HKLM\Software\Policies\Microsoft\Windows\System
  - Tipo de valor = DWORD
  - Name = CopyFileAllowDecryptedRemoteDestination
  - Value = 1

Lembre-se de que essa chave de registro de saudação configuração afeta todas as operações de cópia que ficam toonetwork compartilhamentos.

## <a name="need-help-contact-support"></a>Precisa de ajuda? Entre em contato com o suporte.
Se você ainda precisar de Ajuda, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget o problema foi resolvido rapidamente.
