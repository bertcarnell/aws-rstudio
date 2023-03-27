FROM aws-rstudio-4-r

# https://stackoverflow.com/questions/75775502/r-install-rgdal-package-error-gdalallregister-not-found-in-libgdal

# rgdal fails to configure
# RUN PKG_CONFIG_PATH=/usr/local/lib64/pkgconfig Rscript -e 'install.packages("https://cran.microsoft.com/src/contrib/Archive/rgdal/rgdal_1.5-32.tar.gz", repos=NULL, type="source")'

# RUN Rscript -e 'install.packages(c("sf"), repos = "https://cran.microsoft.com")'

RUN Rscript -e 'install.packages(c("rJava", "sp"), repos = "https://cran.microsoft.com")'

RUN Rscript -e 'require(rJava); require(sp)'
