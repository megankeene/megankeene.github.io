### Indian Ocean Swordfish R Code

```markdown 
#von Bertalannfy Growth Curve of the Indian Ocean Swordfish

L00 = 455.0
K = 0.23
t = seq(from = 0, to = 9, by = 1)
L_t_est = ((L00) * (1-(exp((-K)*(t+1)))))

growth_curve <- data.frame(L_t_est, K, t)

ggplot(data = growth_curve, aes(x=t, y=L_t_est)) + 
  # Tell ggplot that the plot type should be a scatter plot
  geom_point() +
  # Add a linear model line
  geom_smooth(method = "loess") + 
  # Change the y-axis title
  ylab("Estimated Length (cm)") +   
  # Change the x-axis title
  xlab("Age (years)") + 
  # Title
  ggtitle("von Bertalanffy Growth Curve of Xiphias gladius")
  
```markdown 
#Biomass Graph of the Indian Ocean Swordfish from 1950 to 2014 using data from Ram Legacy 

ggplot(data = Ram_Legacy_Data_Set, aes(x=year, y=SSB)) + 
  # Tell ggplot that the plot type should be a scatter plot
  geom_point() +
  # Change the y-axis title
  ylab("Spawning Stock Biomass") +   
  # Change the x-axis title
  xlab("Year") + 
  # Title
  ggtitle("Change in Biomass of Xiphias gladius")
  
```markdown 
#Catch Data for the Indian Ocean Swordfish for EEZ vs. High Seas using data from Sea Around Us

Sea_Around_Us_Data_csv_ =
  Sea_Around_Us_Data_csv_ %>%
  mutate(area=ifelse(area_type == "eez","EEZ","high seas"))

yearsum =
Sea_Around_Us_Data_csv_ %>%
  group_by(year,area_type) %>%
  summarise(catch=sum(tonnes))


ggplot(data = yearsum, aes(x=year,y=catch,group=area_type, color=area_type)) +
  geom_point() + 
  geom_smooth(method = "loess") +
  ylab("Tonnes") + 
  xlab("Year") + 
    ggtitle("Catch per Year Curve of Xiphias gladius") 

```markdown 
#Fishing Gear Graph used to catch the Indian Ocean Swordfish using data from Sea Around Us

Sea_Around_Us_Data_csv_ =
  Sea_Around_Us_Data_csv_ %>%
  
  mutate(Gear= ifelse(gear_type == "longline","Longline","Other"))

ggplot(data = Sea_Around_Us_Data_csv_, aes(x=year, y=tonnes, fill=Gear)) + 
  geom_bar(stat = "identity") +
  # Change the y-axis title
  ylab("Catch (tonnes)") +   
  # Change the x-axis title
  xlab("Year") + 
  # Title
  ggtitle("Gear Types used to Catch Xiphias gladius")
