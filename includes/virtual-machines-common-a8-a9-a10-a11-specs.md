

## <a name="deployment-considerations"></a>Considerações de implantação
* **Assinatura do Azure** – toodeploy mais do que algumas instâncias de computação intensiva, considere a possibilidade de uma assinatura paga pelo uso ou outras opções de compra. Se estiver usando uma [conta gratuita do Azure](https://azure.microsoft.com/free/), você poderá usar apenas um número limitado de núcleos de computação do Azure.

* **Preços e disponibilidade** -tamanhos de VM esses são oferecidos apenas na camada de preços padrão hello. Verifique [Produtos disponíveis por região] (https://azure.microsoft.com/regions/services/) para disponibilidade em regiões do Azure. 
* **Cota de núcleos** – talvez seja necessário tooincrease cota de núcleos de saudação em sua assinatura do Azure do valor padrão de saudação. Sua assinatura também pode limitar o número de saudação de núcleos que podem ser implantados em determinadas famílias de tamanho VM, incluindo Olá H-series. aumentar a cota toorequest, [abrir uma solicitação de suporte do cliente online](../articles/azure-supportability/how-to-create-azure-support-request.md) sem custo adicional. (Os limites padrão podem variar dependendo de sua categoria de assinatura.)
  
  > [!NOTE]
  > Entre em contato com o Suporte do Azure se precisar de capacidade em larga escala. Cotas do Azure são limites de crédito, não garantias de capacidade. Independentemente de sua cota, você é cobrado apenas pelo núcleos utilizados.
  > 
  > 
* **Rede virtual** – um Azure [rede virtual](https://azure.microsoft.com/documentation/services/virtual-network/) é necessária não toouse instâncias de computação intensiva hello. No entanto, para muitas implantações você precisa de pelo menos uma rede de virtual do Azure baseado em nuvem, ou uma conexão site a site, se você precisar tooaccess recursos locais. Quando necessário, crie uma nova rede virtual toodeploy instâncias de saudação. Não há suporte para a adição de rede virtual de tooa de VMs de computação intensiva em um grupo de afinidade.
* **Redimensionando** – devido a seu hardware especializado, você só pode redimensionar instâncias de computação intensiva dentro de saudação mesmo tamanho família (série H ou computação intensa série). Por exemplo, você somente pode redimensionar uma VM série H de tooanother de tamanho uma série de H. Além disso, o redimensionamento de um tamanho de computação intensa do tamanho de computação intensa tooa não é suportado.  
