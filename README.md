# -z-sin-x-sin-y
экстремумы двумерной функции z = sin(x) * sin(y)
![загруженное](https://github.com/Mertsajus4aja/-z-sin-x-sin-y/assets/112537979/d18f02a4-4378-46ff-8302-e44cf5313e8e)



from mpl_toolkits.mplot3d import Axes3D

import numpy as np

from matplotlib import cm

import matplotlib.pyplot as plt



f = lambda x,y: np.sin(x)*np.sin(y)



def Min_Max(fun):


 xval = np.linspace(0, 15, 100)
 
 yval = np.linspace(0, 15, 100)



 xgrid, ygrid = np.meshgrid(xval, yval)


 zgrid = f(xgrid, ygrid)

 fig = plt.figure(figsize = (30, 30))
 
 ax = fig.gca(projection='3d')
 
 #список на глобальный максимум с у и х
 
 global_maxx =[]
 
 global_maxy =[]


 global_maxz =[]
 
 for a in range(zgrid.shape[0]):
 
  for b in range(zgrid.shape[1]):
  
    if zgrid[a,b] == np.amax(zgrid): 
    
     global_maxx.append(a)
     
     global_maxy.append(b)
     
     global_maxz.append([a,b])
     
 #список на глобальный минимум х и у
 
 global_minx = []
 
 global_miny = []
 
 global_minz = []
 
 for c in range(zgrid.shape[0]):
 
  for d in range(zgrid.shape[1]):
  
    if zgrid[c,d] == np.amin(zgrid):
    
     global_minx.append(c)
     
     global_miny.append(d)
     
     global_minz.append([c,d])
     
 ### Выводим локальные максимумы

 
 local_maxx = []
 
 local_maxy = []
 
 local_maxz = []
 

 for g in range (len(xval)-1):
 
  for h in range (len(yval) -1):
  
     if zgrid[g-1,h-1] < zgrid[g,h]: 
     
      if zgrid[g-1,h] <  zgrid[g,h]:
      
       if zgrid[g-1,h+1] < zgrid[g,h]:
       
        if zgrid[g,h-1] < zgrid[g,h]:
        
         if zgrid[g,h+1] < zgrid[g,h]:
         
          if zgrid[g+1, h-1] < zgrid[g,h]:
          
           if zgrid[g+1, h+1] < zgrid[g,h]:
           
            if zgrid[g+1, h] < zgrid[g,h]:
            
             local_maxx.append(g)
             
             local_maxy.append(h)
             
             local_maxz.append([g,h])


 # локальные минимумы
 
 local_minx = []
 
 local_miny = []
 
 local_minz = []


 for u in range (zgrid.shape[0] - 1):
 
  for v in range (zgrid.shape[1] - 1):
  
     if zgrid[u-1,v-1] > zgrid[u,v]: 
     
      if zgrid[u-1,v] > zgrid[u,v]:
      
       if zgrid[u-1,v+1] > zgrid[u,v]:
       
        if zgrid[u,v-1] > zgrid[u,v]:
        
         if zgrid[u,v+1] > zgrid[u,v]:
         
          if zgrid[u+1, v-1] > zgrid[u,v]:
          
           if zgrid[u+1, v+1] > zgrid[u,v]:
           
            if zgrid[u+1, v] > zgrid[u,v]:
            
             local_minx.append(u)
             
             local_miny.append(v)
             
             local_minz.append([u,v])
             
  
  


 plt.xlabel('x')
 
 plt.ylabel('y')
 
 plt.title('Локальные и глобальные минимумы и максимумы функции z = sin(x) * sin(y)')
 
 ax.scatter(xval[local_maxx], yval[local_maxy], zgrid[local_maxx, local_maxy], color='green', s=1000, marker='o')
 
 ax.scatter(xval[local_minx], yval[local_miny], zgrid[local_minx, local_miny], color='red', s=1000, marker='o')
 
 ax.scatter(xval[global_maxx], yval[global_maxy], zgrid[global_maxx,global_maxy], c!
olor='blue', s=2000, marker='o')

 ax.scatter(xval[global_minx], yval[global_miny], zgrid[global_minx,global_miny], color='black', s=2000, marker='o')
 
 ax.plot_surface(xgrid, ygrid, zgrid, cmap = 'gist_gray_r', alpha=0.3)
 
 plt.show()
 
 print('Лист локальных максимумов - ', local_maxz)
 
 print('Лист локальных минимумов - ', local_minz)
 
 print('Лист глобальных минимумов - ', global_minz)
 
 print('Лист глобальных минимумов - ', global_maxz)


 

Min_Max(f)
