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
