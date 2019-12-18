##################################################################
### Read in data from Wikipedia HTML tables

library(rvest)
#Summer olympics medal tally

url <- "https://en.wikipedia.org/wiki/2016_Summer_Olympics_medal_table"



medal_tally <- url %>% read_html() %>% 
  html_nodes(xpath='//*[@id="mw-content-text"]/div/table[2]') %>% html_table(fill=TRUE)
## copy xpath
## //*[@id="mw-content-text"]/div/table[2]
# //*[@id="mw-content-text"]/div/table[2]

medal_tally <- medal_tally[[1]]
head(medal_tally)

#WHS Sites in the UK

url2="https://en.wikipedia.org/wiki/List_of_World_Heritage_Sites_in_the_United_Kingdom_and_the_British_Overseas_Territories"


whsuk <- url2 %>% read_html() %>% 
  html_nodes(xpath='//*[@id="mw-content-text"]/div/table[3]') %>% html_table(fill=TRUE)

whsuk <- whsuk[[1]]
head(whsuk)