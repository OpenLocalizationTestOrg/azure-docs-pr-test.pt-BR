Você pode conectar tooa VM é implantada tooyour VNet, criando um VM do tooyour de Conexão de área de trabalho remota. Hello tooinitially de maneira recomendada verificar se você pode se conectar tooyour VM é tooconnect por usando seu IP privado de endereços, em vez do nome do computador. Dessa forma, você está testando toosee se você puder se conectar, não se a resolução de nomes está configurada corretamente.

1. Localize o endereço IP privado de saudação. Você pode encontrar o endereço IP privado de saudação de uma VM de várias maneiras. A seguir, mostramos etapas Olá Olá portal do Azure e do PowerShell.

  - Portal do Azure - localizar sua máquina virtual no portal do Azure de saudação. Exibir as propriedades de saudação do hello VM. endereço IP privado de saudação é listado.

  - PowerShell - Use Olá exemplo tooview uma lista de máquinas virtuais e endereços IP privados de seus grupos de recursos. Você não precisa toomodify Este exemplo antes de usá-lo.

    ```powershell
    $VMs = Get-AzureRmVM
    $Nics = Get-AzureRmNetworkInterface | Where VirtualMachine -ne $null

    foreach($Nic in $Nics)
    {
      $VM = $VMs | Where-Object -Property Id -eq $Nic.VirtualMachine.Id
      $Prv = $Nic.IpConfigurations | Select-Object -ExpandProperty PrivateIpAddress
      $Alloc = $Nic.IpConfigurations | Select-Object -ExpandProperty PrivateIpAllocationMethod
      Write-Output "$($VM.Name): $Prv,$Alloc"
    }
    ```

2. Verifique se você está conectado tooyour VNet usando a conexão de VPN hello.
3. Abra **Conexão de área de trabalho remota** digitando "RDP" ou "Conexão de área de trabalho remota" na caixa de pesquisa de saudação na barra de tarefas hello, em seguida, selecionar Conexão de área de trabalho remota. Você também pode abrir a Conexão de área de trabalho remota usando o comando de 'mstsc' hello no PowerShell. 
4. Na Conexão de área de trabalho remota, insira o endereço IP privado de saudação do hello VM. Você pode em configurações adicionais de tooadjust "Mostrar opções", e se conectar.

### <a name="tootroubleshoot-an-rdp-connection-tooa-vm"></a>tootroubleshoot uma conexão de RDP tooa VM

Se você estiver tendo problemas para se conectar a máquina virtual de tooa sobre sua conexão VPN, verifique o seguinte hello:

- Verifique se a conexão VPN é estabelecida.
- Verifique se você estiver se conectando a endereço IP privado de toohello para Olá VM.
- Se você puder se conectar toohello VM usando IP privado Olá endereço, mas não Olá nome do computador, verifique se você configurou o DNS corretamente. Para obter mais informações sobre como funciona a resolução de nome para VMs, confira [Resolução de nomes para VMs](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).
- Para obter mais informações sobre conexões RDP, consulte [tooa de conexões de área de trabalho remota solucionar VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).
