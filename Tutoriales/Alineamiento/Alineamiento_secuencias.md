**ETAPAS DE ALINEAMIENTO**  
<img style="border:1px solid black;" src="" width="400" />

🔴Obtener secuencias Fastq  
1. Crea una carpeta llamada "alineamiento" con el comando `mkdir alineamiento`
2. Ingresa a la carpeta y transfiere los archivos de clase anterior colocando los siguientes comandos en la terminal con los comandos `cd alineamiento` y luego    
 `mv /home2/usuario/SRA_samples/SRR2006763/SRR2006763_1.fastq /home2/usuario/alineamiento/`      
 `mv /home2/usuario/SRA_samples/SRR2006763/SRR2006763_2.fastq /home2/usuario/alineamiento/`  

🔴Descarga genoma mitocondrial 
1. Descarga el genoma mitocondrial en formato fasta desde el siguiente link https://www.ncbi.nlm.nih.gov/genome/?term=salmo+salar
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/123121342-17946380-d413-11eb-9532-c8a69f8f331f.png" width="400" />
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/123121350-195e2700-d413-11eb-8adc-40b3af4f7ae9.png" width="400" />
  

🔴Subir genoma a POMEO con software de acceso remoto  
1. Iniciar sesión en WinSCP con los datos de POMEO
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/123144018-37368680-d429-11eb-8e1f-07e940c01595.png" width="400" />
2.Ingresar a la carpeta "alineamiento" y arrastrar el archivo descargado del genoma mitocondrial hasta la carpeta
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/123144741-0145d200-d42a-11eb-979d-ea808067d00a.png" width="400" />

🔴Indexación genoma mitocondrial 
1. Ejecutar el comando `bwa index mt.fasta`
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/123154279-a06fc700-d434-11eb-82f1-8f7db1e34db9.png" width="400" />


🔴Alineamiento de secuencias contra genoma mitocondrial  
1. Ejecute el comando `nano aln_mt.sh` para crear un script que contenga las siguientes instrucciones:  
`#!/bin/bash -l`  
`# para alinear tus dos secuencias fastq al genoma mitocondrial  
bwa mem mt.fasta SRR2006763_1.fastq SRR2006763_2.fastq > SRR2006763.sam`   
`# Transformar tu archivo sam a bam  
samtools view -Sb -q 30 SRR2006763.sam > SRR2006763.bam`  
`# ordenar tu archivo binario bam  
samtools sort SRR2006763.bam -o SRR2006763.sort.bam`   
`# indexar tu archivo bam  
samtools index SRR2006763.sort.bam`  
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/123155305-f133ef80-d435-11eb-8481-fa31eac232da.png" width="400" />

2. Ejecuta el script con `bash aln_mt.sh`
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/123155323-f6913a00-d435-11eb-9871-c41486803169.png" width="400" />

3. Observa el archivo con `less SRR2006763.sam` y puedes salir con `q`
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/123155339-fd1fb180-d435-11eb-8ae5-016e2b929f7c.png" width="400" />

4. Puedes realizar un análisis estadístico estándar con el siguiente comando `samtools flagstat SRR2006763.bam > muestra_stat.txt`
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/123157584-b54e5980-d438-11eb-8ee4-f9a81f1430a1.png" width="400" />


🔴Conversión SAM a BAM
1. La conversión de SAM a BAM se puede hacer con el comando `samtools view -Sb -q 30 SRR2006763.sam > SRR2006763.bam`
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/123157631-c8612980-d438-11eb-96c3-45c121ef8f9a.png" width="400" />


🔴Orden de lecturas alineadas por posición 
1. Para alinear las secuencias se puede usar el comando `bwa mem mt.fasta SRR2006763_1.fastq SRR2006763_2.fastq > SRR2006763.sam`
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/123157700-e038ad80-d438-11eb-92d9-7458a32ab697.png" width="400" />


🔴Indexación con Samtools 
1. Se puede indexar el archivo bam con el comando `samtools index SRR2006763.sort.bam` 



🔴Exploración de archivos de salida en cada etapa  
1. Utiliza el comando `ls -l -h` para obtener un listado de los archivos que tienes en tu carpeta.
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/123158119-605f1300-d439-11eb-829f-9be1f04f35a0.png" width="400" />
