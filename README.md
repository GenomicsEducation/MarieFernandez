# Práctica elaboración de un proyecto de genómica aplicada.

## Autor
Marie Fernández  
Panameña  
Ingeniero en Biotecnología  

## Descripción
**Especie:** _Bos taurus_  
**Secuenciado:** Completamente  

| Tamaño total de la secuencia | 2,715,853,792 | 
| ------------- | ------------- |
| Número de scaffolds | 2,211 |  
| Número de contigs  | 12 |  
| Número total de cromosomas | 31 |  

**Molécula de interés:** Bos taurus myogenic factor 5 (MYF5), mRNA  
**Locus:** NM_174116  
**Referencia 1, Autores:** Zhao C, Raza SHA, Khan R, Sabek A, Khan S, Ullah I, Memon S,
            El-Aziz AHA, Shah MA, Shijun L, Wang L, Liu X, Zhang Y, Gui L and
            Zan L.  
**Título del artículo:** Genetic variants in MYF5 affected growth traits and beef quality
            traits in Chinese Qinchuan cattle  
**Revista:** Genomics 112 (4), 2804-2812 (2020)  
 **Conclusión:** Genetic variants in MYF5 affected growth traits and beef
            quality traits in Chinese Qinchuan cattle.  
            
**BioProject**  
**Título:** A combined flow cytometric semen analysis and miRNA profiling as a tool to discriminate between high and low fertility bulls.  
**Resumen:** Con esta investigación, se propuso un enfoque integrado entre el análisis avanzado de la calidad del semen y el perfil de miARN del semen criopreservado en toros con diferente fertilidad para identificar biomarcadores y construir un modelo que pueda ser potencialmente utilizado para la predicción de la fertilidad masculina en el campo. El estudio confirma que los rasgos de motilidad de los espermatozoides y los parámetros relacionados con la estructura de la cromatina están asociados con la fertilidad. Se identificaron quince miARN expresados diferencialmente, entre toros de alta y baja fertilidad. A partir del análisis de preferencia multidimensional, se reveló una correlación positiva entre parámetros de calidad in vitro específicos, miARN específicos y el estado de fertilidad de los toros. El enfoque integrado propuesto, podría proporcionar un modelo de predicción de fertilidad que podría ser beneficioso para los centros de IA en la selección de toros de alta fertilidad, facilitando la eliminación de sujetos subfértiles o eyaculados con baja capacidad fertilizante, reduciendo el impacto económico en la industria de la cría.  

| Accession	| PRJNA727990 |  
| --------- | --------- |  
| Data Type	| Raw sequence reads |  
| Scope | Multispecies |  
| Submission | Registration date: 7-May-2021 CNR |  
| Relevance | Agricultural |  

**Project Data:**  

| Resource Name | Number of Links |  
| ------ | ------- |  
| SRA Experiments | 40 |  
| BioSample | 40 |  

**SRA Data Details**  

| Parameter	| Value | 
| ------- | ------- |
| Data volume | Gbases	8 |  
| Data volume | Mbytes	3104 |  

**Referencias**  
[Assembly](https://www.ncbi.nlm.nih.gov/assembly/GCF_002263795.1)  
[Refseq](https://www.ncbi.nlm.nih.gov/nuccore/NM_174116.1) 
[BioProject](https://www.ncbi.nlm.nih.gov/bioproject/727990)
[SRA](https://www.ncbi.nlm.nih.gov/sra/SRX10826180[accn])

# Tarea 9  

**INSTALACIÓN Y CONFIGURACIÓN DE SOFTWARE PARA ACCESO REMOTO Y TRANSFERENCIA DE ARCHIVOS**
-PuTTY  
Para más información sobre cómo instalar PuTTY ingresa a: [PuTTY](Tutoriales/Putty.md)  

-WinSCP
Para más información sobre cómo instalar WinSCP ingresa a: [WinSCP](Tutoriales/WinSCP.md)

**ACCESO REMOTO A SERVIDOR POMEO**  
Para más información sobre cómo acceder al servidor remoto POMEO ingresa al link: [POMEO](Tutoriales/POMEO.md)

**INSTALACIÓN Y CONFIGURACIÓN CONDA, NANO Y SRA TOOLKIT**  
-Miniconda3  
https://docs.conda.io/projects/conda/en/latest/user-guide/install/download.html  
-nano  
https://www.nano-editor.org/download.php  
-SRA Toolkit  
https://hpc.nih.gov/apps/sratoolkit.html  

**PRÁCTICA DE SHELL Y LINUX**  
-Conectar al servidor POMEO usando  
`pc:~ usuario$ ssh -X nombre.apellido@200.54.220.141
usuario@200.54.220.141's password: completar con la password`  
-Información de la versión del software bash  
`bash --version`  
-Nombre del directorio en el que se encuentra  
`pwd`  
-Espacio total en el sistema, espacio usado, espacio disponible  
`df -hP`  
-Evalua el performance de la CPU, similar al monitor del sistema  
`top`  
-Crea un directorio de trabajo denominado tesis  
`mkdir tesis`  
-Cambia al directorio tesis  
`cd tesis`  
-Para volver al directorio anterior  
`cd`  
-Al usar el simbolo > que funciona como una tubería la información del espacio total del sistema se almacena en un documento de texto denominado espacio_libre_pomeo.txt  
`df -hP > espacio_libre_pomeo.txt`  
-Leer datos de un archivo e imprimir su contenido en la terminal  
`cat espacio_libre.txt`  
-Leer datos de un archivo sin imprimir en la terminal y recorrerlo  
`less espacio_libre.txt`  
-Contar líneas, palabras y caracteres de un fichero  
`wc espacio_libre.txt`  
-Listado de objetos en un directorio  
`ls`  
-Información con mas detalle de los objetos y de un tamaño que sea legible por humanos  
`ls -l -h`  
-Remover un fichero o directorio forzando la acción  
`rm tesis  
rm -r tesis`  
-Moverse por las líneas ejecutadas en la terminal  
`flecha arriba/abajo`  
-Imprimir todas las líneas de comando ejecutadas en la terminal  
`history`  
-Autocompletar nombres de ficheros  
`tecla tab`  
-Mover el cursor al comienzo de la línea actual   
`ctrl-a`  
-Mover el cursor al final de la línea actual  
`ctrl-e`  
-Borrar desde el cursor hasta el final de la línea   
`ctrl-k`  
-Borrar desde el cursor hasta el inicio de la línea  
`ctrl-u`  
-Borrar la palabra inmediatamente detras del cursor  
`ctrl-w`  
-Cerrar la sesión  
`exit`  

**PRÁCTICA DESCARGA DE SECUENCIAS NGS CON SRA TOOLKIT**  
-Instalación de SRA Toolkit  
`wget http://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/current/sratoolkit.current-centos_linux64.tar.gz
tar -xzf sratoolkit.current-centos_linux64.tar.gz`  
-Configuración de SRA Toolkit  
`bin/vdb-config --interactive`   
-Descargar y mostrar el contenido de las 5 primeras secuencias del archivo SRR6019464  
`bin/fastq-dump -X 5 -Z SRR6019464`  
-Descargar el contenido de las 5 primeras secuencias y almacenarlas en un archivo con formato fastq  
 `fastq-dump -X 5 SRR6019464`  
 -Descargar la biomuestra completa  
 `fastq-dump --gzip --split-3 SRR6019464`  
 -Dejar de ejectuar  
 `q`  
 -Explorar la muestra  
 `zcat SRR6019464.fastq.gz | echo $((``wc -l``/4))`  
 
 # Tarea 10 y 11
 
 **INSTALACIÓN Y CONFIGURACIÓN SOFTWARE**  

**Control de calidad**  

🔴FastQC  

🔴Trimmomatic  
Para más información sobre como instalar FastQC y Trimmomatic ingresa a: [FastQC_Trimmomatic](Tutoriales/Alineamiento/FastQC_Trimmomatic.md)

**Alineamiento**  

🔴BWA  
1. Para configurar bioconda ejecute el siguiente comando `conda config --add channels bioconda`
2. Instale el software BWA con el comando `conda install -c bioconda bwa`  
  

🔴Samtools  
1. Para instalar samtools ejecute cada uno de estos comandos en orden  
`conda install -c bioconda samtools`    

`conda config --add channels bioconda`     

`conda config --add channels conda-forge`     

`conda install samtools==1.11`  

2. Para verificar los directorios de instalación ejecute 
`whereis sratoolkit`   
`whereis samtools`    
`whereis bwa`   
 Para más información sobre cómo instalar Samtools ingrese a: [Samtools](Tutoriales/Alineamiento/Samtools.md)


**ETAPAS ANÁLISIS DE CONTROL DE CALIDAD, FILTRADO Y PODA**  

🔴Descargar secuencias NGS usando SRA toolkit
1. Primero crear un script con la siguiente información:   
`#!/bin/bash`  
`#SBATCH -J prefetch_usuario`  
`/home2/usuario/sratoolkit.2.11.0-centos_linux64/bin/prefetch --max-size 100G SRR2006763 -O /home2/usuario/SRA_samples/`  
`/home2/usuario/sratoolkit.2.11.0-centos_linux64/bin/vdb-validate /home2/usuario/SRA_samples/SRR2006763/SRR2006763.sra`   
 y correr el script

2. Acceder a la carpeta SRR2006763 y crear el siguiente script y correrlo  
`#!/bin/bash 
#SBATCH - J fdump_usuario
/home2/usuario/sratoolkit.2.11.0-centos_linux64/bin/fasterq-dump /home2/usuario/SRA_samples/SRR2006763/*.sra -O /home2/usuario/SRA_samples/SRR2006763/`  
  
3. Para comprobar la integridad de los archivos ejecute el comando `md5sum SRR2006763_1.fastq SRR2006763_2.fastq > md5_samples` luego el comando para verificar la salida generada `cat md5_samples`   

4. Finalmente para comprobar la integridad de las muestras el comando `md5sum -c md5_samples`
  

🔴Realizar análisis de control de calidad  
1. Correr el siguiente script  
`#!/bin/bash`  
`#SBATCH - J fastqc_usuario`  
`fastqc /home2/usuario/SRA_samples/SRR2006763/*.fastq`  
  2. Transferir archivos mediante protocolo FTP desde Servidor a Cliente entrando a la dirección http://200.54.220.141:8787/
  3. Iniciar sesión con los datos que usa para ingresar a POMEO
  4. Visualizar archivos generados al concluir la descarga
  

🔴Realizar filtrado y poda de secuencias    


🔴Transferir archivos de control de calidad mediante protocolo FTP desde Servidor a Cliente  
 Para más información sobre esta etapa ingresa a la guía paso a paso: [Análisis](Tutoriales/Alineamiento/Analisis.md)  
 
**ETAPAS DE ALINEAMIENTO**  


🔴Obtener secuencias Fastq  
1. Crea una carpeta llamada "alineamiento" con el comando `mkdir alineamiento`
2. Ingresa a la carpeta y transfiere los archivos de clase anterior colocando los siguientes comandos en la terminal con los comandos `cd alineamiento` y luego    
 `mv /home2/usuario/SRA_samples/SRR2006763/SRR2006763_1.fastq /home2/usuario/alineamiento/`      
 `mv /home2/usuario/SRA_samples/SRR2006763/SRR2006763_2.fastq /home2/usuario/alineamiento/`  

🔴Descarga genoma mitocondrial 
1. Descarga el genoma mitocondrial en formato fasta desde el siguiente link https://www.ncbi.nlm.nih.gov/genome/?term=salmo+salar


🔴Subir genoma a POMEO con software de acceso remoto  
1. Iniciar sesión en WinSCP con los datos de POMEO
2.Ingresar a la carpeta "alineamiento" y arrastrar el archivo descargado del genoma mitocondrial hasta la carpeta

🔴Indexación genoma mitocondrial 
1. Ejecutar el comando `bwa index mt.fasta`


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

2. Ejecuta el script con `bash aln_mt.sh`

3. Observa el archivo con `less SRR2006763.sam` y puedes salir con `q`

4. Puedes realizar un análisis estadístico estándar con el siguiente comando `samtools flagstat SRR2006763.bam > muestra_stat.txt`


🔴Conversión SAM a BAM
1. La conversión de SAM a BAM se puede hacer con el comando `samtools view -Sb -q 30 SRR2006763.sam > SRR2006763.bam`


🔴Orden de lecturas alineadas por posición 
1. Para alinear las secuencias se puede usar el comando `bwa mem mt.fasta SRR2006763_1.fastq SRR2006763_2.fastq > SRR2006763.sam`


🔴Indexación con Samtools 
1. Se puede indexar el archivo bam con el comando `samtools index SRR2006763.sort.bam` 



🔴Exploración de archivos de salida en cada etapa  
1. Utiliza el comando `ls -l -h` para obtener un listado de los archivos que tienes en tu carpeta.

Para una guía ilustrada paso a paso sobre esta etapa ingresa a: [Alineamiento](Tutoriales/Alineamiento/Alineamiento_secuencias.md)

