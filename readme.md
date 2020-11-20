## Creacion de la maquina virtual en Azure Cli

### Conectarse desde Azure Cli A Azure

```
az login
```

![login](imagenes/c1.PNG)
![login](imagenes/c2.PNG)


### Creando un grupo de recursos

```
az group create -l EastUS -n myRGCLI 
```
![az group create](imagenes/c3.PNG)

![az group create](imagenes/c4.PNG)

### Creando una máquina virtual Linux

```
az vm create ^
 --name myVMCLI ^
 --resource-group myRGCLI ^
 --image UbuntuLTS ^
 --location EastUS ^
 --admin-username azureuser ^
 --admin-password Pa$$w0rd1234 ^
 --no-wait
```

![az vm create](imagenes/c5.PNG)

![az vm create](imagenes/c6.PNG)

Conectarse a la máquina Virtual de Linux

```
ssh azureuser@104.211.52.252 //IP Publica
Nota: Dar que si en la creación del certificado SSH
```

![ssh](imagenes/c7.PNG) 

![ssh](imagenes/c8.PNG) 

1 - Actualizar en Linux

```
sudo apt-get update
```

2 - Hacer el upgrade

```
sudo apt upgrade
```

3 - Instalar un servidor web

```
sudo apt install -y apache2 apache2-utils
```

4 - Vemos el estatus de Apache

```
systemctl status apache2
```

![systemctl status apache2](imagenes/c11.PNG) 

5 - Ponemos un mensaje en nuestra página de Apache

```
cd /var/www/html
```

6 - Poner una nota en la página inde.html

```
sudo vi index.html <ENTER>
<ESC> : 198 <ENTER> // irme a la linea 198 que es donde esta el mensaje de index.html
<i> PONER EL MENSAJE <ESC>
: x <ENTER>

```



7 - Salir del SSH

```
exit <ENTER>
```

![systemctl status apache2](imagenes/c12.PNG) 

**Nota:**

El puerto 80 deberá ser abierto desde NSG.

Destination PortRanges: 80

Name: Port_80


![Port_80](imagenes/c13.PNG) 

![Port_80](imagenes/c15.PNG) 



Probariamos que llegamos a la maquina virtual: con la IP desde cualquier navegador.

![Port_80](imagenes/c14.PNG) 

## Parar y "deallocate" la máquina virtual

```
az vm stop --resource-group myRGCLI --name myVMCLI --no-wait
```

```
az vm deallocate -g myRGCLI -n myVMCLI --no-wait
```

## Iniciar la máquina virtual

```
az vm start -g myRGCLI -n myVMCLI --no-wait
```

## Borrar la máquina virtual

```
az vm delete -g myRGCLI -n myVMCLI --yes --no-wait
```

### Mostrar informacion de la máquina virtual

```
az vm show -g myRGCLI -n myVMCLI -d
```

Borrar el grupo de recursos

```
az group delete -n myRGCLI  --yes --no-wait
```

![borrar](imagenes/c16.PNG) 

![borrar](imagenes/c17.PNG) 

## Desconectamos de Azure

```
az logout
```

Mas información:

[Manage Linux or Windows virtual machines.](https://docs.microsoft.com/en-us/cli/azure/vm?view=azure-cli-latest)

