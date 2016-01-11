# download-mongodb-data-by-time
Download data from mongodb using time constraints

mongo<-mongo.create(host = "", name = "", db = "", timeout = 0L)
mongo_status<-mongo.is.connected(mongo)
if(mongo_status==FALSE)
  print("MongoDB Server is not available")
  
start.time <- as.POSIXct(max(realtime.data$ts)) #maximum time taken from another dataframe
end.time <- as.POSIXct(Sys.time())
query <- mongo.bson.from.list(list("ts"= list("$gt"= start.time, "$lt" = end.time)))
realtime.data.new<-mongo.find.batch(mongo,'',query=query, fields=mongo.bson.from.JSON(Input))
realtime.data.new <- rbindlist(realtime.data.new,fill = TRUE)
