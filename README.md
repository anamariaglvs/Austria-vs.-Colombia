# Austria-vs.-Colombia
This project compares key stats between my home country and Austria using CIA World Factbook data. It includes population, GDP, and custom indicators, plus a time series analysis of one variable with historical context and visualizations for clear, comparative insight.

country_data <- data.frame(
  Indicator = c("Population", "GDP per capita (USD)", "Life Expectancy (years)",
                "Health Expenditure (% of GDP)", "Education Expenditure (% of GDP)"),
  Austria = c("8,967,982", "$64,600", "82.7", "11.5%", "5.1%"),
  Colombia = c("49,588,357", "$18,800", "74.9", "9%", "4.9%")
)


print(country_data)


df<-data.frame(country=c("AT", "COL"), 
               population= c(8967982, 49588357),
               life_expect= c(82.7, 74.9),
                health_exp= c(0.115,0.09),
                educ_exp =c(0.051, 0.049))

#population time series of AT and COL
pop = read.csv2("~/Documents/R for Data analytics/pop.csv")

austria_index <- which(pop$`Country.Code`=="AUT")
colombia_index <- which(pop$`Country.Code`=="COL")

pop_development <- data.frame(AUT=as.numeric(as.vector(pop[austria_index, -(1:4)])),
                              COL = as.numeric(as.vector(pop[colombia_index, -(1:4)])))
pop_development$AUT = pop_development$AUT/pop_development$AUT[1] #to show the comparison growth we dived by the first value on the time series
pop_development$COL = pop_development$COL/pop_development$COL[1] #both countries start in 100% of their population 
#col has triplet its population by 300% while Austria has remain stable. One reason to be, is that developing countries
#have a tendency to growth much while coming out of poverty, but countries that are full development, are in their steady state. 
#in the solow model colombia capital per person function still gives huge output per worker 

plot(1960:2023, pop_development$AUT, type = "l", xlab = "Year", ylab = "Relative Population", ylim = c(0, max(pop_development$COL)))

lines(1960:2023, pop_development$COL, col = "red", xlab = "Year")
#source: World Bank open data

#c
barplot(df$population, main = "Population", names = df$country)
barplot(df$life_expect, main = "Life Expectations", names= df$country, ylab= "years")
barplot(df$health_exp, main ="Heatlh Expenditure", names=df$country, ylab=" Share of GDP") #which % of GDP
barplot(df$educ_exp, main = "Education Expenditure", names = df$country, ylab= "Share of GDP")
barplot(df$educ_exp, main = "Education Expenditure", names = df$country, ylab= "Share of GDP", ylim = c(0.0485, 0.0515), xpd = FALSE)
#in here the Data is percerived way different, this is a truncated graph,  I started the limits on a number very close to the actual value for colexp
#and increase automatically by so very little.

# Bar plot with full y-axis range
barplot(df$educ_exp,
        names.arg = df$country,
        main = "Education Expenditure as a Share of GDP",
        xlab = "Share of GDP",
        col = "skyblue",
        horiz = TRUE,
        xlim = c(0, max(df$educ_exp) * 1.1)) 



![Rplot02](https://github.com/user-attachments/assets/22c5343a-9158-4792-a065-c60d59770bda)![Rplot05](https://github.com/user-attachments/assets/380290ab-80ac-4323-83bb-8834566b49da)
![Rplot04](https://github.com/user-attachments/assets/8f2b7e62-752d-40ec-b378-e2d8aa46edda)
![Rplot03](https://github.com/user-attachments/assets/2f95fc6d-9112-4e9b-92a3-821908222281)
