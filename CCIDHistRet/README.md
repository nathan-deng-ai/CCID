[<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/banner.png" width="888" alt="Visit QuantNet">](http://quantlet.de/)

## [<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/qloqo.png" alt="Visit QuantNet">](http://quantlet.de/) **CCIDHistRet** [<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/QN2.png" width="60" alt="Visit QuantNet 2.0">](http://quantlet.de/)

```yaml


Name of Quantlet : CCIDHistRet

Published in :  'Rise of the Machines?
Intraday High-Frequency Trading Patterns of Cryptocurrencies'

Description : plots HF (5mins) returns of 12 cryptocurenicies

Keywords : high-frequency, returns, cryptocurrency
 
See also : CCIDcorr, CCIDHistReturnsDensity, CCIDHistVola, CCIDReturns, CCIDvolaGAM, CCIDvolumeGAM.
 
 

Author : Alla Petukhina

Submitted :  Wed, July 17 2019 by Alla Petukhina

Datafile : 

Example : 
```

### R Code
```r

####5Set working directory
#setwd("~")
#### Load packages and libraries ####
source("CCIDPackages.R")

rm(list=ls(all=TRUE))
graphics.off()

load('CCID.Rdata')

cols = rainbow(length(coins), s = 1, v = 1, start = 0, end = max(1, n - 1)/n, alpha = 1)

CC_returns_mat = as.data.frame(CC_returns)
CC_returns_xts = xts::as.xts(CC_returns_mat, order.by = TIME_DATE[-1])
CC_abs_returns_mat = as.data.frame(abs(CC_returns_mat))
CC_abs_returns_xts = xts::as.xts(CC_abs_returns_mat, order.by = TIME_DATE[-1])
CC_price_mat = as.data.frame(CC_price)
CC_price_xts = xts::as.xts(CC_price_mat, order.by = TIME_DATE)
CC_volume_mat = as.data.frame(CC_volume)
CC_volume_mat = as.data.frame(CC_volume_mat, order.by = TIME_DATE)
CC_volume_xts = xts::as.xts(CC_volume_mat, order.by = TIME_DATE)
n = nrow(CC_returns_mat)
result = matrix(1, ncol = 7, nrow = ncol(CC_returns_mat), dimnames = list(coins, c("rho(ret):", 
                                                                                   "rho n(ret^2):", "rho(|ret|):", "S:", "K:", "JB:", "JB p-value:")))
rownames(result) = coins


# 5min returns plots
for (i in 1:length(coins)){
  pdfname =  paste0("Returns_",gsub(" ", "", coins[i], fixed = TRUE),".pdf")
  pdf(file = pdfname)
  plot(zoo(CC_returns_xts[, i]), col = cols[i], ylab = coins[i])
  dev.off()
}
dev.off()


```

automatically created on 2021-04-23