Interpreters vs. Compilers!

Ciao!👋🏽 It's October 1st, 1975. As, Joe Fraizers cornerman threw in the towel the greatest find ever ended. Ali vs. Fraizer. This fight was believed to be the greatest fight of all time. That was until the great debate of "Interpreters vs. Compilers" was introduced. Jk. But this post will cover interpreters vs compilers. 

##Interpreters
Interpreters are these flashy and clever programs that lets users run their own programs. Instead of turning code into machine code or the language that computers understand, interpreters evaluate each line of the program one by one. What does this mean? i asked the same question. I'll explain... 

An interpreter goes through 4 stages. Scanning, Parsing, Semantic analysis, and Interpreting/Evaluating/Executing. You may see these 4 stages with different names but the function should be the same. An interpreter works by scanning each character inputed and creating tokens based on the keywords, literals, etc. The output is a list of tokens. Those tokens are then parsed, to create a parse/abstract syntax tree* (AST). Semantic analysis ensures that the code makes grammatical sense. This will make more sense later. The interpreting actually happens at the last phase where you visit each node in your AST and well, Interpret it. 

##Compilers 
A compiler analyzes and translates your code to an executable file that contains the machine code for you actual computer to run. The main idea here is that the code is translated to machine code that can be directly read by the computer. 

##Interpreters vs. Compilers
Really, you can't versus them becasue they often work with eachother, especially in more modern languages. Swift uses both and uses something called SIL ( Swift Intermediate Langauge ) to pass to the compiler after the interpreting. Languages like C are pretty much purely compiled which uses a bit of preprocessing, translates to assembly, and creates and executable. So, i think the way to properly impress your friends is to nerd out on both. 

p.s. Please let me know if i should clarify on anything but i will have seperate files for going into more detail on parts of the process. Also if there are some seasoned ( or unseasoned ) vets that can give some feedback, please feedback! Thank you.

