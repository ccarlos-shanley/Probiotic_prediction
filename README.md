# Probiotic_prediction

The data was obtained from: ftp://ftp.microbio.me/AmericanGut/ag-April-26-2017/07-taxa.zip .

The dataset was manually curated to remove redundant and uninformative variables.

Need for probiotic was defined based on the ratio between Firmicutes and Bacteroidetes.

Discretization:

if FBratio>= 1.0 and Fbratio <= 5.6:

  Probiotic_need = Healthy
  
 else:
 
  Probiotic_need = Yes
