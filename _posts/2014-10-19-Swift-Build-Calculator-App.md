---
layout: post
title:  "Swift Programming: Build a calculator app"
subtitle: "Create and maintain a sequential text database in PHP"
date:   2014-10-19 16:20:40
tags:
  - iOS
  - Swift
  - Code
  - Swift programming
categories: iOS
---

I was scouring the web for blogs and videos about programming in Swift I found a couple that were showing how to build a calculator. I decided to build one of my own to help me in my swift discovering journey.

If you need the Xcode project files you can download them <a title="iOS Calculator app raw code" href="https://paini.org/federico/depot/iOSCalcAppCode.zip" target="_blank">here</a>.

##How it works

It's a basic calculator, nothing fancy.  The app performs the usual arithmetic operations plus a series specialized percentage buttons intended to be used as tip calculators. I personally tested it on my iPhone 5 and it works as intended.


![Fig 1a](http://codecoms.com/wp-content/uploads/2014/10/CalculatorInAction-2-162x300.png " Fig 1a - The Calculator in action") &nbsp;
![image](http://codecoms.com/wp-content/uploads/2014/10/CalculatorInAction-1-161x300.png "Fig 1b. The Calculator in action")

I created the following user stories to guide me through the development:
<ol>
	<li>I need to be able to perform the basic arithmetic operations +,-,* and /</li>
	<li>I need to be able to perform operations with non integer numbers</li>
	<li>As a  user every time I hit the = sign the operation is performed and the result is shown on the display</li>
	<li>As a user I need to be able to perform an operation on a result displayed</li>
	<li>I need to be able to clear the screen without clear the memory</li>
	<li>I need to be able to clear the memory</li>
	<li>As a user I need to have specialized "tip" calculator button at 10%, 15%, 18%, and 20%.
<ol>
	<li>When I hit those button the resulting percentage in shown on the screen</li>
	<li>Every percentage needs to perform an independent calculation</li>
</ol>
</li>
</ol>
<p>&nbsp;</p>
<h2>Creating the app in XCode 6</h2>
As in every iOS application we need to start in Xcode 6 as a brand new application:
![Fig.2](http://codecoms.com/wp-content/uploads/2014/10/CreateNewSingleScreenAppXcode-300x173.png "Fig 2. Create the calculator project")

<ol>
	<li>Select a single view application</li>
	<li>In the following screen select "Swift" as a language</li>
	<li>We do not need "core data" so leave it uncheck</li>
	<li>To keep it simple I made the app for iPhone only</li>
</ol>

<h2>The Storyboard</h2>
I kept the calculator's look and feel is very simple (see Fig. 3).
I created all the numbers buttons, the Clear and All Clear buttons, and all the standard arithmetic operations plus additional specialized "tip" buttons.

![Fig.3](http://codecoms.com/wp-content/uploads/2014/10/Calculator-Main_storyboard-162x300.png "Fig 3. Storyboard layout of the calculator")

<ul>
	<li>The digits 0-9 and the decimal (.) are connected to the IBAction "<em>digitTapped</em>"</li>
	<li>The buttons <em>AC</em>  is connected to theIBAction "<em>allClearTapped</em>"</li>
	<li>The buttons <em>C</em>  is connected to the IBAction "c<em>learScreenTapped</em>"</li>
	<li>The operands buttons +, -, x, and / are connected to the IBAction "operation<em>Tapped</em>"</li>
	<li>The buttons with <em>10%, 15%, 18%</em> and<em> 20% </em>are connected to the IBAction <em>"percentage<em>Tapped</em>"</em></li>
	<li>The equal (=) button is connected to the IBAction "equal<em>Tapped</em>"</li>
</ul>

The way I organized the layout is explained in Fig.4  and is as follows:

![Fig.4](http://codecoms.com/wp-content/uploads/2014/10/Calculator-Main_storyboard-Explanation-192x300.png "Fig 4. Calculator layout explanation")

<ul>
	<li>(1) Is the main label which is named <em>answerFieldLabel. </em> The results are displayed here</li>
	<li>(2) This is a hidden label named <em>operandLabel</em> in which keeps track of the operand the user has chosen at any given time (+,-,x, /)</li>
	<li>(3) <em>All Clear</em> and <em>Clear</em> buttons. The <em>AC</em> resets all the variables and arrays, the <em>C</em> only resets the <em>answerFieldLabel</em></li>
	<li>(4) This is the percentage or "tip" button and performs a percentage calculation based on the result saved</li>
	<li>(5) The operations buttons: addition, subtraction, multiplication and division</li>
	<li>(6) The equal button that performs the operations</li>
	<li>(7) The keypad including the decimal dot (.)</li>
</ul>

##The Classes
I create two classes for this project: <em>ArithmeticOperation </em>and<em> <em>tipCalculator.</em></em>

The main class for the Calculator is the <em>ArithmeticOperation</em> class which returns the value of the operation requested. Each operation is a method (addition, subtraction, multiplication and division).

All the methods are pretty straight forward. For the <em>division()</em> method I implemented a failsafe to avoid a division by zero operation.


{% highlight swift %}

ArithmeticOperation  {
    let righNumber: Double
    let leftNumber: Double
    
    init(righNumber: Double, leftNumber: Double) {
        self.righNumber = righNumber
        self.leftNumber = leftNumber
    }
    
    func addition() -&gt; Double {
        result = righNumber + leftNumber
        return result
    }
    
    func subtraction() -&gt; Double {
        return righNumber - leftNumber
    }
    
    func multiplication() -&gt; Double {
        return righNumber * leftNumber
    }
    
    func division() -&gt; Double {
        if leftNumber.isZero == false {
            return righNumber / leftNumber
        } else {
            return 0.0
        }
        
    }
}
{% endhighlight %}


For the percentage or "tip" calculator I created a separate class called <em>tipCalculator </em>class<em> </em>that has a method called <em>calculatedTip()</em>  that returns the percentage chosen.

{% highlight swift %}

let total: Double
    let tipPerc: Double
    
    init(total:Double, tipPerc: Double) {
        self.total = total
        self.tipPerc = tipPerc
    }
    
    func calculatedTip() -&gt; Double {
        return total * tipPerc
        
    }

{% endhighlight %}

You can try out all the classes by cutting and pasting the code in the Xcode playground:

![Fig.3](http://codecoms.com/wp-content/uploads/2014/10/TipCalculator-Playground.png "Testing the TipCalculator Class with the Playground")


##The Code
The four most important functions are <em>digitTapped()</em>,<em>  percentageTapped()</em>, <em>equalTapped()</em>,<em> and operatorTapped(). </em>
I use an array called <em>resultArray</em> to keep track of the result. Also I have two variables <em>rNumber</em> and <em>lNumber</em> with the values of the right and left numbers that are needed for an arithmetic operation as in "<em>rNumber + lNumber = result".</em> The variable "<em>op</em>" represent the arithmetic operand chosen and it's connected to <em>operandLabel</em>. 

{% highlight swift %}

var resultArray: Array = []
var rNumber: NSString = ""
var lNumber: NSString = ""
var op: String = ""
var result: Double = 0.0

{% endhighlight %}

This is the code in the *ViewController.swift* file between the brackets under "*class ViewController: UIViewController*":


{% highlight swift %}

@IBOutlet var operandLabel: UILabel!
    
    @IBAction func allClearTapped(sender: UIButton) {
        answerFieldLabel.text = "0.0"
        operandLabel.text = ""
        resultArray.removeAll()
    }

    @IBAction func clearScreenTapped(sender: AnyObject) {
        answerFieldLabel.text = "0.0"
    }
    
    @IBAction func digitTapped(theDigit: UIButton) {
        var digit = theDigit.titleLabel?.text
        if answerFieldLabel.text == "" || answerFieldLabel.text == "0.0" 
        || answerFieldLabel.text == "0.00"
        {
            answerFieldLabel.text = digit
        } else {
            answerFieldLabel.text = answerFieldLabel.text! + digit!
        }
    }
    
    @IBAction func percentageTapped(tipButton: UIButton) {
        var tipDefault: Dictionary = ["10%": 0.1, "15%": 0.15, "18%": 0.18, "20%": 0.2]
        var tip: Double = 0.0
        var numberInScreen: NSString = answerFieldLabel.text!
        
        for (key, value) in tipDefault {
            if tipButton.titleLabel?.text == key {
                tip = value
            }
        }

        resultArray.append(numberInScreen.doubleValue)
        var result = tipCalculator(total: resultArray[0].doubleValue, tipPerc: tip)
        var totalTip = result.calculatedTip()
        answerFieldLabel.text = String(format:"%.02f", totalTip)

    }
    
    @IBAction func equalTapped(sender: AnyObject?) {

        var rightNum: Double
        var leftNum: Double
        var lNumber: NSString = ""
        
        rightNum = rNumber.doubleValue
        lNumber = answerFieldLabel.text! as NSString //Necessary to convert to Double
        leftNum = lNumber.doubleValue
        
        var answer = ArithmeticOperation(righNumber: rightNum, leftNumber: leftNum)
        if op == "+" {
            answerFieldLabel.text = String(format:"%.02f", answer.addition())
            operandLabel.text = ""
        } else if op == "-" {
            answerFieldLabel.text = String(format:"%.02f", answer.subtraction())
            operandLabel.text = ""
        } else if op == "x" {
            answerFieldLabel.text = String(format:"%.02f", answer.multiplication())
            operandLabel.text = ""
        } else if op == "/" {
            answerFieldLabel.text = String(format:"%.02f", answer.division())
            operandLabel.text = ""
        }else {
            answerFieldLabel.text = "Operation Error!"
        }
    }
    
    @IBAction func operationTapped(sender: UIButton) {
        
        if operandLabel.text == "" {
            rNumber = answerFieldLabel.text!
            operandLabel.text = sender.titleLabel?.text
            op = operandLabel.text!
            answerFieldLabel.text = "0.0"
        } else {
            answerFieldLabel.text = "0.0"
            equalTapped(nil)            
        }
        
    }

{% endhighlight %}

<p>&nbsp;</p>
{% include twitter_plug.html %}
