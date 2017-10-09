


Este tópico descreve como:

* Injetar dados em uma VM (máquina virtual) do Azure quando está sendo provisionada.
* Recuperá-los para Windows e Linux.
* Use ferramentas especiais disponíveis em alguns sistemas toodetect e manipular dados personalizados automaticamente.

> [!NOTE]
> Este artigo descreve os dados como personalizada pode ser inserida por meio de uma máquina virtual criada com hello API de gerenciamento de serviços do Azure. toosee como toouse Olá API de gerenciamento de recursos do Azure, consulte [modelo de exemplo hello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).
> 
> 

## <a name="injecting-custom-data-into-your-azure-virtual-machine"></a>Injetando dados personalizados na máquina virtual do Azure
Esse recurso é suportado apenas em Olá [Interface de linha de comando do Azure](https://github.com/Azure/azure-xplat-cli). Aqui criamos uma `custom-data.txt` arquivo que contém os dados, e então insira que em toohello VM durante o provisionamento. Embora você possa usar qualquer uma das opções de saudação para Olá `azure vm create` comando seguinte Olá demonstra uma abordagem muito básica:

```
    azure vm create <vmname> <vmimage> <username> <password> \  
    --location "West US" --ssh 22 \  
    --custom-data ./custom-data.txt  
```


## <a name="using-custom-data-in-hello-virtual-machine"></a>Usando dados personalizados na máquina virtual de saudação
* Se sua VM do Azure é uma VM com base em Windows, o arquivo de dados personalizados de saudação é salvo muito`%SYSTEMDRIVE%\AzureData\CustomData.bin`. Embora fosse tootransfer codificada em base64 de saudação computador local toohello nova VM, ela será automaticamente decodificado e pode ser aberta ou usada imediatamente.
  
  > [!NOTE]
  > Se o arquivo hello existir, ele será substituído. segurança de saudação no diretório de saudação está definida muito**System: Full Control** e **Administrators: Full Control**.
  > 
  > 
* Se sua VM do Azure é uma VM com base em Linux, em seguida, o arquivo de dados personalizados Olá estará localizado em um dos seguintes Olá coloca dependendo de sua distribuição. dados saudação podem ser codificada em base64, portanto, dados de saudação toodecode talvez seja necessário primeiro:
  
  * `/var/lib/waagent/ovf-env.xml`
  * `/var/lib/waagent/CustomData`
  * `/var/lib/cloud/instance/user-data.txt` 

## <a name="cloud-init-on-azure"></a>Cloud-init no Azure
Se sua VM do Azure for de uma imagem Ubuntu ou CoreOS, você pode usar CustomData toosend toocloud-init uma configuração de nuvem. Ou, se o arquivo de dados personalizado for um script, cloud-init poderá simplesmente executá-lo.

### <a name="ubuntu-cloud-images"></a>Imagens de nuvem do Ubuntu
Na maioria das imagens do Linux do Azure, você edita "/ etc/waagent.conf" arquivo de disco e a troca de recursos temporário de saudação do tooconfigure. Consulte o [Guia de usuário agente do Linux do Azure](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para saber mais.

No entanto, nas imagens de nuvem do Ubuntu hello, você deve usar init nuvem tooconfigure Olá recursos disco (ou seja, Olá "efêmera") e troca de partição. Consulte Olá página a seguir no wiki do Ubuntu Olá para obter mais detalhes: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps-using-cloud-init"></a>Próximas etapas: usando cloud-init
Para obter mais informações, consulte Olá [documentação nuvem init para Ubuntu](https://help.ubuntu.com/community/CloudInit).

<!--Link references-->
[Referência da API REST de gerenciamento para adicionar serviço de função](http://msdn.microsoft.com/library/azure/jj157186.aspx)

[Interface de linha de comando do Azure](https://github.com/Azure/azure-xplat-cli)

