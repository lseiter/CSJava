.. qnum::
   :prefix: 5-1-
   :start: 1
   
.. |CodingEx| image:: ../../_static/codingExercise.png
    :width: 30px
    :align: middle
    :alt: coding exercise
    
    
.. |Exercise| image:: ../../_static/exercise.png
    :width: 35
    :align: middle
    :alt: exercise
    
    
.. |Groupwork| image:: ../../_static/groupwork.png
    :width: 35
    :align: middle
    :alt: groupwork

..	index::    
	single: method 
    single: return
    single: parameter
    single: argument
    single: abstraction
    pair: method; parameter
    pair: method; argument
    pair: method; return 
    
Writing Methods
=================

Up until this unit, you wrote all  code in the main method, 
but now you will be creating new methods that can be called by the main method. Why have multiple methods instead of just one? 
**Procedural Abstraction** allows us to name a block of code as a method and 
call it whenever we need it, abstracting away the details of how it works.  
This serves to organize our code by function and reduce 
the repetition of code. In addition, it helps with debugging and maintenance since 
changes to that block of code only need to happen in one place. 
Here are some of the main reasons to use multiple methods in your programs:

- Organization and Reducing Complexity: organize your program into small sections of code to reduce its complexity. Divide a problem into subproblems to solve it a piece at a time.
- Reusing Code: avoid repetition of code. Reuse code by putting it in a method and calling it whenever needed.
- Maintainability and Debugging: smaller methods are easier to debug and understand than searching through a large main method.

Let's look at an example with repetition of code and 
create methods to reduce the repetition of code. 


|Exercise| Check Your Understanding

.. clickablearea:: repeatedcode_methods
    :question: Click on all the lines that are repeated.
    :iscode:
    :feedback: Look for lines that are completely identical.  

    :click-incorrect:public static void main(String args[]) {:endclick:
        :click-correct:System.out.println("I'm looking over a four-leaf clover");:endclick:
        :click-correct:System.out.println("That I overlooked before");:endclick:
        :click-incorrect:System.out.println("One leaf is sunshine, the second is rain");:endclick:
        :click-incorrect:System.out.println("Third is the roses that grow in the lane");:endclick:
        :click-incorrect:System.out.println();:endclick:
        :click-incorrect:System.out.println("No need explaining, the one remaining");:endclick:
        :click-incorrect:System.out.println("Is somebody I adore");:endclick:
        :click-correct:System.out.println("I'm looking over a four-leaf clover");:endclick:
        :click-correct:System.out.println("That I overlooked before");:endclick:
    :click-incorrect:}:endclick:
            
Did you find some repeated lines of the song? 
You may have noticed that the chorus is 
repeated "I'm looking over a four-leaf clover That I overlooked before" 
When you see repeated code, that is a signal for you to make a new method!

A method is a **named** set of statements.  When we want to execute the statements, 
we call the method using its name.
In a subsequent lesson you will create methods that are called using an object, 
referred to as **object methods** or **instance methods**.
The methods in this unit are called without an object, so they are  **static methods**.  
Static methods are also referred to as class methods.

Defining a Static Method
-------------------------

.. figure:: Figures/methodsignature.png
    :width: 400px
    :align: center
    :figclass: align-center

    Figure 1: Method Header(Signature) and Method Body
  

There are two steps to creating and calling a static method:

    **Step 1. Method Definition**:  write the method's **header** and **body**.  
    The header is also called 
    a method **signature**.  The parts of the main method header are shown in Figure 1, 
    which include an access modifier,
    static modifier, return type, name, and formal parameters.   The method body 
    consists of a set of statements enclosed in curly braces { }.  

    The code below contains a chorus() method definition 
    that we could write to encapsulate the two lines that get repeated in the song.  

        .. code-block:: java

            // Step 1: define a new method named chorus
            public static void chorus() 
            { 
                System.out.println("I'm looking over a four-leaf clover");
                System.out.println("That I overlooked before");
            }


    **Step 2. Method Call**: whenever you want to use a method, you can call the method using the method name followed by parenthesis, for example methodName();  
    The statements in the method body will be executed each time the method is called.  
    
    Look at the method header in step 1 above:
    ``public static void chorus()``.  The header indicates the return type is void and there are no formal parameters
    between the parenthesis, which means you can call the method as shown:

        .. code-block:: java

           // Step 2: call the chorus method
           chorus(); 


The main method can call ``chorus();`` anytime we want the two print statements in the method body to be executed.
Notice that we can just call the static method, we don't need to create an object to use for calling the method.

   
|CodingEx| **Coding Exercise**

.. activecode:: fourleafcloversong
  :language: java   
  :autograde: unittest    
  :practice: T

  Run the following code to see the song print out.  
  Notice the first line of code in the main method
  is a call to the new method chorus().
  Can you replace the last two lines in the second verse in the main 
  method with another call to the chorus() method? 
  Step through using on the Code Lens button to see how the main method calls the chorus method.
  ~~~~
  public class Song 
  { 
    // The chorus method
    public static void chorus() 
    {
       System.out.println("I'm looking over a four-leaf clover");
       System.out.println("That I overlooked before");
    }

    public static void main(String args[]) 
    {
      chorus();
      System.out.println("One leaf is sunshine, the second is rain");
      System.out.println("Third is the roses that grow in the lane");
      System.out.println();
      System.out.println("No need explaining, the one remaining");
      System.out.println("Is somebody I adore");
      // Can you replace these 2 lines with a method call to chorus()?
      System.out.println("I'm looking over a four-leaf clover");
      System.out.println("That I overlooked before");
    }
  }
  ====
  import static org.junit.Assert.*;
    import org.junit.*;;
    import java.io.*;
    
    public class RunestoneTests extends CodeTestHelper
    {
        @Test
        public void testMain() throws IOException
        {
            String output = getMethodOutput("main");
            String expect = "I'm looking over a four-leaf clover\nThat I overlooked before\nOne leaf is sunshine, the second is rain\nThird is the roses that grow in the lane\n\nNo need explaining, the one remaining\nIs somebody I adore\nI'm looking over a four-leaf clover\nThat I overlooked before";
            boolean passed = getResults(expect, output, "Expected output from main");
            assertTrue(passed);
        }

        @Test
        public void testcodeContains(){
          int count = countOccurences(getCode(),"chorus();");
          boolean passed = count > 1;
          passed = getResults("> 1 chorus call",  count  + " chorus call(s)", "Added second call to chorus?", passed);
          assertTrue(passed);
        }

    }
  
|Exercise| **Check Your Understanding**
   
.. clickablearea:: greet_method_signature
    :question: A method definition consists of a method header and a method body. Click on all of the method headers (signatures) in the following code.
    :iscode:
    :feedback: There is one method header for the greet method and one for the main method.  
    
    :click-incorrect:public class Test2:endclick:
    :click-incorrect:{:endclick:
        :click-correct:public static void greet():endclick:
        :click-incorrect:{:endclick:
            :click-incorrect:System.out.println("Hello!");:endclick:
            :click-incorrect:System.out.println("How are you?");:endclick:
        :click-incorrect:}:endclick:
        :click-incorrect: :endclick:
        :click-correct:public static void main(String[] args):endclick:
        :click-incorrect:{:endclick:
            :click-incorrect:System.out.println("Before greeting");:endclick:
            :click-incorrect:greet();:endclick:
            :click-incorrect:System.out.println("After greeting");:endclick:
        :click-incorrect:}:endclick:
    :click-incorrect:}:endclick:


|Exercise| **Check Your Understanding**
   
.. clickablearea:: greet_method_body
    :question: Click on all statements contained within the greet method body.
    :iscode:
    :feedback: The greet method body consists of the 2 print statements nested between the curly braces that follow the method header  
    
    :click-incorrect:public class Test2:endclick:
    :click-incorrect:{:endclick:
        :click-incorrect:public static void greet():endclick:
        :click-incorrect:{:endclick:
            :click-correct:System.out.println("Hello!");:endclick:
            :click-correct:System.out.println("How are you?");:endclick:
        :click-incorrect:}:endclick:
        :click-incorrect: :endclick:
        :click-incorrect:public static void main(String[] args):endclick:
        :click-incorrect:{:endclick:
            :click-incorrect:System.out.println("Before greeting");:endclick:
            :click-incorrect:greet();:endclick:
            :click-incorrect:System.out.println("After greeting");:endclick:
        :click-incorrect:}:endclick:
    :click-incorrect:}:endclick:


|Exercise| **Check Your Understanding**
   
.. clickablearea:: greet_method_call
    :question: Click on the greet method call.
    :iscode:
    :feedback: The greet() method call occurs in the main method.  
    
    :click-incorrect:public class Test2:endclick:
    :click-incorrect:{:endclick:
        :click-incorrect:public static void greet():endclick:
        :click-incorrect:{:endclick:
            :click-incorrect:System.out.println("Hello!");:endclick:
            :click-incorrect:System.out.println("How are you?");:endclick:
        :click-incorrect:}:endclick:
        :click-incorrect: :endclick:
        :click-incorrect:public static void main(String[] args):endclick:
        :click-incorrect:{:endclick:
            :click-incorrect:System.out.println("Before greeting");:endclick:
            :click-correct:greet();:endclick:
            :click-incorrect:System.out.println("After greeting");:endclick:
        :click-incorrect:}:endclick:
    :click-incorrect:}:endclick:


.. fillintheblank:: println_called

   Given the Test2 class listed above, how many times is the **System.out.println** called when the main method runs?

   -    :4: Correct.  
        :.*: Incorrect. The main method calls System.out.println directly 2 times, and the call to greet() results in 2 additional calls to System.out.println.



|Exercise| **Check your understanding**

.. mchoice:: likeFoodMethods
   :practice: T
   :answer_a: I like to eat eat eat.
   :answer_b: I like to eat eat eat fruit.
   :answer_c: I like to apples and bananas eat.
   :answer_d: I like to eat eat eat apples and bananas!
   :correct: d
   :feedback_a: Try tracing through the print method and see what happens when it calls the other methods.
   :feedback_b: There is a fruit() method but it does not print out the word fruit.
   :feedback_c: The order things are printed out depends on the order in which they are called from the print method.
   :feedback_d: Yes, the print method calls the consume method 3 times and then the fruit method to print this.
  
   What does the following code print out?

   .. code-block:: java

      public class LikeFood 
      {
        
        public static void fruit()
        {
            System.out.println("apples and bananas!");
        }

        public static void consume() 
        {
           System.out.print("eat ");
        }
        
        public static void main(String[] args) 
        {
            System.out.print("I like to ");
            consume();
            consume();
            consume();
            fruit();
        }
    }






  
|CodingEx| **Coding Exercise**

.. activecode:: FarmerVerse
  :language: java   
  :autograde: unittest    
  :practice: T

  A refrain is similar to a chorus, although usually shorter in length such as a single line that gets repeated.
  Add a method named "refrain" to reduce redundancy in the following code.
  You should update the main method to call the new method.
  ~~~~
  public class FarmerSong 
  { 

    public static void main(String args[]) 
    {
       System.out.println("The farmer in the dell");
       System.out.println("The farmer in the dell");
       System.out.println("Heigh ho the derry-o");
       System.out.println("The farmer in the dell");
    }
    
  }
  ====
  import static org.junit.Assert.*;
    import org.junit.*;;
    import java.io.*;
    
    public class RunestoneTests extends CodeTestHelper
    {
        @Test
        public void testSignature(){
          int count = countOccurences(getCode(),"public static void refrain()");
          boolean passed = count == 1;
          passed = getResults("1 refrain signature",  count  + " refrain signature", "Is your refrain method signature correct?", passed);
          assertTrue(passed);
        }

        @Test
        public void testcodeContains(){
          int count = countOccurences(getCode(),"refrain();");
          boolean passed = count == 3;
          passed = getResults("3 refrain calls",  count  + " refrain calls", "Added enough calls to refrain?", passed);
          assertTrue(passed);
        }

    }


Summary
-------

- **Procedural Abstraction** (creating methods) reduces the complexity and repetition of code. We can name a block of code as a method and call it whenever we need it, abstracting away the details of how it works.  

- A programmer breaks down a large problem into smaller subproblems by creating methods to solve each individual subproblem.

- To write a method, write a **method definition** with a **method signature** like "public void chorus()" and a **method body** that consists of statements nested within {}.

- Call the method using its name to execute the statements in the method body.