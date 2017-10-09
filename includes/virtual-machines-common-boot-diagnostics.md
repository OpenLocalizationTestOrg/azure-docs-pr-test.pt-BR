O suporte a dois recursos de depuração agora está disponível no Azure: Saída do Console e a Captura de Tela para o modelo de implantação do Resource Manager de Máquinas Virtuais do Azure. 

Ao colocar tooAzure sua própria imagem ou até mesmo inicialização uma das imagens da plataforma Olá, pode haver várias razões por que uma máquina Virtual entra em um estado não inicializável. Habilitar esses recursos você tooeasily diagnosticar e recuperar suas máquinas virtuais de falhas de inicialização.

Para máquinas de virtuais de Linux, você pode facilmente exibir saída de hello de seu log de console da saudação Portal:

![Portal do Azure](./media/virtual-machines-common-boot-diagnostics/screenshot1.png)
 
No entanto, para o Windows e máquinas virtuais do Linux Azure também permite que toosee uma captura de tela de Olá VM do hipervisor hello:

![Erro](./media/virtual-machines-common-boot-diagnostics/screenshot2.png)

Esses dois recursos têm suporte em máquinas virtuais do Azure em todas as regiões. Observe, capturas de tela e saída podem demorar até too10 minutos tooappear na sua conta de armazenamento.

## <a name="common-boot-errors"></a>Erros comuns de inicialização

- [0xC000000E](https://support.microsoft.com/help/4010129)
- [0xC000000F](https://support.microsoft.com/help/4010130)
- [0xC0000011](https://support.microsoft.com/help/4010134)
- [0xC0000034](https://support.microsoft.com/help/4010140)
- [0xC0000098](https://support.microsoft.com/help/4010137)
- [0xC00000BA](https://support.microsoft.com/help/4010136)
- [0xC000014C](https://support.microsoft.com/help/4010141)
- [0xC0000221](https://support.microsoft.com/help/4010132)
- [0xC0000225](https://support.microsoft.com/help/4010138)
- [0xC0000359](https://support.microsoft.com/help/4010135)
- [0xC0000605](https://support.microsoft.com/help/4010131)
- [Não foi possível encontrar um sistema operacional](https://support.microsoft.com/help/4010142)
- [Falha de inicialização ou INACCESSIBLE_BOOT_DEVICE](https://support.microsoft.com/help/4010143)

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a>Habilitar o diagnóstico em uma nova máquina virtual
1. Ao criar uma nova máquina Virtual do Portal de visualização de saudação, selecione Olá **do Azure Resource Manager** na lista suspensa de modelo de implantação de saudação:
 
    ![Gerenciador de Recursos](./media/virtual-machines-common-boot-diagnostics/screenshot3.jpg)

2. Configure Olá conta de armazenamento de saudação do monitoramento opção tooselect em que você deseja tooplace esses arquivos de diagnóstico.
 
    ![Criar VM](./media/virtual-machines-common-boot-diagnostics/screenshot4.jpg)

3. Se você estiver implantando um modelo do Azure Resource Manager, navegue tooyour recurso de máquina Virtual e acrescentar a seção de perfil de diagnóstico hello. Lembre-se o cabeçalho de versão de API do toouse hello "2015-06-15".

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. perfil de diagnóstico Olá permite tooselect conta de armazenamento de saudação onde você deseja tooput esses logs.

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

toodeploy um exemplo de máquina Virtual com o diagnóstico de inicialização habilitado, Confira nosso repositório aqui.

## <a name="update-an-existing-virtual-machine"></a>Atualizar uma máquina virtual existente ##

Diagnóstico de inicialização tooenable por meio de saudação Portal, você também pode atualizar uma máquina Virtual existente por meio do Portal de saudação. Selecione Olá opção de diagnóstico de inicialização e salvar. Reinicie o efeito de tootake VM hello.

![Atualizar VM existente](./media/virtual-machines-common-boot-diagnostics/screenshot5.png)

