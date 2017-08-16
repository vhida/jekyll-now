# Troubleshooting Routine on GC Abnormality

Just fixed CPU usage burst problem caused by frequent GC. It turns out that one sorting operation on a very large array would take up the young generation heap of default size very quickly. Usually the sage says don't temper with JVM settings unless you know what you are doing. Many are intimidated and follow the wisdom. However, settings are for users to set, aren't they. Sometimes the problems requires fine-tuning the JVM and some caused by improper parameters . Here are some basic things. 

 First of all, understand the characteristic of your program with regard to the 
object creation. If you are using frameworks like Spring, do understand the part you are using.
Take a heap dump and see what are those objects which trigger the GC.  
Consider possible memory leak.
If the GC is young gen generation, you may consider to increase the young gen, also 
change SurvivorRatio. If it's the full gc, you will have to increase heap 
   


