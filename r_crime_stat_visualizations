crime<-read.csv(filepath)

crime$Dates<-as.POSIXlt(as.character(crime$Dates),tz="","%Y-%m-%d %H:%M:%S")
crime$DayOfYear<-format(crime$Dates, '%j')
crime$Year<-format(crime$Dates, '%Y')
levels(crime$DayOfYear)<-levels(factor(crime$DayOfYear))
crime$DayOfWeek2<-format(crime$Dates, '%A')
crime$Year<-levels(factor(crime$Year))

assault<-subset(crime, Category=='ASSAULT')
assault$Descript<-droplevels(assault$Descript)

##table(crime$Category) #Looks like they're all violent 

crime$CrimeType<-ifelse(crime$Category=='ASSAULT'
						|crime$Category=='ROBBERY'
						|crime$Category=='SEX OFFENSES FORCIBLE',
						'VIOLENT','NON-VIOLENT'
						)

viol<-subset(crime, Category=='VIOLENT')						
library(ggplot2)
c<-ggplot(crime, aes(Year))
c+geom_bar()+facet_wrap(~CrimeType)
#Frequency plot of violent vs non-violent crime
ggplot(crime, aes(Year))+
geom_freqpoly(aes(group=CrimeType, colour=CrimeType))
#given the incomplete 2015 data, subset w/ 2003-2014
crime2<-subset(crime, crime$Year!=2015)
#Line plot of frequency of violent vs non-violent crime, 2003-2014 
ggplot(crime2, aes(Year))+ geom_freqpoly(aes(group=CrimeType, colour=CrimeType), weight=100)

#Next Question: Do certain crimes
levels(crime$DayOfYear)<-levels(factor((as.integer(crime$DayOfYear))))
viol3<-subset(viol3, DayOfYear<=60)
ggplot(viol, aes(factor(DayOfYear),fill=Category))+geom_bar()
#zoom in on violent crime graph
viol3<-subset(viol3, Year==2010)
ggplot(viol3, aes(factor(DayOfYear),fill=Category))+geom_bar()
#look at one year w/ Fridays plotted
viol4<-subset(viol3, Year==2010)
viol2013$DayOfYear<-as.numeric(viol2013$DayOfYear)
viol2013<-subset(viol2013, DayOfYear<80)
levels(viol2013$DayOfYear)<-levels(factor(viol$DayOfYear))

ggplot(viol2013, aes(factor(DayOfYear),fill=Category))+geom_bar()+
+ geom_vline(xintercept=seq(from=4, to=40, by=7))
