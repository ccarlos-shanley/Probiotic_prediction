# Probiotic_prediction

# Data was obtained from: ftp://ftp.microbio.me/AmericanGut/ag-April-26-2017/07-taxa.zip

# Dataset was manually curated to remove redundant variables, no fecal samplas and low variance data

# Need for probiotic was defined based on the ratio between Firmicutes and Bacteroidetes.

if FBratio>= 1.0 and Fbratio <= 5.6:
  Probiotic_need = Healthy
 else:
  Probiotic_need = Yes
  
 
