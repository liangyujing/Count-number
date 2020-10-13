############################################
# create number of correctly solved insight and non-insight word puzzles per participant 
###########################################
number_insight<-experimental_df%>%
  filter(solution_type == 1, ACC == 1)%>%
  group_by(subject)%>%
  count(ACC)

# number of correctly non-insight
number_NonInsight<-experimental_df%>%
  filter(solution_type == 2, ACC == 1)%>%
  group_by(subject)%>%
  count(ACC)

# attach the number of trials solved with insight and non-insight to the df
#######################################################################
experimental_df$nrInsight <- NaN
for (s in unique(number_insight$subject)){
  experimental_df$nrInsight[experimental_df$subject==s] <- number_insight$n[number_insight$subject==s]
} 

experimental_df$nrNonInsight <- NaN
for (s in unique(number_NonInsight$subject)){
  experimental_df$nrNonInsight[experimental_df$subject==s] <- number_NonInsight$n[number_NonInsight$subject==s]
} 

# add to df with behavioral data RMSSD, High-frequency HRV, IBI reject
experimental_df$baseline_RMSSD <- NaN
for (s in unique(artiifact_HRV_df$subject)){
  experimental_df$baseline_RMSSD[experimental_df$subject==s] <- artiifact_HRV_df$Artiifact_RMSSD[artiifact_HRV_df$subject==s]
} 

experimental_df$HF_HRV <- NaN
for (s in unique(artiifact_HRV_df$subject)){
  experimental_df$HF_HRV[experimental_df$subject==s] <- artiifact_HRV_df$Artiifact_HF[artiifact_HRV_df$subject==s]
} 

experimental_df$num_reject_IBI <- NaN
for (s in unique(artiifact_HRV_df$subject)){
  experimental_df$num_reject_IBI[experimental_df$subject==s] <- artiifact_HRV_df$rejected_IBI[artiifact_HRV_df$subject==s]
} 

summary(experimental_df)
summary(experimental_df$ACC)
summary(preliminary_data)
