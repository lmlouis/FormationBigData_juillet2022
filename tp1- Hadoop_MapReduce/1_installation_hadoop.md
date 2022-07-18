
installation de hadoop avec docker 
----------------------
verifier si docker est bien installé et activé 
```
$ sudo systemctl status docker
```

Télécharger hadoop spark via docker hub
------------
syntaxe : `docker pull [userDockerHub/NomFichier]:[#tag]`
```
$ sudo docker pull liliasfaxi/spark-hadoop:hv-2.7.2
```

voir si les images hadoop ont été téléchargé 
---------------------
syntaxe : `docker images`

```
$ sudo docker images 
```

créer un réseau dqui porte le nom hadoop
---------------------

syntaxe : `docker network create --drive=bridge [Nom_Reseau]`

```
$ sudo docker network create --drive=bridge hadoop
```

créer le container à partir de l'image hadoop coorespondant au name node (master)
---------------

nom container  =  hadoop-master 
image source  =  liliasfaxi/spark-hadoop:hv-2.7.2

$ sudo docker run -itd --net=hadoop -p 50070:50070 -p 8088:8088 -p 7077:7077 -p 16010:16010 --name hadoop-master  --hostname hadoop-master liliasfaxi/spark-hadoop:hv-2.7.2 //container hadoop-master avec port 

commznde docker pour verifier un container qui tourner 
------------------------------------------

$ sudo docker ps
$ sudo docker ps -a //tous les container y compris ceux qui sont stopé 

$ sudo docker rm [ID_container] // supprime le container 

créer le container à partir de l'image hadoop coorespondant deux autres node (slave)
---------------

$  sudo docker run -itd --net=hadoop -p 8040:8042 --name hadoop-slave1  --hostname hadoop-slave1 liliasfaxi/spark-hadoop:hv-2.7.2 //le slave1 avec port 8040

$  sudo docker run -itd --net=hadoop -p 8041:8042 --name hadoop-slave2  --hostname hadoop-slave2 liliasfaxi/spark-hadoop:hv-2.7.2 //le slave2 avec port 8041


ensuite faire en sorte que toutes les requetes soient exécutées sur le container hadoop-master 
--------------------------------------------------------
$ sudo docker exec -it hadoop-master bash