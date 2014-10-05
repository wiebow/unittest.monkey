unittest
========

Unittest module for Monkey. Test your application before implementing it!

Introduction
============

Unit testing allows you to test if a particular piece of code is working correctly.

Details
=======

This module uses reflection to automatically add your tests to the suite. As pioneered by Brucey with maxunit. As the module uses Try/Catch and Exception handling, and the new reflection filter definition, Monkey v66 or up is required.

How to use
==========

Import the unittest module and the files containing the test classes. In this example the file simple_test also contains the test class.

TIP: If you use _test as the last part of each of your unit test file names, you can use *_test as your reflection filter to automatically add each test. Ensure that these test files are in the same folder as the main file.

  Strict

  #REFLECTION_FILTER+="*_test"

  Import wdw.unittest
  Import simple_test

  Function Main:Int()
          Local t:TestSuite = New TestSuite
          t.Run()
          Return 0
  End
  

The next thing to do is to create your test class. The class name must end with Test. In this example the following code is located in the file simple_test, as imported in the main test code above.
You extend the Test class to create your own test class. Each method in the test class ending with Test will be run by the Test Suite. A method ending with Before will be run before each unit test, and the method ending with After will be ran, guess what, after each unit test.

  Strict
  Import myclass

  Class MyClassTest Extends Test  
          Field m:MyClass
        
          Method dothisBefore:Void()
                  'we do this before each unit test
                  m = New MyClass
          End
        
          Method dothisAfter:Void()
                  'we do this after each unit test
                  m = Null
          End     
        
          Method constructorTest:Void()
                  Self.assertNotNull(m, "")
          End     

          'this test will fail, of course.                
          Method constructorFailingTest:Void()
                  Self.assertNull(m, "fail!")
          End     
  End Class

This is the class you want to test. It is located in the file myclass, as imported in the file simple_test.

  Strict
  Class MyClass   
          Private 
          Field simplefield:Int
          Public  
        
          Method Simplefield:Int(i:Int) Property
                  simplefield = i
                  Return 0
          End
        
          Method Simplefield:Int() Property
                  Return simplefield
          End
  End


License
-------------------------------------------------------------------------------

Unittest is licensed under the MIT license:

    Copyright (c) 2010 Wiebo de Wit.

    Permission is hereby granted, free of charge, to any person obtaining a copy
    of this software and associated documentation files (the "Software"), to deal
    in the Software without restriction, including without limitation the rights
    to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
    copies of the Software, and to permit persons to whom the Software is
    furnished to do so, subject to the following conditions:

    The above copyright notice and this permission notice shall be included in
    all copies or substantial portions of the Software.

    THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
    IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
    FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
    AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
    LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
    OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
    THE SOFTWARE.
