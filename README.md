# Project1-

library(data.table)

##########PLOT1##############################

#####change txt file to dataframe######
DataFrame <- data.table::fread(input = "household_power_consumption.txt"
                             , na.strings="?")

###Change the value of date to date type
DataFrame[, Date := lapply(.SD, as.Date, "%d/%m/%Y"), .SDcols = c("Date")]

# Filter Dates for (2007-02-01- 2007-02-02)
DateFrame <- DataFrame[(Date >= "2007-02-01") & (Date <= "2007-02-02")]


png("plot1.png", width=480, height=480)

dev.off()


#########PLOT2######################

DataFrame1 <- data.table::fread(input = "household_power_consumption.txt"
                               , na.strings="?")

Dataframe1[, Global_active_power := lapply(.SD, as.numeric), .SDcols = c("Global_active_power")]

###Change the value of date to date type
DataFrame1[, dateTime := as.POSIXct(paste(Date, Time), format = "%d/%m/%Y %H:%M:%S")]

# Filter Dates (2007-02-01 - 2007-02-02)
DataFrame1 <- DataFrame1[(dateTime >= "2007-02-01") & (dateTime < "2007-02-02")]

png("plot2.png", width=480, height=480)

## Plot 2
plot(x =DataFrame1[, dateTime]
     , y = DataFrame1[, Global_active_power]
     , type="l", xlab="", ylab="Global Active Power (kilowatts)")

dev.off()

##########PLOT3##################
DataFrame2 <- data.table::fread(input = "household_power_consumption.txt"
                                , na.strings="?")

###Change the value of date to date type
DataFrame2[, dateTime := as.POSIXct(paste(Date, Time), format = "%d/%m/%Y %H:%M:%S")]

# Filter Dates for 2007-02-01 and 2007-02-02
DataFrame2 <- DataFrame2[(dateTime >= "2007-02-01") & (dateTime < "2007-02-02")]

png("plot3.png", width=480, height=480)

# Plot 3
plot(DataFrame2[, dateTime], DataFrame2[, Sub_metering_1], type="l", xlab="", ylab="Energy sub metering")
lines(DataFrame2[, dateTime], DataFrame2[, Sub_metering_2],col="red")
lines(DataFrame2[, dateTime], DataFrame2[, Sub_metering_3],col="blue")
legend("topright"
       , col=c("black","red","blue")
       , c("Sub_metering_1  ","Sub_metering_2  ", "Sub_metering_3  ")
       ,lty=c(1,1), lwd=c(1,1))

dev.off()

#################Plot4#######################

DataFrame3 <- data.table::fread(input = "household_power_consumption.txt"
                                , na.strings="?")



###Change the value of date to date type
DataFrame3[, dateTime := as.POSIXct(paste(Date, Time), format = "%d/%m/%Y %H:%M:%S")]

# Filter Dates for 2007-02-01 and 2007-02-02
DataFrame3 <- DataFrame3[(dateTime >= "2007-02-01") & (dateTime < "2007-02-02")]

png("plot4.png", width=480, height=480)

par(mfrow=c(2,2))

# Plot 1
plot(DataFrame3[, dateTime], DataFrame3[, Global_active_power], type="l", xlab="", ylab="Global Active Power")

# Plot 2
plot(DataFrame3[, dateTime],DataFrame3[, Voltage], type="l", xlab="datetime", ylab="Voltage")

# Plot 3
plot(DataFrame3[, dateTime], DataFrame3[, Sub_metering_1], type="l", xlab="", ylab="Energy sub metering")
lines(DataFrame3[, dateTime], DataFrame3[, Sub_metering_2], col="red")
lines(DataFrame3[, dateTime], DataFrame3[, Sub_metering_3],col="blue")
legend("topright", col=c("black","red","blue")
       , c("Sub_metering_1  ","Sub_metering_2  ", "Sub_metering_3  ")
       , lty=c(1,1)
       , bty="n"
       , cex=.5) 

# Plot 4
plot(DataFrame3[, dateTime], DataFrame3[,Global_reactive_power], type="l", xlab="datetime", ylab="Global_reactive_power")

dev.off()


