## <a name="create-a-resource-group"></a>Criar um grupo de recursos

Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando. Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados. 

Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a>Criar uma máquina virtual

Criar uma VM com hello [criar vm az](/cli/azure/vm#create) comando. 

Olá, exemplo a seguir cria uma VM denominada *myVM* e cria as chaves de SSH se eles ainda não existir em um local de chave padrão. toouse um conjunto específico de chaves, use Olá `--ssh-key-value` opção.  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

Quando Olá VM tiver sido criado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir. Anote Olá `publicIpAddress`. Esse endereço é usado tooaccess Olá VM.

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/<subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```



## <a name="open-port-80-for-web-traffic"></a>Abra a porta 80 para tráfego da Web 

Por padrão, somente as conexões de SSH têm permissão em VMs Linux implantadas no Azure. Como essa VM toobe um servidor web, você precisa tooopen porta 80 de saudação à internet. Saudação de uso [az vm abrir portas](/cli/azure/vm#open-port) saudação do comando tooopen desejado de porta.  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a>SSH em sua VM


Se você não souber Olá endereço IP público da VM, execute Olá [lista de ip público de rede az](/cli/azure/network/public-ip#list) comando:


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

A seguir Olá Use o comando toocreate uma sessão SSH com a máquina virtual de saudação. Substituir saudação correto endereço IP público de sua máquina virtual. Neste exemplo, o endereço IP de saudação é *40.68.254.142*.

```bash
ssh azureuser@40.68.254.142
```

