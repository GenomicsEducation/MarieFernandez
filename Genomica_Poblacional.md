 1. Conexión a servidor POMEO  
  Para más información sobre cómo conectarte a POMEO ingresa al link[Guía de configuración POMEO](Guias/POMEO.md)
  
  
5.Analisis de estructura poblacional  
6.Analisis de admixture 

2.Configurar bioconda e instalar programas para analisis    
Para configurar bioconda utilice el comando `conda config --add channels bioconda`. Para la instalación de plink utilice el comando `conda install -c bioconda plink`. Para la instalación de admixture utilice el comando `conda install -c bioconda admixture`  
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125715851-98121382-e031-47d6-9387-5f337abdae52.png" width="400" /> 
3.Crear directorio de trabajo “population” y preparar archivos para el analisis poblacional con plink y 
admixture  
Ingrese al directorio population y liste los archivos con los comandos ```cd population
ls -l -h```.  
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712174-eb1e4272-95e5-460c-8382-812a569b912d.png" width="400" /> 

4.Analisis de diversidad 
Para estimar el número de sitios heterocigotos para cada individuo y la heterocigosidad observada y esperada para cada marcador utilice los comandos `vcftools --vcf EU_OC_US.vcf --het --out EU_OC_US

vcftools --vcf EU_OC_US.vcf --hardy --out EU_OC_US`
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712177-e86b4a4b-18f8-422b-8a29-8670480a8e3d.png" width="400" /> 

<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712182-9f43fa41-5804-45cd-bed0-91beb5f0a451.png" width="400" /> 
Calcular la diversidad en una ventana no superpuesta de 200 kb para cada individuo de las tres poblaciones utilice el comando para la población de Europa `vcftools --vcf EU_OC_US.vcf --window-pi 200000 --indv 2_WG0341511-DNA_A02_5408 --indv 3_WG0341511-DNA_A03_5416 --indv 5_WG0341511-DNA_A05_5450 --out EU` 
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712195-203a448f-1f49-4b8b-b510-f4c827a7e711.png" width="400" /> 
Para la población de Oceanía `vcftools --vcf EU_OC_US.vcf --window-pi 200000 --indv FR07958834 --indv FR07958842 --indv FR07958850 --out OC`
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712197-42c91ad1-227b-43aa-b52a-6d541f62be12.png" width="400" /> 

Para la población de Norteamérica `vcftools --vcf EU_OC_US.vcf --window-pi 200000 --indv GNB12-1 --indv GNB12-10 --indv GNB12-11 --out US`
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712199-30cb6b74-7e83-4681-8069-143f9ddf2676.png" width="400" /> 

<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712203-5d6efbdd-c484-4909-bc6a-be065b781a53.png" width="400" /> 
Para calcular el desequilibrio de ligamiento (LD) para Europa utilice el comando `vcftools --vcf EU_OC_US.vcf --geno-r2 --chr 1 --ld-window-bp 100000 --min-r2 0.001 --indv 2_WG0341511-DNA_A02_5408 --indv 3_WG0341511-DNA_A03_5416 --indv 5_WG0341511-DNA_A05_5450 --out EU`
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712205-0861322a-c803-4319-8787-927b327fa86d.png" width="400" /> 
Para Oceanía `vcftools --vcf EU_OC_US.vcf --geno-r2 --chr 1 --ld-window-bp 100000 --min-r2 0.001 --indv FR07958834 --indv FR07958842 --indv FR07958850 --out OC`
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712213-9c5092be-8f8f-418c-9c76-7a9753775782.png" width="400" /> 
Para Norteamérica `vcftools --vcf EU_OC_US.vcf --geno-r2 --chr 1 --ld-window-bp 100000 --min-r2 0.001 --indv GNB12-1 --indv GNB12-10 --indv GNB12-11 --out US`
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712215-a72e998e-36b0-4f9b-9c35-99ec8d2284f6.png" width="400" /> 
Luego en R Studio, inserte el siguiente código ```EU <- read_delim("EU.geno.ld", delim = "\t")
OC <- read_delim("OC.geno.ld", delim = "\t")
US <- read_delim("US.geno.ld", delim = "\t")

EU$dist <- ceiling((EU$POS2 - EU$POS1)/1000)*1000
OC$dist <- ceiling((OC$POS2 - OC$POS1)/1000)*1000
US$dist <- ceiling((US$POS2 - US$POS1)/1000)*1000

EU2 <- group_by(EU,dist) %>%
  summarise(meanR2 = mean(`R^2`))

OC2 <- group_by(OC,dist) %>%
  summarise(meanR2 = mean(`R^2`))
  
US2 <- group_by(US,dist) %>%
  summarise(meanR2 = mean(`R^2`))  

dd <- bind_rows(EU2,OC2,US2)

dd$pop <- rep(c("EU","OC","US"),c(nrow(EU2),nrow(OC2),nrow(US2))) 

write_csv(dd,"EU_OC_US.windowed.ld.csv")```
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712220-7eadd566-eeae-42ba-b630-b9c51f6cfdc8.png" width="400" /> 
Para generar gráficos de Heterogocidad individual use el código ```het <- read_delim("EU_OC_US.het",delim = "\t")
het  
het$Heterozygosity <- 1-(het$`O(HOM)`/het$N_SITES) 
het$Population <- c(rep("EU",3),rep("OC",3),rep("US",3))
A <- ggplot(het,aes(x = Population, y = Heterozygosity, col = Population)) +
  geom_point()+
  theme_bw()+
  theme(legend.position = "none")+
  xlab("")
A```
Para graficar la Diversidad de nucleótidos inserte el siguiente código```pi_EU <- read_delim("EU.windowed.pi",delim = "\t") 
pi_EU``` para la población de Europa.  
Para la población de Oceanía `pi_OC <- read_delim("OC.windowed.pi",delim = "\t")
pi_OC`.
Para la población de Norteamérica `pi_US <- read_delim("US.windowed.pi",delim = "\t")
pi_US` 
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712224-3c91fa1c-37f4-4101-b8fb-3eb191718763.png" width="400" /> 

Para graficar el Desequilibrio de ligamento inserte el código `ld <- read_csv("EU_OC_US.windowed.ld.csv")
ld` y ```C <- ggplot(ld,aes(x = dist/1000, y = meanR2, col = pop)) +
      geom_point()+
      geom_line()+
      theme_bw()+
      xlab("Distance (kb)")+
      ylab(expression(R^2))+
      scale_colour_discrete(name = "Population")
C```
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712228-4e58fcf7-3876-4555-bace-90aec5794d72.png" width="400" /> 
Para obtener un gráfico de paneles múltiples inserte el código ```library(cowplot)
top_row <- plot_grid(A,B,labels = "AUTO")
plot_grid(top_row,C,nrow = 2,labels = c("","C"))```

<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712230-ab855fb4-952f-42be-a383-03ad96ea988e.png" width="400" /> 
5. Análisis de estructura poblacional

Para Generar el archivo de entrada en formato plink use el código `plink --vcf EU_OC_US.vcf --recode --out EU_OC_US --double-id --allow-extra-chr --chr-set 29`
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712233-ffd75528-8601-4213-8277-232ffcb9a2de.png" width="400" /> 
Para Generar el archivo de entrada en formato plink binario `plink --file EU_OC_US --make-bed --out EU_OC_US --allow-extra-chr --chr-set 29`
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712238-6a88b2b9-b445-47b1-af24-083b1ab3b177.png" width="400" /> 
Filtrar basado en equilibrio de Hardy-Weinberg y frecuencia del alelo menor `plink --bfile EU_OC_US --hwe 0.01 --maf 0.05 --make-bed --out EU_OC_US.Filtered --allow-extra-chr --chr-set 29`
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712243-c41a4dcc-11a1-4faf-aa81-9956bfe9eabc.png" width="400" /> 
Filtrar y excluir marcadores por desequilibrio de ligamiento
`plink --bfile EU_OC_US.Filtered --indep-pairwise 50 10 0.05 --make-bed --out EU_OC_US.Filtered --allow-extra-chr --chr-set 29

plink --bfile EU_OC_US.Filtered --extract EU_OC_US.Filtered.prune.in --make-bed --out EU_OC_US.FilteredPruned --allow-extra-chr --chr-set 29`
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712248-a8015850-adb7-4c4b-8604-bf4dc66273d4.png" width="400" /> 
Filtrar para remover individuos relacionados `plink --bfile EU_OC_US.FilteredPruned --rel-cutoff 0.4 --out EU_OC_US.FilteredPruned --allow-extra-chr --chr-set 29

plink --bfile EU_OC_US.FilteredPruned --keep EU_OC_US.FilteredPruned.rel.id --make-bed --out EU_OC_US.FilteredPrunedUnrel --allow-extra-chr --chr-set 29`
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712251-9e2a6b87-b1bc-4fd2-bf72-11506cdb8ebd.png" width="400" /> 

<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712254-5e91e4dd-0740-4f6b-9145-6bc95fae3e54.png" width="400" /> 

<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712256-8f6304f0-bbdd-4e67-a2be-46dd54f41c36.png" width="400" /> 
PCA (Principal Component Analysis)
`plink --bfile EU_OC_US.FilteredPrunedUnrel --pca 4 --out EU_OC_US.FilteredPrunedUnrel --allow-extra-chr --chr-set 29`
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712261-24b4e418-645e-47bb-8cd7-c62946d12944.png" width="400" /> 
Graficos de PCA con R
`pca1 <- read_delim("EU_OC_US.FilteredPrunedUnrel.eigenvec", delim = " ",col_names = F)
    head(pca1)`
    
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712268-6caf34bc-74f4-4191-b3f1-e610ef135dc2.png" width="400" /> 
` colnames(pca1) <- c("Population","Individual",paste0("PC",c(1:4)))
    head(pca1)`
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712273-dae5043a-667e-4053-b6bd-80fdb3936940.png" width="400" /> 
y `mycols <- c("#a6cee3",
              "#1f78b4",
              "#b2df8a",
              "#33a02c",
              "#fb9a99",
              "#e31a1c",
              "#fdbf6f",
              "#ff7f00",
              "#cab2d6")

    D <- ggplot(pca1,aes(x = PC1,y = PC2,col = Population))+
      geom_point()+
      theme_bw()+
      scale_colour_manual(values = mycols)
   D`
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712278-0ced0fda-9fdb-453b-8ffb-d66f52358378.png" width="400" /> 
6. Análisis de admixture
 Seleccion al azar del 1% de los marcadores `plink --bfile EU_OC_US.FilteredPrunedUnrel --thin 0.01 --make-bed --out EU_OC_US.Thinned --allow-extra-chr --chr-set 29`
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712290-f34a0112-eaaa-4cdc-85c7-188c6eaa8eb2.png" width="400" /> 
 Para el Analisis de ancestria de 2 a 6 poblaciones

`for K in `seq 2 6`;
do
admixture EU_OC_US.Thinned.bed $K;
done`

<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712300-71544682-a983-4e44-956d-049dbc09e635.png" width="400" /> 
Graficos de ADMIXTURE para 2, 4 y 6 poblaciones
`library(readr)
source("Admixture_plot.R")

    pops <- read_delim("EU_OC_US.Thinned.fam", delim = " ",col_names = F)

    K2 <- read_delim("EU_OC_US.Thinned.2.Q", delim = " ",col_names = F)
    E <- admixtureplot(str_out = K2,k = 2, pops = pops, xaxis = F)
 E`
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712301-81be46b5-77ff-4d2e-8011-ec7a313ffcdd.png" width="400" /> 
`K4 <- read_delim("EU_OC_US.Thinned.4.Q", delim = " ", col_names = F)
    G <- admixtureplot(str_out = K4,k = 4, pops = pops, xaxis = F)
    G`
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712303-f35947b2-8c7f-4660-9fd6-2426ddcc673f.png" width="400" /> 
` K6 <- read_delim("EU_OC_US.Thinned.6.Q", delim = " ", col_names = F)
    H <- admixtureplot(str_out = K6,k = 6, pops = pops, xaxis = T)
    H`
<img style="border:1px solid black;" src="https://user-images.githubusercontent.com/57970928/125712306-434de486-930e-4041-8fd7-a89b0d64f8e3.png" width="400" /> 

