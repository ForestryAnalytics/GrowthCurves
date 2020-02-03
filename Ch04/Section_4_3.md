## Within-participant Effects

#### TargetFix

Within-subject effects
Example: Target fixation in spoken word-to-picure matching (VWP)

#================#

ggplot(TargetFix, aes(Time, meanFix, color=Condition, fill=Condition)) +
  stat_summary(fun.y=mean, geom="line") +
  stat_summary(fun.data=mean_se, geom="ribbon", color=NA, alpha=0.3) +
  theme_bw() + expand_limits(y=c(0,1)) + legend_positioning(c(1,1)) +
  labs(y="Fixation Proportion", x="Time since word onset (ms)")
  
  
#================#

Within-subject effects: fit full GCA model

#================#
m.full <- lmer(meanFix ~ (poly1+poly2+poly3)*Condition + #fixed effects
                 (poly1+poly2+poly3 | Subject) + #random effects of Subject
                 (poly1+poly2+poly3 | Subject:Condition), #random effects of Subj by Cond
               data=TargetFix.gca, REML=F)
get_pvalues(m.full)
