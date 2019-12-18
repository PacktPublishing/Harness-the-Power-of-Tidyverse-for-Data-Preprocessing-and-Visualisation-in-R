################# dplyr with ggplot2

### corruption perception index

setwd("F:\\DataMining_R\\3_LectureData\\section3")

cpi=read.csv("cpi.csv")
head(cpi)

library(ggplot2)
library(tidyr)
library(dplyr)

######### Gather columns

cpi_history = gather(cpi, year, cpi, CPI.2012.Score:CPI.2016.Score, na.rm = TRUE)

head(cpi_history)

### lets look at the top 15 countries--> use dplyr

top2016 = cpi_history %>% filter(year=="CPI.2016.Score") %>% top_n(15,cpi)
top2016$rnk = "top"

### collect the bottom 15 countries-->use dplyr

bot2016 = cpi_history %>% filter(year=="CPI.2016.Score") %>% top_n(-15,cpi)
bot2016$rnk <- "bot"

######## combine

dt2016 <- rbind(top2016,bot2016) 

head(dt2016)
tail(dt2016)

#plot the data

library(ggplot2)

ggplot(dt2016, aes(reorder(Country, cpi), cpi)) +
  geom_bar(stat="identity", aes(fill=rnk)) +
  coord_flip() +
  xlab("") +
  ggtitle("Top and Bottom CPI's in 2016") +
  scale_fill_manual(values = c("top" = "blue", "bot" = "red"), name="CPI") +
  guides(fill = guide_legend(reverse = TRUE))

