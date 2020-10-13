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
