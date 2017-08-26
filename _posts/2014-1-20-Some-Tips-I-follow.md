Years back, when I first came to the realm of programming I looked for sages and hoped to learn from them. Some tips I found turned out to be truely valueable along these years. I can't remember from where I take them. but anyway.  
  
Decompose the problem to manageable size. This is the essential spirit of Software development.   
     
1. Organize the architecture of your code.    
    
  Every package should have 5~20 classes. If more than 20, you should consider decompose the package to sub-packages. Reason: easy to manage.   

2. Find appropriate tool to finish your task.   
      
I see a lot of colleagues repeating their work day by day and never consider improve the tool. This is amazingly low-efficient.    
    
Some suggestion: first choose a tool you feel comfortable. Then get familiar with it. My favor editor in Windows is UltraEdit. For example, I know how to find a keyword in all files under a directory(and sub-directory), so in programming I choose exact and special keyword as comment if I want to modify it later. Even weeks later, I can find out those spots in one minute.I believe most editor also support multiple word replacement. So for similar class, I copy and paste multi-replace the keyword, modify a little bit, that's it.        
      
In Linux/UNIX, I like to use scripts to avoid daily repeating work. For example: my development tree is complicated, it needs a really good head to memorize tree structure and go to where you want. In this case, create a script called "go", then "go bouquet" will bring me to my implementation: bouquet package.  "go org.dvb.user" will bring me to "org.dvb.user" package.       
          
3. Form good coding habit.    
      
If you have a good habit, you know exactly where a specific part of code is, and you can understand your own code easily  after several months. When I read my colleague's code, I find he used blank line quite well. That is, between meaningful blocks, he add 3 blank lines. So the whole program looks very neat. In just one look, I know where is import, where is variable declaration, where is public methods, where is private methods. And because all methods in each block is organized in alphabetical order, it is really easy to find a method definition.           
      
4. If you don't know how to ..., refer to other's sample code.   
        
I find Sun's Java source code, MFC's sample code, Linux's source code, all of them are really good learning materials.    
       
Last, a book definitely worth reading: "Design Pattern" (Gamma, etc.) If you haven't read it, buy one and read it.    
    
Have fun in programming!    



