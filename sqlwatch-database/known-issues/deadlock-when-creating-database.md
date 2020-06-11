# Deadlock when creating database

A few people experienced a deadlock whilst creating SQLWATCH Database. In all cases this was caused by the Query Store enabled on the model database. The locking transaction was `GetQdsTotalReseveredPageCount`. If you experience such issue, please disable Query Store on the model database and then re-try SQLWATCH deployment. 

