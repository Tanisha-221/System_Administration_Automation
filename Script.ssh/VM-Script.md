#Set Variables 
$resourceGroup = "T-ResourceGroup"              
$location = "UK South"  
$VNetName = "MyVnet"
$SubnetName = "MySubnet"
$NSGName = "MyNSG"
$VMSize = "Standard_DS1_v2"
$VMNames = @("Vm1", "Vm2", "Vm3")

#Creating 3 VM 
foreach ($vmName in $VMNames) {
    New-AzVm `
        -ResourceGroupName $resourceGroup `
        -Name $vmName `
        -Location $location `
        -Image 'Ubuntu2204' `
        -VirtualNetworkName $VNetName `
        -SubnetName $SubnetName `
        -SecurityGroupName $NSGName `
        -PublicIpAddressName "$vmName-pip" `
        -OpenPorts 22,3389
}
    Start-Sleep -Seconds 30
