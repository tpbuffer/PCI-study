# PCI-study
According to PCI(Programming Collective Intelligence),I've learned a lot.
# Returns the Pearson correlation coefficient for p1 and p2 皮尔逊相关系数,根据皮尔逊等价公式进行编写
def sim_pearson(prefs,p1,p2):
  # Get the list of mutually rated items
  si={}
  for item in prefs[p1]: 
    if item in prefs[p2]:
        si[item]=1#item是对应cristcs里面的电影名称，例如Snakes on a Plane

  # if they are no ratings in common, return 0
  if len(si)==0: return 0#如果两者没有共同之处返回0

  # Sum calculations
  n=len(si)
  
  # Sums of all the preferences
  sum1=sum([prefs[p1][it] for it in si])
  sum2=sum([prefs[p2][it] for it in si])
  
  # Sums of the squares
  sum1Sq=sum([pow(prefs[p1][it],2) for it in si])
  sum2Sq=sum([pow(prefs[p2][it],2) for it in si])	
  
  # Sum of the products
  pSum=sum([prefs[p1][it]*prefs[p2][it] for it in si])
  
  # Calculate r (Pearson score)
  num=pSum-(sum1*sum2/n)
  den=sqrt((sum1Sq-pow(sum1,2)/n)*(sum2Sq-pow(sum2,2)/n))
  if den==0: return 0

  r=num/den

  return r
#tp:根据皮尔逊公式等价关系重新编制
def sim_pearson_mean(prefs,p1,p2):
  # Get the list of mutually rated items
  print("这是皮尔逊另外一个等价公式计算函数")
  si={}
  for item in prefs[p1]:
    if item in prefs[p2]:
        si[item]=1#item是对应cristcs里面的电影名称，例如Snakes on a Plane

  # if they are no ratings in common, return 0
  if len(si)==0: return 0#如果两者没有共同之处返回0

  # Sum calculations
  n=len(si)

  #计算平均值
  mean1=sum([prefs[p1][it] for it in si])/n
  mean2=sum([prefs[p2][it] for it in si])/n

  #计算协方差
  cov=sum([(prefs[p1][it]-mean1)*(prefs[p2][it]-mean2) for it in si])

  #计算平方和
  sum1s=sum([pow((prefs[p1][it]-mean1),2) for it in si])
  sum2s=sum([pow((prefs[p2][it]-mean2),2) for it in si])

  #计算分母
  sumM=sqrt(sum1s*sum2s)

  if sumM==0: return 0

  r=cov/sumM

  return r
