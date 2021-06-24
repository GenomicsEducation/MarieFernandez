**ETAPAS ANÁLISIS DE CONTROL DE CALIDAD, FILTRADO Y PODA**  

🔴Descargar secuencias NGS usando SRA toolkit
1. Primero crear un script con la siguiente información:   
`#!/bin/bash`  
`#SBATCH -J prefetch_usuario`  
`/home2/usuario/sratoolkit.2.11.0-centos_linux64/bin/prefetch --max-size 100G SRR2006763 -O /home2/usuario/SRA_samples/`  
`/home2/usuario/sratoolkit.2.11.0-centos_linux64/bin/vdb-validate /home2/usuario/SRA_samples/SRR2006763/SRR2006763.sra`   
 y correr el script
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/123112729-f2e8bd80-d40b-11eb-9d2b-ec605d43ee6d.png" width="400" />
2. Acceder a la carpeta SRR2006763 y crear el siguiente script y correrlo  
`#!/bin/bash 
#SBATCH - J fdump_usuario
/home2/usuario/sratoolkit.2.11.0-centos_linux64/bin/fasterq-dump /home2/usuario/SRA_samples/SRR2006763/*.sra -O /home2/usuario/SRA_samples/SRR2006763/`  
  
3. Para comprobar la integridad de los archivos ejecute el comando `md5sum SRR2006763_1.fastq SRR2006763_2.fastq > md5_samples` luego el comando para verificar la salida generada `cat md5_samples`   
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/123113583-a9e53900-d40c-11eb-98ad-6d839f3df4b7.png" width="400" />  
4. Finalmente para comprobar la integridad de las muestras el comando `md5sum -c md5_samples`
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/123113587-aa7dcf80-d40c-11eb-8a1b-e2c1569fec40.png" width="400" />  
  

🔴Realizar análisis de control de calidad  
1. Correr el siguiente script  
`#!/bin/bash`  
`#SBATCH - J fastqc_usuario`  
`fastqc /home2/usuario/SRA_samples/SRR2006763/*.fastq`  
  2. Transferir archivos mediante protocolo FTP desde Servidor a Cliente entrando a la dirección http://200.54.220.141:8787/
  3. Iniciar sesión con los datos que usa para ingresar a POMEO
  4. Visualizar archivos generados al concluir la descarga
  <img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/123115704-4a882880-d40e-11eb-8f66-db4710e328bb.png" width="400" />  
  

🔴Realizar filtrado y poda de secuencias    


🔴Transferir archivos de control de calidad mediante protocolo FTP desde Servidor a Cliente  