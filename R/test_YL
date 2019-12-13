
################################
# using enrichR package 
################################
#https://github.com/ylippi/enrichR/blob/master/R/api_wrapper.R


genes <- c("DISC1", "ASPG4", "ASPG1", "ASPG2", "SLC6A4", "ASPG3", "FRAXE", "FRAXA", "FHIT", "NTM", "SLTM", "RASGRP4", "NOS2", "NOS1", "SHANK3", "DISC2", "TSNAX", "OXTR", "ARSD")
databases <- c("KEGG_2016", "WikiPathways_2016")

######Step 1: Post gene list to EnrichR
  req.body <- list(list=paste(gene.list, collapse="\n"))
  post.req <- httr::POST("http://amp.pharm.mssm.edu/Enrichr/enrich", encode="multipart", body=I(req.body))
  
	(listpost= httr::content(post.req))
[1] <head>\n<meta http-equiv="Content-Type" content="text/html;charset=UTF-8" ...
[2] <body onload="contributePopup(25176937, 'null');">\n<div id="header">\n   ...
#									^ <=> userListId

 ######Step 2: Get results from posted gene list
  database.enrichments <- list()
  for (idx in 1:length(databases)) {
    database <- databases[idx]
    get.req <- httr::GET(paste("http://amp.pharm.mssm.edu/Enrichr/enrich?backgroundType=", database, sep=""))
    if (!grepl("success", httr::http_status(get.req)$category, ignore.case=T)) stop("Retrieving results from EnrichR failed")
    
    response.content <- mungeResponseContent(httr::content(get.req)[[database]])
    
    if (length(response.content) > 1) {
      database.res <- data.table::rbindlist(response.content)
      database.res[, 1] <- rep(database, nrow(database.res))
      database.enrichments[[idx]] <- database.res[, paste("V", c(1, 2, 3, 7, 6), sep=""), with=F]
    }
  }

################################
# use enricher web site with URLs
################################
## view list genes
http://amp.pharm.mssm.edu/Enrichr/view?userListId=25176937 



#########################
## get result on lib
#userListId=25177101
#backgroundType=KEGG_2019_Human
http://amp.pharm.mssm.edu/Enrichr/enrich?userListId=25176937&backgroundType=KEGG_2019_Human


#################
## download result table
#userListId=25177101
#filename=TEstEnrichDwnld
#backgroundType=KEGG_2019_Human

amp.pharm.mssm.edu/Enrichr/export?userListId=25176937&filename=TEstEnrichDwnld&backgroundType=KEGG_2019_Human

