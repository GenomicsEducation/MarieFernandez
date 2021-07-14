  1. Conexión a servidor POMEO  
  Para más información sobre cómo conectarte a POMEO ingresa al link[Guía de configuración POMEO](Guias/POMEO.md)   
              2. Configurar Bioconda e instalar Gatk4  
    Utilice el comando `conda config --add channels bioconda` y luego `conda install -c bioconda gatk4`
      <img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/124661965-33b5ed00-de76-11eb-882c-e4e1a5356979.png" width="400" />    
            3. Instalar picard  
    Utilice el comando `wget https://github.com/broadinstitute/picard/releases/download/2.8.1/picard.jar`     <img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/124661979-36b0dd80-de76-11eb-9db1-81445a666164.png" width="400" />    
          4. Instalar vcftools   
    Utilice el comando `conda install -c bioconda vcftools`  
    <img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/124661983-37e20a80-de76-11eb-9000-eba024996df2.png" width="400" />  
    5. Crear directorio de trabajo “variant_call” y preparar archivos para el llamado de variantes
    Utilice el comaando `cd variant_call ls -l -h`   
    <img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/124661988-387aa100-de76-11eb-89e4-903a9351f109.png" width="400" />  
    Luego explore el documento con los comandos  
   `less ref_genome.fna  
    less ref_genome.fna.fai  
head -n 20 ref_genome.fna  
head -n 30 ref_genome.fna.fai   
tail -n 20 ref_genome.fna  
tail -n 20 ref_genome.fna.fai`  
  <img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/124661989-39133780-de76-11eb-84f2-9a07e3759c3d.png" width="400" />  
    <img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/124661993-39abce00-de76-11eb-9730-9e8d73d54f10.png" width="400" />  
    <img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/124661998-3a446480-de76-11eb-95ea-762bcaa01996.png" width="400" />  
    <img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/124662002-3adcfb00-de76-11eb-9ed8-ffcc9f0c2214.png" width="400" />  
    <img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/124662003-3b759180-de76-11eb-877c-859b045cd2e1.png" width="400" />  
    <img style="border:1px solid black;" src="    https://user-images.githubusercontent.com/57970928/124662009-3ca6be80-de76-11eb-8cbe-97aedb7b7b14.png" width="400" />  
    Investigue los cromosomas del salmón con los comandos   `grep 'NC_' ref_genome.fna
grep -c 'NC_' ref_genome.fna

grep 'NC_' ref_genome.fna.fai
grep -c 'NC_' ref_genome.fna.fai`  
    <img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/124662684-28af8c80-de77-11eb-8085-0200d3a4d46a.png" width="400" />    
     <img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/124662690-2a795000-de77-11eb-9cb1-593658bc1f6a.png" width="400" />  
      Investigue ahora los contigs no mapeados del salmón con los siguientes comandos:   
      `grep -c 'NW_' ref_genome.fna  
grep -c 'NW_' ref_genome.fna.fai`  
   <img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/124662694-2b11e680-de77-11eb-89e0-0ed02ecdfaeb.png" width="400" />  

   6. Llamado de variantes  
   Para realizar el llamado de variantes debe obtener primero un archivo que representará un “diccionario de referencias” del genoma de referencia  utilice el comando:   
   `java -jar picard.jar CreateSequenceDictionary R=ref_genome.fna O=ref_genome.dict`  
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/124663208-cc00a180-de77-11eb-86e1-3e6b56cba6fb.png" width="400" />  
Explore el archivo `ref_genome.dict` con los comandos `less` y `head`  
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/124663219-cefb9200-de77-11eb-9abd-431aaa9da1f7.png" width="400" />  
Para Añadir grupos de reads al archivo sort bam utilice el comando `java -jar picard.jar AddOrReplaceReadGroups I=SRR2006763.sort.bam O=SSRR2006763_sorted_RG.bam ID=sample LB=Paired-end PL=Illumina PU=Unknown SM=sample`  
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/124663229-d28f1900-de77-11eb-8238-7bef57e6f378.png" width="400" />   
Para el llamado de variantes se debe ejecutar el comando `gatk HaplotypeCaller -R ref_genome.fna -I SRR2006763_sorted_RG.bam -O raw_variants.vcf`  
 Verifique que se ha creado su archivo de salida `raw_variants.vcf`  
 Explore el archivo con los comandos `less`, `head` y `tail`.  
Use grep para contar el numero de lineas en el “vcf header”.  
`grep "^#" -c  raw_variants.vcf`  
 Use grep para contar el número de variantes detectadas `grep "^#" -c -v raw_variants.vcf`   

7. Análisis de variantes con vcftools  
  
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/124665897-4bdc3b00-de7b-11eb-9458-0300113c9ddc.png" width="400" />  
Utilice el comando `grep "^#CHROM" raw_variants.vcf | cut -f 10-`  

<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/124665904-4da5fe80-de7b-11eb-9c0b-3698087f224a.png" width="400" />  

Para imprimir el nombre de las columnas del llamado de variantes  
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/124665907-4ed72b80-de7b-11eb-9dde-77e691419811.png" width="400" />    
Para listar las 10 primeras variantes  
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/124665911-50085880-de7b-11eb-8d5f-0dd94cf3cd22.png" width="400" />  
Para entender la codificación de la columna INFO y FORMAT que contine la información del genotipo de la muestra para las primeras 10 variantes `grep "##INFO" raw_variants.vcf` 
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/124665914-51398580-de7b-11eb-9a3e-34a0252d6572.png" width="400" />  

<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/124665916-526ab280-de7b-11eb-9365-4fca74556ac0.png" width="400" />   
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/124665923-53034900-de7b-11eb-8831-fba53a5d09bc.png" width="400" />  
`grep "##FORMAT" raw_variants.vcf`  
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/124665925-539bdf80-de7b-11eb-905d-958c1536231c.png" width="400" />  
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/124665928-54cd0c80-de7b-11eb-95bd-e3050ecee128.png" width="400" />  
 Use el siguiente comando para extraer las variantes con calidad mayor a 100
`grep -v "#" raw_variants.vcf | awk '{if ($6 > 100 ) print }' > hq_variant.txt  

grep "NC_" -c -v hq_variant.txt  
grep "NW_" -c -v hq_variant.txt`  
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/124665932-5565a300-de7b-11eb-8fa5-368cb84f982a.png" width="400" />  

    
 8. Visualización de variantes con IGV  
Descargue el archivo raw_variants.vcf usando Win Scp generado en su directorio “variant_call”  
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/124665978-657d8280-de7b-11eb-9d55-7833a307e177.png" width="400" />  
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/124665984-67474600-de7b-11eb-877e-698dfe8a0c48.png" width="400" />  
Explore el archivo con el softare IGV  
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/124665986-68787300-de7b-11eb-9520-910838aab0bc.png" width="400" />  

